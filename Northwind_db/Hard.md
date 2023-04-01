## Database: Northwind

<img width="1082" alt="Screenshot 2023-03-31 at 6 27 47 PM" src="https://user-images.githubusercontent.com/25376135/229258213-eda196d0-7d05-462a-ac43-5774d2b2573d.png">


### Difficulty level: Hard 🔴

#### Question

Show the employee's first_name and last_name, a "num_orders" column with a count of the orders taken, and a column called "Shipped" that displays "On Time" if the order shipped on time and "Late" if the order shipped late.

Order by employee last_name, then by first_name, and then descending by number of orders.

```
SELECT
  e.first_name,
  e.last_name,
  COUNT(o.order_id) As num_orders,
  (
    CASE
      WHEN o.shipped_date < o.required_date THEN 'On Time'
      ELSE 'Late'
    END
  ) AS shipped
FROM orders o
  JOIN employees e ON e.employee_id = o.employee_id
GROUP BY
  e.first_name,
  e.last_name,
  shipped
ORDER BY
  e.last_name,
  e.first_name,
  num_orders DESC
```
