# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 


Thank you for providing the abstract of the paper. Based on the abstract, I can provide a more detailed breakdown of the key concepts and methodologies discussed in the paper:

https://openacttexts.github.io/LDACourse1/index.html#why-loss-data-analytics

import pandas as pd

# Read the Excel file
file_path = 'your_excel_file.xlsx'  # Update with your file path
df = pd.read_excel(file_path)

# Define your initial buckets and corresponding mapped values
initial_buckets = [(0, 500), (501, 525), (526, 550), (551, 575), (576, 600),
                   # ... Add more initial buckets here ...
                   (2976, 3000)]

# Define your extended buckets and corresponding mapped values
extended_buckets = [(3001, 3200), (3201, 3400), (3401, 3600),
                    # ... Add more extended buckets here ...
                    (15601, 15800)]

# Create a mapping dictionary for initial buckets
initial_mapping = {i: 0.959 - (i * 0.0022) for i in range(len(initial_buckets))}

# Create a mapping dictionary for extended buckets
extended_mapping = {i + len(initial_buckets): value for i, value in enumerate([
    1.1244, 1.1336, 1.1428, 1.1520, 1.1612, 1.1704, 1.1796, 1.1888, 1.1980, 1.2072,
    1.2159, 1.2246, 1.2333, 1.2420, 1.2507, 1.2594, 1.2681, 1.2768, 1.2855, 1.2942,
    1.3029, 1.3116, 1.3203, 1.3290, 1.3377, 1.3464, 1.3551, 1.3618, 1.3685, 1.3752,
    1.3819, 1.3886, 1.3953, 1.4020, 1.4087, 1.4154, 1.4221, 1.4288, 1.4355, 1.4422,
    1.4489, 1.4556, 1.4623, 1.4690, 1.4757, 1.4824, 1.4891, 1.4958, 1.5025, 1.5092,
    1.5159, 1.5226, 1.5293, 1.5360, 1.5427, 1.5494, 1.5561, 1.5628, 1.5695, 1.5762,
    1.5829, 1.5896, 1.5908, 1.5920])}

# Function to map values based on initial buckets
def map_initial_square_footage(value):
    for i, (lower, upper) in enumerate(initial_buckets):
        if lower <= value <= upper:
            return initial_mapping[i]

# Function to map values based on extended buckets
def map_extended_square_footage(value):
    # Calculate the index for the extended buckets based on the value
    index = (value - 3000) // 200 + len(initial_buckets)

    if len(initial_buckets) <= index < len(initial_buckets) + len(extended_mapping):
        return extended_mapping[index]

    return None

# Apply the mapping functions to the 'Square_Footage' column
df['Mapped_Value'] = df['Square_Footage'].apply(
    lambda x: map_initial_square_footage(x) if x <= 3000 else map_extended_square_footage(x)
)

# Save the updated DataFrame back to the Excel file
df.to_excel(file_path, index=False)

----------------------------------------------------------------------------------------------------------------------
import pandas as pd

# Read the Excel file
file_path = 'your_excel_file.xlsx'  # Update with your file path
df = pd.read_excel(file_path)

# Define your initial buckets and corresponding mapped values
initial_buckets = [(0, 500), (501, 525), (526, 550), (551, 575), (576, 600),
                   # ... Add more initial buckets here ...
                   (2976, 3000)]

# Mapping values for initial buckets
initial_mapping_values = [
    0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959,
    0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959,
    0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959,
    0.959, 0.9612, 0.9634, 0.9656, 0.9678, 0.9700, 0.9722, 0.9744, 0.9766,
    0.9788, 0.9810, 0.9832, 0.9854, 0.9876, 0.9898, 0.9920, 0.9942, 0.9964,
    0.9986, 1.0008, 1.0030, 1.0052, 1.0074, 1.0096, 1.0118, 1.0140, 1.0162,
    1.0184, 1.0206, 1.0228, 1.0250, 1.0272, 1.0294, 1.0316, 1.0338, 1.0360,
    1.0382, 1.0404, 1.0426, 1.0448, 1.0470, 1.0492, 1.0514, 1.0536, 1.0558,
    1.0580, 1.0602, 1.0624, 1.0646, 1.0668, 1.0690, 1.0712, 1.0734, 1.0756,
    1.0778, 1.0800, 1.0822, 1.0844, 1.0866, 1.0888, 1.0910, 1.0932, 1.0954,
    1.0976, 1.0998, 1.1020, 1.1042, 1.1064, 1.1086, 1.1108, 1.1130, 1.1152,
    # Add more values here
]

# Create a mapping dictionary for initial buckets
initial_mapping = {i: initial_mapping_values[i] for i in range(len(initial_buckets))}

# Function to map values based on initial buckets
def map_initial_square_footage(value):
    for i, (lower, upper) in enumerate(initial_buckets):
        if lower <= value <= upper:
            return initial_mapping[i]

# Function to map values based on extended buckets
def map_extended_square_footage(value):
    # Calculate the index for the extended buckets based on the value
    index = (value - 3000) // 200 + len(initial_buckets)

    # ... Continue with the extended_mapping as before ...

# Create a new column for the mapped values
df['Mapped_Value'] = df['Square_Footage'].apply(
    lambda x: map_initial_square_footage(x) if x <= 3000 else map_extended_square_footage(x)
)

# Save the updated DataFrame back to the Excel file
df.to_excel(file_path, index=False)





==================================================================================================================
import pandas as pd

# Sample data
data = {'Square_Footage': [450, 510, 535, 3020, 3250, 15500]}
df = pd.DataFrame(data)

# Define your initial buckets and corresponding mapped values
initial_buckets = [(0, 500), (501, 525), (526, 550), (551, 575), (576, 600),
                   (601, 625), (626, 650), (651, 675), (676, 700), (701, 725),
                   (726, 750), (751, 775), (776, 800), (801, 825), (826, 850),
                   (851, 875), (876, 900), (901, 925), (926, 950), (951, 975),
                   (976, 1000), (1001, 1025), (1026, 1050), (1051, 1075), (1076, 1100),
                   (1101, 1125), (1126, 1150), (1151, 1175), (1176, 1200), (1201, 1225),
                   (1226, 1250), (1251, 1275), (1276, 1300), (1301, 1325), (1326, 1350),
                   (1351, 1375), (1376, 1400), (1401, 1425), (1426, 1450), (1451, 1475),
                   (1476, 1500), (1501, 1525), (1526, 1550), (1551, 1575), (1576, 1600),
                   (1601, 1625), (1626, 1650), (1651, 1675), (1676, 1700), (1701, 1725),
                   (1726, 1750), (1751, 1775), (1776, 1800), (1801, 1825), (1826, 1850),
                   (1851, 1875), (1876, 1900), (1901, 1925), (1926, 1950), (1951, 1975),
                   (1976, 2000), (2001, 2025), (2026, 2050), (2051, 2075), (2076, 2100),
                   (2101, 2125), (2126, 2150), (2151, 2175), (2176, 2200), (2201, 2225),
                   (2226, 2250), (2251, 2275), (2276, 2300), (2301, 2325), (2326, 2350),
                   (2351, 2375), (2376, 2400), (2401, 2425), (2426, 2450), (2451, 2475),
                   (2476, 2500), (2501, 2525), (2526, 2550), (2551, 2575), (2576, 2600),
                   (2601, 2625), (2626, 2650), (2651, 2675), (2676, 2700), (2701, 2725),
                   (2726, 2750), (2751, 2775), (2776, 2800), (2801, 2825), (2826, 2850),
                   (2851, 2875), (2876, 2900), (2901, 2925), (2926, 2950), (2951, 2975),
                   (2976, 3000)]

# Define your extended buckets and corresponding mapped values
extended_buckets = [(3001, 3200), (3201, 3400), (3401, 3600),
                    (3601, 3800), (3801, 4000), (4001, 4200),
                    (4201, 4400), (4401, 4600), (4601, 4800),
                    (4801, 5000), (5001, 5200), (5201, 5400),
                    (5401, 5600), (5601, 5800), (5801, 6000),
                    (6001, 6200), (6201, 6400), (6401, 6600),
                    (6601, 6800), (6801, 7000), (7001, 7200),
                    (7201, 7400), (7401, 7600), (7601, 7800),
                    (7801, 8000), (8001, 8200), (8201, 8400),
                    (8401, 8600), (8601, 8800), (8801, 9000),
                    (9001, 9200), (9201, 9400), (9401, 9600),
                    (9601, 9800), (9801, 10000), (10001, 10200),
                    (10201, 10400), (10401, 10600), (10601, 10800),
                    (10801, 11000), (11001, 11200), (11201, 11400),
                    (11401, 11600), (11601, 11800), (11801, 12000),
                    (12001, 12200), (12201, 12400), (12401, 12600),
                    (12601, 12800), (12801, 13000), (13001, 13200),
                    (13201, 13400), (13401, 13600), (13601, 13800),
                    (13801, 14000), (14001, 14200), (14201, 14400),
                    (14401, 14600), (14601, 14800), (14801, 15000),
                    (15001, 15200), (15201, 15400), (15401, 15600),
                    (15601, 15800)]

# Create a mapping dictionary for initial buckets
initial_mapping = {i: 0.959 - (i * 0.0022) for i in range(len(initial_buckets))}

# Create a mapping dictionary for extended buckets
extended_mapping = {i + len(initial_buckets): value for i, value in enumerate([
    1.1244, 1.1336, 1.1428, 1.1520, 1.1612, 1.1704, 1.1796, 1.188

--------------------------------------------------------------------------------+++++++++++++++++++++++++++++++++++++
# Define your extended buckets and corresponding mapped values
extended_buckets = [(3001, 3200), (3201, 3400), (3401, 3600),
                    (3601, 3800), (3801, 4000), (4001, 4200),
                    (4201, 4400), (4401, 4600), (4601, 4800),
                    (4801, 5000), (5001, 5200), (5201, 5400),
                    (5401, 5600), (5601, 5800), (5801, 6000),
                    (6001, 6200), (6201, 6400), (6401, 6600),
                    (6601, 6800), (6801, 7000), (7001, 7200),
                    (7201, 7400), (7401, 7600), (7601, 7800),
                    (7801, 8000), (8001, 8200), (8201, 8400),
                    (8401, 8600), (8601, 8800), (8801, 9000),
                    (9001, 9200), (9201, 9400), (9401, 9600),
                    (9601, 9800), (9801, 10000), (10001, 10200),
                    (10201, 10400), (10401, 10600), (10601, 10800),
                    (10801, 11000), (11001, 11200), (11201, 11400),
                    (11401, 11600), (11601, 11800), (11801, 12000),
                    (12001, 12200), (12201, 12400), (12401, 12600),
                    (12601, 12800), (12801, 13000), (13001, 13200),
                    (13201, 13400), (13401, 13600), (13601, 13800),
                    (13801, 14000), (14001, 14200), (14201, 14400),
                    (14401, 14600), (14601, 14800), (14801, 15000),
                    (15001, 15200), (15201, 15400), (15401, 15600),
                    (15601, 15800)]

# Create a mapping dictionary for initial buckets
initial_mapping = {i: 0.959 - (i * 0.0022) for i in range(len(initial_buckets))}

# Create a mapping dictionary for extended buckets
extended_mapping = {i + len(initial_buckets): value for i, value in enumerate([
    1.1244, 1.1336, 1.1428, 1.1520, 1.1612, 1.1704, 1.1796, 1.188
























    

   https://mail-attachment.googleusercontent.com/attachment/u/0/?ui=2&ik=9a92c97c12&attid=0.1&permmsgid=msg-f:1775807566243792245&th=18a4ef92a7698575&view=att&disp=inline&realattid=f_lm0375pq0&saddbat=ANGjdJ_P6x6rz_uTpI-nU6PMlScUxaV3C_wB-Lvt8ZyIIFvO3mpdKNPpzjcyNn_x074FNXMJHkdv8nG630spfl0tSFavqbCVqODb9P06Y5mf9_gStS8gvlfYVz7z_wpCinDy71vVPahQB-CyZIJYhSA5HVeV2jpFCoyRmWWrr00su_fcXC9zI78u_8ituxbSjUbjbvCRBAK1I0Ohdk7yzys7DEyn1wRZIesRdGddXPGOakBt6dGBs6ZVMg4BMqdFXGZxFCohXhraQAaj-BbeefT5SF-2mpZhZKg6_Mne-qnlSb-arUZeeSDalDPVQBcew63HvQBa9kMkDQtQqbhhgYPqtE1ydFGMZ6kBhyj2_73cdTzTLLIhV-Pcz1ms7AQ2R2tH6fZPhhI6lrvI3P_G4XyLPWHR-N0KUcVvn6AnrwvTaRih0CbTKcM0heSiJ4Lcz5ELKPK5Vnl3ULVWl5Uy6hlzx3ZpE9UL5dRi9oFlNXO2fuxWVyg4GMw_oT9eQvUsnomWP38O69PxsjF2m5vaYmXJ6mtaZQKaNMMJv_Sqq4NGvyXB-duBj91bDh_RivxKrg3Za2j5BFmcIjjZ2dG4jd7a1xSRC6mcVyhL56dD6Fr6c0kHLIxPrPcqqcU3yUZGv1QZBjyCYI-1yJtw14UhQzx156qW1PRErwM00W1FB3ZY-OIn3TbW06zkIM1mvHAl5BGcL32ZGvxr5rHlkBJTi3OpIl0PAAFE9JhdxDc3Tg5CQkGxxSvyCtX83ta9-ldDQX8qbk6Q4tcgzEy6IpuiJ29RYpvv7uFFcMlwXBUaFf-YQO8bQJFFdN3zXs3FkYIrkh4WZQFy0Lj3hXqXhjlHVwCn8MNqJqhyKLY0G7QAbQE0NeAcyro_C61ZwPvwhCchAt_Xw7v0DmkQJL5oo0Ey2Z59HhbvmHRZhBfSOQBdktEpKOyUBZoCnb2pfvs--br63CPsI1ynUTCm4osEjfpoqsiTuUTLS-hnKIjFTKZBhrWeXo1H28o8DptZYvMnslASI6Yx7xdtnqsLMBAZNQsi





   https://github.com/LFCFireLab/FireLossRate





file:///C:/Users/HP/Downloads/S2215016123002352.htm


https://www.sciencedirect.com/science/article/pii/S2215016123002352




https://www.corelogic.com/intelligence/how-to-predict-fire-insurance-losses/



Certainly, I can provide more detailed information on common data sources for wildfire loss data:

1. **Insurance Claims Data**: Insurance companies maintain detailed records of claims filed by policyholders for losses due to wildfires. These data sources are typically internal and may not be publicly accessible.

2. **Government Agencies**: Government agencies like FEMA (Federal Emergency Management Agency) and state-level emergency management organizations often collect and maintain data on wildfire events and their impacts. You can find some of this data on their respective websites.

   - [FEMA Disaster Declarations](https://www.fema.gov/disasters)
   - State-specific agencies (e.g., California's [Cal Fire](https://www.fire.ca.gov/), or [USDA Forest Service](https://www.fs.usda.gov/))

3. **Satellite Imagery**: Organizations like NASA and NOAA provide access to satellite imagery, which can be used to monitor and assess the extent of wildfires. You can find this data on their respective websites.

   - [NASA Earthdata](https://earthdata.nasa.gov/)
   - [NOAA's National Centers for Environmental Information](https://www.ncei.noaa.gov/)

4. **Climate and Weather Data**: Historical weather and climate data can help assess wildfire risk. The National Weather Service (NWS) and the National Oceanic and Atmospheric Administration (NOAA) are good sources for such data.

   - [National Weather Service](https://www.weather.gov/)
   - [NOAA Climate Data Online (NCDC)](https://www.ncdc.noaa.gov/)

5. **Geospatial Data**: Geographic Information Systems (GIS) data can provide information on the geography of wildfire-prone areas. You can explore GIS data from sources like:

   - [USGS Earth Explorer](https://earthexplorer.usgs.gov/)
   - [GIS Data from State and Local Governments](varies by location)

6. **Historical Records**: Historical data on previous wildfires, their impacts, and losses can sometimes be found in research reports, academic publications, and historical archives.

Please note that access to these data sources may vary, and some data may require permissions or agreements for use. Additionally, specific data sources used by individual companies may not be publicly disclosed due to proprietary considerations, so reaching out to those companies directly may be necessary for more detailed information.



Estimating property-wise losses due to wildfires typically involves a combination of data sources and methodologies. Here are some of the data sources commonly used for this purpose:

1. **Insurance Company Records**: Insurance companies maintain detailed records of insured properties, including their values and the extent of coverage. These records are a primary source for estimating property-specific losses.

2. **Assessment and Appraisal Data**: Property assessments and appraisals conducted by government agencies or private firms provide information about the value of properties. This data can be used to estimate property losses.

3. **Geospatial Data**: Geographic Information Systems (GIS) data, such as parcel maps and land-use data, can help identify the location and characteristics of individual properties in wildfire-prone areas.

4. **Remote Sensing and Satellite Imagery**: High-resolution satellite imagery can be used to assess property damage after a wildfire event. This data can help identify which properties were affected and to what extent.

5. **Census Data**: Census data provides demographic information about populations in wildfire-prone areas. This information can be used to estimate the number of properties at risk and their potential value.

6. **Historical Data**: Historical data on previous wildfire events and their impacts on specific properties can inform loss estimations for future events.

7. **Property Records**: Publicly available property records, including tax assessment data, can provide information on property values and ownership.

8. **Insurance Claims Data**: After a wildfire event, insurance claims data specific to individual properties can be used to verify and refine loss estimates.

9. **Wildfire Behavior Models**: Advanced modeling techniques that simulate wildfire behavior, taking into account factors like wind patterns, terrain, and fuel load, can help estimate property-specific losses.

10. **Field Surveys**: Post-wildfire field surveys by experts and adjusters provide on-the-ground information about property damage and losses.

Please note that the availability and accuracy of these data sources can vary by location and may not always be publicly accessible. Insurance companies and government agencies often combine several of these sources to create comprehensive estimates of property-wise losses due to wildfires. Access to proprietary data held by insurance companies may require direct contact with those companies or partnerships between data providers and researchers.


https://mediatum.ub.tum.de/doc/1452293/document.pdf










------/-----
document.pdf










------/-----
import pandas as pd

# Sample DataFrame (replace this with your actual DataFrame)
data = {
    'Pool Area (Square Feet)': [1000, 1500, 800, 1200],
    'Pool Enclosure Existence (Yes/No)': ['Yes', 'No', 'Yes', 'No'],
    'Temporary Pool (Yes/No)': ['No', 'Yes', 'No', 'No'],
    'Trampoline Existence (Yes/No)': ['No', 'Yes', 'No', 'Yes']
}

df = pd.DataFrame(data)

# Define the updated weights for each feature
weights = {
    'Pool Area (Square Feet)': 0.2,
    'Pool Enclosure Existence (Yes/No)': 0.3,
    'Temporary Pool (Yes/No)': 0.1,
    'Trampoline Existence (Yes/No)': 0.1
}

# Create the 'Pool' feature with updated weights
df['Pool'] = (
    df['Pool Area (Square Feet)'] * weights['Pool Area (Square Feet)'] +
    (df['Pool Enclosure Existence (Yes/No)'] == 'Yes') * weights['Pool Enclosure Existence (Yes/No)'] +
    (df['Temporary Pool (Yes/No)'] == 'Yes') * weights['Temporary Pool (Yes/No)'] +
    (df['Trampoline Existence (Yes/No)'] == 'Yes') * weights['Trampoline Existence (Yes/No)']
)

# Display the updated DataFrame with the 'Pool' feature
print(df)



    https://www.understandconstruction.com/wood-framed-construction.html
    https://www.bigrentz.com/blog/building-construction-types
    https://www.procore.com/library/construction-project-types#2-commercial-projects
    https://www.strongholdengineering.com/the-5-types-of-building-construction-and-their-pros-and-cons/













    [950,975]	0.959
[975,1000]	0.959
[1000,1025]	0.959
[1025,1050]	0.959
[1050,1075]	0.959
[1075,1100]	0.959

