# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 






import requests 
from bs4 import BeautifulSoup
# Define the URL of the page you want to scrape 
url = 'https://www.realtor.com/' 
# Send an HTTP request to the website 
response = requests.get(url)
# Check if the request was successful 
if response.status_code == 200: 
# Parse the HTML content of the page
  soup = BeautifulSoup(response.text, 'html.parser') 
# Find the elements that contain the data you want 
  property_listings = soup.find_all('div', class_='property-listing') 
  for listing in property_listings:
# Extract full address 
    address = listing.find('span', class_='address').text 
# Extract zip code 
    zip_code = listing.find('span', class_='zip-code').text 
# Extract county 
    county = listing.find('span', class_='county').text
# Extract date 
    date = listing.find('span', class_='date').text 
# Extract building value 
    building_value = listing.find('span', class_='building-value').text 
# Print or save the extracted data as needed 
    print(f"Address: {address}") 
    print(f"Zip Code: {zip_code}") 
    print(f"County: {county}") 
    print(f"Date: {date}") 
    print(f"Building Value: {building_value}") 
else: 
  print("Failed to retrieve the page. Status code:", response.status_code)


https://checkmyhomevalue.typeform.com/denver?gclid=CjwKCAjwnOipBhBQEiwACyGLuitaoz-8fUHTwTNfH2j6gLBxcJSTUY6y7ijhNzU19hT1MSzhqOO_zhoCtUAQAvD_BwE&typeform-source=www.google.com
