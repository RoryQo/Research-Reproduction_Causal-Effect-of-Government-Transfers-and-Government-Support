# Replication of "Government Transfers and Political Support" by Manacorda, Miguel, and Vigorito (2011)

## Introduction

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
\[
\text{Political Support}_{it} = \beta_0 + \beta_1 \cdot \text{Treatment}_{it} + \beta_2 \cdot \text{Post}_{t} + \beta_3 \cdot (\text{Treatment}_{it} \times \text{Post}_{t}) + \epsilon_{it}
\]
Where:
- \(\text{Treatment}_{it}\) is a binary variable indicating whether the household received the transfer.
- \(\text{Post}_{t}\) is a binary variable indicating the post-treatment period (2007-2008).
- The coefficient \(\beta_3\) on the interaction term \(\text{Treatment}_{it} \times \text{Post}_{t}\) captures the causal effect of receiving the PANES transfer on political support.



## Step-by-Step Replication

### Step 1: Data Preparation

1. **Load and Clean Data**
   - The dataset is cleaned by selecting relevant variables and handling missing data.
   - Categorical variables such as political support are recoded into numerical values suitable for regression analysis.

2. **Income Percentiles for Treatment Groups**
   - The predicted income variable (`ind_reest`) is used to create income percentiles, which define the treatment and control groups.

3. **Create Treatment Indicators**
   - A treatment indicator is created to identify households that were eligible for the PANES transfer.

### Step 2: Descriptive Analysis

1. **Summarize Data by Treatment Group**
   - Summary statistics for key variables (such as political support and income levels) are calculated by treatment group. This helps to understand the characteristics of those who received the transfer versus those who did not.

### Step 3: Regression Analysis

1. **Run Difference-in-Differences Regression**
   - The DiD model is used to estimate the causal effect of the PANES transfer on political support, adjusting for household income and other covariates.

2. **Robustness Checks**
   - Various specifications are tested to check the sensitivity of the results, such as using income as a continuous variable or including additional covariates like age or education.

### Step 4: Visualizing Results

1. **Graph Political Support Over Time**
   - Political support is plotted for the treatment and control groups before and after the implementation of the PANES program, allowing for a visual assessment of the difference-in-differences effect.

2. **Scatterplot of Predicted Income and Support**
   - The relationship between predicted income and political support is visualized, illustrating how income levels impact the treatment effect.



## Results Interpretation

### Main Findings:
1. **Effect of Transfers on Political Support**
   - The regression results show that receiving the PANES transfer significantly increased political support for the ruling government, especially among low-income households. This suggests that targeted transfers can be used as a tool for enhancing political loyalty.

2. **Income as a Moderator**
   - Income levels moderated the effect of the PANES transfer on political support. Low-income households exhibited a larger increase in political support compared to higher-income households.

### Conclusion:
The study concludes that government transfers can play a role in increasing political support, particularly for lower-income populations. This finding provides evidence of the political economy dynamics behind welfare programs, showing that governments can use targeted transfers to strengthen political loyalty.



## Limitations & Extensions

- **External Validity**: The results of this study are specific to the context of Uruguay and may not necessarily apply to other countries or settings with different political or economic conditions.
- **Long-term Effects**: The study focuses on short-term effects (2007-2008). Future research could investigate the long-term impact of cash transfer programs on political behavior, especially as these transfers may have lasting effects on voter preferences and political alignment.
