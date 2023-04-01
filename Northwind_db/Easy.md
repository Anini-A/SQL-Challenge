## Database: Northwing 

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
