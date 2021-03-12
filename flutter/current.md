<div class="callout callout--warning">
  <p class="callout__title">
    <span class="wysiwyg-font-size-large">Documentation Version</span>
  </p>
  <p>This documentation applies to version 20.11.0.</p>
  <p>
    To access the documentation for versions 20.04 and older, click
    <a href="/hc/en-us/articles/900005264923" target="_self" rel="undefined">here.</a>
  </p>
</div>
<p>
  This document includes the necessary information for integrating Countly Flutter
  SDK in your application. Flutter SDK requires Android and iOS SDKs, hence all
  the features and limitations regarding those platforms also apply to Countly
  Flutter SDK.
</p>
<p>
  <strong>Supported Platforms:</strong><span>&nbsp;Countly SDK supports iOS and Android.</span>
</p>
<p>
  Below you can see steps to download a Flutter example application:
</p>
<pre><code class="shell">git clone https://github.com/Countly/countly-sdk-flutter-bridge.git
cd countly-sdk-flutter-bridge/example
flutter pub get
flutter run</code></pre>
<p>
  This example application has all the methods mentioned in this documentation.
  It is a great way of understanding how different methods work, like custom events,
  custom user profiles and views.
</p>
<h1 id="adding-the-sdk-to-the-project" class="anchor-heading">Adding the SDK to the project</h1>
<p>
  Add this to your package's <code>pubspec.yaml</code> file:
</p>
<pre><code class="yaml">dependencies:
  countly_flutter:
    git: 
      url: https://github.com/Countly/countly-sdk-flutter-bridge.git
      ref: master
</code></pre>
<p>
  You can install packages from the command line with Flutter:
</p>
<pre><code class="shell">flutter pub get</code></pre>
<h1 id="setting-up-the-countly-sdk" class="anchor-heading">SDK Integration</h1>
<p>
  Below you can find necessary code snippets to initialize the SDK for sending
  data to Countly servers. Where possible, use your server URL instead of
  <code>try.count.ly</code> in case you have your own server.
</p>
<p>
  The shortest way to initiate the SDK if you want Countly SDK to take care of
  device ID seamlessly, use the code below. You can find your app key on your Countly
  dashboard, under the "Applications" menu item.
</p>
<pre>Countly.<span>isInitialized</span>().then((bool isInitialized){<br>      <span>if</span>(!isInitialized){<br>        <span>/// Recommended settings for Countly initialisation<br></span><span>        </span>Countly.<span>setLoggingEnabled</span>(<span>true</span>); <span>// Enable countly internal debugging logs<br></span><span>        </span>Countly.<span>enableCrashReporting</span>(); <span>// Enable crash reporting to report unhandled crashes to Countly<br></span><span>        </span>Countly.<span>setRequiresConsent</span>(<span>true</span>); <span>// Set that consent should be required for features to work.<br></span><span>        </span>Countly.<span>giveConsentInit</span>([<span>"location"</span>, <span>"sessions"</span>, <span>"attribution"</span>, <span>"push"</span>, <span>"events"</span>, <span>"views"</span>, <span>"crashes"</span>, <span>"users"</span>, <span>"push"</span>, <span>"star-rating"</span>, <span>"apm"</span>, <span>"feedback"</span>, <span>"remote-config"</span>]);<br>        Countly.<span>setLocationInit</span>(<span>"TR"</span>, <span>"Istanbul"</span>, <span>"41.0082,28.9784"</span>, <span>"10.2.33.12"</span>);<span>// Set user initial location.</span><span><br></span><br>        Countly.<span>init</span>(<span>SERVER_URL</span>, <span>APP_KEY </span>).then((value){<br>          Countly.<span>appLoadingFinished</span>();<br>          Countly.<span>start</span>();<span><br></span><span>        </span>}); <span>// Initialize the countly SDK.<br></span><span>      </span>}<span>else</span>{<br>        print(<span>"Countly: Already initialized."</span>);<br>      }<br>    });</pre>
<p>
  <strong><span class="wysiwyg-font-size-large">Providing the application key</span></strong>
</p>
<p>
  <span>Also called "appKey" as shorthand. The application key is used to identify for which application this information is tracked. You receive this value by creating a new application in your Countly dashboard and accessing it in its application management screen.</span>
</p>
<p>
  <span><strong>Note:&nbsp;</strong>Ensure you are using the App Key (found under Management -&gt; Applications) and not the API Key. Entering the API Key will not work.</span>
</p>
<p id="providing-the-server-url" class="anchor-heading">
  <strong><span class="wysiwyg-font-size-large">Providing the server URL</span></strong>
</p>
<p>
  <span>If you are using Countly Enterprise Edition trial servers, use&nbsp;<code>https://try.count.ly</code>,&nbsp;<code>https://us-try.count.ly</code>&nbsp;or&nbsp;<code>https://asia-try.count.ly</code>&nbsp;It is basically the domain from which you are accessing your trial dashboard.</span>
</p>
<p>
  <span>If you use both Community Edition and Enterprise Edition, use your own domain name or IP address, such as&nbsp;</span><a href="https://example.com/"><span>https://example.com</span></a><span>&nbsp;or&nbsp;</span><a href="https://ip/"><span>https://IP</span></a><span>&nbsp;(if SSL has been set up).</span>
</p>
<h2>Enable logging</h2>
<p>
  If logging is enabled then our SDK will print out debug messages about its internal
  state and encountered problems.
</p>
<p>
  We advise doing this while implementing Countly features in your application.
</p>
<pre><code class="javascript">Countly.setLoggingEnabled(true);</code></pre>
<h2>Device ID</h2>
<p>
  <span style="font-weight:400"><span>When the SDK is initialized for the first time and no device ID is provided, a device ID will be generated by SDK.</span></span><span style="font-weight:400"><span></span></span>
</p>
<p>
  <span style="font-weight:400"><span>For iOS: the device ID generated by SDK is the Identifier For Vendor (IDFV)<br>For Android:&nbsp; the device ID generated by SDK is the OpenUDID or Google Advertising ID</span></span>
</p>
<p>
  <span style="font-weight:400"><span>You may provide your own custom device ID when</span> initializing the SDK</span>
</p>
<pre>Countly.<span>init</span>(<span>SERVER_URL</span>, <span>APP_KEY, DEVICE_ID</span>)</pre>
<h2 class="anchor-heading">SDK data storage</h2>
<p>
  For iOS: SDK data is stored in Application Support Directory in file named "<span>Countly.dat</span>"&nbsp;<br>
  For Android: SDK data is stored in
  <span>SharedPreferences. A SharedPreferences object points to a file containing key-value pairs and provides simple methods to read and write them.</span>
</p>
<h1>Crash reporting</h1>
<p>
  This feature allows the Countly SDK to record crash reports of either encountered
  issues of exceptions which cause your application to crash. Those reports will
  be sent to your Countly server for further inspection.
</p>
<p>
  If a crash report can not be delivered to the server (e.g. no internet connection,
  unavailable server), then SDK stores the crash report locally in order to try
  again later.
</p>
<h2>Automatic crash handling</h2>
<p>
  If you want to enable automatic unhandled crash reporting, you need to call this
  before init:
</p>
<pre>Countly.<span>enableCrashReporting</span>()</pre>
<p>
  By doing that it will automatically catch all errors that are thrown from within
  the Flutter framework.
</p>
<p>
  <br>
  If you want to catch Dart errors,&nbsp;<span>run your app inside a&nbsp;Zone and&nbsp;</span>supply&nbsp;<code>Countly.recordDartError</code>&nbsp;to
  the&nbsp;<code>onError</code>&nbsp;parameter:
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Minimum Countly SDK Version</span></strong>
  </p>
  <p>
    This feature is only supported by the minimum SDK version 20.04.1.
  </p>
</div>
<pre><span>void </span>main() {<br>  runZonedGuarded&lt;Future&lt;<span>void</span>&gt;&gt;(() <span>async </span>{<br>    runApp(<span>MyApp</span>());<br>  }, Countly.<span>recordDartError</span>);<br>}<span></span></pre>
<h2>Automatic crash report segmentation</h2>
<p>
  <span style="font-weight:400">You may add a key/value segment to crash reports. For example, you could set which specific library or framework version you used in your app. You may then figure out if there is any correlation between the specific library or another segment and the crash reports.</span><span style="font-weight:400"></span>
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Minimum Countly SDK Version</span></strong>
  </p>
  <p>
    This feature is only supported by the minimum SDK version 20.04.1.
  </p>
</div>
<p>
  <span style="font-weight:400">The following call will add the provided segmentation to all recorded crashes. Use the following function for this purpose:</span>
</p>
<pre><span>Countly.setCustomCrashSegment</span>(Map&lt;String, Object&gt; segments);</pre>
<h2>Handled exceptions</h2>
<p class="p1">
  There are multiple ways you could report a handled exception/error to Countly.
</p>
<p class="p1">
  This call does not add a stacktrace automatically&nbsp;if it's needed, it should
  already be added to the exception variable, a&nbsp;potential use case would be
  to provide <code>exception.toString()</code>
</p>
<pre><span>Countly.logException</span>(String exception, bool nonfatal, [Map&lt;String, Object&gt; segmentation])</pre>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Minimum Countly SDK Version</span></strong>
  </p>
  <p>
    The following calls are only supported starting from the SDK version 20.04.1.
  </p>
</div>
<p>
  The issue is recorded with a provided Exception object. If no stacktrace is set,<span class="s1"><code>StackTrace.current</code></span>&nbsp;will
  be used.
</p>
<pre><span>Countly.logExceptionEx</span>(Exception exception, bool nonfatal, {StackTrace stacktrace, Map&lt;String, Object&gt; segmentation})</pre>
<p class="p1">
  The exception/error is recorded through a string message. If no stack trace is
  provided,&nbsp;<span class="s1">&nbsp;<code>StackTrace.current</code></span>&nbsp;will
  be used.
</p>
<pre><span>Countly.logExceptionManual</span>(String message, bool nonfatal, {StackTrace stacktrace, Map&lt;String, Object&gt; segmentation})</pre>
<h2>Crash breadcrumbs</h2>
<p>
  Throughout your app, you can leave&nbsp;crash breadcrumbs which would describe
  previous steps that were taken in your app before the crash. After a crash happens,
  they will be sent together with the crash report.
</p>
<p>Following the command adds crash breadcrumb:</p>
<pre>Countly.<span>addCrashLog</span>(<span>String logs</span>)</pre>
<h1>Custom events</h1>
<p>
  A custom event is any type of action that you can send to a Countly instance,
  e.g purchase, settings changed, view enabled and so. This way it's possible to
  get much more information from your application compared to what is sent from
  Flutter SDK to Countly instance by default.
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Data passed should be in UTF-8</span></strong>
  </p>
  <p>
    All data passed to the Countly server via SDK or API should be in UTF-8.
  </p>
</div>
<h2>Recording events</h2>
<p>
  We will be recording a purchase event. Here is a quick summary of what information
  each usage will provide us:
</p>
<ul>
  <li>Usage 1: how many times a purchase event occurred.</li>
  <li>
    Usage 2: how many times purchase event occurred + the total amount of those
    purchases.
  </li>
  <li>
    Usage 3: how many times purchase event occurred + which countries and application
    versions those purchases were made from.
  </li>
  <li>
    Usage 4: how many times a purchase event occurred + the total amount both
    of which are also available segmented into countries and application versions.
  </li>
  <li>
    Usage 5: how many times purchase event occurred + the total amount both of
    which are also available segmented into countries and application versions
    + the total duration of those events (under Timed Events topic below)
  </li>
</ul>
<p>
  <span class="wysiwyg-font-size-large">1. Event key and count</span>
</p>
<pre><code class="javascript">// example for sending basic custom event
var event = {
  "key": "Basic Event",
  "count": 1
};
Countly.recordEvent(event);</code></pre>
<p>
  <span class="wysiwyg-font-size-large">2. Event key, count and sum</span>
</p>
<pre><code class="javascript">// example for event with sum
var event = {
  "key": "Event With Sum",
  "count": 1,
  "sum": "0.99",
};
Countly.recordEvent(event);
</code></pre>
<p>
  <span class="wysiwyg-font-size-large">3. Event key and count with segmentation(s)</span>
</p>
<pre><code class="javascript">// example for event with segment
var event = {
  "key": "Event With Segment",
  "count": 1
};
event["segmentation"] = {
  "Country": "Germany",
  "Age": "28"
};
Countly.recordEvent(event);
</code></pre>
<p>
  <span class="wysiwyg-font-size-large">4. Event key, count and sum with segmentation(s)</span>
</p>
<pre><code class="javascript">
// example for event with segment and sum
var event = {
  "key": "Event With Sum And Segment",
  "count": 1,
  "sum": "0.99"
};
event["segmentation"] = {
  "Country": "Germany",
  "Age": "28"
};
Countly.recordEvent(event);
</code></pre>
<h2>Timed events</h2>
<p>
  <span class="wysiwyg-font-size-large">1.Timed event with key</span>
</p>
<pre><code class="javascript">// Basic event
Countly.startEvent("Timed Event");
Timer timer;
timer = new Timer(new Duration(seconds: 5), () {
    Countly.endEvent({ "key": "Timed Event" });
    timer.cancel();
});
</code></pre>
<p>
  <span class="wysiwyg-font-size-large">2.Timed event with key and sum</span>
</p>
<pre><code class="javascript">// Event with sum
Countly.startEvent("Timed Event With Sum");
Timer timer;
timer = new Timer(new Duration(seconds: 5), () {
    Countly.endEvent({ "key": "Timed Event With Sum", "sum": "0.99" });
    timer.cancel();
});
</code></pre>
<p>
  <span class="wysiwyg-font-size-large">3.Timed event with key, count and segmentation</span>
</p>
<pre><code class="javascript">// Event with segment
Countly.startEvent("Timed Event With Segment");
Timer timer;
timer = new Timer(new Duration(seconds: 5), () {
    var event = {
        "key": "Timed Event With Segment",
        "count": 1,
    };
    event["segmentation"] = {
      	"Country": "Germany",
      	"Age": "28"
    };
    Countly.endEvent(event);
    timer.cancel();
});</code></pre>
<p>
  <span class="wysiwyg-font-size-large">4.Timed event with key, count, sum and segmentation</span>
</p>
<pre><code class="javascript">// Event with Segment, sum and count
Countly.startEvent("Timed Event With Segment, Sum and Count");
Timer timer;
timer = new Timer(new Duration(seconds: 5), () {
    var event = {
        "key": "Timed Event With Segment, Sum and Count",
        "count": 1,
        "sum": "0.99"
    };
    event["segmentation"] = {
        "Country": "Germany",
        "Age": "28"
    };
    Countly.endEvent(event);
    timer.cancel();
});</code></pre>
<h1>Sessions</h1>
<p>To start recording a session you would start it with:</p>
<pre><code class="javascript">Countly.start();</code></pre>
<p>
  If you want to end recording the current session, you would call:
</p>
<pre><code class="javascript">Countly.stop();</code></pre>
<h1>View tracking</h1>
<h2>Manual view recording</h2>
<p>
  You can manually add your own views in your application, and each view will be
  visible under Views menu item. Below you can see two examples of sending a view
  using <code>Countly.recordview</code> function.
</p>
<pre><code class="javascript">// record a view on your application
Countly.recordView("HomePage");
Countly.recordView("Dashboard");</code></pre>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Minimum Countly SDK Version</span></strong>
  </p>
  <p>
    This feature is only supported by the minimum SDK version 20.04.1.
  </p>
</div>
<p>
  While manually tracking views, you may want to add custom segmentation to them.
</p>
<pre>Map&lt;String, Object&gt; segments = {<br>  <span>"Cats"</span>: <span>123</span>,<br>  <span>"Moons"</span>: <span>9.98</span>,<br>  <span>"Moose"</span>: <span>"Deer"<br></span>};<br>Countly.<span>recordView</span>(<span>"HomePage"</span>, segments);</pre>
<h1>Device ID management</h1>
<h2>
  Changing the Device ID<span style="font-weight:400"></span>
</h2>
<p>
  <span style="font-weight:400">You may configure/change the device ID anytime using:<br></span>
</p>
<pre>Countly.<span>changeDeviceId</span>(DEVICE_ID, <span>ON_SERVER</span>);</pre>
<p>
  <span>You may either allow the device to be counted as a new device or merge existing data on the server. </span>If
  the<code>onServer</code><span>&nbsp;</span>bool is set to <code>true</code>,
  <span>the old device ID on the server will be replaced with the new one, and data associated with the old device ID will be merged automatically.<br>Otherwise, if&nbsp;<code>onServer</code> bool is&nbsp;set to <code>false</code>, the device will be counted as a new device on the server.<br></span>
</p>
<h2 id="temporary-device-id" class="anchor-heading">Temporary Device ID</h2>
<p>
  You may use a temporary device ID mode for keeping all requests on hold until
  the real device ID is set later.&nbsp;
</p>
<p>
  You can enable temporary device ID
  <span style="font-weight:400">when initializing the SDK:</span>
</p>
<pre>Countly.<span>init</span>(<span>SERVER_URL</span>, <span>APP_KEY, Countly.deviceIDType["TemporaryDeviceID"]</span>)</pre>
<p>To enable a temporary device ID after init, you would call:</p>
<pre>Countly.<span>changeDeviceId</span>(Countly.deviceIDType["TemporaryDeviceID"], <span>ON_SERVER</span>);</pre>
<p>
  &nbsp;<strong>Note:</strong>&nbsp;When passing<span> </span><code>TemporaryDeviceID</code><span>&nbsp;</span>for<span>&nbsp;</span><code>deviceID</code><span>&nbsp;</span>parameter,
  argument for<span>&nbsp;</span><code>onServer</code>parameter does not matter.
</p>
<p>
  As long as the device ID value is<span> </span><code>TemporaryDeviceID</code>,
  the SDK will be in temporary device ID mode and all requests will be on hold,
  but they will be persistently stored.
</p>
<p>
  When in temporary device ID mode, method calls for presenting feedback widgets
  and updating remote config will be ignored.
</p>
<p>
  Later, when the real device ID is set using<span> </span><code>Countly.<span>changeDeviceId</span>(DEVICE_ID, <span>ON_SERVER</span>);</code><span>&nbsp;</span>method,
  all requests which have been kept on hold until that point will start with the
  real device ID
</p>
<h1>Push notifications</h1>
<h2>Android setup</h2>
<p>
  Step 1: Hope you have created your flutter app, and installed countly_flutter
  package.
</p>
<p>
  Step 2: Make sure you have <code>google-services.json</code> from
  <a href="https://firebase.google.com/">https://firebase.google.com/</a>
</p>
<p>
  Step 3: Make sure the app package name and the
  <code>google-services.json</code> <code>package_name</code> matches.
</p>
<p>
  Step 4: Place the <code>google-services.json</code> file inside
  <code>android/app</code>
</p>
<p>
  Step 5: Add the following line in file
  <code>android/app/src/main/AndroidManifest.xml</code> inside
  <code>application</code> tag.
</p>
<pre><code class="xml">&lt;service android:name="ly.count.dart.countly_flutter.CountlyMessagingService"&gt;
    &lt;intent-filter&gt;
        &lt;action android:name="com.google.firebase.MESSAGING_EVENT" /&gt;
    &lt;/intent-filter&gt;
&lt;/service&gt;
</code></pre>
<p>
  Step 7: Use the latest version from this link
  <a href="https://firebase.google.com/support/release-notes/android#latest_sdk_versions">https://firebase.google.com/support/release-notes/android#latest_sdk_versions</a>
  and this link
  <a href="https://developers.google.com/android/guides/google-services-plugin">https://developers.google.com/android/guides/google-services-plugin</a>
</p>
<p>
  Step 6: Add the following line in file <code>android/build.gradle</code>
</p>
<pre><code class="JavaScript">buildscript {
    dependencies {
        classpath 'com.google.gms:google-services:4.3.2'
    }
}
</code></pre>
<p>
  Step 7: Add the following line in file <code>android/app/build.gradle</code>
</p>
<pre><code class="JavaScript">dependencies {
    implementation 'ly.count.android:sdk:20.04'
    implementation 'com.google.firebase:firebase-messaging:20.0.0'
}
// Add this at the bottom of the file
apply plugin: 'com.google.gms.google-services'
</code></pre>
<h2>iOS setup</h2>
<p>
  By default push notification is enabled for iOS, to disable you need to call
  <code>disablePushNotifications</code> method:
</p>
<pre><span>// // Disable push notifications feature for iOS, by default it is enabled.</span><br>Countly.disablePushNotifications();</pre>
<p>
  For iOS push notification please follow the instruction from this URL
  <a href="https://resources.count.ly/docs/countly-sdk-for-ios-and-os-x#section-push-notifications">https://resources.count.ly/docs/countly-sdk-for-ios-and-os-x#section-push-notifications</a>
</p>
<p>
  For Flutter you can find <code>CountlyNotificationService.h/m</code> file under
  <code>Pods/Development Pods/Countly/{PROJECT_NAME}/ios/.symlinks/plugins/countly_flutter/ios/Classes/CountlyiOS/CountlyNotificationService.h/m</code><br>
  <br>
  <strong>Pro Tips to find the files from deep hierarchy:<br></strong>
</p>
<ul>
  <li>
    You can filter the files in the navigator using a shortcut ⌥⌘J (Option-Command-J),
    in the filter box type "CountlyNotificationService" and it will show the
    related files only.
  </li>
  <li>
    <span>&nbsp;You can find the file using the shortcut</span><span> ⇧⌘O (Shift-Command-O) and then navigate to that file using the shortcut ⇧⌘J (Shift-Command-J)<br><br></span>
  </li>
</ul>
<p>You can drag and drop the file from Pod to Compile Sources.</p>
<div class="img-container">
  <img src="/hc/article_attachments/900005820306/Flutter_iOS_Notifications.png" alt="Flutter_iOS_Notifications.png">
</div>
<h2>General setup</h2>
<p>
  First, when setting up push for the Flutter SDK, you would first select the push
  token mode. This would allow you to choose either test or production modes, push
  token mode should be set before init.
</p>
<pre><span>// Set messaging mode for push notifications</span><br>Countly.<span>pushTokenType</span>(Countly.<span>messagingMode</span>[<span>"TEST"</span>]);<span></span><span></span></pre>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Minimum Countly SDK Version</span></strong>
  </p>
  <p>
    This feature is only supported by the minimum SDK version 20.04.1.
  </p>
</div>
<p>
  You may want to listen to a callback of when a push notification is received.
  You would register to that like this:
</p>
<pre><span>// Set callback to receive push notifications</span><br>Countly.<span>onNotification</span>((String notification){<br>  print(<span>"The notification"</span>);<br>  print(notification);<br>});<span> </span></pre>
<p>
  When you are finally ready to initialise Countly push, you would call this:
</p>
<pre><span>// This method will ask for permission, enables push notification and send push token to countly server.;<br>Countly.askForNotificationPermission();</span></pre>
<h1>User Location</h1>
<p>
  <span>Countly allows you to send geolocation-based push notifications to your users. By default, the Countly Server uses the GeoIP database to deduce a user's location. </span>
</p>
<h2>Set User Location</h2>
<p>
  <span>If your app has a different way of detecting location, you may send this information to the Countly Server by using the <code>setLocationInit</code>&nbsp;or<code>setLocation</code> methods.</span>
</p>
<p>
  <span>We recommend using the <code>setLocationInit</code> method before initialization to sent location. This includes:</span>
</p>
<ul>
  <li>
    <code><span>countryCode</span></code><span>&nbsp;</span>a string in ISO 3166-1
    alpha-2 format country code
  </li>
  <li>
    <code>city</code><span>&nbsp;</span>a string specifying city name
  </li>
  <li>
    <code>location</code><span>&nbsp;</span>a string comma-separated latitude
    and longitude
  </li>
  <li>
    <code>IP</code><span>&nbsp;</span>a string specifying an IP address in IPv4
    or IPv6 formats
  </li>
</ul>
<pre><code class="javascript">// Example for setLocationInit
Countly.<span>setLocationInit</span>(<span>"TR"</span>, <span>"Istanbul"</span>, <span>"41.0082,28.9784"</span>, <span>"10.2.33.12"</span>);</code></pre>
<p>
  <span style="font-weight:400"><span>Geolocation recording methods may also be called at any time after the Countly SDK has started.<br>To do so, use the <code>setLocation</code> method as shown below.</span></span><span style="font-weight:400"></span>
</p>
<pre><code class="javascript">// Example for setLocation
Countly.setLocation(latitude, longitude);
</code></pre>
<h2>Disable Location</h2>
<p>
  <span style="font-weight:400">To erase any cached location data from the device and stop further location tracking, use the following method. Note that i</span><span style="font-weight:400">f after disabling location, the <code>setLocation</code></span><span style="font-weight:400">is called with any non-null value, tracking will resume.</span>
</p>
<pre><code class="javascript">//disable location tracking
Countly.disableLocation();</code></pre>
<h1>Remote config</h1>
<p>
  Remote config allows you to modify how your app functions or looks by requesting
  key-value pairs from your Countly server. The returned values can be modified
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
  before init. As an optional value you can provide a callback to be informed when
  the request is finished.
</p>
<pre><code class="javascript">Countly.setRemoteConfigAutomaticDownload((result){
	print(result);
});</code></pre>
<p>
  If the callback returns a non-null value, then you can expect that the request
  failed and no values were updated.
</p>
<p>
  When doing an automatic update, all locally stored values are replaced with the
  ones received (all locally stored ones are deleted and in their place are put
  new ones). It is possible that a previously valid key returns no value after
  an update.
</p>
<h2>Manual remote config</h2>
<p>
  There are three ways for manually requesting remote config update:
</p>
<ul>
  <li>Manually updating everything</li>
  <li>Manually updating specific keys</li>
  <li>Manually updating everything except specific keys</li>
</ul>
<p>
  Each of these requests also has a callback. If that returns a non-null value,
  the request encountered some error and failed.
</p>
<p>
  Functionally the manual update for everything <code>remoteConfigUpdate</code>
  is the same as the automatic update - replaces all stored values with the ones
  from the server (all locally stored ones are deleted and in their place are put
  new ones). The advantage is that you can make the request whenever it is desirable
  for you. It has a callback to let you know when it has finished.
</p>
<pre><code class="javascript">Countly.remoteConfigUpdate((result){
	print(result);
});</code></pre>
<p>
  You might want to update only specific key values. For that you need to call
  <code>updateRemoteConfigForKeysOnly</code> with a list of keys you want to be
  updated. That list is an array with string values of those keys. It has a callback
  to let you know when the request has finished.
</p>
<pre><code class="javascript">Countly.updateRemoteConfigForKeysOnly(["name"],(result){
	print(result);
});</code></pre>
<p>
  You might want to update all values except a few defined keys, for that call
  <code>updateRemoteConfigExceptKeys</code>. The key list is an array with string
  values of the keys. It has a callback to let you know when the request has finished.
</p>
<pre><code class="javascript">Countly.updateRemoteConfigExceptKeys(["url"],(result){
	print(result);
});</code></pre>
<p>
  When making requests with an "inclusion" or "exclusion" array, if those arrays
  are empty or null, they will function the same as a simple manual request and
  will update all values. This means that it will also erase all keys not returned
  by the server.
</p>
<h2>Getting remote config values</h2>
<p>
  To request a stored value, call getRemoteConfigValueForKey with the specified
  key. If it returns null then no value was found. The SDK has no knowledge of
  the returned value type and therefore returns an Object. The developer needs
  to cast it to the appropriate type. The returned values can also be a JSONArray,
  JSONObject or just a simple value like int.
</p>
<pre><code class="javascript">Countly.getRemoteConfigValueForKey("name", (result){
	print(result);
});</code></pre>
<h2>Clearing stored remote config values</h2>
<p>
  At some point you might want to erase all values downloaded from the server.
  To achieve that you need to call one function.
</p>
<pre><code class="javascript">Countly.remoteConfigClearValues((result){
	print(result);
});</code></pre>
<h1>User feedback</h1>
<p>
  <span style="font-weight:400">There are a couple ways of receiving feedback from your users: star-rating dialog, the rating widget and the feedback widgets (survey, nps).</span>
</p>
<p>
  <span style="font-weight:400">Star-rating dialog allows users to give feedback as a rating from 1 to 5. The rating widget allows users to rate using the same 1 to 5 rating system as well as leave a text comment. Feedback widgets (survey, nps) allow for even more textual feedback from users.</span>
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
  It is just for getting brief feedback from users, to be displayed on the Countly
  dashboard. If the user dismisses star rating dialog without giving a rating,
  the event will not be recorded.
</p>
<pre><code class="javascript">Countly.askForStarRating();</code></pre>
<p>
  The star-rating dialog's title, message, and dismiss button text may be customized
  either through <code>setStarRatingDialogTexts</code> function.&nbsp;
</p>
<pre><code class="javascript">Countly.setStarRatingDialogTexts("Custom title", "Custom message", "Custom dismiss button text");</code></pre>
<h2>Rating widget</h2>
<p>
  Feedback widget shows a server configured widget to your user devices.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/c928493-feedback_widget.png">
</div>
<p>
  It's possible to configure any of the shown text fields and replace them with
  a custom string of your choice.
</p>
<p>
  In addition to a 1 to 5 rating, it is possible for users to leave a text comment
  and also leave an email in case the user would want some contact from the app
  developer.
</p>
<p>
  Trying to show the rating widget is a single call, but underneath is a two-step
  process. Before it is shown, the SDK tries to contact the server to get more
  information about the dialog. Therefore a network connection to it is needed.
</p>
<p>
  You can try to show the widget after you have initialized the SDK. To do that,
  you first have to get the widget ID from your server:
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/dee9bfc-feedback2.png">
</div>
<p>
  Using that you can call the function to show the widget popup:
</p>
<pre><code class="javascript">Countly.askForFeedback("5da0877c31ec7124c8bf398d", "Close");</code></pre>
<h2>Feedback widget</h2>
<p>
  It is possible to display 2 kinds of Surveys widgets:
  <a href="https://support.count.ly/hc/en-us/articles/900003407386-NPS-Net-Promoter-Score-" target="_blank" rel="noopener">NPS</a>
  and
  <a href="https://support.count.ly/hc/en-us/articles/900004337763-Surveys" target="_blank" rel="noopener">Surveys</a>.
  Both widgets are shown as webviews and they both use the same code methods.&nbsp;
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
<pre><code class="javascript">FeedbackWidgetsResponse feedbackWidgetsResponse = await Countly.getAvailableFeedbackWidgets() ;</code></pre>
<p>
  From the callback you would get
  <code class="javascript">FeedbackWidgetsResponse</code> objec which contains
  the list of all available widgets that apply to the current device id.
</p>
<p>The objects in the returned list look like this:</p>
<pre><span>class CountlyPresentableFeedback</span> {<br>    <span>public </span>String <span>widgetId</span>;<br>    <span>public String</span> <span>type</span>;<br>    <span>public </span>String <span>name</span>;<br>}</pre>
<p>
  <span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif">To determine what kind of widget that is, check the "type" value. The potential values are </span><code style="font-size:15px">"survey"</code><span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif"> and </span><code style="font-size:15px">"nps"</code><span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif">.</span>
</p>
<p>
  Then use the widget type and description (which is the same as provided in the
  Dashboard) to decide which widget to show.
</p>
<p>
  After you have decided which widget you want to display, call the function below.
</p>
<p>
  You would then use the widget type and description (which is the same as provided
  in the dashboard) to decide which widget to show.
</p>
<p>
  After you have decided which widget you want to display, you would provide that
  object to the following function:
</p>
<pre><code class="javascript">Countly.presentFeedbackWidget(chosenWidget, "CLOSE_BUTTON_TEXT");</code></pre>
<h2>Feedback widget manual reporting</h2>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Minimum Countly SDK Version</span></strong>
  </p>
  <p>
    This feature is only supported by the minimum SDK version 20.11.1
  </p>
</div>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Supported Platforms</span></strong>
  </p>
  <p>Currently this feature is only available for Android</p>
</div>
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
  of possible `CountlyPresentableFeedback` objects. You would pick the one widget
  you would want to display.
</p>
<p>
  Having the `CountlyPresentableFeedback` object of the widget you would want to
  display, you would use the following call to retrieve the widget information:
</p>
<pre>List result = await Countly.getFeedbackWidgetData(chosenWidget); {<br>    error = result[1];<br>    if(error == null) {<br>       Map&lt;String, dynamic&gt; retrievedWidgetData = result[0];<br>    }<br>}</pre>
<p>
  `retrievedWidgetData` would contain a Map with all of the required information
  to present the widget yourself.
</p>
<p>
  After you have collected the required information from your users, you would
  package the responses into a `Map&lt;String, Object&gt;` and then use it, the
  widgetInformation and the widgetData to report the feedback result with the following
  call:
</p>
<pre>//this contains the reported results<br>Map&lt;String, Object&gt; reportedResult = {};<br><br>//<br>// You would fill out the results here. That step is not displayed in this sample<br>//<br><br>//report the results to the SDK<br>Countly.reportFeedbackWidgetManually(chosenWidget, retrievedWidgetData , reportedResult);</pre>
<p>
  If the user would have closed the widget, you would report that by passaing a
  "null" reportedResult.
</p>
<h1>User Profiles</h1>
<p>
  In order to set a user profile, use the code snippet below. After you send user
  data, it can be viewed under the User Profiles menu.
</p>
<p>
  Note that this feature is available only for Enterprise Edition.
</p>
<pre><code class="javascript">// example for setting user data
Map&lt;String, Object&gt; options = {
    "name": "Nicola Tesla",
    "username": "nicola",
    "email": "info@nicola.tesla",
    "organization": "Trust Electric Ltd",
    "phone": "+90 822 140 2546",
    "picture": "http://images2.fanpop.com/images/photos/3300000/Nikola-Tesla-nikola-tesla-3365940-600-738.jpg",
    "picturePath": "",
    "gender": "M", // "F"
    "byear": "1919",
};
Countly.setUserData(options);</code></pre>
<p>
  In order to modify a user's data (e.g increment, etc), the following code sample
  can be used.
</p>
<h2>Modifying custom data</h2>
<p>
  Additionally, you can do different manipulations on your custom data values,
  like increment current value on the server or store an array of values under
  the same property.
</p>
<p>Below is the list of available methods:</p>
<pre><code class="javascript">
//set one custom properties
Countly.setProperty("setProperty", "My Property");
//increment used value by 1
Countly.increment("increment");
//increment used value by provided value
Countly.incrementBy("incrementBy", 10);
//multiply value by provided value
Countly.multiply("multiply", 20);
//save maximal value
Countly.saveMax("saveMax", 100);
//save minimal value
Countly.saveMin("saveMin", 50);
//set value if it does not exist
Countly.setOnce("setOnce", 200);

//insert value to array of unique values
Countly.pushUniqueValue("type", "morning");;
//insert value to array which can have duplocates
Countly.pushValue("type", "morning");
//remove value from array
Countly.pullValue("type", "morning");
</code></pre>
<h1>Application Performance Monitoring</h1>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Minimum Countly SDK Version</span></strong>
  </p>
  <p>
    This feature is only supported by the minimum SDK version 20.04.1.
  </p>
</div>
<p>
  This SDK provides a few mechanisms for APM. To start using them you would first
  need to enable this feature and give the required consent if it was required.
</p>
<pre>Countly.<span>enableApm</span>(); <span>// Enable APM features, which includes the recording of app start time.</span></pre>
<p>
  While using APM calls, you have the ability to provide trace keys by which you
  can track those parameters in your dashboard.
</p>
<h2 id="app-start-time" class="anchor-heading">App Start Time</h2>
<p>
  For the app start time to be recorded, you need to call the<span>&nbsp;</span><code>appLoadingFinished</code><span>&nbsp;</span>method.
  Make sure this method is called after <code>init</code>.
</p>
<pre><code class="javascript">// Example of appLoadingFinished
Countly.init(SERVER_URL, APP_KEY ).then((value){<br>Countly.appLoadingFinished();<br>});<br></code></pre>
<p>
  This calculates and records the app launch time for performance monitoring.<br>
  It should be called when the app is loaded and it successfully displayed its
  first user-facing view. The time passed since the app has started to launch will
  be automatically calculated and recorded for performance monitoring. Note that
  the app launch time can be recorded only once per app launch. So, the second
  and following calls to this method will be ignored.
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
<pre>Countly.<span>startTrace</span>(traceKey);</pre>
<p>To end a custom trace, use:</p>
<pre>String traceKey = <span>"Trace Key"</span>;<br>Map&lt;String, int&gt; customMetric = {<br>  <span>"ABC"</span>: <span>1233</span>,<br>  <span>"C44C"</span>: <span>1337<br></span>};<br>Countly.<span>endTrace</span>(traceKey, customMetric);</pre>
<p>
  The provided Map of integer values that will be added to that trace in the dashboard.
</p>
<h2>Network trace</h2>
<p>
  You can use the APM to track your requests. You would record the required info
  for your selected approach of making network requests and then call this after
  your network request is done:
</p>
<pre>Countly.<span>recordNetworkTrace</span>(networkTraceKey, responseCode, requestPayloadSize, responsePayloadSize, startTime, endTime);</pre>
<p>
  `networkTraceKey` is a unique identifier of the API endpoint you are targeting
  or just the url you are targeting, all params should be stripped. You would also
  provide the received response code, sent payload size in bytes, received payload
  size in bytes, request start time timestamp in milliseconds, and request end
  finish timestamp in milliseconds.
</p>
<h1>User consent</h1>
<p>
  <span>For compatibility with data protection regulations, such as GDPR, the Countly iOS SDK allows developers to enable/disable any feature at any time depending on user consent.</span>
  More information about GDPR
  <a href="https://blog.count.ly/countly-the-gdpr-how-worlds-leading-mobile-and-web-analytics-platform-can-help-organizations-5015042fab27">can be found here.</a>
</p>
<p>
  By default the requirement for consent is disabled. To enable it, you have to
  call <code>setRequiresConsent</code> with true, before initializing Countly.
</p>
<pre><code class="javascript">Countly.setRequiresConsent(true);</code></pre>
<p>
  By default no consent is given. That means that if no consent is enabled, Countly
  will not work and no network requests, related to features, will be sent. When
  the consent status of a feature is changed, that change will be sent to the Countly
  server.
</p>
<p>
  <span>The Countly SDK does not persistently store the status of given consents except push notifications. You are expected to handle receiving consent from end-users using proper UIs depending on your app's context. You are also expected to store them either locally or remotely. Following this step, you will need to call the<code>giveConsent/giveConsentInit</code> method on each app launch&nbsp;depending on the permissions you managed to get from the end-users.</span>
</p>
<p>
  The ideal location for giving consent is after&nbsp;<span><code>Countly.init</code>&nbsp;and before&nbsp;<code>Countly.start()</code>. Consent for features can be given and revoked at any time, but if it is given after<code>Countly.start()</code>&nbsp;, some features might work partially.</span>
</p>
<p>
  If consent is removed, but the appropriate function can't be called before the
  app closes, it should be done at next app start so that any relevant server-side
  features could be disabled (like reverse geo ip for location)
</p>
<p>
  <span>Currently, available features with consent control are as follows</span>:
</p>
<ul>
  <li>
    sessions - tracking when, how often and how long users use your app
  </li>
  <li>events - allow sending custom events to the server</li>
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
  <li>star-rating - allow sending their rating and feedback</li>
  <li>apm - allow application performance monitoring</li>
  <li>
    remoteConfig - allows downloading remote config values from your server
  </li>
</ul>
<h2>Giving consents</h2>
<p>
  <span>To give consent for features, you can use the <code>giveConsentInit</code>before <code>init</code>&nbsp;or <code>giveConsent</code> after <code>init</code> by passing the feature names </span><span>as an Array.<br>We recommend using the <code>giveConsentInit</code>because some features require consents before <code>init</code></span>
</p>
<pre><code class="javascript">Countly.giveConsentInit(["location", "sessions", "attribution", "push", "events", "views", "crashes", "users", "push", "star-rating", "apm", "feedback", "remote-config"]);<br></code><code class="javascript">Countly.giveConsent(["events", "views", "star-rating", "crashes"]);</code></pre>
<h2>Removing consents</h2>
<p>
  <span>If the end-user changes his/her mind about consents at a later time, you will need to reflect this in the Countly SDK using&nbsp;the&nbsp;<code>removeConsent</code></span><span>method:</span>
</p>
<pre><code class="javascript">Countly.removeConsent(["events", "views", "star-rating", "crashes"]);</code></pre>
<h2>Giving all consents</h2>
<p>
  <span>If you would like to give consent for all the features, you can use the&nbsp;</span><code>giveAllConsent</code><span>&nbsp;method:</span>
</p>
<pre><code class="javascript">Countly.giveAllConsent();</code></pre>
<h2>Removing all consents</h2>
<p>
  <span>If you would like to remove consent for all the features, you can use&nbsp;the&nbsp;<code>removeAllConsent</code></span><span>&nbsp;method:</span>
</p>
<pre><code class="javascript">Countly.removeAllConsent();</code></pre>
<h1>Security and privacy</h1>
<h2>Parameter tampering protection</h2>
<p>
  You can set optional <code>salt</code> to be used for calculating checksum of
  request data, which will be sent with each request using
  <code>&amp;checksum</code> field. You need to set exactly the same
  <code>salt</code> on the Countly server. If <code>salt</code> on Countly server
  is set, all requests would be checked for the validity of
  <code>&amp;checksum</code>&nbsp; field before being processed.
</p>
<pre><code class="javascript">// sending data with salt
Countly.enableParameterTamperingProtection("salt");</code></pre>
<p>
  Make sure not to use salt on the Countly server and not on the SDK side, otherwise,
  Countly won't accept any incoming requests.
</p>
<h2>Using Proguard</h2>
<p>
  <span style="font-weight:400">Proguard obfuscates the OpenUDID &amp; Countly Messaging classes. If you use OpenUDID or Countly Messaging in your application, f<span>ind <strong class="ib cf">app/proguard-rules.pro</strong></span><span>&nbsp;file which sits inside&nbsp;</span><strong class="ib cf">/android/app/</strong><span> folder and adds the following lines:</span></span>
</p>
<pre><code class="java">-keep class org.openudid.** { *; }
-keep class ly.count.android.sdk.** { *; }</code></pre>
<p>
  <span>If <span style="font-weight:400">Proguard is not already configured then</span> first, enable shrinking and obfuscation in the build file. Find </span><strong class="ib cf">build.gradle</strong><span>&nbsp;file which sits inside&nbsp;</span><strong class="ib cf">/android/app/</strong><span> folder and adds lines in bold<br></span>
</p>
<pre><span class="pln">android </span><span class="pun">{</span><span class="pln"><br>&nbsp; &nbsp; buildTypes </span><span class="pun">{</span><span class="pln"><br>&nbsp; &nbsp; &nbsp; &nbsp; release </span><span class="pun">{</span><span class="pln"><br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </span><span class="com">// Enables code shrinking, obfuscation, and optimization for only</span><span class="pln"><br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </span><span class="com">// your project's release build type.</span><span class="pln"><br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <strong>minifyEnabled </strong></span><strong><span class="kwd">true</span></strong><span class="pln"><br><br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </span><span class="com">// Enables resource shrinking, which is performed by the</span><span class="pln"><br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </span><span class="com">// Android Gradle plugin.</span><span class="pln"><br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <strong>shrinkResources </strong></span><strong><span class="kwd">true</span></strong><span class="pln"><br><br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </span><span class="com">// Includes the default ProGuard rules files that are packaged with</span><span class="pln"><br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </span><span class="com">// the Android Gradle plugin. To learn more, go to the section about</span><span class="pln"><br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </span><span class="com">// R8 configuration files.</span><span class="pln"><br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <strong>proguardFiles getDefaultProguardFile</strong></span><strong><span class="pun">(</span><span class="pln"><br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </span><span class="str">'proguard-android-optimize.txt'</span><span class="pun">),</span><span class="pln"><br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </span><span class="str">'proguard-rules.pro'</span></strong><span class="pln"><br>&nbsp; &nbsp; &nbsp; &nbsp; </span><span class="pun">}</span><span class="pln"><br>&nbsp; &nbsp; </span><span class="pun">}<br></span><span class="pln">    ...<br></span><span class="pun">}</span></pre>
<p id="0858" class="hz ia gi ib b ic it id ie if iu ig ih ii iv ij ik il iw im in io ix ip iq is cs ev" data-selectable-paragraph="">
  Next create a configuration that will preserve the entire Flutter wrapper code.
  Create<strong class="ib cf"><span>&nbsp;</span>/android/app/proguard-rules.pro</strong><span>&nbsp;</span>file
  and insert inside:
</p>
<pre class="iy iz ja jb jc jd je jf"><span id="0590" class="ev jg jh gi ji b ct jj jk s jl" data-selectable-paragraph="">#Flutter Wrapper<br>-keep class io.flutter.app.** { *; }<br>-keep class io.flutter.plugin.**  { *; }<br>-keep class io.flutter.util.**  { *; }<br>-keep class io.flutter.view.**  { *; }<br>-keep class io.flutter.**  { *; }<br>-keep class io.flutter.plugins.**  { *; }</span></pre>
<p>
  More info related to code shrinking can be found here for
  <a href="https://flutter.dev/docs/deployment/android#shrinking-your-code-with-r8">flutter</a>
  and
  <a href="https://developer.android.com/studio/build/shrink-code#keep-code" target="_blank" rel="noopener">android</a>.
</p>
<h1>Other features</h1>
<h2>Attribution&nbsp;</h2>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Minimum Countly SDK Version</span></strong>
  </p>
  <p>
    This feature is only supported by the minimum SDK version 20.04.1.
  </p>
</div>
<p>
  <a href="https://count.ly/attribution-analytics">Countly Attribution Analytics</a>
  allows you to measure your marketing campaign performance by attributing installs
  from specific campaigns. This feature is available for the Enterprise Edition.
</p>
<p>Call this before init.</p>
<pre><span>// Enable to measure your marketing campaign performance by attributing installs from specific campaigns.</span><br>Countly.<span>enableAttribution</span>();</pre>
<p>
  <span>For iOS 14+ use the <code><span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif">Countly</span><span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif">.</span><span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif">recordAttributionID("IDFA")</span></code></span><span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif"> function instead of <span><code>Countly.enableAttribution()</code></span></span>
</p>
<p>
  <span>You can use <code><span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif">Countly</span><span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif">.</span><span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif">recordAttributionID</span></code>&nbsp;function to specify IDFA for campaign attribution</span>
</p>
<pre><span><span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif">Countly</span><span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif">.</span><span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif">recordAttributionID("</span>IDFA_VALUE_YOU_GET_FROM_THE_SYSTEM");</span><span></span></pre>
<p>
  <span>For iOS 14+ due to Apple changes regarding Application Tracking, you need to ask the user for permission to track the Application.</span><span></span><span></span>
</p>
<h2>Forcing HTTP POST</h2>
<p>
  If the data sent to the server is short enough, the SDK will use HTTP GET requests.
  In case you want an override so that HTTP POST is used in all cases, call the
  <code>setHttpPostForced</code> function after you called <code>init</code>. You
  can use the same function later in the app's life cycle to disable the override.
  This function has to be called every time the app starts.
</p>
<pre><code class="javascript"> Countly.setHttpPostForced(true); // default is false</code></pre>
<h2>Interacting with the internal request queue</h2>
<p>
  When recording events or activities, the requests don't always get sent immediately.
  Events get grouped together. All the requests contain the same app key which
  is provided in the <code>init</code> function.
</p>
<p>
  There are two ways to interact with the app key in the request queue at the moment.&nbsp;
</p>
<p>
  1. You can replace all requests with a different app key with the current app
  key:&nbsp;
</p>
<pre>//Replaces all requests with a different app key with the current app key.<br>Countly.replaceAllAppKeysInQueueWithCurrentAppKey();</pre>
<p>
  In the request queue, if there are any requests whose app key is different than
  the current app key, these requests app key will be replaced with the current
  app key.<br>
  <br>
  <span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif">2. You can remove all requests with a different app key in the request queue:</span>
</p>
<pre><span>//Removes all requests with a different app key in request queue.<br></span>Countly.removeDifferentAppKeysFromQueue();</pre>
<p>
  <span style="font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif">In the request queue, if there are any requests whose app key is different than the current app key, these requests will be removed from the request queue.</span>
</p>
<h2>Setting an event queue threshold</h2>
<p>
  Events get grouped together and are sent either every minute or after the unsent
  event count reaches a threshold. By default it is 10. If you would like to change
  this, call:
</p>
<pre>Countly.eventSendThreshold(<span>6</span>);</pre>
<h2>Checking if the SDK has been initialized</h2>
<div class="callout callout--info">
  <p class="callout__title">
    <span class="wysiwyg-font-size-large"><strong>Minimum Countly SDK Version</strong></span>
  </p>
  <p>
    This feature is only supported by the minimum SDK version 20.04.1.
  </p>
</div>
<p>
  <span style="font-weight:400">In case you would like to check if init has been called, you may use the following function:</span>
</p>
<pre>Countly.<span>isInitialized</span>();</pre>
<h2>Optional parameters during initialization</h2>
<p>
  You can provide optional parameters that will be used during begin_session request.
  They must be set right after the <code>init</code> function so that they are
  set before the request is sent to the server. To set them, use the
  <code>setOptionalParametersForInitialization</code> function. If you want to
  set those optional parameters, this function has to be called every time the
  app starts. If you don't want to set one off those values, leave that field
  <code>null</code>.
</p>
<p>The optional parameters are:</p>
<ul>
  <li>Country code: ISO Country code for the user's country</li>
  <li>City: Name of the user's city</li>
  <li>
    Location: Comma separate latitude and longitude values, for example "56.42345,123.45325"
  </li>
  <li style="box-sizing:border-box;margin-bottom:calc(12px)">
    <span style="box-sizing:border-box;font-weight:400">Your user’s IP address</span>
  </li>
</ul>
<pre><code class="javascript">
//setting optional parameters
Map&lt;String, Object&gt; options = {
    "city": "Tampa",
    "country": "US",
    "latitude": "28.006324",
    "longitude": "-82.7166183",
    "ipAddress": "255.255.255.255"
};
Countly.setOptionalParametersForInitialization(options);


//and then call the below code
Countly.init(this, "https://YOUR_SERVER", "YOUR_APP_KEY", "YOUR_DEVICE_ID")
</code></pre>
<h2>&nbsp;</h2>