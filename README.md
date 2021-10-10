<h1> Relational Join </h1>

<h3> Background </h3>

In relational database systems, vast information is often divided and stored into multiple tables to achieve operational efficiencies. These tables are named relational tables as they have one-to-one or one-to-many relationships between them. A relational join is a command in Structured Query Language (SQL) to extract meaningful information. It combines multiple relational tables by column and returns a new output table with related rows. The column(s) used to combine these tables are called keys.



<h3> Aim of this Project </h3>

Goal is to:
1.  Introduce basic types of joins and provide examples of few tables manipulation with SQL queries. 
2.  Cover how to make connection with database through python which is the platform we are using to access relational tables.
3.  And will also introduce three tables join

For additional information, see our [Jupyter Notebook](https://github.com/mveele/SQL_join_comms/blob/main/comms_project.ipynb).

<h3> Index </h3>

[Structured Query Langauge (SQL)](#SQL)  </br>
[Types of Joins](#Joins)</br>
[Python Packages and Functions](#package)</br>
[Connection with database](#Python)</br>
[Tables Used and Creation](#tables)</br>
[Two Tables Join](#examples2)</br>
[Three Tables Join](#example3)</br>
[One-to-many and Many-to-Many Joins](#ex_otm_mtm)</br>
[Jupter Notebook](#Notebook_Link)</br>
[Practice Material](#practice_Link)</br>

<h3> Structured Query Langauge (SQL) </h3>
<a id="SQL"></a>

SQL (Structured Query Language) is a standardized programming language that's used to manage relational databases and perform various operations on the data in them.
The uses of SQL include modifying database table and index structures; adding, updating and deleting rows of data; and retrieving subsets of information from within a database.
ommonly used SQL statements include select, add, insert, update, delete, create, alter and truncate.

We are using here Postges SQL language.

General Syntax:

This query will select all rows from 'transactions' where values in column 'id' is 10.

```sql
SELECT * FROM transactions WHERE id = 10;
```

Join Syntax:

```sql
SELECT column_name(s)
FROM table1
JOIN table2 ON table1.column_name = table2.column_name;
```

<h2> Types of Joins </h2>

<a id="Joins"></a>

<h3> Inner Join </h3>

Returns records that have matching values in both tables

<img src="https://github.com/mveele/SQL_join_comms/blob/main/images/inner_join.png" alt="drawing" width="300"/>


```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2 ON table1.column_name = table2.column_name;
```

<br>

<h3> Left Join </h3>

Returns all records from the left table (table1)and the matched records from the right table (table2).The result is NULL from the right side, if there is no match.

<img src="https://github.com/mveele/SQL_join_comms/blob/main/images/left_join.png" alt="drawing" width="300"/>


```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2 ON table1.column_name = table2.column_name;
```

<br>

<h3> Right Join </h3>

The right Join is similar to left join except that it returns all records from the right table (table2), and the matched records from the left table (table1). The result is NULL from the left side, when there is no match.


<img src="https://github.com/mveele/SQL_join_comms/blob/main/images/right_join.png" alt="drawing" width="300"/>


```sql
SELECT column_name(s)
FROM table1
RIGHT JOIN table2 ON table1.column_name = table2.column_name;
```

<br>

<h3> Full Outer Join </h3>

Returns all records when there is a match in either left (table1) or right (table2) table records.

<img src="https://github.com/mveele/SQL_join_comms/blob/main/images/full_join.png" alt="drawing" width="300"/>


```sql
SELECT name, dust_costs.cost AS dust_cost
  FROM dust_costs
  FULL OUTER JOIN basic_cards on dust_costs.card_id = basic_cards.card_id;
```

<br>

<h2> Python Packages and Functions </h2>

<a id="package"></a>

In-Built Packages

1. <i><u> psycopg2 </u></i> - for making Python connection with database
2.<i><u>  pandas </u></i>- for manipulation 
3. <i><u>   numpy </u></i>- for basic operations
4. <i><u>  IPython.core.display </u></i>- for displaying table visuals in notebook

Created Functions
1. <i><u>  display_side_by_side</u></i> - for dsiplaying tables using html side by side.
2. <i><u>  hide_toggle</u></i> - for hiding few cells



<h2> Connection with database  </h2>

<a id="Python"></a>


A. Connect to database with host name, database name and user credentials and create a cursor

```python
conn = psycopg2.connect(host=host, port=port, database=database, user=user)
cur = conn.cursor()
```

B. Fetching table and storing as pandas dataframe

```python
df = pd.read_sql_query(query, conn, coerce_float=False)
```

C. Execution of a query using cursor 
```python
cur.execute(query) 
```

D. Close connection in the end
```python
cur.close()
conn.close() 
```



<h2> Tables Used and Creation </h2>

<a id="tables"></a>

Three tables are used in notebook named: names, transactions, dob 

<b> Table : Names </b>


	id	name
	1	Jon Smith
	2	Sarah Adams
	3	Maria Lopez     


<b> Table : Transactions </b>


	id	amount
	1	10
	3	20
	7	50


<b> Table : Dob </b>


	id	dob
	1	1982-09-29
	3	1996-02-1
    
    
    

<b> Example Syntax for Table Creation </b>

```sql
CREATE TABLE names
(id INTEGER,
name VARCHAR,
PRIMARY KEY (id));
```

```sql
INSERT INTO names
VALUES
(1, 'Jon Smith'),
(2, 'Sarah Adams'),
(3, 'Maria Lopez');
```


<h2> Two Tables Join  </h2>

<a id="examples2"></a>


<b> Inner join example </b>

Tables name and transactions are inner joined based on common column 'id' and columns from both tables: id, name, amount are fetched for all rows matched in both tables.

```sql
SELECT  
names.id, 
names.name, 
transactions.amount
FROM names 
INNER JOIN transactions
ON (names.id = transactions.id)
```

<b> Output Table </b>

<img src="https://github.com/mveele/SQL_join_comms/blob/surbhi33-patch-1/images/Inner.png" alt="drawing" width="300"/>
    

<b> Left join example </b>

Tables name and transactions are inner joined based on common column 'id' and columns from both tables: id, name, amount are fetched for all rows matched in both tables.

```sql
SELECT  
names.id, 
names.name, 
transactions.amount
FROM names 
LEFT JOIN transactions
ON (names.id = transactions.id)
```

<b> Output Table </b>

<img src="https://github.com/mveele/SQL_join_comms/blob/surbhi33-patch-1/images/Left.png" alt="drawing" width="300"/>


<h2> Three Tables Join  </h2>

<a id="example3"></a>


<b> Inner join example </b>

Tables name ,transactions and dob are inner joined based on common column 'id' and columns from all three tables tables: id, name, amount and dob are fetched for all rows matched in both tables.

```sql
SELECT  
names.id, 
names.name, 
transactions.amount, 
dob_table.dob
FROM names
INNER JOIN transactions
ON (names.id = transactions.id)
INNER JOIN dob_table
ON (names.id = dob_table.id)

```

<b> Output Table </b>

<img src="https://github.com/mveele/SQL_join_comms/blob/surbhi33-patch-1/images/Three.png" alt="drawing" width="300"/>

    
<h2> One-to-many and Many-to-Many Joins  </h2>

<a id="ex_otm_mtm"></a>

    

So far, we have seen one-to-one joins means there was no duplicate of ids in any of table (no two rows have same id). But in reality, there is possibility of an id having multiple records in a table. 

The query to do manipulation stays same but the output would change in which the rows will be returned as many times as ids are duplicated in the tables. 

Refer to below image for understanding.

<img src="https://github.com/mveele/SQL_join_comms/blob/surbhi33-patch-1/images/one_to_one.png" alt="drawing" 
width="600"/>
     
The only difference between one-to-many and many-to-many is that many-to-many has duplicate rows in both tables joined due to which the total rows in output table will have cartesian product of number of fuplicate rows in both tables.

<b> Example of One-to-Many </b> 

Table Transaction with duplicate ids.

<img src="https://github.com/mveele/SQL_join_comms/blob/surbhi33-patch-1/images/Long_trans.png" alt="drawing" width="250"/>

Output Table

<img src="https://github.com/mveele/SQL_join_comms/blob/surbhi33-patch-1/images/one2one_out.png" alt="drawing" width="200"/>

Here, id =1 duplicated two tables as transaction table had two rows with id=1.





<h2> Jupter Notebook  </h2>

<a id="Notebook_Link"></a>


For more info and examples using concrete data, please see our [Notebook](https://github.com/mveele/SQL_join_comms/blob/main/comms_project.ipynb).

It has one example each for all types of joins and also covers three tables join. It further gives example of one to many an many to one joins as well.

    
<h2> Practice Material  </h2>

<a id="practice_Link"></a>


For further practice, you can refer to:

A. [41 Essential SQL Questions](https://www.toptal.com/sql/interview-questions)

B. [SQL HackerRank Challenges](https://www.hackerrank.com/domains/sql)

