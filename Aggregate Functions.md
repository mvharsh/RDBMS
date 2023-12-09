## QUERIES AND OUTPUT:

**1) Find average advance amount round up to 2 decimal places for all orders**

      SELECT round(avg(advance_amount),2) FROM orders

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/f33052ff-7484-41b5-a7ac-e0c76544f71b)


**2) Find the second maximum order amount for orders**

      SELECT max(ord_amount) from orders where ord_amount < (select max(ord_amount) from orders)

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/aad16a85-203e-40c6-b4e3-3accf160b40d)


**3) Find the outstanding amount for all customers**

      SELECT sum(outstanding_amt) FROM customer

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/c9240a2e-9cad-42ed-956a-61e4ffdc2dce)


**4) Find how many customers are there in each working area**

      SELECT count(cust_code), working_area FROM customer GROUP BY working_area

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/cb03297c-276e-4b88-b970-9ebdaf148fce)


**5) Find the minimum commission rate for all agents**

      SELECT min(commission) FROM agents

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/cc8c2f35-c5c6-4f68-97d3-4f49deaf94ca)


**6) Find which working areas have more than 2 customers and print how many customers are in each area**

      SELECT working_area, count(*) FROM customer GROUP BY working_area HAVING count(*)>2

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/0f473805-bd67-46fc-b9d9-eefe4d740e3e)


**7) Find is the third minimum commission rate for all agents**

      SELECT min(commission) from agents where commission>(SELECT min(commission) from agents where commission > (SELECT min(commission) from agents)) 

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/de467d52-d3ba-4323-af41-161eb85a2fe6)


**8) Find which working areas are there more than one agent and how many customers are in each area, sorted by the number of customers in ascending order**

      SELECT count(agent_Code), working_area from customer GROUP BY working_area HAVING count(agent_code)>1 ORDER BY count(agent_code) ASC

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/a7c01e90-099f-4849-bd21-8354c6a9b277)


**9) Find working areas with more than one agent with a commission rate greater than 0.13 and print them as “Working City”**

      SELECT working_area, count(*) as "Working City" from agents where commission>0.13 GROUP BY working_area HAVING count(*)>1

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/deeb634b-e125-468c-a275-03183376ce9c)


**10) Find sum of opening and receive amounts for each customer, sorted in descending order of their total amount**

      SELECT cust_code, sum(opening_amt + receive_amt) sum_total from customer GROUP BY cust_code ORDER BY sum_total DESC

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/e02bfebb-5722-42b0-9852-998406efb249)



## EXTRA QUERIES:

**1) Find the average order amount of each customer**

      SELECT cust_code, round(avg(ord_amount),2) as "AVERAGE" from orders group by cust_code
 
![image](https://github.com/mvharsh/RDBMS/assets/111365320/9aa74bce-19d0-4807-a552-214b56722b68)


**2) Find the agent where total orders are the minimum in 2023**

      SELECT agent_code from orders where extract(year from ord_date)=2023 having count(ord_num)=(select min(count(ord_num)) from orders group by agent_code) group by agent_code

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/ba9797da-fb22-4056-9df9-fb7a50bcb181)


**3) Find the count of customers under each agent**

      SELECT agent_code, count(cust_code) as "COUNT OF CUSTOMER" from customer group by agent_code

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/e4985e2a-fce8-4cc7-b6c0-bb41b4a4e9a1)


**4) Find the sum of orders placed in each year**

      SELECT extract(year from ord_date) as "YEAR" , sum(ord_amount) as "SUM OF ORDER AMT" from orders group by extract(year from ord_date)

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/e1134c7c-4cb5-4f36-a20a-9b1bcaf5dcf1)


**5) Find the agent containing minimum number of customers**

      SELECT agent_code from customer having count(cust_code)=(select min(count(cust_code)) from customer group by agent_code) group by agent_code

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/20f9bd2d-03e2-40cf-b2f2-cf38460ee8da)


