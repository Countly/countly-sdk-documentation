<p>
  Java SDK shares a common core with an alternative Android SDK.
</p>
<p>
  Process of setting up Countly Java SDK includes 2 simple steps: adding SDK as
  dependency to your project and initializing SDK. Once those are done, you'll
  have basic analytics on your server like users, sessions, devices, etc.
</p>
<h1>Adding SDK as a dependency</h1>
<p>
  SDK is hosted on bintray, more info can be found
  <a href="https://bintray.com/beta/#/countly/maven/java?tab=overview">here</a>.
  To add it, you first have to add Bintray Maven repository "https://dl.bintray.com/countly/maven".
</p>
<p>The dependency can be added as:</p>
<pre><code class="xml">&lt;dependency&gt;
	&lt;groupId&gt;ly.count.sdk&lt;/groupId&gt;
	&lt;artifactId&gt;java&lt;/artifactId&gt;
	&lt;version&gt;19.09-sdk2-rc&lt;/version&gt;
	&lt;type&gt;pom&lt;/type&gt;
&lt;/dependency&gt;</code></pre>
<h1>Initializing the Java SDK</h1>
<p>
  To start Countly SDK, you need to create a config class and pass it to the
  <code>init</code> method. To that method you also pass the path where countly
  can store it's things.
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
    Told SDK not to use https (note http:// in url) and to send data to Countly
    server located at
    <a href="http://YOUR.SERVER.COM.">http://YOUR.SERVER.COM.</a> We also specified
    app key (YOUR_APP_KEY).
  </li>
  <li>
    Enabled test mode (read - crash whenever in inconsistent state, don't forget
    to disable it in Production!).
  </li>
  <li>
    Set logging level to DEBUG to make sure everything works as expected.
  </li>
  <li>
    Enabled crash reporting feature and tell SDK to use UUID strategy, that is
    random UUID string, as device id.
  </li>
</ul>
<h1>Recording first event</h1>
<p>Now let's record our first custom event:</p>
<pre><code class="java">Countly.getSession().event("dummy").setCount(2).record();</code></pre>
<p>
  Countly will record an event with a key <code>purchase-btn</code> with sum of
  10 and will eventually send it to our Countly server with next request. You can
  also add segmentation, count and duration to an event.
</p>
<h1>Modifying user profile</h1>
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
<p>
  To set custom properties, call set(). To send modification operations, call corresponding
  method:
</p>
<pre><code class="java">Countly.user(getApplicationContext()).edit()
        .set("mostFavoritePet", "dog")
        .inc("phoneCalls", 1)
        .pushUnique("tags", "fan")
        .pushUnique("skill", "singer")
        .commit();</code></pre>
<h1>Storage</h1>
<p>
  Countly SDK stores serialized versions of following classes:
  <code>InternalConfig</code>, <code>SessionImpl</code>,
  <code>RequestImpl</code>, <code>CrashImpl</code>, <code>UserImpl</code> &amp;
  <code>TimedEvents</code>. All those are stored in device memory, in binary form,
  in separate files with filenames prefixed with <code>[CLY]_</code>.
</p>
<h1>Test mode</h1>
<p>
  To ensure correct SDK behaviour, please use
  <code>Config.enableTestMode()</code> when you app is in development and testing.
  In test mode Countly SDK raises <code>RuntimeException</code>s whenever is in
  inconsistent state. Once you remove <code>Config.enableTestMode()</code> call
  from your initialization sequence, SDK stops raising any
  <code>Exception</code>s and switches to logging errors instead (if logging wasn't
  specifically turned off). Without having test mode on during development you
  may encounter some important issues with data consistency in production.
</p>
<h1>Authentication</h1>
<p>
  With no special steps performed, SDK will count any new app install (see note
  above regarding device ID persistence) as new user. In some cases, like when
  you have some kind of authentication system in your app, that's not what you
  want. When actual person should be counted as one user in Countly irrespective
  of number of app installs this user has and when you can provide user id to Countly
  SDK, you should use <code>login</code> calls.
</p>
<h1>Sessions</h1>
<p>
  Session in Countly is a single app launch or several app launches if time between
  them is less than 30 seconds (by default). Of course you can override this behaviour.
</p>
<p>
  <code>Session</code> lifecycle methods include:
</p>
<ul>
  <li>
    session.begin() must be called when you want to send begin session request
    to the server. This request contains all device metrics: device, model, carrier,
    etc.
  </li>
  <li>
    session.update() can be called to send a session duration update to the server
    along with any events, user properties and any other data types supported
    by Countly SDK. Called each Config.sendUpdateEachSeconds seconds in auto
    session mode.
  </li>
  <li>
    session.end() must be called to mark end of session. All the data recorded
    since last session.update() or since session.begin() in case no updates have
    been sent yet, is sent in this request as well.
  </li>
</ul>
<h1>Events</h1>
<p>
  Events in Countly represent some meaningful event user performed in your application
  within a <code>Session</code>. Please avoid recording everything like all taps
  or clicks user performed. In case you do, it will be very hard to extract valuable
  information from generated analytics.
</p>
<p>
  An <code>Event</code> object contains following data types:
</p>
<ul>
  <li>
    <code>name</code>, or event key. Required. Unique string which identifies
    the event.
  </li>
  <li>
    <code>count</code> - number of times. Required, 1 by default. Like number
    of goods added to shopping basket.
  </li>
  <li>
    <code>sum</code> - sum of something, amount. Optional. Like total sum of
    the basket.
  </li>
  <li>
    <code>dur</code> - duration of the event. Optional. For example how much
    time user spent to checking out.
  </li>
  <li>
    <code>segmentation</code> - some data associated with the event. Optional.
    It's a Map&lt;String, String&gt; which can be filled with arbitary data like
    {"category": "Pants", "size": "M"}.
  </li>
</ul>
<p>
  Standard way of recording events is through your <code>Session</code> instance:
</p>
<pre><code class="java">Countly.session().event('purchase')
                    .setCount(2)
                    .setSum(19.98)
                    .setDuration(35)
                    .addSegments("category", "pants", "size", "M")
                .record();</code></pre>
<p>
  Please note last method in that call chain, <code>.record()</code> call is required
  for event to be recorded.
</p>
<p>
  Example above results in new event being recorded in current session. Event won't
  be sent to the server right away. Instead, Countly SDK will wait until one of
  following happens:
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
    <code>Session.update()</code> have been called by developer.
  </li>
  <li>
    <code>Session.end()</code> have been called by developer or by Countly SDK
    in case of automatic session control.
  </li>
</ul>
<h1>Timed events</h1>
<p>
  There is also special type of <code>Event</code> supported by Countly - timed
  events. Timed events help you to track long continuous interactions when keeping
  an <code>Event</code> instance is not very convenient.
</p>
<p>Basic use case for timed events is following:</p>
<ul>
  <li>
    User starts playing a level "37" of your game, you call
    <code>Countly.session().timedEvent("LevelTime").addSegment("level", "37")</code>
    to start tracking how much time user spends on this level.
  </li>
  <li>
    Then something happens when user is in that level, for example user bought
    some coins. Along with regular "Purchase" event, you decide you want to segment
    "LevelTime" event with purchase information:
    <code>Countly.session().timedEvent("LevelTime").setSum(9.99)</code>.
  </li>
  <li>
    Once user stopped playing, you need to stop recording this event:
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
    which levels are generating most revenue (sum per <code>level</code> segmentation);
  </li>
  <li>
    which levels are not generating revenue at all since you don't show ad there
    (0 sum in <code>level</code> segmentation).
  </li>
</ul>
<p>
  With timed events, there is one thing to keep in mind: you have to end timed
  event for it to be recorded. Without <code>endAndRecord()</code> call, nothing
  will happen.
</p>