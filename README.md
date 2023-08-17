# Telecom-Churn-Analysis
Exploring and analyzing the data to discover key factors responsible for customer churn and come up with ways/recommendations to ensure customer retention.
Predict behavior to retain customers. You can analyze all relevant customer data and develop focused customer retention programs. Each row represents a customer, each column contains customer’s attributes described on the column Metadata. The raw data contains 7043 rows (customers) and 21 columns (features). The “Churn” column is our 


Thank you for providing the abstract of the paper. Based on the abstract, I can provide a more detailed breakdown of the key concepts and methodologies discussed in the paper:

1. **Introduction and Problem Statement:**
   Premium pricing in general insurance is a complex task. The paper focuses on how the frequency (how often) and severity (size or amount) of insurance claims impact the premium pricing process. The challenge is to accurately model past and current claim data to project future claim experience for policy portfolios.

2. **Frequency and Severity of Claims:**
   - **Frequency:** How often insurance claims occur for a specific policy or portfolio.
   - **Severity:** The size or amount of loss associated with each claim.

3. **Modeling Past Claim Data:**
   To project future claim amounts and assess risk, insurers need to model historical claim data. The study proposes a framework for selecting the appropriate probability distribution for modeling the frequency and severity of claims.

4. **Maximum Likelihood Estimation (MLE):**
   The paper suggests using the maximum likelihood method to estimate the parameters of the chosen probability distribution. MLE is a common statistical technique for estimating the parameters that make the observed data most probable under the chosen distribution.

5. **Goodness of Fit Testing:**
   - **Frequency Distributions:** The goodness of fit for frequency distributions is assessed using the chi-square test. This test compares the observed and expected frequencies in different bins.
   - **Severity Distributions:** The Anderson-Darling test is used to assess the goodness of fit for severity claim distributions. This test is used to determine how well a given distribution fits the observed data.

6. **Model Selection and Projection:**
   The study employs the Akaike Information Criterion (AIC) to choose the best-fitting models among competing frequency and severity models. AIC is a metric used to compare models based on their fit and complexity.

7. **Selected Models:**
   - **Frequency Models:** The Negative Binomial model is chosen as the best-fitting model for modeling claim frequency.
   - **Severity Models:** The Pareto distribution is selected as the best-fitting model for modeling claim severity.

8. **Projection and Future Estimation:**
   The selected models are used for projecting future claim amounts per risk in the coming year. This projection helps insurers estimate the potential claim payouts they might have to make.

Overall, the paper focuses on developing a framework for accurately modeling insurance claim frequency and severity, selecting appropriate probability distributions, estimating distribution parameters using MLE, assessing goodness of fit, and using the best-fitting models for projecting future claim amounts. This information is crucial for insurers to effectively price premiums and manage risk within their portfolios.






The introduction section of the paper provides context and motivation for the study, explaining the limitations of the classical Bonus-Malus System and the need to simultaneously model both the frequency and severity of insurance claims. Here's a breakdown of the key points made in this section:

1. **Classical Bonus-Malus System:**
   - In the classical Bonus-Malus System, the transition rule for insurance policyholders is based solely on the frequency of claims. This means that the system does not take into account the severity of individual claims.
   - This frequency-driven transition rule is commonly used in many jurisdictions and assumes that frequency and severity are independent. It allows for easy premium calculation as the product of mean frequency and mean severity.

2. **Dependence Between Frequency and Severity:**
   - The assumption of independence between frequency and severity, which is rooted in the classical collective risk model, is theoretically convenient but might not hold in reality.
   - Recent empirical studies (references 4 and 5) have shown that there is a statistically significant dependence between the frequency and severity of claims in auto insurance. This finding challenges the validity of the frequency-driven transition rule.

3. **Need for Dependent Models:**
   - The empirical evidence of dependence between frequency and severity indicates the need to extend the classical collective risk model to incorporate a more realistic dependence structure between these two variables.
   - Several studies have explored different methods to model this dependence, including copula-based models, two-step frequency-severity models, and bivariate random effect-based models.

4. **Bivariate Random Effect Model:**
   - The bivariate random effect model is commonly used in insurance rate-setting due to its mathematical tractability.
   - This model involves two random effect components: one to capture the dependence among frequencies and another to capture the dependence among individual severities.
   - These random effects are jointly modeled to induce the dependence between frequency and severity at the distribution level.

5. **Global Trends in Modeling Frequency and Severity:**
   - The simultaneous modeling of both frequency and severity of insurance claims is a global trend in the insurance industry.
   - Researchers and practitioners are actively working on statistical methods to accommodate various dependent structures in collective risk models.

In essence, the introduction highlights the limitations of the classical frequency-driven Bonus-Malus System, emphasizes the significance of the empirical evidence showing dependence between frequency and severity, and introduces the concept of bivariate random effect models as a way to address this dependence. It also underscores the broader global trend of incorporating dependent structures in insurance claim modeling.

The "Literature Review" section of the paper summarizes previous studies related to the severity and frequency of insurance claims. Here's a breakdown of the key points and findings from the review:

**2.1. Review of Previous Studies on Severity of Insurance Claims:**
- Reference 13 conducted a study that focused on comparing risk classification methods for claims severity.
- The study evaluated several risk classification methods using a weighted equation that calculated the difference between observed and fitted values.
- The weighted equation estimated claim severities, which were essentially the total claim costs divided by the number of claims.
- The classical and regression fitting procedures yielded equal parameter estimates, with the regression procedure showing faster convergence.
- Both multiplicative and additive models resulted in similar parameter estimates.
- The minimum chi-squares model provided the smallest chi-square values, except for the exponential model.
- All models produced similar values for the absolute difference.
- The objective of this study was to determine the best model among the various options for claims severity modeling.

**2.2. Review of Previous Studies on Insurance Claim Frequency:**
- The Poisson regression model, which is a type of Generalized Linear Model (GLM), was introduced by reference 14 and further examined by reference 15.
- Reference 16 proposed the Poisson distribution as a model for modeling the frequency of insurance claims.
- While the Poisson distribution is statistically useful and favorable, it has certain limitations that restrict its applicability.
- The Poisson model has an equidispersion property, meaning that its mean and variance are equal.
- The study considered a wide range of models to identify the best model for analyzing the frequency of insurance claims.

These literature review subsections highlight the methodologies and findings of previous research in the areas of claims severity and claims frequency modeling. The review emphasizes the importance of selecting appropriate models for accurately representing these components of insurance claims. Additionally, the limitations of certain models are acknowledged, and the aim is to identify models that address these limitations and provide better insights into the data.

The literature review serves to position the current study within the broader context of existing research and to underscore the significance of the research problem being addressed. It also suggests that the current study is aiming to contribute to the field by potentially proposing a new or improved method for modeling severity and frequency dependencies in insurance claims.

The "Methodology" section of the paper outlines the steps taken to process and analyze the data related to motor insurance claims. It covers the scope of the research, data assumptions, procedures for processing data, selection of probability distributions, parameter estimation, and model selection. Here's a breakdown of the key components:

**3.1. Scope of the Research:**
- The research used secondary data from APA insurance company, covering the period from January 2017 to July 2019.
- The data specifically pertained to motor insurance claims.

**3.2. Assumptions:**
- Three assumptions were made before using the data:
  i. All claims came from the same distribution.
  ii. Zero claims are assumed to be non-inflated (i.e., no fraudulent claims or intentional zero claims).
  iii. There exist no catastrophic claims.

**3.2. Procedures for Processing Data:**
- Describes the steps followed to fit a statistical distribution to the claim data.
- Outlines the basic standards for fitting various probability distributions.

**3.3. Choosing Model of Distribution:**
- Explains the process of selecting probability distribution models for both frequency and severity.
- Selected distributions for modeling claim frequency: Poisson, Binomial, and Negative Binomial.
- Selected distributions for modeling claim severity: Weibull, Log-normal, Pareto, and Gamma.
- The choice of distributions considered various factors including time constraints, software availability, and data volume and quality.

**3.4. Estimation of Probability Distribution Parameters:**
- Details the use of Maximum Likelihood Estimation (MLE) for parameter estimation.
- MLE is chosen due to its efficiency, unbiasedness, consistency, and normality of invariance properties.

**3.5. Review of Severity Models:**
- Describes various probability distributions used to model claim severity.
- For each distribution, provides the probability density function, likelihood function, and log-likelihood function.
- Specifies how to estimate the distribution's parameters using MLE.

**3.6. Review of Frequency Distributions:**
- Similarly outlines various probability distributions used to model claim frequency.
- Provides expressions for the probability mass functions and likelihood functions of the distributions.
- Describes the estimation of distribution parameters through MLE.

**3.7. Checking the Goodness of Fit:**
- Explains two methods for assessing how well the fitted distribution matches the observed data: Chi-Square Goodness-of-Fit Test and Anderson-Darling Test.
- The Chi-Square test measures the difference between expected and observed frequencies.
- The Anderson-Darling test gives more weight to the tails of the distribution.

**3.8. Criteria for Choosing Distribution:**
- Explains the use of Akaike's Information Criteria (AIC) for model selection.
- AIC is chosen because it considers the trade-off between model fit and complexity.
- The model with the smallest AIC value is selected as the best model.

Overall, this section provides a detailed description of the research methodology, from data processing and distribution selection to parameter estimation and model selection. It showcases the analytical steps taken to determine the best-fitting distributions for modeling claim frequency and severity in the context of motor insurance claims.
