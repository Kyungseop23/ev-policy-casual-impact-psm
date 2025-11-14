# The Causal Impact of EV Supportive Policies on EV Adoption
## A Propensity Score Analysis

## Key Results
[ATT - CI pics]

EV supportive state policies have a clear, positive, and causal impact on Ev registration growth in the U.S.
Using **Propensity Score Matching (PSM)** to control for confounders such as GDP, charging infrastructure, political leaning, and $CO_2$.
- States with EV supportive policies achieved **significantly higher EV registration growth** than matched states without policies.
- The **effect became statistically significant after 2020** (ATT > 0, 95% CI excludes 0).
- Policy impact strengthened over time, indicating that EV supportive policies accelerated adoption beyond natural market growth.


## Project Overview
### Real World Interest: Are EV supportive policies worth maintaining?
With the increasing environmental concerns and rapidly growing EV market, many U.S. states have invested in EV supportive policies to accelerate EV adoption. However, without clear evidence of policy effectiveness, continued policy spending and investment may be difficult to justify or sustain.

### Key Research Question
Does the implementation of EV supportive policies cause an increase in EV resgistrations in U.S. states?

### Goal
- Use Propensity Score Matching (PSM) to create comparable treatment vs. control state groups
- Estimate the Average Treatment Effect on the Treated (ATT) to measure the causal impact of EV supportive policies on EV registration growth.
- Compute 95% Confidence Intervals (CI) to assess the statistical reliability of the estimated policy effects.


## Dataset Sources
| Dataset | Source |
| ----- | ----- |
| EV Policy, EV Registration, EV Charging Station | U.S. Department of Energy's Office of Energy Efficiency and Renewable Energy |
| GDP | U.S. Bureau of Economic Analysis |
| $CO_2$ Emission | U.S. Energy Information Administration | 
| Political Leaning | National Conference of State Legislatures |
| Population | U.S. Census Bureau |


## Tech Stack
- **Data Preprocessing:** Pandas, NumPy, Scikit-learn (StandardScaler)
- **Causal Inference:** Logistic Regression for Propensity Scores, Nearest Neighbor Matching, Stadardized Mean Difference (SMD), Average Treatment Effect on the Treated (ATT), Bootstrap Confidence Intervals (CI)
- **Visualization:** matplotlib, Seaborn
- **Development Environment:** Google Colab


## Full Analysis Notebook
[ev_policy_causal_impact_propensity_score.ipynb](./notebook/ev_policy_causal_impact_propensity_score.ipynb)


## Analysis Workfloww
### 1. Data Preprocessing
- Selected EV supportive policies and created a binary treatment feature indicating whether a state had any selected active policy each year from 2017 to 2023.
- Created EV registration growth per 10,000 people as the outcome.

### 2. Data Merging
- Merged all datasets by state and year.
- Converted features to population based measures to improve comparability across states and to prevent population effect.

### 3. Exploratory Data Analysis (EDA)
- Compared treatment vs. control states to identify pretreatment differences in confounders, confirming the need for matching due to large initial imbalances.
- Examined correlations among confounders and removed highly correlated variables to avoid multicollinearity.

### 4. Propensity Score Estimation & Matching
- Estimated Propensity Scores using **Logistic Regression**.
- Applied **1:2 Nearest Neighbor Matching with 0.2 SD caliper** to ensure high quality matching.

### 5. Covariate Balancing Check
- Evaluated covariate balance before and after matching using **Standardized Mean Difference (SMD)**.
- Matching reduced most imbalances and improved comparability between treatment and control groups.

### 6. Causal Effect 
- Computed the **Average Treatment Effect on the Treated (ATT)** for each year to measure the causal impact of EV supportive policy.
- Applied **bootstrap resampling** to estimate **95% Confidence Intervals** for the ATT.


## Key Insights & Discussion
### Insights
- EV supportive policies had a positive and growing causal impact on EV registratio growth, becoming statistically significant after 2020.
- The positive ATT results provide causal evidence that EV supportive policies are effective, helping policymakers justify, evaluate, and optimize policy decisions.
- Early limited effects, likely due to an immature EV market and COVID-19 disruptions, indicate that policy effectiveness depends heavily on market readiness and external conditions, emphasizing the importance of timing policy interventions.

### Challenges
#### Policy Measurement
- Policies vary in scope and strength, but the analysis considered them as a single binary feature (policy vs. no policy), without reflecting policy type, intensity, or accounting for the number of active policies implemented.

#### Confounding & Matching Limitations
- Unobserved or omitted confounders may still bias results, and propensity score matching cannot ensure perfec balance for all states.
- States with policies implemented before 2016 may already have accumulated effects that are not fully captured in the analysis.

#### Timing & Variation
- Differences in policy timing and year to year changes may influence ATT, making it difficult to isolate the exact annual impact of policy interventions.


## Future Improvements
- Analyze policy types to identify which categories have the strongest impact on EV registration growth.
- Incorporate policy intensity and timing by considering the number of policies implemented, cumulative effects, and lagged effects to better capture difference in policy strength, duration.
- Extend the analysis to 2025 once daat becomes available, especially when there are major revisions to the Federal EV tax credit in 2023-2024 and its termination on September 30, 2025, which are expected to significantly influence state level EV registration growth.