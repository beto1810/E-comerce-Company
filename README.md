# 🛒 E-commerce Company

## Final Test of "BI Course" of MINDX TECHNOLOGY SCHOOL.

 <img src="https://user-images.githubusercontent.com/101379141/201035143-6f1af4fe-4169-4074-8287-6790d88803db.png" alt="Image" width="350" height="160">  



# :books: Table of Contents <!-- omit in toc -->

- [:briefcase: Business Case](#briefcase-business-case)
- [:bookmark_tabs:Example Datasets](#bookmark_tabsexample-datasets)
- [:triangular_flag_on_post: The Requirement](#triangular_flag_on_post-the-final-test-requirements)
- [A. Data Exploration and Cleansing](#a-data-exploration-and-cleansing)
- [B. Analysis](#b-analysis)

- [📃 What can you practice with this case study?](#what-can-you-practice-with-this-case-study)

---

# :briefcase: Business Case


You are a Data Analyst working for an e-commerce company named X. You are tasked with preparing a presentation to present an overview of the company's business and operations to date for Sales and Operations Managers. 

The presentation should include at a minimum the following information: 
- Business overview. 
- Customer satisfaction.  
- 2 to 3 areas of recommendation (areas) where the company can improve.

Some additional information for the case study:
- Since there is only data up to 2018, we will assume that it is currently September 2018 (data after September 2018 you can ignore).
- The company is based in the US, but incorporated in Brazil (that's why some information is written in Portuguese).

---

# :bookmark_tabs:Example Datasets

### Orders dataset
Provide information about orders
- order_id: unique ID of the order
- customer_id: unique ID of the customer
- order_status: order status
- order_purchase_timestamp: time when the order was ordered
- order_approved_at: time the order is approved
- order_delivered_carrier_date: the time the item was delivered to the carrier
- order_delivered_customer_date: the time the item was delivered to the customer
- order_estimated_delivery_date: the estimated time the order will be delivered to the customer


<div align="center">

**Table: orders_dataset** 

<div align="center">
First 10 rows

|order_id|customer_id|order_status|order_purchase_timestamp|order_approved_at|order_delivered_carrier_date|order_delivered_customer_date|order_estimated_delivery_date|
|:----|:-----|:----|:----|:----|:----|:----|:----|
e481f51cbdc54678b7cc49136f2d6af7|	9ef432eb6251297304e76186b10a928d|	delivered|	10/2/2017 10:56|10/2/2017 11:07|	10/4/2017 19:55|	10/10/2017 21:25|	10/18/2017|
53cdb2fc8bc7dce0b6741e2150273451|	b0830fb4747a6c6d20dea0b8c802d7ef|	delivered|	7/24/2018 20:41|	7/26/2018 3:24|	7/26/2018 14:31|	8/7/2018 15:27|	8/13/2018|
47770eb9100c2d0c44946d9cf07ec65d|	41ce2a54c0b03bf3443c3d931a367089|	delivered|	8/8/2018 8:38|	8/8/2018 8:55|	8/8/2018 13:50|	8/17/2018 18:06|	9/4/2018|
949d5b44dbf5de918fe9c16f97b45f8a|	f88197465ea7920adcdbec7375364d82|	delivered|	11/18/2017 19:28|	11/18/2017 19:45|	11/22/2017 13:39|	12/2/2017 0:28|	12/15/2017|
ad21c59c0840e6cb83a9ceb5573f8159|	8ab97904e6daea8866dbdbc4fb7aad2c|	delivered|	2/13/2018 21:18|	2/13/2018 22:20|	2/14/2018 19:46|	2/16/2018 18:17	|2/26/2018|
a4591c265e18cb1dcee52889e2d8acc3|	503740e9ca751ccdda7ba28e9ab8f608|	delivered|	7/9/2017 21:57|	7/9/2017 22:10|	7/11/2017 14:58|	7/26/2017 10:57|	8/1/2017|
136cce7faa42fdb2cefd53fdc79a6098|	ed0271e0b7da060a393796590e7b737a|	invoiced|	4/11/2017 12:22|	4/13/2017 13:25|||			|5/9/2017|
6514b8ad8028c9f2cc2374ded245783f|	9bdf08b4b3b52b5526ff42d37d47f222|	delivered|	5/16/2017 13:10|	5/16/2017 13:22|	5/22/2017 10:07|	5/26/2017 12:55|	6/7/2017|
76c6e866289321a7c93b82b54852dc33|	f54a9f0e6b351c431402b8461ea51999|	delivered|	1/23/2017 18:29|	1/25/2017 2:50|	1/26/2017 14:16|	2/2/2017 14:08|	3/6/2017|
e69bfb5eb88e0ed6a785585b27e16dbf|	31ad1d1b63eb9962463f764d4e6e0c9d|	delivered|	7/29/2017 11:55|	7/29/2017 12:05|	8/10/2017 19:45|	8/16/2017 17:14|	8/23/2017|

</div>
</div>

---

### Order items dataset  
Provide information about each item in the order and shipping costs
- order_id: unique ID of the order
- order_item_id: ID of the item in the order (item number 1 has ID 1, item 2 has ID 2, etc. Based on this we also know how many items each order has)
- product_id: unique ID of the product in the order
- seller_id: unique ID of the seller
- price: the price of the item
- freight_value: shipping fee


<div align="center">

**Table: order_items_dataset** 

<div align="center">
First 10 rows


|order_id|order_item_id|product_id|seller_id|price|freight_value|
|:----|:-----|:----|:----|:----|:----|
00010242fe8c5a6d1ba2dd792cb16214|	1|	4244733e06e7ecb4970a6e2683c13e61|	48436dade18ac8b2bce089ec2a041202|	58.9|	13.29|
00018f77f2f0320c557190d7a144bdd3|	1|	e5f2d52b802189ee658865ca93d83a8f|dd7ddc04e1b6c2c614352b383efe2d36|	239.9|	19.93|
000229ec398224ef6ca0657da4fc703e|	1|	c777355d18b72b67abbeef9df44fd0fd|	5b51032eddd242adc84c38acab88f23d|	199|	17.87|
00024acbcdf0a6daa1e931b038114c75|	1|	7634da152a4610f1595efa32f14722fc|	9d7a1d34a5052409006425275ba1c2b4|	12.99|	12.79|
00042b26cf59d7ce69dfabb4e55b4fd9|	1|	ac6c3623068f30de03045865e4e10089|	df560393f3a51e74553ab94004ba5c87|	199.9|	18.14|
00048cc3ae777c65dbb7d2a0634bc1ea|	1	|ef92defde845ab8450f9d70c526ef70f|	6426d21aca402a131fc0a5d0960a3c90|	21.9|	12.69|
00054e8431b9d7675808bcb819fb4a32|	1|	8d4f2bb7e93e6710a28f34fa83ee7d28|	7040e82f899a04d1b434b795a43b4617|	19.9|	11.85|
000576fe39319847cbb9d288c5617fa6|	1|	557d850972a7d6f792fd18ae1400d9b6|	5996cddab893a4652a15592fb58ab8db|	810|	70.75|
0005a1a1728c9d785b8e2b08b904576c|	1|	310ae3c140ff94b03219ad0adc3c778f|	a416b6a846a11724393025641d4edd5e|	145.95|	11.65|
0005f50442cb953dcd1d21e1fb923495|	1|	4535b0e1091c278dfd193e5a1d63b39f|	ba143b05f0110f0dc71ad71b4466ce92|	53.99|	11.4|
  
</div>
</div>

---

### Order payments dataset
Provide information of order payments.

*Note that we need to combine all values of each order to have total values.*

order_id: unique ID of order
payment_sequential: sequence order
payment_type: payment type
payment_installments: full payment (payment_installments = 1) hay installment (payment_installments > 1,total payment is splited to many payments . payment_value equal total payments of all times payment installments)
payment_value: giá trị của thanh toán

<div align="center">

**Table: order_payments_dataset** 

<div align="center">
First 10 rows

|order_id|payment_sequential|payment_type|payment_installments|payment_value|
|:----|:-----|:----|:----|:----|
b81ef226f3fe1789b1e8b2acac839d17| 1	|credit_card|	8|	99.33|
a9810da82917af2d9aefd1278f1dcfa0|	1	|credit_card|	1|	24.39|
25e8ea4e93396b6fa0d3dd708e76c1bd|	1	|credit_card|	1|	65.71|
ba78997921bbcdc1373bb41e913ab953|	1	|credit_card|	8|	107.78|
42fdf880ba16b47b59251dd489d4441a|	1	|credit_card|	2|	128.45|
298fcdf1f73eb413e4d26d01b25bc1cd|	1	|credit_card|	2|	96.12|
771ee386b001f06208a7419e4fc1bbd7|	1	|credit_card|	1|	81.16|
3d7239c394a212faae122962df514ac7|	1	|credit_card|	3|	51.84|
1f78449c87a54faf9e96e88ba1491fa9|	1	|credit_card|	6|	341.09|
0573b5e23cbd798006520e1d5b4c6714|	1	|cash|	1|	51.95|


</div>
</div>
---

# :triangular_flag_on_post: The Final Test Requirements
## 1.	Market Trending
One of the indicators that the Marketplace team cares about is the conversion rate of users. In other words, they care about the percentage of users who can find the right hotel booking for their needs on the ABC website. One way to determine this is to calculate the booking conversion rate, which is calculated by dividing the number of bookings by the number of clicks.

- These are some suggestions:
  - Draw a daily booking conversion chart for the whole year of 2019 for ABC website
  - Do you notice any trends? What factors are driving this trend? (What are the main drivers of this trend?)
  - Can you guess which country these data are from? On what basis do you speculate?

## 2.	Advertiser performance
- One of your main tasks as a Market Data Analyst is to understand advertisers' performance, using datasets similar to the one you were provided with. From an advertiser's perspective:
  - Assuming every advertiser has a profit margin of 15% for all customer segments (short, medium, long), calculate the total profit of each advertiser for the year.
  - Based on the trends you've discovered, what recommendations do you have for each advertiser to improve their advertising campaigns in 202


# A. [Data Exploration and Cleansing](https://github.com/beto1810/Online_Hotel_Web_Search/blob/main/A.%20Data%20Exploration%20and%20Cleansing.md)


# B. [Analysis](https://github.com/beto1810/Online_Hotel_Web_Search/blob/main/B.Analysis.md)


# 🧾 What can you practice with this case study?
- Python
  - pandas, numpy
  - cleaning, transforming.
  - unpivot, wide_to_long
  - import, save csv file. 
- POWER BI
  - Visualize
  - Analyze
  - Import CSV File and Transform data
