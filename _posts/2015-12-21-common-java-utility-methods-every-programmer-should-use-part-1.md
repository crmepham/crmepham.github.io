---
ID: 505
post_title: >
  Common Java utility methods every
  programmer should use (Part 1)
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/programming/common-java-utility-methods-every-programmer-should-use-part-1/
published: true
post_date: 2015-12-21 17:36:40
---
This post will be the first in a series of posts describing useful utility methods that will help make any programmers day to day code implementation easier.

The methods in this post:
<ul>
String.format()
java.io.FileFilter
Collections.sort()
parsePropertiesFromString()</ul>

<strong>String.format()</strong>
This method is useful to build a string programmatically without using concatenation, it generally makes for more readable and therefore manageable code.
<script src="https://gist.github.com/final60/7d850cbf7519bc7ad2f5.js"></script>

<strong>Collections.sort()</strong>
A straight forward method call used to sort a collection based on its "natural order" - alphabetically for Strings, numerically for Integers.
<script src="https://gist.github.com/final60/bb7d41f6006b209c19f4.js"></script>

<strong>java.io.FileFilter</strong>
This class enables you to specify how you want to filter files that you add to a Collection.
<script src="https://gist.github.com/final60/af01cad3cbf133f87bc0.js"></script>

<strong>CollectionStringUtils.parsePropertiesFromString()</strong>
This handy method is from the impala framework: org.impalaframework, and allows you to create a Map of key value pairs from a String object.
<script src="https://gist.github.com/final60/3ad35d63180559667a4a.js"></script>