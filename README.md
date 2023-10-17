# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 


Thank you for providing the abstract of the paper. Based on the abstract, I can provide a more detailed breakdown of the key concepts and methodologies discussed in the paper:

https://openacttexts.github.io/LDACourse1/index.html#why-loss-data-analytics




import pandas as pd

# Sample DataFrame (replace this with your actual DataFrame)
data = {
    'Primary_Risk': [75, 80, 70, 85],
    'Secondary_Risk': [60, 55, 65, 50],
    'DIS_Vegetation_BU': [300, 1000, 10000, 30000]  # Distance in feet
}

df = pd.DataFrame(data)

def feet_to_km(feet):
    # Convert feet to kilometers (1 foot = 0.0003048 kilometers)
    return feet * 0.0003048

def calculate_final_score(row):
    # Convert the distance in feet to kilometers
    distance_km = feet_to_km(row['DIS_Vegetation_BU'])
    
    # Define the weights for distance ranges in kilometers
    if distance_km <= 5:
        weight_vegetation = 1.0  # 100% Total_Score
    elif 5 < distance_km <= 50:
        weight_vegetation = 0.85  # 85% Total_Score
    elif 50 < distance_km <= 200:
        weight_vegetation = 0.6  # 60% Total_Score
    elif 200 < distance_km <= 500:
        weight_vegetation = 0.2  # 20% Total_Score
    else:
        weight_vegetation = 0.0  # 0% Total_Score

    # Calculate the final score based on the weighted Total_Score
    final_score = weight_vegetation * row['Total_Score']

    return final_score

# Calculate the final score for each row in the DataFrame
df['Final_Score'] = df.apply(calculate_final_score, axis=1)

# Print the DataFrame with the calculated final scores
print(df)
