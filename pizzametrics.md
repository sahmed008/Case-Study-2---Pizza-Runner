# 🍕 Case Study #2 - Pizza Runner

## 🍝 Solution - A. Pizza Metrics

### 1. How many pizzas were ordered?

````sql
SELECT 
 COUNT(*) AS orders
FROM pizza_runner.customer_orders;
````
![image](https://user-images.githubusercontent.com/104872221/226990597-f58bf79d-6948-4f47-8a57-da0235f3b5c2.png)

### 2. How many unique customer orders were made?
````sql
SELECT 
 COUNT(DISTINCT order_id) AS orders
FROM pizza_runner.customer_orders;
````
![image](https://user-images.githubusercontent.com/104872221/226999349-77527194-1a44-4a51-8475-9fe76ffbc344.png)

### 3.How many successful orders were delivered by each runner?
````sql
SELECT 
  runner_id, 
  COUNT(order_id) AS successful_orders
FROM pizza_runner.runner_orders
WHERE distance IS NOT NULL
GROUP BY runner_id;
````
![image](https://user-images.githubusercontent.com/104872221/227003593-18866403-ba42-4e46-97af-defe49439ef8.png)



### 4.How many of each type of pizza was delivered?

````sql
SELECT 
 pizza_name,
 COUNT(runner_orders.order_id) AS number_of_orders_delivered
FROM pizza_runner.customer_orders 
INNER JOIN pizza_runner.pizza_names
ON customer_orders.pizza_id = pizza_names.pizza_id
INNER JOIN pizza_runner.runner_orders
ON runner_orders.order_id = customer_orders.order_id
WHERE runner_orders.distance != 0
GROUP BY pizza_name;
````

### 5. How many Vegetarian and Meatlovers were ordered by each customer?**

````sql
SELECT 
 pizza_names.pizza_name,
 customer_orders.customer_id,
 COUNT(customer_orders.order_id) AS number_of_orders
FROM pizza_runner.pizza_names
INNER JOIN pizza_runner.customer_orders
ON pizza_names.pizza_id = customer_orders.pizza_id
GROUP by pizza_name, customer_id
ORDER BY customer_id, pizza_name;
````

![image](https://user-images.githubusercontent.com/104872221/227732283-eb194679-0bdc-4be2-8636-53f8c327768c.png)

### 6. What was the maximum number of pizzas delivered in a single order?

````sql
SELECT 
 customer_orders.order_id,
 COUNT(customer_orders.pizza_id) AS number_of_orders
FROM pizza_runner.customer_orders
INNER JOIN pizza_runner.runner_orders
ON runner_orders.order_id = customer_orders.order_id
WHERE runner_orders.distance  IS NOT NULL
GROUP BY customer_orders.order_id
ORDER BY number_of_orders DESC, order_id;
````
![image](https://user-images.githubusercontent.com/104872221/227737228-9ba30b4f-a64c-46ad-9aec-63b341547298.png)

### 7. For each customer, how many delivered pizzas had at least 1 change and how many had no changes?



