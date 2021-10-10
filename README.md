# Relational Join

When performing an analysis, it's ideal if all information is stored in a single table. However, it's common that data are stored in many different tables/relations inside the database. In such as case, we will use the relational join to bring data together.

For additional information, see our [notebook](https://github.com/mveele/SQL_join_comms/blob/main/comms_project.ipynb).

<!-- To perform an analysis, it would be ideal if all desired information is in a single table. However, you will find that the data are usually divided into two or more relations to optimize the storage. In such cases, we need to bring relations into one table using a relation join. -->

## SQL keyword

The Relational Join is a Structured Query Language (SQL) keyword to query data from two or more tables.

General Syntax:

SELECT <br>
[Field Names] <br>
FROM TableA A <br>
&emsp; [Join Type] JOIN TableB B <br>
&emsp; &emsp; ON A.key=B.key <br>
<br>

## Join Types


### INNER JOIN
SELECT <br>
[Field Names] <br>
FROM TableA A <br>
&emsp; <b> INNER JOIN </b> TableB B <br>
&emsp; &emsp; ON A.key=B.key <br>

<img src="https://github.com/mveele/SQL_join_comms/blob/main/images/inner_join.png" alt="drawing" width="200"/>
<br>

### LEFT JOIN
SELECT <br>
[Field Names] <br>
FROM TableA A <br>
&emsp; <b> LEFT JOIN </b> TableB B <br>
&emsp; &emsp; ON A.key=B.key <br>

<img src="https://github.com/mveele/SQL_join_comms/blob/main/images/left_join.png" alt="drawing" width="200"/>
<br>

### RIGHT JOIN
SELECT <br>
[Field Names] <br>
FROM TableA A <br>
&emsp; <b> RIGHT JOIN </b> TableB B <br>
&emsp; &emsp; ON A.key=B.key <br>

<img src="https://github.com/mveele/SQL_join_comms/blob/main/images/right_join.png" alt="drawing" width="200"/>
<br>

### FULL JOIN
SELECT <br>
[Field Names] <br>
FROM TableA A <br>
&emsp; <b> FULL JOIN </b> TableB B <br>
&emsp; &emsp; ON A.key=B.key <br>

<img src="https://github.com/mveele/SQL_join_comms/blob/main/images/full_join.png" alt="drawing" width="200"/>
<br>

For more info and examples using concrete data, please see our [notebook](https://github.com/mveele/SQL_join_comms/blob/main/comms_project.ipynb).
