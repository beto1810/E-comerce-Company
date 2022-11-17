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

### Customers Dataset

- There are 4 things I would check in customers dataset:
  - The overall info 
  - There is duplicated value of primary key or not (customer_id)
  - Checking unique values of city name, State.
  - Capitalize the first letter of city name.

<details><summary> The  Overall Infomation </summary>
  
```python
customer.head() 
```
![image](https://user-images.githubusercontent.com/101379141/202383092-4502607a-157e-4982-b843-d386308398e4.png)

```python
customers.info()
```
![image](https://user-images.githubusercontent.com/101379141/202383205-458cecd8-c962-4ca1-9d38-6b04d45a7fb6.png)

 </details>
 
 <details><summary> Checking duplicated values </summary>
  
```python
#Checking the duplicated values of primary key column (customer_id), because number of customer_id is same with total data entries (99441), so we can conclude that there is not duplicated values

customers.nunique()   
```  
![image](https://user-images.githubusercontent.com/101379141/202384243-a902b51d-6423-41ea-9028-c40731efdddc.png)
  
 </details>

 <details><summary> Checking unique values of State </summary>

 ```python
#Checking State typing 
customers['customer_state'].unique() 
 ```
![image](https://user-images.githubusercontent.com/101379141/202384543-036fe5fb-9a9b-48fb-abfb-ca6837b96d6e.png)

 </details>
 
  <details><summary>  Capitalize the first letter of city name  </summary>

 ``` python
#Capitalize the first letter of city name
customers['customer_city'] = customers['customer_city'].str.title()
 
```
```python
customers.head()
```
![image](https://user-images.githubusercontent.com/101379141/202384920-d67e7d24-75b0-47d2-b35e-28254473878b.png)

 </details>
  
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



