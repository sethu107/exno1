# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
from google.colab import drive
drive.mount('/content/drive')

ls drive/MyDrive/'Colab Notebooks'/DATA/

# **DATA CLEANING**
import pandas as pd
import numpy as np

df=pd.read_csv('drive/MyDrive/Data Science/Data_set.csv')

df_null=df.isnull()
print(df_null)

![image](https://github.com/user-attachments/assets/95e316a6-74e3-418b-8000-92551c30e9e2)

df_sum=df.isnull().sum()
print(df_sum)

![image](https://github.com/user-attachments/assets/1bd96c0f-651e-41e6-96de-6a97d002bce9)

df_drop=df.isnull().dropna()
print(df_drop)

![image](https://github.com/user-attachments/assets/54a2b2f3-4995-4897-a96f-e0417d23d056)

df_null_0=df.fillna(0)
print(df_null_0)

![image](https://github.com/user-attachments/assets/cf25b6c8-f5bf-452d-bfda-9230e5538710)

df_null_ffill=df.ffill()
print(df_null_ffill)

![image](https://github.com/user-attachments/assets/6bb2f1ae-4bd9-468c-8126-7fa30cb7146a)

df_bfill=df.bfill()
print(df_bfill)

![image](https://github.com/user-attachments/assets/ef069b05-ed4a-4194-93a8-f09e962643d4)

df_mean1=df['num_episodes'].fillna(df['num_episodes'].mean())
print(df_mean1)

![image](https://github.com/user-attachments/assets/7e8cac54-abd7-4622-ad2f-618b2894e209)

df_mean2=df['rating'].fillna(df['rating'].mean())
print(df_mean2)

![image](https://github.com/user-attachments/assets/4ae535b7-5243-450a-a7a9-3679aa88933d)

df_mean3=df['current_overall_rank'].fillna(df['current_overall_rank'].mean())
print(df_mean3)

![image](https://github.com/user-attachments/assets/d4edc900-9c5f-4977-b8e0-6edecb5a0f3b)

df_mean4=df['lifetime_popularity_rank'].fillna(df['lifetime_popularity_rank'].mean())
print(df_mean4)

![image](https://github.com/user-attachments/assets/6252d34d-19bb-4ed8-8a2f-ff4a72ebb7c4)

df_mean5=df['watchers'].fillna(df['watchers'].mean())
print(df_mean5)

![image](https://github.com/user-attachments/assets/3274e50c-a7d0-4413-be9c-46feeee56f30)

df_dropna=df.dropna()
print(df_dropna)

![image](https://github.com/user-attachments/assets/0eb2fb50-f09a-4d56-91ab-1602e3c3e593)

# **Outlier Detection and Removal - IQR**


import seaborn as sns

age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
print(af)

![image](https://github.com/user-attachments/assets/58e8c210-aa73-4619-bc87-7f8b3a2d4573)

sns.boxplot(af)

![image](https://github.com/user-attachments/assets/8d330702-2d88-4769-a494-04439aea014c)

sns.scatterplot(af)

![image](https://github.com/user-attachments/assets/24b2c6a8-3247-4908-954c-5cd9c0ad0b3d)

q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)

iqr=q3-q1
print(iqr)

Q1=np.percentile(af,25)
Q2=np.percentile(af,50)
Q3=np.percentile(af,75)

IQR=Q3-Q1

lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR

outliers = [x for x in age if x < lower_bound or x > upper_bound]

print('Q1:',Q1)
print('Q3:',Q3)
print('IQR:',IQR)
print('Lower bound:',lower_bound)
print('Upper bound:',upper_bound)
print('Outliers:',outliers)

![image](https://github.com/user-attachments/assets/aaaddf43-55ef-402c-8c97-8d9c813062de)

af=af[((af>=lower_bound)&(af<=upper_bound))]
print(af)

![image](https://github.com/user-attachments/assets/ba3e4c10-d327-4ba3-8adf-d4627844c91f)

af.dropna()

![image](https://github.com/user-attachments/assets/beac3af5-b7ef-4c3c-aed0-d28a4733d154)

sns.boxplot(af)

![image](https://github.com/user-attachments/assets/5d8b6f96-84b4-42db-aaa3-9a4389801374)

sns.scatterplot(af)

![image](https://github.com/user-attachments/assets/b5e89b08-50e3-489b-b0b1-58d4b2ce25ff)

# **Z Score**

from scipy import stats

data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93]
df=pd.DataFrame(data)

sns.boxplot(df)

![image](https://github.com/user-attachments/assets/674c8fdc-a443-41ac-b33e-f3f9faed6b5b)

mean=np.mean(data)
print(mean)
50.724137931034484

std=np.std(data)
print(std)
25.59889080534025

z=np.abs(stats.zscore(df))
print(z)

![image](https://github.com/user-attachments/assets/20f0d255-f5f5-4d01-8156-7e7cb9c3e0d4)

threshold=3
outliers = df[abs(df) > 3]
print("Outliers:")
print(outliers)

![image](https://github.com/user-attachments/assets/a43290be-1191-433d-be5a-25177cffc05e)

df_cleaned = df[(z <= threshold)]
print(df_cleaned)

![image](https://github.com/user-attachments/assets/518250d2-adfc-469a-976d-c7c32ee650e5)

sns.boxplot(df_cleaned)

![image](https://github.com/user-attachments/assets/000fb4db-9817-4342-a973-c3516e8fa090)

sns.scatterplot(df_cleaned)

![image](https://github.com/user-attachments/assets/bd413e69-7ef0-4b3e-b5c3-6efe1da033f9)

# Result
          The Data cleaning process is completed successfuly
