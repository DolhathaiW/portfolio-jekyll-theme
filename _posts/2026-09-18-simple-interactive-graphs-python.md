---
layout: post
title: "Simple and Interactive Graphs in Python"
---

# Required coding activity: Simple and interactive graphs in Python
---
## Overview

This activity is designed to build your familiarity and comfort coding in Python while also helping you review key topics from each module. As you progress through the activity, questions will get increasingly more complex. It is important that you adopt a programmer's mindset when completing this activity. Remember to run your code from each cell before submitting your activity, as doing so will give you a chance to fix any errors before submitting.

### Learning outcome addressed¶
- Create graphs in Python.


```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns
```

    /home/82c898b8-7f1b-4f80-9b23-238272e9d69c/.local/lib/python3.11/site-packages/pandas/core/computation/expressions.py:22: UserWarning: Pandas requires version '2.10.2' or newer of 'numexpr' (version '2.8.4' currently installed).
      from pandas.core.computation.check import NUMEXPR_INSTALLED
    /home/82c898b8-7f1b-4f80-9b23-238272e9d69c/.local/lib/python3.11/site-packages/pandas/core/arrays/masked.py:56: UserWarning: Pandas requires version '1.4.2' or newer of 'bottleneck' (version '1.3.5' currently installed).
      from pandas.core import (


### Setup
Run the code below to create a dataframe **df** containing employee information, such as Education, EducationField, Department, Age, etc. The column **Attrition** shows if an employees has left the company or not.

Take a moment to analyse the dataframe and become familiar with the different attributes.


```python
filename = "WA_Fn-UseC_-HR-Employee-Attrition.csv"
df = pd.read_csv(filename) 
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Attrition</th>
      <th>BusinessTravel</th>
      <th>DailyRate</th>
      <th>Department</th>
      <th>DistanceFromHome</th>
      <th>Education</th>
      <th>EducationField</th>
      <th>EmployeeCount</th>
      <th>EmployeeNumber</th>
      <th>...</th>
      <th>RelationshipSatisfaction</th>
      <th>StandardHours</th>
      <th>StockOptionLevel</th>
      <th>TotalWorkingYears</th>
      <th>TrainingTimesLastYear</th>
      <th>WorkLifeBalance</th>
      <th>YearsAtCompany</th>
      <th>YearsInCurrentRole</th>
      <th>YearsSinceLastPromotion</th>
      <th>YearsWithCurrManager</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>41</td>
      <td>Yes</td>
      <td>Travel_Rarely</td>
      <td>1102</td>
      <td>Sales</td>
      <td>1</td>
      <td>2</td>
      <td>Life Sciences</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td>1</td>
      <td>80</td>
      <td>0</td>
      <td>8</td>
      <td>0</td>
      <td>1</td>
      <td>6</td>
      <td>4</td>
      <td>0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>49</td>
      <td>No</td>
      <td>Travel_Frequently</td>
      <td>279</td>
      <td>Research &amp; Development</td>
      <td>8</td>
      <td>1</td>
      <td>Life Sciences</td>
      <td>1</td>
      <td>2</td>
      <td>...</td>
      <td>4</td>
      <td>80</td>
      <td>1</td>
      <td>10</td>
      <td>3</td>
      <td>3</td>
      <td>10</td>
      <td>7</td>
      <td>1</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>37</td>
      <td>Yes</td>
      <td>Travel_Rarely</td>
      <td>1373</td>
      <td>Research &amp; Development</td>
      <td>2</td>
      <td>2</td>
      <td>Other</td>
      <td>1</td>
      <td>4</td>
      <td>...</td>
      <td>2</td>
      <td>80</td>
      <td>0</td>
      <td>7</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>33</td>
      <td>No</td>
      <td>Travel_Frequently</td>
      <td>1392</td>
      <td>Research &amp; Development</td>
      <td>3</td>
      <td>4</td>
      <td>Life Sciences</td>
      <td>1</td>
      <td>5</td>
      <td>...</td>
      <td>3</td>
      <td>80</td>
      <td>0</td>
      <td>8</td>
      <td>3</td>
      <td>3</td>
      <td>8</td>
      <td>7</td>
      <td>3</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>27</td>
      <td>No</td>
      <td>Travel_Rarely</td>
      <td>591</td>
      <td>Research &amp; Development</td>
      <td>2</td>
      <td>1</td>
      <td>Medical</td>
      <td>1</td>
      <td>7</td>
      <td>...</td>
      <td>4</td>
      <td>80</td>
      <td>1</td>
      <td>6</td>
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 35 columns</p>
</div>




```python
# Do you have any missing values:
df.info()
```

    <class 'pandas.DataFrame'>
    RangeIndex: 1470 entries, 0 to 1469
    Data columns (total 35 columns):
     #   Column                    Non-Null Count  Dtype
    ---  ------                    --------------  -----
     0   Age                       1470 non-null   int64
     1   Attrition                 1470 non-null   str  
     2   BusinessTravel            1470 non-null   str  
     3   DailyRate                 1470 non-null   int64
     4   Department                1470 non-null   str  
     5   DistanceFromHome          1470 non-null   int64
     6   Education                 1470 non-null   int64
     7   EducationField            1470 non-null   str  
     8   EmployeeCount             1470 non-null   int64
     9   EmployeeNumber            1470 non-null   int64
     10  EnvironmentSatisfaction   1470 non-null   int64
     11  Gender                    1470 non-null   str  
     12  HourlyRate                1470 non-null   int64
     13  JobInvolvement            1470 non-null   int64
     14  JobLevel                  1470 non-null   int64
     15  JobRole                   1470 non-null   str  
     16  JobSatisfaction           1470 non-null   int64
     17  MaritalStatus             1470 non-null   str  
     18  MonthlyIncome             1470 non-null   int64
     19  MonthlyRate               1470 non-null   int64
     20  NumCompaniesWorked        1470 non-null   int64
     21  Over18                    1470 non-null   str  
     22  OverTime                  1470 non-null   str  
     23  PercentSalaryHike         1470 non-null   int64
     24  PerformanceRating         1470 non-null   int64
     25  RelationshipSatisfaction  1470 non-null   int64
     26  StandardHours             1470 non-null   int64
     27  StockOptionLevel          1470 non-null   int64
     28  TotalWorkingYears         1470 non-null   int64
     29  TrainingTimesLastYear     1470 non-null   int64
     30  WorkLifeBalance           1470 non-null   int64
     31  YearsAtCompany            1470 non-null   int64
     32  YearsInCurrentRole        1470 non-null   int64
     33  YearsSinceLastPromotion   1470 non-null   int64
     34  YearsWithCurrManager      1470 non-null   int64
    dtypes: int64(26), str(9)
    memory usage: 402.1 KB



```python
# What are some of statistical values for the numerical attributes?
df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>DailyRate</th>
      <th>DistanceFromHome</th>
      <th>Education</th>
      <th>EmployeeCount</th>
      <th>EmployeeNumber</th>
      <th>EnvironmentSatisfaction</th>
      <th>HourlyRate</th>
      <th>JobInvolvement</th>
      <th>JobLevel</th>
      <th>...</th>
      <th>RelationshipSatisfaction</th>
      <th>StandardHours</th>
      <th>StockOptionLevel</th>
      <th>TotalWorkingYears</th>
      <th>TrainingTimesLastYear</th>
      <th>WorkLifeBalance</th>
      <th>YearsAtCompany</th>
      <th>YearsInCurrentRole</th>
      <th>YearsSinceLastPromotion</th>
      <th>YearsWithCurrManager</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1470.000000</td>
      <td>1470.000000</td>
      <td>1470.000000</td>
      <td>1470.000000</td>
      <td>1470.0</td>
      <td>1470.000000</td>
      <td>1470.000000</td>
      <td>1470.000000</td>
      <td>1470.000000</td>
      <td>1470.000000</td>
      <td>...</td>
      <td>1470.000000</td>
      <td>1470.0</td>
      <td>1470.000000</td>
      <td>1470.000000</td>
      <td>1470.000000</td>
      <td>1470.000000</td>
      <td>1470.000000</td>
      <td>1470.000000</td>
      <td>1470.000000</td>
      <td>1470.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>36.923810</td>
      <td>802.485714</td>
      <td>9.192517</td>
      <td>2.912925</td>
      <td>1.0</td>
      <td>1024.865306</td>
      <td>2.721769</td>
      <td>65.891156</td>
      <td>2.729932</td>
      <td>2.063946</td>
      <td>...</td>
      <td>2.712245</td>
      <td>80.0</td>
      <td>0.793878</td>
      <td>11.279592</td>
      <td>2.799320</td>
      <td>2.761224</td>
      <td>7.008163</td>
      <td>4.229252</td>
      <td>2.187755</td>
      <td>4.123129</td>
    </tr>
    <tr>
      <th>std</th>
      <td>9.135373</td>
      <td>403.509100</td>
      <td>8.106864</td>
      <td>1.024165</td>
      <td>0.0</td>
      <td>602.024335</td>
      <td>1.093082</td>
      <td>20.329428</td>
      <td>0.711561</td>
      <td>1.106940</td>
      <td>...</td>
      <td>1.081209</td>
      <td>0.0</td>
      <td>0.852077</td>
      <td>7.780782</td>
      <td>1.289271</td>
      <td>0.706476</td>
      <td>6.126525</td>
      <td>3.623137</td>
      <td>3.222430</td>
      <td>3.568136</td>
    </tr>
    <tr>
      <th>min</th>
      <td>18.000000</td>
      <td>102.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>30.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>...</td>
      <td>1.000000</td>
      <td>80.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>30.000000</td>
      <td>465.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>1.0</td>
      <td>491.250000</td>
      <td>2.000000</td>
      <td>48.000000</td>
      <td>2.000000</td>
      <td>1.000000</td>
      <td>...</td>
      <td>2.000000</td>
      <td>80.0</td>
      <td>0.000000</td>
      <td>6.000000</td>
      <td>2.000000</td>
      <td>2.000000</td>
      <td>3.000000</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>2.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>36.000000</td>
      <td>802.000000</td>
      <td>7.000000</td>
      <td>3.000000</td>
      <td>1.0</td>
      <td>1020.500000</td>
      <td>3.000000</td>
      <td>66.000000</td>
      <td>3.000000</td>
      <td>2.000000</td>
      <td>...</td>
      <td>3.000000</td>
      <td>80.0</td>
      <td>1.000000</td>
      <td>10.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>5.000000</td>
      <td>3.000000</td>
      <td>1.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>43.000000</td>
      <td>1157.000000</td>
      <td>14.000000</td>
      <td>4.000000</td>
      <td>1.0</td>
      <td>1555.750000</td>
      <td>4.000000</td>
      <td>83.750000</td>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>...</td>
      <td>4.000000</td>
      <td>80.0</td>
      <td>1.000000</td>
      <td>15.000000</td>
      <td>3.000000</td>
      <td>3.000000</td>
      <td>9.000000</td>
      <td>7.000000</td>
      <td>3.000000</td>
      <td>7.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>60.000000</td>
      <td>1499.000000</td>
      <td>29.000000</td>
      <td>5.000000</td>
      <td>1.0</td>
      <td>2068.000000</td>
      <td>4.000000</td>
      <td>100.000000</td>
      <td>4.000000</td>
      <td>5.000000</td>
      <td>...</td>
      <td>4.000000</td>
      <td>80.0</td>
      <td>3.000000</td>
      <td>40.000000</td>
      <td>6.000000</td>
      <td>4.000000</td>
      <td>40.000000</td>
      <td>18.000000</td>
      <td>15.000000</td>
      <td>17.000000</td>
    </tr>
  </tbody>
</table>
<p>8 rows × 26 columns</p>
</div>



### Question 1
*3 points*

Perform the following tasks:
- Complete the code below to generate a histogram for the categorical variable Gender.
- Then, answer the following questions in the **Conclusions** cell below.
    - What conclusions can you draw from the histogram?
    - What other categorial variables can you find in the dataframe.
    - What conclusions can you draw after examining the histograms for them?

* Note: you may want to add additional cells to create other histograms.

df['Gender'].value_counts().plot(kind='bar')

<img src="{{ '/assets/Required_activityand%20interactive%20graphs%20in%20Python-2_7_1.png' | relative_url }}

**Conclusions:**

- There are more male employees than female employees

**Conclusions:**

- There are more male employees than female employees

### Question 2
*3 points*

Perform the following tasks:

- Complete the code below to closely examine the attribute **TotalWorkingYears**. Create a histogram showing TotalWorkingYears to see the work experience from all employees.
- Use 10 bins to group the TotalWorkingYears attribute.
- Label the x axis as 'Total Working Years'.
- Label the y axis as 'Counts'.
- Set the title of the histogram as 'Total Working Years'.
- What conclusions can you draw from the histogram? Answer this question in the **Conclusions** cell below.


```python
plt.figure(figsize=(20,5))
plt.hist(df.TotalWorkingYears, bins=10)
plt.xlabel('Total Working Years')
plt.ylabel('Counts')
plt.title('Total Working Years')
plt.show()

```


    
![png](Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_files/Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_10_0.png)
    


**Conclusions:**

- Most employees have been working between 5 to 15 year
- The distribution is right‑skewed, which means fewer employees are in late-career stage

### Question 3
*3 points*

Perform the following tasks:

- Create a dataframe called df from the "data/BCS.csv" file you have been provided. 
- Examine the first rows of the dataframe (df.head()).
- Examine the dataframe data types and how many null values you have in the data set.
- Examine statistical information about the numeric fields.


```python

filename = "BCS.csv"
df = pd.read_csv(filename) 
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Low</th>
      <th>Open</th>
      <th>Volume</th>
      <th>High</th>
      <th>Close</th>
      <th>Adjusted Close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>09-09-1986</td>
      <td>5.040323</td>
      <td>0.000000</td>
      <td>198685</td>
      <td>5.081468</td>
      <td>5.040323</td>
      <td>1.336653</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-09-1986</td>
      <td>5.060895</td>
      <td>5.060895</td>
      <td>3646</td>
      <td>5.102041</td>
      <td>5.102041</td>
      <td>1.353021</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11-09-1986</td>
      <td>5.009463</td>
      <td>5.081468</td>
      <td>159191</td>
      <td>5.081468</td>
      <td>5.009463</td>
      <td>1.328470</td>
    </tr>
    <tr>
      <th>3</th>
      <td>12-09-1986</td>
      <td>4.855168</td>
      <td>4.896313</td>
      <td>12760</td>
      <td>4.896313</td>
      <td>4.896313</td>
      <td>1.298463</td>
    </tr>
    <tr>
      <th>4</th>
      <td>15-09-1986</td>
      <td>4.937459</td>
      <td>4.937459</td>
      <td>31595</td>
      <td>5.009463</td>
      <td>4.937459</td>
      <td>1.309375</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Examine the dataframe data types and how many null values you have in the data set
df.info()
```

    <class 'pandas.DataFrame'>
    RangeIndex: 9106 entries, 0 to 9105
    Data columns (total 7 columns):
     #   Column          Non-Null Count  Dtype  
    ---  ------          --------------  -----  
     0   Date            9106 non-null   str    
     1   Low             9106 non-null   float64
     2   Open            9106 non-null   float64
     3   Volume          9106 non-null   int64  
     4   High            9106 non-null   float64
     5   Close           9106 non-null   float64
     6   Adjusted Close  9106 non-null   float64
    dtypes: float64(5), int64(1), str(1)
    memory usage: 498.1 KB



```python
# Examine statistical information about the numeric fields
df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Low</th>
      <th>Open</th>
      <th>Volume</th>
      <th>High</th>
      <th>Close</th>
      <th>Adjusted Close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>9106.000000</td>
      <td>9106.000000</td>
      <td>9.106000e+03</td>
      <td>9106.000000</td>
      <td>9106.000000</td>
      <td>9106.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>16.762104</td>
      <td>16.915667</td>
      <td>1.724751e+06</td>
      <td>17.079075</td>
      <td>16.932407</td>
      <td>10.174890</td>
    </tr>
    <tr>
      <th>std</th>
      <td>11.702680</td>
      <td>11.800611</td>
      <td>3.591035e+06</td>
      <td>11.903733</td>
      <td>11.812918</td>
      <td>7.315679</td>
    </tr>
    <tr>
      <th>min</th>
      <td>2.534562</td>
      <td>0.000000</td>
      <td>0.000000e+00</td>
      <td>2.967742</td>
      <td>2.829493</td>
      <td>1.156614</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>7.574885</td>
      <td>7.632488</td>
      <td>1.866200e+04</td>
      <td>7.720000</td>
      <td>7.650000</td>
      <td>4.098477</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>12.299539</td>
      <td>12.465438</td>
      <td>2.127685e+05</td>
      <td>12.723503</td>
      <td>12.479262</td>
      <td>9.431916</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>23.997696</td>
      <td>24.298100</td>
      <td>2.634175e+06</td>
      <td>24.654379</td>
      <td>24.413163</td>
      <td>13.257134</td>
    </tr>
    <tr>
      <th>max</th>
      <td>57.188938</td>
      <td>57.741936</td>
      <td>1.496358e+08</td>
      <td>57.769585</td>
      <td>57.566818</td>
      <td>35.969128</td>
    </tr>
  </tbody>
</table>
</div>



### Question 4
*3 points*

Perform the following tasks:

- Complete the code below to display a line plot with the attribute **High**.
- Label the title of the graph as 'Barclays PLC'.
- Label the y axis as 'Barclays Price'.


```python
plt.plot(df['High'])
plt.title('Barclays PLC')
plt.ylabel('Barclays Price')

```




    Text(0, 0.5, 'Barclays Price')




    
![png](Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_files/Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_17_1.png)
    


### Question 5
*3 points*

Perform the following tasks:

- Develop a function called 'get_price' that takes in the NYSE stock symbol (e.g. 'BCS') and ouputs the 'High' and 'Low' share prices.
- Then, pass the 'BCS' symbol to the function and assign the returned 'High' and 'Low' values to the variables high and low.


```python
def get_price(symbol):
  file = symbol+".csv"
  df = pd.read_csv(file) 
  high = df['High']
  low = df['Low']
  return high, low

high, low = get_price('BCS')

```

### Question 6
*3 points*

Perform the following tasks:

- Complete the code below. Using plt subplots so that you can set the figure size, plot the price highs against the price lows. Plot the lows in red.
- Set the figure size to 10 by 10 inches.
- Label your axes and provide a title. You can label the x axis 'Daily', as these are daily prices.


```python
fig,ax = plt.subplots()
high, low =  get_price('BCS')
ax.plot(high)
ax.plot(low,'r')
ax.set_title('BCS Prices Highs and Lows')
ax.set_xlabel('Daily')
ax.set_ylabel('Price')
fig.set_size_inches(10,10)
```


    
![png](Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_files/Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_21_0.png)
    


### Question 7
*3 points*

Perform the following tasks:

- Complete the code below to produce vertical sub plots of the high and low prices using the code below.
- Set the figure size to 10 by 10.


```python
fig, axs = plt.subplots(1, 2, figsize=(10, 10), sharey=False)
plt.subplot(2, 1, 1)
plt.plot(high)
plt.subplot(2, 1, 2)
plt.plot(low,'r')
plt.show()
```

    /tmp/ipykernel_1122/1967846582.py:2: MatplotlibDeprecationWarning: Auto-removal of overlapping axes is deprecated since 3.6 and will be removed two minor releases later; explicitly call ax.remove() as needed.
      plt.subplot(2, 1, 1)



    
![png](Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_files/Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_23_1.png)
    


### Question 8
*3 points*

Perform the following tasks:

- Next, useuse the Seaborn library to do an EDA on the data/autos.csv.
- Use the following code to retrieve the 'tips' data set and examine the various relationships. 
- Create a dataframe called 'auto' abd examine the head of the dataframe.
- Examine the dataframe data types and how many null values you have in the data set.
- Examine statistical information about the numeric fields.


```python
auto= pd.read_csv("autos.csv")
auto.head() 
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>symboling</th>
      <th>make</th>
      <th>fuel_type</th>
      <th>aspiration</th>
      <th>num_of_doors</th>
      <th>body_style</th>
      <th>drive_wheels</th>
      <th>engine_location</th>
      <th>wheel_base</th>
      <th>length</th>
      <th>...</th>
      <th>engine_size</th>
      <th>fuel_system</th>
      <th>bore</th>
      <th>stroke</th>
      <th>compression_ratio</th>
      <th>horsepower</th>
      <th>peak_rpm</th>
      <th>city_mpg</th>
      <th>highway_mpg</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3</td>
      <td>alfa-romero</td>
      <td>gas</td>
      <td>std</td>
      <td>2</td>
      <td>convertible</td>
      <td>rwd</td>
      <td>front</td>
      <td>88.6</td>
      <td>168.8</td>
      <td>...</td>
      <td>130</td>
      <td>mpfi</td>
      <td>3.47</td>
      <td>2.68</td>
      <td>9</td>
      <td>111</td>
      <td>5000</td>
      <td>21</td>
      <td>27</td>
      <td>13495</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>alfa-romero</td>
      <td>gas</td>
      <td>std</td>
      <td>2</td>
      <td>convertible</td>
      <td>rwd</td>
      <td>front</td>
      <td>88.6</td>
      <td>168.8</td>
      <td>...</td>
      <td>130</td>
      <td>mpfi</td>
      <td>3.47</td>
      <td>2.68</td>
      <td>9</td>
      <td>111</td>
      <td>5000</td>
      <td>21</td>
      <td>27</td>
      <td>16500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>alfa-romero</td>
      <td>gas</td>
      <td>std</td>
      <td>2</td>
      <td>hatchback</td>
      <td>rwd</td>
      <td>front</td>
      <td>94.5</td>
      <td>171.2</td>
      <td>...</td>
      <td>152</td>
      <td>mpfi</td>
      <td>2.68</td>
      <td>3.47</td>
      <td>9</td>
      <td>154</td>
      <td>5000</td>
      <td>19</td>
      <td>26</td>
      <td>16500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>audi</td>
      <td>gas</td>
      <td>std</td>
      <td>4</td>
      <td>sedan</td>
      <td>fwd</td>
      <td>front</td>
      <td>99.8</td>
      <td>176.6</td>
      <td>...</td>
      <td>109</td>
      <td>mpfi</td>
      <td>3.19</td>
      <td>3.40</td>
      <td>10</td>
      <td>102</td>
      <td>5500</td>
      <td>24</td>
      <td>30</td>
      <td>13950</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>audi</td>
      <td>gas</td>
      <td>std</td>
      <td>4</td>
      <td>sedan</td>
      <td>4wd</td>
      <td>front</td>
      <td>99.4</td>
      <td>176.6</td>
      <td>...</td>
      <td>136</td>
      <td>mpfi</td>
      <td>3.19</td>
      <td>3.40</td>
      <td>8</td>
      <td>115</td>
      <td>5500</td>
      <td>18</td>
      <td>22</td>
      <td>17450</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 25 columns</p>
</div>




```python
# Examine the dataframe data types and how many null values you have in the dataset
auto.info()

```

    <class 'pandas.DataFrame'>
    RangeIndex: 193 entries, 0 to 192
    Data columns (total 25 columns):
     #   Column             Non-Null Count  Dtype  
    ---  ------             --------------  -----  
     0   symboling          193 non-null    int64  
     1   make               193 non-null    str    
     2   fuel_type          193 non-null    str    
     3   aspiration         193 non-null    str    
     4   num_of_doors       193 non-null    int64  
     5   body_style         193 non-null    str    
     6   drive_wheels       193 non-null    str    
     7   engine_location    193 non-null    str    
     8   wheel_base         193 non-null    float64
     9   length             193 non-null    float64
     10  width              193 non-null    float64
     11  height             193 non-null    float64
     12  curb_weight        193 non-null    int64  
     13  engine_type        193 non-null    str    
     14  num_of_cylinders   193 non-null    int64  
     15  engine_size        193 non-null    int64  
     16  fuel_system        193 non-null    str    
     17  bore               193 non-null    float64
     18  stroke             193 non-null    float64
     19  compression_ratio  193 non-null    int64  
     20  horsepower         193 non-null    int64  
     21  peak_rpm           193 non-null    int64  
     22  city_mpg           193 non-null    int64  
     23  highway_mpg        193 non-null    int64  
     24  price              193 non-null    int64  
    dtypes: float64(6), int64(11), str(8)
    memory usage: 37.8 KB



```python
# Examine statistical information about the numeric fields
auto.describe()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>symboling</th>
      <th>num_of_doors</th>
      <th>wheel_base</th>
      <th>length</th>
      <th>width</th>
      <th>height</th>
      <th>curb_weight</th>
      <th>num_of_cylinders</th>
      <th>engine_size</th>
      <th>bore</th>
      <th>stroke</th>
      <th>compression_ratio</th>
      <th>horsepower</th>
      <th>peak_rpm</th>
      <th>city_mpg</th>
      <th>highway_mpg</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
      <td>193.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.797927</td>
      <td>3.160622</td>
      <td>98.923834</td>
      <td>174.326425</td>
      <td>65.893782</td>
      <td>53.869948</td>
      <td>2561.507772</td>
      <td>4.419689</td>
      <td>128.124352</td>
      <td>3.330622</td>
      <td>3.248860</td>
      <td>9.860104</td>
      <td>103.481865</td>
      <td>5099.740933</td>
      <td>25.326425</td>
      <td>30.787565</td>
      <td>13285.025907</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.235582</td>
      <td>0.989583</td>
      <td>6.152409</td>
      <td>12.478593</td>
      <td>2.137795</td>
      <td>2.394770</td>
      <td>526.700026</td>
      <td>1.023182</td>
      <td>41.590452</td>
      <td>0.272385</td>
      <td>0.315421</td>
      <td>4.002098</td>
      <td>37.960107</td>
      <td>468.694369</td>
      <td>6.387828</td>
      <td>6.816910</td>
      <td>8089.082886</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-2.000000</td>
      <td>2.000000</td>
      <td>86.600000</td>
      <td>141.100000</td>
      <td>60.300000</td>
      <td>47.800000</td>
      <td>1488.000000</td>
      <td>3.000000</td>
      <td>61.000000</td>
      <td>2.540000</td>
      <td>2.070000</td>
      <td>7.000000</td>
      <td>48.000000</td>
      <td>4150.000000</td>
      <td>13.000000</td>
      <td>16.000000</td>
      <td>5118.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>94.500000</td>
      <td>166.300000</td>
      <td>64.100000</td>
      <td>52.000000</td>
      <td>2145.000000</td>
      <td>4.000000</td>
      <td>98.000000</td>
      <td>3.150000</td>
      <td>3.110000</td>
      <td>8.000000</td>
      <td>70.000000</td>
      <td>4800.000000</td>
      <td>19.000000</td>
      <td>25.000000</td>
      <td>7738.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.000000</td>
      <td>4.000000</td>
      <td>97.000000</td>
      <td>173.200000</td>
      <td>65.400000</td>
      <td>54.100000</td>
      <td>2414.000000</td>
      <td>4.000000</td>
      <td>120.000000</td>
      <td>3.310000</td>
      <td>3.290000</td>
      <td>9.000000</td>
      <td>95.000000</td>
      <td>5100.000000</td>
      <td>25.000000</td>
      <td>30.000000</td>
      <td>10245.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2.000000</td>
      <td>4.000000</td>
      <td>102.400000</td>
      <td>184.600000</td>
      <td>66.900000</td>
      <td>55.700000</td>
      <td>2952.000000</td>
      <td>4.000000</td>
      <td>146.000000</td>
      <td>3.590000</td>
      <td>3.410000</td>
      <td>9.000000</td>
      <td>116.000000</td>
      <td>5500.000000</td>
      <td>30.000000</td>
      <td>34.000000</td>
      <td>16515.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>3.000000</td>
      <td>4.000000</td>
      <td>120.900000</td>
      <td>208.100000</td>
      <td>72.000000</td>
      <td>59.800000</td>
      <td>4066.000000</td>
      <td>12.000000</td>
      <td>326.000000</td>
      <td>3.940000</td>
      <td>4.170000</td>
      <td>23.000000</td>
      <td>262.000000</td>
      <td>6600.000000</td>
      <td>49.000000</td>
      <td>54.000000</td>
      <td>45400.000000</td>
    </tr>
  </tbody>
</table>
</div>



### Question 9
*3 points*

Perform the following tasks:

- Complete the code below to use Seaborn to create a relplot of the following: x="engine_size", y="price" and hue="make".
- What can you conclude about the relationship between the engine size and the price of the car? Looking at the colour-coded data points by 'make', what can you conclude about any trend regarding price, engine size and make? Answer these questions in the **Conclusions** cell below.


```python

    sns.relplot(
    data=auto,
    x="engine_size",
    y="price",
    hue="make"
)

```

    /home/82c898b8-7f1b-4f80-9b23-238272e9d69c/.local/lib/python3.11/site-packages/seaborn/axisgrid.py:123: UserWarning: The figure layout has changed to tight
      self._figure.tight_layout(*args, **kwargs)





    <seaborn.axisgrid.FacetGrid at 0x7af55853a090>




    
![png](Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_files/Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_29_2.png)
    


**Conclusions:**

- There is a positive correlation between engine size and price, as the engine size increases,price also increases.
- Some manufacturers/makes cluster in the lower engine size & lower price region including Volkswagen, Toyota or Subaru

### Question 10
*3 points*

Perform the following tasks:

- Box and whisker plots are often useful for exploring the statistics of the data in a visual format. Use a Seaborn catplot with kind = "box" of the engine size against body style. The plot shows the engine size as a function of the body style. It also shows the median value as the black line in the center of the box and the top and bottom edges of the box as the second and third quartiles of the range of engine size.
- Use the code below to plot the boxes.
- What can you conclude from the the plot in terms of engine size and body style? Answer this question in the **Conclusions** cell below.


```python
sns.catplot(data=auto, x="body_style", y="engine_size", kind="box")
```

    /home/82c898b8-7f1b-4f80-9b23-238272e9d69c/.local/lib/python3.11/site-packages/seaborn/axisgrid.py:123: UserWarning: The figure layout has changed to tight
      self._figure.tight_layout(*args, **kwargs)





    <seaborn.axisgrid.FacetGrid at 0x7af4ffb94250>




    
![png](Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_files/Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_32_2.png)
    


**Conclusions:**
- Engine sizes varies, but hardtop has larger engine than others and hatchback tends to have smaller engine
- Convertible has a wider spread, indicates more variation in engine size
- Some body styles such as sedan or hardtop have extreme engine sizes (outliers)


### Question 11
*3 points*

Perform the following tasks:

- You can look at the relationship between the features in the data set by using a pairplot. You can also gain categorical information by setting the hue parameter to a category, such as body style, from the data set.
- To reduce the size of the plot and to eliminate irrelavant and categorical types from the features, you can drop many of the columns. Use the code to drop some columns. Assign the results to a new dataframe called 'auto2', and then pass auto2 into the pairplot. You are doing it this way as you do not want to permanently change the auto dataframe.
<code>
auto2 = auto.drop(['symboling', 'make', 
                'fuel_type', 'aspiration','engine_location', 'engine_type', 
                'num_of_cylinders', 'fuel_system','bore', 'stroke','compression_ratio', 'num_of_doors','drive_wheels', 'length','width', 'curb_weight', 'peak_rpm','city_mpg', 'height'], axis=1)
sns.pairplot(auto2, hue="body_style") 
</code>
- What conclusions can you draw from the pairplot about the relationship between the features? Answer this question in the **Conclusions** cell below.


```python

auto2 = auto.drop([
    'symboling', 'make', 'fuel_type', 'aspiration', 'engine_location',
    'engine_type', 'num_of_cylinders', 'fuel_system', 'bore', 'stroke',
    'compression_ratio', 'num_of_doors', 'drive_wheels', 'length', 'width',
    'curb_weight', 'peak_rpm', 'city_mpg', 'height'], axis=1)

sns.pairplot(auto2, hue="body_style")

```

    /home/82c898b8-7f1b-4f80-9b23-238272e9d69c/.local/lib/python3.11/site-packages/seaborn/axisgrid.py:123: UserWarning: The figure layout has changed to tight
      self._figure.tight_layout(*args, **kwargs)





    <seaborn.axisgrid.PairGrid at 0x7af4fc0f3a90>




    
![png](Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_files/Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_35_2.png)
    


**Conclusions:**

- Positive relationship between engine_size, hourse power and price
- Highway MPG is negatively correlated with engine size and horsepower, means the Bigger engines or the Higher horsepower, the lower fuel efficiency


### Question 12
*3 points*

Perform the following tasks:

- Use Seaborn to look at the relationship between engine size and price, with data points colour-coded (hue) firstly by body style and secondly by drive wheels. You will need to create two sub scatter plots to do this using the the original auto dataframe. 
- Set the figure size to 15 by 4 and plot horizontally.
- What can you conclude from the above subplots about the relationship between the price and the engine size for both body style and drive wheel type? Do these two subplots confirm your previous conclusions? Answer these questions in the **Conclusions** cell below.


```python
fig, axs = plt.subplots(1, 2, figsize=(15, 4))

sns.scatterplot(data=auto, x="engine_size", y="price", hue="body_style", ax=axs[0])
sns.scatterplot(data=auto, x="engine_size", y="price", hue="drive_wheels", ax=axs[1]);


```


    
![png](Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_files/Required_activity-Simple%20and%20interactive%20graphs%20in%20Python-2_38_0.png)
    


**Conclusions:**

- Engine size increases, price increases
- Hatchback tends to have smaller engine size and lower price
- FWD tends to have smaller engine size and lower price


```python

```
