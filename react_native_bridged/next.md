<p>
  This document will guide you through the process of Countly SDK installation
  and it applies to version 21.11.0<br>
  Countly is an open source SDK, you can take a look at our SDK code in the
  <a href="https://github.com/Countly/countly-sdk-react-native-bridge" target="_self">Github repo</a>
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <span class="wysiwyg-font-size-large"><strong>Older documentation</strong></span>
  </p>
  <p>
    To access the documentation for version 20.11 and older, click
    <a href="/hc/en-us/articles/360037813231" target="_self" rel="undefined">here.</a>
  </p>
</div>
<p>
  This is the Countly SDK for React Native applications. It features bridging,
  meaning it includes all the functionalities that Android and iOS SDKs provide
  rather than having those functionalities as React Native code.
</p>
<p>
  <strong>Supported Platforms:</strong> Countly SDK supports iOS and Android.
</p>
<p>
  You can take a look at our sample application in the
  <a href="https://github.com/Countly/countly-sdk-react-native-bridge/tree/master/example" target="_self" rel="undefined">Github repo</a>.
  It should show how most of the functionalities can be used.
</p>
<h1>Adding the SDK to the project</h1>
<p>
  In order to use the React Native SDK, please use the following commands to create
  a new React Native application.
</p>
<pre><code class="shell">npm install -g react-native-cli     # Install React Native
react-native init AwesomeProject    # Create a new project

cd AwesomeProject                   # Go to that directory
react-native run-android # OR       # Run the android project
react-native run-ios                # Run the iOS project

# New terminal
adb reverse tcp:8081 tcp:8081       # Link Android port
npm start                           # Run the build server</code></pre>
<p>
  Run the following snippet in the root directory of your React Native project
  to install the npm dependencies and link <strong>native libraries</strong>.
  <strong>Note: </strong>use the latest SDK version currently available, not specifically
  the one shown in the sample below.
</p>
<pre># Include the Countly Class in the file that you want to use.
npm install --save https://github.com/Countly/countly-sdk-react-native-bridge.git
# OR 
npm install --save countly-sdk-react-native-bridge@20.11.0

# Linking the library to your app

# react-native &lt; 0.60. For both Android and iOS
react-native link countly-sdk-react-native-bridge
cd node_modules/countly-sdk-react-native-bridge/ios/
pod install 
cd ../../../

# react-native &gt;= 0.60 for iOS (Android will autolink)
cd ios 
pod install
cd ..</pre>
<h1>SDK Integration</h1>
<h2>Minimal setup</h2>
<p>
  We will need to call two methods (<code class="JavaScript">init</code> and
  <code class="JavaScript">start</code>) in order to set up our SDK. These methods
  should only be called once during the app's lifecycle and should be done as early
  as possible. Your main app component's
  <code class="JavaScript">componentDidMount</code>method may be a good place.
</p>
<pre><code class="javascript">import Countly from 'countly-sdk-react-native-bridge';

if(!await Countly.isInitialized()) {
  await Countly.init("https://try.count.ly", "YOUR_APP_KEY"); // Initialize the countly SDK.
  Countly.start(); // start session tracking
}</code></pre>
<p>
  For more information on how to acquire your application key (appKey) and server
  URL, check
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#acquiring-your-application-key-and-server-url" target="_self">here</a>
</p>
<p>
  After <code class="JavaScript">init</code> and
  <code class="JavaScript">start</code> have been called once, you may use the
  commands in the rest of this document to send additional data and metrics to
  your server.
</p>
<h2>Enable logging</h2>
<p>
  The first thing you should do while integrating our SDK is enable logging. If
  logging is enabled, then our SDK will print out debug messages about its internal
  state and encountered problems.
</p>
<p>
  Call <code class="JavaScript">setLoggingEnabled</code> on the config class to
  enable logging:
</p>
<pre><code class="hljs coffeescript">Countly.setLoggingEnabled(true); // Enable countly internal debugging logs</code></pre>
<h2>Device ID</h2>
<p>
  You may provide your own custom device ID when initializing the SDK using the
  method below.
</p>
<pre>Countly.init(SERVER_URL, APP_KEY, DEVICE_ID)</pre>
<h2 class="anchor-heading">SDK data storage</h2>
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
  You will need to call the following method before calling
  <code class="JavaScript">init</code> in order to activate automatic crash reporting.
</p>
<pre><code class="javascript">// Using Countly crash reports
Countly.enableCrashReporting();
Countly.init(...);</code></pre>
<h2>Automatic crash report segmentation</h2>
<p>
  You may add a key/value segment to crash reports. For example, you could set
  which specific library or framework version you used in your app. You may then
  figure out if there is any correlation between the specific library or another
  segment and the crash reports.
</p>
<p>Use the following function for this purpose:</p>
<pre><code class="JavaScript">var segment = {"Key": "Value"};
Countly.setCustomCrashSegments(segment);</code></pre>
<h2>Handled exceptions</h2>
<p>
  You might catch an exception or similar error during your app’s runtime.
</p>
<p>
  You may also log these handled exceptions to monitor how and when they are happening
  with the following command:
</p>
<pre><code class="JavaScript">Countly.logException(stack, nonfatal, customSegments);</code></pre>
<p>
  The method <code class="javascript">logException</code>takes a string for the
  stack trace, a boolean flag indicating if the crash is considered fatal or not,
  and a segments dictionary to add additional data to your crash report.
</p>
<p>
  Below are some examples that how to log handled/nonfatal and unhandled/fatal
  exceptions manually.
</p>
<p>
  <strong>1. Manually report handled exception</strong>
</p>
<pre><code class="JavaScript">Countly.logException("STACK_TRACE_STRING", true);</code></pre>
<p>
  <strong>2. Manually report handled exception with segmentation</strong>
</p>
<pre><code class="JavaScript">Countly.logException("STACK_TRACE_STRING", true, {"_facebook_version": "0.0.1"});</code></pre>
<p>
  <strong>3. Manually report fatal exception</strong>
</p>
<pre><code class="JavaScript">Countly.logException("STACK_TRACE_STRING", false);</code></pre>
<p>
  <strong>4. Manually report fatal exception with segmentation</strong>
</p>
<pre><code class="JavaScript">Countly.logException("STACK_TRACE_STRING", false, {"_facebook_version": "0.0.1"});</code></pre>
<h2>Crash breadcrumbs</h2>
<p>
  Throughout your app you can leave crash breadcrumbs which would describe previous
  steps that were taken in your app before the crash. After a crash happens, they
  will be sent together with the crash report.
</p>
<p>Following the command adds crash breadcrumb:</p>
<pre><code class="JavaScript">Countly.addCrashLog(String record) </code></pre>
<h2>Native C++ Crash Reporting</h2>
<p>
  If you have C++ libraries in your React Native Android app, the React Native
  Bridge SDK allows you to record possible crashes in your Countly server by integrating
  the <code class="JavaScript">sdk-native</code>developed within our
  <a href="https://github.com/Countly/countly-sdk-android">Android SDK</a>. Find
  more information
  <a href="https://support.count.ly/hc/en-us/articles/360037754031-Android-SDK#native-c-crash-reporting" target="_blank" rel="noopener">here</a>.
</p>
<p>
  As this feature is optional, you will need to do some changes in your react native
  android project files in order to make it available.
</p>
<p>
  Go to
  <code class="JavaScript">YOUR_REACT_NATIVE_PROJECT_PATH/android/app/build.gradle</code>and
  add the package dependency (please change the
  <code class="JavaScript">LATEST_VERSION</code> below by checking our Maven
  <a href="https://bintray.com/countly/maven/sdk-native">page</a>, currently 20.11.6):
</p>
<pre><code class="shell">dependencies {
    implementation 'ly.count.android:sdk-native:LATEST_VERSION'    
}</code></pre>
<p>
  Then call <code class="JavaScript">Countly.initNative()</code> method as early
  as possible in your react native android project to be able to catch setup time
  crashes, it should be preferably in the "onCreate" callback of the Application
  class.
</p>
<p>
  You may find <code class="JavaScript">MainApplication.java</code> at this path:
</p>
<p>
  <code class="JavaScript">YOUR_REACT_NATIVE_PROJECT_PATH/android/app/src/main/java/com/PROJECT_NAME</code>
</p>
<pre>// import this in your Application class
import ly.count.android.sdknative.CountlyNative; 

// call this function in "onCreate" callback of Application class
CountlyNative.initNative(getApplicationContext());</pre>
<p>
  <code class="JavaScript">getApplicationContext()</code> is needed to determine
  a storage place for minidump files.
</p>
<p>
  Sending crash dump files to the server will be taken care of by the SDK during
  the next app initialization. We also provide a Gradle plugin that automatically
  uploads symbol files to your server (these are needed for the symbolication of
  crash dumps). Integrate it into your React Native project as explained in the
  relevant Android documentation
  <a href="https://support.count.ly/hc/en-us/articles/360037754031-Android#native-c-crash-reporting" target="_self" rel="undefined">page</a>.
</p>
<p>
  This is what the debug logs will look like if you use this feature:
</p>
<pre><code class="text">$ adb logcat -s Countly:V countly_breakpad_cpp:V

# when Countly.initNative() is called 

D/countly_breakpad_cpp(123): breakpad initialize succeeded. dump files will be saved at /Countly/CrashDumps

# when a crash occurs (you may trigger one by Countly.testCrash())

D/countly_breakpad_cpp(123): DumpCallback started
D/countly_breakpad_cpp(123): DumpCallback ==&gt; succeeded path=/Countly/CrashDumps/30f6d9b8-b3b2-1553-2efe0ba2-36588990.dmp

# when app is run again after the crash 

D/Countly (124): Initializing...
D/Countly (124): Checking for native crash dumps
D/Countly (124): Native crash folder exists, checking for dumps
D/Countly (124): Crash dump folder contains [1] files
D/Countly (124): Recording native crash dump: [30f6d9b8-b3b2-1553-2efe0ba2-36588990.dmp]</code></pre>
<h1>Events</h1>
<p>
  An <a href="http://resources.count.ly/docs/custom-events">Event</a> is any type
  of action that you can send to a Countly instance, e.g. purchases, changed settings,
  view enabled, and so on. This way it's possible to get much more information
  from your application compared to what is sent from the SDK to the Countly instance
  by default.
</p>
<p>
  Here are the detail about properties which we can use with event:
</p>
<ul>
  <li>
    <code class="JavaScript">key</code> identifies the event
  </li>
  <li>
    <code class="JavaScript">count</code> is the number of times this event occurred
  </li>
  <li>
    <code class="JavaScript">sum</code> is an overall numerical data set tied
    to an event. For example, total amount of in-app purchase event.
  </li>
  <li>
    <code class="JavaScript">duration</code> is used to record and track the
    duration of events.
  </li>
  <li>
    <code class="JavaScript">segmentation</code> is a key-value pairs, we can
    use <code class="JavaScript">segmentation</code> to track additional information.
  </li>
</ul>
<div class="callout callout--warning">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Data passed should be in UTF-8</span></strong>
  </p>
  <p>
    All data passed to the Countly server via the SDK or API should be in UTF-8.
  </p>
  <h2>Recording events</h2>
</div>
<p>
  We will be recording a <strong>purchase</strong> event below. Here is a quick
  summary of the information with which each usage will provide us:
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
</ul>
<p>
  <strong>1. Event key and count</strong>
</p>
<pre><code class="JavaScript">var event = {"eventName":"Purchase","eventCount":1};
Countly.sendEvent(event);</code></pre>
<p>
  <strong>2. Event key, count, and sum</strong>
</p>
<pre><code class="JavaScript">var event = {"eventName":"Purchase","eventCount":1,"eventSum":"0.99"};
Countly.sendEvent(event);</code></pre>
<p>
  <strong>3. Event key and count with segmentation(s)</strong>
</p>
<pre><code class="JavaScript">var event = {"eventName":"purchase","eventCount":1}; 
event.segments = {"Country" : "Germany", "app_version" : "1.0"}; 
Countly.sendEvent(event);</code></pre>
<p>
  <strong>4. Event key, count, and sum with segmentation(s)</strong>
</p>
<pre><code class="JavaScript">var event = {"eventName":"purchase","eventCount":1};
event.segments = {"Country" : "Germany", "app_version" : "1.0","eventSum":"0.99"};
Countly.sendEvent(event);</code></pre>
<p>
  Those are only a few examples of what you can do with events. You may extend
  those examples and use Country, app_version, game_level, time_of_day, and any
  other segmentation that will provide you with valuable insights.
</p>
<h2>Timed events</h2>
<p>
  It's possible to create timed events by defining a start and a stop moment.
</p>
<pre><code class="JavaScript">String eventName = "Event Name";

//start some event
Countly.startEvent(eventName);
//wait some time

//end the event 
Countly.endEvent(eventName);</code></pre>
<p>
  You may also provide additional information when ending an event. However, in
  that case, you have to provide the segmentation, count, and sum. The default
  values for those are "null", 1 and 0.
</p>
<pre><code class="JavaScript">String eventName = "Event Name";

//start some event
Countly.startEvent(eventName);

var event = { "eventName": eventName, "eventCount": 1, "eventSum": "0.99" };
event.segments = { "Country": "Germany", "Age": "28" };

//end the event while also providing segmentation information, count and sum
Countly.endEvent(event);
</code></pre>
<p>
  You may cancel the started timed event in case it is not relevant anymore:
</p>
<pre><code class="JavaScript">String eventName = "Event name";

//start some event
Countly.startEvent(eventName);
//wait some time

//cancel the event 
Countly.cancelEvent(eventName);</code></pre>
<h1>View tracking</h1>
<p>You may track custom views with the following code snippet:</p>
<pre><code class="JavaScript">Countly.recordView("View Name")</code></pre>
<p>
  While manually tracking views, you may add your custom segmentation to them like
  this:
</p>
<pre><code class="JavaScript">var viewSegmentation = { "Country": "Germany", "Age": "28" };
Countly.recordView("View Name", viewSegmentation);</code></pre>
<p>
  To review the resulting data, open the dashboard and go to
  <code class="JavaScript">Analytics &gt; Views</code>. For more information on
  how to use view tracking data to its fullest potential, click
  <a href="http://resources.count.ly/docs/view-analytics">here</a>.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/1059a04-3.PNG">
</div>
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
<h2>Changing device ID with and without merge</h2>
<p>
  You may configure or change the device ID anytime using the method below.
</p>
<pre>Countly.changeDeviceId(DEVICE_ID, ON_SERVER);</pre>
<p>
  You may either allow the device to be counted as a new device or merge existing
  data on the server. If <code class="JavaScript">onServer</code> is set to
  <code class="JavaScript">true</code>, the old device ID on the server will be
  replaced with the new one, and data associated with the old device ID will be
  merged automatically. Otherwise, if <code class="JavaScript">onServer</code>
  is set to <code class="JavaScript">false</code>, the device will be counted as
  a new device on the server.
</p>
<h2>Temporary Device ID</h2>
<p>
  You may use a temporary device ID mode for keeping all requests on hold until
  the real device ID is set later.
</p>
<p>
  To enable this when initializing the SDK, use the method below.
</p>
<pre>Countly.init(SERVER_URL, APP_KEY, "TemporaryDeviceID")</pre>
<p>
  To enable a temporary device ID <strong>after</strong> initialization, use the
  method below.
</p>
<pre>Countly.changeDeviceId(Countly."TemporaryDeviceID", ON_SERVER);</pre>
<p>
  <strong>Note:</strong> When passing the
  <code class="JavaScript">TemporaryDeviceID</code> for the
  <code class="JavaScript">deviceID</code> parameter, the argument for the
  <code class="JavaScript">onServer</code>parameter does not matter.
</p>
<p>
  As long as the device ID value is
  <code class="JavaScript">TemporaryDeviceID</code>, the SDK will be in temporary
  device ID mode and all requests will be on hold, but they will be persistently
  stored.
</p>
<p>
  When in temporary device ID mode, method calls for presenting feedback widgets
  and updating remote config will be ignored.
</p>
<p>
  Later, when the real device ID is set using the
  <code class="JavaScript">Countly.changeDeviceId(DEVICE_ID, ON_SERVER);</code>
  method, all requests which have been kept on hold until that point will start
  with the real device ID.
</p>
<h2>Retrieving the device id</h2>
<p>
  You may want to see what device id Countly is assigning for the specific device.
  For that, you may use the following calls.
</p>
<pre><code class="JavaScript">String usedId = Countly().getCurrentDeviceId();</code></pre>
<h1>Push Notifications</h1>
<p>
  Please first check our
  <a href="/hc/en-us/articles/360037270012" target="_self" rel="undefined">Push Notifications documentation</a>
  to see how you can use this feature. Since Android and iOS handles notifications
  differently (from how you can send them externally to how they are handled in
  native code), we need to provide different instructions for these two platforms.
</p>
<h2>General Setup</h2>
<p>
  First, when setting up Push for the React Native (Bridge) SDK, select the push
  token mode. This allows you to choose either test or production modes. Note that
  the push token mode should be set before initialization. Use the method below.
</p>
<pre>// Important: call this method before init method
Countly.pushTokenType(Countly.messagingMode.DEVELOPMENT, "Channel Name", "Channel Description");
// Countly.messagingMode.DEVELOPMENT
// Countly.messagingMode.PRODUCTION
// Countly.messagingMode.ADHOC</pre>
<p>
  When you are ready to initialize Countly Push, call
  <code class="JavaScript">Countly.askForNotificationPermission()</code> after
  <code class="JavaScript">init</code>, using the method below.
</p>
<pre>// CUSTOM_SOUND_PATH is an optional parameter and currently only support Android.<br>Countly.askForNotificationPermission("CUSTOM_SOUND_PATH");
// This method will ask for permission, 
// and send push token to countly server.</pre>
<p>
  With an option parameter of custom sound path for push notifications.
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Supported Platforms</span></strong>
  </p>
  <p>
    Currently custom sound feature is only available for Android
  </p>
</div>
<div class="callout callout--warning">
  <p>
    If you would like to use a custom sound in your push notifications, they
    must be present on the device. They may not be stored somewhere on the internet
    and then linked from there.
  </p>
</div>
<h2>Android Setup</h2>
<p>
  Step 1: For FCM credentials setup please follow the instruction from this URL
  <a class="c-link" href="https://support.count.ly/hc/en-us/articles/360037754031-Android#getting-fcm-credentials" target="_blank" rel="noopener noreferrer" data-stringify-link="https://support.count.ly/hc/en-us/articles/360037754031-Android#getting-fcm-credentials" data-sk="tooltip_parent">https://support.count.ly/hc/en-us/articles/360037754031-Android#getting-fcm-credentials</a>.
</p>
<p>
  Step 2: Make sure you have
  <code class="JavaScript">google-services.json</code> from
  <a href="https://firebase.google.com/">https://firebase.google.com/</a>
</p>
<p>
  Step 3: Make sure the app package name and the
  <code class="JavaScript">google-services.json</code>
  <code class="JavaScript">package_name</code> matches.
</p>
<p>
  Step 4: Place the <code class="JavaScript">google-services.json</code> file inside
  <code class="JavaScript">android/app</code>
</p>
<p>
  Step 5: Use google services latest version from this link
  <a href="https://developers.google.com/android/guides/google-services-plugin">https://developers.google.com/android/guides/google-services-plugin</a>
</p>
<p>
  Step 6: Add the following line in the file
  <code class="JavaScript">android/build.gradle</code>
</p>
<pre><code class="JavaScript">buildscript {
    dependencies {
        classpath 'com.google.gms:google-services:4.3.2'
    }
}
</code></pre>
<p>
  Step 7: Add the following line in file
  <code class="JavaScript">android/app/build.gradle</code>
</p>
<pre><code class="JavaScript">// Add this at the bottom of the file
apply plugin: 'com.google.gms.google-services'
</code></pre>
<p>
  <strong>Note:</strong> You need to do some additional steps to handle multiple
  messaging services if you are using other plugins for push notifications, please
  follow the instructions from this URL:<br>
  <a href="/hc/en-us/articles/4412005896217" target="_self">Handling multiple FCM services</a>
</p>
<h2>iOS Setup</h2>
<p>
  For iOS push notification please follow the instruction from this URL
  <a href="https://resources.count.ly/docs/countly-sdk-for-ios-and-os-x#section-push-notifications">https://resources.count.ly/docs/countly-sdk-for-ios-and-os-x#section-push-notifications</a>
</p>
<p>
  For React Native you can find
  <code class="JavaScript">CountlyNotificationService.h/m</code> file under
  <code class="JavaScript">Pods/Development Pods/CountlyReactNative/CountlyNotificationService.h/m</code>
</p>
<p>
  <strong>Pro Tips to find the files from deep hierarchy: </strong>
</p>
<ul>
  <li>
    You can filter the files in the navigator using a shortcut ⌥⌘J (Option-Command-J),
    in the filter box type "CountlyNotificationService" and it will show the
    related files only.
  </li>
  <li>
    You can find the file using the shortcut ⇧⌘O (Shift-Command-O) and then navigate
    to that file using the shortcut ⇧⌘J (Shift-Command-J)
  </li>
</ul>
<p>
  You can drag and drop both .h and .m files from Pod to Compile Sources.
</p>
<div class="img-container">
  <img src="/hc/article_attachments/4404577440025/Countly_RN_PUSH.png" alt="Countly_RN_PUSH.png">
</div>
<h2>Handling push callbacks</h2>
<p>
  To register a Push Notification callback after initialising the SDK, use the
  method below.
</p>
<pre>Countly.registerForNotification(function(theNotification){
console.log(JSON.stringify(theNotification));
});</pre>
<p>
  In order to listen to notification receive and click events, Place below code
  in <code>AppDelegate.m</code>
</p>
<p>Add header files</p>
<pre><code class="JavaScript">#import "CountlyReactNative.h"<br>#import &lt;UserNotifications/UserNotifications.h&gt;
</code></pre>
<p>
  Before <code>@end</code> add these method
</p>
<pre><code class="JavaScript">// Required for the notification event. You must call the completion handler after handling the remote notification.
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
{
  [CountlyReactNative onNotification: userInfo];
  completionHandler(0);
}

// When app is killed.
- (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void (^)(void))completionHandler{
  [CountlyReactNative onNotificationResponse: response];
  completionHandler();
}

// When app is running.
- (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler{
  [CountlyReactNative onNotification: notification.request.content.userInfo];
  completionHandler(0);
}
</code></pre>
<h1>User Location</h1>
<p>
  Countly allows you to send geolocation-based push notifications to your users.
  By default, the Countly Server uses the GeoIP database to deduce a user's location.
</p>
<h2>Set User Location</h2>
<p>
  If your app has a different way of detecting location, you may send this information
  to the Countly Server by using the
  <code class="JavaScript">setLocationInit</code> or<code class="JavaScript">setLocation</code>
  methods.
</p>
<p>
  We recommend using the <code class="JavaScript">setLocationInit</code> method
  before initialization to sent location. This includes:
</p>
<ul>
  <li>
    <code class="JavaScript">countryCode</code> a string in ISO 3166-1 alpha-2
    format country code
  </li>
  <li>
    <code class="JavaScript">city</code> a string specifying city name
  </li>
  <li>
    <code class="JavaScript">location</code> a string comma-separated latitude
    and longitude
  </li>
  <li>
    <code class="JavaScript">IP</code> a string specifying an IP address in IPv4
    or IPv6 formats
  </li>
</ul>
<pre><code class="javascript">// Example for setLocationInit
var countryCode = "us";
var city = "Houston";
var latitude = "29.634933";
var longitude = "-95.220255";
var ipAddress = "103.238.105.167";

Countly.setLocationInit(countryCode, city, latitude + "," + longitude, ipAddress);</code></pre>
<p>
  Geolocation recording methods may also be called at any time after the Countly
  SDK has started. To do so, use the <code class="JavaScript">setLocation</code>
  method as shown below.
</p>
<pre><code class="javascript">// Example for setLocation
var countryCode = "us";
var city = "Houston";
var latitude = "29.634933";
var longitude = "-95.220255";
var ipAddress = "103.238.105.167";

Countly.setLocation(countryCode, city, latitude + "," + longitude, ipAddress);
</code></pre>
<h2>Disable Location</h2>
<p>
  To erase any cached location data from the device and stop further location tracking,
  use the following method. Note that if after disabling location, the
  <code class="JavaScript">setLocation</code>is called with any non-null value,
  tracking will resume.
</p>
<pre><code class="javascript">//disable location tracking
Countly.disableLocation();</code></pre>
<h1>Remote Config</h1>
<p>
  Remote config allows you to modify how your app functions or looks by requesting
  key-value pairs from your Countly server. The returned values may be modified
  based on the user profile. For more details, please see the
  <a href="https://resources.count.ly/docs/remote-config">Remote Config documentation</a>.
</p>
<h2>Manual Remote Config download</h2>
<p>
  There are three ways for manually requesting a remote config update:
</p>
<ul>
  <li>Manually updating everything</li>
  <li>Manually updating specific keys</li>
  <li>Manually updating everything except specific keys.</li>
</ul>
<p>
  Each of these requests also has a callback. If the callback returns a non-null
  value, the request will encounter an error and fail.
</p>
<p>
  The <code class="JavaScript">remoteConfigUpdate</code> replaces all stored values
  with the ones from the server (all locally stored values are deleted and replaced
  with new ones). The advantage is that you can make the request whenever it is
  desirable for you. It has a callback to let you know when it has finished.
</p>
<pre><code class="JavaScript">Countly.remoteConfigUpdate(function(data){
console.log(data);
});</code></pre>
<p>
  Or you might only want to update specific key values. To do so, you will need
  to call <code class="JavaScript">updateRemoteConfigForKeysOnly</code> with the
  list of keys you would like to be updated. That list is an array with the string
  values of those keys. It has a callback to let you know when the request has
  finished.
</p>
<pre><code class="JavaScript">Countly.updateRemoteConfigForKeysOnly(){
Countly.updateRemoteConfigForKeysOnly(["aa", "bb"],function(data){
console.log(data);
});</code></pre>
<p>
  Or you might want to update all the values except a few defined keys. To do so,
  call <code class="JavaScript">updateRemoteConfigExceptKeys</code>. The key list
  is an array with string values of the keys. It has a callback to let you know
  when the request has finished.
</p>
<pre><code class="JavaScript">Countly.updateRemoteConfigExceptKeys(["aa", "bb"],function(data){
console.log(data);
});</code></pre>
<p>
  When making requests with an "inclusion" or "exclusion" array, if those arrays
  are empty or null, they will function the same as a simple manual request and
  will update all the values. This means it will also erase all keys not returned
  by the server.
</p>
<h2>Getting Remote Config values</h2>
<p>
  To request a stored value, call
  <code class="JavaScript">getRemoteConfigValueForKey</code> or
  <code class="JavaScript">getRemoteConfigValueForKeyP</code> with the specified
  key.
</p>
<pre><code class="JavaScript">Countly.getRemoteConfigValueForKey("KeyName", function(data){
console.log(data);
});

var data = await Countly.getRemoteConfigValueForKeyP("KeyName");</code></pre>
<h2>Clearing Stored Remote Config values</h2>
<p>
  At some point, you might like to erase all the values downloaded from the server.
  You will need to call one function to do so.
</p>
<pre><code class="JavaScript">Countly.remoteConfigClearValues();</code></pre>
<h1>User feedback</h1>
<p>
  There are a different ways of receiving feedback from your users: the Star-rating
  dialog, the Ratings widget, and the Surveys widgets (Surveys and NPS®).
</p>
<p>
  The Star-rating dialog allows users to give feedback as a rating from 1 to 5.
  The Ratings widget allows users to rate using the same 1 to 5 emoji-based rating
  system as well as leave a text comment. The Surveys widgets (Surveys and NPS®)
  allow for even more targeted feedback from users.
</p>
<h2>Star rating dialog</h2>
<p>
  The Star-rating integration provides a dialog for getting user feedback about
  an application. It contains a title, a simple message explaining its purpose,
  a 1 through 5-star meter for getting users rating, and a dismiss button in case
  the user does not want to give a rating.
</p>
<p>
  This star rating has nothing to do with Google Play Store ratings and reviews.
  It is simply for getting brief feedback from your users to be displayed on the
  Countly dashboard. If the user dismisses the star-rating dialog without giving
  a rating, the event will not be recorded.
</p>
<pre><code class="javascript">Countly.showStarRating();</code></pre>
<p>
  The star-rating dialog's title, message, and dismiss button text may be customized
  either through the <code class="JavaScript">init</code> function or the
  <code class="JavaScript">SetStarRatingDialogTexts</code> function.
</p>
<pre><code class="javascript">Countly.SetStarRatingDialogTexts("Custom title", "Custom message", "Custom dismiss button text");</code></pre>
<h2>Rating widget</h2>
<p>
  The rating widget displays a server-configured widget to your user devices.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/ea55d24-072bb00-t1.png">
</div>
<p>
  All the text fields in the example above can be configured and replaced with
  a custom string of your choice.
</p>
<p>
  In addition to a 1 through 5 rating, it is possible for users to leave a text
  comment and an email, should the user like to be contacted by the app developer.
</p>
<p>
  Showing the rating widget in a single call involves a two-set process: before
  it is shown, the SDK tries to contact the server to get more information about
  the dialog. Therefore, a network connection to it is needed.
</p>
<p>
  To display the widget after initializing the SDK, you will first need to get
  the widget ID from your server, as shown below.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/f773cf4-2dd58c6-t2.png">
</div>
<p>
  Then, call the function to show the widget popup using the widget ID below.
</p>
<pre><code class="javascript">Countly.presentRatingWidgetWithID("WidgetId", "Button Text", function(error){<br>if (error != null) {<br>  console.log(error);<br>}<br>});</code></pre>
<h2>Feedback widget</h2>
<p>
  It is possible to display 2 kinds of Surveys widgets:
  <a href="https://support.count.ly/hc/en-us/articles/900003407386-NPS-Net-Promoter-Score-" target="_blank" rel="noopener">NPS</a>
  and
  <a href="https://support.count.ly/hc/en-us/articles/900004337763-Surveys" target="_blank" rel="noopener">Surveys</a>.
  Both widgets are shown as webviews and they both use the same code methods.
</p>
<p>
  Before any Surveys widget can be shown, you need to create them in your Countly
  Dashboard.
</p>
<p>
  When the widgets are created, you need to use 2 calls in your SDK: one to get
  all available widgets for a user and another to display a chosen widget.
</p>
<p>To get your available widget list, use the call below.</p>
<pre><code class="javascript">Countly.getAvailableFeedbackWidgets().then((retrivedWidgets) =&gt; {
},(err) =&gt; {
});</code></pre>
<p>
  From the callback, get the list of all available widgets that apply to the current
  device ID.
</p>
<p>The objects in the returned list look like this:</p>
<pre><code class="javascript">{ "WIDGET_TYPE" : "WIDGET_ID" }</code></pre>
<p>
  To determine what kind of widget that is, check the "type" value. The potential
  values are <code class="JavaScript">survey</code> and
  <code class="JavaScript">nps</code>.
</p>
<p>
  Then use the widget type and description (which is the same as provided in the
  Dashboard) to decide which widget to show.
</p>
<p>
  After you have decided which widget you want to display, call the function below.
</p>
<pre><code class="javascript">Countly.presentFeedbackWidget("WIDGET_TYPE", "WIDGET_ID", "CLOSE_BUTTON_TEXT");</code></pre>
<h1>User Profiles</h1>
<p>
  You can provide Countly any details you may have about your user or visitor.
  This will allow you to track each specific user on the "User Profiles" tab, which
  is available in Countly Enterprise Edition. For more details, please review the
  <a href="/hc/en-us/articles/360037630571" target="_self" rel="undefined">User Profiles documentation</a>.
</p>
<p>
  In order to set a user profile, use the code snippet below. After you send a
  user’s data, it can be found in your Dashboard under
  <code class="JavaScript">Users &gt; User Profiles</code>.
</p>
<pre><code class="javascript">// Example for setting user data
var options = {};
options.name = "Nicola Tesla";
options.username = "nicola";
options.email = "info@nicola.tesla";
options.organization = "Trust Electric Ltd";
options.phone = "+90 822 140 2546";
options.picture = "http://www.trust.electric/images/people/nicola.png";
options.picturePath = "";
options.gender = "M";
options.byear = 1919;
Countly.setUserData(options);</code></pre>
<p>
  Countly also supports custom user properties that you can attach for each user.
  In order to set or modify a user's data (e.g. increment, multiply, etc.), use
  the code snippet below.
</p>
<pre><code class="javascript">// examples for custom user properties
Countly.userData.setProperty("keyName", "keyValue"); //set custom property
Countly.userData.setOnce("keyName", 200); //set custom property only if property does not exist
Countly.userData.increment("keyName"); //increment value in key by one
Countly.userData.incrementBy("keyName", 10); //increment value in key by provided value
Countly.userData.multiply("keyName", 20); //multiply value in key by provided value
Countly.userData.saveMax("keyName", 100); //save max value between current and provided
Countly.userData.saveMin("keyName", 50); //save min value between current and provided
Countly.userData.setOnce("setOnce", 200);//insert value to array of unique values
Countly.userData.pushUniqueValue("type", "morning");//insert value to array of unique values
Countly.userData.pushValue("type", "morning");//insert value to array which can have duplicates
Countly.userData.pullValue("type", "morning");//remove value from array</code></pre>
<h1>Application Performance Monitoring</h1>
<p>
  The Performance Monitoring feature allows you to analyze your application's performance
  on various aspects. For more details, please review the
  <a href="https://support.count.ly/hc/en-us/articles/900000819806-Performance-monitoring" target="_self">Performance Monitoring documentation</a>.
</p>
<p>
  Here is how you can utilize the Performance Monitoring feature in your apps:
</p>
<p>
  First, you need to enable the Performance Monitoring feature:
</p>
<pre><code class="javascript">// Enable APM features.
Countly.enableApm();</code></pre>
<p>
  With this, the Countly SDK will start measuring some performance traces automatically,
  including app foreground time, app background time. Additionally, custom traces
  and network traces can be manually recorded.
</p>
<h2>App Start Time</h2>
<p>
  For the app start time to be recorded, you need to call the
  <code class="JavaScript">appLoadingFinished</code> method. Make sure this method
  is called after <code class="JavaScript">init</code>.
</p>
<pre><code class="javascript">// Example of appLoadingFinished
await Countly.init("https://try.count.ly", "YOUR_APP_KEY");
Countly.appLoadingFinished();</code></pre>
<p>
  This calculates and records the app launch time for performance monitoring. It
  should be called when the app is loaded and it successfully displayed its first
  user-facing view. E.g. <code class="JavaScript">componentDidMount:</code> method
  or wherever is suitable for the app's flow. The time passed since the app has
  started to launch will be automatically calculated and recorded for performance
  monitoring. Note that the app launch time can be recorded only once per app launch.
  So, the second and following calls to this method will be ignored.
</p>
<h2>Custom trace</h2>
<p>
  You may also measure any operation you want and record it using custom traces.
  First, you need to start a trace by using the
  <code class="objectivec">startTrace(traceKey)</code> method:
</p>
<pre>Countly.startTrace(traceKey);</pre>
<p>
  Then you may end it using the
  <code class="objectivec">endTrace(traceKey, customMetric)</code>method, optionally
  passing any metrics as key-value pairs:
</p>
<pre>String traceKey = "Trace Key";
Map&lt;String, int&gt; customMetric = {
  "ABC": 1233,
  "C44C": 1337
};
Countly.endTrace(traceKey, customMetric);</pre>
<p>
  The duration of the custom trace will be automatically calculated upon ending.
</p>
<p>
  Trace names should be non-zero length valid strings. Trying to start a custom
  trace with the already started name will have no effect. Trying to end a custom
  trace with already ended (or not yet started) name will have no effect.
</p>
<p>
  You may also cancel any custom trace you started using the
  <code class="objectivec">cancelTrace(traceKey)</code>method:
</p>
<pre>Countly.cancelTrace(traceKey);</pre>
<p>
  Additionally, if you need you may cancel <strong>all</strong> custom traces you
  started, using the <code class="objectivec">clearAllTraces()</code>method:
</p>
<pre>Countly.clearAllTraces(traceKey);</pre>
<h2>Network trace</h2>
<p>
  You may record manual network traces using the
  <code class="JavaScript">recordNetworkTrace(networkTraceKey, responseCode, requestPayloadSize, responsePayloadSize, startTime, endTime)</code>
  method.
</p>
<p>
  A network trace is a collection of measured information about a network request.
  When a network request is completed, a network trace can be recorded manually
  to be analyzed via Performance Monitoring later using the following parameters:
</p>
<p>
  - <code class="JavaScript">networkTraceKey</code>: A non-zero length valid string
  - <code class="JavaScript">responseCode</code>: HTTP status code of the received
  response - <code class="JavaScript">requestPayloadSize</code>: Size of the request's
  payload in bytes - <code class="JavaScript">responsePayloadSize</code>: Size
  of the received response's payload in bytes -
  <code class="JavaScript">startTime</code>: UNIX timestamp in milliseconds for
  the starting time of the request - <code class="JavaScript">endTime</code>: UNIX
  timestamp in milliseconds for the ending time of the request
</p>
<pre>Countly.recordNetworkTrace(networkTraceKey, responseCode, requestPayloadSize, responsePayloadSize, startTime, endTime);</pre>
<h1>User consent</h1>
<p>
  Being compliant with GDPR and other data privacy regulations, Countly provides
  ways to toggle different Countly tracking features on or off depending on a user's
  given consent. For more details, please review the
  <a href="https://resources.count.ly/docs/compliance-hub">Compliance Hub plugin</a>
  documentation.
</p>
<p>
  Currently, available features with consent control are as follows:
</p>
<ul>
  <li>
    sessions - tracking when, how often, and how long users use your app
  </li>
  <li>events - allows sending events to the server</li>
  <li>views - allows tracking which views user visits</li>
  <li>location - allows sending location information</li>
  <li>crashes - allows tracking crashes, exceptions, and errors</li>
  <li>
    attribution - allows tracking from which campaign did the user come
  </li>
  <li>
    users - allows collecting and providing user information, including custom
    properties
  </li>
  <li>push - allows push notifications</li>
  <li>
    star-rating - allows sending the results from Rating Feedback widgets
  </li>
  <li>
    feedback - allows showing the results from Survey and NPS® Feedback widgets
  </li>
  <li>apm - allows application performance monitoring</li>
  <li>
    <span>remote-config</span> - allows downloading remote config values from
    your server
  </li>
</ul>
<p>
  Since the React Native Bridge SDK employs our iOS and Android SDKs, you may also
  be interested in reviewing their relevant documentation on this topic (<a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#consents" target="_self" rel="undefined">iOS Consents</a>
  and
  <a href="https://support.count.ly/hc/en-us/articles/360037754031-Android-SDK#user-consent-management" target="_self" rel="undefined">Android Consents</a>).
</p>
<p>
  Next we will go over the methods that are available in this SDK.
</p>
<table>
  <tbody>
    <tr>
      <th>Method</th>
      <th>Parameters / Examples</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>
        <code class="JavaScript">setRequiresConsent</code>
      </td>
      <td>boolean</td>
      <td>
        <p>
          The requirement for checking consent is disabled by default.
          To enable it, you will have to call
          <code class="JavaScript">setRequiresConsent</code>with
          <code class="JavaScript">true</code>before initializing Countly.
          You may also pass a consent flag as true or false when you call
          <code class="JavaScript">init</code>.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code class="JavaScript">giveConsentInit</code>
      </td>
      <td>string array of strings</td>
      <td>
        <p>
          To add consent for a single feature (string parameter) or a subset
          of features (array of strings parameter). Use this method for
          giving consent before initializing.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code class="JavaScript">giveConsent</code>
      </td>
      <td>string array of strings</td>
      <td>
        <p>
          To add consent for a single feature (string parameter) or a subset
          of features (array of strings parameter). Use this method for
          giving consent after initializing.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code class="JavaScript">removeConsent</code>
      </td>
      <td>string array of strings</td>
      <td>
        <p>
          To remove consent for a single feature (string parameter) or
          a subset of features (array of strings parameter).
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <code class="JavaScript">giveAllConsent</code>
      </td>
      <td>none</td>
      <td>To give consent for all available features.</td>
    </tr>
    <tr>
      <td>
        <code class="JavaScript">removeAllConsent</code>
      </td>
      <td>none</td>
      <td>To remove consent for all available features.</td>
    </tr>
  </tbody>
</table>
<pre><code class="javascript">// Usage examples

Countly.setRequiresConsent(true);

// for a single feature
Countly.giveConsentInit("events");
Countly.giveConsent("events");
Countly.removeConsent("events");

// for a subset of features
Countly.giveConsentInit(["events", "views", "star-rating", "crashes"]);
Countly.giveConsent(["events", "views", "star-rating", "crashes"]);
Countly.removeConsent(["events", "views", "star-rating", "crashes"]);

// for all available features
Countly.giveAllConsent();
Countly.removeAllConsent();</code></pre>
<p>
  The string values corresponding to the features that will be used in the
  <code class="JavaScript">giveConsent</code> or
  <code class="JavaScript">removeConsent</code> methods may be found
  <a href="https://support.count.ly/hc/en-us/articles/360037753291-SDK-development-guide#exposing-available-features-for-consent" target="_self">here</a>.
  In addition, please review our platform SDK documents if the feature is applicable
  or not for that platform.
</p>
<h1>Security and privacy</h1>
<h2>Parameter tampering protection</h2>
<p>
  You can set optional <code class="JavaScript">salt</code> to be used for calculating
  checksum of request data, which will be sent with each request using
  <code class="JavaScript">&amp;checksum</code> field. You need to set exactly
  the same <code class="JavaScript">salt</code> on the Countly server. If
  <code class="JavaScript">salt</code> on Countly server is set, all requests would
  be checked for the validity of <code class="JavaScript">&amp;checksum</code>
  field before being processed.
</p>
<pre><code class="javascript hljs">// sending data with salt
Countly.enableParameterTamperingProtection("salt");</code></pre>
<p>
  Make sure not to use salt on the Countly server and not on the SDK side, otherwise,
  Countly won't accept any incoming requests.
</p>
<h2>Pinned Certificate (Call this method before initialization)</h2>
<p>
  <strong>Terminal</strong>
</p>
<pre>openssl s_client -connect try.count.ly:443 -showcerts</pre>
<p>
  Run the above command and copy the content inside the begin certificate and the
  end certificate.
</p>
<p>
  Example files:
  <a href="https://github.com/Countly/countly-sdk-react-native-bridge/blob/dev-nicolson/example/android.count.ly.cer" target="_blank" rel="noopener">Android</a>
  and
  <a href="https://github.com/Countly/countly-sdk-react-native-bridge/blob/dev-nicolson/example/ios.count.ly.cer" target="_blank" rel="noopener">iOS</a>.
  Note that Android needs the certificate string, while iOS needs the entire .cer
  file.
</p>
<p>
  <strong>Android</strong>
</p>
<pre>cd AwesomeProject
ls
count.ly.cer
mkdir -p ./android/app/src/main/assets/
cp ./count.ly.cer ./android/app/src/main/assets/</pre>
<p>
  <strong>iOS</strong>
</p>
<pre>open ./ios/AwesomeProject.xcworkspace
Right click on AwesomeProject and select `New Group` (ScreenShot 1)
Name it `Resources`
Drag and Drop count.ly.cer file under that folder (ScreenShot 2)
Make sure copy bundle resources has your certificate (Screenshot 4).</pre>
<pre><img src="/hc/article_attachments/900002229303/Screenshot_2020-07-07_at_11.39.02_AM.png" alt="Screenshot_2020-07-07_at_11.39.02_AM.png">
<img src="/hc/article_attachments/900001515963/ScreenShot_Pinned_Certificate_1.png" alt="ScreenShot_Pinned_Certificate_1.png"></pre>
<p>
  <img src="/hc/article_attachments/900001515983/Screenshot_Pinned_Certificate_2.png" alt="Screenshot_Pinned_Certificate_2.png">
</p>
<pre><img src="/hc/article_attachments/900002229363/Screenshot_2020-07-07_at_11.39.40_AM.png" alt="Screenshot_2020-07-07_at_11.39.40_AM.png"></pre>
<p>
  <strong>JavaScript</strong>
</p>
<pre>Countly.pinnedCertificates("count.ly.cer");</pre>
<p>
  Note that <code class="JavaScript">count.ly.cer</code> is the name of the file.
  Replace this file with the one you have.
</p>
<h1>Other features</h1>
<h2>Custom Metrics</h2>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Minimum Countly SDK Version</span></strong>
  </p>
  <p>
    This feature is only supported by the minimum SDK version 20.11.7.
  </p>
</div>
<p>
  For overriding default metrics or adding extra ones that are sent with begin_session
  requests, you can use pass 'customMetric' Object to the function
  <code>Countly.setCustomMetrics(customMetric)</code>, 'customMetric' should be
  an Object with keys and values that are both Strings only. Note that the custom
  metrics should be set before initialization.
</p>
<pre><code class="JavaScript">var customMetric = {"key": "value"};
Countly.setCustomMetrics(customMetric);</code></pre>
<p>
  For overriding default metrics, keys should be one of the below String value's:
</p>
<pre>"_device"<br>"_device_type"<br>"_os"<br>"_os_version"<br>"_app_version"<br>"_carrier"<br>"_resolution"<br>"_density"<br>"_locale"</pre>
<p>Example to override 'Carrier' and 'App Version'</p>
<pre><code class="JavaScript">var customMetric = {"_carrier": "custom carrier", "_app_version": "2.1"};
Countly.setCustomMetrics(customMetric);</code></pre>
<h2>Attribution analytics &amp; install campaigns</h2>
<p>
  <a href="https://count.ly/attribution-analytics">Countly Attribution Analytics</a>
  allows you to measure the performance of your marketing campaign by attributing
  installs from specific campaigns. This feature is available for the Enterprise
  Edition.
</p>
<p>
  For version 20.11.4 and greater we highly recommend allowing Countly to listen
  to the <strong>INSTALL_REFERRER</strong> intent in order to receive more precise
  attribution on Android, something you may do by adding the following XML code
  to your <strong>AndroidManifest.xml</strong> file inside the
  <strong>application</strong> tag.
</p>
<pre><code class="xml">&lt;receiver android:name="ly.count.android.sdk.ReferrerReceiver" android:exported="true"&gt;
	&lt;intent-filter&gt;
		&lt;action android:name="com.android.vending.INSTALL_REFERRER" /&gt;
	&lt;/intent-filter&gt;
&lt;/receiver&gt;</code></pre>
<p>
  <strong>For more information about how to set up your campaigns, please <a href="http://resources.count.ly/docs/referral-analytics">review this documentation</a>.</strong>
</p>
<p>Call the method below before initialization.</p>
<pre>// Enable to measure your marketing campaign performance by attributing installs from specific campaigns.
Countly.enableAttribution();</pre>
<p>
  For iOS 14+ use the
  <code class="JavaScript">recordAttributionID("IDFA")</code> function instead
  of <code class="JavaScript">Countly.enableAttribution()</code>
</p>
<p>
  You can use <code class="JavaScript">Countly.recordAttributionID</code> function
  to specify IDFA for campaign attribution
</p>
<pre>Countly.recordAttributionID("IDFA_VALUE_YOU_GET_FROM_THE_SYSTEM");</pre>
<p>
  For iOS 14+ due to Apple changes regarding Application Tracking, you need to
  ask the user for permission to track the Application.
</p>
<p>
  For IDFA you can use this Plugin, which also supports iOS 14+ changes for Application
  tracking permission:
  <a href="https://github.com/ijunaid/react-native-advertising-id.git">https://github.com/ijunaid/react-native-advertising-id.git</a>
</p>
<p>
  Here is how to use this plugin with the Countly attribution feature:
</p>
<div>
  <pre>npm install --save <a href="https://github.com/ijunaid/react-native-advertising-id.git">https://github.com/ijunaid/react-native-advertising-id.git</a>

cd ./ios
pod install

<strong>NSUserTrackingUsageDescription</strong>
Add "Privacy - Tracking Usage Description" in your ios info.plist file.

<strong>#Example Code for Countly attribution feature to support iOS 14+.</strong>

import RNAdvertisingId from 'react-native-advertising-id';

if (Platform.OS.match("ios")) {
RNAdvertisingId.getAdvertisingId()
.then(response =&gt; {
Countly.recordAttributionID(response.advertisingId);
})
.catch(error =&gt; console.error(error));
}
else {
Countly.enableAttribution(); // Enable to measure your marketing campaign performance by attributing installs from specific campaigns.
}</pre>
</div>
<h2>Forcing HTTP POST</h2>
<p>
  If the data sent to the server is short enough, the SDK will use HTTP GET requests.
  In the event you would like an override so that HTTP POST may be used in all
  cases, call the <code class="JavaScript">setHttpPostForced</code> function after
  you have called <code class="JavaScript">init</code>. You may use the same function
  later in the app’s life cycle to disable the override. This function has to be
  called every time the app starts, using the method below.
</p>
<pre><code class="javascript">  
// enabling the override
Countly.setHttpPostForced(true);
  
// disabling the override
Countly.setHttpPostForced(false);</code></pre>
<h2>Checking if init has been called</h2>
<p>
  In the event you would like to check if init has been called, use the function
  below.
</p>
<pre><code class="javascript">Countly.isInitialized().then(result =&gt; console.log(result)); // true or false
</code></pre>
<h2>Checking if onStart has been called</h2>
<p>
  For some applications, there might be a use case where the developer would like
  to check if the Countly SDK onStart function has been called. To do so, use the
  call below.
</p>
<pre><code class="javascript">Countly.hasBeenCalledOnStart().then(result =&gt; console.log(result)); // true or false </code></pre>
<h2>Interacting with the internal request queue</h2>
<p>
  When recording events or activities, the requests don't always get sent immediately.
  Events get grouped together. All the requests contain the same app key which
  is provided in the <code class="JavaScript">init</code> function.
</p>
<p>
  There are two ways to interact with the app key in the request queue at the moment.
</p>
<p>
  1. You can replace all requests with a different app key with the current app
  key:
</p>
<pre>//Replaces all requests with a different app key with the current app key.
Countly.replaceAllAppKeysInQueueWithCurrentAppKey();</pre>
<p>
  In the request queue, if there are any requests whose app key is different than
  the current app key, these requests app key will be replaced with the current
  app key. 2. You can remove all requests with a different app key in the request
  queue:
</p>
<pre>//Removes all requests with a different app key in request queue.
Countly.removeDifferentAppKeysFromQueue();</pre>
<p>
  In the request queue, if there are any requests whose app key is different than
  the current app key, these requests will be removed from the request queue.
</p>
<h2>Setting an event queue threshold</h2>
<p>
  Events get grouped together and are sent either every minute or after the unsent
  event count reaches a threshold. By default it is 10. If you would like to change
  this, call:
</p>
<pre>Countly.setEventSendThreshold(6);</pre>