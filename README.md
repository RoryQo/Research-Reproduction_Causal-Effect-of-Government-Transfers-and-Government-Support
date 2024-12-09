# Reproduction of "Government Transfers and Political Support" by Manacorda, Miguel, and Vigorito (2011)         
          
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

<p align="center">
  <img src="https://github.com/RoryQo/Research-Reproduction_Causal-Effect-of-Government-Transfers-and-Government-Support/raw/main/Figures/Fig2.jpg" width="450px">
</p>

#### Treatment Group
Households that received PANES transfers in 2005-2007 make up the treatment group.

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

### Step 3: Regression Analysis (Reproducing Row 2 of Table 1)

The main objective of the regression analysis is to estimate the effect of the PANES transfer on political support, with a particular focus on how this effect varies by income group. The **Difference-in-Differences (DiD)** methodology is used for this purpose. Below, we specify the regression models in greater detail.

#### 1. Basic Regression Model (Difference-in-Differences)

The **Difference-in-Differences (DiD)** method compares the changes in political support over time between the treatment and control groups, accounting for time trends and group-specific factors. The basic DiD regression model is specified as:

<br>

```math
\text{Government Support}_{07} = \beta_0 + \beta_1 \cdot \text{Eligibility} + \epsilon
```

#### 2. Linear Specification

<br>

```math
\text{Government Support}_{07} = \beta_0 + \beta_1 \cdot \text{Eligibility} + \beta_2 \cdot \text{Score}_ + \beta_3 \cdot (\text{Eligibility}\times \text{Score}) + \epsilon
```
Where:
- $\(\text{Political Support}\)$ is the political support for household. This is typically measured as an ordinal variable (e.g., 1-3 scale), with higher values indicating stronger support.
- $\(\text{Treatment}\)$ is a binary variable indicating whether household \(i\) was eligible for the PANES transfer. It equals 1 if the household is in the treatment group, 0 otherwise.
- $\(\text{Score}\)$ is predicted income score.
- $\(\text{Treatment} \times \text{Score}\)$ is the interaction term, which captures the effect of the treatment in the post-treatment period. This is the key variable of interest, as it identifies whether the treatment has had an impact on political support after the program's rollout.
- $\(\epsilon\)$ is the error term, assumed to be independently and identically distributed.

The coefficient $\(\beta_3\)$ on the interaction term is the DiD estimator and represents the causal effect of receiving the PANES transfer on political support. If the transfer increases political support, we expect $\(\beta_3\)$ to be positive and statistically significant.


#### 3. Nonlinear Specification

Income is a key factor in determining both eligibility for the PANES transfer and political support. It is possible that the relationship between income and political support is nonlinear. For example, the impact of receiving the PANES transfer might be stronger for lower-income households compared to higher-income ones. 

To explore potential nonlinear effects, the model is extended by including squared income terms to allow for a curvilinear relationship:

<br> 

```math
Gov.Support_{07}=\beta_0+\beta_1Eligibility+\beta_2Score+\beta_3Score^2+\beta_4(Eligibility:Score)+\beta_5(Eligibility:Score)^2+\epsilon
```
<br>

Where:
- $\(\text{Score}\)$ is the household's income.
- $\(\text{Score}^2\)$ is the squared income term.

By including both linear and squared terms for income, this model captures potential diminishing or increasing returns to income with respect to political support.

<p align="center">
  <img src="https://github.com/RoryQo/Research-Reproduction_Causal-Effect-of-Government-Transfers-and-Government-Support/raw/main/Figures/R2T1.jpg" width="550px">
</p>


#### 5. Robustness Checks

To ensure that the results are not driven by particular assumptions or model specifications. 
The author used 2% bandwidth, we check 1%, 5% and 15% bandwidths to ensure robustness.  All of the coefficients are very similar indicating that the results are robust, because the smaller bandwidth estimates are very similar to the larger bandwidth results.

```
# Example of different bandwidths (in terms of score)
bandwidths <- c(0.01, 0.05, 0.15)  # 1%, 5%, 10% bandwidths around the cutoff

# Subset data for each bandwidth
narrow_bandwidth_data <- lapply(bandwidths, function(bw) {
  subset(df, abs(df$ind_reest - cutoff) <= bw)
})
```

<p align="center">
  <img src="https://github.com/RoryQo/Research-Reproduction_Causal-Effect-of-Government-Transfers-and-Government-Support/raw/main/Figures/Robust.jpg" width="400px">
</p>

### Step 4: Visualizing Results

1. **Graph Political Support During Program (Firgure 3.)**
   - Political support is graphed for both the treatment and control groups over time. This provides a visual representation of the parallel trends assumption (i.e., the assumption that, in the absence of the treatment, the treatment and control groups would have followed similar trends in political support).
  
<p align="center">
  <img src="https://github.com/RoryQo/Research-Reproduction_Causal-Effect-of-Government-Transfers-and-Government-Support/raw/main/Figures/Fig3.jpg" width="450px">
</p>

2. **Graph Political Support After Program (Figure 4.)**
   - A scatterplot is generated to explore how income levels interact with political support, providing insight into how income might moderate the effect of the PANES transfer on political support.

<p align="center">
  <img src="https://github.com/RoryQo/Research-Reproduction_Causal-Effect-of-Government-Transfers-and-Government-Support/raw/main/Figures/Fig4.jpg" width="450px">
</p>


## Results Interpretation

### Main Findings:
1. **Effect of Transfers on Political Support**
   - The results indicate that the PANES transfer led to a significant increase in political support, particularly among lower-income households. The estimated $\(\beta_3\)$ coefficient is positive and statistically significant, confirming the causal impact of receiving the transfer.

2. **Income as a Moderator**
   - The interaction between income and political support shows that the effect of the transfer is more pronounced among lower-income households. The results from the nonlinear model suggest that income moderates the effect of the PANES transfer.

### Conclusion:
The study highlights the role of targeted transfers in shaping political loyalty, with evidence showing that government transfers can increase political support, particularly among low-income populations. These findings are crucial for understanding the political economy of welfare programs and their potential for influencing electoral outcomes.
