---
layout: post
title: Assessing Campaign Performance Using the Chi-Square Test for Independence
image: "/posts/ab-testing-title-img.png"
tags: [AB Testing, Hypothesis Testing, Chi-Square, Python]
---

In this project I apply the chi-square hypothesis test for independence to a grocery store mail campaign. For this campaign different versions of the mailer were sent to potential customers, allowing for comparison each mailer's effectiveness. I use the chi-square hypothesis test output to assess whether the sign up rates by mailer were significantly different from one another.

# Table of Contents

- [Project Overview](#overview-main)
    - [Context](#overview-context)
    - [Actions](#overview-actions)
    - [Results & Discussion](#overview-results)
- [Concept Overview](#concept-overview)
- [Data Overview & Preparation](#data-overview)
- [Applying Chi-Square Test for Independence](#chi-square-application)
- [Analysing the Results](#chi-square-results)
- [Discussion](#discussion)

___

# Project Overview  <a name="overview-main"></a>

### Context <a name="overview-context"></a>

A grocery store ran a mail campaign to promote their new Delivery Club. The Delivery Club costs $100 per year, with a maximum of 52 deliveries. The normal cost of grocery delivery is $10 per delivery.

Potential Delivery Club customers were put randomly into three groups for the campaign. Each group received a different mailer, with no mailer for the control group.
<ol type="A">
    <li>A low quality, low cost mailer</li>
    <li>A high quality, high cost mailer</li>
    <li>No mailer (control group)</li>
</ol>

Based on initial signups, the grocery store management team already knew that receiving a mailer was very effective for Delivery Club signups. The management team was interested to know if there is a significant difference in signups between group A (cheap mailer) and B (expensive mailer). This knowledge will affect decisions for future mail campaigns.

<br/>

### Actions <a name="overview-actions"></a>

<ol type="1">
    <li>I chose the chi-squared hypothesis test to compare signup rates between the mailers, since I was comparing percentage outcomes between groups</li>
    <li>To prepare the data for the test, I removed the control group data</li>
    <li>I set hypotheses and acceptance criteria for the test</li>
        <ol type="a">
            <li><b>Null Hypothesis</b>: There is no relationship between mailer type and signup rate. They are independent.</li>
            <li><b>Alternate Hypothesis</b>: There is a relationship between mailer type and signup rate. They are not independent.</li>
            <li><b>Acceptance Criteria</b>: 0.05</li>
        </ol>
    <li>I aggregated the data in a 2x2 matrix: signup flag by mailer type</li>
    <li>Using python, I calculated the chi-square statistic, p-value, and expected values</li>
</ol>

<br/>

### Results & Discussion <a name="overview-results"></a>

Observed values for the sign-up rate of groups A and B:

* Group A (low cost mailer): <b>32.8%</b> signup rate
* Group B (high cost mailer): <b>37.8%</b> signup rate

The chi-square test results in:

* Chi-square test statistic: <b>1.94</b>
* p-value: <b>0.16</b>
* Critical value: <b>3.84</b> (for the specified Acceptance Criteria of 0.05)

Since the test statistic is lower than the critical value (and our p-value is higher than the acceptance criteria), I did not reject the null hypothesis. I concluded that although there is a difference in signup rate between the two mailer groups, there is not enough evidence to say that this difference is due to more than random chance.

Without this hypothesis test, the grocery store management team may have incorrectly concluded that there is a relationship between mailer type and signup rate. This conclusion could have resulted in spending more on future expensive mailers, but not necessarily gaining extra signups as a result.

It is worth noting that the test results do not suggest that there is no relationship between mailer cost and sign up rate. The test results could be due to a small sample size. If more mailer data was collected and there still was a difference in signups, the hypothesis test may reach a different conclusion.

<br/>

___

# Concept Overview  <a name="concept-overview"></a>

<br>
### A/B Hypothesis Testing

An A/B test is a randomized experiment containing two groups, A and B. As part of the experiment, both groups receive different experiences while researchers measure participant responses. Researchers then look to understand each group's response to their experience, determining if the responses are different enough to be considered statistically significant.

Among many potential uses, companies use A/B Tests to select online ads, email subject lines for customer contact, and coupon offerings. These tests are an excellent way for a company to differentiate between potential options when making business decisions. 

<br>
#### The Null Hypothesis

The null hypothesis is the hypothesis that there is no statistically significant difference between groups A and B. This hypothesis assumes that any difference observed between the two groups is the result of random chance.

In an A/B test, the null hypothesis is the researcher's initial viewpoint. The researcher is seeking evidence to disprove (reject) the null hypothesis in favor of another hypothesis, or keep (not reject) the null hypothesis.

<br>
#### The Alternate Hypothesis

The other hypothesis in an A/B Test is called the alternative hypothesis. The alternative hypothesis states the opposite viewpoint of the null hypothesis: that the difference between groups A and B is statistically significant, and not a result of random chance.

In the event that the researcher rejects the null hypothesis, they do so in favor of the alternative hypothesis.

<br>
#### p-value

The p-value is the probability that if the A/B test was run many times, researchers would see results equal to or more extreme than what they observed in the current experiment.

<br>
#### The Acceptance Criteria

The acceptance criteria is a p-value threshold at which we'll decide whether to reject or not reject the null hypothesis. In order to remain impartial, researchers specify the acceptance criteria before they run an A/B Test. 

By convention the acceptance criteria is set at 0.05. If desired, it could be set at other levels such as 0.10 or 0.01.

<br>
#### Bringing Topics Together
In an A/B test researchers test the null hypothesis. They do so by collecting evidence, and using that evidence to determine a p-value. This p-value is compared against the acceptance criteria to determine whether to reject or fail to reject the null hypothesis.

If the p-value is less than or equal to the acceptance criteria, then researchers reject the null hypothesis in favor of the alternative hypothesis. In this case researchers determine that there is a statistically significant difference of the metric measured between groups A and B.

If the p-value is greater than the acceptance criteria, then researchers fail to reject the Null Hypothesis. They determine that the difference in metric measurements between groups A and B is likely the result of random chance or low sample size.

<br>
#### Types of Hypothesis Test

There are many different types of hypothesis tests. The type of test best suited for an experiment depends on they type of data being used and the question that the researcher asks.

The mailer campaign measures the difference in signup rates between two groups, which makes the chi-square test for independence an acceptable test choice.

___

<br>
# Data Overview & Preparation  <a name="data-overview"></a>

There exists a *campaign_data* table that shows which customers received each type of Delivery Club mailer, which customers were in the control group, and which customers joined the club as a result.

I sought evidence that the Delivery Club signup rate for potential customers that received Mailer 1 (low cost) was different to those who received Mailer 2 (high cost). As such, I excluded potential customers in the control group.

Description of Python code below:
* Load Python libraries required to import the data and perform the chi-square test
* Import the required data from the *campaign_data* table
* Exclude customers in the control group, providing a dataset with only Mailer 1 and Mailer 2 potential customers

<br>
```python

# install the required python libraries
import pandas as pd
from scipy.stats import chi2_contingency, chi2

# import campaign data
campaign_data = pd.read_csv(campaign_data.csv)

# remove customers who were in the control group
campaign_data = campaign_data.loc[campaign_data["mailer_type"] != "Control"]

```
<br>
Data sample (first 10 rows):
<br>
<br>

| **customer_id** | **campaign_name** | **mailer_type** | **signup_flag** |
|---|---|---|---|
| 74 | delivery_club | Mailer1 | 1 |
| 524 | delivery_club | Mailer1 | 1 |
| 607 | delivery_club | Mailer2 | 1 |
| 343 | delivery_club | Mailer1 | 0 |
| 322 | delivery_club | Mailer2 | 1 |
| 115 | delivery_club | Mailer2 | 0 |
| 1 | delivery_club | Mailer2 | 1 |
| 120 | delivery_club | Mailer1 | 1 |
| 52 | delivery_club | Mailer1 | 1 |
| 405 | delivery_club | Mailer1 | 0 |
| 435 | delivery_club | Mailer2 | 0 |

<br>
Data frame:
* customer_id (unique ID)
* campaign_name (all delivery_club)
* mailer_type (either Mailer1 or Mailer2)
* signup_flag (either 1 or 0)

___

<br>
# Applying Chi-Square Test for Independence <a name="chi-square-application"></a>

<br>
### State Hypotheses & Acceptance Criteria for Test

```python

# specify hypotheses & acceptance criteria for test
null_hypothesis = "There is no statistically significant relationship between mailer type and signup rate.  They are independent."
alternate_hypothesis = "There is a relationship between mailer type and signup rate.  They are not independent."
acceptance_criteria = 0.05

```

<br>
### Calculate Observed Frequencies & Expected Frequencies

Code description:
* Summarize dataset into 2x2 matrix for *signup_flag* by *mailer_type*
* Calculate:
    * Chi-square statistic
    * p-value
    * Degrees of freedom
    * Expected values
* Display chi-square statistic & p-value from the test
* Calculate critical value based upon our acceptance criteria & the degrees Of freedom
* Display critical value

```python

# aggregate our data to get observed values
observed_values = pd.crosstab(campaign_data["mailer_type"], campaign_data["signup_flag"]).values

# run the chi-square test
chi2_statistic, p_value, dof, expected_values = chi2_contingency(observed_values, correction = False)

# print chi-square statistic
print(chi2_statistic)
>> 1.94

# print p-value
print(p_value)
>> 0.16

# find the critical value for our test
critical_value = chi2.ppf(1 - acceptance_criteria, dof)

# print critical value
print(critical_value)
>> 3.84

```
<br>
As context, the observed signup rates:
* Mailer 1 (Low Cost): **32.8%**
* Mailer 2 (High Cost): **37.8%**

The higher cost mailer leads to a higher signup rate.  The result from the chi-square test will provide information about whether this difference is statistically significant, or if it might have occured by chance.

The chi-square test results in:
* Test statistic of **1.94**
* p-value of **0.16**

The critical value for our specified Acceptance Criteria of 0.05 is **3.84**

**Note** When applying the Chi-Square Test above, there is a parameter *correction = False* which means we are applying what is known as the *Yate's Correction*. This correction is applied when the degrees of freedom is equal to one.  This correction helps to prevent overestimation of statistical signficance.

___

<br>
# Analyzing the Results <a name="chi-square-results"></a>

The p-value of **0.16** is greater than the acceptance criteria of 0.05. As such, I failed to reject the null hypothesis. This means that there is not evidence of a statistically significant difference in the signup rates between Mailer 1 and 2.

The same conclusion is reached due to the chi-square statistic of **1.94** being lower than the critical value of **3.84**.

The code below interprets the test results and explains the outcome:

```python

# print the results (based upon p-value)
if p_value <= acceptance_criteria:
    print(f"The p-value of {p_value} is less than or equal to the acceptance_criteria of {acceptance_criteria} - I reject the null hypothesis, and conclude that: {alternate_hypothesis}")
else:
    print(f"The p-value of {p_value} is greater than the acceptance_criteria of {acceptance_criteria} - I fail to reject the null hypothesis, and conclude that: {null_hypothesis}")

>> The p-value of 0.16351 is greater than the acceptance_criteria of 0.05 - I fail to reject the null hypothesis, and conclude that: There is no relationship between mailer type and signup rate.  They are independent


# print the results (based upon p-value)
if chi2_statistic >= critical_value:
    print(f"As our chi-square statistic of {chi2_statistic} is higher than our critical value of {critical_value} - we reject the null hypothesis, and conclude that: {alternate_hypothesis}")
else:
    print(f"As our chi-square statistic of {chi2_statistic} is lower than our critical value of {critical_value} - we retain the null hypothesis, and conclude that: {null_hypothesis}")
    
>> As our chi-square statistic of 1.9414 is lower than our critical value of 3.841458820694124 - we retain the null hypothesis, and conclude that: There is no statistically significant relationship between mailer type and signup rate.  They are independent.

```
<br>
As we can see from the outputs of these print statements, we do indeed retain the null hypothesis.  We could not find enough evidence that the signup rates for Mailer 1 and Mailer 2 were different - and thus conclude that there was no significant difference.

___

<br>
# Discussion <a name="discussion"></a>

While we saw that the higher cost Mailer 2 had a higher signup rate (37.8%) than the lower cost Mailer 1 (32.8%) it appears that this difference is not significant, at least at our Acceptance Criteria of 0.05.

Without running this Hypothesis Test, the client may have concluded that they should always look to go with higher cost mailers - and from what we've seen in this test, that may not be a great decision.  It would result in them spending more, but not *necessarily* gaining any extra revenue as a result

Our results here also do not say that there *definitely isn't a difference between the two mailers* - we are only advising that we should not make any rigid conclusions *at this point*.  

Running more A/B Tests like this, gathering more data, and then re-running this test may provide us, and the client more insight!
