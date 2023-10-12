# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 


Thank you for providing the abstract of the paper. Based on the abstract, I can provide a more detailed breakdown of the key concepts and methodologies discussed in the paper:

https://openacttexts.github.io/LDACourse1/index.html#why-loss-data-analytics









  import pandas as pd

# Sample data with Roof_Material_RF and Roof_Condition_RF values (in percentages)
data = {'Roof_Material_RF': [80, 60, 100, 20],
        'Roof_Condition_RF': [90, 60, 40, 20]}
df = pd.DataFrame(data)

# Assign weights to each feature
weight_material = 0.7  # 70% weight for Roof_Material_RF
weight_condition = 0.3  # 30% weight for Roof_Condition_RF

# Calculate the combined risk as a weighted average of the percentages
df['Combined_Risk'] = (df['Roof_Material_RF'] * weight_material) + (df['Roof_Condition_RF'] * weight_condition)

# Print the resulting dataframe
print(df)
