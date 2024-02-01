<p>
  This documentation is for the Countly Java SDK version 23.10.X. The SDK source
  code repository can be found
  <a href="https://github.com/Countly/countly-sdk-java" target="_blank" rel="noopener noreferrer">here.</a>
</p>
<div class="callout callout--info">
  <p>
    Click
    <a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-and-Installing-SDKs#h_01H9QCP8G8QD0W9EMHT11F2N8P" target="_self" rel="undefined">here, </a>to
    access the documentation for older SDK versions.
  </p>
</div>
<p>
  The Countly Java SDK minimum supported target version is Java 8.
</p>
<p>
  To examine the example integrations please have a look
  <a href="#h_01HNFH7ZFRE3CKRCTZE6EZWM86">here.</a>
</p>
<h1 id="h_01HABV0K6BZ251ANK02RZK3Z5H">Adding the SDK to the Project</h1>
<p>
  SDK is hosted on MavenCentral, more info can be found
  <a href="https://search.maven.org/artifact/ly.count.sdk/java" target="_self" rel="undefined">here</a>
  and
  <a href="https://search.maven.org/artifact/ly.count.sdk/core" target="_self">here</a>.
  To add it, you first have to add the MavenCentral repository. For Gradle you
  would do it something like this:
</p>
<pre>buildscript {
  repositories {
    mavenCentral()
  }
}</pre>
<p>The dependency can be added as:</p>
<pre>dependencies {
  implementation "ly.count.sdk:java:23.10.0"
}</pre>
<p>Or as:</p>
<pre><code class="xml">&lt;dependency&gt;
  &lt;groupId&gt;ly.count.sdk&lt;/groupId&gt;
  &lt;artifactId&gt;java&lt;/artifactId&gt;
  &lt;version&gt;23.10.0&lt;/version&gt;
  &lt;type&gt;pom&lt;/type&gt;
&lt;/dependency&gt;</code></pre>
<h1 id="h_01HABV0K6CDY5FSWH5QBHTT79R">SDK Integration</h1>
<h2 id="h_01HABV0K6C4H1G71VV85BDXV91">Minimal Setup</h2>
<p>
  Before you can use any functionality, you have to initiate the SDK.
</p>
<p>
  The shortest way to initiate the SDK is with this code snippet:
</p>
<pre><code class="java hljs">File targetFolder = new File("d:\\__COUNTLY\\java_test\\");

Config config = new Config("http://YOUR.SERVER.COM", "YOUR_APP_KEY", targetFolder)
  .enableTestMode()
  .setLoggingLevel(Config.LoggingLevel.DEBUG)
  .enableFeatures(Config.Feature.Events, Config.Feature.Sessions, Config.Feature.CrashReporting, Config.Feature.UserProfiles)
  .setDeviceIdStrategy(Config.DeviceIdStrategy.UUID);

Countly.instance().init(config);</code></pre>
<p>
  This code will initiate the SDK in test mode with logging enabled. Here you would
  also need to provide your application key and server URL. Please check
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KX44C9SF48WRPQNCP3">here</a>
  for more information on how to acquire your application key (APP_KEY) and server
  URL.
</p>
<div class="callout callout--info">
  <p>
    If you are in doubt about the correctness of your Countly SDK integration
    you can learn about the verification methods from
    <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KXE6YKVETHDWPP8J3K" target="blank">here</a>.
  </p>
</div>
<h2 id="h_01HABV0K6C4TED33TF2K40S71H">SDK Data Storage</h2>
<p>
  Countly SDK stores serialized versions of the following classes:
  <code>InternalConfig</code>, <code>SessionImpl</code>, <code>EventQueue</code>,
  <code>RequestImpl</code>, <code>CrashImpl</code>, <code>UserImpl</code>
  <code>TimedEvents</code>. All those are stored in device memory, in binary form,
  in separate files with filenames prefixed with <code>[CLY]_</code>.
</p>
<h2 id="h_01HABV0K6CHWK7XBEWV8ZM5SB7">SDK Notes</h2>
<h3 id="h_01HABV0K6C87QCRAFK9DD0PYT4">Test Mode</h3>
<p>
  To ensure correct SDK behavior, please use
  <code>Config.enableTestMode()</code> when your app is in development and testing.
  In test mode, Countly SDK raises <code>RuntimeException</code>s whenever is in
  an inconsistent state. Once you remove <code>Config.enableTestMode()</code> call
  from your initialization sequence, SDK stops raising any
  <code>Exception</code>s and switches to logging errors instead (if logging wasn't
  specifically turned off). Without having test mode on during development you
  may encounter some important issues with data consistency in production.
</p>
<h1 id="h_01HD19HWGTN49PGHRQ8WPA2RA6">SDK Logging Mode</h1>
<p>
  The first thing you should do while integrating our SDK is enable logging. If
  logging is enabled, the Countly Java SDK will print out debug messages about
  its internal state and encountered problems. The SDK will print these debug messages
  to the console.
</p>
<p>
  Set <code class="java">setLoggingLevel</code> on the config object to enable
  logging:
</p>
<pre><code class="java hljs">File targetFolder = new File("d:\\__COUNTLY\\java_test\\");

Config config = new Config("http://YOUR.SERVER.COM", "YOUR_APP_KEY", targetFolder)
  .setLoggingLevel(Config.LoggingLevel.DEBUG)
  .enableFeatures(Config.Feature.Events, Config.Feature.Sessions, Config.Feature.CrashReporting, Config.Feature.UserProfiles)
  .setDeviceIdStrategy(Config.DeviceIdStrategy.UUID);</code></pre>
<p>
  This logging level would not influence the log listener. That will always receive
  all the printed logs event if the logging level is "OFF."
</p>
<h2 id="h_01GVR02HH6X27TPH3MS6TE08AT">Log Listener</h2>
<p>
  To listen to the SDK's internal logs, you can call <code>setLogListener</code><span> on the <code>Config</code> Object. If set, SDK will forward its internal logs to this listener regardless of SDK's <code>loggingLevel</code> . </span>
</p>
<pre><code class="java hljs">config.setLogListener(new LogCallback() {
  @Override
  public void LogHappened(String logMessage, Config.LoggingLevel logLevel) {
    //print log
  }
});</code></pre>
<h1 id="h_01HD1AJNNA11E9NMY0K0S5B3XN">Crash Reporting</h1>
<p>
  The Countly Java SDK has the ability to collect
  <a href="/hc/en-us/articles/4404213566105" target="_blank" rel="noopener noreferrer">crash reports</a>,
  which you may examine and resolve later on the server. The SDK can collect unhandled
  exceptions by default if the consent for crash reporting is given. You can reach
  all crash-related functionality from the returned interface on:
</p>
<pre><code>Countly.instance().crashes()</code></pre>
<h2 id="h_01HG0S0PNJB87NG192K43SP5CS">Automatic Crash Handling</h2>
<p>
  Automatic crash handling is enabled by default. To disable it call this method
  on the config object during initialization:
</p>
<pre>config.disableUnhandledCrashReporting();</pre>
<h2 id="h_01HD1AK4K4M40M1J7W0R50QGQM">Handled Exceptions</h2>
<p>
  <span>You might catch an exception or similar error during your app’s runtime. To report them use the following method</span>:
</p>
<pre><code class="java">Countly.instance().crashes().recordHandledException(Throwable t);

// Or you can also add segment to be recorded with the error
Countly.instance().crashes().recordHandledException(Throwable t, Map&lt;String, Object&gt; segment);</code></pre>
<p>
  <span>If you have handled an exception and it turns out to be fatal to your app, you may use this call:</span>
</p>
<pre><code class="java">Countly.instance().crashes().recordUnhandledException(Throwable t);

// Or you can also add segment to be recorded with the error
Countly.instance().crashes().recordUnhandledException(Throwable t, Map&lt;String, Object&gt; segment);</code></pre>
<h2 id="h_01HG0S5QWDC5WEQSV0W724XCG4">Crash Breadcrumbs</h2>
<p>
  Throughout your app you can leave crash breadcrumbs which would describe previous
  steps that were taken in your app before the crash. After a crash happens, they
  will be sent together with the crash report.
</p>
<p>Following command adds crash breadcrumb:</p>
<pre><code class="java hljs">Countly.instance().crashes().addCrashBreadcrumb(String record);</code></pre>
<p>
  The maximum breadcrumb limit is 100. To change the maximum limit use this method
  during initialization:
</p>
<pre>config.setMaxBreadcrumbCount(int maxBreadcrumbCount);</pre>
<h1 id="h_01HABV0K6C0FGCV0NJV59ZFJSC">Events</h1>
<p>
  <a href="/hc/en-us/articles/4403721560857" target="_blank" rel="noopener noreferrer">Events</a>
  in Countly represent some meaningful event user performed in your application
  within a <code>Session</code>. Please avoid recording everything like all taps
  or clicks users performed. In case you do, it will be very hard to extract valuable
  information from generated analytics.
</p>
<p>
  An <code>Event</code> object contains the following data types:
</p>
<ul>
  <li>
    <code>name</code>, or event key. Required. A unique string that identifies
    the event.
  </li>
  <li>
    <code>count</code> - number of times. Required, 1 by default. Like a number
    of goods added to the shopping basket.
  </li>
  <li>
    <code>sum</code> - sum of something, amount. Optional. Like a total sum of
    the basket.
  </li>
  <li>
    <code>dur</code> - duration of the event. Optional. For example how much
    time users spent checking out.
  </li>
  <li>
    <code>segmentation</code> - some data associated with the event. Optional.
    It's a Map&lt;String, Object&gt; which can be filled with arbitrary data
    like {"category": "Pants", "size": "M"}. The valid data types for segmentation
    are: "String", "Integer", "Double", "Boolean", "Long" and "Float". All other
    types will be ignored.
  </li>
</ul>
<h2 id="h_01HABV0K6CDJHPP9HBQG26BZYR">Recording Events</h2>
<p>
  The standard way of recording events is through your <code>Countly</code> instance's
  <code>events</code> interface:
</p>
<div>
  <pre><code class="java hljs">Map&lt;String, Object&gt; segmentation = new HashMap&lt;String, Object&gt;();
segmentation.put("Time Spent", 60);
segmentation.put("Retry Attempts", 60);

Countly.instance().events().recordEvent("purchase", segmentation, 2, 19.98, 35);</code></pre>
</div>
<p>
  The example above results in a new event being recorded in the current session.
  The event won't be sent to the server right away. Instead, Countly SDK will wait
  until one of the following happens:
</p>
<ul>
  <li>
    <code>Config.sendUpdateEachSeconds</code> seconds passed since begin or last
    update request in case of automatic session control.
  </li>
  <li>
    <code>Config.eventsBufferSize</code> events have been already recorded and
    not sent yet.
  </li>
  <li>
    <code>Session.update()</code> have been called by the developer.
  </li>
  <li>
    <code>Session.end()</code> have been called by the developer or by Countly
    SDK in case of automatic session control.
  </li>
</ul>
<p>
  <span>We have provided an example of recording a <strong>purchase</strong> event below. Here is a quick summary of the information with which each usage will provide us:</span>
</p>
<ul>
  <li>
    Usage 1: how many times the <strong>purchase</strong> event occurred.
  </li>
  <li>
    Usage 2: how many times the <strong>purchase</strong> event occurred + the
    total amount of those purchases.
  </li>
  <li>
    Usage 3: how many times the <strong>purchase</strong> event occurred + from
    which countries and application versions those purchases were made.
  </li>
  <li>
    Usage 4: how many times the <strong>purchase</strong> event occurred + the
    total amount, both of which are also available, segmented into countries
    and application versions.
  </li>
  <li>
    Usage 5: how many times the <strong>purchase</strong> event occurred + the
    total amount, both of which are also available, segmented into countries
    and application versions + the total duration of those events.
  </li>
</ul>
<p>
  <strong>1. Event key and count</strong>
</p>
<pre><code class="java hljs">Countly.instance().events().recordEvent("purchase", 1);</code></pre>
<p>
  <strong>2. Event key, count, and sum</strong>
</p>
<pre><code class="java hljs">Countly.instance().events().recordEvent("purchase", 1, 20.3);</code></pre>
<p>
  <strong>3. Event key and count with segmentation(s)</strong>
</p>
<pre><code class="java hljs">HashMap&lt;String, Object&gt; segmentation = new HashMap&lt;String, Object&gt;();
segmentation.put("country", "Germany");
segmentation.put("app_version", 1.0);

Countly.instance().events().recordEvent("purchase", segmentation, 1);</code></pre>
<p>
  <strong>4. Event key, count, and sum with segmentation(s)</strong>
</p>
<pre><code class="java hljs">HashMap&lt;String, Object&gt; segmentation = <span class="hljs-keyword">new</span> HashMap&lt;String, Object&gt;();
segmentation.put("country", "Germany");
segmentation.put("app_version", 1.0);

Countly.instance().events().recordEvent("purchase", segmentation, 1, 34.5);<br></code></pre>
<p>
  <strong>5. Event key, count, sum, and duration with segmentation(s)</strong>
</p>
<pre><code class="java hljs">HashMap&lt;String, Object&gt; segmentation = <span class="hljs-keyword">new</span> HashMap&lt;String, Object&gt;();
segmentation.put("country", "Germany");
segmentation.put("app_version", 1.0);

Countly.instance().events().recordEvent("purchase", segmentation, 1, 34.5, 5.3);<br></code></pre>
<p>
  <span>Those are only a few examples of what you can do with events. You may extend those examples and use Country, app_version, game_level, time_of_day, and any other segmentation that will provide you with valuable insights.</span>
</p>
<h2 id="h_01HABV0K6CAY109S796CY5P6DZ">Timed Events</h2>
<p>
  There is also a special type of <code>Event</code> supported by Countly - timed
  events. Timed events help you to track long continuous interactions when keeping
  an <code>Event</code> instance is not very convenient.
</p>
<p>The basic use case for timed events is following:</p>
<ul>
  <li>
    User starts playing a level "37" of your game, you call
    <code>Countly.instance().events().startEvent("LevelTime")</code> to start
    tracking how much time a user spends on this level. Also keep your segmentation
    values in a map like
  </li>
</ul>
<pre><code class="java hljs">HashMap&lt;String, Object&gt; segmentation = <span class="hljs-keyword">new</span> HashMap&lt;String, Object&gt;();
segmentation.put("level", 37);</code></pre>
<ul>
  <li>
    <span data-preserver-spaces="true">Then, something happens when the user is at that level; for example, the user buys some coins. Along with the regular "Purchase" event, you decide you want to segment the "LevelTime" event with purchase information. While ending the event, you also pass the sum value as the purchase amount to the function call.</span>
  </li>
  <li>
    <span data-preserver-spaces="true">Once the user stops playing, you need to stop this event and call:</span>
    <code>Countly.instance().events().endEvent("LevelTime",segmentation, 1, 9.99)</code>
  </li>
  <li>
    If you decide to cancel the event you can call:
    <code>Countly.instance().events().cancelEvent("LevelTime")</code>
  </li>
</ul>
<p>Once this event is sent to the server, you'll see:</p>
<ul>
  <li>
    how much time users spend on each level (duration per <code>level</code>
    segmentation);
  </li>
  <li>
    which levels are generating the most revenue (sum per <code>level</code>
    segmentation);
  </li>
  <li>
    which levels are not generating revenue at all since you don't show ad there
    (0 sums in <code>level</code> segmentation).
  </li>
</ul>
<p>
  With timed events, there is one thing to keep in mind: you have to end timed
  event for it to be recorded. Without <code>endEvent("LevelTime")</code> call,
  nothing will happen.
</p>
<h1 id="h_01HABV0K6C1HY4JZZHKT5A83DD">Sessions</h1>
<p>
  Session tracking is a tool to track the specific time period that the end user
  is using the application. It is a timeframe with a start and end.
</p>
<h2 id="h_01HABV0K6CR39VT9PG99M1M0WX">Manual Sessions</h2>
<p>
  Session tracking does not happen automatically. It has to be started. After that
  the elapsed session duration will be sent every 60 seconds.
</p>
<p>
  <code>Session</code> lifecycle methods include:
</p>
<ul>
  <li>
    <code>session.begin()</code> must be called when you want to send begin session
    request to the server. This request contains all device metrics: device,
    model, carrier, etc.
  </li>
  <li>
    <code>session.update()</code> can be called to send a session duration update
    to the server along with any events, user properties, and any other data
    types supported by Countly SDK. Called each Config.sendUpdateEachSeconds
    seconds automatically. It can also be called more often manually.
  </li>
  <li>
    <code>session.end()</code> must be called to mark the end of the session.
    All the data recorded since the last <code>session.update()</code> or since
    <code>session.begin()</code> in case no updates have been sent yet, is sent
    in this request as well.
  </li>
</ul>
<h1 id="h_01HD1EJB1JHW9PJSSQDX0YC0TC">View Tracking</h1>
<p>
  You can track the views of your application with the Java SDK. With views feature,
  you can also create
  <a class="editor-rtfLink" href="/hc/en-us/articles/4444616740249" target="_blank" rel="noopener">flows</a>
  to see view transitions. Public interface of the views can be accessed via:
</p>
<pre>Countly.instance().views()</pre>
<h2 id="h_01HD1F6YJJJCXHNG0FA0X8CAKJ">
  <span data-preserver-spaces="true">Manual View Reporting</span>
</h2>
<p>
  The SDK provides various ways to track views. You can have a single view at a
  given time or track multiple views according to your needs. Each view would have
  its own unique view ID which could be used for manipulating the view further.
</p>
<h3 id="h_01HJ3JGGKS9E23WF0BY0XPT4MS">Auto Stopped Views</h3>
<p>
  <span>An easy way to track views is with using the auto stopped views. These views would stop if another view starts. You can start an auto stopped view with or without segmentation like this:</span>
</p>
<pre><code class="java">// without segmentation, use view id for further manipulation of views
String viewID = Countly.instance().views().startAutoStoppedView("View Name");
  
// Or with segmentation
Map&lt;String, Object&gt; viewSegmentation = new HashMap&lt;&gt;();
viewSegmentation.put("Cats", 123);
viewSegmentation.put("Moons", 9.98d);
viewSegmentation.put("Moose", "Deer");

// use view id for further manipulation of views
String view2ID = Countly.instance().views().startAutoStoppedView("View Name", viewSegmentation);</code></pre>
<h3 id="h_01HJ3JP8GW4DF2JC5B8DM75XTF">Regular Views</h3>
<p>
  <span>As opposed to the "auto stopped views", with regular views you can have multiple of them started at the same time, and then you can control them independently.</span>
</p>
<p>
  You can start a view that would not close when another view starts, like this:
</p>
<pre><code class="java">Countly.instance().views().startView("View Name");</code></pre>
<p>
  While manually tracking views, you may add your custom segmentation to them like
  this:
</p>
<pre><code class="java">Map&lt;String, Object&gt; viewSegmentation = new HashMap&lt;&gt;();
viewSegmentation.put("Cats", 123);
viewSegmentation.put("Moons", 9.98d);
viewSegmentation.put("Moose", "Deer");

Countly.instance().views().startView("View Name", viewSegmentation);</code></pre>
<p>
  These views would also return a string view ID when they are called.
</p>
<h3 id="h_01HHNY9513MGDDJMP3SDWV4KWW" class="anchor-heading">Stopping Views</h3>
<p>
  You can stop a view with its name or its view ID. To stop it with its name:
</p>
<pre><code class="java">Countly.instance().views().stopViewWithName("View Name");</code></pre>
<p>You can provide a segmentation while doing so:</p>
<pre><code class="java">Map&lt;String, Object&gt; viewSegmentation = new HashMap&lt;&gt;();
viewSegmentation.put("Cats", 123);
viewSegmentation.put("Moons", 9.98d);
viewSegmentation.put("Moose", "Deer");

Countly.instance().views().stopViewWithName("View Name", viewSegmentation);</code></pre>
<p>
  <span>If there are multiple views with the same name then <code class="java">stopViewWithName</code> would close the one that has started first. These views would have different identifiers even though their names are same.</span>
</p>
<p>
  <span>To stop a view with its view ID:</span>
</p>
<pre><code class="java">Countly.instance().views().stopViewWithID("View ID");</code></pre>
<p>
  <span>You can provide a segmentation while doing so:</span>
</p>
<pre><code class="java">Map&lt;String, Object&gt; viewSegmentation = new HashMap&lt;&gt;();
viewSegmentation.put("Cats", 123);
viewSegmentation.put("Moons", 9.98d);
viewSegmentation.put("Moose", "Deer");

Countly.instance().views().stopViewWithID("View ID", viewSegmentation);</code></pre>
<p>
  You can also stop all running views at once with a segmentation:
</p>
<pre><code class="java">Map&lt;String, Object&gt; viewSegmentation = new HashMap&lt;&gt;();
viewSegmentation.put("Cats", 123);
viewSegmentation.put("Moons", 9.98d);
viewSegmentation.put("Moose", "Deer");

Countly.instance().views().stopAllViews(viewSegmentation); // pass null if no segmentation</code></pre>
<h3 id="h_01HHNYPKFGD5CC7SJECDWQ7EXB" class="anchor-heading">Pausing and Resuming Views</h3>
<p>
  <span>If you are starting multiple views at the same time it might be necessary for you to pause some views while others are still continuing. This can be achieved by using the unique identifier you get while starting a view.</span>
</p>
<p>
  <span>To pause a view with its ID:</span>
</p>
<pre><code class="java">Countly.instance().views().pauseViewWithID("View ID");</code></pre>
<p>
  <span>To resume a view with its ID:</span>
</p>
<pre><code class="java">Countly.instance().views().resumeViewWithID("View ID");</code></pre>
<h3 id="h_01HHNZEE94N9FH6GYZTR4A1H0M" class="anchor-heading">Adding Segmentation to Started Views</h3>
<p>
  <span>You can add segmentation values to a view before it ends. This can be done as many times as desired and the final segmentation that will be send to the server would be the cumulative sum of all segmentations. However if a certain segmentation value for a specific key has been updated, the latest value will be used.</span>
</p>
<p>
  <span>To add segmentation to a view using its view ID:</span>
</p>
<pre><code class="java">Map&lt;String, Object&gt; viewSegmentation = new HashMap&lt;&gt;();
viewSegmentation.put("Cats", 123);
viewSegmentation.put("Moons", 9.98d);
viewSegmentation.put("Moose", "Deer");

Countly.instance().views().addSegmentationToViewWithID("View ID", viewSegmentation);</code></pre>
<p>
  <span>To add segmentation to a view using its name:</span>
</p>
<pre><code class="java">Map&lt;String, Object&gt; viewSegmentation = new HashMap&lt;&gt;();
viewSegmentation.put("Cats", 123);
viewSegmentation.put("Moons", 9.98d);
viewSegmentation.put("Moose", "Deer");

Countly.instance().views().addSegmentationToViewWithName("View Name", viewSegmentation);</code></pre>
<h1 id="h_01HABV0K6CCY07B2BS5JVW72QQ">Device ID Management</h1>
<p>
  A device ID is a unique identifier for your users. You may specify the device
  ID yourself or allow the SDK to generate it. When providing one yourself, keep
  in mind that it has to be unique for all users. Some potential sources for such
  an id may be the users username, email or some other internal ID used by your
  other systems.
</p>
<h2 id="h_01HABV0K6C0RVYQ6JWPQ2EXR55">Retrieving Current Device ID</h2>
<p>
  You may want to see what device id and device id type Countly is assigning for
  the specific device. For that, you may use the following calls. Current device
  id types are 'DEVELOPER_SUPPLIED', 'SDK_GENERATED'.
</p>
<pre><code class="java hljs">Countly.instance().deviceId().getID() // will return String
Countly.instance().deviceId().getType() // will return DeviceIdType enum</code></pre>
<h2 id="h_01HABV0K6CZSJPRK4RYG23YH7F">Changing Device ID</h2>
<p>
  The SDK allows you to change the Device ID at any point in time. You can use
  any of the following two methods to changing the Device ID, depending on your
  needs.
</p>
<p class="anchor-heading">
  <strong>Changing Device ID with server merge</strong>
</p>
<p>
  <span>In case your application authenticates users, you might want to change the ID to the one in your backend after he has logged in. This helps you identify a specific user with a specific ID on a device he logs in, and the same scenario can also be used in cases this user logs in using a different way. In this case, any data stored in your Countly server database associated with the current device ID will be transferred (merged) into the user profile with the device id you specified in the following method call:</span>
</p>
<pre><code class="java hljs">Countly.instance().deviceId().changeWithMerge("New Device Id");</code></pre>
<p class="anchor-heading">
  <strong>Changing Device ID without server merge</strong>
</p>
<p>
  <span>You might want to track information about another separate user that starts using your app (changing apps account), or your app enters a state where you no longer can verify the identity of the current user (user logs out). In that case, you can change the current device ID to a new one without merging their data. You would call:</span>
</p>
<pre><code class="java hljs">Countly.instance().deviceId().changeWithoutMerge("New Device Id");</code></pre>
<p>
  <span>Doing it this way, will not merge the previously acquired data with the new id.</span>
</p>
<p>
  <span>Do note that every time you change your deviceId without a merge, it will be interpreted as a new user. Therefore implementing id management in a bad way could inflate the users count by quite a lot.</span>
</p>
<h2 id="h_01HD3QC31PBFGVZSRG6906NQGS">Device ID Generation</h2>
<p>
  When initializing Countly, If no custom ID is provided, the Countly Java SDK
  generates a unique device ID. The SDK uses a random UUID string for the device
  ID generation. For example, after you init the SDK without providing a custom
  id, this call will return something like this:
</p>
<pre><code class="java">Countly.instance().deviceId().getID(); // CLY_1930183b-77b7-48ce-882a-87a14056c73e</code></pre>
<h1 id="h_01HFPBH065MSZER3S0X3J15Y3E">User Location</h1>
<p>
  You can track your users' location with Countly Java SDK. This information can
  then be used for various tasks in your Countly server, like creating cohorts
  or sending push notifications depending on the location. You can only provide
  these four parameters regarding a user's location:
</p>
<ul>
  <li>
    <span>Country code in the two-letter, ISO standard, e.g. "en-US", "zh-CN"</span>
  </li>
  <li>
    <span>City name (must be set together with the country code), e.g. "Reykjavik"</span>
  </li>
  <li>
    <span>Latitude and longitude values, separated by a comma, e.g. "56.42345,123.45325"</span>
  </li>
  <li>
    <span>Your user’s IP address, e.g. "192.168.1.1"</span>
  </li>
</ul>
<h2 id="h_01HFPBH065HDQ0E63Q5T3F3V70">
  <span>Setting Location</span>
</h2>
<p>
  <span>If you set the user location during SDK initialization it will be sent to the server during the start of the user session:</span>
</p>
<pre>config.setLocation(countryCode, city, gpsCoordinates, ipAddress);</pre>
<p>
  As server side location calculations depends on the location info coming at the
  beginning of a user session, providing this info at init time is recommended.
</p>
<p>
  If you get your users' location info after SDK initialization, you can still
  provide them with the following call:
</p>
<pre><code class="java">//set user location
String countryCode = "us";
String city = "Houston";
String latitude = "29.634933";
String longitude = "-95.220255";
String ipAddress = null; // IP address must only be provided during init.<br>
Countly.instance().location().setLocation(countryCode, city, latitude + "," + longitude, ipAddress);
</code></pre>
<p>
  Here you if you don't want to set specific fields, you should set them to null.
</p>
<p>
  When these values are set, a separate request will be created to send them to
  the server and these values would be cached for location tracking later, so at
  the start of the next user session they would be used in server side calculations.&nbsp;
</p>
<h2 id="h_01HFPBSR2PTZB0VKMBQK133MYA">Disabling Location</h2>
<p>
  To turn off location tracking during init, use this method. Otherwise the location
  tracking is enabled by default:
</p>
<pre>config.disableLocation();</pre>
<p>
  To turn off location tracking after init you can use this method:
</p>
<pre><span>Countly.instance().location().disableLocation();</span></pre>
<p>
  <span>This action will erase the cached location data from the device and the server.</span>
</p>
<h1 id="h_01HE5J5B7V6DSCZWS0KMDV63WY">Remote Config</h1>
<p>
  Remote config allows you to modify the app by requesting key-value pairs from
  the Countly server. The returned values can be changed based on the users. For
  more details, please see the Remote Config
  <a href="https://support.count.ly/hc/en-us/articles/9895605514009-Remote-Config">documentation</a>.
  It is accessible through
  <code class="java">Countly.instance().remoteConfig()</code> interface. Remote
  config values are stored when downloaded unless they are deleted. Also, if values
  downloaded with full update, stored values are overwritten by newly downloaded
  values.;
</p>
<h2 id="h_01HE5J5B7V469TP7BF10DRHXSR">Downloading values</h2>
<h3 id="h_01HE5J61AFXNSTEKVR62NR56X7">
  <span>Automatic Remote Config Triggers</span>
</h3>
<p>
  <span>Automatic remote config triggers are disabled by default so there is no need for disable action. If you enable it by <code class="java">enableRemoteConfigAutomaticTriggers</code>, the remote config values are going to be fully updated.</span>
</p>
<pre><code class="java">Config config = new Config(COUNTLY_SERVER_URL, COUNTLY_APP_KEY, sdkStorageRootDirectory);
config.enableRemoteConfigAutomaticTriggers();
...</code></pre>
<p>
  Remote configs are going to be downloaded from scratch in these triggers:
</p>
<ul>
  <li>
    <span>Just after initialization of the Countly Java SDK</span>
  </li>
  <li>
    <span>After a device id change</span>
  </li>
</ul>
<h3 id="h_01HE5JSPP4G9YCH8HY4QAZ7RE4">Manual Calls</h3>
<p>
  There are three ways to trigger remote config value download manually:
</p>
<ul>
  <li>
    <span>Manually downloading all keys</span>
  </li>
  <li>
    <span>Manually downloading specific keys</span>
  </li>
  <li>Manually downloading, omitting (everything except) keys.</li>
</ul>
<p>
  <span>Each of these calls also has an optional RCDownloadCallback callback parameter which would be called when the download has finished.</span>
</p>
<p>
  <code class="java">dowloadAllKeys</code> is the same as the automatic update
  - it replaces all stored values with the ones from the server (all locally stored
  values are deleted and replaced with new ones).
</p>
<p>
  <span>Or downloading values of only specific keys might be needed. To do so, calling <code class="java">downloadSpecificKeys</code> to download new values for the specific keys would update only those keys which are provided with a String array.</span>
</p>
<p>
  <span>Or downloading values of only a few keys might not be needed. To do so, calling <code class="java">downloadOmittingKeys</code> would update all values except the provided keys</span><span>. The keys are provided with a String array.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">All Keys</span>
    <span class="tabs-link">Include Keys</span>
    <span class="tabs-link">Omit Keys</span>
  </div>
  <div class="tab">
    <pre><code class="java">Countly.instance().remoteConfig().downloadAllKeys((requestResult, error, fullValueUpdate, downloadedValues) -&gt; {
  if(requestResult.equals(RequestResult.Success){
    //do sth
  }
});</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="java">Countly.instance().remoteConfig().downloadSpecificKeys(String[] keysToInclude, (requestResult, error, fullValueUpdate, downloadedValues) -&gt; {
  if(requestResult.equals(RequestResult.Success){
    //do sth
  }
});</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="java">Countly.instance().remoteConfig().downloadOmittingKeys(String[] keysToOmit, (requestResult, error, fullValueUpdate, downloadedValues) -&gt; {
  if(requestResult.equals(RequestResult.Success){
    //do sth
  }
});</code></pre>
  </div>
</div>
<p>
  <span>When making requests with an "keysToInclude" or "keysToOmit" array, if those arrays are empty or null, they will function the same as a <code class="java">dowloadAllKeys</code> request and will update all the values. This means it will also erase all keys not returned by the server.</span>
</p>
<h2 id="h_01HE7DEWNAQGDF1X2QGS367TJ4">
  <span>Accessing Values</span>
</h2>
<p>
  There is two way to access remote config values. Either all values can be gathered,
  or a value can be obtained for a specific key.
</p>
<pre><code class="java">//Which will return map of all stored remote config values
Map&lt;String,RCData&gt; allValues = Countly.instance().remoteConfig().getValues();
Object valueOfKey = allValues.get("key").value;</code></pre>
<p>
  <span>RCData looks like this:</span>
</p>
<pre><code class="java">class RCData {
  //value that is downloaded from the server for that key
  Object value;
  //metadata about ownership of the value
  //it is false when device id changed but that key's value is not updated
  boolean isCurrentUsersData;
}</code></pre>
<p>
  <span>Why value is in Object class? Because all data types supported by JSON can be a stored. For example it can be a JSONArray, JSONObject, Integer, Boolean, Float, String, Double, Long. So it is needed to cast to appropriate data type. If value is null then there is no value for that key found.</span>
</p>
<p>
  <span>To get a value's of a specific key:</span>
</p>
<pre><code class="java">RCData data = Countly.instance().remoteConfig().getValue("key");
RCData data1 = Countly.instance().remoteConfig().getValue("key1");
RCData data2 = Countly.instance().remoteConfig().getValue("key2");
JSONObject json = (JSONObject) data.value;
JSONArray jArray = (JSONArray) data1.value;
Integer intValue = (Integer) data2.value;
</code></pre>
<h2 id="h_01HE7FERK1CT5SPCGQCTY041M7">Clearing Stored Values</h2>
<p>
  Clearing the remote config values might be needed at some case, so by this call
  you can clean the remote config values:
</p>
<pre><code class="java">Countly.instance().remoteConfig().clearAll();</code></pre>
<h2 id="h_01HE7FM8E24B9GWXGN0MG709BN">Global Download Callbacks</h2>
<p>
  A callback function might be needed after remote config values downloaded. Remote
  config download callback functions can be registered during initialization of
  Countly or via remoteConfig interface.
</p>
<pre><code class="java">//during initialization
Config config = new Config(COUNTLY_SERVER_URL, COUNTLY_APP_KEY, sdkStorageRootDirectory);
config.remoteConfigRegisterGlobalCallback(RCDownloadCallback callback);
...</code></pre>
<p>
  RCDownloadCallback is called when the remote config download request is finished,
  and it would have the following parameters:
</p>
<ul>
  <li>
    <code class="java">rResult</code>: RequestResult Enum (either Error, Success
    or NetworkIssue)
  </li>
  <li>
    <code class="java">error</code>: String (error message. "null" if there is
    no error)
  </li>
  <li>
    <code class="java">fullValueUpdate</code>: boolean ("true" - all values updated,
    "false" - a subset of values updated)
  </li>
  <li>
    <code class="java">downloadedValues</code>: Map&lt;String, RCData&gt; (the
    whole downloaded remote config values from server)
  </li>
</ul>
<pre><code class="java">RCDownloadCallback {
  void callback(RequestResult rResult, String error, boolean fullValueUpdate, Map&lt;String, RCData&gt; downloadedValues);
}</code></pre>
<p>
  Via remoteConfig interface, already registered callback can be also removed
</p>
<pre><code class="java">//register a download callback
Countly.instance().remoteConfig().registerDownloadCallback(RCDownloadCallback callback);
<br>//remove already registered download callback
Countly.instance().remoteConfig().removeDownloadCallback(RCDownloadCallback callback);</code></pre>
<h2 id="h_01HE7H1PHM3HJ82YDSYJWQZKNH">A/B Testing</h2>
<p>
  User's participation in <a href="/hc/en-us/articles/4416496362393">A/B</a> tests
  can be accessed from the Remote Config feature in multiple ways. Possible ways
  to enroll or remove your users for A/B tests are listed below.
</p>
<h3 id="h_01HE7H4D2C4N6AZ55RTSKGTGXY">Enrollment on Download</h3>
<p>
  Enrollment to A/B tests can be done automatically when downloading remote config
  values. This can be enabled on the initialization of the Countly.
</p>
<pre><code class="java">//during initialization
Config config = new Config(COUNTLY_SERVER_URL, COUNTLY_APP_KEY, sdkStorageRootDirectory);
config.enrollABOnRCDownload();
...</code></pre>
<h3 id="h_01HE7H4GRQCW16QGRYCT87CNJV">Enrollment on Access</h3>
<p>
  A/B tests can be enrolled while getting remote config values from storage. If
  there is no key exists functions does not enroll user to A/B tests:
</p>
<pre><code class="java">//This call returns RCData, works same way with non-enrolling variant getValue 
Countly.instance().remoteConfig().getValueAndEnroll(String key); 
  
//This call returns Map&lt;String,RCData&gt;, works same way with non-enrolling variant getValues 
Countly.instance().remoteConfig().getAllValuesAndEnroll();</code></pre>
<h3 id="h_01HE7H4MM8SJG3K0RAXPW0QTV5">Enrollment on Action</h3>
<p>
  To enroll a user into the A/B tests for the given keys following method should
  be used:
</p>
<pre><code class="java">Countly.instance().remoteConfig().enrollIntoABTestsForKeys(String[] keys);</code></pre>
<p>
  Keys array is the required parameter. If it is not given this function does nothing.
</p>
<h3 id="h_01HE7H4RATY8ZTBVN7VJJNMA40">Exiting A/B Tests</h3>
<p>
  To remove users from A/B tests of certain keys, following function should be
  used:
</p>
<pre><code class="java">Countly.instance().remoteConfig().exitABTestsForKeys(String[] keys);</code></pre>
<p>
  Keys array is the required parameter. If it is not given, user is going to be
  removed from all tests.
</p>
<h1 id="01HD3Q7MES8WBFJXDP7CP6E5V2">User Feedback</h1>
<p>
  <span style="font-weight: 400;">You can receive <a href="/hc/en-us/articles/4652903481753">feedback</a> from your users with nps, survey and rating feedback widgets.</span>
</p>
<p>
  <span style="font-weight: 400;">The rating feedback widget allows users to rate using the 1 to 5 rating system as well as leave a text comment. Survey and nps feedback widgets allow for even more textual feedback from users.</span>
</p>
<h2 id="h_01HAVQDM5VNQE1BKTPNSXMX3BM">Feedback Widget</h2>
<p>
  It is possible to display 3 kinds of feedback widgets:
  <a href="https://support.count.ly/hc/en-us/articles/900003407386-NPS-Net-Promoter-Score-" target="_blank" rel="noopener">nps</a>,
  <a href="https://support.count.ly/hc/en-us/articles/900004337763-Surveys" target="_blank" rel="noopener">survey</a>
  and
  <a href="https://support.count.ly/hc/en-us/articles/360037641291-Ratings" target="_blank" rel="noopener">rating</a>.
  All widgets have their generated URL to be shown in a web viewer and should be
  approached using the same methods.
</p>
<div class="callout callout--warning">
  <p>
    Before any feedback widget can be shown, you need to create them in your
    Countly dashboard.
  </p>
</div>
<h3 id="h_01HD3PX5GQ390KDHFCH1FD6ER9">Getting Available Widgets</h3>
<p>
  After you have created widgets at your dashboard you can reach their related
  information as a list, corresponding to the current user's device ID, by providing
  a callback to the getAvailableFeedbackWidgets method, which returns the list
  as the first parameter and error as the second:
</p>
<div>
  <pre><code class="java hljs">Countly.instance().feedback().getAvailableFeedbackWidgets((retrievedWidgets, error) -&gt; {
  // handle error
  // do something with the returned list here like pick a widget and then show that widget etc...
});</code></pre>
</div>
<p>The objects in the returned list would look like this:</p>
<pre><code class="java hljs">class CountlyFeedbackWidget {
  public String widgetId;
  public FeedbackWidgetType type;
  public String name;
  public String[] tags;
}</code></pre>
<p>
  Here all the values are same with the values that can be seen at your Countly
  server like the widget ID, widget type, widget name and the tags you have passed
  while creating the widget. Tags can contain information that you would like to
  have in order to keep track of the widget you have created. Its usage is totally
  left to the developer.
</p>
<p>Potential 'type' values are:</p>
<pre><code class="java hljs">FeedbackWidgetType {survey, nps, rating}</code></pre>
<h3 id="h_01HD3PXZPF49C292RN6EHXF4DB">Presenting A Widget</h3>
<p>
  After you have decided which widget you want to show, you would provide that
  object to the following function as the first parameter. Second is a callback
  with constructed url to show and error message in case an error occurred:
</p>
<div>
  <pre><code class="java hljs">Countly.instance().feedback().constructFeedbackWidgetUrl(chosenWidget, (constructedUrl, error) -&gt; {
  // handle error and the constructed url
});
</code></pre>
</div>
<h3 id="h_01HAVQDM5V90VKV6QA45CK8Z49">Manual Reporting</h3>
<p>
  There might be some cases where you might want to use the native UI or a custom
  UI you have created. At those times you would want to request all the information
  related to that widget and then report the result manually. You can see more
  information about manual reporting from
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts#h_01HABT18WT0D08H8DR2BAD77T2" target="_blank" rel="noopener noreferrer">here</a>.
</p>
<div class="callout callout--info">
  <p>
    For a sample integration, have a look at our
    <a href="https://github.com/Countly/countly-sdk-java/blob/master/app-java/src/main/java/ly/count/java/demo/Example.java" target="_blank" rel="noopener">sample code</a>
    at our github repo.
  </p>
</div>
<h4 id="h_01HD3PHEFBGA26HTB82MS2ZE1W">Getting Feedback Widget Data</h4>
<p>
  Initial steps for manually reporting your widget results, first you would need
  to retrieve the available widget list with the
  <code>getAvailableFeedbackWidgets</code> method. After that you would have a
  list of possible <code>CountlyFeedbackWidget</code> objects. You would pick the
  widget you want to display and pass that widget object to the function below
  as the first parameter. Second parameter is a callback that would return the
  widget data as first parameter and the error as second:
</p>
<div>
  <pre><code class="java hljs">Countly.instance().feedback().getFeedbackWidgetData(chosenWidget, (retrievedWidgetData, error) -&gt; {
  // handle data and error here
});</code></pre>
</div>
<p>
  Here the retrievedWidgetData would yield to a JSON Object with all of the information
  you would need to present the widget by yourself.
</p>
<div class="callout callout--info">
  <p>
    For how this retrievedWidgetData would look like and in depth information
    on this topic please check our detailed article
    <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts#h_01HABT18WT0D08H8DR2BAD77T2" target="_blank" rel="noopener noreferrer">here</a>.
  </p>
</div>
<h4 id="h_01HD3PPXTPFRV8246MBB7W1F47">Reporting Widget Result Manually</h4>
<p>
  After you have collected the required information from your users with the help
  of the <code>retrievedWidgetData</code> you have received, you would then package
  the responses into a Map&lt;String, Object&gt;, and then pass it (reportedResult)
  together with the widget object you picked from the retrieved widget list (widgetToReport)
  and the <code>retrievedWidgetData</code> to report the feedback result with the
  following call:
</p>
<pre><code class="java hljs">//this contains the reported results
Map&lt;String, Object&gt; reportedResult = new HashMap&lt;&gt;();

//
// You would fill out the results here. That step is not displayed in this sample check the detailed documentation linked above
//

//report the results to the SDK
Countly.instance().feedback().reportFeedbackWidgetManually(widgetToReport, retrievedWidgetData, reportedResult);
</code></pre>
<p>
  If the user would have closed the widget, you would report that by passing a
  "null" as the reportedResult.
</p>
<h1 id="h_01HABV0K6C4TX8B97XNK8XWNVA">User Profiles</h1>
<p>
  For information about User Profiles, review
  <a href="http://resources.count.ly/docs/user-profiles">this documentation</a>.
  You can access user profiles via <code>Countly.instance().userProfile()</code>.&nbsp;
</p>
<h2 id="h_01HD3M0EYQAERWFGMRVZXQ2RR1">Setting User Properties</h2>
<h3 id="h_01HABV0K6CJE3JS8YYM8TNYV9A">Setting Custom Values</h3>
<p>
  To set custom properties, call setProperty(). To send modification operations,
  call the corresponding methods and
  <span>ensure to call <code>Countly.instance().userProfile().save()</code> to send the configured user properties to the server after setting them</span>:
</p>
<pre><code class="java">Countly.instance().userProfile().setProperty("mostFavoritePet", "dog");
Countly.instance().userProfile().increment("phoneCalls"); // increments by 1
Countly.instance().userProfile().pushUnique("tags", "fan");
Countly.instance().userProfile().pushUnique("skill", "singer");
Countly.instance().userProfile().save();
</code></pre>
<h3 id="h_01HABV0K6CJR090QF0ZTKB1MNG">Setting Predefined Values</h3>
<p>
  The Countly Java SDK allows you to upload specific data related to a user to
  the Countly server. You may set the following predefined data for a particular
  user:
</p>
<ul>
  <li>
    <strong>Name</strong>: Full name of the user.
  </li>
  <li>
    <strong>Username</strong>: Username of the user.
  </li>
  <li>
    <strong>Email</strong>: Email address of the user.
  </li>
  <li>
    <strong>Organization</strong>: Organization the user is working in.
  </li>
  <li>
    <strong>Phone</strong>: Phone number.
  </li>
  <li>
    <strong>Picture</strong>: Picture path for the user’s profile.
  </li>
  <li>
    <strong>Gender</strong>: Gender of the user (use only single char like ‘M’
    for Male and ‘F’ for Female).
  </li>
  <li>
    <strong>BirthYear</strong>: Birth year of the user.
  </li>
</ul>
<p>
  The SDK allows you to upload user details using the methods listed below.
</p>
<p>
  To set standard properties, call respective methods and
  <span>ensure to call <code>Countly.instance().userProfile().save()</code> to send the configured user properties to the server after setting them</span>:
</p>
<pre><code class="java">Countly.instance().userProfile().setProperty(PredefinedUserPropertyKeys.NAME, "Firstname Lastname");
Countly.instance().userProfile().setProperty(PredefinedUserPropertyKeys.EMAIL, "test@test.com");
Countly.instance().userProfile().setProperty(PredefinedUserPropertyKeys.USERNAME, "nickname");
Countly.instance().userProfile().setProperty(PredefinedUserPropertyKeys.ORGANIZATION, "Tester");
Countly.instance().userProfile().setProperty(PredefinedUserPropertyKeys.PHONE, "+123456789");
Countly.instance().userProfile().save();
</code></pre>
<h2 id="h_01HD3M6CQAF1H7T6SWVHW1AWS9">Setting User Picture</h2>
<p>You can either upload a profile picture by this call:</p>
<pre>Countly.instance().userProfile().setProperty(PredefinedUserPropertyKeys.PICTURE, BYTE_IMAGE)</pre>
<p>
  or you can provide a picture url or local file path to set (only JPG, JPEG files
  are supported by the Java SDK):
</p>
<pre>Countly.instance().userProfile().setProperty(PredefinedUserPropertyKeys.PICTURE_PATH, String)</pre>
<h2 id="h_01HD3ME354FKRADNYDMRQWK7WE">User Property Modificators</h2>
<p>Here is the list of property modificators:</p>
<pre><code lang="java">//set a custom property
Countly.instance().userProfile().setProperty("money", 1000);
//increment money by 50
Countly.instance().userProfile().increment("money", 50);
//multiply money with 2
Countly.instance().userProfile().multiply("money", 2);
//save maximum value
Countly.instance().userProfile().saveMax("score", 400);
//save minimum value
Countly.instance().userProfile().saveMin("time", 60);
//add property to array which can have unique values
Countly.instance().userProfile().pushUnique("currency", "dollar");
//add property to array which can be duplicate
Countly.instance().userProfile().push("currency", "dollar");
//remove value from array
Countly.instance().userProfile().pull("currency","dollar");
//set only a value
Countly.instance().userProfile().setOnce("bank","TestBank");
//save changes
Countly.instance().userProfile().save();</code></pre>
<h1 id="h_01HD1H1HNJVYBP0PNP0YSMFZY6">Security and Privacy</h1>
<h2 id="h_01HD1H1HNJM6EBH29WE8AJSF80">Parameter Tamper Protection</h2>
<p>
  You may set the optional <code>salt</code> to be used for calculating the checksum
  of requested data, which will be sent with each request, using the
  <code>checksum</code> field. You will need to set the same salt on the Countly
  server. If the salt on the Countly server is selected, all requests will be checked
  for the validity of the <code>checksum</code> field before being processed.
</p>
<pre><span>Config config </span>= <span>new </span>Config(<span>COUNTLY_SERVER_URL</span>, <span>COUNTLY_APP_KEY</span>, sdkStorageRootDirectory);<br><span>config</span>.enableParameterTamperingProtection(<span>"salt"</span>);<br><span>Countly</span>.<span>instance</span>().init(<span>config</span>);<code class="java"></code></pre>
<h1 id="h_01HABV0K6DQMRJ4VJ3X328HXT5">Other Features and Notes</h1>
<h2 id="h_01HAXVT7C5C8C64NHXNVG0TS4W">SDK Config Parameters Explained</h2>
<p>
  These are the methods that lets you set values in your Countly config object:
</p>
<ul>
  <li>
    <strong>setUpdateSessionTimerDelay(int delay)</strong> - Sets the interval
    for the automatic session update calls. The delay can not be smaller than
    1 sec.
  </li>
  <li>
    <strong>setEventQueueSizeToSend()</strong> - Sets the threshold for event
    grouping.
  </li>
  <li>
    <strong>setSdkPlatform(String platform)</strong> - Sets the SDK platform
    if it is used in multiple platforms. Default value is OS name.
  </li>
  <li>
    <strong>setRequiresConsent(boolean requiresConsent)</strong> - Enable GDPR
    compliance by disallowing SDK to record any data until corresponding consent
    calls are made. Default is false.
  </li>
  <li>
    <div>
      <strong>setMetricOverride(Map&lt;String, String&gt; metricOverride)</strong>
      - Mechanism for overriding metrics that are sent together with "begin
      session" requests and remote.
    </div>
  </li>
  <li>
    <div>
      <strong>setApplicationVersion(String version)</strong> - Change application
      version reported to Countly server.
    </div>
  </li>
  <li>
    <strong>setApplicationName(String name) </strong>- Change application name
    reported to Countly server.
  </li>
  <li>
    <div>
      <strong>setLoggingLevel(LoggingLevel loggingLevel)</strong> - Logging
      level for Countly SDK. Default is OFF.
    </div>
  </li>
  <li>
    <div>
      <strong>enableParameterTamperingProtection(String salt)</strong> - Enable
      parameter tampering protection.
    </div>
  </li>
  <li>
    <div>
      <strong>setRequestQueueMaxSize(int requestQueueMaxSize)</strong> - In
      backend mode set the in memory request queue size. Default is 1000.
    </div>
  </li>
  <li>
    <div>
      <strong>enableForcedHTTPPost()</strong> - Force usage of POST method
      for all requests.
    </div>
  </li>
  <li>
    <div>
      <strong>setCustomDeviceId(String customDeviceId) </strong>- Set device
      id to specific string and strategy to
      <code>DeviceIdStrategy.CUSTOM_ID</code>.
    </div>
  </li>
  <li>
    <div>
      <strong>setLogListener(LogCallback logCallback)</strong> - Add a log
      callback that will duplicate all logs done by the SDK.
    </div>
  </li>
  <li>
    <strong>enrollABOnRCDownload()</strong> - Enables A/B tests enrollment when
    remote config keys downloaded
  </li>
  <li>
    <strong>remoteConfigRegisterGlobalCallback(RCDownloadCallback callback)</strong>
    - Register a callback to be called when remote config values is downloaded
  </li>
  <li>
    <strong>enableRemoteConfigValueCaching()</strong> - Enable caching of remote
    config values
  </li>
  <li>
    <strong>enableRemoteConfigAutomaticTriggers()</strong> - Enable automatic
    download of remote config values on triggers
  </li>
  <li>
    <strong>disableLocation() </strong>- Disable location tracking
  </li>
  <li>
    <strong>setLocation(String countryCode, String city, String geoLocation, String ipAddress)</strong>
    - Set location parameters to be sent with session begin
  </li>
  <li>
    <strong>setMaxBreadcrumbCount(int maxBreadcrumbCount)</strong> - To change
    maximum limit of crash breadcrumb
  </li>
  <li>
    <strong>disableUnhandledCrashReporting()</strong> - To disable unhandled
    crash reporting
  </li>
</ul>
<h2 id="h_01HNFH7ZFRE3CKRCTZE6EZWM86">Example Integrations</h2>
<p>
  <a href="https://github.com/Countly/countly-sdk-java/tree/master/app-java">app-java</a>
  module contains example use cases for the Countly Java SDK
</p>
<p>
  -
  <a href="https://github.com/Countly/countly-sdk-java/blob/master/app-java/src/main/java/ly/count/java/demo/Example.java">Example</a>
  is a java application that covers most of the functionalities.
</p>
<p>
  -
  <a href="https://github.com/Countly/countly-sdk-java/blob/master/app-java/src/main/java/ly/count/java/demo/BackendModeExample.java">BackendModeExample</a>
  is a java application of an example usage of the BackendMode
</p>
<h2 id="h_01HD3J87NT4XC7YQ66JQ7HFTHF">SDK storage and Requests</h2>
<h3 id="h_01HAXVT7C5GTQ0D0HRCZ83J0VQ">Setting Event Queue Threshold</h3>
<p>
  Events get grouped together and are sent either every minute or after the unsent
  event count reaches a threshold. By default it is 10. If you would like to change
  this, call:
</p>
<pre>config.setEventQueueSizeToSend(<span>6</span>);</pre>
<h3 id="h_01HD3JE2GZ6PJDBWN1XWQ51JVV">Setting Maximum Request Queue Size</h3>
<p>
  The request queue is flushed when the session timer delay exceeds. If network
  or server are not reachable, If the number of requests in the queue reaches the
  setRequestQueueMaxSize limit, the oldest requests in the queue will be dropped,
  and the newest requests will take their place. by default request queue size
  is 1000. You can change this by:
</p>
<pre>config.setRequestQueueMaxSize(<span>56</span>);</pre>
<h3 id="h_01HD3JPGMZP46HZAJHZSPN59F2">Forcing HTTP POST</h3>
<p>You can force HTTP POST request for all requests by:</p>
<pre>config.enableForcedHTTPPost();</pre>
<h2 id="h_01HAXVT7C5G91JJG8FSCXH3CJV">Custom Metrics</h2>
<div class="callout callout--warning">
  <p>This functionality is available since SDK version 22.09.1.</p>
</div>
<p>
  During some specific circumstances, like beginning a session or requesting remote
  config, the SDK is sending device metrics.
</p>
<p>
  It is possible for you to either override the sent metrics (like the application
  version for some specific variant) or provide either your own custom metrics.
  If you are providing your own custom metrics, you would need your own custom
  plugin server-side which would interpret it appropriately. If there is no plugin
  to handle those custom values, they will be ignored.
</p>
<div>
  <pre><code class="java hljs">Map&lt;String, String&gt; metricOverride = new HashMap&lt;&gt;();
metricOverride.put("SomeKey", "123");
metricOverride.put("_locale", "xx_yy");

Config config = new Config(COUNTLY_SERVER_URL, COUNTLY_APP_KEY)
  .setMetricOverride(metricOverride);
  
Countly.init(targetFolder, config);
</code></pre>
</div>
<p>
  For more information on the specific metric keys used by Countly, check
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305#h_01HABT18WWYQ2QYPZY3GHZBA9B" target="_self">here</a>.
</p>
<h2 id="h_01HABV0K6D57PGC01NJ1V3QYSB">Backend Mode</h2>
<p>
  The SDK provides a special mode to transfer data to your Countly Server, called
  'Backend Mode'. This mode disables the regular API of the SDK and offers an alternative
  interface to record user data. This alternative approach would be useful when
  integrated in backend scenarios or when importing data into countly from a different
  source.
</p>
<p>
  Data recorded with this mode is kept in memory queues and is not stored persistently.
  This means that any data, that was not yet sent to the server when the app is
  closed/killed, will be lost.
</p>
<h3 id="h_01HABV0K6D46WXJ4FAWTKQF7HX">Enabling Backend Mode</h3>
<p>
  To enable Backend Mode you should create a config class and call
  <code class="java">enableBackendMode</code>on this object, and later you should
  pass it to the <code>init</code> method.
</p>
<pre><code class="java hljs">Config config = new Config("http://YOUR.SERVER.COM", "YOUR_APP_KEY")
  .enableBackendMode()
  .setRequestQueueMaxSize(<span>500</span>)
  .setLoggingLevel(Config.LoggingLevel.DEBUG);

Countly.init(targetFolder, config);</code></pre>
<p>
  If the Backend Mode is enabled the SDK stores up to a maximum of 1000 requests
  by default. Then when this limit is exceeded the SDK will drop the oldest request
  from the queue in the memory. To change this request queue limit, call
  <code class="java">setRequestQueueMaxSize</code> on the
  <code class="java">Config</code>object before the SDK init.
</p>
<h3 id="h_01HABV0K6DB0KK25C4P7GV0WVW">Recording Data</h3>
<p>
  In order to record data using the SDK, users are required to provide a device
  ID and may optionally include a timestamp, specified in milliseconds. It is important
  to note that the device ID is a mandatory field and cannot be set to null or
  omitted.
</p>
<p>
  It is also worth noting that if a timestamp value is not provided or is less
  than 1, the SDK will automatically update the value to the current time, specified
  in milliseconds. This ensures that all recorded data is accurately timestamped
  and prevents data duplication.
</p>
<h4 id="h_01HABV0K6DTND55NRZ3SEGS3JP">Recording an Event</h4>
<p>
  <span data-preserver-spaces="true">You may record as many events as you want.</span>
</p>
<p>
  <span data-preserver-spaces="true">There are a couple of values that can be set when recording an event.</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID-</span></strong><span data-preserver-spaces="true"> Device id is mandatory, it can not be empty or null.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">key-</span></strong><span data-preserver-spaces="true"> This is the main property which would be the identifier/name for that event. It is mandatory and it can not be empty or null.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">count -</span></strong><span data-preserver-spaces="true"> A whole positive numerical number value that marks how many times this event has happened. It is optional and if it is provided and its value is less than </span><strong><span data-preserver-spaces="true">1</span></strong><span data-preserver-spaces="true">, SDK will automatically set it to </span><strong><span data-preserver-spaces="true">1</span></strong><span data-preserver-spaces="true">.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">sum -</span></strong><span data-preserver-spaces="true"> This value will be summed up across all events in the dashboard. It is optional you may set it <strong>null</strong>.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">duration - </span></strong><span data-preserver-spaces="true">This value is used for recording and tracking the duration of events. Set it to </span><strong><span data-preserver-spaces="true">0</span></strong><span data-preserver-spaces="true"> if you don't want to report any duration.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">segmentation - </span></strong><span data-preserver-spaces="true">A map where you can provide custom data for your events to track additional information. It is not a mandatory field, so you may set it to </span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true"> or </span><strong><span data-preserver-spaces="true">empty</span></strong><span data-preserver-spaces="true">. It is a map that consists of key and value pairs. The accepted data types for the values are "String", "Integer", "Double", and "Boolean". All other types will be ignored.</span>
  </li>
</ul>
<p>Example:</p>
<pre><code class="java hljs">Map&lt;String, String&gt; segment = new HashMap&lt;String, String&gt;();
segment.put("Time Spent", "60");
segment.put("Retry Attempts", "60");

Countly.instance().backendM().recordEvent("device-id", "Event Key", 1, 10.5, 5, segment, 1646640780130L);
</code></pre>
<p>
  <strong>Note: </strong>Device ID and 'key' both are mandatory. The event will
  not be recorded if any of these two parameters is null or empty.;
</p>
<h4 id="h_01HABV0K6DRZ993XGKMFF29MGF">Recording a View</h4>
<p>
  <span data-preserver-spaces="true">You may record views by providing the view details in segmentation with a timestamp.</span>
</p>
<p>
  <span data-preserver-spaces="true">There are a couple of values that can be set when recording an event.</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID -</span></strong><span data-preserver-spaces="true"> Device id is mandatory, if it is null or empty data will not be recorded.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">name -</span></strong><span data-preserver-spaces="true"> It is the name of the view and it must not be empty or null.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">segmentation - </span></strong><span data-preserver-spaces="true">A map where you can provide custom data for your view to track additional information. It is not a mandatory field, you may set it to </span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true"> or leave it </span><strong><span data-preserver-spaces="true">empty</span></strong><span data-preserver-spaces="true">. It is a map of key/value pairs and the accepted data types are "String", "Integer", "Double", and "Boolean". All other types will be ignored.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">timestamp -</span></strong><span data-preserver-spaces="true"> It is time in milliseconds. It is not mandatory, and you may set it to null.</span>
  </li>
</ul>
<p>Example:</p>
<pre><code class="java hljs">Map&lt;String, String&gt; segmentation = new HashMap&lt;String, String&gt;();
segmentation.put("visit", "1");
segmentation.put("segment", "Windows");
segmentation.put("start", "1");

Countly.instance().backendM().recordView("device-id", "SampleView", segmentation, 1646640780130L);
</code></pre>
<p>
  <strong>Note: </strong>Device ID and 'name' both are mandatory. The view will
  not be recorded if any of these two parameters is null or empty.
</p>
<h4 id="h_01HABV0K6D86BYQ81T2VGYZJKM">Recording a Crash</h4>
<p>
  <span>To report exceptions provide the following detail:</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID -</span></strong><span data-preserver-spaces="true"> Device id is mandatory, and if it is null or not provided no data will be recorded. </span>
  </li>
  <li>
    <strong>message -</strong>
    <span>This is the main property which would be the identifier/name for that event. It should not be null or empty.</span>
  </li>
  <li>
    <strong>stacktrace -</strong>
    <span>A string that describes the contents of the call stack</span>. It
    <span data-preserver-spaces="true">is mandatory, and should not be null or empty.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">segmentation - </span></strong><span data-preserver-spaces="true">A map where you can provide custom data for your view to track additional information. It is not a mandatory field, so you may set it to </span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true"> or leave it </span><strong><span data-preserver-spaces="true">empty</span></strong><span data-preserver-spaces="true">. It is a map of key/value pairs and the accepted data types are "String", "Integer", "Double", and "Boolean". All other types will be ignored.</span>
  </li>
  <li>
    <strong>crashDetail - </strong><span data-preserver-spaces="true">It is not a mandatory field, so you may set it to </span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true"> or leave it </span><strong><span data-preserver-spaces="true">empty</span></strong><span data-preserver-spaces="true">. It is a map of key/value pairs. To know more about crash parameters, <a href="https://support.count.ly/hc/en-us/articles/360037753291-SDK-development-guide#01H821RTQ20M61EKN76EY6RJ84" target="_self">click here</a>.</span><span data-preserver-spaces="true"></span>
  </li>
  <li>
    <strong>timestamp -</strong>
    <span data-preserver-spaces="true">It is time in milliseconds. It is not mandatory, and you may set it to null.</span>
  </li>
</ul>
<pre><code class="java hljs">Map&lt;String, String&gt; segmentation = new HashMap&lt;String, String&gt;();
segmentation.put("login page", "authenticate request");

Map&lt;String, String&gt; crashDetails = new HashMap&lt;String, String&gt;();
crashDetails.put("_os", "Windows 11");
crashDetails.put("_os_version", "11.202");
crashDetails.put("_logs", "main page");

Countly.instance().backendM().recordException("device-id", "message", "stacktrace", segmentation, crashDetails, null);
</code></pre>
<p>
  You may also pass an instance of an exception instead of the message and the
  stack trace to record a crash.
</p>
<p>For example:</p>
<pre><code class="java">Map&lt;String, String&gt; segmentation = new HashMap&lt;String, String&gt;();
segmentation.put("login page", "authenticate request");

Map&lt;String, String&gt; crashDetails = new HashMap&lt;String, String&gt;();
crashDetails.put("_os", "Windows 11");
crashDetails.put("_os_version", "11.202");
crashDetails.put("_logs", "main page");

try {
  int a = 10 / 0;
} catch(Exception e) {
  Countly.instance().backendM().recordException("device-id", e, segmentation, crashDetails, null);
}</code></pre>
<p>
  <strong>Note: </strong>Throwable is a mandatory parameter, the crash will not
  be recorded if it is null.
</p>
<h4 id="h_01HABV0K6DTQ7W3AVREGG1KVHP">Recording Sessions</h4>
<p>
  <span>To start a session please provide the following details:</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID -</span></strong><span data-preserver-spaces="true"> Device id is mandatory, if it is null or empty data will not be recorded.</span>
  </li>
  <li>
    <strong>metrics - </strong>It is a map that contains device and app information<span data-preserver-spaces="true"> as key-value pairs. </span>
    It can be null or empty<span> and the accepted data type for the pairs is </span><span>"String".</span>
  </li>
  <li>
    <strong>location - </strong><span data-preserver-spaces="true">It is not a mandatory field, so you may set it to </span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true"> or leave it </span><strong><span data-preserver-spaces="true">empty</span></strong><span data-preserver-spaces="true">. It is a map of key/value pairs and the accepted keys are "city", "country_code", "ip_address", and "location".</span>
  </li>
  <li>
    <strong>timestamp -</strong>
    <span data-preserver-spaces="true">It is time in milliseconds. It is not mandatory, and you may set it to <strong>null</strong>.</span><span data-preserver-spaces="true"></span>
  </li>
</ul>
<p>Example:</p>
<pre><code class="java hljs">Map&lt;String, String&gt; metrics = new HashMap&lt;String, String&gt;();
metrics.put("_os", "Android");
metrics.put("_os_version", "10");
metrics.put("_app_version", "1.2");

Map&lt;String, String&gt; location = new HashMap&lt;String, String&gt;();
location.put("ip_address", "192.168.1.1");
location.put("city", "Lahore");
location.put("country_code", "PK");
location.put("location", "31.5204,74.3587");

Countly.instance().backendM().sessionBegin("device-id", metrics, location, 1646640780130L);
</code></pre>
<p>
  <strong>Note:</strong> In above example '_os', '_os_version' and '_app_version'
  are predefined metrics keys. To know more about metrics, click
  <a href="https://support.count.ly/hc/en-us/articles/360037753291-SDK-development-guide#01H821RTQ2TZF21BH3ZSR8XHNW" target="_self">here.</a>
</p>
<p>
  <span>To update or end a session please provide the following details:</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID -</span></strong><span data-preserver-spaces="true"> Device id is mandatory, if it is null or empty no action will be taken.</span>
  </li>
  <li>
    <strong>duration - </strong>It is the duration of a session, you may pass
    <strong>0</strong> if you don't want to submit a duration.
  </li>
  <li>
    <strong>timestamp -</strong>
    <span data-preserver-spaces="true">It is time in milliseconds. It is not mandatory, and you may set it to <strong>null</strong>.</span>
  </li>
</ul>
<p>
  <span data-preserver-spaces="true">Session update:</span>
</p>
<pre><code class="java hljs">double duration = 60;
Countly.instance().backendM().sessionUpdate("device-id", duration, null);
</code></pre>
<p>Session end:</p>
<pre><code class="java hljs">double duration = 20;
Countly.instance().backendM().sessionEnd("device-id", duration, 1223456767L);
</code></pre>
<p>
  <strong>Note:</strong> Java SDK automatically sets the duration to 0 if you have
  provided a value that is less than 0.
</p>
<h4 id="h_01HABV0K6EF1ZF35KQD5VVSN6X">Recording User Properties</h4>
<p>
  If you want to record some user information the SDK lets you do so by passing
  data as user details and custom properties.
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID -</span></strong><span data-preserver-spaces="true"> Device id is mandatory, if it is null or empty no data will be recorded.</span>
  </li>
  <li>
    <strong>userProperties -</strong>
    <span>It is a map of key/value pairs</span> and it should not be null or
    empty<span>. The accepted data types as a value are </span><span>"String", "Integer", "Double", and "Boolean". All other types will be ignored.</span>
  </li>
  <li>
    <strong>timestamp -</strong>
    <span data-preserver-spaces="true">It is time in milliseconds. It is not mandatory, and you may set it to <strong>null</strong>.</span>
  </li>
</ul>
<p>For example:</p>
<pre><code class="java hljs">Map&lt;String, Object&gt; userDetail = new HashMap&lt;&gt;();
userDetail.put("name", "Full Name");
userDetail.put("username", "username1");
userDetail.put("email", "user@gmail.com");
userDetail.put("organization", "Countly");
userDetail.put("phone", "000-111-000");
userDetail.put("gender", "M");
userDetail.put("byear", "1991");

//custom detail
userDetail.put("hair", "black");
userDetail.put("height", 5.9);
userDetail.put("marks", "{$inc: 1}");

Countly.instance().backendM().recordUserProperties("device-id", userDetail, 0);
</code></pre>
<p>
  <span>You may also perform certain manipulations to your custom property values, such as incrementing the current value on a server by a certain amount or storing an array of values under the same property.</span>
</p>
<p>
  <span>For example:</span>
</p>
<pre><code class="java hljs">Map&lt;String, Object&gt; operation = new HashMap&lt;&gt;();
userDetail.put("fav-colors", "{$push: black}");
userDetail.put("marks", "{$inc: 1}");

Countly.instance().backendM().recordUserProperties("device-id", userDetail, 0);
</code></pre>
<p>
  The keys for predefined <span>modification operation</span>s are as follows:
</p>
<div class="table-container">
  <table style="width: 427px;">
    <tbody>
      <tr>
        <th style="width: 86.0938px;">Key</th>
        <th style="width: 333.906px;">Description</th>
      </tr>
      <tr>
        <td style="width: 78.0938px;">$inc</td>
        <td style="width: 325.906px;">
          <span>increment used value by 1</span>
        </td>
      </tr>
      <tr>
        <td style="width: 78.0938px;">$mul</td>
        <td style="width: 325.906px;">
          <span>multiply value by the provided value</span>
        </td>
      </tr>
      <tr>
        <td style="width: 78.0938px;">$min</td>
        <td style="width: 325.906px;">
          <span>minimum value</span>
        </td>
      </tr>
      <tr>
        <td style="width: 78.0938px;">$max</td>
        <td style="width: 325.906px;">
          <span>maximal value</span>
        </td>
      </tr>
      <tr>
        <td style="width: 78.0938px;">$setOnce</td>
        <td style="width: 325.906px;">
          <span>set value if it does not exist</span>
        </td>
      </tr>
      <tr>
        <td style="width: 78.0938px;">$pull</td>
        <td style="width: 325.906px;">
          <span>remove value from an array</span>
        </td>
      </tr>
      <tr>
        <td style="width: 78.0938px;">$push</td>
        <td style="width: 325.906px;">
          <span>insert value to an array</span>
        </td>
      </tr>
      <tr>
        <td style="width: 78.0938px;">$addToSet</td>
        <td style="width: 325.906px;">
          <span>insert value to an array of unique values</span>
        </td>
      </tr>
    </tbody>
  </table>
  <h4 id="h_01HABV0K6ECC7ZMFD74ME9HEWZ">Recording Direct Requests</h4>
  <p>
    The SDK allows you to record direct requests to the server. To record a request
    you should provide the request data along with the device id and timestamp.
    Here are the details:
  </p>
  <ul>
    <li>
      <strong><span data-preserver-spaces="true">deviceID -</span></strong><span data-preserver-spaces="true"> Device id is mandatory, so if it is null or empty no data will be recorded.</span>
    </li>
    <li>
      <strong>requestData -</strong> <span>It is a map of key/value pairs</span>
      and it should not be null or empty<span>. The accepted data type for the value is </span><span>"String".</span>
    </li>
    <li>
      <strong>timestamp -</strong>
      <span data-preserver-spaces="true">It is time in milliseconds. It is not mandatory, and you may set it to <strong>null</strong>.</span>
    </li>
  </ul>
  <p>For example:</p>
  <pre><code class="java hljs">Map&lt;String, String&gt; requestData = new HashMap&lt;&gt;();
requestData.put("device_id", "device-id-2");
requestData.put("timestamp", "1646640780130");
requestData.put("key-name", "data");

Countly.instance().backendM().recordDirectRequest("device-id-1", requestData, 1646640780130L);
</code></pre>
  <p>
    <span data-preserver-spaces="true">Values in the 'requestData' map will override the base request's respective values. In the above example, 'timestamp' and 'device_id' will be overridden by their respective values in the base request.</span>
  </p>
  <p>
    <strong><span data-preserver-spaces="true">Note:</span></strong><span data-preserver-spaces="true"> 'sdk_name', 'sdk_version', and 'checksum256' are protected by default and their values will not be overridden by 'requestData'.</span><span data-preserver-spaces="true"></span>
  </p>
  <h3 id="h_01HABV0K6EKZG5YRJH47E2DY3Q">Getting the Request Queue Size</h3>
  <p>
    <span>In case you would like to get the size of the request queue, you can use:</span>
  </p>
  <pre><code class="java hljs">int queueSize = Countly.instance().backendM().getQueueSize();</code></pre>
  <p>
    It will return the number of requests in the memory request queue.
  </p>
  <h1 id="h_01HD3EHQ4A3HMEJSF4YP4CBZ8P">FAQ</h1>
  <h2 id="h_01HD3EJBRFM3FJ0F1P3K172TZV">
    <span>Where Does the SDK Store the Data?</span>
  </h2>
  <p>
    <span data-preserver-spaces="true">The Countly Java SDK stores data in a directory/file structure. All SDK-related files are stored inside the directory given with </span><strong><span data-preserver-spaces="true">sdkStorageRootDirectory</span></strong><span data-preserver-spaces="true"> parameter to the Config class during init. The SDK creates files for sessions, users, event queues, requests, crashes, and JSON storage to keep the device ID, migration version, etc.</span>
  </p>
  <h2 id="h_01HD3F2TTEZ5KF3H2MDYA7CF9B">
    <span>What Information Is Collected by the SDK?</span>
  </h2>
  <p>
    The data that SDKs gather to carry out their tasks and implement the necessary
    functionalities is mentioned in
    <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts#h_01HJ5MD0WB97PA9Z04NG2G0AKC">here</a>.
    It is saved locally before any of it is transferred to the server.
  </p>
  <p>
    When events are recorded, the time of when the event is recorded, will be
    collected
  </p>
  <p>
    Any other information like data in custom events, location, user profile
    information or other manual requests depends on what the developer decides
    to provide and is not collected by the SDK itself.
  </p>
</div>
