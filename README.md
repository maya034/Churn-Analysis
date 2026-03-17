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






-- -------------------------------------------------------
-- File: select-inforce-policies-from-chub-by-client-id.sql
-- Cell 150 in old code.
-- -------------------------------------------------------

!print -------------------------------------------------------
!print -- Table: emsel_inforce_policies_from_chub_by_client_id
!print -- Time: 5 seconds.
!print -------------------------------------------------------

!set quiet=True

CREATE OR REPLACE TABLE emsel_inforce_policies_from_chub_by_client_id AS
SELECT DISTINCT
    a.client_id                        client_id,
    a.policy_nbr                       policy_nbr,
    a.plcy_efdt                        pol_eff_dt,
    a.plcy_exdt                        pol_exp_dt,
    NULL                               qcn,
    upper(b.rev_email_addr)            acct_email_addr,
    NULL                               first_nm,
    NULL                               last_nm,
    a.named_insured_state_cd           nm_insd_st_cd,
    NULL                               secnd_nm_insd_prty_id,
    1                                  is_inforce,
    'CHUB'                             src_sys_cd,
    NULL                               me_dt
FROM PRD_ENT_CHUB_DB.EDW_DM_DLV_PL.CUST_HUB_INFORCE_PL_POL_VW a,
    (SELECT DISTINCT
         cp_extrnl_sys_key_id,
         rev_email_addr
     FROM PRD_ENT_CHUB_DB.EDW_DM_DLV_PL.CUST_HUB_EMAIL_PL_VW
     WHERE rev_email_valid_ind = 'Y'
    ) b
WHERE lob = 'AUTO'
AND   a.client_id = b.cp_extrnl_sys_key_id(+)
;

!set quiet=False

select count(*) row_count
from emsel_inforce_policies_from_chub_by_client_id;

select *
from emsel_inforce_policies_from_chub_by_client_id
where client_id is not null
and   acct_email_addr is not null
order by 1 desc limit 5;





























Good. Now run this UNION file:

```sql
CREATE OR REPLACE TABLE emsel_inforce_policies_by_client_id AS

SELECT DISTINCT
    client_id,
    policy_nbr,
    pol_eff_dt,
    pol_exp_dt,
    qcn,
    email_addr,
    first_nm,
    last_nm,
    nm_insd_st_cd,
    secnd_nm_insd_prty_id,
    is_inforce,
    src_sys_cd,
    me_dt
FROM emsel_inforce_policies_from_chub_by_client_id

UNION

SELECT DISTINCT
    client_id,
    policy_nbr,
    pol_eff_dt,
    pol_exp_dt,
    qcn,
    email_addr,
    first_nm,
    last_nm,
    nm_insd_st_cd,
    secnd_nm_insd_prty_id,
    is_inforce,
    src_sys_cd,
    me_dt
FROM emsel_inforce_policies_from_dcpa_by_client_id
;

select count(*) row_count from emsel_inforce_policies_by_client_id;
```

Share the row count. 📸



























































CREATE OR REPLACE TABLE emsel_cancelled_policies_by_client_id AS

SELECT DISTINCT
    client_id,
    policy_nbr,
    rev_email_addr          email_addr,
    sfmc_held,
    matched_ind,
    first_nm,
    last_nm,
    canc_eff_dt,
    nm_insd_st_cd,
    delivery_status_desc,
    internal_engagement_desc,
    external_engagement_desc,
    internal_recency_dt,
    external_recency_dt,
    email_domain_owner,
    ap_best_day_of_wk_nm,
    ap_best_time_of_day,
    ap_optimal_send_time,
    ap_frequency,
    audience_pnt_score_num,
    sfmc_email_status,
    is_cancelled,
    src_sys_cd,
    NULL                    status
FROM emsel_cancelled_policies_from_chub_by_client_id

UNION

SELECT DISTINCT
    client_id,
    policy_nbr,
    acct_email_addr         email_addr,
    NULL                    sfmc_held,
    NULL                    matched_ind,
    first_nm,
    last_nm,
    canc_eff_dt,
    state_cd                nm_insd_st_cd,
    NULL                    delivery_status_desc,
    NULL                    internal_engagement_desc,
    NULL                    external_engagement_desc,
    NULL                    internal_recency_dt,
    NULL                    external_recency_dt,
    NULL                    email_domain_owner,
    NULL                    ap_best_day_of_wk_nm,
    NULL                    ap_best_time_of_day,
    NULL                    ap_optimal_send_time,
    NULL                    ap_frequency,
    NULL                    audience_pnt_score_num,
    NULL                    sfmc_email_status,
    is_cancelled,
    src_sys_cd,
    status
FROM emsel_cancelled_policies_from_dcpa_by_client_id
;

select count(*) row_count from emsel_cancelled_policies_by_client_id;
select * from emsel_cancelled_policies_by_client_id order by 1 desc limit 5;







































SELECT
    DISTINCT CF.ACCOUNT_ID          client_id,
    CF.POL_NBR                      policy_nbr,
    AD.ACCT_EMAIL_ADDR              acct_email_addr,
    NULL                            sfmc_held,
    NULL                            matched_ind,
    AD.ACCT_FIRST_NM                first_nm,
    AD.ACCT_LAST_NM                 last_nm,
    NULL                            canc_eff_dt,
    NULL                            state_cd,
    NULL                            delivery_status_desc,
    NULL                            internal_engagement_desc,
    NULL                            external_engagement_desc,
    NULL                            internal_recency_dt,
    NULL                            external_recency_dt,
    NULL                            email_domain_owner,
    NULL                            ap_best_day_of_wk_nm,
    NULL                            ap_best_time_of_day,
    NULL                            ap_optimal_send_time,
    NULL                            ap_frequency,
    NULL                            audience_pnt_score_num,
    NULL                            sfmc_email_status,
    1                               is_cancelled,
    'PLDW'                          src_sys_cd,
    POLICY_TAB.POL_STATUS_CD        status
FROM
    PRD_PL_DB.APP_PLA_CLIENT.CONTRACT_FACT CF,
    PRD_PL_DB.APP_PLA_CLIENT.ACCOUNT_DIM AD,
    POLICY_TAB
WHERE
    AD.ACCOUNT_ID = CF.ACCOUNT_ID
    AND CF.REGIONAL_OFFICE_CD || CF.POL_SYMBOL_CD || CF.POL_NBR = POLICY_TAB.POL_ID
    AND POLICY_TAB.BUS_UNIT_ABBR = 'AARP'



1. b.rev_email_addr → aliased as acct_email_addr
2. a.nm_insd_st_cd  → aliased as state_cd
3. NULL status      → added
4. NULL regional_office_cd → added
5. NULL pol_symbol_cd      → added
6. NULL acct_home_phone_nbr → added
7. NULL bus_unit_abbr       → added
8. CAST(client_id AS VARCHAR) → added for data type match


1. Columns reordered to match CHUB exactly
2. NULL sfmc_held, matched_ind added
3. NULL for all AP scoring columns added
4. NULL regional_office_cd → added
5. NULL pol_symbol_cd      → added
6. NULL acct_home_phone_nbr → added
7. NULL bus_unit_abbr       → added
8. CAST(client_id AS VARCHAR) → added for data type match

1. SELECT reordered to match CHUB/DCPA column order
2. NULL added for all missing columns
3. Real values kept for:
   CF.REGIONAL_OFFICE_CD
   CF.POL_SYMBOL_CD
   AD.ACCT_HOME_PHONE_NBR
   POLICY_TAB.BUS_UNIT_ABBR
4. CAST(account_id AS VARCHAR) → added as client_id
5. 1 is_cancelled added
6. 'PLDW' src_sys_cd added

CHUB:   5,536,955
DCPA:     393,780
PLDW:   6,534,303
─────────────────
TOTAL: 12,465,038


"I completed the cancelled policies UNION table.
All 3 sources — CHUB, DCPA, and PLDW — are now
combined into emsel_cancelled_policies_by_client_id
using SELECT * as requested.

Key fixes needed were:
1. Column alignment across all 3 tables
2. Data type mismatch on client_id — PLDW uses
   alphanumeric IDs while CHUB/DCPA use numeric
   — resolved with VARCHAR cast
3. Had to re-run all 3 branch tables before
   the UNION could run cleanly

Final count: 12.4 million cancelled records." ✅
