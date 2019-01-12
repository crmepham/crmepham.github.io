---
classes: wide
tags: [slack, api, integration]
---
Slack has made integration extremely easy! This tutorial will show you how to create a Slack app that will send messages to a specific Slack channel.

<strong>Pre-requisites</strong>

1. This tutorial assumes you have already setup your Slack workstations and that you have admin privileges.

<strong>Setup</strong>

1. Navigate to <a href="https://api.slack.com/apps">https://api.slack.com/apps</a> and click on the "Create new App" button.

2. Choose a name for your new app. and the workstation that you want to associate it with.

<img class="aligncenter size-full wp-image-950" src="http://chrismepham.co.uk/blog/wp-content/uploads/2018/06/slack-create.png" alt="" width="1020" height="595" />

3. Once created click on the "Incoming Webhooks" link under the "Add features and functionality" section of the "Basic Information" page for the newly created app.

4. Activate the "Incoming Webhooks" functionality, select the channel you wish messages from this app. to be posted to, and then click "Authorize" button.

<img class="aligncenter size-full wp-image-954" src="http://chrismepham.co.uk/blog/wp-content/uploads/2018/06/slack-authorize.png" alt="" width="628" height="418" />

<strong>That's it!</strong>

Now all you need to do is post data to the Webhook URI that was created. Here are a couple of different methods for doing this:

1. Using Curl:
<pre class="EnlighterJSRAW" data-enlighter-language="shell">curl -X POST -H 'Content-type: application/json' --data '{"text":"Hello, World!"}' https://hooks.slack.com/services/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</pre>
2. Using JAVA:
<pre class="EnlighterJSRAW" data-enlighter-language="java">package com.crm.api.slack;

import com.crm.utils.HttpUtils;
import junit.framework.TestCase;

import java.io.IOException;
import java.util.HashMap;
import java.util.Map;

public class SlackApiManualTest extends TestCase {

  private static final String CHANNEL_URL_MONITOR = "https://hooks.slack.com/services/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";

  public void testSendMessage() {
    Map&lt;String, String&gt; headers = new HashMap&lt;String, String&gt;();
    headers.put("Content-Type", "application/json");
  
    try {
      HttpUtils.post(CHANNEL_URL_MONITOR, "{\"text\":\"A message\"}", headers, HttpUtils.METHOD_POST);
  
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
  
  }
}</pre>
&nbsp;
