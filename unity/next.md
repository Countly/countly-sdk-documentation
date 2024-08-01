<p>
  This documentation is for the Countly Unity SDK version 23.12.X. The SDK source
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
  <a href="https://github.com/Countly/countly-sdk-unity/releases" target="_blank" rel="noopener">GitHub</a>
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
  <span data-preserver-spaces="true">Since Unity version 2020 this package is added to your project automatically by Unity. For versions before that, (2018 and 2019) you have to install this package in the project manually. </span>
</p>
<p>
  <span data-preserver-spaces="true">One way to do Install the </span><strong><span data-preserver-spaces="true">Newtonsoft Json </span></strong><span data-preserver-spaces="true">package would be to use the built-in package manager. You would go to </span><strong><span data-preserver-spaces="true">Windows </span></strong><span data-preserver-spaces="true">=&gt; </span><strong><span data-preserver-spaces="true">Package Manager</span></strong><span data-preserver-spaces="true">. In there you would see something like this:<img src="/guide-media/01GVDG0BAGCD7VJ9EYNK3GS32F" alt="image-newtonsoft.png"></span>
</p>
<h2 id="h_01HABTZ314XCMNWWK698JR773J">Minimal Setup</h2>
<p>
  Before you can use any functionality, you have to initiate the SDK.
</p>
<p>
  The shortest way to initiate the SDK is with this code snippet:
</p>
<pre><code class="!whitespace-pre hljs language-csharp">string appKey = "<span>COUNTLY_APP_KEY";</span>
string serverUrl = "<span>COUNTLY_SERVER_URL"</span>;

CountlyConfiguration config = <strong>new</strong> CountlyConfiguration(appKey, serverUrl);
Countly.Instance.Init(config);
</code></pre>
<p>
  <span>In the </span><code>CountlyConfiguration</code><span> object, you provide appKey and your Countly server URL. Please check <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KX44C9SF48WRPQNCP3">here</a> for more information on how to acquire your application key (APP_KEY) and server URL.</span>
</p>
<div class="callout callout--info">
  <p>
    If you are in doubt about the correctness of your Countly SDK integration
    you can learn about the verification methods from
    <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#how-to-validate-your-countly-integration" target="blank">here</a>.
  </p>
</div>
<h2 id="require-app-permissions" class="anchor-heading">Required App Permissions</h2>
<p>
  If you expect the game to be saved on an SD card or any other type of external
  storage, set <strong>Write Permission</strong> to 'External (SDCard). This can
  be found in your Android platform settings under 'Other Settings'.
</p>
<p>
  When configuring your app, make sure that it has permission to access the internet.
</p>
<h2 id="h_01HABTZ314QNCDAQT0SC5NETCG" class="anchor-heading">SDK Data Storage</h2>
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
  <a href="https://www.iboxdb.com/" target="_self"> iBoxDB</a> database file, named
  'db3.box'.
</p>
<p>
  <span>The specific path where the database file would be stored is different for different platforms. To determine the specific path where the database is stored, you would look at the value returned by </span><span><code>Application.persistentDataPath</code>.</span>
</p>
<div>
  <p>
    <span>Following are the locations of the database file were used in our sample app:</span>
  </p>
  <ul>
    <li>
      <span><strong>Android: </strong>'/storage/emulated/0/Android/data/ly.count.demo/files/db3.box'</span>
    </li>
    <li>
      <span><strong>Linux: </strong>'home/&lt;username&gt;/.config/unity3d/Countly/CountlyDotNetSDK/db3.box'</span>
    </li>
    <li>
      <span><strong>Windows: </strong></span>'C:/Users/&lt;username&gt;/AppData/LocalLow/Countly/CountlyDotNetSDK/db3.box'
    </li>
    <li>
      <strong>Mac OSX: </strong><span>'~/Library/Application Support/Countly/CountlyDotNetSDK/db3.box'</span>
    </li>
    <li>
      <span><strong>iOS: </strong>'/var/mobile/Containers/Data/Application/&lt;random-folder-name&gt;/Documents/db3.box'</span><span></span>
    </li>
  </ul>
</div>
<h2 id="h_01HABTZ31446VPCP3M6Y0PWMNY">SDK Notes</h2>
<p>
  To access the Countly Global Instance use the following code snippet:
</p>
<pre>Countly.Instance</pre>
<h1 id="enabling-logging" class="anchor-heading">SDK Logging / Debug Mode</h1>
<p>
  <span>The first thing you should do while integrating our SDK is enabling logging. If logging is enabled, then our SDK will print out debug messages about its internal state and encountered problems.</span>
</p>
<p>
  Call <code>EnableLogging</code> on the config object to enable logging:
</p>
<pre><code class="csharp">CountlyConfiguration config = new CountlyConfiguration(appKey, serverUrl)
  .EnableLogging();</code></pre>
<p>
  For more information on where to find the SDK logs you can check the documentation
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#finding-sdk-logs" target="blank">here</a>.
</p>
<h1 id="h_01HABTZ31464JJFMECCZEH8F4C" class="anchor-heading" tabindex="-1">Crash Reporting</h1>
<p>
  The Countly SDK for Unity can collect
  <a href="http://resources.count.ly/docs/introduction-to-crash-reporting-and-analytics">Crash Reports</a>,
  which you may examine and resolve later on the server.
</p>
<p>
  In the SDK all crash-related functionalities can be browsed from the returned
  interface on:
</p>
<pre>countly.CrashReports</pre>
<h2 id="h_01HABTZ314AT5KAJCM51D304ZV">Automatic Crash Handling</h2>
<p>
  The Unity SDK can automatically report uncaught exceptions/crashes in the application
  to the Countly server. This feature is enabled by default. In order to, stop
  reporting uncaught exceptions/crashes automatically, call<strong> DisableAutomaticCrashReporting()</strong><span>, </span><span>in the SDK configuration.</span>
</p>
<h2 id="h_01HABTZ314W6CP02BBBHB6FBKJ" class="anchor-heading">Handled Exceptions</h2>
<p>
  <span>You might catch an exception or similar error during your app’s runtime.</span><span> You may also log these handled exceptions to monitor how and when they are happening. </span>To
  log exception use the following code snippet:
</p>
<pre><strong>await</strong> countly.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, null, false); </pre>
<p>Here is the detail of the parameters:</p>
<ul>
  <li>
    <strong>message -</strong> (<span>Mandatory</span>, string) a string that
    contains a detailed description of the exception.
  </li>
  <li>
    <strong>stackTrace -</strong> (<span>Mandatory, </span>string) a string that
    describes the contents of the call stack.
  </li>
  <li>
    <strong>segments -</strong> (Optional, IDictionary&lt;string, string&gt;)
    custom key/values to be reported.
  </li>
  <li>
    <strong>nonfatal -</strong> (Optional, bool) set false if the error is fatal.
  </li>
</ul>
<p>Example:</p>
<pre><code class="csharp">try {
  throw new DivideByZeroException();
} catch (Exception ex) {
  await countly.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace);
}</code></pre>
<p class="anchor-heading">You can also send a segmentation with an exception.</p>
<pre><code class="csharp"><span>Dictionary&lt;string, object&gt; segmentation = <strong>new</strong> Dictionary&lt;string, object&gt;();
segmentation.Add("Action", "click");</span>
try {
  throw new DivideByZeroException();
} catch (Exception ex) {
  await countly.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, segmentation, true);
}</code></pre>
<p>
  <span>If you have handled an exception and it turns out to be fatal to your app, you may use the following calls:</span>
</p>
<pre><code class="!whitespace-pre hljs language-csharp"><strong>await</strong> countly.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, null, false);</code></pre>
<pre><code class="!whitespace-pre hljs language-csharp">Dictionary&lt;string, object&gt; segmentation = <strong>new</strong> Dictionary&lt;string, object&gt;();
segmentation.Add("Action", "click");
<strong>await</strong> countly.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, segmentation, false);</code></pre>
<h2 id="h_01HABTZ314FEB9WM3P718TVMHY" class="anchor-heading">Crash Breadcrumbs</h2>
<p>
  Throughout your app, you can leave crash breadcrumbs. They are short logs<span> that </span>would
  describe the previous steps that were taken in your app before the crash. After
  a crash happens, they will be sent together with the crash report.
</p>
<p>The following command adds a crash breadcrumb:</p>
<pre><code class="!whitespace-pre hljs language-csharp">countly.CrashReports.AddBreadcrumbs("breadcrumb");</code></pre>
<h2 id="h_01HABTZ3140XGZJY6K0J169K5Q" class="anchor-heading">Consent</h2>
<p>
  This feature uses <code>Crashes</code><span> consent. No additional crash logs will be recorded if consent is required and not given.</span>
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
<pre>countly.Events</pre>
<p>
  <span>There are a couple of values that can be set when recording an event. The main one is the <strong>key</strong> property which would be the identifier/name for that event. For example, in case a user purchased an item in a game, you could create an event with the key 'purchase'.</span>
</p>
<p>
  <span>Optionally there are also other properties that you might want to set:</span>
</p>
<ul>
  <li>
    <strong>count -</strong> a whole numerical value that marks how many times
    this event has happened. The default value for that is <strong>1</strong>.
  </li>
  <li>
    <strong>sum -</strong> this value would be summed across all events in the
    dashboard. F<span>or example, in-app purchase events sum of purchased items. Its default value is <strong>0</strong>.</span>
  </li>
  <li>
    <strong>duration - </strong>used to record and track the duration of events.
    The default value is <strong>0</strong>.
  </li>
  <li>
    <strong>segments - </strong>a value where you can provide custom segmentation
    for your events to track additional information. It is a key and value map.
    The accepted data types for the value are "String", "Integer", "Double",
    and "Boolean". All other types will be ignored.
  </li>
</ul>
<h2 id="h_01HABTZ314FCF1V827B38D1TEA">Recording Events</h2>
<p>
  <span>Here is a quick way to </span><span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">record an event:</span>
</p>
<pre><strong>public</strong> async Task RecordEventAsync(string key, IDictionary&lt;string, object&gt; segmentation = null, int? count = 1, double? sum = 0, double? duration = null);</pre>
<p>
  <span style="font-weight: 400;">Based on the example below of an event recording a <strong>purchase</strong>, h</span><span style="font-weight: 400;">ere is a quick summary of the information for each usage:</span>
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
    Usage 3: how many times the <strong>purchase</strong> event occurred +
    <span style="font-weight: 400;">from which countries and application versions those purchases were made.</span>
  </li>
  <li>
    Usage 4: how many times the <strong>purchase</strong> event occurred +
    <span style="font-weight: 400;">the total amount, both of which are also available, segmented into countries and application versions.</span>
  </li>
  <li>
    Usage 5: how many times the <strong>purchase</strong> event occurred +
    <span style="font-weight: 400;">the total amount, both of which are also available, segmented by countries and application versions + the total duration of those events.</span>
  </li>
</ul>
<p>
  <strong>1. Event key and count</strong>
</p>
<pre><code class="!whitespace-pre hljs language-csharp"><strong>await</strong> countly.Events.RecordEventAsync(key: "purchase", count: 1);</code></pre>
<p>
  <strong>2. Event key, count, and sum</strong>
</p>
<pre><code class="!whitespace-pre hljs language-csharp"><strong>await</strong> countly.Events.RecordEventAsync(key: "purchase", count: 1, sum: 0.99);</code></pre>
<p>
  <strong>3. Event key and count with segmentation(s)</strong>
</p>
<pre><code class="!whitespace-pre hljs language-csharp">Dictionary&lt;string, object&gt; segmentation = new Dictionary&lt;string, object&gt;();
segmentation.Add("country", "Germany");
segmentation.Add("app_version", "1.0");

<strong>await</strong> countly.Events.RecordEventAsync(key: "<span>purchase</span>", segmentation: segmentation, count: 1);</code></pre>
<p>
  <strong>4. Event key, count, and sum with segmentation(s)</strong>
</p>
<pre><code class="!whitespace-pre hljs language-csharp">Dictionary&lt;string, object&gt; segmentation = new Dictionary&lt;string, object&gt;();
segmentation.Add("country", "Germany");
segmentation.Add("app_version", "1.0");

<strong>await</strong> countly.Events.RecordEventAsync(key: "<span>purchase</span>", segmentation: segmentation, count: 1, sum: 0.99);</code></pre>
<p>
  <strong>5. Event key, count, sum, and duration with segmentation(s)</strong>
</p>
<pre><code class="!whitespace-pre hljs language-csharp">Dictionary&lt;string, object&gt; segmentation = new Dictionary&lt;string, object&gt;();
segmentation.Add("country", "Germany");
segmentation.Add("app_version", "1.0");

<strong>await</strong> countly.Events.RecordEventAsync(key: "<span>purchase</span>", segmentation: segmentation, count: 1, sum: 0.99, duration: 60);
</code></pre>
<p>
  These are only a few examples of what you can do with Events. You may go beyond
  those examples and use country, app_version, game_level, time_of_day, and any
  other segmentation of your choice that will provide you with valuable insights.
</p>
<h2 id="h_01HABTZ314NDJQTBAS03YREYZ7">Timed Events</h2>
<p>
  <span>It's possible to create timed events by defining a start and a stop moment.</span>
</p>
<pre><code class="!whitespace-pre hljs language-csharp">string eventName = <span class="hljs-string">"Some event"</span>;

<span class="hljs-comment">//start some event</span>
Countly.Instance.Events.StartEvent(eventName);
<span class="hljs-comment">//wait some time</span>

<span class="hljs-comment">//end the event </span>
Countly.Instance.Events.EndEvent(eventName);</code></pre>
<p>
  <span>You may also provide additional information when ending an event. In that case you can provide the segmentation, count, or sum values. The default values for those are "null", 1, and 0.</span>
</p>
<pre><code class="!whitespace-pre hljs language-csharp">string eventName = "Some event";

//start some event
Countly.Instance.Events.StartEvent(eventName);
//wait some time

IDictionary&lt;string, object&gt; segmentation = new Dictionary&lt;string, object&gt;();
segmentation.Add("wall", "orange");

//end the event while also providing segmentation information
Countly.Instance.Events.EndEvent(eventName, segmentation);
</code></pre>
<p>Here are other options to end timed events:</p>
<pre><code class="!whitespace-pre hljs language-csharp">//end the event while providing segmentation information and count
Countly.Instance.Events.EndEvent("timed-event", segmentation, 4);

//end the event while providing segmentation information, count and sum
Countly.Instance.Events.EndEvent("timed-event", segmentation, 4, 10);</code></pre>
<p>
  You may cancel the started timed event in case it is not relevant anymore:
</p>
<pre><code class="!whitespace-pre hljs language-csharp">//start some event
Countly.Instance.Events.StartEvent(eventName);
//wait some time

//cancel the event
Countly.Instance.Events.CancelEvent(eventName);</code></pre>
<h2 id="h_01HABTZ315TW0Q6G8BFK19SDTM" class="anchor-heading">Consent</h2>
<p>
  <span>This feature uses <code>Events</code> consent. </span><span>No additional events will be recorded if consent is required and not given.</span>
</p>
<p>
  <span>When consent is removed, all previously started timed events will be canceled.</span>
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
  <span>You might want to disable automatic session tracking. To do so, use the following code snippet before</span><span> init call.</span>
</p>
<pre>config.DisableAutomaticSessionTracking();</pre>
<p>
  Note that after disabling session tracking, the following things would happen:
</p>
<ul>
  <li class="p-rich_text_section">Session information would not be recorded</li>
  <li class="p-rich_text_section">Device metrics would not be recorded</li>
  <li class="p-rich_text_section">
    On dashboard location map would not be updated and, overview and analytics
    session related to sessions and users would all be empty
  </li>
</ul>
<h2 id="h_01HABTZ315Y9VYNGNW2XBFGREJ" class="anchor-heading">Consent</h2>
<p>
  <span>This feature requires<code>Sessions</code> consent. Sessions and metrics will not be recorded if consent is required and not given.</span>
</p>
<p>
  If consent was given and then is removed, the current session will not get explicitly
  ended.
</p>
<p>
  If consent was removed and then given, and automatic sessions were enabled, a
  session will automatically be started.<span></span>
</p>
<h1 id="h_01HABTZ315E40XEHJHRMQMW0J6">View Tracking</h1>
<p>
  In the SDK, all view-related functionality can be browsed from the returned interface
  on:
</p>
<pre><code class="!whitespace-pre hljs language-csharp">Countly.Instance.Views</code></pre>
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
<pre><code class="!whitespace-pre hljs language-csharp">// without segmentation
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
<pre><code class="!whitespace-pre hljs language-csharp">string id = Countly.Instance.Views.StartAutoStoppedView("View Name");</code></pre>
<h3 id="h_01HHNY1G0SVAKPH1BAKJTVVSBZ">Regular Views</h3>
<p>
  Opposed to auto-stopped views, with regular views, you can have multiple of them
  started simultaneously, and then you can control them independently.
</p>
<p>
  You can start a view that would not close when another view starts like this:
</p>
<pre><code class="!whitespace-pre hljs language-csharp">Countly.Instance.Views.StartView("View Name");</code></pre>
<p>
  While manually tracking views, you may add your custom segmentation to them like
  this:
</p>
<pre><code class="!whitespace-pre hljs language-csharp">Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
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
<pre><code class="!whitespace-pre hljs language-csharp">Countly.Instance.Views.StopViewWithName("View Name");</code></pre>
<p>You can provide a segmentation while doing so:</p>
<pre><code class="!whitespace-pre hljs language-csharp">Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("CardName", "Spell Pierce");
viewSegmentation.Add("ManaCost", 1);
viewSegmentation.Add("CardValue", 3.5);
viewSegmentation.Add("IsFoil", false);
viewSegmentation.Add("CardPower", 0.0f);
viewSegmentation.Add("CardID", 9876543210L);

Countly.Instance.Views.StopViewWithName("View Name", viewSegmentation);</code></pre>
<p>
  <span>If multiple views have the same name (they would have different identifiers), but if you try to stop one with that name, the SDK will close the one that started last.</span>
</p>
<p>To stop a view with its view ID:</p>
<pre><code class="!whitespace-pre hljs language-csharp">Countly.Instance.Views.StopViewWithID("View ID");</code></pre>
<p>You can provide a segmentation while doing so:</p>
<pre><code class="!whitespace-pre hljs language-csharp">// starting view and recording view id
string id = Countly.Instance.Views.StartAutoStoppedView("View Name");<br>
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
<pre><code class="!whitespace-pre hljs language-csharp">Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("StationName", "Alpha Centauri Base");
viewSegmentation.Add("CrewCount", 120);
viewSegmentation.Add("DistanceFromEarth", 4.37E13);
viewSegmentation.Add("HasArtificialGravity", true);
viewSegmentation.Add("OrbitalPeriod", 365.25f);
viewSegmentation.Add("StationID", 2233445566L);
  
Countly.Instance.Views.StopAllViews(viewSegmentation);</code></pre>
<h3 id="h_01HHNYPKFGD5CC7SJECDWQ7EXB">Pausing and Resuming Views</h3>
<p>
  <span>If you start multiple views simultaneously, pausing some views while others continue might be necessary. You can achieve this by using the unique identifier you get when starting a view.</span>
</p>
<p>
  <span>To pause a view with its ID:</span>
</p>
<pre><code class="!whitespace-pre hljs language-csharp">Countly.Instance.Views.PauseViewWithID("View ID");</code></pre>
<p>To resume a view with its ID:</p>
<pre><code class="!whitespace-pre hljs language-csharp">Countly.Instance.Views.ResumeViewWithID("View ID");</code></pre>
<h3 id="h_01HHNZEE94N9FH6GYZTR4A1H0M">Adding Segmentation to Started Views</h3>
<p>
  You can add segmentation values to a view before it ends. This can be done as
  often as desired, and the final segmentation sent to the server will be the cumulative
  sum of all segmentations. However, if a certain segmentation value for a specific
  key has been updated, the latest value will be used.
</p>
<p>To add segmentation to a view using its view ID:</p>
<pre><code class="!whitespace-pre hljs language-csharp">string id = Countly.Instance.Views.StartView("View Name");

Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("BookTitle", "Dune");
viewSegmentation.Add("Author", "Frank Herbert");
viewSegmentation.Add("PublicationYear", 1965);
viewSegmentation.Add("NumberofPages", 412);
viewSegmentation.Add("IsScienceFiction", true);
viewSegmentation.Add("AverageRating", 4.35f);
  
Countly.Instance.Views.AddSegmentationToViewWithID(id, viewSegmentation);</code></pre>
<p>To add segmentation to a view using its name:</p>
<pre><code class="!whitespace-pre hljs language-csharp">string viewName = "View Name";
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
<pre><code class="!whitespace-pre hljs language-csharp">Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("DeskPlant", "Cactus");
viewSegmentation.Add("CoffeeMugsOwned", 7);
viewSegmentation.Add("AverageMeetingLength", 1.5);
viewSegmentation.Add("HasOfficeDog", true);
viewSegmentation.Add("DeskHeight", 1.2f);
viewSegmentation.Add("EmployeeID", 1122334455L);

Countly.Instance.Views.SetGlobalViewSegmentation(viewSegmentation);</code></pre>
<p>You can update this segmentation any time you want:</p>
<pre><code class="!whitespace-pre hljs language-csharp">Dictionary&lt;string, object&gt; viewSegmentation = new Dictionary&lt;string, object&gt;();
viewSegmentation.Add("FavoriteGenre", "Sci-Fi");
viewSegmentation.Add("MoviesWatchedThisMonth", 15);
viewSegmentation.Add("AverageRating", 4.8);
viewSegmentation.Add("HasStreamingSubscription", true);
viewSegmentation.Add("ScreenSize", 55.0f);
viewSegmentation.Add("UserID", 5566778899L);
  
Countly.Instance.Views.UpdateGlobalViewSegmentation(viewSegmentation);</code></pre>
<h2 id="h_01HABTZ315ECG69VS4DKTX0W2N" class="anchor-heading">Consent</h2>
<p>
  <span>This feature requires <code>Views</code> consent. No additional views will be recorded if consent is required and not given.</span>
</p>
<h1 id="h_01HABTZ315QACRZ219TTBZS5ZN" class="anchor-heading" tabindex="-1">Device ID Management</h1>
<p>
  <span>A device ID is a unique identifier for your users. </span><span>You may specify the device ID yourself or allow the SDK to generate it. When providing one yourself, keep in mind that it has to be unique for all users. Some potential sources for such an id may be the users username, email or some other internal ID used by your other systems.</span>
</p>
<p>
  You can provide a device ID during initialization like this:
</p>
<pre><code class="!whitespace-pre hljs language-csharp">string DeviceId = "UNIQUE_DEVICE_ID";
CountlyConfiguration config = new CountlyConfiguration(appKey, serverUrl)
  .SetDeviceId(DeviceId);
  
Countly.Instance.Init(config);</code></pre>
<h2 id="h_01HABTZ315MW7E9560TS40F65Z" class="anchor-heading">Retrieving Current Device ID</h2>
<p>
  You may want to see what device id Countly is assigning for the specific device.
  For that, you may use the following calls.
</p>
<pre><code class="!whitespace-pre hljs language-csharp">string usedId = Countly.Instance.Device.DeviceId;</code></pre>
<p>
  <span>You can get the current device ID type. The id type is an enum with the possible values of:</span>
</p>
<ul>
  <li>SDKGenerated - device ID generated by the SDK</li>
  <li>DeveloperProvided - device ID provided by the host app</li>
</ul>
<pre><code class="!whitespace-pre hljs language-csharp">DeviceIdType type = Countly.Instance.Device.DeviceIdType;</code></pre>
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
  <span>In case your application authenticates users, you might want to change the ID to the one in your backend after he has logged in. This helps you identify a specific user with a specific ID on a device he logs in, and the same scenario can also be used in cases this user logs in using a different way (e.g another tablet, another mobile phone, or web). In this case, any data stored in your Countly server database associated with the current device ID will be transferred (merged) into the user profile with the device id you specified in the following method call:</span>
</p>
<pre><code class="!whitespace-pre hljs language-csharp"><strong>await</strong> countly.Device.ChangeDeviceIdWithMerge("New Device Id");</code></pre>
<p class="anchor-heading">
  <strong>Changing Device ID without Server Merge</strong>
</p>
<p>
  <span>You might want to track information about another separate user that starts using your app (changing apps account), or your app enters a state where you no longer can verify the identity of the current user (user logs out). In that case, you can change the current device ID to a new one without merging their data. You would call:</span>
</p>
<pre><code class="!whitespace-pre hljs language-csharp"><strong>await</strong> countly.Device.ChangeDeviceIdWithoutMerge("New Device Id");</code></pre>
<p>
  <span>Doing it this way, will not merge the previously acquired data with the new id.</span>
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
  <span>If no device ID is provided the first time the SDK is initialised, the SDK will generate a unique device ID. The source of that id is</span><span><code class="!csharp">SystemInfo.deviceUniqueIdentifier</code>which is a value exposed by Unity. It should be unique for every device.</span>
</p>
<p>
  <span>Here are the underlying mechanisms used to generate that value for some platforms:</span>
</p>
<p>
  <span><strong>IOS:</strong> on pre-iOS7 devices, it will return a hash of the MAC address. On iOS7 devices, it will be</span>
</p>
<p>
  <span><code class="!csharp">UIDevice identifierForVendor</code> or, if that fails for any reason,</span>
</p>
<p>
  <span><code class="!csharp">ASIdentifierManager advertisingIdentifier</code></span>
</p>
<p>
  <span><strong>Android: </strong><code class="!csharp">SystemInfo.deviceUniqueIdentifier</code> returns the md5 of ANDROID_ID. Note that since Android 8.0 (API level 26) ANDROID_ID depends on the app signing key. That means "unsigned" builds (which are by default signed with a debug keystore) will have a different value than signed builds (which are signed with a key provided in the player settings).</span>
</p>
<p>
  <span><strong>Windows Store Apps:</strong> uses <code class="!csharp">AdvertisingManager::AdvertisingId</code>for returning unique device identifiers.</span>
</p>
<p>
  <span><strong>Windows Standalone</strong>: returns a hash from the concatenation of strings taken from Computer System Hardware Classes. For more information, <a href="https://docs.unity3d.com/ScriptReference/SystemInfo-deviceUniqueIdentifier.html" target="_self">click here</a>.</span><span></span>
</p>
<h2 id="h_01HABTZ315T6Z5NV8QWZVYMSCG" class="anchor-heading">Consent</h2>
<p>No consent is required to change device ID.</p>
<p>
  If device ID is changed without merging and consent was enabled, all previously
  given consent will be removed. This means that all features will cease to function
  until new consent has been given again for that new device ID.
</p>
<h1 id="h_01HABTZ3157PQZHXH7YT210DJQ">Push Notifications</h1>
<p>
  <span>The Unity SKD uses FCM and APNs as push notification providers for Android and iOS platforms respectively, and it doesn't support the Huawei Push Kit push service.</span>
</p>
<p>
  <span>By default, FCM and APNs dependencies are added as part of the SDK. They can be removed in case you don't need them.</span><span></span>
</p>
<p>
  <span>Note that SDK doesn't support Deep linking, </span><span>Data only push, and </span><span>Rich push notifications yet. You can send text push notifications only.</span>
</p>
<h2 id="h_01HABTZ3152EEE6CDNGW0B29J7">Integration</h2>
<p>
  <strong><span class="wysiwyg-font-size-large">Android</span></strong>
</p>
<p>
  <span>The Countly server needs an FCM server key to send notifications through FCM. </span><span></span>
</p>
<p id="integrating-fcm-into-your-app" class="anchor-heading">
  To set it up, refer to
  <a href="https://support.count.ly/hc/en-us/articles/360037754031-Android-SDK#getting-fcm-credentials" target="_self" rel="undefined">Android documentation</a>
  and follow the following steps:
</p>
<ol>
  <li>
    <span>Download google-services.json from </span><a href="https://console.firebase.google.com/">Firebase console.</a>
  </li>
  <li>
    <span>Create google-services.xml from google-services.json. You can use an online converter </span><a href="https://dandar3.github.io/android/google-services-json-to-xml.html" rel="nofollow">here</a><span>.</span>
  </li>
  <li>
    <span>Put your file google-services.xml in /Plugins/Android/Notifications/res/values (replace if necessary).</span>
  </li>
</ol>
<p>
  <strong><span class="wysiwyg-font-size-large">iOS</span></strong>
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
  <span><strong>"COUNTLY_ENABLE_IOS_PUSH" </strong>symbol in </span><strong>Scripting Define Symbols.</strong><strong><img src="/guide-media/01GV9ZT9T72NE430KKRJMGNE4X" alt="Screenshot_2020-10-27_at_4.07.16_PM.png"></strong>
</p>
<p>
  2. After exporting the <strong>iOS</strong> project, open the project in
  <strong>Xcode</strong>, and add <strong>Push Notifications</strong> Capability.
  For further information regarding iOS app configuring refer to
  <a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#configuring-ios-app" target="_self" rel="undefined">iOS Documentation.</a>
</p>
<h2 id="h_01HABTZ3154KW34FPCX7AEJM86">
  <span>Enabling Push</span>
</h2>
<p>
  <span>By default Push Notifications are disabled. To enable push, set Notification mode other than <code>None</code> in the Configuration before SDK init call.</span>
</p>
<p>
  <span>Example:</span>
</p>
<pre><code class="!whitespace-pre hljs language-csharp">CountlyConfiguration configuration = <strong>new</strong> CountlyConfiguration(appKey, serverUrl)
  .SetNotificationMode(TestMode.AndroidTestToken);</code></pre>
<p>
  <span> Here is an overview of notification modes:</span>
</p>
<ul>
  <li>
    <span><code>None</code>- it is the default value of notification mode. This mode disables the notification feature.</span>
  </li>
  <li>
    <span><code>AndroidTestToken</code> / <code>iOSTestToken</code>- during development build, use <code>AndroidTestToken</code> and <code>iOSTestToken</code> modes for Android and iOS platforms respectively.</span>
  </li>
  <li>
    <span><code>iOSAdHocToken</code> - use this for distribution of iOS builds on TestFlight and AdHoc.</span>
  </li>
  <li>
    <span><code>ProductionToken</code> - use this mode for the production builds.</span><span></span>
  </li>
</ul>
<h2 id="h_01HABTZ315RJBF6DFEK5VPM8C0">Removing Push and Its Dependencies</h2>
<p>
  <span>By default, push dependencies are part of the SDK. You may remove them, and add them back after removing them. Don't forget to change notification mode to <code>None</code>, after removing push notification dependencies from SDK.</span>
</p>
<p>
  <strong><span class="wysiwyg-font-size-large">Android</span></strong><span></span>
</p>
<p>
  <span>To remove FCM dependencies from the android build, go to the <strong>Assets\Plugins\Android </strong>folder and delete the <strong>Notifications</strong> folder.</span>
</p>
<p>
  <span>To</span> add them back after removing<span>, re-import the Unity package.</span><span></span>
</p>
<p>
  <span class="wysiwyg-font-size-large"><strong>IOS</strong></span>
</p>
<p>
  <span>The <strong>APN's</strong> dependencies are part of the <strong>SDK.</strong> To remove the <strong>APNs</strong> dependencies, go to the <strong>Assets\Plugins </strong>folder and delete the <strong>iOS</strong> folder. Remove the <strong>"COUNTLY_ENABLE_IOS_PUSH"</strong> symbol from <strong>Scripting Define Symbols </strong>in <strong>Player Settings.</strong></span>
</p>
<p>
  <span>To</span> add them back after removing<span>, re-import the Unity package and add back the <strong>"COUNTLY_ENABLE_IOS_PUSH"</strong> symbol.</span>
</p>
<h2 id="h_01HABTZ315MGGW3YG4RHS97BVY">
  <span>Customizing Push Messages</span>
</h2>
<p>
  <strong><span class="wysiwyg-font-size-large">Android</span></strong>
</p>
<p>
  <span>To change the sound and icons of the android notifications, update the sound and icons in the folder Assets/Plugins/Android/Notifications/res.</span>
</p>
<p>
  <span><strong>Note</strong>: The Notification channel name and description can be updated through the <strong>strings.xml</strong> file located in the <strong>Assets\Plugins\Android\Notifications\res\values </strong>folder.</span>
</p>
<h2 id="h_01HABTZ315PX7MATCGB1H307YY">Handling Push Callbacks</h2>
<p>
  <span>In order to listen to notification receive and click events, implement <code>INotificationListener</code> interface and its members' methods <code>OnNotificationClicked</code> and <code>OnNotificationReceived</code> into your class.</span>
</p>
<p>
  <span>Example:</span>
</p>
<pre><code class="csharp">public class CountlyEntryPoint : MonoBehaviour, INotificationListener
{
  public void OnNotificationReceived(string message)
  {
  
  }
  public void OnNotificationClicked(string message, int index)
  {
  
  }
}</code></pre>
<p>
  <span> There are two ways to register for this class to listen to notification events.</span>
</p>
<p>
  <span>1. You may call <code>AddListener(this)</code>on <code>CountlyConfiguration</code> object before the SDK Init call.</span>
</p>
<p>
  <span>Example:</span>
</p>
<pre><code class="csharp">private void Awake()
{
  CountlyConfiguration config = <strong>new</strong> CountlyConfiguration(appKey, serverUrl);
  config.AddNotificationListener(this);
  Countly.Instance.Init(config);
}</code></pre>
<p>
  <span></span><span></span>2. If SDK has been initialized<span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">, use the following code snippet to listen to push notification events.</span>
</p>
<pre><code>Countly.Instance.Notifications.AddListener(this);</code></pre>
<p>
  <span>To stop listening notification receive and click events, call</span>
</p>
<pre><code>Countly.Instance.Notifications.RemoveListener(this);</code></pre>
<p>
  <span>For more information, check the sample app on <a href="http://github.com/countly/countly-sdk-unity" target="_blank" rel="noopener">GitHub</a>.</span>
</p>
<h2 id="h_01HABTZ315P5G15ZP38X4DMB3X" class="anchor-heading">Consent</h2>
<p>
  <span>This feature requires<code>Push</code> consent. No push notifications will be received if consent is required and not given.</span>
</p>
<h1 id="user-location" class="anchor-heading garden-focus-visible" tabindex="-1" data-garden-focus-visible="true">
  <span>User Location</span>
</h1>
<p>
  <span>While integrating this SDK into your application, you might want to track your user location. You could use this information to better know your app’s user base. There are 4 fields that can be provided:</span>
</p>
<ul>
  <li>
    <span>Country code (two-letter ISO standard).</span>
  </li>
  <li>
    <span>City name (must be set together with the country code).</span>
  </li>
  <li>
    <span>Latitude and longitude values separated by a comma, e.g. "56.42345,123.45325". </span>
  </li>
  <li>
    <span>Your user’s IP address.</span><span></span>
  </li>
</ul>
<h2 id="setting-location" class="anchor-heading">Setting Location</h2>
<p>
  <span>During init, you can </span><span>set location info in the configuration:</span>
</p>
<pre>config.SetLocation(countryCode, city, gpsCoordinates, ipAddress);</pre>
<p>
  <span>After SDK initialization, this location info will be sent to the server at the start of the user session.</span>
</p>
<p>
  <span>Note that the IP address will only be updated if set through the init process.</span>
</p>
<p>
  <span>Use <code>Countly.Location.</code> to disable or set the location at any time after the SDK Init call.</span>
</p>
<p>
  <span>For example:</span>
</p>
<pre><code class="hljs cs"><span><span class="hljs-keyword">string</span> countryCode = </span><span class="hljs-string">"us"</span><span>;
<span class="hljs-keyword">string</span> city = </span><span class="hljs-string">"Houston"</span><span>;
<span class="hljs-keyword">string</span> latitude = </span><span class="hljs-string">"29.634933"</span><span>;
<span class="hljs-keyword">string</span> longitude = </span><span class="hljs-string">"-95.220255"</span><span>;
<span class="hljs-keyword">string</span> ipAddress = </span><span class="hljs-keyword"><span class="hljs-literal">null</span></span>;

<span>Countly.Instance</span>.Location.S<span>etLocation</span>(<span>countryCode, city, latitude + </span><span class="hljs-string">","</span><span> + longitude, ipAddress</span>);</code></pre>
<p>
  When those values are set, a separate request will be created to send them. Except
  for IP address, because Countly server processes IP address only when starting
  a session.
</p>
<p>If you don't want to set specific fields, set them to null.</p>
<h2 id="disabling-location" class="anchor-heading">Disabling Location</h2>
<p>
  <span>Users might want to opt-out of location tracking. To do so, </span><span>you can disable location during init:</span>
</p>
<pre>config.DisableLocation();</pre>
<p>To disable location after SDK initialization, call:</p>
<pre>Countly.Instance.Location.DisableLocation();</pre>
<p>
  <span>These actions will erase the cached location data from the device and the server.</span><span></span>
</p>
<h2 id="h_01HABTZ316DN526NN0V577XVCQ" class="anchor-heading">Consent</h2>
<p>
  <span>This feature requires<code>Location</code> consent. If consent is not given and is required, no location information will be recorded. No reverse geo IP will be performed server side. SDK will behave as if location tracking is disabled.</span>
</p>
<p>
  If consent was given and then was removed, it will create a request that will
  clear location information server side.
</p>
<h1 id="remote-config" class="anchor-heading" tabindex="-1">Remote Config</h1>
<p>
  <span>Available in the Enterprise Edition, Remote Config allows you to modify how your app functions or looks by requesting key-value pairs from your Countly server. The returned values may be modified based on the user profile. For more details, please see the </span><a href="https://resources.count.ly/docs/remote-config"><span>Remote Config documentation</span></a><span>.</span>
</p>
<h2 id="manual-remote-config-download" class="anchor-heading">Manual Remote Config</h2>
<p>
  To download Remote Config, call
  <code>Countly.Instance.RemoteConfigs.Update()</code>. After the successful download,
  the SDK stores the updated config locally.
</p>
<pre><strong>await</strong> Countly.Instance.RemoteConfigs.Update();</pre>
<h2 id="h_01HABTZ3164Y5JMBXVP1JCMWNK">Accessing Remote Config Values</h2>
<p>
  To access the stored config, call
  <code>Countly.Instance.RemoteConfigs.Configs</code>. It will return
  <code>null</code> if there isn't any config stored.
</p>
<pre><strong>Dictionary</strong>&lt;string, object&gt; config = Countly.Instance.RemoteConfigs.Configs;</pre>
<p>
  <span>The <code>Dictionary&lt;string, object&gt;</code> returns a value of the type <code>object</code> against a key. The developer then needs to cast it to the appropriate type. </span>
</p>
<h2 id="h_01HABTZ316D1SCDFXWV0VMDARS" class="anchor-heading">Consent</h2>
<p>
  <span>This feature requires<code>RemoteConfig</code> consent. If consent is required and not given, no remote config information will be downloaded and stored.</span>
</p>
<p>
  If consent was given and then is removed, locally stored remote config information
  will be cleared.
</p>
<h1 id="h_01HABTZ3167DDCYDQ3N6QSRZ6D">User Feedback</h1>
<h2 id="h_01HABTZ316A3KZFNEG63TSS6GT">Star Rating Dialog</h2>
<p>
  <span>When a user rates your application, you can report it to the Countly server.</span><span></span>
</p>
<p>
  <span>Example:</span>
</p>
<pre><code><strong>await</strong> countly.StarRating.ReportStarRatingAsync(platform: "android", appVersion: "0.1", rating: 3);</code></pre>
<p>
  <span>All parameters are mandatory.</span>
</p>
<ul>
  <li>
    <span><strong>platform -</strong> (string) the name of the platform.</span>
  </li>
  <li>
    <span><strong>appVersion -</strong> (string) the current version of the app.</span>
  </li>
  <li>
    <span><strong>rating -</strong> (int) v</span><span>alue from 0 to 5 that will be set as the rating value.</span><span></span>
  </li>
</ul>
<h2 id="h_01HABTZ316JXD672PVFWMTVEMP" class="anchor-heading">Consent</h2>
<p>
  If consent is required, recording Star Rating requires<code>StarRating</code><span>consent. If consent is required and not given, recording a Star Rating will not be possible.</span><span></span>
</p>
<h1 id="h_01HABTZ3164RBD3AC31PH330W9">User Profiles</h1>
<p>
  <span>For information about User Profiles, review </span><a href="http://resources.count.ly/docs/user-profiles"><span>this documentation</span></a><span>.</span>
</p>
<p>
  If a property is set as an empty string, it will be deleted from the user on
  the server side.
</p>
<h2 id="h_01HABTZ316D6XXE1MP0RMYV6ZV">Setting Predefined Values</h2>
<p>
  The Countly Unity SDK allows you to upload specific data related to a user to
  the Countly server. You may set the following predefined data for a particular
  user:
</p>
<ul>
  <li>
    <strong>Name</strong>: full name of the user.
  </li>
  <li>
    <strong>Username</strong>: username of the user.
  </li>
  <li>
    <strong>E-mail</strong>: e-mail address of the user.
  </li>
  <li>
    <strong>Organization</strong>: organization the user is working in.
  </li>
  <li>
    <strong>Phone</strong>: phone number.
  </li>
  <li>
    <strong>PictureUrl</strong>: web-based URL for the user’s profile.
  </li>
  <li>
    <strong>Gender</strong>: gender of the user (use only single char like ‘M’
    for Male and ‘F’ for Female).
  </li>
  <li>
    <strong>BirthYear</strong>: birth year of the user.
  </li>
</ul>
<p>
  The SDK allows you to upload user details using the methods listed below.
</p>
<p>Example:</p>
<pre><code>CountlyUserDetailsModel userDetails = <strong>new</strong> CountlyUserDetailsModel(name: "Full Name", username: "username", email: "useremail@email.com", organization: "Organization", phone: "222-222-222", pictureUrl: "http://webresizer.com/images2/bird1_after.jpg", gender: "M", birthYear: "1986", null);
<strong>await</strong> Countly.Instance.UserDetails.SetUserDetailsAsync(userDetails);</code></pre>
<h2 id="h_01HABTZ316PCFDVF0EJGXMABY9">Setting Custom Values</h2>
<p>
  The SDK gives you the flexibility to send only the custom data to Countly servers,
  even when you don’t want to send other user-related data. To achieve this, you
  can generate a custom data segment using a
  <code>Dictionary&lt;string, object&gt;</code>. You can leave all the parameters
  in the constructor as null and simply provide your custom data. This allows you
  to easily send your specific data to Countly servers without unnecessary steps.
</p>
<p>Example:</p>
<pre><code class="!whitespace-pre hljs language-csharp">Dictionary&lt;string, object&gt; userDetails = <strong>new</strong> Dictionary&lt;string, object&gt;();
userDetails.Add("Height", "5.8");
userDetails.Add("Mole", "Lower Left Cheek");
Countly.Instance.UserDetails.SetCustomUserDetails(userDetails);</code></pre>
<h2 id="h_01HABTZ3166RSMTP5JC3Y2PVZC">Setting User Picture</h2>
<p>
  The SDK allows you to set the user's picture URL along with other details using
  the methods listed below.
</p>
<p>Example:</p>
<pre><code>CountlyUserDetailsModel userDetails = <strong>new</strong> CountlyUserDetailsModel(name: "Full Name", username: "username", email: "useremail@email.com", organization: "Organization", phone: "222-222-222", pictureUrl: "http://webresizer.com/images2/bird1_after.jpg", gender: "M", birthYear: "1986", null);
<strong>await</strong> Countly.Instance.UserDetails.SetUserDetailsAsync(userDetails);</code></pre>
<h2 id="h_01HABTZ3160SY1KJCM2G1JPYK0">Modifying Data</h2>
<p>
  <span>You may also manipulate your custom data values in different ways, such as incrementing the current value on a server or storing an array of values under the same property.</span>
</p>
<p>
  <span>You will find the list of available manipulations below:</span>
</p>
<pre><code class="!whitespace-pre hljs language-csharp">//set one custom properties
Countly.Instance.UserDetails.Set("test", "test");

//increment used value by 1
Countly.Instance.UserDetails.Increment("used");

//increment used value by provided value
Countly.Instance.UserDetails.IncrementBy("used", 2);

//multiply value by provided value
Countly.Instance.UserDetails.Multiply("used", 3);

//save maximal value
Countly.Instance.UserDetails.Max("highscore", 300);

//save minimal value
Countly.Instance.UserDetails.Min("best_time", 60);

//set value if it does not exist
Countly.Instance.UserDetails.SetOnce("tag", "test");

//insert value to array of unique values
Countly.Instance.UserDetails.PushUnique("type", new string[] { "morning" });

//insert value to array which can have duplicates
Countly.Instance.UserDetails.Push("type", new string[] { "morning" });

//remove value from array
Countly.Instance.UserDetails.Pull("type", new string[] { "morning" });

//send provided values to server
<strong>await</strong> Countly.Instance.UserDetails.SaveAsync();</code></pre>
<p>
  In the end, always call
  <code><strong>await</strong> <span>Countly.Instance</span>.UserDetails.SaveAsync();</code>
  to send them to the server.
</p>
<p>
  Apart from updating a single property in one request, you can modify multiple
  (unique) properties in one single request. This way you can increment Weight
  and multiply Height in the same request. Similarly, you can record any number
  of modified requests and Save them all together in one single request instead
  of multiple requests.
</p>
<p>
  Note that if you are going to modify multiple properties in one request, make
  sure your properties are unique, i.e. a property shouldn’t be modified more than
  once in a single request. However, if you record a property more than once, only
  the latest value will be posted to the server.
</p>
<p>Example:</p>
<pre><code class="!whitespace-pre hljs language-csharp"><span>Countly.Instance</span>.UserDetails.Max("Weight", 90);
<span>Countly.Instance</span>.UserDetails.SetOnce("Distance", "10KM");
<span>Countly.Instance</span>.UserDetails.Push("Mole", new string[] { "Left Cheek", "Back", "Toe" });
<strong>await</strong> <span>Countly.Instance</span>.UserDetails.SaveAsync();</code></pre>
<h2 id="h_01HABTZ316445B91Y1ZHCS6DGK" class="anchor-heading">Consent</h2>
<p>
  This feature requires<code>User</code><span>consent. If consent is required and not given, recording user profile information will not be possible.</span>
</p>
<h1 id="user-consent-management" class="anchor-heading" tabindex="-1">User Consent</h1>
<p>
  <span>In an effort to comply with GDPR, starting from 20.11.1, Unity Countly SDK provides ways to toggle different Countly features on/off depending on the given consent.</span>
</p>
<p>
  More information about GDPR can be found<span> </span><a href="https://medium.com/countly/countly-the-gdpr-how-worlds-leading-mobile-and-web-analytics-platform-can-help-organizations-5015042fab27">here</a>.
</p>
<h2 id="h_01HABTZ3166JHBX2JCSEG70T78">Setup During Init</h2>
<p>
  <span>The requirement for consent is disabled by default. To enable it, you will have to set <code>RequiresConsent</code></span><span> value <code>true</code> before initializing Countly.</span>
</p>
<pre><code>CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .EnableLogging()
  .SetNotificationMode(TestMode.AndroidTestToken)
  .SetRequiresConsent(true);
  
Countly.Instance.Init(configuration);</code></pre>
<p>
  <span>By default, when consent is required, no consent is given. If no consent is given, SDK will not work and no network requests related to its features will be sent. When the consent status of a feature is changed, that change will be sent to the Countly server.</span>
</p>
<p>
  <span>Set consent is not persistent and will have to be set each time before Countly init. Therefore, the storage and persistence of the given consent fall on the SDK integrator.</span>
</p>
<p>
  <span>Consent for features may be given and revoked at any time, but if it is given after Countly init, some features may only work in part.</span>
</p>
<p>
  <span>Feature names in the <strong>Unity SDK,</strong> are stored as <strong>Enum</strong> called <code>Consents</code></span><span>.</span>
</p>
<p>The current features are:</p>
<ul>
  <li>
    <code>Sessions</code> - tracking when, how often, and how long users use
    your app
  </li>
  <li>
    <code>Events</code> - allow sending events to the server
  </li>
  <li>
    <code>Views</code> - allow the tracking of which views users visit
  </li>
  <li>
    <code>Location</code> - allow the sending of location information
  </li>
  <li>
    <code>Crashes</code> - allow the tracking of crashes, exceptions, and errors
  </li>
  <li>
    <code>Users</code> - allow the collecting/providing of user information,
    including custom properties
  </li>
  <li>
    <code>Push</code> - allow push notifications
  </li>
  <li>
    <code>StarRating</code> - allow their rating and feedback to be sent
  </li>
  <li>
    <code>RemoteConfig</code> - allow downloading remote config values from your
    server
  </li>
</ul>
<p>
  In case consent is required, you may give consent to features before the SDK
  Init call. These features consents are not persistent and must be given on every
  restart.
</p>
<pre><code class="!whitespace-pre hljs language-csharp">// prepare consents that should be given
Consents[] consents = new Consents[] { Consents.Users, Consents.Location };

// give consents to the features
configuration.GiveConsent(consents);</code></pre>
<h2 id="changing-consent" class="anchor-heading">Changing Consent</h2>
<p>
  After init call, use <code class="!csharp">Countly.Instance.Consents.</code>
  to change consent.
</p>
<p>
  <span>There are 2 ways of changing feature consent: </span>
</p>
<ul>
  <li>
    <span> <code>GiveConsent</code>/<code>RemoveConsent</code></span><span> - gives or removes consent to a specific feature.</span>
  </li>
</ul>
<pre><code class="!whitespace-pre hljs language-csharp">// give consent to "sessions" feature
Countly.Instance.Consents.GiveConsent(new Consents[] { Consents.Sessions });

// remove consent from "sessions" feature
Countly.Instance.Consents.RemoveConsent(new Consents[] { Consents.Sessions });</code></pre>
<ul>
  <li>
    <code>GiveConsentAll</code> / <code>RemoveAllConsent</code>-
    <span>gives or removes</span> all consents.
  </li>
</ul>
<pre><code class="!whitespace-pre hljs language-csharp">// give consent to all features
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
<pre><code class="!whitespace-pre hljs language-csharp">// prepare consents that should be added to the group 
Consents[] consents = <strong>new</strong> Consents[] { Consents.Users, Consents.Location };

// create the Consent group
configuration.CreateConsentGroup("User-Consents", consents);

// give consent to the provide consent group
configuration.GiveConsentToGroup("User-Consents");</code></pre>
<p>
  After init has been called, use <code>GiveConsentToGroup</code> /
  <code>RemoveConsentOfGroup</code> to <span>give or remove </span>consent for
  a feature group.
</p>
<p>Example:</p>
<pre><code class="!whitespace-pre hljs language-csharp">// prepare array of groups 
string[] groupName = new string[] { "User-Consents", "Events-Consents" };

// give consent to groups
Countly.Instance.Consent.GiveConsentToGroup(groupName);

// remove consent of groups
Countly.Instance.Consent.RemoveConsentOfGroup(groupName);</code></pre>
<h1 id="h_01HABTZ316AYQFEVA6BEXF711V">Security and Privacy</h1>
<h2 id="parameter-tampering-protection" class="anchor-heading">Parameter Tamper Protection</h2>
<p>
  <span>You may set the optional <code>salt</code></span><span> to be used for calculating the checksum of requested data which will be sent with each request, using the <code>&amp;checksum</code> field. You will need to set exactly the same <code>salt</code> on the Countly server. If the <code>salt</code> on the Countly server is set, all requests would be checked for the validity of the <code>&amp;checksum</code> field before being processed. </span>
</p>
<pre><code class="!whitespace-pre hljs language-csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetParameterTamperingProtectionSalt("Salt");</code></pre>
<h1 id="h_01HABTZ317YY21TT4G68H4VJM4">Other Features</h1>
<h2 id="h_01HCHSPK9JJC6GC35NHZJQ4F4Y">SDK Config Parameters Explained</h2>
<p>
  <span>To change the Configuration, update the values of parameters in the "<strong>CountlyConfiguration" </strong>object. These are the methods that lets you set values in your "<strong>CountlyConfiguration</strong>" object:</span><span></span>
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
  Reporting. When<span> </span><strong>enabled</strong>, the SDK will catch exceptions
  and automatically report them to the Countly server. It's enabled by default.
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
  <span>In case you would like to check if init has been called, you may use the following property:</span>
</p>
<pre><code class="!whitespace-pre hljs language-csharp">Countly.Instance.IsSDKInitialized;</code></pre>
<h2 id="sdk-internal-limits" class="anchor-heading">SDK Internal Limits</h2>
<p>
  SDK does have configurable fields to manipulate the internal SDK value and key
  limits. If values or keys provided by the user, would exceed the limits, they
  would be truncated. These are the methods that let's you set limits. For further
  details please have a look
  <a href="/hc/en-us/articles/9290669873305#sdk_internal_limits">here</a>.<span></span>
</p>
<h3 id="h_01HRYHGASG78HB8NM4T64KZ0NS">Key Length</h3>
<p>
  <span><strong>SetMaxKeyLength(int length) - </strong>maximum size of all string keys. The default value is <strong>128</strong>.</span>
</p>
<pre><code class="csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetMaxKeyLength(120);</code></pre>
<h3 id="h_01HRYHGASG1C44VHKRAHNTW0HR">Value Size</h3>
<p>
  <span><strong>SetMaxValueSize(int size) - </strong>maximum size of all values in our key-value pairs. The default value is <strong>256</strong>.</span>
</p>
<pre><code class="csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetMaxValueSize(240);</code></pre>
<h3 id="h_01HRYHGASG9DBJF5KNRT0JWQ55">Segmentation Values</h3>
<p>
  <span><strong>SetMaxSegmentationValues(int values) - </strong>maximum amount of custom (dev provided) segmentation in one event. The default value is <strong>100</strong>.</span>
</p>
<pre><code class="csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetMaxSegmentationValues(35);</code></pre>
<h3 id="h_01HRYHGASHPHPEZ3RB698QQ73W">Breadcrumb Count</h3>
<p>
  <strong>SetMaxBreadcrumbCount(int amount) </strong>- maximum amount of breadcrumbs.
  The default value is <strong>100</strong>.
</p>
<pre><code class="csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetMaxBreadcrumbCount(101);</code></pre>
<h3 id="h_01HRYHGASH3B0YQRS1065R5BHW">Stack Trace Lines Per Thread</h3>
<p>
  <span><strong>SetMaxStackTraceLinesPerThread(int lines) - </strong>limits how many stack trace lines would be recorded per thread. The default value is <strong>30</strong>.</span>
</p>
<pre><code class="csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetMaxStackTraceLinesPerThread(32);</code></pre>
<h3 id="h_01HRYHGASH45K0F6KWG2B8RY0X">Stack Trace Line Length</h3>
<p>
  <span><strong>SetMaxStackTraceLineLength(int length) - </strong>limits how many characters are allowed per stack trace line. The default value is <strong>200</strong>.</span>
</p>
<pre><code class="csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
  .SetMaxStackTraceLineLength(230);</code></pre>
<h2 id="01HFEMPN4D6V1PJ7R9WC6WZ17H">Custom Metrics</h2>
<p>
  In certain situations, such as beginning a session or requesting remote config,
  the SDK sends device metrics. You have the flexibility to override the sent metrics,
  such as the operating system for a specific variant, or to provide your own custom
  metrics by using <code>SetMetricOverride</code>.
</p>
<p>Example:</p>
<pre><code class="!whitespace-pre hljs language-csharp">// overriding default metrics
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
<pre><code class="!whitespace-pre hljs language-csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
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
<pre><code class="!whitespace-pre hljs language-csharp">CountlyConfiguration configuration = new CountlyConfiguration(appKey, serverUrl)
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
  <li>
    When generating a device ID, if no custom ID is provided, the SDK will use:
    <ul>
      <li>Android: md5 of ANDROID_ID</li>
      <li>iOS: It will be vendor id and advertising id as a fallback</li>
      <li>Windows Store Apps: It will be advertising id</li>
      <li>
        Windows Standalone: It will be hash from the concatenation of strings
        taken from computer system hardware classes.
      </li>
    </ul>
  </li>
</ul>