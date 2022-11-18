# 🛒 Case Study - E-commerce Company
# A. Data Exploration and Cleansing

<p align="right"> Using Python - Google Colab vs Power BI </p>

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

### 1️⃣ Customers Dataset

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

---
### 2️⃣ Orders Dataset

- There are 3 things I would check in Orders dataset:
  - Check Overall Info
  - Transform data type of some columns from object to datatime
  - Check Null values

<details><summary> The  Overall  </summary>
  
```python
orders.head() 
```
![image](https://user-images.githubusercontent.com/101379141/202590328-96673499-1c64-4a7b-a446-84457184fddc.png)

```python
orders.info()
```
![image](https://user-images.githubusercontent.com/101379141/202590347-7419779c-917a-47c9-81c3-bc94df5c63e6.png)
  
 </details>

<details><summary> Transform Data Type  </summary>
  
```python
#Transforming the data type from object to datetime 
orders['order_purchase_timestamp'] = pd.to_datetime(orders['order_purchase_timestamp'], format = '%Y-%m-%d %H:%M:%S')
orders['order_approved_at'] = pd.to_datetime(orders['order_approved_at'], format = '%Y-%m-%d %H:%M:%S')
orders['order_delivered_carrier_date'] = pd.to_datetime(orders['order_delivered_carrier_date'], format = '%Y-%m-%d %H:%M:%S')
orders['order_delivered_customer_date'] = pd.to_datetime(orders['order_delivered_customer_date'], format = '%Y-%m-%d %H:%M:%S')
orders['order_estimated_delivery_date'] = pd.to_datetime(orders['order_estimated_delivery_date'], format = '%Y-%m-%d %H:%M:%S')

orders.info()
```
![image](https://user-images.githubusercontent.com/101379141/202590474-5722e629-b482-4c4e-8065-f1e7b2b266f6.png)
  
</details>

<details><summary> Check Null Values </summary>

```python
#Check Null Values
orders.isnull().sum()
```

```python
#Check Percent of Null values. 
# Because the null values does not accounts much of total dataset ( about 3% is max), we can ignore or drop it
# However, The null values of these columns were also mean that the orders were not delivered to customer or carrier. So We can not drop them. 
orders.isnull().mean() * 100

```
![image](https://user-images.githubusercontent.com/101379141/202590671-f64db3e4-4fa4-49d6-9c68-908cea61fee4.png)

</details>

---
### 3️⃣ Order Items Dataset

- The order items dataset is clean so we don't need to adjust it.

<details><summary> The  Overall  </summary>

 ```python
 order_items.head() 
 ```
 ![image](https://user-images.githubusercontent.com/101379141/202591464-b8cd4a4a-91f9-401c-9c75-e2c33a6235e3.png)

 ```python
 order_items.describe() 
 ```
 ![image](https://user-images.githubusercontent.com/101379141/202591488-d3e2293e-cd45-4865-ac51-c0e7d548658d.png)

 ```python
 order_items.info() 
 ```
 
 ![image](https://user-images.githubusercontent.com/101379141/202591523-23610480-51e9-401c-9ca9-3b462101b617.png)
 
  
</details>
 
---
### 4️⃣ Order Payments Dataset

- After The order payments dataset is clean. We don't need to adjust it.

<details><summary> The  Overall  </summary>

 ```python
 order_payments.head() 
 ```
![image](https://user-images.githubusercontent.com/101379141/202591939-ccd8d81a-2a52-4cab-affc-efded8b4b934.png)

```python
order_payments.info() 
```
![image](https://user-images.githubusercontent.com/101379141/202591974-428d8f50-9fd3-4ce2-b206-8dbbd40c60e1.png)

  
```python
order_payments['payment_type'].unique() 
```
![image](https://user-images.githubusercontent.com/101379141/202591995-81284279-97c3-49a2-a953-f3b0b3bab9cb.png)
  
</details>

---
### 5️⃣ Order Reviews Dataset

- There are 2 things that we are doing with this dataset:
  - The Overall
  - Transform data type from object to datetime 

<details><summary> The  Overall  </summary>

 ```python
 order_reviews.head() 
 ```
![image](https://user-images.githubusercontent.com/101379141/202593250-30d0b6e6-fd98-4413-98ac-93772b75b8d7.png)
  
```python
order_reviews.info() 
```
![image](https://user-images.githubusercontent.com/101379141/202593274-eb0ce20e-5c1e-4b96-8936-ed3a2d43536a.png)
  
```python
order_reviews['review_score'].value_counts()
```
![image](https://user-images.githubusercontent.com/101379141/202593298-38b5ceb6-5e8d-4695-93c6-8d624c479258.png)
 
</details>

<details><summary> Transform data type  </summary>

```python
 order_reviews['review_creation_date'] = pd.to_datetime(order_reviews['review_creation_date'])
order_reviews['review_answer_timestamp'] = pd.to_datetime(order_reviews['review_answer_timestamp'])

order_reviews['review_creation_date'] = order_reviews.review_creation_date.dt.strftime('%m/%d/%Y')
order_reviews['review_answer_timestamp'] = order_reviews.review_answer_timestamp.dt.strftime('%m/%d/%Y')
order_reviews.head(5)
 ```
  
![image](https://user-images.githubusercontent.com/101379141/202593442-736774bf-875a-4ff0-a273-bb31b2958a31.png)
 
</details>

---  
###  6️⃣Products Dataset
  
- There are 3 things that we are doing with this dataset:
  - The Overall
  - Checking Null values .
  - Replacing the "0 gram" of product weight to median

<details><summary> The  Overall  </summary>
  
 ```python
 products.head() 
 ```
![image](https://user-images.githubusercontent.com/101379141/202595562-89179cb5-d1b8-4503-ac9b-908cc286c44a.png)
  
```python
products.info() 
```
![image](https://user-images.githubusercontent.com/101379141/202595592-4a82a95a-9136-48ed-bba7-2fa4bc89777c.png)

  
```python
products.describe()
``` 
![image](https://user-images.githubusercontent.com/101379141/202595632-653f740c-1449-4279-a542-d9d506b269bf.png)

```python
# Min of product_weight_g = 0 , so we check this column to make sure there is nothing anomaly
products[products['product_weight_g']== 0]  
```
  
 ![image](https://user-images.githubusercontent.com/101379141/202595685-8a7e6a1c-c51d-4c21-a6b4-779cce86637b.png)

</details>

<details><summary> Check Null Values  </summary>

```python
#Check Null Values
products.isnull().sum()
```
![image](https://user-images.githubusercontent.com/101379141/202596089-660af9b9-c2b1-4f9b-b894-945d6c388aba.png)

  
```python
#Check Null values of category name column
products[products['product_category_name'].isnull() == True]
```
![image](https://user-images.githubusercontent.com/101379141/202596188-5f0c384f-8126-4b1e-b4b6-fc80c8d0841b.png)
  
```python
#Check Null values of weight column
products[products['product_weight_g'].isnull() == True]
```
![image](https://user-images.githubusercontent.com/101379141/202596235-c4e5dffb-90cf-4c80-97a0-3d14e83ba554.png)
  
```python
#Drop all 610 Null value rows , because they are not significant ( 610  rows >< 32951 total entries )
products = products.dropna()  
products.isnull().sum()  
                                                                                     
```
![image](https://user-images.githubusercontent.com/101379141/202596277-466fbd1b-d48b-4621-87a7-de256a357f78.png)
                                                                                     
</details>

  
---

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



