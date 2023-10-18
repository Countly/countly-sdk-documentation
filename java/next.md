<p>
  This document will guide you through the process of Countly SDK installation
  and it applies to version 23.8.X
</p>
<div class="callout callout--info">
  <p>
    Click
    <a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-and-Installing-SDKs#h_01H9QCP8G8QD0W9EMHT11F2N8P" target="_self" rel="undefined">here, </a>to
    access the documentation for older SDK versions.
  </p>
</div>
<p>
  The Countly Java SDK supports minimum JDK version 8 (Java 8, JDK 1.8). You can
  reach the Countly Java SDK
  <a href="https://github.com/Countly/countly-sdk-java" target="_blank" rel="noopener noreferrer">here</a>.
  Also, you can inspect the sample application
  <a href="https://github.com/Countly/countly-sdk-java/blob/master/app-java/src/main/java/ly/count/java/demo/Example.java" target="_blank" rel="noopener noreferrer">here</a>
  to understand how most functionalities work.
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
<pre>buildscript <span>{<br></span><span>    </span>repositories <span>{<br></span><span>        </span>mavenCentral()<br>    <span>}<br></span><span>}</span></pre>
<p>The dependency can be added as:</p>
<pre>dependencies <span>{<br></span><span> </span>implementation <span>"ly.count.sdk:java:23.8.0"<br></span><span>}</span></pre>
<p>Or as:</p>
<pre><code class="xml">&lt;dependency&gt;
  &lt;groupId&gt;ly.count.sdk&lt;/groupId&gt;
  &lt;artifactId&gt;java&lt;/artifactId&gt;
  &lt;version&gt;23.8.0&lt;/version&gt;
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
<h2 id="h_01HABV0K6C1TBRCQBZJ45PE13H">SDK Logging Mode</h2>
<p>
  <span>The first thing you should do while integrating our SDK is enabling logging. If logging is enabled, then our SDK will print out debug messages about its internal state and encountered problems. These debug messages will be printed to the console.</span>
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
  In case you want to forward the SDK logs to your own logging mechanism, you would
  have a look at the
  <a href="#h_01GVR02HH6X27TPH3MS6TE08AT" target="_self">log listener section</a>.
</p>
<p>
  This logging level would have no influence over the log listener. That would
  always receive all the printed logs event if the logging level would be set to
  "OFF".
</p>
<h2 id="h_01HABV0K6C4TED33TF2K40S71H">SDK Data Storage</h2>
<p>
  Countly SDK stores serialized versions of the following classes:
  <code>InternalConfig</code>, <code>SessionImpl</code>, <code>EventQueue</code>,
  <code>RequestImpl</code>, <code>CrashImpl</code>, <code>UserImpl</code> &amp;
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
    like {"category": "Pants", "size": "M"}.
  </li>
</ul>
<h2 id="h_01HABV0K6CDJHPP9HBQG26BZYR">Recording Events</h2>
<p>
  The standard way of recording events is through your <code>Countly</code> instance's
  <code>events</code> interface:
</p>
<div>
  <pre><code class="java hljs">Map&lt;String, Object&gt; segmentation = new HashMap&lt;String, Object&gt;() {
  put("Time Spent", 60);
  put("Retry Attempts", 60);
};

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
  <span>We have provided an example of recording a&nbsp;</span><strong>purchase</strong><span>&nbsp;event below. Here is a quick summary of the information with which each usage will provide us:</span>
</p>
<ul>
  <li>
    Usage 1: how many times the&nbsp;<strong>purchase</strong><span>&nbsp;</span>event
    occurred.
  </li>
  <li>
    Usage 2: how many times the&nbsp;<strong>purchase</strong><span>&nbsp;</span>event
    occurred + the total amount of those purchases.
  </li>
  <li>
    Usage 3: how many times the&nbsp;<strong>purchase</strong><span>&nbsp;</span>event
    occurred +<span>&nbsp;</span><span>from which countries and application versions those purchases were made.</span>
  </li>
  <li>
    Usage 4: how many times the&nbsp;<strong>purchase</strong><span>&nbsp;</span>event
    occurred +&nbsp;<span>the total amount, both of which are also available, segmented into countries and application versions.</span>
  </li>
  <li>
    Usage 5: how many times the&nbsp;<strong>purchase</strong><span>&nbsp;</span>event
    occurred +<span>&nbsp;</span><span>the total amount, both of which are also available, segmented into countries and application versions + the total duration of those events.</span>
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
    values in a map like&nbsp;
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
<h2 id="h_01HABV0K6CR39VT9PG99M1M0WX">Manual Sessions</h2>
<p>
  In Countly Java SDK, a session starts with the launch of an application. This
  can occur upon a single instance of an app launch or multiple launches within
  a predefined time frame, typically set at 60 seconds by default.
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
    seconds in auto session mode.
  </li>
  <li>
    <code>session.end()</code>&nbsp;must be called to mark the end of the session.
    All the data recorded since the last <code>session.update()</code> or since
    <code>session.begin()</code> in case no updates have been sent yet, is sent
    in this request as well.
  </li>
</ul>
<h1 id="h_01HABV0K6CCY07B2BS5JVW72QQ">Device ID Management</h1>
<p>
  <span>A device ID is a unique identifier for your users.&nbsp;</span><span>You may specify the device ID yourself or allow the SDK to generate it. When providing one yourself, keep in mind that it has to be unique for all users. Some potential sources for such an id may be the users username, email or some other internal ID used by your other systems.</span>
</p>
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
<pre><code class="java hljs">Countly.session().changeDeviceIdWithMerge("New Device Id");</code></pre>
<p class="anchor-heading">
  <strong>Changing Device ID without server merge</strong>
</p>
<p>
  <span>You might want to track information about another separate user that starts using your app (changing apps account), or your app enters a state where you no longer can verify the identity of the current user (user logs out). In that case, you can change the current device ID to a new one without merging their data. You would call:</span>
</p>
<pre><code class="java hljs">Countly.session().changeDeviceIdWithoutMerge("New Device Id");</code></pre>
<p>
  <span>Doing it this way, will not merge the previously acquired data with the new id.</span>
</p>
<p>
  <span>Do note that every time you change your deviceId without a merge, it will be interpreted as a new user. Therefore implementing id management in a bad way could inflate the users count by quite a lot.</span>
</p>
<h2 id="h_01HABV0K6C0RVYQ6JWPQ2EXR55">Retrieving Current Device ID</h2>
<p>
  You may want to see what device id Countly is assigning for the specific device.
  For that, you may use the following calls.&nbsp;
</p>
<pre><code class="java hljs">Countly.session().getDeviceId()</code></pre>
<h1 id="h_01HAVQDM5V3Y4YRMCBYQH911M2">User Feedback</h1>
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
  related to that widget and then report the result manually.
</p>
<div class="callout callout--info">
  <p>
    For a sample integration, have a look at our
    <a href="https://github.com/Countly/countly-sdk-java/blob/master/app-java/src/main/java/ly/count/java/demo/Example.java" target="_blank" rel="noopener">sample code</a>
    at our github repo.
  </p>
</div>
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
  <span>For information about User Profiles, review&nbsp;</span><a href="/hc/en-us/articles/4403281285913">this documentation</a>
</p>
<h2 id="h_01HABV0K6CJR090QF0ZTKB1MNG">Setting Predefined Values</h2>
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
  To set standard properties, call respective methods of <code>UserEditor</code>:
</p>
<pre><code class="java hljs">Countly.api().user().edit()
  .setName("Firstname Lastname")
  .setUsername("nickname")
  .setEmail("test@test.com")
  .setOrg("Tester")
  .setPhone("+123456789")
  .commit();</code></pre>
<h2 id="h_01HABV0K6CJE3JS8YYM8TNYV9A">Setting Custom Values</h2>
<p>
  To set custom properties, call set(). To send modification operations, call the
  corresponding method:
</p>
<pre><code class="java hljs">Countly.api().user().edit()
  .set("mostFavoritePet", "dog")
  .inc("phoneCalls", 1)
  .pushUnique("tags", "fan")
  .pushUnique("skill", "singer")
  .commit();</code></pre>
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
    <strong>setApplicationName(String name)&nbsp;</strong>- Change application
    name reported to Countly server.
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
      <strong>setCustomDeviceId(String customDeviceId)&nbsp;</strong>- Set
      device id to specific string and strategy to
      <code>DeviceIdStrategy.CUSTOM_ID</code>.
    </div>
  </li>
  <li>
    <div>
      <strong>setLogListener(LogCallback logCallback)</strong> - Add a log
      callback that will duplicate all logs done by the SDK.
    </div>
  </li>
</ul>
<h2 id="h_01HAXVT7C5GTQ0D0HRCZ83J0VQ">Setting Event Queue Threshold</h2>
<p>
  Events get grouped together and are sent either every minute or after the unsent
  event count reaches a threshold. By default it is 10. If you would like to change
  this, call:
</p>
<pre>config.setEventQueueSizeToSend(<span>6</span>);</pre>
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
<h2 id="h_01GVR02HH6X27TPH3MS6TE08AT">Log Listener</h2>
<p>
  To listen to the SDK's internal logs, you can call <code>setLogListener</code><span> on the <code>Config</code> Object. If set, SDK will forward its internal logs to this listener regardless of SDK's <code>loggingLevel</code> . </span>
</p>
<pre><code class="java hljs">config.setLogListener(new LogCallback() {
  @Override
  public void LogHappened(String logMessage, Config.LoggingLevel logLevel) {
    //print log
  }
});
</code></pre>
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
  <span data-preserver-spaces="true">There are a couple of values that can be set when recording an event.&nbsp;</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID-</span></strong><span data-preserver-spaces="true"> Device id is mandatory, it can not be empty or null.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">key-</span></strong><span data-preserver-spaces="true"> This is the main property which would be the identifier/name for that event. It is mandatory and it can not be empty or null.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">count -</span></strong><span data-preserver-spaces="true">&nbsp;A whole positive numerical number value that marks how many times this event has happened. It is optional and if it is provided and its value is less than&nbsp;</span><strong><span data-preserver-spaces="true">1</span></strong><span data-preserver-spaces="true">, SDK will automatically set it to&nbsp;</span><strong><span data-preserver-spaces="true">1</span></strong><span data-preserver-spaces="true">.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">sum -</span></strong><span data-preserver-spaces="true"> This value will be summed up across all events in the dashboard. It is optional you may set it <strong>null</strong>.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">duration -&nbsp;</span></strong><span data-preserver-spaces="true">This value is used for recording and tracking the duration of events. Set it to&nbsp;</span><strong><span data-preserver-spaces="true">0</span></strong><span data-preserver-spaces="true">&nbsp;if you don't want to report any duration.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">segmentation -&nbsp;</span></strong><span data-preserver-spaces="true">A map where you can provide custom data for your events to track additional information. It is not a mandatory field, so you may set it to&nbsp;</span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true">&nbsp;or&nbsp;</span><strong><span data-preserver-spaces="true">empty</span></strong><span data-preserver-spaces="true">.&nbsp;It is a map that consists of key and value pairs. The accepted data types for the values are&nbsp;"String", "Integer", "Double", and "Boolean". All other types will be ignored.</span>
  </li>
</ul>
<p>Example:</p>
<pre><code class="java hljs">Map&lt;String, String&gt; segment = new HashMap&lt;String, String&gt;() {{
  put("Time Spent", "60");
  put("Retry Attempts", "60");
}};

Countly.backendMode().recordEvent("device-id", "Event Key", 1, 10.5, 5, segment, 1646640780130L);
</code></pre>
<p>
  <strong>Note: </strong>Device ID and 'key' both are mandatory. The event will
  not be recorded if any of these two parameters is null or empty.&nbsp;
</p>
<h4 id="h_01HABV0K6DRZ993XGKMFF29MGF">Recording a View</h4>
<p>
  <span data-preserver-spaces="true">You may record views by providing the view details in segmentation with a timestamp.</span>
</p>
<p>
  <span data-preserver-spaces="true">There are a couple of values that can be set when recording an event.&nbsp;</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID -</span></strong><span data-preserver-spaces="true">&nbsp;Device id is mandatory, if it is null or empty data will not be recorded.&nbsp;</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">name -</span></strong><span data-preserver-spaces="true">&nbsp;It is the name of the view and it must not be empty or null.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">segmentation -&nbsp;</span></strong><span data-preserver-spaces="true">A map where you can provide custom data for your view to track additional information. It is not a mandatory field, you may set it to&nbsp;</span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true">&nbsp;or leave it&nbsp;</span><strong><span data-preserver-spaces="true">empty</span></strong><span data-preserver-spaces="true">.&nbsp;It is a map of key/value pairs and the accepted data types are&nbsp;"String", "Integer", "Double", and "Boolean". All other types will be ignored.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">timestamp -</span></strong><span data-preserver-spaces="true">&nbsp;It is time in milliseconds. It is not mandatory, and you may set it to null.</span>
  </li>
</ul>
<p>Example:</p>
<pre><code class="java hljs">Map&lt;String, String&gt; segmentation = new HashMap&lt;String, String&gt;() {{
  put("visit", "1");
  put("segment", "Windows");
  put("start", "1");
}};

Countly.backendMode().recordView("device-id", "SampleView", segmentation, 1646640780130L);
</code></pre>
<p>
  <strong>Note:&nbsp;</strong>Device ID and 'name' both are mandatory. The view
  will not be recorded if any of these two parameters is null or empty.
</p>
<h4 id="h_01HABV0K6D86BYQ81T2VGYZJKM">Recording a Crash</h4>
<p>
  <span>To report exceptions provide the following detail:</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID -</span></strong><span data-preserver-spaces="true"> Device id is mandatory, and if it is null or not provided no data will be recorded.&nbsp;</span>
  </li>
  <li>
    <strong>message -</strong>&nbsp;
    <span>This is the main property which would be the identifier/name for that event. It should not be null or empty.</span><span></span>
  </li>
  <li>
    <strong>stacktrace -</strong>&nbsp;
    <span>A string that describes the contents of the call stack</span>. It
    <span data-preserver-spaces="true">is mandatory, and should not be null or empty.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">segmentation -&nbsp;</span></strong><span data-preserver-spaces="true">A map where you can provide custom data for your view to track additional information. It is not a mandatory field, so you may set it to&nbsp;</span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true">&nbsp;or leave it&nbsp;</span><strong><span data-preserver-spaces="true">empty</span></strong><span data-preserver-spaces="true">.&nbsp;It is a map of key/value pairs and the accepted data types are&nbsp;"String", "Integer", "Double", and "Boolean". All other types will be ignored.</span>
  </li>
  <li>
    <strong>crashDetail - </strong><span data-preserver-spaces="true">It is not a mandatory field, so you may set it to&nbsp;</span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true">&nbsp;or leave it&nbsp;</span><strong><span data-preserver-spaces="true">empty</span></strong><span data-preserver-spaces="true">. It is a map of key/value pairs. To know more about crash parameters, <a href="https://support.count.ly/hc/en-us/articles/360037753291-SDK-development-guide#01H821RTQ20M61EKN76EY6RJ84" target="_self">click here</a>.</span><span data-preserver-spaces="true"></span>
  </li>
  <li>
    <strong>timestamp -</strong>
    <span data-preserver-spaces="true">It is time in milliseconds. It is not mandatory, and you may set it to null.</span>
  </li>
</ul>
<pre><code class="java hljs">Map&lt;String, String&gt; segmentation = new HashMap&lt;String, String&gt;() {{
  put("login page", "authenticate request");
}};

Map&lt;String, String&gt; crashDetails = new HashMap&lt;String, String&gt;() {{
  put("_os", "Windows 11");
  put("_os_version", "11.202");
  put("_logs", "main page");
}};

Countly.backendMode().recordException("device-id", "message", "stacktrace", segmentation, crashDetails, null);
</code></pre>
<p>
  You may also pass an instance of an exception instead of the message and the
  stack trace to record a crash.
</p>
<p>For example:</p>
<pre><code class="java hljs">Map&lt;String, String&gt; segmentation = new HashMap&lt;String, String&gt;() {{
  put("login page", "authenticate request");
}};

Map&lt;String, String&gt; crashDetails = new HashMap&lt;String, String&gt;() {{
  put("_os", "Windows 11");
  put("_os_version", "11.202");
  put("_logs", "main page");
}};

try {
  int a = 10 / 0;
} catch(Exception e) {
  Countly.backendMode().recordException("device-id", e, segmentation, crashDetails, null);
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
    <strong><span data-preserver-spaces="true">deviceID -</span></strong><span data-preserver-spaces="true">&nbsp;Device id is mandatory, if it is null or empty data will not be recorded.&nbsp;</span>
  </li>
  <li>
    <strong>metrics -<span>&nbsp;</span></strong>It is a map that contains device
    and app information<span data-preserver-spaces="true"> as key-value pairs.&nbsp;</span>
    It can be null or empty<span> and the accepted data type for the pairs is </span><span>"String".</span>
  </li>
  <li>
    <strong>location - </strong><span data-preserver-spaces="true">It is not a mandatory field, so you may set it to&nbsp;</span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true">&nbsp;or leave it&nbsp;</span><strong><span data-preserver-spaces="true">empty</span></strong><span data-preserver-spaces="true">. It is a map of key/value pairs and the accepted keys are "city", "country_code", "ip_address", and "location".</span>
  </li>
  <li>
    <strong>timestamp -</strong>
    <span data-preserver-spaces="true">It is time in milliseconds. It is not mandatory, and you may set it to <strong>null</strong>.</span><span data-preserver-spaces="true"></span>
  </li>
</ul>
<p>Example:</p>
<pre><code class="java hljs">Map&lt;String, String&gt; metrics = new HashMap&lt;String, String&gt;() {{
  put("_os", "Android");
  put("_os_version", "10");
  put("_app_version", "1.2");
}};

Map&lt;String, String&gt; location = new HashMap&lt;String, String&gt;() {{
  put("ip_address", "192.168.1.1");
  put("city", "Lahore");
  put("country_code", "PK");
  put("location", "31.5204,74.3587");
}};

Countly.backendMode().sessionBegin("device-id", metrics, location, 1646640780130L);
</code></pre>
<p>
  <strong>Note:&nbsp;</strong>In above example '_os', '_os_version' and '_app_version'
  are predefined metrics keys. To know more about metrics, click
  <a href="https://support.count.ly/hc/en-us/articles/360037753291-SDK-development-guide#01H821RTQ2TZF21BH3ZSR8XHNW" target="_self">here.</a>
</p>
<p>
  <span>To update or end a session please provide the following details:</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID -</span></strong><span data-preserver-spaces="true"> Device id is mandatory, if it is null or empty no action will be taken.&nbsp;</span>
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
Countly.backendMode().sessionUpdate("device-id", duration, null);
</code></pre>
<p>Session end:</p>
<pre><code class="java hljs">double duration = 20;
Countly.backendMode().sessionEnd("device-id", duration, 1223456767L);
</code></pre>
<p>
  <strong>Note:</strong> Java SDK automatically sets the duration to 0 if you have
  provided a value that is less than 0.
</p>
<h4 id="h_01HABV0K6EF1ZF35KQD5VVSN6X">Recording User Properties</h4>
<p>
  If you want to record some user information the SDK lets you do so by passing
  data as user details and custom properties.&nbsp;
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID -</span></strong><span data-preserver-spaces="true"> Device id is mandatory, if it is null or empty no data will be recorded.&nbsp;</span>
  </li>
  <li>
    <strong>userProperties -</strong>
    <span>It is a map of key/value pairs</span> and it should not be null or
    empty<span>. The accepted data types as a value are&nbsp;</span><span>"String", "Integer", "Double", and "Boolean". All other types will be ignored.</span>
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

Countly.backendMode().recordUserProperties("device-id", userDetail, 0);
</code></pre>
<p>
  <span>You may also perform certain manipulations to your custom property values, such as incrementing the current value on a server by a certain amount or storing an array of values under the same property.</span><span></span>
</p>
<p>
  <span>For example:</span>
</p>
<pre><code class="java hljs">Map&lt;String, Object&gt; operation = new HashMap&lt;&gt;();
userDetail.put("fav-colors", "{$push: black}");
userDetail.put("marks", "{$inc: 1}");

Countly.backendMode().recordUserProperties("device-id", userDetail, 0);
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
      <strong><span data-preserver-spaces="true">deviceID -</span></strong><span data-preserver-spaces="true"> Device id is mandatory, so if it is null or empty no data will be recorded.&nbsp;</span>
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

Countly.backendMode().recordDirectRequest("device-id-1", requestData, 1646640780130L);
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
  <pre><code class="java hljs">int queueSize = Countly.backendMode().getQueueSize();</code></pre>
  <p>
    It will return the number of requests in the memory request queue.
  </p>
</div>