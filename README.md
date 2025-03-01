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

- ==side==: This designates what side of the map a team was on, distinguishing
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

## Univariate Analysis
## Bivariate Analysis
## Integrating Aggregates 

# Assessment of Missingness

# Hypothesis Testing

# Framing a Prediction Problem

# Baseline Model

# Final Model

# Fairneess Analysis