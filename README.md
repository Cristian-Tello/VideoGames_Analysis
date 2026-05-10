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
