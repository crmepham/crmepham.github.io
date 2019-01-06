---
ID: 1004
post_title: >
  Implement a Back-off and Retry mechanism
  using Spring Retry
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/programming/implement-a-back-off-and-retry-mechanism-using-spring-retry/
published: true
post_date: 2018-06-23 12:57:34
---
It may be necessary, especially when dealing with 3rd party API integrations, to implement a "Back-off and retry" mechanism, in cases where, for example, the 3rd party API becomes non-responsive, or lock's you out.

I recently had an issue where an application I had developed was pinging the AWS API to often. This resulted in AWS throttling the amount that my AWS account could use the API. However, the throttle threshold and the duration that the throttling persists could not be known.

In cases like this it is useful to delay the next time your application attempts to perform an action where the reliability or responsiveness of the external API cannot be guaranteed. This is called the "Back-off". After you have paused the next attempt for a period of time, you will want your application to retry the action it previously failed to complete.

Spring has an excellent library called <a href="http://www.baeldung.com/spring-retry">Spring Retry</a> that can automate the "Back-off and Retry" mechanism for us.

<strong>Install Spring Retry</strong>

Add the following Maven dependencies:
<pre class="EnlighterJSRAW" data-enlighter-language="xml">&lt;dependency&gt;
    &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
    &lt;artifactId&gt;spring-boot-starter-aop&lt;/artifactId&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
    &lt;groupId&gt;org.springframework.retry&lt;/groupId&gt;
    &lt;artifactId&gt;spring-retry&lt;/artifactId&gt;
    &lt;version&gt;1.1.2.RELEASE&lt;/version&gt;
&lt;/dependency&gt;</pre>
<strong>Configure the RetryTemplate</strong>
<pre class="EnlighterJSRAW" data-enlighter-language="java">import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.retry.backoff.ExponentialBackOffPolicy;
import org.springframework.retry.policy.SimpleRetryPolicy;
import org.springframework.retry.support.RetryTemplate;

/**
 * Configuration class for Spring-Retry.
 */
@Configuration
public class RetryConfiguration
{
    @Bean
    public RetryTemplate retryTemplate() {
        SimpleRetryPolicy retryPolicy = new SimpleRetryPolicy();
        retryPolicy.setMaxAttempts(5);

        ExponentialBackOffPolicy backOffPolicy = new ExponentialBackOffPolicy();
        backOffPolicy.setInitialInterval(10000);
        backOffPolicy.setMaxInterval(60000);
        backOffPolicy.setMultiplier(2);

        RetryTemplate template = new RetryTemplate();
        template.setRetryPolicy(retryPolicy);
        template.setBackOffPolicy(backOffPolicy);

        return template;
    }
}</pre>
Notice that you can configure the following:
<ol>
 	<li>maxAttempt - This is the maximum number of times that Spring Retry will attempt the action.</li>
 	<li>initialInterval - The initial "back-off" period in milliseconds.</li>
 	<li>maxInterval - The maximum "back-off" duration in milliseconds.</li>
 	<li>multiplier - Will be used when determining the next "back-off" duration. If you have this set to 2 and start with a 10 second interval, the second interval will be 20 seconds, and the third will be 40 seconds. The fourth would not be 80 seconds, however, it will be 60 seconds, because that is the maximum interval we specified.</li>
</ol>
<strong>Implement the retryTemplate</strong>
<pre class="EnlighterJSRAW" data-enlighter-language="java">@Autowired
private RetryTemplate retryTemplate;

@Autowired
private HttpService httpService;

[...]

public static void main() {
    retryTemplate.execute(context -&gt; attemptHttpRequest());
}</pre>
Above we have wired in the retryTemplate and called the execute() method on it within a Lamda expression.
<pre class="EnlighterJSRAW" data-enlighter-language="java">public void attemptHttpRequest() throws Exception {
    
    System.out.println("Got here");
    
    throw new Exception();
}</pre>
The method being called will throw an exception on purpose to demonstrate the "back-off and retry" mechanism. Put a break-point on the sout and debug the above. You should notice that after the exception is thrown, the method will be called again after 10 seconds, and then again after 20 seconds, and so on.

If an exception is thrown on the final attempt then the program will continue as normal and will not retry. Be aware that this mechanism does block the thread it is running on.