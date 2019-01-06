In this post I will explain what database normalization is and describe an example of how to develop a relational database schema at 3rd normal form. I recommend reading this post on a large screen.
<h2>What is a relational database?</h2>
A well designed relational database will consist of structured tables that are related to one another through the use of foreign keys. Each table maps directly to a real world entity and will consist of columns that correspond to that entities attributes. It will also contain a primary key (one or more columns that uniquely identify a row), and foreign keys to map a row in that table to rows in other tables.
<h2>What is normalization?</h2>
Normalization of a database table is done to reduce data redundancy and duplication of attribute data. By normalizing a table in to more manageable smaller tables, it becomes easier to manage changes to attribute data, by making the change in a single table, and having that change propagate through the other tables via foreign keys.
<h2>Establishing the first normal form (1NF)</h2>
[caption id="attachment_625" align="alignleft" width="1246"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/invoice.png"><img class="size-full wp-image-625" src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/invoice.png" alt="invoice" width="1246" height="203" /></a> invoice[/caption]

Above is an invoice containing customer orders from a company that sells fish. You will notice that there is a large amount of duplication in many of the rows. First normal form is achieved when all attributes become atomic (contain only a single value), any repeating groups are eliminated and a primary key is identified to uniquely identify a single row of related data. The primary key can be made up of multiple attributes provided they combine to uniquely identify a given row in the table, this is called a <strong>composite primary key</strong>. In its current un-normalised form (UNF) the primary key is made up of two fields: <strong>Invoice Number</strong> and <strong>Product Code. </strong>It takes the combination of these two attributes to uniquely identify a row in the table.
<h3>First normal form dependency diagram</h3>
[caption id="attachment_608" align="alignright" width="190"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/key.png"><img class="size-full wp-image-608" src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/key.png" alt="Dependency diagram key" width="190" height="65" /></a> Dependency diagram key[/caption]

[caption id="attachment_606" align="alignleft" width="1102"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/1nf.png"><img class="size-full wp-image-606" src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/1nf.png" alt="first normal form" width="1102" height="213" /></a> first normal form[/caption]

&nbsp;

&nbsp;

&nbsp;

<strong>1NF</strong> (INVOICE_NUMBER, PRODUCT_CODE → CUSTOMER_NUMBER, CUSTOMER_NAME, INVOICE_DATE, LINE_NUMBER, COMMON_NAME, SCIENTIFIC_NAME, CATEGORY, QUANTITY, PRICE_CHARGED)
<strong>PARTIAL DEPENDENCIES:</strong>
(PRODUCT_CODE → COMMON_NAME, SCIENTIFIC_NAME)
(INVOICE_NUMBER → LINE_NUMBER, QUANTITY, PRICE_CHARGED, INVOICE_DATE)
<strong>TRANSITIVE DEPENDENCY</strong>
(CUSTOMER_NUMBER → CUSTOMER_NAME)
<h2>What are transitive and partial dependencies?</h2>
A partial dependency exists when an attribute in a table relies on part or all of an existing primary key.

A transitive dependency exists when an attribute in a tables relies on one or more attributes that are not primary keys.
<h2>Establishing the second normal form (2NF)</h2>
[caption id="attachment_619" align="alignleft" width="877"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/2nf.png"><img class="size-full wp-image-619" src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/2nf.png" alt="second normal form" width="877" height="264" /></a> second normal form[/caption]

At this stage you must separate the 1NF diagram to illustrate the separate tables based on the partial relationships that were identified, and identify the primary key for each table.
<h2>Establishing the third normal form (3NF)</h2>
[caption id="attachment_621" align="alignleft" width="872"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/3nf.png"><img class="size-full wp-image-621" src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/3nf.png" alt="third normal form" width="872" height="420" /></a> third normal form[/caption]

Finally you need to extract any transitive dependencies that reside within a table that was created during 2NF. The existing partial relationship tables are retained and a new table is created to represent the transitive dependency. The determinants in the transitive relationship become the primary key in the new table.

This database of tables can now be considered normalised.
<h2>3NF Entity-relationship diagram</h2>
[caption id="attachment_623" align="alignleft" width="422"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/erd.png"><img class="size-full wp-image-623" src="http://chrismepham.co.uk/blog/wp-content/uploads/2016/01/erd.png" alt="3NF entity-relationship diagram" width="422" height="439" /></a> 3NF entity-relationship diagram[/caption]

&nbsp;
