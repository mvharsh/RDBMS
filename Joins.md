## QUERIES AND OUTPUT:

**1) Retrieve all orders along with customer names and agent names**
      
      SELECT o.ord_num, c.cust_name, a.agent_name FROM orders o INNER JOIN customer c ON o.cust_code = c.cust_code INNER JOIN agents a ON o.agent_code = a.agent_code;

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/ef296fb7-8616-42da-a07e-36d518653ab8)


**2) Get all customers and their orders placed before Jan 2022**

      SELECT c.cust_name, o.ord_num, o.ord_date FROM customer c LEFT OUTER JOIN orders o ON c.cust_code = o.cust_code WHERE o.ord_date < '01-01-2022';

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/477a134f-45c9-4a8c-8035-cabc74830969)


**3) Find the total number of orders and total order amount for each customer along with their name and country**

      SELECT c.cust_name, c.cust_country, COUNT(o.ord_num) AS total_orders, SUM(o.ord_amount) AS total_order_amount FROM customer c JOIN orders o ON c.cust_code = o.cust_code GROUP BY c.cust_name, c.cust_country;

![image](https://github.com/mvharsh/RDBMS/assets/111365320/47d7bf7b-6f64-4e34-b2f9-066fa84e193f)
 

**4) Find the customer name who have placed atleast one order in each year between 2022 and 2023**

    SELECT c.cust_name FROM customer c JOIN orders o ON c.cust_code = o.cust_code WHERE o.ord_date BETWEEN '01-01-2020' AND '12-31-2023' GROUP BY c.cust_name HAVING COUNT(DISTINCT EXTRACT(YEAR FROM o.ord_date)) = 3;

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/ed622bad-9beb-4ec6-99f0-03daac4082d5)


**5) Retrieve agent name, customer name, order number and order date for all orders made by customers with a grade of 1 or 2**

    SELECT a.agent_name, c.cust_name, o.ord_num, o.ord_date FROM agents a JOIN customer c ON a.agent_code = c.agent_code JOIN orders o ON c.cust_code = o.cust_code WHERE c.grade IN (1, 2);

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/44822716-746c-4688-ad57-f9c1168bda8f)


**6) Get agent name and total outstanding amount of all orders made by customers in working area 'New York'**

    SELECT a.agent_name, SUM(c.outstanding_amt) as total_outstanding_amt FROM agents a JOIN customer c ON a.agent_code = c.agent_code JOIN orders o ON c.cust_code = o.cust_code WHERE c.working_area = 'New York' GROUP BY a.agent_name;

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/f395ba2b-cfcf-4284-bfed-78f3c4e4e6ce)


**7) Print customer name and their total outstanding amount for all orders made by customers who have not paid more than 50% of the order amount**

      SELECT c.cust_name, SUM(c.outstanding_amt) as total_outstanding_amt FROM customer c JOIN orders o ON c.cust_code = o.cust_code WHERE o.advance_amount < o.ord_amount * 0.5 GROUP BY c.cust_name;

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/6755e975-13cb-47bf-b7ae-081e3930761c)


**8) Find the agents whose code is not in customer table**

      SELECT a.agent_code, a.agent_name FROM agents a LEFT JOIN customer c ON a.agent_code = c.agent_code WHERE c.agent_code IS NULL;

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/31ff8a8e-772a-4c7d-8b80-12d24717d26e)



**9) Get agent name and sum of opening and receive amount of all customers working in 'London'**

      SELECT a.agent_name, SUM(c.opening_amt + c.receive_amt) as total_amt FROM agents a JOIN customer c ON a.agent_code = c.agent_code JOIN orders o ON c.cust_code = o.cust_code WHERE c.working_area = 'London' GROUP BY a.agent_name;

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/03d2b548-929b-4382-8858-a92fe6ba1d64)



**10) Find the agent names who have more than one orders under them**

      SELECT a.agent_name, COUNT(*) as COUNT FROM agents a JOIN orders o ON a.agent_code = o.agent_code GROUP BY a.agent_name HAVING COUNT(*) > 1;

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/5fbd6b82-2fe3-4bc3-84d2-648ca2cbb6af)



**11) Print all agents and customers with grade greater than 2**

      SELECT a.agent_name, c.cust_name, c.grade FROM agents a INNER JOIN customer c ON a.agent_code = c.agent_code WHERE c.grade > 2;

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/02d7b038-0f83-4209-924c-32e78745634a)


**12) Get all customers and agents working in India**

      SELECT c.cust_name, a.agent_name, a.country FROM customer c INNER JOIN agents a ON c.agent_code = a.agent_code WHERE a.country = 'India';
 
 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/7eaae577-26fb-4210-b540-69bfbf12c688)


**13) Print total commission of all agents in descending order**

      SELECT a.agent_name, SUM(o.ord_amount * a.commission / 100) AS total_commission FROM agents a JOIN orders o ON a.agent_code = o.agent_code GROUP BY a.agent_name ORDER BY total_commission DESC 

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/1272098e-2193-40d2-94ce-b6207f5078d6)




## EXTRA QUERIES:


**1) Show all the primary key in all the table by joining all the table in your Database**

      SELECT c.table_name, c.column_name
      FROM user_constraints pk
      JOIN user_cons_columns c
      ON pk.constraint_name = c.constraint_name
      WHERE pk.constraint_type = 'P'
      AND c.table_name IN ('AGENTS', 'CUSTOMER', 'ORDERS');

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/e8e7f889-dbd5-4516-86d5-45ba2de68790)


**2) Find the Union of Agent and Customer - remove duplicates**

      SELECT * FROM customer FULL OUTER JOIN agents ON customer.agent_code = agents.agent_code

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/473f148e-81d1-4026-b4b8-4278cf43b315)


**3) Find the Intersection of Order and Customer**

      SELECT * FROM customer INNER JOIN orders ON customer.cust_code = orders.cust_code

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/2899cee2-d9e7-433e-bdb1-f5e895127ace)


**4) Find all the customers whose customer code is not in the order table**

      SELECT c.cust_code FROM customer c LEFT JOIN orders o ON c.cust_code = o.cust_Code WHERE o.cust_code IS NULL

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/80afc00c-fff9-4fe0-be19-cabd69d9d621)


**5) Find the number of agent whose code is not in the order table**

      SELECT COUNT(*) FROM agents a LEFT JOIN orders o ON a.agent_code = o.agent_Code WHERE o.agent_Code IS NULL;

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/41908e9b-456b-4437-ae86-4a60d7f5a4e1)


