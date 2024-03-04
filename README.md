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
```
name: sanjeevi.j
reg no: 212222110040
```
# data cleaning
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
data = pd.read_csv("/content/SAMPLEIDS.csv")
data.head()
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/167e21a6-b41e-4d8f-94c1-17f0b3c18bbb)
```
data = pd.get_dummies(data)
data.isnull().sum()
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/2af926e6-0803-4ad1-81fa-d2b13c08805f)
```
columns_with_null = data.columns[data.isnull().any()]
import seaborn as sns
plt.figure(figsize=(10,10))
sns.barplot(columns_with_null)
plt.title("NULL VALUES")
plt.show()
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/30770250-d3b6-4002-b2e5-a967739fdd4c)
```
for column in columns_with_null:
    median = data[column].median()  
    data[column].fillna(median, inplace=True)
data.isnull().sum().sum()
```
#IQR
```
import pandas as pd
import seaborn as sns
ir = pd.read_csv("/content/iris (1).csv")
ir.head()
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/24a30842-fc6f-4152-a1f9-39634f82f649)
```
ir.describe()
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/5b3762ea-fdf4-41bc-9951-ab865879de16)
```
sns.boxplot(x='sepal_width',data=ir)
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/b84c9840-ac43-476d-982a-72d610ea4080)
```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
3.3
```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/6fbca869-432e-4713-a848-41577d82c9be)
```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/13104544-9ad2-44ef-951a-3c6383cf8163)
```
sns.boxplot(x='sepal_width',data=delid)
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/64759be7-a1a6-4798-aa4d-2340091bc11f)

#Z SCORE
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/bb22b907-a354-4eb2-8d5d-4ffa388b2fc9)
```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/0ac433c6-7baf-4d3c-a391-1d5a45765541)
```
low = q1 - 1.5*iqr
low
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/1c9de67c-8389-4740-932b-80b2a7ac72a6)
```
high = q3 + 1.5*iqr
high
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/bc39d9b0-cc11-4684-85a2-e813951cad5b)
```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/88e8b6c9-7ff4-40b9-8361-605eee9133c6)
```
z = np.abs(stats.zscore(df['height']))
z
```
![image](https://github.com/jsanjeevi05/exno1/assets/121484976/a8c40477-30c1-4935-8ae5-b1ceddf1bdb9)
```

# Result
Thus the outliers are detected and removed in the given file and the final data set is saved into the file.     
