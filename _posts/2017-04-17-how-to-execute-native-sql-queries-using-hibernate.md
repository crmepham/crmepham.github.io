---
classes: wide
tags: [spring, hibernate]
---
In some cases, there may be a need for you to write native SQL. Typically you may use a framework such as Spring JDBC for this, but if you already have an ORM framework that allows you to perform native queries, although, in an arguably less trivial way, you might as well use it.

The following example assumes you already have setup Hibernate for your application.

First, setup the class to represent the data you wish to query using native SQL.
<pre class="EnlighterJSRAW" data-enlighter-language="java">public class RemoteKnowledge {

  private Date lastUpdated;
  
  private String text;
  
  private String createdBy;

  public Date getLastUpdated() {
    return lastUpdated;
  }

  public void setLastUpdated(Date lastUpdated) {
    this.lastUpdated = lastUpdated;
  }

  public String getText() {
    return text;
  }

  public void setText(String text) {
    this.text = text;
  }

  public String getCreatedBy() {
    return createdBy;
  }

  public void setCreatedBy(String createdBy) {
    this.createdBy = createdBy;
  }
}</pre>
Next, we will perform the simplest of the native SQL queries.
<pre class="EnlighterJSRAW" data-enlighter-language="java">@Override
public Object getRemoteKnowledge(String externalReference) {
  
  String select = "select wc.text as text, u.login as createdBy, wc.updated_on as lastUpdated ";
  
  String sql = select + BASE_SQL + "and p.identifier = :externalReference";
  
  Query query = getSession().createSQLQuery(sql)
      .setParameter("externalReference", externalReference)
  List results = query.list();
  
  if (results.size() &gt; 0) {
    return results.iterator().next();
  }
  
  return null;
}</pre>
The above code will perform the native query which will return a list of Objects. But we have to create logic in our business layer to identify the columns and map it our object above.

Next, we will perform the same native SQL query but we will also perform the mapping.
<pre class="EnlighterJSRAW" data-enlighter-language="java">public RemoteKnowledge getRemoteKnowledge(String externalReference) {
  
  String select = "select wc.text as text, u.login as createdBy, wc.updated_on as lastUpdated ";
  
  String sql = select + BASE_SQL + "and p.identifier = :externalReference";
  
  Query query = getSession().createSQLQuery(sql)
      .addScalar("text", StandardBasicTypes.STRING)
      .addScalar("createdBy", StandardBasicTypes.STRING)
      .addScalar("lastUpdated", StandardBasicTypes.DATE)
      .setParameter("externalReference", externalReference)
      .setResultTransformer(Transformers.aliasToBean(RemoteKnowledge.class));
  List results = query.list();
  
  if (results.size() &gt; 0) {
    return (RemoteKnowledge) results.iterator().next();
  }
  
  return null;
}</pre>
The above query allowed us to specify the names of the columns using the method <code class="EnlighterJSRAW" data-enlighter-language="java">addScalar()</code>, specifying the name and datatype. We can also allow Hibernate to automatically map the results to our RemoteKnowledge Object using the method <code class="EnlighterJSRAW" data-enlighter-language="java">setResultTransformer()</code>.
