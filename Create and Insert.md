	
# PROBLEM STATEMENT:
**Customer orders:**

![image](https://github.com/mvharsh/RDBMS/assets/111365320/d277ab8c-809a-4fa7-8a1b-f8880f374077)

 
# QUERIES AND OUTPUT:

## CREATING:

      CREATE TABLE agents(
        agent_code CHAR(6) PRIMARY KEY,
        agent_name CHAR(40),
        working_area CHAR(35),
        commission DECIMAL(10,2),
        phone_no CHAR(15),
        country VARCHAR(25)
        );

      DESCRIBE agents
![image](https://github.com/mvharsh/RDBMS/assets/111365320/5887100b-a834-4459-84c0-d06ff6966d61)

 
      CREATE TABLE customer(
        cust_code VARCHAR(6) PRIMARY KEY,
        cust_name VARCHAR(40),
        cust_city CHAR(35),
        working_area VARCHAR(20),
        cust_country VARCHAR(20),
        grade DECIMAL(2,0),
        opening_amt DECIMAL(12,2),
        receive_amt DECIMAL(12,2),
        payment_amt DECIMAL(12,2),
        outstanding_amt DECIMAL(12,2),
        phone_no VARCHAR(17),
        agent_code CHAR(6) REFERENCES agents(agent_code)
      );
      
      DESCRIBE customer

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/8b907024-40b9-4818-ae33-4ee48fd50d5f)





      CREATE TABLE orders(
        ord_num INT PRIMARY KEY,
        ord_amount DECIMAL(12,2),
        advance_amount DECIMAL(12,2),
        ord_date DATE,
        cust_code VARCHAR(6) REFERENCES customer(cust_code),
        agent_code CHAR(6) REFERENCES agents(agent_code),
        ord_description VARCHAR(60)
      );
      
      DESCRIBE orders
 
![image](https://github.com/mvharsh/RDBMS/assets/111365320/b4553215-8631-427e-b237-46b56a2b11fa)


## INSERTING:

      INSERT ALL
      
      INTO agents(agent_code, agent_name, working_area, commission, phone_no, country) VALUES ('A1', 'Ram', 'Bangalore', '0.15', '7725814763', 'India')
      
      INTO agents(agent_code, agent_name, working_area, commission, phone_no, country) VALUES ('A2', 'Sundar', 'Delhi', '0.13', '7512458969', 'India')
      
      INTO agents(agent_code, agent_name, working_area, commission, phone_no, country) VALUES ('A3', 'Harsh', 'Mumbai', '0.12', '8425874365', 'India')
      
      INTO agents(agent_code, agent_name, working_area, commission, phone_no, country) VALUES ('A4', 'Ramya', 'Hyderabad', '0.15', '9745625874', 'India')
      
      INTO agents(agent_code, agent_name, working_area, commission, phone_no, country) VALUES ('A5', 'Sweatha', 'Chennai', '0.14', '6722388644', 'India')
      
      INTO agents(agent_code, agent_name, working_area, commission, phone_no, country) VALUES ('A6', 'Sarah', 'Delhi', '0.12', ' 6725814763', 'India')
      
      INTO agents(agent_code, agent_name, working_area, commission, phone_no, country) VALUES ('A7', 'Ravi', 'Bangalore', '0.15', ' 8912458969', 'India')
      
      SELECT * FROM DUAL;
      
      SELECT * FROM agents

![image](https://github.com/mvharsh/RDBMS/assets/111365320/6b34a761-c4cb-4075-a25e-3d810b1b683d)

 

      INSERT ALL
      
      INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C1', 'Harish', 'London', 'London' ,'UK', '2', '6000.00', '5000.00', '7000.00', '4000.00', '8765432193', 'A1') 
      
      INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C2', 'Vivek', 'New York', 'New York', 'USA', '2', '3000.00', '5000.00', '2000.00', '6000.00', '9876535678', 'A2')
      INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C3', 'Keerthy', 'New York', 'New York', 'USA', '3', '5000.00', '7000.00', '6000.00', '6000.00', '9874683245', 'A3')
      
      INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C4', 'Naveena', 'Bangalore', 'Bangalore', 'India', '2','5000.00', '7000.00', '4000.00', '8000.00', '8312347532', 'A4')
      
      INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C5', 'Jessica', 'London', 'London', 'UK', '2', '4000.00', '9000.00', '7000.00', '6000.00', '6783214567', 'A5')
      
      INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C6', 'Kiara', 'London', 'London', 'UK', '3', '4000.00', '6000.00', '4000.00', '3000.00', '84654321931212', 'A1')
      
      INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C7', 'Sid', 'New York', 'New York', 'USA', '3', '2000.00', '4000.00', '1000.00', '5000.00', '76765#$5678', 'A2')
      
      INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C8', 'John', 'London', 'London', 'UK', '2', '6000.00', '5000.00', '7000.00', '4000.00', '968432193', 'A1')
      
      INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C9', 'Jay', 'Delhi', 'Delhi', 'India', '2', '3000.00', '5000.00', '2000.00', '6000.00', '9871212568', 'A2')
      
      INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C10', 'May', 'New York', 'New York', 'USA', '3', '5000.00', '7000.00', '3000.00', '6000.00', '8874683245', 'A3')
      
      INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C11', 'Smith', 'Bangalore', 'Bangalore', 'India', '2', '5000.00', '7000.00', '4000.00', '8000.00', '7312347532', 'A4')
      
      INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C12', 'Jordan', 'Delhi', 'Delhi', 'India', '3', '4000.00', '9000.00', '7000.00', '6000.00', '8783214567', 'A5')
      
      SELECT * FROM DUAL;
      
      
      SELECT * FROM customer

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/360e7103-d02c-4f51-9f94-e18434dffaa4)


      INSERT ALL
      
      INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100100', '1000.00', '600.00', '01/01/2020', 'C1', 'A1', 'Office furniture')
      
      INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100101', '3000.00', '500.00', '04/15/2021', 'C2', 'A2', 'Electronics accessories')
      
      INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100102', '4500.00', '900.00', '08/30/2021', 'C3', 'A3', 'Kitchen appliances')
      
      INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100103', '2000.00', '400.00', '01/30/2022', 'C4', 'A4', 'Clothing for Men')
      
      INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100104', '4000.00', '600.00', '06/10/2022', 'C5', 'A5', 'Shoes for Women')
      
      INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100105', '2000.25', '400.00', '01/20/2020', 'C6', 'A6', 'Sports equipment')
      
      INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100106', '4000.75', '700.00', '03/15/2021', 'C5', 'A5', 'Home decor')
      
      INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100107', '1000.00', '600.00', '08/01/2022', 'C1', 'A1', 'Pet supplies')
      
      INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100108', '3000.00', '500.00', '04/15/2023', 'C2', 'A2', 'Automotive parts')
      
      INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100109', '2000.00', '200.00', '08/01/2023', 'C1', 'A1', 'Books and magazines')
      
      INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100110', '1000.00', '500.00', '04/15/2023', 'C2', 'A2', 'Toys and games')
      
      INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100111', '7000.00', '600.00', '08/01/2023', 'C3', 'A3', 'Outdoor gear')
      INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100112', '4000.00', '800.00', '04/15/2023', 'C4', 'A4', 'Food and beverages')
      
      SELECT * FROM DUAL;
      
      SELECT * FROM orders

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/6c0269a3-4d2f-4769-8ab1-10a4c967f407)


