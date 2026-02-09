<p>
  This documentation is for the Countly Unity SDK version 24.8.X. The SDK source
  code repository can be found
  <a href="https://github.com/Countly/countly-sdk-unity" target="_blank" rel="noopener noreferrer">here.</a>
</p>
<div class="callout callout--info">
  <p>
    Click
    <a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-and-Installing-SDKs#h_01H9QCP8G8GY2M2KEKK3CSKY3F" target="_self" rel="undefined">here, </a>to
    access the documentation for older SDK versions.
  </p>
</div>
<p>
  The SDK requires the .NET profile to be at least ".NET 4.x" (".NET Framework
  " or ".NET Standard 2.1" are acceptable targets)
</p>
<p>
  The SDK is validated against the following platforms: Android, iOS, Windows,
  UWP, Linux, and Mac OSX. The SDK is also validated against the following LTS
  versions: 2020.X, 2021.X, 2022.X, and 2023.X.
</p>
<p>
  To examine the example integrations, please have a look
  <a href="#h_01HPGPY37EVNPFRRXH07DTV7QV">here.</a>
</p>
<h1 id="h_01HABTZ3143Z9ZY3H02CEV868Z">SDK Integration</h1>
<h2 id="h_01HABTZ314WVHKW01D3RTT1RYX">Adding the SDK to the Project</h2>
<p>
  Download the Unity package from
  <a href="https://github.com/Countly/countly-sdk-unity/releases" target="_blank" rel="noopener noreferrer">GitHub</a>
  and import it into your project.
</p>
<p>
  To import the package (right click on <strong>Assets </strong>=&gt;
  <strong>Import Package </strong>=&gt; <strong>Custom Package </strong>=&gt;
  <strong>Path_To_Package</strong>) and leave all the files checked because we
  need to import all the files in the package.
</p>
<p class="wysiwyg-text-align-center">
  <img src="/guide-media/01GVC1JBG025D3FBPJYN3EJR9V" alt="Screenshot_2021-03-09_at_6.02.04_PM.png" width="435" height="719">
</p>
<p>
  This SDK uses the <strong>Newtonsoft Json</strong> package internally and it
  is required for the SDK to work.
</p>
<p>
  <span data-preserver-spaces="true">Since Unity version 2020 this package is added to your project automatically by Unity. For versions before that, (2018 and 2019) you have to install this package in the project manually.</span>
</p>
<p>
  <span data-preserver-spaces="true">One way to do Install the </span><span data-preserver-spaces="true"><strong>Newtonsoft Json </strong></span><span data-preserver-spaces="true">package would be to use the built-in package manager. You would go to </span><span data-preserver-spaces="true"><strong>Windows </strong></span><span data-preserver-spaces="true">=&gt; </span><span data-preserver-spaces="true"><strong>Package Manager</strong></span><span data-preserver-spaces="true">. In there you would see something like this:<img src="/guide-media/01GVDG0BAGCD7VJ9EYNK3GS32F" alt="image-newtonsoft.png"></span>
</p>
<p>
  If the Newtonsoft Json package doesn't appear in the Package Manager, you can
  add it manually. To achieve this, you would need to add:
</p>
<p>
  <code>"com.unity.nuget.newtonsoft-json": "3.0.2"</code>
</p>
<p>
  This line, in the "<strong>manifest.json</strong>" file. After adding the line
  and saving it, the package would be added automatically. It should also appear
  in the Package Manager afterward.
</p>
<h2 id="h_01HABTZ314XCMNWWK698JR773J">Minimal Setup</h2>
<p>
  Before you can use any functionality, you have to initiate the SDK.
</p>
<p>
  The shortest way to initiate the SDK is with this code snippet:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">string appKey = "COUNTLY_APP_KEY";
string serverUrl = "COUNTLY_SERVER_URL";

CountlyConfiguration config = new CountlyConfiguration(appKey, serverUrl);
Countly.Instance.Init(config);
</code></pre>
<p>
  In the <code>CountlyConfiguration</code> object, you provide appKey and your
  Countly server URL. Please check
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KX44C9SF48WRPQNCP3">here</a>
  for more information on how to acquire your application key (APP_KEY) and server
  URL.
</p>
<div class="callout callout--info">
  <p>
    If you are in doubt about the correctness of your Countly SDK integration
    you can learn about the verification methods from
    <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#how-to-validate-your-countly-integration" target="blank">here</a>.
  </p>
</div>
<h2 class="anchor-heading" id="require-app-permissions">Required App Permissions</h2>
<p>
  If you expect the game to be saved on an SD card or any other type of external
  storage, set <strong>Write Permission</strong> to 'External (SDCard). This can
  be found in your Android platform settings under 'Other Settings'.
</p>
<p>
  When configuring your app, make sure that it has permission to access the internet.
</p>
<h2 class="anchor-heading" id="h_01HABTZ314QNCDAQT0SC5NETCG">SDK Data Storage</h2>
<p>
  Countly SDK store data that are meant for your app's use only, within an internal
  storage volume. If your game saves in external storage, SDK will store data within
  external storage. You may need to add permission to store data on an SD card.
  Please read the
  <a href="#require-app-permissions" target="_self" rel="undefined">Required app permissions</a>
  section for more information.
</p>
<p>
  SDK uses Preferences to keep track of application and user preferences and store
  private, primitive data in key-value pairs. Operational data is stored in
  <a href="https://www.iboxdb.com/" target="_self">iBoxDB</a> database file, named
  'db3.box'.
</p>
<p>
  The specific path where the database file would be stored is different for different
  platforms. To determine the specific path where the database is stored, you would
  look at the value returned by <code>Application.persistentDataPath</code>.
</p>
<div>
  <p>
    Following are the locations of the database file were used in our sample
    app:
  </p>
  <ul>
    <li data-list-item-id="edf5d922c69e58c9d28b0c36696af928c">
      <strong>Android: </strong>'/storage/emulated/0/Android/data/ly.count.demo/files/db3.box'
    </li>
    <li data-list-item-id="ee9da0f6a95f2d2505f4536b3d4efe549">
      <strong>Linux: </strong>'home/&lt;username&gt;/.config/unity3d/Countly/CountlyDotNetSDK/db3.box'
    </li>
    <li data-list-item-id="ef97dfe9d9720a22c5c1b992508750dd7">
      <strong>Windows: </strong>'C:/Users/&lt;username&gt;/AppData/LocalLow/Countly/CountlyDotNetSDK/db3.box'
    </li>
    <li data-list-item-id="eabe52fb40b96d6f0496468648ebb5bd9">
      <strong>Mac OSX: </strong>'~/Library/Application Support/Countly/CountlyDotNetSDK/db3.box'
    </li>
    <li data-list-item-id="e1d42069362b082390eb9b4b185fee14d">
      <strong>iOS: </strong>'/var/mobile/Containers/Data/Application/&lt;random-folder-name&gt;/Documents/db3.box'
    </li>
  </ul>
</div>
<h2 id="h_01HABTZ31446VPCP3M6Y0PWMNY">SDK Notes</h2>
<p>
  To access the Countly Global Instance use the following code snippet:
</p>
<pre><code class="language-csharp">Countly.Instance</code></pre>
<h1 class="anchor-heading" id="enabling-logging">SDK Logging / Debug Mode</h1>
<p>
  The first thing you should do while integrating our SDK is enabling logging.
  If logging is enabled, then our SDK will print out debug messages about its internal
  state and encountered problems.
</p>
<p>
  Call <code>EnableLogging</code> on the config object to enable logging:
</p>
<pre><code class="language-csharp">CountlyConfiguration config = new CountlyConfiguration(appKey, serverUrl)
  .EnableLogging();</code></pre>
<p>
  For more information on where to find the SDK logs you can check the documentation
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#finding-sdk-logs" target="blank">here</a>.
</p>
<h1 class="anchor-heading" id="h_01HABTZ31464JJFMECCZEH8F4C" tabindex="-1">Crash Reporting</h1>
<p>
  The Countly SDK for Unity can collect
  <a href="http://resources.count.ly/docs/introduction-to-crash-reporting-and-analytics">Crash Reports</a>,
  which you may examine and resolve later on the server.
</p>
<p>
  In the SDK all crash-related functionalities can be browsed from the returned
  interface on:
</p>
<pre><code class="language-csharp">Countly.Instance.CrashReports</code></pre>
<h2 id="h_01HABTZ314AT5KAJCM51D304ZV">Automatic Crash Handling</h2>
<p>
  The Unity SDK can automatically report uncaught exceptions/crashes in the application
  to the Countly server. This feature is enabled by default. In order to, stop
  reporting uncaught exceptions/crashes automatically, call<strong> DisableAutomaticCrashReporting()</strong>,
  in the SDK configuration.
</p>
<h2 class="anchor-heading" id="h_01HABTZ314W6CP02BBBHB6FBKJ">Handled Exceptions</h2>
<p>
  You might catch an exception or similar error during your app’s runtime. You
  may also log these handled exceptions to monitor how and when they are happening.
  To log exception use the following code snippet:
</p>
<pre><code class="language-csharp">await Countly.Instance.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, null, false); </code></pre>
<p>Here is the detail of the parameters:</p>
<ul>
  <li data-list-item-id="e8deec9f325b36e025d15403e1e39ccaa">
    <strong>message -</strong> (Mandatory, string) a string that contains a detailed
    description of the exception.
  </li>
  <li data-list-item-id="eedd79ed5768e1227d158b7b06999ebbf">
    <strong>stackTrace -</strong> (Mandatory, string) a string that describes
    the contents of the call stack.
  </li>
  <li data-list-item-id="e513bd05c21e4b9065bb4a84cc9b0d3fb">
    <strong>segments -</strong> (Optional, IDictionary&lt;string, string&gt;)
    custom key/values to be reported.
  </li>
  <li data-list-item-id="e2a5c10c93b6ae35bc513cc0a5967c96d">
    <strong>nonfatal -</strong> (Optional, bool) set false if the error is fatal.
  </li>
</ul>
<p>Example:</p>
<pre><code class="language-csharp">try {
  throw new DivideByZeroException();
} catch (Exception ex) {
  await Countly.Instance.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace);
}</code></pre>
<p class="anchor-heading">You can also send a segmentation with an exception.</p>
<pre><code class="language-csharp">Dictionary&lt;string, object&gt; segmentation = new Dictionary&lt;string, object&gt;();
segmentation.Add("Action", "click");
try {
  throw new DivideByZeroException();
} catch (Exception ex) {
  await Countly.Instance.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, segmentation, true);
}</code></pre>
<p>
  If you have handled an exception and it turns out to be fatal to your app, you
  may use the following calls:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">await Countly.Instance.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, null, false);</code></pre>
<pre><code class="language-csharp !whitespace-pre hljs">Dictionary&lt;string, object&gt; segmentation = new Dictionary&lt;string, object&gt;();
segmentation.Add("Action", "click");
await Countly.Instance.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, segmentation, false);</code></pre>
<h2 class="anchor-heading" id="h_01HABTZ314FEB9WM3P718TVMHY">Crash Breadcrumbs</h2>
<p>
  Throughout your app, you can leave crash breadcrumbs. They are short logs that
  would describe the previous steps that were taken in your app before the crash.
  After a crash happens, they will be sent together with the crash report.
</p>
<p>The following command adds a crash breadcrumb:</p>
<pre><code class="language-csharp !whitespace-pre hljs">Countly.Instance.CrashReports.AddBreadcrumbs("breadcrumb");</code></pre>
<h2 class="anchor-heading" id="h_01HABTZ3140XGZJY6K0J169K5Q">Consent</h2>
<p>
  This feature uses <code>Crashes</code> consent. No additional crash logs will
  be recorded if consent is required and not given.
</p>
<h1 id="h_01HABTZ3149D9QF1CGYMK66JRV">Events</h1>
<p>
  <span style="font-weight: 400;">An </span><a href="http://resources.count.ly/docs/custom-events"><span style="font-weight: 400;">event</span></a><span style="font-weight: 400;"> is any type of action that you can send to a Countly instance, e.g. purchases, changed settings, view enabled, and so on, letting you get valuable information about your application.</span>
</p>
<p>
  The Unity SDK helps record as many events as you want (you can set a threshold
  limit during initialization), and the system will send them automatically to
  the server once the threshold limit is reached. By default, Countly tracks only
  up to 100 events. However, this is also configurable.
</p>
<p>
  In the SDK, all event-related functionalities can be browsed from the returned
  interface on:
</p>
<pre><code class="language-csharp">Countly.Instance.Events</code></pre>
<p>
  There are a couple of values that can be set when recording an event. The main
  one is the <strong>key</strong> property which would be the identifier/name for
  that event. For example, in case a user purchased an item in a game, you could
  create an event with the key 'purchase'.
</p>
<p>
  Optionally there are also other properties that you might want to set:
</p>
<ul>
  <li data-list-item-id="ea81e17d826ecd2fc3c4925d428fd8361">
    <strong>count -</strong> a whole numerical value that marks how many times
    this event has happened. The default value for that is <strong>1</strong>.
  </li>
  <li data-list-item-id="ee887d75784b2d19b9fa28ca83b502d38">
    <strong>sum -</strong> this value would be summed across all events in the
    dashboard. For example, in-app purchase events sum of purchased items. Its
    default value is <strong>0</strong>.
  </li>
  <li data-list-item-id="ed9a419a4cb3f98633c5bf577461f31b2">
    <strong>duration - </strong>used to record and track the duration of events.
    The default value is <strong>0</strong>.
  </li>
  <li data-list-item-id="e012d9917f84ca35424155f398efb6cfd">
    <strong>segments - </strong>a value where you can provide custom segmentation
    for your events to track additional information. It is a key and value map.
    The accepted data types for the value are "String", "Integer", "Double",
    and "Boolean". All other types will be ignored.
  </li>
</ul>
<h2 id="h_01HABTZ314FCF1V827B38D1TEA">Recording Events</h2>
<p>
  Here is a quick way to
  <span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">record an event:</span>
</p>
<pre><code class="language-csharp">public async Task RecordEventAsync(string key, IDictionary&lt;string, object&gt; segmentation = null, int? count = 1, double? sum = 0, double? duration = null);</code></pre>
<p>
  <span style="font-weight: 400;">Based on the example below of an event recording a <strong>purchase</strong>, h</span><span style="font-weight: 400;">ere is a quick summary of the information for each usage:</span>
</p>
<ul>
  <li data-list-item-id="e9120b7f8fc5f96c6d696bb825152de58">
    Usage 1: how many times the <strong>purchase</strong> event occurred.
  </li>
  <li data-list-item-id="e2844c520881b77633d299ff8711b98f2">
    Usage 2: how many times the <strong>purchase</strong> event occurred + the
    total amount of those purchases.
  </li>
  <li data-list-item-id="ef024be648bc6a5386c7ab14881ca240a">
    Usage 3: how many times the <strong>purchase</strong> event occurred +
    <span style="font-weight: 400;">from which countries and application versions those purchases were made.</span>
  </li>
  <li data-list-item-id="e47956d59377a2eef38a3ab64afb4824e">
    Usage 4: how many times the <strong>purchase</strong> event occurred +
    <span style="font-weight: 400;">the total amount, both of which are also available, segmented into countries and application versions.</span>
  </li>
  <li data-list-item-id="e0ba6295e00c8fdfd4a7e871dc6963806">
    Usage 5: how many times the <strong>purchase</strong> event occurred +
    <span style="font-weight: 400;">the total amount, both of which are also available, segmented by countries and application versions + the total duration of those events.</span>
  </li>
</ul>
<p>
  <strong>1. Event key and count</strong>
</p>
<pre><code class="language-csharp !whitespace-pre hljs">await Countly.Instance.Events.RecordEventAsync(key: "purchase", count: 1);</code></pre>
<p>
  <strong>2. Event key, count, and sum</strong>
</p>
<pre><code class="language-csharp !whitespace-pre hljs">await Countly.Instance.Events.RecordEventAsync(key: "purchase", count: 1, sum: 0.99);</code></pre>
<p>
  <strong>3. Event key and count with segmentation(s)</strong>
</p>
<pre><code class="language-csharp !whitespace-pre hljs">Dictionary&lt;string, object&gt; segmentation = new Dictionary&lt;string, object&gt;();
segmentation.Add("country", "Germany");
segmentation.Add("app_version", "1.0");

await Countly.Instance.Events.RecordEventAsync(key: "purchase", segmentation: segmentation, count: 1);</code></pre>
<p>
  <strong>4. Event key, count, and sum with segmentation(s)</strong>
</p>
<pre><code class="language-csharp !whitespace-pre hljs">Dictionary&lt;string, object&gt; segmentation = new Dictionary&lt;string, object&gt;();
segmentation.Add("country", "Germany");
segmentation.Add("app_version", "1.0");

await Countly.Instance.Events.RecordEventAsync(key: "purchase", segmentation: segmentation, count: 1, sum: 0.99);</code></pre>
<p>
  <strong>5. Event key, count, sum, and duration with segmentation(s)</strong>
</p>
<pre><code class="language-csharp !whitespace-pre hljs">Dictionary&lt;string, object&gt; segmentation = new Dictionary&lt;string, object&gt;();
segmentation.Add("country", "Germany");
segmentation.Add("app_version", "1.0");

await Countly.Instance.Events.RecordEventAsync(key: "purchase", segmentation: segmentation, count: 1, sum: 0.99, duration: 60);
</code></pre>
<p>
  These are only a few examples of what you can do with Events. You may go beyond
  those examples and use country, app_version, game_level, time_of_day, and any
  other segmentation of your choice that will provide you with valuable insights.
</p>
<h2 id="h_01HABTZ314NDJQTBAS03YREYZ7">Timed Events</h2>
<p>
  It's possible to create timed events by defining a start and a stop moment.
</p>
<pre><code class="language-csharp !whitespace-pre hljs">string eventName = "Some event";

//start some event
Countly.Instance.Events.StartEvent(eventName);
//wait some time

//end the event 
Countly.Instance.Events.EndEvent(eventName);</code></pre>
<p>
  You may also provide additional information when ending an event. In that case
  you can provide the segmentation, count, or sum values. The default values for
  those are "null", 1, and 0.
</p>
<pre><code class="language-csharp !whitespace-pre hljs">string eventName = "Some event";

//start some event
Countly.Instance.Events.StartEvent(eventName);
//wait some time

IDictionary&lt;string, object&gt; segmentation = new Dictionary&lt;string, object&gt;();
segmentation.Add("wall", "orange");

//end the event while also providing segmentation information
Countly.Instance.Events.EndEvent(eventName, segmentation);
</code></pre>
<p>Here are other options to end timed events:</p>
<pre><code class="language-csharp !whitespace-pre hljs">//end the event while providing segmentation information and count
Countly.Instance.Events.EndEvent("timed-event", segmentation, 4);

//end the event while providing segmentation information, count and sum
Countly.Instance.Events.EndEvent("timed-event", segmentation, 4, 10);</code></pre>
<p>
  You may cancel the started timed event in case it is not relevant anymore:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">//start some event
Countly.Instance.Events.StartEvent(eventName);
//wait some time

//cancel the event
Countly.Instance.Events.CancelEvent(eventName);</code></pre>
<h2 class="anchor-heading" id="h_01HABTZ315TW0Q6G8BFK19SDTM">Consent</h2>
<p>
  This feature uses <code>Events</code> consent. No additional events will be recorded
  if consent is required and not given.
</p>
<p>
  When consent is removed, all previously started timed events will be canceled.
</p>
<h1 id="h_01HABTZ315HHZYGQ0HX865WJ5M">Sessions</h1>
<h2 id="h_01HABTZ3158ADXT4BY5W6G7GWT">
  <span style="font-weight: 400;">Automatic Session Tracking</span>
</h2>
<p>
  The Unity SDK handles the session automatically. After calling the
  <strong>Init</strong> method, the SDK starts the session automatically and extending
  the session after every 60 seconds. This value is configured during initialization.
  It cannot be modified after initialization.
</p>
<p>
  The SDK ends the current session whenever the user quits the app or app goes
  into the background. A session would be started again when the app comes to the
  foreground.
</p>
<h3 id="h_01HABTZ315VFW4RZCBGE17PX0G">
  <span style="font-weight: 400;">Disable Automatic Session Tracking</span>
</h3>
<p>
  You might want to disable automatic session tracking. To do so, use the following
  code snippet before init call.
</p>
<pre><code class="language-csharp">config.DisableAutomaticSessionTracking();</code></pre>
<p>
  Note that after disabling session tracking, the following things would happen:
</p>
<ul>
  <li class="p-rich_text_section" data-list-item-id="ed3a5f9cb1d40fc90dde14146d9417e46">Session information would not be recorded</li>
  <li class="p-rich_text_section" data-list-item-id="e434f1272b5a64088c3f2ac96cad1ea7f">Device metrics would not be recorded</li>
  <li class="p-rich_text_section" data-list-item-id="ef8659a6c4bc227ccb9ce662067dbd4aa">
    On dashboard location map would not be updated and, overview and analytics
    session related to sessions and users would all be empty
  </li>
</ul>
<h2 class="anchor-heading" id="h_01HABTZ315Y9VYNGNW2XBFGREJ">Consent</h2>
<p>
  This feature requires<code>Sessions</code> consent. Sessions and metrics will
  not be recorded if consent is required and not given.
</p>
<p>
  If consent was given and then is removed, the current session will not get explicitly
  ended.
</p>
<p>
  If consent was removed and then given, and automatic sessions were enabled, a
  session will automatically be started.
</p>
<h1 id="h_01HABTZ315E40XEHJHRMQMW0J6">View Tracking</h1>
<p>
  In the SDK, all view-related functionality can be browsed from the returned interface
  on:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">Countly.Instance.Views</code></pre>
<p>
  To review the resulting data from view tracking, open the dashboard and go to
  <code>Analytics &gt; Views</code>. For more information on using view tracking
  data to its fullest potential, click
  <a href="https://support.count.ly/hc/en-us/articles/4431589003545-Analytics#h_01HAWAJ8QP89XMBYDBPWBPQ14C" target="_blank" rel="noopener noreferrer">here</a>.
</p>
<h2 id="h_01HABTZ31504DKRD8DBNE1W400">Manual View Recording</h2>
<p>
  The SDK provides various ways to track views. You can track a single view at
  a given time or multiple views according to your needs. Each view has its unique
  view ID, which can be used to manipulate the view further.
</p>
<h3 id="h_01HHNXGAJ3J8YHYDSX7J8S180R">Auto Stopped Views</h3>
<p>
  An easy way to track views is by using the auto-stopped views. These views would
  stop if another view starts. You can start an auto-stopped view with or without
  segmentation like this:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">// without segmentation
Countly.Instance.Views.StartAutoStoppedView("View Name");
  
// Or with segmentation
Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("Game", "Space Invaders");
viewSegmentation.Add("HighScore", 999999);
viewSegmentation.Add("Accuracy", 99.99);
viewSegmentation.Add("IsMultiplayer", false);
viewSegmentation.Add("ResponseTime", 0.45f);
viewSegmentation.Add("PlayerID", 2468135790L);

Countly.Instance.Views.StartAutoStoppedView("View Name", viewSegmentation);</code></pre>
<p>It would return a string view ID:</p>
<pre><code class="language-csharp !whitespace-pre hljs">string id = Countly.Instance.Views.StartAutoStoppedView("View Name");</code></pre>
<h3 id="h_01HHNY1G0SVAKPH1BAKJTVVSBZ">Regular Views</h3>
<p>
  Opposed to auto-stopped views, with regular views, you can have multiple of them
  started simultaneously, and then you can control them independently.
</p>
<p>
  You can start a view that would not close when another view starts like this:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">Countly.Instance.Views.StartView("View Name");</code></pre>
<p>
  While manually tracking views, you may add your custom segmentation to them like
  this:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("Class", "Wizard");
viewSegmentation.Add("Level", 42);
viewSegmentation.Add("ManaPoints", 150.75);
viewSegmentation.Add("HasMagicStaff", true);
viewSegmentation.Add("CastingSpeed", 1.1f);
viewSegmentation.Add("CharacterID", 9988776655L);

Countly.Instance.Views.StartView("View Name", viewSegmentation);</code></pre>
<p>
  These views would also return a string view ID when they are called.
</p>
<h3 id="h_01HHNY9513MGDDJMP3SDWV4KWW">Stopping Views</h3>
<p>
  You can stop a view with its name or its view ID. To stop it with its name:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">Countly.Instance.Views.StopViewWithName("View Name");</code></pre>
<p>You can provide a segmentation while doing so:</p>
<pre><code class="language-csharp !whitespace-pre hljs">Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("CardName", "Spell Pierce");
viewSegmentation.Add("ManaCost", 1);
viewSegmentation.Add("CardValue", 3.5);
viewSegmentation.Add("IsFoil", false);
viewSegmentation.Add("CardPower", 0.0f);
viewSegmentation.Add("CardID", 9876543210L);

Countly.Instance.Views.StopViewWithName("View Name", viewSegmentation);</code></pre>
<p>
  If multiple views have the same name (they would have different identifiers),
  but if you try to stop one with that name, the SDK will close the one that started
  last.
</p>
<p>To stop a view with its view ID:</p>
<pre><code class="language-csharp !whitespace-pre hljs">Countly.Instance.Views.StopViewWithID("View ID");</code></pre>
<p>You can provide a segmentation while doing so:</p>
<pre><code class="language-csharp !whitespace-pre hljs">// starting view and recording view id
string id = Countly.Instance.Views.StartAutoStoppedView("View Name");

Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("OpeningName", "Sicilian Defense");
viewSegmentation.Add("ECOCode", "B40");
viewSegmentation.Add("AverageGameDurationInMinutes", 45.5);
viewSegmentation.Add("IsAggressive", true);
viewSegmentation.Add("WinRatePercentage", 54.3f);
viewSegmentation.Add("OpeningID", 123456789L);

Countly.Instance.Views.StopViewWithID(id, viewSegmentation);</code></pre>
<p>
  You can also stop all running views at once with a segmentation:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("StationName", "Alpha Centauri Base");
viewSegmentation.Add("CrewCount", 120);
viewSegmentation.Add("DistanceFromEarth", 4.37E13);
viewSegmentation.Add("HasArtificialGravity", true);
viewSegmentation.Add("OrbitalPeriod", 365.25f);
viewSegmentation.Add("StationID", 2233445566L);
  
Countly.Instance.Views.StopAllViews(viewSegmentation);</code></pre>
<h3 id="h_01HHNYPKFGD5CC7SJECDWQ7EXB">Pausing and Resuming Views</h3>
<p>
  If you start multiple views simultaneously, pausing some views while others continue
  might be necessary. You can achieve this by using the unique identifier you get
  when starting a view.
</p>
<p>To pause a view with its ID:</p>
<pre><code class="language-csharp !whitespace-pre hljs">Countly.Instance.Views.PauseViewWithID("View ID");</code></pre>
<p>To resume a view with its ID:</p>
<pre><code class="language-csharp !whitespace-pre hljs">Countly.Instance.Views.ResumeViewWithID("View ID");</code></pre>
<h3 id="h_01HHNZEE94N9FH6GYZTR4A1H0M">Adding Segmentation to Started Views</h3>
<p>
  You can add segmentation values to a view before it ends. This can be done as
  often as desired, and the final segmentation sent to the server will be the cumulative
  sum of all segmentations. However, if a certain segmentation value for a specific
  key has been updated, the latest value will be used.
</p>
<p>To add segmentation to a view using its view ID:</p>
<pre><code class="language-csharp !whitespace-pre hljs">string id = Countly.Instance.Views.StartView("View Name");

Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("BookTitle", "Dune");
viewSegmentation.Add("Author", "Frank Herbert");
viewSegmentation.Add("PublicationYear", 1965);
viewSegmentation.Add("NumberofPages", 412);
viewSegmentation.Add("IsScienceFiction", true);
viewSegmentation.Add("AverageRating", 4.35f);
  
Countly.Instance.Views.AddSegmentationToViewWithID(id, viewSegmentation);</code></pre>
<p>To add segmentation to a view using its name:</p>
<pre><code class="language-csharp !whitespace-pre hljs">string viewName = "View Name";
Countly.Instance.Views.StartView(viewName);
  
Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("FavoritePet", "Unicorn");
viewSegmentation.Add("PetAge", 1);
viewSegmentation.Add("PetMagicLevel", 100.0);
viewSegmentation.Add("IsMythical", true);
viewSegmentation.Add("HeightInMeters", 2.5f);
viewSegmentation.Add("PetID", 1234567890L);
  
Countly.Instance.Views.AddSegmentationToViewWithName(viewName, viewSegmentation);</code></pre>
<h2 id="h_01HHNZ0MAP34090BTSV1KAYD4J">Global-View Segmentation</h2>
<p>
  You can set a global segmentation to be sent with all views when it ends:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("DeskPlant", "Cactus");
viewSegmentation.Add("CoffeeMugsOwned", 7);
viewSegmentation.Add("AverageMeetingLength", 1.5);
viewSegmentation.Add("HasOfficeDog", true);
viewSegmentation.Add("DeskHeight", 1.2f);
viewSegmentation.Add("EmployeeID", 1122334455L);

Countly.Instance.Views.SetGlobalViewSegmentation(viewSegmentation);</code></pre>
<p>You can update this segmentation any time you want:</p>
<pre><code class="language-csharp !whitespace-pre hljs">Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("FavoriteGenre", "Sci-Fi");
viewSegmentation.Add("MoviesWatchedThisMonth", 15);
viewSegmentation.Add("AverageRating", 4.8);
viewSegmentation.Add("HasStreamingSubscription", true);
viewSegmentation.Add("ScreenSize", 55.0f);
viewSegmentation.Add("UserID", 5566778899L);
  
Countly.Instance.Views.UpdateGlobalViewSegmentation(viewSegmentation);</code></pre>
<h2 class="anchor-heading" id="h_01HABTZ315ECG69VS4DKTX0W2N">Consent</h2>
<p>
  This feature requires <code>Views</code> consent. No additional views will be
  recorded if consent is required and not given.
</p>
<h1 class="anchor-heading" id="h_01HABTZ315QACRZ219TTBZS5ZN" tabindex="-1">Device ID Management</h1>
<p>
  A device ID is a unique identifier for your users. You may specify the device
  ID yourself or allow the SDK to generate it. When providing one yourself, keep
  in mind that it has to be unique for all users. Some potential sources for such
  an id may be the users username, email or some other internal ID used by your
  other systems.
</p>
<p>
  You can provide a device ID during initialization like this:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">string DeviceId = "UNIQUE_DEVICE_ID";
CountlyConfiguration config = new CountlyConfiguration(appKey, serverUrl)
  .SetDeviceId(DeviceId);
  
Countly.Instance.Init(config);</code></pre>
<h2 class="anchor-heading" id="h_01HABTZ315MW7E9560TS40F65Z">Retrieving Current Device ID</h2>
<p>
  You may want to see what device id Countly is assigning for the specific device.
  For that, you may use the following calls.
</p>
<pre><code class="language-csharp !whitespace-pre hljs">string usedId = Countly.Instance.Device.DeviceId;</code></pre>
<p>
  You can get the current device ID type. The id type is an enum with the possible
  values of:
</p>
<ul>
  <li data-list-item-id="ee5da766fb8bb0f89e15936b8ed243658">SDKGenerated - device ID generated by the SDK</li>
  <li data-list-item-id="ed88fd58885937206393caf1283657fbb">DeveloperProvided - device ID provided by the host app</li>
</ul>
<pre><code class="language-csharp !whitespace-pre hljs">DeviceIdType type = Countly.Instance.Device.DeviceIdType;</code></pre>
<h2 id="h_01HABTZ3151FMVABED60J1FB2Y">Changing Device ID</h2>
<p>
  The SDK allows you to change the Device ID at any point in time. You can use
  any of the following two methods to changing the Device ID, depending on your
  needs.
</p>
<div class="callout callout--warning">
  <p>
    <strong>Performance risk.</strong> Changing device id with server merging
    results in huge load on server as it is rewriting all the user history. This
    should be done only once per user.
  </p>
</div>
<p class="anchor-heading">
  <strong>Changing Device ID with Server Merge</strong>
</p>
<p>
  In case your application authenticates users, you might want to change the ID
  to the one in your backend after he has logged in. This helps you identify a
  specific user with a specific ID on a device he logs in, and the same scenario
  can also be used in cases this user logs in using a different way (e.g another
  tablet, another mobile phone, or web). In this case, any data stored in your
  Countly server database associated with the current device ID will be transferred
  (merged) into the user profile with the device id you specified in the following
  method call:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">await Countly.Instance.Device.ChangeDeviceIdWithMerge("New Device Id");</code></pre>
<p class="anchor-heading">
  <strong>Changing Device ID without Server Merge</strong>
</p>
<p>
  You might want to track information about another separate user that starts using
  your app (changing apps account), or your app enters a state where you no longer
  can verify the identity of the current user (user logs out). In that case, you
  can change the current device ID to a new one without merging their data. You
  would call:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">await Countly.Instance.Device.ChangeDeviceIdWithoutMerge("New Device Id");</code></pre>
<p>
  Doing it this way, will not merge the previously acquired data with the new id.
</p>
<div class="callout callout--warning">
  <p>
    <span style="font-weight: 400;">If device ID is changed without merging and consent was enabled, all previously given consent will be removed. This means that all features will cease to function until new consent has been given again for that new device ID.</span>
  </p>
</div>
<p>
  Do note that every time you change your deviceId without a merge, it will be
  interpreted as a new user. Therefore implementing id management in a bad way
  could inflate the users count by quite a lot.
</p>
<h2 id="h_01HABTZ315MARV8KKQMHM9EZBB">Device ID Generation</h2>
<p>
  If no device ID is provided the first time the SDK is initialised, the SDK will
  generate a unique device ID. The source of that id is<code class="!csharp">SystemInfo.deviceUniqueIdentifier</code>which
  is a value exposed by Unity. It should be unique for every device.
</p>
<p>
  Here are the underlying mechanisms used to generate that value for some platforms:
</p>
<p>
  <strong>IOS:</strong> on pre-iOS7 devices, it will return a hash of the MAC address.
  On iOS7 devices, it will be
</p>
<p>
  <code class="!csharp">UIDevice identifierForVendor</code> or, if that fails for
  any reason,
</p>
<p>
  <code class="!csharp">ASIdentifierManager advertisingIdentifier</code>
</p>
<p>
  <strong>Android: </strong><code class="!csharp">SystemInfo.deviceUniqueIdentifier</code>
  returns the md5 of ANDROID_ID. Note that since Android 8.0 (API level 26) ANDROID_ID
  depends on the app signing key. That means "unsigned" builds (which are by default
  signed with a debug keystore) will have a different value than signed builds
  (which are signed with a key provided in the player settings).
</p>
<p>
  <strong>Windows Store Apps:</strong> uses
  <code class="!csharp">AdvertisingManager::AdvertisingId</code>for returning unique
  device identifiers.
</p>
<p>
  <strong>Windows Standalone</strong>: returns a hash from the concatenation of
  strings taken from Computer System Hardware Classes. For more information,
  <a href="https://docs.unity3d.com/ScriptReference/SystemInfo-deviceUniqueIdentifier.html" target="_self">click here</a>.
</p>
<h2 class="anchor-heading" id="h_01HABTZ315T6Z5NV8QWZVYMSCG">Consent</h2>
<p>No consent is required to change device ID.</p>
<p>
  If device ID is changed without merging and consent was enabled, all previously
  given consent will be removed. This means that all features will cease to function
  until new consent has been given again for that new device ID.
</p>
<h1 id="h_01HABTZ3157PQZHXH7YT210DJQ">Push Notifications</h1>
<p>
  The Unity SKD uses FCM and APNs as push notification providers for Android and
  iOS platforms respectively, and it doesn't support the Huawei Push Kit push service.
</p>
<p>
  By default, FCM and APNs dependencies are added as part of the SDK. They can
  be removed in case you don't need them.
</p>
<p>
  Note that SDK doesn't support Deep linking, Data only push, and Rich push notifications
  yet. You can send text push notifications only.
</p>
<h2 id="h_01HABTZ3152EEE6CDNGW0B29J7">Integration</h2>
<p>
  <span class="wysiwyg-font-size-large"><strong>Android</strong></span>
</p>
<p>
  The Countly server needs an FCM server key to send notifications through FCM.
</p>
<p class="anchor-heading" id="integrating-fcm-into-your-app">
  To set it up, refer to
  <a href="https://support.count.ly/hc/en-us/articles/360037754031-Android-SDK#getting-fcm-credentials" target="_self" rel="undefined">Android documentation</a>
  and follow the following steps:
</p>
<ol>
  <li data-list-item-id="e77972e166594a82dd2737fe54df7f454">
    Download google-services.json from
    <a href="https://console.firebase.google.com/">Firebase console.</a>
  </li>
  <li data-list-item-id="e5f7926df418ce9ab7a26e41958b00d66">
    Create google-services.xml from google-services.json. You can use an online
    converter
    <a href="https://dandar3.github.io/android/google-services-json-to-xml.html" rel="nofollow">here</a>.
  </li>
  <li data-list-item-id="e54b1af3a00652a33e4aea4b10c09ada9">
    Put your file google-services.xml in /Plugins/Android/Notifications/res/values
    (replace if necessary).
  </li>
</ol>
<p>
  <span class="wysiwyg-font-size-large"><strong>iOS</strong></span>
</p>
<p>
  The Countly server needs the APNs Auth Key to send notifications. To get the
  APNs Auth Key and upload it to the County Server, for further information refer
  to
  <a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#setting-up-apns-authentication" target="_self">iOS Documentation.</a>
</p>
<p>To set up push for iOS, follow the next two steps:</p>
<p>
  1. In Unity, go to <strong>Player Settings. </strong>In the
  <strong>Other Settings</strong> section, add the
  <strong>"COUNTLY_ENABLE_IOS_PUSH" </strong>symbol in
  <strong>Scripting Define Symbols.<img src="/guide-media/01GV9ZT9T72NE430KKRJMGNE4X" alt="Screenshot_2020-10-27_at_4.07.16_PM.png"></strong>
</p>
<p>
  2. After exporting the <strong>iOS</strong> project, open the project in
  <strong>Xcode</strong>, and add <strong>Push Notifications</strong> Capability.
  For further information regarding iOS app configuring refer to
  <a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#configuring-ios-app" target="_self" rel="undefined">iOS Documentation.</a>
</p>
<h2 id="h_01HABTZ3154KW34FPCX7AEJM86">Enabling Push</h2>
<p>
  By default Push Notifications are disabled. To enable push, set Notification
  mode other than <code>None</code> in the Configuration before SDK init call.
</p>
<p>Example:</p>
<pre><code class="language-csharp !whitespace-pre hljs">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetNotificationMode(TestMode.AndroidTestToken);</code></pre>
<p>Here is an overview of notification modes:</p>
<ul>
  <li data-list-item-id="efef3a4737927f3a991c0162f511643aa">
    <code>None</code>- it is the default value of notification mode. This mode
    disables the notification feature.
  </li>
  <li data-list-item-id="e098f052aa0bf267daf94100b9dd4b38d">
    <code>AndroidTestToken</code> / <code>iOSTestToken</code>- during development
    build, use <code>AndroidTestToken</code> and <code>iOSTestToken</code> modes
    for Android and iOS platforms respectively.
  </li>
  <li data-list-item-id="ec26dfb2f9f32b20be3ca97093a18c407">
    <code>iOSAdHocToken</code> - use this for distribution of iOS builds on TestFlight
    and AdHoc.
  </li>
  <li data-list-item-id="e7959e898a3ce0a8f2b886faecde609a6">
    <code>ProductionToken</code> - use this mode for the production builds.
  </li>
</ul>
<h2 id="h_01HABTZ315RJBF6DFEK5VPM8C0">Removing Push and Its Dependencies</h2>
<p>
  By default, push dependencies are part of the SDK. You may remove them, and add
  them back after removing them. Don't forget to change notification mode to
  <code>None</code>, after removing push notification dependencies from SDK.
</p>
<p>
  <span class="wysiwyg-font-size-large"><strong>Android</strong></span>
</p>
<p>
  To remove FCM dependencies from the android build, go to the
  <strong>Assets\Plugins\Android </strong>folder and delete the
  <strong>Notifications</strong> folder.
</p>
<p>
  To add them back after removing, re-import the Unity package.
</p>
<p>
  <span class="wysiwyg-font-size-large"><strong>IOS</strong></span>
</p>
<p>
  The <strong>APN's</strong> dependencies are part of the <strong>SDK.</strong>
  To remove the <strong>APNs</strong> dependencies, go to the
  <strong>Assets\Plugins </strong>folder and delete the <strong>iOS</strong> folder.
  Remove the <strong>"COUNTLY_ENABLE_IOS_PUSH"</strong> symbol from
  <strong>Scripting Define Symbols </strong>in <strong>Player Settings.</strong>
</p>
<p>
  To add them back after removing, re-import the Unity package and add back the
  <strong>"COUNTLY_ENABLE_IOS_PUSH"</strong> symbol.
</p>
<h2 id="h_01HABTZ315MGGW3YG4RHS97BVY">Customizing Push Messages</h2>
<p>
  <span class="wysiwyg-font-size-large"><strong>Android</strong></span>
</p>
<p>
  To change the sound and icons of the android notifications, update the sound
  and icons in the folder Assets/Plugins/Android/Notifications/res.
</p>
<p>
  <strong>Note</strong>: The Notification channel name and description can be updated
  through the <strong>strings.xml</strong> file located in the
  <strong>Assets\Plugins\Android\Notifications\res\values </strong>folder.
</p>
<h2 id="h_01HABTZ315PX7MATCGB1H307YY">Handling Push Callbacks</h2>
<p>
  In order to listen to notification receive and click events, implement
  <code>INotificationListener</code> interface and its members' methods
  <code>OnNotificationClicked</code> and <code>OnNotificationReceived</code> into
  your class.
</p>
<p>Example:</p>
<pre><code class="language-csharp">public class CountlyEntryPoint : MonoBehaviour, INotificationListener
{
  public void OnNotificationReceived(string message)
  {
  
  }
  public void OnNotificationClicked(string message, int index)
  {
  
  }
}</code></pre>
<p>
  There are two ways to register for this class to listen to notification events.
</p>
<p>
  1. You may call <code>AddListener(this)</code>on
  <code>CountlyConfiguration</code> object before the SDK Init call.
</p>
<p>Example:</p>
<pre><code class="language-csharp">private void Awake()
{
  CountlyConfiguration config = new CountlyConfiguration(appKey, serverUrl);
  config.AddNotificationListener(this);
  Countly.Instance.Init(config);
}</code></pre>
<p>
  2. If SDK has been initialized<span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">, use the following code snippet to listen to push notification events.</span>
</p>
<pre><code class="language-csharp">Countly.Instance.Notifications.AddListener(this);</code></pre>
<p>
  To stop listening notification receive and click events, call
</p>
<pre><code class="language-csharp">Countly.Instance.Notifications.RemoveListener(this);</code></pre>
<p>
  For more information, check the sample app on
  <a href="http://github.com/countly/countly-sdk-unity" target="_blank" rel="noopener noreferrer">GitHub</a>.
</p>
<h2 class="anchor-heading" id="h_01HABTZ315P5G15ZP38X4DMB3X">Consent</h2>
<p>
  This feature requires<code>Push</code> consent. No push notifications will be
  received if consent is required and not given.
</p>
<h1 class="anchor-heading garden-focus-visible" id="user-location" tabindex="-1" data-garden-focus-visible="true">User Location</h1>
<p>
  While integrating this SDK into your application, you might want to track your
  user location. You could use this information to better know your app’s user
  base. There are 4 fields that can be provided:
</p>
<ul>
  <li data-list-item-id="e127ecbcf49c1a8a77d0aa34c9f27325c">Country code (two-letter ISO standard).</li>
  <li data-list-item-id="eb28dd7ea01c7bc73b1e1a5959456c6f5">City name (must be set together with the country code).</li>
  <li data-list-item-id="ec1c20ccd44f56d1b6bd384b0019982a1">
    Latitude and longitude values separated by a comma, e.g. "56.42345,123.45325".
  </li>
  <li data-list-item-id="e3009f07e81ccdf13945f67e93b9dd1e5">Your user’s IP address.</li>
</ul>
<h2 class="anchor-heading" id="setting-location">Setting Location</h2>
<p>
  During init, you can set location info in the configuration:
</p>
<pre><code class="language-csharp">config.SetLocation(countryCode, city, gpsCoordinates, ipAddress);</code></pre>
<p>
  After SDK initialization, this location info will be sent to the server at the
  start of the user session.
</p>
<p>
  Note that the IP address will only be updated if set through the init process.
</p>
<p>
  Use <code>Countly.Location.</code> to disable or set the location at any time
  after the SDK Init call.
</p>
<p>For example:</p>
<pre><code class="language-csharp">string countryCode = "us";
string city = "Houston";
string latitude = "29.634933";
string longitude = "-95.220255";
string ipAddress = null;

Countly.Instance.Location.SetLocation(countryCode, city, latitude + "," + longitude, ipAddress);</code></pre>
<p>
  When those values are set, a separate request will be created to send them. Except
  for IP address, because Countly server processes IP address only when starting
  a session.
</p>
<p>If you don't want to set specific fields, set them to null.</p>
<h2 class="anchor-heading" id="disabling-location">Disabling Location</h2>
<p>
  Users might want to opt-out of location tracking. To do so, you can disable location
  during init:
</p>
<pre><code class="language-csharp">config.DisableLocation();</code></pre>
<p>To disable location after SDK initialization, call:</p>
<pre><code class="language-csharp">Countly.Instance.Location.DisableLocation();</code></pre>
<p>
  These actions will erase the cached location data from the device and the server.
</p>
<h2 class="anchor-heading" id="h_01HABTZ316DN526NN0V577XVCQ">Consent</h2>
<p>
  This feature requires<code>Location</code> consent. If consent is not given and
  is required, no location information will be recorded. No reverse geo IP will
  be performed server side. SDK will behave as if location tracking is disabled.
</p>
<p>
  If consent was given and then was removed, it will create a request that will
  clear location information server side.
</p>
<h1 class="anchor-heading" id="remote-config" tabindex="-1">Remote Config</h1>
<p>
  Available in the Enterprise Edition, Remote Config allows you to modify how your
  app functions or looks by requesting key-value pairs from your Countly server.
  The returned values may be modified based on the user profile. For more details,
  please see the
  <a href="https://resources.count.ly/docs/remote-config">Remote Config documentation</a>.
</p>
<h2 class="anchor-heading" id="manual-remote-config-download">Manual Remote Config</h2>
<p>
  To download Remote Config, call
  <code>Countly.Instance.RemoteConfigs.Update()</code>. After the successful download,
  the SDK stores the updated config locally.
</p>
<pre><code class="language-csharp">await Countly.Instance.RemoteConfigs.Update();</code></pre>
<h2 id="h_01HABTZ3164Y5JMBXVP1JCMWNK">Accessing Remote Config Values</h2>
<p>
  To access the stored config, call
  <code>Countly.Instance.RemoteConfigs.Configs</code>. It will return
  <code>null</code> if there isn't any config stored.
</p>
<pre><code class="language-csharp">Dictionary&lt;string, object&gt; config = Countly.Instance.RemoteConfigs.Configs;</code></pre>
<p>
  The <code>Dictionary&lt;string, object&gt;</code> returns a value of the type
  <code>object</code> against a key. The developer then needs to cast it to the
  appropriate type.
</p>
<h2 class="anchor-heading" id="h_01HABTZ316D1SCDFXWV0VMDARS">Consent</h2>
<p>
  This feature requires<code>RemoteConfig</code> consent. If consent is required
  and not given, no remote config information will be downloaded and stored.
</p>
<p>
  If consent was given and then is removed, locally stored remote config information
  will be cleared.
</p>
<h1 id="h_01HABTZ3167DDCYDQ3N6QSRZ6D">User Feedback</h1>
<h2 id="h_01HABTZ316A3KZFNEG63TSS6GT">Star Rating Dialog</h2>
<p>
  When a user rates your application, you can report it to the Countly server.
</p>
<p>Example:</p>
<pre><code class="language-csharp !whitespace-pre hljs">await Countly.Instance.StarRating.ReportStarRatingAsync(platform: "android", appVersion: "0.1", rating: 3);</code></pre>
<p>All parameters are mandatory.</p>
<ul>
  <li data-list-item-id="e25a51f6b16f4776e66decde2896ff00d">
    <strong>platform -</strong> (string) the name of the platform.
  </li>
  <li data-list-item-id="e75d0f66a84fcd8db30071894d9f245ed">
    <strong>appVersion -</strong> (string) the current version of the app.
  </li>
  <li data-list-item-id="ee8272c1f6410a5afe33e533f7e684917">
    <strong>rating -</strong> (int) value from 0 to 5 that will be set as the
    rating value.
  </li>
</ul>
<h2 class="anchor-heading" id="h_01HABTZ316JXD672PVFWMTVEMP">Consent</h2>
<p>
  If consent is required, recording Star Rating requires<code>StarRating</code>consent.
  If consent is required and not given, recording a Star Rating will not be possible.
</p>
<h1 id="h_01HABTZ3164RBD3AC31PH330W9">User Profiles</h1>
<div class="callout callout--info">
  <p>
    The User Profiles feature is available in
    <a href="https://countly.com/enterprise" target="_blank" rel="noopener noreferrer">Countly Enterprise</a>
    and built-in
    <a href="https://countly.com/flex" target="_blank" rel="noopener noreferrer">Flex</a>.
  </p>
</div>
<p>
  User Profiles is a tool for identifying users, their devices, event timelines,
  and application crash information. It may contain any information you collect
  or that is collected automatically by the Countly SDK.
</p>
<p>
  You may send user-related information to Countly and let the Countly Dashboard
  show and segment this data. You may also send a notification to a group of users.
  For more information about User Profiles, review
  <a href="https://support.count.ly/hc/en-us/articles/4403281285913-User-Profiles" target="_blank" rel="noopener noreferrer">this documentation</a>
</p>
<h2 id="h_01J47DCBMMFRVW76KFDDJ6HD55">Setting User Properties</h2>
<p>
  In the SDK, the typical workflow involves using the following methods to provide
  information about the current user:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">// Provide multiple properties at once within a dictionary
Countly.Instance.UserProfile.SetProperties(Dictionary &lt;string, object&gt; userProperties);

// Provide single user property as key and value
Countly.Instance.UserProfile.SetProperty(string key, object value);</code></pre>
<p>
  These methods allow you to set predefined fields or any custom fields you wish
  to include. While saving User Profile data by calling
  <code>Countly.UserProfile.Save()</code> is not mandatory, if required manually
  saving User Profile data by that call can still be applied. Recorded User Profile
  data is automatically sent when:
</p>
<ul>
  <li data-list-item-id="e8ef7afa1f3d9480b90e3e6bc372108d0">An event is recorded</li>
  <li data-list-item-id="e78e1815b3e4f86f044b66457c36af6b6">A session update occurs</li>
  <li data-list-item-id="e8c30e549ee5857a8eee753f28ccbceaf">The device ID changes</li>
</ul>
<p>The keys for predefined user data fields are as follows:</p>
<div class="table">
  <figure class="wysiwyg-table">
    <table class="table--bordered table--color-header">
      <thead>
        <tr>
          <th>Key</th>
          <th>Type</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>name</td>
          <td>string</td>
          <td>User's full name</td>
        </tr>
        <tr>
          <td>username</td>
          <td>string</td>
          <td>User's nickname</td>
        </tr>
        <tr>
          <td>email</td>
          <td>string</td>
          <td>User's email address</td>
        </tr>
        <tr>
          <td>organization</td>
          <td>string</td>
          <td>User's organization name</td>
        </tr>
        <tr>
          <td>phone</td>
          <td>string</td>
          <td>User's phone number</td>
        </tr>
        <tr>
          <td>picture</td>
          <td>string</td>
          <td>URL to avatar or profile picture of the user</td>
        </tr>
        <tr>
          <td>gender</td>
          <td>string</td>
          <td>User's gender as M for male and F for female</td>
        </tr>
        <tr>
          <td>byear</td>
          <td>int</td>
          <td>User's year of birth as integer</td>
        </tr>
      </tbody>
    </table>
  </figure>
</div>
<p>
  Using "" for strings or a negative number for 'byear' will effectively delete
  that property.
</p>
<p>
  You may use any key values to store and display on your Countly backend for custom
  user properties.
  <strong>Note: Keys with . or $ symbols will have those symbols removed.</strong>
</p>
<h3 id="h_01J47DN92CDNYHA24827B3VBXD">Recording Custom Values</h3>
<p>
  Both methods can be used to record custom User Profile data. Example usage would
  be:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">// Record the User Profile data by SetProperty method
    Countly.Instance.UserProfile.SetProperty("ExampleKey", "ExampleValue");
    // Send recorded value to the server manually if needed
    Countly.Instance.UserProfile.Save();
        
    // Create a Dictionary for SetProperties method
    Dictionary&lt;string, object&gt; userProperties = new Dictionary&lt;string, object&gt;
    {
      { "ExampleKey2", "ExampleValue2" }
    };
    // Record the User Profile data by SetProperties method
    Countly.Instance.UserProfile.SetProperties(userProperties);
    // Send recorded value to the server manually if needed
    Countly.Instance.UserProfile.Save();
  </code></pre>
<h3 id="h_01J47ECBQ9A9Z9KH7Z9EQ7PWYP">Recording Predefined Values</h3>
<p>
  In the same way as recording custom User Profile data, both methods can be used
  again to record predefined User Profile data. Example usage would be:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">// Record single User Profile data by SetProperty method
    Countly.Instance.UserProfile.SetProperty("name", "Albert Einstein");
    // Send recorded value to the server manually if needed
    Countly.Instance.UserProfile.Save();
    
// Create a Dictionary containing User Profile data
    Dictionary&lt;string, object&gt; userProperties = new Dictionary&lt;string, object&gt;
    {
      { "name", "Albert Einstein" },
      { "username", "albert" },
      { "email", "info@albert.einstein" },
      { "organization", "Theoretical Physics Institute" },
      { "phone", "90 123 456 7890" },
      { "picture", "https://ExamplePictureUrl.org/geniuses/Albert_Einstein.jpg" },
      { "gender", "M" },
      { "byear", 1879 }
    };
    // Record the User Profile data by SetProperties method
    Countly.Instance.UserProfile.SetProperties(userProperties);
    // Send recorded value to the server manually if needed
    Countly.Instance.UserProfile.Save();
  </code></pre>
<p>
  It's also possible to record custom and predefined data within the same dictionary
  in a single call. Example usage would be:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">// Record both custom and predefined values
    Dictionary&lt;string, object&gt; userProperties = new Dictionary&lt;string, object&gt;
    {
      // User values
      { "name", "Marie Curie" },
      { "username", "marie" },
      { "email", "info@marie.curie" },
      { "organization", "Institute of Radium" },
      { "phone", "90 987 654 3210" },
      { "picture", "https://ExamplePictureUrl.org/geniuses/Marie_Curie.jpg" },
      { "gender", "F" },
      { "byear", 1867 },
      // Custom values
      { "fieldOfStudy", "Radioactivity" },
      { "nobelPrizes", new List { "Physics 1903", "Chemistry 1911" } },
      { "discovery", "Polonium and Radium" }
    };
    // Record the values with SetProperties call
    Countly.Instance.UserProfile.SetProperties(userProperties);
    // Send recorded value to the server manually if needed
    Countly.Instance.UserProfile.Save();
  </code></pre>
<h2 id="h_01HABTZ3166RSMTP5JC3Y2PVZC">Setting User Picture</h2>
<p>
  As mentioned above SDK allows you to set the user's picture URL along with other
  details using both <code>SetProperties</code> and <code>SetProperty</code> methods.
</p>
<p>Example usage would be:</p>
<pre><code class="language-csharp !whitespace-pre hljs">// Set User Picture with SetProperty method
    Countly.Instance.UserProfile.SetProperty("picture", "https://ExamplePictureUrl.org/geniuses/Richard_Garfield.jpg");
    // Send recorded value to the server manually if needed
    Countly.Instance.UserProfile.Save();

    //Create a dictionary that contains picture URL data
    Dictionary&lt;string, object&gt; userProperties = new Dictionary&lt;string, object&gt;
    {
      { "picture", "https://ExamplePictureUrl.org/geniuses/Marshall_Mathers.jpg" }
    };
    // Set the user profile picture using the SetProperties method
    Countly.Instance.UserProfile.SetProperties(userProperties);
// Send recorded value to the server manually if needed
    Countly.Instance.UserProfile.Save();
  </code></pre>
<h2 id="h_01HABTZ3160SY1KJCM2G1JPYK0">Modifying Data</h2>
<p>
  You may also manipulate your custom data values in different ways, such as incrementing
  the current value on a server or storing an array of values under the same property.
</p>
<p>You will find the list of available manipulations below:</p>
<pre><code class="language-csharp !whitespace-pre hljs">// Increment custom property value by 1
Countly.Instance.UserProfile.Increment("used");

// Increment custom property value by provided value
Countly.Instance.UserProfile.IncrementBy("used", 2);

// Save maximal value between existing and provided
Countly.Instance.UserProfile.SaveMax("highscore", 300);

// Save minimal value between existing and provided
Countly.Instance.UserProfile.SaveMin("best_time", 60);
  
// Multiply custom property value by the provided value
Countly.Instance.UserProfile.Multiply("used", 3);

// Removes existing property from the array
Countly.Instance.UserProfile.Pull("type", "remove");

// Insert value to the array, which can have duplicates
Countly.Instance.UserProfile.Push("force", "add");

// Insert value to the array of unique values
Countly.Instance.UserProfile.PushUnique("single", "unique");

// Set value if it does not exist yet
Countly.Instance.UserProfile.SetOnce("tag", "test");

// Send provided values to server
Countly.Instance.UserProfile.Save();</code></pre>
<p>
  Apart from updating a single property in one request, modifying multiple (unique)
  properties in one request is possible. For example, this enables incrementing
  HighScore and multiplying BestTime in the same request. Similarly, it's possible
  to record any number of modified requests and save them all together in one single
  request instead of multiple requests.
</p>
<p>
  It should be noted that when modifying multiple properties in one request, the
  properties must be unique. A property shouldn’t be modified more than once in
  a single request. However, if a property is recorded more than once, only the
  latest value will be posted to the server.
</p>
<p>Example:</p>
<pre><code class="language-csharp !whitespace-pre hljs">Countly.Instance.UserProfile.IncrementBy("HighScore", 90);
Countly.Instance.UserProfile.Multiply("BestTime", 20);
Countly.Instance.UserProfile.Save();</code></pre>
<h2 class="anchor-heading" id="h_01HABTZ316445B91Y1ZHCS6DGK">Consent</h2>
<p>
  This feature requires<code>Users</code>consent. If consent is required and not
  given, recording user profile information will not be possible.
</p>
<h1 class="anchor-heading" id="user-consent-management" tabindex="-1">User Consent</h1>
<p>
  In an effort to comply with GDPR, starting from 20.11.1, Unity Countly SDK provides
  ways to toggle different Countly features on/off depending on the given consent.
</p>
<p>
  More information about GDPR can be found
  <a href="https://medium.com/countly/countly-the-gdpr-how-worlds-leading-mobile-and-web-analytics-platform-can-help-organizations-5015042fab27">here</a>.
</p>
<h2 id="h_01HABTZ3166JHBX2JCSEG70T78">Setup During Init</h2>
<p>
  The requirement for consent is disabled by default. To enable it, you will have
  to set <code>RequiresConsent</code> value <code>true</code> before initializing
  Countly.
</p>
<pre><code class="language-csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .EnableLogging()
  .SetNotificationMode(TestMode.AndroidTestToken)
  .SetRequiresConsent(true);
  
Countly.Instance.Init(configuration);</code></pre>
<p>
  By default, when consent is required, no consent is given. If no consent is given,
  SDK will not work and no network requests related to its features will be sent.
  When the consent status of a feature is changed, that change will be sent to
  the Countly server.
</p>
<p>
  Set consent is not persistent and will have to be set each time before Countly
  init. Therefore, the storage and persistence of the given consent fall on the
  SDK integrator.
</p>
<p>
  Consent for features may be given and revoked at any time, but if it is given
  after Countly init, some features may only work in part.
</p>
<p>
  Feature names in the <strong>Unity SDK,</strong> are stored as
  <strong>Enum</strong> called <code>Consents</code>.
</p>
<p>The current features are:</p>
<ul>
  <li data-list-item-id="eca9885bd43de6c60b8859e6645f34f97">
    <code>Sessions</code> - tracking when, how often, and how long users use
    your app
  </li>
  <li data-list-item-id="eeb7735e7f179ea937505f00cb2f6d78e">
    <code>Events</code> - allow sending events to the server
  </li>
  <li data-list-item-id="e5104a88d6226941b6820efd8ab1a20a9">
    <code>Views</code> - allow the tracking of which views users visit
  </li>
  <li data-list-item-id="eed2c0c4dd16cf0c7b430bcc3523d8147">
    <code>Location</code> - allow the sending of location information
  </li>
  <li data-list-item-id="e3e305c08a58b177e3fea38f3b4a5be30">
    <code>Crashes</code> - allow the tracking of crashes, exceptions, and errors
  </li>
  <li data-list-item-id="ec260e1a10d4a1b53de6a8ff7c529daae">
    <code>Users</code> - allow the collecting/providing of user information,
    including custom properties
  </li>
  <li data-list-item-id="ee9fbb18a9c8e5d3a2ce8dc822349b534">
    <code>Push</code> - allow push notifications
  </li>
  <li data-list-item-id="e3796863dc558cf62d0b2e228c0fea552">
    <code>StarRating</code> - allow their rating and feedback to be sent
  </li>
  <li data-list-item-id="e8fab7f14b5ce31fae7b32f7e1960bd8a">
    <code>RemoteConfig</code> - allow downloading remote config values from your
    server
  </li>
</ul>
<p>
  In case consent is required, you may give consent to features before the SDK
  Init call. These features consents are not persistent and must be given on every
  restart.
</p>
<pre><code class="language-csharp !whitespace-pre hljs">// prepare consents that should be given
Consents[] consents = new Consents[] { Consents.Users, Consents.Location };

// give consents to the features
configuration.GiveConsent(consents);</code></pre>
<h2 class="anchor-heading" id="changing-consent">Changing Consent</h2>
<p>
  After init call, use <code class="!csharp">Countly.Instance.Consents.</code>
  to change consent.
</p>
<p>There are 2 ways of changing feature consent:</p>
<ul>
  <li data-list-item-id="e6bc241a840093d268fc3f9d46534453b">
    <code>GiveConsent</code>/<code>RemoveConsent</code> - gives or removes consent
    to a specific feature.
  </li>
</ul>
<pre><code class="language-csharp !whitespace-pre hljs">// give consent to "sessions" feature
Countly.Instance.Consents.GiveConsent(new Consents[] { Consents.Sessions });

// remove consent from "sessions" feature
Countly.Instance.Consents.RemoveConsent(new Consents[] { Consents.Sessions });</code></pre>
<ul>
  <li data-list-item-id="ed4aacc2661dcc9ec8faf91bdc3df8225">
    <code>GiveConsentAll</code> / <code>RemoveAllConsent</code>- gives or removes
    all consents.
  </li>
</ul>
<pre><code class="language-csharp !whitespace-pre hljs">// give consent to all features
Countly.Instance.Consent.GiveConsentAll();

// remove consent from all features
Countly.Instance.Consent.RemoveAllConsent();</code></pre>
<h2 id="h_01HABTZ316CNJB7T2VB4A5ASSW">
  <span style="font-weight: 400;">Feature Groups</span>
</h2>
<p>
  Consents may be put into groups. By doing this, you may give/remove consent to
  multiple features in the same call. Groups may be created using
  <code>CreateConsentGroup</code> call during SDK configuration. Those groups are
  not persistent and must be created on every restart. During SDK configuration
  consents to groups may be given by using <code>GiveConsentToGroup</code>.
</p>
<pre><code class="language-csharp !whitespace-pre hljs">// prepare consents that should be added to the group 
Consents[] consents = new Consents[] { Consents.Users, Consents.Location };

// create the Consent group
configuration.CreateConsentGroup("User-Consents", consents);

// give consent to the provide consent group
configuration.GiveConsentToGroup("User-Consents");</code></pre>
<p>
  After init has been called, use <code>GiveConsentToGroup</code> /
  <code>RemoveConsentOfGroup</code> to give or remove consent for a feature group.
</p>
<p>Example:</p>
<pre><code class="language-csharp !whitespace-pre hljs">// prepare array of groups 
string[] groupName = new string[] { "User-Consents", "Events-Consents" };

// give consent to groups
Countly.Instance.Consent.GiveConsentToGroup(groupName);

// remove consent of groups
Countly.Instance.Consent.RemoveConsentOfGroup(groupName);</code></pre>
<h1 id="h_01HABTZ316AYQFEVA6BEXF711V">Security and Privacy</h1>
<h2 class="anchor-heading" id="parameter-tampering-protection">Parameter Tamper Protection</h2>
<p>
  You may set the optional <code>salt</code> to be used for calculating the checksum
  of requested data which will be sent with each request, using the
  <code>&amp;checksum</code> field. You will need to set exactly the same
  <code>salt</code> on the Countly server. If the <code>salt</code> on the Countly
  server is set, all requests would be checked for the validity of the
  <code>&amp;checksum</code> field before being processed.
</p>
<pre><code class="language-csharp !whitespace-pre hljs">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetParameterTamperingProtectionSalt("Salt");</code></pre>
<h1 id="h_01HABTZ317YY21TT4G68H4VJM4">Other Features</h1>
<h2 id="h_01HCHSPK9JJC6GC35NHZJQ4F4Y">SDK Config Parameters Explained</h2>
<p>
  To change the Configuration, update the values of parameters in the "<strong>CountlyConfiguration" </strong>object.
  These are the methods that lets you set values in your "<strong>CountlyConfiguration</strong>"
  object:
</p>
<p>
  <strong>SetDeviceId(string deviceId)</strong> - your Device ID. It is an optional
  parameter. <strong>Example:</strong> f16e5af2-8a2a-4f37-965d-qwer5678ui98.
</p>
<p>
  <strong>SetParameterTamperingProtectionSalt(string salt)</strong> - used to prevent
  parameter tampering. The default value is <strong>NULL</strong>.
</p>
<p>
  <strong>EnableForcedHttpPost()</strong> - when enabled, all requests made to
  the Countly server will be done using HTTP POST. Otherwise, the SDK sends all
  requests using the HTTP GET method. In some cases, if the data to be sent exceeds
  the 1800-character limit, the SDK uses the POST method.The default value is
  <strong>false</strong>
</p>
<p>
  <strong>SetRequiresConsent(bool enable)</strong> - this is useful during the
  app run when the user wants to opt-out of SDK features.
</p>
<p>
  <strong>EnableLogging()</strong> - this parameter is useful when you are debugging
  your application. When set to <strong>true</strong>, it basically turns on Logging.
</p>
<p>
  <strong>SetUpdateSessionTimerDelay(int duration)</strong> - sets the interval
  (in seconds) after which the application will automatically extend the session,
  providing the manual session is disabled. This interval is also used to process
  requests in the queue. The default value is <strong>60</strong> (seconds).
</p>
<p>
  <strong>SetEventQueueSizeToSend(int threshold)</strong> - sets a threshold value
  that limits the number of events that can be recorded internally by the system
  before they can all be sent together in one request. Once the threshold limit
  is reached, the system groups all recorded events and sends them to the server.
  The default value is <strong>100.</strong>
</p>
<p>
  <strong>SetMaxRequestQueueSize(int limit)</strong> - sets a threshold value that
  limits the number of requests that can be stored internally by the system. The
  system processes these requests after every session duration interval has passed.
  The default value is <strong>1000.</strong>
</p>
<p>
  <strong>SetNotificationMode(TestMode mode)</strong> - when
  <strong>None</strong>, the SDK disables Push Notifications for the device. Use
  an <strong>iOS Test Token </strong>or an <strong>Android Test Token</strong>
  for testing purposes, and in production use a
  <strong>Production Token.</strong> The SDK uses the supplied mode for sending
  Push Notifications. The default value is <strong>None.</strong>
</p>
<p>
  <strong>DisableAutomaticCrashReporting()</strong> - turns off Automatic Crash
  Reporting. When <strong>enabled</strong>, the SDK will catch exceptions and automatically
  report them to the Countly server. It's enabled by default.
</p>
<h2 id="h_01HPGPY37EVNPFRRXH07DTV7QV">Example Integrations</h2>
<p>
  To look at our sample application, download the sample project from
  <a href="http://github.com/countly/countly-sdk-unity" target="_self" rel="undefined">GitHub repo</a>
  and open the 'EntryPoint.unity' scene. 'EntryPoint.unity' located in 'Example'
  folder under Assets. There is also 'CountlyEntryPoint.cs' script in Example folder,
  and this script shows how most of the functionality can be used.
</p>
<h2 id="h_01HCHSPK9K9CM6204WD2Z06WTZ">Checking If the SDK Has Been Initialized</h2>
<p>
  In case you would like to check if init has been called, you may use the following
  property:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">Countly.Instance.IsSDKInitialized;</code></pre>
<h2 class="anchor-heading" id="sdk-internal-limits">SDK Internal Limits</h2>
<p>
  SDK does have configurable fields to manipulate the internal SDK value and key
  limits. If values or keys provided by the user, would exceed the limits, they
  would be truncated. These are the methods that let's you set limits. For further
  details please have a look
  <a href="/hc/en-us/articles/9290669873305#sdk_internal_limits">here</a>.
</p>
<h3 id="h_01HRYHGASG78HB8NM4T64KZ0NS">Key Length</h3>
<p>
  <strong>SetMaxKeyLength(int length) - </strong>maximum size of all string keys.
  The default value is <strong>128</strong>.
</p>
<pre><code class="language-csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetMaxKeyLength(120);</code></pre>
<h3 id="h_01HRYHGASG1C44VHKRAHNTW0HR">Value Size</h3>
<p>
  <strong>SetMaxValueSize(int size) - </strong>maximum size of all values in our
  key-value pairs. The default value is <strong>256</strong>.
</p>
<pre><code class="language-csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetMaxValueSize(240);</code></pre>
<h3 id="h_01HRYHGASG9DBJF5KNRT0JWQ55">Segmentation Values</h3>
<p>
  <strong>SetMaxSegmentationValues(int values) - </strong>maximum amount of custom
  (dev provided) segmentation in one event. The default value is
  <strong>100</strong>.
</p>
<pre><code class="language-csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetMaxSegmentationValues(35);</code></pre>
<h3 id="h_01HRYHGASHPHPEZ3RB698QQ73W">Breadcrumb Count</h3>
<p>
  <strong>SetMaxBreadcrumbCount(int amount) </strong>- maximum amount of breadcrumbs.
  The default value is <strong>100</strong>.
</p>
<pre><code class="language-csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetMaxBreadcrumbCount(101);</code></pre>
<h3 id="h_01HRYHGASH3B0YQRS1065R5BHW">Stack Trace Lines Per Thread</h3>
<p>
  <strong>SetMaxStackTraceLinesPerThread(int lines) - </strong>limits how many
  stack trace lines would be recorded per thread. The default value is
  <strong>30</strong>.
</p>
<pre><code class="language-csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetMaxStackTraceLinesPerThread(32);</code></pre>
<h3 id="h_01HRYHGASH45K0F6KWG2B8RY0X">Stack Trace Line Length</h3>
<p>
  <strong>SetMaxStackTraceLineLength(int length) - </strong>limits how many characters
  are allowed per stack trace line. The default value is <strong>200</strong>.
</p>
<pre><code class="language-csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetMaxStackTraceLineLength(230);</code></pre>
<h2 id="01HFEMPN4D6V1PJ7R9WC6WZ17H">Custom Metrics</h2>
<p>
  In certain situations, such as beginning a session or requesting remote config,
  the SDK sends device metrics. You have the flexibility to override the sent metrics,
  such as the operating system for a specific variant, or to provide your own custom
  metrics by using <code>SetMetricOverride</code>.
</p>
<p>Example:</p>
<pre><code class="language-csharp !whitespace-pre hljs">// overriding default metrics
Dictionary&lt;string, string&gt; overridenMetrics = new Dictionary&lt;string, string&gt;();
overridenMetrics.Add("_os", "CustomOS");
configuration.SetMetricOverride(overridenMetrics);

// providing custom metrics
Dictionary&lt;string, string&gt; customMetric = new Dictionary&lt;string, string&gt;();
customMetric.Add("customMetric", "CustomValue");
configuration.SetMetricOverride(customMetric);</code></pre>
<p class="anchor-heading">
  For more information about metric keys, you can refer
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts#h_01HABT18WWYQ2QYPZY3GHZBA9B">here</a>
  for a comprehensive list and descriptions of available metrics.
</p>
<h2 id="h_01HCHSPK9K615SPYZP2NF2KXN0">Setting Event Queue Threshold</h2>
<p>
  In SDK configuration, you may limit the number of events that can be recorded
  internally by the system before they can all be sent together in one request.
  Example:
</p>
<pre><code class="language-csharp !whitespace-pre hljs">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetEventQueueSizeToSend(1222);

Countly.Instance.Init(configuration);</code></pre>
<p>
  Once the threshold limit is reached, the system groups all recorded events and
  sends them to the server.
</p>
<h2 id="h_01HCHSPK9KGDDVYABV77TPEDFM">Setting Maximum Request Queue Size</h2>
<p>
  When you initialize Countly, you can specify a value for the StoredRequestLimit
  flag. This flag limits the number of requests that can be stored in the request
  queue when the Countly server is unavailable or experiencing connection problems.
</p>
<p>
  If the server is down, requests sent to it will be queued on the device. If the
  number of queued requests becomes excessive, it can cause problems with delivering
  the requests to the server, and can also take up valuable storage space on the
  device. To prevent this from happening, the StoredRequestLimit flag limits the
  number of requests that can be stored in the queue.
</p>
<p>
  If the number of requests in the queue reaches the StoredRequestLimit limit,
  the oldest requests in the queue will be dropped, and the newest requests will
  take their place. This ensures that the queue doesn't become too large, and that
  the most recent requests are prioritized for delivery.
</p>
<p>
  If you do not specify a value for the StoredRequestLimit flag, the default setting
  of 1,000 will be used.
</p>
<pre><code class="language-csharp !whitespace-pre hljs">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetMaxRequestQueueSize(500);</code></pre>
<h1 id="h_01HCHSPK9KVEWVKRB0CRY25S8K">FAQ</h1>
<h2 id="h_01HCHSPK9KTK4V1CCZXVND2TSV">What Information is Collected by the SDK</h2>
<p>
  The following description mentions data that is collected by SDK to perform their
  functions and implement the required features. Before any of it is sent to the
  server, it is stored locally. For further information please have a look
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts#h_01HJ5MD0WB97PA9Z04NG2G0AKC">here</a>.
</p>
<ul>
  <li data-list-item-id="ebeb50dcaef4628a02aeeb4c9d6e664ad">
    When generating a device ID, if no custom ID is provided, the SDK will use:
    <ul>
      <li data-list-item-id="ecc9751f1f637389b1d6f8061e0f9c4bf">Android: md5 of ANDROID_ID</li>
      <li data-list-item-id="ecb8a44bde84af1f88b0aed6a03018b4a">iOS: It will be vendor id and advertising id as a fallback</li>
      <li data-list-item-id="e3f572873296f61ca2b12991bf7b64a84">Windows Store Apps: It will be advertising id</li>
      <li data-list-item-id="e2a880e793fb0217afb3386fdbf1aeb56">
        Windows Standalone: It will be hash from the concatenation of strings
        taken from computer system hardware classes.
      </li>
    </ul>
  </li>
</ul>