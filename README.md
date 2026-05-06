# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.


# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:

<img width="710" height="568" alt="image" src="https://github.com/user-attachments/assets/57d943e3-aa17-49c2-8748-5befe755c90d" />

### Entities and Attributes

| Entity       | Attributes (PK, FK)                                                                          | Notes                                                                                                  |
| ------------ | -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| Customer     | customer_id (PK), name, phone, email                                                         | Customers can make reservations or walk in.                                                            |
| Table        | table_id (PK), table_number, capacity, location                                              | Represents physical tables in the restaurant.                                                          |
| Reservation  | reservation_id (PK), date, time, num_guests, customer_id (FK), table_id (FK), waiter_id (FK) | Links customers, tables, and waiters. Walk-ins can also be stored as reservations with immediate time. |
| Waiter       | waiter_id (PK), name, phone                                                                  | Each waiter serves multiple reservations.                                                              |
| DishCategory | category_id (PK), category_name                                                              | Categories like Starter, Main, Dessert.                                                                |
| Dish         | dish_id (PK), name, price, category_id (FK)                                                  | Menu items belong to categories.                                                                       |
| Order        | order_id (PK), reservation_id (FK), order_time                                               | Orders are linked to reservations.                                                                     |
| OrderItem    | order_id (FK, PK), dish_id (FK, PK), quantity                                                | Junction table for many-to-many between Orders and Dishes.                                             |
| Bill         | bill_id (PK), reservation_id (FK), food_total, service_charge, grand_total, payment_status   | One bill per reservation.                                                                              |

### Relationships and Constraints

| Relationship                 | Cardinality | Participation                                   | Notes                                                                            |
| ---------------------------- | ----------- | ----------------------------------------------- | -------------------------------------------------------------------------------- |
| Customer – Reservation       | 1 : N       | Total (for reservation), Partial (for customer) | A customer can make many reservations; each reservation belongs to one customer. |
| Reservation – Table          | 1 : 1       | Total                                           | Each reservation is linked to exactly one table at a time.                       |
| Waiter – Reservation         | 1 : N       | Partial (waiter), Total (reservation)           | A waiter can serve many reservations; each reservation has exactly one waiter.   |
| Reservation – Order          | 1 : N       | Total                                           | Each reservation can have multiple orders.                                       |
| Order – Dish (via OrderItem) | M : N       | Total                                           | Each order can include multiple dishes; each dish can appear in many orders.     |
| DishCategory – Dish          | 1 : N       | Total                                           | Each dish belongs to one category.                                               |
| Reservation – Bill           | 1 : 1       | Total                                           | Each reservation generates exactly one bill.                                     |

### Assumptions

Walk-in customers are also recorded as reservations with immediate date/time.

A reservation is always tied to a single table (no table sharing in this model).

Bills include both food cost (sum of ordered dishes) and service charges.

A waiter must be assigned to every reservation.

Orders cannot exist without a reservation.

Payment status is tracked in the Bill entity (e.g., Paid / Pending).

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**

## Design Choices

In this restaurant reservation and ordering system, separate entities are created for Customer, Table, Reservation, Waiter, DishCategory, Dish, Order, OrderItem, and Bill to clearly define responsibilities, with OrderItem serving as a junction table to manage the many-to-many relationship between Orders and Dishes. The design is reservation-centric, meaning all business flows such as orders, billing, and waiter assignments are linked to a Reservation, while walk-in customers are also treated as reservations with the same-day date and time. A waiter is assigned at the reservation level, as service is tied to the entire table rather than individual dishes. Billing is generated per reservation instead of per order to simplify accounting, and totals such as food cost, service charge, and grand total are stored for performance. Dishes are categorized under DishCategory for easier menu organization and filtering. Each reservation is tied to one table, but for larger groups, the design can be extended with a junction table to allow multiple tables per reservation. Data integrity is ensured through foreign key constraints, and cascade deletes are avoided to preserve historical data. The model supports scalability by separating Orders and OrderItems, which allows handling complex orders and enables billing extensions like discounts or taxes. Finally, payment status is tracked in the Bill entity with simple states (e.g., Paid, Pending, Cancelled), though the design can be extended with a separate Payment entity for more advanced payment handling.

## RESULT

Hence, the concepts of ER modeling is understood and applied by creating an ER diagram for a real-world application.




