# Assignment

## Brief

Write the SQL statements for the following questions.

## Instructions

Paste the answer as SQL in the answer code section below each question.

### Question 1

Using the `claim` and `car` tables, write a SQL query to return a table containing `id, claim_date, travel_time, claim_amt` from `claim`, and `car_type, car_use` from `car`. Use an appropriate join based on the `car_id`.

Answer:

```sql
SELECT CLAIM.ID, CLAIM_DATE, TRAVEL_TIME, CLAIM_AMT, CAR_TYPE, CAR_USE FROM CLAIM 
INNER JOIN CAR ON CLAIM.CAR_ID = CAR.ID ;


```

### Question 2

Write a SQL query to compute the running total of the `travel_time` column for each `car_id` in the `claim` table. The resulting table should contain `id, car_id, travel_time, running_total`.

Answer:

```sql
SELECT ID, CAR_ID, TRAVEL_TIME, SUM(TRAVEL_TIME) OVER
 (PARTITION BY CAR_ID ORDER BY ID) AS RUNNING_TOTAL
FROM CLAIM;

```

### Question 3

Using a Common Table Expression (CTE), write a SQL query to return a table containing `id, resale_value, car_use` from `car`, where the car resale value is less than the average resale value for the car use.

Answer:

```sql
WITH AVG_RESALE_VALUE_CAR_USE AS (
SELECT 	CAR_USE,AVG(RESALE_VALUE) AS AVG_RESALE_VALUE
FROM CAR
GROUP BY CAR_USE )
SELECT ID, 	RESALE_VALUE, C1.CAR_USE
FROM CAR C1 INNER JOIN AVG_RESALE_VALUE_CAR_USE  C2 ON C1.CAR_USE = C2.CAR_USE
WHERE RESALE_VALUE < AVG_RESALE_VALUE;


```

## Submission

- Submit the URL of the GitHub Repository that contains your work to NTU black board.
- Should you reference the work of your classmate(s) or online resources, give them credit by adding either the name of your classmate or URL.
