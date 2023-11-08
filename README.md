# Ex-08-Data-Visualization-
# AIM
To Perform Data Visualization on a complex dataset and save the data to a file.

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
## STEP 1
Read the given Data

## STEP 2
Clean the Data Set using Data Cleaning Process

## STEP 3
Apply Feature generation and selection techniques to all the features of the data set

## STEP 4
Apply data visualization techniques to identify the patterns of the data.

# CODE
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from google.colab import files
uploaded = files.upload()
df=pd.read_csv("SuperStore.csv",encoding='unicode_escape')
df
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/cb63cc08-d743-49b5-8a9d-7d2aef29c3f4)
```
df.isnull().sum()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/938ca4e8-085e-49cd-b253-88172cbf6eb2)
```
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/76da2735-cbfc-4a16-b29a-26baccc71079)
```
#detecting and removing outliers in current numeric data
plt.figure(figsize=(8,8))
plt.title("Data with outliers")
df.boxplot()
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/6e59aa0c-8168-4c7a-8440-6fc689a5de35)
```
plt.figure(figsize=(8,8))
cols = ['Sales','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/2f804b65-750f-4831-a982-d77909aa9122)

## Which Segment has Highest sales?
```
sns.lineplot(x="Segment",y="Sales",data=df,marker='o')
plt.title("Segment vs Sales")
plt.xticks(rotation = 90)
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/7296d066-9f25-4402-babd-54f21154b08b)
```
sns.barplot(x="Segment",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/15f815ec-4ed2-4cff-9897-81f1a18f1ccb)

## Which City has Highest profit?
```
df.shape
df1 = df[(df.Profit >= 60)]
df1.shape
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/59259f09-d1b1-4a87-bc16-fc9d795bebc7)
```
plt.figure(figsize=(30,8))
states=df1.loc[:,["City","Profit"]]
states=states.groupby(by=["City"]).sum().sort_values(by="Profit")
sns.barplot(x=states.index,y="Profit",data=states)
plt.xticks(rotation = 90)
plt.xlabel=("City")
plt.ylabel=("Profit")
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/828646be-91c9-4b2d-9165-4dce050eec06)

## Which ship mode is profitable?
```
sns.barplot(x="Ship Mode",y="Profit",data=df)
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/c854a787-497d-4990-8fab-cd07477fd4f2)
```
sns.lineplot(x="Ship Mode",y="Profit",data=df)
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/03a74d14-a8bf-4b11-ae33-fab1d37eab72)
```
sns.violinplot(x="Profit",y="Ship Mode",data=df)
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/246ab893-0cb2-4812-ad88-c3b0f53230dc)
```
sns.pointplot(x=df["Profit"],y=df["Ship Mode"])
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/da852893-005d-4d75-bdc9-e0d9930fc14c)

## Sales of the product based on region.
```
states=df.loc[:,["Region","Sales"]]
states=states.groupby(by=["Region"]).sum().sort_values(by="Sales")
sns.barplot(x=states.index,y="Sales",data=states)
plt.xticks(rotation = 90)
plt.xlabel=("Region")
plt.ylabel=("Sales")
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/2f938c72-6c62-4ebb-b48f-8a13e98b4b26)
```
df.groupby(['Region']).sum().plot(kind='pie', y='Sales',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/d658e734-3c70-407f-99b0-cb4c839d9e2f)

## Find the relation between sales and profit.
```
df["Sales"].corr(df["Profit"])
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/d6f69581-6599-4c40-9808-0ae9a479a68f)
```
df_corr = df.copy()
df_corr = df_corr[["Sales","Profit"]]
df_corr.corr()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/6475fe1a-11c9-467b-8690-b44ac2a2bdd2)
```
sns.pairplot(df_corr, kind="scatter")
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/8cbb8a41-4c06-4b30-a04f-cbf5d5782f0d)

## Heatmap
```
df4=df.copy()

#encoding
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])

#scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])

#Heatmap
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()

```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/7f466cdd-ed61-4128-a055-e507bd091839)

## Find the relation between sales and profit based on the following category.

### Segment
```
grouped_data = df.groupby('Segment')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('Segment')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/0d3ca8f0-d19c-42a4-aee5-f575c693ca5e)

### City
```
grouped_data = df.groupby('City')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('City')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/659a0f6a-d2a1-4118-a153-911e2b487864)

### States
```
grouped_data = df.groupby('State')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('State')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/3c279dc9-a711-4350-990a-20dce59bed19)

### Segment and Ship Mode
```
grouped_data = df.groupby(['Segment', 'Ship Mode'])[['Sales', 'Profit']].mean()
pivot_data = grouped_data.reset_index().pivot(index='Segment', columns='Ship Mode', values=['Sales', 'Profit'])
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
pivot_data.plot(kind='bar', ax=ax)
ax.set_xlabel('Segment')
ax.set_ylabel('Value')
plt.legend(title='Ship Mode')
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/7af54628-1f0a-4b45-89f4-488b24527adf)

### Segment, Ship mode and Region
```
grouped_data = df.groupby(['Segment', 'Ship Mode','Region'])[['Sales', 'Profit']].mean()
pivot_data = grouped_data.reset_index().pivot(index=['Segment', 'Ship Mode'], columns='Region', values=['Sales', 'Profit'])
sns.set_style("whitegrid")
sns.set_palette("Set1")
pivot_data.plot(kind='bar', stacked=True, figsize=(10, 5))
plt.xlabel('Segment-Ship Mode')
plt.ylabel('Value')
plt.legend(title='Region')
plt.show()
```
![image](https://github.com/Vaish-1011/ODD2023-Datascience-Ex-08/assets/135130074/9e25a0fb-5432-4734-8e71-2aae19db3712)


# RESULT:
Thus, Data Visualization is performed on the given dataset and save the data to a file.
