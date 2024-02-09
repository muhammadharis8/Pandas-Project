# Pandas-Project
In this project , there’s a data set consisting of multiple columns like age, amount , gender etc. It is basically having data of online purchasing platform and I performed Data Analysis using the library “Pandas” of Python and first I imported that data set of multiple rows and columns then performed data cleaning and manipulation .Improved customer experience by identifying potential customers across different states, gender and age groups.
Improved sales by identifying best selling products in different states and products being purchased by the people of different sectors which can help in maintaining inventory and hence meet the demands.
This all analysis tells me that most of the females did online shopping and they work in IT sector , Aviation and Health care sector they spent most of their amount in buying food online and clothing and they were mostly belongs to marastha, Haryana and multiple states of India 

# IMPORTING ALL LIBRARIES THAT ARE GOING TO BE USED IN THIS PROJECT.
!pip install numpy
import numpy as np
!pip install pandas
import pandas as pd
!pip install matplotlib
import matplotlib.pyplot as plt
%matplotlib inline
!pip install seaborn
import seaborn as sms

#Importing CSV
df = pd.read_csv("Diwali Sales Data.csv", encoding='unicode_escape')
df

df.info()
#DROPPIG NULL COLUMNS AND COLUMNS WHICH AREN"T GONNA BE USED
df.drop(["Status",'unnamed1'], axis=1, inplace = True)
#Plot for gedners
ax = sms.countplot(x = "Gender",data = df)
for bars in ax.containers:
    ax.bar_label(bars)
# plot for groupby gender and age group
ax = sms.countplot(data = df , x= "Age Group", hue = "Gender")
for bars in ax.containers:
    ax.bar_label(bars)
# plot for groupy State and orders
sales_state = df.groupby(["State"] , as_index = False)["Orders"].sum().sort_values(by="Orders",ascending = False).head(10)
sms.set(rc ={"figure.figsize":(15,8)})
sms.barplot(x= "State", y= "Orders",data = sales_state)
# plot for groupy State and amount
sales_state = df.groupby(["State"] , as_index = False)["Amount"].sum().sort_values(by="Amount",ascending = False).head(10)
sms.set(rc ={"figure.figsize":(15,8)})
sms.barplot(x= "State", y= "Amount",data = sales_state)

# plot for groupby Martial status and gender
x1 = sms.countplot(x = "Marital_Status",data = df,hue = "Gender")
sms.set(rc ={"figure.figsize":(7,5)})
for bars in ax1.containers:
    ax1.bar_label(bars)
# plotting occupation of people buying things online
ax1 = sms.countplot(x = "Occupation",data = df)
sms.set(rc ={"figure.figsize":(20,5)})
for bars in ax1.containers:
    ax1.bar_label(bars)
  # Now groupby Occupation and amount 
sales_state = df.groupby(["Occupation"] , as_index = False)["Amount"].sum().sort_values(by="Amount",ascending = False).head(10)
sms.set(rc ={"figure.figsize":(20,5)})
sms.barplot(x= "Occupation", y= "Amount",data = sales_state)

# now proudct category is analyzed
sales_state = df.groupby(["Product_Category"] , as_index = False)["Amount"].sum().sort_values(by="Amount",ascending = False).head(10)
sms.set(rc ={"figure.figsize":(20,5)})
sms.barplot(x= "Product_Category", y= "Amount",data = sales_state)

# In last we gonna find the most selling products
sales_state = df.groupby(["Product_ID"] , as_index = False)["Orders"].sum().sort_values(by="Orders",ascending = False).head(10)
sms.set(rc ={"figure.figsize":(15,8)})
sms.barplot(x= "Product_ID", y= "Orders",data = sales_state)
