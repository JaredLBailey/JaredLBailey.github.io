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
### A/B Testing

An A/B Test is a randomized experiment containing two groups, A and B. As part of the experiment, both groups receive different experiences while researchers measure participant responses. Researchers then look to understand each group's response to their experience, determining if the responses are different enough to be considered statistically significant.

Among many potential uses, companies use A/B Tests to select online ads, email subject lines for customer contact, and coupon offerings. These tests are an excellent way for a company to differentiate between potential options when making business decisions. 

<br>
### Hypothesis Testing

A Hypothesis Test is used to assess the plausibility, or likelihood of an assumed viewpoint based on sample data - in other words, a it helps us assess whether a certain view we have about some data is likely to be true or not.

There are many different scenarios we can run Hypothesis Tests on, and they all have slightly different techniques and formulas - however they all have some shared, fundamental steps & logic that underpin how they work.

<br>
#### The Null Hypothesis

The Null Hypothesis is the hypothesis that there is no statistically significant difference between groups A and B. This hypothesis assumes that any difference observed between the two groups is the result of random chance.

For an A/B Test, the Null Hypothesis is the researcher's initial viewpoint. The researcher is seeking evidence to disprove (reject) the Null Hypothesis in favor of another hypothesis, or keep (not reject) the Null Hypothesis.

<br>
#### The Alternate Hypothesis

The other hypothesis in an A/B Test is called the Alternative Hypothesis. The Alternative Hypothesis states the opposite viewpoint of the Null Hypothesis: that the difference between groups A and B is statistically significant, and not a result of random chance.

In the event that the researcher rejects the Null Hypothesis, they do so in favor of the Alternative Hypothesis.

<br>
#### p-value

The Acceptance Cri

<br>
#### The Acceptance Criteria

The Acceptance Criteria is a p-value threshold at which we'll decide whether to reject or not reject the Null Hypothesis. In order to remain impartial, researchers specify the Acceptance Criteria before they run an A/B Test. 

By convention the Acceptance Criteria is set at 0.05. If desired, it could be set at other levels such as 0.10 or 0.01.

<br>
#### Bringing Topics Together
In a Hypothesis Test researchers test the Null Hypothesis. They do so by collecting evidence, and using that evidence to determine a p-value. This p-value is measured against the Acceptance Criteria to determine whether to reject or fail to reject the Null Hypothesis. If the Null Hypothesis is rejected, it is done so in favor of the Alternative Hypothesis.

<br>
#### Types of Hypothesis Test

There are many different types of Hypothesis Tests, each of which is appropriate for use in differing scenarios - depending on a) the type of data that you’re looking to test and b) the question that you’re asking of that data.

In the case of our task here, where we are looking to understand the difference in sign-up *rate* between two groups - we will utilise the Chi-Square Test For Independence.

<br>
### Chi-Square Test For Independence

The Chi-Square Test For Independence is a type of Hypothesis Test that assumes observed frequencies for categorical variables will match the expected frequencies.

The *assumption* is the Null Hypothesis, which as discussed above is always the viewpoint that the two groups will be equal.  With the Chi-Square Test For Independence we look to calculate a statistic which, based on the specified Acceptance Criteria will mean we either reject or support this initial assumption.

The *observed frequencies* are the true values that we’ve seen.

The *expected frequencies* are essentially what we would *expect* to see based on all of the data.

**Note:** Another option when comparing "rates" is a test known as the *Z-Test For Proportions*.  While, we could absolutely use this test here, we have chosen the Chi-Square Test For Independence because:

* The resulting test statistic for both tests will be the same
* The Chi-Square Test can be represented using 2x2 tables of data - meaning it can be easier to explain to stakeholders
* The Chi-Square Test can extend out to more than 2 groups - meaning the business can have one consistent approach to measuring signficance

___

<br>
# Data Overview & Preparation  <a name="data-overview"></a>

In the client database, we have a *campaign_data* table which shows us which customers received each type of "Delivery Club" mailer, which customers were in the control group, and which customers joined the club as a result.

For this task, we are looking to find evidence that the Delivery Club signup rate for customers that received "Mailer 1" (low cost) was different to those who received "Mailer 2" (high cost) and thus from the *campaign_data* table we will just extract customers in those two groups, and exclude customers who were in the control group.

In the code below, we:

* Load in the Python libraries we require for importing the data and performing the chi-square test (using scipy)
* Import the required data from the *campaign_data* table
* Exclude customers in the control group, giving us a dataset with Mailer 1 & Mailer 2 customers only

<br>
```python

# install the required python libraries
import pandas as pd
from scipy.stats import chi2_contingency, chi2

# import campaign data
campaign_data = ...

# remove customers who were in the control group
campaign_data = campaign_data.loc[campaign_data["mailer_type"] != "Control"]

```
<br>
A sample of this data (the first 10 rows) can be seen below:
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
In the DataFrame we have:

* customer_id
* campaign name
* mailer_type (either Mailer1 or Mailer2)
* signup_flag (either 1 or 0)

___

<br>
# Applying Chi-Square Test for Independence <a name="chi-square-application"></a>

<br>
### State Hypotheses & Acceptance Criteria for Test

The very first thing we need to do in any form of Hypothesis Test is state our Null Hypothesis, our Alternate Hypothesis, and the Acceptance Criteria (more details on these in the section above)

In the code below we code these in explcitly & clearly so we can utilise them later to explain the results.  We specify the common Acceptance Criteria value of 0.05.

```python

# specify hypotheses & acceptance criteria for test
null_hypothesis = "There is no relationship between mailer type and signup rate.  They are independent"
alternate_hypothesis = "There is a relationship between mailer type and signup rate.  They are not independent"
acceptance_criteria = 0.05

```

<br>
### Calculate Observed Frequencies & Expected Frequencies

As mentioned in the section above, in a Chi-Square Test For Independence, the *observed frequencies* are the true values that we’ve seen, in other words the actual rates per group in the data itself.  The *expected frequencies* are what we would *expect* to see based on *all* of the data combined.

The below code:

* Summarises our dataset to a 2x2 matrix for *signup_flag* by *mailer_type*
* Based on this, calculates the:
    * Chi-Square Statistic
    * p-value
    * Degrees of Freedom
    * Expected Values
* Prints out the Chi-Square Statistic & p-value from the test
* Calculates the Critical Value based upon our Acceptance Criteria & the Degrees Of Freedom
* Prints out the Critical Value

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
Based upon our observed values, we can give this all some context with the sign-up rate of each group.  We get:

* Mailer 1 (Low Cost): **32.8%** signup rate
* Mailer 2 (High Cost): **37.8%** signup rate

From this, we can see that the higher cost mailer does lead to a higher signup rate.  The results from our Chi-Square Test will provide us more information about how confident we can be that this difference is robust, or if it might have occured by chance.

We have a Chi-Square Statistic of **1.94** and a p-value of **0.16**.  The critical value for our specified Acceptance Criteria of 0.05 is **3.84**

**Note** When applying the Chi-Square Test above, we use the parameter *correction = False* which means we are applying what is known as the *Yate's Correction* which is applied when your Degrees of Freedom is equal to one.  This correction helps to prevent overestimation of statistical signficance in this case.

___

<br>
# Analysing the Results <a name="chi-square-results"></a>

At this point we have everything we need to understand the results of our Chi-Square test - and just from the results above we can see that, since our resulting p-value of **0.16** is *greater* than our Acceptance Criteria of 0.05 then we will _retain_ the Null Hypothesis and conclude that there is no significant difference between the signup rates of Mailer 1 and Mailer 2.

We can make the same conclusion based upon our resulting Chi-Square statistic of **1.94** being _lower_ than our Critical Value of **3.84**

To make this script more dynamic, we can create code to automatically interpret the results and explain the outcome to us...

```python

# print the results (based upon p-value)
if p_value <= acceptance_criteria:
    print(f"As our p-value of {p_value} is lower than our acceptance_criteria of {acceptance_criteria} - we reject the null hypothesis, and conclude that: {alternate_hypothesis}")
else:
    print(f"As our p-value of {p_value} is higher than our acceptance_criteria of {acceptance_criteria} - we retain the null hypothesis, and conclude that: {null_hypothesis}")

>> As our p-value of 0.16351 is higher than our acceptance_criteria of 0.05 - we retain the null hypothesis, and conclude that: There is no relationship between mailer type and signup rate.  They are independent


# print the results (based upon p-value)
if chi2_statistic >= critical_value:
    print(f"As our chi-square statistic of {chi2_statistic} is higher than our critical value of {critical_value} - we reject the null hypothesis, and conclude that: {alternate_hypothesis}")
else:
    print(f"As our chi-square statistic of {chi2_statistic} is lower than our critical value of {critical_value} - we retain the null hypothesis, and conclude that: {null_hypothesis}")
    
>> As our chi-square statistic of 1.9414 is lower than our critical value of 3.841458820694124 - we retain the null hypothesis, and conclude that: There is no relationship between mailer type and signup rate.  They are independent

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
