## Database: Northwind

<img width="1082" alt="Screenshot 2023-03-31 at 6 27 47 PM" src="https://user-images.githubusercontent.com/25376135/229258213-eda196d0-7d05-462a-ac43-5774d2b2573d.png">


### Difficulty level: Easy 🟢

#### Question 1

Show the category_name and description from the categories table sorted by category_name.

   ```
select
  category_name,
  description
from categories
  ```

#### Question 2

Show all the contact_name, address, city of all customers which are not from 'Germany', 'Mexico', 'Spain'

   ```
select
  contact_name,
  address,
  city
from customers
Where country NOT IN ('Germany', 'Mexico', 'Spain')
  ```
  
#### Question 3

Show order_date, shipped_date, customer_id, Freight of all orders placed on 2018 Feb 26

   ```
select
order_date,
shipped_date,
customer_id,
freight
from orders
where order_date = '2018-02-26'
  ```

#### Question 4

Show the employee_id, order_id, customer_id, required_date, shipped_date from all orders shipped later than the required date

  ```
select
  employee_id,
  order_id,
  customer_id,
  required_date,
  shipped_date
from orders
where shipped_date > required_date
  ```
  
#### Question 5

Show all the even numbered Order_id from the orders table

  ```
select order_id
from orders
where order_id % 2 = 0
  ```
  
#### Question 6

Show the city, company_name, contact_name of all customers from cities which contains the letter 'L' in the city name, sorted by contact_name

  ```
select
  city,
  company_name,
  contact_name
from customers
where city like '%L%'
order by contact_name asc
  ```
  
#### Question 7

Show the company_name, contact_name, fax number of all customers that has a fax number. (not null)

  ```
select
  company_name,
  contact_name,
  fax
from customers
where fax is not null
  ```
  
#### Question 8

Show the first_name, last_name of the most recently hired employee.

  ```
select
  first_name,
  last_name,
  max(hire_date)
from employees
  ```
  
#### Question 9

Show the average unit price rounded to 2 decimal places, the total units in stock, total discontinued products from the products table.

  ```
select
  ROUND(AVG(unit_price), 2) AS avg_unit_price,
  sum(units_in_stock) as total_stock,
  sum(discontinued) as total_discontinued
from products
  ```
