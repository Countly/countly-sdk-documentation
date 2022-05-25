<p>
  This document explains how to download, setup, and use the Unity SDK for Countly.
  You can download the latest release from
  <a href="https://github.com/Countly/countly-sdk-unity/releases/" target="_self" rel="undefined">Github</a>.&nbsp;
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <span class="wysiwyg-font-size-large"><strong>Older documentation</strong></span>
  </p>
  <p>
    To access the documentation for version 20.11.5 and older, click
    <a href="https://support.count.ly/hc/en-us/articles/4410908291737" target="_self" rel="undefined">here.</a>
  </p>
</div>
<p>
  The following are some of the key assumptions being considered while developing
  the SDK. Please take into account the following <strong>before</strong> integrating
  this SDK:
</p>
<ol>
  <li>Scripting version is based on .NET 4.x equivalent</li>
  <li>API Compatibility Level is based on .NET 4.x equivalent</li>
  <li>
    SDK is tested on IOS, Android, Windows, UWP, Linux and Mac OSX
  </li>
</ol>
<p>
  To look at our sample application, download the sample project from
  <a href="http://github.com/countly/countly-sdk-unity" target="_self" rel="undefined">Github repo</a>
  and open the 'EntryPoint.unity' scene. 'EntryPoint.unity' located in 'Example'
  folder under Assest. There is also 'CountlyEntryPoint.cs' script in Example folder,
  and this script shows how most of the functionality can be used.
</p>
<h1>Adding the SDK to the project</h1>
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
  <img src="/hc/article_attachments/4404570305433/Screenshot_2021-03-09_at_6.02.04_PM.png" alt="Screenshot_2021-03-09_at_6.02.04_PM.png" width="435" height="719">
</p>
<p>
  <span data-preserver-spaces="true">This SDK uses the </span><strong><span data-preserver-spaces="true">Newtonsoft Json</span></strong><span data-preserver-spaces="true"> package internally and it is required for the SDK to work. </span>
</p>
<p>
  <span data-preserver-spaces="true">Since Unity version 2020 this package is added to your project automatically by Unity. For versions before that (2018 and 2019) you would have to install this package in the project manually. </span>
</p>
<p>
  <span data-preserver-spaces="true">One way to do Install the </span><strong><span data-preserver-spaces="true">Newtonsoft Json&nbsp;</span></strong><span data-preserver-spaces="true">package would be to use the built-in package manager. You would go to </span><strong><span data-preserver-spaces="true">Windows&nbsp;</span></strong><span data-preserver-spaces="true">=&gt;&nbsp;</span><strong><span data-preserver-spaces="true">Package Manager</span></strong><span data-preserver-spaces="true">. In there you would see something like this:<img src="/hc/article_attachments/6537960964505/image-newtonsoft.png" alt="image-newtonsoft.png"></span>
</p>
<h1>SDK Integration</h1>
<h2>Minimal Setup</h2>
<p>
  Before you can use any functionality, you have to initiate the SDK.&nbsp;
</p>
<p>
  The shortest way to initiate the SDK is with this code snippet:
</p>
<pre>CountlyConfiguration config = <strong>new</strong> CountlyConfiguration<br>{<br><strong>AppKey</strong> = <span>COUNTLY_APP_KEY,</span><br><strong>ServerUrl</strong> = <span>COUNTLY_SERVER_URL</span>,<br>};<br><br>Countly.Instance.Init(config);</pre>
<p>
  <span><strong>AppKey - </strong>(Mandatory) The “App Key” for the app that you created on the Countly server. Example<strong>:</strong>&nbsp;124qw3er5u678qwef88d6123456789qwertyui123.</span>
</p>
<p>
  <span><strong>ServerUrl -</strong> (Mandatory) The URL of the Countly server where you are going to post your requests. Example<strong>:</strong>&nbsp;<a href="https://us-try.count.ly/">https://try.count.ly/</a></span>
</p>
<p>
  To configure the SDK during init, a config object called "<strong>CountlyConfiguration</strong>"
  is used. The configuration is done by creating such an object. Afterward that
  config object is provided to the "Init" method.
</p>
<h3 id="providing-the-application-key" class="anchor-heading">Providing the application key</h3>
<p>
  <span>Also called "AppKey" as shorthand. The application key is used to identify for which application this information is tracked. You receive this value by creating a new application in your Countly dashboard and accessing it in its application management screen.</span>
</p>
<p>
  <span><strong>Note:&nbsp;</strong>Ensure you are using the App Key (found under Management -&gt; Applications) and not the API Key. Entering the API Key will not work.</span>
</p>
<h3 id="providing-the-server-url" class="anchor-heading">Providing the server URL</h3>
<p>
  <span>If you are using Countly Enterprise Edition trial servers, use&nbsp;<code>https://try.count.ly</code>,&nbsp;<code>https://us-try.count.ly</code>&nbsp;or&nbsp;<code>https://asia-try.count.ly</code>&nbsp;It is basically the domain from which you are accessing your trial dashboard.</span>
</p>
<p>
  <span>If you use both Community Edition and Enterprise Edition, use your own domain name or IP address, such as&nbsp;</span><a href="https://example.com/"><span>https://example.com</span></a><span>&nbsp;or&nbsp;</span><a href="https://ip/"><span>https://IP</span></a><span>&nbsp;(if SSL has been set up).</span>
</p>
<h2 id="enabling-logging" class="anchor-heading">SDK logging / debug mode</h2>
<p>
  <span>The first thing you should do while integrating our SDK is enabling logging. If logging is enabled, then our SDK will print out debug messages about its internal state and encountered problems.&nbsp;</span>
</p>
<p>
  Set <code>EnableConsoleLogging</code> on the config object to enable logging:
</p>
<pre>CountlyConfiguration config = new CountlyConfiguration<br>{<br>AppKey = <span>COUNTLY_APP_KEY,</span><br>ServerUrl = <span>COUNTLY_SERVER_URL</span>,<br>EnableConsoleLogging = true<br>};</pre>
<h2 id="device-id" class="anchor-heading">Device ID</h2>
<p>
  <span>All tracked information is tied to a "device ID". A device ID is a unique identifier for your users.</span>
</p>
<p>
  <span>You may specify the device ID by yourself if you have one (it has to be unique for each of your users). It may be an email or some other internal ID used by your other systems.</span>
</p>
<pre>CountlyConfiguration config = <strong>new</strong> CountlyConfiguration<br>{<br>AppKey = <span>COUNTLY_APP_KEY,</span><br>ServerUrl = <span>COUNTLY_SERVER_URL</span>,<br>EnableConsoleLogging = true,<br>DeviceId = UNIQUE_DEVICE_ID<br>};<br><br>Countly.Instance.Init(config);</pre>
<p>
  <span>You may let Countly SDK handles the initial device ID on its own. Then if in the future you can change this ID with an appropriate call. Then you would use the following config:</span>
</p>
<pre>CountlyConfiguration config = <strong>new</strong> CountlyConfiguration<br>{<br>AppKey = <span>COUNTLY_APP_KEY,</span><br>ServerUrl = <span>COUNTLY_SERVER_URL</span>,<br>EnableConsoleLogging = true<br>};<br><br>Countly.Instance.Init(config);</pre>
<h2 class="anchor-heading">SDK data storage</h2>
<p>
  Countly SDK s<span>tore data that are meant for your app's use only, within an internal storage volume. If your game saves in external storage, SDK will store data within external storage. You may need to add permission to store data on an SD card. Please read the </span><a href="#require-app-permissions" target="_self" rel="undefined">Required app permissions</a>
  section for more information.
</p>
<p>
  SDK uses Preferences to keep track of application and user preferences and s<span>tore private, primitive data in key-value pairs. </span>Operational
  data is stored in<span><a href="https://www.iboxdb.com/" target="_self"> iBoxDB</a> database file, named 'db3.box'.&nbsp;<br></span>
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
      <span><strong>Android:&nbsp;</strong>'/storage/emulated/0/Android/data/ly.count.demo/files/db3.box'</span>
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
<h2 id="require-app-permissions" class="anchor-heading">Required app permissions</h2>
<p>
  If you expect the game to be saved
  <span>on an SD card or any other type of external storage</span>, set
  <strong>Write Permission</strong><span>&nbsp;</span><span>to 'External (SDCard). This can be found in your Android platform settings under 'Other Settings'.</span>
</p>
<p>
  <span class="c-message_attachment__text" data-qa="message_attachment_text"><span dir="auto">When configuring your app, make sure that it has permission to access the internet.</span></span>
</p>
<h2 class="c-message_attachment__row">SDK notes</h2>
<p>
  To access the Countly Global Instance use the following code snippet:
</p>
<pre>Countly.Instance.</pre>
<h1 class="anchor-heading" tabindex="-1">Crash reporting</h1>
<p>
  <span>The Countly SDK for Unity can collect </span><a href="http://resources.count.ly/docs/introduction-to-crash-reporting-and-analytics"><span>Crash Reports</span></a><span>,</span><span>&nbsp;which you may examine and resolve later on the server.</span>
</p>
<p>
  In the SDK all crash-related functionalities can be browsed from the returned
  interface on:
</p>
<pre>countly.CrashReports.</pre>
<h2>Automatic crash handling</h2>
<p>
  The Unity SDK can automatically report uncaught exceptions/crashes in the application
  to the Countly server. To report uncaught exceptions/crashes automatically, enable
  <strong>enableAutomaticCrashReporting<span>&nbsp;</span></strong><span>in the SDK configuration.</span>
</p>
<h2 class="anchor-heading">Handled exceptions</h2>
<p>
  <span>You might catch an exception or similar error during your app’s runtime.</span><span>You may also log these handled exceptions to monitor how and when they are happening. </span>To
  log exception use the following code snippet:
</p>
<pre><strong>await</strong> countly.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, LogType.Exception, null, false); </pre>
<p>Here is the detail of the parameters:</p>
<ul>
  <li>
    <strong>message -</strong> (<span>Mandatory</span>, string) a string that
    contains a detailed description of the exception.
  </li>
  <li>
    <strong>stackTrace -</strong> (<span>Mandatory, </span>string) A string that
    describes the contents of the call stack.
  </li>
  <li>
    <strong>type - </strong>(<span>Mandatory, </span>LogType) The type of the
    log message.
  </li>
  <li>
    <strong>segments - </strong>(Optional, ) Custom key/values to be reported.
  </li>
  <li>
    <strong>nonfatal -</strong>&nbsp; (Optional, bool) Set false if the error
    is fatal.
  </li>
</ul>
<p>Example:</p>
<pre><strong>try</strong><br> {<br><strong>    throw</strong> <strong>new</strong> DivideByZeroException();<br> }<br> <strong>catch</strong> (Exception ex)<br> {<br>    <strong>await</strong> countly.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, LogType.Exception); <br> }&nbsp;<br><br></pre>
<p class="anchor-heading">You can also send a segmentation with an exception.</p>
<pre><span><br>Dictionary&lt;string, object&gt; segmentation = <strong>new</strong> Dictionary&lt;string, object&gt;{<br>{ "Action", "click"}<br>};<br><strong><br>try</strong><br>{<br><strong> throw</strong> <strong>new</strong> DivideByZeroException();<br>}<br><strong>catch</strong> (Exception ex)<br>{<br><strong>await</strong> countly.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, LogType.Exception, segmentation, true); <br>}&nbsp;</span></pre>
<p>
  <span>If you have handled an exception and it turns out to be fatal to your app, you may use the following calls:</span>
</p>
<pre><strong>await</strong> countly.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, LogType.Exception, null, false); </pre>
<pre>Dictionary&lt;string, object&gt; segmentation = <strong>new</strong> Dictionary&lt;string, object&gt;{<br>{ "Action", "click"}<br>};<br><br><strong>await</strong> countly.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, LogType.Exception, segmentation, false); </pre>
<h2 class="anchor-heading">Crash breadcrumbs</h2>
<p>
  Throughout your app, you can leave crash breadcrumbs. They are shory logs<span>&nbsp;that </span>would
  describe the previous steps that were taken in your app before the crash. After
  a crash happens, they will be sent together with the crash report.
</p>
<p>The following command adds a crash breadcrumb:</p>
<pre>countly.CrashReports.AddBreadcrumbs("breadcrumb");</pre>
<h2 class="anchor-heading">Consent</h2>
<p>
  This feature uses <code>Crashes</code><span> consent. No additinal crash logs will be recorded if consent is required and not given.</span>
</p>
<h1>Events</h1>
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
<pre>countly.Events.</pre>
<p>
  <span>There are a couple of values that can be set when recording an event. The main one is the <strong>key</strong> property which would be the identifier/name for that event.&nbsp; For example, in case a user purchased an item in a game, you could create an event with the key 'purchase'.</span>
</p>
<p>
  <span>Optionally there are also other properties that you might want to set:</span>
</p>
<ul>
  <li>
    <strong>count -</strong>&nbsp; a whole numerical value that marks how many
    times this event has happened. The default value for that is
    <strong>1</strong>.
  </li>
  <li>
    <strong>sum -</strong> This value would be summed across all events in the
    dashboard. F<span>or example, in-app purchase events sum of purchased items. Its default value is <strong>0</strong>.</span>
  </li>
  <li>
    <strong>duration - </strong>Used to record and track the duration of events.
    The default value is <strong>0</strong>.
  </li>
  <li>
    <strong>segments - </strong>A value where you can provide custom segmentation
    for your events to track additional information. It is a key and value map.
    The accepted data types for the value are
    <span style="font-weight: 400;">"String", "Integer", "Double", and "Boolean". All other types will be ignored.</span>
  </li>
</ul>
<h2>Recording events</h2>
<p>
  <span>Here is a quick way to </span><span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">record an event:</span>
</p>
<pre><strong>public</strong> async Task ReportCustomEventAsync(string key, IDictionary&lt;string, object&gt; segmentation = null, int? count = 1, double? sum = null, double? duration = null)</pre>
<p>
  <span style="font-weight: 400;">Based on the example below of an event recording a <strong>purchase</strong>, h</span><span style="font-weight: 400;">ere is a quick summary of the information for each usage:</span>
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
    <span style="font-weight: 400;">the total amount, both of which are also available, segmented by countries and application versions + the total duration of those events.</span>
  </li>
</ul>
<p>
  <strong>1. Event key and count</strong>
</p>
<pre><code class="java"><strong>await</strong> countly.Events.ReportCustomEventAsync("purchase", count: 1);</code></pre>
<p>
  <strong>2. Event key, count, and sum</strong>
</p>
<pre><code class="java"><strong>await</strong> countly.Events.ReportCustomEventAsync(key: "purchase", count: 1, sum: 0.99);</code></pre>
<p>
  <strong>3. Event key and count with segmentation(s)</strong>
</p>
<pre><code class="java">Dictionary&lt;string, object&gt; segmentation = new Dictionary&lt;string, object&gt;<br>{<br>{ "country", "Germany" },<br>{ "app_version", "1.0" }<br>};

<strong>await</strong> countly.Events.ReportCustomEventAsync(key: "<span>purchase</span>", segmentation: segmentation, count: 1);<br></code></pre>
<p>
  <strong>4. Event key, count, and sum with segmentation(s)</strong>
</p>
<pre><code class="java">Dictionary&lt;string, object&gt; segmentation = new Dictionary&lt;string, object&gt;<br>{<br>{ "country", "Germany" },<br>{ "app_version", "1.0" }<br>};

<strong>await</strong> countly.Events.ReportCustomEventAsync(key: "<span>purchase</span>", segmentation: segmentation, count: 1, sum: 0.99);</code></pre>
<p>
  <strong>5. Event key, count, sum, and duration with segmentation(s)</strong>
</p>
<pre><code class="java">Dictionary&lt;string, object&gt; segmentation = new Dictionary&lt;string, object&gt;<br>{<br>{ "country", "Germany" },<br>{ "app_version", "1.0" }<br>};

<strong>await</strong> countly.Events.ReportCustomEventAsync(key: "<span>purchase</span>", segmentation: segmentation, count: 1, sum: 0.99, duration: 60);<br></code></pre>
<p>
  <span style="font-weight: 400;">These are only a few examples of what you can do with Events. You may go beyond those examples and use country, app_version, game_level, time_of_day, and any other segmentation of your choice that will provide you with valuable insights.</span>
</p>
<h2>Timed events</h2>
<p>
  <span style="font-weight: 400;">Currently, SDK doesn't have any direct mechanism to record timed Events. To record a timed event, you would have to calculate the duration of an event yourself. You could record the timestamp at the start of it and at the end, and then you would pass the calculated duration to Countly when you are recording the event.</span>
</p>
<p>
  <span style="font-weight: 400;">Example:</span>
</p>
<pre><code class="java">//At the start of your planned event you would record the start timestamp
DateTime startTime = DateTime.UtcNow;
...
//Some time would pass and you would determine that your planned event has ended and you would record how many seconds passed 
double duration = (DateTime.UtcNow - startTime).TotalSeconds; 
//Then you would pass this information when recording a Countly event
<strong>await</strong> countly.Events.ReportCustomEventAsync(key: "<span>music</span>", duration: duration);</code></pre>
<p>
  <span>You may provide segmentation, count, and sum while recording a timed event.</span>
</p>
<h2 class="anchor-heading">Consent</h2>
<p>
  <span>This feature uses <code>Events</code> consent. </span><span>No additional events will be recorded if consent is required and not given.</span>
</p>
<p>
  <span>When consent is removed, all previously started timed events will be cancelled.</span>
</p>
<h1>Sessions</h1>
<h2>
  <span style="font-weight: 400;">Automatic session tracking&nbsp;</span>
</h2>
<p>
  The Unity SDK handles the session automatically. After calling the
  <strong>Init</strong> method, the SDK starts the session automatically and extending
  the session after every 60 seconds. This value is configurable during initialization.
  It cannot be modified after initialization.
</p>
<p>
  The SDK ends the current session whenever the user quits the app or app goes
  into the background. A session would be started again when the app comes to the
  foreground.
</p>
<h3>
  <span style="font-weight: 400;">Disable automatic session tracking&nbsp;</span>
</h3>
<p>
  <span>You might want to disable automatic session tracking. To do so, use the following code snippet before</span><span> init call.<br></span>
</p>
<pre>config.DisableAutomaticSessionTracking();</pre>
<p>
  Note that after disabling session tracking, the following things would happen:
</p>
<ul>
  <li class="p-rich_text_section">Session information would not be recorded&nbsp;</li>
  <li class="p-rich_text_section">Device metrics would not be recorded</li>
  <li class="p-rich_text_section">
    On dashboard location map would not be updated and, overview and analytics
    session related to sessions and users would all be empty
  </li>
</ul>
<h2 class="anchor-heading">Consent</h2>
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
<h1>View tracking</h1>
<h2>Manual view recording</h2>
<p>
  The Countly Unity SDK supports manual view (screen) tracking. With this feature,
  you can report what views a user did and for how long. Thus, whenever there is
  a screen switch in your app, you can report it to the Countly server by using
  the following method:
</p>
<pre><strong>await</strong> countly.Views.RecordOpenViewAsync("Home Scene");</pre>
<p>
  <br>
  When the screen closes you can report it to the server by using the following
  method:
</p>
<pre><strong>await</strong> countly.Views.RecordCloseViewAsync("Home Scene");</pre>
<h2 class="anchor-heading">Consent</h2>
<p>
  <span>This feature requires<code>Views</code> consent. No additional views will be recorded if consent is required and not given.</span>
</p>
<h1 class="anchor-heading" tabindex="-1">Device ID management</h1>
<p>
  <span>A device ID is a unique identifier for your users. </span><span>You may specify the device ID yourself or allow the SDK to generate it. When providing one yourself, keep in mind that it has to be unique for all users. Some potential sources for such an id may be the users username, email or some other internal ID used by your other systems.</span>
</p>
<h2>Device ID generation</h2>
<p>
  <span>If no device ID is provided the first time the SDK is initialised, the SDK will generate a unique device ID. The source of that id is</span><span><code class="java">SystemInfo.deviceUniqueIdentifier</code>which is a value exposed by Unity. It should be unique for every device.</span>
</p>
<p>
  <span>Here are the underlying mechanisms used to generate that value for some platforms:</span>
</p>
<p>
  <span><strong>IOS:</strong> on pre-iOS7 devices, it will return a hash of the MAC address. On iOS7 devices, it will be</span>
</p>
<p>
  <span><code class="java">UIDevice identifierForVendor</code> or, if that fails for any reason,</span>
</p>
<p>
  <span><code class="java">ASIdentifierManager advertisingIdentifier</code></span>
</p>
<p>
  <span>&nbsp;<strong>Android: </strong><code class="java">SystemInfo.deviceUniqueIdentifier</code>&nbsp;returns the md5 of ANDROID_ID.<br>Note that since Android 8.0 (API level 26) ANDROID_ID depends on the app signing key. That means "unsigned" builds (which are by default signed with a debug keystore) will have a&nbsp;different value&nbsp;than signed builds (which are signed with a key provided in the player settings).&nbsp;</span>
</p>
<p>
  <span><strong>Windows Store Apps:</strong> uses <code class="java">AdvertisingManager::AdvertisingId</code>for returning unique device identifiers.</span>
</p>
<p>
  <span><strong>Windows Standalone</strong>: returns a hash from the concatenation of strings taken from Computer System Hardware Classes.<br>For more information, <a href="https://docs.unity3d.com/ScriptReference/SystemInfo-deviceUniqueIdentifier.html" target="_self">click here</a>.</span><span></span>
</p>
<h2>Changing device ID</h2>
<p>
  The SDK allows you to change the Device ID at any point in time. You can use
  any of the following two methods to changing the Device ID, depending on your
  needs.
</p>
<p class="anchor-heading">
  <strong>Changing Device ID with server merge</strong>
</p>
<p>
  <span>In case your application authenticates users, you might want to change the ID to the one in your backend after he has logged in. This helps you identify a specific user with a specific ID on a device he logs in, and the same scenario can also be used in cases this user logs in using a different way (e.g another tablet, another mobile phone, or web). In this case, any data stored in your Countly server database associated with the current device ID will be transferred (merged) into the user profile with the device id you specified in the following method call:</span>
</p>
<pre><strong>await</strong> countly.Device.ChangeDeviceIdAndMergeSessionDataAsync("New Device Id");</pre>
<p class="anchor-heading">
  <strong>Changing Device ID without server merge</strong>
</p>
<p>
  <span>You might want to track information about another separate user that starts using your app (changing apps account), or your app enters a state where you no longer can verify the identity of the current user (user logs out). In that case, you can change the current device ID to a new one without merging their data. You would call:</span>
</p>
<pre><strong>await</strong> countly.Device.ChangeDeviceIDAndEndCurrentSessionAsync("New Device Id");</pre>
<p>
  <span>Doing it this way, will not merge the previously acquired data with the new id.</span>
</p>
<div class="callout callout--warning">
  <p>
    <span style="font-weight: 400;">If device ID is changed without merging and consent was enabled, all previously given consent will be removed. This means that all features will cease to function until new consent has been given again for that new device ID.</span>
  </p>
</div>
<p>
  <span>Do note that every time you change your deviceId without a merge, it will be interpreted as a new user. Therefore implementing id management in a bad way could inflate the users count by quite a lot.<br></span>
</p>
<h2 class="anchor-heading">Retrieving current device ID&nbsp;</h2>
<p>
  You may want to see what device id Countly is assigning for the specific device.
  For that, you may use the following calls.&nbsp;
</p>
<pre><code class="java hljs">string usedId = Countly.Instance.Device.DeviceId;</code></pre>
<p>
  <span>You can get the current device ID type. The id type is an enum with the possible values of:</span>
</p>
<ul>
  <li>
    <span><code class="java hljs">SystemGenerated</code> - device ID generated by the SDK</span>
  </li>
  <li>
    <span><code class="java hljs">DeveloperProvided</code> - device ID provided by the host app</span><span></span>
  </li>
</ul>
<pre><code class="java hljs">DeviceIdType type = Countly.Instance.Device.DeviceIdType;</code></pre>
<h2 class="anchor-heading">Consent</h2>
<p>No consent is required to change device ID.</p>
<p>
  If device ID is changed without merging and consent was enabled, all previously
  given consent will be removed. This means that all features will cease to function
  until new consent has been given again for that new device ID.
</p>
<h1>Push notifications</h1>
<p>
  <span>The Unity SKD uses FCM and APNs as push notification providers for Android and iOS platforms respectively, and it doesn't support the Huawei Push Kit push service.<br></span>
</p>
<p>
  <span>By default, FCM and APNs dependencies are added as part of the SDK. They can be removed in case you don't need them.</span><span></span>
</p>
<p>
  <span>Note that SDK doesn't support Deep linking, </span><span>Data only push, and </span><span>Rich push notifications yet. You can send text push notifications only.</span>
</p>
<h2>Integration</h2>
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
  The Countly server needs the APNs Auth Key&nbsp;to send notifications. To get
  the APNs Auth Key&nbsp;and upload it to the County Server, for further information
  refer to
  <a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#setting-up-apns-authentication" target="_self">iOS Documentation.</a>
</p>
<p>To set up push for iOS, follow the next two steps:</p>
<p>
  1. In Unity, go to <strong>Player Settings.&nbsp;</strong>In the
  <strong>Other Settings</strong> section, add the
  <span><strong>"COUNTLY_ENABLE_IOS_PUSH"&nbsp; </strong>symbol in </span><strong>Scripting Define Symbols.</strong><strong><img src="/hc/article_attachments/900004317706/Screenshot_2020-10-27_at_4.07.16_PM.png" alt="Screenshot_2020-10-27_at_4.07.16_PM.png"></strong>
</p>
<p>
  2. After exporting the <strong>iOS</strong> project, open the project in
  <strong>Xcode</strong>, and add <strong>Push Notifications</strong> Capability.
  For further information regarding iOS app configuring refer to
  <a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#configuring-ios-app" target="_self" rel="undefined">iOS Documentation.</a>
</p>
<h2>
  <span>Enabling push</span>
</h2>
<p>
  <span>By default Push Notifications are disabled. To enable push, set Notification mode other than <code>None</code> in the Configuration before SDK init call.<br></span>
</p>
<p>
  <span>Example:</span>
</p>
<pre><span>CountlyConfiguration config = new CountlyConfiguration<br>{<br>AppKey = COUNTLY_APP_KEY,<br>ServerUrl = COUNTLY_SERVER_URL,<br>EnableConsoleLogging = true,<br>NotificationMode = TestMode.AndroidTestToken<br>};<br></span></pre>
<p>
  <span> Here is an overview of notification modes:</span>
</p>
<ul>
  <li>
    <span><code>None</code>- it is the default value of notification mode. This mode disables the notification feature.</span>
  </li>
  <li>
    <span><code>AndroidTestToken</code> / <code>iOSTestToken</code>- during development build, use <code>AndroidTestToken</code>&nbsp;and <code>iOSTestToken</code>&nbsp;modes for Android and iOS platforms respectively.</span>
  </li>
  <li>
    <span><code>iOSAdHocToken</code> - use this for distribution of iOS builds on TestFlight and AdHoc.</span>
  </li>
  <li>
    <span><code>ProductionToken</code> - use this mode for the production builds.</span><span></span>
  </li>
</ul>
<h2>Removing push and its dependencies</h2>
<p>
  <span>By default, push dependencies are part of the SDK. You may remove them, and add them back after removing them.<br>Don't forget to change notification mode to <code>None</code>, after removing push notification dependencies from SDK.<br></span>
</p>
<p>
  <strong><span class="wysiwyg-font-size-large">Android</span></strong><span></span>
</p>
<p>
  <span>To remove FCM dependencies from the android build, go to the <strong>Assets\Plugins\Android </strong>folder and delete the <strong>Notifications</strong> folder.</span>
</p>
<p>
  <span>To</span>&nbsp;add them back after removing<span>, re-import the Unity package.</span><span></span>
</p>
<p>
  <span class="wysiwyg-font-size-large"><strong>IOS</strong></span>
</p>
<p>
  <span>The <strong>APN's</strong> dependencies are part of the <strong>SDK.</strong> To remove the <strong>APNs</strong> dependencies, go to the <strong>Assets\Plugins </strong>folder and delete the <strong>iOS</strong> folder. Remove the <strong>"COUNTLY_ENABLE_IOS_PUSH"</strong> symbol from <strong>Scripting Define Symbols </strong>in <strong>Player Settings.</strong></span>
</p>
<p>
  <span>To</span>&nbsp;add them back after removing<span>, re-import the Unity package and add back the <strong>"COUNTLY_ENABLE_IOS_PUSH"</strong> symbol.</span>
</p>
<h2>
  <span>Customizing push messages</span>
</h2>
<p>
  <strong><span class="wysiwyg-font-size-large">Android</span></strong>
</p>
<p>
  <span>To change the sound and icons of the android notifications, update the sound and icons in the folder Assets/Plugins/Android/Notifications/res.&nbsp;</span>
</p>
<p>
  <span><strong>Note</strong>: The Notification channel name and description can be updated through the <strong>strings.xml</strong> file located in the <strong>Assets\Plugins\Android\Notifications\res\values </strong>folder.</span>
</p>
<h2>Handling push callbacks</h2>
<p>
  <span>In order to listen to notification receive and click events, implement <code>INotificationListener</code> interface and its members' methods <code>OnNotificationClicked</code> and <code>OnNotificationReceived</code> into your class.&nbsp;</span><span><br></span>
</p>
<p>
  <span>Example:</span>
</p>
<pre><br><span><code>public class CountlyEntryPoint : MonoBehaviour, INotificationListener<br>{<br>  public void OnNotificationReceived(string message)<br>  {<br>  }<br><br>  public void OnNotificationClicked(string message, int index)<br>  {<br>  }<br>}</code></span></pre>
<p>
  <span>&nbsp;There are two ways to register for this class to listen to notification events.</span>
</p>
<p>
  <span>1. You may call <code>AddListener(this)</code>on <code>CountlyConfiguration</code> object before the SDK Init call.</span>
</p>
<p>
  <span>Example:</span>
</p>
<pre><span><code>private void Awake()<br>{<br>  CountlyConfiguration config = <strong>new</strong> CountlyConfiguration<br>  {<br>  AppKey = COUNTLY_APP_KEY,<br>  ServerUrl = COUNTLY_SERVER_URL,<br>  };<br>  config.AddListener(this);<br>  Countly.Instance.Init(config);<br>}</code></span><span></span></pre>
<p>
  <span></span><span></span>2. If SDK has been initialized<span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">, use the following code snippet to listen to push notification events.</span>
</p>
<pre><code style="font-size: 15px;">Countly.Instance.Notifications.AddListener(this);</code></pre>
<p>
  <span>To stop listening notification receive and click events, call</span>
</p>
<pre><span><code>Countly.Instance.Notifications.RemoveListener(this);</code></span></pre>
<p>
  <span>For more information, check the sample app on <a href="http://github.com/countly/countly-sdk-unity" target="_blank" rel="noopener">Github</a>.&nbsp;<br></span>
</p>
<h2 class="anchor-heading">Consent</h2>
<p>
  <span>This feature requires<code>Push</code> consent. No push notifications will be received if consent is required and not given.</span>
</p>
<h1 id="user-location" class="anchor-heading garden-focus-visible" tabindex="-1" data-garden-focus-visible="true">
  <span>User location</span>
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
    <span>Latitude and longitude values separated by a comma, e.g.</span><span>&nbsp;</span>"56.42345,123.45325".
  </li>
  <li>
    <span>Your user’s IP address.</span><span></span>
  </li>
</ul>
<h2 id="setting-location" class="anchor-heading">Setting location</h2>
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
  <span>Use <code>Countly.Location.</code>&nbsp;to disable or set the location at any time after the SDK Init call.</span>
</p>
<p>
  <span>For example:</span>
</p>
<pre><code class="hljs cs"><span><span class="hljs-keyword">string</span> countryCode = </span><span class="hljs-string">"us"</span><span>;<br><span class="hljs-keyword">string</span> city = </span><span class="hljs-string">"Houston"</span><span>;<br><span class="hljs-keyword">string</span> latitude = </span><span class="hljs-string">"29.634933"</span><span>; <br><span class="hljs-keyword">string</span> longitude = </span><span class="hljs-string">"-95.220255"</span><span>; <br><span class="hljs-keyword">string</span> ipAddress = </span><span class="hljs-keyword"><span class="hljs-literal">null</span></span><span>;</span>&nbsp;<br><br><span>Countly.Instance</span>.Location.S<span>etLocation</span>(<span>countryCode, city, latitude + </span><span class="hljs-string">","</span><span> + longitude, ipAddress</span>);</code></pre>
<p>
  When those values are set, a separate request will be created to send them. Except
  for IP address, because Countly server processes IP address only when starting
  a session.
</p>
<p>If you don't want to set specific fields, set them to null.</p>
<h2 id="disabling-location" class="anchor-heading">Disabling location</h2>
<p>
  <span>Users might want to opt-out of location tracking. To do so, </span><span>you can disable location during init:<br></span>
</p>
<pre>config.DisableLocation();</pre>
<p>To disable location after SDK initialization, call:</p>
<pre>Countly.Instance.Location.DisableLocation();</pre>
<p>
  <span>These actions will erase the cached location data from the device and the server.</span><span></span>
</p>
<h2 class="anchor-heading">Consent</h2>
<p>
  <span>This feature requires<code>Location</code> consent. If consent is not given and is required, no location information will be recorded. No reverse geo IP will be performed server side. SDK will behave as if location tracking is disabled.</span>
</p>
<p>
  If consent was given and then was removed, it will create a request that will
  clear location information server side.
</p>
<h1 id="remote-config" class="anchor-heading" tabindex="-1">Remote config</h1>
<p>
  <span>Available in the Enterprise Edition, Remote Config allows you to modify how your app functions or looks by requesting key-value pairs from your Countly server. The returned values may be modified based on the user profile. For more details, please see the </span><a href="https://resources.count.ly/docs/remote-config"><span>Remote Config documentation</span></a><span>.</span>
</p>
<h2 id="manual-remote-config-download" class="anchor-heading">Manual remote config</h2>
<p>
  To download Remote Config, call
  <code>Countly.Instance.RemoteConfigs.Update()</code>. After the successful download,
  the SDK stores the updated config locally.
</p>
<pre><strong>await</strong> Countly.Instance.RemoteConfigs.Update();</pre>
<h2>Accessing remote config values</h2>
<p>
  To access the stored config,&nbsp; call
  <code>Countly.Instance.RemoteConfigs.Configs</code>. It will return
  <code>null</code> if there isn't any config stored.
</p>
<pre><strong>Dictionary</strong>&lt;<strong>string</strong>, <strong>object</strong>&gt; config = Countly.Instance.RemoteConfigs.Configs;</pre>
<p>
  <span>The <code>Dictionary&lt;string, object&gt;</code> returns a value of the type <code>object</code> against</span><span> a key</span><span>. The developer then needs to cast it to the appropriate type.&nbsp;</span>
</p>
<h2 class="anchor-heading">Consent</h2>
<p>
  <span>This feature requires<code>RemoteConfig</code> consent. If consent is required and not give, no remote config information will be downloaded and stored.</span>
</p>
<p>
  If consent was given and then is removed, locally stored remote config information
  will be cleared.
</p>
<h1>User feedback</h1>
<h2>Ratings</h2>
<p>
  <span class="wysiwyg-color-black">Rating is a customer satisfaction tool that collects direct user feedback. For more details</span>,
  please see the
  <a href="/hc/en-us/articles/360037641291" target="_self">Rating documentation</a>.
</p>
<h3>Manual rating reporting</h3>
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
<h2 class="anchor-heading">Consent</h2>
<p>
  If consent is required, recording star rating requires<code>StarRating</code><span>consent. If consent is required and not give, it will not be possible to record star rating.</span><span></span>
</p>
<h1>User profiles</h1>
<p>
  <span>For information about User Profiles, review </span><a href="http://resources.count.ly/docs/user-profiles"><span>this documentation</span></a><span>.</span>
</p>
<h2>Setting predefined values</h2>
<p>
  The Countly Unity SDK allows you to upload specific data related to a user to
  the Countly server. You may set the following predefined data for a particular
  user:
</p>
<ul>
  <li>
    <strong>Name</strong>: Full name of the user.
  </li>
  <li>
    <strong>Username</strong>: Username of the user.
  </li>
  <li>
    <strong>Email</strong>: Email address of the user.
  </li>
  <li>
    <strong>Organization</strong>: Organization the user is working in.
  </li>
  <li>
    <strong>Phone</strong>: Phone number.
  </li>
  <li>
    <strong>PictureUrl</strong>: Web-based Url for the user’s profile.
  </li>
  <li>
    <strong>Gender</strong>: Gender of the user (use only single char like ‘M’
    for Male and ‘F’ for Female).
  </li>
  <li>
    <strong>BirthYear</strong>: Birth year of the user.
  </li>
</ul>
<p>
  The SDK allows you to upload user details using the methods listed below.
</p>
<p>Example:</p>
<pre><code>CountlyUserDetailsModel userDetails = <strong>new</strong> CountlyUserDetailsModel(name: "Full Name", username: "username", email: "useremail@email.com", organization: "Organization", phone: "222-222-222", pictureUrl: "http://webresizer.com/images2/bird1_after.jpg", gender: "M", birthYear: "1986", null);<br><strong>await</strong> Countly.Instance.UserDetails.SetUserDetailsAsync(userDetails);</code></pre>
<h2>Setting custom values</h2>
<p>
  The SDK gives you the flexibility to send only the custom data to Countly servers,
  even when you don’t want to send other user-related data. You first need to create
  an instance of the class <code>CountlyUserDetailsModel</code>. All the parameters
  expected in the constructor remain the same. You can leave all parameters as
  <strong>null</strong> and just provide the custom data segment for sending custom
  data to the Countly server.
</p>
<p>Example:</p>
<pre><code>CountlyUserDetailsModel userDetails = <strong>new</strong> CountlyUserDetailsModel( <strong>new</strong> Dictionary&lt;string, object&gt; { <br>    { "Height", "5.8" }, <br>    { "Mole", "Lower Left Cheek" } <br>    });<br><strong>await</strong> <span>Countly.Instance</span>.UserDetails.SetCustomUserDetailsAsync(userDetails);</code></pre>
<h2>Setting User picture</h2>
<p>
  The SDK allows you to set the user's picture URL along with other details using
  the methods listed below.
</p>
<p>Example:</p>
<pre><code>CountlyUserDetailsModel userDetails = <strong>new</strong> CountlyUserDetailsModel(name: "Full Name", username: "username", email: "useremail@email.com", organization: "Organization", phone: "222-222-222", pictureUrl: "http://webresizer.com/images2/bird1_after.jpg", gender: "M", birthYear: "1986", null);<br><strong>await</strong> Countly.Instance.UserDetails.SetUserDetailsAsync(userDetails);</code></pre>
<h2>Modifying data</h2>
<p>
  <span>You may also perform different manipulations to your custom data values, such as incrementing the current value on a server or storing an array of values under the same property.</span>
</p>
<p>
  <span>You will find the list of available manipulations below:</span>
</p>
<pre><code class="java hljs"><span class="hljs-comment">//set one custom properties</span>
<strong>await</strong> <span>Countly.Instance</span>.UserDetails.Set(<span class="hljs-string">"test"</span>, <span class="hljs-string">"test"</span>);<br>
<span class="hljs-comment">//increment used value by 1</span>
<strong>await</strong> <span>Countly.Instance</span>.UserDetails.Increment(<span class="hljs-string">"used"</span>);<br>
<span class="hljs-comment">//increment used value by provided value</span>
<strong>await</strong> <span>Countly.Instance</span>.UserDetails.IncrementBy(<span class="hljs-string">"used"</span>, <span class="hljs-number">2</span>);<br>
<span class="hljs-comment">//multiply value by provided value</span>
<strong>await</strong> <span>Countly.Instance</span>.UserDetails.Multiply(<span class="hljs-string">"used"</span>, <span class="hljs-number">3</span>);<br>
<span class="hljs-comment">//save maximal value</span>
<strong>await</strong> <span>Countly.Instance</span>.UserDetails.Max(<span class="hljs-string">"highscore"</span>, <span class="hljs-number">300</span>);<br>
<span class="hljs-comment">//save minimal value</span>
<strong>await</strong> <span>Countly.Instance</span>.UserDetails.Min(<span class="hljs-string">"best_time"</span>,<span class="hljs-number">60</span>);<br>
<span class="hljs-comment">//set value if it does not exist</span>
<strong>await</strong> <span>Countly.Instance</span>.UserDetails.SetOnce(<span class="hljs-string">"tag"</span>, <span class="hljs-string">"test"</span>);<br>
<span class="hljs-comment">//insert value to array of unique values</span>
<strong>await</strong> <span>Countly.Instance</span>.UserDetails.PushUnique(<span class="hljs-string">"type"</span>, new string[] {<span class="hljs-string">"morning"}</span>);<br>
<span class="hljs-comment">//insert value to array which can have duplicates</span>
<strong>await</strong> <span>Countly.Instance</span>.UserDetails.Push(<span class="hljs-string">"type"</span>, new string[] {<span class="hljs-string">"morning"}</span>);<br>
<span class="hljs-comment">//remove value from array</span>
<strong>await</strong> <span>Countly.Instance</span>.UserDetails.Pull(<span class="hljs-string">"type"</span>, new string[] {<span class="hljs-string">"morning"}</span>);

<span class="hljs-comment">//send provided values to server</span>
<strong>await</strong> <span>Countly.Instance</span>.UserDetails.SaveAsync()<br></code></pre>
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
  the latest value will be posted to the server.&nbsp;
</p>
<p>Example:</p>
<pre><code><span>Countly.Instance</span>.UserDetails.Max("Weight", 90);<br><span>Countly.Instance</span>.UserDetails.SetOnce("Distance", "10KM");<br><span>Countly.Instance</span>.UserDetails.Push("Mole", new string[] { "Left Cheek", "Back", "Toe" }); ;<br><strong>await</strong> <span>Countly.Instance</span>.UserDetails.SaveAsync();</code></pre>
<h2 class="anchor-heading">Consent</h2>
<p>
  This feature requires<code>User</code><span>consent. If consent is required and not given, it will not be possible to record user profile information.</span>
</p>
<h1 id="user-consent-management" class="anchor-heading" tabindex="-1">User consent</h1>
<p>
  <span>In an effort to comply with GDPR, starting from 20.11.1, Unity Countly SDK provides ways to toggle different Countly features on/off depending on the given consent.</span>
</p>
<p>
  More information about GDPR can be found<span>&nbsp;</span><a href="https://blog.count.ly/countly-the-gdpr-how-worlds-leading-mobile-and-web-analytics-platform-can-help-organizations-5015042fab27">here</a>.
</p>
<h2>Setup during init</h2>
<p>
  <span>The requirement for consent is disabled by default. To enable it, you will have to set <code>RequiresConsent</code></span><span> value <code>true</code></span><span>&nbsp;before initializing Countly.</span>
</p>
<pre><code>CountlyConfiguration configuration = new CountlyConfiguration {<br>ServerUrl = "https://try.count.ly/",<br>AppKey = "YOUR_APP_KEY",<br>EnableConsoleLogging = true,<br>NotificationMode = TestMode.AndroidTestToken,<br>RequiresConsent = true<br>};<br><br>Countly.Instance.Init(configuration);</code></pre>
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
<p>
  *<span> </span><code>Sessions</code><span>&nbsp;</span>- tracking when, how often,
  and how long users use your app
</p>
<p>
  *<span> </span><code>Events</code><span>&nbsp;</span>- allow sending events to
  the server
</p>
<p>
  *<span> </span><code>Views</code><span>&nbsp;</span>- allow the tracking of which
  views user visits
</p>
<p>
  *<span> </span><code>Location</code><span>&nbsp;</span>- allow the sending of
  location information
</p>
<p>
  *<span> </span><code>Crashes</code><span>&nbsp;</span>- allow the tracking of
  crashes, exceptions, and errors
</p>
<p>
  *<span> </span><code>Users</code><span>&nbsp;</span>- allow the collecting/providing
  of user information, including custom properties
</p>
<p>
  *<span> </span><code>Push</code><span>&nbsp;</span>- allow push notifications
</p>
<p>
  *<span> </span><code>StarRating</code><span>&nbsp;</span>- allow their rating
  and feedback to be sent
</p>
<p>
  *<span> </span><code>RemoteConfig</code><span>&nbsp;</span>- allow downloading
  remote config values from your server
</p>
<p>
  In case consent is required, you may give consent to features before the SDK
  Init call. These features consents are not persistent and must be given on every
  restart.
</p>
<pre><code>// prepare consents that should be given</code><br><code>Consents[] consents = <strong>new</strong> Consents[] { Consents.Users, Consents.Location;</code><br><code>// give consents to the features</code><br><code>configuration.GiveConsent(consents);</code></pre>
<h2 id="changing-consent" class="anchor-heading">Changing consent</h2>
<p>
  After init call, use<span>&nbsp;<code class="java">Countly.Instance.Consents.</code> to change co</span>nsent.
</p>
<p>
  <span>There are 2 ways of changing feature consent: </span>
</p>
<ul>
  <li>
    <span>&nbsp;<code>GiveConsent</code>/<code>RemoveConsent</code></span><span>&nbsp;- gives or removes consent to a specific feature.</span>
  </li>
</ul>
<pre><code class="java">// give consent to "sessions" feature</code><br><code>Countly.Instance.Consents.GiveConsent(new Consents[] { Consents.Sessions});</code><br><code class="java">// remove consent from "sessions" feature </code><br><code>Countly.Instance.Consents.RemoveConsent(new Consents[] { Consents.Sessions});</code></pre>
<ul>
  <li>
    <code>GiveConsentAll</code> / <code>RemoveAllConsent</code>-
    <span>gives or removes</span> all consents.
  </li>
</ul>
<pre><code class="hljs-comment">// Give consent to all features</code><br><code>Countly.Instance.Consent.GiveConsentAll();</code><br><code class="hljs-comment">// Remove consent from all features</code><br><code>Countly.Instance.Consent.RemoveAllConsent();</code></pre>
<h2>
  <span style="font-weight: 400;">Feature groups</span>
</h2>
<p>
  <span>Consents may be put into groups. By doing this, you may give/remove consent to multiple features in the same call. Groups may be created using <code>CreateConsentGroup</code> call during SDK configuration</span><span>. Those groups are not persistent and must be created on every restart. During SDK configuration consents to groups may be given by using <code class="java">GiveConsentToGroup</code>.</span>
</p>
<pre><code class="java hljs"><span class="java">// prepare consents that should be added to the group</span></code><br><code class="java hljs">Consents[] <span class="hljs-comment">consents</span> = <strong>new</strong> Consents[] { Consents.Users, Consents.Location;</code><br><code class="java"><span class="java">// create the Consent group</span></code><br><code class="java">configuration.CreateConsentGroup("User-Consents", <span class="hljs-comment">consents</span>);</code><br><code class="java hljs"><span class="hljs-comment">// give consent to the provide consent group</span></code><br><code class="java hljs">configuration.GiveConsentToGroup("User-Consents");</code></pre>
<p>
  After init has been called, use <code>GiveConsentToGroup</code> /
  <code>RemoveConsentOfGroup</code> to <span>give or remove </span>consent for
  a feature group.
</p>
<p>Example:</p>
<pre><code class="java">// prepare array of groups</code><br><code>string[] groupName = new string[]{ "User-Consents", "Events-Consents" };</code><br><code class="java">// give consent to groups</code><br><code>Countly.Instance.Consent.GiveConsentToGroup(groupName);</code><br><code class="java">// remove consent of groups </code><br><code>Countly.Instance.Consent.RemoveConsentOfGroup(groupName);</code></pre>
<p>&nbsp;</p>
<h1>Security and privacy</h1>
<h2 id="parameter-tampering-protection" class="anchor-heading">Parameter tamper protection</h2>
<p>
  <span>You may set the optional&nbsp;<code>salt</code></span><span>&nbsp;to be used for calculating the checksum of requested data which will be sent with each request, using the&nbsp;<code>&amp;checksum</code></span><span>&nbsp;field. You will need to set exactly the same&nbsp;<code>salt</code></span><span>&nbsp;on the Countly server. If&nbsp;the&nbsp;<code>salt</code></span><span>&nbsp;on the Countly server is set, all requests would be checked for the validity of the&nbsp;<code>&amp;checksum</code></span><span> field before being processed.</span>
</p>
<pre><code class="java hljs">configuration.Salt = "salt";</code></pre>
<h1>Other features</h1>
<h2>Setting event queue threshold</h2>
<p>
  In SDK configuration, you may limit the number of events that can be recorded
  internally by the system before they can all be sent together in one request.&nbsp;<br>
  Example:
</p>
<pre><code>CountlyConfiguration configuration = new CountlyConfiguration {<br>ServerUrl = "https://try.count.ly/",<br>AppKey = "YOUR_APP_KEY",<br>EnableConsoleLogging = true,<br>NotificationMode = TestMode.AndroidTestToken,<br>EventThreshold = 1000<br>};<br><br>Countly.Instance.Init(configuration);</code></pre>
<p>
  Once the threshold limit is reached, the system groups all recorded events and
  sends them to the server.
</p>
<h2 id="checking-if-init-has-been-called" class="anchor-heading">Checking if the SDK has been initialized</h2>
<p>
  <span>In case you would like to check if init has been called, you may use the following property:</span>
</p>
<pre><code class="java hljs">Countly.Instance.IsSDKInitialized;</code></pre>
<h2 id="checking-if-init-has-been-called" class="anchor-heading">SDK config parameters explained</h2>
<p>
  <span>To change the Configuration, update the values of parameters in the "<strong>CountlyConfiguration" </strong>object. Here are the details of the optional parameters:</span><span></span>
</p>
<p>
  <strong>DeviceId -<span>&nbsp;</span></strong>(Optional, string) Your Device
  ID. It is an optional parameter.<span>&nbsp;</span><strong>Example:</strong><span>&nbsp;</span>f16e5af2-8a2a-4f37-965d-qwer5678ui98.
</p>
<p>Below you can find details of each parameter:</p>
<p>
  <strong>Salt -<span>&nbsp;</span></strong>(Optional, string) Used to prevent
  parameter tampering. The default value is<span>&nbsp;</span><strong>NULL</strong>.&nbsp;
</p>
<p>
  <strong>EnablePost -<span>&nbsp;</span></strong>(bool) When set to<span>&nbsp;</span><strong>true</strong>,
  all requests made to the Countly server will be done using HTTP POST. Otherwise,
  the SDK sends all requests using the HTTP GET method. In some cases, if the data
  to be sent exceeds the 1800-character limit, the SDK uses the POST method.<span>&nbsp;The default value is&nbsp;<strong>false</strong>.&nbsp;</span>
</p>
<p>
  <span><strong>EnableTestMode - </strong>(Optional, bool) This parameter is useful in development when you don't want to send requests to the Countly server. The default value is<strong>&nbsp;false</strong>.</span>
</p>
<p>
  <strong>RequiresConsent -<span>&nbsp;</span></strong><span>(Optional, bool)&nbsp;</span>This
  is useful
  <span>during the app run when the user wants to opt-out of SDK features.</span>
</p>
<p>
  <strong>EnableConsoleLogging -<span>&nbsp;</span></strong><span>(Optional, bool)&nbsp;</span>This
  parameter is useful when you are debugging your application. When set to<span>&nbsp;</span><strong>true</strong>,
  it basically turns on Logging.&nbsp;
</p>
<p>
  <strong>SessionDuration -</strong><span>&nbsp;(Optional, int)&nbsp;</span>Sets
  the interval (in seconds) after which the application will automatically extend
  the session, providing the manual session is disabled. This interval is also
  used to process requests in the queue. The default value is<strong><span>&nbsp;</span>60<span>&nbsp;</span></strong>(seconds).
</p>
<p>
  <strong>EventThreshold -</strong><span>&nbsp;(Optional, int) Sets&nbsp;</span>a
  threshold value that limits the number of events that can be recorded internally
  by the system before they can all be sent together in one request. Once the threshold
  limit is reached, the system groups all recorded events and sends them to the
  server. The default value is<span>&nbsp;</span><strong>100.</strong><span>&nbsp;</span>
</p>
<p>
  <strong>StoredRequestLimit -</strong><span>&nbsp;(Optional, int)&nbsp;</span>Sets
  a threshold value that limits the number of requests that can be stored internally
  by the system. The system processes these requests after every session duration
  interval has passed. The default value is<span>&nbsp;</span><strong>1000.</strong>
</p>
<p>
  <strong>NotificationMode -<span>&nbsp;</span></strong>(Optional, enum) When<span>&nbsp;</span><strong>None</strong>,
  the SDK disables Push Notifications for the device. Use an<span>&nbsp;</span><strong>iOS Test Token<span>&nbsp;</span></strong>or
  an<span>&nbsp;</span><strong>Android Test Token</strong><span>&nbsp;</span>for
  testing purposes, and in production use a<span>&nbsp;</span><strong>Production</strong><span>&nbsp;</span><strong>Token.</strong><span>&nbsp;</span>The
  SDK uses the supplied mode for sending Push Notifications. The default value
  is<span>&nbsp;</span><strong>None.</strong>
</p>
<p>
  <strong>EnableAutomaticCrashReporting -<span>&nbsp;</span></strong><span>(Optional, bool) U</span>sed
  to turn on/off Automatic Crash Reporting. When set to<span>&nbsp;</span><strong>true</strong>,
  the SDK will catch exceptions and automatically report them to the Countly server.
  The default value is<span>&nbsp;</span><strong>true.</strong>
</p>
<h1>FAQ</h1>
<h2>What information is collected by the SDK</h2>
<p>
  The following description mentions data that is collected by SDK to perform their
  functions and implement the required features. Before any of it is sent to the
  server, it is stored locally.
</p>
<p>
  * When sending any network requests to the server, the following things are sent
  in addition to the main data:<br>
  - Timestamp of when the request is created<br>
  - Current hour<br>
  - Current day of week<br>
  - Current timezone<br>
  - SDK version<br>
  - SDK name
</p>
<p>
  * If sessions are used then it would record the session start time, end time,
  and duration
</p>
<p>
  * If sessions are used then also device metrics are collected which contains:<br>
  - Device model<br>
  - Screen resolution<br>
  - Screen density<br>
  - OS name<br>
  - OS version<br>
  - App version<br>
  <span>- Locale identifier</span>
</p>
<p>
  <span></span><span>* When generating a device ID, if no custom ID is provided, the SDK will use:</span><br>
  <span>- Android: md5 of ANDROID_ID&nbsp;<br></span><span>- iOS: I</span><span>t will be vendor id and </span><span>advertising id as a fallback<br></span><span>- Windows stores apps: It will be advertising id<br></span><span>- Windows Standalone: It will be hash from the concatenation of strings taken from computer system hardware classes.</span><span></span>
</p>
<p>
  * If push notification is used:<br>
  - The devices push notification token<br>
  - If the user clicks on the notification then the time of the click and on which
  button the user has clicked on&nbsp;
</p>
<p>
  * When events are recorded, the following information collected:<br>
  - Time of event<br>
  - Current hour<br>
  - Current day of week
</p>
<p>
  <span>* If crash tracking is enabled, it will collect the following information at the time of the crash:<br>- OS name<br>- OS version<br>- Device model<br>- Device architecture<br></span>-
  The graphics API type<br>
  <span>- Device resolution<br>- App version<br>- Time of the crash<br>- Crash stack trace<br>- Error description<br>- Total RAM<br>- Device battery level<br>- Device orientation<br></span>-
  The type of Internet reachability<br>
  <span>- If there is a network connection<br>- If the app is in the background<br>- How long has the application been running<br></span>
</p>
<p>
  <span>Any other information like data in events, location, user profile information, or other manual requests depends on what the developer decides to provide and is not collected by the SDK itself.</span>
</p>