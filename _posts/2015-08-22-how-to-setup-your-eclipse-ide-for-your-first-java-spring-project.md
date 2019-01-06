---
ID: 384
post_title: >
  How to setup your Eclipse IDE for your
  first Java Spring project
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/guide/how-to-setup-your-eclipse-ide-for-your-first-java-spring-project/
published: true
post_date: 2015-08-22 12:48:39
---
This tutorial will cover the process of setting up your newly installed Eclipse IDE for Java Spring development. This tutorial assumes you have already downloaded and installed <a href="https://glassfish.java.net/download.html#gfoseTab" target="_blank">Glassfish 4</a> and <a href="https://eclipse.org/downloads/" target="_blank">Eclipse for EE Developers</a>.

<strong>What is Glassfish?</strong>
Glassfish is a Java EE server implementation by Oracle that supports Enterprise technologies such as Servlets, JavaBeans, JSF and many more technologies. Basically all the stuff your application will need to persist on the web. An alternative to Glassfish is <a href="http://tomee.apache.org/tomcat-java-ee.html" target="_blank">TomEE</a> which adds Enterprise application support to the already popular Tomcat container.

<strong>Can't I just use Tomcat?</strong>
Yes you can! TomEE and GlassFish are convenient in that they support Enterprise applications "out of the box", but the down side to this is that they tend to be bulky and may contain many technologies that you might never use. This attributes to a slower code -> deploy -> test cycle. 

In many instances you may only need a Tomcat container with a few additional libraries added to it, plus some additional configuration. Right now, however, we are focused on preparing our work station for the type of Enterprise productivity that will be required in a commercial environment.

<strong>Add Spring IDE to Eclipse</strong>
Click "Help" -> "Eclipse Marketplace", and search for Spring IDE. Click "install". This will install a number of plugins that will make your life easier when developing Spring applications.

<strong>Add Spring maven dependencies</strong>
Next we will need the Spring API. Spring is actually separated into a number of modules, depending on the type of development we are doing.

Because we installed "Eclipse for Java EE developers" we already have Maven installed!

Firstly, create a new "Maven Project" by clicking "File" -> "New" -> "Other..." and selecting "Maven Project" under the "Maven" folder. The following wizard will suggest that you use the "quickstart" archetype. An archetype is basically a way of organizing your projects folder structure. We will stick with version 1.1. 

Next you will need to give the project a "Group Id" and "Artifact Id". For the purposes of the tutorial use the group id: com.crm.springexample, and the artifact id: spring-tutorial. Click Finish and give Maven a moment to finish building the file structure and download any default dependencies.

Your new Maven project should look similar to this:
[caption id="attachment_394" align="aligncenter" width="408"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2015/08/maven-project1.png"><img src="http://chrismepham.co.uk/blog/wp-content/uploads/2015/08/maven-project1.png" alt="maven project structure" width="408" height="236" class="size-full wp-image-394" /></a> maven project structure[/caption]

Now we have a Maven project, let's Spring-ify it by adding the Spring modules to the project using Maven.

<strong>Adding the Spring API to a Maven project</strong>
Start by double-clicking the "pom.xml" (Project Object Model) file. You should be presented with various tabs, allowing you to modify your POM file using a convenient GUI instead of editing a traditional xml file. Again, this is thanks to installing the "Eclipse for Java EE Developers" version of the IDE.

Click on the "Dependencies" tab. You'll notice that Maven already added the Junit library. Let's add the first Spring library now by clicking on "Add". In the new window you are given the option of inputting the Group id, Artifact id and Version explicitly, or by searching for the library underneath. Search for "springframework". A long list of libraries should present themselves. The ones you want are under org.springframework. I don't recommend downloading the full spring package, because it is a much older version. To start with - add the spring-core, spring-context and spring-beans artifacts individually.
[caption id="attachment_396" align="aligncenter" width="536"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2015/08/maven-adding-spring.png"><img src="http://chrismepham.co.uk/blog/wp-content/uploads/2015/08/maven-adding-spring.png" alt="maven adding spring" width="536" height="717" class="size-full wp-image-396" /></a> maven adding spring[/caption]

Once you have added the Spring artifacts, save the pom file and give Maven a minute to download them. Once finished you will notice that Maven conveniently downloads any dependencies that the artifacts have.

Finally, because we added the Spring IDE plugin, we can now easily create a new Spring Bean configuration file by right-clicking on the project folder and selecting "New" -> "Other..." -> "Spring" -> "Spring Bean Configuration File". Give the configuration file a name and add any xml namespaces to it.

You are now ready to start wiring your Spring beans.