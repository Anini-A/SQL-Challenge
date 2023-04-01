## Database: Northwind

<img width="1082" alt="Screenshot 2023-03-31 at 6 27 47 PM" src="https://user-images.githubusercontent.com/25376135/229258213-eda196d0-7d05-462a-ac43-5774d2b2573d.png">


### Difficulty level: Medium 🟡

#### Question 1

Show the ProductName, CompanyName, CategoryName from the products, suppliers, and categories table

```
select
  product_name,
  company_name,
  category_name
from products
  join suppliers on products.supplier_id = suppliers.supplier_id
  join categories on products.category_id = categories.category_id
```

#### Question 2

Show the category_name and the average product unit price for each category rounded to 2 decimal places.

```
select
  category_name,
  round(avg(unit_price), 2) as avg_unit_price
from categories
  join products on categories.category_id = products.category_id
group by category_name
```

#### Question 3

Show the city, company_name, contact_name from the customers and suppliers table merged together.
Create a column which contains 'customers' or 'suppliers' depending on the table it came from.

```
select
  city,
  company_name,
  contact_name,
  'customers' AS relationship
from customers
union
SELECT
  city,
  company_name,
  contact_name,
  'suppliers' AS suppliers
FROM suppliers
```
