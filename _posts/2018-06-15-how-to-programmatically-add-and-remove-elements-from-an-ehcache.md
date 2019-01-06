<strong>Pre-requisites</strong>

This guide assumes that you have already configured <a href="http://www.ehcache.org/">Ehcache</a>, and is specifically concerned with programmatic addition and removal of elements.

<strong>Adding an element to a cache</strong>

```java
@Autowired
private CacheManager cacheManager;

[...]

public Ehcache getCache(String name)
{
    return cacheManager.getCache(name);
}
```

In the above example we have simply "wired-in" the cache manager and called the "getCache()" method on it. This takes a String which is the name of the cache you wish to retrieve.

```java
private void updateCache()
{
    getCache("health").put(new Element(health.getName(), health));
}
```

Once we have retrieved the cache, we can call "put()" on it. This method takes the type "Element" which encapsulates the key and value to be stored in the cache. The key can consist of 1 or more values that will uniquely identify the element in the specified cache.

<strong>Removing an element from a cache</strong>

```java
public void remove(String name, Collection&lt;Object&gt; key)
{
    Ehcache cache = getCache(name);

    if (cache.isKeyInCache(key))
    {
        cache.remove(key);
    }
}
```

To remove an element from a cache we first need to built the key. This is a collection of type "Object" which will contain 1 or more values that will uniquely identify the element. First we will check that the key exists in the cache. If it does, we can call the "remove" method on the cache. This method takes the key as an argument.

```java
private void removeFromCache(ApplicationHealth health)
{
    remove("health", Arrays.asList(health.getName()));
}
```
