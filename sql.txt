NOTES
********
>the order in the sql syntax is very important if not followed it will give syntax error.
1.select
2.from
3.where
4.group by
5.having
6.order by
7.limit

>the AND operator has higher presidence than the OR operator.
>we use LAST_INSERT_ID() to get the position of the id which is the primary key.




select  where  order
**********************
USE STORE;

SELECT * FROM CUSTOMERS
WHERE LAST_NAME="Mynett"
ORDER BY CUSTOMER_ID;

and or
***********
USE STORE;



SELECT
******
SELECT * FROM CUSTOMERS
where birth_date >'1990-01-01' or points > 1000 and state='VA';

--ex2--
SELECT lastname,firstname,points,points+10*100 AS discount factor
FROM customers;

here we select lastname,firstname,points as well as it will calculate the points and the "AS" keyword will set the name of the column after discount as discount factor.


--ex3--
SELECT DISTINCT state 
FROM customer;

Here due to the DISTINCT keyword we will get a unique list of states that the customer belongs to from the customer table.  

IN-----it will find the values in the tables that matches the values the that are in the brackets.
****
USE STORE;

SELECT * FROM CUSTOMERS
where state in ('VA','FL','GA')  / where state='VA' OR state ='GA' OR state='FA'
;

between------it will find the data inbetween the given values.
**********
USE STORE;

SELECT * FROM CUSTOMERS
where birth_date between '1970-01-01' and '1999-01-01';

like-----it will get a specific values with the string put after like.
*****
we can use any no of string after like to find it.
1.'b%' -it will find the customers whose lastname start with b
2.'%b%'-it will find the customers whose lastname somewhere has b in it .
3.'%y' -it will find the customers whose lastname ends with y.
4.'_y' -it will find the customers whose lastname has y as their second letter.
5.'____y'-it will find the customers whose lastname has y as their 5th character. Like that we can use any no of dashes but only those positons of the character in the query that matches with the mata data will get displayed.
6.we can aslo use it like'b____y'.

USE STORE;

SELECT * FROM CUSTOMERS
where last_name like 'b%'
;

Regexp----
it uses some special character to find a value much like the 'like' operator.
'^field'-it will find the customer with the last name beginning with field.
'field$'-it means the lastname that ends with field. 
'field|mac|rose'-it will show the customer eho has field or mac in their last name.We use '|'(pipe) to represents multiple search paths.
'[gim]e'-it will find the customers with their last name having {'ge' or 'ie' or 'me'}.We can also write it as 
e[fmg] -where it will search customer having {'ef' or 'em' or 'eg'}their last name.   
'[a-h]e'-it will search any character with the range.
******
USE STORE;

SELECT * FROM CUSTOMERS
where last_name regexp 'y$'
;

is null----it returns the box in the row that is null.
*********
USE STORE;

SELECT * FROM CUSTOMERS
where phone is null
;

order by----here we are arrenging the data according to our need, we can even sort multiple column.WHILE USING 'ORDER BY' WE DO NOT USE 'AND'.
********
SELECT *
FROM customer
ORDER BY state DESC, first_name DESC;

-------OR------
SELECT first_name,last_name
FROM customer
ORDER BY birth_date;     ------>here it will sort the customer data by birth_date but it will display only the first_name and last_name with respect to the ordered birth_dates.

limit---- it will limit the data that is being displayed.
*******
USE STORE;

SELECT * FROM customers
limit 5
;

--------OR-------

SELECT * FROM customers
limit 5,3             ------->here the sql will skip the first 5 data and display the next 3 data.
;
inner join[explicite join syntax]---use to join tables in the same db.
************
USE STORE;

select order_id,o.customer_id,first_name,last_name
from orders o
inner join customers c
 on o.customer_id=c.customer_id;

joining across DB
*******************
USE STORE;

select * from store.order_items o
join sql_inventory.products p
on o.product_id=p.product_id;

self join--use to join columns in the same tables.
***********
use sql_hr;

select * from employees e
join employees m
on e.reports_to=m.employee_id;

compound join conditions-----we use it when there is no unique column to identify in a table.
****************************
use store;

select * from order_items oi
join order_item_notes oin
on oi.order_id=oin.order_id
and oi.product_id=oin.product_id;

explicit join syntax
***********************
select * from order o
join customers c
on o.customer_id=c.customer_id;

implicit join syntax---here we just use where clause instead of join,it is discouraged to use because in case if we forgot to mention the where clause then we will get a cross join i.e every data will join to every other data in the other table.	
********************
select * from orders o,customers c
where o.customer_id=c.customer_id;

outer joins-there are two kinds of outer joins.
1.left join-here it will display all the customer table i.e the left table weather they ordered or not.
2.right join-here it will display from the order table i.e the left table  weather they ordered or not.
************
select 
	c.customer_id,
	o.order_id
from orders o
left join customers c
on c.customer_id=o.customer_id
order by c.customer_id;


outer join with multiple tables
********************************
select 
	c.customer_id,
	o.order_id
from orders o
left join customers c
on c.customer_id=o.customer_id
left join shipper sh
on o.shipper_id=sh.shipper_id
order by c.customer_id;

self outer joins---it shows all the employees with and without manager to report to along with the manager.[this is the the way any outer join works]
********************
select * from employees e
left join employees m
on m.reports_to=e.employee_id;

using
******
if the column name is same accross the two connecting table we can replace the on clause and use the using clause.

select p.date,c.name as client,p.amount,m.name as payment_method
from clients c
join payments p
using (client_id)
join payment_methods m
on p.payment_method=m.payment_method_id;

natural joins[not recommended]
**************
it will join the db with the similar name columns in those tabeles.

select o.order_id
	c.first_name
from orders o
natural join customers c;

cross joins
***********
it will join each and every record with each of the other table records.

#cross joints using explicite syntax

select * from customers c
cross join products p;

***that's why it coes not have any conditions.***

#cross joints using implicite syntax

select * from shippers,products;

union
******
using union we can combine queries ,it can be from the same tabel or the different table.
_______________THE NO OF COLUMNS WACH QUERY RETURNS SHOULD BE EQUAL OTHERWISE SQL WILL GIVE ERROR_________________ 

select customer_id,first_name,points, 'GOLD' as type
from customers
where points>=3000
union
select customer_id,first_name,points, 'SILVER' as type
from customers
where points between 2000 and 3000
union
select customer_id,first_name,points, 'BRONZE' as type
from customers
where points<2000
order by first_name;


create a copy of a tabel
*************************

create table order_archive as
select * from orders;

inserting a specific data into the copied table [example for using a select statement as a subquery in an insert statement]
***************************************************************************
insert into order_archive
select * from orders
where order_date >'2019-01-01';


update
*******

update invoices
set payment_total=10, payment_date='2019-03-02'
where invoice_id=1;

avg
*****
round(avg(population))
to get the average of example population in a city we use the avg() and to round of that no we use the round().











IMPORTANT QUESTIONS
************************************************************************************************************************************************************************************
1.difference between order by and group by in sql
A GROUP BY statement sorts data by grouping it based on column(s) you 
specify in the query and is used with aggregate functions. 
An ORDER BY allows you to organize result sets alphabetically or numerically
and in ascending or descending order.