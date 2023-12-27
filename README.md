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











Category	Overall Weightage	Sub-Category 	Goals	 	
			Goal Name (Target to be defined for each Goal)	Guidelines	Actual Weightage	 	
Financial	50%	Revenue	Project Performance and overall utilization	Communication - Clear and timely communication/feedback
Performance - Timeliness, Quality, Documentation
Customer Satisfaction (based on client feedback) and optimum utilization
Optimization and automation*	40%	 	
 	 	Compliance	Compliance	Compliance: - relating to company wide code of conduct, procedures and policies, client specific requirements, timelines and accuracy of submissions on I Expense etc.	10%	 	
Strategic	30%	Strategic Initiatives	EXL Initiatives	1. Support with training, recruitment, onboarding (buddy), transitions.
2. Support EXL initiatives by preparing training material, case studies	30%	 	
People	20%	Development and Capability building	Self-development	- trainings attended
- Knowledge transfer sessions
- Technical and Behavioral skills
- Completing certifications/working towards actuarial exams/associateship/fellowship	20%	 	
