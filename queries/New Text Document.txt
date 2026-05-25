-- 1. TOTAL ORDERS
SELECT COUNT(*) AS total_orders
FROM olist_orders_dataset;

-- 2. TOTAL REVENUE
SELECT SUM(payment_value) AS total_revenue
FROM olist_order_payments_dataset;

-- 3. UNIQUE CUSTOMERS
SELECT COUNT(DISTINCT customer_unique_id) AS total_customers
FROM olist_customers_dataset;

-- 4. AVERAGE PAYMENT
SELECT AVG(payment_value) AS average_payment
FROM olist_order_payments_dataset;

-- 5. ORDER STATUS COUNT
SELECT order_status, COUNT(*) AS number_of_orders
FROM olist_orders_dataset
GROUP BY order_status;

-- 6. MAX PAYMENT
SELECT MAX(payment_value) AS max_payment
FROM olist_order_payments_dataset;

-- 7. MIN PAYMENT
SELECT MIN(payment_value) AS min_payment
FROM olist_order_payments_dataset;

-- 8. PAYMENT TYPES
SELECT DISTINCT payment_type
FROM olist_order_payments_dataset;

-- 9. REVENUE BY PAYMENT TYPE
SELECT payment_type,
       SUM(payment_value) AS total_revenue_per_type
FROM olist_order_payments_dataset
GROUP BY payment_type
ORDER BY total_revenue_per_type DESC;

-- 10. TOP 3 PAYMENT TYPES
SELECT TOP 3 payment_type,
       SUM(payment_value) AS total_revenue_per_type
FROM olist_order_payments_dataset
GROUP BY payment_type
ORDER BY total_revenue_per_type DESC;

-- 11. TOP 5 LATEST ORDERS
SELECT TOP 5 order_purchase_timestamp, order_id
FROM olist_orders_dataset
ORDER BY order_purchase_timestamp DESC;

-- 12. HIGH VALUE PAYMENTS
SELECT order_id, payment_type, payment_value
FROM olist_order_payments_dataset
WHERE payment_value > 1000;

-- 13. TOP 10 PAYMENTS
SELECT TOP 10 payment_value, order_id, payment_type
FROM olist_order_payments_dataset
ORDER BY payment_value DESC;

-- 14. ORDERS AFTER 2018
SELECT order_id, order_purchase_timestamp
FROM olist_orders_dataset
WHERE order_purchase_timestamp > '2018-01-01';

-- 15. YEARLY ORDERS
SELECT YEAR(order_purchase_timestamp) AS year,
       COUNT(*) AS total_orders
FROM olist_orders_dataset
GROUP BY YEAR(order_purchase_timestamp);

-- 16. YEARLY REVENUE
SELECT YEAR(o.order_purchase_timestamp) AS year,
       SUM(p.payment_value) AS total_revenue
FROM olist_orders_dataset o
JOIN olist_order_payments_dataset p
ON o.order_id = p.order_id
GROUP BY YEAR(o.order_purchase_timestamp);

-- 17. TOP CUSTOMERS BY REVENUE
SELECT TOP 10 o.customer_id,
       SUM(p.payment_value) AS total_revenue
FROM olist_orders_dataset o
JOIN olist_order_payments_dataset p
ON o.order_id = p.order_id
GROUP BY o.customer_id
ORDER BY total_revenue DESC;

-- 18. CUSTOMERS WITH MULTIPLE ORDERS
SELECT customer_id,
       COUNT(order_id) AS total_orders
FROM olist_orders_dataset
GROUP BY customer_id
HAVING COUNT(order_id) > 1;

-- 19. AVERAGE REVENUE PER CUSTOMER
SELECT o.customer_id,
       AVG(p.payment_value) AS average_revenue
FROM olist_orders_dataset o
JOIN olist_order_payments_dataset p
ON o.order_id = p.order_id
GROUP BY o.customer_id;

-- 20. TOP 5 CUSTOMERS BY AVERAGE REVENUE
SELECT TOP 5 o.customer_id,
       AVG(p.payment_value) AS average_revenue
FROM olist_orders_dataset o
JOIN olist_order_payments_dataset p
ON o.order_id = p.order_id
GROUP BY o.customer_id
ORDER BY average_revenue DESC;

-- 21. MONTHLY REVENUE
SELECT MONTH(o.order_purchase_timestamp) AS month,
       SUM(p.payment_value) AS total_revenue
FROM olist_orders_dataset o
JOIN olist_order_payments_dataset p
ON o.order_id = p.order_id
GROUP BY MONTH(o.order_purchase_timestamp);

-- 22. PAYMENT CATEGORY (CASE WHEN)
SELECT order_id,
       payment_value,
       CASE
           WHEN payment_value > 500 THEN 'High Payment'
           WHEN payment_value >= 100 THEN 'Medium Payment'
           ELSE 'Low Payment'
       END AS payment_category
FROM olist_order_payments_dataset;

-- 23. CTE: HIGH VALUE CUSTOMERS
WITH customer_revenue AS
(
    SELECT o.customer_id,
           SUM(p.payment_value) AS total_revenue
    FROM olist_orders_dataset o
    JOIN olist_order_payments_dataset p
    ON o.order_id = p.order_id
    GROUP BY o.customer_id
)
SELECT *
FROM customer_revenue
WHERE total_revenue > 5000;

-- 24. CUSTOMER RANKING (RANK)
WITH customer_revenue AS
(
    SELECT o.customer_id,
           SUM(p.payment_value) AS total_revenue
    FROM olist_orders_dataset o
    JOIN olist_order_payments_dataset p
    ON o.order_id = p.order_id
    GROUP BY o.customer_id
)
SELECT customer_id,
       total_revenue,
       RANK() OVER (ORDER BY total_revenue DESC) AS rnk
FROM customer_revenue;