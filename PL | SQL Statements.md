# QUERIES AND OUTPUT:

      CREATE TABLE SALESMEN
      (
       SID VARCHAR2 (5) PRIMARY KEY,	 
       SNAME VARCHAR2 (20),	  
       CITY VARCHAR2 (15), 	    
       SALARY NUMBER (8, 2),	       
       TARGET NUMBER (10, 2),	
       SALES NUMBER (10, 2),       	    		   
       COMM NUMBER (5, 2)
      );
      
      INSERT ALL
      INTO SALESMEN (SID, SNAME, CITY, SALARY, TARGET, SALES, COMM) VALUES ('101','Harsh','Mumbai','200000','250000','300000','0.15')
      INTO SALESMEN (SID, SNAME, CITY, SALARY, TARGET, SALES, COMM) VALUES ('102','Harish','Chennai','100000','150000','200000','0.13')
      INTO SALESMEN (SID, SNAME, CITY, SALARY, TARGET, SALES, COMM) VALUES ('103','Jesse','Bangalore','70000','90000','100000','0.14')
      INTO SALESMEN (SID, SNAME, CITY, SALARY, TARGET, SALES, COMM) VALUES ('104','Ramya','Hyderabad','80000','100000','70000','0.12')
      INTO SALESMEN (SID, SNAME, CITY, SALARY, TARGET, SALES, COMM) VALUES ('105','Girish','Coimbatore','150000','200000','100000','0.17')
      SELECT * FROM DUAL;
      
      SELECT * FROM SALESMEN

**OUTPUT:**

![image](https://github.com/mvharsh/RDBMS/assets/111365320/db8c131d-f895-432c-bba6-12077300b982)


 
 
## 1. Write a  PL/SQL function to calculate the sum of digits of an integer.

      CREATE OR REPLACE PROCEDURE sum_digits(id IN salesmen.sid%TYPE)
      IS
          total_digits NUMBER := 0;
          s_salary salesmen.salary%TYPE;
      BEGIN
          SELECT salary INTO s_salary FROM salesmen WHERE sid = id;
          FOR i IN 1..LENGTH(s_salary)
          LOOP
              total_digits := total_digits + TO_NUMBER(SUBSTR(s_salary, i, 1));
          END LOOP;
          DBMS_OUTPUT.PUT_LINE('The sum of digits in the salary of salesman ' || id || ' is: ' || total_digits);
      END;
      
      DECLARE
       id VARCHAR2(5);
      BEGIN 
       id := :id;
       sum_digits(id);
      END;

**OUTPUT:**
![image](https://github.com/mvharsh/RDBMS/assets/111365320/b64551e6-8cd0-49d8-8745-2018caf26919)

 
 ## 2. Write s PL/SQL function to find whether an input string is palindrome or not.
 
        CREATE OR REPLACE PROCEDURE palindrome(id IN salesmen.sid%TYPE)
        IS
            total_digits NUMBER := 0;
            name1 salesmen.sname%TYPE;
            name2 salesmen.sname%TYPE;
            name3 salesmen.sname%TYPE;
        BEGIN
            SELECT sname INTO name1 FROM salesmen WHERE sid = id;
            FOR i IN REVERSE 1..LENGTH(name1) LOOP 
                name2 := substr(name1, i, 1); 
                name3 := name3 || name2; 
            END LOOP; 
            IF (name1 = name3) THEN 
              dbms_output.put_line(name1 ||' is palindrome'); 
            ELSE 
              dbms_output.put_line(name1 ||' is not palindrome'); 
            END IF; 
        END;
        
        DECLARE
         id VARCHAR2(5);
        BEGIN 
         id := :id;
         palindrome(id);
        END;

**OUTPUT:**

![image](https://github.com/mvharsh/RDBMS/assets/111365320/7d049b00-11f1-48e8-856a-839f487ea227)



## 3. Write s PL/SQL procedure to increase the salesman salary by 10% of the monthly sales.

      DECLARE  
         total_rows number(2); 
      BEGIN 
         UPDATE salesmen 
         SET salary = salary + 0.1*sales; 
         IF sql%notfound THEN 
            dbms_output.put_line('No Salesman Selected'); 
         ELSIF sql%found THEN 
            total_rows := sql%rowcount;
            dbms_output.put_line( total_rows || ' salary selected '); 
         END IF;  
      END;
      
![image](https://github.com/mvharsh/RDBMS/assets/111365320/ab518a4d-788b-4ca8-a68f-c5143fb150ba)

      
      SELECT * FROM SALESMEN

![image](https://github.com/mvharsh/RDBMS/assets/111365320/93353993-a763-407b-83f3-cb04fdf11e3a)

 

## 4. Write a PL/SQL block to display the total salary (.Salary + Commission) of each employee if total salary exceeds 25,000.

      DECLARE
        total_salary NUMBER(8,2);
      BEGIN
        FOR emp IN (SELECT * FROM SALESMEN)
        LOOP
          total_salary := emp.SALARY + (emp.SALES * emp.COMM);
          IF total_salary > 25000 THEN
            DBMS_OUTPUT.PUT_LINE('Employee ' || emp.SID || ': Total Salary = ' || total_salary);
          END IF;
        END LOOP;
      END;

**OUTPUT:**
![image](https://github.com/mvharsh/RDBMS/assets/111365320/8482ddee-e479-4502-a2f8-756c36393012)

 

## 5. Write a PL/SQL block which has a procedure get_salesman_details which accepts a salesman number and returns the salesman name and salary. The main block must get any salesman id as input and pass the id to the procedure and display the returned result.
      DECLARE
       s_name VARCHAR2(20);
       s_salary NUMBER(8, 2);
       s_id VARCHAR2(5) ;
      BEGIN
       s_id:= :s_id;
       SELECT SNAME, SALARY INTO s_name,s_salary
       FROM salesmen
       WHERE SID= s_id;
       DBMS_OUTPUT.PUT_LINE('Name: '||s_name);
       DBMS_OUTPUT.PUT_LINE('Salary: '||s_salary);
      END;

**OUTPUT:**
![image](https://github.com/mvharsh/RDBMS/assets/111365320/c1239537-9d04-4efe-a13b-26e5dcb7d63a)

 

# EXTRA QUERIES:


## 1) Get year as input from user. Print customer name and agent name of those who placed orders in that particular year. Also print sum of order amount for each.

      DECLARE
         input_year NUMBER;
         total_order_amount NUMBER;
      BEGIN
         input_year := :year;
         DBMS_OUTPUT.PUT_LINE('CUST_NAME     AGENT_NAME     TOTAL_ORDER_AMOUNT');
      
         FOR c IN (SELECT DISTINCT customer.cust_name, agents.agent_name FROM orders
                   JOIN customer ON orders.cust_code = customer.cust_code
                   JOIN agents ON orders.agent_code = agents.agent_code
                   WHERE EXTRACT(YEAR FROM ord_date) = input_year)
         LOOP
            DBMS_OUTPUT.PUT(RPAD(c.cust_name, 13) || '  ' || LPAD(c.agent_name, 13));
      
            SELECT SUM(ord_amount) INTO total_order_amount FROM orders
            WHERE cust_code = (SELECT cust_code FROM customer WHERE cust_name = c.cust_name)
            AND agent_code = (SELECT agent_code FROM agents WHERE agent_name = c.agent_name)
            AND EXTRACT(YEAR FROM ord_date) = input_year;
      
            DBMS_OUTPUT.PUT_LINE('  ' || total_order_amount);
         END LOOP;
      END;

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/4cfaaa86-6d3e-4710-b541-21117726a083)

