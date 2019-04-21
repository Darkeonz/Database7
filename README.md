# Database7

Exercise 1
Mention which violation there are to:

First normal form (if any)
Second normal form (if any)
Third normal form (if any)


![image](https://user-images.githubusercontent.com/40825848/54499266-0abd6700-4910-11e9-9e49-fdb4160a715c.png)


The table above have the following violations:
1.NF
The first NF might be violated by the customername column and the address column due to the fact that they contain more than one value (customername consists of both a first and a last name)

2.NF
(the table is not in NF1)
The second NF is violated in the following columns:
customerCity and customerZip and all the columns containing information about the rep 

3NF.
(the table is not in NF2)
This is the same problem as with NF2, there are several columns that are not solely dependent on the primary key. That means that atributes such as city and zipcode are dependent on each other but not on the primary key. The rules of normalizations in relational database states that the table must be split up in multiple tables.

Exercise 2
Assume we did not include the customerNumber in the table. What could be a key, and do we get the same violations of the normal forms?

If the business case dictates that only one customer per phonenumber is allowed, then the phonenumber could be used as a valid key. However it will be an issue as phonenumbers are recycled. Ontop of that you could be registeret through a company. Personally I prefer to just create an ID for an entity, as it is easier to work with.
 
The conclusion is that none of the columns - composites or otherwise can functions as a valid primary key. 
Without a primary key the table would therefore be violating the NF.1 and thereby all the rest of the NFs.

Exercise 3
Write a safe update statement that change the repPhone column from oldNumber (say 12345678) to newNumber (say 87654321).
  
    update CustomerOverview set repPhone = 87654321 where repPhone = 12345678

The ‘safe’ part of this update is the fact that the ‘where’-clause is used

Write an update of repEmail which do not update properly (do not update it everywhere it should)

    update CustomerOverview set repEmail = “new@email.address” where customerName = "Mini Wheels Co." and repName = "Leslie Jennings"

The ‘unsafe’ part of this update is the fact that both the repName and the customerName can change, this would lead to undesired updates. In other word it lacks the unique identification of the desired update. 

Exercise 4
In this exercise we will assume we have materialized this query into a table tblEx4Sydney.
Assume we have an index on customerName, and assume a fan-out in the B+ tree of 4.
Draw a representation of of the B+ tree with index and leaf nodes, as well as the actual table data. The drawing must be a combination of Figure 1.1 and 1.2 from Anatomy of an SQL index.

     with my_cust as
        (select customerNumber,
            customerName,
            customers.country as custCountry,
            offices.city      as repCity
         from employees
            inner join customers on employees.employeeNumber = customers.salesRepEmployeeNumber
            inner join offices on employees.officeCode = offices.officeCode)
     select *
     from my_cust
     where repCity = 'Sydney'

The query is as the table below

![image](https://user-images.githubusercontent.com/40825848/54499937-e9607900-4917-11e9-898a-9f6ea2077bff.png)

