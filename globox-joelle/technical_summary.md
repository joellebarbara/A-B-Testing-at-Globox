# A/B Test Report: Food and Drink Banner

## Purpose
In this comprehensive analysis, a detailed examination has been conducted to evaluate the outcomes of an A/B test aimed at gauging the
effectiveness of an additional banner (Treatment group) in contrast to the current homepage layout (Control group). The investigation reveals
compelling evidence that the treatment group yielded a notably substantial surge in conversion rates, supported by a remarkably low p-value of
0.0001. Given the favorable cost dynamics associated with launching this feature, the recommendation stands strong in favor of implementing
the new banner to strategically harness and optimize the observed enhancement in conversion rates.
    
## Hypotheses

### Conversion Rate
- **Null hypothesis (H0)**- There is **no difference** in the conversion rate per user between Control and Treatment groups. 
- **Alternative hypothesis (H1)**- There **is difference** in the conversion rate per user between Control and Treatment groups.

### Average Amount Spent per User
- **Null hypothesis (H0)**- There is **no difference** in the average amount spent per user between Control and Treatment groups. 
- **Alternative hypothesis (H1)**- There **is difference** in the average amount spent per user between Control and Treatment groups. 


## Methodology
### Test Design
- **Population:** Both groups were using the Mobile Version of GloBox. The control group (A) remained banner-free and the test group (B) were introduced to the food & beverage banner.
- **Duration:** Test started at 2023-01-25 and ended at 2024-02-06.
- **Success Metrics:** First metrics is conversion rate and the second one is average amount spent per user. Moreover, caulated confidence intervals.

## Results
### Data Analysis
- **Pre-Processing Steps:** 

Calculating the user conversion rate for the control and treatment groups:
```sql
WITH user_activity_group AS (
 SELECT us.id,
 g.group,
 CASE
 WHEN SUM(ac.spent) > 0 THEN 1
 ELSE 0
 END AS converted
 FROM users AS us
 LEFT JOIN activity AS ac ON us.id = ac.uid
 JOIN groups AS g ON g.uid = us.id
 GROUP BY us.id, g.group
 )
SELECT "group",
COUNT( DISTINCT id) AS total_users,
SUM(converted) AS total_converted,
ROUND(SUM(converted) * 100.0 /COUNT(DISTINCT id),2) AS conversion_rate
FROM user_activity_group
GROUP BY "group";
```

Data for Hypothesis testing:
```sql

WITH user_activity_group AS (
 SELECT us.id, us.country, us.gender, ac.device, g.group,
 COALESCE(ROUND(SUM(spent),2),0) AS total_spent,
 CASE
 WHEN COALESCE(ROUND(SUM(ac.spent),2),0) > 0 THEN 1
 ELSE 0
 END AS converted
 FROM users AS us
 LEFT JOIN activity AS ac ON us.id = ac.uid
 JOIN groups AS g ON g.uid = us.id
 GROUP BY us.id, us.country, us.gender, ac.device, g.group
 )
SELECT id, country, gender, device AS device_type,"group" as test_group, total_spent,
converted
FROM user_activity_group;

```
Calculating the average amount spent per user for the control andtreatment groups, including users who did not convert query:
```sql
WITH user_activity_group AS (
 SELECT us.id, ac.spent, g.group
 FROM users AS us
 LEFT JOIN activity AS ac ON us.id = ac.uid
 JOIN groups AS g ON g.uid = us.id
 GROUP BY us.id, ac.spent, g.group
 )
SELECT "group",
ROUND(SUM(spent) /COUNT(DISTINCT id),2) AS avg_amt_spent_per_user
FROM user_activity_group
GROUP BY "group";

- **Statistical Tests Used:** For Conversion Rate used Two-sample z-test for a difference in proportions, for Average Amount used Two-sample t-test for a difference in means.
- **Results Overview:** Average Amount- The p-value, standing at 0.9438, indicates a lack of statistical significance, thereby leading to the retention of the null hypothesis. Consequently, there exists no discernible variance in the mean expenditure between the two groups under examination. Conversion Rate- The obtained p-value of 0.0001 attains statistical significance, leading to the rejection of the null hypothesis. This implies a discernible distinction in the conversion rates between the two groups.
``` 

Preparing for advaced tasks:
```sql
WITH user_activity_group AS (
 SELECT us.id, us.country, us.gender, ac.device, g.group, g.join_dt AS join_date, ac.dt AS
activity_date,
 COALESCE(ROUND(SUM(spent),2),0) AS total_spent,
 CASE
 WHEN COALESCE(ROUND(SUM(ac.spent),2),0) > 0 THEN 1
 ELSE 0
 END AS converted
 FROM users AS us
 LEFT JOIN activity AS ac ON us.id = ac.uid
 JOIN groups AS g ON g.uid = us.id
 GROUP BY us.id, us.country, us.gender, ac.device, g.group, ac.dt, g.join_dt,ac.dt
 )
SELECT id, country, gender, device AS device_type, total_spent, "group" as test_group,
converted, join_date, activity_date
FROM user_activity_group;
```

### Findings

## Interpretation
- **Outcome of the Test(s):** Average Amount Spent per User - We fail to reject the null hypothesis. Conversion Rate - We reject the null hypothesis
- **Confidence Level:** 95% confidence interval for the difference in the avarge amount per user is between -0.439 and 0.471. Confidence interval for the difference in the conversion rate is between -0.0107 and 0.0035

##Forward Findings

###**Novelty Effects:**
The graph in tableau shows that the distribution of the number of user visiting the website each day is
almost equally split between the two group. Therefore, we can assume that there is no novelty
effect affecting the experiment

###**Power Analysis:**
Using a 60% Statistical Power with 10% minimum detectable effect and the 3.92% baseline
conversion rate of the Control group, the ideal sample size is 24,144 per group. We can then
assume that our sample size is normally distributed between the 2 groups.




## Conclusions
- **Key Takeaways:** Through our analysis, we have discerned that the inclusion of the banner significantly enhances conversion rates, thus underscoring its potential for augmenting user engagement and revenue generation. This emphasizes the pivotal role of strategic interventions in shaping consumer behavior and bolstering business performance.
  
- **Limitations/Considerations:** While our findings are promising, it's crucial to acknowledge potential biases stemming from factors such as user preferences and external market dynamics. Additionally, the analysis might not capture all nuances of user behavior, warranting further exploration and refinement.

## Recommendations
- **Next Steps:** In light of the compelling data supporting the banner's efficacy, the immediate course of action entails its full-scale integration across all user segments. This initiative promises to fortify GloBox's competitive edge by maximizing conversion rates and amplifying user interaction.
  
- **Further Analysis:** To refine our understanding and optimize outcomes, iterative analysis is essential. Exploring avenues such as segmentation analysis and cohort studies can unveil deeper insights into user behavior patterns and preferences. Additionally, continuous testing coupled with a granular examination of user feedback can furnish valuable insights for refining the banner's design and functionality, thereby sustaining its impact on conversion rates and revenue generation.
