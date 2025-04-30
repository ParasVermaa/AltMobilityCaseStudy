# AltMobilityCaseStudy
# SQL Queries for Customer Orders and Payments Analysis
This repository contains a set of SQL queries I wrote to analyze customer orders and payment data. The goal is to get a clearer picture of customer behavior, sales patterns, and payment trends. I used these queries to answer questions like: How many orders are we getting each month? What’s the status of payments? Are our customers repeat buyers or one-time shoppers?
1. Total Orders and Total Amount
<br>
This one is pretty simple – it just gives us the total number of orders placed and the total sales amount. It’s a great starting point for any analysis since it gives us the overall picture of how much business we’ve done.

2. Order Status Breakdown
<br>This query helps us see how many orders are in each status, like ‘Completed’, ‘Pending’, or ‘Cancelled’. Sorting them by count helps highlight which statuses are most common, and it can show us if there’s an issue with a particular stage in the order process.

3. Monthly Orders and Sales
<br>
This one focuses on analyzing sales over time, breaking them down by month. By formatting the order date, we can track both the number of orders and the total amount of money coming in each month. It’s perfect for spotting trends and seasonal changes.

4. Customer Type (One-Time vs Repeat)
<br>
This query checks how many of our customers are one-time buyers versus repeat customers. It looks at how many orders each customer has placed. By counting them, we get a better understanding of customer loyalty, which can help us improve retention strategies.

5. New vs Returning Customers by Month
<br>
I wanted to track how many new versus returning customers we have each month. This query compares each order’s date to the customer’s first order date, helping to distinguish between new customers and those who have shopped with us before. It’s great for understanding customer retention.

6. Payment Status Breakdown
<br>
This one gives a quick view of how many payments fall into each status (like ‘Completed’, ‘Failed’, etc.). If there’s a lot of failed payments, this could signal an issue with our payment processing system.

7. Failed Payments by Method
<br>
This query is designed to dig deeper into failed payments, showing us which payment methods are causing the most issues. It’s super useful if you want to figure out if specific payment gateways or methods need attention.

8. Customer Orders with Payment Info
<br>
Finally, this query joins the customerorders table with the payments table to give a detailed view of each order along with its payment info. It includes everything from the order date to the payment status, making it easy to track which payments are linked to which orders.

