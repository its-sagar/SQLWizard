# SQL Solutions Repository

This repository contains solutions to various SQL questions, covering topics from **beginner** to **advanced** levels. Each solution is provided as a `.sql` file and is grouped by difficulty level. You can find questions on topics like data selection, aggregation, joins, subqueries, and more.

## Contents

- [Beginner](#beginner)
- [Intermediate](#intermediate)
- [Advanced](#advanced)

## Beginner
Basic SQL questions covering topics like simple `SELECT` queries, `WHERE` clauses, `ORDER BY`, and basic aggregate functions.

- [Question 1](./sql_solutions/beginner/question1.sql): Write a query to select all records from the `employees` table.
- [Question 2](./sql_solutions/beginner/question2.sql): Write a query to find employees whose salary is above 5000.
  
## Intermediate
Intermediate-level SQL questions including `JOINs`, `GROUP BY`, `HAVING`, and more complex aggregates.

- [Question 1](./sql_solutions/intermediate/question1.sql): Write a query to find the total number of employees in each department.
- [Question 2](./sql_solutions/intermediate/question2.sql): Write a query to find the average salary of employees grouped by department.

## Advanced
Advanced SQL questions covering `subqueries`, `window functions`, `CTEs`, and performance optimizations.

- [Question 1](./sql_solutions/advanced/question1.sql): Write a query to find employees whose salary is in the top 10%.
- [Question 2](./sql_solutions/advanced/question2.sql): Write a query to rank employees by their performance score using window functions.

## Datasets

The datasets used for these SQL queries are provided in the [datasets](./datasets) directory. You can load them into your SQL environment to test the queries.

- `dataset1.csv`: Employee dataset
- `dataset2.csv`: Sales dataset

## How to Use

1. Clone the repository:

    ```bash
    git clone https://github.com/your-username/SQL-Solutions.git
    ```

2. Navigate to the directory:

    ```bash
    cd SQL-Solutions/sql_solutions
    ```

3. Load the datasets in your SQL database and run the `.sql` files as queries.

## Contributing

Feel free to contribute your own SQL solutions or improve the existing ones. Here's how:

1. Fork the repository.
2. Create a new branch for your feature or fix.
3. Submit a pull request with a description of the changes.

## License

This repository is licensed under the MIT License. See the [LICENSE](./LICENSE) file for more details.
