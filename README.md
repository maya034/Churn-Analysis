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







Throughout the research period, I have successfully completed all mandatory training and actively participated in knowledge transfer to share insights and experiences with teams of colleagues. To keep up with industry trends, I expanded my skill set, moving into technologies like MongoDB, modular programming, and time management methods for learning. Additionally, I am currently involved in academic programs focused on data technology, aiming to enhance my understanding of cloud technologies and pipelines.

In contributing to the organization, I played a key role in supporting a team with Python automation needs and actively supported knowledge sharing initiatives. This includes regularly updating my work, preparing project documentation in line with EXL policies, and promoting a collaborative working environment My commitment to continuing education and support extends to beyond individual contributions, as I look forward to contributing to EXL’s broader strategy for organizational growth.

While demonstrating a strong commitment to compliance, I always prioritize and uphold all aspects of the established company-wide Code of Conduct, policies and procedures. This commitment strongly contributes to maintaining a work environment that is consistent with our organizational values ​​and ethical standards. Looking ahead, I am excited to uphold these values ​​and contribute to our excellent culture.

In terms of communication, I maintained transparent and timely communication across projects, ensuring that the team and senior management were well aware of project progress. As for project performance, I thoroughly researched various competitors in the wildland fire industry, exploring different strategies




Throughout the appraisal period, I have prioritized continuous learning, completing all required training sessions and expanding my skill set in technologies such as MongoDB and machine learning. My current engagement in data engineering learning initiatives underscores my commitment to staying at the forefront of industry advancements. I consistently supported the organization by aiding a team with a Python automation requirement, actively contributing to knowledge-sharing initiatives, and aligning with EXL initiatives by preparing project documentation. My commitment extends beyond individual contributions, aiming to contribute to broader organizational growth. Upholding compliance, including the code of conduct and policies, is integral to my daily work, contributing to a work environment aligned with organizational values. Looking forward, I am enthusiastic about upholding these standards and contributing to our culture of excellence. In terms of communication, I ensured transparent and timely communication throughout projects, while my contributions to project performance included comprehensive research, documentation, and the initiation of streamlined processes for enhanced efficiency.





1. Please provide feedback on how your manager has supported you throughout the year.
1. Please provide feedback on how your manager has supported you throughout the year.
*		2. Has your manager provided you developmental inputs to help you perform better?
2. Has your manager provided you developmental inputs to help you perform better?
*		3. Does your manager demonstrate EXL values/The Better Way Code effectively?
3. Does your manager demonstrate EXL values/The Better Way Code effectively?
*		4. What do you want your manager to (Please share 1-2 bullet points each)
a. Start
b. Stop
c. Continue




Since i have joined exl, my managers had been kept on changing from anubhav patra to namit chopra and then to visheshtha khanna and at last my current mananger is saurab. However, after a few months when i was moved to internal project i was completely working in nishant jairath’s team. Though in record he is not my manager. I was working under his supervision in his team. We had regular team meetings to foster open communication and also discuss about the problems and approaches to enhance collaboration and ensure diverse perspectives. These regular team meetings helped in comprehensive decisions and improved overall output. He also helped me to address other problems that i faced apart from the project. Also, the constructive feedbacks provided on my work really helped me to work effectively.




Certainly! Here are some suggestions for each category:

**Start:**
- Implement regular one-on-one meetings to discuss career development and goals, fostering a more personalized and supportive relationship.
- Initiate a mentorship program within the team to promote knowledge sharing and professional growth.

**Stop:**
- Cease micro-managing tasks to allow for more autonomy and creativity within the team.
- Stop last-minute changes in project priorities to enhance workflow consistency and efficiency.

**Continue:**
- Continue providing constructive feedback on performance to facilitate ongoing improvement.
- Maintain the practice of recognizing and appreciating team achievements to boost morale and motivation.
