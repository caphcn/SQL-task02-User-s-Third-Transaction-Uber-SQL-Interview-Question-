# Task2: User's Third Transaction [Uber SQL Interview Question]
## Assume you are given the table below on Uber transactions made by users. Write a query to obtain the third transaction of every user. Output the user id, spend and transaction date.
transactions **Table:**

|**Column Name**|**Type**|
|-|-|
|user_id|integer|
|spend|decimal|
|transaction_date|timestamp|

transactions **Example Input:**

|user_id|spend|transaction_date|
|-|-|-|
|111|100.50|01/08/2022 12:00:00|
|111|55.00|01/10/2022 12:00:00|
|121|36.00|01/18/2022 12:00:00|
|145|24.99|01/26/2022 12:00:00|
|111|89.60|02/05/2022 12:00:00|

# My Solution
***
```
SELECT user_id, spend, transaction_date
FROM
  (SELECT
    user_id,
    spend,
    transaction_date,
    row_number()OVER(PARTITION BY user_id ORDER BY transaction_date) AS rownum
  FROM
    transactions) AS new_table
WHERE rownum = 3
```
# Result
***
|user_id|spend|transaction_date
|-|-|-|
|111|89.60|02/05/2022 12:00:00|
|121|67.90|04/03/2022 12:00:00|
|263|100.00|07/12/2022 12:00:00|
