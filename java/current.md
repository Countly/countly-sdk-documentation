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