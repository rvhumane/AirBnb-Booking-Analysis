# AirBnb-Booking-Analysis

Project Name - AirBnb Booking Analysis
Project Type - EDA/Regression/Classification/Unsupervised
Contribution - Individual
Name - Ravi Humane
Project Summary -
Write the summary here within 500-600 words.

GitHub Link -
https://github.com/rvhumane/AirBnb-Booking-Analysis/edit/main/README.md

Problem Statement
Write Problem Statement Here.

Define Your Business Objective?
Answer Here.

General Guidelines : -
Well-structured, formatted, and commented code is required.

Exception Handling, Production Grade Code & Deployment Ready Code will be a plus. Those students will be awarded some additional credits.

The additional credits will have advantages over other students during Star Student selection.

    [ Note: - Deployment Ready Code is defined as, the whole .ipynb notebook should be executable in one go
              without a single error logged. ]
Each and every logic should have proper comments.

You may add as many number of charts you want. Make Sure for each and every chart the following format should be answered.

# Chart visualization code
Why did you pick the specific chart?
What is/are the insight(s) found from the chart?
Will the gained insights help creating a positive business impact? Are there any insights that lead to negative growth? Justify with specific reason.
You have to create at least 20 logical & meaningful charts having important insights.
[ Hints : - Do the Vizualization in a structured way while following "UBM" Rule.

U - Univariate Analysis,

B - Bivariate Analysis (Numerical - Categorical, Numerical - Numerical, Categorical - Categorical)

M - Multivariate Analysis ]

Let's Begin !
1. Know Your Data
Import Libraries
[ ]
# Import Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
Dataset Loading
[ ]
# Load Dataset

[ ]
from google.colab import drive
drive.mount('/content/drive')
Mounted at /content/drive
[ ]
path='/content/Airbnb NYC 2019.csv'
airbnb_df = pd.read_csv(path)
Dataset First View
[ ]
# Dataset First Look
airbnb_df.head()

Dataset Rows & Columns count
[ ]
# Dataset Rows & Columns count
airbnb_df.shape
(48895, 16)
Dataset Information
[ ]
# Dataset Info
airbnb_df.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 48895 entries, 0 to 48894
Data columns (total 16 columns):
 #   Column                          Non-Null Count  Dtype  
---  ------                          --------------  -----  
 0   id                              48895 non-null  int64  
 1   name                            48879 non-null  object 
 2   host_id                         48895 non-null  int64  
 3   host_name                       48874 non-null  object 
 4   neighbourhood_group             48895 non-null  object 
 5   neighbourhood                   48895 non-null  object 
 6   latitude                        48895 non-null  float64
 7   longitude                       48895 non-null  float64
 8   room_type                       48895 non-null  object 
 9   price                           48895 non-null  int64  
 10  minimum_nights                  48895 non-null  int64  
 11  number_of_reviews               48895 non-null  int64  
 12  last_review                     38843 non-null  object 
 13  reviews_per_month               38843 non-null  float64
 14  calculated_host_listings_count  48895 non-null  int64  
 15  availability_365                48895 non-null  int64  
dtypes: float64(3), int64(7), object(6)
memory usage: 6.0+ MB
Duplicate Values
[ ]
airbnb_data = airbnb_df.copy()
[ ]
# Dataset Duplicate Value Count
dupl_dt= airbnb_data.groupby(airbnb_data.columns.tolist()).size().reset_index().rename(columns={0:'count'})
print(dupl_dt)
             id                                              name    host_id  \
0          2539                Clean & quiet apt home by the park       2787   
1          2595                             Skylit Midtown Castle       2845   
2          3831                   Cozy Entire Floor of Brownstone       4869   
3          5022  Entire Apt: Spacious Studio/Loft by central park       7192   
4          5099         Large Cozy 1 BR Apartment In Midtown East       7322   
...         ...                                               ...        ...   
38816  36425863        Lovely Privet Bedroom with Privet Restroom   83554966   
38817  36427429                          No.2 with queen size bed  257683179   
38818  36438336                                   Seas The Moment  211644523   
38819  36442252                     1B-1B apartment near by Metro  273841667   
38820  36455809           Cozy Private Room in Bushwick, Brooklyn   74162901   

         host_name neighbourhood_group    neighbourhood  latitude  longitude  \
0             John            Brooklyn       Kensington  40.64749  -73.97237   
1         Jennifer           Manhattan          Midtown  40.75362  -73.98377   
2      LisaRoxanne            Brooklyn     Clinton Hill  40.68514  -73.95976   
3            Laura           Manhattan      East Harlem  40.79851  -73.94399   
4            Chris           Manhattan      Murray Hill  40.74767  -73.97500   
...            ...                 ...              ...       ...        ...   
38816        Rusaa           Manhattan  Upper East Side  40.78099  -73.95366   
38817         H Ai              Queens         Flushing  40.75104  -73.81459   
38818          Ben       Staten Island      Great Kills  40.54179  -74.14275   
38819       Blaine               Bronx       Mott Haven  40.80787  -73.92400   
38820    Christine            Brooklyn         Bushwick  40.69805  -73.92801   

             room_type  price  minimum_nights  number_of_reviews last_review  \
0         Private room    149               1                  9  2018-10-19   
1      Entire home/apt    225               1                 45  2019-05-21   
2      Entire home/apt     89               1                270  2019-07-05   
3      Entire home/apt     80              10                  9  2018-11-19   
4      Entire home/apt    200               3                 74  2019-06-22   
...                ...    ...             ...                ...         ...   
38816     Private room    129               1                  1  2019-07-07   
38817     Private room     45               1                  1  2019-07-07   
38818     Private room    235               1                  1  2019-07-07   
38819  Entire home/apt    100               1                  2  2019-07-07   
38820     Private room     30               1                  1  2019-07-08   

       reviews_per_month  calculated_host_listings_count  availability_365  \
0                   0.21                               6               365   
1                   0.38                               2               355   
2                   4.64                               1               194   
3                   0.10                               1                 0   
4                   0.59                               1               129   
...                  ...                             ...               ...   
38816               1.00                               1               147   
38817               1.00                               6               339   
38818               1.00                               1                87   
38819               2.00                               1                40   
38820               1.00                               1                 1   

       count  
0          1  
1          1  
2          1  
3          1  
4          1  
...      ...  
38816      1  
38817      1  
38818      1  
38819      1  
38820      1  

[38821 rows x 17 columns]
Missing Values/Null Values
[ ]
# Missing Values/Null Values Count
airbnb_data.isnull().values.sum()
20141
[ ]
 #total null per column
total_values = airbnb_data.isnull().sum().sort_values(ascending = False)  

print(total_values)
last_review                       10052
reviews_per_month                 10052
host_name                            21
name                                 16
id                                    0
host_id                               0
neighbourhood_group                   0
neighbourhood                         0
latitude                              0
longitude                             0
room_type                             0
price                                 0
minimum_nights                        0
number_of_reviews                     0
calculated_host_listings_count        0
availability_365                      0
dtype: int64
