# SQL Solutions Repository

This repository contains solutions to various SQL questions, covering topics from **beginner** to **advanced** levels. Each solution is provided as a `.sql` file and is grouped by difficulty level. You can find questions on topics like data selection, aggregation, joins, subqueries, and more.

## SQL Questions
1.  [IMDB Rating](#imdb-rating)
2.  [IMDb Metacritic Rating](#imdb-metacritic-rating)
3.  [Students DB](#students-db)
4.   [IMDb Genre](#imdb-genre)


## Contents

- [Beginner](#beginner)
- [Intermediate](#intermediate)
- [Advanced](#advanced)

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

- [Question 2](./sql_solutions/intermediate/question2.sql): Write a query to find the average salary of employees grouped by department.

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


- [Question 2](./sql_solutions/advanced/question2.sql): Write a query to rank employees by their performance score using window functions.

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
