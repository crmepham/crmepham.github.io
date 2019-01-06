---
ID: 464
post_title: >
  How to import a generic Github project
  as an Eclipse/Maven Dynamic Web project
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/programming/eclipse/how-to-import-a-generic-github-project-into-an-eclipse-maven-dynamic-web-project/
published: true
post_date: 2015-09-05 12:19:37
---
In this tutorial I will describe the steps necessary to successfully import a generic web project from Github into a Dynamic Web Maven Project in Eclipse.

The problem:
Previously I had been developing an application using IntelliJ IDEA (A great IDE), and used Git for version control along with it's .ignore file to ignore any IDE specific and unnecessary files. I also used Github as my remote git repository. Now I am on a new system without any local files and a new IDE - Eclipse. I want to be able to create an equivalent project by importing the application files that are being stored remotely in Github.

Unfortunately it isn't quite as straight forward as I would have liked, but here's how I did it.

<strong>Step 1) Create a new Git directory</strong>
Make sure you have <a href="https://git-scm.com/download/win">Git Bash</a> installed. Navigate to your desired local directory and create a new git repository here and remotely pull the application files stored remotely on Github.

<code>git init
git clone https://github.com/username/project.git
</code>

<strong>Step 3) Import General File System source</strong>
Firstly, rename the "src" file to "srcold", then in Eclipse go to File -> Import -> General -> File System. Select the directory of the new git repository you created, and if not already selected - select all relevant files underneath, and complete the wizard.

Eclipse will create new "src" and "WebContent" folders as well as other Eclipse directories and files. You now need to delete the src folder and rename your "srcold" back to "src" and move any files inside an existing "web" or similarly named equivalent of Eclipses "WebContent" folder into the new folder. Now restart Eclipse.

Assuming you have Eclipses "Git" and "Team Synchronizing" plugins installed (I believe these come pre-installed in "Eclipse for JavaEE Developers"), but if not, you can easily install them through the "Eclipse Marketplace".

<strong>Step 4) Maven-ify it!</strong>
To convert the project into a Maven Project, simply right-click the project folder and click "Configure" -> "Convert to Maven Project...". You will then be able to add dependencies as normal.

You should have a file structure similar to this:
[caption id="attachment_468" align="aligncenter" width="366"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2015/09/Capture.png"><img src="http://chrismepham.co.uk/blog/wp-content/uploads/2015/09/Capture.png" alt="Eclipse Maven project" width="366" height="437" class="size-full wp-image-468" /></a> Eclipse Maven project[/caption]

You will notice in the above diagram that some of the directories have little icons on them which mean they are being tracked by the Git plugin and are currently in sync with the Git repository. Let's test the Eclipse remote Git repository functionality.

<strong>Step 5) Push to existing remote Git repository</strong>
When I started I manually created a local git repository and cloned my remote Github repository. Because of that I now do not need to configure Eclipse. Make a simple change to one of your projects files and select the "Team Synchronizing" view. You may need to click the "Synchronize Git" button in the top-left pane. Next click the "+" button and it will show you all the differences between your local files and the local git repository. Now you can either commit individual files by right-clicking them or right-click the project folder and click "commit". Next enter a commit message and make sure the files are selected at the bottom, and the click "commit and push". You should now see that repository has updated at Github.com. 

<strong>Additional</strong>
To do the equivalent of SVN's "revert" you need to right-click on the project folder in "Java EE" view and select "Team" -> "Reset", then select "Hard" under "reset type" and click "reset". This will revert all changes made since the last push. Granted it isn't as helpful as SVN's "revert" which allows you to revert individual files.