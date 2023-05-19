<p>
  This document will guide you through the process of SDK installation and it applies
  to version 23.2.X.
</p>
<div class="callout callout--info">
  <p>
    Click
    <a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-and-Installing-SDKs#c-sdks" target="_blank" rel="noopener">here, </a>to
    access the documentation for older SDK versions.
  </p>
</div>
<p>
  It is an open-source SDK, you can take a look at our SDK code in the
  <a href="https://github.com/Countly/countly-sdk-cpp/" target="_self" rel="undefined">Github repo</a>
</p>
<p>
  <strong>Supported Platforms:</strong> Windows, GNU/Linux, and Mac OS X.
</p>
<h1 id="AddingTheSdkToTheProject">Adding the SDK to the Project</h1>
<p>
  Countly C++ SDK has been designed to work with very few dependencies in order
  to run on most platforms. To build this SDK, you need:
</p>
<ul>
  <li>C++ compiler with C++14 support</li>
  <li>libcurl (with openssl) and its headers if you are on *nix</li>
  <li>cmake &gt;= 3.13</li>
</ul>
<p>First, clone the repository with its submodules:</p>
<div>
  <pre><code>git clone --recursive https://github.com/Countly/countly-sdk-cpp</code></pre>
</div>
<p>
  If submodules in your project are empty you can run this command at root of your
  project:
</p>
<div>
  <pre><code>git submodule update --init --recursive</code></pre>
</div>
<p>
  If you want to use SQLite to store session data persistently, build sqlite:
</p>
<div>
  <pre><code># assuming we are on project root
cd vendor/sqlite
cmake -D BUILD_SHARED_LIBS=ON -B build . # out of source build, we don't like clutter :)
# we define `BUILD_SHARED_LIBS` because sqlite's cmake file compiles statically by default for some reason
cd build
make # you might want to add something like -j8 to parallelize the build process</code></pre>
</div>
<p>The cmake build flow is pretty straightforward:</p>
<div>
  <pre><code># assuming we are on project root again
ccmake -B build . # this will launch a TUI, configure the build as you see fit
cd build
make</code></pre>
  <p>
    In case you would also need to install the built library, check for more
    information
    <a href="#additional-project-install-option" target="_self">here</a>.
  </p>
  <p>
    Build with the option <code>COUNTLY_BUILD_TESTS</code> and
    <code>COUNTLY_BUILD_SAMPLE</code><strong>ON</strong> to build executables
    to run the tests and the sample app. Also set the
    <code>COUNTLY_USE_SQLITE</code><strong>ON</strong> to use SQLite in your
    project.
  </p>
  <div>
    <pre><code>cmake -DCOUNTLY_BUILD_SAMPLE=ON -DCOUNTLY_BUILD_TESTS=ON -DCOUNTLY_USE_SQLITE=ON -B build . # or do it interactively with cmake
cd build
make ./countly-tests   # run unit test<br>make ./countly-sample  # run sample app</code></pre>
  </div>
</div>
<h1>SDK Integration</h1>
<h2>Minimal Setup</h2>
<p>
  Before you can use any functionality, you have to initiate the SDK.
</p>
<p>
  The shortest way to initiate the SDK is with this code snippet:
</p>
<pre><code>cly::Countly&amp; countly = cly::Countly::getInstance();<br>countly.setDeviceID(<span class="pl-s"><span class="pl-pds">"test-device-id<span class="pl-pds">");<br>countly.start(<span class="pl-s"><span class="pl-pds">"YOUR_APP_KEY<span class="pl-pds">", <span class="pl-s"><span class="pl-pds">"https://try.count.ly<span class="pl-pds">", 443, true);</span></span></span></span></span></span></span></span></span></code></pre>
<p>
  Here, you have to provide your appKey, and your Countly server URL. Please check
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#acquiring-your-application-key-and-server-url">here</a>
  for more information on how to acquire your application key (APP_KEY) and server
  URL.
</p>
<p>
  The third parameter with type<code>int</code> is a virtual port number and it
  is an optional parameter with a default value of <strong>0 </strong>(expected
  range is 0 to 65535).<br>
  The last <code>bool</code> parameter is also optional with the default value
  of <code>false</code>. When you set this value to <code>true</code> SDK automatically
  extends the session every 60 seconds.
</p>
<div class="callout callout--info">
  <p>
    If you are in doubt about the correctness of your Countly SDK integration,
    you can learn more about methods to verify it from
    <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#how-to-validate-your-countly-integration" target="blank">here</a>.
  </p>
</div>
<h2>SDK Logging</h2>
<p>
  The first thing you should do while integrating our SDK is to enable logging.
  If logging is enabled, then our SDK will print out debug messages about its internal
  state and about encountered problems.
</p>
<p>
  Set <code>setLogger(logger_function)</code> on the <code>Counlty</code> object
  to enable logging:
</p>
<pre><span class="pl-k"><code>void <span class="pl-en">printLog(cly::Countly::LogLevel level, const string&amp; msg) {...}<br>...<br><br>void (*logger_function)(cly::Countly::LogLevel level, const std::string&amp; message);<br>logger_function = printLog;<br>cly::Countly::getInstance().setLogger(logger_function);</span></code></span></pre>
<h2>Device ID</h2>
<p>
  All tracked information is tied to a "device ID", which is used as a unique identifier
  of your users.
</p>
<p>
  You have to specify the device ID by yourself (it has to be unique for each of
  your users). It may be an email or some other internal ID used in your system's
  internal logic.
</p>
<div>
  <pre><code>cly::Countly::getInstance().setDeviceID("UNIQUE_DEVICE_ID");</code></pre>
</div>
<h2>SDK Data Storage</h2>
<p>
  In its unconfigured state, the SDK stores everything in memory.
</p>
<p>
  There is an alternative SDK configuration option where the SDK will try to save
  data peristently with SQLite. In that case you would provide a path and filename
  where the database would be located. More information on that can be found
  <a href="#SettingUpSQLiteStorage">here</a>.
</p>
<h2>SDK Notes</h2>
<p>
  To access the Countly Global Instance use the following code snippet:
</p>
<pre><code>cly::Countly::getInstance().</code></pre>
<h1>Crash Reporting</h1>
<p>
  The Countly SDK for C++ can collect
  <a style="background-color: #ffffff;" href="http://resources.count.ly/docs/introduction-to-crash-reporting-and-analytics">Crash Reports</a>,
  which you may examine and resolve later on the server.
</p>
<p>
  In the SDK all crash-related functionalities can be browsed from the returned
  interface on:
</p>
<pre><code class="java">countly.crash().</code></pre>
<h2>Handled Exceptions</h2>
<p>
  You might catch an exception or similar error during your app’s runtime. You
  may also log these handled exceptions to monitor how and when they are happening.
  To log handled exceptions use the following code snippet:
</p>
<pre><code class="java">/*any additional info can be provided as a segmentation*/<br>std::map&lt;std::string, std::string&gt; segmentation = {<br>{"platform", "ubuntu"},<br>{"time", "60"},<br>};<br><br>/*should create the crashMetrics map*/<br>std::map&lt;std::string, std::any&gt; crashMetrics;<br><br>/*mandatory values*/<br>crashMetrics["_os"] = "Android"; # your OS info<br>crashMetrics["_app_version"] = "1.22";<br><br>/*any optional info*/<br>crashMetrics["_cpu"] = "armv7"; <br><br><span class="wysiwyg-color-black">countly.crash().recordException("title", "stackTrace", true, crashMetrics, segmentation);</span></code></pre>
<p>
  <code>recordException</code> expects the parameters below:
</p>
<ul>
  <li>
    <code>title</code> - a string that describes the exception.
  </li>
  <li>
    <code>stackTrace</code> - a string that describes the contents of the call
    stack.
  </li>
  <li>
    <code>fatal</code> - set true if the error is fatal.
  </li>
  <li>
    <code>crashMetrics</code> - key/values contain device information e.g., app
    version, OS.
  </li>
  <li>
    <code>segments</code> - custom key/values to be reported.
  </li>
</ul>
<p>
  <code>crashMetrics</code> is a map that contains the core information about the
  crash you want to capture and report. If it is not properly formed, your Countly
  server would not be able to recognize and interpret your crash report and you
  would not be able to observe the error from your server. There are two mandatory
  key-value pairs that you need to fill when forming the
  <code>crashMetrics</code> object. These are _os and_app_version keys. Any other
  keys are optional, so you can add more key-value pairs to form a detailed crash
  report from the available options shown below:
</p>
<pre><code class="java">std::map&lt;std::string, std::any&gt; crashMetrics;<br><br>/*mandatory values*/<br>crashMetrics[<span class="hljs-string">"_os"] = <span class="hljs-string">"Android"; /*your OS info*/<br>crashMetrics[<span class="hljs-string">"_app_version"] = <span class="hljs-string">"22.06.1"; /*SDK version*/<br><br>/*optional values*/<br>crashMetrics[<span class="hljs-string">"_os_version"] = <span class="hljs-string">"4.1";<br>crashMetrics[<span class="hljs-string">"_manufacture"] = <span class="hljs-string">"Samsung"; /*may not be provided for ios or be constant, like Apple*/<br>crashMetrics[<span class="hljs-string">"_device"] = <span class="hljs-string">"Galaxy S4"; /*model for Android, iPhone1,1 etc for iOS*/<br>crashMetrics[<span class="hljs-string">"_resolution"] = <span class="hljs-string">"1900x1080"; /*SDK version*/<br>crashMetrics[<span class="hljs-string">"_cpu"] = <span class="hljs-string">"armv7"; /*type of cpu used on device (for ios will be based on device)*/<br>crashMetrics[<span class="hljs-string">"_opengl"] = <span class="hljs-string">"2.1"; /*version of open gl supported*/<br>crashMetrics[<span class="hljs-string">"_ram_current"] = 1024; /*in megabytes*/<br>crashMetrics[<span class="hljs-string">"_ram_total"] = 4096; /*in megabytes*/<br>crashMetrics[<span class="hljs-string">"_disk_current"] = 3000; /*in megabytes*/<br>crashMetrics[<span class="hljs-string">"_disk_total"] = 10240; /*in megabytes*/<br>crashMetrics[<span class="hljs-string">"_bat"] = 99; /*battery level from 0 to 100*/<br>crashMetrics[<span class="hljs-string">"_orientation"] = <span class="hljs-string">"portrait"; /*in which device was held, landscape, portrait, etc*/<br>crashMetrics[<span class="hljs-string">"_root"] = f<span class="hljs-string">alse; /*true if device is rooted/jailbroken, false or not provided if not*/<br>crashMetrics[<span class="hljs-string">"_online"] = f<span class="hljs-string">alse; /*true if device is connected to the internet (WiFi or 3G), false or not provided if not connected*/<br>crashMetrics[<span class="hljs-string">"_muted"] = f<span class="hljs-string">alse; /*true if volume is off, device is in muted state*/<br>crashMetrics[<span class="hljs-string">"_background"] = f<span class="hljs-string">alse; /*true if app was in background when it crashed*/<br>crashMetrics[<span class="hljs-string">"_run"] = 2000; /*running time since app start in seconds*/</span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></span></code></pre>
<h2>Crash Breadcrumbs</h2>
<p>
  Throughout your app, you can leave crash breadcrumbs. They are short string logs
  that would ideally describe the previous steps that were taken in your app before
  the crash. After a crash happens, they will be sent together with the crash report.
</p>
<p>The following command adds a crash breadcrumb:</p>
<pre><code class="java">countly.crash().addBreadcrumb("breadcrumb");</code></pre>
<h1>Events</h1>
<p>
  <span style="font-weight: 400;">An <a href="http://resources.count.ly/docs/custom-events"><span style="font-weight: 400;">event</span></a><span style="font-weight: 400;"> is any type of action that you can send to a Countly instance, e.g. purchases, changed settings, view enabled, and so on, letting you get valuable information about your application. </span></span>
</p>
<p>
  There are a couple of values that can be set when recording an event. The main
  one is the <strong>key</strong> property which would be the identifier/name for
  that event. For example, in case a user buys an item in your game, you can create
  an event with the key 'purchase' to inform this action on your Countly server.
</p>
<p>
  Optionally there are also other properties that you might want to set:
</p>
<ul>
  <li>
    <strong>count -</strong> a whole numerical value that marks how many times
    this event has happened. The default value for this is <strong>1</strong>.
  </li>
  <li>
    <strong>sum -</strong> This value would be summed across all events in the
    dashboard. For example, for in-app purchase events, it can be the sum of
    purchased items. Its default value is <strong>0</strong>.
  </li>
  <li>
    <strong>duration - </strong>For recording and tracking the duration of events.
    The default value is <strong>0</strong>.
  </li>
  <li>
    <strong>segments - </strong>A value where you can provide custom segmentation
    for your events to track additional information. It is a key and value map.
    The accepted data type for the value is
    <span style="font-weight: 400;"><code class="java">std::string</code>. </span>
  </li>
</ul>
<h2>Recording Events</h2>
<p>
  <span style="font-weight: 400;">Here are some examples below, showing how to record an event for a <strong>purchase</strong> with varying levels of complexity<span style="font-weight: 400;">: </span></span>
</p>
<ul>
  <li>
    Usage 1: Times the <strong>purchase</strong> event occurred.
  </li>
  <li>
    Usage 2: Times the <strong>purchase</strong> event occurred + the total amount
    of those purchases.
  </li>
  <li>
    Usage 3: Times the <strong>purchase</strong> event occurred +
    <span style="font-weight: 400;">origin of the purchase. </span>
  </li>
  <li>
    Usage 4: Times the <strong>purchase</strong> event occurred +
    <span style="font-weight: 400;">the total amount + origin of the purchase. </span>
  </li>
  <li>
    Usage 5: Times the <strong>purchase</strong> event occurred +
    <span style="font-weight: 400;">the total amount + origin of the purchase + the total duration of those events. </span>
  </li>
</ul>
<p>
  <strong>1. Event key and count</strong>
</p>
<pre><code class="java">cly::Countly::getInstance().RecordEvent("purchase", 1);</code></pre>
<p>
  <strong>2. Event key, count, and sum</strong>
</p>
<pre><code class="java">cly::Countly::getInstance().RecordEvent("purchase", 1, 0.99);</code></pre>
<p>
  <strong>3. Event key and count with segmentation(s)</strong>
</p>
<pre><code class="java">std::map&lt;std::string, std::string&gt; segmentation;<br>segmentation["country"] = "Germany";<br><br>cly::Countly::getInstance().RecordEvent("purchase", segmentation, 1);<br></code></pre>
<p>
  <strong>4. Event key, count, and sum with segmentation(s)</strong>
</p>
<pre><code class="java">std::map&lt;std::string, std::string&gt; segmentation;<br>segmentation["country"] = "Germany";<br><br>cly::Countly::getInstance().RecordEvent("purchase", segmentation, 1, 0.99);</code></pre>
<p>
  <strong>5. Event key, count, sum, and duration with segmentation(s)</strong>
</p>
<pre><code class="java">std::map&lt;std::string, std::string&gt; segmentation;<br>segmentation["country"] = "Germany";<br><br>cly::Countly::getInstance().RecordEvent("purchase", segmentation, 1, 0.99, 60.0);<br></code></pre>
<p>
  <span style="font-weight: 400;">These are only a few examples of what you can do with Events. You may go beyond those examples and use country, app_version, game_level, time_of_day, or any other segmentation of your choice that will provide you with valuable insights. </span>
</p>
<h2>Timed Events</h2>
<p>
  It's possible to create timed events by defining a start and a stop moment.
</p>
<pre><code class="java hljs">cly::Event event("Some event", 1);</code><br><span class="hljs-comment"><br>//start some event<br><code class="java hljs">event.startTimer();<br></code><span class="hljs-comment">//wait some time<br><br><span class="hljs-comment">//end the timer and record event<br><code class="java hljs">event.stopTimer();<br>
cly::Countly.getInstance().addEvent(event);</code></span></span></span></pre>
<p>
  You may also provide additional information e.g segmentation, count, and sum.
</p>
<pre><span class="hljs-comment">//event with count and sum
<code class="java hljs">cly::Event event("Some event", 1, 0.99);</code><br><span class="hljs-comment">//add segmentation to event<br><code class="java hljs">event.addSegmentation("country", "Germany");</code><br>...<br><br><code class="java hljs">cly::Countly.getInstance().addEvent(event);</code></span></span></pre>
<h1>Sessions</h1>
<h2>Automatic Session Tracking</h2>
<p>
  The SDK handles the sessions automatically. After calling the
  <span style="font-weight: 400;"><code class="java">start(...)</code> method, the SDK starts the session tracking automatically and extends sessions after every 60 seconds. This value is configurable during and after initialization. <br>Example: </span>
</p>
<pre><span style="font-weight: 400;"><code class="java">cly::Countly::getInstance().setAutomaticSessionUpdateInterval(10);</code></span></pre>
<p>
  <span style="font-weight: 400;">The SDK ends the current session whenever the user exits from the app. </span>
</p>
<h1>View Tracking</h1>
<h2>Manual View Recording</h2>
<p>
  The Countly C++ SDK supports manual view (screen) tracking, with which, you can
  report which views a user has visited with the duration of that visit. To report
  a screen from your app to the Countly server, you can use the following method:
</p>
<pre><span style="font-weight: 400;"><code>std::string&amp; viewID = cly::Countly::getInstance().views()("Home Scene");</code></span></pre>
<p>
  While tracking views manually, you may add your custom segmentation to those
  views like this:
</p>
<pre><code>std::map&lt;std::string, std::string&gt; segmentation = {<br>{"cats", "123"},<br>{"moons", "9.98"},<br>{"Moose", "deer"},<br>};<br><br><span class="c-mrkdwn__br" data-stringify-type="paragraph-break">std::string&amp; viewID = cly::Countly::getInstance().views().openView("Home Scene", segmentation);</span></code></pre>
<p>
  When the screen closes you can report it to the server by using one of the following
  methods:
</p>
<p>
  <strong>1. Ending a view with a view ID:</strong>
</p>
<p>
  When you start recording a view by calling the
  <span class="hljs-selector-tag">openView method, it returns a view ID of type <span class="hljs-keyword">std::string. You can use this ID to close a view. </span></span>
</p>
<p>For example:</p>
<pre><code>std::string&amp; viewID = cly::Countly::getInstance().views().openView("Home Scene");<br>...<br>cly::Countly::getInstance().views().closeViewWithID(viewId);</code></pre>
<p>
  <strong>2. Ending a view with a view name:<br></strong>You may close a view by
  its name using the following method:
</p>
<pre><code>cly::Countly::getInstance().views().closeViewWithName("Home Scene");</code></pre>
<p>
  To review the resulting view data, go to the <code>Analytics &gt; Views</code>
  section in your Countly server. For more information on how to utilize view tracking
  data to its fullest potential, click
  <a href="http://resources.count.ly/docs/view-analytics">here</a>.
</p>
<h1>Device ID management</h1>
<p>
  A device ID is a unique identifier of your users. You have to specify the device
  ID yourself. When providing one you should keep in mind that it has to be unique
  for all users. Some potential sources for such an ID may be the user's username,
  email, or some other internal ID used within your other systems.
</p>
<p>
  In the C++ SDK the device ID is not persistent and has to be provided every time
  you start the SDK.
</p>
<h2>Changing Device ID</h2>
<p>
  In case your application authenticates users, you might want to change the initial
  device ID of the user to another one in your backend after the user logs in.
  This helps you identify a specific user with a specific ID on a device the user
  logs in, and the same scenario can also be used in cases where same user logs
  in using a different device (e.g another tablet, another mobile phone, or web).
  If you employ this logic, any data stored in your Countly server database associated
  with the current device ID will be transferred (merged) into the user profile
  with the device ID you specified in the following method call:
</p>
<pre><span style="font-weight: 400;"><code class="java">cly::Countly::getInstance().setDeviceID("new-device-id", true);</code></span></pre>
<p>
  If you integrate this method, there might be times where you might want to track
  information about another user that starts using your app from the same device
  (an account change), or your app enters a state where you no longer can verify
  the identity of the current user (user logs out). In those cases, you can change
  the current device ID to a new one without merging their data. You would call:
</p>
<pre><span style="font-weight: 400;"><code class="java">cly::Countly::getInstance().setDeviceID("new-device-id", false);</code></span></pre>
<p>
  Doing it this , will prevent the previous user's data to merge with the new id.
</p>
<p>
  If the second parameter <code>same_user</code> is set to <code>true</code>, the
  old device ID on the server will be replaced with the new one, and data associated
  with the old device ID will be merged automatically.
</p>
<p>
  Otherwise, if <code>same_user</code> is set to <code>false</code>, the device
  will be counted as a new device on the server.
</p>
<h1>User Location</h1>
<p>
  While integrating this SDK into your application, you might want to track your
  user's location. You could use this information to learn more about your app’s
  user base. There are 4 fields that can be provided:
</p>
<ul>
  <li>Country code (two-letter ISO standard).</li>
  <li>City name (must be set together with the country code).</li>
  <li>
    Latitude and longitude values, separated by a comma e.g. "56.42345,123.45325".
  </li>
  <li>Your user’s IP address.</li>
</ul>
<h2>Setting Location</h2>
<p>
  During init, you may set location, and after the SDK initialization, this location
  info will be sent to the server at the start of the user session.
</p>
<p>Example:</p>
<pre><code class="hljs cs"><span class="hljs-keyword">string countryCode = <span class="hljs-string">"us";<br><span class="hljs-keyword">string city = <span class="hljs-string">"Houston";<br><span class="hljs-keyword">string latitude = <span class="hljs-string">"29.634933"; <br><span class="hljs-keyword">string longitude = <span class="hljs-string">"-95.220255"; <br><span class="hljs-keyword">string ipAddress = "192.168.0.1"; <br><br>cly::Countly::getInstance().setLocation(countryCode, city, latitude + <span class="hljs-string">"," + longitude, ipAddress);</span></span></span></span></span></span></span></span></span></span></code></pre>
<p>
  Note that the IP address would only be updated if it's set during the init process.
</p>
<p>
  When these values are set after the SDK initialization, a separate request will
  be created to send them to the server. Except for the IP address, because Countly
  server can process an IP address only when starting a new session.
</p>
<p>
  If you don't want to set specific fields, you should set them to empty.
</p>
<h1>Remote Config</h1>
<p>
  Available in the Enterprise Edition, Remote Config allows you to modify how your
  app functions or looks by requesting key-value pairs from your Countly server.
  The returned values may be modified based on the user profile. For more details,
  please see the
  <a href="https://resources.count.ly/docs/remote-config">Remote Config documentation</a>.
</p>
<h2>Manual Remote Config</h2>
<p>
  To download Remote Config, call <code>updateRemoteConfig()</code>.
</p>
<pre><code>cly::Countly.getInstance().updateRemoteConfig();</code></pre>
<h2>Accessing Remote Config Values</h2>
<p>
  To access the stored config, call
  <code>cly::Countly.getInstance().getRemoteConfigValue(const std::string&amp; key)</code>.
  It will return <code>null</code> if there isn't any config stored.
</p>
<pre><code>cly::Countly.getInstance().getRemoteConfigValue("Key");</code></pre>
<p>
  It returns a value of the type <code>json</code>.
</p>
<h1>User profiles</h1>
<p>
  For information about User Profiles, review
  <a href="http://resources.count.ly/docs/user-profiles">this documentation</a>.
</p>
<h2>Setting Predefined Values</h2>
<p>
  The Countly C++ SDK allows you to upload user specific data to your Countly server.
  You may set the data against predefined keys for a particular user.
</p>
<p>The keys for predefined user data fields are as follows:</p>
<div class="table-container">
  <table style="height: 220px;">
    <tbody>
      <tr style="height: 22px;">
        <th style="width: 104px; height: 22px;">Key</th>
        <th style="width: 61px; height: 22px;">Type</th>
        <th style="width: 337px; height: 22px;">Description</th>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 96px; height: 22px;">name</td>
        <td style="width: 53px; height: 22px;">string</td>
        <td style="width: 329px; height: 22px;">User's full name</td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 96px; height: 22px;">username</td>
        <td style="width: 53px; height: 22px;">string</td>
        <td style="width: 329px; height: 22px;">User's nickname</td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 96px; height: 22px;">email</td>
        <td style="width: 53px; height: 22px;">string</td>
        <td style="width: 329px; height: 22px;">User's email address</td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 96px; height: 22px;">organization</td>
        <td style="width: 53px; height: 22px;">string</td>
        <td style="width: 329px; height: 22px;">User's organization name</td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 96px; height: 22px;">phone</td>
        <td style="width: 53px; height: 22px;">string</td>
        <td style="width: 329px; height: 22px;">User's phone number</td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 96px; height: 22px;">picture</td>
        <td style="width: 53px; height: 22px;">string</td>
        <td style="width: 329px; height: 22px;">URL to avatar or profile picture of the user</td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 96px; height: 22px;">gender</td>
        <td style="width: 53px; height: 22px;">string</td>
        <td style="width: 329px; height: 22px;">User's gender as M for male and F for female</td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 96px; height: 22px;">byear</td>
        <td style="width: 53px; height: 22px;">string</td>
        <td style="width: 329px; height: 22px;">User's year of birth as integer</td>
      </tr>
    </tbody>
  </table>
</div>
<p>
  The SDK allows you to upload user details using the methods listed below.
</p>
<p>Example:</p>
<pre><code>std::map&lt;std::string, std::string&gt; userdetail = { <br>{"name", "Full name"}, <br>{"username", "username123"},<br>{"email", "useremail@email.com"},<br>{"phone", "222-222-222"},<br>{"picture", "http://webresizer.com/images2/bird1_after.jpg"},<br>{"gender", "M"},<br>{"byear", "1991"},<br>{"organization", "Organization"},<br>};<br>cly::Countly.getInstance().setUserDetails(userdetail);</code></pre>
<h2>Setting Custom Values</h2>
<p>
  The SDK gives you the flexibility to send only the custom data to Countly servers,
  even when you don’t want to send other user-related data.
</p>
<p>Example:</p>
<pre><code>std::map&lt;std::string, std::string&gt; userdetail = { <br>{"Height", "5.8"}, <br>{"Mole", "Lower Left Cheek"}<br>};<br><br>cly::Countly.getInstance().setCustomUserDetails(userdetail);</code></pre>
<h2>Setting User Picture</h2>
<p>
  The SDK allows you to set the user's picture URL along with other details using
  the methods listed below.
</p>
<p>Example:</p>
<pre><code>std::map&lt;std::string, std::string&gt; userdetail = { <br>{"name", "Full name"}, <br>{"picture", "http://webresizer.com/images2/bird1_after.jpg"},<br>};<br><br>cly::Counlty.getInstance().setUserDetails(userdetail);</code></pre>
<h1>Security and Privacy</h1>
<h2 id="parameter-tampering-protection" class="anchor-heading">Parameter Tamper Protection</h2>
<p>
  You may set an optional <code>salt</code> to be used for calculating the checksum
  of requested data which will be sent with each request, using the
  <code>&amp;checksum</code> field. You will need to set the exact same
  <code>salt</code> on the Countly server. If the <code>salt</code> on the Countly
  server is set, all requests would be checked for the validity of the
  <code>&amp;checksum</code> the field before being processed.
</p>
<pre><code class="java hljs">cly::Countly.getInstance().setSalt("salt");</code></pre>
<h1>Other Features and Notes</h1>
<h2>Setting Event Queue Threshold</h2>
<p>
  Before or after SDK starts, you can set a threshold for the number of events
  that the system can record internally (on memory or persistently) before they
  are all sent to the request queue.<br>
  Example:
</p>
<pre><code>cly::Counlty.getInstance().setEventsToRQThreshold(10);</code></pre>
<p>
  When the threshold is reached, the SDK batches all the events in the event queue
  and sends them to the request queue to be sent to the server in a single request.
  The default value is set to 100, but you can change it to any whole number between
  1 to 10000.
</p>
<h2>Setting Request Queue Processing Batch Size</h2>
<p>
  Before or after SDK starts, you can set a threshold for the number of requests
  the request queue can try sending to the server in one go. If this threshold
  is high and there are an increased number of requests in the queue, it can prevent
  the application from closing until it sends all requests to the server. To prevent
  this from happening, the SDK stops this process whenever the threshold is reached
  (100 by default) and starts again at the next iteration of the update loop.<br>
  Example:
</p>
<pre><code>cly::Counlty.getInstance().setMaxRQProcessingBatchSize(10);</code></pre>
<h2 id="SettingUpSQLiteStorage">Setting Up SQLite Storage</h2>
<p>
  In case you need persistent storage, you would need to build the SDK with that
  option enabled. In that case, you must build the SDK with the COUNTLY_USE_SQLITE
  option, as explained <a href="#AddingTheSdkToTheProject">here</a>.
</p>
<p>
  You would also need to provide a path before initialization where the database
  file could be stored.
</p>
<div>
  <pre><code>cly::Countly::getInstance().SetPath("databaseFileName.db");</code></pre>
</div>
<p>
  Building your SDK with SQLite would enable event and request queues to be stored
  persistently in your device. SDK would also try to rebuild the database file,
  repacking it into a minimal amount of disk space (SQLite Vacuum) every initialization.
</p>
<h2>Setting Custom SHA-256</h2>
<p>
  C++ SDK allows users to set a custom SHA-256 method for calculating the checksum
  of request data.
</p>
<p>
  To use the custom SHA-256 feature follow the following steps:
</p>
<p>
  1. Build the Countly C++ SDK executable with the
  <code>COUNTLY_USE_CUSTOM_SHA256</code> option.
</p>
<div class="highlight highlight-source-shell notranslate position-relative overflow-auto">
  <pre>cmake -DCOUNTLY_USE_SQLITE=1 -DCOUNTLY_USE_CUSTOM_SHA256=1 -B build</pre>
</div>
<p>
  2. Set custom SHA-256 method <code>setSha256</code>
</p>
<p>For example:</p>
<pre><code class="java hljs">std::string customChecksumCalculator(const std::string&amp; data) {<br>...<br>return result;<br>} </code><br><br><code class="java hljs">cly::Countly&amp; countly = cly::Countly.getInstance();</code><br><code class="java hljs">countly.setSalt("salt");<br>countly.setSha256(customChecksumCalculator);</code></pre>
<h2 class="p-rich_text_section">Additional project install option</h2>
<p>
  In some cases your project might need to install Countly globally one the system.
  In those situation you would also want to run the <code>make install</code>command.
  As per the description, it install the countly library on the system.
</p>
<p>For example:</p>
<pre class="notranslate notranslate"><code>#configure the SDK build
cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr/local -DBUILD_SHARED_LIBS=OFF -B build
<br>cd build<br>#build the SDK
make
<br>#install countly on the system
make install</code></pre>
<ul>
  <li>
    <code>CMAKE_INSTALL_PREFIX</code><br>
    Install directory used by install. If “make install” is invoked or INSTALL
    is built, this directory is prepended onto all install directories. This
    variable defaults to '/usr/local' on UNIX and 'c:/Program Files' on Windows.
  </li>
  <li>
    <code>BUILD_SHARED_LIBS</code><br>
    If present and true, this will cause all libraries to be built shared unless
    the library was explicitly added as a static library.
  </li>
</ul>
<h1>FAQ</h1>
<h2>What Information is Collected by the SDK</h2>
<p>
  There are some data that is collected by SDK to perform their functions and implement
  the required features. Before any of it is sent to the server, it is stored locally.
</p>
<p>
  * When sending any network requests to the server, the following things are sent
  in addition to the main data:<br>
  - Timestamp of when the request is created<br>
  - SDK version<br>
  - SDK name
</p>
