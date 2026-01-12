image# Telecom-Churn-Analysis Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention. Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). 


















1539 High St, Fort Myers, FL, USA
Lat Long
(26.649090, -81.852070)


GPS Coordinates
26° 38' 56.724'' N
81° 51' 7.452'' W















When considering various types of disasters like hurricanes, floods, and fires, the key damage attributes to annotate will vary depending on the nature of the disaster. Below is a detailed list of key damage attributes for each type of disaster, which can be used to annotate satellite images:

### 1. Hurricane Damage Attributes

**a. Roof Damage:**
- Missing shingles or tiles.
- Holes or punctures.
- Entire roof sections blown off.

**b. Structural Damage:**
- Collapsed walls.
- Visible interior structures (due to missing walls or roof sections).
- Tilted or leaning buildings.

**c. Debris:**
- Debris scattered around the property (e.g., tree limbs, building materials).
- Vehicles or large objects displaced.

**d. Water Damage:**
- Flooding around the property.
- Water lines or marks on buildings indicating water level rise.
- Damaged or submerged infrastructure (e.g., roads, bridges).

**e. Vegetation Damage:**
- Uprooted or broken trees.
- Damaged landscaping.

### 2. Flood Damage Attributes

**a. Standing Water:**
- Areas with visible standing water around or inside properties.
- Roads and paths covered with water.

**b. Water Lines:**
- Visible water lines on buildings indicating the height of floodwaters.
- Mud or silt deposits around the property.

**c. Structural Damage:**
- Walls or foundations weakened or collapsed due to water pressure.
- Buildings partially or completely submerged.

**d. Debris:**
- Floating debris around the property.
- Accumulated debris near water bodies or drainage systems.

**e. Infrastructure Damage:**
- Damaged roads and bridges.
- Submerged or eroded infrastructure.

### 3. Fire Damage Attributes

**a. Burnt Structures:**
- Completely burnt buildings.
- Partially burnt structures with visible scorch marks.

**b. Roof Damage:**
- Roof sections burnt or collapsed.
- Scorched or missing roofing materials.

**c. Smoke Damage:**
- Soot and smoke stains on buildings.
- Discoloration of walls and roofs due to smoke.

**d. Vegetation Damage:**
- Burnt or charred trees and plants.
- Burnt ground cover or grass.

**e. Debris:**
- Rubble and ash piles.
- Burnt remnants of structures or vehicles.

### 4. General Damage Attributes (Applicable to All Disasters)

**a. Infrastructure Damage:**
- Damaged roads, bridges, and utility poles.
- Broken or damaged utility lines (e.g., power lines, water pipes).

**b. Environmental Impact:**
- Erosion and landslides.
- Changes in landscape due to the disaster.

**c. Human Activity Indicators:**
- Emergency response vehicles and personnel.
- Temporary shelters or relief camps.

### Annotating Damage Attributes

**1. Bounding Boxes:**
- Draw rectangular boxes around damaged areas.
- Label each box with the appropriate damage type (e.g., "Roof Damage", "Flooding").

**2. Polygons:**
- Draw precise polygon shapes around irregularly shaped damaged areas.
- Useful for detailed annotations of complex damage patterns.

**3. Segmentation Masks:**
- Create pixel-level annotations where each pixel is classified as part of a specific damage type.
- Provides the most detailed and precise representation of damage.

### Example Annotation Workflow

**1. Tools:**
- Use annotation tools like Labelbox, CVAT, or VGG Image Annotator (VIA).

**2. Steps:**
- **Load Image:** Open the satellite image in the annotation tool.
- **Select Tool:** Choose the appropriate annotation tool (bounding box, polygon, segmentation).
- **Draw Annotations:** Mark the areas of damage and label them with the corresponding damage type.
- **Save Annotations:** Save the annotations in a structured format (JSON, XML).

**3. Quality Control:**
- **Review Annotations:** Ensure annotations are accurate and consistent.
- **Validate with Experts:** Have domain experts review a subset of annotations to ensure quality.
- **Iterative Refinement:** Continuously refine annotations based on feedback.

By comprehensively annotating these key damage attributes, you can create a rich dataset that captures the impact of various disasters. This dataset can then be used to train models to automatically detect and assess damage in new satellite images. If you need more specific examples or further details on any part of this process, let me know!





Training data shape: (700, 807)
Testing data shape: (300, 807)
Classification Report:
              precision    recall  f1-score   support

        Easy       0.00      0.00      0.00         4
        Hard       0.98      0.96      0.97        53
      Medium       0.98      1.00      0.99       243

    accuracy                           0.98       300
   macro avg       0.65      0.65      0.65       300
weighted avg       0.96      0.98      0.97       300

Confusion Matrix:
[[  0   0   4]
 [  0  51   2]
 [  0   1 242]]





 https://www.dezeen.com/2019/01/04/north-fork-bluff-house-long-island-res4/
# Create a new presentation
presentation = Presentation()

# Add a title slide
title_slide_layout = presentation.slide_layouts[0]
slide = presentation.slides.add_slide(title_slide_layout)
title = slide.shapes.title
subtitle = slide.placeholders[1]

title.text = "Mayank Kumar"
subtitle.text = "Profile"

# Add a slide for the summary and key projects
bullet_slide_layout = presentation.slide_layouts[1]
slide = presentation.slides.add_slide(bullet_slide_layout)
shapes = slide.shapes
title_shape = shapes.title
body_shape = shapes.placeholders[1]

title_shape.text = "Summary and Key Projects"

# Add the content to the slide
tf = body_shape.text_frame
p = tf.add_paragraph()
p.text = "Summary\nAnalytics professional with 3+ years of experience in domain of analytics - predictive as well as descriptive, data and information management."

p = tf.add_paragraph()
p.text = "\nKey Projects"
p.level = 0

# Adding Fire Insurance Risk Score at the top
projects = [
    {
        "title": "Fire Insurance Risk Score",
        "details": """
Tags: Research, Methodology, Risk Scoring
Objective: To develop a risk scoring model for fire insurance specific to US properties by researching competitors and creating a unique methodology.
Data Preparation: Conducted extensive research on competitor methodologies and existing risk scoring models in the industry. Collected and analyzed relevant data including historical fire incidents, property characteristics, and geographical factors.
Analysis: Explored various methods and techniques to develop an accurate risk score. Conducted multiple experiments and evaluations to identify the most effective approach.
Outcome: Successfully developed a robust risk scoring model that provides accurate fire risk assessments for US properties. The model incorporates comprehensive data analysis and competitor insights, ensuring reliable risk evaluations.
""".strip()
    },
    {
        "title": "Citroen brand sentiment analysis",
        "details": """
Tags: EDA, Python, Binary Classification, NLP, NER, Spacy
Objective: To predict the sentiment of twitter users associated with a particular tweet of Citroen brand to devise better marketing strategy for the brand.
Data preparation: Data was fetched from twitter, the dataset had features such as username, location, screen name, tweet at, the original tweet, etc. We had used pipelines on the data such as text mining, text normalization, text vectorization in text mining we did basic EDA of original tweet feature such that checking often used words via word cloud. In Text Normalization, we implemented several text preprocessing techniques such as text cleaning (Replacing RT tag, replaced emojis with meaningful text, ...
Data analysis: Later in-Text Vectorization, we used TFIDF to convert all the meaningful words into a sparse matrix. Generated optimal document words sparse matrix.
Model deployment: Experimented with different classification algorithms such as Random Forest, XGBoost to identify the feedback of Users and obtained 0.75 as F1 score which was considered as our evaluation metric.
""".strip()
    },
    {
        "title": "Health insurance cross sale prediction",
        "details": """
Tags: EDA, Hyperparameter Tuning, SHAP, GridsarearCV, AUC-ROC, Logistic Regression, XGBoost, Random Forest, Feature Engineering, F1 Score, Recall, Precision
Objective: To prognosticate whether the policy holder from past years will additionally be intrigued with vehicle insurance provided by the company.
Data Preparation: Merged 5 different dataset (yes & no - vehicle data, policy data, customer data, etc.) into a unified master dataset. We had features such as vehicle age, demographic age, region code, policy premium, surrounding channel, policy sales channel, previously insured, avg time to settle a claim, avg cost per claim, annual rate, etc. Organized the data by filling out the missing values from different data set and replacing errors.
Data analysis: Dataset was imbalanced with target 0.85% and target 1 is 15%. So, we used SMOTE to oversample the minority class. Reduced the count of relevant features to 30 by merging few of them and removing less important features.
Predictive modelling: Developed binary classification algorithm such as logistic regression, random forest and XG boost and carried out hyperparameter tuning using GridSearchCV optimization and achieved an F1 score of 72%.
""".strip()
    },
    {
        "title": "Quality Site Visitors",
        "details": """
Tags: Data Analysis, SQL, Python, Pandas, Big query, Digital Marketing
Objective: To understand the site analytics for the Adobe warehouse site and analyze the site score.
Data Preparation: Pulled out data using SQL from Adobe Data Warehouse and stored it in Big Query for further analysis. We required few data from the trackers for newly advertisers such as user Id, location, number of visits on site, visit date, etc.
Data Analysis: Used Shapely method to understand conversion activities and touch points based on daily site count contribution to conversion. Also, worked on building an intuition that a particular channel is better than other. We build a pipeline where the advertiser need not just pay activity Ids, total activity Ids, site Ids, etc. but have all Ids converted. We get a visualization of touchpoints analysis showing all the touchpoints (site) with shapely scores.
""".strip()
    }
]

for project in projects:
    p = tf.add_paragraph()
    p.text = project["title"]
    p.level = 1
    p = tf.add_paragraph()
    p.text = project["details"]
    p.level = 2

# Ensure the text fits within a single page
for paragraph in tf.paragraphs:
    if len(paragraph.text) > 1000:
        paragraph.text = paragraph.text[:1000] + "..."

# Save the presentation
updated_ppt_path = "/mnt/data/Updated_Mayank_Kumar_Profile_Top_Fire.pptx"
presentation.save(updated_ppt_path)

updated_ppt_path






















Over the year, I have consistently delivered on my project responsibilities with a strong focus on quality, accuracy, and business impact. I initially worked closely with Chirag to understand the email campaign process end-to-end and gradually took complete ownership of the email execution independently. Since then, I have been responsible for executing the email process on a recurring basis, ensuring timely delivery and high accuracy across all runs.

In addition to the core email workflow, I independently handled multiple ad-hoc requests from the client, often within tight timelines. These ad-hoc activities required quick analysis, execution, and validation, and I ensured that all such deliverables were completed accurately and aligned with client expectations. During peak months, when multiple or repeat email runs were required due to additional business needs, I supported the team by executing the process multiple times without impacting quality or timelines.

I also proactively started contributing toward automation initiatives to improve efficiency and reduce manual effort in the email process. This included understanding the existing workflow, identifying opportunities for optimization, and supporting initial automation efforts alongside ongoing deliveries.

There were instances where last-minute changes or fixes were required, and I remained flexible with working hours to ensure uninterrupted delivery. I consistently demonstrated ownership by supporting extended working hours when needed to meet business deadlines and ensure smooth client outcomes.

Overall, my contributions helped maintain consistent delivery, accuracy, and operational stability for the HIG Marketing email process, while also supporting incremental improvements and addressing evolving client requirements. I continue to focus on strengthening my consulting mindset by balancing delivery ownership with process improvement and stakeholder support.
