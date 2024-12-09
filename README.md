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


![image](https://github.com/user-attachments/assets/6639e02d-1a26-473a-b6e8-43f80f0ee4c2)

df_sum=df.isnull().sum()
print(df_sum)


![image](https://github.com/user-attachments/assets/339ee462-081c-4ff2-a006-e61d94ea85fe)


df_drop=df.isnull().dropna()
print(df_drop)


![image](https://github.com/user-attachments/assets/8329f151-fd82-47db-bad2-ad29a877c649)


df_null_0=df.fillna(0)
print(df_null_0)


![image](https://github.com/user-attachments/assets/7c001703-1ae9-4c2a-bb01-c3eea8fbc578)


df_null_ffill=df.ffill()
print(df_null_ffill)


![image](https://github.com/user-attachments/assets/aa04f84e-4476-49ef-b9d4-bb916ae6457d)


df_bfill=df.bfill()
print(df_bfill)


![image](https://github.com/user-attachments/assets/63e67880-2994-448a-802b-f8a8893bad85)


df_mean1=df['num_episodes'].fillna(df['num_episodes'].mean())
print(df_mean1)


![image](https://github.com/user-attachments/assets/9222eb0e-41df-464d-95bf-fcfe51a77b5c)


df_mean2=df['rating'].fillna(df['rating'].mean())
print(df_mean2)


![image](https://github.com/user-attachments/assets/2af1cfb9-0f25-4ecd-9dea-d5a104eff884)


df_mean3=df['current_overall_rank'].fillna(df['current_overall_rank'].mean())
print(df_mean3)


![image](https://github.com/user-attachments/assets/5bf37785-69c5-4f65-936c-61a560cda75c)


df_mean4=df['lifetime_popularity_rank'].fillna(df['lifetime_popularity_rank'].mean())
print(df_mean4)


![image](https://github.com/user-attachments/assets/ee246d32-ffa6-4510-9d95-844acc305838)


df_mean5=df['watchers'].fillna(df['watchers'].mean())
print(df_mean5)

![image](https://github.com/user-attachments/assets/b910f32b-7dc9-4d38-82e0-1f3dd8a1667d)

df_dropna=df.dropna()
print(df_dropna)

![image](https://github.com/user-attachments/assets/5869d464-356a-43e2-bb29-57127ae62d01)

# **Outlier Detection and Removal - IQR**

import seaborn as sns
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
print(af)

![image](https://github.com/user-attachments/assets/8c3d49b2-b69e-4cb5-bca0-ca41e7e08195)

sns.boxplot(af)

![image](https://github.com/user-attachments/assets/c9d72145-a3eb-4383-943b-d6396abc0ff0)

sns.scatterplot(af)

![image](https://github.com/user-attachments/assets/4c132361-22a2-4563-a398-e29c5b5980b3)


q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)
iqr=q3-q1
print(iqr)


![image](https://github.com/user-attachments/assets/d4d6477e-2b28-4d37-9059-17bf0ea9e343)

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

![image](https://github.com/user-attachments/assets/46e5c130-5d98-4db0-9efa-c238b4059f02)

af=af[((af>=lower_bound)&(af<=upper_bound))]
print(af)

![image](https://github.com/user-attachments/assets/d5de8edd-adb1-4ed7-97d4-574a0835eeb1)

af.dropna()

![image](https://github.com/user-attachments/assets/8a759f2e-9316-4b49-89af-1e3045af3f01)

sns.boxplot(af)

![image](https://github.com/user-attachments/assets/f5963d3f-68f8-4b05-aaf4-285e649446b0)

sns.scatterplot(af)

![image](https://github.com/user-attachments/assets/795388f5-b9cd-4378-a414-e112e27a8bf9)

# **Z Score**
from scipy import stats
data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93]
df=pd.DataFrame(data)
sns.boxplot(df)


![image](https://github.com/user-attachments/assets/a68735c9-a775-48db-b5d5-4141969d8c88)

mean=np.mean(data)
print(mean)


![image](https://github.com/user-attachments/assets/067a4a1c-620c-42fb-8691-0dbe5d3d8b9a)

std=np.std(data)
print(std)


![image](https://github.com/user-attachments/assets/169a60ef-e078-4c05-8fea-6a74db066ae1)

z=np.abs(stats.zscore(df))
print(z)


![image](https://github.com/user-attachments/assets/8c166683-4727-4303-830e-fa612cf455f2)

threshold=3
outliers = df[abs(df) > 3]
print("Outliers:")
print(outliers)

![image](https://github.com/user-attachments/assets/3ea51a4b-6bdc-47fd-a80c-33a6517005a3)


df_cleaned = df[(z <= threshold)]
print(df_cleaned)

![image](https://github.com/user-attachments/assets/cd47b3fb-1d18-4e05-a542-a4dd3843e185)

sns.boxplot(df_cleaned)

![image](https://github.com/user-attachments/assets/549a6177-8b7e-4f6f-9c13-750ae6f62b41)

sns.scatterplot(df_cleaned)

![image](https://github.com/user-attachments/assets/d1f86de0-ad92-4412-ac9b-4b95e0100eba)

# Result
          <<include your Result here>>
