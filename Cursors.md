# QUERIES AND OUTPUT:


## 1. Write a PL/SQL block using cursor to get all agents and their working area whose customers work in India

      DECLARE
         cursor cur is 
            select * from agents 
            where agent_code IN (select agent_code from customer where cust_country = 'India');
      BEGIN
         FOR agents in cur LOOP
            dbms_output.put_line('Agent Code : '||agents.agent_code||'Working Area : '||agents.working_area);
         end loop;
      END;
      
![image](https://github.com/mvharsh/RDBMS/assets/111365320/cf420764-e70b-4efa-9487-39ed082f897a)

## 2. Write a PL/SQL block using cursor to get all agents who have maximum commission

      DECLARE
         cursor cur is 
            select * from agents 
            where commission = (select max(commission) from agents);
      BEGIN
          FOR agents in cur LOOP
             dbms_output.put_line('Agent Code : '||agents.agent_code||' Agent Name : '||LPAD(agents.agent_name,10)||'Commission : '||agents.commission);
          end loop;
      END;

![image](https://github.com/mvharsh/RDBMS/assets/111365320/cd69f240-2643-4368-83f7-0981c22f695b)
      

## 3. Write a PL/SQL block using cursor to get all orders whose order amount is less than average order amount

      DECLARE
         cursor cur is 
            select * from orders 
            where ord_amount < (select avg(ord_amount) from orders);
      BEGIN
        FOR orders in cur LOOP
         dbms_output.put_line('Order Id : '||orders.ord_num||'   Order amount : '||orders.ord_amount);
          end loop;
      END;
![image](https://github.com/mvharsh/RDBMS/assets/111365320/b437b712-4bde-403b-afbf-aef2cdbf1ab9)



## 4. Write a PL/SQL block to get an agent code and display the details of customers under that agent

      CREATE OR REPLACE PROCEDURE cust_under_agent(id IN customer.agent_code%TYPE)
      IS
         cursor cur is 
            select * from customer
            where customer.agent_code = id;
      BEGIN
          for customer in cur loop
             dbms_output.put_line('Customer Id : '||customer.cust_code||'   Customer Name : '||customer.cust_name);
          end loop;
      END;
      
      DECLARE
       agent_id VARCHAR2(5);
      BEGIN 
       agent_id := :agent_id;
       cust_under_agent(agent_id);
      END;

![image](https://github.com/mvharsh/RDBMS/assets/111365320/912ab762-e61b-4407-af5f-d119da90f108)

 
## 5. Write PL/SQL block with cursor to increase the payment amount of customers by 10% 

      declare
         n integer;
         cursor cur is 
            select * from customer 
            for update;
      begin
          for customer in cur loop
             n:= customer.payment_amt;
             update customer
             set payment_amt = payment_amt + (n *(10/100));
          end loop;
      end;
      
      select * from customer

![image](https://github.com/mvharsh/RDBMS/assets/111365320/39ea40f4-724e-43eb-8ace-77272675fd1f)
 

## 6. Write PL/SQL block using cursor fetch to display the customers with valid phone no

      declare
         cursor cur is 
            select * from customer 
            where regexp_like(phone_no,'^[a-zA-Z0-9]{10}*$');
      begin
          for customer in cur loop
             dbms_output.put_line('Customer Id : '||RPAD(customer.cust_code,4)||'   Customer Name : '||RPAD(customer.cust_name,10)||'   Phone no : '||customer.phone_no);
          end loop;
      end;

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/d7ff3709-a401-4597-a173-86c3ced469fe)


## 7. Write PL/SQL block with Cursor to display the orders placed in May

      declare
         cursor cur is 
            select * from orders 
            where extract(month from ord_date) = 4;
      begin
          for orders in cur loop
             dbms_output.put_line('Order Id : '||orders.ord_num||'   Order Date : '||orders.ord_date);
          end loop;
      end;

![image](https://github.com/mvharsh/RDBMS/assets/111365320/29c677d0-6305-4a0a-ae05-1b24123c0b66)

 
# EXTRA QUERIES:


## 1) Get agent code as input from user, and delete agent details of that agent from that table

      CREATE OR REPLACE PROCEDURE delete_agent_code(id IN agents.agent_code%TYPE)
      IS
         cursor cur is 
            select * from agents
            where agents.agent_code = id;
      BEGIN
          for customer in cur loop
          DELETE FROM agents WHERE agent_code = id;  
             dbms_output.put_line('Data Deleted');
          end loop;
      END;
      
      DECLARE
       agent_id CHAR(6);
      BEGIN 
       agent_id := :agent_id;
       delete_agent_code(agent_id);
      END;


**Before deleting:**

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/e40ab13e-e2b1-4209-b51f-38b7c81503cb)


**After deleting A9:**

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/a7551b81-632c-43db-8114-acdcbb71a08a)

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/18853980-03ed-4baa-88cb-29da223e5757)




