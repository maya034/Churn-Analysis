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






















Hi Raunaq,
I’ve completed and submitted my year-end goal comments in the system. When you get a chance, please do have a look.

I also wanted to reconnect on the discussion we had last year regarding role progression and compensation. Having completed close to three years at EXL and taking on increased ownership and responsibilities, I’m keen to understand the next steps and your guidance on growth, promotion, and a commensurate hike this cycle.

Looking forward to your feedback. Thanks.


Hi Raunaq,
I’ve completed and submitted my year-end goal comments. Please let me know whenever you get a chance to review them.

I also wanted to follow up on our discussion from last year around growth and progression. It’s been close to three years at EXL now, and I’ve taken on more ownership and responsibilities. I’d really appreciate your guidance on promotion and a suitable hike this cycle.

Thanks.







Employee Comments – Compliance

I have consistently adhered to EXL’s Code of Conduct, company policies, and all client-specific requirements throughout the year. All mandatory compliance and security trainings were completed within timelines. I ensured adherence to defined procedures, data governance standards, and delivery timelines, with no compliance or conduct-related issues raised during the review period.


Employee Comments – Development & Capability Building

I have built strong functional understanding of the email campaign process and shared this knowledge by conducting knowledge transfer sessions for team members, including training Abhishek on the end-to-end workflow. I also supported new joiners during onboarding by helping them set up required tools, understand client-specific procedures, and get familiar with the technical and process requirements. These efforts helped ensure smoother transitions and continuity within the team.



Employee Comments – Upskill Trainings

I actively participated in relevant trainings conducted on the HIG engagement and broader technical upskilling areas, including GitHub, Linux, data engineering concepts, and cloud fundamentals. I have been applying these learnings in my day-to-day work, particularly while exploring automation opportunities for the email process to improve efficiency and reduce manual effort. I continue to focus on strengthening my technical skillset to better support ongoing and future project requirements.


Employee Comments – Client Satisfaction

I have received positive feedback from the client for my work on the email process, particularly around accuracy, timeliness, and clarity of deliverables. Presentations and final outputs shared with the client stakeholders were well received and met evaluation expectations. I continue to work closely with the client and internal managers on exploring automation opportunities for the email process and am actively building the required technical understanding to support these initiatives and enhance overall client value.


Employee Comments – Communication

I have consistently communicated information clearly and accurately during the email process through well-structured and concise emails. I proactively raised questions and clarifications with the client whenever required and maintained effective verbal communication during discussions to ensure alignment. This helped in avoiding ambiguity, ensuring smooth execution, and maintaining clarity across stakeholders.


Overall Summary

Over the past year, I have demonstrated strong ownership and consistency in delivering high-quality outcomes across the HIG Marketing engagement. I independently managed critical components of the email process, handled ad-hoc client requirements, supported knowledge transfer within the team, and actively contributed toward process improvements and automation initiatives. I have consistently met delivery timelines while maintaining accuracy, compliance, and positive client feedback.

With close to three years at EXL and continued growth in my role as Assistant Manager – Data Science, I have progressively taken on responsibilities aligned with higher expectations, including end-to-end ownership, stakeholder communication, and mentoring support. I have also been actively upskilling in relevant technical areas to strengthen my contribution toward scalable and efficient solutions.

Based on prior discussions around career progression, I remain keen to continue growing within EXL and take on broader responsibilities at the Manager level. I believe my performance, ownership mindset, and commitment to continuous improvement position me well for the next level, and I look forward to feedback and guidance on progression and compensation aligned with my contributions.
