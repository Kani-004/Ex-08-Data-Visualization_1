# Ex-08-Data-Visualization-

## AIM
To Perform Data Visualization on a complex dataset and save the data to a file. 

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature generation and selection techniques to all the features of the data set
### STEP 4
Apply data visualization techniques to identify the patterns of the data.


# CODE

~~~

#loading the dataset
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df
#removing unnecessary data variables
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

df.isnull().sum()
#detecting and removing outliers in current numeric data
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
#data visualization
#line plots
import seaborn as sns
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()
#bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()
#Histogram
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
#count plot
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
#Barplot 
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
#KDE plot
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
#violin plot
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
#point plot
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
#Pie Chart
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()
#HeatMap
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

~~~

# OUPUT

# Initial Dataset:

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/048e901b-bd53-43a1-928e-bff236d6f43c)

# Cleaned Dataset:

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/ca02ce9f-2141-4617-a4bd-b7ad8f184291)

# Removing Outliers:

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/85108869-a2e9-44ac-9c6f-6d55d73b27d7)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/98e30b96-3215-4a26-88fc-ed928171d285)

# Line PLot:

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/cacb2ca5-52fe-4c16-be9c-1aa4aceb078e)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/d959409f-fa3e-4199-9c7e-ecff3d4c3ad0)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/cdb4a28c-2c69-4819-9533-19cd4d92bc5b)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/02c86fbe-2517-4a43-965e-f6b9161303f8)

# Bar Plots:

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/c03abf2b-f092-43b4-99e6-a195ed3e40eb)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/bf3ffc13-cc4b-4aff-be8a-7a401bd06c59)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/8c998f34-1ae3-496a-83ab-6f08e954aa05)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/b2c093be-ee88-4582-b338-251d7c43a0bf)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/63f42801-c5ab-4065-9ed7-10c5b909f008)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/a484f827-75bd-4890-ac93-165eaef759d8)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/2c3101c4-46b9-4ca3-8cca-79a4a6e4580e)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/12fcbf6f-80f7-4bfc-88d4-405be70ab247)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/c8262a57-82e5-4952-a16e-2a1e69e88eff)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/9ce09bd4-22c1-4e7a-ae59-e53d70958806)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/541f7dda-d77e-4698-93b8-5341624eff66)

# Histograms:

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/daae180a-3d61-4009-8f9d-b5dbfb3c00dc)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/fe691200-5e6d-4f3c-9a07-b30834ed12a1)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/6caee2c9-7b8d-4023-9da9-63f7634a2cf4)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/68cdc5c9-bce6-46cf-800a-22bdb85c8e14)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/2a92c660-f7f1-4cf0-a988-15b686e2bd51)

# Count plots:

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/f3555fad-e1a1-4b5d-b4de-754cd8d26647)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/500efa53-3c77-466b-b0f9-4d2f1ba951dd)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/815f49ee-c63d-4e74-9762-ef1c890ebb58)

# Bar Charts:

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/6c229943-c240-41a2-a64e-b4307f631efd)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/6c5cd12c-5544-4913-9e34-3d43ed5414af)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/d3ea2fc6-bbfc-4d61-8c81-a483ccf12946)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/8edba820-aa4b-43d1-a777-416351b72b24)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/374ddfe0-8cde-4aca-b120-5bd6d06f5b95)

# KDE Plots:

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/e47be171-b7cf-4d6a-9a2d-b4503ea6f719)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/e37f167b-eaa9-460a-9711-afc694add426)

# Violin Plot:

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/211d6bd4-2f6b-4ab5-87a3-6dc30a4bd1eb)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/5fd777fa-9e5b-4f28-afbb-bfd1129a9e24)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/381f732b-f193-4982-91b9-cf397ec24973)

# Point Plots:

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/78883ad5-0432-421a-a329-81d1d6da130f)

# Pie Charts:

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/724fa688-76e4-4d78-ae85-2238fe1cb70a)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/cf87b8a9-17a4-4866-b331-2c8b90b5216a)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/8db8c480-b806-44b3-802c-68caffa7c624)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/a088225d-e37f-425b-be4f-e87562215514)

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/8029302c-3391-41af-910f-98aa123cf431)

# HeatMap:

![image](https://github.com/Kani-004/Ex-08-Data-Visualization_1/assets/129577149/9c34fda5-0e0c-4146-816a-e40d38b41723)

~~~
# Result:

Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file.

~~~




