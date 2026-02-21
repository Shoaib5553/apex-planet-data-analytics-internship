# Data Dictionary: Brazilian E-Commerce Dataset (Olist)

This document provides a comprehensive overview of the 9 datasets used in this analysis, detailing the schema, data types, and business context for every column.

## 1. olist_orders_dataset

The core fact table that records every order made on the platform.

| Column Name | Data Type | Business Meaning | 
| ----- | ----- | ----- | 
| `order_id` | String | Unique identifier for the order. (Primary Key) | 
| `customer_id` | String | Unique identifier linking to the customer who made the purchase. (Foreign Key) | 
| `order_status` | String | Reference to the order state (e.g., delivered, shipped, canceled, invoiced). | 
| `order_purchase_timestamp` | Datetime | The exact date and time the purchase was completed by the customer. | 
| `order_approved_at` | Datetime | Timestamp indicating when the payment was approved. | 
| `order_delivered_carrier_date` | Datetime | Timestamp when the order was handed over to the logistics partner. | 
| `order_delivered_customer_date` | Datetime | Timestamp when the order was actually delivered to the customer. | 
| `order_estimated_delivery_date` | Datetime | The estimated delivery date provided to the customer at the time of purchase. | 

## 2. olist_order_items_dataset

Contains the specific items purchased within each order.

| Column Name | Data Type | Business Meaning | 
| ----- | ----- | ----- | 
| `order_id` | String | Unique identifier for the order. (Foreign Key) | 
| `order_item_id` | Integer | Sequential number identifying the number of items included in the same order. | 
| `product_id` | String | Unique identifier for the product purchased. (Foreign Key) | 
| `seller_id` | String | Unique identifier for the seller who fulfilled the order. (Foreign Key) | 
| `shipping_limit_date` | Datetime | The seller's deadline for transferring the goods to the logistics partner. | 
| `price` | Float | The item price. | 
| `freight_value` | Float | The shipping fee associated with the specific item (prorated if multiple items). | 

## 3. olist_customers_dataset

Information about the customers making the purchases.

| Column Name | Data Type | Business Meaning | 
| ----- | ----- | ----- | 
| `customer_id` | String | Key linking to the orders dataset. Represents a specific transaction instance of a customer. (Primary Key) | 
| `customer_unique_id` | String | Unique identifier for a customer. Used to track repeat purchases across multiple `customer_id`s. | 
| `customer_zip_code_prefix` | String | First five digits of the customer's zip code. | 
| `customer_city` | String | Customer's city name. | 
| `customer_state` | String | Customer's state code (e.g., SP, RJ). | 

## 4. olist_sellers_dataset

Information about the merchants selling on the Olist platform.

| Column Name | Data Type | Business Meaning | 
| ----- | ----- | ----- | 
| `seller_id` | String | Unique identifier for the seller. (Primary Key) | 
| `seller_zip_code_prefix` | String | First five digits of the seller's zip code. | 
| `seller_city` | String | Seller's city name. | 
| `seller_state` | String | Seller's state code. | 

## 5. olist_products_dataset

Details about the physical products sold.

| Column Name | Data Type | Business Meaning | 
| ----- | ----- | ----- | 
| `product_id` | String | Unique identifier for the product. (Primary Key) | 
| `product_category_name` | String | Root category of the product, written in Portuguese. | 
| `product_name_lenght` | Integer | Number of characters extracted from the product name. | 
| `product_description_lenght` | Integer | Number of characters extracted from the product description. | 
| `product_photos_qty` | Integer | Number of photos published for the product. | 
| `product_weight_g` | Integer | Product weight measured in grams. | 
| `product_length_cm` | Integer | Product length measured in centimeters. | 
| `product_height_cm` | Integer | Product height measured in centimeters. | 
| `product_width_cm` | Integer | Product width measured in centimeters. | 

## 6. product_category_name_translation

Translates the Portuguese product categories into English for international analysis.

| Column Name | Data Type | Business Meaning | 
| ----- | ----- | ----- | 
| `product_category_name` | String | Category name in Portuguese. (Matches `olist_products_dataset`) | 
| `product_category_name_english` | String | Category name translated to English. | 

## 7. olist_order_payments_dataset

Records of how customers paid for their orders.

| Column Name | Data Type | Business Meaning | 
| ----- | ----- | ----- | 
| `order_id` | String | Unique identifier for the order. (Foreign Key) | 
| `payment_sequential` | Integer | A sequence number indicating if a customer paid using multiple methods (e.g., voucher + credit card). | 
| `payment_type` | String | The method of payment chosen (e.g., credit_card, boleto, voucher). | 
| `payment_installments` | Integer | The number of installments chosen by the customer for the payment. | 
| `payment_value` | Float | The transaction value associated with that specific payment sequential. | 

## 8. olist_order_reviews_dataset

Customer feedback and satisfaction ratings left after an order is fulfilled.

| Column Name | Data Type | Business Meaning | 
| ----- | ----- | ----- | 
| `review_id` | String | Unique identifier for the review. | 
| `order_id` | String | Unique identifier for the order being reviewed. (Foreign Key) | 
| `review_score` | Integer | Satisfaction score ranging from 1 to 5 given by the customer. | 
| `review_comment_title` | String | The title left by the customer in the review. | 
| `review_comment_message` | String | The detailed text message left by the customer. | 
| `review_creation_date` | Datetime | The date the satisfaction survey was sent to the customer. | 
| `review_answer_timestamp` | Datetime | The exact timestamp when the customer submitted the review answer. | 

## 9. olist_geolocation_dataset

Mapping of Brazilian zip codes to geographic coordinates.

| Column Name | Data Type | Business Meaning | 
| ----- | ----- | ----- | 
| `geolocation_zip_code_prefix` | String | First five digits of the zip code. | 
| `geolocation_lat` | Float | Latitude coordinate corresponding to the zip code. | 
| `geolocation_lng` | Float | Longitude coordinate corresponding to the zip code. | 
| `geolocation_city` | String | City name. | 
| `geolocation_state` | String | State code. |
