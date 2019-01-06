This tutorial will describe how to implement custom JPA methods for dynamically-driven queries in Spring Boot.
<h3>Maven package dependencies</h3>
<pre class="EnlighterJSRAW" data-enlighter-language="xml">&lt;parent&gt;
    &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
    &lt;artifactId&gt;spring-boot-starter-parent&lt;/artifactId&gt;
    &lt;version&gt;1.5.1.RELEASE&lt;/version&gt;
    &lt;relativePath /&gt;
  &lt;/parent&gt;

  &lt;dependencies&gt;
   &lt;dependency&gt;
      &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
      &lt;artifactId&gt;spring-boot-starter-web&lt;/artifactId&gt;
    &lt;/dependency&gt;
    &lt;dependency&gt;
      &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
      &lt;artifactId&gt;spring-boot-starter-data-jpa&lt;/artifactId&gt;
    &lt;/dependency&gt;
    &lt;dependency&gt;
      &lt;groupId&gt;mysql&lt;/groupId&gt;
      &lt;artifactId&gt;mysql-connector-java&lt;/artifactId&gt;
    &lt;/dependency&gt;
  &lt;/dependencies&gt;</pre>
<h3></h3>
<h3>The JPA interface</h3>
Typically JPA is very useful because it removes a lot of implementation boilerplate code. Your DAO interface only needs to extend the JPARepository (or more generic CrudRepository), but the basic CRUD methods do not need to be defined or implement in a concrete class because the concrete implementation is automatically created at runtime.

&nbsp;
<pre class="EnlighterJSRAW" data-enlighter-language="java">import javax.transaction.Transactional;

import org.springframework.data.jpa.repository.JpaRepository;

import com.crm.model.User;

@Transactional
public interface UserDao extends JpaRepository&lt;User, Long&gt; {
  
  // ... No need to define any methods here for basic crud operations
}</pre>
&nbsp;

But if you want to start being more specific, JPA allows you to define custom query methods.
<pre class="EnlighterJSRAW" data-enlighter-language="java">import javax.transaction.Transactional;

import org.springframework.data.jpa.repository.JpaRepository;

import com.crm.model.User;

@Transactional
public interface UserDao extends JpaRepository&lt;User, Long&gt; {
  
  public User findByEmail(String email);
  
  public User findByUserNameAndEmailContaining(String username, String email);

}</pre>
The second of the above method queries would result in the following JPQL query:
<pre class="EnlighterJSRAW" data-enlighter-language="sql">... where username = ? and email like '%?%';</pre>
Click <a href="https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories.query-methods">here</a> for more information on JPA method queries.
<h3>Dynamic JPA queries</h3>
The above JPA query methods are restrictive because they rely on the method and query parameters being known. But what if we need to programmatically define a query without knowing how many parameters will be received or what criteria to use. A common example being search.

JPA allows you to define custom interfaces.
<pre class="EnlighterJSRAW" data-enlighter-language="java">import javax.transaction.Transactional;

import com.crm.model.User;

@Transactional
public interface UserDaoCustom {
  
  public List&lt;User&gt; customMethod(String email);

}</pre>
You will then need an implementation class. Note, there is nothing stopping you using some other implementation, like JdbcTemplate here.
<pre class="EnlighterJSRAW" data-enlighter-language="java">import java.util.List;

import javax.persistence.EntityManager;
import javax.persistence.PersistenceContext;
import javax.transaction.Transactional;

import org.springframework.stereotype.Repository;

import com.crm.model.User;

@Transactional
@Repository
public class UserDaoImpl implements UserDaoCustom {
  
  @PersistenceContext
  EntityManager em;

  public List&lt;User&gt; customMethod(String email) {
    return em.createQuery("from User", User.class).getResultList();
  }

}</pre>
You can then combine your custom interface with the method queries interface to access both the custom methods, query methods and the basic crud methods all at the same time.
<pre class="EnlighterJSRAW" data-enlighter-language="java">import javax.transaction.Transactional;

import org.springframework.data.jpa.repository.JpaRepository;

import com.crm.model.User;

@Transactional
public interface UserDao extends JpaRepository&lt;User, Long&gt;, UserDaoCustom {
  
  public User findByEmail(String email);
  
  public User findByUserNameAndEmailContaining(String username, String email);

}</pre>
You then wire in the UserDao to your service or controller.
<pre class="EnlighterJSRAW" data-enlighter-language="java">import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

import com.crm.dao.UserDao;
import com.crm.model.User;

@Controller
public class UserController {
  
  @Autowired
  private UserDao userDao;

  @RequestMapping("/searchUsers")
  @ResponseBody
  public String searchUsers(String search) {
    Long userId;
    try {
      User user = userDao.customMethod(search);
      userId = user.getId();
    } catch (Exception ex) {
      return "User not found";
    }
    return "The user id is: " + userId;
  }
...</pre>
Note the JPA is very strict with its naming policies. In the above examples note that the first interface <code class="EnlighterJSRAW" data-enlighter-language="java">userDao</code> can extend a custom interface <code class="EnlighterJSRAW" data-enlighter-language="java">userDaoCustom</code>, which can in turn be implemented by <code class="EnlighterJSRAW" data-enlighter-language="java">userDaoImpl.</code>

The use of the suffixes here is very important and must be followed, otherwise, you will get a compiler error.

&nbsp;

&nbsp;

&nbsp;
