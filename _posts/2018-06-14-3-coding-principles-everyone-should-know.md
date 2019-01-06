---
ID: 961
post_title: >
  3 Coding principles everyone should
  know!
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/programming/3-coding-principles-everyone-should-know/
published: true
post_date: 2018-06-14 11:47:15
---
This post will describe 3 of the main principles I use when coding. These principles help me to write clean, readable and manageable code.

<strong>1. Get out quick (Short-circuit methods)</strong>

When writing methods, always be trying to return as soon as possible. Take the following example:
<pre class="EnlighterJSRAW" data-enlighter-language="java">/**
 * Fetch the usernames in the specified group. If a username is provided, lookup just that single
 * {@link User}.
 *
 * @param group The name of the group within which the user belongs.
 * @param username The optional username with which to lookup the user.
 * @return A collection of {@link Users}'s.
 */
public Collection&lt;User&gt; getUsers(String group, String username) {
    Collection&lt;User&gt; users = new ArrayList&lt;User&gt;();
    Collection&lt;String&gt; groups = getGroupNames();

    if (group != null &amp;&amp; groups.contains(group)) {
        if (username != null) {
            User user = userRepository.findByUsername(username);
            users.add(user);
        } else {
            users = userRepository.findByGroup(group);
        }
    }

    return users;
}</pre>
There is no point instantiating the users and groups collections (or doing anything else for that matter) if no group parameter has been supplied. Take the following example:
<pre class="EnlighterJSRAW" data-enlighter-language="java">public Collection&lt;User&gt; getUsers(String group, String username) {

    if (group == null) {
        return Collections.emptyList();
    }

    Collection&lt;User&gt; users = new ArrayList&lt;User&gt;();
    Collection&lt;String&gt; groups = getGroupNames();

    if (groups.contains(group)) {
        if (username != null) {
            User user = userRepository.findByUsername(username);
            users.add(user);
        } else {
            users = userRepository.findByGroup(group);
        }
    }

    return users;
}</pre>
Notice that I have added an if condition to check that the group parameter is not null. If it is null I will simply return an empty collection. You may instead want to throw an exception if this is not an expected state, or move this check up to the calling class to prevent the method ever getting called with a null group value. I will improve it further with the following example:
<pre class="EnlighterJSRAW" data-enlighter-language="java">public Collection&lt;User&gt; getUsers(String group, String username) {

    if (group == null) {
        return Collections.emptyList();
    }

    Collection&lt;String&gt; groups = getGroupNames();
    if (!groups.contains(group)) {
        return Collections.emptyList();
    }

    Collection&lt;User&gt; users = new ArrayList&lt;User&gt;();

    if (username != null) {
        User user = userRepository.findByUsername(username);
        users.add(user);
    } else {
        users = userRepository.findByGroup(group);
    }

    return users;
}</pre>
Notice that I have moved up and reversed the if condition that checks that the group name is a valid name that exists and can be used to lookup the users. This condition will now check is the name doesn't exist and return an empty collection if it doesn't. Notice, also, that by moving and reversing this boolean condition we have removed the nesting of the subsequent logic.

<strong>2. Sing Responsibility Principle (SRP)</strong>

As stated by Robert C. Martin, in the book <a href="https://www.amazon.co.uk/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882/ref=sr_1_1?ie=UTF8&amp;qid=1528975193&amp;sr=8-1&amp;keywords=the+clean+code">Clean code: A handbook of Agile Software Craftmanship</a>, a method should only be concerned with doing 1 thing. Sticking to this principle will make your code much easier to manage, read, and unit test. Take the following example:
<pre class="EnlighterJSRAW" data-enlighter-language="java">public Collection&lt;User&gt; getUsers(String group) {

    if (group == null) {
        return Collections.emptyList();
    }

    Collection&lt;String&gt; groups = getGroupNames();
    if (!groups.contains(group)) {
        return Collections.emptyList();
    }

    return userRepository.findByGroup(group);
}

public User getUser(String username) {

    if (username == null) {
        throw new InvalidStateException("Username must not be null");
    }
    return userRepository.findByUsername(username);
}</pre>
Notice that where previously we had 1 single method doing 2 things (Looking up a collection of Users based on the supplied group name, and also looking up a single User if a username was supplied), we have now separated this functionality out into 2 methods.

One method is specifically concerned with doing the lookup of users based on the supplied group name, and the new method is specifically concerned with looking up the single  User based on the supplied username. Now both methods can be unit tested individually, and it is must easier to understand what each method is responsible for doing.

<strong>3. Sniff out those bad smells.</strong>

The following are a few things to watch out for whilst you are coding to help you identify when you may be starting to allow bad code design to creep in.

<strong>Too many nested conditions.</strong>

Try to keep you nested if conditions down to as little as possible. More than 3 may mean you could be short-circuiting, or the method is trying to do too much.

<strong>Too much setup.</strong>

If you are having to write many lines of code to setup a unit test method, this could be a sign that the method under test is trying to do too much. Could the method be split out, as per the Single Responsibility Principle, making for smaller, easier to test methods?

More tips to come in a later post...