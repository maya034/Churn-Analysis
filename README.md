![image](https://github.com/maya034/Churn-Analysis/assets/61015843/4747de26-fb67-4dc6-92ee-ebfc5f3aa0ac)# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 











import json

# Load the provided JSON annotations
with open('annotations.json', 'r') as f:
    annotations = json.load(f)

# Initialize COCO format dictionary
coco_data = {
    "info": {},
    "licenses": [],
    "categories": [],
    "images": [],
    "annotations": []
}

# Define category mapping
category_mapping = {
    "roof": 1,
    "tree_overhang": 2,
    "chimney": 3,
    "vegetation": 4,
    "debris": 5
}

# Add categories to COCO data
for label, category_id in category_mapping.items():
    coco_data["categories"].append({
        "id": category_id,
        "name": label,
        "supercategory": "object"
    })

# Iterate through annotations and convert to COCO format
image_id = 1
annotation_id = 1
for annotation in annotations["shapes"]:
    # Extract label, points, and category_id
    label = annotation["label"]
    points = annotation["points"]
    category_id = category_mapping.get(label)
    
    # Add image info to COCO data
    coco_data["images"].append({
        "id": image_id,
        "file_name": "image_{}.jpg".format(image_id),
        "width": 500,  # Example width, replace with actual image width
        "height": 500  # Example height, replace with actual image height
    })
    
    # Add annotation to COCO data
    coco_data["annotations"].append({
        "id": annotation_id,
        "image_id": image_id,
        "category_id": category_id,
        "segmentation": [list(map(int, point)) for point in points],  # Convert points to integers
        "area": 0,  # Area can be calculated if needed
        "bbox": [],  # Bounding box can be calculated if needed
        "iscrowd": 0  # Indicate if the annotation represents a crowd
    })
    
    # Increment image_id and annotation_id
    image_id += 1
    annotation_id += 1

# Save the converted annotations to a JSON file
with open('annotations_coco.json', 'w') as f:
    json.dump(coco_data, f)



