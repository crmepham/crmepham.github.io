When you start developing software professionally you will want to ensure that you are writing the best code you can be. Luckily, there are a handful of tools that can help you with. These tools can be configured to automatically check your code style and look for potential bugs in your code, when you build you project.

I have selected a handful of tools which I currently use professionally, and will briefly summarise each of them. Each of them can be used with Mavens reporting framework, to produce easy to view reports.
<ol>
 	<li>CheckStyle</li>
 	<li>Findbugs</li>
 	<li>PMD and CPD</li>
</ol>
<strong>CheckStyle</strong>
<blockquote>Checkstyle is a development tool to help programmers write Java code that adheres to a coding standard. It automates the process of checking Java code to spare humans of this boring (but important) task. This makes it ideal for projects that want to enforce a coding standard.

Checkstyle is highly configurable and can be made to support almost any coding standard.</blockquote>
To install <a href="https://maven.apache.org/plugins/maven-checkstyle-plugin/">CheckStyle</a> simply add the following reporting plugin to your pom.xml file:
<pre class="EnlighterJSRAW" data-enlighter-language="xml">[...]
&lt;reporting&gt;
   &lt;plugins&gt;
      &lt;plugin&gt;
         &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
         &lt;artifactId&gt;maven-checkstyle-plugin&lt;/artifactId&gt;
         &lt;reportSets&gt;
            &lt;reportSet&gt;
               &lt;reports&gt;
                  &lt;report&gt;checkstyle&lt;/report&gt;
               &lt;/reports&gt;
            &lt;/reportSet&gt;
         &lt;/reportSets&gt;
      &lt;/plugin&gt;
   &lt;/plugins&gt;
&lt;/reporting&gt;
[...]</pre>
Then run <code class="EnlighterJSRAW" data-enlighter-language="shell">mvn site</code> which will produce the checkstyle report. The report can be accessed via <em>target/site/checkstyle.html</em> and should look similar to the following:

<img class="aligncenter size-full wp-image-986" src="http://chrismepham.co.uk/blog/wp-content/uploads/2018/06/checkstyle.png" alt="" width="1759" height="685" />

The default ruleset that is used is <em>sun_checks.xml</em> which will check for a ridiculous number of rules. when you get used to using Checkstyle you will probably want to create your own custom ruleset with a specific subset of rules that you want to enforce for your projects.

<strong>FindBugs</strong>
<blockquote>FindBugs looks for bugs in Java programs. It is based on the concept of bug patterns. A bug pattern is a code idiom that is often an error. Bug patterns arise for a variety of reasons:

Difficult language features
Misunderstood API methods
Misunderstood invariants when code is modified during maintenance
Garden variety mistakes: typos, use of the wrong boolean operator

FindBugs uses static analysis to inspect Java bytecode for occurrences of bug patterns. We have found that FindBugs finds real errors in most Java software. Because its analysis is sometimes imprecise, FindBugs can report false warnings, which are warnings that do not indicate real errors. In practice, the rate of false warnings reported by FindBugs is generally less than 50%.</blockquote>
To install <a href="https://gleclaire.github.io/findbugs-maven-plugin/usage.html">FindBugs</a> simply add the following report plugin to your projects pom.xml:
<pre class="EnlighterJSRAW" data-enlighter-language="xml">&lt;reporting&gt;
  &lt;plugins&gt;
    &lt;plugin&gt;
      &lt;groupId&gt;org.codehaus.mojo&lt;/groupId&gt;
      &lt;artifactId&gt;findbugs-maven-plugin&lt;/artifactId&gt;
    &lt;/plugin&gt;
  &lt;/plugins&gt;
&lt;/reporting&gt;</pre>
You can then generate your projects reports (FindBugs being one of them) by using the <code class="EnlighterJSRAW" data-enlighter-language="shell">mvn site</code> command again.

Access the report the same way you did with CheckStyle (via the <em>target/site/</em> directory).

<strong>PMD and CPD</strong>
<blockquote>PMD is a source code analyzer. It finds common programming flaws like unused variables, empty catch blocks, unnecessary object creation, and so forth. It supports Java, JavaScript, Salesforce.com Apex and Visualforce, PLSQL, Apache Velocity, XML, XSL.

Additionally it includes CPD, the copy-paste-detector. CPD finds duplicated code in Java, C, C++, C#, Groovy, PHP, Ruby, Fortran, JavaScript, PLSQL, Apache Velocity, Scala, Objective C, Matlab, Python, Go, Swift and Salesforce.com Apex and Visualforce.</blockquote>
Install <a href="https://maven.apache.org/plugins/maven-pmd-plugin/">PMD and CPD</a> by adding the following plugin to your projects pom.xml:
<pre class="EnlighterJSRAW" data-enlighter-language="xml">&lt;reporting&gt;
  &lt;plugins&gt;
    &lt;plugin&gt;
      &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
      &lt;artifactId&gt;maven-pmd-plugin&lt;/artifactId&gt;
    &lt;/plugin&gt;
  &lt;/plugins&gt;
&lt;/reporting&gt;</pre>
When your projects build is complete you can view the results of PMD and CPD from the projects site reporting section (the same as the above reporting tools).

Let's take a look at a couple of violations:

<img class="aligncenter size-full wp-image-992" src="http://chrismepham.co.uk/blog/wp-content/uploads/2018/06/pmd-imports.png" alt="" width="1065" height="156" />

Let's check the code that the first violation is referring to. It it in class BlockchainApiHandler on line 12:

<img class="aligncenter size-full wp-image-993" src="http://chrismepham.co.uk/blog/wp-content/uploads/2018/06/pmd-imports-code.png" alt="" width="754" height="261" />

As you can see, it correctly identified the unused import, and also the unused constants!

Let's look at another one:

<img class="aligncenter size-full wp-image-994" src="http://chrismepham.co.uk/blog/wp-content/uploads/2018/06/pmd-errors1.png" alt="" width="767" height="256" />

And let's check the code:

<img class="aligncenter size-full wp-image-995" src="http://chrismepham.co.uk/blog/wp-content/uploads/2018/06/unused-param.png" alt="" width="488" height="172" />

<img class="aligncenter size-full wp-image-996" src="http://chrismepham.co.uk/blog/wp-content/uploads/2018/06/useless-parenthesis.png" alt="" width="791" height="184" />

Yup, both very valid violations.

As you can see, these kinds of tools are extremely useful. They will help you to keep your code clean and robust, and they automate the entire process. If you are coding at a professional level you should be using these tools.

<strong>Jacoco</strong>
<blockquote><em>JaCoCo is a free code coverage library for Java, which has been created by the EclEmma team based on the lessons learned from using and integration existing libraries for many years.</em></blockquote>
Install <a href="https://www.jacoco.org/jacoco/">Jacoco</a> by adding the following to your &lt;em&gt;pom.xml&lt;/em&gt;:
<pre class="EnlighterJSRAW" data-enlighter-language="xml">&lt;plugin&gt;
    &lt;groupId&gt;org.jacoco&lt;/groupId&gt;
    &lt;artifactId&gt;jacoco-maven-plugin&lt;/artifactId&gt;

    &lt;configuration&gt;
        &lt;excludes&gt;
            &lt;exclude&gt;**/ListenerCallQueue.*&lt;/exclude&gt;
            &lt;exclude&gt;**/*PerListenerQueue.*&lt;/exclude&gt;
        &lt;/excludes&gt;
    &lt;/configuration&gt;
&lt;/plugin&gt;</pre>
Then run <code class="EnlighterJSRAW" data-enlighter-language="shell">mvn clean install</code> and <code class="EnlighterJSRAW" data-enlighter-language="null">mvn jacoco:report</code>

The Jacoco code coverage report will then be generated which you can access from &lt;em&gt;/target/site/jacoco&lt;/em&gt; and will look something like the following:

<img class="aligncenter size-full wp-image-1001" src="http://chrismepham.co.uk/blog/wp-content/uploads/2018/06/jacoco.png" alt="" width="1027" height="229" />

Any code highlighted in <span style="color: #339966;">green</span> has been covered by unit tests.

Any code highlighted in <span style="color: #ff0000;">red</span> has not been covered by unit tests.

Any code highlighted in <span style="color: #ffcc00;">yellow</span> has only been partially covered by unit tests. This will usually be conditionals, where only one of the conditions has been covered.
