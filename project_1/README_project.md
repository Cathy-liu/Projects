# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 1: Standardized Test Analysis

### Overview
The SAT and ACT are standardized tests that many colleges and universities in the United States require for their admissions process. This score is used along with other materials such as grade point average (GPA) and essay responses to determine whether or not a potential student will be accepted to the university.

A new version of the SAT is in place as of March 2016 that includes dramatic revisions to the test's scoring and content. The old 2400-point scale has been replaced by the 1600-point system that was in use prior to the last major round of revisions in 2005. The essay, which is now optional, is scored separately. Changes made to the SAT in 2016 have made it easier.

The SAT has two sections of the test: Evidence-Based Reading and Writing and Math ([*source*](https://www.princetonreview.com/college/sat-sections)). The ACT has 4 sections: English, Mathematics, Reading, and Science, with an additional optional writing section ([*source*](https://www.act.org/content/act/en/products-and-services/the-act/scores/understanding-your-scores.html)). They have different score ranges, which you can read more about on their websites or additional outside sources (a quick Google search will help you understand the scores for each test):
* [SAT](https://collegereadiness.collegeboard.org/sat)
* [ACT](https://www.act.org/content/act/en.html)

Standardized tests have long been a controversial topic for students, administrators, and legislators. Since the 1940's, an increasing number of colleges have been using scores from sudents' performances on tests like the SAT and the ACT as a measure for college readiness and aptitude ([*source*](https://www.minotdailynews.com/news/local-news/2017/04/a-brief-history-of-the-sat-and-act/)). Supporters of these tests argue that these scores can be used as an objective measure to determine college admittance. Opponents of these tests claim that these tests are not accurate measures of students potential or ability and serve as an inequitable barrier to entry.

This project covers:
- Background
- Data Import & Cleaning
- Exploratory Data Analysis
- Data Visualization
- Conclusions and Recommendations

### Problem Statement
The new format for the SAT was released in March 2016. Changes made to the SAT in 2016 have made it easier. As such, there might be switch in participation rate across the states between ACT and SAT. Therefore, the purpose of the project is to review the trend of participation rate from year 2017 to 2019 for both ACT/SAT and to identify if there is increase of participation rate on SAT.
 
### Datasets

#### Provided Data

There are 8 datasets included in the [`data`](./data/) the project for analysis from year 2017 and 2019 on ACT and SAT.

* [`act_2017.csv`](./data/act_2017.csv): 2017 ACT Scores by State ([source](https://blog.prepscholar.com/act-scores-by-state-averages-highs-and-lows))
* [`act_2018.csv`](./data/act_2018.csv): 2018 ACT Scores by State ([source](https://blog.prepscholar.com/act-scores-by-state-averages-highs-and-lows))
* [`act_2019.csv`](./data/act_2019.csv): 2019 ACT Scores by State ([source](https://blog.prepscholar.com/act-scores-by-state-averages-highs-and-lows))
* [`act_2019_ca.csv`](./data/act_2019_ca.csv): 2019 ACT Scores in California by School
* [`sat_2017.csv`](./data/sat_2017.csv): 2017 SAT Scores by State ([source](https://blog.collegevine.com/here-are-the-average-sat-scores-by-state/))
* [`sat_2018.csv`](./data/sat_2018.csv): 2018 SAT Scores by State ([source](https://blog.collegevine.com/here-are-the-average-sat-scores-by-state/))
* [`sat_2019.csv`](./data/sat_2019.csv): 2019 SAT Scores by State ([source](https://blog.prepscholar.com/average-sat-scores-by-state-most-recent))
* [`sat_act_by_college.csv`](./data/sat_act_by_college.csv): Ranges of Accepted ACT & SAT Student Scores by Colleges ([source](https://www.compassprep.com/college-profiles/))

### Data Dictionary
2017-2019 ACT&SAT Data Dictionary Entry after merge: 

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**State**|*integer*|2017-2019 ACT&SAT|State across US.| 
|**Participation_19_x**|*float*|2019 ACT|The percentage of student who join ACT exam by state.|
|**Composite_19**|*float*|2019 ACT|The size of the population being tested. |
|**Participation_18_x**|*float*|2018 ACT|The percentage of student who join ACT exam by state.|
|**Composite_18**|*float*|2018 ACT|The size of the population being tested. |
|**Participation_17_x**|*float*|2017 ACT|The percentage of student who join ACT exam by state.|
|**Composite_17**|*float*|2017 ACT|The size of the population being tested. |
|**Participation_19_y**|*float*|2019 SAT|The percentage of student who join ACT exam by state.|
|**Total_19**|*float*|2019 SAT|Total SAT score range of 400-1600. |
|**Participation_18_y**|*float*|2018 SAT|The percentage of student who join ACT exam by state.|
|**Total_18**|*float*|2018 SAT|Total SAT score range of 400-1600. |
|**Participation_17_y**|*float*|2017 SAT|The percentage of student who join ACT exam by state.|
|**Total_17**|*float*|2017 SAT|Total SAT score range of 400-1600. |

## Exploratory Data Analysis
**Question: Which states have the highest and lowest participation rates for the 2017, 2018, or 2019 SAT and ACT?**
By examined 2019 data, it shows that 2019 ACT highest participation rate is 100 percent. Total of 15 states achieve the 100 percent rate, which are Alabama, Kentucky, Wyoming. Wisconsin, Utah, Tennessee, Oklahoma, Ohio, North Carolina, Nevada, Nebraska, Mississippi, Louisiana, Montana and Arkansas.
2019 SAT highest participation rate is 100 percent. Total of 8 states achieve the 100 percent rate, which are Rhode Island, Illinois, Michigan, Colorado, Connecticut, Delaware, Florida and Idaho.
2019 ACT lowest participation rate 6.0 percent which is Maine.
2019 SAT lowest participation rate 2.0 percent which is North Dakota.

**Question: Which states have the highest and lowest mean total/composite scores for the 2017, 2018, or 2019 SAT and ACT?**
By examined 2019 data, it shows that 2019 ACT highest mean composiste is 25.5 contributed by the states Massachusetts and Connecticut.
2019 SAT highest mean total is 1284.0 contributed by the states of Minnesota.
2019 ACT lowest mean composiste is 17.9 which is from the state of Nevada.
2019 SAT lowest mean total is 943.0 which is from the states of West Virginia.

**Question: Do any states with 100% participation on a given test have a rate change year-to-year?**
Yes, the 100% participation rate on ACT were changed from year 2017 to 2019. The states are Minnesota, Missouri, South Carolina and Colorado.
For SAT, there are 3 states show improving participation rate from year 2017 to 2019, which are Florida, Illinois and Rhode Island. However, there are one state show decreasing trend in 100% participation rate from year 2017 to 2019, which is District of Columbia.

**Question: Do any states show have >50% participation on *both* tests each year?**
In year 2019, there are 4 states show >50% participation on both tests, which are South Carolina, North Carolina, Hawaii and Florida.
In year 2018, there are 5 states show >50% participation on both tests, which are South Carolina, North Carolina, Hawaii, Georgia and Florida.
In year 2017, there are 3 states show >50% participation on both tests, which are Hawaii, Georgia and Florida.

**Question: Which colleges have the highest median SAT and ACT scores for admittance?**
California Institute of Technology have the highest median SAT and ACT scores for admittance.

**Question: Which California school districts have the highest and lowest mean test scores?**
Lynbrook High and Monta Vista High have the highest mean test while Citrus High (Continuation) has the lowest mean test score in 2019 ACT.

## Visualize the Data
Seaborn's heatmap:
The correlation of SAT and ACT participation rates show negatively correlated to each other from year 2017 to 2019. For example, the correlation between ACT Participation 19 and SAT Participation 19 are -87% correlated to each other. This means that states that have high ACT participation rates tend to have low SAT participation rates and vice versa.

Histograms:
3 histograms are plotted for ACT year 2017-2019 on the left while another 3 histograms are plotted for SAT year 2017-2019 on the right. For ACT test, it shows peak at the right as the 100% participation rate show higher frequency. However, for SAT test, it shows peak at the left as the 100% participation rate are lower as compared to ACT test. The distribution are not normal for both SAT and ACT. Low participation was prevalent with the SAT for year 2017-2019 as compared to ACT test.

Barplots:
With the 3 barplots shown above from year 2017 to year 2019, there are increase in state by achieving 100% participation rate for SAT. There were only 3 states shown 100% participation rate in year 2017. It further increased to 5 states by year 2018 and 8 states by year 2019. In contrast, although ACT had higher participation rate but it shown decreasing trend in participation rate. There were 17 states achieved 100% participation rate in 2017 and 2018, however, it dropped to 15 states in 2019. 

Boxplots:
In addition to the summary statistics and historgrams above, these boxplots illustrate the distribution of participation rates and scores.The SAT score distributions between 2017 and 2018 were largely similar. Except distribution in 2019, it shows much lower total were scored in year 2019. For ACT, the score distributions were largely similar as well with no big variations. 
Comparing SAT and ACT participation rates, SAT participations have a lower median between 2017 and 2018, indicating that more states had higher participation rates for ACT. However, SAT shows higher median in year 2019 as compared to ACT participation. This indicates that there is increase in participating SAT test.

Scatter plots:
The participation rate were further examined with score to understand the correlation in between. Both SAT and ACT subplot show that high participation rate are associated with low composite/total score while low participation rate are associated with high composite/total score. Therefore, it can be concluded that participation rate are negatively correlated to score in both SAt and ACT.

## Conclusions and Recommendations
From the above analysis, the key takeaways are:
- High participation rates in one test usually means low participation rates in the other. The states that have high SAT participation rates tend to have low ACT participation rates and vice versa.
- Participation rates are negatively correlated with test scores. This suggests that the higher the participation rate, the lower the average. This probably occurs because in cases of low participation only highly motivated students are likely to take exams. High participation rates bring in a wider range of student skills lowering the average.
- Generally, low participation was prevalent with the SAT as compared to ACT test. However, the participation rate in SAT have increased in year 2019 by comparing the 2019 SAT/ACT participation median.

Recommendation to improve SAT participation rate:
- SAT is more popular among the coastal states, whereas ACT is more popular inland. Based on both an examination of the data and a review of state college entrance exam testing policy, it is clear that participation in such tests is heavily influenced by state policy towards testing. Therefore, we recommend to target those inland school which have not already done so can consider making SAT as mandatory high school graduation requirement. In this project, we recommend to target Iowa as it has one of the lowest overall participation rate for SAT based on our data. 