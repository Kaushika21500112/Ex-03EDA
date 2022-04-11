# Ex-03EDA

## AIM
To perform EDA on the given data set. 

# Explanation
The primary aim with exploratory analysis is to examine the data for distribution, outliers and 
anomalies to direct specific testing of your hypothesis.
 

# ALGORITHM
### STEP 1
Import the required packages(pandas,numpy,seaborn).

### STEP 2
Read and Load the Dataset.

### STEP 3
Remove the null values from the data and remove the outliers.

### STEP 4
Remove the non numerical data columns using drop() method.

### STEP 5:
returns object containing counts of unique values using (value_counts()).

### STEP 6:
Plot the counts in the form of Histogram or Bar Graph.

### STEP 7:
find the pairwise correlation of all columns in the dataframe(.corr()).

### STEP 8:
Save the final data set into the file.

# CODE
```
'''
Program 
Developed by:Kaushika.A
Register no:212221230048
'''
import pandas as pd
import numpy as np
import seaborn as sns
df=pd.read_csv("titanic_dataset.csv")
df

#removing data containing too many null values
df.isnull().sum()
df.drop('Cabin',axis=1,inplace=True)

#analysing dataframe contents
df.info()
df.isnull().sum()

#cleaning data
df['Age']=df['Age'].fillna(df['Age'].median())
df['Embarked']=df['Embarked'].fillna(df['Embarked'].mode()[0])
df.isnull().sum()

#data is cleaned, checking for outliers
df.boxplot()
#removing outliers
cols = ['Age', 'Fare','SibSp','Parch','Fare']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
df
df.boxplot()

#maximum outliers removed
# performing data analysis
#statistical analysis for single data group
df['Survived'].value_counts()
df['Pclass'].value_counts()
df['SibSp'].value_counts()
df['Embarked'].value_counts()
df['Sex'].value_counts()

#statistical analysis for two data groups
pd.crosstab(df["Pclass"],df["Survived"])
pd.crosstab(df["Sex"],df["Survived"])
pd.crosstab(df["Embarked"],df["Survived"])
pd.crosstab(df["SibSp"],df["Survived"])

#graphical analysis of categorical data--univariate
sns.countplot(x="Survived",data=df)
sns.countplot(x="Pclass",data=df)
sns.countplot(x="SibSp",data=df)
sns.countplot(x="Embarked",data=df)
sns.countplot(x="Sex",data=df)

#graphical analysis of non-categorical data or data with multiple categories--univariate
sns.displot(df["Fare"])
sns.displot(df["Age"])

#graphical analysis of categorical data--bivariate
sns.countplot(x="Sex",hue="Survived",data=df)
sns.countplot(x='Pclass',hue='Survived',data=df)
sns.countplot(x='Embarked',hue='Survived',data=df)

#graphical analysis of non-categorical data or data with multiple categories--bivariate
sns.displot(df[df["Survived"]==0]["Age"])
sns.displot(df[df["Survived"]==1]["Age"])

#Graphical representation of data--multivariate 
df.drop('Parch',axis=1,inplace=True)
sns.heatmap(df.corr(),annot=True)

#analysing pairwise correlation of columns in dataset
df.corr()
```

# OUPUT
## Original Data
![](o1.png)
## Data after removing values with multiple null entries
![](o2.png)
![](o3.png)
![](o4.png)
## Data Cleaning Process
![](o5.png)
## Removing Outliers Process
![](o6.png)
![](o7.png)
![](o8.png)

## performing data analysis
## statistical analysis for single data group
![](o9.png)
![](o10.png)
![](o11.png)
![](o12.png)
![](o13.png)

## statistical analysis for two data groups
![](o14.png)
![](o15.png)
![](o16.png)
![](o17.png)

## graphical analysis of categorical data--univariate
![](o18.png)
![](o19.png)
![](o20.png)
![](o21.png)
![](o22.png)

## graphical analysis of non-categorical data or data with multiple categories--univariate
![](o23.png)
![](o24.png)

## graphical analysis of categorical data--bivariate
![](o25.png)
![](o26.png)
![](o27.png)

## graphical analysis of non-categorical data or data with multiple categories--bivariate
![](o28.png)
![](o29.png)

## graphical representation of data--multivariate 
![](o31.png)

## pairwise correlation of columns in dataset
![](o30.png)

# RESULT
The data has been cleaned, outlier has been removed and the EDA on the given data has been performed.