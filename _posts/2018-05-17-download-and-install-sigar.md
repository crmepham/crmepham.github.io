---
ID: 932
post_title: Download and install Sigar
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/programming/download-and-install-sigar/
published: true
post_date: 2018-05-17 09:50:28
---
<a href="https://github.com/hyperic/sigar">Sigar</a> is a Java library that allows you to monitor various aspects of your system. Including Network, Memory, and CPU.

To use Sigar in you Java application follow these steps:

1. Copy the following Maven dependency into your project:
<pre class="EnlighterJSRAW" data-enlighter-language="xml"> &lt;dependency&gt;
 &lt;groupId&gt;org.gridkit.lab&lt;/groupId&gt;
 &lt;artifactId&gt;sigar-lib&lt;/artifactId&gt;
 &lt;version&gt;1.6.4&lt;/version&gt;
&lt;/dependency&gt;</pre>
2. Download the necessary system files:

<em>Note: This example will demonstrate how with the Linux based .so file. Make sure you copy across the correct file for you system. If you are unsure, there is no harm in copying all of the .dll and .so files across.</em>
<pre class="EnlighterJSRAW" data-enlighter-language="shell"> wget https://netcologne.dl.sourceforge.net/project/sigar/sigar/1.6/hyperic-sigar-1.6.4.tar.gz
 tar xvf hyperic-sigar-1.6.4.tar.gz
 cd hyperic-sigar-1.6.4
 sudo cp sigar-bin/lib/libsigar-amd64-linux.so /usr/lib</pre>
3. Use Sigar in your application
<pre class="EnlighterJSRAW" data-enlighter-language="java">@Test
public void testGetSearchResultsGroupedByEntity() throws Exception {
  
  Sigar sigar = new Sigar();
  
  System.out.println(sigar.getCpu().getTotal());
}</pre>
&nbsp;