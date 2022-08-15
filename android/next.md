<p>
  <span style="font-weight: 400;">This document will guide you through the process of Countly SDK installation and it applies to version 21.11.X</span>
</p>
<div class="callout callout--info">
  <p>
    To access the documentation for version 20.11.X and older, click
    <a href="/hc/en-us/articles/4409196247065" target="_self" rel="undefined">here.</a>
  </p>
</div>
<p>
  The Countly Android SDK requires a minimum Android version of 4.2.x (API Level
  17). You can take a look at our sample application in the
  <a href="https://github.com/Countly/countly-sdk-android" target="_self">Github repo</a>.
  It should show how most of the functionalities can be used.
</p>
<h1>Adding the SDK to the project</h1>
<p>
  <span style="font-weight: 400;">You need to use the MavenCentral repository to download the SDK package. If it is not included in your project, include it as follows:</span>
</p>
<pre><code>buildscript {
    repositories {
        mavenCentral()
    }
}</code></pre>
<p>
  <span style="font-weight: 400;">Now, add the Countly SDK dependency (</span><strong>use the latest SDK version currently available from gradle, not specifically the one shown in the sample below</strong><span style="font-weight: 400;">).</span>
</p>
<pre><code class="java">dependencies {
    compile 'ly.count.android:sdk:21.11.0'
}</code></pre>
<h1>SDK Integration</h1>
<p>
  Before you can use any functionality, you have to initiate the SDK. That is done
  either in your&nbsp;<code>Application</code> subclass (preferred), or from your
  main activity <code>onCreate</code> method.
</p>
<h2>Minimal setup</h2>
<p>The shortest way to initiate the SDK is with this call:</p>
<pre><code>Countly.<span>sharedInstance</span>().init(<span>new </span>CountlyConfig(<span>this</span>, <span>COUNTLY_APP_KEY</span>, <span>COUNTLY_SERVER_URL</span>));</code></pre>
<p>
  <span style="font-weight: 400;">It is there that you provide the Android context, your appKey, and your Countly server URL. For more information on how to acquire you application key (appKey) and server URL, check <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#acquiring-your-application-key-and-server-url" target="_self">here</a>.</span>
</p>
<p>
  To configure the SDK during init, a config object called "CountlyConfig" is used.
  Configuration is done by creating such an object and then calling it's provided
  function calls to enable functionality you need. Afterward that config object
  is provided to the "init" method.<span style="font-weight: 400;"></span>
</p>
<h2>SDK logging</h2>
<p>
  <span style="font-weight: 400;">The first thing you should do while integrating our SDK is enabling logging. If logging is enabled, then our SDK will print out debug messages about its internal state and encountered problems. Those messages may be screened in logcat and may use Androids internal log calls.</span>
</p>
<p>
  Call&nbsp;<code>setLoggingEnabled</code>&nbsp;on the config class to enable logging:
</p>
<pre><code>CountlyConfig config = (<span>new </span>CountlyConfig(appC, <span>COUNTLY_APP_KEY</span>, <span>COUNTLY_SERVER_URL</span>));<br>config.setLoggingEnabled(<span>true</span>);</code></pre>
<h2>Device ID</h2>
<p>
  <span style="font-weight: 400;">All tracked information is tied to a "device ID". A device ID is a unique identifier for your users.</span>
</p>
<p>
  <span style="font-weight: 400;">One of the first things you'll need to decide is which device ID generation strategy to use. There are several options defined below:</span>
</p>
<p>
  <span style="font-weight: 400;">The easiest method is letting the Countly SDK seamlessly handle the device ID on its own. You may then use the following calls. It will use the default strategy, which currently is OpenUDID (don't forget to finish setting up OpenUDID as described below).</span>
</p>
<pre><code class="java">CountlyConfig config = (new CountlyConfig(appC, COUNTLY_APP_KEY, COUNTLY_SERVER_URL));<br>Countly.sharedInstance().init(config);</code></pre>
<p>
  <span style="font-weight: 400;">You may specify the device ID by yourself if you have one (it has to be unique for each device). It may be an email or some other internal ID used by your other systems.</span>
</p>
<pre><code class="java">CountlyConfig config = (new CountlyConfig(appC, COUNTLY_APP_KEY, COUNTLY_SERVER_URL));<br>config.setDeviceId("YOUR_DEVICE_ID");<br>Countly.sharedInstance().init(config);</code></pre>
<p>
  <span style="font-weight: 400;">You may rely on the Google Advertising ID for device ID generation.</span>
</p>
<pre><code class="java">CountlyConfig config = (new CountlyConfig(appC, COUNTLY_APP_KEY, COUNTLY_SERVER_URL));<br>config.setIdMode(DeviceId.Type.ADVERTISING_ID);<br>Countly.sharedInstance().init(config);</code></pre>
<p>
  <span style="font-weight: 400;">In regard to the Google Advertising ID, please ensure you have Google Play services 4.0+ included in your project. Also, note that the Advertising ID silently falls back to OpenUDID in case it fails to get the Advertising ID when Google Play services are not available on a device.</span>
</p>
<p>You may also explicitly use OpenUDID:</p>
<pre><code class="java">CountlyConfig config = (new CountlyConfig(appC, COUNTLY_APP_KEY, COUNTLY_SERVER_URL));<br>config.setIdMode(DeviceId.Type.OPEN_UDID);<br>Countly.sharedInstance().init(config);</code></pre>
<h2>Adding callbacks</h2>
<p>
  After the&nbsp;<code>Countly.sharedInstance().init(...)</code><span style="font-weight: 400;">call, you'll need to add the following calls to all your activities:</span>
</p>
<ul>
  <li>
    Call <code>Countly.sharedInstance().onStart(this)</code> in onStart, where
    <code>this</code> is a link to the current Activity.
  </li>
  <li>
    Call <code>Countly.sharedInstance().onStop()</code> in onStop.
  </li>
  <li>
    Call&nbsp;<code>Countly.sharedInstance().onConfigurationChanged(newConfig)</code>&nbsp;in
    onConfigurationChanged if you want to track orientation changes.
  </li>
</ul>
<p>
  <span style="font-weight: 400;">If the "onStart" and "onStop" calls are not added, some functionalities will not work, e.g. automatic sessions will not be tracked. The Countly "onStart" has to be called in the activities "onStart" function, it cannot be called in "onCreate" or in any other place, otherwise, the application will receive exceptions.</span>
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/283f96f-activity_lifecycle.png">
</div>
<h2>Required app permissions</h2>
<p>
  <span style="font-weight: 400;">Additionally, ensure the&nbsp;</span><em><span style="font-weight: 400;">INTERNET</span></em><span style="font-weight: 400;">&nbsp;and&nbsp;</span><em><span style="font-weight: 400;">ACCESS_NETWORK_STATE</span></em><span style="font-weight: 400;">&nbsp;permissions are set if there aren’t any in your manifest file. Those calls should look something like this:</span>
</p>
<pre><code>&lt;uses-permission android:name="android.permission.INTERNET"/&gt;<br>&lt;uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /&gt;</code></pre>
<h1>Crash reporting</h1>
<p>
  <span style="font-weight: 400;">The Countly SDK for Android has the ability to collect&nbsp;</span><a href="http://resources.count.ly/docs/introduction-to-crash-reporting-and-analytics"><span style="font-weight: 400;">crash reports</span></a><span style="font-weight: 400;">,</span><span style="font-weight: 400;">&nbsp;which you may examine and resolve later on the server.</span>
</p>
<p>
  In the SDK all crash-related functionality can be browsed from the returned interface
  on:
</p>
<pre><code class="java">Countly.sharedInstance().crashes()</code></pre>
<h2>Automatic crash handling</h2>
<p>
  To enable automatic crash reporting, call the following function on the config
  object.
  <span style="font-weight: 400;">After init, this will enable crash reporting, which will automatically catch uncaught Java exceptions.&nbsp;</span>They
  will be sent to the dashboard once the app is launched again and the SDK is initiated.
</p>
<pre><code class="java">config.enableCrashReporting();</code></pre>
<h2>Automatic crash report segmentation</h2>
<p>
  <span style="font-weight: 400;">You may add a key/value segment to crash reports. For example, you could set which specific library or framework version you used in your app. You may then figure out if there is any correlation between the specific library or another segment and the crash reports.</span>
</p>
<p>
  <span style="font-weight: 400;">Use the following function for this purpose:</span>
</p>
<pre><code class="java">config.setCustomCrashSegment(Map&lt;String, String&gt; segments)</code></pre>
<h2>Handled exceptions</h2>
<p>
  <span style="font-weight: 400;">You might catch an exception or similar error during your app’s runtime.</span>
</p>
<p>
  <span style="font-weight: 400;">You may also log these handled exceptions to monitor how and when they are happening with the following command:</span>
</p>
<pre><code class="java">Countly.sharedInstance().crashes().recordHandledException(Exception exception);</code></pre>
<p>
  <span style="font-weight: 400;">If you have handled an exception and it turns out to be fatal to your app, you may use this call:</span>
</p>
<pre><code class="java">Countly.sharedInstance().crashes().recordUnhandledException(Exception exception);</code></pre>
<h2>Crash breadcrumbs</h2>
<p>
  Throughout your app you can leave&nbsp;crash breadcrumbs which would describe
  previous steps that were taken in your app before the crash. After a crash happens,
  they will be sent together with the crash report.
</p>
<p>Following the command adds crash breadcrumb:</p>
<pre><code class="java">Countly.sharedInstance().crashes().addCrashBreadcrumb(String record) </code></pre>
<h2>Recording all threads</h2>
<p>
  If you would like to record the state of all other threads during an uncaught
  exception or during the recording of a handled exception, you can call this during
  init:
</p>
<pre>config.setRecordAllThreadsWithCrash();</pre>
<h2>Crash filtering</h2>
<p>
  There might be cases where a crash could contain sensitive information. For such
  situations, there is a crash filtering option. You can provide a callback which
  will be called every time a crash is recorded. It gets the string value of the
  crash, which would be sent to the server, and should return "true" if the crash
  should not be sent to the server:
</p>
<pre>config.setCrashFilterCallback(<span>new </span>CrashFilterCallback() {<br>    <span>@Override<br></span><span>    </span><span>public boolean </span>filterCrash(String crash) {<br>        //returns true if the crash should be ignored<br>        <span>return </span>crash.contains(<span>"secret"</span>);<br>    }<br>})</pre>
<h2>Native C++ Crash Reporting</h2>
<div class="callout callout--warning">
  <p>
    Due to the limitations of the <code>dump_syms</code> binary, C++ symbol extraction
    and automatic upoload of them is only supported on Linux devices.
  </p>
</div>
<p>
  <span style="font-weight: 400;">Countly uses&nbsp;</span><a href="https://github.com/google/breakpad"><span style="font-weight: 400;">Google's Breakpad open source library</span></a><span style="font-weight: 400;">&nbsp;to be able to report crashes that occurred within the C++ components of your application, assuming there are any. Breakpad provides:</span>
</p>
<ul>
  <li>
    <span style="font-weight: 400;">a tool for creating symbol files from your object files (<code>dump_syms</code></span><span style="font-weight: 400;">)</span>
  </li>
  <li>
    <span style="font-weight: 400;">the ability to detect and record crashes via compact minidump files (crash handler)</span>
  </li>
  <li>
    <span style="font-weight: 400;">a tool for generating human readable stack traces by using symbol files and crash minidump files.</span>
  </li>
</ul>
<div class="img-container">
  <img src="https://count.ly/images/guide/7cbb985-breakpad.png">
</div>
<p>
  <span style="font-weight: 400;">Countly provides the&nbsp;</span><a href="https://github.com/Countly/countly-sdk-android/tree/master/sdk-native"><span style="font-weight: 400;">sdk_native</span></a><span style="font-weight: 400;">&nbsp;Android library to add crash handler to your native code and create crash minidump files. The SDK will check for those minidump files and send them automatically to your Countly server upon application start. You would download <code>sdk_native</code></span><span style="font-weight: 400;">&nbsp;from the MavenCentral repository and include it in your project, similar to how you included our SDK (please change the <code>LATEST_VERSION</code></span><span style="font-weight: 400;">&nbsp;below by checking our Maven&nbsp;</span><a href="https://search.maven.org/artifact/ly.count.android/sdk"><span style="font-weight: 400;">page</span></a><span style="font-weight: 400;">, currently 20.11.12):</span>
</p>
<pre><code class="java">// build gradle file 

repositories {
    mavenCentral()
}

dependencies {
    implementation 'ly.count.android:sdk-native:LATEST_VERSION'
}</code></pre>
<p>
  <span style="font-weight: 400;">Then call our init method as early as possible in your application life cycle to be able to catch crashes that occur during initialization:</span>
</p>
<pre><code class="java">import ly.count.android.sdknative.CountlyNative;

CountlyNative.initNative(getApplicationContext());</code></pre>
<p>
  <code>getApplicationContext()</code> is needed to determine a storage place for
  minidump files.
</p>
<h2>Automatic symbol file upload</h2>
<p>
  <span style="font-weight: 400;">You may create Breakpad symbol files yourself and upload them to your Countly server using our UI. They will be needed to create stack traces from minidump files. Countly also developed a Gradle plugin to automate this process. To use the upload plugin in Studio, you first need to include it (the LATEST_VERSION is currently 20.11.12):</span>
</p>
<pre><code class="java">apply plugin: ly.count.android.plugins.UploadSymbolsPlugin 

buildscript {
    repositories {
        mavenCentral()
    }
    // for LATEST_VERSION check https://search.maven.org/artifact/ly.count.android/sdk
    dependencies {
        classpath group: 'ly.count.android', 'name': 'sdk-plugin', 'version': 'LATEST_VERSION'
    }
}</code></pre>
<p>
  <span style="font-weight: 400;">Then you will need to configure a Gradle Countly block for the plugin:</span>
</p>
<pre><code class="java">countly {
    server "https://YOUR_SERVER" 
    app_key "YOUR_APP_KEY"  
}</code></pre>
<p>
  Next, you will have two new Gradle tasks available to you:
  <code>uploadJavaSymbols</code> and <code>uploadNativeSymbols</code>.
  <code>uploadJavaSymbols</code> is for uploading the <code>mapping.txt</code>
  file generated by Proguard. After building your project, you may run these tasks
  through Studio's Gradle tool window (1). They will be available under your app
  (2) and grouped as Countly tasks (3).
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/6ddc195-Selection_006.png">
</div>
<p>Another option is to run them from the command line:</p>
<pre><code class="java">./gradlew uploadNativeSymbols

// or if you have subprojects

./gradlew :project-name:uploadNativeSymbols</code></pre>
<p>
  <span style="font-weight: 400;">You may also configure your build so these tasks will run after every build (leave out the task which is not required for you):</span>
</p>
<pre><code class="java">tasks.whenTaskAdded { task -&gt;
    if (task.name.startsWith('assemble')) {
        //this would upload your Java mapping file
        task.dependsOn('uploadJaveSymbols')
        
        //this would upload your native (c++) symbols
        task.dependsOn('uploadNativeSymbols')
    }
}</code></pre>
<p>
  <span style="font-weight: 400;">In addition, you may also override some default values in the Countly block in an effort to specify your server and app info.</span>
</p>
<pre><code class="java">countly {
  // required by both tasks
  server "https://try.count.ly"
  app_key "XXXXXX"  // same app_key used for SDK integration

  // optional properties for uploadJavaSymbols. Shown are the default values.

  // location of mapping.txt file relative to project build directory
  mappingFile "outputs/mapping/release/mapping.txt"

  // note that will be saved with the upload and can be checked in the UI
  noteJava "sdk-plugin automatic upload of mapping.txt"

  // optional properties for uploadNativeSymbols. Shown are the default values.

  // directory of .so files relative to project build directory.
  // you can check the tar.gz file created under intermediates/countly
  // BUILD_TYPE could be debug or release
  nativeObjectFilesDir "intermediates/merged_native_libs/BUILD_TYPE"
  
  // path for breakpad tool dump_syms executable 
  dumpSymsPath "/usr/bin/dump_syms" // note that will be saved with the upload and can be checked in the UI noteNative "sdk-plugin automatic upload of breakpad symbols" } 
  </code></pre>
<p>
  <span style="font-weight: 400;">It is possible that two of these properties will need to be configured manually: <code>dumpSymsPath</code></span><span style="font-weight: 400;">&nbsp;and <code>nativeObjectFilesDir</code></span><span style="font-weight: 400;">. The plugin assumes you will run the task after a release build. To test it for debug builds, please change <code>nativeObjectFilesDir</code></span><span style="font-weight: 400;">&nbsp;to <code>"intermediates/cmake/debug/obj"</code></span><span style="font-weight: 400;">&nbsp;(or to wherever your build process puts .so files under the build directory).</span>
</p>
<p>
  <span style="font-weight: 400;">We created a&nbsp;</span><a href="https://github.com/Countly/countly-sdk-android/tree/master/app-native"><span style="font-weight: 400;">sample app</span></a><span style="font-weight: 400;">&nbsp;in our github repo that demonstrates both how to use SDK-native and our upload plugin.</span>
</p>
<h1>Events</h1>
<p>
  <span style="font-weight: 400;">An</span><a href="http://resources.count.ly/docs/custom-events"><span style="font-weight: 400;">&nbsp;event</span></a><span style="font-weight: 400;">&nbsp;is any type of action that you can send to a Countly instance, e.g. purchases, changed settings, view enabled, and so on. This way it's possible to get much more information from your application compared to what is sent from the Android SDK to the Countly instance by default.</span>
</p>
<p>
  All data passed to the Countly server via the SDK or API should be in UTF-8.
</p>
<p>&nbsp;</p>
<p>
  In the SDK all event-related functionality can be browsed from the returned interface
  on:
</p>
<pre><code class="java">Countly.sharedInstance().events()</code></pre>
<p>&nbsp;</p>
<p>
  When providing segmentation for events, the only valid data types are: "String",
  "Integer", "Double" and "Boolean". All other types will be ignored.
</p>
<h2>Recording events</h2>
<p>
  <span style="font-weight: 400;">We have provided an example of recording a&nbsp;</span><strong>purchase</strong><span style="font-weight: 400;">&nbsp;event below. Here is a quick summary of the information with which each usage will provide us:</span>
</p>
<ul>
  <li>
    Usage 1: how many times the&nbsp;<strong>purchase</strong> event occurred.
  </li>
  <li>
    Usage 2: how many times the&nbsp;<strong>purchase</strong> event occurred
    + the total amount of those purchases.
  </li>
  <li>
    Usage 3: how many times the&nbsp;<strong>purchase</strong> event occurred
    +
    <span style="font-weight: 400;">from which countries and application versions those purchases were made.</span>
  </li>
  <li>
    Usage 4: how many times the&nbsp;<strong>purchase</strong> event occurred
    +&nbsp;<span style="font-weight: 400;">the total amount, both of which are also available, segmented into countries and application versions.</span>
  </li>
  <li>
    Usage 5: how many times the&nbsp;<strong>purchase</strong> event occurred
    +
    <span style="font-weight: 400;">the total amount, both of which are also available, segmented into countries and application versions + the total duration of those events.</span>
  </li>
</ul>
<h3>1. Event key and count</h3>
<pre><code class="java">Countly.sharedInstance().events().recordEvent("purchase", 1);</code></pre>
<h3>2. Event key, count, and sum</h3>
<pre><code class="java">Countly.sharedInstance().events().recordEvent("purchase", 1, 0.99);</code></pre>
<h3>3. Event key and count with segmentation(s)</h3>
<pre><code class="java">HashMap&lt;String, String&gt; segmentation = new HashMap&lt;String, Object&gt;();
segmentation.put("country", "Germany");
segmentation.put("app_version", "1.0");

Countly.sharedInstance().events().recordEvent("purchase", segmentation, 1);</code></pre>
<h3>4. Event key, count, and sum with segmentation(s)</h3>
<pre><code class="java">HashMap&lt;String, String&gt; segmentation = new HashMap&lt;String, Object&gt;();
segmentation.put("country", "Germany");
segmentation.put("app_version", "1.0");

Countly.sharedInstance().events().recordEvent("purchase", segmentation, 1, 0.99);</code></pre>
<h3>5. Event key, count, sum, and duration with segmentation(s)</h3>
<pre><code class="java">HashMap&lt;String, String&gt; segmentation = new HashMap&lt;String, Object&gt;();
segmentation.put("country", "Germany");
segmentation.put("app_version", "1.0");

Countly.sharedInstance().events().recordEvent("purchase", segmentation, 1, 0.99, 60);</code></pre>
<p>
  <span style="font-weight: 400;">Those are only a few examples of what you can do with events. You may extend those examples and use Country, app_version, game_level, time_of_day, and any other segmentation that will provide you with valuable insights.</span>
</p>
<h2>Timed events</h2>
<p>
  <span style="font-weight: 400;">It's possible to create timed events by defining a start and a stop moment.</span>
</p>
<pre><code class="java">String eventName = "Some event";

//start some event
Countly.sharedInstance().events().startEvent(eventName);
//wait some time

//end the event 
Countly.sharedInstance().events().endEvent(eventName);</code></pre>
<p>
  <span style="font-weight: 400;">You may also provide additional information when ending an event. However, in that case, you have to provide the segmentation, count, and sum. The default values for those are "null", 1 and 0.</span>
</p>
<pre><code class="java">String eventName = "Some event";

//start some event
Countly.sharedInstance().events().startEvent(eventName);
//wait some time

Map&lt;String, String&gt; segmentation = new HashMap&lt;&gt;();
segmentation.put("wall", "orange");

//end the event while also providing segmentation information, count and sum
Countly.sharedInstance().events().endEvent(eventName, segmentation, 4, 34);
</code></pre>
<p>
  You may cancel the started timed event in case it is not relevant anymore:
</p>
<pre><code class="java">//start some event<br>Countly.sharedInstance().events().startEvent(eventName);
//wait some time

//cancel the event 
Countly.sharedInstance().events().cancelEvent(eventName);</code></pre>
<h2>Past events</h2>
<p>
  In the previous examples, the event creation time is recorded once the event
  is created.
</p>
<p>
  In some use cases, you might want to cache and store events by yourself and then
  record them in the SDK with a past timestamp. The timestamp is a Unix timestamp
  stored in milliseconds. For that you would use:
</p>
<pre><code class="java">Countly.sharedInstance().events().recordPastEvent(key, segmentation, count, sum, dur, timestamp)</code></pre>
<h1>Sessions</h1>
<h2>Manual sessions</h2>
<p>
  Sometimes it might be preferable to control the session manually instead of relying
  on the SDK.
</p>
<p>It can be enabled during init with:</p>
<pre>config.enableManualSessionControl();</pre>
<p>Afterwards it is up to the implementer to make calls to:</p>
<ul>
  <li>Begin session</li>
  <li>Update session duration</li>
  <li>End session (also updates duration)</li>
</ul>
<p>The approprate call to do that are:</p>
<pre>Countly.<span>sharedInstance</span>().sessions().beginSession();<br>Countly.<span>sharedInstance</span>().sessions().updateSession();<br>Countly.<span>sharedInstance</span>().sessions().endSession();</pre>
<p>
  By default, you should do some session call every 60 seconds after beginning
  a session so that it is not closed server side. If you would want to increase
  that duration, you would have to increase the "<span>Maximal Session Duration" in your server API configuration.</span>
</p>
<h1>View tracking</h1>
<p>
  In the SDK all view related functionality can be browsed from the returned interface
  on:
</p>
<pre><code class="java">Countly.sharedInstance().views()</code></pre>
<h2>Automatic views</h2>
<p>
  <span style="font-weight: 400;">View tracking is a means to report every screen view to the Countly dashboard. In order to enable automatic view tracking, call:</span>
</p>
<pre><code class="java">config.setViewTracking(true);</code></pre>
<p>
  The tracked views will use the full activity names which include their package
  name. It would look similar to "com.my.company.activityname".
</p>
<p>
  <span style="font-weight: 400;">It is possible to use short view names that make use of the simple activity name. This would look like "activityname". To use this functionality, call this before calling init:</span>
</p>
<pre><code class="java">config.setAutoTrackingUseShortName(true);</code></pre>
<h2>Automatic view segmentation</h2>
<p>
  It's possible to provide custom segmentation that will be set to all automatically
  recorded views:
</p>
<pre><code class="java">Map&lt;String, Object&gt; automaticViewSegmentation = new HashMap&lt;&gt;();
automaticViewSegmentation.put("One", 2);
automaticViewSegmentation.put("Three", 4.44d);
automaticViewSegmentation.put("Five", "Six");

config.setAutomaticViewSegmentation(automaticViewSegmentation);</code></pre>
<h2>Manual view recording</h2>
<p>
  <span style="font-weight: 400;">You may track custom views with the following code snippet as well:</span>
</p>
<pre><code class="java">Countly.sharedInstance().views().recordView("View name");</code></pre>
<p>
  While manually tracking views, you may add your custom segmentation to them like
  this:
</p>
<pre>Map&lt;String, Object&gt; viewSegmentation = <span>new </span>HashMap&lt;&gt;();<br><br>viewSegmentation.put(<span>"Cats"</span>, <span>123</span>);<br>viewSegmentation.put(<span>"Moons"</span>, <span>9.98d</span>);<br>viewSegmentation.put(<span>"Moose"</span>, <span>"Deer"</span>);<br><br>Countly.<span>sharedInstance</span>().views().recordView(<span>"Better view"</span>, viewSegmentation);</pre>
<p>
  <span style="font-weight: 400;">To review the resulting data, open the dashboard and go to</span><span style="font-weight: 400;">&nbsp;<code>Analytics &gt; Views</code></span><span style="font-weight: 400;">. For more information on how to use view tracking data to its fullest potential, click&nbsp;</span><a href="http://resources.count.ly/docs/view-analytics"><span style="font-weight: 400;">here</span></a><span style="font-weight: 400;">.</span>
</p>
<div class="img-container">
  <img src="/hc/article_attachments/9508351988121/001.png" alt="001.png">
</div>
<h1>Device ID management</h1>
<p>
  When the SDK is initialized the first time and no custom device ID is provided,
  a random one will be generated. For most use cases that is enough as it provides
  a random identity to one of your apps users.
</p>
<p>
  To solve other potential use cases, we provide 3 ways to handle your device id:
</p>
<ul>
  <li>Changing device ID with merge</li>
  <li>Changing device ID without merge</li>
  <li>Using a temporary ID</li>
</ul>
<h2>Changing device ID</h2>
<p>
  In case your application authenticates users, you might want to change the ID
  to the one in your backend after he has logged in. This helps you identify a
  specific user with a specific ID on a device he logs in, and the same scenario
  can also be used in cases this user logs in using a different way (e.g another
  tablet, another mobile phone, or web). In this case, any data stored in your
  Countly server database associated with the current device ID will be transferred
  (merged) into user profile with device id you specified in the following method
  call:
</p>
<pre><code class="java">Countly.sharedInstance().changeDeviceIdWithMerge("new device ID")</code></pre>
<p>
  In other circumstances, you might want to track information about another separate
  user that starts using your app (changing apps account), or your app enters a
  state where you no longer can verify the identity of the current user (user logs
  out). In that case, you can change the current device ID to a new one without
  merging their data. You would call:
</p>
<pre><code class="java">Countly.sharedInstance().changeDeviceIdWithoutMerge(DeviceId.Type.OPEN_UDID, null)</code></pre>
<p>
  Doing it this way, will not merge the previously acquired data with the new id.
</p>
<p>
  You can also set Advertising ID as your device ID generation strategy or even
  supply your own string with <code>DeviceId.Type.DEVELOPER_SPECIFIED</code> type.
</p>
<p>
  Do note that every time you change your deviceId without a merge, it will be
  interpreted as a new user. Therefore implementing id management in a bad way
  could inflate the users count by quite a lot.
</p>
<p>
  The worst would be to not merge device id on login and generate a new random
  ID on logout. This way, by repeatedly logging in and out one could generate an
  infinite amount of users.
</p>
<p>
  So the recommendation is (depending on your apps use case) either to keep the
  same deviceId even if the user logs out or to have a predetermined deviceId for
  when the users on the specific device logs out. The first method would not inflate
  the user count, but not viable for single device, multiple users use case. The
  second would create a "multiuser" id for every device and possibly slightly inflate
  the user count.
</p>
<h2>Temporary device ID</h2>
<p>
  In the previous ID management approaches, data is still sent to your server,
  but it adds user inflation risk if badly managed. The use of a temporary ID can
  help to mitigate such problems.
</p>
<p>
  During app start or any time after init, you can enter a temporary device ID
  mode. All requests will be stored internally and not sent to your server until
  a new device ID is provided. In that case, all events created during this temporary
  ID mode will be associated with the new device ID and sent to the server.
</p>
<p>
  To enable this mode during init, you would call this on your config object before
  init:
</p>
<pre>countlyConfig.enableTemporaryDeviceIdMode();</pre>
<p>To enable temporary id after init, you would call:</p>
<pre>Countly.sharedInstance().enableTemporaryIdMode();</pre>
<p>
  To exit temporary id mode, you would call either "changeDeviceIdWithoutMerge"
  or "changeDeviceIdWithMerge" or init the SDK with a developer supplied device
  ID.
</p>
<h2>Retrieving current device ID</h2>
<p>
  You may want to see what device id Countly is assigning for the specific device
  and what the source of that id is. For that, you may use the following calls.
  The id type is an enum with the possible values of: "DEVELOPER_SUPPLIED", "OPEN_UDID",
  "ADVERTISING_ID".
</p>
<pre><code class="java">String usedId = Countly.sharedInstance().getDeviceID();
Type idType = Countly.sharedInstance().getDeviceIDType();</code></pre>
<h1>Push notifications</h1>
<p>
  Countly supports FCM (Firebase Cloud Messaging) and Huawei Push Kit as push notification
  service providers.&nbsp;The SDK doesn't have any direct dependencies on FCM or
  HMS libraries and uses reflection instead, so
  <strong>it's up to application developers to ensure correct dependencies are present</strong>
  (please refer to our
  <a href="https://github.com/Countly/countly-sdk-android/blob/master/app/build.gradle" target="_self">Demo app build.gradle</a>
  for a reference).
</p>
<p>
  By default Countly SDK uses FCM as push notification provider. If FCM is not
  present in the system, Countly would try to get HMS token instead. It's possible
  to alter this behaviour by supplying HMS as a preferred provider:
</p>
<pre>CountlyPush.<span>init</span>(<span>this</span>, <br>    Countly.CountlyMessagingMode.<span>PRODUCTION</span>, <br>    Countly.CountlyMessagingProvider.<span>HMS</span>)</pre>
<h2>General SDK&nbsp;initialisation</h2>
<p>
  To have the best experience with push notifications, the SDK should be initialised
  in the your Application subclass' "onCreate" method.&nbsp;<span style="font-weight: 400;">Don't forget that Android O and later models require the use of <code>NotificationChannel</code>s</span>.
  Use <code>CountlyPush.CHANNEL_ID</code>&nbsp;for Countly-displayed notifications:
</p>
<pre><code class="java">public class App extends Application {

    @Override
    public void onCreate() {
        super.onCreate();

        if (Build.VERSION.SDK_INT &gt;= Build.VERSION_CODES.O) {

            // Register the channel with the system; you can't change the importance
            // or other notification behaviors after this
            NotificationManager notificationManager = (NotificationManager) getSystemService(NOTIFICATION_SERVICE);
            if (notificationManager != null) {
                // Create the NotificationChannel
                NotificationChannel channel = new NotificationChannel(CountlyPush.CHANNEL_ID, getString(R.string.countly_hannel_name), NotificationManager.IMPORTANCE_DEFAULT);
                channel.setDescription(getString(R.string.countly_channel_description));
                notificationManager.createNotificationChannel(channel);
            }
        }

        Countly.sharedInstance()
                .setLoggingEnabled(true)
                .init(this, "http://try.count.ly", "APP_KEY");

        CountlyPush.init(this, Countly.CountlyMessagingMode.PRODUCTION);

        FirebaseInstanceId.getInstance().getInstanceId()
                .addOnCompleteListener(new OnCompleteListener&lt;InstanceIdResult&gt;() {
                    @Override
                    public void onComplete(@NonNull Task&lt;InstanceIdResult&gt; task) {
                        if (!task.isSuccessful()) {
                            Log.w(TAG, "getInstanceId failed", task.getException());
                            return;
                        }

                        // Get new Instance ID token
                        String token = task.getResult().getToken();
                        CountlyPush.onTokenRefresh(token);
                    }
                });
    }
}</code></pre>
<p>
  <span style="font-weight: 400;">Please note second parameter in&nbsp;<code>CountlyPush.init()</code></span><span style="font-weight: 400;">&nbsp;call, it defines whether a particular device would be handled as a test setup or a production one. It's quite handy to separate test devices from production ones by changing <code>CountlyMessagingMode</code></span><span style="font-weight: 400;">,</span><span style="font-weight: 400;">&nbsp;so you could test your notifications before sending them to all your users.</span>
</p>
<p>
  <span style="font-weight: 400;">You should add this permision entry into your app manifest:<br></span>
</p>
<pre>&lt;<span>uses-permission </span><span>android</span><span>:name</span><span>="${applicationId}.CountlyPush.BROADCAST_PERMISSION" </span>/&gt;</pre>
<p>
  Please follow provider-specific instructions for Firebase and / or Huawei PushKit
  below.
</p>
<h2>Firebase</h2>
<h3>Getting FCM credentials</h3>
<p>
  <span style="font-weight: 400;">In order to be able to send notifications through FCM, Countly server needs a FCM server key.&nbsp;</span>In
  order to get one, open&nbsp;Project settings in&nbsp;<a href="https://console.firebase.google.com">Firebase console</a>:
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/57c5e32-Screenshot_2018-04-21_17.20.16.png">
</div>
<p>Select Cloud Messaging tab</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/fb244d1-Screenshot-2018-04-21-17.20.41-x.png">
</div>
<p>
  <span style="font-weight: 400;">Copy &amp; paste the FCM key into your application FCM credentials upload form in the Countly server and press “Save changes”.</span>
</p>
<div class="img-container">
  <img src="/hc/article_attachments/9508421820313/002.png" alt="002.png">
</div>
<h3>Integrating FCM into your app</h3>
<p>
  <span style="font-weight: 400;">Please review our&nbsp;</span><a href="https://github.com/Countly/countly-sdk-android/tree/master/app" target="_self">Demo app</a><span style="font-weight: 400;">&nbsp;for a complete integration example.</span>
</p>
<p>
  <span style="font-weight: 400;">Once you have followed the Google's guide for&nbsp;</span><a href="https://firebase.google.com/docs/android/setup"><span style="font-weight: 400;">Adding Firebase to your project</span></a><span style="font-weight: 400;">, setting up the Countly FCM is quite easy.</span>
</p>
<p>
  <strong>Adding dependencies</strong>
</p>
<p>
  <span style="font-weight: 400;">Add the following dependency to your <code>build.gradle</code></span><span style="font-weight: 400;">&nbsp;(</span><strong>use latest Firebase version</strong><span style="font-weight: 400;">):</span>
</p>
<pre>//latest firebase-messaging version that is available<code class="java">
implementation 'com.google.firebase:firebase-messaging:22.0.0'</code></pre>
<p>
  <span style="font-weight: 400;">Then add&nbsp;<code>CountlyPush.init()</code>&nbsp;call</span><span style="font-weight: 400;">&nbsp;to your <code>Application</code></span><span style="font-weight: 400;">&nbsp;subclass</span><span style="font-weight: 400;">. </span><span style="font-weight: 400;">Don't forget that Android O and later models require the use of <code>NotificationChannel</code>s</span><span style="font-weight: 400;">. Use <code>CountlyPush.CHANNEL_ID</code></span><span style="font-weight: 400;">&nbsp;for Countly-displayed notifications:</span>
</p>
<pre><code class="java">public class App extends Application {

    @Override
    public void onCreate() {
        super.onCreate();

        if (Build.VERSION.SDK_INT &gt;= Build.VERSION_CODES.O) {

            // Register the channel with the system; you can't change the importance
            // or other notification behaviors after this
            NotificationManager notificationManager = (NotificationManager) getSystemService(NOTIFICATION_SERVICE);
            if (notificationManager != null) {
                // Create the NotificationChannel
                NotificationChannel channel = new NotificationChannel(CountlyPush.CHANNEL_ID, getString(R.string.countly_hannel_name), NotificationManager.IMPORTANCE_DEFAULT);
                channel.setDescription(getString(R.string.countly_channel_description));
                notificationManager.createNotificationChannel(channel);
            }
        }

        Countly.sharedInstance()
                .setLoggingEnabled(true)
                .init(this, "http://try.count.ly", "APP_KEY");

        CountlyPush.init(this, Countly.CountlyMessagingMode.PRODUCTION);

        FirebaseInstanceId.getInstance().getInstanceId()
                .addOnCompleteListener(new OnCompleteListener&lt;InstanceIdResult&gt;() {
                    @Override
                    public void onComplete(@NonNull Task&lt;InstanceIdResult&gt; task) {
                        if (!task.isSuccessful()) {
                            Log.w(TAG, "getInstanceId failed", task.getException());
                            return;
                        }

                        // Get new Instance ID token
                        String token = task.getResult().getToken();
                        CountlyPush.onTokenRefresh(token);
                    }
                });
    }
}</code></pre>
<p>
  <span style="font-weight: 400;">Please note that in <code>CountlyPush.init()</code></span><span style="font-weight: 400;">&nbsp;you will also specify the mode of your token - test or production. It's quite handy to separate the test devices from production devices by changing <code>CountlyMessagingMode</code></span><span style="font-weight: 400;">,</span><span style="font-weight: 400;">&nbsp;so you may test your notifications before sending them to all your users.</span>
</p>
<p>
  <span style="font-weight: 400;">Now, we will need to add the <code>Service</code></span><span style="font-weight: 400;">. Add a service definition to your <code>AndroidManifest.xml</code></span><span style="font-weight: 400;">:</span>
</p>
<pre><code class="xml">&lt;service android:name=".DemoFirebaseMessagingService"&gt;
    &lt;intent-filter&gt;
        &lt;action android:name="com.google.firebase.MESSAGING_EVENT" /&gt;
    &lt;/intent-filter&gt;
&lt;/service&gt;
</code></pre>
<p>... and add a class for it as well:</p>
<pre><code class="java">public class DemoFirebaseMessagingService extends FirebaseMessagingService {
    private static final String TAG = "DemoMessagingService";

    @Override
    public void onNewToken(String token) {
        super.onNewToken(token);

        Log.d("DemoFirebaseService", "got new token: " + token);
        CountlyPush.onTokenRefresh(token);
    }

    @Override
    public void onMessageReceived(RemoteMessage remoteMessage) {
        super.onMessageReceived(remoteMessage);

        Log.d("DemoFirebaseService", "got new message: " + remoteMessage.getData());

        // decode message data and extract meaningful information from it: title, body, badge, etc.
        CountlyPush.Message message = CountlyPush.decodeMessage(remoteMessage.getData());

        if (message != null &amp;&amp; message.has("typ")) {
            // custom handling only for messages with specific "typ" keys
            message.recordAction(getApplicationContext());
            return;
        }

        Intent notificationIntent = null;
        if (message.has("anotherActivity")) {
            notificationIntent = new Intent(getApplicationContext(), AnotherActivity.class);
        }
      
        Boolean result = CountlyPush.displayMessage(getApplicationContext(), message, R.drawable.ic_message, notificationIntent);
        if (result == null) {
            Log.i(TAG, "Message wasn't sent from Countly server, so it cannot be handled by Countly SDK");
        } else if (result) {
            Log.i(TAG, "Message was handled by Countly SDK");
        } else {
            Log.i(TAG, "Message wasn't handled by Countly SDK because API level is too low for Notification support or because currentActivity is null (not enough lifecycle method calls)");
        }
    }

    @Override
    public void onDeletedMessages() {
        super.onDeletedMessages();
    }
}</code></pre>
<p>
  <span style="font-weight: 400;">This class is responsible for token changes and message handling logic. Countly provides default UI for your notifications, which would display a <code>Notification</code></span><span style="font-weight: 400;">,</span><span style="font-weight: 400;">&nbsp;if your app is in the background, or <code>Dialog</code></span><span style="font-weight: 400;">,</span><span style="font-weight: 400;">&nbsp;if your app is active. It will also automatically report button clicks back to the server for Actioned metric conversion tracking. However, it is completely up to you, whether you would like to use this class or not. Let's have an overview of&nbsp;the <code>onMessageReceived</code></span><span style="font-weight: 400;">&nbsp;method:</span>
</p>
<ol>
  <li>
    <span style="font-weight: 400;">It calls <code>CountlyPush.decodeMessage()</code></span><span style="font-weight: 400;">&nbsp;to decode a message from the Countly-specific format. In this way, you'll have a method of accessing standard fields, such as a badge, URL, or your custom data keys.</span>
  </li>
  <li>
    <span style="font-weight: 400;">Then it checks if the message has&nbsp;a <code>typ</code></span><span style="font-weight: 400;">custom data key, and if it does, it only records the Actioned metric. Let's assume your custom notification is to preload some data from a remote server. Our demo app has a more in-depth scenario for this case.</span>
  </li>
  <li>
    <span style="font-weight: 400;">In case the message also has <code>anotherActivity</code></span><span style="font-weight: 400;">&nbsp;custom data key, it creates a <code>notificationIntent</code></span><span style="font-weight: 400;">&nbsp;to launch the activity, named <code>AnotherActivity</code></span><span style="font-weight: 400;">. This intent is only used as default content intent for the user tap on a <code>Notification</code></span><span style="font-weight: 400;">. It is not used for<code>Dialog</code></span><span style="font-weight: 400;">.</span>
  </li>
  <li>
    <span style="font-weight: 400;">Then the service calls <code>CountlyPush.displayMessage()</code></span><span style="font-weight: 400;">to perform a standard Countly notification displaying logic - <code>Notification</code></span><span style="font-weight: 400;">,</span><span style="font-weight: 400;">&nbsp;assuming your app is in the background or not running, and the <code>Dialog</code></span><span style="font-weight: 400;">&nbsp;is in the foreground. Note that this method takes an <code>int</code></span><span style="font-weight: 400;">&nbsp;resource parameter. It must be compatible with the corresponding version of the Android notification small icon.</span>
  </li>
</ol>
<p>
  <span style="font-weight: 400;">Apart from that which is listed above</span>,
  the SDK also exposes methods <code>CountlyPush.displayNotification()</code> &amp;
  <code>CountlyPush.displayDialog()</code>
  <span style="font-weight: 400;">in case you only</span> need
  <code>Notification</code>&nbsp;and don't want <code>Dialog</code> or vice versa.
</p>
<p>
  <span style="font-weight: 400;">This is an example of a push notification payload sent from the Countly server:</span>
</p>
<pre><code class="json">{
  collapse_key: “collapse_key”, // if present
  time_to_live: 123,
  data: {
    message: “message string”, // if present
    title: “title string”, // if present
    sound: “sound string”, // if present
    badge: 123, // if present
    c.i: “message id string”,
    c.l: “http://message-wide-url”, // if present
    c.m: “http://rich.media.url.jpg”, // if present
    c.s: “true”, // if sound &amp; message absent
    c.b: [ // if present
      {t: “Button 1 title”, l: “http://button.1.url”},
      {t: “Button 2 title”, l: “http://button.2.url”} // if present
    ],
    // any other data properties if present
  }
}
</code></pre>
<h2>
  <strong>Huawei PushKit</strong>
</h2>
<h3>Getting Huawei credentials</h3>
<p>
  Assuming you have followed Huawei's guide of
  <a href="https://developer.huawei.com/consumer/en/doc/distribution/app/agc-help-createapp-0000001146718717" target="_self">setting up an application</a>,
  next step would be to
  <a href="https://developer.huawei.com/consumer/en/doc/distribution/app/agc-enable_service#enable-service" target="_self">enable PushKit</a>.
  Then&nbsp;<a href="https://developer.huawei.com/consumer/en/doc/development/HMS-Guides/push-receipt" target="_self">enable Receipt status</a>:
</p>
<ul>
  <li>
    enter&nbsp;<code>https://YOUR_COUNTLY_SERVER/i/pushes/huawei</code> into
    the callback address field, while replacing YOUR_COUNTLY_SERVER with actual
    server address;
  </li>
  <li>
    and enter your certificate in PEM format (only your certificate, without
    the rest of the chain; usually first one in
    <code>openssl s_client -connect YOUR_COUNTLY_SERVER:443 -showcerts</code>).&nbsp;
  </li>
</ul>
<p>
  <img src="/hc/article_attachments/900003139063/Screenshot_2020-08-25_at_15.52.49.png" alt="Screenshot_2020-08-25_at_15.52.49.png">
</p>
<p>
  Then you'd need to get your App ID &amp; App secret from AppGallery Connect -&gt;
  My Apps:
</p>
<p>
  <img src="/hc/article_attachments/900003139103/Screenshot_2020-08-25_at_15.49.12.png" alt="Screenshot_2020-08-25_at_15.49.12.png">
</p>
<p>
  Copy your App ID &amp; the secret and paste it into Countly dashboard :
</p>
<p>
  <img src="/hc/article_attachments/900003139143/Screenshot_2020-08-25_at_16.04.29.png" alt="Screenshot_2020-08-25_at_16.04.29.png">
</p>
<h3>Integrating HMS into your app</h3>
<p>
  HMS implementation in Countly SDK looks very much like FCM: add dependencies,
  add service definition and the service class. Please refer to our
  <a href="https://github.com/Countly/countly-sdk-android/tree/master/app" target="_self">Demo app</a>
  for a reference implementation. Assuming you've already integrated
  <a href="https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides/android-integrating-sdk-0000001050040084" target="_self">HMS Core</a>
  into your app, all you need to do is add a dependency into build.gradle (<strong>use latest dependency version!</strong>):
</p>
<pre>implementation <span>'com.huawei.hms:push:4.0.3.301'<br></span></pre>
<p>... add service definition into AndroidManifest.xml:</p>
<pre>&lt;<span>service<br></span><span>    </span><span>android</span><span>:name</span><span>=".DemoHuaweiMessagingService"<br></span><span>    </span><span>android</span><span>:exported</span><span>="false"</span>&gt;<br>    &lt;<span>intent-filter</span>&gt;<br>        &lt;<span>action </span><span>android</span><span>:name</span><span>="com.huawei.push.action.MESSAGING_EVENT" </span>/&gt;<br>    &lt;/<span>intent-filter</span>&gt;<br>&lt;/<span>service</span>&gt;</pre>
<p>... and the service itself:</p>
<pre><span>public class </span>DemoHuaweiMessagingService <span>extends </span>HmsMessageService {<br>    <span>private static final </span>String <span>TAG </span>= <span>"DemoHuaweiMessagingService"</span>;<br><br>    <span>@Override<br></span><span>    </span><span>public void </span>onNewToken(String token) {<br>        <span>super</span>.onNewToken(token);<br><br>        CountlyPush.<span>onTokenRefresh</span>(token, Countly.CountlyMessagingProvider.<span>HMS</span>);<br>    }<br><br>    <span>@SuppressLint</span>(<span>"LongLogTag"</span>)<br>    <span>@Override<br></span><span>    </span><span>public void </span>onMessageReceived(RemoteMessage remoteMessage) {<br>        <span>super</span>.onMessageReceived(remoteMessage);<br><br>        Log.<span>d</span>(<span>TAG</span>, <span>"got new message: " </span>+ remoteMessage.getDataOfMap());<br><br>        <span>// decode message data and extract meaningful information from it: title, body, badge, etc.<br></span><span>        </span>CountlyPush.Message message = CountlyPush.<span>decodeMessage</span>(remoteMessage.getDataOfMap());<br>        <span>if </span>(message == <span>null</span>) {<br>            Log.<span>d</span>(<span>TAG</span>, <span>"Not a Countly message"</span>);<br>            <span>return</span>;<br>        }<br><br>        <span>if </span>(message.has(<span>"typ"</span>)) {<br>            <span>// custom handling only for messages with specific "typ" keys<br></span><span>            </span><span>if </span>(message.data(<span>"typ"</span>).equals(<span>"download"</span>)) {<br>                message.recordAction(getApplicationContext());<br>                <span>return</span>;<br>            } <span>else if </span>(message.data(<span>"typ"</span>).equals(<span>"promo"</span>)) {<br>                <span>return</span>;<br>            }<br>        }<br><br>        Intent intent = <span>null</span>;<br>        <span>if </span>(message.has(<span>"another"</span>)) {<br>            intent = <span>new </span>Intent(getApplicationContext(), ActivityExampleOthers.<span>class</span>);<br>        }<br>        Boolean result = CountlyPush.<span>displayMessage</span>(getApplicationContext(), message, R.drawable.<span>ic_message</span>, intent);<br>        <span>if </span>(result == <span>null</span>) {<br>            Log.<span>i</span>(<span>TAG</span>, <span>"Message doesn't have anything to display or wasn't sent from Countly server, so it cannot be handled by Countly SDK"</span>);<br>        } <span>else if </span>(result) {<br>            Log.<span>i</span>(<span>TAG</span>, <span>"Message was handled by Countly SDK"</span>);<br>        } <span>else </span>{<br>            Log.<span>i</span>(<span>TAG</span>, <span>"Message wasn't handled by Countly SDK because API level is too low for Notification support or because currentActivity is null (not enough lifecycle method calls)"</span>);<br>        }<br>    }<br>}</pre>
<p>
  ... which is almost identical to the FCM demo service.&nbsp;
</p>
<h2>Advanced features</h2>
<h3>Custom notification sound</h3>
<div class="callout callout--warning">
  <p>
    If you would like to use a custom sound in your push notifications, they
    must be present on the device. They may not be stored somewhere on the internet
    and then linked from there.
  </p>
</div>
<p>
  <span style="font-weight: 400;">For you to use a custom notification sound, there are 2 things you will need to do.</span>
</p>
<p>
  <span style="font-weight: 400;">First, you will need to prepare the URI that will link to the resource on your device. It would look something like this:</span>
</p>
<pre><code class="java">String soundUri = ContentResolver.SCHEME_ANDROID_RESOURCE + "://"+ getApplicationContext().getPackageName() + "/" + R.raw.notif_sound;</code></pre>
<p>
  <span style="font-weight: 400;">You would then send this URI as part of the push notification, using the "Send sound" field. This should cover devices with the Android SDK version less than 26.</span>
</p>
<p>
  <span style="font-weight: 400;">For devices with the SDK version 26+, you will also need to provide this URI during the notification channel setup. It would look something like this:</span>
</p>
<pre><code class="java">AudioAttributes audioAttributes = new AudioAttributes.Builder()
           .setContentType(AudioAttributes.CONTENT_TYPE_SONIFICATION)
           .setUsage(AudioAttributes.USAGE_NOTIFICATION)
           .build();

channel.setSound(soundUri, audioAttributes);</code></pre>
<p>
  More info about that here:
  <a href="https://stackoverflow.com/questions/48986856/android-notification-setsound-is-not-working">https://stackoverflow.com/questions/48986856/android-notification-setsound-is-not-working</a>
</p>
<h3>Automatic message handling</h3>
<p>
  <span style="font-weight: 400;">Countly handles most common message handling tasks for you. For example, it generates and shows <code>Notification</code></span><span style="font-weight: 400;">&nbsp;or <code>Dialog</code></span><span style="font-weight: 400;">&nbsp;and tracks conversion rates automatically. In most cases, it’s not necessary for you to know how it works, but if you would like to customize the behavior or exchange it with your own implementation, here is a more in-depth explanation of what it does.</span>
</p>
<p>
  <span style="font-weight: 400;">First, the received notification payload is analyzed and, if it's a Countly notification (if it has a <code>"c"</code></span><span style="font-weight: 400;">&nbsp;dictionary in the payload), it processes it. Otherwise, or if the notification analysis says it is a <code>Data-only</code></span><span style="font-weight: 400;">&nbsp;notification (you're the one responsible for message processing), it does nothing.</span>
</p>
<p>
  <span style="font-weight: 400;">Next, it automatically makes callbacks to the Countly Messaging server to calculate the number of open push notifications which got open and the number of notifications with positive reactions.</span>
</p>
<p>
  <span style="font-weight: 400;">Here are the explanations of common usage scenarios that are handled automatically:&nbsp;</span>
</p>
<ul>
  <li>
    <span style="font-weight: 400;"> It doesn't do anything, apart from conversion tracking if you specify it as a <code>Data-only</code></span><span style="font-weight: 400;">&nbsp;notification in the dashboard. This effectively sets a special flag in the message payload, so you may process it on your own. </span>
  </li>
  <li>
    <span style="font-weight: 400;">It displays a <code>Notification</code></span><span style="font-weight: 400;">&nbsp;whenever a message arrives, and your application is in the background. </span>
  </li>
  <li>
    <span style="font-weight: 400;">It displays <code>Dialog</code></span><span style="font-weight: 400;">&nbsp;when a new message arrives, and your application is in the foreground.&nbsp;</span>
  </li>
  <li>
    <span style="font-weight: 400;"> It displays <code>Dialog</code></span><span style="font-weight: 400;">&nbsp;when a new message with an action arrives (open URL), and the user responds to it by swiping or tapping the notification.</span>
  </li>
</ul>
<p>
  A <code>Dialog</code>
  <span style="font-weight: 400;">always has a message, but the set of displayed buttons depends on the message type:</span>
</p>
<ul>
  <li>
    <span style="font-weight: 400;">It displays a single ‘Cancel’ button for notifications without any actions (only a text message).</span>
  </li>
  <li>
    <span style="font-weight: 400;">For notifications with a&nbsp;</span><strong>URL</strong><span style="font-weight: 400;">&nbsp;(for instance, you ask the user to open a link to some blog post), it displays both the ‘Cancel’ &amp; ‘Open’ buttons.</span>
  </li>
  <li>
    <span style="font-weight: 400;">It displays the corresponding buttons for notifications with custom buttons.</span>
  </li>
</ul>
<h3>Using Android deep links</h3>
<p>
  <span style="font-weight: 400;">When using Countly push notifications, you may benefit from Android deep links in your application for the buttons you provide. Those are basically links for specific activities of your application. A link may either be a generic ‘http’ link, such as <code>http://www.oneexample.com/survey</code></span><span style="font-weight: 400;">,</span><span style="font-weight: 400;">&nbsp;or a link with a custom URI (uniform resource indicator) scheme, such as <code>otherexample://things</code></span><span style="font-weight: 400;">.</span>
</p>
<p>
  <span style="font-weight: 400;">In order for Android deep links to work, you will need to specify the intent filters in your application's manifest for the specific groups of links you would like to use.</span>
</p>
<p>
  <span style="font-weight: 400;">A deeper guide on how to configure your application to use deep links may be found&nbsp;</span><a href="https://developer.android.com/training/app-links/deep-linking.html"><span style="font-weight: 400;">here</span></a><span style="font-weight: 400;">.</span>
</p>
<h3>Developer-overridden message handling</h3>
<p>
  <span style="font-weight: 400;">You may also completely disable the push notification handling made by the Countly SDK. To do so, just add <code>true</code></span><span style="font-weight: 400;">&nbsp;to the end of your <code>initMessaging()</code></span><span style="font-weight: 400;">call:</span>
</p>
<pre><code class="java">Countly.sharedInstance()
    .init(this, "YOUR_SERVER", "APP_KEY", null, DeviceId.Type.ADVERTISING_ID)
    .initMessaging(this, CountlyActivity.class, "PROJECT_NUMBER", Countly.CountlyMessagingMode.TEST, true);

</code></pre>
<p>
  <span style="font-weight: 400;">This parameter effectively disables any UI interactions and <code>Activity</code></span><span style="font-weight: 400;">&nbsp;instantiation from the Countly SDK. To enable the custom processing of push notifications, you may either register your own <code>WakefulBroadcastReceiver</code></span><span style="font-weight: 400;">&nbsp;or use&nbsp;</span><a href="https://support.count.ly/hc/en-us/articles/360037754031-Android#push-notifications"><span style="font-weight: 400;">our example with the broadcast action</span></a><span style="font-weight: 400;">. Once you have switched off the default push notification UI, please make sure to call <code>CountlyMessaging.recordMessageOpen(id)</code></span>whenever
  a push notification is delivered to your device, and&nbsp;<code>CountlyMessaging.recordMessageAction(id, index)</code><span style="font-weight: 400;">, </span><span style="font-weight: 400;">whenever a user positively reacts to your notification. <code>id</code></span><span style="font-weight: 400;">&nbsp;is a message ID string you may receive from&nbsp;the <code>c.i</code></span><span style="font-weight: 400;">&nbsp;key of the push notification payload. <code>index</code></span><span style="font-weight: 400;">&nbsp;is optional and used to identify the type of action as follows: 0 for the tap on the notification in drawer, 1 for tap on first button of rich push, 2 for tap on the second button if there is any.</span>
</p>
<h3>Handling button or push clicks</h3>
<p>
  <span style="font-weight: 400;">When receiving a push notification, the user may click the notification directly or they may click the button. When a user clicks anywhere on the push notification, an intent is launched to open the provided link. This may be a web page URL or a deep link. If you have configured your app, so that opening this intent will open an activity of your app, it should be possible to track which button was pressed.</span>
</p>
<p>
  <span style="font-weight: 400;">There is also the option to add additional metadata to those intents. The included meta information contains data, such as which button was pressed, which link was given in the notification, the title, and the message of the notification.</span>
</p>
<p>
  <span style="font-weight: 400;">This functionality is disabled by default, and the additional metadata might be added as extras to the intent.</span>
</p>
<p>
  <span style="font-weight: 400;">In order to enable this functionality, you will need to call the following function before initializing Countly messaging:</span>
</p>
<pre><code class="java">Countly.sharedInstance().setPushIntentAddMetadata(true);</code></pre>
<p>
  <span style="font-weight: 400;">To access those extras from the intent, you should use these names:</span>
</p>
<pre><code class="java">ProxyActivity.intentExtraButtonLink
ProxyActivity.intentExtraMessageText
ProxyActivity.intentExtraMessageTitle
ProxyActivity.intentExtraWhichButton</code></pre>
<p>
  <span style="font-weight: 400;">To read the extra from the intent, you would use something similar to this:</span>
</p>
<pre><code class="java">String buttonUrl = intent.getStringExtra(ProxyActivity.intentExtraButtonLink);</code></pre>
<h2>Testing</h2>
<p>
  <span style="font-weight: 400;">You've probably noticed that we used <code>Countly.CountlyMessagingMode.TEST</code></span><span style="font-weight: 400;">&nbsp;in our example. That is because we are currently building the application only for testing purposes. Countly separates users who run apps built for test and for release. This way you'll be able to test messages before sending them to all your users. When releasing your app, please use <code>Countly.CountlyMessagingMode.PRODUCTION</code></span><span style="font-weight: 400;">.</span>
</p>
<h1>User location</h1>
<p>
  <span style="font-weight: 400;">While integrating this SDK into your application, you might want to track your user location. You could use this information to better know your app’s user base or to send them tailored push notifications based on their coordinates. There are 4 fields that may be provided:</span>
</p>
<ul>
  <li>
    <span style="font-weight: 400;">Country code in the two-letter, ISO standard</span>
  </li>
  <li>
    <span style="font-weight: 400;">City name (must be set together with the country code)</span>
  </li>
  <li>
    <span style="font-weight: 400;">Latitude and longitude values separated by a comma, e.g.</span>
    "56.42345,123.45325"
  </li>
  <li>
    <span style="font-weight: 400;">Your user’s IP address</span>
  </li>
</ul>
<p>During init you can either disable location:</p>
<pre>config.setDisableLocation();</pre>
<p>
  or set location info that will be sent during the start of the user session:
</p>
<pre>config.setLocation(countryCode, city, gpsCoordinates, ipAddress);</pre>
<p>
  Note that the ipAddress will only be updated if set through the init process.
</p>
<pre><code class="java">//set user location
String countryCode = "us";
String city = "Houston";
String latitude = "29.634933";
String longitude = "-95.220255";
String ipAddress = null;

Countly.sharedInstance().setLocation(countryCode, city, latitude + "," + longitude, ipAddress);</code></pre>
<p>
  When those values are set, a separate request will be created to send them sent.
  Except for ip address, because Countly Server processes IP address only when
  starting a session.
</p>
<p>If you don't want to set specific fields, set them to null.</p>
<p>
  Users might want to opt-out of location tracking. To do so, call:
</p>
<pre><code class="java">//disable location
Countly.sharedInstance().disableLocation();</code></pre>
<p>
  <span style="font-weight: 400;">This action will erase the cached location data from the device and the server.</span>
</p>
<h1>Remote Config</h1>
<p>
  <span style="font-weight: 400;">Remote config allows you to modify how your app functions or looks by requesting key-value pairs from your Countly server. The returned values may be modified based on the user profile. For more details, please see the&nbsp;</span><a href="https://resources.count.ly/docs/remote-config"><span style="font-weight: 400;">Remote Config documentation</span></a><span style="font-weight: 400;">.</span>
</p>
<h2>Automatic Remote Config download</h2>
<p>
  <span style="font-weight: 400;">There are two ways of acquiring remote config data: automatic download or manual request. Automatic remote config has been disabled by default and, therefore, without developer intervention, no remote config values will be requested.</span>
</p>
<p>
  <span style="font-weight: 400;">Automatic value download happens when the SDK is initiated or when the device ID is changed. You have to call <code>setRemoteConfigAutomaticDownload</code></span><span style="font-weight: 400;">&nbsp;before init to enable it. As an optional value, you may provide a callback to be informed when the request is finished.</span>
</p>
<pre><code class="java">Countly.sharedInstance().setRemoteConfigAutomaticDownload(true, new RemoteConfig.RemoteConfigCallback() {
            @Override
            public void callback(String error) {
                if(error == null) {
                    Toast.makeText(activity, "Automatic remote config download has completed", Toast.LENGTH_LONG).show();
                } else {
                    Toast.makeText(activity, "Automatic remote config download encountered a problem, " + error, Toast.LENGTH_LONG).show();
                }
            }
        });
Countly.sharedInstance().init(appC, COUNTLY_SERVER_URL, COUNTLY_APP_KEY);</code></pre>
<p>
  <span style="font-weight: 400;">If the callback returns a non-null value, you can expect that the request failed and no values were updated.</span>
</p>
<p>
  <span style="font-weight: 400;">When performing an automatic update, all locally stored values are replaced with the ones received (all locally stored values are deleted and replaced by new ones). It is possible that a previously valid key will return no value after an update.</span>
</p>
<h2>Manual Remote Config</h2>
<p>
  <span style="font-weight: 400;">There are three ways for manually requesting a remote config update: * Manually updating everything * Manually updating specific keys * Manually updating everything except specific keys.</span>
</p>
<p>
  <span style="font-weight: 400;">Each of these requests also has a callback. If the callback returns a non-null value, the request will encounter an error and fail.</span>
</p>
<p>
  <span style="font-weight: 400;">Functionally, the manual update for </span><span style="font-weight: 400;">everything&nbsp;<code>remoteConfigUpdate</code></span><span style="font-weight: 400;">&nbsp;is</span><span style="font-weight: 400;"> the same as the automatic update - it replaces all stored values with the ones from the server (all locally stored values are deleted and replaced with new ones). The advantage is that you can make the request whenever it is desirable for you. It has a callback to let you know when it has finished.</span>
</p>
<pre><code class="java">Countly.sharedInstance().remoteConfigUpdate(new RemoteConfig.RemoteConfigCallback() {
            @Override
            public void callback(String error) {
                if(error == null) {
                    Toast.makeText(activity, "Update finished", Toast.LENGTH_SHORT).show();
                } else {
                    Toast.makeText(activity, "Error: " + error, Toast.LENGTH_SHORT).show();
                }
            }
        });</code></pre>
<p>
  <span style="font-weight: 400;">Or you might only want to update specific key values. To do so, you will need to call <code>updateRemoteConfigForKeysOnly</code></span><span style="font-weight: 400;">&nbsp;with the list of keys you would like to be updated. That list is an array with the string values of those keys. It has a callback to let you know when the request has finished.</span>
</p>
<pre><code class="java">Countly.sharedInstance().updateRemoteConfigForKeysOnly(new String[]{"aa", "dd"}, new RemoteConfig.RemoteConfigCallback() {
            @Override
            public void callback(String error) {
                if(error == null) {
                    Toast.makeText(activity, "Update with inclusion finished", Toast.LENGTH_SHORT).show();
                } else {
                    Toast.makeText(activity, "Error: " + error, Toast.LENGTH_SHORT).show();
                }
            }
        });</code></pre>
<p>
  <span style="font-weight: 400;">Or you might want to update all the values except a few defined keys. To do so,&nbsp; call <code>updateRemoteConfigExceptKeys</code></span><span style="font-weight: 400;">. The key list is an array with string values of the keys. It has a callback to let you know when the request has finished.</span>
</p>
<pre><code class="java">Countly.sharedInstance().updateRemoteConfigExceptKeys(new String[]{"aa", "dd"}, new RemoteConfig.RemoteConfigCallback() {
            @Override
            public void callback(String error) {
                if (error == null) {
                    Toast.makeText(activity, "Update with exclusion finished", Toast.LENGTH_SHORT).show();
                } else {
                    Toast.makeText(activity, "Error: " + error, Toast.LENGTH_SHORT).show();
                }
            }
        });</code></pre>
<p>
  <span style="font-weight: 400;">When making requests with an "inclusion" or "exclusion" array, if those arrays are empty or null, they will function the same as a simple manual request and will update all the values. This means it will also erase all keys not returned by the server.</span>
</p>
<h2>Accessing Remote Config values</h2>
<p>
  To request a stored value, call <code>getRemoteConfigValueForKey</code>&nbsp;with
  the specified key. If it returns <code>null</code>
  <span style="font-weight: 400;">then no value was found. The SDK has no knowledge of the returned value type, and therefore, it will return the <code>Object</code></span>
  <span style="font-weight: 400;">. The developer then needs to cast it to the appropriate type. The returned values may also be <code>JSONArray</code></span><span style="font-weight: 400;">,&nbsp;</span><code>JSONObject</code>,
  or just a simple value, such as <code>int</code>.
</p>
<pre><code class="java">Object value_1 = Countly.sharedInstance().getRemoteConfigValueForKey("aa");
Object value_2 = Countly.sharedInstance().getRemoteConfigValueForKey("bb");
Object value_3 = Countly.sharedInstance().getRemoteConfigValueForKey("cc");
Object value_4 = Countly.sharedInstance().getRemoteConfigValueForKey("dd");

int int_value = (int) value_1;
double double_value = (double) value_2;
JSONArray jArray = (JSONArray) value_3;
JSONObject jobj = (JSONObject) value_4;</code></pre>
<h2>Clearing Stored values</h2>
<p>
  <span style="font-weight: 400;">At some point, you might like to erase all the values downloaded from the server. You will need to call one function to do so.</span>
</p>
<pre><code class="java">Countly.sharedInstance().remoteConfigClearValues();</code></pre>
<h1>User feedback</h1>
<p>
  <span style="font-weight: 400;">There are a couple ways of receiving feedback from your users: star-rating dialog, the rating widget and the feedback widgets (survey, nps).</span>
</p>
<p>
  <span style="font-weight: 400;">Star-rating dialog allows users to give feedback as a rating from 1 to 5. The rating widget allows users to rate using the same 1 to 5 rating system as well as leave a text comment. Feedback widgets (survey, nps) allow for even more textual feedback from users.</span>
</p>
<h2>Ratings</h2>
<h3>Star-rating dialog</h3>
<p>
  <span style="font-weight: 400;">Star-rating integration provides a dialog for receiving users’ feedback about the application. It contains a title, a simple message explaining its uses, a 1-to-5-star meter for receiving users’ ratings, and a dismiss button in case the user does not want to give a rating.</span>
</p>
<p>
  <span style="font-weight: 400;">This star rating has nothing to do with the Google Play Store ratings and reviews. It is just for getting brief feedback from users to be displayed on the Countly dashboard. If the user dismisses the star-rating dialog without providing a rating, the event will not be recorded.</span>
</p>
<p>
  <span style="font-weight: 400;">The star-rating dialog's title, message, and dismiss button text may be customized either through the init function or the <code>SetStarRatingDialogTexts</code></span><span style="font-weight: 400;">&nbsp;function. If you don't want to override one of those values, set it to "null".</span>
</p>
<pre><code class="java">//set it through the init function
Countly.sharedInstance().init(context, serverURL, appKey, deviceID, idMode, starRatingLimit, starRatingCallback, "Custom title", "Custom message", "Custom dismiss button text");

//Use the designated function:
Countly.sharedInstance().setStarRatingDialogTexts(context, "Custom title", "Custom message", "Custom dismiss button text");
</code></pre>
<p>
  <span style="font-weight: 400;">The star-rating dialog can be displayed in 2 ways:</span>
</p>
<ul>
  <li>Manually by the developer</li>
  <li>Automatically, depending on the session count</li>
</ul>
<p>
  <span style="font-weight: 400;">In order to display the star-rating dialog manually, you must call the <code>ShowStarRating</code></span><span style="font-weight: 400;">&nbsp;function. Optionally, you may provide the callback functions. There is no limit on how many times the star-rating dialog may be displayed manually.</span>
</p>
<pre><code class="java">//show the star rating without a callback
Countly.sharedInstance().showStarRating(context, null);

//show the star rating with a callback
Countly.sharedInstance().showStarRating(context, callback)</code></pre>
<p>
  <span style="font-weight: 400;">The star-rating dialog will be displayed automatically when an application's session count reaches the specified limit, i.e. once for each new version of the application. This session count limit may be specified upon initial configuration or through the <code>SetAutomaticStarRatingSessionLimit</code></span><span style="font-weight: 400;">&nbsp;function. The default limit is 3. Once the star-rating dialog has been displayed automatically, it will not be displayed again, unless a new app version comes along.</span>
</p>
<p>
  <span style="font-weight: 400;">You will need to pass the activity context during init in order to show the automatic star-rating dialog.</span>
</p>
<pre><code class="java">//set the rating limit through the init function
int starRatingLimit = 5;
Countly.sharedInstance().init(context, serverURL, appKey, deviceID, idMode, starRatingLimit, starRatingCallback, starRatingTextTitle, starRatingTextMessage, starRatingTextDismiss);

//set it through the designated function
Countly.sharedInstance().starRatingLimit(context, 5);</code></pre>
<p>
  <span style="font-weight: 400;">If you would like to enable the automatic star-rating function, use the <code>SetIfStarRatingShownAutomatically</code></span><span style="font-weight: 400;">&nbsp;function, it is disabled by default.</span>
</p>
<pre><code class="java">//enable automatic star rating
Countly.sharedInstance().ratings().setIfStarRatingShownAutomatically(true);

//disable automatic star rating
Countly.sharedInstance().ratings().setIfStarRatingShownAutomatically(false);</code></pre>
<p>
  <span style="font-weight: 400;">If you would like to have the star rating shown only once per app's lifetime and not for each new version, use the <code>SetStarRatingDisableAskingForEachAppVersion</code> function.</span>
</p>
<pre><code class="java">//disable star rating for each new version
Countly.sharedInstance().setStarRatingDisableAskingForEachAppVersion(true);

//enable star rating for each new version
Countly.sharedInstance().setStarRatingDisableAskingForEachAppVersion(false);</code></pre>
<p>
  <span style="font-weight: 400;">The star-rating callback provides functions for two events. <code>OnRate</code></span><span style="font-weight: 400;">&nbsp;is called when the user chooses a rating. <code>OnDismiss</code></span><span style="font-weight: 400;">&nbsp;is called when the user clicks the back button, clicks outside the dialog, or clicks the "Dismiss" button. The callback provided in the init function is only used when displaying the automatic star rating. Only the provided callback will be used for the manual star rating.</span>
</p>
<pre><code class="java">StarRatingCallback callback = new StarRatingCallback() {
    @Override
    public void OnRate(int rating) {
      //the user rated the app
    }

    @Override
    public void OnDismiss() {
      //the star rating dialog was dismissed
    }
};</code></pre>
<h3>Rating widget</h3>
<p>
  <span style="font-weight: 400;">The rating widget shows a server configured widget to your user devices.</span>
</p>
<div class="img-container">
  <img src="/hc/article_attachments/9508502169241/003.png" alt="003.png">
</div>
<p>
  <span style="font-weight: 400;">It's possible to configure any of the shown text fields and replace them with a custom string of your choice.</span>
</p>
<p>
  <span style="font-weight: 400;">In addition to a 1 to 5 rating, users may also leave a text comment along with an email, should the user desire to be contacted by the app developer.</span>
</p>
<p>
  <span style="font-weight: 400;">Trying to show the rating widget is a single call, but, in reality, it’s a two-step process. Before it is displayed, the SDK attempts to contact the server to receive more information regarding the dialog. Therefore, a network connection is needed.</span>
</p>
<p>
  <span style="font-weight: 400;">You may try to show the widget after you have initialized the SDK. To do so, you will first need to receive the widget ID from your server:</span>
</p>
<div class="img-container">
  <img src="/hc/article_attachments/9508523082649/004.png" alt="004.png">
</div>
<p>
  <span style="font-weight: 400;">Using the widget ID, you may call the function to show the widget popup:</span>
</p>
<pre><code class="java">String widgetId = "xxxxx";
String closeButtonText = "Close";
Countly.sharedInstance().ratings().showFeedbackPopup(widgetId, closeButtonText, activity, new FeedbackRatingCallback() {
  @Override
  public void callback(String error) {
    if(error != null){
      Toast.makeText(activity, "Encountered error while showing raging widget dialog: [" + error + "]", Toast.LENGTH_LONG).show();
    }
  }
});</code></pre>
<h3>Manual rating reporting</h3>
<p>
  You may want to display your own custom UI to query users about the information
  in the rating widget. In case you do that, you would then report that rating
  result manually. To do that you would use the following call:
</p>
<pre><code class="java">String widgetId = <span>"5f15c01425f83c169c33cb65"</span>;<br><span>int </span>rating = <span>3</span>;<br>String email = <span>"foo@bar.garr"</span>;<br>String comment = <span>"Ragnaros should watch out"</span>;<br>Boolean userCanBeContacted = <span>true</span>;<br>Countly.<span>sharedInstance</span>().ratings().recordManualRating(widgetId, rating, email, comment, userCanBeContacted);</code></pre>
<h2>Feedback widget</h2>
<p>
  It is possible to display 2 kinds of feedback widgets:
  <a href="https://support.count.ly/hc/en-us/articles/900003407386-NPS-Net-Promoter-Score-" target="_blank" rel="noopener">nps</a>
  and
  <a href="https://support.count.ly/hc/en-us/articles/900004337763-Surveys" target="_blank" rel="noopener">survey.</a>&nbsp;Both
  widgets are shown as webviews.
</p>
<p>They both use the same code mechanisms.&nbsp;</p>
<p>
  Before any feedback widgets can be shown, you need to create them in your countly
  dashboard.
</p>
<p>
  When the widgets are created, you need to use 2 calls in your SDK: one to get
  all currently available widgets for this user and the second to display a chosen
  widget.
</p>
<p>To get your available widget list, you would use:</p>
<pre>Countly.<span>sharedInstance</span>().feedback().getAvailableFeedbackWidgets(<span>new </span>RetrieveFeedbackWidgets() {<br>    <span>@Override </span><span>public void </span>onFinished(List&lt;CountlyFeedbackWidget&gt; retrievedWidgets, String error) {<br><br>    }<br>});</pre>
<p>
  From the callback you would get the list of all available widgets that apply
  to the current device id.
</p>
<p>The objects in the returned list look like this:</p>
<pre><span>class </span>CountlyFeedbackWidget {<br>    <span>public </span>String <span>widgetId</span>;<br>    <span>public </span>FeedbackWidgetType <span>type</span>;<br>    <span>public </span>String <span>name</span>;<br>}</pre>
<p>
  To determine what kind of widget that is, you would check the "type" value. The
  potential values are:
</p>
<pre>FeedbackWidgetType {<span>survey</span>, <span>nps</span>}</pre>
<p>
  You would then use the widget type and description (which is the same as provided
  in the dashboard) to decide which widget to show.
</p>
<p>
  After you have decided which widget you want to display, you would provide that
  object to the following function:
</p>
<pre>Countly.<span>sharedInstance</span>().feedback().presentFeedbackWidget(chosenWidget, context, <span>"Close"</span>, <span>new </span>FeedbackCallback() {<br>    <span>@Override </span><span>public void </span>onFinished(String error) {<br><br>    }<br>});</pre>
<h2>Feedback widget manual reporting</h2>
<p>
  There might be some usecases where you might to use the native UI or a custom
  UI you have created instead of our webview solution. In those cases you would
  have to request all the widget related information and then report the result
  manually.
</p>
<p>
  For a sample integration, have a look at our sample app in the repo.
</p>
<p>
  First you would need to retrieve the available widget list with the previously
  mentioned `getAvailableFeedbackWidgets` call. After that you would have a list
  of possible `CountlyFeedbackWidget` objects. You would pick the one widget you
  would want to display.
</p>
<p>
  Having the `CountlyFeedbackWidget` object of the widget you would want to display,
  you would use the following call to retrieve the widget information:
</p>
<pre>Countly.<span>sharedInstance</span>().feedback().getFeedbackWidgetData(chosenWidget, <span>new </span>RetrieveFeedbackWidgetData() {<br>    <span>@Override </span><span>public void </span>onFinished(JSONObject retrievedWidgetData, String error) {<br><br>    }<br>}</pre>
<p>
  `retrievedWidgetData` would contain a JSON with all of the required information
  to present the widget yourself.
</p>
<p>
  After you have collected the required information from your users, you would
  package the responses into a `Map&lt;String, Object&gt;` and then use it, the
  widgetInformation and the widgetData to report the feedback result with the following
  call:
</p>
<pre>//this contains the reported results<br>Map&lt;String, Object&gt; reportedResult = <span>new </span>HashMap&lt;&gt;();<br><br>//<br>// You would fill out the results here. That step is not displayed in this sample<br>//<br><br>//report the results to the SDK<br>Countly.<span>sharedInstance</span>().feedback().reportFeedbackWidgetManually(<span>widgetToReport</span>, retrievedWidgetData, reportedResult);</pre>
<p>
  If the user would have closed the widget, you would report that by passaing a
  "null" reportedResult.
</p>
<p>
  For more information regarding the returned data structure and how to structure
  the response, you would look
  <a href="/hc/en-us/articles/900004340186" target="_self">here</a>.
</p>
<h1>User Profiles</h1>
<p>
  <span style="font-weight: 400;">Available with Enterprise Edition, User Profiles is a tool that helps you identify users, their devices, event timelines, and application crash information. User Profiles may contain any information you either collect or is collected automatically by the Countly SDK.</span>
</p>
<p>
  <span style="font-weight: 400;">You may send user-related information to Countly and let the Countly dashboard show and segment this data. You may also send a notification to a group of users. For more information about User Profiles, review&nbsp;</span><a href="http://resources.count.ly/docs/user-profiles"><span style="font-weight: 400;">this documentation</span></a><span style="font-weight: 400;">.</span>
</p>
<p>
  <span style="font-weight: 400;">You must call the <code>Countly.userData.setUserData</code></span><span style="font-weight: 400;">&nbsp;function in order to provide information regarding the current user. You may call this function by providing a bundle of only the predefined fields, or you may call this function while also providing a second bundle of fields with your custom keys. After you have provided the user profile information, you must save it by calling <code>Countly.userData.save()</code></span><span style="font-weight: 400;">.</span>
</p>
<pre><code class="java">//Update the user profile using only predefined fields
Map&lt;String, String&gt; predefinedFields = new HashMap&lt;&gt;();
Countly.userData.setUserData(predefinedFields);
Countly.userData.save()


//Update the user profile using predefined and custom fields
Map&lt;String, String&gt; predefinedFields = new HashMap&lt;&gt;();
Map&lt;String, String&gt; customFields = new HashMap&lt;&gt;();
Countly.userData.setUserData(predefinedFields, customFields);
Countly.userData.save()</code></pre>
<p>The keys for predefined user data fields are as follows:</p>
<table>
  <tbody>
    <tr>
      <th>Key</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>name</td>
      <td>String</td>
      <td>User's full name</td>
    </tr>
    <tr>
      <td>username</td>
      <td>String</td>
      <td>User's nickname</td>
    </tr>
    <tr>
      <td>email</td>
      <td>String</td>
      <td>User's email address</td>
    </tr>
    <tr>
      <td>organization</td>
      <td>String</td>
      <td>User's organization name</td>
    </tr>
    <tr>
      <td>phone</td>
      <td>String</td>
      <td>User's phone number</td>
    </tr>
    <tr>
      <td>picture</td>
      <td>String</td>
      <td>URL to avatar or profile picture of the user</td>
    </tr>
    <tr>
      <td>picturePath</td>
      <td>String</td>
      <td>Local path to the user's avatar or profile picture</td>
    </tr>
    <tr>
      <td>gender</td>
      <td>String</td>
      <td>User's gender as M for male and F for female</td>
    </tr>
    <tr>
      <td>byear</td>
      <td>String</td>
      <td>User's year of birth as integer</td>
    </tr>
  </tbody>
</table>
<p>
  <span style="font-weight: 400;">Using "" for strings or a negative number for 'byear' will effectively delete that property.</span>
</p>
<p>
  <strong><span style="font-weight: 400;">You may use any key values to be stored and displayed on your Countly backend for custom user properties.&nbsp;</span>Note: keys with . or $ symbols will have those symbols removed.</strong>
</p>
<h2>Modifying custom data</h2>
<p>
  <span style="font-weight: 400;">Additionally, you may perform different manipulations on your custom data values, such as incrementing the current value on a server or storing an array of values under the same property.</span>
</p>
<p>
  <span style="font-weight: 400;">You will find the list of available methods below:</span>
</p>
<pre><code class="java">//set one custom properties
Countly.userData.setProperty("test", "test");
//increment used value by 1
Countly.userData.increment("used");
//increment used value by provided value
Countly.userData.incrementBy("used", 2);
//multiply value by provided value
Countly.userData.multiply("used", 3);
//save maximal value
Countly.userData.saveMax("highscore", 300);
//save minimal value
Countly.userData.saveMin("best_time",60);
//set value if it does not exist
Countly.userData.setOnce("tag", "test");
//insert value to array of unique values
Countly.userData.pushUniqueValue("type", "morning");
//insert value to array which can have duplocates
Countly.userData.pushValue("type", "morning");
//remove value from array
Countly.userData.pullValue("type", "morning");

//send provided values to server
Countly.userData.save();</code></pre>
<p>
  In the end, always call <strong>Countly.userData.save()</strong> to send them
  to the server.
</p>
<h2>Orientation tracking</h2>
<p>
  To record your applications orientation changes, you need to enable it on your
  init object like:
</p>
<pre>config.setTrackOrientationChanges(<span>true</span>);</pre>
<p>
  You need to add this to all of your activities where you want to track orientation:
</p>
<pre><code><span>android</span><span>:configChanges</span><span>="orientation|screenSize"</span></code></pre>
<p>Inside of your manifest, it would look something like this:</p>
<pre><code>&lt;<span>activity<br></span><span>    </span><span>android</span><span>:name</span><span>=".ActivityExample"<br></span><span>    </span><span>android</span><span>:label</span><span>="@string/activity_name"<br></span><span>    </span><span>android</span><span>:configChanges</span><span>="orientation|screenSize"</span>&gt;<br>&lt;/<span>activity</span>&gt;</code></pre>
<p>
  To finish your setup for orientation tracking, you need to set up the android
  callback for "onConfigurationChanged". In those you would have to call "Countly.sharedInstance().onConfigurationChanged(newConfig)".&nbsp;You
  may set it up similarly to this:
</p>
<pre><code class="java"><span>@Override<br></span><span>public void </span>onConfigurationChanged (Configuration newConfig){<br>    <span>super</span>.onConfigurationChanged(newConfig);<br>    Countly.<span>sharedInstance</span>().onConfigurationChanged(newConfig);<br>}</code></pre>
<h1>Application Performance Monitoring</h1>
<p>
  This SDK provides a few mechanisms for APM. To browse some of the provided functionality,
  check the returned interface from here:
</p>
<pre>Countly.<span>sharedInstance</span>().apm()</pre>
<p>
  While using APM calls, you have the ability to provide trace keys by which you
  can track those parameters in your dashboard. Those keys have to abide by the
  following regex:
</p>
<pre><span>/^[a-zA-Z][a-zA-Z0-9_]*$/</span></pre>
<p>
  In short, only Latin letters, numbers, and underscores can be used. The key can
  not start with an underscore or number. The key also has to be shorter than 32
  characters.
</p>
<h2>Custom trace</h2>
<p>
  Currently, you can use custom traces to record the duration of application processes.
  At the end of them, you can also provide any additionally gathered data.
</p>
<p>
  The trace key uniquely identifies the thing you are tracking and the same name
  will be shown in the dashboard. The SDK does not support tracking multiple events
  with the same key.
</p>
<p>To start a custom trace, use:</p>
<pre>Countly.<span>sharedInstance</span>().apm().startTrace(String traceKey);</pre>
<p>To end a custom trace, use:</p>
<pre>Map&lt;String, Integer&gt; customMetric = <span>new </span>HashMap();<br>customMetric.put(<span>"ABC"</span>, <span>1233</span>);<br>customMetric.put(<span>"C44C"</span>, <span>1337</span>);<br><br>Countly.<span>sharedInstance</span>().apm().endTrace(String traceKey, customMetric);</pre>
<p>
  The provided Map of integer values that will be added to that trace in the dashboard.
</p>
<h2>Network trace</h2>
<p>You can use the APM to track your requests.</p>
<p>Call this just before making your network request:</p>
<pre>Countly.<span>sharedInstance</span>().apm().startNetworkRequest(String networkTraceKey, String uniqueId);</pre>
<p>
  `NetworkTraceKey` would be a unique identifier of the API endpoint you are targeting.
  `UniqueId` is an identifier for requests for a specific traceKey. In case you
  have overlapping network requests, you would have a unique id for each of the
  requests.&nbsp;`NetworkTraceKey` and&nbsp;`UniqueId` are used as a pair to uniquely
  identify the request you are making.
</p>
<p>Call this after your network request is done:</p>
<pre>Countly.<span>sharedInstance</span>().apm().endNetworkRequest(String networkTraceKey, String uniqueId, int responseCode, int requestPayloadSize, int responsePayloadSize);</pre>
<p>
  You would provide the same `NetworkTraceKey` and&nbsp;`UniqueId` as starting
  the request and then also provided the received response code, sent payload size
  in bytes, and received payload size in bytes.
</p>
<h2>Automatic device traces</h2>
<p>Currently, the Android SDK provides 3 automatic traces:</p>
<ul>
  <li>App start time</li>
  <li>App time in the background</li>
  <li>App time in foreground</li>
</ul>
<p>To record app start time you need to implement 3 things.</p>
<p>First, you must enable this feature in config on init:</p>
<pre>config.setRecordAppStartTime(<span>true</span>)</pre>
<p>
  Second, you must call `Countly.applicationOnCreate();` right after your application
  classes `onCreate` like:
</p>
<pre><span>public class </span>App <span>extends </span>Application {<br>    <span>@Override<br></span><span>    </span><span>public void </span>onCreate() {<br>        <span>super</span>.onCreate();<br>        Countly.<span>applicationOnCreate</span>();<br>        ...<br>    }<br>}</pre>
<p>
  Third, you must initialize countly in your apps Application onStart callback.
</p>
<p>If you do this, you will get the correct on start times.</p>
<h2>App time in background/foreground</h2>
<p>
  Countly will record the time your users spend in the foreground and background.
  For this to work, your users need to be given any consent. You also need to provide
  your Application class to your config object with "<span>setApplication" during init.</span>
</p>
<h1>User Consent</h1>
<p>
  <span style="font-weight: 400;">In an effort to comply with GDPR, starting from 18.04, Countly provides ways to toggle different Countly features on/off depending on the given consent.</span>
</p>
<p>
  More information about GDPR can be found
  <a href="https://blog.count.ly/countly-the-gdpr-how-worlds-leading-mobile-and-web-analytics-platform-can-help-organizations-5015042fab27">here</a>.
</p>
<p>
  <span style="font-weight: 400;">The requirement for consent is disabled by default. To enable it, you will have to call <code>setRequiresConsent</code></span><span style="font-weight: 400;">&nbsp;with <code>true</code></span><span style="font-weight: 400;">&nbsp;before initializing Countly.</span>
</p>
<pre><code class="java">Countly.sharedInstance().setRequiresConsent(true);
Countly.sharedInstance().init(appC, COUNTLY_SERVER_URL, COUNTLY_APP_KEY);</code></pre>
<p>
  <span style="font-weight: 400;">By default, no consent is given. That means that if no consent is enabled, Countly will not work and no network requests related to its features will be sent. When the consent status of a feature is changed, that change will be sent to the Countly server.</span>
</p>
<p>
  <span style="font-weight: 400;">For all features, except <code>push</code></span><span style="font-weight: 400;">, consent is not persistent and will have to be set each time before Countly init. Therefore, the storage and persistence of the given consent falls on the SDK integrator.</span>
</p>
<p>
  <span style="font-weight: 400;">Consent for features may be given and revoked at any time, but if it is given after Countly init, some features may only work in part.</span>
</p>
<p>
  <span style="font-weight: 400;">If consent is removed, but the appropriate function can't be called before the app closes, it should be done upon the next app start, so that any relevant server-side features may be disabled (such as the reverse geo IP for location).</span>
</p>
<p>
  <span style="font-weight: 400;">Feature names in the Android SDK are stored as static fields in the class called <code>CountlyFeatureNames</code></span><span style="font-weight: 400;">.</span>
</p>
<p>The current features are:</p>
<p>
  * <code>sessions</code> - tracking when, how often and how long users use your
  app
</p>
<p>
  * <code>events</code> - allow sending events to the server
</p>
<p>
  * <code>views</code> - allow the tracking of which views user visits
</p>
<p>
  * <code>location</code> - allow the sending of location information
</p>
<p>
  * <code>crashes</code> - allow the tracking of crashes, exceptions, and errors
</p>
<p>
  * <code>attribution</code> - allow tracking of which campaign did the user come
  from
</p>
<p>
  * <code>users</code> - allow the collecting/providing of user information, including
  custom properties
</p>
<p>
  * <code>push</code> - allow push notifications
</p>
<p>
  * <code>starRating</code> - allow their rating and feedback to be sent
</p>
<p>
  * <code>apm</code> - allow usage of APM features and collection of APM related
  data
</p>
<p>
  * <code>feedback</code> - allow to show the survey and nps feedback widgets
</p>
<p>
  * <code>remoteConfig</code> - allow to download remote config values from your
  server
</p>
<h2>Feature groups</h2>
<p>
  <span style="font-weight: 400;">Features may be put into groups. By doing this, you may give/remove consent to multiple features in the same call. They may be created using <code>createFeatureGroup</code></span><span style="font-weight: 400;">. Those groups are not persistent and must be created on every restart.</span>
</p>
<pre><code class="java">// prepare features that should be added to the group
String[] groupFeatures = new String[]{ Countly.CountlyFeatureNames.sessions, Countly.CountlyFeatureNames.location };

// create the feature group
Countly.sharedInstance().createFeatureGroup("groupName", groupFeatures);</code></pre>
<h2>Changing consent</h2>
<p>
  <span style="font-weight: 400;">There are 3 ways of changing feature consent: </span>
</p>
<ul>
  <li>
    <span style="font-weight: 400;"><code>giveConsent</code>/<code>removeConsent</code></span><span style="font-weight: 400;">&nbsp;- gives or removes consent to a specific feature.</span>
  </li>
</ul>
<pre><code class="java">// give consent to "sessions" feature
Countly.sharedInstance().giveConsent(new String[]{Countly.CountlyFeatureNames.sessions});

// remove consent from "sessions" feature
Countly.sharedInstance().removeConsent(new String[]{Countly.CountlyFeatureNames.sessions});</code></pre>
<ul>
  <li>
    <code>setConsent</code> - set consent to a specific (true/false) value
  </li>
</ul>
<pre><code class="java">// give consent to "sessions" feature
Countly.sharedInstance().setConsent(new String[]{Countly.CountlyFeatureNames.sessions}, true);

// remove consent from "sessions" feature
Countly.sharedInstance().setConsent(new String[]{Countly.CountlyFeatureNames.sessions}, false);</code></pre>
<ul>
  <li>
    <code>setConsentFeatureGroup</code> - set consent for a feature group to
    a specific (true/false) value
  </li>
</ul>
<pre><code class="java">// prepare features that should be added to the group
String[] groupFeatures = new String[]{ Countly.CountlyFeatureNames.sessions, Countly.CountlyFeatureNames.location };

String groupName = "featureGroup1";

// give consent to "sessions" and "location" feature with a single consent group call
Countly.sharedInstance().setConsentFeatureGroup(groupName, true);

// remove consent from "sessions" and "location" feature with a single consent group call
Countly.sharedInstance().setConsentFeatureGroup(groupName, false);</code></pre>
<h1>Security and privacy</h1>
<h2>SSL certificate pinning</h2>
<p>
  <span>Public key and certificate pinning are techniques that improve communication security by eliminating the threat of&nbsp;</span><a href="https://en.wikipedia.org/wiki/Man-in-the-middle_attack">man-in-the-middle attack (MiM)</a><span>&nbsp;in SSL connections.&nbsp;</span>
</p>
<p>
  <span>When you supply a list of acceptable SSL certificates to Countly SDK with either&nbsp;</span><code>countlyConfig.enablePublicKeyPinning()</code><span>&nbsp;or&nbsp;</span><code>countlyConfig.enableCertificatePinning()</code><span>, it will ensure that connection is made with one of the public keys specified or one of the certificates specified respectively. Using whole certificate pinning is somewhat safer, but using public key pinning is preferred since certificates can be rotated and do expire while public keys don't (assuming you don't change your CA).</span>
</p>
<p>
  Pinning is done during init through the CountlyConfig object.
</p>
<p>
  <span>To get the current public key or whole certificate from your server you can use one of these snippets (replace try.count.ly with your server name):</span>
</p>
<pre>//get the public key<br>openssl s_client -connect <span>try</span>.count.ly:<span>443 | openssl x509 -pubkey -noout
<br>//get the list of certificates<br>openssl s_client -connect <span>try</span>.count.ly:<span>443 </span>-showcerts</span></pre>
<p>
  In the certificate case, the first entry would be the certificate for your server
  (what you need to enter into SDK configuration) and the rest would be the chain
  of trust to the root certificate authority.
</p>
<p>
  Here is an example of public key pinning for the <strong>try.count.ly</strong>
  server.
</p>
<pre><span>//sample certificate for the countly try server<br></span>String[] certificates = <span>new </span>String[] {<br>    <span>"MIIGnjCCBYagAwIBAgIRAN73cVA7Y1nD+S8rToAqBpQwDQYJKoZIhvcNAQELBQAwgY8xCzAJ"<br></span><span>        </span>+ <span>"BgNVBAYTAkdCMRswGQYDVQQIExJHcmVhdGVyIE1hbmNoZXN0ZXIxEDAOBgNVBAcTB1"<br></span><span>        </span>+ <span>"NhbGZvcmQxGDAWBgNVBAoTD1NlY3RpZ28gTGltaXRlZDE3MDUGA1UEAxMuU2VjdGln"<br></span><span>        </span>+ <span>"byBSU0EgRG9tYWluIFZhbGlkYXRpb24gU2VjdXJlIFNlcnZlciBDQTAeFw0yMDA2MD"<br></span><span>        </span>+ <span>"EwMDAwMDBaFw0yMjA5MDMwMDAwMDBaMBUxEzARBgNVBAMMCiouY291bnQubHkwggEi"<br></span><span>        </span>+ <span>"MA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCl9zmATVRwrGRtRQJcmBmA+zc/ZL"<br></span><span>        </span>+ <span>"io3YfkwXO2w8u9lnw60J4JpPNn9OnGcxdM+sqbXKU3jTdjY4j3yaA6NlWibq2jU2x6"<br></span><span>        </span>+ <span>"HT2sS+I5gFFE/6tO53WqjoMk48i3FkyoJDittwtQrVaRGcP8RjJH0pfXaP+JLrLAgg"<br></span><span>        </span>+ <span>"HuW3tCFqYzkWi3uLGVjQbSIRNiXsM3FI0UMEa/x1I3U4hLjMjH28KagZbZLWnHOvks"<br></span><span>        </span>+ <span>"AvGLg3xQkS+GSQ+6ARZ2/bGh5O9q4hCCCk0/PpwAXmrOnWtwrNuwHcCDOvuB22JxLd"<br></span><span>        </span>+ <span>"t8jQDYrjwtJIvq4Yut8FQPv/75SKoETWWHyxe0x5NsB34UwA/BAgMBAAGjggNsMIID"<br></span><span>        </span>+ <span>"aDAfBgNVHSMEGDAWgBSNjF7EVK2K4Xfpm/mbBeG4AY1h4TAdBgNVHQ4EFgQU8uf/ND"<br></span><span>        </span>+ <span>"Rt8cu+AwARVIGXPMfxGbQwDgYDVR0PAQH/BAQDAgWgMAwGA1UdEwEB/wQCMAAwHQYD"<br></span><span>        </span>+ <span>"VR0lBBYwFAYIKwYBBQUHAwEGCCsGAQUFBwMCMEkGA1UdIARCMEAwNAYLKwYBBAGyMQ"<br></span><span>        </span>+ <span>"ECAgcwJTAjBggrBgEFBQcCARYXaHR0cHM6Ly9zZWN0aWdvLmNvbS9DUFMwCAYGZ4EM"<br></span><span>        </span>+ <span>"AQIBMIGEBggrBgEFBQcBAQR4MHYwTwYIKwYBBQUHMAKGQ2h0dHA6Ly9jcnQuc2VjdG"<br></span><span>        </span>+ <span>"lnby5jb20vU2VjdGlnb1JTQURvbWFpblZhbGlkYXRpb25TZWN1cmVTZXJ2ZXJDQS5j"<br></span><span>        </span>+ <span>"cnQwIwYIKwYBBQUHMAGGF2h0dHA6Ly9vY3NwLnNlY3RpZ28uY29tMB8GA1UdEQQYMB"<br></span><span>        </span>+ <span>"aCCiouY291bnQubHmCCGNvdW50Lmx5MIIB9AYKKwYBBAHWeQIEAgSCAeQEggHgAd4A"<br></span><span>        </span>+ <span>"dQBGpVXrdfqRIDC1oolp9PN9ESxBdL79SbiFq/L8cP5tRwAAAXJwTJ0kAAAEAwBGME"<br></span><span>        </span>+ <span>"QCIEErTN/aGJ8LV9brGklKeGAXMg1EN/FUxXDu13kNfXhcAiBrKMYe+W4flPyuLNm5"<br></span><span>        </span>+ <span>"jp6FJwtUTZPNpZ+TmM40dRdwjQB0AN+lXqtogk8fbK3uuF9OPlrqzaISpGpejjsSwC"<br></span><span>        </span>+ <span>"BEXCpzAAABcnBMncsAAAQDAEUwQwIfEYSpsSDtKpmj9ZmRWsx73G622N74v09JDjzP"<br></span><span>        </span>+ <span>"bkg9RQIgUelIqSwqu69JanH7losrqTTsjwNv+3QJBNJ6GxJKkh0AdgBvU3asMfAxGd"<br></span><span>        </span>+ <span>"iZAKRRFf93FRwR2QLBACkGjbIImjfZEwAAAXJwTJ0YAAAEAwBHMEUCIQCMBaaQAoua"<br></span><span>        </span>+ <span>"97R+z2zONMUq1XsDP5aoAiutZG4XxuQ6wAIgW1p6XS3az4CCqjwbDKxL9qEnw8fWd+"<br></span><span>        </span>+ <span>"yLx2skviSsTS0AdwApeb7wnjk5IfBWc59jpXflvld9nGAK+PlNXSZcJV3HhAAAAXJw"<br></span><span>        </span>+ <span>"TJ1PAAAEAwBIMEYCIQDg1YFbJPPKDIyrFZJ9rtrUklkh2k/wpgwjDuIp7tPtOgIhAL"<br></span><span>        </span>+ <span>"dZl9s/qISsFm2E64ruYbdE4HKR1ZJ0zbIXOZcds7XXMA0GCSqGSIb3DQEBCwUAA4IB"<br></span><span>        </span>+ <span>"AQB2Ar1h2X/S4qsVlw0gEbXO//6Rj8mTB4BFW6c5r84n0vTwvA78h003eX00y0ymxO"<br></span><span>        </span>+ <span>"i5hkqB8gd1IUSWP1R1ijYtBVPdFi+SsMjUsB5NKquQNlWpo0GlFjRlcXnDC6R6toN2"<br></span><span>        </span>+ <span>"QixJb47VM40Vmn2g0ZuMGfy1XoQKvIyRosT92jGm1YcF+nLEHBDr+89apZ8sUpFfWo"<br></span><span>        </span>+ <span>"AnCom+8sBGwje6zP10eBbprHyzM8snvdwo/QNLAzLcvVNKP+Sr4H7HKzec3g1+THI0"<br></span><span>        </span>+ <span>"M72TzoguJcOZQEI6Pd+FIP5Xad53rq4jCtRGwYrsieH49a3orBnkkJvUKni+mtkxMb"<br></span><span>        </span>+ <span>"PTJ7eeMmX9g/0h"<br></span>};<br><br>CountlyConfig countlyConfig = <span>new </span>CountlyConfig(getApplicationContext(), <span>"c4608d0a021b1cef0f8cb031f51200e9cbe48dd4"</span>, <span>"https://try.count.ly"</span>);<br>countlyConfig.enablePublicKeyPinning(certificates);<br>Countly.<span>sharedInstance</span>().init(countlyConfig);</pre>
<p>
  In case you get a <code>CertificateException</code> with&nbsp;<code>"Public keys didn't pass checks"</code>
  that means the certificate or public key for the reached server did not match
  to any one of the provided ones. Usually, it means that your provided certificate
  is wrong.
</p>
<p>
  In case you encounter some other certificate or SSL related exception,
  <a href="https://developer.android.com/training/articles/security-ssl" target="_blank" rel="noopener">here </a>is
  a list of the common reasons for issues.
</p>
<p>
  In case of those issues, sometimes a good way of exploring the cause of the problem
  further is the same openssl certificate command:
</p>
<pre>openssl s_client -connect <span>try</span>.count.ly:<span>443 </span>-showcerts</pre>
<p>It's error codes can sometimes lead you to a solution.</p>
<p>
  A common issue, which can be encountered is that the server's certificate does
  not contain the full chain of trust in it and it shows only 1 entry. In such
  cases,&nbsp;<a href="https://serverfault.com/questions/875297/verify-return-code-21-unable-to-verify-the-first-certificate-lets-encrypt-apa" target="_blank" rel="noopener">this</a>&nbsp;may
  be helpful.
</p>
<h2>Using Proguard</h2>
<p>
  <span style="font-weight: 400;">Proguard obfuscates the OpenUDID &amp; Countly Messaging classes. If you use OpenUDID or Countly Messaging in your application, you will need to add the following lines to your Proguard rules file:</span>
</p>
<pre><code class="java">-keep class org.openudid.** { *; }
-keep class ly.count.android.sdk.** { *; }</code></pre>
<p>
  More info can be found
  <a href="https://developer.android.com/studio/build/shrink-code#keep-code" target="_blank" rel="noopener">here</a>.
</p>
<h2>Parameter Tampering Protection</h2>
<p>
  <span style="font-weight: 400;">You may set the optional <code>salt</code></span><span style="font-weight: 400;">&nbsp;to be used for calculating the checksum of requested data which will be sent with each request, using the <code>&amp;checksum</code></span><span style="font-weight: 400;">&nbsp;field. You will need to set exactly the same <code>salt</code></span><span style="font-weight: 400;">&nbsp;on the Countly server. If&nbsp;the <code>salt</code></span><span style="font-weight: 400;">&nbsp;on the Countly server is set, all requests would be checked for the validity of the <code>&amp;checksum</code></span><span style="font-weight: 400;">&nbsp;field before being processed.</span>
</p>
<pre><code class="java">Countly.sharedInstance().enableParameterTamperingProtection("salt");</code></pre>
<h1>Other features</h1>
<h2>Attribution analytics &amp; install campaigns</h2>
<p>
  <a href="https://support.count.ly/hc/en-us/articles/360037639271-Attribution-Analytics">Countly Attribution Analytics</a>
  allows you to measure your marketing campaign performance by attributing installs
  from specific campaigns. This feature is available for the Enterprise Edition.
</p>
<p>
  <span style="font-weight: 400;">We highly recommend allowing Countly to listen to the&nbsp;</span><strong>INSTALL_REFERRER</strong><span style="font-weight: 400;">&nbsp;intent in order to receive more precise attribution on Android, something you may do by adding the following XML code to your&nbsp;</span><strong>AndroidManifest.xml</strong><span style="font-weight: 400;">&nbsp;file inside&nbsp;the </span><strong>application</strong><span style="font-weight: 400;">&nbsp;tag.</span>
</p>
<pre><code class="xml">&lt;receiver android:name="ly.count.android.sdk.ReferrerReceiver" android:exported="true"&gt;
  &lt;intent-filter&gt;
    &lt;action android:name="com.android.vending.INSTALL_REFERRER" /&gt;
  &lt;/intent-filter&gt;
&lt;/receiver&gt;</code></pre>
<p>
  <span style="font-weight: 400;">Note that modifying&nbsp;your </span><strong>AndroidManifest.xml</strong><span style="font-weight: 400;">&nbsp;file is the only thing you would need to do in order to start receiving data from your campaigns via the Attribution Analytics plugin.</span>
</p>
<p>
  <strong><span style="font-weight: 400;">For more information about how to set up your campaigns, please&nbsp;</span><a href="https://support.count.ly/hc/en-us/articles/360037639271-Attribution-Analytics"><span style="font-weight: 400;">review this documentation</span></a><span style="font-weight: 400;">.</span></strong>
</p>
<h2>Receiving and showing badge numbers from push notifications</h2>
<p>
  <span style="font-weight: 400;">While showing badges isn't supported natively for versions before Android O, there are some devices and launchers that support it. Therefore, you may want to implement such a feature in your app. However, not all devices will support badges.</span>
</p>
<p>
  <span style="font-weight: 400;">While creating a new message in the messaging overview and preparing its content, there is an optional prompt called "Add iOS badge". You may use this prompt to also send badges to Android devices.</span>
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/5fbc4a2-Ekran_Resmi_2017-01-27_07.15.34.png">
</div>
<p>
  <span style="font-weight: 400;">In order to receive this badge number in your application, you must subscribe to the broadcasts about received messages. There you will be informed about all received push notifications using Message and the bundle. The badge number is sent with the key "badge". You may use it to extract the badge number from the bundle received and then use it to display badge numbers with your implementation of choice.</span>
</p>
<p>
  <span style="font-weight: 400;">In the example below we will use a badge library called&nbsp;</span><a href="https://github.com/leolin310148/ShortcutBadger"><span style="font-weight: 400;">ShortcutBadger</span></a><span style="font-weight: 400;">, which is used to show badges on Android. Follow their instructions&nbsp;</span><a href="https://github.com/leolin310148/ShortcutBadger#usage"><span style="font-weight: 400;">in this link</span></a><span style="font-weight: 400;">&nbsp;on how to implement it in your Android project.
</p>
<pre><code class="java">/** Register for broadcast action if you need to be notified when Countly message received */
messageReceiver = new BroadcastReceiver() {
    @Override
    public void onReceive(Context context, Intent intent) {
        Message message = intent.getParcelableExtra(CountlyMessaging.BROADCAST_RECEIVER_ACTION_MESSAGE);
        Log.i("CountlyActivity", "Got a message with data: " + message.getData());

        //Badge related things
        Bundle data = message.getData();
        String badgeString = data.getString("badge");
        try {
            int badgeCount = Integer.parseInt(badgeString);

            boolean succeded = ShortcutBadger.applyCount(getApplicationContext(), badgeCount);
            if(!succeded) {
                Toast.makeText(getApplicationContext(), "Unable to put badge", Toast.LENGTH_SHORT).show();
            }
        } catch (NumberFormatException exception) {
            Toast.makeText(getApplicationContext(), "Unable to parse given badge number", Toast.LENGTH_SHORT).show();
        }
    }
};
IntentFilter filter = new IntentFilter();
filter.addAction(CountlyMessaging.getBroadcastAction(getApplicationContext()));
registerReceiver(messageReceiver, filter);</code></pre>
<h2>Checking if init has been called</h2>
<p>
  <span style="font-weight: 400;">In case you would like to check if init has been called, you may use the following function:</span>
</p>
<pre><code class="java">Countly.sharedInstance().isInitialized();</code></pre>
<h2>Checking if onStart has been called</h2>
<p>
  <span style="font-weight: 400;">For some applications, there might a use case where the developer would like to check if the Countly SDK <code>onStart</code></span><span style="font-weight: 400;">&nbsp;function has been called. To do so, they may use the following call:</span>
</p>
<pre><code class="java">Countly.sharedInstance().hasBeenCalledOnStart();</code></pre>
<h2>Ignoring app crawlers</h2>
<p>
  <span style="font-weight: 400;">Sometimes server data might be polluted with app crawlers which are not real users, and you would like to ignore them. Starting from the 17.05 release, it's possible to ignore app crawlers by filtering on the app level. The current version does that, using device names. Internally, the Countly SDK has a list of crawler device names. If a device name matches one from that list, no information is sent to the server. </span>
</p>
<p>
  <span style="font-weight: 400;">At the moment, that list has only one entry: "Calypso AppCrawler". In the future we might add more crawler device names if such are reported. If you have encountered a crawler that is not on that list, and you would like to ignore it, you may add it to your SDK list yourself by calling <code>addAppCrawlerName</code></span><span style="font-weight: 400;">. </span>
</p>
<p>
  <span style="font-weight: 400;">Currently, the SDK ignores crawlers by default. If you would like to change this setting, use <code>ifShouldIgnoreCrawlers</code></span><span style="font-weight: 400;">. If you would like to check if the current device was detected as a crawler, use <code>isDeviceAppCrawler</code></span><span style="font-weight: 400;">. Detection is done in the init function, meaning you would have to add the crawler names before that and perform the check after.</span>
</p>
<pre><code class="java">//set that the sdk should ignore app crawlers
Countly.sharedInstance().ifShouldIgnoreCrawlers(true);

//set that the sdk should not ignore app crawlers
Countly.sharedInstance().ifShouldIgnoreCrawlers(false);

//add another app crawler device name to ignore
Countly.sharedInstance().addAppCrawlerName("App crawler");

//returns true if this device is detected as a app crawler and false otherwise
Countly.sharedInstance().isDeviceAppCrawler();f</code></pre>
<h2>Forcing HTTP POST</h2>
<p>
  <span style="font-weight: 400;">If the data sent to the server is short enough, the SDK will use HTTP GET requests. In case you would like an override so that HTTP POST is used in all cases, call the "setHttpPostForced" function after you call "init". You may use the same function later in the app’s life cycle to disable the override. This function must be called every time the app starts.</span>
</p>
<pre><code class="java">//the init call before the override
Countly.sharedInstance().init(this, "https://YOUR_SERVER", "YOUR_APP_KEY", "YOUR_DEVICE_ID")
  
//enabling the override
Countly.sharedInstance().setHttpPostForced(true);
  
//disabling the override
Countly.sharedInstance().setHttpPostForced(false);</code></pre>
<h2>Setting Custom HTTP header values</h2>
<p>
  <span style="font-weight: 400;">In case you would like to add custom header key/value pairs to each request sent to the Countly server, you may make the following call:</span>
</p>
<pre><code class="java">HashMap&lt;String, String&gt; customHeaderValues = new HashMap&lt;&gt;();
customHeaderValues.put("foo", "bar");

Countly.sharedInstance().addCustomNetworkRequestHeaders(customHeaderValues);</code></pre>
<p>
  <span style="font-weight: 400;">The provided values will override any previously stored value pairs. In case you would like to erase any previously stored pairs, provide <code>null</code>.</span>
</p>
<h2>Interacting with the internal request queue</h2>
<p>
  When recording events or activities, the requests don't always get sent immediately.
  Events get grouped together and sometimes there is no connection to the server
  and the requests can't be sent.
</p>
<p>
  There are two ways how to interact with this request queue at the moment.&nbsp;
</p>
<p>
  You can force the SDK to try to send the requests immediately:
</p>
<pre>//Doing internally stored requests<br>Countly.<span>sharedInstance</span>().doStoredRequests();</pre>
<p>
  This way the SDK will not wait for its internal triggers and it will try to empty
  the queue on demand.
</p>
<p>
  There are some circumstances where you would want to delete all stored requests.
  Then you would call:
</p>
<pre><span>//Delete all stored requests in queue<br></span>Countly.<span>sharedInstance</span>().flushRequestQueues();</pre>
<h2>Setting an event queue threshold</h2>
<p>
  Events get grouped together and are sent either every minute or after the unsent
  event count reaches a threshold. By default it is 10. If you would like to change
  this, call:
</p>
<pre>config.setEventQueueSizeToSend(<span>6</span>);</pre>
<h2>Custom Metrics</h2>
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
<pre>//provide custom metric values<br>Map&lt;String, String&gt; metricOverride = new HashMap&lt;&gt;();<br>metricOverride.put("SomeKey", "123");<br>metricOverride.put("_app_version", "custom_version-123");<br><br>setMetricOverride(metricOverride);</pre>
<h1>
  <span style="font-weight: 400;">FAQ</span>
</h1>
<h2>How can I build the the Android SDK?</h2>
<p>
  <span style="font-weight: 400;">If you need to customize our Android SDK to fit your needs, you may find it&nbsp;</span><a href="https://github.com/Countly/countly-sdk-android"><span style="font-weight: 400;">here</span></a><span style="font-weight: 400;">&nbsp;among our Countly Github repositories as an Android Studio project. Modules included in the project are:</span>
</p>
<table>
  <tbody>
    <tr>
      <th>Module Name</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>
        <code>sdk</code>
      </td>
      <td>Countly Android SDK.</td>
    </tr>
    <tr>
      <td>
        <code>app</code>
      </td>
      <td>
        Sample app to test <code>sdk</code>
      </td>
    </tr>
    <tr>
      <td>
        <code>sdk-native</code>
      </td>
      <td>
        Module needed for
        <a href="https://resources.count.ly/docs/countly-sdk-for-android#section-native-c-crash-reporting">Native C++ crash reporting</a>
      </td>
    </tr>
    <tr>
      <td>
        <code>app-native</code>
      </td>
      <td>
        Sample app to test <code>sdk-native</code>
      </td>
    </tr>
  </tbody>
</table>
<p>
  <span style="font-weight: 400;">Recently, Android Studio versions have a&nbsp;</span><a href="https://github.com/Countly/countly-sdk-android/issues/96#issuecomment-492327285"><span style="font-weight: 400;">bug</span></a><span style="font-weight: 400;"> which</span><span style="font-weight: 400;">&nbsp;you may encounter when building your project in Studio. If you see a build error such as <code>SIMPLE: Error configuring</code></span><span style="font-weight: 400;">,</span><span style="font-weight: 400;">&nbsp;please check your text view for the build Gradle output. If you see this error <code>CMake was unable to find a build program corresponding to "Ninja". CMAKE_MAKE_PROGRAM is not set</code></span><span style="font-weight: 400;">,</span><span style="font-weight: 400;">&nbsp;then you need to make <code>ninja</code></span><span style="font-weight: 400;">&nbsp;available in your&nbsp;</span><span style="font-weight: 400;">PATH</span><span style="font-weight: 400;">. If you are using <code>cmake</code></span><span style="font-weight: 400;">&nbsp;embedded in Studio, <code>ninja</code></span><span style="font-weight: 400;">&nbsp;may be found in&nbsp;the <code>&lt;sdk_location&gt;/cmake/&lt;cmake_version&gt;/bin</code></span><span style="font-weight: 400;">&nbsp;directory.</span>
</p>
<p>
  <span style="font-weight: 400;">There is a build step for the <code>sdk-native</code></span><span style="font-weight: 400;">&nbsp;module which takes place outside of Studio. You may find the related code and build scripts in <code>sdk-native/src/cpp_precompilation</code></span><span style="font-weight: 400;">. We are working on building a breakpad library with an appropriate ndk version to integrate this step into your Studio build. Meanwhile, it seems OK to use the library files in <code>sdk-native/src/main/jniLibs/</code></span><span style="font-weight: 400;">&nbsp;that are externally built.</span>
</p>
<h2>Which operating systems are supported?</h2>
<p>
  Our Android SDK should be able support Android based operating systems without
  issues. It should also work without any major issues on devices that don't have
  Google services, for example, on Huawei devices which have the HarmonyOS operating
  system.
</p>
<h2>Is it possible to use Android SDK with another crash SDK?</h2>
<p>
  It should be fine to use Countly together with another crash SDK. If you would
  like to track caught exception, you would just pass them to both SDKs. When catching
  uncaught exceptions with both, there are some uncertainties. Although in Android
  there can be only one uncaught exception handler, you can save the previous handler
  and when receiving an uncaught exception, pass it also to the saved one. We can't
  be certain how other SDKs are implemented or if the OS would give enough time
  to propagate the exception through all handlers. Therefore, if you want to use
  Countly with another crash SDK, we advise to initialize Countly as the last one.
</p>
<h2>
  How can I tell which Countly Android SDK version I am using?
</h2>
<p>
  The Countly class has a public static string called
  <code>COUNTLY_SDK_VERSION_STRING</code> that contains the current SDK version.
  You can access it by calling <code>Countly.COUNTLY_SDK_VERSION_STRING</code>.
  It would return something similar to "20.11.10".
</p>
<h2>What information is collected by the SDK</h2>
<p>
  The following description mentions data that is collected by SDK's to perform
  their functions and implement the required features. Before any of it is sent
  to the server, it is stored locally.
</p>
<p>
  * When sending any network requests to the server, the following things are sent
  in addition of the main data:<br>
  - Timestamp of when the request is creted<br>
  - Current hour<br>
  - Current day of week<br>
  - Current timezone<br>
  - SDK version<br>
  - SDK name
</p>
<p>
  * If sessions are used then it would record the session start time, end time
  and duration
</p>
<p>
  * If sessions are used then also device metrics are collected which contains:<br>
  - Device model<br>
  - Device type (phone, tablet, etc)<br>
  - Screen resolution<br>
  - Screen density<br>
  - OS name<br>
  - OS version<br>
  - App version<br>
  - Locale identifier<br>
  - Carrier name
</p>
<p>* The current device orientation</p>
<p>
  * When generating a device ID, if no custom ID is provided, the SDK will use:<br>
  - Secure.ANDROID_ID as the default ID and advertising id as a fallback devices
  ID
</p>
<p>
  * If push notification are used:<br>
  - The devices push notification token<br>
  - If the user clicks on the notification then the time of the click and on which
  button the user has clicked on&nbsp;
</p>
<p>
  * If automatic view tracking is enabled, it will collect:<br>
  - activity class name&nbsp;
</p>
<p>
  * If feedback or rating widgets are used, it will collect the users input and
  time of the widgets completion
</p>
<p>
  * When events are recorded, the time of when the event is recorded, will be collected
</p>
<p>
  * If the consent feature is used, the SDK will collect and send what consent
  has been given to the SDK or removed from the SDK
</p>
<p>
  * If crash tracking is enabled, it will collect the following information at
  the time of the crash:<br>
  - OS name<br>
  - OS version<br>
  - Device model<br>
  - Device architecture<br>
  - Device resolution<br>
  - App version<br>
  - Time of the crash<br>
  - Crash stacktrace<br>
  - Error description<br>
  - Total RAM<br>
  - Currently used RAM<br>
  - Total disk size<br>
  - Currently used disk size<br>
  - Device battery level<br>
  - Device orientation<br>
  - If there is a network connection<br>
  - If the app is in the background<br>
  - How long has the application been running<br>
  - If the device has been rooted
</p>
<p>
  Any other information like data in custom events, location, user profile information
  or other manual requests depends on what the developer decides to provide and
  is not collected by the SDK itself.
</p>