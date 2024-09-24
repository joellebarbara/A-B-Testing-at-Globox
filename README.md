# A/B Test Report: Food and Drink Banner

## Overview
This project presents a detailed analysis of an A/B test conducted to evaluate the effectiveness of introducing an additional banner on the GloBox homepage. The goal was to determine whether the banner (Treatment group) would increase conversion rates compared to the current homepage layout (Control group).

## Table of Contents
- [Overview](#overview)
- [Purpose](#purpose)
- [Hypotheses](#hypotheses)
- [Methodology](#methodology)
- [Results](#results)
- [Conclusion](#conclusion)
- [Recommendations](#recommendations)
- [Installation](#installation)
- [Usage](#usage)
- [Technologies Used](#technologies-used)
- [Contributing](#contributing)
- [License](#license)
- [Authors](#authors)

## Purpose
The primary objective was to assess the impact of adding a food & drink banner on user conversion rates. The analysis was focused on determining if the Treatment group, which viewed the new banner, exhibited a higher conversion rate compared to the Control group, which did not see the banner.

## Hypotheses

### Conversion Rate
- **Null Hypothesis (H0)**: There is **no difference** in conversion rates between the Control and Treatment groups.
- **Alternative Hypothesis (H1)**: There **is a difference** in conversion rates between the Control and Treatment groups.

### Average Amount Spent per User
- **Null Hypothesis (H0)**: There is **no difference** in the average amount spent per user between the Control and Treatment groups.
- **Alternative Hypothesis (H1)**: There **is a difference** in the average amount spent per user between the Control and Treatment groups.

## Methodology
- **Test Design**: The A/B test was conducted using the mobile version of GloBox. The Control group (A) did not have a banner, while the Treatment group (B) saw the food & drink banner.
- **Duration**: The test spanned from January 25, 2023, to February 6, 2024.
- **Success Metrics**: Conversion rates and average amount spent per user were analyzed. Confidence intervals were calculated to validate the significance of the results.

## Results
- The Treatment group showed a **statistically significant increase in conversion rates** compared to the Control group, with a **p-value of 0.0001**.
- Power analysis determined the ideal sample size, confirming that the results were robust and statistically valid.

## Conclusion
The results demonstrate that the inclusion of the banner led to a substantial improvement in conversion rates. This highlights the effectiveness of visual interventions in driving user engagement and boosting overall revenue.

## Recommendations
- **Next Steps**: It is recommended to fully implement the banner across all user segments to capitalize on the observed increase in conversion rates.
- **Further Analysis**: To optimize the banner’s performance, additional analyses like segmentation and cohort studies are recommended, along with ongoing testing and refinement based on user feedback.

## Installation
```bash
git clone https://github.com/joellebarbara/A-B-Testing-at-Globox
cd A-B-Testing-at-Globox
pip install -r requirements.txt
```

## Usage
To run the analysis, execute the following command:
```bash
python ab_test_analysis.py
```

## Technologies Used
- Python for data analysis and testing
- Libraries: pandas for data manipulation, matplotlib for plotting results, scipy for statistical tests
- SQL for querying the database
- Tableau for data visualization

## Contributing
Contributions are welcome! Please fork the repository and submit a pull request. For major changes, open an issue first to discuss your ideas.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Authors
- **Joelle Barbara** - [GitHub Profile](https://github.com/joellebarbara)


