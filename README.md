# AltMobilityCaseStudy
# SQL Queries for Customer Orders and Payments Analysis
This repository contains a set of SQL queries I wrote to analyze customer orders and payment data. The goal is to get a clearer picture of customer behavior, sales patterns, and payment trends. I used these queries to answer questions like: How many orders are we getting each month? What’s the status of payments? Are our customers repeat buyers or one-time shoppers?
1. Total Orders and Total Amount
sql
Copy
Edit
select 
    count(order_id) as "total order", 
    round(sum(order_amount), 0) as "total amount" 
from customerorders;
This one is pretty simple – it just gives us the total number of orders placed and the total sales amount. It’s a great starting point for any analysis since it gives us the overall picture of how much business we’ve done.

2. Order Status Breakdown
sql
Copy
Edit
select 
    order_status, 
    count(*) as status_count 
from customerorders 
group by order_status 
order by status_count desc;
This query helps us see how many orders are in each status, like ‘Completed’, ‘Pending’, or ‘Cancelled’. Sorting them by count helps highlight which statuses are most common, and it can show us if there’s an issue with a particular stage in the order process.

3. Monthly Orders and Sales
sql
Copy
Edit
select 
    format(order_date, 'yyyy-MM') as order_month,
    count(order_id) as total_orders,
    round(sum(order_amount), 0) as total_sales
from customerorders 
group by format(order_date, 'yyyy-MM') 
order by order_month;
This one focuses on analyzing sales over time, breaking them down by month. By formatting the order date, we can track both the number of orders and the total amount of money coming in each month. It’s perfect for spotting trends and seasonal changes.

4. Customer Type (One-Time vs Repeat)
sql
Copy
Edit
select 
    customer_type,
    count(*) as customer_count
from (
    select 
        customer_id,
        case 
            when count(*) = 1 then 'one-time'
            else 'repeat'
        end as customer_type
    from customerorders 
    group by customer_id
) as sub 
group by customer_type;
This query checks how many of our customers are one-time buyers versus repeat customers. It looks at how many orders each customer has placed. By counting them, we get a better understanding of customer loyalty, which can help us improve retention strategies.

5. New vs Returning Customers by Month
sql
Copy
Edit
with first_orders as (
    select 
        customer_id,
        min(order_date) as first_order_date
    from customerorders 
    group by customer_id
)
select 
    format(c.order_date, 'yyyy-MM') as order_month,
    sum(case when c.order_date = f.first_order_date then 1 else 0 end) as new_customers,
    sum(case when c.order_date <> f.first_order_date then 1 else 0 end) as returning_customers
from customerorders c 
join first_orders f on c.customer_id = f.customer_id 
group by format(c.order_date, 'yyyy-MM') 
order by order_month;
I wanted to track how many new versus returning customers we have each month. This query compares each order’s date to the customer’s first order date, helping to distinguish between new customers and those who have shopped with us before. It’s great for understanding customer retention.

6. Payment Status Breakdown
sql
Copy
Edit
select 
    payment_status,
    count(*) as count 
from payments 
group by payment_status 
order by count desc;
This one gives a quick view of how many payments fall into each status (like ‘Completed’, ‘Failed’, etc.). If there’s a lot of failed payments, this could signal an issue with our payment processing system.

7. Failed Payments by Method
sql
Copy
Edit
select 
    payment_method,
    count(*) as failed_count 
from payments 
where payment_status = 'failed' 
group by payment_method 
order by failed_count desc;
This query is designed to dig deeper into failed payments, showing us which payment methods are causing the most issues. It’s super useful if you want to figure out if specific payment gateways or methods need attention.

8. Customer Orders with Payment Info
sql
Copy
Edit
select 
    o.order_id,
    o.customer_id,
    o.order_date,
    o.order_status,
    o.order_amount,
    p.payment_date,
    p.payment_amount,
    p.payment_method,
    p.payment_status
from customerorders o 
left join payments p on o.order_id = p.order_id;
Finally, this query joins the customerorders table with the payments table to give a detailed view of each order along with its payment info. It includes everything from the order date to the payment status, making it easy to track which payments are linked to which orders.

