image# Telecom-Churn-Analysis Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention. Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). 


















1539 High St, Fort Myers, FL, USA
Lat Long
(26.649090, -81.852070)


GPS Coordinates
26° 38' 56.724'' N
81° 51' 7.452'' W















import pandas as pd
import geopandas as gpd
import matplotlib.pyplot as plt
import cartopy.crs as ccrs
import geopandas as gpd
import folium
import math
from shapely.geometry import Point
from folium.plugins import AntPath
import cartopy.feature as cfeature
import time
import multiprocessing


def plot_us_hemisphere_map(latitudes, longitudes):
    # Create a GeoDataFrame from the DataFrame
    data = {"Latitude": latitudes, "Longitude": longitudes}
    df = pd.DataFrame(data)
    geometry = [Point(lon, lat) for lat, lon in zip(df["Latitude"], df["Longitude"])]
    gdf = gpd.GeoDataFrame(
        df, geometry=geometry, crs="EPSG:4326"
    )  # Use WGS84 CRS (EPSG:4326)

    # Create a world map centered around the US
    fig, ax = plt.subplots(subplot_kw={"projection": ccrs.PlateCarree()})

    # Set the extent to cover the US and surrounding ocean
    ax.set_extent(
        [-180, -65, 0, 75], crs=ccrs.PlateCarree()
    )  # Adjust these values as needed

    # Add coastlines and borders
    ax.add_feature(cfeature.COASTLINE, linewidth=0.5)
    ax.add_feature(cfeature.BORDERS, linestyle="--")

    # Plot the hurricane path GeoDataFrame
    gdf.plot(ax=ax, marker="o", markersize=5, color="red", label="Hurricane Path")

    # Add a title
    ax.set_title("US Hemisphere Map")

    return plt


def plot_map_1(latitudes, longitudes, house_lat, house_long):
    start_time = time.time()
    # import pdb
    # pdb.set_trace()

    # Create a map centered around the house location
    property_map = folium.Map(location=[house_lat, house_long], zoom_start=5)

    # Add a marker for the house
    folium.Marker([house_lat, house_long], popup="Your House").add_to(property_map)

    # Define a list of colors for the hurricane paths
    colors = [
        "red",
        "blue",
        "green",
        "purple",
        "orange",
        "pink",
        "brown",
    ]  # You can add more colors as needed

    # for i in range(len(latitudes)):
    #     # Create a line to represent the hurricane path with a specific color
    #     hurricane_path = list(zip(latitudes[i], longitudes[i]))
    #     color = colors[i % len(colors)]  # Cycle through colors for different paths
    #     folium.PolyLine(locations=hurricane_path, color=color, weight=2, opacity=1).add_to(property_map)
    #     # Add arrows to indicate the direction of the hurricane
    #     for j in range(1, len(latitudes[i])):
    #         start_point = (latitudes[i][j - 1], longitudes[i][j - 1])
    #         end_point = (latitudes[i][j], longitudes[i][j])
    #         angle = math.degrees(math.atan2(end_point[1] - start_point[1], end_point[0] - start_point[0]))
    #         folium.RegularPolygonMarker(location=start_point, fill_color=color, number_of_sides=3,
    #                                    rotation_angle=angle, radius=6).add_to(property_map)

    for i in range(len(latitudes)):
        # Create a line to represent the hurricane path
        hurricane_path = list(zip(latitudes[i], longitudes[i]))
        color = colors[i % len(colors)]  # Cycle through colors for different paths
        folium.PolyLine(
            locations=hurricane_path, color=color, weight=2, opacity=1
        ).add_to(property_map)
        # Add a big dot marker for the hurricane's origination (eye)
        arrow = AntPath(
            locations=hurricane_path, dash_array=[10, 20], delay=800, color=color
        )  # # Add arrows to indicate the direction of the hurricane
        arrow.add_to(property_map)
        folium.CircleMarker(
            location=(latitudes[i][0], longitudes[i][0]),
            radius=8,
            color=color,
            fill=True,
            fill_color=color,
            fill_opacity=1,
            popup="Hurricane Eye",
        ).add_to(property_map)

        # for j in range(1, len(latitudes[i])):
        #     start_point = (latitudes[i][j - 1], longitudes[i][j - 1])
        #     end_point = (latitudes[i][j], longitudes[i][j])
        #     arrow_color = color
        #     folium.PolyLine([start_point, end_point], color=arrow_color, weight=2, opacity=1).add_to(property_map)

    # Save the map to an HTML file or display it
    property_map.save("hurricane_map.jpeg")  # You can change the filename if needed
    end_time = time.time()
    print(f"Elapsed Time seconds:", (end_time - start_time))


def plot_map_multiprocessing(
    latitudes, longitudes, house_lat, house_long, intersection_times
):
    def create_hurricane_path(
        property_map, latitudes, longitudes, color, intersection_times
    ):
        hurricane_path = list(zip(latitudes, longitudes))
        folium.PolyLine(
            locations=hurricane_path, color=color, weight=2, opacity=1
        ).add_to(property_map)
        popup_text = f"Intersection Time: {time}"
        popup = folium.Popup(popup_text, max_width=300)
        arrow = AntPath(
            locations=hurricane_path,
            dash_array=[10, 20],
            delay=800,
            color=color,
            popup=popup,
        )
        arrow.add_to(property_map)
        folium.CircleMarker(
            location=(latitudes[0], longitudes[0]),
            radius=8,
            color=color,
            fill=True,
            fill_color=color,
            fill_opacity=1,
            popup="Hurricane Eye",
        ).add_to(property_map)

    start_time = time.time()

    property_map = folium.Map(location=[house_lat, house_long], zoom_start=5)
    folium.Marker([house_lat, house_long], popup="Your House").add_to(property_map)

    colors = ["red", "blue", "green", "purple", "orange", "pink", "brown"]

    pool = multiprocessing.Pool(processes=multiprocessing.cpu_count())
    for i in range(len(latitudes)):
        color = colors[i % len(colors)]
        pool.apply_async(
            create_hurricane_path,
            (property_map, latitudes[i], longitudes[i], color, intersection_times[i]),
        )

    pool.close()
    pool.join()
    property_map.save("hurricane_map.html")
    end_time = time.time()
    print(f"Elapsed Time seconds:", (end_time - start_time))


def plot_map(
    latitudes,
    longitudes,
    house_lat,
    house_long,
    hurricane_names,
    intersection_times,
    intersection_distances,
):
    start_time = time.time()

    property_map = folium.Map(location=[house_lat, house_long], zoom_start=5)
    folium.Marker([house_lat, house_long], popup="Your House").add_to(property_map)

    colors = ["red", "blue", "green", "purple", "orange", "pink", "brown"]

    legend_html = """
    <div style="position:fixed; bottom:10px; right:10px; z-index:1000; background:white; border:2px solid grey; padding:5px;">
    <h4>Intersection Times and Distances</h4>
    <table style="width:100%">
    <tr>
    <th>Color</th>
    <th>Name</th>
    <th>Intersection Time</th>
    <th>Intersection Distance</th>
    </tr>
    """

    for i in range(len(latitudes)):
        color = colors[i % len(colors)]
        hurricane_path = list(zip(latitudes[i], longitudes[i]))

        # Round off the intersection time to two decimal places
        intersection_distance_rounded = round(intersection_distances[i], 2)

        # Create a custom popup that includes the rounded intersection time
        popup_text = f"Intersection Time: {intersection_times[i].date()}<br>Intersection Distance: {intersection_distance_rounded}"
        popup = folium.Popup(popup_text, max_width=300)

        # Add the AntPath with the customized popup
        ant_path = AntPath(
            locations=hurricane_path,
            dash_array=[10, 20],
            delay=800,
            color=color,
            popup=popup,
        )
        ant_path.add_to(property_map)

        # Add a big dot marker for the hurricane's origination (eye)
        folium.CircleMarker(
            location=(latitudes[i][0], longitudes[i][0]),
            radius=8,
            color=color,
            fill=True,
            fill_color=color,
            fill_opacity=1,
            popup="Hurricane Eye",
        ).add_to(property_map)

        # Update the legend with the color, hurricane name, rounded intersection time, and intersection distance
        legend_html += f'<tr><td><span style="color: {color}; font-weight: bold;">&#9679;</span></td><td>{hurricane_names[i]}</td><td>{intersection_times[i].date()}</td><td>{intersection_distance_rounded}</td></tr>'
        # break

    legend_html += "</table></div>"
    # Convert the legend to an HTML element and add it to the map
    property_map.get_root().html.add_child(folium.Element(legend_html))
    end_time = time.time()
    print(f"Elapsed Time seconds:", (end_time - start_time))
    return property_map

