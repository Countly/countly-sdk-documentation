<p>
  This documentation is for the Countly Flutter SDK version 24.7.X. The SDK source
  code repository can be found
  <a href="https://github.com/Countly/countly-sdk-flutter-bridge" target="_blank" rel="noopener noreferrer">here.</a>
</p>
<div class="callout callout--info">
  <p>
    Click
    <a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-and-Installing-SDKs#h_01H9QCP8G768WD943FT6WS38TH" target="_self" rel="undefined">here, </a>to
    access the documentation for older SDK versions.
  </p>
</div>
<p>
  For iOS builds, this SDK requires a minimum Deployment Target iOS 10.0 (watchOS
  4.0, tvOS 10.0, macOS 10.14), and it requires Xcode 13.0+.<br>
  For Android builds, this SDK requires a minimum Android version of 4.2.x (API
  Level 17).
</p>
<p>
  To examine the example integrations, please have a look
  <a href="#h_01HPGP75J54BBZFVZE7S7K1N2H">here.</a>
</p>
<h1 id="h_01H930GAQ59MD94NK0NP68GNGT">Adding the SDK to the Project</h1>
<p>
  Add this to your project's <code>pubspec.yaml</code> file:
</p>
<pre><code class="yaml">dependencies:
  countly_flutter: ^24.7.1
</code></pre>
<p>
  After you can install packages from the command line with Flutter:
</p>
<pre><code class="shell">flutter pub get</code></pre>
<h1 id="h_01H930GAQ51K98YA1RGR2ZMKN5">SDK Integration</h1>
<h2 id="h_01H930GAQ5RGKSA3CTNVTBTDZF">Minimal Setup</h2>
<p>
  The shortest way to initialize the SDK, if you want Countly SDK to take care
  of device ID seamlessly, is to use the code below.
</p>
<pre><code class="dart">Countly.isInitialized().then((bool isInitialized){
  if(!isInitialized) {
    // Create the configuration with your app key and server URL
    CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);

    // Initialize with that configuration
    Countly.initWithConfig(config).then((value){
      // handle extra logic after init
    });
  } else {
    print("Countly: Already initialized.");
  }
});</code></pre>
<p>
  Please check
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KX44C9SF48WRPQNCP3">here</a>
  for more information on how to acquire your application key (APP_KEY) and server
  URL.
</p>
<p>
  A "CountlyConfig" object is used to configure the SDK during initialization.
  As shown above, you would create a "CountlyConfig" object and then call its provided
  methods to enable the functionalities you need before initializing the SDK.
</p>
<p>
  Click
  <a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ8P3ZQAA3DGJT0RJVE" target="_self">here</a>
  for more information about the "CountlyConfig" object functionalities.
</p>
<div class="callout callout--info">
  <p>
    If you are in doubt about the correctness of your Countly SDK integration
    you can learn about the verification methods from
    <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KXE6YKVETHDWPP8J3K" target="blank">here</a>.
  </p>
</div>
<h2 id="h_01H930GAQ5TH1KDYE8FFHE3NYC">SDK Data Storage</h2>
<p>SDK data storage locations are platform-specific:</p>
<ul>
  <li>
    For <strong>iOS</strong>, the SDK data is stored in the Application Support
    Directory in a file named "Countly.dat"
  </li>
  <li>
    For <strong>Android</strong>, the SDK data is stored in SharedPreferences.
    A SharedPreferences object points to a file containing key-value pairs and
    provides simple reading and writing methods.
  </li>
</ul>
<h1 id="h_01H930GAQ5BDPD0XHVV8RSR0XK">SDK Logging</h1>
<p>
  If logging is enabled, then our SDK will print out debug messages about its internal
  state and encountered problems.
</p>
<p>
  We advise doing this while implementing Countly features in your application.
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setLoggingEnabled(true);</code></pre>
<p>
  For more information on where to find the SDK logs you can check the documentation
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KXC5S8Q1NQWDZ33HXC" target="blank">here</a>.
</p>
<h1 id="h_01H930GAQ5G76N9W9XM7JACE5B">Crash Reporting</h1>
<p>
  This feature allows the Countly SDK to record crash reports of either encountered
  issues or exceptions which cause your application to crash. Those reports will
  be sent to your Countly server for further inspection.
</p>
<p>
  If a crash report can not be delivered to the server (e.g. no internet connection,
  unavailable server), then SDK stores the crash report locally in order to try
  again later.
</p>
<h2 id="h_01H930GAQ55ZND3R5TD6WWP4R6">Automatic Crash Handling</h2>
<p>
  If you want to enable automatic unhandled crash reporting, you need to call this
  before init:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.enableCrashReporting()</code></pre>
<p>
  By doing that it will automatically catch all errors that are thrown from within
  the Flutter framework.
</p>
<div class="callout callout--warning">
  <p>
    <strong>Important:</strong> If you are using SDK version 24.7.1 or earlier,
    you must use <code>runZonedGuarded</code> to catch asynchronous Dart errors,
    as shown below:
  </p>
  <pre><code class="dart">void main() {
  runZonedGuarded&lt;Future&lt;void&gt;&gt;(() async {
    runApp(MyApp());
  }, Countly.recordDartError);
}</code></pre>
</div>
<h2 id="h_01H930GAQ524KXJKJ2FQYVH075">Automatic Crash Report Segmentation</h2>
<p>
  You may add a key/value segment to crash reports. For example, you could set
  which specific library or framework version you used in your app. You may then
  figure out if there is any correlation between the specific library or another
  segment and the crash reports.
</p>
<p>
  The following call will add the provided segmentation to all recorded crashes.
  Use the following function for this purpose:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setCustomCrashSegment(Map&lt;String, Object&gt; segments);</code></pre>
<h2 id="h_01H930GAQ5D1WSF2DZZJ8XA12T">Handled Exceptions</h2>
<p class="p1">
  There are multiple ways you could report a handled exception/error to Countly.
</p>
<p class="p1">
  This call does not add a stacktrace automatically. If it is required, it should
  be provided to the function. A potential use case would be to
  <code>exception.toString()</code>
</p>
<pre><code class="dart">Countly.logException(String exception, bool nonfatal, [Map&lt;String, Object&gt; segmentation])</code></pre>
<p>
  The issue is recorded with a provided Exception object. If no stacktrace is set,<code>StackTrace.current</code>
  will be used.
</p>
<pre><code class="dart">Countly.logExceptionEx(Exception exception, bool nonfatal, {StackTrace stacktrace, Map&lt;String, Object&gt; segmentation})</code></pre>
<p class="p1">
  The exception/error is recorded through a string message. If no stack trace is
  provided, <code>StackTrace.current</code> will be used.
</p>
<pre><code class="dart">Countly.logExceptionManual(String message, bool nonfatal, {StackTrace stacktrace, Map&lt;String, Object&gt; segmentation})</code></pre>
<p>
  Below are some examples that how to log handled/nonfatal and unhandled/fatal
  exceptions manually.
</p>
<p>
  <strong>1. Manually report exception</strong>
</p>
<pre><code class="dart">bool nonfatal = true; // Set it false in case of fatal exception
// With Exception object
Countly.logExceptionEx(EXCEPTION_OBJECT, nonfatal);

// With String message
Countly.logExceptionManual("MESSAGE_STRING", nonfatal);
</code></pre>
<p>
  <strong>2. Manually report exception with stack trace</strong>
</p>
<pre><code class="dart">bool nonfatal = true; // Set it false in case of fatal exception
// With Exception object
Countly.logExceptionEx(EXCEPTION_OBJECT, nonfatal, stacktrace: STACK_TRACE_OBJECT);

// With String message
Countly.logExceptionManual("MESSAGE_STRING", nonfatal, stacktrace: STACK_TRACE_OBJECT);
</code></pre>
<p>
  <strong>3. Manually report exception with segmentation</strong>
</p>
<pre><code class="dart">bool nonfatal = true; // Set it false in case of fatal exception
// With Exception object
Countly.logExceptionEx(EXCEPTION_OBJECT, nonfatal, segmentation: {"_facebook_version": "0.0.1"});

// With String message
Countly.logExceptionManual("MESSAGE_STRING", nonfatal, segmentation: {"_facebook_version": "0.0.1"});
</code></pre>
<p>
  <strong>4. Manually report exception with stack trace and segmentation</strong>
</p>
<pre><code class="dart">bool nonfatal = true; // Set it false in case of fatal exception
// With Exception object
Countly.logExceptionEx(EXCEPTION_OBJECT, nonfatal, STACK_TRACE_OBJECT, {"_facebook_version": "0.0.1"});

// With String message
Countly.logExceptionManual("MESSAGE_STRING", nonfatal, STACK_TRACE_OBJECT, {"_facebook_version": "0.0.1"});
</code></pre>
<h2 id="h_01H930GAQ5PX812FVSVEAKZMJ8">Crash Breadcrumbs</h2>
<p>
  Throughout your app, you can leave crash breadcrumbs which would describe previous
  steps that were taken in your app before the crash. After a crash happens, they
  will be sent together with the crash report.
</p>
<p>The following function call adds a crash breadcrumb:</p>
<pre><code class="dart">Countly.addCrashLog(String logs)</code></pre>
<h1 id="h_01H930GAQ5NTNH59KY6FB5CCEN">Events</h1>
<p>
  <a href="https://support.count.ly/hc/en-us/articles/360037093532-Custom-events">Event</a>
  is any type of action that you can send to a Countly instance, e.g purchase,
  settings changed, view enabled and so. This way it's possible to get much more
  information from your application compared to what is sent from Flutter SDK to
  Countly instance by default.
</p>
<p>
  Here are the detail about properties which we can use with event:
</p>
<ul>
  <ul>
    <li>
      <code>key</code> identifies the event.
    </li>
    <li>
      <code>count</code> is the number of times this event occurred.
    </li>
    <li>
      <code>sum</code> is an overall numerical data set tied to an event. For
      example, total amount of in-app purchase event.
    </li>
    <li>
      <code class="dart">duration</code> is used to record and track the duration
      of events.
    </li>
    <li>
      <code>segmentation</code> is a key-value pairs, we can use
      <code>segmentation</code> to track additional information. The only valid
      data types are: "String", "Integer", "Double", "Boolean" and "List".
      All other types will be ignored.
    </li>
  </ul>
</ul>
<div class="callout callout--info">
  <strong>Data passed should be in UTF-8</strong>
  <p>
    All data passed to the Countly server via SDK or API should be in UTF-8.
  </p>
</div>
<h2 id="h_01H930GAQ5RVJC7NBPQFGPQ41Y">Recording Events</h2>
<p>
  We will be recording a <strong>purchase</strong> event. Here is a quick summary
  of what information each usage will provide us:
</p>
<ul>
  <li>
    Usage 1: how many times a <strong>purchase</strong> event occurred.
  </li>
  <li>
    Usage 2: how many times a <strong>purchase</strong> event occurred + the
    total amount of those purchases.
  </li>
  <li>
    Usage 3: how many times a <strong>purchase</strong> event occurred + which
    countries and application versions those purchases were made from.
  </li>
  <li>
    Usage 4: how many times a <strong>purchase</strong> event occurred + the
    total amount both of which are also available segmented into countries and
    application versions.
  </li>
  <li>
    Usage 5: how many times <strong>purchase</strong> event occurred + the total
    amount both of which are also available segmented into countries and application
    versions + the total duration of those events (under Timed Events topic below).
  </li>
</ul>
<p>
  <span class="wysiwyg-font-size-large">1. Event key and count</span>
</p>
<pre><code class="dart">// example for sending basic event
var event = {
  "key": "Basic Event",
  "count": 1
};

Countly.recordEvent(event);</code></pre>
<p>
  <span class="wysiwyg-font-size-large">2. Event key, count and sum</span>
</p>
<pre><code class="dart">// example for event with sum
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
<pre><code class="dart">// example for event with segment
var event = {
  "key": "Event With Segment",
  "count": 1
};

event["segmentation"] = {
  "country": "Germany",
  "app_version": "1.0",
  "rating": 10,
  "precision": 324.54678,
  "timestamp": 1234567890,
  "clicked": false,
  "languages": ["en", "de", "fr"],
  "sub_names": ["John", "Doe", "Jane"]
};

Countly.recordEvent(event);
</code></pre>
<p>
  <span class="wysiwyg-font-size-large">4. Event key, count and sum with segmentation(s)</span>
</p>
<pre><code class="dart">// example for event with segment and sum
var event = {
  "key": "Event With Sum And Segment",
  "count": 1,
  "sum": "0.99"
};

event["segmentation"] = {
  "country": "Germany",
  "app_version": "1.0",
  "rating": 10,
  "precision": 324.54678,
  "timestamp": 1234567890,
  "clicked": false,
  "languages": ["en", "de", "fr"],
  "sub_names": ["John", "Doe", "Jane"]
};

Countly.recordEvent(event);
</code></pre>
<p>
  <span class="wysiwyg-font-size-large">5. Event key, count, sum and duration with segmentation(s)</span>
</p>
<pre><code class="dart">// example for event with segment and sum
var event = {
  "key": "Event With Sum And Segment",
  "count": 1,
  "sum": "0.99",
  "duration": "0"
};

event["segmentation"] = {
  "country": "Germany",
  "app_version": "1.0",
  "rating": 10,
  "precision": 324.54678,
  "timestamp": 1234567890,
  "clicked": false,
  "languages": ["en", "de", "fr"],
  "sub_names": ["John", "Doe", "Jane"]
};

Countly.recordEvent(event);
</code></pre>
<h2 id="h_01H930GAQ5SWK23EQBNNRM4TZD">Timed Events</h2>
<p>
  It's possible to create timed events by defining a start and a stop moment.
</p>
<p>
  <span class="wysiwyg-font-size-large">1.Timed event with key</span>
</p>
<pre><code class="dart">// Basic event
Countly.startEvent("Timed Event");

Timer timer = Timer(new Duration(seconds: 5), () {
  Countly.endEvent({ "key": "Timed Event" });
});
</code></pre>
<p>
  <span class="wysiwyg-font-size-large">2.Timed event with key and sum</span>
</p>
<pre><code class="dart">// Event with sum
Countly.startEvent("Timed Event With Sum");

Timer timer = Timer(new Duration(seconds: 5), () {
  Countly.endEvent({ "key": "Timed Event With Sum", "sum": "0.99" });
});
</code></pre>
<p>
  <span class="wysiwyg-font-size-large">3.Timed event with key, count and segmentation</span>
</p>
<pre><code class="dart">// Event with segment
Countly.startEvent("Timed Event With Segment");

Timer timer = Timer(new Duration(seconds: 5), () {
  var event = {
    "key": "Timed Event With Segment",
    "count": 1,
  };
  event["segmentation"] = {
    "country": "Germany",
    "app_version": "1.0",
    "rating": 10,
    "precision": 324.54678,
    "timestamp": 1234567890,
    "clicked": false,
    "languages": ["en", "de", "fr"],
    "sub_names": ["John", "Doe", "Jane"]
  };
  Countly.endEvent(event);
});</code></pre>
<p>
  <span class="wysiwyg-font-size-large">4.Timed event with key, count, sum and segmentation</span>
</p>
<pre><code class="dart">// Event with Segment, sum and count
Countly.startEvent("Timed Event With Segment, Sum and Count");

Timer timer = Timer(new Duration(seconds: 5), () {
  var event = {
    "key": "Timed Event With Segment, Sum and Count",
    "count": 1,
    "sum": "0.99"
  };
  event["segmentation"] = {
    "country": "Germany",
    "app_version": "1.0",
    "rating": 10,
    "precision": 324.54678,
    "timestamp": 1234567890,
    "clicked": false,
    "languages": ["en", "de", "fr"],
    "sub_names": ["John", "Doe", "Jane"]
  };
  Countly.endEvent(event);
});</code></pre>
<h1 id="h_01H930GAQ5AHF46JK3WQ9Y7M01">Sessions</h1>
<h2 id="h_01H930GAQ5GC90X94VG7NAG6K1">Automatic Session Tracking</h2>
<p>
  Automatic sessions tracks user activity with respect to the app visibility. Basically
  it handles making certain requests to the server to inform it about the user
  session. Automatic sessions are enabled by default and SDK handles the necessary
  calls (by sending start session, update session and end session requests) to
  track a session automatically. This is how it works:
</p>
<ul>
  <li>
    <strong>Start/Begin session Request:</strong> It is sent to the server when
    the app comes back to the foreground from the background, and it includes
    basic metrics.
  </li>
  <li>
    <strong>Update Session Request:</strong> It automatically sends a periodical
    (60 sec by default) update session request while the app is in the foreground.
  </li>
  <li>
    <strong>End Session Request:</strong> It is sent at the end of a session
    when the app goes to the background or terminates.
  </li>
</ul>
<h2 id="h_01HGDN3SPBVME2S4HP5GM2D7NG">Manual Sessions</h2>
<p>
  Sometimes, it might be preferable to control the session manually instead of
  relying on the SDK.
</p>
<p>It can be enabled during init with:</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
</code>config.enableManualSessionHandling();</pre>
<p>Afterwards it is up to the implementer to make calls to:</p>
<ul>
  <li>Begin session (Starts a session)</li>
  <li>
    Update session duration (By default, you would call this every 60 seconds
    after beginning a session so that it is not closed server side. If you would
    want to increase that duration, you would have to increase the "<span>Maximal Session Duration" in your server API configuration)</span>
  </li>
  <li>End session (Ends and updates duration)</li>
</ul>
<p>You can use the 'sessions interface' to make these calls:</p>
<pre>Countly.instance.sessions.beginSession();
Countly.instance.sessions.updateSession();
Countly.instance.sessions.endSession();</pre>
<h1 id="h_01H930GAQ6R8N0G7CAPDJ60AN0">View Tracking</h1>
<p>
  The SDK provides access to all view-related functionality through the interface
  returned by:
</p>
<pre><code class="dart">Countly.instance.views</code></pre>
<h2 id="h_01H930GAQ6CANPDTP8H1K86K7W">Manual View Recording</h2>
<p>You can manually track views in your application.</p>
<p>
  When starting a view it would return an ID. This ID can be used to further interract
  with the view to pause, resume and stop it. You can start multiple views with
  the same name. The ID is used to uniquely identify the view.
</p>
<p>
  Views will be automatically paused when going to the background, and resumed
  when coming back.
</p>
<h3 id="h_01HFDVX9G293G57VFBANCB4GN6">Auto Stopped Views</h3>
<p>
  If you want to start a view that will be automatically stopped when starting
  another view, use the following method:
</p>
<pre><code class="dart">// record a view on your application
final String? viewID = await Countly.instance.views.<span>startAutoStoppedView</span>("Dashboard");</code></pre>
<p>
  <span style="font-weight: 400;">You can also specify the custom segmentation key-value pairs while starting views:</span>
</p>
<pre><code class="dart">Map&lt;String, Object&gt; segmentation = {
  "country": "Germany",
  "app_version": "1.0",
  "rating": 10,
  "precision": 324.54678,
  "timestamp": 1234567890,
  "clicked": false,
  "languages": ["en", "de", "fr"],
  "sub_names": ["John", "Doe", "Jane"]
};

final String? anotherViewID = Countly.instance.views.<span>startAutoStoppedView</span>("HomePage", segmentation);
</code></pre>
<h3 id="h_01HFDVXW74N8XR9TXQA8K7K3F8">Regular Views</h3>
<p>
  Opposed to "auto stopped views", with regular views you can have multiple of
  them started at the same time, and then you can control them independently. You
  can manually start a view using the <code>startView</code><span style="font-weight: 400;">method with a view name. This will <span>start tracking a view and return a unique identifier</span>, and the view will remain active until explicitly stopped using <code>stopViewWithName</code> or <code>stopViewWithID</code> </span>
</p>
<pre><code class="dart">// record a view on your application
Countly.instance.views.startView("HomePage");
final String? viewID = await Countly.instance.views.startView("Dashboard");</code></pre>
<p>
  <span style="font-weight: 400;">You can also specify the custom segmentation key-value pairs while starting views:</span>
</p>
<pre><code class="dart">Map&lt;String, Object&gt; segmentation = {
  "country": "Germany",
  "app_version": "1.0",
  "rating": 10,
  "precision": 324.54678,
  "timestamp": 1234567890,
  "clicked": false,
  "languages": ["en", "de", "fr"],
  "sub_names": ["John", "Doe", "Jane"]
};

final String? anotherViewID = Countly.instance.views.startView("HomePage", segmentation);</code></pre>
<h3 id="h_01HFDVY8YAXBP812A870NAZ6Q2">Stopping Views</h3>
<p>
  Stopping a view can either be done using the view id or the name. If there are
  multiple views with the same name (they would have different identifiers) and
  you try to stop one with that name, the SDK would close one of those randomly.
</p>
<p>Below you can see example ways of stopping views.</p>
<pre><code class="dart">Countly.instance.views.stopViewWithName("HomePage");</code></pre>
<p>
  This function allows you to manually stop the tracking of a view identified by
  its name.<span style="font-weight: 400;"> You can also specify the custom segmentation key-value pairs while stopping views:</span>
</p>
<pre><code class="dart">Countly.instance.views.stopViewWithName("HomePage", segmentation);</code></pre>
<p>
  You can also stop view tracking by its unique idetifier using
  <span style="font-weight: 400;"><code>stopViewWithID</code></span>
</p>
<pre><code class="dart">Countly.instance.views.stopViewWithID(viewID);</code></pre>
<p>
  <span style="font-weight: 400;">You can also specify the custom segmentation key-value pairs while stopping views:</span>
</p>
<pre><code class="dart">Countly.instance.views.stopViewWithID(anotherViewID, segmentation);</code></pre>
<p>
  You can stop all views tracking using
  <span style="font-weight: 400;"><code>stopAllViews</code></span>
</p>
<pre><code class="dart">Countly.instance.views.stopAllViews();</code></pre>
<p>
  <span style="font-weight: 400;">You can also specify the custom segmentation key-value pairs while stopping all views:</span>
</p>
<pre><code class="dart">Countly.instance.views.stopAllViews(segmentation);</code></pre>
<h3 id="h_01HFDVYJHTJKNHSYQAVYRRPPJE">Pausing and Resuming Views</h3>
<p>
  <span style="font-weight: 400;"></span>This SDK allows you to start multiple
  views at the same time. If you are starting multiple views at the same time it
  might be necessary for you to pause some views while others are still continuing.
  This can be achieved by using the unique identifier you get while starting a
  view.
</p>
<p>
  You can pause view tracking by its unique identifier using
  <span style="font-weight: 400;"><code>pauseViewWithID</code></span>
</p>
<pre><code class="dart">Countly.instance.views.pauseViewWithID(viewID);</code></pre>
<p>
  <span>This function temporarily pauses the tracking of a view identified by its unique identifier.</span>
</p>
<p>
  You can resume view tracking by its unique identifier using<span style="font-weight: 400;"> <code>resumeViewWithID:</code></span>
</p>
<pre><code class="dart">Countly.instance.views.resumeViewWithID(viewID);</code></pre>
<p>
  <span>This function resumes the tracking of a view identified by its unique identifier.</span>
</p>
<h3 id="h_01HK6YJTHP4Y0WVZSC0ZPNZFDJ">Adding Segmentation to Started Views</h3>
<p>
  You can add segmentation values to a view before it ends. This can be done as
  many times as desired and the final segmentation that will be send to the server
  would be the cumulative sum of all segmentations.
</p>
<p>
  So, once added, any segmentation key/value pairs will stay until that view ends.
  The only way to change it before it ends would be to provide a new value under
  the key you want to update. In that case, when a particular segmentation value
  for a specific key has been updated, only the latest value will be used.
</p>
<p>
  Here is an example on how to achieve that using the view name:
</p>
<pre><code class="dart">String viewName = 'HomePage';
await Countly.instance.views.startView(viewName);

Map&lt;String, Object&gt; segmentation = {
  "country": "Germany",
  "app_version": "1.0",
  "rating": 10,
  "precision": 324.54678,
  "timestamp": 1234567890,
  "clicked": false,
  "languages": ["en", "de", "fr"],
  "sub_names": ["John", "Doe", "Jane"]
};

await Countly.instance.views.addSegmentationToViewWithName(viewName, segmentation);</code></pre>
<p>
  Here is an example for how to add segmentation to a view using its ID:
</p>
<pre><code class="dart">String? viewID = await Countly.instance.views.startView('HomePage');

Map&lt;String, Object&gt; segmentation = {
  "country": "Germany",
  "app_version": "1.0",
  "rating": 10,
  "precision": 324.54678,
  "timestamp": 1234567890,
  "clicked": false,
  "languages": ["en", "de", "fr"],
  "sub_names": ["John", "Doe", "Jane"]
};

await Countly.instance.views.addSegmentationToViewWithID(viewID!, segmentation);</code></pre>
<h2 id="h_01HFDVW0B9P67GT7PWD4EB1J1A">Global View Segmentation</h2>
<p>
  It is possible to set global segmentation for all recorded views. This can be
  done either during initialization or subsequently. Segmentation provided with
  the start or stop calls will take precedence, and neither of them can override
  segmentation keys used by the SDK internally for views.
</p>
<p>
  For setting global segmentation values during SDK initialization, use the following
  method:
</p>
<pre><code class="dart">// set global segmentation at initialization
final CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setGlobalViewSegmentation(segmentation);</code></pre>
<p>
  If you want to change the segmentation after initialization, you can use one
  of the following methods.
</p>
<p>
  The<code>setGlobalViewSegmentation</code> method will replace the previously
  set values..
</p>
<pre><code class="dart">Countly.instance.views.setGlobalViewSegmentation(segmentation);</code></pre>
<p>
  The <code>updateGlobalViewSegmentation</code> method will modify the previously
  set values and overwrite any previously set keys.
</p>
<pre><code class="dart">Countly.instance.views.updateGlobalViewSegmentation(segmentation);</code></pre>
<h1 id="h_01H930GAQ65W1S9T2R1K2EQQFJ">Device ID Management</h1>
<p>
  A device ID is a unique identifier for your users. You may specify the device
  ID or allow the SDK to generate it. When providing your device ID, ensure it
  is unique for all users. Potential sources for such an ID include the username,
  email, or other internal ID used by your other systems.
</p>
<p>
  You may provide your custom device ID when initializing the SDK:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setDeviceId(DEVICE_ID);</code></pre>
<h2 id="h_01H930GAQ682G16Z7M570XKSPD">Changing the Device ID</h2>
<div class="callout callout--warning">
  <p>
    If you need a more complicated logic or using the SDK version 24.7.0 and
    below then you will need to use this method mentioned
    <a href="#h_01JCGHR95YCTVF6C81WF2B0FMW">here</a>.
  </p>
</div>
<p>You may configure or change the device ID anytime using:</p>
<pre><code class="dart">Countly.instance.deviceId.setID(DEVICE_ID);</code></pre>
<p>
  When using <code>setID</code>, the SDK determines internally if the device will
  be counted as a new device on the server or if it will merge the new and old
  IDs. If the previous ID was generated by the SDK (<code>DeviceIDType.SDK_GENERATED</code>),
  then <code>setID</code> merges the device ID. In any other case,
  <code>setID</code> changes the device ID without merging.
</p>
<p>
  Note: <code>setID</code> cannot be used to enter temporary ID mode.
</p>
<h2 id="h_01H930GAQ6PWYGR33SGRYFBE3R">Temporary Device ID</h2>
<div class="callout callout--warning">
  <p>
    If you need a more complicated logic or using the SDK version 24.7.0 and
    below then you will need to use this method mentioned
    <a href="#h_01JCGHWKDGDVRB9JNBQJ099QEX">here</a>.
  </p>
</div>
<p>
  You may use a temporary device ID mode to keep all requests on hold until the
  device ID is set later.
</p>
<p>
  You can enable temporary device ID mode when initializing the SDK:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.enableTemporaryDeviceIDMode();

// Initialize with that configuration
Countly.initWithConfig(config);</code></pre>
<p>
  To enable a temporary device ID after initialization, you can call:
</p>
<pre><code class="dart">Countly.instance.deviceId.enableTemporaryIDMode();</code></pre>
<p>
  The SDK will be in temporary device ID mode, all requests will be on hold and
  they will be persistently stored.
</p>
<p>
  When in temporary device ID mode, method calls for presenting feedback widgets
  and updating remote config will be ignored.
</p>
<p>
  Later, when a new device ID is set using
  <code class="dart">Countly.instance.deviceId.setID(DEVICE_ID);</code> method,
  all requests that have been kept on hold will be sent with the new device ID.
</p>
<h2 id="h_01H930GAQ6PX99Z205GC9DDZ1J">Retrieving Current Device ID</h2>
<p>
  You may want to see what the current device ID is. For that, you can use the
  following call:
</p>
<pre><code class="dart">String? currentDeviceId = Countly.instance.deviceId.getID();</code></pre>
<p>
  <span>You can use </span><code>getIDType</code> method which returns a
  <code>DeviceIDType</code><span> to get the current device ID type. The ID type is an enum with the possible values of: </span>
</p>
<ul>
  <li>
    <span>"DEVELOPER_SUPPLIED" - device ID was supplied by the host app.</span>
  </li>
  <li>
    <span>"SDK_GENERATED" - device ID was generated by the SDK.</span>
  </li>
  <li>
    <span>"TEMPORARY_ID" - the SDK is in temporary device ID mode.</span>
  </li>
</ul>
<pre><code class="dart">DeviceIdType? deviceIdType = await Countly.instance.deviceId.getIDType();</code></pre>
<h2 id="h_01H930GAQ61FQNZ1X9NS4QSA4N">Device ID Generation</h2>
<p>
  When the SDK is initialized for the first time with no device ID, it will generate
  a device ID.
</p>
<p>
  Here are the underlying mechanisms used to generate that value for some platforms:
</p>
<p>
  For iOS: the device ID generated by the SDK is the Identifier For Vendor (IDFV).
  For Android: the device ID generated by the SDK is the OpenUDID.
</p>
<h1 id="h_01H930GAQ6K5T1NRS29Z3Y8WSY">Push Notifications</h1>
<p>
  Countly gives you the ability to send Push Notifications to your users using
  your app with the Flutter SDK integration. For more information on how to best
  use this feature you can check
  <a href="https://support.count.ly/hc/en-us/articles/4405405459225-Push-Notifications" target="_blank" rel="noopener noreferrer">this</a>
  article.
</p>
<p>
  To make this feature work you will need to make some configurations both in your
  app and at your Countly server. Both platforms (Android and iOS) would need different
  steps to integrate Push Notification feature into your application, as explained
  below.
</p>
<h2 id="h_01H930GAQ6AQ5REWTYT4CB27CQ">Integration</h2>
<h3 id="h_01H930GAQ6C3B3RYSEXZX4ZY3F">Android Setup</h3>
<p>
  Step 1: For FCM credentials setup please follow the instruction from
  <a href="https://support.count.ly/hc/en-us/articles/360037754031-Android#h_01HNF9WBDT037TDHVHRSEPEMZV" target="_blank" rel="noopener noreferrer">here</a>.
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
<pre><code class="xml">&lt;application ...&gt;
...
  &lt;service android:name="ly.count.dart.countly_flutter.CountlyMessagingService"&gt;
    &lt;intent-filter&gt;
      &lt;action android:name="com.google.firebase.MESSAGING_EVENT" /&gt;
    &lt;/intent-filter&gt;
  &lt;/service&gt;
&lt;/application&gt;
</code></pre>
<p>
  Step 6: Add the following line in file <code>android/build.gradle</code>
</p>
<pre><code class="dart">buildscript {
  dependencies {
    classpath 'com.google.gms:google-services:4.3.15'
    }
}
</code></pre>
<p>
  You can get the latest version from
  <a href="https://firebase.google.com/support/release-notes/android#latest_sdk_versions" target="_blank" rel="noopener noreferrer">here</a>
  and
  <a href="https://developers.google.com/android/guides/google-services-plugin" target="_blank" rel="noopener noreferrer">here.</a>
</p>
<p>
  Step 7: Add the following line in file <code>android/app/build.gradle</code>
</p>
<pre><code class="dart">dependencies {
  implementation 'ly.count.android:sdk:22.02.1'
  implementation 'com.google.firebase:firebase-messaging:20.0.0'
}
// Add this at the bottom of the file
apply plugin: 'com.google.gms.google-services'
</code></pre>
<h3 id="h_01H930GAQ6VJHE7EZ937JJ6HB9">iOS Setup</h3>
<p>
  First, you will need to acquire Push Notification credentials from Apple. (If
  you don't have them you can check
  <a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#h_01HNF5NPFR0W8WJ1BW8WVXJ5AB" target="_blank" rel="noopener noreferrer">this</a>
  article to learn how you can do it.)
</p>
<p>
  Then you would need to upload these credentials to your Countly server. You can
  refer to
  <a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#h_01HNF5QRPJGG0GKMMH2SZWVK85" target="_blank" rel="noopener noreferrer">this</a>
  article for learning how you can do that.
</p>
<p>
  Finally, under the Capabilities section of Xcode, enable
  <strong>Push Notifications</strong> and the
  <strong>Remote notifications Background Mode</strong> for your target.
</p>
<p>
  For Swift projects you might need to make sure Bridging Header File is configured
  properly for each target as explained
  <a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#h_01HAVHW0RT9DP8543XYWP278JC" target="_blank" rel="noopener noreferrer">here</a>.
  For this purpose you can find <code>CountlyNotificationService.h/m</code> file
  under:
</p>
<pre><code class="bash">Pods/Development Pods/Countly/{PROJECT_NAME}/ios/.symlinks/plugins/countly_flutter/ios/Classes/CountlyiOS/CountlyNotificationService.h/m</code></pre>
<p>Some tips to find the files from deep hierarchy:</p>
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
<p>You can drag and drop the file from Pod to Compile Sources.</p>
<div class="img-container">
  <img src="/guide-media/01GVCKG6BTNK2EK9JYCG3SR73X" alt="Flutter_iOS_Notifications.png">
</div>
<h2 id="h_01H930GAQ6FAB8TBJDJXW2F2A7">Enabling Push</h2>
<p>
  First, when setting up push for the Flutter SDK, you would first select the push
  token mode. This would allow you to choose either test or production modes, push
  token mode should be set before init.
</p>
<pre><code class="dart">// Set messaging mode for push notifications
Countly.pushTokenType(Countly.messagingMode["TEST"]);</code></pre>
<p>
  When you are finally ready to initialise Countly push, you would call this:
</p>
<pre><code class="dart">// This method will ask for permission, enables push notification and send push token to countly server.
Countly.askForNotificationPermission();</code></pre>
<p>
  Also it is important to note that push notification is enabled for iOS by default,
  so to disable you need to call <code>disablePushNotifications</code> method:
</p>
<pre><code class="dart">// Disable push notifications feature for iOS, by default it is enabled.
Countly.disablePushNotifications();</code></pre>
<h2 id="h_01HNFJBRCKHFFZZYWK1CD485FT">Removing Push and Its Dependencies</h2>
<p>
  Countly Flutter SDK comes with push notification capabilities embedded. For the
  flavor without the push notifications features (like Firebase libraries) please
  check <a href="https://pub.dev/packages/countly_flutter_np">here</a>.
</p>
<h2 id="h_01H930GAQ67F7994ZMTG30J1C5">Handling Push Callbacks</h2>
<p>
  To register a Push Notification callback after initializing the SDK, use the
  method below.
</p>
<pre>Countly.onNotification((String notification) {
  print(notification);
});</pre>
<p>
  In order to listen to notification receive and click events, Place below code
  in <code>AppDelegate.swift</code>
</p>
<p>Add header files</p>
<pre><code class="dart">import countly_flutter
</code></pre>
<p>Add these methods:</p>
<pre><code class="dart">// Required for the notification event. You must call the completion handler after handling the remote notification.
func application(application: UIApplication,  didReceiveRemoteNotification userInfo: [NSObject : AnyObject],  fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -&gt; Void) {
  CountlyFlutterPlugin.onNotification(userInfo);
  completionHandler(.newData);
}

@available(iOS 10.0, \*)
override func userNotificationCenter(_ center: UNUserNotificationCenter, willPresent notification: UNNotification, withCompletionHandler completionHandler: @escaping (_ options: UNNotificationPresentationOptions) -&gt; Void) {

  //Called when a notification is delivered to a foreground app.

  let userInfo: NSDictionary = notification.request.content.userInfo as NSDictionary
  CountlyFlutterPlugin.onNotification(userInfo as? [AnyHashable : Any])
}

@available(iOS 10.0, \*)
override func userNotificationCenter(\_ center: UNUserNotificationCenter, didReceive response: UNNotificationResponse, withCompletionHandler completionHandler: @escaping () -&gt; Void) {

  // Called to let your app know which action was selected by the user for a given notification.
  let userInfo: NSDictionary = response.notification.request.content.userInfo as NSDictionary
  // print("\(userInfo)")
  CountlyFlutterPlugin.onNotification(userInfo as? [AnyHashable : Any])
}
</code></pre>
<h3 id="h_01H930GAQ6GZBENE2SZZF3NGS3">Data Structure Received in Push Callbacks</h3>
<p>
  Here is the example of how data will receive in push callbacks:<img src="/guide-media/01GVDG0K4G51KAKZJZVZHNYQ4A" alt="Screenshot_2022-06-24_at_7.04.23_PM.png">
  Data Received for Android platform:
</p>
<pre>{
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
}</pre>
<p>Data Received for iOS platform:</p>
<pre>{
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
}</pre>
<h1 id="h_01H930GAQ69F33CMKEBBV57FVB">User Location</h1>
<p>
  Countly allows you to send geolocation-based push notifications to your users.
  By default, the Countly Server uses the GeoIP database to deduce a user's location.
</p>
<h2 id="h_01H930GAQ6EQZ7TBJWV2KWWSVN">Set User Location</h2>
<p>
  If your app has a different way of detecting location, you may send this information
  to the Countly Server by using the <code>setLocation</code> of&nbsp;
  <code>CountlyConfig</code> during init or<code>setUserLocation</code> method
  after init.
</p>
<p>
  When setting user location information, you would be setting these values:
</p>
<ul>
  <li>
    <code>countryCode</code> a string in ISO 3166-1 alpha-2 format country code
  </li>
  <li>
    <code>city</code> a string specifying city name
  </li>
  <li>
    <code>location</code> a string comma-separated latitude and longitude
  </li>
  <li>
    <code>IP</code> a string specifying an IP address in IPv4 or IPv6 formats
  </li>
</ul>
<p>
  <span>All values are optional, but at least one should be set.</span>
</p>
<pre><code class="dart">// Example for setLocation
CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setLocation(country_code: 'TR', city: 'Istanbul', gpsCoordinates: '41.0082,28.9784', ipAddress: '10.2.33.12')</code></pre>
<p>
  Geolocation recording methods may also be called at any time after the Countly
  SDK has started. To do so, use the <code>setUserLocation</code> method as shown
  below.
</p>
<pre><code class="dart">// Example for setUserLocation
Countly.setUserLocation(countryCode: 'TR', city: 'Istanbul', gpsCoordinates: '41.0082,28.9784', ipAddress: '10.2.33.12');
</code></pre>
<h2 id="h_01H930GAQ6ZJ0P4SAE3CF0H47J">Disable Location</h2>
<p>
  To erase any cached location data from the device and stop further location tracking,
  use the following method. Note that if after disabling location, the
  <code>setUserLocation</code> is called with any non-null value, tracking will
  resume.
</p>
<pre><code class="dart">//disable location tracking
Countly.disableLocation();</code></pre>
<h1 id="h_01H930GAQ6GWEATBC0DAVDHW7R">Remote Config</h1>
<p>
  <span style="font-weight: 400;">Remote config allows you to modify how your app functions or looks by requesting key-value pairs from your Countly server. The returned values may be modified based on the user properties. For more details, please see the </span><a href="https://support.count.ly/hc/en-us/articles/360037270492-Remote-config"><span style="font-weight: 400;">Remote Config documentation</span></a><span style="font-weight: 400;">.</span>
</p>
<p>
  Once downloaded, Remote config values will be saved persistently and available
  on your device between app restarts unless they are erased.
</p>
<p>
  <span style="font-weight: 400;">The two ways of acquiring remote config data are enabling automatic download triggers or manual requests.</span>
</p>
<p>
  If a full download of remote config values is performed, the previous list of
  values is replaced with the new one. If a partial download is performed, only
  the retrieved keys are updated, and values that are not part of that download
  stay as they were. A previously valid key may return no value after a full download.
</p>
<div>
  <h2 id="h_01HD1KQCFTNES9EPJAT0DWT0HJ">
    <span>Downloading Values</span>
  </h2>
  <h3 id="h_01H930GAQ7BDR4FWH4NCATN7B4">Automatic Remote Config Triggers</h3>
  <p>
    <span style="font-weight: 400;">Automatic remote config triggers have been turned off by default; therefore, no remote config values will be requested without developer intervention.</span>
  </p>
  <p>
    <span style="font-weight: 400;">The automatic download triggers that would trigger a full value download are:</span>
  </p>
  <ul>
    <li>
      <span style="font-weight: 400;">when the SDK has finished initializing</span>
    </li>
    <li>
      <span style="font-weight: 400;">after the device ID is changed without merging</span>
    </li>
    <li>
      <span style="font-weight: 400;">when user gets out of temp ID mode</span>
    </li>
    <li>
      <span style="font-weight: 400;">when <code>CountlyConsent.remoteConfig</code> consent is given after it had been removed before (if consents are enabled)</span>
    </li>
  </ul>
  <p>
    To enable the automatic triggers, you have to call
    <code class="dart">enableRemoteConfigAutomaticTriggers</code> on the configuration
    object you will provide during init.
  </p>
  <pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY)
  ..enableRemoteConfigAutomaticTriggers(); // necessary to enable the feature
</code></pre>
  <p>
    Another thing you can do is to enable value caching with the
    <code class="dart">enableRemoteConfigValueCaching</code> flag. If all values
    were not updated, you would have metadata indicating if a value belongs to
    the old or current user.
  </p>
  <pre>CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY) 
  ..enableRemoteConfigValueCaching(); </pre>
</div>
<h3 id="h_01H930GAQ68M62GD62G8JC2ZVC">Manually Calls</h3>
<p>
  There are three ways to trigger remote config value download manually:
</p>
<ul>
  <li>
    <span style="font-weight: 400;">Manually downloading all keys</span>
  </li>
  <li>
    <span style="font-weight: 400;">Manually downloading specific keys</span>
  </li>
  <li>Manually downloading, omitting (everything except) keys.</li>
</ul>
<p>
  <span style="font-weight: 400;">Each of these calls also has an optional parameter that you can provide a RCDownloadCallback to, which would be triggered when the download attempt has finished.</span>
</p>
<p>
  <span style="font-weight: 400;"><code class="java">dowloadAllKeys</code></span><span style="font-weight: 400;">&nbsp;is</span><span style="font-weight: 400;"> the same as the automatically triggered update - it replaces all stored values with the ones from the server (all locally stored values are deleted and replaced with new ones).</span>
</p>
<p>
  <span style="font-weight: 400;">Or you might only want to update specific key values. To do so, you will need to call <code class="dart">downloadSpecificKeys</code> to downloads new values for the wanted keys. Those are provided with a String array.</span>
</p>
<p>
  <span style="font-weight: 400;">Or you might want to update all the values except a few defined keys. To do so,&nbsp; call <code class="dart">downloadOmittingKeys</code> would update all values except the provided keys</span><span style="font-weight: 400;">. The keys are provided with a String array.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">All Keys</span>
    <span class="tabs-link">Certain Keys</span>
    <span class="tabs-link">Omit Keys</span>
  </div>
  <div class="tab">
    <pre><code class="dart">Countly.instance.remoteConfig.downloadAllKeys((rResult, error, fullValueUpdate, downloadedValues) {
  if (rResult == RequestResult.Success) {
    // do sth
  } else {
    // do sth
  }
});</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="dart">Countly.instance.remoteConfig.downloadSpecificKeys(List&lt;String&gt; keysToInclude, (rResult, error, fullValueUpdate, downloadedValues) {
  if (rResult == RequestResult.Success) {
    // do sth
  } else {
    // do sth
  }
});</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="dart">Countly.instance.remoteConfig.downloadOmittingKeys(List&lt;String&gt; keysToExclude, (rResult, error, fullValueUpdate, downloadedValues) {
  if (rResult == RequestResult.Success) {
    // do sth
  } else {
    // do sth
  }
});</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">When making requests with an "inclusion" or "exclusion" array, if those arrays are empty or null, they will function the same as a <code class="java">dowloadAllKeys</code> request and will update all the values. This means it will also erase all keys not returned by the server.</span>
</p>
<h2 id="h_01HD1KX616GDFGTV2AR8BSWWG9">Accessing Values</h2>
<p>
  To get a stored value, call <code class="dart">getValue</code> with the specified
  key. This returns an Future&lt;RCData&gt; object that contains the value of the
  key and the metadata about that value's owner. If value in RCData was
  <code>null</code>
  <span style="font-weight: 400;">then no value was found or the value was <code>null</code>.</span>
  &nbsp;
</p>
<pre><code class="dart">Object? value_1 = await Countly.instance.remoteConfig.getValue("key_1").value;
Object? value_2 = await Countly.instance.remoteConfig.getValue("key_2").value;
Object? value_3 = await Countly.instance.remoteConfig.getValue("key_3").value;
Object? value_4 = await Countly.instance.remoteConfig.getValue("key_4").value;

int intValue = value1 as int;
double doubleValue = value2 as double;
JSONArray jArray = value3 as JSONArray;
JSONObject jObj = value4 as JSONObject;
</code></pre>
<p>
  If you want to get all values together you can use
  <code class="dart">getAllValues</code> which returns a Future&lt;Map&lt;String,
  RCData&gt;&gt;.
  <span style="font-weight: 400;">The SDK does not know the returned value type, so, it will return the <code>Object</code></span><span style="font-weight: 400;">. The developer then needs to cast it to the appropriate type. The returned values may also be <code>JSONArray</code></span><span style="font-weight: 400;">,&nbsp;</span><code>JSONObject</code>,
  or just a simple value, such as <code>int</code>.
</p>
<pre><code class="dart">Map&lt;String, RCData&gt; allValues = await Countly.instance.remoteConfig.getAllValues();

int intValue = allValues["key_1"] as int;
double doubleValue = allValues["key_2"] as double;
JSONArray jArray = allValues["key_3"] as JSONArray;
JSONObject jObj = allValues["key_4"] as JSONObject;</code></pre>
<p>
  RCData object has two keys: value (Object) and isCurrentUsersData (Boolean).
  Value holds the data sent from the server for the key that the RCData object
  belongs to. The isCurrentUsersData is only false when there was a device ID change,
  but somehow (or intentionally) a remote config value was not updated.
</p>
<pre><code class="dart">Class RCData {
  Object value;
  Boolean isCurrentUsersData;
}</code></pre>
<h2 id="01HD1KQVYS1NHR0ZFMJ12AVP0P">Clearing Stored Values</h2>
<p>
  <span style="font-weight: 400;">At some point, you might like to erase all the values downloaded from the server. You will need to call one function to do so.</span>
</p>
<pre>Countly.instance.remoteConfig.clearAll();</pre>
<h2 id="h_01H930GAQ738M1K5HJR3DMHMCN">Global Download Callbacks</h2>
<p>
  Also, you may provide a global callback function to be informed when the remote
  config download request is finished with
  <code class="dart">remoteConfigRegisterGlobalCallback</code> during the SDK initialization:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY) 
  ..remoteConfigRegisterGlobalCallback((rResult, error, fullValueUpdate, downloadedValues) {
    if (error != null) {
      // do sth
    }
  })
</code></pre>
<p>
  RCDownloadCallback is called when the remote config download request is finished,
  and it would have the following parameters:
</p>
<ul>
  <li>
    <code class="dart">rResult</code>: RequestResult Enum (either
    <span class="hljs-built_in">Error</span><span>, Success or NetworkIssue</span>)
  </li>
  <li>
    <code class="dart">error</code>: String (error message. "null" if there is
    no error)
  </li>
  <li>
    <code class="dart">fullValueUpdate</code>: boolean ("true" - all values updated,
    "false" - a subset of values updated)
  </li>
  <li>
    <code class="dart">downloadedValues</code>: Map&lt;String, RCData&gt; (the
    whole downloaded remote config values)
  </li>
</ul>
<pre><code class="dart">RCDownloadCallback {
  void callback(RequestResult rResult, String error, boolean fullValueUpdate, Map&lt;String, RCData&gt; downloadedValues)
}
</code></pre>
<p>
  <code class="dart">downloadedValues</code> would be the downloaded remote config
  data where the keys are remote config keys, and their value is stored in RCData
  class with metadata showing to which user data belongs. The data owner will always
  be the current user.
</p>
<p>
  You can also register (or remove) callbacks to do different things after the
  SDK initialization. You can register these callbacks multiple times:
</p>
<pre><code class="dart">// register a callback
Countly.instance.remoteConfig.registerDownloadCallback((rResult, error, fullValueUpdate, downloadedValues) {
  // do sth
});

// remove a callback
Countly.instance.remoteConfig.removeDownloadCallback((rResult, error, fullValueUpdate, downloadedValues) {
  // do sth
});</code></pre>
<h2 id="h_01H930GAQ6KZKGR0NMP6QM2JW6">A/B Testing</h2>
<p>
  You can enroll your users into into A/B tests for certain keys or remove them
  from some or all existing A/B tests available.
</p>
<div>
  <h3 id="h_01HD1KX616DPMYXJCCRQ01XAFQ">
    <span>&nbsp;</span><span>Enrollment on Download</span>
  </h3>
  <p>
    You can enroll into the A/B tests automatically whenever you download RC
    values from the server. To do so you have to set the following flag at the
    config object during initialization:
  </p>
  <pre>CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY)
..<span>enrollABOnRCDownload();</span></pre>
  <h3 id="h_01HD1KX6164ZKKCQS4B15G1NC5">
    <span>&nbsp;</span><span>Enrollment on Access</span>
  </h3>
  <p>
    <span>You can also enroll to A/B tests while getting RC values from storage. You can use <code>getValueAndEnroll</code> while getting a single value and <code>getAllValuesAndEnroll</code> while getting all values to enroll to the keys that exist. If no value was stored for those keys these functions would not enroll the user. Both of these functions works the same way with their non-enrolling variants, namely; <code>getValue</code> and <code>getAllValues</code>.</span>
  </p>
  <h3 id="h_01HD1KX6170D1FV7M4HHS1NGTE">
    <span>&nbsp;</span><span>Enrollment on Action</span>
  </h3>
  <p>
    To enroll a user into the A/B tests for the given keys you use the following
    method:
  </p>
  <pre>Countly.instance.remoteConfig.enrollIntoABTestsForKeys(List&lt;String&gt; keys);</pre>
  <p>
    Here the keys array is the mandatory parameter for this method to work.
  </p>
  <h3 id="h_01HD1KX617T07K6KD77Q4THRCC">
    <span>Exiting A/B Tests</span>
  </h3>
</div>
<p>
  If you want to remove users from A/B tests of certain keys you can use the following
  function:
</p>
<pre>Countly.instance.remoteConfig.exitABTestsForKeys(List&lt;String&gt; keys);</pre>
<p>
  Here if no keys are provided it would remove the user from all A/B tests instead.
</p>
<h1 id="h_01H930GAQ71TKNV8BD6Q0F4P8H">User Feedback</h1>
<p>
  There are two ways to receive user feedback: the Star Rating Dialog and the Feedback
  Widgets (Survey, NPS, Rating).
</p>
<p>
  The Star Rating Dialog allows users to give feedback as a rating from 1 to 5.
  Feedback Widgets allow for even more textual feedback from users.
</p>
<h2 id="h_01H930GAQ75H8R1SPMVD66PD2N">Star Rating Dialog</h2>
<p>
  Star Rating Dialog provides a dialog for getting user's feedback about the application.
  It contains a title, a simple message explaining what it is for, a 1-to-5 star
  meter for getting users' ratings, and a dismiss button in case the user does
  not want to give a rating.
</p>
<p>
  This star-rating has nothing to do with Google Play Store ratings and reviews.
  It is just for getting brief feedback from users, to be displayed on the Countly
  dashboard. If the user dismisses star rating dialog without giving a rating,
  the event will not be recorded.
</p>
<pre><code class="dart">Countly.askForStarRating();</code></pre>
<p>
  The star-rating dialog's title, message, and dismiss button text may be customized
  through the following functions:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setStarRatingTextTitle("Custom title"); // Only available for Android
config.setStarRatingTextMessage("Custom message");
config.setStarRatingTextDismiss("Custom message"); // Only available for Android</code></pre>
<h2 id="h_01H930GAQ7XASR12CMDC11Q265">Feedback Widget</h2>
<div class="callout callout--info">
  <p>
    Feedback Widgets is a
    <a href="https://countly.com/enterprise" target="_blank" rel="noopener noreferrer">Countly Enterprise</a>
    plugin.
  </p>
</div>
<p>
  It is possible to display 3 kinds of feedback widgets:
  <a href="https://support.count.ly/hc/en-us/articles/4652903481753-Feedback-Surveys-NPS-and-Ratings-#h_01HAY62C2QB9K7CRDJ90DSDM0D" target="_blank" rel="noopener">NPS</a>,
  <a href="https://support.count.ly/hc/en-us/articles/4652903481753-Feedback-Surveys-NPS-and-Ratings-#h_01HAY62C2Q965ZDAK31TJ6QDRY" target="_blank" rel="noopener">Survey</a>
  and
  <a href="https://support.count.ly/hc/en-us/articles/4652903481753-Feedback-Surveys-NPS-and-Ratings-#h_01HAY62C2R4S05V7WJC5DEVM0N" target="_blank" rel="noopener">Rating</a>.
  All widgets are shown as webviews and should be approached using the same methods.
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
  When the widgets are created, you need to use 2 calls in your SDK: one to get
  all available widgets for a user and another to display a chosen widget.
</p>
<p>To get your available widget list, use the call below.</p>
<pre><code class="dart">FeedbackWidgetsResponse feedbackWidgetsResponse = await Countly.getAvailableFeedbackWidgets() ;</code></pre>
<p>
  From the callback you would get
  <code class="dart">FeedbackWidgetsResponse</code> object which contains the list
  of all available widgets that apply to the current device id.
</p>
<p>The objects in the returned list look like this:</p>
<pre><code class="dart">class CountlyPresentableFeedback {
  public String widgetId;
  public String type;
  public String name;
}</code></pre>
<p>
  To determine what kind of widget that is, check the "type" value.
</p>
<p>Potential 'type' values are:</p>
<pre>FeedbackWidgetType {survey, nps, rating}</pre>
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
<pre><code class="dart">await Countly.presentFeedbackWidget(widgets.first, 'Close', widgetShown: () {
  print('Widget Appeared');
}, widgetClosed: () {
  print('Widget Dismissed');
});</code></pre>
<p>
  <code class="dart">widgetShown</code> and
  <code class="dart">widgetClosed</code> are optional callbacks, you can pass these
  callbacks if you want to perform some actions when widget appear or dismiss.
</p>
<h3 id="h_01H930GAQ7HMVWZBVTXTCDTF50">Manual Reporting</h3>
<p>
  There might be some use-cases where you might to use the native UI or a custom
  UI you have created instead of our webview solution. In those cases you would
  have to request all the widget related information and then report the result
  manually.
</p>
<p>
  For a sample integration, have a look at our sample app in the repo.
</p>
<p>
  First you would need to retrieve the available widget list with the previously
  mentioned <code>getAvailableFeedbackWidgets</code> call. After that you would
  have a list of possible <code>CountlyPresentableFeedback</code> objects. You
  would pick the one widget you would want to display.
</p>
<p>
  Having the <code>CountlyPresentableFeedback</code> object of the widget you would
  want to display, you could use the '<code class="dart">getFeedbackWidgetData</code>'&nbsp;
  method to retrieve the widget information with an optional 'onFinished' callback.
  In case you want to use with callback then you can call '<code class="dart">getFeedbackWidgetData</code>'
  in this way:
</p>
<pre><code class="dart">Countly.getFeedbackWidgetData(chosenWidget, onFinished: (retrievedWidgetData, error) {
  if (error == null) {
  }
});</code></pre>
<p>
  If you want to use it without a callback then you can call '<code class="dart">getFeedbackWidgetData</code>'
  in this way:
</p>
<pre><code class="dart">List result = await Countly.getFeedbackWidgetData(chosenWidget);
String? error = result[1];
if (error == null) {
  Map&lt;String, dynamic&gt; retrievedWidgetData = result[0];
}</code></pre>
<p>
  <code>retrievedWidgetData</code> would contain a Map with all of the required
  information to present the widget yourself.
</p>
<p>
  After you have collected the required information from your users, you would
  package the responses into a <code>Map&lt;String, Object&gt;</code> and then
  use it, the widgetInformation and the widgetData to report the feedback result
  with the following call:
</p>
<pre><code class="dart">//this contains the reported results
Map&lt;String, Object&gt; reportedResult = {};

//
// You would fill out the results here. That step is not displayed in this sample
//

//report the results to the SDK
Countly.reportFeedbackWidgetManually(chosenWidget, retrievedWidgetData , reportedResult);
</code></pre>
<p>
  If the user would have closed the widget, you would report that by passing a
  "null" reportedResult.
</p>
<p>
  For more information regarding how to structure the reported result, you would
  look
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts" target="_self">here</a>.
</p>
<h2 id="h_01J21BAQ9RWS12RS2C7JTRGD4A">Consent</h2>
<p>
  If consents are enabled, to use Feedback Widgets, you have to provide the 'feedback'
  consent and to use Star Rating Dialog you have to provide the 'starRating' consent
  for these features to work.
</p>
<h1 id="h_01H930GAQ7DZQB56330E1PGK1E">User Profiles</h1>
<p>
  Using the following calls, you can set key/value to the visitors user profile.
  After you send user data, it can be viewed under the User Profiles menu.
</p>
<p>
  Note that this feature is available only for Enterprise Edition.
</p>
<p>
  You would call <code>Countly.instance.userProfile.</code> to see the available
  functionality for modifying user properties.
</p>
<p>
  If a property is set as an empty string, it will be deleted from the user on
  the server side.
</p>
<h2 id="h_01H930GAQ7J7R8CVHTSYM34ZM9">Setting User profile values during init</h2>
<p>
  If possible set user properties during initialization. This way they would be
  reflected when the session is started shortly.
</p>
<p>
  Using the following call, you can set both the predefined and the custom user
  properties during initialization:
</p>
<pre><code class="dart">var userProperties = {
  "customProperty": "custom Value",
  "username": "USER_NAME",
  "email": "USER_EMAIL"
};
CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setUserProperties(userProperties); </code></pre>
<h2 id="setting-user-profile-values-during-init" class="anchor-heading">Setting User profile values</h2>
<p>Ther following calls can be used after init.</p>
<p>
  If you want to set a single property, you can call
  <code class="dart">Countly.instance.userProfile.setProperty(key, value)</code>
</p>
<pre>Countly.instance.userProfile.setProperty("specialProperty", "value");
Countly.instance.userProfile.save();</pre>
<p>
  If you want to set multiple properties at the same time, you can use:
  <code class="dart">Countly.instance.userProfile.setUserProperties(userProperties)</code>
</p>
<pre><code class="dart">// example for setting user data
Map&lt;String, Object&gt; userProperties= {
  "name": "Nicola Tesla",
  "username": "nicola",
  "email": "info@nicola.tesla",
  "organization": "Trust Electric Ltd",
  "phone": "+90 822 140 2546",
  "picture": "http://images2.fanpop.com/images/photos/3300000/Nikola-Tesla-nikola-tesla-3365940-600-738.jpg",
  "picturePath": "",
  "gender": "M", // "F"
  "byear": "1919",
  "special_value": "something special"
};
Countly.instance.userProfile.setUserProperties(userProperties);
Countly.instance.userProfile.save();</code></pre>
<p>
  After you have provided the user profile information, you must save it by calling
  <code class="dart">Countly.instance.userProfile.save()</code>. This would then
  create a request and send it to the server.
</p>
<p>
  If you changed your mind and want to clear the currently prepared values, call
  <code class="dart">Countly.instance.userProfile.clear()</code>before calling
  "save".
</p>
<h2 id="h_01H930GAQ793MEBMSC774K6VFM">Modifying custom data</h2>
<p>
  Additionally, you can do different manipulations on your custom data values,
  like increment current value on the server or store an array of values under
  the same property.
</p>
<p>Below is the list of available methods:</p>
<pre><code class="dart">//increment used value by 1
Countly.instance.userProfile.increment("increment");
//increment used value by provided value
Countly.instance.userProfile.incrementBy("incrementBy", 10);
//multiply value by provided value
Countly.instance.userProfile.multiply("multiply", 20);
//save maximal value
Countly.instance.userProfile.saveMax("saveMax", 100);
//save minimal value
Countly.instance.userProfile.saveMin("saveMin", 50);
//set value if it does not exist
Countly.instance.userProfile.setOnce("setOnce", 200);

//insert value to array of unique values
Countly.instance.userProfile.pushUnique("type", "morning");;
//insert value to array which can have duplicates
Countly.instance.userProfile.push("type", "morning");
//remove value from array
Countly.instance.userProfile.pull("type", "morning");

//call 'save' to persist the changes
Countly.instance.userProfile.save();</code></pre>
<h1 id="h_01H930GAQ7PNW0DA85DV7PK2EJ">Application Performance Monitoring</h1>
<p>
  The SDK provides manual and automatic mechanisms for Application Performance
  Monitoring (APM). All of the automatic mechanisms are disabled by default and
  to start using them you would first need to enable them and give the required
  consent if it was required:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);

// this interface exposes the available APM features and their modifications.
config.apm. </code></pre>
<p>
  While using APM calls, you have the ability to provide trace keys by which you
  can track those parameters in your dashboard.
</p>
<h2 id="h_01H930GAQ7ASS6HMSKF6HMPEMX">Custom Traces</h2>
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
<pre><code class="dart">Countly.startTrace(traceKey);</code></pre>
<p>To end a custom trace, use:</p>
<pre><code class="dart">String traceKey = "Trace Key";
Map&lt;String, int&gt; customMetric = {
  "ABC": 1233,
  "C44C": 1337
};
Countly.endTrace(traceKey, customMetric);</code></pre>
<p>
  In this sample, a Map of integer values is provided when ending a trace. Those
  will be added to that trace in the dashboard.
</p>
<h2 id="h_01H930GAQ7BZESXJYJ893PHR18">Network Traces</h2>
<p>
  You can use the APM to track your requests. You would record the required info
  for your selected approach of making network requests and then call this after
  your network request is done:
</p>
<pre><code class="dart">Countly.recordNetworkTrace(networkTraceKey, responseCode, requestPayloadSize, responsePayloadSize, startTime, endTime);</code></pre>
<p>
  <code>networkTraceKey</code> is a unique identifier of the API endpoint you are
  targeting or just the url you are targeting, all params should be stripped. You
  would also provide the received response code, sent payload size in bytes, received
  payload size in bytes, request start time timestamp in milliseconds, and request
  end finish timestamp in milliseconds.
</p>
<h2 id="h_01H930GAQ7RY1ZGWMJWFN3N3G9">Automatic Device Traces</h2>
<p>
  There are a couple of performance metrics the SDK can gather for you automatically.
  These are:
</p>
<ul>
  <li>App Start Time</li>
  <li>App Background and Foreground time</li>
</ul>
<p>
  Tracking of these metrics are disabled by default and must be explicitly enabled
  by the developer during init.
</p>
<p>
  For tracking app start time automatically you will need to enable it in SDK init
  config:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);

// enable it here separately with 'apm' interface.
config.apm.<strong>enableAppStartTimeTracking</strong>();</code></pre>
<p>
  This calculates and records the app launch time for performance monitoring.
</p>
<p>
  If you want to determine when the end time for this calculation should be you,
  will have to enable the usage of manual triggers together with
  <code class="dart">enableAppStartTimeTracking</code> during init:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);

// enable it here separately with 'apm' interface.
config.apm.enableAppStartTimeTracking().<strong>enableManualAppLoadedTrigger</strong>();</code></pre>
<p>
  Now you can call <code class="dart">Countly.appLoadingFinished()</code> any time
  after SDK initialization to record that moment as the end of app launch time.
  The starting time of the app load will be automatically calculated and recorded.
  Note that the app launch time can be recorded only once per app launch. So, the
  second and following calls to this method will be ignored.
</p>
<p>
  If you also want to manipulate the app launch starting time instead of using
  the SDK calculated value then you will need to call a third method on the config
  object with the timestamp (in milliseconds) of that time you want:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);

// generate the timestamp you want (or you can directly pass a ts)
int ts = DateTime.now().millisecondsSinceEpoch - 500; // 500 ms ago as an example

// this would also work with manual trigger
config.apm.enableAppStartTimeTracking().<strong>setAppStartTimestampOverride</strong>(ts);</code></pre>
<p>
  Lastly if you want to enable the SDK to record the time an app is in foreground
  or background automatically you would need to enable this option during init:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);

// enable it here separately with 'apm' interface.
config.apm.<strong>enableForegroundBackgroundTracking</strong>();</code></pre>
<h1 id="h_01H930GAQ77F3QXV695Z9DE6PJ">User Consent</h1>
<p>
  For compatibility with data protection regulations, such as GDPR, the Countly
  Flutter SDK allows developers to enable/disable any feature at any time depending
  on user consent. More information about GDPR
  <a href="/hc/en-us/articles/360037997132" target="_self">can be found here.</a>
</p>
<p>
  You can use CountlyConsent interface (e.g <code>CountlyConsent.sessions</code>)
  to reach all possible consent options.<br>
  Currently, available features with consent control are as follows:
</p>
<ul>
  <li>
    sessions - tracking when, how often and how long users use your app.
  </li>
  <li>events - allow sending events to the server.</li>
  <li>views - allow tracking which views user visits.</li>
  <li>location - allow sending location information.</li>
  <li>crashes - allow tracking crashes, exceptions and errors.</li>
  <li>
    attribution - allow tracking from which campaign did user come.
  </li>
  <li>
    users - allow collecting/providing user information, including custom properties.
  </li>
  <li>push - allow push notifications</li>
  <li>starRating - allow sending their rating and feedback</li>
  <li>apm - allow application performance monitoring</li>
  <li>
    remoteConfig - allows downloading remote config values from your server
  </li>
</ul>
<h2 id="h_01H930GAQ85BFVYS2RZGN7TRA0">Setup During Init</h2>
<p>
  By default the requirement for consent is disabled. To enable it, you have to
  call <code>setRequiresConsent</code> with true, before initializing Countly.
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setRequiresConsent(true);</code></pre>
<p>
  By default, no consent is given. That means that if no consent is enabled, Countly
  will not work and no network requests, related to features, will be sent. When
  the consent status of a feature is changed, that change will be sent to the Countly
  server.
</p>
<p>
  To give consent during initialization, you have to call
  <code class="dart">setConsentEnabled</code>on the config object with an array
  of consent values.
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setConsentEnabled([CountlyConsent.location, CountlyConsent.sessions, CountlyConsent.attribution, CountlyConsent.push, CountlyConsent.events, CountlyConsent.views, CountlyConsent.crashes, CountlyConsent.users, CountlyConsent.push, CountlyConsent.starRating, CountlyConsent.apm, CountlyConsent.feedback, CountlyConsent.remoteConfig])</code></pre>
<p>
  The Countly SDK does not persistently store the status of given consents except
  push notifications. You are expected to handle receiving consent from end-users
  using proper UIs depending on your app's context. You are also expected to store
  them either locally or remotely. Following this step, you will need to call the
  <code>giveConsent</code> method on each app launch depending on the permissions
  you managed to get from the end-users.
</p>
<p>Ideally you would give consent during initialization.</p>
<h2 id="h_01H930GAQ8XT5R7Q3JP2AZFSXA">Changing Consent</h2>
<p>
  The end-user can change their mind about consents at a later time.
</p>
<p>
  To reflect these changes in the Countly SDK, you can use the
  <code>removeConsent</code> or <code>giveConsent</code> methods.
</p>
<pre><code class="dart">//give consent values after init
Countly.giveConsent([CountlyConsent.events, CountlyConsent.views, CountlyConsent.starRating, CountlyConsent.crashes]);

//remove consent values after init
Countly.removeConsent([CountlyConsent.events, CountlyConsent.views, CountlyConsent.starRating, CountlyConsent.crashes]);
</code></pre>
<p>
  You can also either give or remove consent to all possible SDK features:
</p>
<pre><code class="dart">//give consent to all features
Countly.giveAllConsent();

//remove consent from all features
Countly.removeAllConsent();</code></pre>
<h1 id="h_01H930GAQ8RHCMMEPCJGC36BR7">Security and Privacy</h1>
<h2 id="h_01H930GAQ865YY5RAJN9ZYP7H2">Parameter Tampering Protection</h2>
<p>
  You can set optional <code>salt</code> to be used for calculating checksum of
  request data, which will be sent with each request using
  <code>&amp;checksum</code> field. You need to set exactly the same
  <code>salt</code> on the Countly server. If <code>salt</code> on Countly server
  is set, all requests would be checked for the validity of
  <code>&amp;checksum</code> field before being processed.
</p>
<pre><code class="dart">// sending data with salt
CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setParameterTamperingProtectionSalt("salt");</code></pre>
<p>
  Make sure not to use salt on the Countly server and not on the SDK side, otherwise,
  Countly won't accept any incoming requests.
</p>
<h2 id="h_01H930GAQ8PTNSJ1YV6WFRN15C">Using Proguard</h2>
<p>
  The Android side of the SDK does not require specific proguard exclusions and
  can be fully obfuscated.
</p>
<h1 id="h_01H930GAQ8DQ2KJTQCAFZTRHD9">Other Features and Notes</h1>
<h2 id="h_01H930GAQ8P3ZQAA3DGJT0RJVE">SDK Config Parameters Explained</h2>
<p>
  Here is the list of functionalities "CountlyConfig" provides:
</p>
<ul>
  <li>
    <span><strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ65W1S9T2R1K2EQQFJ" target="_self">Device Id</a> - </strong>A device ID is a unique identifier for your users. You may specify the device ID yourself or allow the SDK to generate it. </span>
  </li>
  <li>
    <strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ5BDPD0XHVV8RSR0XK" target="_self">Enable Logging</a> -</strong>
    To enable countly internal debugging logs.<span></span>
  </li>
  <li>
    <strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ55ZND3R5TD6WWP4R6" target="_self" rel="undefined">Enable Crash Reporting</a> -</strong>
    To enable uncaught crash reporting.
  </li>
  <li>
    <strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ865YY5RAJN9ZYP7H2" target="_self">Salt</a> -</strong>
    Set the optional salt to be used for calculating the checksum of requested
    data which will be sent with each request.<span></span>
  </li>
  <li>
    <strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ8GF1RMBD9MPWBBZ5J" target="_self" rel="undefined">Event queue threshold</a> -</strong>
    Set the threshold for event grouping. Event count that is bellow the threshold
    will be sent on update ticks.<span></span>
  </li>
  <li>
    <strong>Update Session Timer -</strong> Sets the interval for the automatic
    session update calls.
  </li>
  <li>
    <strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ524KXJKJ2FQYVH075" target="_self">Custom Crash Segment</a> -</strong>Set
    custom crash segmentation which will be added to all recorded crashes.
  </li>
  <li>
    <a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ77F3QXV695Z9DE6PJ" target="_self"><strong>User consent</strong></a>
    - Set if consent should be required and give consents.
  </li>
  <li>
    <strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ8WN5X15PVGKP5VYJZ" target="_self">Forcing HTTP POST</a> -<span> </span></strong><span>When set to</span><span>&nbsp;</span><strong>true</strong><span>, all requests made to the Countly server will be done using HTTP POST. Otherwise, the SDK sends all requests using the HTTP GET method. In some cases, if the data to be sent exceeds the 1800-character limit, the SDK uses the POST method.</span><span>&nbsp;The default value is&nbsp;<strong>false</strong>. </span>
  </li>
  <li>
    <span><strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ74F34S2RYAVJFPG53" target="_self">Star Rating Text</a> -</strong> Set shown title, message and dismiss buttim text for the star rating dialogs.</span>
  </li>
  <li>
    <span><strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ7PNW0DA85DV7PK2EJ" target="_self">Application Performance Monitoring</a> -</strong> Enable APM features, which includes the recording of app start time.</span>
  </li>
  <li>
    <span><strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ6EQZ7TBJWV2KWWSVN" target="_self">Set User Location</a> -</strong> Set user location manually instead of using Countly server to use GeoIP database to deduce a user's location. </span>
  </li>
  <li>
    <span><strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ81R7TMXJ7Z7RRBZ7A" target="_self">Max Queue Size Limit</a> - </strong>Set maximum size for the request queue.</span>
  </li>
  <li>
    <span><strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01HGDN3SPBVME2S4HP5GM2D7NG" target="_self">Manual Sessions</a> -</strong> To enable manual session handling</span>
  </li>
  <li>
    <strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ7BDR4FWH4NCATN7B4" target="_self">Automatic Remote Config</a> - </strong>If
    enabled, will automatically download newest remote config values.
  </li>
  <li>
    <strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ8A62X8BFPAWQPZ1DA" target="_self">Direct Attribution</a> -</strong>
    Report direct user attribution
  </li>
  <li>
    <strong><a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#h_01H930GAQ8QNMCJGCMC0TS6CEV" target="_self" rel="undefined">Indirect Attribution</a> -</strong>
    Report indirect user attribution
  </li>
</ul>
<h2 id="h_01HPGP75J54BBZFVZE7S7K1N2H">Example Integrations</h2>
<p>
  Below you can see steps to download the Countly Flutter
  <a href="https://github.com/Countly/countly-sdk-flutter-bridge/tree/master/example">example</a>
  application. It assumes Flutter is installed in your system:
</p>
<pre><code class="bash"># clone the Countly SDK repository
git clone https://github.com/Countly/countly-sdk-flutter-bridge.git

# dive into the cloned repo
cd countly-sdk-flutter-bridge/example

# install packages and run
flutter pub get
flutter run</code></pre>
<p>
  This example application has most of the methods mentioned in this documentation,
  and it is an excellent way to understand how different methods work, like events,
  custom user profiles, and views.
</p>
<h2 id="h_01H930GAQ81R7TMXJ7Z7RRBZ7A">Setting Maximum Request Queue Size</h2>
<p>
  When you initialize Countly, you can specify a value for the setMaxRequestQueueSize
  flag. This flag limits the number of requests that can be stored in the request
  queue when the Countly server is unavailable or experiencing connection problems.
</p>
<p>
  If the server is down, requests sent to it will be queued on the device. If the
  number of queued requests becomes excessive, it can cause problems with delivering
  the requests to the server, and can also take up valuable storage space on the
  device. To prevent this from happening, the setMaxRequestQueueSize flag limits
  the number of requests that can be stored in the queue.
</p>
<p>
  If the number of requests in the queue reaches the setMaxRequestQueueSize limit,
  the oldest requests in the queue will be dropped, and the newest requests will
  take their place. This ensures that the queue doesn't become too large, and that
  the most recent requests are prioritized for delivery.
</p>
<p>
  If you do not specify a value for the setMaxRequestQueueSize flag, the default
  setting of 1,000 will be used.
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setMaxRequestQueueSize(5000);</code></pre>
<h2 id="h_01HTF4H350DJ15WXZWCK6PBACR">SDK Internal Limits</h2>
<p>
  Countly SDKs have internal limits to prevent users from unintentionally sending
  large amounts of data to the server. If these limits are exceeded, the data will
  be truncated to keep it within the limit. You can check the exact parameters
  these limits effect from
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts#sdk_internal_limits" target="_blank" rel="noopener noreferrer">here</a>.
</p>
<h3 id="h_01HTF4H350DC2PMY77ASMHAGBA">Key Length</h3>
<p>
  Limits the maximum size of all user set keys (default: 128 chars):
</p>
<pre><code>CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.sdkInternalLimits.setMaxKeyLength(int MAX_KEY_LENGTH);
await Countly.initWithConfig(config);</code></pre>
<h3 id="h_01HTF4H350PB7ZRJDKFVZEFXQT">Value Size</h3>
<p>
  Limits the size of all user set string segmentation (or their equivalent) values
  (default: 256 chars):
</p>
<pre><code>CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.sdkInternalLimits.setMaxValueSize(int MAX_VALUE_SIZE);
await Countly.initWithConfig(config);</code></pre>
<h3 id="h_01HTF4H3507WWAHMBH7MGKW0V4">Segmentation Values</h3>
<p>
  Limits the amount of user set segmentation key-value pairs (default: 100 entries):
</p>
<pre><code>CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.sdkInternalLimits.setMaxSegmentationValues(int MAX_SEGMENTATION_COUNT);
await Countly.initWithConfig(config);</code></pre>
<h3 id="h_01HTF4H350W0RY8HQKB31H1FTS">Breadcrumb Count</h3>
<p>
  Limits the amount of user set breadcrumbs that can be recorded (default: 100
  entries, exceeding this deletes the oldest one):
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
<h2 id="h_01H930GAQ8QRF6ED3PXEF0QFAD">Attribution</h2>
<p>
  <a href="https://support.count.ly/hc/en-us/articles/360037639271-Attribution-Analytics">Countly Attribution Analytics</a>
  allows you to measure your marketing campaign performance by attributing installs
  from specific campaigns. This feature is available for the Enterprise Edition.
</p>
<p>
  <span>There are 2 forms of attribution: direct Attribution and indirect Attribution.</span><span></span>
</p>
<h3 id="h_01H930GAQ8A62X8BFPAWQPZ1DA">
  <span>Direct Attribution</span>
</h3>
<div class="callout callout--info">
  <p>
    Currently, direct attribution is only available for Android.
  </p>
</div>
<p>
  You can pass "Campaign type" and "Campaign data". The "type" determines for what
  purpose the attribution data is provided. Depending on the type, the expected
  data will differ, but usually that will be a string representation of a JSON
  object.
</p>
<p>
  <span>You can use <code>recordDirectAttribution</code> to set attribution values during initialization</span><span>.</span>
</p>
<pre><code class="dart">String campaignData = 'JSON_STRING';
CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.recordDirectAttribution('CAMPAIN_TYPE', campaignData);</code></pre>
<p>
  You can also use <code>recordDirectAttribution</code> function to manually report
  attribution later:
</p>
<pre><code class="dart">String campaignData = 'JSON_STRING';
Countly.recordDirectAttribution('CAMPAIN_TYPE', campaignData);</code></pre>
<p>
  Currently this feature is limited and accepts data only in a specific format
  and for a single type. That type is "countly". It will be used to record install
  attribution. The data also needs to be formatted in a specific way. Either with
  the campaign id or with the campaign id and campaign user id.
</p>
<pre><code class="dart">String campaignData = '{cid:"[PROVIDED_CAMPAIGN_ID]", cuid:"[PROVIDED_CAMPAIGN_USER_ID]"}';
Countly.recordDirectAttribution('countly', campaignData);</code></pre>
<h3 id="h_01H930GAQ8QNMCJGCMC0TS6CEV">
  <span>Indirect Attribution</span>
</h3>
<p>
  This feature would be used to report things like advertising ID's. For each platform
  those would be different values. For the most popular keys we have a class with
  predefined values to use, it is called "AttributionKey".
</p>
<p>
  <span>You can use <code>recordDirectAttribution</code> to set attribution values during initialization</span><span>.</span>
</p>
<pre><code class="dart">Map&lt;String, String&gt; attributionValues = {};
if(Platform.isIOS){
  attributionValues[AttributionKey.IDFA] = 'IDFA';
}
else {
  attributionValues[AttributionKey.AdvertisingID] = 'AdvertisingID';
}

CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.recordIndirectAttribution(attributionValues);</code><span></span></pre>
<p>
  You can also use <code>recordIndirectAttribution</code> function to manually
  report attribution later
</p>
<pre><code class="dart">Map&lt;String, String&gt; attributionValues = {};
if(Platform.isIOS){
  attributionValues[AttributionKey.IDFA] = 'IDFA';
}
else {
  attributionValues[AttributionKey.AdvertisingID] = 'AdvertisingID';
}

Countly.recordIndirectAttribution(attributionValues);</code></pre>
<p>
  In case you would be accessing IDFA for ios, for iOS 14+ due to the changes made
  by Apple, regarding Application Tracking, you need to ask the user for permission
  to track the Application.
</p>
<h2 id="h_01H930GAQ8WN5X15PVGKP5VYJZ">Forcing HTTP POST</h2>
<p>
  If the data sent to the server is short enough, the SDK will use HTTP GET requests.
  In case you want an override so that HTTP POST is used in all cases, call the
  <code>setHttpPostForced</code> function after you called <code>init</code>. You
  can use the same function later in the app's life cycle to disable the override.
  This function has to be called every time the app starts.
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setHttpPostForced(true); // default is false</code></pre>
<h2 id="h_01H930GAQ8QBSG5GB1P8AY1ARX">Interacting with the internal request queue</h2>
<p>
  When recording events or activities, the requests don't always get sent immediately.
  Events get grouped together. All the requests contain the same app key which
  is provided in the <code>init</code> function.
</p>
<p>
  There are two ways to interact with the app key in the request queue at the moment.
</p>
<p>
  1. You can replace all requests with a different app key with the current app
  key:
</p>
<pre><code class="dart">//Replaces all requests with a different app key with the current app key.
Countly.replaceAllAppKeysInQueueWithCurrentAppKey();</code></pre>
<p>
  In the request queue, if there are any requests whose app key is different than
  the current app key, these requests app key will be replaced with the current
  app key. 2. You can remove all requests with a different app key in the request
  queue:
</p>
<pre><code class="dart">//Removes all requests with a different app key in request queue.
Countly.removeDifferentAppKeysFromQueue();</code></pre>
<p>
  In the request queue, if there are any requests whose app key is different than
  the current app key, these requests will be removed from the request queue.
</p>
<h2 id="h_01HD3ZJYNBDW19BCE6NM12HM7T">Drop Old Requests</h2>
<p>
  If you are concerned about your app being used sparsely over a long time frame,
  old requests inside the request queue might not be important. If, for any reason,
  you don't want to get data older than a certain timeframe, you can configure
  the SDK to drop old requests:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setRequestDropAgeHours(10); // a positive integer indicating hours</code></pre>
<p>
  By using the <code>setRequestDropAgeHours</code> method while configuring the
  SDK initialization options, you can set a timeframe (in hours) after which the
  requests would be removed from the request queue. For example, by setting this
  option to 10, the SDK would ensure that no request older than 10 hours would
  be sent to the server.
</p>
<h2 id="h_01H930GAQ8GF1RMBD9MPWBBZ5J">Setting an event queue threshold</h2>
<p>
  Events get grouped together and are sent either every minute or after the unsent
  event count reaches a threshold. By default it is 10. If you would like to change
  this, call:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setEventQueueSizeToSend(6);</code></pre>
<h2 id="h_01H930GAQ8NM827P2ZCEZWCP5H">Checking if the SDK has been initialized</h2>
<p>
  In case you would like to check if init has been called, you may use the following
  function:
</p>
<pre><code class="dart">Countly.isInitialized();</code></pre>
<h2 id="h_01HEMEGDNWGA4HXRPCYPB0G613">A/B Experiment Testing</h2>
<h3 id="h_01HEMEGDNWMH4E1WRGXRS7CF7E">
  <span>Variant Level Control</span>
</h3>
<h4 id="h_01HEMEGMXC8XKRT4ZCN813ZV8N">
  <span>Downloading</span>
</h4>
<p>
  You can fetch a map of all A/B testing parameters (keys) and variants associated
  with it:
</p>
<pre><code class="java">Countly.instance.remoteConfig.testingDownloadVariantInformation((rResult, error){
  // do sth
})</code></pre>
<p>
  You can provide a callback (which is optional) to be called when the fetching
  process ends. Depending on the situation, this would return a RequestResponse
  Enum (Success, NetworkIssue, or Error) as the first parameter and a String error
  as the second parameter if there was an error ("null" otherwise).
</p>
<h4 id="h_01HEMEGQ86GCT56RN4FYFJR1S3">
  <span>Accessing</span>
</h4>
<p>
  When test variants are fetched, they are saved to the memory. If the memory is
  erased, you must fetch the variants again. So a common flow is to use the fetched
  values right after fetching them. To access all fetched values, you can use:
</p>
<pre><code class="java">Countly.sharedInstance().remoteConfig().testingGetAllVariants()</code></pre>
<p>
  This would return a Future&lt;Map&lt;String, List&lt;String&gt;&gt;&gt; where
  a test's parameter is associated with all variants under that parameter. The
  parameter would be the key, and its value would be a String List of variants.
  For example:
</p>
<pre><code class="java">{
  "key_1" : ["variant_1", "variant_2"],
  "key_2" : ["variant_3"]
}
</code></pre>
<p>Or instead you can get the variants of a specific key:</p>
<pre><code class="java">Countly.sharedInstance().remoteConfig().testingGetVariantsForKey(String valueKey)</code></pre>
<p>
  This would only return a Future&lt;List&lt;String&gt;&gt; of variants for that
  specific key. If no variants were present for a key, it would return an empty
  list. A typical result would look like this:
</p>
<pre><code class="java">["variant_1", "variant_2"]
</code></pre>
<h4 id="h_01HEMEH9T2G6KQA6HNKHEFFDDD">
  <span>Enrolling / Exiting</span>
</h4>
<p>
  After fetching A/B testing parameters and variants from your server, you next
  would like to enroll the user to a specific variant. To do this, you can use
  the following method:
</p>
<pre><code class="java">Countly.instance.remoteConfig.testingEnrollIntoVariant(String keyName, String variantName, void Function(RequestResult, String?)? callback)</code></pre>
<p>
  Here the 'valueKey' would be the parameter of your A/B test, and 'variantName'
  is the variant you have fetched and selected to enroll for. The callback function
  is optional and works the same way as explained above in the Fetching Test Variants
  section.
</p>
<h3 id="h_01HEMEGJ3XR0T33CT8NDQKRXVV">
  <span>Experiment Level Control</span>
</h3>
<h4 id="h_01HEMEGSWG4J0HD4JFHG9D0C1X">
  <span>Downloading</span>
</h4>
<p>
  You can fetch information about the A/B tests in your server including test name,
  description and the current variant:
</p>
<pre><code class="java">Countly.instance.remoteConfig.<span>testingDownloadExperimentInformation((rResult, error){
  // do sth
})</span></code></pre>
<p>
  You can provide a callback (which is optional) to be called when the fetching
  process ends. Depending on the situation, this would return a RequestResponse
  Enum (Success, NetworkIssue, or Error) as the first parameter and a String error
  as the second parameter if there was an error ("null" otherwise).
</p>
<h4 id="h_01HEMEGW7HNPX7XBHJ0VZDAQ0X">
  <span>Accessing</span>
</h4>
<p>
  After fetching the experiment information the SDK saves it in the RAM, so if
  the memory is erased, you must fetch the information again. You can access this
  information through this call:
</p>
<pre><code class="java">Countly.sharedInstance().remoteConfig().<span>testingGetAllExperimentInfo</span>()</code></pre>
<p>
  This would return a Future&lt;Map&lt;String, ExperimentInformation&gt;&gt; where
  the keys are experiment IDs as String and the values are the ExperimentInformation
  Class which contains information about the experiment with that ID. This Class'
  structure is like this:
</p>
<pre><code class="dart">class ExperimentInformation {
  // same ID as used in the map
  String experimentID;
  // the name of the experiment
  String experimentName;
  // the description of the experiment
  String experimentDescription;
  // the name of the currently assigned variant for this user (e.g., 'Control Group', 'Variant A')
  String currentVariant;
  // variant information for this experiment
  Map&lt;String, Map&lt;String, Object?&gt;&gt; variants;
}</code></pre>
<p>
  So an example data structure you might get at the end would look something similar
  to this:
</p>
<pre><code class="dart">{
  some_exp_ID: {
    experimentID: some_ID,
    experimentName: some_name,
    experimentDescription: some description,
    currentVariant: variant_name,
    variants: {
      Control Group: {
        key_1: val,
        key_2: val,
      },
      Variant A: {
        key_1: val,
        key_2: val,
      }
    }
  }
}
</code></pre>
<h4 id="h_01HEMEGYZEPX60J2NJWJM59K4E">
  <span>Enrolling / Exiting</span>
</h4>
<p>
  To enroll a user into the A/B experiment using experiment ID, you use the following
  method:
</p>
<pre>Countly.instance.remoteConfig.testingEnrollIntoABExperiment(String expID);</pre>
<p>
  If you want to remove users from A/B experiment using experiment ID, you can
  use the following function:
</p>
<pre>Countly.instance.remoteConfig.testingExitABExperiment(String expID);</pre>
<h2 id="h_01JCGHR95YCTVF6C81WF2B0FMW">Extended Device ID Management</h2>
<div class="callout callout--warning">
  <p>
    <strong>Performance risk.</strong> Changing device id with server merging
    results in huge load on server as it is rewriting all the user history. This
    should be done only once per user.
  </p>
</div>
<p>You may configure/change the device ID anytime using:</p>
<pre><code class="dart">Countly.changeDeviceId(DEVICE_ID, ON_SERVER);</code></pre>
<p>
  You may either allow the device to be counted as a new device or merge existing
  data on the server. If the<code>onServer</code> bool is set to
  <code>true</code>, the old device ID on the server will be replaced with the
  new one, and data associated with the old device ID will be merged automatically.
  Otherwise, if <code>onServer</code> bool is set to <code>false</code>, the device
  will be counted as a new device on the server.
</p>
<h3 id="h_01JCGHWKDGDVRB9JNBQJ099QEX">Temporary Device ID</h3>
<p>
  You may use a temporary device ID mode for keeping all requests on hold until
  the real device ID is set later.
</p>
<p>
  You can enable temporary device ID when initializing the SDK:
</p>
<pre><code class="dart">CountlyConfig config = CountlyConfig(SERVER_URL, APP_KEY);
config.setDeviceId(Countly.deviceIDType["TemporaryDeviceID"]);

// Initialize with that configuration
Countly.initWithConfig(config);</code></pre>
<p>To enable a temporary device ID after init, you would call:</p>
<pre><code class="dart">Countly.changeDeviceId(Countly.deviceIDType["TemporaryDeviceID"], ON_SERVER);</code></pre>
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
<h1 id="h_01HNAP3C92TG1JKYJKG3MRBK4C">FAQ</h1>
<h2 id="h_01HNAP3C923GCJ1VHHFE051PXA">What Information is Collected by the SDK?</h2>
<p>
  The data that SDKs gather to carry out their tasks and implement the necessary
  functionalities is mentioned in
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts#h_01HJ5MD0WB97PA9Z04NG2G0AKC">here</a>
</p>
<h2 id="h_01HNAP3C923GCJ1VHHFE051PXA">What Platforms are supported?</h2>
<p>
  Currently our Flutter SDK only supports Android and iOS platforms.
</p>