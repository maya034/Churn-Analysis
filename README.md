![image](https://github.com/maya034/Churn-Analysis/assets/61015843/4747de26-fb67-4dc6-92ee-ebfc5f3aa0ac)# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 



import folium
from folium.plugins import MarkerCluster, HeatMap
from geopy.geocoders import Nominatim
from math import radians, sin, cos, sqrt, atan2
from IPython.display import IFrame

# Function to calculate distance between two sets of coordinates (in kilometers)
def calculate_distance(lat1, lon1, lat2, lon2):
    # Radius of the Earth in kilometers
    R = 6371.0

    # Convert latitude and longitude from degrees to radians
    lat1, lon1, lat2, lon2 = map(radians, [lat1, lon1, lat2, lon2])

    # Calculate the change in coordinates
    dlat = lat2 - lat1
    dlon = lon2 - lon1

    # Haversine formula to calculate distance
    a = sin(dlat / 2)**2 + cos(lat1) * cos(lat2) * sin(dlon / 2)**2
    c = 2 * atan2(sqrt(a), sqrt(1 - a))

    # Distance in kilometers
    distance = R * c
    return distance

# Use the entire dataframe
sample_data = df1

# Address to be marked on the map
address = "650 KLEBBA LN, MIAMI, FL 33133"

# Get coordinates for the address
geolocator = Nominatim(user_agent="my_geocoder")
location = geolocator.geocode(address)

if location:
    address_lat, address_lon = location.latitude, location.longitude

    # Create a base map centered around the specified address
    m = folium.Map(location=[address_lat, address_lon], zoom_start=10)

    # Create MarkerCluster for the address
    marker_cluster = MarkerCluster().add_to(m)

    # Add a marker for the specified address
    folium.Marker(
        location=[address_lat, address_lon],
        popup=f"Address: {address}",
        icon=folium.Icon(color='green')
    ).add_to(marker_cluster)

    # Filter data points within 50 km from the address
    filtered_data = sample_data[
        sample_data.apply(lambda row: calculate_distance(row['LATITUDE'], row['LONGITUDE'], address_lat, address_lon) <= 50, axis=1)
    ]

    # Create a heatmap based on fire size with a custom color gradient
    heat_data = [[row['LATITUDE'], row['LONGITUDE'], row['FIRE_SIZE']] for index, row in filtered_data.iterrows()]
    HeatMap(heat_data, radius=15, blur=10, gradient={0.4: 'yellow', 0.65: 'orange', 1: 'red'}).add_to(m)

    # Save the map to an HTML file
    m.save('wildfire_heatmap_custom_colors.html')


# Display the map in the notebook
iframe = IFrame(src='wildfire_heatmap_custom_colors.html', width=700, height=600)
display(iframe)






from pymongo import MongoClient
import json

# Connect to the MongoDB server running on your localhost
client = MongoClient('localhost', 27017)

# Create or access a database
db = client['your_database_name']

# Access the collection you want to check
collection1 = db['collection1']

# Find all documents in the collection
cursor = collection1.find({})

# Iterate over the cursor to check each document
for idx, document in enumerate(cursor):
    try:
        # Attempt to parse the document as JSON
        parsed_json = json.loads(json.dumps(document, default=str))
        print(f"Document {idx + 1} is valid JSON.")
    except json.JSONDecodeError as e:
        print(f"Error in document {idx + 1}: {e}")
        print("Invalid JSON document:")
        print(document)









