# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 



PROPERTY ATTRIBUTES
Property attributes are basically essential features of a property that has been used to calculate the risk factor and risk score of any specific property or building. There are two types of attributes that had been considered-

Primary attributes contribute 75% and secondary attributes contribute 25% in the total calculation of risk score.

Primary attributes

Occupancy
                      15%
Construction
                      45%
Yearbuilt
                      10%
No of building
                        5%
Floor area/square foot area
                      15%
Stories
                      10%


Secondary attributes

Roof_Type_RF/geometry
                    5%
Roof_Condition_RF

10%
Roof_Material_RF
Pool_Enclosure_PA
5%
DIS_Firestation_BU
10%
Chimneys_RF

5%
Roof_Evidence_RF


Solar_Panels_RF
5%
Air_Conditioner_RF
5%
Skylights_RF
5%




Tree_Overhang_RF
10%
DIS_ClosestBuilding_BU
10%
DIS_Trees_BU
10%




Pool_AR_PA


Temporary_pool_PA


Trampoline_PA


Yard_Debris_PA
10%
DIS_WaterBody_BU
10%














from uszipcode import SearchEngine
import pandas as pd

# Sample DataFrame 'df' with 'state_name' and 'city_name' columns
data = {'state_name': ['California', 'New York', 'Texas'],
        'city_name': ['Los Angeles', 'New York City', 'Houston']}
df = pd.DataFrame(data)

# Create a search engine instance
search = SearchEngine(simple_zipcode=True)

def get_county(row):
    state = row['state_name']
    city = row['city_name']
    
    # Use the search engine to find the county based on state and city
    result = search.by_city_and_state(city, state)
    
    # Extract the county information
    if result:
        county = result[0].county
    else:
        county = 'Unknown'
    
    return county

# Apply the function to add a 'county' column to the DataFrame
df['county'] = df.apply(get_county, axis=1)

# Print the updated DataFrame
print(df)
Attribute
Assumption
Occupancy
As the data provided to us did not have this attribute, therefore by default we have assumed it as 1.
Construction
As the data provided to us did not have this attribute, therefore by default we have assumed it as 1.
Yearbuilt
As the data provided to us did not have this attribute, therefore by default we have assumed it as 1.
No of building
As the data provided to us did not have this attribute, therefore by default we have assumed it as 1.
Floor area/square foot area
Risk Bucket :
(1-2000)= 85%
(2001-4000)= 90%
(4001-6000)= 95%
(6001+)= 100%
Stories
number of floors <=3 : 80%
<=6 : 90%
>=7 : 100%




Roof_Type_RF/geometry
Hip : 40%
Mix : 60%
Flat : 80%
Gable : 100%
Roof_Condition_RF
Bad : 100%
Damaged : 85%
Fair : 60%
Good : 30%
Roof_Material_RF
Concrete : 20%
Metal : 20%
Shingle : 100%
Tile : 80%
For roof condition and roof material, this is the risk bucket calculated. However we have combined both to calculate the combined risk as a weighted average of the percentage
in the following manner:
Weight material = 0.7 i.e. 70% weight for roof material
Weight condition= 0.3 i.e. 30% weight for roof condition






DIS_Firestation_BU
Distance <=0.2 miles : 60%
>0.2 but <=0.5 miles : 80%
>0.5 miles : 100%
Chimneys_RF
If yes = 100% or else 1%
Air_Conditioner_RF
(1-2) = 70%
(3-5) = 85%
(6-8) = 90%
(9+) = 100%
Skylights_RF
Count 0 : 1%
=>1 but <=3 : 80%
=>4 but <=6 : 85%
=>7 but <=10 : 95%
>10 or else : 100%




Tree_Overhang_RF
Category 0 : 1%
1 : 60%
2 : 75%
3 : 90%
4 : 100%
DIS_ClosestBuilding_BU
Distance <= 65.62 (20m) : 90%
>65.62 but <= 164.04 (50m) : 70%
>164.04 but <=328.08 (100m) : 50%
else : 20%
DIS_Trees_BU
Distance <= 164.04 (50m) : 100%
>164.04 but <= 328.08 : 80%
>328.08 but <=492.13 : 50%
else : 20%




Pool_AR_PA
Distance <= 500 ft : 80%
>500 ft but <=1000 ft : 70%
> 1000 ft : 60%
Temporary_pool_PA
Distance <= 500 ft : 80%
>500 ft but <=1000 ft : 70%
> 1000 ft : 60%


Here risk bucket for pool area and temporary pool area has been calculated and then combined together to calculate the combined risk as a weighted average of the percentage as-
weight pool: 0.8 i.e. 80% weight for pool area
weight temporary pool area: 0.2 i.e. 20% weight for temporary pool def get_county(state_name, city_name):
    location = geolocator.geocode(f"{city_name}, {state_name}", exactly_one=True)
    
    if location:
        address = location.raw
        county = address.get("address", {}).get("county", "Unknown")
    else:
        county = "Unknown"
    
    return county




GeocoderUnavailable: HTTPSConnectionPool(host='nominatim.openstreetmap.org', port=443): Max retries exceeded with url: /search?q=PEARL+RIVER%2C+Louisiana&format=json&limit=1 (Caused by SSLError(SSLCertVerificationError(1, '[SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: self signed certificate in certificate chain (_ssl.c:1129)')))



from geopy.geocoders import Nominatim
import requests

# Create a geocoder instance using Nominatim
geolocator = Nominatim(user_agent="myGeocoder")

# Define a function to get the county information based on state and city
def get_county(state_name, city_name):
    url = f"https://nominatim.openstreetmap.org/search?q={city_name}, {state_name}&format=json&limit=1"
    
    try:
        response = requests.get(url, verify=False)  # Disable SSL certificate verification
        data = response.json()
        
        if data:
            county = data[0].get("address", {}).get("county", "Unknown")
        else:
            county = "Unknown"
    
    except Exception as e:
        print(f"Error: {e}")
        county = "Unknown"
    
    return county

# Use the function to find the county for a specific state and city
state = "Louisiana"
city = "Pearl River"
county = get_county(state, city)
print(f"The county for {city}, {state} is {county}")








Yard_Debris_PA
Distance <= 5 : 100%
>5 but <=30 : 90%
>30 but <=100 : 70%
else : 20%
DIS_WaterBody_BU
Distance <= 0.2 miles : 60%
>0.2 but <=0.5 miles : 80%
> 0.5 miles : 100%
DIS_Coast_BU
Distance <= 500 ft : 80%
>500 ft but <=2000 ft : 40%
> 2000 ft : 1%


