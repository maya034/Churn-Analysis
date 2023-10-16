# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 


Thank you for providing the abstract of the paper. Based on the abstract, I can provide a more detailed breakdown of the key concepts and methodologies discussed in the paper:

https://openacttexts.github.io/LDACourse1/index.html#why-loss-data-analytics









Roof_Type_RF/geometry	5
Roof_Condition_RF	
Roof_Material_RF	10
Pool_Enclosure_PA	
DIS_Firestation_BU	10
Chimneys_RF	5
Roof_Evidence_RF	
Solar_Panels_RF	
Air_Conditioner_RF	5
Skylights_RF	5
	
Tree_Overhang_RF	10
DIS_ClosestBuilding_BU	5
DIS_Trees_BU	10
DIS_Coast_BU	10
Pool_AR_PA	5
Temporary_pool_PA	
	
Yard_Debris_PA	10
DIS_WaterBody_BU	10
![Uploading image.png…]()



import pandas as pd

# Sample DataFrame (replace this with your actual DataFrame)
data = {
    'Roof_Type_RF': ['Flat', 'Gable', 'Hip', 'Gable'],
    'Roof_Material_Condition': [3, 2, 3, 4],
    'DIS_Firestation_BU': [0.5, 1.2, 0.8, 0.7],
    'Chimneys_RF': [0, 1, 0, 0],
    'Air_Conditioner_RF': [1, 0, 1, 1],
    'Skylights_RF': [0, 0, 0, 1],
    'Tree_Overhang_RF': [0.2, 0.3, 0.1, 0.4],
    'DIS_ClosestBuilding_BU': [2, 1.5, 2.5, 3.1],
    'DIS_Trees_BU': [0.2, 0.3, 0.4, 0.5],
    'DIS_Coast_BU': [2.5, 1.8, 3.2, 2.9],
    'Pools': [0, 0, 1, 0],
    'Yard_Debris_PA': [0.5, 0.3, 0.4, 0.2],
    'DIS_WaterBody_BU': [2.1, 2.5, 2.3, 1.9]
}

df = pd.DataFrame(data)

# Define the percentages for each secondary feature
percentages = {
    'Roof_Type_RF': 5,
    'Roof_Material_Condition': 5,
    'DIS_Firestation_BU': 10,
    'Chimneys_RF': 5,
    'Air_Conditioner_RF': 5,
    'Skylights_RF': 5,
    'Tree_Overhang_RF': 10,
    'DIS_ClosestBuilding_BU': 10,
    'DIS_Trees_BU': 10,
    'DIS_Coast_BU': 10,
    'Pools': 5,
    'Yard_Debris_PA': 10,
    'DIS_WaterBody_BU': 10
}

def calculate_secondary_risk_score(row):
    # Calculate the risk score for the row based on the weighted sum of secondary features
    risk_score = sum(row[feature] * percentages[feature] / 100 for feature in percentages)
    return risk_score

# Calculate the risk score for each row in the DataFrame
df['Secondary_Risk_Score'] = df.apply(calculate_secondary_risk_score, axis=1)

# Print the DataFrame with the calculated secondary risk scores
print(df)


