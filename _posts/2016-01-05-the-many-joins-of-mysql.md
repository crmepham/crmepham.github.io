[caption id="attachment_545" align="aligncenter" width="1044"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/joins.png"><img class="size-full wp-image-545" src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/joins.png" alt="Mysql joins" width="1044" height="695" /></a> Mysql joins[/caption]

Following the process of normalization - a well designed Relational database will usually have more than one table with related data in it. The reason for normalization is to separate data into tables, representing single entities, to prevent data redundancy. These tables will be linked together using foreign keys. When we want to correlate data from multiple tables we can use the <strong>join </strong>key word to do so. The following is a brief description of three commonly used joins: <strong>left</strong>, <strong>inner </strong>and <strong>right</strong>.

<strong>LEFT JOIN</strong>
Will return all the rows in the table on the left of the join. It will then attempt to get any matching rows in the right table. If it can't match a particular row, it will return NULL.

<strong>RIGHT JOIN</strong>
This will do the opposite of the above, by returning all the rows in the table in the right of the join and then attempt to get matching rows from the table in the left. This join is less commonly used because you can simple swap the left and right tables in a left join to have the same effect.

<strong>INNER JOIN</strong>
This join will return no NULL values. It will only return complete rows. That is, where a row in the left table matches a row in the right table. If there is a row in the left table but no matching row in the right table, the left row is not returned.

Example database tables

Dog
<table width="373">
<tbody>
<tr>
<td width="64">id</td>
<td width="64">name</td>
<td width="64">age</td>
<td width="64">typeId</td>
<td width="117">healthStatsId</td>
</tr>
<tr>
<td>1</td>
<td>Bengy</td>
<td>5</td>
<td>1</td>
<td>3</td>
</tr>
<tr>
<td>2</td>
<td>Maisie</td>
<td>9</td>
<td>4</td>
<td>2</td>
</tr>
<tr>
<td>3</td>
<td>Milly</td>
<td>2</td>
<td>4</td>
<td>12</td>
</tr>
</tbody>
</table>
Dog type
<table width="288">
<tbody>
<tr>
<td width="64">id</td>
<td width="81">name</td>
<td width="143">description</td>
</tr>
<tr>
<td>8</td>
<td>boxer</td>
<td>The Boxer is ..</td>
</tr>
<tr>
<td>2</td>
<td>poodle</td>
<td>The poodle is..</td>
</tr>
<tr>
<td>3</td>
<td>labrador</td>
<td>The labrador is..</td>
</tr>
<tr>
<td>4</td>
<td>cavalier</td>
<td>The Cavalier is..</td>
</tr>
</tbody>
</table>
Health
<table width="396">
<tbody>
<tr>
<td width="64">id</td>
<td width="140">blood pressure</td>
<td width="64">weight</td>
<td width="64">height</td>
<td width="64">length</td>
</tr>
<tr>
<td>3</td>
<td>60-90</td>
<td>65</td>
<td>57</td>
<td>82</td>
</tr>
<tr>
<td>12</td>
<td>65-90</td>
<td>55</td>
<td>50</td>
<td>70</td>
</tr>
</tbody>
</table>
<strong>Left join of tables</strong>
<script src="https://gist.github.com/final60/744cee0e85f18f09c2e5.js"></script><strong>Left join results</strong>

<table width="547">
<tbody>
<tr>
<td width="64">name</td>
<td width="64">age</td>
<td width="65">breed</td>
<td width="99">description</td>
<td width="103">blood pressure</td>
<td width="52">weight</td>
<td width="50">height</td>
<td width="50">length</td>
</tr>
<tr>
<td>Bengy</td>
<td>5</td>
<td>null</td>
<td>null</td>
<td>60-90</td>
<td>65</td>
<td>57</td>
<td>82</td>
</tr>
<tr>
<td>Maisie</td>
<td>9</td>
<td>cavalier</td>
<td>The Cavalier..</td>
<td>null</td>
<td>null</td>
<td>null</td>
<td>null</td>
</tr>
<tr>
<td>Milly</td>
<td>2</td>
<td>cavalier</td>
<td>The Cavalier..</td>
<td>65-90</td>
<td>55</td>
<td>50</td>
<td>70</td>
</tr>
</tbody>
</table>

You will notice that in every row we have the Dog data. This is because the left join will return data from this table whether or not there is a match with rows in the table dog_type or the table health. For the top row "Bengy" - because it could not match any rows from dog_type it returns null values for those columns, next it did match a row from the health table and display the data.

<strong>Inner join of tables</strong><script src="https://gist.github.com/final60/6ff1d57ea5fd6328a029.js"></script>
<strong>Inner join results</strong>
<table width="547">
<tbody>
<tr>
<td width="64">name</td>
<td width="64">age</td>
<td width="65">breed</td>
<td width="99">description</td>
<td width="103">blood pressure</td>
<td width="52">weight</td>
<td width="50">height</td>
<td width="50">length</td>
</tr>
<tr>
<td>Milly</td>
<td>2</td>
<td>cavalier</td>
<td>The Cavalier..</td>
<td>65-90</td>
<td>55</td>
<td>50</td>
<td>70</td>
</tr>
</tbody>
</table>
In this case only one row was returned. This is because an inner join will only return matching rows, and because we have two inner joins in our query there must be a match in both right tables for the query to return a resulting row.
