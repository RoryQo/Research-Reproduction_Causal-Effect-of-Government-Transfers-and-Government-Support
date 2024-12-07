# Replication of "Government Transfers and Political Support" by Manacorda, Miguel, and Vigorito (2011)

## Overview

The paper by Manacorda, Miguel, and Vigorito (2011) explores the effect of government transfers on political support. The authors specifically focus on the *PANES* (Plan de Atención Nacional a la Emergencia Social) program, a large-scale cash transfer program implemented in Uruguay. The objective of the study is to investigate whether the receipt of government transfers increases political support for the ruling government, especially among households that were more directly impacted by the program.

### Key Research Questions
- **Primary Research Question**: Does receiving government transfers increase political support for the ruling government?
- **Secondary Question**: How do income levels and eligibility for the PANES program influence political support?

### Contribution
The study contributes to the literature on the political economy of welfare programs, suggesting that cash transfers can serve as a mechanism for governments to garner political loyalty, particularly among lower-income populations.


## Data Description

The study uses data from a survey conducted in Uruguay between 2005 and 2007, focusing on households that participated in the PANES program. The dataset contains key variables related to household characteristics, political support, and eligibility for the program.

### Key Variables
- **`aprobado`**: A binary variable indicating whether a household received the PANES transfer in 2005-2007.
- **`untracked07`**: A variable that indicates whether a household was untracked in 2007 (i.e., did not participate in the survey).
- **`h_89`**: The respondent’s level of political support for the government in 2007 (on a scale from 1 to 3).
- **`hv34`**: The respondent’s level of political support for the government in 2008 (on a scale from 1 to 3).
- **`ind_reest`**: Predicted income for each household, used to define treatment eligibility.
- **`newtreat`**: A variable indicating eligibility for the PANES program.

Additional variables include:
- **`pct`**: Percentiles of predicted income, which helps to define treatment and control groups.
- **`income_sq`**: The squared value of predicted income, included as a control in regression models.


## Methodology

### 1. **Identification Strategy: Difference-in-Differences (DiD)**

The authors apply a **Difference-in-Differences** (DiD) methodology to estimate the causal effect of receiving the PANES transfer on political support. The key assumption behind this approach is that, in the absence of the treatment (transfers), the political support of treated and control households would have followed parallel trends over time.

#### Treatment Group
Households that received PANES transfers in 2005-2007 make up the treatment group.

#### Control Group
Households that did not receive PANES transfers but were eligible based on predicted income levels serve as the control group. Eligibility is determined using the predicted income (`ind_reest`), with households below a certain threshold receiving the PANES transfer.

The DiD model is specified as follows:
```math
\text{Political Support}_{it} = \beta_0 + \beta_1 \cdot \text{Treatment}_{it} + \beta_2 \cdot \text{Post}_{t} + \beta_3 \cdot (\text{Treatment}_{it} \times \text{Post}_{t}) + \epsilon_{it}
```
Where:
- \(\text{Treatment}_{it}\) is a binary variable indicating whether the household received the transfer.
- \(\text{Post}_{t}\) is a binary variable indicating the post-treatment period (2007-2008).
- The coefficient \(\beta_3\) on the interaction term \(\text{Treatment}_{it} \times \text{Post}_{t}\) captures the causal effect of receiving the PANES transfer on political support.


## Step-by-Step Replication

### Step 1: Data Preparation

1. **Load and Clean Data**
   - The dataset is cleaned by selecting the relevant variables such as income, political support, treatment indicators, and time periods.
   - Variables are checked for missing values, and appropriate methods (e.g., imputation or removal) are used to address these missing data.

2. **Income Percentiles for Treatment Groups**
   - The predicted income variable (`ind_reest`) is used to calculate income percentiles. Households are then categorized into treatment and control groups based on their predicted income and eligibility for the PANES transfer.

3. **Create Treatment Indicators**
   - A binary treatment indicator is created: 1 if the household was eligible for the PANES transfer, and 0 otherwise.
   - A post-treatment period indicator is also created, which takes the value 1 if the observation is from the post-treatment period (2007-2008) and 0 otherwise.

### Step 2: Descriptive Analysis

1. **Summarize Data by Treatment Group**
   - Descriptive statistics for key variables (e.g., political support, income, demographic characteristics) are provided separately for the treatment and control groups. This helps to assess any potential differences between the groups prior to the treatment.

### Step 3: Regression Analysis

The main objective of the regression analysis is to estimate the effect of the PANES transfer on political support, with a particular focus on how this effect varies by income group. The **Difference-in-Differences (DiD)** methodology is used for this purpose. Below, we specify the regression models in greater detail.

#### 1. Basic Regression Model (Difference-in-Differences)

The **Difference-in-Differences (DiD)** method compares the changes in political support over time between the treatment and control groups, accounting for time trends and group-specific factors. The basic DiD regression model is specified as:

```math
\text{Government Support}_{07} = \beta_0 + \beta_1 \cdot \text{Eligibility} + \beta_2 \cdot \text{Score}_ + \beta_3 \cdot (\text{Eligibility}\times \text{Score}_{t}) + \epsilon
```
Where:
- \(\text{Political Support}_{it}\) is the political support for household \(i\) at time \(t\). This is typically measured as an ordinal variable (e.g., 1-3 scale), with higher values indicating stronger support.
- \(\text{Treatment}_{it}\) is a binary variable indicating whether household \(i\) was eligible for the PANES transfer at time \(t\). It equals 1 if the household is in the treatment group, 0 otherwise.
- \(\text{Post}_{t}\) is a binary variable indicating whether the observation is from the post-treatment period (2007-2008). It equals 1 if the observation is after the program's implementation, 0 otherwise.
- \(\text{Treatment}_{it} \times \text{Post}_{t}\) is the interaction term, which captures the effect of the treatment in the post-treatment period. This is the key variable of interest, as it identifies whether the treatment has had an impact on political support after the program's rollout.
- \(\epsilon_{it}\) is the error term, assumed to be independently and identically distributed.

The coefficient \(\beta_3\) on the interaction term is the DiD estimator and represents the causal effect of receiving the PANES transfer on political support. If the transfer increases political support, we expect \(\beta_3\) to be positive and statistically significant.


#### 3. Nonlinear Specification

Income is a key factor in determining both eligibility for the PANES transfer and political support. It is possible that the relationship between income and political support is nonlinear. For example, the impact of receiving the PANES transfer might be stronger for lower-income households compared to higher-income ones. 

To explore potential nonlinear effects, the model is extended by including squared income terms to allow for a curvilinear relationship:

```math
\text{Political Support}_{it} = \beta_0 + \beta_1 \cdot \text{Treatment}_{it} + \beta_2 \cdot \text{Post}_{t} + \beta_3 \cdot (\text{Treatment}_{it} \times \text{Post}_{t}) + \gamma_1 \cdot \text{Income}_{it} + \gamma_2 \cdot \text{Income}_{it}^2 + \epsilon_{it}
```

Where:
- \(\text{Income}_{it}\) is the household's income.
- \(\text{Income}_{it}^2\) is the squared income term.

By including both linear and squared terms for income, this model captures potential diminishing or increasing returns to income with respect to political support.

#### 4. Fixed Effects Models

In the previous models, the analysis assumes that all unobserved heterogeneity across households is captured by the control variables. However, it’s possible that there are unobserved time-invariant characteristics of households (e.g., household preferences, political ideologies) that influence both treatment assignment and political support.

To address this, a fixed-effects model can be used to account for unobserved, time-invariant household characteristics. The fixed-effects model eliminates the bias that could arise from omitted variables that do not change over time (e.g., political beliefs, family dynamics).

The fixed-effects model is specified as:

\[
\text{Political Support}_{it} = \alpha_i + \beta_1 \cdot \text{Treatment}_{it} + \beta_2 \cdot \text{Post}_{t} + \beta_3 \cdot (\text{Treatment}_{it} \times \text{Post}_{t}) + \gamma \cdot \mathbf{X}_{it} + \epsilon_{it}
\]

Where:
- \(\alpha_i\) is the household-specific fixed effect, which absorbs all time-invariant heterogeneity at the household level.
- The rest of the variables are as defined earlier.

The inclusion of fixed effects controls for all unobservable factors that remain constant over time but may vary across households, providing a cleaner estimate of the treatment effect.

#### 5. Robustness Checks

To ensure that the results are not driven by particular assumptions or model specifications, various robustness checks are conducted. These include:

- **Alternative Operationalizations of Political Support**: Political support may be measured in different ways (e.g., categorical versus continuous outcomes). The analysis is repeated using different measures of political support to ensure the robustness of the findings.
  
- **Varying Time Windows**: The post-treatment period may not immediately reflect the full effects of the program. Alternative time windows for the post-treatment period are tested (e.g., 2007–2009) to check if the estimated effect is consistent over time.
  
- **Fixed Effects at the Regional Level**: In addition to household fixed effects, we may include fixed effects for geographic regions (e.g., provinces or municipalities) to account for regional trends that could influence both the treatment and political support outcomes.



### Step 4: Visualizing Results

1. **Graph Political Support Over Time**
   - Political support is graphed for both the treatment and control groups over time. This provides a visual representation of the parallel trends assumption (i.e., the assumption that, in the absence of the treatment, the treatment and control groups would have followed similar trends in political support).

2. **Scatterplot of Predicted Income and Support**
   - A scatterplot is generated to explore how income levels interact with political support, providing insight into how income might moderate the effect of the PANES transfer on political support.



## Results Interpretation

### Main Findings:
1. **Effect of Transfers on Political Support**
   - The results indicate that the PANES transfer led to a significant increase in political support, particularly among lower-income households. The estimated \(\beta_3\) coefficient is positive and statistically significant, confirming the causal impact of receiving the transfer.

2. **Income as a Moderator**
   - The interaction between income and political support shows that the effect of the transfer is more pronounced among lower-income households. The results from the nonlinear model suggest that income moderates the effect of the PANES transfer.

### Conclusion:
The study highlights the role of targeted transfers in shaping political loyalty, with evidence showing that government transfers can increase political support, particularly among low-income populations. These findings are crucial for understanding the political economy of welfare programs and their potential for influencing electoral outcomes.
