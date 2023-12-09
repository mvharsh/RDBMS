## QUERIES AND OUTPUT:

**1) Print all orders whose orders amount is less than the average order amount**

      SELECT ord_num, ord_amount FROM orders where ord_amount  < (SELECT AVG (ord_amount) FROM orders)
 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/a7314f6e-4b9e-4de4-a04b-91a952dd682a)


**2) Print agent code, customer code and orders having least order amount**

      SELECT agent_code,cust_code, ord_amount, ord_num FROM orders WHERE ord_amount = (SELECT MIN (ord_amount) FROM orders);
 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/8a636ff8-5d23-4d30-9e57-349ee6b6a3e2)



**3) Find all customers whose advance amount is 600**

      SELECT cust_code, cust_name FROM customer WHERE cust_code IN (SELECT cust_code FROM orders WHERE advance_amount=600) 
 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/3bc37e63-f698-4ee8-a2ff-085f951d23c2)


**4) Find all the agent names whose customer grade is 2**

      SELECT agent_code, agent_name FROM agents WHERE agent_code IN (SELECT distinct agent_code FROM customer WHERE grade=2)
 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/a4df7b41-0237-467d-8c4b-edb2df42dae1)


**5) Print details of orders of customers whose payment amount is greater than 6500**

      SELECT * FROM orders WHERE cust_code IN (SELECT cust_code FROM customer WHERE payment_amt>6500);
 
![image](https://github.com/mvharsh/RDBMS/assets/111365320/899919cb-6cdb-41d3-ba21-ab14229b812e)


**6) Print all agents and their working area whose customers work in India**


      SELECT agent_code, agent_name, working_area FROM agents WHERE agent_code IN (SELECT agent_code FROM customer WHERE cust_country = 'India') 

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/ccdbf3ca-75ff-4fe9-89c4-7acaaac1fff4)



**7) Find all the agents who have the maximum commission**

      SELECT agent_code,agent_name, commission FROM agents WHERE commission = (SELECT MAX (commission) FROM agents);

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/ca4468a3-af86-4e0f-a3b4-c044c0918155)


**8) Find the agents containing minimum number of customers**

      SELECT agent_code from customer having count(cust_code)=(select min(count(cust_code)) from customer group by agent_code) group by agent_code 

![image](https://github.com/mvharsh/RDBMS/assets/111365320/4d7c4e93-8dfe-456a-ac70-3e426c387d27)
 

**9) Find the sum of opening amount paid by customer who placed their orders in January**

      SELECT sum(opening_amt) from customer WHERE cust_code IN (select cust_code from orders where extract(month from ord_date)=1)   

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/358c3d6b-2eb7-4900-bc25-f071171e1918)

**10) Find the orders placed under agent A1**

      SELECT ord_num from orders where agent_code IN (SELECT agent_code FROM agents WHERE agent_code = 'A1')  

![image](https://github.com/mvharsh/RDBMS/assets/111365320/98c2ca67-6446-473b-a6db-88d2c10cc437)

 
**11) Find the count of agents whose average advance amount is between 500 and 1000**

      SELECT count(avg(advance_amount)) from orders GROUP BY agent_code HAVING avg(advance_amount) BETWEEN 500 and 1000
 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/f30f9734-88c6-4488-bfa0-a40dcba8e6f7)


## EXTRA QUERIES:

**1) Find all the customer whose order amount is between 500 and 1000 – remove the duplicates**

      select cust_code, cust_name from customer where cust_code IN (select distinct cust_code from orders where ord_amount between 500 AND 1000)
![image](https://github.com/mvharsh/RDBMS/assets/111365320/0249a68d-b503-48bc-9037-7c03b8a5817a)
 

**2) Find the Agent code of the agent whose has customer in India – remove the duplicates**

      select agent_code from agents where agent_code IN (select distinct agent_code from customer where cust_country = 'India')
 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/792f608b-9327-46e3-878a-6ba19babeed2)


**3) Find Average commission of the agent who has placed order today**

      select avg(commission) from agents where agent_code IN (select agent_code from orders where ord_date = to_date(current_date))
 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/0aa877e3-06b6-4218-ad44-986e4d52ff68)


**4) Find sum of payment amount of the customer who ordered today**

      select sum(payment_amt) from customer where cust_code IN (select cust_code from orders where ord_date = to_date(current_date))
 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/132f79cf-26ec-46c1-bf06-da957874c162)


**5) Find the working area of agent whose average advance amount us between 100 to 1000**

      select working_area from agents where agent_code IN (select agent_code from orders group by agent_code having avg(advance_amount) between 100 and 1000)
 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/7dce3860-24b7-4c2b-a832-abe6d84326cd)

