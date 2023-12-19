![image](https://github.com/maya034/Churn-Analysis/assets/61015843/4747de26-fb67-4dc6-92ee-ebfc5f3aa0ac)# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 





import folium
from folium.plugins import MarkerCluster
from geopy.geocoders import Nominatim

# Sample 1000 random rows from the dataframe
sample_data = df.sample(n=1000)

# Create a base map
map_center = [sample_data['LATITUDE'].mean(), sample_data['LONGITUDE'].mean()]
m = folium.Map(location=map_center, zoom_start=4)

# Plot each wildfire incident on the map
for index, row in sample_data.iterrows():
    folium.CircleMarker(
        location=[row['LATITUDE'], row['LONGITUDE']],
        radius=5,
        color='red',
        fill=True,
        fill_color='red',
        fill_opacity=0.7,
        popup=f"Fire Name: {row['FIRE_NAME']}, Date: {row['DISCOVERY_DATE']}, Size: {row['FIRE_SIZE']} acres"
    ).add_to(m)

# Add a marker for the specified address
address = "650 KLEBBA LN, MIAMI, FL 33133"
geolocator = Nominatim(user_agent="my_geocoder")
location = geolocator.geocode(address)

if location:
    folium.Marker(
        location=[location.latitude, location.longitude],
        popup=f"Address: {address}",
        icon=folium.Icon(color='green')
    ).add_to(m)

# Save the map to an HTML file
m.save('wildfire_map_with_address.html')


from IPython.display import IFrame

# Replace 'wildfire_map_with_address.html' with the actual file path
iframe = IFrame(src='wildfire_map_with_address.html', width=700, height=600)
display(iframe)

