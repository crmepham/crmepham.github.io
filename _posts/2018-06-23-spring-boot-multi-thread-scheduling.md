---
ID: 1009
post_title: Spring Boot multi-thread scheduling
author: crm
post_excerpt: ""
layout: post
permalink: >
  http://chrismepham.co.uk/blog/programming/spring-boot-multi-thread-scheduling/
published: true
post_date: 2018-06-23 13:14:25
---
Spring Boot provides impressive <a href="https://spring.io/guides/gs/scheduling-tasks/">scheduling</a> functionality out-of-the-box. To install it all you need to do is include the Spring Boot Starter dependency in your Maven project:
<pre class="EnlighterJSRAW" data-enlighter-language="xml">&lt;dependency&gt;
    &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
    &lt;artifactId&gt;spring-boot-starter&lt;/artifactId&gt;
&lt;/dependency&gt;</pre>
<strong>Configuration</strong>

By default Spring Boot will use just a single thread for all scheduled tasks to run on. This is not ideal, because these tasks will be blocking. Instead we will configure the scheduler to run each scheduled tasks on a separate thread (if there is enough threads available).
<pre class="EnlighterJSRAW" data-enlighter-language="java">import org.springframework.context.annotation.Configuration;
import org.springframework.scheduling.annotation.SchedulingConfigurer;
import org.springframework.scheduling.concurrent.ThreadPoolTaskScheduler;
import org.springframework.scheduling.config.ScheduledTaskRegistrar;

/**
 * Configures the scheduler to allow multiple concurrent pools.
 * Prevents blocking.
 */
@Configuration
public class SchedulerConfig implements SchedulingConfigurer
{
    /**
     * The pool size.
     */
    private final int POOL_SIZE = 10;

    /**
     * Configures the scheduler to allow multiple pools.
     *
     * @param taskRegistrar The task registrar.
     */
    @Override
    public void configureTasks(ScheduledTaskRegistrar taskRegistrar)
    {
        ThreadPoolTaskScheduler threadPoolTaskScheduler = new ThreadPoolTaskScheduler();

        threadPoolTaskScheduler.setPoolSize(POOL_SIZE);
        threadPoolTaskScheduler.setThreadNamePrefix("scheduled-task-pool-");
        threadPoolTaskScheduler.initialize();

        taskRegistrar.setTaskScheduler(threadPoolTaskScheduler);
    }
}</pre>
In the above example, we have created a new configuration class which extends <em>SchedulingConfigurer</em>. This has allowed us to configure a task scheduler, and pass in the pool size we want to use.

<strong>Scheduling tasks</strong>

To create a scheduled task, all you need to do is annotate a method as follows:
<pre class="EnlighterJSRAW" data-enlighter-language="java">@Scheduled(fixedRate = 60000, initialDelay = 60000)
public void databaseCleanup()
{
    databaseCleanupService.clean();
}</pre>
In the above example, the <em>databaseCleanup()</em> method will be called once every minute, with an initial delay (after the application has started) of 1 minute. Instead of a fixed rate, you could instead use a cron expression.

&nbsp;