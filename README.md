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
import json

class Wildfire:
    def __init__(self, property_file_path, hazard_file_path):
        # Read the property and hazard Excel files into dataframes
        self.property_data = pd.read_excel(property_file_path)
        self.hazard_data = pd.read_excel(hazard_file_path)
        
        # Concatenate County and State columns to create a common key
        self.property_data['County_State'] = self.property_data['County'] + '_' + self.property_data['State']
        self.hazard_data['County_State'] = self.hazard_data['County'] + '_' + self.hazard_data['State']

        # Merge property and hazard data on the 'County_State' column
        self.merged_data = pd.merge(self.property_data, self.hazard_data, on='County_State', how='inner')

    def predict_risk_score(self, address_json):
        # Parse the JSON input
        address_data = json.loads(address_json)
        
        # Extract County and State from the JSON
        county = address_data.get('County')
        state = address_data.get('State')
        
        # Create a key for matching with the merged data
        county_state_key = county + '_' + state
        
        # Filter the merged data for the given County_State
        filtered_data = self.merged_data[self.merged_data['County_State'] == county_state_key]
        
        if len(filtered_data) == 0:
            return "Address not found in the dataset"
        
        # Calculate the final risk score by multiplying Property Score and Exposure Score
        final_score = filtered_data['Property_Score'] * filtered_data['Exposure_Score']
        
        return final_score.iloc[0]  # Return the final risk score for the given address

# Example usage:
property_file_path = 'property_data.xlsx'
hazard_file_path = 'hazard_data.xlsx'
wildfire = Wildfire(property_file_path, hazard_file_path)

address_json = '{"County": "YourCounty", "State": "YourState"}'
risk_score = wildfire.predict_risk_score(address_json)
print("Final Risk Score:", risk_score)



