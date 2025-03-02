# League of Legends First Achievements Analysis
Author: Erika Tong

# Introduction

## General Introduction

This is a data science project conducted at UCSD which examines a professional 
data set developed by Oracle's Elixir and contains over 10,000 League of Legends 
competitive matches from 2022. In this project there are various states of analysis 
starting with exploratory data analysis including the missingness of values, then 
hypothesis testing, creating models for a prediction problem, and concludes with 
a fairness analysis. The primary focus of the project is to investigate the 
significance of the first achievements gained throughout the game and its impact 
on outcomes.

League of Legends (LoL) is a multiplayer online battle arena game developed by 
Riot Games and played by millions worldwide. In the game there are many first 
achievements that can be gained by a side including "first blood", "first dragon",
"first herald", "first baron", "first tower", and "first midtower". These achievements
can set the tone throughout the match and holds significant weight in the outcome 
of the match.

The central question I am interested in investigating is: **How does gaining the 
first achievements (first blood, first dragon, first herald, first tower, first 
baron, first midtower) impact the outcome?** I will build a prediction model to 
predict the outcome of a match. This model holds potential to enhance teams 
strategic planning, gaming insights, and performance analysis by predicting outcomes
based on the teams historical data.

## Dataset Introduction
The original dataset contains 161 columns representing gameplay statistics and 
match outcomes with rows for each player on both teams and a row for each team 
with summary data. For this project I'll be focusing on a subset of the original 
data set containing only the team rows (25,098) and 12 of the columns. Here is a
brief introduction to the columns essential for my analysis:

- **side**: This designates what side of the map a team was on, distinguishing
between the "blue" and "red" side.
- **league**: This designates the specific league tournament the match took place 
in. 
- **teamname**: This designates the professional team that played the match.
- **kills**: This quantifies the total number of enemy champions the team killed
during the match.
- **deaths**: This quantifies the total number of champions on the team that died 
during the match.
- **result**: This designates the outcome of a match, 1 indicates the team won and 
0 indicates the team lost.
- **first_blood**: This binary column indicates 1 if the team gained first blood- 
the first kill- of the match and 0 otherwise. 
- **first_dragon**: This binary column indicates 1 if the team gained the first dragon
of the match and 0 otherwise.
- **first_herald**: This binary column indicates 1 if the team gained the first herald 
of the match and 0 otherwise.
- **first_baron**: This binary column indicates 1 if the team gained the first baron 
of the match and 0 otherwise.
- **first_tower**: This binary column indicates 1 if the team destroyed the first tower
of the match and 0 otherwise.
- **first_midtower**: This binary column indicates 1 if the team destroys the first
midtower of the match and 0 otherwise.

# Data Cleaning and Exploratory Data Analysis
## Data Cleaning
Given the original data set contains vast amount of statistical data, the first step 
for data analysis is to clean the data, keeping only relevant columns and rows to make 
my analysis more efficienct and convenient. First I filtered the data set to keep 
only the rows representing the summary data for a team's match since my focus is on
the outcome of the team as a whole. Then I kept only the revelant columns: **side**, 
**league**, **teamname**, **kills**, **deaths**, **result**, **firstblood**, 
**firstdragon**, **firstherald**, **firstbaron**, **firsttower**, **firstmidtower**.
To make it easier to read I renamed the columns that start with "first" so no they 
are: **first_blood**, **first_dragon**, **first_herald**, **first_baron**, 
**first_tower**, **first_midtower**. Lastly I checked the data types for each of 
my columns to see if I needed to conduct any data type conversions and found that 
no conversions were needed. 

Below is the head of my team_data dataframe.

| side   | league   | teamname                 |   kills |   deaths |   result |   first_blood |   first_dragon |   first_herald |   first_baron |   first_tower |   first_midtower |
|:-------|:---------|:-------------------------|--------:|---------:|---------:|--------------:|---------------:|---------------:|--------------:|--------------:|-----------------:|
| Blue   | LCKC     | BRION Challengers        |       9 |       19 |        0 |             1 |              0 |              1 |             0 |             1 |                1 |
| Red    | LCKC     | Nongshim Esports Academy |      19 |        9 |        1 |             0 |              1 |              0 |             0 |             0 |                0 |
| Blue   | LCKC     | T1 Esports Academy       |       3 |       16 |        0 |             0 |              0 |              1 |             0 |             0 |                0 |
| Red    | LCKC     | Liiv SANDBOX Youth       |      16 |        3 |        1 |             1 |              1 |              0 |             1 |             1 |                1 |
| Blue   | LPL      | Oh My God                |      13 |        6 |        1 |             0 |            nan |            nan |           nan |           nan |              nan |

Note: I kept nan values for missingness assessment later in the project
## Exploratory Data Analysis
In my exploratory Data Analysis I will perform univariate analysis to examine the
distribution of single variable. Then I will perform bivariate analysis to examine the 
relationship between multiple variables and finally grouped data to examine aggregate 
statistics.
### Univariate Analysis
For this analysis I created a new column that contains the total number of first 
achievements a team gained during the match. The plot below shows the distribution 
from 0-6 total first achievements that teams can gain for their side in a match.
It appears like it is more rare to achieve all 6 but more common to achieve 1. This 
could give some insight to team strategy and the importance of gaining achievements 
to the outcome.
<iframe
	src = "assets/Univariate_plot.html"
	width = "800"
	height = "600"
	frameborder = "0"
></iframe>

### Bivariate Analysis
For this analysis I examined the distribution of match results based on each first 
achievemnt. The plot below shows that teams tend to win more than lose the match after
gaining the achievement. Some of the first achievements such as "first_baron" seems 
to have significant more wins than losses compared to the other achievements. This 
shows there may be a relationship between match outcomes and first achievements,
later we will look into this relationship more.
<iframe
	src = "assets/Bivariate_plot.html"
	width = "800"
	height = "600"
	frameborder = "0"
></iframe>

### Grouping and Aggregates 
For this analysis I created a pivot table below with a row for each unique team that 
participated in 2022 to find the average number of time a team gained a first 
achievement. By looking at the values we can see if some teams favor one achievemnet
or are better at getting it during their matches. This can give insight into game 
strategy and what achievements teams focus more or less on achieving. 

|   first_baron |   first_blood |   first_dragon |   first_herald |   first_midtower |   first_tower |
|--------------:|--------------:|---------------:|---------------:|-----------------:|--------------:|
|      0.526316 |      0.473684 |       0.473684 |       0.486842 |         0.486842 |      0.421053 |
|      0.487179 |      0.495726 |       0.376068 |       0.444444 |         0.65812  |      0.487179 |
|      0.649351 |      0.597403 |       0.311688 |       0.467532 |         0.714286 |      0.597403 |
|      0.666667 |      0.5      |       0.416667 |       0.333333 |         0.5      |      0.583333 |
|      0.25     |      0.25     |       0.625    |       0.375    |         0.25     |      0.375    |

# Assessment of Missingness
## Not Missing at Random (NMAR) Analysis
Several columns in my dataframe have missing values. After looking through the 
missing values I do not believe there are any columns that are NMAR. The values 
that are missing look to be completely random or can be explained by another column.

## Missingness Dependency
After examining the missing values I decided to investigate if the missingness 
in the first_dragon column depends on the league column. To test the missingness 
I'll perform a permutation test with a significance level of 0.05 and Total Variance 
Distance (TVD) as my test statistic.
**Null hypothesis**: The distribution of league when first_dragon is missing is the 
same as the distribtion of league when first_dragon is not missing.
**Alternative Hypothesis**: The distribution of league when first_dragon is missing 
is not the same as the distribution of league when first_dragon is not missing.
Below is the first few rows of a pivot table showing the distribution of league 
when first_dragon is missing (True) and not missing (False).
| league   |      False |      True |
|:---------|-----------:|----------:|
| ASCI     | 0          | 0.0390914 |
| CBLOL    | 0.0228041  | 0         |
| CBLOLA   | 0.0202703  | 0         |
| CDF      | 0.00713213 | 0         |
| CT       | 0.00243994 | 0         |

After I ran a permutation test by shuffling league 500 times to collect 500 simulated 
TVD values. I got an observed TVD value of 0.992604 and a p-value of 0.0. Since my 
p-value of 0.0 is less than my significance level of 0.05 I reject the null in favor 
of the alternative suggesting the missingness of first_dragon is dependent on the 
league column, indicating that some leagues may have more frequently missing values. 
Below is a plot of the empirical distribution of TVD's from my permutation test.
<iframe
	src = "assets/Missingness_plot.html"
	width = "800"
	height = "600"
	frameborder = "0"
></iframe>

# Hypothesis Testing

# Framing a Prediction Problem

# Baseline Model

# Final Model

# Fairneess Analysis