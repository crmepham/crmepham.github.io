---
ID: 628
post_title: >
  Mysql Functions, declarations and common
  methods
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/programming/mysql-functions-declarations-and-common-methods/
published: true
post_date: 2016-01-14 17:54:28
---
The following is a reference implementation of a function declaration and explanation of common method usages.

This example function can be used to capitalize the first letter of each word in a String and add a full-stop to the end of the String if one doesn't already exist.

<script src="https://gist.github.com/final60/8a53fde038f24d44bfbc.js"></script>

Note: The main difference between functions and procedures are their usage:

    A stored routine is either a procedure or a function.

    A procedure is invoked using a CALL statement and can only pass back values using output variables.

    A function can be called from inside a statement just like any other function and can return a scalar value.

    A function can return only 1 value, where a procedure can return up to a maximum of 1024 values or non at all.