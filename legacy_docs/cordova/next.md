<p>
  This document will guide you through the process of Countly SDK installation
  and it applies to version 22.09.0<br>
  Countly is an open source SDK, you can take a look at our SDK code in the
  <a href="https://github.com/Countly/countly-sdk-cordova" target="_self" rel="undefined">Github repo</a>
</p>
<div class="callout callout--info">
  <p>
    Click
    <a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-and-Installing-SDKs#cordova-sdk" target="_self" rel="undefined">here, </a>to
    access the documentation for older SDK versions.
  </p>
</div>
<p>
  <strong>Supported Platforms:</strong> Countly SDK supports iOS and Android.
</p>
<p>
  You can take a look at our sample application in the
  <a href="https://github.com/Countly/countly-sdk-cordova-example" target="_self" rel="undefined">Github repo</a>.
  It should show how most of the functionalities can be used.
</p>
<h1 id="01GSFET8D6Y6VRS8XJZTY3NN9X">Adding the SDK to the project</h1>
<p>
  The core of this SDK is developed around Cordova. We have a minimum version requirement
  for it's core and android, ios modules that have to be satisfied:
</p>
<ul>
  <li data-list-item-id="ed4652aff93ce799d2e6797a4fffe25b7">cordova &gt;= 9.0.0</li>
  <li data-list-item-id="e3226c4e117de4dfd1d1e8085982fed60">cordova-android &gt;= 8.0.0</li>
  <li data-list-item-id="e81ffbc2a58d1894af5ace473ff3c873f">cordova-ios &gt;= 5.0.0</li>
</ul>
<p>
  If you would integrate this SDK in any other project similar to cordova (like
  ionic, phonegap, meteor), you would have to make sure that you are setting the
  platform requirements for those projects similar to these.
</p>
<p>
  <strong>Note : </strong>Development on PhoneGap stopped in 14 Aug 2020. To the
  best of our knowledge, this SDK should still be compatible with the final release.
</p>
<p>
  For more information about PhoneGap shut down,
  <a href="https://cordova.apache.org/announcements/2020/08/14/goodbye-phonegap.html#:~:text=Adobe%20recently%20announced%20that%20PhoneGap%20is%20shutting%20down." target="_self">click here</a>
</p>
<p>
  Setting up Countly SDK inside your Cordova, Ionics application is straightforward.
  Just follow the laid out steps for the specific projects:
</p>
<p>
  <span class="wysiwyg-font-size-large"><strong>Cordova</strong></span>
</p>
<p>
  Add Countly SDK in your Cordova project using following commands:<br>
  <strong>Note: </strong>use the latest SDK version currently available, not specifically
  the one shown in the sample below.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto shell">cd PATH_TO_YOUR_PROJECT

cordova plugin add https://github.com/Countly/countly-sdk-cordova.git

# OR

cordova plugin add countly-sdk-js@20.11.0</code></pre>
<p>
  If iOS/Android Platform are already added in your project, first remove them
</p>
<pre class="wysiwyg-code-block"><code class="language-auto shell">cordova platform remove android
cordova platform remove ios</code></pre>
<p>Now add platform of your choice</p>
<pre class="wysiwyg-code-block"><code class="language-auto shell">cordova platform add android
cordova platform add ios</code></pre>
<p>
  It's important that you make sure you build it with Cordova, as Cordova links
  folders very well.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto shell">cordova build android
ordova build ios</code></pre>
<p>Now run the application directly for Android,</p>
<pre class="wysiwyg-code-block"><code class="language-auto shell">cordova run android</code></pre>
<p>Or iOS:</p>
<pre class="wysiwyg-code-block"><code class="language-auto shell">cordova run ios</code></pre>
<p>
  Alternatively, you can open the source in Xcode, or Android Studio and move on
  with further development.
</p>
<p>
  <span class="wysiwyg-font-size-large"><strong>Ionic</strong></span>
</p>
<p>
  Add Countly SDK in your Ionic project using following commands:<br>
  <strong>Note: </strong>use the latest SDK version currently available, not specifically
  the one shown in the sample below.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto shell">cd PATH_TO_YOUR_PROJECT

ionic cordova plugin add https://github.com/Countly/countly-sdk-cordova.git

# OR

ionic cordova plugin add countly-sdk-js@20.11.0</code></pre>
<p>
  If iOS/Android Platform are already added in your project, first remove them
</p>
<pre class="wysiwyg-code-block"><code class="language-auto shell">ionic cordova platform remove android
ionic cordova platform remove ios</code></pre>
<p>Now add platform of your choice</p>
<pre class="wysiwyg-code-block"><code class="language-auto shell">ionic cordova platform add android
ionic cordova platform add ios</code></pre>
<p>Now prepare the platforms you have added</p>
<pre class="wysiwyg-code-block"><code class="language-auto shell">ionic cordova prepare android
ionic cordova prepare ios</code></pre>
<p>
  It's important that you make sure you build it with Cordova, as Cordova links
  folders very well.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto shell">ionic cordova build android
ionic cordova build ios</code></pre>
<p>Now run the application directly for Android,</p>
<pre class="wysiwyg-code-block"><code class="language-auto shell">ionic cordova run android</code></pre>
<p>Or iOS:</p>
<pre class="wysiwyg-code-block"><code class="language-auto shell">ionic cordova run ios</code></pre>
<p>
  Alternatively, you can open the source in Xcode, or Android Studio and move on
  with further development.
</p>
<p>In your index.html, use the following lines:</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">&lt;script type="text/javascript" src="cordova.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="Countly.js"&gt;&lt;/script&gt;</code></pre>
<h1 id="01GSFET8D6A7G6ZJJFW8SB10YH">SDK Integration</h1>
<h2 id="01GSFET8D6FYDYXGRGQFZK5Y9G">Minimal setup</h2>
<p>
  Below you can find necessary code snippets to initialize the SDK for sending
  data to Countly servers. Where possible, use your server URL instead of
  <code>try.count.ly</code> in case you have your own server.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// initialize
Countly.isInitialized().then((result) =&gt; {
            if(result  != "true") {
                Countly.init("https://try.count.ly", "YOUR_APP_KEY").then((result) =&gt; {
                    Countly.start();
                },(err) =&gt; {
                    console.error(err);
                });
            }
        },(err) =&gt; {
            console.error(err);
        });</code></pre>
<p>
  Please check
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#acquiring-your-application-key-and-server-url">here</a>
  for more information on how to acquire your application key (APP_KEY) and server
  URL.
</p>
<div class="callout callout--info">
  <p>
    If you are in doubt about the correctness of your Countly SDK integration
    you can learn about methods to verify it from
    <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#how-to-validate-your-countly-integration" target="blank">here</a>.
  </p>
</div>
<h2 id="01GSFET8D6BA6HPEP0PC2VAH81">Enable logging</h2>
<p>
  If logging is enabled then our sdk will print out debug messages about it's internal
  state and encountered problems.
</p>
<p>
  When advise doing this while implementing countly features in your application.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// example for setLoggingEnabled
Countly.setLoggingEnabled();</code></pre>
<h2 id="01GSFET8D62BTNVFR2G3AC9B7D">Device ID</h2>
<p>
  When the SDK is initialized for the first time and no device ID is provided,
  a device ID will be generated by SDK.
</p>
<p>
  For iOS: the device ID generated by SDK is the Identifier For Vendor (IDFV) For
  Android: the device ID generated by SDK is the OpenUDID.
</p>
<p>
  You may provide your own custom device ID when initializing the SDK
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.init(SERVER_URL, APP_KEY, DEVICE_ID)</code></pre>
<h2 id="01GSFET8D68JQ7J50EHP25E1PW">SDK data storage</h2>
<p>
  For iOS: SDK data is stored in Application Support Directory in file named "Countly.dat"
  For Android: SDK data is stored in SharedPreferences. A SharedPreferences object
  points to a file containing key-value pairs and provides simple methods to read
  and write them.
</p>
<h1 id="01GSFET8D6KDFHTKQ7XK021GSQ">Crash reporting</h1>
<p>
  The Countly SDK has the ability to collect
  <a href="http://resources.count.ly/docs/introduction-to-crash-reporting-and-analytics">crash reports</a>,
  which you may examine and resolve later on the server.
</p>
<h2 id="01GSFET8D6SF7T3AXB80W19MVQ">Automatic crash handling</h2>
<p>
  With this feature, the Countly SDK will generate a crash report if your application
  crashes due to an exception and send it to the Countly server for further inspection.
</p>
<p>
  If a crash report cannot be delivered to the server (e.g. no internet connection,
  unavailable server, etc.), then the SDK stores the crash report locally in order
  to try again at a later time.
</p>
<p>
  You will need to call the following method before calling <code>init</code> in
  order to activate automatic crash reporting.
</p>
<zd-html-block>
  <p>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/stacktrace.js/2.0.0/stacktrace.min.js">// <![CDATA[

// ]]></script>
  </p>
</zd-html-block>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// Using countly crash reports
Countly.enableCrashReporting();
</code></pre>
<h2 id="01GSFET8D63TGR0B7HPQAVVTES">Handled exceptions</h2>
<p>
  You might catch an exception or similar error during your app’s runtime.
</p>
<p>
  You may also log these handled exceptions to monitor how and when they are happening
  with the following command:
</p>
<p>
  You can also send a custom crash log to Countly using code below.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// Send Exception to the server
Countly.logException(["My Customized error message"], true, {"_facebook_version": "0.0.1"});
Countly.logException(stackFramesFromStackTraceJS, booleanNonFatal, segments);</code></pre>
<p>
  The method <code class="javascript">logException</code>takes a string, array
  of strings or strackframes for the stack trace, a boolean flag indicating if
  the crash is considered fatal or not, and a segments dictionary to add additional
  data to your crash report.
</p>
<p>
  Below are some examples that how to log handled/nonfatal and unhandled/fatal
  exceptions manually.
</p>
<p>
  <strong>1. Manually report handled exception</strong>
</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">// With stackframes
try {
  // your code here...
} catch (err) {
  StackTrace.fromError(err).then(function(stackframes) {
    Countly.logException(stackframes, true);
  });
}

// With error string
Countly.logException("ERROR_STRING", true);

// With array of strings
Countly.logException(["ERROR_STRING", "ERROR_STRING_2"], true);</code></pre>
<p>
  <strong>2. Manually report handled exception with segmentation</strong>
</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">// With stackframes
try {
  // your code here...
} catch (err) {
  StackTrace.fromError(err).then(function(stackframes) {
    Countly.logException(stackframes, true, {"_facebook_version": "0.0.1"});
  });
}

// With error string
Countly.logException("ERROR_STRING", true, {"\_facebook_version": "0.0.1"});

// With array of strings
Countly.logException(["ERROR_STRING", "ERROR_STRING_2"], true, {"\_facebook_version": "0.0.1"});</code></pre>
<p>
  <strong>3. Manually report fatal exception</strong>
</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">// With stackframes
try {
  // your code here...
} catch (err) {
  StackTrace.fromError(err).then(function(stackframes) {
    Countly.logException(stackframes, false);
  });
}

// With error string
Countly.logException("ERROR_STRING", false);

// With array of strings
Countly.logException(["ERROR_STRING", "ERROR_STRING_2"], false);</code></pre>
<p>
  <strong>4. Manually report fatal exception with segmentation</strong>
</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">// With stackframes
try {
  // your code here...
} catch (err) {
  StackTrace.fromError(err).then(function(stackframes) {
    Countly.logException(stackframes, false, {"_facebook_version": "0.0.1"});
  });
}

// With error string
Countly.logException("ERROR_STRING", false, {"\_facebook_version": "0.0.1"});

// With array of strings
Countly.logException(["ERROR_STRING", "ERROR_STRING_2"], false, {"\_facebook_version": "0.0.1"});</code></pre>
<h2 id="01GSFET8D6DT2G7QB7W90AR84V">Crash breadcrumbs</h2>
<p>
  Throughout your app you can leave crash breadcrumbs which would describe previous
  steps that were taken in your app before the crash. After a crash happens, they
  will be sent together with the crash report.
</p>
<p>Following the command adds crash breadcrumb:</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// Add crash breadcrumb
Countly.addCrashLog("My crash log from JavaScript");
</code></pre>
<h1 id="01GSFET8D6QR16MKKKJ0P3WN1M">Events</h1>
<p>
  An <a href="http://resources.count.ly/docs/custom-events">Event</a> is any type
  of action that you can send to a Countly instance, e.g purchase, settings changed,
  view enabled and so. This way it's possible to get much more information from
  your application compared to what is sent from SDK to Countly instance by default.
</p>
<p>
  Here are the detail about properties which we can use with event:
</p>
<ul>
  <li data-list-item-id="e709e8128f91a9f917c385bd0a97bfa9d">
    <code>key</code> identifies the event
  </li>
  <li data-list-item-id="e3188fc25718099da0edae905c1e51609">
    <code>count</code> is the number of times this event occurred
  </li>
  <li data-list-item-id="ee123d5fce8a68c297aaa888c9dd72f96">
    <code>sum</code> is an overall numerical data set tied to an event. For example,
    total amount of in-app purchase event.
  </li>
  <li data-list-item-id="ea64e5ae460b3251f7182ddd2eac64ea2">
    <code class="JavaScript">duration</code> is used to record and track the
    duration of events.
  </li>
  <li data-list-item-id="ecec63bd828b8ffe0cde06cb4292442a9">
    <code>segmentation</code> is a key-value pairs, we can use
    <code>segmentation</code> to track additional information. The only valid
    data types are: "String", "Integer", "Double" and "Boolean". All other types
    will be ignored.
  </li>
</ul>
<div class="callout callout--info">
  <p>
    <strong>Data passed should be in UTF-8</strong>
  </p>
  <p>
    All data passed to Countly server via SDK or API should be in UTF-8.
  </p>
</div>
<h2 id="01GSFET8D79VNGTWGFD9RD3ATW">Recording events</h2>
<p>
  We will be recording a <strong>purchase</strong> event. Here is a quick summary
  of what information each usage will provide us:
</p>
<ul>
  <li data-list-item-id="e880b4ed083b54d31383fed04cea58d5a">
    Usage 1: how many times <strong>purchase</strong> event occurred.
  </li>
  <li data-list-item-id="e7b471830aebe0fa62bb8520fdd3743e2">
    Usage 2: how many times <strong>purchase</strong> event occurred + the total
    amount of those purchases.
  </li>
  <li data-list-item-id="ee4bbf07f5497d5ab85356c61f5d9877f">
    Usage 3: how many times <strong>purchase</strong> event occurred + which
    countries and application versions those purchases were made from.
  </li>
  <li data-list-item-id="e705af8745af533d4e82d5d59f7a30b39">
    Usage 4: how many times <strong>purchase</strong> event occurred + the total
    amount both of which are also available segmented into countries and application
    versions.
  </li>
  <li data-list-item-id="eceff2235948e73e31a2130e250bf342d">
    Usage 5: how many times <strong>purchase</strong> event occurred + the total
    amount both of which are also available segmented into countries and application
    versions + the total duration of those events.
  </li>
</ul>
<p>
  <strong>1. Event key and count</strong>
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// example for sending basic event
var events = {"key":"Basic Event","count":1};
Countly.recordEvent(events);</code></pre>
<p>
  <strong>2. Event key, count and sum</strong>
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// example for event with sum
var events = {"key":"Event With Sum","count":1,"sum":"0.99"};
Countly.recordEvent(events);</code></pre>
<p>
  <strong>3. Event key and count with segmentation(s)</strong>
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// example for event with segment
var events = {"key":"Event With Segment","count":1};
events.segments = {"Country" : "Turkey", "Age" : "28"};
Countly.recordEvent(events);</code></pre>
<p>
  <strong>4. Event key, count and sum with segmentation(s)</strong>
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// example for event with segment and sum
var events = {"key":"Event With Segment And Sum","count":1,"sum":"0.99"};
events.segments = {"Country" : "Turkey", "Age" : "28"};
Countly.recordEvent(events);</code></pre>
<p>
  <strong>5. Event key, count, sum and duration with segmentation(s)</strong>
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">var events = {
  "key": "Event With Sum And Segment duration",
  "count": 1,
  "Sum": "0.99",
  "duration": "0"
};
events.segments = {
  "Country": "Turkey",
  "Age": "28"
};
Countly.recordEvent(events);</code></pre>
<p>
  Those are only a few examples of what you can do with events. You can extend
  those examples and use country, app_version, game_level, time_of_day and any
  other segmentation that will provide you valuable insights.
</p>
<h2 id="01GSFET8D7PKZADD05EFWY4SFN">Timed events</h2>
<p>
  It's possible to create timed events by defining a start and stop moment.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// Time Event
Countly.startEvent("Timed Event");
setTimeout(function() {
    Countly.endEvent({ "key": "Timed Event");
}, 1000);

// Time Event With Sum
Countly.startEvent("Timed Event With Sum");
setTimeout(function() {
countly.endEvent({"key": "Timed Event With Sum", "sum": "0.99"});
}, 1000);</code></pre>
<p>
  When ending an event you can also provide additional information. But in that
  case, you have to provide segmentation, count and sum. The default values for
  those are "null", 1 and 0.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">
// Time Event with segment
Countly.startEvent("Timed Event With Segment");
setTimeout(function() {
    var events = {
        "key": "Timed Event With Segment"
    };
    events.segments = {
        "Country": "Turkey",
        "Age": "28"
    };
    Countly.endEvent(events);
}, 1000)

// Time Event with Segment, sum and count
Countly.startEvent("Timed Event With Segment, Sum And Count");
setTimeout(function() {
var events = {
"key": "timedEvent",
"count": 1,
"sum": "0.99"
};
events.segments = {
"Country": "Turkey",
"Age": "28"
};
Countly.endEvent(events);
}, 1000);</code></pre>
<h1 id="01GSFET8D792PGTFWC15WG4NN9">Sessions</h1>
<h2 id="01GSFET8D7GNVQGWR1WB8REP5Q">Automatic session tracking</h2>
<p>
  To start recording an automatic session tracking you would call:
</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">Countly.start();</code></pre>
<p>
  <code class="JavaScript">Countly.start();</code> will handle the start session,
  update session and end session automatically.<br>
  This is how it works:
</p>
<ul>
  <li data-list-item-id="ebb18f71a08b57635fb50fbaa770a2f32">
    <strong>Start/Begin session Request:</strong> It is sent on
    <code class="JavaScript">Countly.start();</code> call and when the app comes
    back to the foreground from the background, and it includes basic metrics.
  </li>
  <li data-list-item-id="eda498a39f48b2d22d2e28427e41b39c3">
    <strong>Update Session Request:</strong> It automatically sends a periodical
    (60 sec by default) update session request while the app is in the foreground.
  </li>
  <li data-list-item-id="e3763dbb5cf26bbe7cc7fa62c3ca3db99">
    <strong>End Session Request:</strong> It is sent at the end of a session
    when the app goes to the background or terminates.
  </li>
</ul>
<p>
  If you want to end automatic session tracking you would call:
</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">Countly.stop();</code></pre>
<h1 id="01GSFET8D7GKZXSCA20EB3PB30">View tracking</h1>
<p>You may track custom views with the following code snippet:</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">Countly.recordView("View Name")</code></pre>
<p>
  While manually tracking views, you may add your custom segmentation to them like
  this:
</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">var viewSegmentation = { "Country": "Germany", "Age": "28" };
Countly.recordView("View Name", viewSegmentation);</code></pre>
<p>
  To review the resulting data, open the dashboard and go to
  <code class="JavaScript">Analytics &gt; Views</code>. For more information on
  how to use view tracking data to its fullest potential, click
  <a href="http://resources.count.ly/docs/view-analytics">here</a>.
</p>
<div class="img-container">
  <img src="/guide-media/01GVCTF96JGT05D6E6463GN8Q5" alt="001.png">
</div>
<h1 id="01GSFET8D706CP9G11HTC2MYHB">Device ID management</h1>
<p>
  A device ID is a unique identifier for your users. You may specify the device
  ID yourself or allow the SDK to generate it. When providing one yourself, keep
  in mind that it has to be unique for all users. Some potential sources for such
  an id could be the username, email or some other internal ID used by your other
  systems.
</p>
<h2 id="01GSFET8D7K2KD69EW8WMRPX4W">Device ID generation</h2>
<p>
  When the SDK is initialized for the first time with no device ID, then SDK will
  generate a device ID.
</p>
<p>
  Here are the underlying mechanisms used to generate that value for some platforms:
</p>
<p>
  For iOS: the device ID generated by SDK is the Identifier For Vendor (IDFV)<br>
  For Android: the device ID generated by SDK is the OpenUDID
</p>
<h2 id="01GSFET8D7579NGZY75QF3WF6Y">Changing the Device ID</h2>
<p>You may configure/change the device ID anytime using:</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">Countly.changeDeviceId(DEVICE_ID, ON_SERVER);</code></pre>
<p>
  You may either allow the device to be counted as a new device or merge existing
  data on the server. If the<code>onServer</code> bool is set to
  <code>true</code>, the old device ID on the server will be replaced with the
  new one, and data associated with the old device ID will be merged automatically.<br>
  Otherwise, if <code>onServer</code> bool is set to <code>false</code>, the device
  will be counted as a new device on the server.
</p>
<h2 id="01GSFET8D7QAMT8BMBEYQMQW6R">Temporary Device ID</h2>
<p>
  You may use a temporary device ID mode for keeping all requests on hold until
  the real device ID is set later.
</p>
<p>
  You can enable temporary device ID when initializing the SDK:
</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">Countly.init(SERVER_URL, APP_KEY, "TemporaryDeviceID")</code></pre>
<p>To enable a temporary device ID after init, you would call:</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">Countly.changeDeviceId("TemporaryDeviceID", ON_SERVER);</code></pre>
<p>
  <strong>Note:</strong> When passing <code>TemporaryDeviceID</code> for
  <code>deviceID</code> parameter, argument for <code>onServer</code>parameter
  does not matter.
</p>
<p>
  As long as the device ID value is <code>TemporaryDeviceID</code>, the SDK will
  be in temporary device ID mode and all requests will be on hold, but they will
  be persistently stored.
</p>
<p>
  When in temporary device ID mode, method calls for presenting feedback widgets
  and updating remote config will be ignored.
</p>
<p>
  Later, when the real device ID is set using
  <code>Countly.changeDeviceId(DEVICE_ID, ON_SERVER);</code> method, all requests
  which have been kept on hold until that point will start with the real device
  ID
</p>
<h2 id="01GSFET8D78513SN4GGSV9QFBV">Retrieving current device ID</h2>
<p>
  You may want to see what device id Countly is assigning for the specific device.
  For that you may use the following call:
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// get device id
Countly.getCurrentDeviceId(function(deviceId){
  console.log(deviceId);
}, function(getDeviceIDError){
  console.log(getDeviceIDError);
});</code></pre>
<h1 id="01GSFET8D7JWMNJRNXTSE2TT30">Push notifications</h1>
<h2 id="01GSFET8D7JCZ730KDFNYABJ5B">Integration</h2>
<h3 id="01GSFET8D71S56M8EGZVHGDR0M">Android setup</h3>
<p>
  Here are the steps to make push notifications work on Android:
</p>
<ol>
  <li data-list-item-id="e73f833441f1302556fe4198d808a9931">
    For FCM credentials setup please follow the instruction from this URL
    <a class="c-link" href="https://support.count.ly/hc/en-us/articles/360037754031-Android#getting-fcm-credentials" target="_blank" rel="noopener noreferrer" data-stringify-link="https://support.count.ly/hc/en-us/articles/360037754031-Android#getting-fcm-credentials" data-sk="tooltip_parent">https://support.count.ly/hc/en-us/articles/360037754031-Android#getting-fcm-credentials</a>.
  </li>
  <li data-list-item-id="e0e6a5b1b65f18ac82b716c117203a51b">
    Make sure you have <code class="JavaScript">google-services.json</code> from
    <a href="https://firebase.google.com/">https://firebase.google.com/</a>
  </li>
  <li data-list-item-id="ebf1dc84a4ff5141123b72c101c2ac376">
    Make sure the app package name and the
    <code class="JavaScript">google-services.json</code>
    <code class="JavaScript">package_name</code> matches.
  </li>
  <li data-list-item-id="eacb804787f31c9ae7c458dfa74e44267">
    Place this <code class="JavaScript">google-services.json</code> file under
    your root project folder. i.e. above www folder.
  </li>
  <li data-list-item-id="e3782232333f2a4ac741c041c421dc610">
    <p>Put these tags in config.xml file for Android:</p>
    <div class="tabs">
      <div class="tab">
        <pre class="wysiwyg-code-block"><code class="language-auto xml">&lt;platform name="android"&gt;
   &lt;resource-file src="google-services.json" target="app/google-services.json" /&gt;
&lt;/platform&gt;</code></pre>
      </div>
    </div>
  </li>
  <li data-list-item-id="e89ce161f42314468816b53a6224b8f81">
    <p>
      Put these tags in config.xml file if you are using cordova-android 9.x
      or greater:
    </p>
    <div class="tabs">
      <div class="tab">
        <pre class="wysiwyg-code-block"><code class="language-auto xml">&lt;preference name="GradlePluginGoogleServicesEnabled" value="true" /&gt;
&lt;preference name="GradlePluginGoogleServicesVersion" value="4.2.0" /&gt;</code></pre>
      </div>
    </div>
  </li>
  <li data-list-item-id="e0c2b830880bb4202a3c2c273fa8607ad">
    <p>
      Install the google services plugin if you use cordova-android below version
      9
    </p>
    <pre class="wysiwyg-code-block"><code class="language-auto shell">cordova plugin add cordova-support-google-services --save</code></pre>
  </li>
  <li data-list-item-id="e58fab92ddd81cd3a211d0701063f519d">Build your app, and test push notifications.</li>
</ol>
<h3 id="01GSFET8D8ZAHABSQPGRJRBZZT">iOS setup</h3>
<p>
  <span style="font-weight: 400;">By default push notification is enabled for iOS, to disable you need to add the </span><code><span style="font-weight: 400;">COUNTLY_EXCLUDE_PUSHNOTIFICATIONS=1</span></code><span style="font-weight: 400;">&nbsp;flag to the </span><code><span style="font-weight: 400;">Build Settings</span></code><span style="font-weight: 400;"> &gt; </span><code><span style="font-weight: 400;">Preprocessor Macros</span></code><span style="font-weight: 400;"> section in Xcode.</span><span style="font-weight: 400;"></span>
</p>
<p>
  <span style="font-weight: 400;"><img src="/hc/article_attachments/7912645823513/Screenshot_2022-06-27_at_5.35.43_PM.png" alt="Screenshot_2022-06-27_at_5.35.43_PM.png"></span>
</p>
<p>
  There are no additional steps required for iOS,everything is set up for you by
  the Countly Cordova SDK.
</p>
<h2 id="01GSFET8D8SDB5NHQ6XNY82YSN">Enabling push</h2>
<p>
  First, when setting up push for the Cordova SDK, you would first select the push
  token mode. This would allow you to choose either test or production modes, push
  token mode should be set before init.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">// Set messaging mode for push notifications
Countly.pushTokenType(Countly.messagingMode.DEVELOPMENT, "Channel Name", "Channel Description");</code></pre>
<p>
  When you are finally ready to initialise Countly push, you would call this:
</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">// This method will ask for permission, enables push notification and send push token to countly server.
Countly.askForNotificationPermission();</code></pre>
<h2 id="01GSFET8D84CWPQZT5BHF7G84R">Handling push callbacks</h2>
<p>
  To register a Push Notification callback after initializing the SDK, use the
  method below.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.registerForNotification(function(theNotification){
  console.log(JSON.stringify(theNotification));
});</code></pre>
<p>
  In order to listen to notification receive and click events, Place the below
  code in <code>AppDelegate.m</code>
</p>
<p>Add header files</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">#import "CountlyNative.h"
#import &lt;UserNotifications/UserNotifications.h&gt;
</code></pre>
<p>
  Before <code>@end</code> add these methods
</p>
<pre class="wysiwyg-code-block"><code class="language-auto JavaScript">// Required for the notification event. You must call the completion handler after handling the remote notification.
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
{
    [CountlyNative onNotification: userInfo];
    completionHandler(0);
}

// When app is killed.

- (void)userNotificationCenter:(UNUserNotificationCenter _)center didReceiveNotificationResponse:(UNNotificationResponse _)response withCompletionHandler:(void (^)(void))completionHandler{
  NSDictionary \*notification = response.notification.request.content.userInfo;
  [CountlyNative onNotification: notification];
  completionHandler();
  }

// When app is running.

- (void)userNotificationCenter:(UNUserNotificationCenter _)center willPresentNotification:(UNNotification _)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler{
[CountlyNative onNotification: notification.request.content.userInfo];
completionHandler(0);
}</code></pre>
<h3 id="01GSFET8D8E7E8QP9D72P5G1GM">Data Structure Received in Push Callbacks</h3>
<p>
  Here is the example of how data will receive in push callbacks:<img src="/guide-media/01GVDG0K4G51KAKZJZVZHNYQ4A" alt="Screenshot_2022-06-24_at_7.04.23_PM.png"><br>
  <br>
  Data Received for Android platform:
</p>
<pre class="wysiwyg-code-block"><code class="language-auto">{
"c.e.cc": "TR",
"c.e.dt": "mobile",
"Key": "value",
"c.i": "62b59b979f05a1f5e5592036",
"c.l": "https:\/\/www.google.com\/",
"c.m": "https:\/\/count.ly\/images\/logos\/countly-logo-mark.png?v2",
"c.li": "notify_icon",
"badge": "1",
"sound": "custom",
"title": "title",
"message": "Message"
}</code></pre>
<p>Data Received for iOS platform:</p>
<pre class="wysiwyg-code-block"><code class="language-auto">{
Key = value;
 aps = {
  alert = {
   body = Message;
   subtitle = subtitle;
   title = title;
  };
 badge = 1;
 "mutable-content" = 1;
 sound = custom;
 };
 c = {
  a = "https://count.ly/images/logos/countly-logo-mark.png";
   e = {
    cc = TR;
    dt = mobile;
   };
  i = 62b5b945cabedb0870e9f217;
  l = "https://www.google.com/";
 };
}</code></pre>
<h1 id="01GSFET8D8N3V7TBZQ3JQ8XWE1">User location</h1>
<p>
  While integrating this SDK into your application, you might want to track your
  user location. You could use this information to better know your apps user base
  or to send them tailored push notifications based on their coordinates. There
  are 4 fields that can be provided:
</p>
<ul>
  <li data-list-item-id="ebaea2488f045013112aa07ed00ac4b12">country code in the 2 letter iso standard</li>
  <li data-list-item-id="ef89ec7ca83f73d3fc3f3087273c1d9a4">city name (has to be set together with country code)</li>
  <li data-list-item-id="ecfa3aedfd052e3117b93d343268a2657">
    Comma separate latitude and longitude values, for example "56.42345,123.45325"
  </li>
  <li data-list-item-id="eafd0bd67c82e322559ef110b6f03e28d">ip address of your user</li>
</ul>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// send user location
Countly.setLocation("28.006324", "-82.7166183");</code></pre>
<p>
  When those values are set, they will be sent every time when initiating a session.
  If they are set after a session was initiated, a separate request will also be
  sent. Except for ip address, because Countly Server processes ip address only
  when starting a session.
</p>
<p>If you don't want to set specific fields, set them to null.</p>
<p>
  Users might want to opt out of location tracking. To do that, call:
</p>
<p>
  It will erase cached location data from the device and the server.
</p>
<h1 id="01GSFET8D8XH24EPYB9YR4M2V6">Remote Config</h1>
<p>
  Remote config allows you to modiffy how your app functions or looks by requesting
  key-value pairs from your Countly server. The returned values can be modiffied
  based on the user profile. For more details please see Remote Config documentation.
</p>
<h2 id="01GSFET8D8V5F4FEM865WZPGNC">Automatic remote config</h2>
<p>
  There are two ways of acquiring remote config data, by automatic download or
  manual request. By default, automatic remote config is disabled and therefore
  without developer intervention no remote config values will be requested.
</p>
<p>
  Automatic value download happens when the SDK is initiated or when the device
  ID is changed. To enable it, you have to call setRemoteConfigAutomaticDownload
  before init. As a optional value you can provide a callback to be informed when
  the request is finished.
</p>
<p>
  Note: call <code class="javascript">setRemoteConfigAutomaticDownload</code> method
  before init
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// Call this method before init
Countly.setRemoteConfigAutomaticDownload(function(r){
  alert(r)
}, function(r){
  alert(r);
});
</code></pre>
<p>
  If the callback returns a non null value, then you can expect that the request
  failed and no values where updated.
</p>
<p>
  When doing an automatic update, all locally stored values are replaced with the
  ones received (all locally stored ones are deleted and new ones are associated
  instead). It is possible that a previously valid key returns no value after an
  update.
</p>
<h2 id="01GSFET8D82BEJVKRQGS65PN47">Manual remote config</h2>
<p>
  There are three ways for manually requesting a Remote Config update:
</p>
<ul>
  <li data-list-item-id="e9252542022e7947553a4caba8d4526c3">Manually updating everything</li>
  <li data-list-item-id="ea34f0bd06367ad78f3c536eead1ba651">Manually updating specific keys</li>
  <li data-list-item-id="e0f6295d1c0c676b3c2bebc0c28ddcb99">Manually updating everything except specific keys</li>
</ul>
<p>
  Each of these requests also has a callback. If that returns a non-null value,
  that means the request encountered an error and failed.
</p>
<p>
  Functionally, the manual update for everything remoteConfigUpdate is the same
  as the automatic update - it replaces all stored values with the ones from the
  server (all locally stored ones are deleted and replaced with new ones instead).
  The advantage is that you can make the request whenever it is desirable for you.
  It has a callback to let you know when it has finished.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.remoteConfigUpdate(function(r){
  alert(r)
}, function(r){
  alert(r);
});</code></pre>
<p>
  You might want to update only specific key values. For that you need to call
  <code>updateRemoteConfigForKeysOnly</code> with a list of keys you want to be
  updated. That list is an array with string values of those keys. It has a callback
  to let you know when the request has finished.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.updateRemoteConfigForKeysOnly(["name"], function(r){
  alert(r)
}, function(r){
  alert(r);
});</code></pre>
<p>
  You might want to update all values except a few defined keys, for that call
  updateRemoteConfigExceptKeys. The key list is a array with string values of the
  keys. It has a callback to let you know when the request has finished.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.updateRemoteConfigExceptKeys(["url"], function(r){
  alert(r)
}, function(r){
  alert(r);
});</code></pre>
<p>
  When making requests with a "inclusion" or "exclusion" array, if those arrays
  ar empty or null, they will function the same as a simple manual request and
  will update all values. This means that it will also erase all keys not returned
  by the server.
</p>
<h2 id="01GSFET8D86YE0QFXZP90YY6PZ">Getting Remote Config values</h2>
<p>
  To request a stored value, call <code>getRemoteConfigValueForKey</code> with
  the specified key. If it returns null then no value was found. The SDK has no
  knowledge of the returned value type and therefore returns an object. The developer
  needs to cast it to the appropriate type. The returned values can also be a JSONArray,
  JSONObject or just a simple value like int.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.getRemoteConfigValueForKey("name", function(r){
   alert(r)
 }, function(r){
   alert(r);
 });</code></pre>
<h2 id="01GSFET8D8PEH7J89PPDTRQFGE">Clearing stored values</h2>
<p>
  At some point you might want to erase all values downloaded from the server.
  To achieve that you need to call one function, depicted below:
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.remoteConfigClearValues(function(r){
  alert(r)
}, function(r){
  alert(r);
});</code></pre>
<h1 id="01GSFET8D8W93W3PTRRPQBC161">User Feedback</h1>
<p>
  There are two ways of getting feedback from your users: Star rating dialog, feedback
  widget.
</p>
<p>
  Star rating dialog allows users to give feedback as a rating from 1 to 5. The
  feedback widget allows to get the same 1 to 5 rating and also a text comment.
</p>
<h2 id="01GSFET8D849MFHGEVYMMS1KRH">Ratings</h2>
<h3 id="01GSFET8D8JFWX4ZTDQ8816N2X">Star Rating Dialog</h3>
<p>
  Star rating integration provides a dialog for getting user's feedback about the
  application. It contains a title, simple message explaining what it is for, a
  1-to-5 star meter for getting users rating and a dismiss button in case the user
  does not want to give a rating.
</p>
<p>
  This star-rating has nothing to do with Google Play Store ratings and reviews.
  It is just for getting a brief feedback from users, to be displayed on the Countly
  dashboard. If the user dismisses star rating dialog without giving a rating,
  the event will not be recorded.
</p>
<p>
  Star-rating dialog's title, message and dismiss button text can be customized
  either through the init function or the <code>SetStarRatingDialogTexts</code>
  function. If you don't want to override one of those values, set it to "null".
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// Star Rating
countly.askForStarRating(Function(ratingResult){
  console.log(ratingResult);
});</code></pre>
<div></div>
<h3 id="01GSFET8D9Y9557G5HWVM4D1YR">Rating Widget</h3>
<p>
  Feedback widget shows a server configured widget to your user devices.
</p>
<p>
  <img src="/guide-media/01GVDG0PGJZ4H1QYYCE4KWEP9B" alt="002.png">
</p>
<p>
  It's possible to configure any of the shown text fields and replace with a custom
  string of your choice.
</p>
<p>
  In addition to a 1 to 5 rating, it is possible for users to leave a text comment
  and also leave a email in case the user would want some contact from the app
  developer.
</p>
<p>
  Trying to show the rating widget is a single call, but underneath is a two step
  process. Before it is shown, the SDK tries to contact the server to get more
  information about the dialog. Therefore a network connection to it is needed.
</p>
<p>
  You can try to show the widget after you have initialized the SDK. To do that,
  you first have to get the widget ID from your server:
</p>
<p>
  <img src="/guide-media/01GVBACJ8ZQBWG1KH1CB53T6K1" alt="003.png">
</p>
<p>
  Using that you can call the function to show the widget popup:
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// Feedback Modal
countly.askForFeedback("5e425407975d006a22535fc", "close");</code></pre>
<h1 id="01GSFET8D9VPPA9R4997GH6C7G">User Profiles</h1>
<p>
  Available with Enterprise Edition, User Profiles is a tool which helps you identify
  users, their devices, event timeline and application crash information. User
  Profiles can contain any information that either you collect, or is collected
  automatically by Countly SDK.
</p>
<p>
  You can send user related information to Countly and let Countly dashboard show
  and segment this data. You may also send a notification to a group of users.
  For more information about User Profiles, see this documentation.
</p>
<p>
  To provide information about the current user, you must call the Countly.userData.setUserData
  function. You can call it by providing a bundle of only the predefined fields
  or call it while also providing a second bundle of fields with your custom keys.
  After you have provided user profile information, you must save it by calling
  Countly.userData.save().
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">/ example for setting user data
var options = {};
options.name = "Nicola Tesla";
options.username = "nicola";
options.email = "info@nicola.tesla";
options.organization = "Trust Electric Ltd";
options.phone = "+90 822 140 2546";
options.picture = "http://www.trust.electric/images/people/nicola.png";
options.picturePath = "";
options.gender = "Male";
options.byear = 1919;
Countly.setUserData(options);</code></pre>
<p>The keys for predefined user data fields are as follows:</p>
<figure class="wysiwyg-table wysiwyg-table-align-left">
  <table>
    <thead>
      <tr>
        <th style="text-align: center;">Key</th>
        <th style="text-align: center;">Type</th>
        <th style="text-align: center;">Description</th>
      </tr>
    </thead>
    <tbody>
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
        <td>User's organisation name</td>
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
</figure>
<p>
  Using "" for strings or a negative number for 'byear' will effectively delete
  that property.
</p>
<p>
  For custom user properties you may use any key values to be stored and displayed
  on your Countly backend. Note: keys with . or $ symbols will have those symbols
  removed.
</p>
<h2 id="01GSFET8D9YH6RBE6EX5AWT3KD">Setting custom values</h2>
<p>
  Additionally you can do different manipulations on your custom data values, like
  increment current value on server or store a array of values under the same property.
</p>
<p>Below is the list of available methods:</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// example for extra user features

Countly.userData.setProperty("setProperty", "My Property");
Countly.userData.increment("increment");
Countly.userData.incrementBy("incrementBy", 10);
Countly.userData.multiply("multiply", 20);
Countly.userData.saveMax("saveMax", 100);
Countly.userData.saveMin("saveMin", 50);
Countly.userData.setOnce("setOnce", 200);
Countly.userData.pushUniqueValue("pushUniqueValue","morning");
Countly.userData.pushValue("pushValue", "morning");
Countly.userData.pullValue("pullValue", "morning");</code></pre>
<p>
  In the end always call Countly.userData.save() to send them to the server.
</p>
<h1 id="01GSFET8D96TW3F9X5T8M2CMSR">Application Performance Monitoring</h1>
<p>
  Performance Monitoring feature allows you to analyze your application's performance
  on various aspects. For more details please see
  <a href="https://support.count.ly/hc/en-us/articles/900000819806-Performance-monitoring" target="_self">Performance Monitoring documentation</a>.
</p>
<p>
  Here is how you can utilize Performance Monitoring feature in your apps:
</p>
<p>First, you need to enable Performance Monitoring feature::</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.enableApm(); 
// Enable APM features.</code></pre>
<p>
  With this, Countly SDK will start measuring some performance traces automatically.
  Those include app foreground time, app background time. Additionally, custom
  traces and network traces can be manually recorded.
</p>
<h2 id="01GSFET8D9EF15EYJJS21JP3CB">App Start Time</h2>
<p>
  For the app start time to be recorded, you need to call the
  <code>appLoadingFinished</code> method. Make sure this method is called after
  <code>init</code>.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// Example of appLoadingFinished
Countly.init("https://try.count.ly", "YOUR_APP_KEY").then((result) =&gt; {
  Countly.appLoadingFinished();
},(err) =&gt; {
  onsole.error(err);
});</code></pre>
<p>
  This calculates and records the app launch time for performance monitoring. It
  should be called when the app is loaded and it successfully displayed its first
  user-facing view. E.g. <code>onDeviceReady:</code> method or wherever is suitable
  for the app's flow. The time passed since the app has started to launch will
  be automatically calculated and recorded for performance monitoring. Note that
  the app launch time can be recorded only once per app launch. So, the second
  and following calls to this method will be ignored.
</p>
<h2 id="01GSFET8D92BTY293ZFQFZFVZ9">Custom traces</h2>
<p>
  You may also measure any operation you want and record it using custom traces.
  First, you need to start a trace by using the
  <code class="objectivec">startTrace(traceKey)</code> method:
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.startTrace(traceKey);</code></pre>
<p>
  Then you may end it using the
  <code class="objectivec">endTrace(traceKey, customMetric)</code>method, optionally
  passing any metrics as key-value pairs:
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">String traceKey = "Trace Key"
;
Map&lt;String, int&gt; customMetric = {
  "ABC": 1233,
  "C44C": 1337
};
Countly.endTrace(traceKey, customMetric);</code></pre>
<p>
  The duration of the custom trace will be automatically calculated on ending.
  Trace names should be non-zero length valid strings. Trying to start a custom
  trace with the already started name will have no effect. Trying to end a custom
  trace with already ended (or not yet started) name will have no effect.
</p>
<p>
  You may also cancel any custom trace you started, using
  <code class="objectivec">cancelTrace(traceKey)</code>method:
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.cancelTrace(traceKey);</code></pre>
<p>
  Additionally, if you need you may cancel all custom traces you started, using
  <code class="objectivec">clearAllTraces()</code>method:
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.clearAllTraces(traceKey);</code></pre>
<h2 id="01GSFET8D9HYEZZ8E2Z9SSQ902">Network traces</h2>
<p>
  You may record manual network traces using the<code>ecordNetworkTrace(networkTraceKey, responseCode, requestPayloadSize, responsePayloadSize, startTime, endTime)</code>
  method.
</p>
<p>
  A network trace is a collection of measured information about a network request.
  When a network request is completed, a network trace can be recorded manually
  to be analyzed in the Performance Monitoring feature later with the following
  parameters:
</p>
<p>
  - <code>networkTraceKey</code>: A non-zero length valid string -
  <code>responseCode</code>: HTTP status code of the received response -
  <code>requestPayloadSize</code>: Size of the request's payload in bytes -
  <code>responsePayloadSize</code>: Size of the received response's payload in
  bytes - <code>startTime</code>: UNIX time stamp in milliseconds for the starting
  time of the request - <code>endTime</code>: UNIX time stamp in milliseconds for
  the ending time of the request
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.recordNetworkTrace(networkTraceKey, responseCode, requestPayloadSize, responsePayloadSize, startTime, endTime);</code></pre>
<div></div>
<h1 id="01GSFET8D96EJ30EQTZN00M5GZ">User Consent</h1>
<p>
  To be compliant with GDPR, starting from 18.04, Countly provides ways to toggle
  different Countly features on/off depending on the given consent.
</p>
<p>More information about GDPR can be found here.</p>
<p>
  By default the requirement for consent is disabled. To enable it, you have to
  call setRequiresConsent with true, before initializing Countly.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.setRequiresConsent(true);</code></pre>
<p>
  By default no consent is given. That means that if no consent is enabled, Countly
  will not work and no network requests, related to features, will be sent. When
  consent status of a feature is changed, that change will be sent to the Countly
  server.
</p>
<p>
  For all features, except push, consent is not persistent and will have to be
  set every time before countly init. Therefore the storage and persistance of
  given consent falls on the sdk integrator.
</p>
<p>
  Consent for features can be given and revoked at any time, but if it is given
  after Countly init, some features might work partially.
</p>
<p>
  If consent is removed, but the appropriate function can't be called before the
  app closes, it should be done at next app start so that any relevant server side
  features could be disabled (like reverse geo ip for location)
</p>
<p>
  Feature names in the Android SDK are stored as static fields in the class called
  CountlyFeatureNames.
</p>
<p>The current features are:</p>
<ul>
  <li data-list-item-id="e183df093f3ecea59d8007b50599526b4">
    sessions - tracking when, how often and how long users use your app
  </li>
  <li data-list-item-id="e990a321868f42dca38fdf8c8fb9c9204">events - allow sending events to server</li>
  <li data-list-item-id="ec52883a9990a2daf320cd90eee410f4a">views - allow tracking which views user visits</li>
  <li data-list-item-id="eb0a6e083412a25756f27821469ab914b">location - allow sending location information</li>
  <li data-list-item-id="e56a39d437dae910e7e4e2756cea5c7d6">crashes - allow tracking crashes, exceptions and errors</li>
  <li data-list-item-id="ea3d81f0e5ae4dd660b494d3473b0b701">
    attribution - allow tracking from which campaign did user come
  </li>
  <li data-list-item-id="ec3561fe8515d9a540eb22641aaa6aed9">
    users - allow collecting/providing user information, including custom properties
  </li>
  <li data-list-item-id="e32d1b9bc33c87058c0e0fdb0ff763420">push - allow push notifications</li>
  <li data-list-item-id="e2875d9e9ca318f223ca281b2294e8836">starRating - allow to send their rating and feedback</li>
  <li data-list-item-id="eee162bc248e40150e45d19c46b31e193">apm - allow application performance monitoring</li>
  <li data-list-item-id="e7361d791000587316a958fc7a8afa3b9">
    remote-config - allows downloading remote config values from your server
  </li>
</ul>
<h2 id="01GSFET8D9XJ9CP4ESM6PGV0JA">Changing consent</h2>
<p>There are 3 ways of changing feature consent:</p>
<ul>
  <li data-list-item-id="ed9bab579244303add9ac63c35d094013">
    giveConsentInit - To add consent for a single feature (string parameter)
    or a subset of features (array of strings parameter). Use this method for
    giving consent before initializing.
  </li>
</ul>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">//giveConsent
Countly.giveConsentInit(["events", "views", "star-rating", "crashes"]);

// removeConsent
Countly.removeConsent(["events", "views", "star-rating", "crashes"]);</code></pre>
<ul>
  <li data-list-item-id="e40c26e5764e2d5f2a230d4be2c024f78">
    giveConsent/removeConsent - gives or removes consent to a specific feature
  </li>
</ul>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">//giveConsent
Countly.giveConsent(["events", "views", "star-rating", "crashes"]);

// removeConsent
Countly.removeConsent(["events", "views", "star-rating", "crashes"]);</code></pre>
<ul>
  <li data-list-item-id="e5e7f16d7152a3a0a1e72df3fb5fd4bf9">
    giveAllConsent/removeAllConsent - giveAll or removeAll consent to a specific
    feature
  </li>
</ul>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">//giveAllConsent
Countly.giveAllConsent();

//removeAllConsent
Countly.removeAllConsent();
</code></pre>
<div></div>
<h1 id="01GSFET8DAKHSBT54BXGNJH3AW">Security and privacy</h1>
<h2 id="01GSFET8DA1TZEZ3PEMEJKEXKN">Parameter Tampering Protection</h2>
<p>
  You can set optional salt to be used for calculating checksum of request data,
  which will be sent with each request using &amp;checksum field. You need to set
  exactly the same salt on Countly server. If salt on Countly server is set, all
  requests would be checked for validity of &amp;checksum field before being processed.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">// sending data with salt
Countly.enableParameterTamperingProtection("salt");</code></pre>
<h2 id="01GSFET8DAC3BFKR0PE19GHGPP">Using Proguard</h2>
<p>
  If you are using Countly Messaging in your Android application, it is recommended
  to obfuscate the Countly Messaging classes using Proguard. To do so, please follow
  the instructions below:
</p>
<ol>
  <li data-list-item-id="e6ada9de0c7194470b95c378b4676c211">
    Locate the app/proguard-rules.pro file within the /android/app/ folder.
  </li>
  <li data-list-item-id="e143f5a98365349104553c4b1efcbdf91">Add the following lines to the file:</li>
</ol>
<pre class="wysiwyg-code-block"><code class="language-auto Kotlin">-keep class ly.count.android.sdk.** { *; }
</code></pre>
<ol start="3">
  <li data-list-item-id="efa9ddbf54d99e7e37c2372bdd8d78ea9">
    If Proguard is not yet configured, you must first enable shrinking and obfuscation
    in the build file. To do so, locate the build.gradle file within the /android/app/
    folder.
  </li>
  <li data-list-item-id="ee07f29c48a2d73bee1d96b79543e9e68">Add the following lines in bold to the build.gradle file:</li>
</ol>
<pre class="wysiwyg-code-block"><code class="language-auto">...

buildTypes {
        release { // Enables code shrinking, obfuscation, and optimization for only your project's release build type.
            ...
            minifyEnabled true
            shrinkResources true
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
...</code></pre>
<p>
  By following these steps, the Countly Messaging classes will be obfuscated using
  Proguard and your application will be better protected against reverse engineering.
</p>
<h1 id="01GSFET8DA7HG9EFVGH6TB8P41">Other features</h1>
<h2 id="01GSFET8DAP2N73W03JY5PKS8N">Forcing HTTP POST</h2>
<p>
  If the data sent to the server is short enough, the sdk will use HTTP GET requests.
  In case you want an override so that HTTP POST is used in all cases, call the
  "setHttpPostForced" function after you called "init". You can use the same function
  to later in the apps life cycle disable the override. This function has to be
  called every time the app starts.
</p>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">Countly.setHttpPostForced(true); // default is false
</code></pre>
<h2 id="01GSFET8DABK6ZFWAK5GHC6P9Q">Optional parameters during initialization</h2>
<p>
  You can provide optional parameters that will be used during begin_session request.
  They must be set right after the <code>init</code> function so that they are
  set before the request is sent to the server. To set them, use the
  <code>setOptionalParametersForInitialization</code> function. If you want to
  set those optional parameters, this function has to be called every time the
  app starts. If you don't to set one off those values, leave that field
  <code>null</code>.
</p>
<p>The optional parameters are:</p>
<ul>
  <li data-list-item-id="e5581c43ca9ed8befa56d7bef3904baa9">Country code: ISO Country code for the user's country</li>
  <li data-list-item-id="e9b5fdf7d3290efc9c7e306ed6235a79f">City: Name of the user's city</li>
  <li data-list-item-id="e2964d37ce3c96f6ed583ed4d6b4f5b42">
    Location: Comma separate latitude and longitude values, for example "56.42345,123.45325"
  </li>
</ul>
<pre class="wysiwyg-code-block"><code class="language-auto javascript">
//setting optional parameters
Countly.setOptionalParametersForInitialization({
    city: "Tampa",
    country: "US",
    latitude: "28.006324",
    longitude: "-82.7166183",
    ipAddress: "255.255.255.255"
});

//and then call the below code
Countly.init(this, "https://YOUR_SERVER", "YOUR_APP_KEY", "YOUR_DEVICE_ID")</code></pre>