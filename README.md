# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 






STRT_LINE_1_DESC	CITY_NME	ST_ABBR_CD	ZIP_CD	Footprint_Area	Story_Num_BU	Square_Footage	Roof_Type_RF	Roof_Material_RF	Roof_Condition_RF	Roof_Evidence_RF	Solar_Panels_RF	Air_Conditioner_RF	Skylights_RF	Chimneys_RF	Tree_Overhang_RF	Gable_Wall_DI_RF	Building_Height_BU	Ground_Height_BU	DIS_ClosestBuilding_BU	DIS_Vegetation_BU	Tree_height_BU	DIS_Trees_BU	Pool_AR_PA	Pool_Enclosure_PA	Temporary_pool_PA	Trampoline_PA	Yard_Debris_PA	DIS_WaterBody_BU	DIS_Firestation_BU	DIS_Coast_BU	Construction	Occupancy	Year_built	No of Building																																																																																																																																																																																																																																																															from pymongo import MongoClient

# Connect to MongoDB
client = MongoClient('mongodb://localhost:27017')  # Adjust the connection URL as needed
db = client['your_database_name']  # Replace 'your_database_name' with your actual database name
collection = db['house_collection']

# Assuming merge_data_score is a Pandas DataFrame
for index, row in merge_data_score.iterrows():
    # Extract the specific fields from each row
    document = {
        'STRT_LINE_1_DESC': row['STRT_LINE_1_DESC'],
        'CITY_NME': row['CITY_NME'],
        'ST_ABBR_CD': row['ST_ABBR_CD'],
        'ZIP_CD': row['ZIP_CD'],
        'Footprint_Area': row['Footprint_Area'],
        'Story_Num_BU': row['Story_Num_BU'],
        'Square_Footage': row['Square_Footage'],
        'Roof_Type_RF': row['Roof_Type_RF'],
        'Roof_Material_RF': row['Roof_Material_RF'],
        'Roof_Condition_RF': row['Roof_Condition_RF'],
        'Roof_Evidence_RF': row['Roof_Evidence_RF'],
        'Solar_Panels_RF': row['Solar_Panels_RF'],
        'Air_Conditioner_RF': row['Air_Conditioner_RF'],
        'Skylights_RF': row['Skylights_RF'],
        'Chimneys_RF': row['Chimneys_RF'],
        'Tree_Overhang_RF': row['Tree_Overhang_RF'],
        'Gable_Wall_DI_RF': row['Gable_Wall_DI_RF'],
        'Building_Height_BU': row['Building_Height_BU'],
        'Ground_Height_BU': row['Ground_Height_BU'],
        'DIS_ClosestBuilding_BU': row['DIS_ClosestBuilding_BU'],
        'DIS_Vegetation_BU': row['DIS_Vegetation_BU'],
        'Tree_height_BU': row['Tree_height_BU'],
        'DIS_Trees_BU': row['DIS_Trees_BU'],
        'Pool_AR_PA': row['Pool_AR_PA'],
        'Pool_Enclosure_PA': row['Pool_Enclosure_PA'],
        'Temporary_pool_PA': row['Temporary_pool_PA'],
        'Trampoline_PA': row['Trampoline_PA'],
        'Yard_Debris_PA': row['Yard_Debris_PA'],
        'DIS_WaterBody_BU': row['DIS_WaterBody_BU'],
        'DIS_Firestation_BU': row['DIS_Firestation_BU'],
        'DIS_Coast_BU': row['DIS_Coast_BU'],
        'Construction': row['Construction'],
        'Occupancy': row['Occupancy'],
        'Year_built': row['Year_built'],
        'No of Building': row['No of Building']
    }
    
    # Insert the document into the MongoDB collection
    collection.insert_one(document)

# Close the MongoDB connection
client.close()
