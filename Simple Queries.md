## QUERIES AND OUTPUT:

**1) Retrieve all customer details who are not from London**
     
      SELECT * FROM customer WHERE NOT cust_city = 'London'

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/8dd406c8-91fb-44fc-b6cf-b013a1d5ae72)
 

**2) Get all the cities where the customers work (remove duplicate value)**
     
      SELECT DISTINCT cust_city FROM customer
 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/d0a7857e-40b2-4873-9d82-17b6668d7478)


**3) Rename all the customer names to ‘Harsh’ if their payment amount is 6000**

      UPDATE customer SET cust_name = 'Harsh' WHERE payment_amt = 6000

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/d0ca4c72-2869-44dc-b263-cdee526836c7)


**4) Get all the details of customer whose opening amount is between 4000 and 6000**

      SELECT * FROM customer WHERE opening_amt BETWEEN 4000 AND 6000

![image](https://github.com/mvharsh/RDBMS/assets/111365320/0a835a1a-234f-4c45-8eef-c01987cb4c7a)
 

**5) Get all the details of customer whose opening amount is 3000 or 5000**

      SELECT * FROM customer WHERE opening_amt IN (3000,5000)

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/74643cf7-908b-46c0-a594-749bba1ff372)


**6) Print all the details of agents in descending order of their names**

      SELECT * FROM agents ORDER BY agent_name DESC

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/96930bda-a439-4ff2-b69b-df3c32c40a3b)


**7) Get all the orders on 1 September 2023 and 15 April 2023**

      SELECT * FROM orders WHERE ord_date='08/01/2023' OR ord_date='04/15/2023'

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/7162062d-3b5d-4075-8c7a-c389730d222e)


**8) Print agent details of agents whose name starts with ‘Ra’**

      SELECT * FROM agents WHERE agent_name LIKE '%Ra%'

![image](https://github.com/mvharsh/RDBMS/assets/111365320/c504a991-f255-48d2-adf6-efbb8f3b1e89)
 

**9) Print working area of agents in uppercase**

      SELECT UPPER(working_area) FROM agents

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/89eeb266-6df5-495f-964a-14530e07f48c)



**10) Replace f by F and print order description details of orders**

      SELECT REPLACE(ord_description,'f','F') FROM orders

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/e429d948-7a4c-48b6-977e-0acf42766436)


**11) List all orders in recent 6 months**

      SELECT * from orders where ord_date >= add_months(sysdate,-6);

![image](https://github.com/mvharsh/RDBMS/assets/111365320/9a6deff8-a62e-4894-a76a-482739cf4d03)

 
## EXTRA QUERIES:

**1)  List all the orders which has the decimal value of order amount greater than 0.5**
      
      select * from orders where mod(ord_amount,1)>0.50

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/4bee0ca2-1639-4eb7-8a2d-a549e8d7d584)


**2) Orders placed in January**
      
      select * from orders where extract(month from ord_date) = 1

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/93819488-4cee-40be-9146-225bfbf4af52)


**3) List the customers whose phone numbers are not valid**
      
      select * from customer where not regexp_like (phone_no, '^[0-9]{10}$')

![image](https://github.com/mvharsh/RDBMS/assets/111365320/0d27190e-5d34-47ef-95b2-be38ed400d39)
