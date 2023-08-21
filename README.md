# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 


Thank you for providing the abstract of the paper. Based on the abstract, I can provide a more detailed breakdown of the key concepts and methodologies discussed in the paper:

https://openacttexts.github.io/LDACourse1/index.html#why-loss-data-analytics


import pandas as pd
from uszipcode import SearchEngine

class CountyLocator:
    def __init__(self, excel_file):
        self.excel_data = pd.read_excel(excel_file)
        self.search = SearchEngine()  # Using simple_zipcode to reduce data size

    def get_county_from_address(self, address):
        try:
            location_info = self.search.by_full_address(address)
        except Exception as e:
            return f"Error: {e}"

        if not location_info:
            return "Location not found."

        county = location_info[0].county
        if county:
            return county
        else:
            return "County information not available for this location."
    
    
    def get_county_from_coords(self, latitude, longitude):
        try:
            zipcode = self.search.by_coordinates(latitude, longitude, radius=10, returns=1)
            if zipcode:
                county = zipcode[0].county
                if county:
                    return county
        except Exception as e:
            return f"Error: {e}"

        return "County information not available for this location."

    def get_county_info_based_on_input(self, address=None, latitude=None, longitude=None):
        if address:
            return self.get_county_from_address(address)
        elif latitude is not None and longitude is not None:
            return self.get_county_from_coords(latitude, longitude)
        else:
            return "Not valid. Please provide either an address or both latitude and longitude."

    def get_score_from_county(self, county_output):
        if county_output and county_output != "County information not available for this location.":
            matched_row = self.excel_data[self.excel_data['county'] == county_output]

            if not matched_row.empty:
                total_score = matched_row['total_score'].values[0]
                score_category = matched_row['score_category'].values[0]

                return total_score, score_category

        return None, None

    # Rest of the class remains unchanged...

# Test examples
excel_file = "F:\CARDIO\Book1.xlsx"  # Replace with the path to your Excel file
county_locator = CountyLocator(excel_file)

address = "1600 Amphitheatre Parkway, Mountain View, CA"
county_output = county_locator.get_county_info_based_on_input(address=address)

total_score, score_category = county_locator.get_score_from_county(county_output)

if total_score and score_category:
    print(f"Total Score: {total_score}")
    print(f"Score Category: {score_category}")
else:
    print("County not found in the Excel data or no match found.")
