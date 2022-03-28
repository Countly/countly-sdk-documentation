<p>
  This document will guide you through the process of Countly SDK installation
  and it applies to version 20.11.0
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <span class="wysiwyg-font-size-large"><strong>Older documentation</strong></span>
  </p>
  <p>
    To access the documentation for version 19.09-sdk2-rc, click
    <a href="/hc/en-us/articles/4404187501465" target="_self" rel="undefined">here.</a>
  </p>
</div>
<p>
  The process of setting up Countly Java SDK includes 2 simple steps: adding SDK
  as a dependency to your project and initializing SDK. Once those are done, you'll
  have basic analytics on your server like users, sessions, devices, etc.
</p>
<h1>Adding SDK to the project</h1>
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
<pre>dependencies <span>{<br></span><span>    </span>implementation <span>"ly.count.sdk:java:19.09-sdk2-rc"<br></span><span>}</span></pre>
<p>Or as:</p>
<pre><code class="xml">&lt;dependency&gt;
	&lt;groupId&gt;ly.count.sdk&lt;/groupId&gt;
	&lt;artifactId&gt;java&lt;/artifactId&gt;
	&lt;version&gt;19.09-sdk2-rc&lt;/version&gt;
	&lt;type&gt;pom&lt;/type&gt;
&lt;/dependency&gt;</code></pre>
<h1 class="anchor-heading">SDK Integration</h1>
<h2 id="minimal-setup" class="anchor-heading">Minimal Setup</h2>
<p>
  To start Countly SDK, you need to create a config class and pass it to the
  <code>init</code> method. To that method, you also pass the path where countly
  can store its things.
</p>
<pre><code class="java">Config config = new Config("http://YOUR.SERVER.COM", "YOUR_APP_KEY")
                .enableTestMode()
                .setLoggingLevel(Config.LoggingLevel.DEBUG)
                .enableFeatures(Config.Feature.Events, Config.Feature.Sessions, Config.Feature.CrashReporting, Config.Feature.UserProfiles)
                .setDeviceIdStrategy(Config.DeviceIdStrategy.UUID);

File targetFolder = new File("d:\\__COUNTLY\\java_test\\");

Countly.init(targetFolder, config);</code></pre>
<p>
  In our <code>Config</code> instance we:
</p>
<ul>
  <li>
    Told SDK not to use HTTPS (note http:// in URL) and to send data to Countly
    server located at
    <a href="http://YOUR.SERVER.COM.">http://YOUR.SERVER.COM.</a> We also specified
    the app key (YOUR_APP_KEY).
  </li>
  <li>
    Enabled test mode (read - crash whenever in an inconsistent state, don't
    forget to disable it in Production!).
  </li>
  <li>
    Set logging level to DEBUG to make sure everything works as expected.
  </li>
  <li>
    Enabled crash reporting feature and tell SDK to use UUID strategy, that is
    random UUID string, as device id.
  </li>
</ul>
<h3 id="providing-the-application-key" class="anchor-heading">Providing the application key</h3>
<p>
  <span>Also called "AppKey" as shorthand. The application key is used to identify for which application this information is tracked. You receive this value by creating a new application in your Countly dashboard and accessing it in its application management screen.</span>
</p>
<p>
  <span><strong>Note:&nbsp;</strong>Ensure you are using the App Key (found under Management -&gt; Applications) and not the API Key. Entering the API Key will not work.</span>
</p>
<h3 id="providing-the-server-url" class="anchor-heading">Providing the server URL</h3>
<p>
  <span>If you are using Countly Enterprise Edition trial servers, use&nbsp;<code>https://try.count.ly</code>,&nbsp;<code>https://us-try.count.ly</code>&nbsp;or&nbsp;<code>https://asia-try.count.ly</code>&nbsp;It is basically the domain from which you are accessing your trial dashboard.</span>
</p>
<p>
  <span>If you use both Community Edition and Enterprise Edition, use your own domain name or IP address, such as&nbsp;</span><a href="https://example.com/"><span>https://example.com</span></a><span>&nbsp;or&nbsp;</span><a href="https://ip/"><span>https://IP</span></a><span>&nbsp;(if SSL has been set up).</span>
</p>
<h2 id="enabling-logging" class="anchor-heading">SDK logging / debug mode</h2>
<p>
  <span>The first thing you should do while integrating our SDK is enabling logging. If logging is enabled, then our SDK will print out debug messages about its internal state and encountered problems.&nbsp;</span>
</p>
<p>
  Set<span> <code class="java">setLoggingLevel</code></span><span>&nbsp;</span>on
  the config object to enable logging:
</p>
<pre><code class="java">Config config = new Config("http://YOUR.SERVER.COM", "YOUR_APP_KEY")
                .setLoggingLevel(Config.LoggingLevel.DEBUG)
                .enableFeatures(Config.Feature.Events, Config.Feature.Sessions, Config.Feature.CrashReporting, Config.Feature.UserProfiles)
                .setDeviceIdStrategy(Config.DeviceIdStrategy.UUID);</code></pre>
<h2 id="sdk-data-storage" class="anchor-heading">SDK data storage</h2>
<p>
  Countly SDK stores serialized versions of the following classes:
  <code>InternalConfig</code>, <code>SessionImpl</code>,
  <code>RequestImpl</code>, <code>CrashImpl</code>, <code>UserImpl</code> &amp;
  <code>TimedEvents</code>. All those are stored in device memory, in binary form,
  in separate files with filenames prefixed with <code>[CLY]_</code>.
</p>
<h2 id="sdk-notes" class="anchor-heading" tabindex="-1">SDK notes</h2>
<h3>Test mode</h3>
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
<h1>Events</h1>
<p>
  Events in Countly represent some meaningful event user performed in your application
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
    It's a Map&lt;String, String&gt; which can be filled with arbitrary data
    like {"category": "Pants", "size": "M"}.
  </li>
</ul>
<h2 id="recording-events" class="anchor-heading">Recording events</h2>
<p>
  The standard way of recording events is through your <code>Session</code> instance:
</p>
<pre><code class="java">Countly.session().event('purchase')
                    .setCount(2)
                    .setSum(19.98)
                    .setDuration(35)
                    .addSegments("category", "pants", "size", "M")
                .record();</code></pre>
<p>
  Please note the last method in that call chain, <code>.record()</code> call is
  required for the event to be recorded.
</p>
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
<h3 id="1-event-key-and-count" class="anchor-heading">1. Event key and count</h3>
<pre><code class="java hljs">Countly.session().events(<span class="hljs-string">"purchase"</span>).setCount(1).record();</code></pre>
<h3 id="2-event-key-count-and-sum" class="anchor-heading">2. Event key, count, and sum</h3>
<pre><code class="java hljs">Countly.session().events(<span class="hljs-string">"purchase"</span>).setCount(1).setSum(20.3).record();</code></pre>
<h3 id="3-event-key-and-count-with-segmentations" class="anchor-heading">3. Event key and count with segmentation(s)</h3>
<pre><code class="java hljs">HashMap&lt;String, String&gt; segmentation = <span class="hljs-keyword">new</span> HashMap&lt;String, Object&gt;();
segmentation.put(<span class="hljs-string">"country"</span>, <span class="hljs-string">"Germany"</span>);
segmentation.put(<span class="hljs-string">"app_version"</span>, <span class="hljs-string">"1.0"</span>);

Countly.session().events(<span class="hljs-string">"purchase"</span>).setCount(1).setSegmentation(segmentation).record();</code></pre>
<h3 id="4-event-key-count-and-sum-with-segmentations" class="anchor-heading">4. Event key, count, and sum with segmentation(s)</h3>
<pre><code class="java hljs">HashMap&lt;String, String&gt; segmentation = <span class="hljs-keyword">new</span> HashMap&lt;String, Object&gt;();
segmentation.put(<span class="hljs-string">"country"</span>, <span class="hljs-string">"Germany"</span>);
segmentation.put(<span class="hljs-string">"app_version"</span>, <span class="hljs-string">"1.0"</span>);

Countly.session().events(<span class="hljs-string">"purchase"</span>).setCount(1).setSum(34.5).setSegmentation(segmentation).record();</code></pre>
<h3 id="5-event-key-count-sum-and-duration-with-segmentations" class="anchor-heading">5. Event key, count, sum, and duration with segmentation(s)</h3>
<pre><code class="java hljs">HashMap&lt;String, String&gt; segmentation = <span class="hljs-keyword">new</span> HashMap&lt;String, Object&gt;();
segmentation.put(<span class="hljs-string">"country"</span>, <span class="hljs-string">"Germany"</span>);
segmentation.put(<span class="hljs-string">"app_version"</span>, <span class="hljs-string">"1.0"</span>);

Countly.session().events(<span class="hljs-string">"purchase"</span>).setCount(1).setSum(34.5).setDuration(5.3).setSegmentation(segmentation).record();;</code></pre>
<p>
  <span>Those are only a few examples of what you can do with events. You may extend those examples and use Country, app_version, game_level, time_of_day, and any other segmentation that will provide you with valuable insights.</span>
</p>
<h2>Timed events</h2>
<p>
  There is also a special type of <code>Event</code> supported by Countly - timed
  events. Timed events help you to track long continuous interactions when keeping
  an <code>Event</code> instance is not very convenient.
</p>
<p>The basic use case for timed events is following:</p>
<ul>
  <li>
    User starts playing a level "37" of your game, you call
    <code>Countly.session().timedEvent("LevelTime").addSegment("level", "37")</code>
    to start tracking how much time a user spends on this level.
  </li>
  <li>
    Then something happens when the user is at that level, for example, the user
    bought some coins. Along with regular "Purchase" event, you decide you want
    to segment the "LevelTime" event with purchase information:
    <code>Countly.session().timedEvent("LevelTime").setSum(9.99)</code>.
  </li>
  <li>
    Once the user stopped playing, you need to stop recording this event:
    <code>Countly.session().timedEvent("LevelTime").endAndRecord()</code>
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
  event for it to be recorded. Without <code>endAndRecord()</code> call, nothing
  will happen.
</p>
<h1>Sessions</h1>
<h2>Manual sessions</h2>
<p>
  Session in Countly is a single app launch or several app launches if the time
  between them is less than 30 seconds (by default). Of course, you can override
  this behavior.
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
<h1 id="user-profiles" class="anchor-heading" tabindex="-1">User profiles</h1>
<p>
  <span>For information about User Profiles, review&nbsp;</span><a href="http://resources.count.ly/docs/user-profiles"><span>this documentation</span></a>
</p>
<h2 id="setting-predefined-values" class="anchor-heading">Setting predefined values</h2>
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
<pre><code class="java">Countly.user(getApplicationContext()).edit()
        .setName("Firstname Lastname")
        .setUsername("nickname")
        .setEmail("test@test.com")
        .setOrg("Tester")
        .setPhone("+123456789")
        .commit();</code></pre>
<h2 id="setting-custom-values" class="anchor-heading">Setting custom values</h2>
<p>
  To set custom properties, call set(). To send modification operations, call the
  corresponding method:
</p>
<pre><code class="java">Countly.user(getApplicationContext()).edit()
        .set("mostFavoritePet", "dog")
        .inc("phoneCalls", 1)
        .pushUnique("tags", "fan")
        .pushUnique("skill", "singer")
        .commit();</code></pre>
<h1 id="device-id-management" class="anchor-heading" tabindex="-1">Device ID management</h1>
<p>
  <span>A device ID is a unique identifier for your users.&nbsp;</span><span>You may specify the device ID yourself or allow the SDK to generate it. When providing one yourself, keep in mind that it has to be unique for all users. Some potential sources for such an id may be the users username, email or some other internal ID used by your other systems.</span>
</p>
<h2 id="changing-device-id" class="anchor-heading">Changing device ID</h2>
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
<pre><code class="java hljs">Countly.<span>session</span>().changeDeviceIdWithMerge("New Device Id");</code></pre>
<p class="anchor-heading">
  <strong>Changing Device ID without server merge</strong>
</p>
<p>
  <span>You might want to track information about another separate user that starts using your app (changing apps account), or your app enters a state where you no longer can verify the identity of the current user (user logs out). In that case, you can change the current device ID to a new one without merging their data. You would call:</span>
</p>
<pre><code class="java hljs">Countly.<span>session</span>().changeDeviceIdWithoutMerge("New Device Id");</code></pre>
<p>
  <span>Doing it this way, will not merge the previously acquired data with the new id.</span>
</p>
<p>
  <span>Do note that every time you change your deviceId without a merge, it will be interpreted as a new user. Therefore implementing id management in a bad way could inflate the users count by quite a lot.</span>
</p>
<h2 id="retrieving-current-device-id&nbsp;" class="anchor-heading">Retrieving current device ID&nbsp;</h2>
<p>
  You may want to see what device id Countly is assigning for the specific device.
  For that, you may use the following calls.&nbsp;
</p>
<pre><code class="java hljs">Countly.<span>session</span>().getDeviceId()</code></pre>
<h1 id="other-features" class="anchor-heading" tabindex="-1">Other features</h1>
<h2 id="backend-mode" class="anchor-heading" tabindex="-1">Backend Mode</h2>
<div class="callout callout--info">
  <p class="callout__title">
    <span class="wysiwyg-font-size-large"><strong>Minimum Countly SDK Version</strong></span>
  </p>
  <p>
    The minimum SDK version requirement for this feature is 20.11.2.
  </p>
</div>
<p>
  Java SDK provides a special mode to transfer data to Countly Servers, called
  the 'Backend Mode'. It is useful when users have their data stored in one data
  store and want to transfer this data directly to the servers without storing
  it persistently beforehand.&nbsp;With the help of this mode, users are able to
  record and send data to their server without storing it locally.
</p>
<p>
  <strong>Note:</strong> When this mode is enabled, SDK enters into a special mode
  where all features (Sessions, Events, Views, Crash, User properties, Consents)
  will stop working. SDK keeps the data recorded during this mode in volatile memory
  and when the application is closed the data will be lost.
</p>
<h3>Enabling Backend Mode</h3>
<p>
  To enable Backend Mode you should create a config class and call
  <code class="java">enableBackendMode</code>on this object, and later you should
  pass it to the <code>init</code> method.
</p>
<pre><code class="java">Config config = new Config("http://YOUR.SERVER.COM", "YOUR_APP_KEY")
                .enableBackendMode()<br>                .setRequestQueueMaxSize(<span>500</span>)
                .setLoggingLevel(Config.LoggingLevel.DEBUG);

Countly.init(targetFolder, config);</code></pre>
<p>
  If the Backend Mode is enabled the SDK stores up to a maximum of 1000 requests
  by default. Then when this limit is exceeded the SDK will drop the oldest request
  from the queue in the memory. To change this request queue limit, call
  <code class="java">setRequestQueueMaxSize</code> on the
  <code class="java">Config</code>object before the SDK init.
</p>
<h3>Recording Data</h3>
<p>
  <span data-preserver-spaces="true">Users have to provide a device id, and optionally, the time in milliseconds every time they record any data. Device id is mandatory, so you can not set it null or not provide it while recording data.</span>
</p>
<p>
  <strong><span data-preserver-spaces="true">Note:</span></strong><span data-preserver-spaces="true">&nbsp;If the provided timestamp is null or less than 1, SDK updates its value to the current time in milliseconds.</span>
</p>
<h4>Recording an event</h4>
<p>
  <span data-preserver-spaces="true">You may record as many events as you want.</span>
</p>
<p>
  <span data-preserver-spaces="true">There are a couple of values that can be set when recording an event.&nbsp;</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID-</span></strong><span data-preserver-spaces="true">&nbsp;Device id is mandatory, if it is null or empty data will not be recorded.&nbsp;</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">key-</span></strong><span data-preserver-spaces="true">&nbsp;This is the main property which would be the identifier/name for that event. It is mandatory and the event will not be recorded if it is empty or null.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">count -</span></strong><span data-preserver-spaces="true">&nbsp;A whole positive numerical number value that marks how many times this event has happened. It is optional and if it is provided and its value is less than&nbsp;</span><strong><span data-preserver-spaces="true">1</span></strong><span data-preserver-spaces="true">, SDK will automatically set it to&nbsp;</span><strong><span data-preserver-spaces="true">1</span></strong><span data-preserver-spaces="true">.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">sum -</span></strong><span data-preserver-spaces="true">&nbsp;This value will be summed up across all events in the dashboard. It is optional and if provided, and it is less than&nbsp;</span><strong><span data-preserver-spaces="true">0</span></strong><span data-preserver-spaces="true">, SDK will automatically set it to&nbsp;</span><strong><span data-preserver-spaces="true">0</span></strong><span data-preserver-spaces="true">.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">duration -&nbsp;</span></strong><span data-preserver-spaces="true">This value is used for recording and tracking the duration of events. Set it to&nbsp;</span><strong><span data-preserver-spaces="true">0</span></strong><span data-preserver-spaces="true">&nbsp;if you don't want to report any duration.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">segmentation -&nbsp;</span></strong><span data-preserver-spaces="true">A map where you can provide custom data for your events to track additional information. It is not a mandatory field, so you may set it to&nbsp;</span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true">&nbsp;or&nbsp;</span><strong><span data-preserver-spaces="true">empty</span></strong><span data-preserver-spaces="true">.&nbsp;It is a map that consists of key and value pairs. The accepted data types for the values are&nbsp;"String", "Integer", "Double", and "Boolean". All other types will be ignored.</span>
  </li>
</ul>
<p>Example:</p>
<pre><code class="java">Map&lt;String, String&gt; segment = <span>new </span>HashMap&lt;String, String&gt;() {{<br>put(<span>"Time Spent"</span>, <span>"60"</span>);<br>put(<span>"Retry Attempts"</span>, <span>"60"</span>);<br>}};<br><br>Countly.<span>backendMode</span>().recordEvent(<span>"device-id"</span>, <span>"Event Key"</span>, <span>1</span>, <span>0</span>, <span>5</span>, segment, <span>1646640780130L</span>);</code></pre>
<h4>Recording a view</h4>
<p>
  <span data-preserver-spaces="true">You may record views by providing the view details in segmentation with timestamp.</span>
</p>
<p>
  <span data-preserver-spaces="true">There are a couple of values that can be set when recording an event.&nbsp;</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID-</span></strong><span data-preserver-spaces="true">&nbsp;Device id is mandatory, if it is null or empty data will not be recorded.&nbsp;</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">name-</span></strong><span data-preserver-spaces="true">&nbsp;It is the name of the view and it must not be empty or null.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">segmentation -&nbsp;</span></strong><span data-preserver-spaces="true">A map where you can provide custom data for your view to track additional information. It is not a mandatory field, you may set it to&nbsp;</span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true">&nbsp;or leave it&nbsp;</span><strong><span data-preserver-spaces="true">empty</span></strong><span data-preserver-spaces="true">.&nbsp;It is a map of key/value pairs and the accepted data types are&nbsp;"String", "Integer", "Double", and "Boolean". All other types will be ignored.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">timestamp -</span></strong><span data-preserver-spaces="true">&nbsp;It is time in milliseconds. It is not mandatory, and you may set it to null.</span>
  </li>
</ul>
<p>Example:</p>
<pre><code class="java">Map&lt;String, String&gt; segmentation = <span>new </span>HashMap&lt;String, String&gt;() {{<br>put(<span>"visit"</span>, <span>"1"</span>);<br>put(<span>"segment"</span>, <span>"Windows"</span>);<br>put(<span>"start"</span>, <span>"1"</span>);<br>}};<br><br>Countly.<span>backendMode</span>().recordView(<span>"device-id"</span>, <span>"SampleView"</span>, segmentation, <span>1646640780130L</span>);</code></pre>
<h4>Recording a crash</h4>
<p>
  <span>To report exceptions provide the following detail:</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID-</span></strong><span data-preserver-spaces="true">&nbsp;Device id is mandatory, and if it is null or not provide no data will be recorded.&nbsp;</span>
  </li>
  <li>
    <strong>message-</strong>&nbsp;
    <span>This is the main property which would be the identifier/name for that event. It should not be null or empty.</span><span></span>
  </li>
  <li>
    <strong>stacktrace-</strong>&nbsp;
    <span>A string that describes the contents of the call stack</span>. It
    <span data-preserver-spaces="true">is mandatory, and should not be null or empty.</span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">segmentation -&nbsp;</span></strong><span data-preserver-spaces="true">A map where you can provide custom data for your view to track additional information. It is not a mandatory field, so you may set it to&nbsp;</span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true">&nbsp;or leave it&nbsp;</span><strong><span data-preserver-spaces="true">empty</span></strong><span data-preserver-spaces="true">.&nbsp;It is a map of key/value pairs and the accepted data types are&nbsp;"String", "Integer", "Double", and "Boolean". All other types will be ignored.</span>
  </li>
  <li>
    <strong>timestamp -</strong>
    <span data-preserver-spaces="true">It is time in milliseconds. It is not mandatory, and you may set it to null.</span>
  </li>
</ul>
<pre><code class="java">Map&lt;String, String&gt; segmentation = <span>new </span>HashMap&lt;String, String&gt;() {{<br>    put(<span>"login page"</span>, <span>"authenticate request"</span>);<br>}};<br> Countly.<span>backendMode</span>().recordException(<span>"device-id"</span>, "message", "stacktrace", segmentation, null);</code></pre>
<p>
  You may also pass an instance of an exception instead of the message and the
  stacktrace to record a crash.
</p>
<p>For example:</p>
<pre><code class="java">Map&lt;String, String&gt; segmentation = <span>new </span>HashMap&lt;String, String&gt;() {{<br>    put(<span>"login page"</span>, <span>"authenticate request"</span>);<br>}};<br><span>try </span>{<br><span>    int </span>a = <span>10 </span>/ <span>0</span>;<br>} <span>catch </span>(Exception e) {<br>    Countly.<span>backendMode</span>().recordException(<span>"device-id"</span>, e, segmentation, null);<br>}</code></pre>
<h4>Recording sessions</h4>
<p>
  <span>To start a session please provide the following details:</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID-</span></strong><span data-preserver-spaces="true">&nbsp;Device id is mandatory, if it is null or empty data will not be recorded.&nbsp;</span>
  </li>
  <li>
    <strong>metrics-<span>&nbsp;</span></strong>It is a map that contains device
    and app information<span data-preserver-spaces="true"> as key value pairs.&nbsp;</span>
    It should not be null or empty<span> and the accepted data type for the pairs is </span><span>"String".</span>
  </li>
  <li>
    <strong>timestamp -</strong>
    <span data-preserver-spaces="true">It is time in milliseconds. It is not mandatory, and you may set it to <strong>null</strong>.</span><span data-preserver-spaces="true"></span>
  </li>
</ul>
<p>Example:</p>
<pre><code class="java">Map&lt;String, String&gt; metrics = <span>new </span>HashMap&lt;String, String&gt;() {{<br>    put(<span>"_os"</span>, <span>"Android"</span>);<br>    put(<span>"_os_version"</span>, <span>"10"</span>);<br>    put(<span>"_app_version"</span>, <span>"1.2"</span>);<br>}};<br>Countly.<span>backendMode</span>().sessionBegin(<span>"device-id"</span>, metrics, <span>1646640780130L</span>);</code><code class="java"></code><code class="java"></code></pre>
<p>
  <span>To update or end a session please provide the following details:</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID-</span></strong><span data-preserver-spaces="true"> Device id is mandatory, if it is null or empty no action will be taken.&nbsp;</span>
  </li>
  <li>
    <strong>duration-&nbsp;</strong>It is the duration of a session, you may
    pass <strong>0</strong> if you don't want to submit a duration.
  </li>
  <li>
    <strong>timestamp -</strong>
    <span data-preserver-spaces="true">It is time in milliseconds. It is not mandatory, and you may set it to <strong>null</strong>.</span>
  </li>
</ul>
<p>
  <span data-preserver-spaces="true">Session update:</span>
</p>
<pre><code class="java">double duration = 60;<br>Countly.<span>backendMode</span>().sessionUpdate(<span>"device-id"</span>, duration, null);</code></pre>
<p>Session end:</p>
<pre><code class="java">double duration = 20;<br>Countly.<span>backendMode</span>().sessionEnd(<span>"device-id"</span>, duration, 1223456767L);</code></pre>
<h4>
  Note: Java SDK automatically sets the duration to 0 if you have provided a value
  that is less than 0.
</h4>
<h4>Recording user properties</h4>
<p>
  If you want to record some user information the SDK lets you do so by passing
  data as user details and custom properties.&nbsp;
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">deviceID-</span></strong><span data-preserver-spaces="true"> Device id is mandatory, if it is null or empty no data will be recorded.&nbsp;</span>
  </li>
  <li>
    <strong>userProperties-</strong> <span>It is a map of key/value pairs</span>
    and it should not be null or empty<span>. The accepted data types as a value are&nbsp;</span><span>"String", "Integer", "Double", and "Boolean". All other types will be ignored.</span>
  </li>
  <li>
    <strong>timestamp -</strong>
    <span data-preserver-spaces="true">It is time in milliseconds. It is not mandatory, and you may set it to <strong>null</strong>.</span>
  </li>
</ul>
<p>For example:</p>
<pre><code class="java">Map&lt;String, Object&gt; userDetail = new HashMap&lt;&gt;();<br>userDetail.put("name", "Full Name");<br>userDetail.put("username", "username1");<br>userDetail.put("email", "user@gmail.com");<br>userDetail.put("organization", "Countly");<br>userDetail.put("phone", "000-111-000");<br>userDetail.put("gender", "M");<br>userDetail.put("byear", "1991");<br><br>//custom detail<br>userDetail.put("hair", "black");<br>userDetail.put("height", 5.9);<br>userDetail.put("marks", "{$inc: 1}");<br><br>Countly.<span>backendMode</span>().recordUserProperties(<span>"device-id"</span>, userDetail, <span>0</span>);</code><code class="java"></code></pre>
<p>
  <span>You may also perform certain manipulations to your custom property values, such as incrementing the current value on a server by a certain amount or storing an array of values under the same property.</span><span></span>
</p>
<p>
  <span>For example:</span>
</p>
<pre><code class="java">Map&lt;String, Object&gt; operation = new HashMap&lt;&gt;();<br>userDetail.put("fav-colors", "{$push: black}");<br>userDetail.put("marks", "{$inc: 1}");<br><br>Countly.<span>backendMode</span>().recordUserProperties(<span>"device-id"</span>, userDetail, <span>0</span>);</code></pre>
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
  <h4>Recording direct requests</h4>
  <p>
    The SDK allows you to record direct requests to the server. To record a request
    you should provide the request data along with the device id and timestamp.
    Here are the details:
  </p>
  <ul>
    <li>
      <strong><span data-preserver-spaces="true">deviceID-</span></strong><span data-preserver-spaces="true"> Device id is mandatory, so if it is null or empty no data will be recorded.&nbsp;</span>
    </li>
    <li>
      <strong>requestData-</strong> <span>It is a map of key/value pairs</span>
      and it should not be null or empty<span>. The accepted data type for the value is </span><span>"String".</span>
    </li>
    <li>
      <strong>timestamp -</strong>
      <span data-preserver-spaces="true">It is time in milliseconds. It is not mandatory, and you may set it to <strong>null</strong>.</span>
    </li>
  </ul>
  <p>For example:</p>
  <pre><code class="java">Map&lt;String, String&gt; requestData = <span>new </span>HashMap&lt;&gt;();<br>requestData.put(<span>"device_id"</span>, <span>"device-id-2"</span>);<br>requestData.put(<span>"timestamp"</span>, <span>"1646640780130"</span>);<br>requestData.put(<span>"key-name"</span>, <span>"data"</span>);<br><br>Countly.<span>backendMode</span>().recordDirectRequest("device-id-1", requestData, <span>1646640780130L</span>);</code></pre>
  <p>
    <span data-preserver-spaces="true">Values in the 'requestData' map will override the base request's respective values. In the above example, 'timestamp' and 'device_id' will be overridden by their respective values in the base request.</span>
  </p>
  <p>
    <strong><span data-preserver-spaces="true">Note:</span></strong><span data-preserver-spaces="true">&nbsp;'sdk_name', 'sdk_version', and 'checksum256' are protected by default and their values will not overridden by 'requestData'.</span><span data-preserver-spaces="true"></span>
  </p>
  <h3 id="checking-if-init-has-been-called" class="anchor-heading">Getting the request queue size</h3>
  <p>
    <span>In case you would like to get the size of the request queue, you can use:</span>
  </p>
  <pre><span><code class="java hljs">int queueSize = Countly.backendMode().getQueueSize();</code></span></pre>
  <p>
    It will return the number of requests of the request queue in the memory.
  </p>
</div>
