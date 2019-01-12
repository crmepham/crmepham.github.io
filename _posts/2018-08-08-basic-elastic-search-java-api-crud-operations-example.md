---
classes: wide
tags: [elasticsearch, java, spring]
---
This guide assumes you have already setup the <a href="https://www.baeldung.com/elasticsearch-java">Elastic Search API</a> with your Java application.

The following examples use a 'Part' entity:

```java
public class Part
{

    private String elasticSearchId;

    @SerializedName("PartId")
    @Expose
    public String partId;
    @SerializedName("PartNumber")
    @Expose
    public String partNumber;
    @SerializedName("PartDescription")
   
    [...]
```
    
Indexing a Part document:

```java
@Override
    public void index(@Nonnull final Part part)
    {
        final Client client = elasticClient.getClient();

        Gson gson = new GsonBuilder().setDateFormat("yyyy-MM-dd").create();
        final String source = gson.toJson(part);
        IndexResponse response = client.prepareIndex("indexName", "part")
                     .setSource(source, JSON).get();

        part.setElasticSearchId(response.getId());
    }
```
    
The above example uses GSON to convert the Part object into JSON, and illustrates how to correctly format dates to be accepted by Elastic Search. The prepareIndex() method takes the name of the index and the name of the document, then the sets the source of the document to the JSON. The response that is return will contain the unique String id of the newly indexed document.

Getting an indexed document:

```java
@Override
    public Part get(@Nonnull final String id)
    {
        GetResponse response = elasticClient.getClient()
                .prepareGet("indexName","part", id)
                .get();

        final String sourceAsString = response.getSourceAsString();
        Gson gson =  new GsonBuilder().setDateFormat("yyyy-MM-dd").create();
        return gson.fromJson(sourceAsString, Part.class);
    }
```
    
To get the specific document in the above example, we have supplied the Elastic Search id of the document to the prepareGet() and parse the source of the document that is returned in the GetResponse object. Really straight-forward!

Deleting an indexed document:

```java
@Override
    public void delete(@Nonnull final String id)
    {
        elasticClient.getClient()
                     .prepareDelete("indexName", part, id)
                     .get();
    }
```
    
Probably the simplest of all - To delete a document, simply pass in the elastic search id of the document to the prepareDelete() method.

List all documents:

```java
@Override
    public Set&lt;Part&gt; list()
    {

        SearchResponse searchResponse = elasticClient.getClient()
                .prepareSearch("indexName")
                .setSearchType(SearchType.QUERY_THEN_FETCH)
                .setQuery(QueryBuilders.matchAllQuery())
                .setFetchSource(true)
                .setTypes("part")
                .get();

        return maybePopulateParts(new HashSet&lt;Part&gt;(), searchResponse);
    }
```
    
Another fairly straight-forward operation - Simply cal the prepareSearch() method with a .setQuery() to match all entries of the given document type. The resulting SearchResponse object will contain the "hits". The hits will contain a source which can be extracted as a String and parsed using a JSON parser such as GSON.

Searching documents:

```java
private void search(String term, Set&lt;Part&gt; parts)
    {
        SearchResponse searchResponse = elasticClient.getClient()
                .prepareSearch("indexName")
                .setSearchType(SearchType.QUERY_THEN_FETCH)
                .setQuery(QueryBuilders.prefixQuery("PartNumber", term))
                .setFetchSource(true)
                .setTypes("part")
                .get();

        maybePopulateParts(parts, searchResponse);
    }

    private Set&lt;Part&gt; maybePopulateParts(Set&lt;Part&gt; parts, SearchResponse searchResponse)
    {
        List&lt;SearchHit&gt; results = Arrays.asList(searchResponse.getHits().getHits());

        if (results.size() &gt; 0)
        {
            Gson gson = new GsonBuilder().setDateFormat("yyyy-MM-dd").create();

            results.forEach(h -&gt; {

                Part part = gson.fromJson(h.getSourceAsString(), Part.class);
                if (part != null)
                {
                    parts.add(part);
                }
            });
        }

        return parts;
    }
```
    
The above example demonstrates how to search for a specific document where the field "PartNumber" starts with the specific search term. This is achieved using the query builder "prefixQuery()" supplying both the field name and the search term to search for. Buy default, when indexing a new document, elastic search will pass the document through an "analyser" which will create "terms" for each of the fields so the can be searched. For example: The value "One-234" will result in 2 terms being created: "one" and "234. Elastic search has split the value by the dash and lowercased the values. For this reason, searching for the field value "One-234" or "one-" would not actually find a document containing a field with the value "One-234". It would find the document if you search for "On" or "23" for example. Note that with the prefixQuery() builder using the the text "34" wouldn't find the document.

There are a large number of built in query builders, and you can also create custom analyser's. Or remove the analysers entirely in the settings.

Going back to the example above - given that SearchReponse contains a number of "hits", you will notice that you can get the list of hits, iterate on them, and parse the source using GSON.

&nbsp;
