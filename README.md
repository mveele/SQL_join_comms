<h1> Relational Joins </h1>

<h3> Background </h3>

In relational database systems, vast information is often divided and stored into multiple tables to achieve operational efficiencies. These tables are named relational tables as they have one-to-one or one-to-many relationships between them. A relational join is a command in Structured Query Language (SQL) to extract meaningful information. It combines multiple relational tables by column and returns a new output table with related rows. The column(s) used to combine these tables are called keys.

The information extracted is dependent on the type of relational join used. SQL provides four different types of joins named inner, full outer, left, and right outer join that can handle all possible forms of retrieval. Each type filters data that does or doesn’t match on keys differently. 



<h3> Objective </h3>

The goal is to:
1.  Introduce basic types of joins and provide examples of a few tables manipulation with SQL queries. 
2.  Cover how to make a connection with the database through Python which is the platform we are using to access relational tables.
3.  Introduce three tables join
4.  Discuss the difference in results of the one-to-many and many-to-many types of joins.

For additional information, see our [Jupyter Notebook](https://github.com/mveele/SQL_join_comms/blob/main/comms_project.ipynb).

<h3> Index </h3>

1. [Structured Query Langauge (SQL)](#SQL)  </br>

2. [Types of Joins](#Joins)</br>

3. [Python Packages and Functions](#package)</br>

4. [Connection with database](#Python)</br>

5. [Tables Used and Creation](#tables)</br>

6. [Two Tables Join](#examples2)</br>

7. [Three Tables Join](#example3)</br>

8. [One-to-many and Many-to-Many Joins](#ex_otm_mtm)</br>

9. [Jupyter Notebook](#Notebook_Link)</br>

10. [Practice Material](#practice_Link)</br>

<a id="SQL"></a>
<h3> Structured Query Langauge (SQL) </h3>


SQL (Structured Query Language) is a standardized programming language that's used to manage relational databases and perform various operations on the data in them.
The uses of SQL include modifying database table and index structures; adding, updating, and deleting rows of data; and retrieving subsets of information from within a database.
Commonly used SQL statements include select, add, insert, update, delete, create, alter and truncate.

We are using here Postgres SQL language.

General Syntax:

This query selects all rows from 'transactions' where values in column 'id' = 10.

```sql
SELECT * FROM transactions WHERE id = 10;
```

Join Syntax:

```sql
SELECT column_name(s)
FROM table1
JOIN table2 ON table1.column_name = table2.column_name;
```

<a id="Joins"></a>
<h2> Types of Joins </h2>

There are five main types of joins in SQL; inner, full outer, left, right outer, and cross join.

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

Returns all records from the left table (table1) and the matched records from the right table (table2). The result is NULL from the right side if there is no match.

<img src="https://github.com/mveele/SQL_join_comms/blob/main/images/left_join.png" alt="drawing" width="300"/>


```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2 ON table1.column_name = table2.column_name;
```

<br>

<h3> Right Join </h3>

The right join is similar to the left join except that it returns all records from the right table (table2), and the matched records from the left table (table1). The result is NULL from the left side when there is no match.


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
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2 ON table1.column_name = table2.column_name;
```

<br>

<h3> Cross Join </h3>

Returns all combinations of records from both left (table1) and right (table2) table records as the cartesian product of rows of two tables.

<img src="https://github.com/mveele/SQL_join_comms/blob/main/images/cross_join.png" alt="drawing" width="300"/>


```sql
SELECT column_name(s)
FROM table1
CROSS JOIN table2;
```

For additional information, see our [Jupyter Notebook](https://github.com/mveele/SQL_join_comms/blob/main/comms_project.ipynb).

<a id="package"></a>
<h2> Python Packages and Functions </h2>



In-Built Packages

1. <i><u> psycopg2 </u></i> - for making Python connection with database
2.<i><u>  pandas </u></i>- for manipulation 
3. <i><u>   numpy </u></i>- for basic operations
4. <i><u>  IPython.core.display </u></i>- for displaying table visuals in the notebook

Created Functions
1. <i><u>  display_side_by_side</u></i> - for dsiplaying tables using html side by side.
2. <i><u>  hide_toggle</u></i> - for hiding few cells


<a id="Python"></a>
<h2> Connection with database  </h2>




A. Connect to the database with host name, database name and user credentials and create a cursor

```python
conn = psycopg2.connect(host=host, port=port, database=database, user=user)
cur = conn.cursor()
```

B. Fetching a table and storing it as a pandas dataframe

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


<a id="tables"></a>
<h2> Tables Used and Creation </h2>



Three tables are used in the notebook named: names, transactions, dob 

<b> Table: Names </b>


	id	name
	1	Jon Smith
	2	Sarah Adams
	3	Maria Lopez     


<b> Table: Transactions </b>


	id	amount
	1	10
	3	20
	7	50


<b> Table: Dob </b>


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

<a id="examples2"></a>
<h2> Two Tables Join  </h2>

<b> Inner join example </b>

Table names and transactions are inner joined based on common column 'id' and columns from both tables: id, name, amount are fetched for all rows matched in both tables.

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

	id	name	      amount
	 1	Jon Smith	  10
	 3	Maria Lopez	20
    

<b> Left join example </b>

Table names and transactions are left joined based on common column 'id' and columns from both tables: id, name, amount are fetched for all rows matched in the left table.

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

	id	name	       amount
	 1	Jon Smith	   10
	 2	Sarah Adams	 null
	 3	Maria Lopez	 20

<a id="example3"></a>
<h2> Three Tables Join  </h2>




<b> Inner join example </b>

Tables name, transactions, and dob are inner joined based on common column 'id' and columns from all three tables: id, name, amount, and dob are fetched for all rows matched in both tables.

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

	id	name	      amount	dob
	1	Jon Smith	  10	  1982-09-29
	3	Maria Lopez	20	  1996-02-16


 <a id="ex_otm_mtm"></a>   
<h2> One-to-many and Many-to-Many Joins  </h2>



    

So far, we have seen one-to-one joins means there was no duplicate of ids in any table (no two rows have the same id). But in reality, there is a possibility of an id having multiple records in a table. 

The query to do manipulation stays the same but the output would change in which the rows will be returned as many times as ids are duplicated in the tables. 

Refer to the image below:

<img src="https://github.com/mveele/SQL_join_comms/blob/surbhi33-patch-1/images/one_to_one.png" alt="drawing" 
width="800"/>
     
The only difference between one-to-many and many-to-many is that many-to-many has duplicate rows in both tables joined due to which the total rows in the output table will have a cartesian product of the number of duplicate rows in both tables.

<b> Example of One-to-Many </b> 

Table Transaction with duplicate ids.

<img src="https://github.com/mveele/SQL_join_comms/blob/surbhi33-patch-1/images/Long_trans.png" alt="drawing" width="200"/>

Output Table

<img src="https://github.com/mveele/SQL_join_comms/blob/surbhi33-patch-1/images/one2one_out.png" alt="drawing" width="200"/>

Here, id =1 duplicated two tables as the transaction table had two rows with id=1.


For many-to-many examples, see our [Jupyter Notebook](https://github.com/mveele/SQL_join_comms/blob/main/comms_project.ipynb).


<a id="Notebook_Link"></a>
<h2> Jupyter Notebook  </h2>




For more info and examples using concrete data, please see our [Notebook](https://github.com/mveele/SQL_join_comms/blob/main/comms_project.ipynb).

It has one example each for all types of joins and also covers three tables join. It also gives examples of one to many and many to one joins as well.

<h2> Summary </h2>

We covered the background of relations joins and why it is essential in the real world. We started with the basics of types of joins and explained what is SQL. Further, we got familiar with SQL syntax for basic queries of joins and then deep-dived into each join with examples of two tables and their respective queries. Often we need to join more than two tables. Hence, We went into the complexity of three tables join and also explained with visuals difference in outcomes in cases of duplicate values in the common column i.e. key between tables.

Finally, SQL Joins are a very useful tool required for day-to-day tasks of fetching information from data divided across many tables in the database. The examples above introduce us to the basics of joins which can be consolidated by going through the notebook and few practice materials mentioned below.


<h2> External videos for reference: </h2>

A. Joins: [SQL Joins](https://www.youtube.com/watch?v=2HVMiPPuPIM)

B. SQL Basics: [SQL in 1 Hour](https://www.youtube.com/watch?v=9Pzj7Aj25lw)

<a id="practice_Link"></a>    
<h2> Practice Material  </h2>



For further practice, you can refer to:

A. [41 Essential SQL Questions](https://www.toptal.com/sql/interview-questions)

B. [SQL HackerRank Challenges](https://www.hackerrank.com/domains/sql)
