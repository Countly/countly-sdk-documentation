<p>
  This documentation is for the Countly React Native SDK version 24.4.X The SDK
  source code repository can be found
  <a href="https://github.com/Countly/countly-sdk-react-native-bridge/" target="_blank" rel="noopener noreferrer">here.</a>
</p>
<div class="callout callout--info">
  <p>
    Click
    <a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-and-Installing-SDKs#h_01H9QCP8G7F8Y2PP937KS4DQE2" target="_blank" rel="noopener noreferrer">here, </a>to
    access the documentation for older SDK versions.
  </p>
</div>
<p>
  This is the Countly SDK for React Native applications. It features bridging,
  meaning it includes all the functionalities that Countly Android and iOS SDKs
  provide rather than having those functionalities as React Native code.
</p>
<p>
  For this reason, Countly Android and iOS SDK system requirements are also extended
  to React Native SDK:
</p>
<p>
  For iOS builds, this SDK requires a minimum Deployment Target iOS 10.0 (watchOS
  4.0, tvOS 10.0, macOS 10.14), and it requires Xcode 13.0+.
</p>
<p>
  For Android builds, this SDK requires a minimum Android version of 4.2.x (API
  Level 17).
</p>
<p>
  This SDK also depends on the react-native library for communicating with the
  native side. While it can possibly work with older versions, the currently supported
  react-native versions are 0.60.0 and up.
</p>
<p>
  To examine the example integrations, please have a look
  <a href="#h_01HPKC2VFEH3K77VCES1WPH7MN">here.</a>
</p>
<h1 id="h_01HAVQNJQQY6AYCGY7TW5TR2GC">Adding the SDK to the Project</h1>
<p>
  Run the following snippet in the root directory of your React Native project
  to install the npm dependencies and link <strong>native libraries</strong>.
</p>
<pre><code class="bash"># Include the Countly Class in the file that you want to use.
npm install --save https://github.com/Countly/countly-sdk-react-native-bridge.git

# OR

npm install --save countly-sdk-react-native-bridge@latest

# Linking the library to your app

cd ios
pod install
cd ..</code></pre>
<h1 id="h_01HAVQNJQQBPYNQ7D6ACZTPEMM">SDK Integration</h1>
<h2 id="h_01HAVQNJQQQAZSCX41W0SPS5P3">Minimal Setup</h2>
<p>
  We will need to call two methods (<code class="JavaScript">initWithConfig</code>
  and <code class="JavaScript">start</code>) in order to set up our SDK. These
  methods should only be called once during the app's lifecycle and should be done
  as early as possible. Your main app component's
  <code class="JavaScript">componentDidMount</code>method may be a good place.
</p>
<pre><code class="javascript">import Countly from 'countly-sdk-react-native-bridge';
import CountlyConfig from 'countly-sdk-react-native-bridge/CountlyConfig';

if(!await Countly.isInitialized()) {
  // create Countly config object
  const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");
  await Countly.initWithConfig(countlyConfig); // Initialize the countly SDK with config.
}</code></pre>
<p>
  Please check
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KX44C9SF48WRPQNCP3" target="_blank" rel="noopener noreferrer">here</a>
  for more information on how to acquire your application key (APP_KEY) and server
  URL.
</p>
<p>
  After <code class="JavaScript">initWithConfig</code> has been called once, you
  may use the commands in the rest of this document to send additional data and
  metrics to your server.
</p>
<div class="callout callout--info">
  <p>
    If you are in doubt about the correctness of your Countly SDK integration
    you can learn about the verification methods from
    <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KXE6YKVETHDWPP8J3K" target="_blank" rel="noopener noreferrer">here</a>.
  </p>
</div>
<h1 id="h_01HAVQNJQQ1QSEBM46DBK2DR77">SDK Logging</h1>
<p>
  The first thing you should do while integrating our SDK is enable logging. If
  logging is enabled, then our SDK will print out debug messages about its internal
  state and encountered problems.
</p>
<p>
  Call <code class="javascript">setLoggingEnabled</code> on the config object to
  enable logging:
</p>
<pre><code class="javascript">// create Countly config object
const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");
// ...
countlyConfig.setLoggingEnabled(true); // Enable countly internal debugging logs
await Countly.initWithConfig(countlyConfig); // Initialize the countly SDK with config.</code></pre>
<p>
  For more information on where to find the SDK logs you can check the documentation
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KXC5S8Q1NQWDZ33HXC" target="blank">here</a>.
</p>
<h1 id="h_01HAVQNJQQ54VGN5SK3J9YZYCN">Crash Reporting</h1>
<p>
  The Countly SDK has the ability to collect
  <a href="https://support.count.ly/hc/en-us/articles/4404213566105" target="_blank" rel="noopener noreferrer">crash reports</a>,
  which you may examine and resolve later on the server.
</p>
<h2 id="h_01HAVQNJQQ8BMDZBKTHKSMAHQQ">Automatic Crash Handling</h2>
<p>
  With this feature, the Countly SDK will generate a crash report if your application
  crashes due to an exception and will send it to the Countly server for further
  inspection.
</p>
<p>
  If a crash report cannot be delivered to the server (e.g. no internet connection,
  unavailable server, etc.), then the SDK stores the crash report locally in order
  to send the report again, when the connection to server is restored.
</p>
<p>
  You will need to call the following method before calling
  <code class="JavaScript">initWithConfig</code> in order to activate automatic
  crash reporting.
</p>
<pre><code class="javascript">// create Countly config object
const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");
// ...
countlyConfig.enableCrashReporting(); // Enable crash reports
await Countly.initWithConfig(countlyConfig); // Initialize the countly SDK with config.</code></pre>
<h2 id="h_01HAVQNJQQH45W0XT6VXNT2VG0">Automatic Crash Report Segmentation</h2>
<p>
  You may add a key/value segment to crash reports. For example, you could set
  which specific library or framework version you used in your app. You may then
  figure out if there is any correlation between the specific library or another
  segment and the crash reports.
</p>
<p>Use the following function for this purpose:</p>
<pre><code class="JavaScript">var segment = {"Key": "Value"};
Countly.setCustomCrashSegments(segment);</code></pre>
<h2 id="h_01HAVQNJQQP9T6KQT0Y0PRW5RF">Handled Exceptions</h2>
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
<h2 id="h_01HAVQNJQQW9G8MJHFW3EAR78S">Crash Breadcrumbs</h2>
<p>
  Throughout your app, you can leave crash breadcrumbs which would describe previous
  steps that were taken in your app before the crash. After a crash happens, they
  will be sent together with the crash report.
</p>
<p>Following the command adds crash breadcrumb:</p>
<pre><code class="JavaScript">Countly.addCrashLog(String record) </code></pre>
<h2 id="h_01HAVQNJQQ8E0Y6GS98ZT7P1NP">Native C++ Crash Reporting</h2>
<p>
  If you have C++ libraries in your React Native Android app, the React Native
  Bridge SDK allows you to record possible crashes in your Countly server by integrating
  the <code class="JavaScript">sdk-native</code>developed within our
  <a href="https://github.com/Countly/countly-sdk-android" target="_blank" rel="noopener noreferrer">Android SDK</a>.
  Find more information
  <a href="https://support.count.ly/hc/en-us/articles/360037754031-Android-SDK#h_01HAVQDM5TFKEHBN5G8J9VSP37" target="_blank" rel="noopener">here</a>.
</p>
<p>
  As this feature is optional, you will need to do some changes in your react native
  android project files, to make it available.
</p>
<p>
  Go to
  <code class="JavaScript">YOUR_REACT_NATIVE_PROJECT_PATH/android/app/build.gradle</code>and
  add the package dependency (please change the
  <code class="JavaScript">LATEST_VERSION</code> below by checking our Maven
  <a href="https://central.sonatype.com/artifact/ly.count.android/sdk-native/versions" target="_blank" rel="noopener noreferrer">page</a>,
  currently 23.8.0):
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
<pre><code class="java">// import this in your Application class
import ly.count.android.sdknative.CountlyNative;

// call this function in "onCreate" callback of Application class
CountlyNative.initNative(getApplicationContext());</code></pre>
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
  <a href="https://support.count.ly/hc/en-us/articles/360037754031-Android#h_01HAVQDM5TFKEHBN5G8J9VSP37" target="_blank" rel="noopener noreferrer">page</a>.
</p>
<p>
  This is what the debug logs will look like if you use this feature:
</p>
<pre><code class="bash">$ adb logcat -s Countly:V countly_breakpad_cpp:V

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
<h1 id="h_01HAVQNJQR1DMRFF2T44003S59">Events</h1>
<p>
  An
  <a href="https://support.count.ly/hc/en-us/articles/4403721560857-Events" target="_blank" rel="noopener noreferrer">Event</a>
  is any type of action or data that you can send to a Countly instance, e.g. purchases,
  changed settings, view enabled, and so on. This way it's possible to get much
  more information from your application compared to what is sent from the SDK
  to the Countly instance by default.
</p>
<p>
  Here are the details about the properties which you can send with an event:
</p>
<ul>
  <li>
    <code class="JavaScript">eventName</code> name of the event at server (String)
    (<strong>mandatory</strong>)
  </li>
  <li>
    <code class="JavaScript">segmentation</code> key-value pairs that can be
    used to track additional information (Object)
  </li>
  <li>
    <code class="JavaScript">eventCount</code> number of times this event occurred.
    Total count can be viewed at server (Number)
  </li>
  <li>
    <code class="JavaScript">eventSum</code> any numerical data tied to an event.
    Total sum can be viewed at server (Number)
  </li>
</ul>
<div class="callout callout--warning">
  <strong>Data passed should be in UTF-8</strong>
  <p>
    All data passed to the Countly server via the SDK or API should be in UTF-8.
  </p>
</div>
<h2 id="h_01HAVQNJQR1RXEQ6KYGTMJFJDP">Recording Events</h2>
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
<pre>Countly.events.recordEvent("Purchase", undefined, 1);</pre>
<p>
  <strong>2. Event key, count, and sum</strong>
</p>
<pre><code class="JavaScript">Countly.events.recordEvent("Purchase", undefined, 1, 0.99);</code></pre>
<p>
  <strong>3. Event key and count with segmentation(s)</strong>
</p>
<pre>Countly.events.recordEvent("Purchase", { Country: "Germany" }, 1 )</pre>
<p>
  <strong>4. Event key, count, and sum with segmentation(s)</strong>
</p>
<pre>Countly.events.recordEvent("Purchase", { Country: "Germany" }, 1, 0.99)</pre>
<p>
  Those are only a few examples of what you can do with events. You may extend
  those examples and use Country, game_level, time_of_day, and any other segmentation
  that will provide you with valuable insights.
</p>
<h2 id="h_01HAVQNJQRBRHVK5WF42VPFZF2">Timed Events</h2>
<p>
  It's possible to create timed events by calling start and stop methods. This
  would calculate the duration between those two calls and record it as the duration
  of the event. However the start method only serves as a timer and unless the
  end method is called no event will be recorded.
</p>
<pre><code class="JavaScript">//start a timed event
Countly.events.startEvent("Event name");
//wait some time

//end the event
Countly.events.endEvent("Event name");<br></code></pre>
<p>
  You may also provide additional information when ending an event:
</p>
<pre><code class="JavaScript">//start a timed event
Countly.events.startEvent("Event name");
//wait some time

//end the event
Countly.events.endEvent("Event name", { Country: "Germany", Age: "21" }, 1, 0.99);
</code></pre>
<p>
  You may cancel the started timed event in case it is not relevant anymore. Also
  restarting the app would cancel a started timed event.
</p>
<pre><code class="JavaScript">//start a timed event
Countly.events.startEvent("Event name");
//wait some time<br><br>// cancels the timed event
Countly.events.cancelEvent("Event name");

// now this will not work
Countly.events.endEvent("Event name");</code></pre>
<h1 id="h_01H930GAQ5AHF46JK3WQ9Y7M01">Sessions</h1>
<h2 id="h_01H930GAQ5GC90X94VG7NAG6K1">Automatic Session Tracking</h2>
<p>
  This is enabled by default and tracks the users session with respect to the app
  visibility.
</p>
<p>
  The SDK will automatically handle all required requests (begin session, update
  session and end session).
</p>
<h1 id="h_01HAVQNJQR7VTSADNK0KZGAE8H">View Tracking</h1>
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
  <code class="JavaScript">Analytics &gt; Views</code>
</p>
<div class="img-container">
  <img src="/guide-media/01GV9ZW9XVCXCTTKN1DT3684EV" alt="001.png">
</div>
<h1 id="h_01HAVQNJQR4M6EJ5WS9HRBX2Q4">Device ID Management</h1>
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
<h2 id="h_01HAVQNJQR1HPTNTJ711DVNFD1">Changing Device ID</h2>
<div class="callout callout--warning">
  <p>
    <strong>Performance risk.</strong> Changing device id with server merging
    results in huge load on server as it is rewriting all the user history. This
    should be done only once per user.
  </p>
</div>
<p>
  You may configure or change the device ID anytime using the method below.
</p>
<pre>Countly.changeDeviceId(DEVICE_ID, ON_SERVER);</pre>
<p>
  You may either allow the device to be counted as a new device or merge it with
  the existing data on the server. If <code class="JavaScript">onServer</code>
  is set to <code class="JavaScript">true</code>, the old device ID on the server
  will be replaced with the new one, and data associated with the old device ID
  will be merged automatically. Otherwise, if
  <code class="JavaScript">onServer</code> is set to
  <code class="JavaScript">false</code>, the device will be counted as a new device
  on the server.
</p>
<h2 id="h_01HAVQNJQRHVERZJ1YR7QJHMVG">Temporary Device ID</h2>
<p>
  You may use a temporary device ID mode for keeping all requests on hold until
  the real device ID is set later.
</p>
<p>
  To enable this when initializing the SDK, use the method below.
</p>
<pre><code class="javascript">// create Countly config object
const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");
//...
countlyConfig.setDeviceId(Countly.TemporaryDeviceIDString); // Set temporary device ID
await Countly.initWithConfig(countlyConfig); // Initialize the countly SDK with config.
</code></pre>
<p>
  To enable a temporary device ID <strong>after</strong> initialization, use the
  method below.
</p>
<pre>Countly.changeDeviceId(Countly.TemporaryDeviceIDString, ON_SERVER);</pre>
<p>
  <strong>Note:</strong> When passing
  <code class="JavaScript"><span>Countly.TemporaryDeviceIDString</span></code>
  for the <code class="JavaScript">deviceID</code> parameter, the argument for
  the <code class="JavaScript">onServer</code>parameter does not matter.
</p>
<p>
  As long as the device ID value is
  <code class="JavaScript"><span>Countly.TemporaryDeviceIDString</span></code>,
  the SDK will be in temporary device ID mode and all requests will be on hold,
  but they will be persistently stored.
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
<h2 id="h_01HAVQNJQREEYRDZ2HNBMRZ7HF">Retrieving Current Device ID</h2>
<p>
  You may want to see what device id Countly is assigning for the specific device.
  For that, you may use the following calls.
</p>
<pre><code class="JavaScript">let currentDeviceId = await Countly().getCurrentDeviceId();</code></pre>
<p>
  <span>You can use </span><code>getDeviceIDType</code><span> method which returns a value identifying the </span><span>the current device ID type. The possible type are: </span>
</p>
<ul>
  <li>
    <span>DEVELOPER_SUPPLIED - device ID was supplied by the host app.</span>
  </li>
  <li>
    <span>SDK_GENERATED - device ID was generated by the SDK.</span>
  </li>
  <li>
    <span>TEMPORARY_ID - the SDK is in temporary device ID mode.</span>
  </li>
</ul>
<p>
  To determine the specific type, you would compare the return value to SDK defined
  constants.
</p>
<pre><code class="JavaScript">let deviceIdType = await Countly.getDeviceIDType();
if(deviceIdType == <span class="pl-v">DeviceIdType.<span>SDK_GENERATED</span><span>) {
  //this is a SDK generated device ID
} else if(deviceIdType == DeviceIdType.DEVELOPER_SUPPLIED) {
  //this is a device ID that was provided by the developer
} else if(deviceIdType == DeviceIdType.TEMPORARY_ID) {
  //the SDK is in temporary ID mode
}</span></span></code></pre>
<h1 id="h_01HAVQNJQR5GW08NR6A2P814QT">Push Notifications</h1>
<p>
  Please first check our
  <a href="https://support.count.ly/hc/en-us/articles/4405405459225-Push-Notifications" target="_blank" rel="noopener noreferrer">Push Notifications documentation</a>
  to see how you can use this feature. Since Android and iOS handles notifications
  differently (from how you can send them externally to how they are handled in
  native code), we need to provide different instructions for these two platforms.
</p>
<h2 id="h_01HAVQNJQRSZVS0Y9J8WZ1AW2D">General Setup</h2>
<p>
  Android and iOS devices require different setups to enable the push notifications.
  Android uses the <code>setPushNotificationChannelInformation</code>, whereas
  iOS uses the <code>setPushTokenType</code> method on the CountlyConfig object.
  Both of these methods must be called before initializing the SDK.
</p>
<div class="callout callout--warning">
  <p>
    <code>setPushTokenType</code> and
    <code>setPushNotificationChannelInformation</code> methods require the minimum
    SDK version of 23.2.4.
  </p>
  <p>
    For previous versions, please use <code>pushTokenType</code> instead.
  </p>
</div>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">iOS</span>
    <span class="tabs-link">Android</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">// create Countly config object
const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");
// Set the token types: DEVELOPMENT, PRODUCTION or ADHOC
countlyConfig.setPushTokenType(Countly.messagingMode.DEVELOPMENT);
// Initialize the countly SDK with config.
await Countly.initWithConfig(countlyConfig);
    </code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">// create Countly config object
const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");
// Method to set the push channel name and description.
countlyConfig.setPushNotificationChannelInformation("Channel Name", "Channel Description");
// Initialize the countly SDK with config.
await Countly.initWithConfig(countlyConfig);
    </code></pre>
  </div>
</div>
<p>
  When you are ready to initialize Countly Push, call
  <code class="JavaScript">Countly.askForNotificationPermission()</code> after
  <code class="JavaScript">initWithConfig</code>, using the method below. This
  method will ask for permission, and send push token to Countly server.
</p>
<pre>Countly.askForNotificationPermission();</pre>
<h3 id="h_01HAVQNJQRF1EPT9FZ5YETHTBN">Push Notification Customization</h3>
<h4 id="h_01HAVQNJQRGAKZN0PZZM9ENZB5">Notification Accent Color</h4>
<div class="callout callout--warning">
  <p>
    <code>setPushNotificationAccentColor</code> requires the minimum SDK version
    of 23.2.4.
  </p>
</div>
<p>
  Currently, push notification customization is only supported for Android devices.
  You can only select the accent color of your notifications and provide a custom
  notification sound.
</p>
<p>
  You can provide a color in hexadecimal color system to the CountlyConfig object
  with the <code>setPushNotificationAccentColor</code> method before the SDK initialization.
</p>
<pre><code class="javascript">// Set notification accent color
countlyConfig.setPushNotificationAccentColor("#000000");</code></pre>
<h4 id="h_01HAVQNJQSDNA1SBTY0ZWKREJV">Custom Sound</h4>
<p>
  Currently custom sound feature is only available for Android.
</p>
<p>
  To use a custom sound for your notifications in Android you should provide a
  path to your sound file and pass it as the first parameter of the
  <code>askForNotificationPermission</code> method.
</p>
<pre>// CUSTOM_SOUND_PATH is an optional parameter and currently only supported for Android.<br>Countly.askForNotificationPermission("CUSTOM_SOUND_PATH");</pre>
<p>
  We will use this custom sound path to create a soundUri and set the sound of
  notification channel.
</p>
<div class="callout callout--warning">
  <p>
    If you would like to use a custom sound in your push notifications, they
    must be present on the device. They cannot be linked from the Internet.
  </p>
</div>
<p>
  We recommend to add the custom sound file in your Android project res/raw folder.
  Always create a "raw" folder by right clicking on Resources (res) folder and
  select New -&gt; Android Resource Directory.<br>
  Your custom sound path will be like this after adding it in res/raw folder:<br>
  "android.resource://PACKAGE_NAME/raw/NAME_OF_SOUND_WITHOUT_EXTENSION";
</p>
<p>
  For more information about custom push notification sounds in Android check
  <a href="https://support.count.ly/hc/en-us/articles/360037754031-Android#h_01HAVQDM5TZ37DMR7CVMDRHDX6" target="_blank" rel="noopener noreferrer">this section</a>
  of Android article.
</p>
<h2 id="h_01HAVQNJQSDMY43FAAN5D1GQ74">Android Setup</h2>
<p>
  Step 1: For FCM credentials setup please follow the instruction from this
  <a href="https://support.countly.com/hc/en-us/articles/360037754031-Android#h_01HAVQDM5TN4XSRHM5NPVQ8THG" target="_blank" rel="noopener noreferrer">URL</a>
</p>
<p>
  Step 2: Make sure you have
  <code class="JavaScript">google-services.json</code> from
  <a href="https://firebase.google.com/" target="_blank" rel="noopener noreferrer">Firebase</a>
  website
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
  Step 5: Use google services latest version from
  <a href="https://developers.google.com/android/guides/google-services-plugin" target="_blank" rel="noopener noreferrer">this link</a>
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
  <strong>Note:</strong> You need to take additional steps to handle multiple messaging
  services. If you are using other plugins for push notifications, please follow
  the instructions from this URL:<br>
  <a href="/hc/en-us/articles/4412005896217" target="_blank" rel="noopener noreferrer">Handling multiple FCM services</a>
</p>
<p>
  <strong>Additional Intent Redirection Checks</strong>
</p>
<p>
  Intent Redirection Vulnerability is an issue that lets your app allow malicious
  apps to access private app components or files. Google removes apps from Google
  Play that is susceptible to Intent Redirection Vulnerability. For Push Notifications,
  we are also using Intent Redirection in our SDK, so for that reason, we have
  also implemented additional Intent Redirection protection.
</p>
<p>
  By default additional intent redirection is enabled for intent redirect security,
  you can disable the additional intent redirection with
  <code>disableAdditionalIntentRedirectionChecks</code>:
</p>
<pre><code class="javascript"><br>const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");
// ...
countlyConfig.disableAdditionalIntentRedirectionChecks(); // Disable intent redirection security
await Countly.initWithConfig(countlyConfig); // Initialize the countly SDK with config.
</code></pre>
<p>
  If these are enabled then the SDK will enforce additional security checks. More
  info can be found
  <a href="https://support.google.com/faqs/answer/9267555?hl=en" target="_blank" rel="noopener">here</a>.
</p>
<p>
  If, for some reason, the 'activity name' does not start with the 'application
  package name' (for e.g if you are using Android Product/Build Flavors to create
  multiple apps with the same code base), then you need to provide the additional
  allowed class and package names for Intent Redirection manually.
</p>
<p>
  You can set the allowed package and class names for Intent Redirection using
  this call:
</p>
<pre><code class="javascript">// create Countly config object
const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");
// ...
countlyConfig.configureIntentRedirectionCheck(["MainActivity"], ["com.countly.demo"]);
// configure redirection check
await Countly.initWithConfig(countlyConfig); // Initialize the countly SDK with config.
</code></pre>
<h2 id="h_01HAVQNJQSZ2E3RWEEZ9QEAB02">iOS Setup</h2>
<p>
  Push notifications are enabled by default for iOS, but if you wish to disable
  them, you can define the macro "COUNTLY_EXCLUDE_PUSHNOTIFICATIONS" in the project's
  preprocessor macros setting. The location of this setting may vary depending
  on the development environment you are using.
</p>
<p>
  For example, in Xcode, you can define this macro by navigating to the project
  settings, selecting the build target, and then selecting the "Build Settings"
  tab. Under the "Apple LLVM - Preprocessing" section, you will find the "Preprocessor
  Macros" where you can add the macro "COUNTLY_EXCLUDE_PUSHNOTIFICATIONS" to the
  Debug and/or Release fields. This will exclude push notifications from the build.
</p>
<p>
  For iOS push notification integration please follow the instructions from
  <a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#h_01HAVHW0RQD3WBN560GAKTB77T" target="_blank" rel="noopener noreferrer">here</a>
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
  <img src="/guide-media/01GVDFZ17C5QDJTNSY6AKV01ZY" alt="Countly_RN_PUSH.png">
</div>
<h2 id="h_01HNFJBRCKHFFZZYWK1CD485FT">Removing Push and Its Dependencies</h2>
<p>
  Countly React Native SDK comes with embedded push notification capabilities.
  For the flavor without these features (like Firebase libraries), please check
  <a href="https://www.npmjs.com/package/countly-sdk-react-native-bridge-np" target="_blank" rel="noopener noreferrer">here</a>.
</p>
<h2 id="h_01HAVQNJQSJT44XRDEHJX0SZYC">Handling Push Callbacks</h2>
<p>
  Use the method below to register a Push Notification callback after initializing
  the SDK.
</p>
<pre><code class="java">Countly.registerForNotification(function(theNotification){
  console.log(JSON.stringify(theNotification));
});</code></pre>
<p>
  To listen to notifications received and the click events, add the code below
  in <code>AppDelegate.m</code>
</p>
<p>Add header files</p>
<pre><code class="JavaScript">#import "CountlyReactNative.h"<br>#import &lt;UserNotifications/UserNotifications.h&gt;
</code></pre>
<p>
  Add this call
  <code class="JavaScript">[CountlyReactNative startObservingNotifications];</code>
  in <code>didFinishLaunchingWithOptions:</code> method to handle push notification
  receive and action callbacks when SDK is not initialized.
</p>
<pre><code class="objectivec">// For push notification received and action callbacks.
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions<br>{<br>  [CountlyReactNative startObservingNotifications];<br>}</code></pre>
<p>
  Before <code>@end</code> add these methods
</p>
<pre><code class="objectivec">// Required for the notification event. You must call the completion handler after handling the remote notification.
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
{
  [CountlyReactNative onNotification: userInfo];
  completionHandler(0);
}

// When app is killed.

- (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse*)response withCompletionHandler:(void (^)(void))completionHandler{
  [CountlyReactNative onNotificationResponse: response];
  completionHandler();
}

// When app is running.

- (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification*)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler{
  [CountlyReactNative onNotification: notification.request.content.userInfo];
  completionHandler(0);
}
</code></pre>
<h3 id="h_01HAVQNJQS165PB76SXZHC84PV">Data Structure Received in Push Callbacks</h3>
<p>
  Here is an example of how the data will be received in push callbacks:<img src="/guide-media/01GYZ1ETTFDZQAMC8YA0Y0AQ8G" alt="002.png"><br>
  <br>
  Data Received for Android Platform:
</p>
<pre><code class="json">{
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
<p>Data Received for iOS Platform:</p>
<pre><code class="json">{
 "c": {
  "i": "62b5b945cabedb0870e9f217",
  "l": "https:\/\/www.google.com\/",
  "e": {
   "dt": "mobile",
   "cc": "TR"
  },
  "a": "https:\/\/count.ly\/images\/logos\/countly-logo-mark.png"
 },
 "aps": {
  "mutable-content": 1,
  "alert": {
   "title": "title",
   "subtitle": "subtitle",
   "body": "Message"
  },
  "badge": 1,
  "sound": "custom"
 },
 "Key": "value"
}</code></pre>
<h1 id="h_01HAVQNJQSHA4P0WW2K60R3SNV">User Location</h1>
<p>
  Countly allows you to send geolocation-based push notifications to your users.
  By default, the Countly Server uses the GeoIP database to deduce a user's location.
</p>
<h2 id="h_01HAVQNJQS3NHED2YPDARB5V33">Set User Location</h2>
<p>
  If your app has a different way of detecting location, you may send this information
  to the Countly Server by using the
  <code class="JavaScript">countlyConfig.setLocation</code> or<code class="JavaScript">Countly.setLocation</code>
  methods.
</p>
<p>
  We recommend using the
  <code class="JavaScript">countlyConfig.setLocation</code> method before initialization
  to send location. This includes:
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
<pre><code class="javascript">// create Countly config object
const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");
//...
var countryCode = "us";
var city = "Houston";
var latitude = "29.634933";
var longitude = "-95.220255";
var ipAddress = "103.238.105.167";

countlyConfig.setLocation(countryCode, city, latitude + "," + longitude, ipAddress);
// Set location
await Countly.initWithConfig(countlyConfig); // Initialize the countly SDK with config.
</code></pre>
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
<h2 id="h_01HAVQNJQSVG65ZFJZ335BTARP">Disable Location</h2>
<p>
  To erase any cached location data from the device and stop further location tracking,
  use the following method. Note that if after disabling location, the
  <code class="JavaScript">setLocation</code>is called with any non-null value,
  tracking will resume.
</p>
<pre><code class="javascript">//disable location tracking
Countly.disableLocation();</code></pre>
<h1 id="h_01HAVQNJQSE9AD9KM7WS7R68J8">Remote Config</h1>
<p>
  Remote config allows you to modify how your app functions or looks by requesting
  key-value pairs from your Countly server. The returned values may be modified
  based on the user profile. For more details, please see the
  <a href="https://support.count.ly/hc/en-us/articles/9895605514009-Remote-Config" target="_blank" rel="noopener noreferrer">Remote Config documentation</a>.
</p>
<h2 id="h_01HAVQNJQS9RY5XN2RG153BG79">Manual Remote Config Download</h2>
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
<h2 id="h_01HAVQNJQSN1VVTHGZSWR9JDAC">Getting Remote Config Values</h2>
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
<h2 id="h_01HAVQNJQSRE44ZND5CQ1WZKAK">Clearing Stored Remote Config Values</h2>
<p>
  At some point, you might like to erase all the values downloaded from the server.
  You will need to call one function to do so.
</p>
<pre><code class="JavaScript">Countly.remoteConfigClearValues();</code></pre>
<h1 id="h_01HAVQNJQS2ZB1K5WM9YA34TX9">User Feedback</h1>
<p>
  <span style="font-weight: 400;">There are several ways to receive user feedback: the Star Rating Dialog and the Feedback Widgets (Survey, NPS, Rating).</span>
</p>
<p>
  <span style="font-weight: 400;">Star Rating Dialog allows users to give feedback by rating it from 1 to 5. Feedback Widgets (Survey, NPS, Rating) allow for even more textual feedback from users.</span>
</p>
<h2 id="h_01HAVQNJQSE7TGN56S5RGJVDE4">Star Rating Dialog</h2>
<p>
  The Star-rating integration provides a dialog for getting user feedback about
  an application. It contains a title, a simple message explaining its purpose,
  a 1 through 5-star meter for getting users' ratings, and a dismiss button in
  case the user does not want to give a rating.
</p>
<p>
  This star rating has nothing to do with Google Play Store ratings and reviews.
  It is simply for getting brief user feedback to be displayed on the Countly dashboard.
  If the user dismisses the star-rating dialog without giving a rating, the event
  will not be recorded.
</p>
<pre><code class="javascript">Countly.showStarRating();</code></pre>
<p>
  The star-rating dialog's title, message, and dismiss button text may be customized
  through the <code class="JavaScript">setStarRatingDialogTexts</code> method.
</p>
<pre><code class="javascript">const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");<br>// ...
countlyConfig.setStarRatingDialogTexts("Custom title", "Custom message", "Custom dismiss button text");
// Set dialog texts
await Countly.initWithConfig(countlyConfig); // Initialize the countly SDK with config.
</code></pre>
<h2 id="h_01HAVQNJQS4TRX89X6GSGWQGGV">Feedback Widget</h2>
<div class="callout callout--info">
  <p>
    Feedback Widgets is a
    <a href="https://countly.com/enterprise" target="_blank" rel="noopener noreferrer">Countly Enterprise</a>
    plugin.
  </p>
</div>
<p>
  It is possible to display 3 kinds of Feedback widgets:
  <a href="https://support.count.ly/hc/en-us/articles/4652903481753-Feedback-Surveys-NPS-and-Ratings-#h_01HAY62C2QB9K7CRDJ90DSDM0D" target="_blank" rel="noopener noreferrer">NPS</a>,
  <a href="https://support.count.ly/hc/en-us/articles/4652903481753-Feedback-Surveys-NPS-and-Ratings-#h_01HAY62C2Q965ZDAK31TJ6QDRY" target="_blank" rel="noopener noreferrer">Surveys</a>
  and
  <a href="https://support.count.ly/hc/en-us/articles/4652903481753-Feedback-Surveys-NPS-and-Ratings-#h_01HAY62C2R4S05V7WJC5DEVM0N" target="_blank" rel="noopener noreferrer">Rating</a>.
  All widgets are shown as webviews, and the same methods are used to present them.
</p>
<p>
  For more detailed information about Feedback Widgets, you can refer to
  <a href="https://support.countly.com/hc/en-us/articles/4652903481753-Feedback-Overview" target="_blank" rel="noopener noreferrer">here</a>.
</p>
<div class="callout callout--warning">
  <p>
    Before any feedback widget can be shown, you need to create them in your
    Countly dashboard.
  </p>
</div>
<p>
  When the widgets are created, you need to use 2 calls in your SDK to show them:
  one to get all available widgets for a user and another to display a chosen widget.
</p>
<p>To get your available widget list, use the call below.</p>
<pre><code class="javascript">Countly.feedback.getAvailableFeedbackWidgets(function(retrivedWidgets, error){<br> if (error != null) {<br>  console.log("Error : " + error);<br> }<br> else {<br>  console.log(retrivedWidgets.length)<br> }<br>});</code></pre>
<p>
  From the callback, get the list of all available widgets that apply to the current
  device ID.
</p>
<p>The objects in the returned list look like this:</p>
<pre><code class="json">{ 
  "id"   : "WIDGET_ID",
  "type" : "WIDGET_TYPE",
  "name" : "WIDGET_NAME",
  "tag"  : "WIDGET_TAG"
}</code></pre>
<p>
  To determine what kind of widget that is, check the "type" value. The potential
  values are <code>survey</code>, <code>nps</code> and <code>rating</code>.
</p>
<p>
  Then use the widget type and description (which is the same as provided in the
  Dashboard) to decide which widget to show.
</p>
<p>
  After you have decided which widget you want to display, call the function below.
</p>
<pre><code class="javascript">Countly.feedback.presentFeedbackWidget(RETRIEVED_WIDGET_OBJECT, "CLOSE_BUTTON_TEXT", function() {<br>  console.log("Widgetshown");<br>},<br>function() {<br>  console.log("Widgetclosed");<br>})<br></code></pre>
<h3 id="h_01HBZPWR8E1BF4J850A5VB9BGJ">Manual Reporting</h3>
<p>
  If you have a custom UI where you collect user feedback or you already have some
  feedback data in your system you can report that information to specific feedback
  widgets that you have created in your dashboard through the SDK manually.
</p>
<p>This process consists of three steps:</p>
<ul>
  <li>
    Retrieving the list of available widgets and picking one. This is the same
    initial step while using the feedback widgets and reuses the same call to
    retrieve them.
  </li>
  <li>
    Download widget data from the server (here you would use a widget you pick
    at step one).
  </li>
  <li>
    Report the feedback result (for that single widget according to the data
    from the previous step).
  </li>
</ul>
<p>To get your available widget list, use the call below.</p>
<pre><code class="javascript">// with callback
Countly.feedback.getAvailableFeedbackWidgets(function(retrivedWidgets, error){
  if (error != null) {
    console.log("Error : " + error);
  }
  else {
    console.log(retrivedWidgets)
  }
});

//OR async
Object response = await Countly.feedback.getAvailableFeedbackWidgets();
if (!response.error) {
  // pick a widget from response.data array
  const widgetInfo = response.data[0];
}</code></pre>
<p>To download the widget data use:</p>
<pre><code class="javascript">// with callback
Countly.feedback.getFeedbackWidgetData(widget,function(retrivedWidgetData, error){
  if (error != null) {
    console.log("Error : " + error);
  }
  else {
    console.log(retrivedWidgetData)
  }
});

//OR async
Object response = await Countly.feedback.getFeedbackWidgetData(widget);
if (!response.error) {
// check the response.data Object to learn what is needed to be reported
  const widgetData = response.data;
}</code></pre>
<p>
  Then after these two steps you would need to create a widgetResult Object and
  pass it to the function below with the other information you have gathered so
  far. You can check
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts#h_01HABT18WT0D08H8DR2BAD77T2" target="_blank" rel="noopener noreferrer">this</a>
  in-depth guide to learn how to form this object:
</p>
<pre><code class="javascript">Countly.feedback.reportFeedbackWidgetManually(widgetInfo, widgetData, widgetResult);</code></pre>
<h1 id="h_01HAVQNJQSW54CC0XFHA30BPC8">User Profiles</h1>
<div class="callout callout--info">
  <p>
    User Profiles is a
    <a href="https://countly.com/enterprise" target="_blank" rel="noopener noreferrer">Countly Enterprise</a>
    plugin and built-in
    <a href="https://countly.com/flex" target="_blank" rel="noopener noreferrer">Flex</a>.
  </p>
</div>
<p>
  You can provide Countly any details about your user or visitor. This will allow
  you to track each specific user on the "User Profiles" tab. For more information,
  please check the
  <a href="https://support.count.ly/hc/en-us/articles/4403281285913-User-Profiles" target="_blank" rel="noopener noreferrer">User Profiles documentation</a>.
</p>
<p>
  User details can be sent to your Countly instance in two separate ways: bulk
  mode using <code class="JavaScript">Countly.userDataBulk</code>, and singular
  mode using <code class="JavaScript">Countly.userData</code>.
</p>
<p>
  Bulk mode allows you to be more efficient and make multiple user profiles changes
  in a single network request. This allows you to minimize the traffic to your
  server. Just do note that after you have made the required changes, you need
  to call <code class="JavaScript">Countly.userDataBulk.save()</code>for the changes
  to be bundled and sent.
</p>
<p>
  Singular mode is more intended for ease of use. Every time a change is done through
  that interface, the SDK internally performs a "save" action silently and creates
  a separate request. If used too often, it would lead to bad performance.
</p>
<p>
  <strong>Note:</strong> There is some inconsistency in underlying iOS and Android
  code when using the bulk mode. This problem surfaces when modifying the same
  key multiple times. For iOS it keeps the last value for a key on all push/pull
  user property calls, for Android it will try to combine them. For now the work
  around is that you need to call the “Countly.userDataBulk.save();” after every
  push/pull user property call. This does eliminate some of the potential gains
  of this mode, but it does result in the expected result server-side.
</p>
<p>
  If a property is set as an empty string, it will be deleted on the server side.
</p>
<h2 id="h_01HRW8HQCTY2Y2Q890DPE7YT9A">Setting User Properties</h2>
<h3 id="h_01HAVQNJQSX9KWT0HTGJCEKPRK">Custom Values</h3>
<p>
  Custom user properties are any arbitrary values that you would like to store
  under your user's profile. These values can be internal IDs, registration dates
  or any other value that is not included in the predefined user properties.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Bulk mode</span>
    <span class="tabs-link">Singular mode</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">var options = {};

options.customValueA = "Custom value A";
options.customValueB = "Custom value B";
// ...

Countly.userDataBulk.setUserProperties(options);

// Unless you call this last function your data would not be sent to your server
Countly.userDataBulk.save();</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">var options = {};

options.customValueA = "nicola";
options.customValueB = "info@nicola.tesla";
// ...

Countly.setUserData(options);</code></pre>
  </div>
</div>
<h3 id="h_01HAVQNJQSBR8S36NF4KQ8X0D3">Predefined Values</h3>
<p>
  Predefined user properties are a set of default keys that are commonly used in
  visitor data collection.
</p>
<p>
  Bellow you can see how this can be set using the singular user property access
  mode and using the bulk mode:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Bulk mode</span>
    <span class="tabs-link">Singular mode</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">var options = {};<br>
options.name = "Name of User";
options.username = "Username";
options.email = "User Email";
options.organization = "User Organization";
options.phone = "User Contact number";
options.picture = "https://count.ly/images/logos/countly-logo.png";
options.picturePath = "";
options.gender = "Male";
options.byear = 1989;<br>
Countly.userDataBulk.setUserProperties(options);

// Unless you call this last function your data would not be sent to your server
Countly.userDataBulk.save();
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">var options = {};<br>
options.name = "Nicola Tesla";
options.username = "nicola";
options.email = "info@nicola.tesla";
options.organization = "Trust Electric Ltd";
options.phone = "+90 822 140 2546";
options.picture = "http://www.trust.electric/images/people/nicola.png";
options.picturePath = "";
options.gender = "M";
options.byear = 1919;<br>
Countly.setUserData(options);</code></pre>
  </div>
</div>
<h2 id="h_01HAVQNJQTQ671N13EP5MF5EFV">Modifying Data</h2>
<p>
  Additionally, you can modify these custom values in various ways like increasing
  a number, pushing new values to an array, etc. You can see the whole range of
  operations below.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Bulk mode</span>
    <span class="tabs-link">Singular mode</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Promise.allSettled([
  Countly.userDataBulk.setProperty("key", "value"),
  Countly.userDataBulk.setProperty("increment", 5),
  Countly.userDataBulk.increment("increment"),
  Countly.userDataBulk.setProperty("incrementBy", 5),
  Countly.userDataBulk.incrementBy("incrementBy", 10),
  Countly.userDataBulk.setProperty("multiply", 5),
  Countly.userDataBulk.multiply("multiply", 20),
  Countly.userDataBulk.setProperty("saveMax", 5),
  Countly.userDataBulk.saveMax("saveMax", 100),
  Countly.userDataBulk.setProperty("saveMin", 5),
  Countly.userDataBulk.saveMin("saveMin", 50),
  Countly.userDataBulk.setOnce("setOnce", 200),
  Countly.userDataBulk.pushUniqueValue("type", "morning"),
  Countly.userDataBulk.pushValue("type", "morning"),
  Countly.userDataBulk.pullValue("type", "morning")
]).then(values =&gt; {
  // We need to call the "save" in then block else it will cause a race condition and "save" may call before all the user profiles calls are completed
  Countly.userDataBulk.save();
});</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.userData.setProperty("keyName", "keyValue"); //set custom property
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
  </div>
</div>
<h1 id="h_01HAVQNJQT2HD7EVT4QTCXGG6G">Application Performance Monitoring</h1>
<p>
  The Performance Monitoring feature allows you to analyze your application's performance
  on various aspects. For more details, please review the
  <a href="https://support.count.ly/hc/en-us/articles/4734457847705-Performance" target="_blank" rel="noopener noreferrer">Performance Monitoring documentation</a>.
</p>
<p>
  The SDK provides manual and automatic mechanisms for Application Performance
  Monitoring (APM). All of the automatic mechanisms are disabled by default and
  to start using them you would first need to enable them and give the required
  consent if it was required:
</p>
<pre><code class="javascript">const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");<br>// ...
// this interface exposes the available APM features and their modifications.
countlyConfig.apm.
</code></pre>
<h2 id="h_01HAVQNJQT9NWPZS7ADXQ5E170">Custom Traces</h2>
<p>
  You may measure any operation you want and record it using custom traces. First,
  you need to start a trace by using the
  <code class="objectivec">startTrace(traceKey)</code> method:
</p>
<pre>Countly.startTrace(traceKey);</pre>
<p>
  Then you may end it using the
  <code class="objectivec">endTrace(traceKey, customMetric)</code>method, optionally
  passing any metrics as key-value pairs:
</p>
<pre><code class="java">String traceKey = "Trace Key";
Map&lt;String, int&gt; customMetric = {
  "ABC": 1233,
  "C44C": 1337
};
Countly.endTrace(traceKey, customMetric);</code></pre>
<p>
  The duration of the custom trace will be automatically calculated upon ending.
</p>
<p>
  Trace names should be non-zero length valid strings, and custom metric values
  can only be numbers. Trying to start a custom trace with the already started
  name will have no effect. Trying to end a custom trace with already ended (or
  not yet started) name will have no effect.
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
<h2 id="h_01HAVQNJQTQGM8NFD1KBVYVCA6">Network Traces</h2>
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
<h2 id="h_01HAVQNJQTH9C8YR2B0MZV0S4F">Automatic Device Traces</h2>
<p>
  SDK can automatically track the app start time for you. Tracking of app start
  time is disabled by default and must be explicitly enabled by the developer during
  init.
</p>
<p>
  For tracking app start time automatically you will need to enable it in SDK init
  config:
</p>
<pre><code class="javascript">const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");<br><br>// enable it here separately with 'apm' interface.
countlyConfig.<strong>enableAppStartTimeTracking</strong>();</code></pre>
<p>
  This calculates and records the app launch time for performance monitoring.
</p>
<p>
  If you want to determine when the end time for this calculation should be you
  will have to enable the usage of manual triggers together with enableAppStartTimeTracking
  during init:
</p>
<pre><code class="javascript">const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");<br>
// enable it here separately with 'apm' interface.
countlyConfig.apm.enableAppStartTimeTracking().<strong>enableManualAppLoadedTrigger</strong>();<br></code></pre>
<p>
  Now you can call Countly.appLoadingFinished() any time after SDK initialization
  ( E.g. <code class="JavaScript">componentDidMount</code>&nbsp;method) to record
  that moment as the end of app launch time. The starting time of the app load
  will be automatically calculated and recorded. Note that the app launch time
  can be recorded only once per app launch. So, the second and following calls
  to this method will be ignored.
</p>
<p>
  If you also want to manipulate the app launch starting time instead of using
  the SDK calculated value then you will need to call a third method on the config
  object with the timestamp (in milliseconds) of that time you want:
</p>
<pre><code class="javascript">const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");

// generate the timestamp you want (or you can directly pass a ts)
let ts = Date.now() - 500; // 500 ms before now

// this would also work with manual trigger
countlyConfig.apm.enableAppStartTimeTracking().<strong>setAppStartTimestampOverride</strong>(ts);<br></code></pre>
<h2 id="h_01HVNVCBQ6HCE2Y3Q0WR7NG53Y">App Time in Background / Foreground</h2>
<p>
  Lastly if you want to enable the SDK to record the time an app is in foreground
  or background automatically you would need to enable this option during init:
</p>
<pre><code class="javascript">const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");<br><br>// enable it here separately with 'apm' interface.
countlyConfig.apm.<strong>enableForegroundBackgroundTracking</strong>();</code></pre>
<h1 id="h_01HAVQNJQTPBHA4HKBXA3SJG7Z">User Consent</h1>
<p>
  Being compliant with GDPR and other data privacy regulations, Countly provides
  ways to toggle different Countly tracking features on or off depending on a user's
  given consent. For more details, please review the
  <a href="https://support.count.ly/hc/en-us/articles/4404570865433-Utilities#h_01HBC3FWCBVBZDYS0NSSGQN5F0" target="_blank" rel="noopener noreferrer">Compliance Hub plugin</a>
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
    attribution - allows tracking from which campaign did the user come.
  </li>
  <li>
    users - allows collecting and providing user information, including custom
    properties.
  </li>
  <li>push - allows push notifications,</li>
  <li>
    star-rating - allows sending the results from Rating Feedback widgets.
  </li>
  <li>
    feedback - allows showing the results from Survey and NPS® Feedback widgets.
  </li>
  <li>apm - allows application performance monitoring.</li>
  <li>
    <span>remote-config</span> - allows downloading remote config values from
    your server.
  </li>
</ul>
<h2 id="h_01HAVQNJQT9EZ8R01NCM6ENW9Z">Setup During Init</h2>
<p>
  <span>The requirement for consent is disabled by default. To enable it, you will have to call <code>setRequiresConsent</code> with <code>true</code> during initializing Countly.</span>
</p>
<pre><code class="javascript">const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");
// Enable consent requirement
countlyConfig.setRequiresConsent(true);</code></pre>
<p>
  <span>By default, no consent is given. That means that if no consent is enabled, Countly will not work and no network requests related to its features will be sent.</span>
</p>
<p>
  <span>To give consent during initialization, you have to call <code class="JavaScript">giveConsent</code>on the config object with an array of consent values.</span>
</p>
<pre><code class="javascript">const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");</code><br>countlyConfig.giveConsent(["events", "views", "star-rating", "crashes"]);</pre>
<p>
  The Countly SDK does not persistently store the status of given consents except
  push notifications. You are expected to handle receiving consent from end-users
  using proper UIs depending on your app's context. You are also expected to store
  them either locally or remotely. Following this step, you will need to call the
  <code>giveConsent</code> method on each app launch depending on the permissions
  you managed to get from the end-users.
</p>
<p>Ideally you would give consent during initialization.</p>
<h2 id="h_01HAVQNJQTN2M47W4JY10SZVY9">Changing Consent</h2>
<p>
  The end-user can change their mind about consents at a later time.
</p>
<p>
  To reflect these changes in the Countly SDK, you can use the removeConsent or
  giveConsent methods.
</p>
<pre><code class="javascript">// To add/remove consent for a single feature (string parameter)
Countly.giveConsent("events");
Countly.removeConsent("events");

// To add/remove consent for a subset of features (array of strings parameters)
Countly.giveConsent(["events", "views", "star-rating", "crashes"]);
Countly.removeConsent(["events", "views", "star-rating", "crashes"]);</code></pre>
<p>
  You can also either give or remove consent to all possible SDK features:
</p>
<pre><code class="javascript">// To add/remove consent for all available features
Countly.giveAllConsent();
Countly.removeAllConsent();</code></pre>
<h1 id="h_01HAVQNJQTD0RS47PZ0SX4ZW1X">Security and Privacy</h1>
<h2 id="h_01HAVQNJQTMSE0N9EHEDS3P8M8">Parameter Tampering Protection</h2>
<p>
  You can set optional <code class="JavaScript">salt</code> to be used for calculating
  checksum of request data, which will be sent with each request using
  <code class="JavaScript">&amp;checksum</code> field. You need to set exactly
  the same <code class="JavaScript">salt</code> on the Countly server. If
  <code class="JavaScript">salt</code> on Countly server is set, all requests would
  be checked for the validity of <code class="JavaScript">&amp;checksum</code>
  field before being processed.
</p>
<pre><code class="javascript hljs">const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");<br>// ...
countlyConfig.enableParameterTamperingProtection("salt"); // Enable tamper protection salt
await Countly.initWithConfig(countlyConfig); // Initialize the countly SDK with config.
</code></pre>
<p>
  Make sure not to use salt on the Countly server and not on the SDK side, otherwise,
  Countly won't accept any incoming requests.
</p>
<h2 id="h_01HAVQNJQTDBG5DJ85J2ERN6QH">Pinned Certificate (Call this method before initialization)</h2>
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
<pre><code class="bash">cd AwesomeProject
ls
count.ly.cer
mkdir -p ./android/app/src/main/assets/
cp ./count.ly.cer ./android/app/src/main/assets/</code></pre>
<p>
  <strong>iOS</strong>
</p>
<pre>open ./ios/AwesomeProject.xcworkspace
Right click on AwesomeProject and select `New Group` (ScreenShot 1).
Name it `Resources`.
Drag and Drop count.ly.cer file under that folder (ScreenShot 2).
Make sure copy bundle resources has your certificate (Screenshot 4).</pre>
<pre><img src="/guide-media/01GVCPK3524DAMTR4N4RQTENRJ" alt="Screenshot_2020-07-07_at_11.39.02_AM.png">
<img src="/guide-media/01GVAYMBW370WBR1NJBQ83ZFT1" alt="ScreenShot_Pinned_Certificate_1.png"></pre>
<p>
  <img src="/guide-media/01GVDFYEK5674YH9AZFB15ZPYF" alt="Screenshot_Pinned_Certificate_2.png">
</p>
<pre><img src="/guide-media/01GVB664B0Z9XWSW87KCMCPD36" alt="Screenshot_2020-07-07_at_11.39.40_AM.png"></pre>
<p>
  <strong>JavaScript</strong>
</p>
<pre>Countly.pinnedCertificates("count.ly.cer");</pre>
<p>
  Note that <code class="JavaScript">count.ly.cer</code> is the name of the file.
  Replace this file with the one you have.
</p>
<h2 id="h_01H930GAQ8PTNSJ1YV6WFRN15C">Using Proguard</h2>
<p>
  The Android side of the SDK does not require specific proguard exclusions and
  can be fully obfuscated.
</p>
<h1 id="h_01HAVQNJQTVQ1CQD7VGBYY6HFV">Other Features and Notes</h1>
<h2 id="h_01HBZGC0M48MT2JRYM9N89SJ8P">SDK Config Parameters Explained</h2>
<p>
  You may provide your own custom device ID when initializing the SDK using the
  method below.
</p>
<pre><code class="javascript">// create Countly config object
const countlyConfig = new CountlyConfig("https://try.count.ly", "YOUR_APP_KEY");
// ...
countlyConfig.setDeviceId(DEVICE_ID); // Set device ID
await Countly.initWithConfig(countlyConfig); // Initialize the countly SDK with config.
</code></pre>
<h2 id="h_01HPKC2VFEH3K77VCES1WPH7MN">Example Integrations</h2>
<p>
  You can take a look at our example application in
  <a href="https://github.com/Countly/countly-sdk-rnb-example.git" target="_blank" rel="noopener">this Github repo</a>.
  It shows how the majority of the SDK functionality can be used. After you have
  cloned the repo, run the following commands from the root folder:
</p>
<pre><code class="bash">npm install                         # Install dependencies
cd ios                              # Move to ios directory
pod install                         # Download and install pods<br>
cd ../                              # Move to parent directory
react-native run-android # OR       # Run the android project
react-native run-ios                # Run the iOS project</code></pre>
<h2 id="h_01HTF4H350DJ15WXZWCK6PBACR">SDK Internal Limits</h2>
<p>
  Countly SDKs have internal limits to prevent users from unintentionally sending
  large amounts of data to the server. If these limits are exceeded, the data will
  be truncated to keep it within the limit. You can check the exact parameters
  these limits affect from
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts#sdk_internal_limits" target="_blank" rel="noopener noreferrer">here</a>.
</p>
<p>
  The SDK Internal Limit functions can be accessed via an interface called
  <code>sdkInternalLimits</code>, which is available through the
  <code>CountlyConfig</code> object, as demonstrated in the examples.
</p>
<div class="callout callout--warning">
  <p>
    The SDK Internal Limit functions are introduced in SDK version 24.4.1.
  </p>
</div>
<h3 id="h_01HTF4H350DC2PMY77ASMHAGBA">Key Length</h3>
<p>
  Limits the maximum size of all user set keys (default: 128 chars):
</p>
<pre><code>CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.sdkInternalLimits.setMaxKeyLength(int MAX_KEY_LENGTH);
await Countly.initWithConfig(config);</code></pre>
<h3 id="h_01HTF4H350PB7ZRJDKFVZEFXQT">Value Size</h3>
<p>
  Limits the size of all user-set string segmentation (or their equivalent) values
  (default: 256 chars):
</p>
<pre><code>CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.sdkInternalLimits.setMaxValueSize(int MAX_VALUE_SIZE);
await Countly.initWithConfig(config);</code></pre>
<h3 id="h_01HTF4H3507WWAHMBH7MGKW0V4">Segmentation Values</h3>
<p>
  Limits the amount of user-set segmentation key-value pairs (default: 100 entries):
</p>
<pre><code>CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.sdkInternalLimits.setMaxSegmentationValues(int MAX_SEGMENTATION_COUNT);
await Countly.initWithConfig(config);</code></pre>
<h3 id="h_01HTF4H350W0RY8HQKB31H1FTS">Breadcrumb Count</h3>
<p>
  Limits the amount of user-set breadcrumbs that can be recorded (default: 100
  entries; exceeding this deletes the oldest one):
</p>
<pre><code>CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.sdkInternalLimits.setMaxBreadcrumbCount(int MAX_BREADCRUMB_COUNT);
await Countly.initWithConfig(config);</code></pre>
<h3 id="h_01HTF4H35049TZ4ZTX7QK83YBQ">Stack Trace Lines Per Thread</h3>
<p>
  Limits the stack trace lines that would be recorded per thread (default: 30 lines):
</p>
<pre><code>CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.sdkInternalLimits.setMaxStackTraceLinesPerThread(int MAX_STACK_THREAD);
await Countly.initWithConfig(config);</code></pre>
<h3 id="h_01HTF4H3500XJ84CSECQFPXE67">Stack Trace Line Length</h3>
<p>
  Limits the characters that are allowed per stack trace line (default: 200 chars):
</p>
<pre><code>CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.sdkInternalLimits.setMaxStackTraceLineLength(int MAX_STACK_LENGTH);
await Countly.initWithConfig(config);</code></pre>
<h2 id="h_01HBZGC0M4JG8E6DCYCD04HQTJ">SDK Storage and Requests</h2>
<p>
  For iOS: SDK data is stored in Application Support Directory in a file named
  "Countly.dat" For Android: SDK data is stored in SharedPreferences. A SharedPreferences
  object points to a file containing key-value pairs and provides simple methods
  to read and write them.
</p>
<h3 id="h_01HAVQNJQVEMEHN5ZF3DTYNG84">Setting Event Queue Threshold</h3>
<p>
  Events get grouped together and are sent either every minute or after the unsent
  event count reaches a threshold. By default it is 10. If you would like to change
  this, call:
</p>
<pre>Countly.setEventSendThreshold(6);</pre>
<h3 id="h_01HAVQNJQTRAKGYDMT0NB7GVNA">Forcing HTTP POST</h3>
<p>
  If the data sent to the server is short enough, the SDK will use HTTP GET requests.
  In the event you would like an override so that HTTP POST may be used in all
  cases, call the <code class="JavaScript">setHttpPostForced</code> function after
  you have called <code class="JavaScript">initWithConfig</code>. You may use the
  same function later in the app’s life cycle to disable the override. This function
  has to be called every time the app starts, using the method below.
</p>
<pre><code class="javascript">// enabling the override
Countly.setHttpPostForced(true);
  
// disabling the override
Countly.setHttpPostForced(false);</code></pre>
<h3 id="h_01HAVQNJQTKPQPAY8MBKTP66DE">Interacting with the Internal Request Queue</h3>
<p>
  When recording events or activities, the requests don't always get sent immediately.
  Events get grouped together. All the requests contain the same app key which
  is provided in the <code class="JavaScript">initWithConfig</code> function.
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
<h2 id="01HBZGDQ57D82CFMYJH2FBXWEQ">Checking If the SDK Has Been Initialized</h2>
<p>
  In the event you would like to check if initWithConfig has been called, use the
  function below.
</p>
<pre><code class="javascript">Countly.isInitialized().then(result =&gt; console.log(result)); // true or false</code></pre>
<h2 id="h_01HAVQNJQTHCHN59TAVZC63NAD">Attribution</h2>
<p>This feature is available for the Enterprise Edition.</p>
<p>
  <span>There are 2 forms of attribution: direct Attribution and indirect Attribution.</span><span></span>
</p>
<h3 id="h_01HAVQNJQT0P9MZH69BJ1MFRCG">Direct Attribution</h3>
<p>
  You can pass "Campaign type" and "Campaign data". The "type" determines for what
  purpose the attribution data is provided. Depending on the type, the expected
  data will differ, but usually that will be a string representation of a JSON
  object.
</p>
<p>
  <span>You can use <code>recordDirectAttribution</code> to set attribution values during initialization</span><span>.</span>
</p>
<pre><code class="JavaScript">const campaignData = 'JSON_STRING';<br>const config = CountlyConfig(SERVER_URL, APP_KEY);<br>config.recordDirectAttribution('CAMPAIGN_TYPE', campaignData);</code><span><br></span></pre>
<p>
  You can also use <code>recordDirectAttribution</code> function to manually report
  attribution later:
</p>
<pre><code class="JavaScript">const campaignData = 'JSON_STRING';<br>Countly.recordDirectAttribution('CAMPAIGN_TYPE', campaignData);</code></pre>
<p>
  Currently this feature is limited and accepts data only in a specific format
  and for a single type. That type is "countly". It will be used to record install
  attribution. The data also needs to be formatted in a specific way. Either with
  the campaign id or with the campaign id and campaign user id.
</p>
<pre><code class="JavaScript">const campaignData = '{cid:"[PROVIDED_CAMPAIGN_ID]", cuid:"[PROVIDED_CAMPAIGN_USER_ID]"}';<br>Countly.recordDirectAttribution('countly', campaignData);</code></pre>
<h3 id="h_01HAVQNJQT4EARSVPB4XZCBT39">Indirect Attribution</h3>
<p>
  This feature would be used to report things like advertising ID's. For each platform
  those would be different values. For the most popular keys we have a class with
  predefined values to use, it is called "AttributionKey".
</p>
<p>
  <span>You can use <code>recordDirectAttribution</code> to set attribution values during initialization</span><span>.</span>
</p>
<pre><code class="JavaScript">const attributionValues = {};<br>if(Platform.OS.match('ios')){<br>  attributionValues[AttributionKey.IDFA] = 'IDFA';<br>} else {<br>  attributionValues[AttributionKey.AdvertisingID] = 'AdvertisingID';<br>}<br><br>const config = CountlyConfig(SERVER_URL, APP_KEY);<br>config.recordIndirectAttribution(attributionValues);</code><span></span></pre>
<p>
  You can also use <code>recordIndirectAttribution</code> function to manually
  report attribution later
</p>
<pre><code class="JavaScript">const attributionValues = {};<br>if(Platform.OS.match('ios')){<br>  attributionValues[AttributionKey.IDFA] = 'IDFA';<br>} else {<br>  attributionValues[AttributionKey.AdvertisingID] = 'AdvertisingID';<br>}<br><br>Countly.recordIndirectAttribution(attributionValues);</code></pre>
<p>
  In case you would be accessing IDFA for ios, for iOS 14+ due to the changes made
  by Apple, regarding Application Tracking, you need to ask the user for permission
  to track the Application.
</p>
<h2 id="h_01HAVQNJQTXCW1K0039GTD0Z3R">Custom Metrics</h2>
<div class="callout callout--info">
  <strong>Minimum Countly SDK Version</strong>
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
  For more information on the specific metric keys used by Countly, check
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305#h_01HABT18WWYQ2QYPZY3GHZBA9B" target="_blank" rel="noopener noreferrer">here</a>.
</p>
<p>Example to override 'Carrier' and 'App Version'</p>
<pre><code class="JavaScript">var customMetric = {"_carrier": "custom carrier", "_app_version": "2.1"};
Countly.setCustomMetrics(customMetric);</code></pre>