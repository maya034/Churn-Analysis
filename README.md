# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 


Thank you for providing the abstract of the paper. Based on the abstract, I can provide a more detailed breakdown of the key concepts and methodologies discussed in the paper:

https://openacttexts.github.io/LDACourse1/index.html#why-loss-data-analytics




import pandas as pd

# Sample DataFrame (replace this with your actual DataFrame)
data = {
    'Primary_risk': [75, 80, 70, 85],
    'Secondary_Risk': [60, 55, 65, 50]
}

df = pd.DataFrame(data)

def calculate_total_score(row):
    # Define the weights for primary and secondary scores
    weight_primary = 0.75
    weight_secondary = 0.25

    # Calculate the total score for the row based on the specified weights
    total_score = (weight_primary * row['Primary_risk']) + (weight_secondary * row['Secondary_Risk'])

    return total_score

# Calculate the total score for each row in the DataFrame
df['Total_Score'] = df.apply(calculate_total_score, axis=1)

# Print the DataFrame with the calculated total scores
print(df)


