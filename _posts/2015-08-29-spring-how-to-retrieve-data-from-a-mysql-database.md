In this tutorial I will demonstrate how to retrieve multiple rows of data from a MySQL database using Spring.

Before I start I will setup a standard eclipse Maven project that has the following dependencies:
spring-beans, spring-context, spring-core, mysql-connector-java, commons-dbcp and spring-jdbc.

Next I will setup my MySQL database so it contains a dog table with some data ready to be queried by my Java application.
<script src="https://gist.github.com/final60/ad22aa100aa92552071e.js"></script>

<strong>1) Create a model of type Dog</strong>
<script src="https://gist.github.com/final60/09d72364247f389dd7ff.js"></script>
Above you can see a plain old Java object (POJO), which contains some basic properties and getter/setter methods. This Dog class will be used as the object equivalent of the dog table in the database I created earlier and resides in package com.crm.hibernate.dao. Notice that I am using the <strong>@Component</strong> annotation to specify to Spring that this is a bean, but more on that a bit later when I configure the Spring bean configuration file.

<strong>2) Create a properties file</strong>
Now I will create a standard properties file called jdbc.properties in package com.crm.hibernate.properties.
<script src="https://gist.github.com/final60/ed6fbbb147ce4b051891.js"></script>
It is important that the property names match up to the properties of the BasicDataSource class that I will be using to create a database connection for pooling. More on this a bit later.

<strong>3) Create a Spring beans configuration file</strong>
Next I will create a beans.xml configuration file in package com.crm.hibernate.xml.
<script src="https://gist.github.com/final60/6dfe9addc32b0bd0c8ec.js"></script>
<strong>context:property-placeholder</strong> is a tag that tells Spring where to look for a properties file, who's containing properties I can reference in this configuration file using the ${} notation. Within the curly braces I simply put the name of the relevant property I defined in the properties file.

<strong>context:component-scan</strong> is a tag that tells Spring where to look for annotated classes. For this example I have annotated two classes with the <strong>@Component</strong> annotation, these classes reside in packages that will be scanned by Spring when the application is run.

Next I am simply defining a new bean explicitly, using traditional xml. The bean is of the class BasicDataSource which is the magic class that will be used to provide a database connection from a pool of available connections, which a Spring JDBC object will query, more on that later.

<strong>4) Create a database connection class</strong>
<script src="https://gist.github.com/final60/a77841aa078121b61900.js"></script>
In the above example I have created a class called dogDAO which resides in the package com.crm.hibernate.dao (which will be scanned for Spring annotations). You will notice that the class is annotated with @Component, so Spring will create a bean out of it, which can be used elsewhere in the application at runtime. Next I have declared a JdbcTemplate object. This class is a Spring class that contains many great methods that I can use to query a database with. Further down the code you will notice that I have a setter method which instantiates the "jdbc" object and passes it the DataSource bean auto-magically, because that method is annotated with <strong>@Autowired</strong>, which means that Spring will automatically pass this object from its own "Spring pool" at runtime. So now the jdbc object has been instantiated and it has a connection that it can query.

Next I am defining a method called "getDogs" which will return a list of dogs, where each element in the list will represent a row in the corresponding dog table.

Inside the "getDogs" method I am returning the result of a query to the data source. The jdbc object contains a "query" method which takes a standard SQL query as part of it's arguments and an anonymous class as another. Inside the anonymous class I am implementing a method that the interface "RowMapper" specifies, which maps a row from the JDBC resultset to a single Dog object and adds that Dog object to a list. Once all rows have been mapped to Dog objects a list of these Dog objects is returned from the "getDogs" method.

<strong>5) Print the list of dogs to the console</strong>
<script src="https://gist.github.com/final60/58eb50c857c483dd16cd.js"></script>
In the above example I am instantiating a new dogDAO bean and generating a list of Dogs by calling the "getDogs" method of the "dogDAO" object and then simply looping through the list calling each Dog objects "toString" method.

Output:



<blockquote>Dog [name=buster, age=3, id=1, canTalk=true]
Dog [name=millie, age=1, id=2, canTalk=false]
Dog [name=maisie, age=8, id=3, canTalk=true]</blockquote>


Finally, here is the file structure for context:
[caption id="attachment_448" align="aligncenter" width="284"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2015/08/file-structure.png"><img src="http://chrismepham.co.uk/blog/wp-content/uploads/2015/08/file-structure.png" alt="file-structure" width="284" height="614" class="size-full wp-image-448" /></a> file-structure[/caption]
