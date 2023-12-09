## **Problem 1:**

**A company database needs to store information about employees (identified by ssn, with salary and phone as attributes), departments (identified by dno, with dname and budget as attributes), and children of employees (with name and age as attributes).Employees work in departments; each department is managed by an employee; a child must be identified uniquely by name when the parent (who is an employee; assume that only one parent works for the company) is known. We are not interested in information about a child once the parent leaves the company.**

## **Solution**

**Entity:** The entities are Employee, Department and Children. Here children is a weak entity

**Attributes:** The attributes are SSN, Salary, Phone, Dno, Dname, Budget, Name and Age

**Relationships:** The relationships are Works in, Managed by and Has.


## ER Diagram:

![image](https://github.com/mvharsh/RDBMS/assets/111365320/1da144a0-07ce-4ae0-bba3-5dd86142012e)
