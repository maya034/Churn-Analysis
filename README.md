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




Communication - Clear and Timely Communication/Feedback:
Throughout the project, I consistently maintained transparent and timely communication with both team members and the manager. This ensured that all stakeholders were well-informed about project progress and any relevant updates.

Performance - Timeliness, Quality, Documentation:
Regarding the internal project, I conducted comprehensive research on various competitors in the wildfire domain and explored diverse methodologies. A detailed document was meticulously compiled, encompassing information on all approaches undertaken. This documentation facilitated a comprehensive presentation to the client, outlining our strategies. Additionally, we initiated the development of a streamlined pipeline, optimizing and automating our existing codebase to enhance efficiency.



I always follow the rules and guidelines set by the company, ensuring compliance with our code of conduct and established policies. For example, in recent projects, I made sure to strictly follow our procedures, which resulted in [mention a positive outcome or achievement]. I also stay updated on client-specific requirements, helping us maintain strong client relationships. Additionally, I consistently meet submission deadlines on I Expense, emphasizing accuracy and timeliness. My commitment to compliance is a daily practice, contributing to our team's success. Looking ahead, I'm eager to continue upholding these standards and contributing to our culture of excellence


I consistently prioritize and adhere to all aspects of compliance, including the company-wide code of conduct, established procedures, and policies. In doing so, I actively contribute to a work environment that aligns with our organizational values and ethical standards. For instance, during [specific project or initiative], I ensured strict adherence to our established procedures by [provide a specific example or achievement]. Additionally, my proactive approach to staying updated on any changes in client-specific requirements has been instrumental in maintaining strong client relationships. Furthermore, I have consistently met or exceeded timelines for submissions on I Expense, showcasing my dedication to timeliness and accuracy in financial processes.

This commitment to compliance is not just a checkbox for me; it is ingrained in my daily work, contributing to the overall success of our team and the organization. Moving forward, I am eager to continue championing a culture of compliance and excellence, ensuring that our practices align seamlessly with industry standards and regulations."


Certainly! Let's enhance your comment to provide more context and detail:

"I have consistently supported our organization in various capacities, particularly in the areas of training, recruitment, onboarding, and transitions. For instance, I played a pivotal role in assisting a team with a Python automation requirement, showcasing my dedication to enhancing our technological capabilities and streamlining processes. Additionally, I actively contributed to the onboarding process by serving as a buddy, ensuring new team members felt welcomed and had the necessary support to integrate seamlessly into the team.

Moreover, I have been actively involved in sharing knowledge and insights with my team members, providing regular updates on my work and offering assistance when needed. In alignment with EXL initiatives, I have prepared training materials and case studies to contribute to our continuous learning culture.

My commitment to supporting the team extends beyond individual contributions, as I believe in fostering a collaborative and supportive work environment. Moving forward, I remain dedicated to playing a key role in the success of our training, recruitment, and onboarding initiatives, and I am enthusiastic about contributing to the broader EXL initiatives that drive our organizational growth."


I have successfully completed all required training sessions and actively participated in knowledge transfer sessions, sharing insights and experiences with my teammates. In order to stay current and facilitate my continuous growth, I expanded my skill set by acquiring knowledge in new technologies such as MongoDB, modular programming, and time series approaches in machine learning. Additionally, I am currently undertaking learning initiatives in data engineering from another platform, aiming to deepen my understanding of cloud technologies and pipelines. My commitment to ongoing learning reflects my dedication to professional development and staying at the forefront of industry advancements.
 	
