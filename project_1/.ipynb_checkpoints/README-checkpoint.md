**Problem statement**

Given the datasets on pass rate for the ACT and SAT tests of all the schools in California, I wish to find out the correlation between the pass rates of the two exams on three levels:
SAT pass rates between Grade 11 test takers and Grade 12 test takers from the same school;
the correlation between the pass rates of the two exams at a school level;
the correlation between the pass rates of the two exams at a county level.

**Data dictionary**

The raw data are from two datasets: act_2019_ca.csv and sat_2019_ca.csv; after cleasing the combined dataset is named merged_19.csv. And the data dictionary as follows.

|Feature|Type|Dataset|Description|
|---|---|---|---|
|cds|14-character-string|merged_19.csv|The unique code for each school. | 
|enroll_12|float|merged_19.csv|The number of enrolled students for Grade 12 in Year 2018-2019. |
|num_act|float|merged_19.csv|The number of ACT takers from Grade 11/12 in Year 2018-2019.|
|act_pass_21|float|merged_19.csv|The number ACT takers whose composite ACT score has passed 21 in Year 2018-2019. One's composite ACT score means the average score from the four scores (English, mathematics, reading, science).|
|num_sat_12|float|merged_19.csv|The number of students from Grade 12 who took SAT test in Year 2018-2019.|
|sat_pass_12|float|merged_19.csv|The number of SAT takers from Grade 12 whose scores have both passed the benchmark score for the EWR test and the Math test in Year 2018-2019.|
|enroll_11|float|merged_19.csv|The number of SAT takers from Grade 11 in Year 2018-2019.|
|sat_pass_11|float|merged_19.csv|The number of SAT takers from Grade 11 whose scores have both passed the benchmark score for the EWR test and the Math test in Year 2018-2019.|
|act_pt_r|float|merged_19.csv|The participation rate of ACT test among Grade 11 and 12 students.|
|act_ps_r|float|merged_19.csv|The pencentage of ACT test takers whose score has passed 21. |
|sat_pt_r_12|float|merged_19.csv|The participation rate of SAT test among Grade 12 students. |
|sat_pt_r_11|float|merged_19.csv|The participation rate of SAT test among Grade 11 students. |
|sat_pt_r|float|merged_19.csv|The participation rate of SAT test among Grade 11 and 12 students. |
|sat_ps_r|float|merged_19.csv|The participation rate of SAT test among Grade 11 and 12 studnets. |


**Brief summary of your analysis**

Based on the number of enrolled students for Grade 11 and 12, the number of test takers, and the number of students that have actually passed the ACT test/passed a benchmark score in the SAT test, I calculated the participation rate and pass rate for Grade 11 and 12 students for both ACT and SAT tests for all the public schools in California, and obtained some key statisitics in these features. 

As there are over 13,00 schools in the combined dataset, I further aggregated the data based on the county each school is located in (by the 'Ccode' column which stands for County Code). County is selected as the level to aggregate the data because there is only a quite limited number of counties (55 counties in California) and only 53 present in the dataset. After that, statistics of the key features (participation rate and pass rate) are obtained at the county level, and the counties that perform the best are identified. 

Subsequently scatterplots have been used to identify the possible correlations between ACT and SAT pass rates on the school level and also on the county level, as well as possible correlation between SAT performance by students from different grades from the same school. 


**Conclusions/recommendations**
From the EDA and visualization sections, the conclusions we can make are:
1. On a school level, there is positive correlation between the ACT and SAT pass rate;
2. Also on a school level, there is positive correlation between SAT pass rate by Grade 11 test takers and Grade 12 test takers;
3. On a county level, there is also a positive correlation between ACT and SAT pass rates.

**Additional information sources**
The meaning of each column in act_2019_ca.csv: http://wgetsnaps.github.io/cde.ca.gov--ds-sp-ai/ds/sp/ai/reclayoutact.asp.html

The administration levels in California. Basically there are four levels from a high to low hierarchy - state, county, district, and school level in the SAT and ACT records system.
https://www.cde.ca.gov/re/pr/satdata.asp