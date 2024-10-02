# SQL Solutions Repository

This repository contains solutions to various SQL questions, covering topics from **beginner** to **advanced** levels. Each solution is provided as a `.sql` file and is grouped by difficulty level. You can find questions on topics like data selection, aggregation, joins, subqueries, and more.

## SQL Questions
1.  [IMDB Rating](#imdb-rating)
2.  [IMDb Metacritic Rating](#imdb-metacritic-rating)
3.  [Students DB](#students-db)
4.  [IMDb Genre](#imdb-genre)
5.  [Sales Executive](#sales-executive)   
6.  [IMDb Max Weighted Rating](#imdb-max-weighted-rating)
7.  [Swap Salary](#swap-salary)
8.  [Second Highest Salary](#second-highest-salary)
9.  [Big Countriesy](#big-countries) 


## Contents

- [Beginner](#beginner)
- [Intermediate](#intermediate)
- [Advanced](#advanced)
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Beginner
Basic SQL questions covering topics like simple `SELECT` queries, `WHERE` clauses, `ORDER BY`, and basic aggregate functions.


###  IMDb Metacritic Rating
- [Question 1](./sql_solutions/beginner/question1.sql): Print the title and ratings of the movies released in 2012 whose metacritic rating is more than 60 and Domestic collections exceed 10 Crores.

```sql
select title, rating from imdb
join earning on earning.movie_id = imdb.movie_id
where title like '%2012%'
and metacritic > 60
and earning.domestic > 100000000;
```

### Students DB
  
- [Question 2](./sql_solutions/beginner/question2.sql): Insert below student details in students table and print all data of table.

| ID  |  Name       | Gender|
|---------|--------|-------|
|   3     |  Kim    |   F   |
|   4     | Molina  |   F   |
|   5     | Dev     |   M   |

```sql
insert into students(id, name, gender) 
values
(3, 'Kim', 'F'),
(4, 'Molina', 'F'),
(5, 'Dev', 'M');

select * from students;
```

### Sales Executive

- [Question 3](./sql_solutions/beginner/question3.sql):Given three tables: salesperson, company, orders.
Output all the names in the table salesperson, who didn’t have sales to company 'RED'.

Example

Input

Table: Salesperson

|sales_id | name | salary | commission_rate | hire_date |
|----------|------|--------|----------------|------------|
|   1      | John | 100000 |     6           | 4/1/2006  |
|   2      | Amy  | 120000 |     5           | 5/1/2010  |
|   3      | Mark | 65000  |     12          | 12/25/2008|
|   4      | Pam  | 25000  |     25          | 1/1/2005  |
|   5      | Alex | 50000  |     10          | 2/3/2007  |


The table salesperson holds the salesperson information. Every salesperson has a sales_id and a name.

Table: Company

| com_id  |  name  |    city    |
|---------|-------|-------------|
|   1     |  RED   |   Boston   |
|   2     | ORANGE |   New York |
|   3     | YELLOW |   Boston   |
|   4     | GREEN  |   Austin   |

The table company holds the company information. Every company has a com_id and a name.

Table: Orders

| order_id | order_date | com_id  | sales_id | amount |
|----------|------------|---------|----------|--------|
| 1        |   1/1/2014 |    3    |    4     | 100000 |
| 2        |   2/1/2014 |    4    |    5     | 5000   |
| 3        |   3/1/2014 |    1    |    1     | 50000  |
| 4        |   4/1/2014 |    1    |    4     | 25000  |

The table orders holds the sales record information, salesperson and customer company are represented by sales_id and com_id.

Output


| name | 
|------|
| Amy  | 
| Mark | 
| Alex |

```sql
SELECT name 
FROM Salesperson
WHERE sales_id NOT IN (
    SELECT sales_id 
    FROM Orders 
    WHERE com_id IN (
        SELECT com_id 
        FROM Company 
        WHERE name = 'RED'
    )
);
```
### IMDb Max Weighted Rating

- [Question 4](./sql_solutions/beginner/question4.sql): Print the genre and the maximum weighted rating among all the movies of that genre released in 2014 per genre. (Download the dataset from console)

Note:
1. Do not print any row where either genre or the weighted rating is empty/null.
2.  weighted_rating = avgerge of (rating + metacritic/10.0)
3. Keep the name of the columns as 'genre' and 'weighted_rating'
4. The genres should be printed in alphabetical order.

```sql
SELECT 
    genre.genre, 
    MAX((imdb.rating + imdb.metacritic / 10.0)/2) AS weighted_rating
FROM 
    genre
JOIN 
    imdb ON imdb.movie_id = genre.movie_id
WHERE 
    imdb.title like '%2014%'
    AND genre.genre IS NOT NULL
    AND imdb.rating IS NOT NULL
    AND imdb.metacritic IS NOT NULL
GROUP BY 
    genre.genre
ORDER BY 
    genre.genre ASC;
```

## Swap Salary

- [Question 5](./sql_solutions/beginner/question5.sql): Table: Salary


| Column Name | Type     |
|-------------|----------|
| id          | int      |
| name        | varchar  |
| sex         | ENUM     |
| salary      | int      |

id is the primary key for this table.
The sex column is ENUM value of type ('m', 'f').
The table contains information about an employee.

```sql
update salary

 set sex=case 

 when sex='m' 

 then 'f'

  else 'm'

  end;
```

## Big Countries
- [Question 6](./sql_solutions/intermediate/question6.sql): There is a table World


| name            | continent  | area       | population   | gdp         |
|-----------------|------------|------------|--------------|-------------|

| Afghanistan     | Asia       | 652230     | 25500100    |20343000  | 
| Albania         | Europe     | 28748      | 2831741     | 12960000  |
| Algeria         | Africa     | 2381741    | 37100000    | 188681000 |    
| Andorra         | Europe     | 468        | 78115       | 3712000   |
| Angola          | Africa     | 1246700    | 20609294    | 100990000 |    


A country is big if it has an area of bigger than 3 million square km or a population of more than 25 million.

Write a SQL solution to output big countries' name, population and area.

For example, according to the above table, we should output:


| name         | population  | area         |
|--------------|-------------|--------------|
| Afghanistan  | 25500100    | 652230       |
| Algeria      | 37100000    | 2381741      |

```sql
select name, population, area from world
where area > 300000
and population > 25000000;
```

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Intermediate
Intermediate-level SQL questions including `JOINs`, `GROUP BY`, `HAVING`, and more complex aggregates.


### IMDB Rating
- [Question 1](./sql_solutions/intermediate/question1.sql): From the IMDb dataset, print the title and rating of those movies which have a genre starting from 'C' released in 2014 with a budget higher than 4 Crore.

```sql
SELECT imdb.title, imdb.rating
FROM imdb
JOIN genre ON imdb.movie_id = genre.movie_id
WHERE genre.genre LIKE 'C%'
  AND imdb.title LIKE '%2014%'
  AND imdb.budget > 40000000;
```
## Second Highest Salary
- [Question 2](./sql_solutions/intermediate/question2.sql):Write a SQL query to get the second highest salary from the 
Employee table.


| Id | Salary |
-----|--------|
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |

For example, given the above Employee table, the query should return 200 as the second highest salary. If there is no second highest salary, then the query should return null.


| SecondHighestSalary |
|---------------------|
| 200                 |

```sql
select salary from Employee
order by salary desc
offset 1
limit 1;
```
-----------------------------------------------------------------------------------------------------------------------------------------
## Advanced
Advanced SQL questions covering `subqueries`, `window functions`, `CTEs`, and performance optimizations.

### IMDb Genre
- [Question 1](./sql_solutions/advanced/question1.sql):Print the genre and the maximum net profit among all the movies of that genre released in 2012 per genre.

Note:
1. Do not print any row where either genre or the net profit is empty/null.
2. net_profit = Domestic + Worldwide - Budget
3. Keep the name of the columns as 'genre' and 'net_profit'
4. The genres should be printed in alphabetical order.

```sql
select genre, max(earning.domestic + earning.worldwide - imdb.budget) as net_profit
from genre
join imdb on imdb.movie_id = genre.movie_id
join earning on earning.movie_id = genre.movie_id
where (earning.domestic + earning.worldwide - imdb.budget) is not null
and genre.genre is not null
and imdb.title like '%2012%'
group by genre.genre
order by genre.genre asc;
```


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Datasets

The datasets used for these SQL queries are provided in the [datasets](./datasets) directory. You can load them into your SQL environment to test the queries.

- `dataset1.csv`: Employee dataset
- `dataset2.csv`: Sales dataset

## How to Use

1. Clone the repository:

    ```bash
    https://github.com/its-sagar/SQLWizard.git
    ```

2. Navigate to the directory:

    ```bash
    cd SQLWizard/sql_solutions
    ```

3. Load the datasets in your SQL database and run the `.sql` files as queries.

## Contributing

Feel free to contribute your own SQL solutions or improve the existing ones. Here's how:

1. Fork the repository.
2. Create a new branch for your feature or fix.
3. Submit a pull request with a description of the changes.


## References
1. [Naukri.com](https://www.naukri.com/code360/problems/)

## License

This repository is licensed under the MIT License. See the [LICENSE](./LICENSE) file for more details.
