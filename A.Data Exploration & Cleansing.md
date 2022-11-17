# 🛒 Case Study - E-commerce Company
# A. Data Exploration and Cleansing

<p align="right"> Using Microsoft Python - Google Colab vs Power BI </p>

#

## 🔤 IMPORT LIBRARY AND DATASET ##

<details><summary> Click to expand :arrow_down: </summary>
  
```python

import pandas as pd 
import numpy as np 
import matplotlib as plt
import seaborn as sns
from matplotlib import dates
import datetime
print('Completed import lib')
```

```python
from google.colab import drive
drive.mount('/content/drive')
```


```python

#Upload dataset
customers = pd.read_csv('/content/drive/MyDrive/Final/De 1/dataset/customers_dataset.csv')
order_items = pd.read_csv('/content/drive/MyDrive/Final/De 1/dataset/order_items_dataset.csv')
order_payments = pd.read_csv('/content/drive/MyDrive/Final/De 1/dataset/order_payments_dataset.csv')
order_reviews = pd.read_csv('/content/drive/MyDrive/Final/De 1/dataset/order_reviews_dataset.csv')
orders = pd.read_csv('/content/drive/MyDrive/Final/De 1/dataset/orders_dataset.csv')
product_name_translation = pd.read_csv('/content/drive/MyDrive/Final/De 1/dataset/product_category_name_translation.csv')
products = pd.read_csv('/content/drive/MyDrive/Final/De 1/dataset/products_dataset.csv')

```
  
</details>

## 🔎 EXPLORE DATA

**1.Info** 

<details><summary> Click to expand code </summary>
  
- head:
```python
df.head()
```
![image](https://user-images.githubusercontent.com/101379141/201867839-85dabca5-face-4635-88a6-3cc45c3867de.png)

- info:
```python
df.info()
```
![image](https://user-images.githubusercontent.com/101379141/201867903-202d0ced-fef0-4e45-b22c-bb311985d9da.png)

- describe:
```python
df.describe()
```
![image](https://user-images.githubusercontent.com/101379141/201867986-b76f63f5-8832-48a0-b2db-68c6efb067e1.png)

- Check unique values:
```python
df.nunique()
```
![image](https://user-images.githubusercontent.com/101379141/201868179-07f8d314-7799-42d5-b305-0434e8da4645.png)

- Checking duplicate values:
```python
df[df.duplicated()]
```
![image](https://user-images.githubusercontent.com/101379141/201868255-2cc7e91d-88a0-4208-a253-cc7224c25bbe.png)

 </details>

**2.Checking Null Values**

<details><summary> Click to expand code </summary>

```python
#Checking null Values
df.isnull().sum()
 ```

```python
#% Null values
dict_null = dict()
for i in df.columns:
  dict_null[i] = df[i].isnull().sum()/len(df['Price'])*100
df1 = pd.DataFrame.from_dict(dict_null.items())
print(df1)
```
![image](https://user-images.githubusercontent.com/101379141/201873131-15f9b46e-2a4e-4f05-96e7-2b5c74b34852.png)

--> The Null values of Manufacturer and Material Columns account for more than 10 %, they are really significant and they need to be transformed .

- Transforming Null Values :

```python
#Fill Null Value of Manufacturer, Material, Location, Type
values_replace = {'Manufacturer':'unspecified','Material':'unspecified','Location':'Unknow','Type':'unspecified'}
df.fillna(value = values_replace, inplace = True)
```

```python
#check again
df.isnull().sum()
```

```python
#Fill Null Value with mean of length and width 

length_mean = df['Length'].mean()
width_mean = df['Width'].mean()
df = df.fillna({'Length' :length_mean ,'Width' :width_mean })
df.isnull().sum()
```

![image](https://user-images.githubusercontent.com/101379141/201873787-df9065ea-42c4-4249-9043-f0c0208e9da6.png)

 </details>


## ✔ CHECKING COLUMNS


**1. Price Column**

- Firstly , we need to split Price column into 2 colunms (currency, price)
- Secondly, we need to check unique of currency , transform the wrong typing currency and convert all currency to EUR

 <details><summary> Click to expand code </summary>

```python
#Slit Price column into to two column currency and price
df[['currency','price']] = df.Price.str.split(expand = True)
df.head()
```
![image](https://user-images.githubusercontent.com/101379141/201875704-017f0096-7410-4c8c-b52a-fe7f77d27840.png)
 
 ```python
#Check Unique variable
df['currency'].unique()
 ```

 ```python
#Replace currency to GBP
df = df.replace('Â£','GBP') 
 ```
 
  ```python
#Histogram of currency to choose the mode of currency column
df['currency'].hist() 
 ```
 
  ```python
 #Convert all to EUR
df['price'] = df['price'].astype('int64')
c = CurrencyConverter()

def currency_convertor(row,new_currency='EUR'):
 amount = row['price']
 curr = row['currency']
 new_curr = c.convert(amount,curr,new_currency)
 return new_curr

df['Price'] = df.apply(lambda x: currency_convertor(x,new_currency="EUR"), axis=1).astype('int64')
 ```
 
 ![image](https://user-images.githubusercontent.com/101379141/201877724-5a69d7bf-a8f1-489e-ad41-471ea1ced337.png)
 
 - Drop unnecessary columns and check info again :

```python
#Drop column currency and price
df = df.drop(columns=['currency', 'price'])
```

```python
df.head()
```
</details>

![image](https://user-images.githubusercontent.com/101379141/201878087-1e286939-ebcb-4572-aebf-abe3b3c2a115.png)


**2. Boat Type Column**

- Check Boat Type and we can realize that one value of this column containing many types . We need to specify the most important type of boat.

<details><summary> Click to expand code </summary>

```python
df['Boat Type'].unique()
```
![image](https://user-images.githubusercontent.com/101379141/201879481-2b3885a5-f72d-4ea3-bed4-a0b21194f552.png)

```python
df[['Boat Type - 1st','Boat Type - 2nd', 'Boat Type - 3rd']] = df['Boat Type'].str.split(",",expand=True)
print(df[['Boat Type - 1st','Boat Type - 2nd', 'Boat Type - 3rd']])```
 ``` 
</details>

![image](https://user-images.githubusercontent.com/101379141/201890969-86d81e2b-9f20-42a3-945a-025d33d1f669.png)

**3. Type Column**

- Type column contain 2 different informations : Condition of boat & Type of Boat Engine. We need to split it to 2 diffrent columns

<details><summary> Click to expand code </summary>

```python
df[['Condition', 'Engine']] = df['Type'].str.split(",",expand=True)
print(df[['Condition', 'Engine']])
```
 </details>

![image](https://user-images.githubusercontent.com/101379141/201890124-160d1656-e0c5-4207-9101-25bd1eb322e0.png)

**4. Price Column**

- We group price column values by different group of price values 

<details><summary> Click to expand code </summary>
  
```python
sns.displot(df['Price'], bins = 20) 
```
![image](https://user-images.githubusercontent.com/101379141/201891626-9764385d-4cb7-4fc9-9f50-2a3d70c5ab2d.png)
  
```python
df['Price'].quantile([0.25,0.5,0.75])  
```

```python
Price_group = pd.cut(df['Price'],bins=[-1,50001,150001,300001,1000001,31000000],labels=['Lower_50K', '50K-150K','150K-300K', '300K-1M', 'Higher_1M'])
df.insert(15,'Price Group',Price_group) 
```
  
```python
print(df['Price Group'])
```
</details>

![image](https://user-images.githubusercontent.com/101379141/201891815-67a35019-e0ed-4d9c-ab2c-84de66f1fa08.png)

**5. Age Column**

- We group Age column values by different group of age

<details><summary> Click to expand code </summary>

 ```python
df['Age'] = 2022 - df['Year Built']
df['Age'] = df['Age'].replace(2022, 0) # Replace 2022 with 0
 ```
  
 ```python
 df['Age'].quantile([0.25,0.5,0.75])
 ``` 

 ```python
category_age = pd.cut(df['Age'],bins=[-1,6,16,31,51,101,137],labels=['0-5 years', '6-15 years','16-30 years', '31-50 years', '51-100 years', '101+ years'])
df.insert(16,'Age Group',category_age)
df['Age Group'] 
  
```
 </details>

![image](https://user-images.githubusercontent.com/101379141/201890440-2d03673b-bc19-421b-b192-3221ea0e521e.png)

**6. Location Column**
 - We need to transform and verify the valid country name. Because some customers input the city name only.
 
 <details><summary> Click to expand code </summary>
  
 ```python
 #Tranforming wrong typing country 
df['Location'] = df['Location'].replace('United','United Kingdom')
df['Location'] = df['Location'].replace('Slovak','Slovakia')
 ```
 ```python
 srs = validate_country(df["Location"])
df[~validate_country(df["Location"])]
 ```
 --> There are only 137 rows including invalid country names. So we can drop it

 ```python
df = df[validate_country(df["Location"])]
print(df)
 ```
 </details>
 
 - 137 rows invalid country
 
![image](https://user-images.githubusercontent.com/101379141/201885056-6976b300-4875-42e5-a167-ca90940f88f9.png)

 - Keep valid country rows. There are 9751 rows with valid country names
 
![image](https://user-images.githubusercontent.com/101379141/201887291-3d4e2510-1a49-4e22-b54f-45ebd9aca134.png)  

**7. View Columns**
- We group View column values by different group values.

 <details><summary> Click to expand code </summary>

```python
sns.distplot(df['Number of views last 7 days'], bins=20)
```

```python
df['Number of views last 7 days'].quantile([0.25,0.5,0.75])
```
```python
pv_category = pd.cut(df['Number of views last 7 days'],bins=[-1,71,111,176,1001,3263],labels=['Low', 'Medium','More than avergae', 'Good', 'Best'])
df.insert(17,'PV Group',pv_category)
```
```python
print(df['PV Group'])
```
</details>
 
![image](https://user-images.githubusercontent.com/101379141/201890594-18e6f879-583b-4633-8ef3-aeb1a3f6218d.png)

## Save File 

```python
df.to_csv('data_new_boat_1.csv')
```
## IMPORT CLEAN FILE TO POWER BI

**1. Transform Data** 

Use First rows as Header, Change type of click,cost,bookings,booking_rev,month column to Number type. Remove First Column (order column)
- Source data :
![image](https://user-images.githubusercontent.com/101379141/201894513-c4263575-e40b-42cc-a2f4-9b7933c7fd6e.png)

![image](https://user-images.githubusercontent.com/101379141/201894684-97f12f6b-6fee-4f88-8ed9-c13dbbc955d2.png)

![image](https://user-images.githubusercontent.com/101379141/201894759-e110a007-f81a-45e3-a0df-78f373ea8ce0.png)

- Promoted header, Change type 

![image](https://user-images.githubusercontent.com/101379141/201894136-a9bfc207-47aa-436b-96d6-751af62d8f5f.png)

- Replace values and fix typing errors :

![image](https://user-images.githubusercontent.com/101379141/201894397-af46c3c7-807b-4feb-a779-e28ce06ff844.png)



