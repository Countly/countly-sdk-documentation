<p>
  This document will guide you through the process of Countly SDK installation
  and it applies to version 20.11.<br>Countly is an open source SDK, you can take a look at our SDK code in the <a href="https://github.com/Countly/countly-sdk-flutter-bridge" target="_self" rel="undefined">Github repo</a>
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <span class="wysiwyg-font-size-large"><strong>Older documentation</strong></span>
  </p>
  <p>
    To access the documentation for version 19.9.3 and older, click
    <a href="/hc/en-us/articles/900004883663" target="_self" rel="undefined">here.</a>
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
<h1>Adding the SDK to the project</h1>
<p>
  The core of this SDK is developed around Cordova. We have a minimum version requirement
  for it's core and android, ios modules that have to be satisfied:
</p>
<ul>
  <li>cordova &gt;= 9.0.0</li>
  <li>cordova-android &gt;= 8.0.0</li>
  <li>cordova-ios &gt;= 5.0.0</li>
</ul>
<p>
  If you would integrate this SDK in any other project similar to cordova (like
  ionic, phonegap, meteor), you would have to make sure that you are setting the
  platform requirements for those projects similar to these.
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
<pre><code class="shell">cd PATH_TO_YOUR_PROJECT

cordova plugin add https://github.com/Countly/countly-sdk-cordova.git
# OR
cordova plugin add countly-sdk-js@20.11.0</code></pre>
<p>
  If iOS/Android Platform are already added in your project, first remove them
</p>
<pre><code class="shell">cordova platform remove android
cordova platform remove ios</code></pre>
<p>Now add platform of your choice</p>
<pre><code class="shell">cordova platform add android
cordova platform add ios</code></pre>
<p>
  It's important that you make sure you build it with Cordova, as Cordova links
  folders very well.
</p>
<pre><code class="shell">cordova build android
ordova build ios</code></pre>
<p>Now run the application directly for Android,</p>
<pre><code class="shell">cordova run android</code></pre>
<p>Or iOS:</p>
<pre><code class="shell">cordova run ios</code></pre>
<p>
  Alternatively, you can open the source in Xcode, or Android Studio and move on
  with further development.
</p>
<p>
  <strong><span class="wysiwyg-font-size-large">Ionic</span></strong>
</p>
<p>
  Add Countly SDK in your Ionic project using following commands:<br>
  <strong>Note: </strong>use the latest SDK version currently available, not specifically
  the one shown in the sample below.
</p>
<pre><code class="shell">cd PATH_TO_YOUR_PROJECT

ionic cordova plugin add https://github.com/Countly/countly-sdk-cordova.git
# OR
ionic cordova plugin add countly-sdk-js@20.11.0</code></pre>
<p>
  If iOS/Android Platform are already added in your project, first remove them
</p>
<pre><code class="shell">ionic cordova platform remove android
ionic cordova platform remove ios</code></pre>
<p>Now add platform of your choice</p>
<pre><code class="shell">ionic cordova platform add android
ionic cordova platform add ios</code></pre>
<p>Now prepare the platforms you have added</p>
<pre><code class="shell">ionic cordova prepare android
ionic cordova prepare ios</code></pre>
<p>
  It's important that you make sure you build it with Cordova, as Cordova links
  folders very well.
</p>
<pre><code class="shell">ionic cordova build android
ionic cordova build ios</code></pre>
<p>Now run the application directly for Android,</p>
<pre><code class="shell">ionic cordova run android</code></pre>
<p>Or iOS:</p>
<pre><code class="shell">ionic cordova run ios</code></pre>
<p>
  Alternatively, you can open the source in Xcode, or Android Studio and move on
  with further development.
</p>
<p>In your index.html, use the following lines:</p>
<pre><code class="javascript">&lt;script type="text/javascript" src="cordova.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="Countly.js"&gt;&lt;/script&gt;</code></pre>
<h1>SDK Integration</h1>
<h2>
  Minimal setup
</h2>
<p>
  Below you can find necessary code snippets to initialize the SDK for sending
  data to Countly servers. Where possible, use your server URL instead of
  <code>try.count.ly</code> in case you have your own server.
</p>
<pre><code class="javascript">// initialize
Countly.isInitialized().then((result) =&gt; {
            if(result  != "true") {
                Countly.init("https://try.count.ly", "YOUR_API_KEY").then((result) =&gt; {
                    Countly.start();
                },(err) =&gt; {
                    console.error(err);
                });
            }
        },(err) =&gt; {
            console.error(err);
        });</code></pre>
<p>
  <span class="wysiwyg-font-size-large"><strong>Providing the application key</strong></span>
</p>
<p>
  Also called "appKey" as shorthand. The application key is used to identify for
  which application this information is tracked. You receive this value by creating
  a new application in your Countly dashboard and accessing it in its application
  management screen.
</p>
<p>
  <strong>Note: </strong>Ensure you are using the App Key (found under Management
  -&gt; Applications) and not the API Key. Entering the API Key will not work.
</p>
<p>
  <strong><span class="wysiwyg-font-size-large">Providing the server URL</span></strong>
</p>
<p>
  If you are using Countly Enterprise Edition trial servers, use
  <code>https://try.count.ly</code>, <code>https://us-try.count.ly</code> or
  <code>https://asia-try.count.ly</code> It is basically the domain from which
  you are accessing your trial dashboard.
</p>
<p>
  If you use both Community Edition and Enterprise Edition, use your own domain
  name or IP address, such as
  <a href="https://example.com/">https://example.com</a> or
  <a href="https://ip/">https://IP</a> (if SSL has been set up).
</p>
<h2>Enable logging</h2>
<p>
  If logging is enabled then our sdk will print out debug messages about it's internal
  state and encountered problems.
</p>
<p>
  When advise doing this while implementing countly features in your application.
</p>
<pre><code class="javascript">// example for setLoggingEnabled
Countly.setLoggingEnabled();</code></pre>
<h2>Device ID</h2>
<p>
  When the SDK is initialized for the first time and no device ID is provided,
  a device ID will be generated by SDK.
</p>
<p>
  For iOS: the device ID generated by SDK is the Identifier For Vendor (IDFV) For
  Android: the device ID generated by SDK is the OpenUDID or Google Advertising
  ID
</p>
<p>
  You may provide your own custom device ID when initializing the SDK
</p>
<pre><code class="javascript">Countly.init(SERVER_URL, APP_KEY, DEVICE_ID)</code></pre>
<h2>SDK data storage</h2>
<p>
  For iOS: SDK data is stored in Application Support Directory in file named "Countly.dat"
  For Android: SDK data is stored in SharedPreferences. A SharedPreferences object
  points to a file containing key-value pairs and provides simple methods to read
  and write them.
</p>
<h1>Crash reporting</h1>
<p>
  The Countly SDK has the ability to collect
  <a href="http://resources.count.ly/docs/introduction-to-crash-reporting-and-analytics">crash reports</a>,
  which you may examine and resolve later on the server.
</p>
<h2>Automatic crash handling</h2>
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
<p>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/stacktrace.js/2.0.0/stacktrace.min.js">// <![CDATA[

// ]]></script>
</p>
<pre><code class="javascript">// Using countly crash reports
Countly.enableCrashReporting();
</code></pre>
<h2>Handled exceptions</h2>
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
<pre><code class="javascript">// Send Exception to the server
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
<pre><code class="JavaScript">// With stackframes
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
<pre><code class="JavaScript">// With stackframes
try {
  // your code here...
} catch (err) {
  StackTrace.fromError(err).then(function(stackframes) {
    Countly.logException(stackframes, true, {"_facebook_version": "0.0.1"});
  });
}

// With error string 
Countly.logException("ERROR_STRING", true, {"_facebook_version": "0.0.1"});

// With array of strings 
Countly.logException(["ERROR_STRING", "ERROR_STRING_2"], true, {"_facebook_version": "0.0.1"});</code></pre>
<p>
  <strong>3. Manually report fatal exception</strong>
</p>
<pre><code class="JavaScript">// With stackframes
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
<pre><code class="JavaScript">// With stackframes
try {
  // your code here...
} catch (err) {
  StackTrace.fromError(err).then(function(stackframes) {
    Countly.logException(stackframes, false, {"_facebook_version": "0.0.1"});
  });
}

// With error string 
Countly.logException("ERROR_STRING", false, {"_facebook_version": "0.0.1"});

// With array of strings 
Countly.logException(["ERROR_STRING", "ERROR_STRING_2"], false, {"_facebook_version": "0.0.1"});</code></pre>
<h2>Crash breadcrumbs</h2>
<p>
  Throughout your app you can leave crash breadcrumbs which would describe previous
  steps that were taken in your app before the crash. After a crash happens, they
  will be sent together with the crash report.
</p>
<p>Following the command adds crash breadcrumb:</p>
<pre><code class="javascript">// Add crash breadcrumb
Countly.addCrashLog("My crash log from JavaScript");
</code></pre>
<h1>Events</h1>
<p>
  A <a href="http://resources.count.ly/docs/custom-events">custom event</a> is
  any type of action that you can send to a Countly instance, e.g purchase, settings
  changed, view enabled and so. This way it's possible to get much more information
  from your application compared to what is sent from SDK to Countly instance by
  default.
</p>
<p>
  Here are the detail about properties which we can use with event:
</p>
<ul>
  <li>
    <code>key</code> identifies the event
  </li>
  <li>
    <code>count</code> is the number of times this event occurred
  </li>
  <li>
    <code>sum</code> is an overall numerical data set tied to an event. For example, total amount of in-app purchase event.
  </li>
  <li>
    <code class="JavaScript">duration</code> is used to record and track the
    duration of events.
  </li>
  <li>
    <code>segmentation</code> is a key-value pairs, we can use <code>segmentation</code> to track additional information.
  </li>
</ul>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Data passed should be in UTF-8</span></strong>
  </p>
  <p>
    All data passed to Countly server via SDK or API should be in UTF-8.
  </p>
</div>
<h2>Recording events</h2>
<p>
  We will be recording a <strong>purchase</strong> event. Here is a quick summary
  of what information each usage will provide us:
</p>
<ul>
  <li>
    Usage 1: how many times <strong>purchase</strong> event occured.
  </li>
  <li>
    Usage 2: how many times <strong>purchase</strong> event occured + the total
    amount of those purchases.
  </li>
  <li>
    Usage 3: how many times <strong>purchase</strong> event occured + which countries
    and application versions those purchases were made from.
  </li>
  <li>
    Usage 4: how many times <strong>purchase</strong> event occured + the total
    amount both of which are also available segmented into countries and application
    versions.
  </li>
  <li>
    Usage 5: how many times <strong>purchase</strong> event occured + the total
    amount both of which are also available segmented into countries and application
    versions + the total duration of those events.
  </li>
</ul>
<p>
  <strong>1. Event key and count</strong>
</p>
<pre><code class="javascript">// example for sending basic custom event
var events = {"key":"Basic Event","count":1};
Countly.recordEvent(events);</code></pre>
<p>
  <strong>2. Event key, count and sum</strong>
</p>
<pre><code class="javascript">// example for event with sum
var events = {"key":"Event With Sum","count":1,"sum":"0.99"};
Countly.recordEvent(events);</code></pre>
<p>
  <strong>3. Event key and count with segmentation(s)</strong>
</p>
<pre><code class="javascript">// example for event with segment
var events = {"key":"Event With Segment","count":1};
events.segments = {"Country" : "Turkey", "Age" : "28"};
Countly.recordEvent(events);</code></pre>
<p>
  <strong>4. Event key, count and sum with segmentation(s)</strong>
</p>
<pre><code class="javascript">// example for event with segment and sum
var events = {"key":"Event With Segment And Sum","count":1,"sum":"0.99"};
events.segments = {"Country" : "Turkey", "Age" : "28"};
Countly.recordEvent(events);</code></pre>
<p>
  <strong>5. Event key, count, sum and duration with segmentation(s)</strong>
</p>
<pre><code class="javascript">var events = {
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
  Those are only a few examples with what you can do with custom events. You can
  extend those examples and use country, app_version, game_level, time_of_day and
  any other segmentation that will provide you valuable insights.
</p>
<h2>Timed events</h2>
<p>
  It's possible to create to create timed events by defining a start and stop moment.
</p>
<pre><code class="javascript">// Time Event
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
  When ending a event you can also provide additional information. But in that
  case you have to provide segmentation, count and sum. The default values for
  those are "null", 1 and 0.
</p>
<pre><code class="javascript">
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

// Time  Event with Segment, sum and count
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
},  1000);</code></pre>
<h1>View tracking</h1>
<p>
  You can manually add your own views in your application, and each view will be
  visible under Analytics &gt; Views. Below you can see two examples of sending
  a view using <code>Countly.recordview</code> function.
</p>
<pre><code class="javascript">// record a view on your application
Countly.recordView("My Home Page");
Countly.recordView("Profile Page");
</code></pre>
<h1>Device ID management</h1>
<p>
  When the SDK is initialized the first time and no custom device ID is provided,
  a random one will be generated. For most use cases that is enough as it provides
  a random identity to one of your apps users.
</p>
<p>
  For iOS: the device ID generated by the SDK is the Identifier For Vendor (IDFV).
  For Android: the device ID generated by the SDK is the OpenUDID or Google Advertising
  ID.
</p>
<p>
  To solve other potential use cases, we provide 3 ways to handle your device id:
</p>
<ul>
  <li>Changing device ID with merge</li>
  <li>Changing device ID without merge</li>
  <li>Using a temporary ID</li>
</ul>
<h2>Changing the Device ID</h2>
<p>You may configure/change the device ID anytime using:</p>
<pre><code class="javascript">Countly.changeDeviceId(DEVICE_ID, ON_SERVER);</code></pre>
<p>
  You may either allow the device to be counted as a new device or merge existing
  data on the server. If the<code>onServer</code> bool is set to
  <code>true</code>, the old device ID on the server will be replaced with the
  new one, and data associated with the old device ID will be merged automatically.
  Otherwise, if <code>onServer</code> bool is set to <code>false</code>, the device
  will be counted as a new device on the server.
</p>
<h2>Temporary Device ID</h2>
<p>
  You may use a temporary device ID mode for keeping all requests on hold until
  the real device ID is set later.
</p>
<p>
  You can enable temporary device ID when initializing the SDK:
</p>
<pre><code class="javascript">Countly.init(SERVER_URL, APP_KEY, "TemporaryDeviceID")</code></pre>
<p>To enable a temporary device ID after init, you would call:</p>
<pre><code class="javascript">Countly.changeDeviceId(Countly."TemporaryDeviceID", ON_SERVER);</code></pre>
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
<h2>Retrieving current device ID</h2>
<p>
  You may want to see what device id Countly is assigning for the specific device
  and what the source of that id is. For that you may use the following calls.
  The id type is an enum with the possible values of: "DEVELOPER_SUPPLIED", "OPEN_UDID",
  "ADVERTISING_ID".
</p>
<pre><code class="javascript">// get device id
Countly.getDeviceID(function(deviceId){
  console.log(deviceId);
}, function(getDeviceIDError){
  console.log(getDeviceIDError);
});</code></pre>
<h1>Push notifications</h1>
<p>Here are the steps to make push notifications work:</p>
<ol>
  <li>
    Go to <a href="https://firebase.google.com">https://firebase.google.com</a>
  </li>
  <li>
    Register / Login to the Firebase console. You should be logged in to
    <a href="https://console.firebase.google.com.">https://console.firebase.google.com.</a>
  </li>
  <li>Create and select a project if you haven't done before.</li>
  <li>Go to Settings &gt; Project settings.</li>
  <li>Create an app for Android.</li>
  <li>
    Download the <code>google-services.json</code> for Android.
  </li>
  <li>
    Place this file under your root project folder. i.e. above www folder.
  </li>
  <li>
    Put these tags in config.xml file for Android:
    <div class="tabs">
      <div class="tab">
        <pre><code class="xml">&lt;platform name="android"&gt;
   &lt;resource-file src="google-services.json" target="app/google-services.json" /&gt;
&lt;/platform&gt;</code></pre>
      </div>
    </div>
  </li>
  <li>
    Put these tags in config.xml file if you are using cordova-android 9.x or
    greater:
    <div class="tabs">
      <div class="tab">
        <pre><code class="xml">&lt;preference name="GradlePluginGoogleServicesEnabled" value="true" /&gt;
&lt;preference name="GradlePluginGoogleServicesVersion" value="4.2.0" /&gt;</code></pre>
      </div>
    </div>
  </li>
  <li>
    Install the google services plugin if you use cordova-android below version
    9
    <pre><code class="shell">cordova plugin add cordova-support-google-services --save</code></pre>
  </li>
  <li>Build your app, and test push notifications.</li>
</ol>
<div class="callout callout--warning">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Limitations of Cordova</span></strong>
  </p>
  <p>
    Due to limitations of the way push is handled in a Cordova application, it's
    not possible to report back actions done when a push notification is received.
  </p>
</div>
<h2>Push Method Implementation</h2>
<p>
  First, when setting up push for the Cordova SDK, you would first select the push
  token mode. This would allow you to choose either test or production modes, push
  token mode should be set before init.
</p>
<pre><code class="javascript">// Important call this method before init method
Countly.pushTokenType(Countly.messagingMode.DEVELOPMENT, "Channel Name", "Channel Description");
// Countly.messagingMode.DEVELOPMENT
// Countly.messagingMode.PRODUCTION
// Countly.messagingMode.ADHOC</code></pre>
<p>
  When you are finally ready to initialize Countly push, you would call Countly.askForNotificationPermission(),
  this function should be call after init.
</p>
<pre><code class="javascript">// Call this method any time.
Countly.askForNotificationPermission();
// This method will ask for permission, and send push token to countly server.</code></pre>
<p>
  Cordova code to receive notification data. Call anywhere or event before init.
</p>
<pre><code class="javascript">Countly.registerForNotification(function(theNotification){
  console.log(JSON.stringify(theNotification));
});</code></pre>
<h2>Rich Push Notification</h2>
<p>
  For Android, there is no special procedure required, you can install the community
  plugin, and it should work.
</p>
<p>
  For iOS, you will need to follow these instruction:
  <a href="https://resources.count.ly/docs/countly-sdk-for-ios-and-os-x#section-rich-push-notifications-ios10-only-">https://resources.count.ly/docs/countly-sdk-for-ios-and-os-x#section-rich-push-notifications-ios10-only-</a>
</p>
<h1>User location</h1>
<p>
  While integrating this SDK into your application, you might want to track your
  user location. You could use this information to better know your apps user base
  or to send them tailored push notifications based on their coordinates. There
  are 4 fields that can be provided:
</p>
<ul>
  <li>country code in the 2 letter iso standard</li>
  <li>city name (has to be set together with country code)</li>
  <li>
    Comma separate latitude and longitude values, for example "56.42345,123.45325"
  </li>
  <li>ip address of your user</li>
</ul>
<pre><code class="javascript">// send user location
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
<h1>Remote Config</h1>
<p>
  Remote config allows you to modiffy how your app functions or looks by requesting
  key-value pairs from your Countly server. The returned values can be modiffied
  based on the user profile. For more details please see Remote Config documentation.
</p>
<h2>Automatic remote config</h2>
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
<pre><code class="javascript">// Call this method before init
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
<h2>Manual remote config</h2>
<p>
  There are three ways for manually requesting a Remote Config update:
</p>
<ul>
  <li>Manually updating everything</li>
  <li>Manually updating specific keys</li>
  <li>Manually updating everything except specific keys</li>
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
<pre><code class="javascript">Countly.remoteConfigUpdate(function(r){
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
<pre><code class="javascript">Countly.updateRemoteConfigForKeysOnly(["name"], function(r){
  alert(r)
}, function(r){
  alert(r);
});</code></pre>
<p>
  You might want to update all values except a few defined keys, for that call
  updateRemoteConfigExceptKeys. The key list is a array with string values of the
  keys. It has a callback to let you know when the request has finished.
</p>
<pre><code class="javascript">Countly.updateRemoteConfigExceptKeys(["url"], function(r){
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
<h2>Getting Remote Config values</h2>
<p>
  To request a stored value, call <code>getRemoteConfigValueForKey</code> with
  the specified key. If it returns null then no value was found. The SDK has no
  knowledge of the returned value type and therefore returns an object. The developer
  needs to cast it to the appropriate type. The returned values can also be a JSONArray,
  JSONObject or just a simple value like int.
</p>
<pre><code class="javascript">Countly.getRemoteConfigValueForKey("name", function(r){
   alert(r)
 }, function(r){
   alert(r);
 });</code></pre>
<h2>Clearing stored values</h2>
<p>
  At some point you might want to erase all values downloaded from the server.
  To achieve that you need to call one function, depicted below:
</p>
<pre><code class="javascript">Countly.remoteConfigClearValues(function(r){
  alert(r)
}, function(r){
  alert(r);
});</code></pre>
<h1>User feedback</h1>
<p>
  There are two ways of getting feedback from your users: Star rating dialog, feedback
  widget.
</p>
<p>
  Star rating dialog allows users to give feedback as a rating from 1 to 5. The
  feedback widget allows to get the same 1 to 5 rating and also a text comment.
</p>
<h2>Star rating dialog</h2>
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
<pre><code class="javascript">// Star Rating
countly.askForStarRating(Function(ratingResult){
  console.log(ratingResult);
});</code></pre>
<div></div>
<h2>Rating widget</h2>
<p>
  Feedback widget shows a server configured widget to your user devices.
</p>
<p>
  <img src="/hc/article_attachments/360050033271/072bb00-t1.png" alt="072bb00-t1.png">
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
  <img src="/hc/article_attachments/360049916892/2dd58c6-t2.png" alt="2dd58c6-t2.png">
</p>
<p>
  Using that you can call the function to show the widget popup:
</p>
<pre><code class="javascript">// Feedback Modal
countly.askForFeedback("5e425407975d006a22535fc", "close");</code></pre>
<h1>User Profiles</h1>
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
<pre><code class="javascript">/ example for setting user data
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
<p>
  Using "" for strings or a negative number for 'byear' will effectively delete
  that property.
</p>
<p>
  For custom user properties you may use any key values to be stored and displayed
  on your Countly backend. Note: keys with . or $ symbols will have those symbols
  removed.
</p>
<h2>Setting custom values</h2>
<p>
  Additionally you can do different manipulations on your custom data values, like
  increment current value on server or store a array of values under the same property.
</p>
<p>Below is the list of available methods:</p>
<pre><code class="javascript">// example for extra user features

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
<h1>Application Performance Monitoring</h1>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Minimum Countly SDK Version</span></strong>
  </p>
  <p>
    This feature is only supported by the minimum SDK version 20.4.0.
  </p>
</div>
<p>
  Performance Monitoring feature allows you to analyze your application's performance
  on various aspects. For more details please see
  <a href="https://support.count.ly/hc/en-us/articles/900000819806-Performance-monitoring" target="_self">Performance Monitoring documentation</a>.
</p>
<p>
  Here is how you can utilize Performance Monitoring feature in your apps:
</p>
<p>First, you need to enable Performance Monitoring feature::</p>
<pre><code class="javascript">Countly.enableApm(); 
// Enable APM features.</code></pre>
<p>
  With this, Countly SDK will start measuring some performance traces automatically.
  Those include app foreground time, app background time. Additionally, custom
  traces and network traces can be manually recorded.
</p>
<h2>App Start Time</h2>
<p>
  For the app start time to be recorded, you need to call the
  <code>appLoadingFinished</code> method. Make sure this method is called after
  <code>init</code>.
</p>
<pre><code class="javascript">// Example of appLoadingFinished
Countly.init("https://try.count.ly", "YOUR_API_KEY").then((result) =&gt; {
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
<h2>Custom traces</h2>
<p>
  You may also measure any operation you want and record it using custom traces.
  First, you need to start a trace by using the
  <code class="objectivec">startTrace(traceKey)</code> method:
</p>
<pre><code class="javascript">Countly.startTrace(traceKey);</code></pre>
<p>
  Then you may end it using the
  <code class="objectivec">endTrace(traceKey, customMetric)</code>method, optionally
  passing any metrics as key-value pairs:
</p>
<pre><code class="javascript">String traceKey = "Trace Key"
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
<pre><code class="javascript">Countly.cancelTrace(traceKey);</code></pre>
<p>
  Additionally, if you need you may cancel all custom traces you started, using
  <code class="objectivec">clearAllTraces()</code>method:
</p>
<pre><code class="javascript">Countly.clearAllTraces(traceKey);</code></pre>
<h2>Network traces</h2>
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
<pre><code class="javascript">Countly.recordNetworkTrace(networkTraceKey, responseCode, requestPayloadSize, responsePayloadSize, startTime, endTime);</code></pre>
<div></div>
<h1>User Consent</h1>
<p>
  To be compliant with GDPR, starting from 18.04, Countly provides ways to toggle
  different Countly features on/off depending on the given consent.
</p>
<p>More information about GDPR can be found here.</p>
<p>
  By default the requirement for consent is disabled. To enable it, you have to
  call setRequiresConsent with true, before initializing Countly.
</p>
<pre><code class="javascript">Countly.setRequiresConsent(true);</code></pre>
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
  <li>
    sessions - tracking when, how often and how long users use your app
  </li>
  <li>events - allow sending custom events to server</li>
  <li>views - allow tracking which views user visits</li>
  <li>location - allow sending location information</li>
  <li>crashes - allow tracking crashes, exceptions and errors</li>
  <li>
    attribution - allow tracking from which campaign did user come
  </li>
  <li>
    users - allow collecting/providing user information, including custom properties
  </li>
  <li>push - allow push notifications</li>
  <li>starRating - allow to send their rating and feedback</li>
  <li>apm - allow application performance monitoring</li>
  <li>
    remoteConfig - allows downloading remote config values from your server
  </li>
</ul>
<h2>Changing consent</h2>
<p>There are 3 ways of changing feature consent:</p>
<ul>
  <li>
    giveConsentInit - To add consent for a single feature (string parameter)
    or a subset of features (array of strings parameter). Use this method for
    giving consent before initializing.
  </li>
</ul>
<pre><code class="javascript">//giveConsent
Countly.giveConsentInit(["events", "views", "star-rating", "crashes"]);

// removeConsent
Countly.removeConsent(["events", "views", "star-rating", "crashes"]);</code></pre>
<ul>
  <li>
    giveConsent/removeConsent - gives or removes consent to a specific feature
  </li>
</ul>
<pre><code class="javascript">//giveConsent
Countly.giveConsent(["events", "views", "star-rating", "crashes"]);

// removeConsent
Countly.removeConsent(["events", "views", "star-rating", "crashes"]);</code></pre>
<ul>
  <li>
    giveAllConsent/removeAllConsent - giveAll or removeAll consent to a specific
    feature
  </li>
</ul>
<pre><code class="javascript">//giveAllConsent
Countly.giveAllConsent();

//removeAllConsent
Countly.removeAllConsent();
</code></pre>
<div></div>
<h1>Security and privacy</h1>
<h2>Parameter Tampering Protection</h2>
<p>
  You can set optional salt to be used for calculating checksum of request data,
  which will be sent with each request using &amp;checksum field. You need to set
  exactly the same salt on Countly server. If salt on Countly server is set, all
  requests would be checked for validity of &amp;checksum field before being processed.
</p>
<pre><code class="javascript">// sending data with salt
Countly.enableParameterTamperingProtection("salt");</code></pre>
<h1>Other features</h1>
<h2>Forcing HTTP POST</h2>
<p>
  If the data sent to the server is short enough, the sdk will use HTTP GET requests.
  In case you want an override so that HTTP POST is used in all cases, call the
  "setHttpPostForced" function after you called "init". You can use the same function
  to later in the apps life cycle disable the override. This function has to be
  called every time the app starts.
</p>
<pre><code class="javascript">Countly.setHttpPostForced(true); // default is false
</code></pre>
<h2>Optional parameters during initialization</h2>
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
  <li>Country code: ISO Country code for the user's country</li>
  <li>City: Name of the user's city</li>
  <li>
    Location: Comma separate latitude and longitude values, for example "56.42345,123.45325"
  </li>
</ul>
<pre><code class="javascript">
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