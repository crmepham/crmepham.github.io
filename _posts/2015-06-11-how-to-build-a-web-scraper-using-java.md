<strong>What is a web scraper?</strong>

Web scraping is a term used to describe the various methods for automating the process of retrieving large amounts of data from websites that don't provide a service (usually an API) for allowing a user to store data from a website locally.

There is an extremely large amount of data online, but not all websites make it easy for users to access this data easily.

We have all been in the situation where we are searching for images of one thing or another. We go to a website, find the image, right click on it and click "Save Image As" to store it on our desktop. We do this a few more times by visiting different websites, and eventually we have a collection of images of our favourite celebrity.

A web scraper can do this same thing automatically, a lot faster, retrieving a far greater number of images.

One example of data scraping is Google's Image search.

When you type in your image search criteria, Google scours the worlds websites reading all kinds of image attributes, matching the criteria you specified, and providing all of the relevant images in a paginated website. Google has used a web scraper to retrieve the image URI, title, description and website for each image, and used this data to display each image and relevant information.

Another example is one of the many comparison websites that exist. Today you can go to a comparison website to compare numerous insurance websites based the information you provide, to find the best quote. You provide the information about yourself and the web scraper will submit this data to a multitude of insurance websites. It will retrieve each websites quote and all the quotes will then be listed on the comparison website, usually ordered by which is cheapest.

In this post I will give you a brief example of how to create a web scraper, using Java, to retrieve my top five Github repository titles and descriptions and save them to a text file.

<strong>What is Jsoup?</strong>

<a href="http://jsoup.org/" target="_blank">Jsoup </a>is Java Application Programming Interface (API) which provides a set of simple methods for reading and extracting data from HTML webpages. It implements the HTML5 specification which enables you to select HTML elements the same way you would using CSS. making DOM traversal very easy.

<strong>Simple Jsoup implementation</strong>

In this example I will utilize two basic classes. One is used to crawl a website using a single HTML selector per object. The second is used to combine each crawler and generate a list to be written to a text file.

This program can be run from the command line. It requires 4 arguments:

1. jsoup HTTP communication method (GET/POST)
2. website URI
3. HTML element identifier 1
4. HTML element identifier 2

This is how the program can be run from the command line or using cronjob:

<strong>java get https://github.com/final60/ .repo .repo-description</strong>

Read the code comments to understand what is happening.

<strong>Main webCrawler class.</strong>
<script src="https://gist.github.com/final60/27df7ed49c59cd793221.js"></script>

<strong>Crawler Class</strong> that does the crawling per HTML element
<script src="https://gist.github.com/final60/c2c334905a75b7e539df.js"></script>

<strong>FileGenerator Class</strong> that collates the two Crawler object lists and generates a text file
<script src="https://gist.github.com/final60/ebd0675d207cd46a5b55.js"></script>

This is the console output:
[caption id="attachment_205" align="aligncenter" width="1180"]<a href="http://chrismepham.co.uk/blog/wp-content/uploads/2015/06/consoleoutput.png"><img src="http://chrismepham.co.uk/blog/wp-content/uploads/2015/06/consoleoutput.png" alt="console output" width="1180" height="268" class="size-full wp-image-205" /></a> console output[/caption]

As you can see, it is relatively easy to create a web crawler. The above program could be improved to allow an arbitrary number of HTML elements to crawl for. You could save the output to a database for instant access via your own website. Provided you know the URI structure and the element identifiers.
