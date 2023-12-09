# QUERIES AND OUTPUT:


## 1. Write a database trigger before insert for each row on the customer table not allowing grades greater than 5 or less than 1.
    CREATE OR REPLACE TRIGGER customer_grade_trigger
    BEFORE INSERT ON customer
    FOR EACH ROW
    BEGIN
      IF :NEW.grade < 1 OR :NEW.grade > 5 THEN
        RAISE_APPLICATION_ERROR(-20002, 'Customer grade must be between 1 and 5.');
      ELSE
        dbms_output.put_line('Data inserted successfully');
      END IF;
    END;
    
    INSERT INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C13', 'Ajay', 'Delhi', 'Delhi', 'India', '6', '3000.00', '5000.00', '6000.00', '7000.00', '9793211543', 'A4') 

![image](https://github.com/mvharsh/RDBMS/assets/111365320/09b83779-6a3a-4a94-867a-d66c7df7d295)


    INSERT INTO customer(cust_code, cust_name, cust_city, working_area, cust_country, grade, opening_amt, receive_amt, payment_amt, outstanding_amt, phone_no, agent_code) VALUES ('C13', 'Ajay', 'Delhi', 'Delhi', 'India', '1', '3000.00', '5000.00', '6000.00', '7000.00', '9793211543', 'A4')	

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/1c210094-c5f8-4d50-89e2-9607b0429900)


## 2. Write a database trigger after insert for each row on the customer table for displaying a welcome message with the customer name.

      CREATE OR REPLACE TRIGGER welcome_message
      AFTER INSERT ON customer
      FOR EACH ROW
      DECLARE
          welcome_msg VARCHAR2(100);
      BEGIN
          welcome_msg := 'Welcome, ' || :NEW.cust_name || '!';
          DBMS_OUTPUT.PUT_LINE(welcome_msg);
      END;
      
      INSERT INTO customer VALUES ('C15', 'Harshini', 'Mumbai', 'Mumbai', 'India', '1', '3000.00', '5000.00', '6000.00', '7000.00', '9793211543', 'A4');

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/48e3b071-a232-484d-ae37-0efcb49296cf)
 

## 3. Write a database trigger before delete for each row on the Agent table not allowing deletion and giving message of invalid attempt of deletion.

      CREATE OR REPLACE TRIGGER prevent_agent_deletion
      BEFORE DELETE ON agents
      FOR EACH ROW
      BEGIN
          RAISE_APPLICATION_ERROR(-20001, 'Invalid attempt to delete a row from the agent table.');
      END;
      
      DELETE FROM agents WHERE agent_code = 'A7';

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/7d50d032-4387-4b4b-9515-3e0ceb46f004)


## 4. Write a database trigger after delete for each row giving the date and the time on which the delete is performed on the order table.

    INSERT INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100114', '4000.00', '800.00', '04/20/2023', 'C4', 'A4', 'Softdrinks')
    
    CREATE OR REPLACE TRIGGER order_updated
    AFTER DELETE ON orders
    FOR EACH ROW
    DECLARE
        update_time TIMESTAMP := SYSTIMESTAMP ;
    BEGIN
        DBMS_OUTPUT.PUT_LINE('The order was deleted on ' || update_time );
    END;
    
    
    DELETE FROM orders WHERE ord_num = 100114

![image](https://github.com/mvharsh/RDBMS/assets/111365320/64c5233a-4c6d-4bda-b1a9-89714d70f6a9)
 

## 5. Write a database trigger before update not allowing commission to be decreased

    CREATE OR REPLACE TRIGGER check_agent_commission
    BEFORE UPDATE ON agents
    FOR EACH ROW
    BEGIN
      IF :NEW.commission < :OLD.commission THEN
        RAISE_APPLICATION_ERROR(-20001, 'Commission cannot be decreased');
      END IF;
    END;
    
    SELECT * FROM agents

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/01529b29-a093-4733-bd4e-b4c8b35fa110)


    UPDATE agents SET commission = 0.10 WHERE agent_code = 'A8'

![image](https://github.com/mvharsh/RDBMS/assets/111365320/5f9389ac-5e85-4a41-9060-ae5d6759b620)
 

 	  UPDATE agents SET commission = 0.19 WHERE agent_code = 'A8'

![image](https://github.com/mvharsh/RDBMS/assets/111365320/7782699b-bb1b-4575-8a4b-4d8f8b6a0cf3)

![image](https://github.com/mvharsh/RDBMS/assets/111365320/ec069b37-0c61-447a-9c38-0ecfb691e751)

 
## 6. Write a database trigger after update for each row giving the date and the day on which the update is performed on the order table.

      CREATE OR REPLACE TRIGGER order_updated
      AFTER UPDATE ON orders
      FOR EACH ROW
      DECLARE
          update_date DATE := SYSDATE;
          update_day VARCHAR2(20) := TO_CHAR(update_date, 'Day');
      BEGIN
          DBMS_OUTPUT.PUT_LINE('The order was updated on ' || TO_CHAR(update_date, 'DD-MON-YYYY') || ' (' || update_day || ')');
      END;
      
      
      UPDATE orders
      SET ord_date = SYSDATE
      WHERE ord_num = 100113;

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/fe2fc7d2-a927-409d-b915-dbd909c5973d)


# EXTRA QUERIES:


## 1) Write trigger to deletes order details from order table, and creates a new table named deleted_orders, and inserts the deleted row into that table.

        INSERT INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100114', '1000.00', '600.00', '01/01/2020', 'C1', 'A1', 'Woolen Scarves')
        
        INSERT INTO orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description) VALUES('100115', '3000.00', '500.00', '04/04/2021', 'C2', 'A2', 'Masks')
        
        
        CREATE TABLE deleted_orders(
          ord_num INT PRIMARY KEY,
          ord_amount DECIMAL(12,2),
          advance_amount DECIMAL(12,2),
          ord_date DATE,
          cust_code VARCHAR(6) REFERENCES customer(cust_code),
          agent_code CHAR(6) REFERENCES agents(agent_code),
          ord_description VARCHAR(60)
        );
        
        
        CREATE OR REPLACE TRIGGER order_deleted
        BEFORE DELETE ON orders
        FOR EACH ROW
        BEGIN
            INSERT INTO deleted_orders(ord_num, ord_amount, advance_amount, ord_date, cust_code, agent_code, ord_description)
            VALUES(:OLD.ord_num, :OLD.ord_amount, :OLD.advance_amount, :OLD.ord_date, :OLD.cust_code, :OLD.agent_code, :OLD.ord_description);
        END;
        
        DELETE FROM orders WHERE ord_num IN (100114,100115)
        
        SELECT * FROM deleted_orders

 ![image](https://github.com/mvharsh/RDBMS/assets/111365320/1756f17d-74db-480d-8f26-e9fa2f38a1c1)

