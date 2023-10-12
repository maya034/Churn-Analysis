# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 


Thank you for providing the abstract of the paper. Based on the abstract, I can provide a more detailed breakdown of the key concepts and methodologies discussed in the paper:

https://openacttexts.github.io/LDACourse1/index.html#why-loss-data-analytics








import pandas as pd

# Sample data with distances to the closest building (in feet)
data = {'DIS_ClosestBuilding_BU': [1.0, 2.5, 4.0, 7.0, 10.0, 15.0, 0.5, 3.0, 5.0, 8.0, 12.0]}
df = pd.DataFrame(data)

# Define risk categories based on percentiles
low_risk_max = df['DIS_ClosestBuilding_BU'].quantile(0.25)
moderate_risk_max = df['DIS_ClosestBuilding_BU'].quantile(0.75)
high_risk_max = df['DIS_ClosestBuilding_BU'].quantile(0.75)

# Define a function to categorize distances into risk levels (closer is riskier)
def categorize_wildfire_risk(distance):
    if distance <= low_risk_max:
        return 'Very High Risk'
    elif low_risk_max < distance <= moderate_risk_max:
        return 'High Risk'
    elif moderate_risk_max < distance <= high_risk_max:
        return 'Moderate Risk'
    else:
        return 'Low Risk'

# Create a new feature 'Wildfire_Risk' based on distances
df['Wildfire_Risk'] = df['DIS_ClosestBuilding_BU'].apply(categorize_wildfire_risk)

# Print the resulting dataframe
print(df)
