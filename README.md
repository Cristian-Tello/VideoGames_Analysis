# Data Analytics applied to the global video game market

## Problem Description

Ice, an online store dedicated to selling video games globally, seeks to identify the factors that determine a title's commercial success. To do this, they have a dataset that includes user and expert reviews, genres, platforms (such as Xbox and PlayStation), ESRB ratings, and historical sales records dating back to 2016.

The challenge is to analyze this data to discover behavioral patterns and key variables that influence a video game's performance in the market. The goal is to generate information that will allow them to identify promising projects and design more effective advertising campaigns.

The analysis is presented in a simulated context: December 2016, with the task of forecasting 2017 sales. However, the project's main value lies in the practical experience of working with data, applicable to any time frame.

The dataset's rating column, which reflects the age classification assigned by the ESRB, adds an additional dimension to the study, allowing for an evaluation of how content restrictions can impact the acceptance and success of video games.

## Data
1. Name	
2. Platform	
3. Year_of_Release	
4. Genre	
5. NA_sales	= North American sales in millions of US dollars
6. EU_sales	= European sales in millions of US dollars
7. JP_sales	= Japan sales in millions of US dollars
8. Other_sales	= Sales in other countries in millions of US dollars
9. Critic_Score = maximum of 100	
10. User_Score	= maximum of 10
11. Rating = ESRB

# Applied Libraries:
```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
from scipy import stats
```
# Conclusions on data types
* Columns exhibit inconsistencies in their data types
- Year_of_Release -> INT
- User_Score -> FLOAT

* Missing values
- Name: 16713 = 2 Missing values
- Year_of_Release: 16446 = 269 Missing values ​​-> 1% of the data is missing
- Genre: 16713 = 2 Missing values
- Critic_Score: 8137 = 8578 Missing values ​​-> 50% of the data is missing and should be deleted, but it will be assigned a missing value using NumPy (np.nan)
- User_Score: 10014 = 6701 Missing values ​​-> 40% of the data is missing
- Rating: 9949 = 6766 Missing values ​​-> 40% of the data is missing Missing values

* Duplicate values ​​and rows

- Remove 3 columns (#16230, 659, 14244) because they are duplicate columns and do not contribute any value to the data.

## Data Analysis
```python
# Counting games in different years
games_launch_years = clean_data['year_of_release'].value_counts().sort_index()

plt.figure(figsize=(12, 8))
games_launch_years.plot(kind='bar', color='skyblue')
plt.title('Games Launch in differents years', fontsize=20)
plt.xlabel('Years', fontsize=16)
plt.ylabel('Quantity Games', fontsize=16)
plt.grid(axis='y', alpha=0.3)
plt.show()
```
<p align="center">
  <img src="https://github.com/Cristian-Tello/VideoGames_Analysis/blob/main/Games%20Launch%20in%20differents%20years.png" alt="Sample Image">
</p>

# General Conclusion for Games Lauch in different years.

The graph shows how the video game industry experienced sustained growth from the 1980s, reaching its peak between 2007 and 2009 with over 1,400 releases annually. 

This boom reflects market consolidation and platform expansion during that period. Subsequently, a decrease in the number of releases is observed, which can be attributed to changes in company strategy, a greater focus on quality over quantity, and the transition to new digital distribution models. Overall, the visualization allows us to understand the evolution of the sector and the factors that have shaped its dynamics over time.

<p align="center">
  <img src="https://github.com/Cristian-Tello/VideoGames_Analysis/blob/main/Platform%20Sales.png" alt="Sample Image">
</p>

# Platform sales Conclusion

The chart clearly shows the PlayStation 2 (PS2) leading the way as the top-selling platform, solidifying its status as a historical benchmark in the gaming industry. It is followed by the Xbox 360 and PlayStation 3, reflecting the intense competition between Sony and Microsoft during that generation. The performance of consoles like the Wii and Nintendo DS demonstrates Nintendo's ability to capture different market segments with innovative offerings. In contrast, platforms like the PSP and PC show lower figures, suggesting a more limited market or one with different consumption patterns. Overall, the visualization allows us to identify how each console impacted the market and how each company's strategies influenced the distribution of global sales.

```python
clean_data[clean_data['platform'].isin(top10_platform)].groupby(['year_of_release', 'platform'])['total_sales'].sum().unstack(fill_value=0)
```
<p align="center">
  <img src="https://github.com/Cristian-Tello/VideoGames_Analysis/blob/main/Dataframe%20total%20sales%20by%20year%20on%20each%20platform.png" alt="Sample Image">
</p> 

# Determinate data to take desicions on model 2017

The data should be taken from the most recent and representative period, that is, the years 2006 to 2016

Technical Justification:
* This range includes the most current platforms (PS3, PS4, X360, Wii, etc.), whose trends are relevant for projecting market behavior in 2017.
* Years prior to 2006 reflect generations of now-obsolete consoles (PS2, GBA, original DS), so their dynamics do not provide useful information for predicting future sales.
* The 2006–2016 period captures both the rise and decline of various platforms, allowing the model to learn patterns of growth and technological replacement.

Conclusion: Use the data from 2006 to 2016 to train your sales or release prediction model for 2017, ensuring that the variables reflect the most recent market conditions and the evolution of modern consoles.

<p align="center">
  <img src="https://github.com/Cristian-Tello/VideoGames_Analysis/blob/main/Platform%20Sales%202006-2016.png" alt="Sample Image">
</p> 
 
* Xbox 360 (952.99), PlayStation 3 (931.33) and Wii (891.18) : These three consoles dominate the market, reflecting the intense competition of the 2006–2016 generation.

* Platforms with Growth: PlayStation 4 (314.14): Although with lower cumulative sales than its predecessors, it shows an upward trend due to being more recent.

* Nintendo 3DS (257.81): Good performance in the handheld segment, with sustained growth.

* Xbox One (159.32): Expanding, although still far from the historical leaders.

* Platforms in Decline or with Less Impact : PS2 (265.80) and PSP (238.63): Consoles that were very successful but are now declining.

* Wii U (82.19) and PS Vita (53.81): Low performance, with difficulties in consolidating their position.

* GameCube, Original Xbox, Dreamcast: Marginal sales, currently irrelevant.

* Potentially Profitable Platforms
PS4 and Xbox One: Modern consoles with room to grow.

* 3DS and DS: Handheld segment with good acceptance.

* PC (163.42): Although smaller in volume, it maintains stability and relevance due to its open ecosystem.

Conclusion:
The market shows a clear generational replacement cycle: older consoles are losing relevance while newer ones (PS4, XOne, 3DS) concentrate the growth potential. For a predictive model towards 2017, it is advisable to focus on these emerging platforms and on the stability of the PC as a complementary market.

<p align="center">
  <img src="https://github.com/Cristian-Tello/VideoGames_Analysis/blob/main/Critic%20reviews.png" alt="Sample Image">
</p> 

* Critic Reviews: A stronger positive correlation exists. Games with higher professional ratings tend to sell more, although with some variation. This suggests that expert opinion significantly influences purchasing decisions.

* User Reviews: The correlation with sales is much weaker. While some titles with good user scores achieve high sales, a consistent pattern is not generally observed.

* Conclusion: Professional reviews have a greater impact on the commercial performance of PS4 games, while user reviews reflect individual perceptions more than a direct impact on sales.

<p align="center">
  <img src="https://github.com/Cristian-Tello/VideoGames_Analysis/blob/main/Sales%20by%20Genre.png" alt="Sample Image">
</p> 

conclusion: The Action, Sports, and Shooter genres account for the majority of sales and are the most profitable, while genres such as Strategy, Puzzle, and Adventure show limited reach. This suggests that, for a predictive model or market strategy, it is advisable to prioritize leading genres while still considering that smaller genres can be valuable in specific niches.

<p align="center">
  <img src="https://github.com/Cristian-Tello/VideoGames_Analysis/blob/main/platform%20region.png" alt="Sample Image">
</p>

* Market Share Variations by Region
1. North America: Xbox 360 leads, followed by PS2, Wii, and PS3. This reflects Microsoft's strong market penetration.

2. Europe: PS2 and PS3 dominate, with Xbox 360 and Wii in secondary positions. Sony maintains a historical advantage in the region.

3. Japan: Nintendo DS leads, followed by PS2 and PS3. Nintendo has a stronger cultural presence and local preference.

 Conclusion: Each market has a different leader. Microsoft dominates in North America, Sony in Europe, and Nintendo in Japan, highlighting cultural and strategic differences within the industry.


 * Impact by Region
1. North America (NA): This region boasts the highest sales across nearly all ratings.
- Games rated E (Everyone) and RP (Rating Pending) stand out, reflecting a broad, family-oriented market.
- There is also a strong presence of M (Mature) titles, demonstrating that the adult audience is a significant segment.

2. Europe (EU): This region maintains a similar pattern to North America, although with lower figures.
- E and M games account for the majority of sales, indicating a balance between family and adult titles.

3. Japan (JP): Sales are lower compared to NA and EU.
- A preference for E and T (Teen) games is observed, suggesting a market more geared towards young and family audiences.
- M titles have lower penetration than in the West.

<p align="center">
  <img src="https://github.com/Cristian-Tello/VideoGames_Analysis/blob/main/ESRB.png" alt="Sample Image">
</p>

* Conclusion
- ESRB ratings do influence regional sales:
- E and T are the most universal, with strong global acceptance.
- The M genre carries significant weight in the West, especially in North America.
- Japan shows less interest in games for adults, prioritizing family or youth-oriented experiences.

```python
# Hypothesis Testing

# H0 = The average user ratings for the Xbox One and PC platforms are the same
# H1 = The average user ratings for the Xbox One and PC platforms are NOT the same.

xbox_one_scores = clean_data[clean_data['platform'] == 'XOne']['user_score'].dropna()
pc_scores = clean_data[clean_data['platform'] == 'PC']['user_score'].dropna()


# Significance level
alpha = 0.05

# T test value
results = stats.ttest_ind(xbox_one_scores, pc_scores)
print('P Value:', results.pvalue)

if (results.pvalue < alpha):
    print('We reject the null hypothesis')
else:
    print('We accept the null hypothesis')
```
```python
Results:
P Value: 0.0005833414469972193
We reject the null hypothesis
```
In the hypothesis test, the result indicates that the p-value was less than the significance level (α = 0.05).
conclusion: The null hypothesis (H0) is rejected, meaning there is statistically significant evidence to suggest that average user ratings on Xbox One and PC are different.
In other words, the data suggests that users rate games differently on each platform, and this difference cannot be attributed to chance.

```python
# Hypothesis Testing

# H0 = The average user ratings for the Action and Sports genres are different
# H1 = The average user ratings for the Action and Sports genres are not different.

action_genres = clean_data[clean_data['genre'] == 'Action']['user_score'].dropna()
sports_genres= clean_data[clean_data['genre'] == 'Sports']['user_score'].dropna()


# Significance level
alpha = 0.05

# T test value
results = stats.ttest_ind(action_genres, sports_genres)
print('P Value:', results.pvalue)

if (results.pvalue < alpha):
    print('We reject the null hypothesis')
else:
```
```python
Results:
P Value: 1.1356758476860633e-08
We reject the null hypothesis
```
* conclusion of the hypothesis test results: 

The p-value obtained was much lower than the significance level (α = 0.05), therefore the null hypothesis is rejected. This means that there is statistically significant evidence to support the claim that the average ratings for the Action and Sports genres are different.

In other words, users rate action games differently from sports games, and this difference cannot be attributed to chance.

## General Conclusions:

1.The analysis, set in a simulated December 2016 scenario to project sales for 2017, provides practical value by demonstrating how to work with real data and extract insights applicable to any period.

2. The industry showed sustained growth since the 1980s, reaching its peak between 2007 and 2009, followed by a decline attributed to strategic changes and the transition to digital distribution.

3. The PlayStation 2 established itself as the best-selling console, while the Xbox 360 and PS3 reflected the intense competition of their generation. Nintendo, with the Wii and DS, captured distinct segments with innovative offerings.

4. To build a predictive model for 2017, the 2006–2016 period is the most representative, as it includes both the rise and fall of modern platforms, allowing for the identification of technological replacement patterns.

5. The PS4, Xbox One, and 3DS consoles, along with the stability of the PC market, represent the potential for future growth, while platforms like the PS2, PSP, and Wii U are showing decline.

6. In terms of genres, Action, Sports, and Shooter games account for the majority of sales and are the most profitable, while genres like Strategy, Puzzle, and Adventure have less reach, although they are useful in specific niches.

  For a predictive model toward 2017, it is advisable to focus on emerging platforms (PS4, Xbox One, 3DS, PC) and the most profitable genres, ensuring that the variables reflect the most recent conditions and the evolution of the sector.
