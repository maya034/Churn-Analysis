# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 


Thank you for providing the abstract of the paper. Based on the abstract, I can provide a more detailed breakdown of the key concepts and methodologies discussed in the paper:

https://openacttexts.github.io/LDACourse1/index.html#why-loss-data-analytics

import pandas as pd

# Read the Excel file
file_path = 'your_excel_file.xlsx'  # Update with your file path
df = pd.read_excel(file_path)

# Define your initial buckets and corresponding mapped values
initial_buckets = [(0, 500), (501, 525), (526, 550), (551, 575), (576, 600),
                   # ... Add more initial buckets here ...
                   (2976, 3000)]

# Define your extended buckets and corresponding mapped values
extended_buckets = [(3001, 3200), (3201, 3400), (3401, 3600),
                    # ... Add more extended buckets here ...
                    (15601, 15800)]

# Create a mapping dictionary for initial buckets
initial_mapping = {i: 0.959 - (i * 0.0022) for i in range(len(initial_buckets))}

# Create a mapping dictionary for extended buckets
extended_mapping = {i + len(initial_buckets): value for i, value in enumerate([
    1.1244, 1.1336, 1.1428, 1.1520, 1.1612, 1.1704, 1.1796, 1.1888, 1.1980, 1.2072,
    1.2159, 1.2246, 1.2333, 1.2420, 1.2507, 1.2594, 1.2681, 1.2768, 1.2855, 1.2942,
    1.3029, 1.3116, 1.3203, 1.3290, 1.3377, 1.3464, 1.3551, 1.3618, 1.3685, 1.3752,
    1.3819, 1.3886, 1.3953, 1.4020, 1.4087, 1.4154, 1.4221, 1.4288, 1.4355, 1.4422,
    1.4489, 1.4556, 1.4623, 1.4690, 1.4757, 1.4824, 1.4891, 1.4958, 1.5025, 1.5092,
    1.5159, 1.5226, 1.5293, 1.5360, 1.5427, 1.5494, 1.5561, 1.5628, 1.5695, 1.5762,
    1.5829, 1.5896, 1.5908, 1.5920])}

# Function to map values based on initial buckets
def map_initial_square_footage(value):
    for i, (lower, upper) in enumerate(initial_buckets):
        if lower <= value <= upper:
            return initial_mapping[i]

# Function to map values based on extended buckets
def map_extended_square_footage(value):
    # Calculate the index for the extended buckets based on the value
    index = (value - 3000) // 200 + len(initial_buckets)

    if len(initial_buckets) <= index < len(initial_buckets) + len(extended_mapping):
        return extended_mapping[index]

    return None

# Apply the mapping functions to the 'Square_Footage' column
df['Mapped_Value'] = df['Square_Footage'].apply(
    lambda x: map_initial_square_footage(x) if x <= 3000 else map_extended_square_footage(x)
)

# Save the updated DataFrame back to the Excel file
df.to_excel(file_path, index=False)

----------------------------------------------------------------------------------------------------------------------
import pandas as pd

# Read the Excel file
file_path = 'your_excel_file.xlsx'  # Update with your file path
df = pd.read_excel(file_path)

# Define your initial buckets and corresponding mapped values
initial_buckets = [(0, 500), (501, 525), (526, 550), (551, 575), (576, 600),
                   # ... Add more initial buckets here ...
                   (2976, 3000)]

# Mapping values for initial buckets
initial_mapping_values = [
    0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959,
    0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959,
    0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959, 0.959,
    0.959, 0.9612, 0.9634, 0.9656, 0.9678, 0.9700, 0.9722, 0.9744, 0.9766,
    0.9788, 0.9810, 0.9832, 0.9854, 0.9876, 0.9898, 0.9920, 0.9942, 0.9964,
    0.9986, 1.0008, 1.0030, 1.0052, 1.0074, 1.0096, 1.0118, 1.0140, 1.0162,
    1.0184, 1.0206, 1.0228, 1.0250, 1.0272, 1.0294, 1.0316, 1.0338, 1.0360,
    1.0382, 1.0404, 1.0426, 1.0448, 1.0470, 1.0492, 1.0514, 1.0536, 1.0558,
    1.0580, 1.0602, 1.0624, 1.0646, 1.0668, 1.0690, 1.0712, 1.0734, 1.0756,
    1.0778, 1.0800, 1.0822, 1.0844, 1.0866, 1.0888, 1.0910, 1.0932, 1.0954,
    1.0976, 1.0998, 1.1020, 1.1042, 1.1064, 1.1086, 1.1108, 1.1130, 1.1152,
    # Add more values here
]

# Create a mapping dictionary for initial buckets
initial_mapping = {i: initial_mapping_values[i] for i in range(len(initial_buckets))}

# Function to map values based on initial buckets
def map_initial_square_footage(value):
    for i, (lower, upper) in enumerate(initial_buckets):
        if lower <= value <= upper:
            return initial_mapping[i]

# Function to map values based on extended buckets
def map_extended_square_footage(value):
    # Calculate the index for the extended buckets based on the value
    index = (value - 3000) // 200 + len(initial_buckets)

    # ... Continue with the extended_mapping as before ...

# Create a new column for the mapped values
df['Mapped_Value'] = df['Square_Footage'].apply(
    lambda x: map_initial_square_footage(x) if x <= 3000 else map_extended_square_footage(x)
)

# Save the updated DataFrame back to the Excel file
df.to_excel(file_path, index=False)
