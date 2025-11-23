# 10.sql

-- Day 10/30 SQL Interview Question - Medium


create table transactions (
   id int primary key,
   country varchar (50),
   state varchar(45),
   amount int,
   transaction_date date
)

-- now ab hum apne table me data fill karenege 

INSERT INTO transactions (id, country, state, amount, transaction_date)
VALUES
(1, 'USA', 'California', 5200, '2024-01-04'),
(2, 'USA', 'Texas', 3100, '2024-01-12'),
(3, 'India', 'Maharashtra', 1800, '2024-01-18'),
(4, 'India', 'Delhi', 2400, '2024-01-25'),
(5, 'UK', 'London', 6500, '2024-02-03'),
(6, 'Germany', 'Berlin', 4300, '2024-02-10'),
(7, 'India', 'Karnataka', 2100, '2024-02-14'),
(8, 'Canada', 'Ontario', 3700, '2024-02-18'),
(9, 'USA', 'New York', 5900, '2024-02-25'),
(10, 'Australia', 'Sydney', 4800, '2024-03-02'),

(11, 'India', 'Tamil Nadu', 1600, '2024-03-07'),
(12, 'UAE', 'Dubai', 7200, '2024-03-14'),
(13, 'Japan', 'Tokyo', 5400, '2024-03-18'),
(14, 'Canada', 'Quebec', 2900, '2024-04-01'),
(15, 'USA', 'Florida', 3300, '2024-04-04'),
(16, 'India', 'Gujarat', 2500, '2024-04-09'),
(17, 'UK', 'Manchester', 4100, '2024-04-16'),
(18, 'Germany', 'Hamburg', 4700, '2024-04-20'),
(19, 'India', 'Rajasthan', 1400, '2024-05-01'),
(20, 'USA', 'Washington', 6200, '2024-05-05'),

(21, 'Canada', 'British Columbia', 3600, '2024-05-09'),
(22, 'Australia', 'Melbourne', 5100, '2024-05-18'),
(23, 'India', 'Punjab', 1900, '2024-05-21'),
(24, 'Japan', 'Osaka', 5800, '2024-06-01'),
(25, 'UAE', 'Abu Dhabi', 6900, '2024-06-05');


select * from transactions

UPDATE transactions SET state = 'approved' WHERE id = 1;
UPDATE transactions SET state = 'declined' WHERE id = 2;
UPDATE transactions SET state = 'approved' WHERE id = 3;
UPDATE transactions SET state = 'declined' WHERE id = 4;
UPDATE transactions SET state = 'approved' WHERE id = 5;

UPDATE transactions SET state = 'declined' WHERE id = 6;
UPDATE transactions SET state = 'approved' WHERE id = 7;
UPDATE transactions SET state = 'declined' WHERE id = 8;
UPDATE transactions SET state = 'approved' WHERE id = 9;
UPDATE transactions SET state = 'declined' WHERE id = 10;

UPDATE transactions SET state = 'approved' WHERE id = 11;
UPDATE transactions SET state = 'declined' WHERE id = 12;
UPDATE transactions SET state = 'approved' WHERE id = 13;
UPDATE transactions SET state = 'declined' WHERE id = 14;
UPDATE transactions SET state = 'approved' WHERE id = 15;

UPDATE transactions SET state = 'declined' WHERE id = 16;
UPDATE transactions SET state = 'approved' WHERE id = 17;
UPDATE transactions SET state = 'declined' WHERE id = 18;
UPDATE transactions SET state = 'approved' WHERE id = 19;
UPDATE transactions SET state = 'declined' WHERE id = 20;

UPDATE transactions SET state = 'approved' WHERE id = 21;
UPDATE transactions SET state = 'declined' WHERE id = 22;
UPDATE transactions SET state = 'approved' WHERE id = 23;
UPDATE transactions SET state = 'declined' WHERE id = 24;
UPDATE transactions SET state = 'approved' WHERE id = 25;

select * from transactions

/*
Write an SQL query to find for each month and country, 
the number of transactions and their total amount, 
the number of approved transactions and their total amount.

*/

Output: 
+----------+---------+-------------+----------------+--------------------+-----------------------+
| month    | country | trans_count | approved_count | trans_total_amount | approved_total_amount |
+----------+---------+-------------+----------------+--------------------+-----------------------+
| 2018-12  | US      | 2           | 1              | 3000               | 1000                  |
| 2019-01  | US      | 1           | 1              | 2000               | 2000                  |
| 2019-01  | DE      | 1           | 1              | 2000               | 2000                  |
+----------+---------+-------------+----------------+--------------------+-----------------------+
*/

solution - -- first we create month column from trans_date yyyy-mm format using to_char

select 
      to_CHAR(transaction_date, 'YYYY-mm') as month,
	  country,
	  count(1) as trans_count,
	  sum(case when state = 'approved' then 1 else 0 end) as approved_count,
	  sum(amount) as trans_totalamount,
	  sum(case when state = 'approved' then amount else 0 end) as approved_total_amount
from transactions
group by 1,2;
