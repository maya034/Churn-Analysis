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
