In Java you can use the Java Database connector (JDBC) API to connect your program with most databases. In this example I will demonstrate how to establish a connection Pool and use a JDBC connection to do some basic CRUD functions with a MySQL database.

To start with you need to download the JDBC driver for your chosen Database. In this case I am using the MySQL driver which can be downloaded <a title="MySQL JDBC driver" href="http://dev.mysql.com/downloads/connector/j/" target="_blank">here</a>.

Simply add this driver to your projects class path.

Next we will create a DataSourceFactory class that will be used to establish a connection with our MySQL database.

<script src="https://gist.github.com/final60/aa25fedb53c1a7014f22.js"></script>

Next we will instantiate the database connection object.

<script src="https://gist.github.com/final60/1189b09b047d09bf908e.js"></script>

And use this object to get a connection from the connection pool. In the following example I will check a users credentials using a SELECT MySQL query.

<script src="https://gist.github.com/final60/481c19e8e0673abc2a6e.js"></script>

This form of connection pooling is considered quite a low level method of establishing a connection to a database. In industry it is more common to use Frameworks like Spring that hide most of this functionality, but it is still useful to know.

Connection pooling is necessary to ensure a persistent connection is available for the entire duration that the program is running, which in the case of a web service could potentially be indefinitely. If you attempted to establish a direct connection to a database, this connection would timeout after a short period of time and require the service to be restarted.
