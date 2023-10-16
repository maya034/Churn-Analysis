# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 


Thank you for providing the abstract of the paper. Based on the abstract, I can provide a more detailed breakdown of the key concepts and methodologies discussed in the paper:

https://openacttexts.github.io/LDACourse1/index.html#why-loss-data-analytics









import pandas as pd

# Sample DataFrame (replace this with your actual DataFrame)
data = {
    'Construction': [4, 3, 2, 5],
    'Occupancy': [1, 2, 3, 1],
    'Year_built': [1990, 1980, 2000, 1975],
    'No of Building': [1, 2, 1, 1],
    'Square_Footage': [3000, 2500, 2000, 3500],
    'Story_Num_BU': [2, 1, 2, 3]
}
df = pd.DataFrame(data)

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
df['Risk_Score'] = df.apply(calculate_primary_risk_score, axis=1)

# Print the DataFrame with the calculated risk scores
print(df)























primary		100	convert it to 75												
occupany		15	residential-30%			secondary(25%)	100				DIS_Vegetation_BU	risk			
construction		45				Roof_Type_RF/geometry	5				10km	very high	100		
yearbuilt		10				Roof_Condition_RF					10-50km	high	80		
no of building	ex dlf	5				Roof_Material_RF	10				50-200km	risky	60		
floor area/square foot area		15				Pool_Enclosure_PA	5				200-500	less risky	20		
stories		10				DIS_Firestation_BU	10				>500	no risk	0		
						Chimneys_RF	5				wind direction 	?			
primary	secondary					Roof_Evidence_RF					wind storm part				
75	25				exclude	Solar_Panels_RF	5								
6 fields						Air_Conditioner_RF	5								
						Skylights_RF	5								
															
						Tree_Overhang_RF	10								
						DIS_ClosestBuilding_BU	10								
						DIS_Trees_BU	10								
															
						Pool_AR_PA									
						Temporary_pool_PA									
						Trampoline_PA									
						Yard_Debris_PA	10								
						DIS_WaterBody_BU	10								
															
						BUILDING WALL TYPE	NOT THR	10 IMP OVERHANG CLOSEST BUILD 5-5							
															
				risk score 											
	x	y	x+y=100	(x+y)*disbu											
															
![image](https://github.com/maya034/Churn-Analysis/assets/61015843/7fe6942d-3ee9-4fce-9117-a0b674c57f36)
