# **Parametric Significance Tests: Detailed Notes**

This guide covers the key concepts and methods related to parametric significance tests, focusing on A/B test designs and hypothesis testing. It includes explanations of z-tests, t-tests, degrees of freedom, types of errors, and the Analysis of Variance (ANOVA).

---

## **1. Introduction to Hypothesis Testing**

### **1.1. The Hypothesis Testing Framework**

Hypothesis testing is a systematic method used in statistics to determine whether there is enough evidence in a sample of data to infer that a certain condition is true for the entire population.

### **1.2. Steps in Hypothesis Testing**

1. **Formulate the Hypothesis**: Begin by proposing a hypothesis, often stating that a treatment or intervention has an effect. This is commonly tested using an A/B test design.

2. **State the Null Hypothesis (H₀)**: Assume that the treatment has no effect. The null hypothesis serves as the default or starting assumption for statistical testing.

3. **Administer the Treatment**: Apply the treatment to the experimental group while keeping the control group untreated.

4. **Collect Data**: Measure the outcomes for both the treatment and control groups.

5. **Compare Outcomes**: Analyze the data to compare the outcomes between the two groups. Acknowledge that any observed difference could be due to chance (sampling variability).

6. **Make a Decision**:

   - **Reject H₀**: If the observed difference is too large to be plausibly attributed to chance, reject the null hypothesis, suggesting that the treatment has an effect.
   - **Fail to Reject H₀**: If the difference is consistent with chance variability, do not reject the null hypothesis, concluding that there is no evidence to suggest the treatment has an effect.

---

## **2. Understanding Errors in Decision Making**

In hypothesis testing, two types of errors can occur:

### **2.1. Type I Error (α)**

- **Definition**: Incorrectly rejecting a true null hypothesis (a false positive).
- **Consequence**: Concluding that the treatment has an effect when it does not.

### **2.2. Type II Error (β)**

- **Definition**: Failing to reject a false null hypothesis (a false negative).
- **Consequence**: Concluding that the treatment has no effect when it actually does.

---

## **3. The Z-test**

### **3.1. When to Use the Z-test**

- Applicable when the population parameters (mean and standard deviation) are known.
- Suitable for large sample sizes due to reliance on the Central Limit Theorem.

### **3.2. Example Scenario**

**Question**: Does the drug NZT improve IQ scores?

- **Null Hypothesis (H₀)**: NZT does not improve IQ.
- **Known Population Parameters**:
  - Mean (μ) = 100
  - Standard Deviation (σ) = 15
- **Sample**:
  - Sample Size (n) = 25
  - Sample Mean (\( \bar{x} \)) = 109

### **3.3. Calculating the Z-score**

The z-score measures how many standard errors the sample mean is from the population mean.

**Formula**:

\[ z = \frac{\bar{x} - \mu}{\text{SEM}} \]

Where:

- \( \bar{x} \) = Sample mean
- \( \mu \) = Population mean
- SEM = Standard Error of the Mean = \( \frac{\sigma}{\sqrt{n}} \)

**Calculations**:

1. **Compute SEM**:

   \[ \text{SEM} = \frac{15}{\sqrt{25}} = \frac{15}{5} = 3 \]

2. **Compute z-score**:

   \[ z = \frac{109 - 100}{3} = \frac{9}{3} = 3 \]

### **3.4. Interpreting the Z-score**

- A z-score of 3 indicates that the sample mean is 3 standard errors above the population mean.
- Using standard normal distribution tables, a z-score of 3 corresponds to a p-value less than 0.01.
- **Decision**: Since p < 0.01, reject the null hypothesis, concluding that NZT improves IQ scores.

### **3.5. Limitations of the Z-test**

- **Known Population Parameters**: Requires known population mean and standard deviation, which is often unrealistic.
- **Sample Size**: Relies on the Central Limit Theorem, thus less accurate for small sample sizes.
- **Normal Distribution**: Assumes the data are normally distributed.

---

## **4. The t-test**

### **4.1. Introduction to the t-test**

- Developed by William Gosset under the pseudonym "Student."
- Used when population parameters are unknown and/or the sample size is small.
- Relies on the t-distribution, which accounts for extra uncertainty due to estimating the population standard deviation from the sample.

### **4.2. Degrees of Freedom (df)**

#### **4.2.1. Definition**

- **Degrees of Freedom**: The number of independent values or quantities that can vary in the analysis without violating any constraints.
- Represents the amount of information available for estimating statistical parameters.

#### **4.2.2. Calculating Degrees of Freedom**

- **General Formula**: \( df = n - k \)
  - \( n \) = Total number of observations.
  - \( k \) = Number of parameters estimated.
- In t-tests:
  - For independent samples t-test: \( df = n_1 + n_2 - 2 \)
  - For paired samples t-test: \( df = n - 1 \)

### **4.3. The t-Distribution**

- **Characteristics**:
  - Similar to the normal distribution but with heavier tails.
  - Shape depends on the degrees of freedom; as \( df \) increases, the t-distribution approaches the normal distribution.
- **Usage**: Accounts for variability introduced by estimating the population standard deviation from the sample.

### **4.4. Types of t-tests**

#### **4.4.1. Independent Samples t-test**

- **Purpose**: Compare the means of two independent groups.
- **Assumptions**:
  - Observations are independent.
  - Data in each group are normally distributed.
  - Homogeneity of variances (variances are equal across groups).

- **Formula**:

  \[ t = \frac{\bar{X}_1 - \bar{X}_2}{\text{SEM}_{\text{pooled}}} \]

  Where:

  - \( \bar{X}_1, \bar{X}_2 \) = Sample means of group 1 and group 2.
  - \( \text{SEM}_{\text{pooled}} \) = Pooled Standard Error of the Mean.

- **Calculating Pooled Standard Error**:

  \[ \text{SEM}_{\text{pooled}} = \sqrt{\left( \frac{s_1^2}{n_1} + \frac{s_2^2}{n_2} \right)} \]

  - \( s_1^2, s_2^2 \) = Sample variances.
  - \( n_1, n_2 \) = Sample sizes.

- **Degrees of Freedom**:

  \[ df = n_1 + n_2 - 2 \]

#### **4.4.2. Paired Samples t-test (Dependent Samples t-test)**

- **Purpose**: Compare means from the same group at different times (e.g., before and after treatment).
- **Assumptions**:
  - Differences are normally distributed.
  - Observations are dependent (paired).

- **Formula**:

  \[ t = \frac{\bar{D}}{\text{SEM}_D} \]

  Where:

  - \( \bar{D} \) = Mean of the difference scores.
  - \( \text{SEM}_D = \frac{s_D}{\sqrt{n}} \)
    - \( s_D \) = Standard deviation of the difference scores.

- **Degrees of Freedom**:

  \[ df = n - 1 \]

### **4.5. Practical Example**

**Scenario**: Testing whether a new drug reduces reaction time.

- **Independent Samples t-test Attempt**:

  - **Data**:

    | Group          | Reaction Times (ms) |
    |----------------|---------------------|
    | Without Drug   | 1700, 2000, 2300    |
    | With Drug      | 1100, 1500, 1900    |

  - **Calculations**:

    - Means: \( \bar{X}_{\text{without}} = 2000 \) ms, \( \bar{X}_{\text{with}} = 1500 \) ms.
    - Pooled standard deviation and SEM are calculated.
    - Resulting t-value is compared to critical t-value.
    - **Conclusion**: t-value is not significant; cannot conclude the drug is effective.

- **Paired Samples t-test Attempt**:

  - **Data**: Same participants measured before and after taking the drug.

    | Participant | Without Drug (ms) | With Drug (ms) | Difference (ms) |
    |-------------|-------------------|----------------|-----------------|
    | 1           | 1700              | 1100           | 600             |
    | 2           | 2000              | 1500           | 500             |
    | 3           | 2300              | 1900           | 400             |

  - **Calculations**:

    - Mean difference: \( \bar{D} = 500 \) ms.
    - Standard deviation of differences: \( s_D = 100 \) ms.
    - SEM of differences: \( \text{SEM}_D = \frac{100}{\sqrt{3}} \approx 57.7 \) ms.
    - t-value: \( t = \frac{500}{57.7} \approx 8.66 \).
    - **Degrees of Freedom**: \( df = 3 - 1 = 2 \).
    - **Conclusion**: t-value is significant; the drug effectively reduces reaction time.

### **4.6. Welch’s t-test**

- **Purpose**: Compare means of two independent samples when variances are unequal (violating homogeneity of variance assumption).
- **Characteristics**:
  - Does not assume equal variances.
  - Adjusts degrees of freedom using the Satterthwaite approximation, often resulting in fractional degrees of freedom.

- **Degrees of Freedom Calculation**:

  \[ df \approx \frac{\left( \frac{s_1^2}{n_1} + \frac{s_2^2}{n_2} \right)^2}{\frac{\left( \frac{s_1^2}{n_1} \right)^2}{n_1 - 1} + \frac{\left( \frac{s_2^2}{n_2} \right)^2}{n_2 - 1}} \]

- **Use Case**: Appropriate when sample sizes are unequal, and variances differ between groups.

---

## **5. Assumptions of Parametric Tests**

Parametric tests rely on certain assumptions about the data:

### **5.1. Normal Distribution**

- Data should be approximately normally distributed.
- The means and variances are meaningful and representative.

### **5.2. Homogeneity of Variance**

- The variances within each group should be similar.
- Known as the assumption of equal variances.

### **5.3. Independence**

- Observations should be independent of each other.
- In paired tests, differences should be independent and normally distributed.

### **5.4. Robustness**

- Parametric tests are considered robust, meaning they can tolerate some violations of these assumptions, especially with large sample sizes.

---

## **6. Degrees of Freedom in Depth**

### **6.1. Conceptual Understanding**

- **Degrees of Freedom (df)**: Number of independent values that can vary in an analysis without breaking any constraints.
- In statistical calculations, certain parameters (like the mean) impose constraints, reducing the degrees of freedom.

### **6.2. Example**

- Calculating a sample mean from \( n \) observations uses up one degree of freedom.
- When calculating the sample variance, degrees of freedom are adjusted to \( n - 1 \) because the mean is estimated from the data.

### **6.3. Importance in Statistical Tests**

- Degrees of freedom affect the shape of the t-distribution.
- Lower degrees of freedom result in heavier tails (more variability).
- Adjusting degrees of freedom accounts for the uncertainty introduced by estimating parameters.

---

## **7. The t-Distribution**

### **7.1. Characteristics**

- Family of distributions varying based on degrees of freedom.
- Symmetrical and bell-shaped like the normal distribution but with heavier tails.
- As degrees of freedom increase, the t-distribution approaches the normal distribution.

### **7.2. Significance Testing Using the t-Distribution**

- **Critical t-values** are determined based on the desired significance level (α) and degrees of freedom.
- The calculated t-value from the sample is compared to the critical t-value to make a decision regarding the null hypothesis.

---

## **8. Homogeneity of Variance**

### **8.1. Definition**

- The assumption that different samples have similar variances.
- Essential for the validity of certain statistical tests, like the independent samples t-test.

### **8.2. Consequences of Violation**

- If variances are unequal, the test may yield inaccurate results.
- May increase the likelihood of Type I or Type II errors.

### **8.3. Addressing Violations**

- Use tests that do not assume equal variances, such as Welch's t-test.
- Transform data to stabilize variances or use non-parametric tests.

---

## **9. Analysis of Variance (ANOVA)**

### **9.1. Purpose**

- Extends hypothesis testing to compare means across more than two groups.
- Determines whether there are any statistically significant differences between the means of three or more independent groups.

### **9.2. Logic of ANOVA**

- Analyzes the variance within groups and between groups.
- **Null Hypothesis (H₀)**: All group means are equal.
- **Alternative Hypothesis (H₁)**: At least one group mean is different.

### **9.3. ANOVA vs. Multiple t-tests**

- Performing multiple t-tests increases the risk of Type I errors.
- ANOVA controls the overall Type I error rate while testing multiple groups simultaneously.

### **9.4. F-statistic**

- ANOVA uses the F-statistic to compare variances.
- **F-statistic Formula**:

  \[ F = \frac{\text{Variance between groups}}{\text{Variance within groups}} \]

- A higher F-value suggests a greater disparity between group means relative to within-group variability.

---

## **10. Practical Considerations**

### **10.1. Choosing the Right Test**

- **Z-test**: Use when population parameters are known, and the sample size is large.
- **t-test**: Use when population parameters are unknown, especially with small sample sizes.
  - **Independent Samples t-test**: For comparing two independent groups.
  - **Paired Samples t-test**: For comparing measurements from the same group at different times.
- **ANOVA**: For comparing means across three or more groups.

### **10.2. Ensuring Assumptions Are Met**

- Check for normality using graphical methods (histograms, Q-Q plots) or statistical tests.
- Assess homogeneity of variances using tests like Levene's test.
- Consider data transformations or non-parametric alternatives if assumptions are violated.

### **10.3. Understanding Limitations**

- Statistical significance does not imply practical significance.
- Always consider the effect size and confidence intervals.
- Be cautious of Type I and Type II errors, and interpret results in the context of the study.

---

## **11. Summary**

Parametric significance tests are powerful tools in statistical analysis, allowing researchers to infer population parameters based on sample data. Understanding when and how to use z-tests, t-tests, and ANOVA is crucial for proper hypothesis testing. Always ensure that the assumptions underlying these tests are reasonably met and interpret the results within the broader context of the research question.

---

This comprehensive guide covers all key points from the presentation, providing detailed explanations and examples of each concept related to parametric significance tests.
