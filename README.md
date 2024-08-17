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
## DATA CLEANING
```
import pandas as pd
df=pd.read_csv("SAMPLEIDS.csv")
df
```
![Screenshot 2024-08-17 111539](https://github.com/user-attachments/assets/5849f02b-0f76-45d3-80be-d7d4303e417d)

```
df.isnull().sum()
```
![Screenshot 2024-08-17 111743](https://github.com/user-attachments/assets/4987dd32-cb71-4a6b-a73d-9895661f56ec)
```
df.isnull().any()
```
![Screenshot 2024-08-17 112047](https://github.com/user-attachments/assets/ebee2711-9efb-4ad8-8d82-c4aadea683f0)
```
df.dropna()
```
![Screenshot 2024-08-17 112214](https://github.com/user-attachments/assets/c18441ba-1153-40c5-a4e1-d54c55e3ff35)

```
df.fillna(0)
```
![Screenshot 2024-08-17 112332](https://github.com/user-attachments/assets/bbebbf35-5376-4830-9d6e-343f1f048b9e)
```
df.fillna(method = 'ffill')
```
![Screenshot 2024-08-17 112445](https://github.com/user-attachments/assets/5b9d83a0-31ec-438e-9807-7c0e22492ed1)
```
df.fillna(method = 'bfill')
```
![Screenshot 2024-08-17 112539](https://github.com/user-attachments/assets/67c9d01e-67ba-4c7e-8a27-dda6d7cbf26c)
```
df_dropped = df.dropna()
df_dropped
```
![Screenshot 2024-08-17 112643](https://github.com/user-attachments/assets/1c8697b3-b151-492f-913e-9a81916da48b)
```
df.fillna({'GENDER':'MALE','NAME':'SRI','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![Screenshot 2024-08-17 112756](https://github.com/user-attachments/assets/2b36195b-9389-4573-a903-fc3f6953b18d)
## IQR(Inter Quartile Range)
```
import pandas as pd
ir=pd.read_csv('iris.csv')
ir
```
![Screenshot 2024-08-17 112848](https://github.com/user-attachments/assets/c90cabc3-b099-4cac-ba2b-51a6bfd79536)
```
ir.describe()
```
![Screenshot 2024-08-17 112950](https://github.com/user-attachments/assets/e39de136-1ede-4187-93ba-61b4d6ac6d8e)
```
sns.boxplot(x='sepal_width',data=ir)
```
![Screenshot 2024-08-17 113041](https://github.com/user-attachments/assets/c9e80cb5-b52e-407c-96ef-9d6d7ad96528)
```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![Screenshot 2024-08-17 113249](https://github.com/user-attachments/assets/ff4e5a48-e164-4072-9c73-cac8503f0809)
```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![Screenshot 2024-08-17 113351](https://github.com/user-attachments/assets/e067bb52-dcd7-4eba-9ed0-db140eeb6ef3)
```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![Screenshot 2024-08-17 113435](https://github.com/user-attachments/assets/0e51f2fe-755e-43d9-8488-81cf1ad6c8e6)
```
sns.boxplot(x='sepal_width',data=delid)
```
![Screenshot 2024-08-17 113532](https://github.com/user-attachments/assets/9d2537a2-f255-497d-be59-0606c013cd9a)
## Z-Score

```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("heights.csv")
dataset
```
![Screenshot 2024-08-17 113623](https://github.com/user-attachments/assets/f47507cc-371b-4bf1-aaf7-f418f903d2f9)
```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```
![Screenshot 2024-08-17 113715](https://github.com/user-attachments/assets/1f01dd47-6d7b-4737-a771-6d1507190340)
```
low = q1 - 1.5*iqr
low
```
![Screenshot 2024-08-17 113846](https://github.com/user-attachments/assets/eb34b093-103f-4f74-831d-9e2e6cf697a8)
```
high = q3 + 1.5*iqr
high
```
![Screenshot 2024-08-17 113937](https://github.com/user-attachments/assets/fb088052-8de6-4699-b657-1bc3fd8b6197)
```

df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![Screenshot 2024-08-17 114048](https://github.com/user-attachments/assets/2a821478-29c4-41b2-8ac1-224481b3cce7)
```
z = np.abs(stats.zscore(df['height']))
z
```
![Screenshot 2024-08-17 114153](https://github.com/user-attachments/assets/5e88aff5-ded3-4cea-80ca-f2e6ea9633ee)
```
df1 = df[z<3]
df1
```
![Screenshot 2024-08-17 114318](https://github.com/user-attachments/assets/7dc4c6d0-9135-42fc-8e76-62d74e729bda)
```

# Result
          Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
