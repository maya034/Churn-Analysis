# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 






STRT_LINE_1_DESC	CITY_NME	ST_ABBR_CD	ZIP_CD	Footprint_Area	Story_Num_BU	Square_Footage	Roof_Type_RF	Roof_Material_RF	Roof_Condition_RF	Roof_Evidence_RF	Solar_Panels_RF	Air_Conditioner_RF	Skylights_RF	Chimneys_RF	Tree_Overhang_RF	Gable_Wall_DI_RF	Building_Height_BU	Ground_Height_BU	DIS_ClosestBuilding_BU	DIS_Vegetation_BU	Tree_height_BU	DIS_Trees_BU	Pool_AR_PA	Pool_Enclosure_PA	Temporary_pool_PA	Trampoline_PA	Yard_Debris_PA	DIS_WaterBody_BU	DIS_Firestation_BU	DIS_Coast_BU	Construction	Occupancy	Year_built	No of Building																																																									

from fastapi import FastAPI
from pymongo import MongoClient
from pydantic import BaseModel

app = FastAPI()

# Connect to MongoDB
client = MongoClient('mongodb://localhost:27017')  # Adjust the connection URL as needed
db = client['your_database_name']  # Replace 'your_database_name' with your actual database name
collection = db['house_collection']

class AddressInput(BaseModel):
    address: str

@app.post("/get_risk_score")
async def get_risk_score(address_input: AddressInput):
    # Query the MongoDB collection for the risk score based on the provided address
    query = {"STRT_LINE_1_DESC": address_input.address}
    result = collection.find_one(query, {"_id": 0, "Total_Score": 1})

    if result:
        risk_score = result.get("Total_Score")
        return {"address": address_input.address, "risk_score": risk_score}
    else:
        return {"address": address_input.address, "error": "Address not found"}

if __name__ == "__main__":
    import uvicorn

    uvicorn.run(app, host="0.0.0.0", port=8000)








Replace 'your_database_name' with your actual database name and 'house_collection' with the name of the collection where your data is stored.

Save this code to a Python file, and run it using UVicorn:
bash
Copy code
uvicorn your_file_name:app --host 0.0.0.0 --port 8000
Now, you have a FastAPI application running with an endpoint at http://localhost:8000/get_risk_score. You can send a POST request with an address as input, and it will search the MongoDB collection for the corresponding risk score and return it.

Remember to customize the code further as needed for your specific use case, including handling error cases and adding security features if required.











import pandas as pd

# Assuming your DataFrame is named merged_data_score
# Define the quantile values
quantile_values = {
    0.00: 0.357284,
    0.25: 783.035629,
    0.50: 2328.276703,
    0.75: 4123.877565,
    1.00: 63173.158836
}

# Define a function to categorize values
def categorize_score(score):
    if score <= quantile_values[0.25]:
        return 'minor'
    elif score <= quantile_values[0.50]:
        return 'moderate'
    elif score <= quantile_values[0.75]:
        return 'high'
    else:
        return 'very high'

# Apply the categorization function to create a new column
merged_data_score['overall_category'] = merged_data_score['overall_scoring'].apply(categorize_score)

# Print the updated DataFrame
print(merged_data_score)
































import pandas as pd
import json

class Wildfire:
    def __init__(self, property_file_path, hazard_file_path):
        # Read the property and hazard Excel files into dataframes
        self.property_data = pd.read_excel(property_file_path)
        self.hazard_data = pd.read_excel(hazard_file_path)
        
        # Concatenate County and State columns to create a common key
        #self.property_data['County_State'] = self.property_data['County'] + '_' + self.property_data['State']
        #self.hazard_data['County_State'] = self.hazard_data['County'] + '_' + self.hazard_data['State']

        # Merge property and hazard data on the 'County_State' column
        self.merged_data = pd.merge( self.hazard_data,self.property_data, on='county', how='inner')

    def predict_risk_score(self, address_json):
        # Parse the JSON input
        address_data = json.loads(address_json)
        
        # Extract County and State from the JSON
        county = address_data.get('County').lower()
        state = address_data.get('State').lower
        
        # Create a key for matching with the merged data
        county_state_key = county + ',' + state
        
        # Filter the merged data for the given County_State
        filtered_data = self.merged_data[self.merged_data['County_State'] == county_state_key]
        
        if len(filtered_data) == 0:
            return "Address not found in the dataset"
        
        # Calculate the final risk score by multiplying Property Score and Exposure Score
        final_score = filtered_data['Property_Score'] * filtered_data['Exposure_Score']
        
        return final_score.iloc[0]  # Return the final risk score for the given address

# Example usage:
property_file_path = 'vendor_property_attribute.xlsx'
hazard_file_path = 'hazard_exposure_score.xlsx'
wildfire = Wildfire(property_file_path, hazard_file_path)

address_json = '{"County": "gwinnett county", "State": "georgia"}'
risk_score = wildfire.predict_risk_score(address_json)
print("Final Risk Score:", risk_score)






















import pandas as pd
import json

class Wildfire:
    def __init__(self, property_file_path, hazard_file_path):
        # Read the property and hazard Excel files into dataframes
        self.property_data = pd.read_excel(property_file_path)
        self.hazard_data = pd.read_excel(hazard_file_path)

        # Merge property and hazard data on the 'County' column (assuming 'County' is the common key)
        self.merged_data = pd.merge(self.hazard_data, self.property_data, on='County', how='inner')

    def predict_risk_score(self, address_json):
        # Parse the JSON input
        address_data = json.loads(address_json)

        # Extract County and State from the JSON and convert to lowercase
        county = address_data.get('County').lower()
        state = address_data.get('State').lower()

        # Create a key for matching with the merged data
        county_state_key = f"{county},{state}"

        # Filter the merged data for the given County_State
        filtered_data = self.merged_data[self.merged_data['County_State'] == county_state_key]

        if len(filtered_data) == 0:
            return "Address not found in the dataset"

        # Calculate the final risk score by multiplying Property Score and Exposure Score
        final_score = filtered_data['Property_Score'] * filtered_data['Exposure_Score']

        return final_score.iloc[0]  # Return the final risk score for the given address

# Example usage:
property_file_path = 'vendor_property_attribute.xlsx'
hazard_file_path = 'hazard_exposure_score.xlsx'
wildfire = Wildfire(property_file_path, hazard_file_path)

address_json = '{"County": "gwinnett county", "State": "georgia"}'
risk_score = wildfire.predict_risk_score(address_json)
print("Final Risk Score:", risk_score)


 File "C:\Users\mayank205427\AppData\Local\Temp\1\ipykernel_24396\2076836893.py", line 46
    ​
    ^
SyntaxError: invalid non-printable character U+200B
















# Corrected code without non-printable characters
import pandas as pd
import json

class Wildfire:
    def __init__(self, property_file_path, hazard_file_path):
        # Read the property and hazard Excel files into dataframes
        self.property_data = pd.read_excel(property_file_path)
        self.hazard_data = pd.read_excel(hazard_file_path)

        # Merge property and hazard data on the 'County' column (assuming 'County' is the common key)
        self.merged_data = pd.merge(self.hazard_data, self.property_data, on='County', how='inner')

    def predict_risk_score(self, address_json):
        # Parse the JSON input
        address_data = json.loads(address_json)

        # Extract County and State from the JSON and convert to lowercase
        county = address_data.get('County').lower()
        state = address_data.get('State').lower()

        # Create a key for matching with the merged data
        county_state_key = f"{county},{state}"

        # Filter the merged data for the given County_State
        filtered_data = self.merged_data[self.merged_data['County_State'] == county_state_key]

        if len(filtered_data) == 0:
            return "Address not found in the dataset"

        # Calculate the final risk score by multiplying Property Score and Exposure Score
        final_score = filtered_data['Property_Score'] * filtered_data['Exposure_Score']

        return final_score.iloc[0]  # Return the final risk score for the given address

# Example usage:
property_file_path = 'vendor_property_attribute.xlsx'
hazard_file_path = 'hazard_exposure_score.xlsx'
wildfire = Wildfire(property_file_path, hazard_file_path)

address_json = '{"County": "gwinnett county", "State": "georgia"}'
risk_score = wildfire.predict_risk_score(address_json)
print("Final Risk Score:", risk_score)







import pandas as pd
from sklearn.externals import joblib
from pymongo import MongoClient

class PropertyDataProcessor:
    def __init__(self, property_file_path, hazard_file_path, model_file_path, db_name, collection_name):
        self.property_attributes = pd.read_excel(property_file_path)
        self.hazard_values = pd.read_excel(hazard_file_path)
        self.model = joblib.load(model_file_path)

        # Merge the two DataFrames on the common column (County_State)
        self.merged_data = pd.merge(self.property_attributes, self.hazard_values, how='inner', on='County_State')

        # MongoDB Connection
        self.client = MongoClient('localhost', 27017)  # Modify connection details as needed
        self.db = self.client[db_name]
        self.collection = self.db[collection_name]

    def convert_to_categories(self, categorical_features):
        for feature in categorical_features:
            self.merged_data[feature] = self.merged_data[feature].astype('category')

    def calculate_property_score(self, feature_weights):
        self.merged_data['Property_Score'] = 0
        for feature, weight in feature_weights.items():
            self.merged_data['Property_Score'] += self.merged_data[feature].cat.codes * weight

    def insert_into_mongodb(self):
        records = self.merged_data.to_dict(orient='records')
        self.collection.insert_many(records)

    def process_new_row(self, new_row, feature_weights):
        for feature in feature_weights:
            new_row[feature] = new_row[feature].astype('category')

        new_row['Property_Score'] = sum(new_row[feature].cat.codes * weight for feature, weight in feature_weights.items())

        # Insert the new row into MongoDB
        records = new_row.to_dict(orient='records')
        self.collection.insert_many(records)


# Example usage:

# Define file paths
property_file_path = "property_attributes.xlsx"
hazard_file_path = "hazard_values.xlsx"
model_file_path = "your_model.pkl"

# Define MongoDB details
db_name = 'your_database'
collection_name = 'your_collection'

# Create an instance of PropertyDataProcessor
property_processor = PropertyDataProcessor(property_file_path, hazard_file_path, model_file_path, db_name, collection_name)

# Define categorical features and weights
categorical_features = ['STRT_LINE_1_DESC', 'CITY_NME', 'ST_ABBR_CD', 'Roof_Type_RF', 'Roof_Material_RF', 'Roof_Condition_RF', 'Roof_Evidence_RF', 'Solar_Panels_RF',
                         'Air_Conditioner_RF', 'Skylights_RF', 'Chimneys_RF', 'Tree_Overhang_RF', 'Gable_Wall_DI_RF', 'Construction', 'Occupancy']

feature_weights = {
    'STRT_LINE_1_DESC': 0.1,
    'CITY_NME': 0.05,
    'ST_ABBR_CD': 0.05,
    # ... add weights for other features
}

# Process data and insert into MongoDB
property_processor.convert_to_categories(categorical_features)
property_processor.calculate_property_score(feature_weights)
property_processor.insert_into_mongodb()

# Example new row
new_row = pd.DataFrame({
    'STRT_LINE_1_DESC': ['New Street'],
    'CITY_NME': ['New City'],
    'ST_ABBR_CD': ['NY'],
    # ... other attributes for the new row
})

# Process the new row and insert into MongoDB
property_processor.process_new_row(new_row, feature_weights)
​






















import pandas as pd
from pymongo import MongoClient

class PropertyDataProcessor:
    def __init__(self, hazard_file_path, db_name, collection_name):
        self.hazard_values = pd.read_excel(hazard_file_path)

        # MongoDB Connection
        self.client = MongoClient('localhost', 27017)  # Modify connection details as needed
        self.db = self.client[db_name]
        self.collection = self.db[collection_name]

    def fetch_property_attributes(self, attributes):
        # Fetch specified property attributes from MongoDB collection
        query = {}  # You can add more specific query parameters if needed
        projection = {'_id': 0, 'County_State': 1, **{attr: 1 for attr in attributes}}
        property_attributes = pd.DataFrame(list(self.collection.find(query, projection)))

        return property_attributes

    def merge_data(self, property_attributes):
        # Merge property attributes and hazard values on the common column (County_State)
        merged_data = pd.merge(property_attributes, self.hazard_values, how='inner', on='County_State')

        # Calculate the final score by multiplying Property_Score and Exposure_Score
        merged_data['Final_Score'] = merged_data['Property_Score'] * merged_data['Exposure_Score']

        return merged_data

    def update_mongodb(self, merged_data):
        # Update MongoDB collection with the new data
        records = merged_data.to_dict(orient='records')
        self.collection.insert_many(records)

# Example usage:
# Define file paths and MongoDB details
hazard_file_path = "hazard_values.xlsx"
db_name = 'your_database'
collection_name = 'your_collection'

# Create an instance of PropertyDataProcessor
property_processor = PropertyDataProcessor(hazard_file_path, db_name, collection_name)

# Specify property attributes to fetch from MongoDB
attributes_to_fetch = ['STRT_LINE_1_DESC', 'CITY_NME', 'ST_ABBR_CD', 'Roof_Type_RF', 'Roof_Material_RF', 'Roof_Condition_RF',
                        'Roof_Evidence_RF', 'Solar_Panels_RF', 'Air_Conditioner_RF', 'Skylights_RF', 'Chimneys_RF', 'Tree_Overhang_RF',
                        'Gable_Wall_DI_RF', 'Construction', 'Occupancy']

# Fetch property attributes from MongoDB
property_attributes = property_processor.fetch_property_attributes(attributes_to_fetch)

# Merge data and calculate the final score
merged_data = property_processor.merge_data(property_attributes)

# Update MongoDB with the merged data
property_processor.update_mongodb(merged_data)



















STRT_LINE_1_DESC
CITY_NME
ST_ABBR_CD
ZIP_CD
Story_Num_BU
Square_Footage
Roof_Type_RF
Roof_Material_RF
Roof_Condition_RF
Air_Conditioner_RF
Skylights_RF
Chimneys_RF
Tree_Overhang_RF
DIS_ClosestBuilding_BU
DIS_Vegetation_BU
DIS_Trees_BU
Pool_AR_PA
Temporary_pool_PA
Yard_Debris_PA
DIS_WaterBody_BU
DIS_Firestation_BU
DIS_Coast_BU
Construction
Occupancy
Year_built
No of Building












































import pandas as pd
from pymongo import MongoClient

class PropertyScoreCalculator:
    def __init__(self, db_name, collection_name, push_new_data_to_mongo=True):
        self.push_new_data_to_mongo = push_new_data_to_mongo

        # MongoDB Connection
        self.client = MongoClient('localhost', 27017)  # Modify connection details as needed
        self.db = self.client[db_name]
        self.collection = self.db[collection_name]

    def fetch_property_attributes(self):
        # Fetch all property attributes from MongoDB collection
        query = {}  # You can add more specific query parameters if needed
        projection = {'_id': 0}  # Exclude '_id' field from the result
        property_attributes = pd.DataFrame(list(self.collection.find(query, projection)))

        return property_attributes

    def calculate_score(self, property_attributes):
        # Fill NaN values with 1
        property_attributes.fillna(1, inplace=True)

        # Define risk buckets for different attributes (you can modify as needed)
        risk_buckets = {
            'Square_Footage': [(1, 2000), (2001, 4000), (4001, 6000), (6001, float('inf'))],
            # Add more attributes and buckets
        }

        # Iterate through each attribute and apply the corresponding risk bucket
        for attribute, buckets in risk_buckets.items():
            property_attributes[attribute] = property_attributes[attribute].apply(
                lambda x: next((score for start, end, score in buckets if start <= x <= end), None)
            )

        # Add logic for other steps of score calculation here

        return property_attributes

    def update_mongodb(self, property_attributes):
        if self.push_new_data_to_mongo:
            # Update MongoDB collection with the new data
            records = property_attributes.to_dict(orient='records')
            self.collection.insert_many(records)

# Example usage:
# Define MongoDB details
db_name = 'your_database'
collection_name = 'your_collection'

# Create an instance of PropertyScoreCalculator
score_calculator = PropertyScoreCalculator(db_name, collection_name)

# Fetch existing property attributes from MongoDB
existing_attributes = score_calculator.fetch_property_attributes()

# Calculate scores for existing attributes
calculated_scores = score_calculator.calculate_score(existing_attributes)

# Update MongoDB with the calculated scores
score_calculator.update_mongodb(calculated_scores)




# Define custom risk buckets as percentiles
risk_buckets = {
    85: (1, 2000),
    90: (2001, 4000),
    95: (4001, 6000),
    100: (6001, float('inf'))
}

# Define a function to assign risk buckets based on square footage
def define_risk_bucket(sqft):
    if sqft==0:
        return 1
    else:
        
        for risk, (min_sqft, max_sqft) in risk_buckets.items():
            if min_sqft <= sqft <= max_sqft:
                return risk

# Apply the risk bucketing function to each property
df['Square_Footage'] = df['Square_Footage'].apply(define_risk_bucket)














import pandas as pd
from pymongo import MongoClient

class PropertyScoreCalculator:
    def __init__(self, db_name, collection_name):
        # MongoDB Connection
        self.client = MongoClient('localhost', 27017)  # Modify connection details as needed
        self.db = self.client[db_name]
        self.collection = self.db[collection_name]

    def fetch_property_attributes(self):
        # Fetch all property attributes from MongoDB collection
        query = {}  # You can add more specific query parameters if needed
        projection = {'_id': 0}  # Exclude '_id' field from the result
        property_attributes = pd.DataFrame(list(self.collection.find(query, projection)))

        return property_attributes

    def calculate_score(self, property_attributes):
        # Create a copy to avoid modifying the original DataFrame
        property_attributes_copy = property_attributes.copy()

        # Define custom risk buckets as percentiles
        risk_buckets = {
            85: (1, 2000),
            90: (2001, 4000),
            95: (4001, 6000),
            100: (6001, float('inf'))
        }

        # Define a function to assign risk buckets based on square footage
        def define_risk_bucket(sqft):
            if sqft == 0:
                return 1
            else:
                for risk, (min_sqft, max_sqft) in risk_buckets.items():
                    if min_sqft <= sqft <= max_sqft:
                        return risk

        # Apply the risk bucketing function to each property and create a temporary column
        property_attributes_copy['Temp_Square_Footage'] = property_attributes_copy['Square_Footage'].apply(define_risk_bucket)

        # Add logic for other steps of score calculation here

        return property_attributes_copy

# Example usage:
# Define MongoDB details
db_name = 'your_database'
collection_name = 'your_collection'

# Create an instance of PropertyScoreCalculator
score_calculator = PropertyScoreCalculator(db_name, collection_name)

# Fetch existing property attributes from MongoDB
existing_attributes = score_calculator.fetch_property_attributes()

# Calculate scores on the fly without modifying the raw data
calculated_scores = score_calculator.calculate_score(existing_attributes)

# You can use 'calculated_scores' for your analysis without changing the original data in MongoDB
print(calculated_scores)





































import pandas as pd
from pymongo import MongoClient

class PropertyScoreCalculator:
    def __init__(self, db_name, collection_name, push_new_data_to_mongo=True):
        self.push_new_data_to_mongo = push_new_data_to_mongo

        # MongoDB Connection
        self.client = MongoClient('localhost', 27017)  # Modify connection details as needed
        self.db = self.client[db_name]
        self.collection = self.db[collection_name]

    def fetch_property_attributes(self):
        # Fetch all property attributes from MongoDB collection
        query = {}  # You can add more specific query parameters if needed
        projection = {'_id': 0}  # Exclude '_id' field from the result
        property_attributes = pd.DataFrame(list(self.collection.find(query, projection)))

        return property_attributes

    def calculate_score(self, property_attributes):
        # Define attributes to fetch
        attributes_to_fetch = ['STRT_LINE_1_DESC', 'CITY_NME', 'ST_ABBR_CD', 'Roof_Type_RF', 'Roof_Material_RF',
                               'Roof_Condition_RF', 'Roof_Evidence_RF', 'Solar_Panels_RF', 'Air_Conditioner_RF',
                               'Skylights_RF', 'Chimneys_RF', 'Tree_Overhang_RF', 'Gable_Wall_DI_RF', 'Construction',
                               'Occupancy']

        # Create a copy with only the selected attributes
        selected_attributes = property_attributes[attributes_to_fetch].copy()

        # Define custom risk buckets as percentiles
        risk_buckets = {
            85: (1, 2000),
            90: (2001, 4000),
            95: (4001, 6000),
            100: (6001, float('inf'))
        }

        # Define a function to assign risk buckets based on square footage
        def define_risk_bucket(sqft):
            if sqft == 0:
                return 1
            else:
                for risk, (min_sqft, max_sqft) in risk_buckets.items():
                    if min_sqft <= sqft <= max_sqft:
                        return risk

        # Apply the risk bucketing function to 'Square_Footage'
        selected_attributes['Square_Footage'] = property_attributes['Square_Footage'].apply(define_risk_bucket)

        # Add logic for other steps of score calculation here

        return selected_attributes

    def update_mongodb(self, property_attributes):
        if self.push_new_data_to_mongo:
            # Exclude the 'Square_Footage' column from the DataFrame before updating MongoDB
            property_attributes_to_update = property_attributes.drop(columns=['Square_Footage'])

            # Update MongoDB collection with the new data
            records = property_attributes_to_update.to_dict(orient='records')
            self.collection.insert_many(records)

# Example usage:
# Define MongoDB details
db_name = 'your_database'
collection_name = 'your_collection'

# Create an instance of PropertyScoreCalculator
score_calculator = PropertyScoreCalculator(db_name, collection_name)

# Fetch existing property attributes from MongoDB
existing_attributes = score_calculator.fetch_property_attributes()

# Calculate scores on the fly without modifying the raw data
calculated_scores = score_calculator.calculate_score(existing_attributes)

# You can use 'calculated_scores' for your analysis without changing the original data in MongoDB
print(calculated_scores)


















































































#Loss due to primary features
def calculate_primary_risk_score(row):
    # Define the percentages for each primary feature
    construction_percentage = 45
    occupancy_percentage = 15
    year_built_percentage = 10
    num_buildings_percentage = 5
    square_footage_percentage = 15
    story_num_percentage = 10

    # Calculate the risk score for the row
    risk_score = (
        (row['Construction'] * construction_percentage / 100) +
        (row['Occupancy'] * occupancy_percentage / 100) +
        (row['Year_built'] * year_built_percentage / 100) +
        (row['No of Building'] * num_buildings_percentage / 100) +
        (row['Square_Footage'] * square_footage_percentage / 100) +
        (row['Story_Num_BU'] * story_num_percentage / 100)
    )

    return risk_score

# Calculate the risk score for each row in the DataFrame
df['Primary_risk'] = df.apply(calculate_primary_risk_score, axis=1)
















TypeError                                 Traceback (most recent call last)
~\AppData\Local\Temp\1\ipykernel_16156\903857533.py in <module>
     22 
     23 # Calculate the risk score for each row in the DataFrame
---> 24 df['Primary_risk'] = df.apply(calculate_primary_risk_score, axis=1)
     25 

~\Anaconda3\lib\site-packages\pandas\core\frame.py in apply(self, func, axis, raw, result_type, args, **kwargs)
   8846             kwargs=kwargs,
   8847         )
-> 8848         return op.apply().__finalize__(self, method="apply")
   8849 
   8850     def applymap(

~\Anaconda3\lib\site-packages\pandas\core\apply.py in apply(self)
    731             return self.apply_raw()
    732 
--> 733         return self.apply_standard()
    734 
    735     def agg(self):

~\Anaconda3\lib\site-packages\pandas\core\apply.py in apply_standard(self)
    855 
    856     def apply_standard(self):
--> 857         results, res_index = self.apply_series_generator()
    858 
    859         # wrap results

~\Anaconda3\lib\site-packages\pandas\core\apply.py in apply_series_generator(self)
    871             for i, v in enumerate(series_gen):
    872                 # ignore SettingWithCopy here in case the user mutates
--> 873                 results[i] = self.f(v)
    874                 if isinstance(results[i], ABCSeries):
    875                     # If we have a view on v, we need to make a copy because

~\AppData\Local\Temp\1\ipykernel_16156\903857533.py in calculate_primary_risk_score(row)
     12     risk_score = (
     13         (row['Construction'] * construction_percentage / 100) +
---> 14         (row['Occupancy'] * occupancy_percentage / 100) +
     15         (row['Year_built'] * year_built_percentage / 100) +
     16         (row['No of Building'] * num_buildings_percentage / 100) +

TypeError: unsupported operand type(s) for /: 'str' and 'int'
























import pandas as pd

# Assuming df is your DataFrame

# Convert relevant columns to numeric
numeric_columns = ['Construction', 'Occupancy', 'Year_built', 'No of Building', 'Square_Footage', 'Story_Num_BU']
df[numeric_columns] = df[numeric_columns].apply(pd.to_numeric, errors='coerce')

# Loss due to primary features
def calculate_primary_risk_score(row):
    # Define the percentages for each primary feature
    construction_percentage = 45
    occupancy_percentage = 15
    year_built_percentage = 10
    num_buildings_percentage = 5
    square_footage_percentage = 15
    story_num_percentage = 10

    # Calculate the risk score for the row
    risk_score = (
        (row['Construction'] * construction_percentage / 100) +
        (row['Occupancy'] * occupancy_percentage / 100) +
        (row['Year_built'] * year_built_percentage / 100) +
        (row['No of Building'] * num_buildings_percentage / 100) +
        (row['Square_Footage'] * square_footage_percentage / 100) +
        (row['Story_Num_BU'] * story_num_percentage / 100)
    )

    return risk_score

# Calculate the risk score for each row in the DataFrame
df['Primary_risk'] = df.apply(calculate_primary_risk_score, axis=1)





















































import pandas as pd
from fuzzywuzzy import fuzz

def find_most_relevant_record(query_address, fire_scores_file):
    """
    Find the most relevant record in the fire scores Excel file based on the 'address' column.

    Args:
        query_address (str): The query address to find the most relevant record.
        fire_scores_file (str): The path to the Excel file containing fire scores.

    Returns:
        The most relevant record in the fire scores Excel file.
    """
    most_relevant_record = None
    highest_relevance_score = 0

    # Read the Excel file into a DataFrame
    fire_scores_df = pd.read_excel(fire_scores_file)

    # Iterate through the DataFrame to find the most relevant record
    for index, row in fire_scores_df.iterrows():
        address = row.get("address", "")
        similarity_score = fuzz.ratio(query_address.lower(), address.lower())
        if (similarity_score > 70) and (similarity_score > highest_relevance_score):
            highest_relevance_score = similarity_score
            most_relevant_record = row.to_dict()

    return most_relevant_record

# Example usage:
query_address = "123 Main Street"  # Replace with your actual query address
fire_scores_file_path = "static/fire_scores.xlsx"  # Replace with the actual path to your Excel file

result = find_most_relevant_record(query_address, fire_scores_file_path)
print(result)

