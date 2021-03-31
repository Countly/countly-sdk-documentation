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
    To access the documentation for version 19.09 and older, click
    <a href="https://support.count.ly/hc/en-us/articles/900002413783" target="_self" rel="undefined">here.</a>
  </p>
</div>
<p>
  The following are some of the key assumptions being considered while developing
  the SDK. Please take into account the following <strong>before</strong> integrating
  this SDK:
</p>
<ol>
  <li>Scripting version is based on .NET 4.x equivalent</li>
  <li>API Compatibility Level is based on .NET 4.x</li>
</ol>
<h1>Integration</h1>
<p>
  Download the Unity package from
  <a href="https://github.com/Countly/countly-sdk-unity/releases" target="_blank" rel="noopener">GitHub</a>
  and import it into your project.
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Adding Write Permission</span></strong>
  </p>
  <p>
    If you expect the game to be saved
    <span>on an SD card or any other type of external storage</span>, set
    <strong>Write Permission</strong><span>&nbsp;</span><span>to 'External (SDCard). This can be found in your Android platform settings under 'Other Settings'.</span>
  </p>
</div>
<p>
  For more information, check the sample app on
  <a href="http://github.com/countly/countly-sdk-unity" target="_blank" rel="noopener">Github</a>.&nbsp;
</p>
<h1>
  <span>Setting up the SDK</span>
</h1>
<p>
  <span>Prefabs are stored in the <strong>Assets\Plugins\Countly\Prefabs</strong> folder. </span>Select
  the Countly prefab and in the inspector view, add <strong>serverUrl</strong>
  and <strong>appKey</strong>.&nbsp;<br>
  <br>
  <img src="/hc/article_attachments/900004493906/Screenshot_2020-11-06_at_7.25.57_PM.png" alt="Screenshot_2020-11-06_at_7.25.57_PM.png" width="689" height="614"><br>
  <br>
  <strong>serverUrl -</strong> (Mandatory, string) The URL of the Countly server
  where you are going to post your requests. <strong>Example:</strong>
  <a href="https://us-try.count.ly/">https://try.count.ly/<br></a>
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <strong><span class="wysiwyg-font-size-large">Which server/hostname should I use inside the SDK?</span></strong>
  </p>
  <p>
    If you are using Countly Enterprise Edition trial servers, use the corresponding
    server name, such as
    <a href="https://try.count.ly,">https://try.count.ly,</a>
    <a href="https://us-try.count.ly">https://us-try.count.ly</a> or
    <a href="https://asia-try.count.ly">https://asia-try.count.ly</a>.
  </p>
  <p>
    If you use Community Edition and Enterprise Edition, use your domain name.
  </p>
</div>
<p>
  <strong>appKey - </strong>(Mandatory, string) The “App Key” for the app that
  you created on the Countly server. <strong>Example:</strong> 124qw3er5u678qwef88d6123456789qwertyui123.
</p>
<p>
  <strong>deviceId - </strong>(Optional, string) Your Device ID. It is an optional
  parameter. <strong>Example:</strong> f16e5af2-8a2a-4f37-965d-qwer5678ui98.
</p>
<p>
  <span>To change the Configuration, update the parameter values.</span>
</p>
<p>Below you can find details of each parameter:</p>
<p>
  <strong>salt - </strong>(Optional, string) Used to prevent parameter tampering.
  The default value is <strong>NULL</strong>.&nbsp;
</p>
<p>
  <strong>enablePost - </strong>(bool) When set to <strong>true</strong>, all requests
  made to the Countly server will be done using HTTP POST. Otherwise, the SDK sends
  all requests using the HTTP GET method. In some cases, if the data to be sent
  exceeds the 1800-character limit, the SDK uses the POST method.<span> The default value is <strong>false</strong>.&nbsp;</span>
</p>
<p>
  <span><strong>enableTestMode - </strong> (Optional, bool) This parameter is useful in development when you don't want to send requests to the Countly server. The default value is<strong> false</strong>.</span>
</p>
<p>
  <strong>enableConsoleLogging - </strong><span> (Optional, bool) </span>This parameter
  is useful when you are debugging your application. When set to
  <strong>true</strong>, it basically turns on Logging.&nbsp;
</p>
<p>
  <strong>ignoreSessionCooldown -</strong><span>&nbsp;(Optional, bool) </span>Turns
  on/off the session cooldown behavior.
  <span>The default value is <strong>false</strong>.&nbsp;</span>
</p>
<p>
  <strong>sessionDuration -</strong><span> (Optional, int) </span>Sets the interval
  (in seconds) after which the application will automatically extend the session,
  providing the manual session is disabled. This interval is also used to process
  requests in the queue. The default value is<strong> 60 </strong>(seconds).
</p>
<p>
  <strong>eventThreshold -</strong><span> (Optional, int) Sets </span>a threshold
  value that limits the number of events that can be recorded internally by the
  system before they can all be sent together in one request. Once the threshold
  limit is reached, the system groups all recorded events and sends them to the
  server. The default value is <strong>100.</strong><span>&nbsp;</span>
</p>
<p>
  <strong>storedRequestLimit -</strong><span> (Optional, int) </span>Sets a threshold
  value that limits the number of requests that can be stored internally by the
  system. The system processes these requests after every sessionDuration interval
  has passed. The default value is <strong>1000.</strong>
</p>
<p>
  <strong>notificationMode - </strong>(Optional, enum) When
  <strong>None</strong>, the SDK disables Push Notifications for the device. Use
  an <strong>iOS Test Token </strong>or an <strong>Android Test Token</strong>
  for testing purposes and in production use a <strong>Production</strong>
  <strong>Token.</strong> The SDK uses the supplied mode for sending Push Notifications.
  The default value is <strong>None.</strong>
</p>
<p>
  <strong>enableAutomaticCrashReporting - </strong><span>(Optional, bool) U</span>sed
  to turn on/off Automatic Crash Reporting. When set to <strong>true</strong>,
  the SDK will catch exceptions and automatically report them to the Countly server.
  The default value is <strong>true.</strong>
</p>
<h2>Initializing the SDK</h2>
<p>
  <span>To start using Countly, you need to attach a script to any GameObject in your scene. Add a public field of type <strong>Countly </strong>in this script and assign the <strong>Countly prefab</strong> to this field.&nbsp;Prefabs are stored in the Prefabs folder.&nbsp;<br></span><span></span>
</p>
<p>
  <span>Instantiate the Countly prefab in the awake method.<br></span>
</p>
<pre><span><strong>public</strong> <strong>Countly</strong> countlyPrefab;<br><strong>private</strong> <strong>Countly</strong> countly;<br></span><br><strong>void</strong> Awake ()<br>{<br> countly = <strong>Instantiate</strong>(countlyPrefab);<br>}<span></span></pre>
<p class="callout__title">
  <strong><span class="wysiwyg-font-size-large"> Accessing Countly Global Instance</span></strong>
</p>
<p>
  To access the Countly Global Instance use the following code snippet:
</p>
<pre>Countly.Instance.</pre>
<h1>Session handling</h1>
<p>The Unity SDK handles the session automatically.</p>
<p>
  <strong>Begin Session:</strong> the SDK is responsible for automatically handling
  the Countly session in your app. As soon as you call the initialization methods
  (Begin and SetDefaults) in your app start event, the SDK will start the session
  automatically (only when you set <code>enableManualSessionHandling</code> to
  true during initialization).
</p>
<p>
  <strong>Update Session:</strong> the SDK is responsible for automatically extending
  the session after every 60 seconds (default value). This value is configurable
  during initialization using the parameter sessionDuration. It cannot be modified
  after initialization.
</p>
<p>
  Note that in iOS, the session will not be extended when the app is in the background.
  As soon as the user switches back to the app, the session extension will resume.
  In Android, the session will extend on both occasions: foreground and background.
</p>
<p>
  <strong>End Session:</strong> the SDK is responsible for automatically ending
  the session whenever the user quits the application.
</p>
<p>
  The Session will be ended automatically when the user
  <span class="wysiwyg-color-black">calls </span><span style="background-color: #e9ebed; font-family: monospace, monospace; font-size: 13px; white-space: pre;">Application.Quit()</span>.
</p>
<h1>Events</h1>
<h2>Setting up events</h2>
<p>
  <span style="font-weight: 400;">An </span><a href="http://resources.count.ly/docs/custom-events"><span style="font-weight: 400;">event</span></a><span style="font-weight: 400;"> is any type of action that you can send to a Countly instance, e.g. purchases, changed settings, view enabled, and so on, letting you get valuable information about your application.</span>
</p>
<p>
  The Unity SDK helps record as many events as you want (you can set a threshold
  limit during initialization), and the system will send them automatically to
  the server once the threshold limit is reached. By default, Countly tracks only
  up to 100 events. However, this is also configurable.
</p>
<h2>Accessing event-related functionalities</h2>
<p>
  In the SDK, all event-related functionalities can be browsed from the returned
  interface on:
</p>
<pre>countly.Events.</pre>
<h2>Segmentation</h2>
<p>
  When providing segmentation for events, the only valid data types are: "String",
  "Integer", "Double", and "Boolean". All other types will be ignored.
</p>
<h2>Event usage examples</h2>
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
<h3>1. Event key and count</h3>
<pre><code class="java"><strong>await</strong> countly.Events.RecordEventAsync("purchase", count: 1);</code></pre>
<h3>2. Event key, count, and sum</h3>
<pre><code class="java"><strong>await</strong> countly.Events.RecordEventAsync(key: "purchase", count: 1, sum: 0.99);</code></pre>
<h3>3. Event key and count with segmentation(s)</h3>
<pre><code class="java">SegmentModel segmentation= new SegmentModel();

<strong>await</strong> countly.Events.RecordEventAsync(key: "<span>purchase</span>", segmentation: segment, count: 1);<br></code></pre>
<h3>4. Event key, count, and sum with segmentation(s)</h3>
<pre><code class="java">SegmentModel segmentation = new SegmentModel();
 segmentation.Add("country", "Germany");<br> segmentation.Add("app_version", "1.0");

<strong>await</strong> countly.Events.RecordEventAsync(key: "<span>purchase</span>", segmentation: segment, count: 1, sum: 0.99);</code></pre>
<h3>5. Event key, count, sum, and duration with segmentation(s)</h3>
<pre><code class="java">SegmentModel segmentation = new SegmentModel();
 segmentation.Add("country", "Germany");<br> segmentation.Add("app_version", "1.0");

<strong>await</strong> countly.Events.RecordEventAsync(key: "<span>purchase</span>", segmentation: segment, count: 1, sum: 0.99, duration: 60);<br></code></pre>
<p>
  <span style="font-weight: 400;">These are only a few examples of what you can do with Events. You may go beyond those examples and use country, app_version, game_level, time_of_day, and any other segmentation of your choice that will provide you with valuable insights.</span>
</p>
<h1 id="crash-reporting" class="anchor-heading" tabindex="-1">Crash reporting</h1>
<p>
  <span>The Countly SDK for Unity can collect </span><a href="http://resources.count.ly/docs/introduction-to-crash-reporting-and-analytics"><span>Crash Reports</span></a><span>,</span><span>&nbsp;which you may examine and resolve later on the server.</span>
</p>
<h2>Automatic crash reporting</h2>
<p>
  The Unity SDK can automatically report uncaught exceptions/crashes in the application
  to the Countly server. To report uncaught exceptions/crashes automatically, enable
  <strong>enableAutomaticCrashReporting<span>&nbsp;</span></strong><span>in the SDK configuration.</span>
</p>
<h2 id="accessing-crashrelated-functionality" class="anchor-heading">Accessing crash-related functionalities</h2>
<p>
  In the SDK all crash-related functionalities can be browsed from the returned
  interface on:
</p>
<pre>countly.CrashReports.</pre>
<h2 id="adding-breadcrumbs" class="anchor-heading">Adding breadcrumbs</h2>
<p>
  Throughout your app, you can leave&nbsp;crash breadcrumbs which would describe
  previous steps that were taken in your app before the crash. After a crash happens,
  they will be sent together with the crash report.
</p>
<p>The following command adds a crash breadcrumb:</p>
<pre>countly.CrashReports.AddBreadcrumbs("breadcrumb");</pre>
<h2 id="logging-handled-exceptions" class="anchor-heading">Logging handled exceptions</h2>
<p>
  <span>You might catch an exception or similar error during your app’s runtime.</span>
</p>
<p>
  <span>You may also log these handled exceptions to monitor how and when they are happening.</span>
</p>
<p>Example:</p>
<pre><strong>try</strong><br> {<br><strong>    throw</strong> <strong>new</strong> DivideByZeroException();<br> }<br> <strong>catch</strong> (Exception ex)<br> {<br>    <strong>await</strong> countly.CrashReports.SendCrashReportAsync(ex.Message, ex.StackTrace, LogType.Exception); <br> }&nbsp;</pre>
<h1>View tracking</h1>
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
<h1>View actions</h1>
<p>
  It is possible to report actions taken on views for heat maps or any other purpose.
  For that, use the following method:
</p>
<pre><strong>await</strong> countly.Views.ReportActionAsync("Click", 300, 500, 720, 1280);</pre>
<h1>
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
    <span>Your user’s IP address.</span>
  </li>
</ul>
<pre><span>string countryCode = </span><span class="hljs-string">"us"</span><span>;<br>string city = </span><span class="hljs-string">"Houston"</span><span>;<br>string latitude = </span><span class="hljs-string">"29.634933"</span><span>; <br>string longitude = </span><span class="hljs-string">"-95.220255"</span><span>; <br>string ipAddress = </span><span class="hljs-keyword">null</span><span>;</span>&nbsp;<br><br>countly.OptionalParameters.S<span>etLocation</span>(<span>countryCode, city, latitude + </span><span class="hljs-string">","</span><span> + longitude, ipAddress</span>);<br><br></pre>
<h2>Disabling location</h2>
<p>
  <span>Users might want to opt-out of location tracking. To do so, call:</span>
</p>
<pre>countly.OptionalParameters.DisableLocation();</pre>
<p>
  <span>This action will erase the cached location data from the device and the server.</span>
</p>
<h1>
  <span class="wysiwyg-color-black">Ratings</span>
</h1>
<p>
  <span class="wysiwyg-color-black">Ratings is a customer satisfaction tool that collects direct user feedback and comments. For more details</span>,
  please see the
  <a href="/hc/en-us/articles/360037641291" target="_self">Ratings documentation</a>.
</p>
<p>
  <span>When a user rates your application, you can report it to the Countly server using the following method:</span>
</p>
<pre><strong>await</strong> countly.StarRatingReport.StarRatingAsync("android", "0.1", 3);</pre>
<h1 id="remote-config" class="anchor-heading" tabindex="-1">Remote Config</h1>
<p>
  <span>Available in the Enterprise Edition, Remote Config allows you to modify how your app functions or looks by requesting key-value pairs from your Countly server. The returned values may be modified based on the user profile. For more details, please see the </span><a href="https://resources.count.ly/docs/remote-config"><span>Remote Config documentation</span></a><span>.</span>
</p>
<h2 id="manual-remote-config-download" class="anchor-heading">Downloading Remote Config</h2>
<p>
  To download Remote Config, call <code>countly.RemoteConfigs.Update()</code>.
  After the successful download, the SDK stores the updated config locally.
</p>
<pre><strong>await</strong> countly.RemoteConfigs.Update();</pre>
<h2 id="getting-remote-config-values" class="anchor-heading">Getting Remote Config</h2>
<p>
  To access the stored config,&nbsp; call
  <code>countly.RemoteConfigs.Configs</code>. It will return <code>null</code>
  if there isn't any config stored.
</p>
<pre><strong>Dictionary</strong>&lt;<strong>string</strong>, <strong>object</strong>&gt; config = countly.RemoteConfigs.Configs;</pre>
<h1>User Profiles</h1>
<p>
  The Countly Unity SDK allows you to upload specific data related to a user to
  the Countly server. The SDK allows you to set the following predefined data for
  a particular user:
</p>
<ol>
  <li>Name: Full name of the user.</li>
  <li>Username: Username of the user.</li>
  <li>Email: Email address of the user.</li>
  <li>Organization: Organization the user is working in.</li>
  <li>Phone: Phone number.</li>
  <li>Picture Url: Web-based Url for the user’s profile.</li>
  <li>
    Gender: Gender of the user (use only single char like ‘M’ for Male and ‘F’
    for Female).
  </li>
  <li>Birth year: Birth year of the user.</li>
</ol>
<p>
  Apart from the above data, you can also add custom data for a user. The SDK allows
  you to upload user details using the methods listed below.
</p>
<h2 id="setting-up-user-profiles" class="anchor-heading" tabindex="-1">Setting up User Profiles</h2>
<p>
  <span>Available in the Enterprise Edition, User Profiles is a tool that helps you identify users, their devices, event timelines, and application crash information.&nbsp;</span>
</p>
<p>
  <span>You may send user-related information to Countly and let the Countly Dashboard show and segment this data. You may also send a notification to a group of users. For more information about User Profiles, review </span><a href="http://resources.count.ly/docs/user-profiles"><span>this documentation</span></a><span>.</span>
</p>
<p>Example:</p>
<pre><strong>var</strong> userDetails = <strong>new</strong> CountlyUserDetailsModel( "Full Name", "username", "useremail@email.com", "Organization", "222-222-222", "http://webresizer.com/images2/bird1_after.jpg", "M", "1986",<br>    <strong>new</strong> Dictionary&lt;string, object&gt; { <br>    { "Hair", "Black" }, <br>    { "Race", "Asian" }, <br>}); <br><strong>await</strong> countly.UserDetails.SetUserDetailsAsync(userDetails);</pre>
<h2>Setting up custom user details</h2>
<p>
  The SDK gives you the flexibility to send only the custom data to Countly servers,
  even when you don’t want to send other user-related data. Similar to the above
  method, it is also an instance method and not a static method. So, you first
  need to create an instance of the class <code>CountlyUserDetailsModel</code>.
  All the parameters expected in the constructor remain the same. You can leave
  all parameters as <strong>null</strong> and just provide the custom data segment
  for sending custom data to the Countly server.
</p>
<p>Example:</p>
<pre>var userDetails = <strong>new</strong> CountlyUserDetailsModel( <strong>new</strong> Dictionary&lt;string, object&gt; { <br>    { "Height", "5.8" }, <br>    { "Mole", "Lower Left Cheek" } <br>    });<br><strong>await</strong> countly.UserDetails.SetCustomUserDetailsAsync(userDetails);</pre>
<h2 id="modifying-custom-data" class="anchor-heading">Modifying custom data</h2>
<p>
  <span>You may also perform different manipulations to your custom data values, such as incrementing the current value on a server or storing an array of values under the same property.</span>
</p>
<p>
  <span>You will find the list of available manipulations below:</span>
</p>
<pre><code class="java hljs"><span class="hljs-comment">//set one custom properties</span>
<strong>await</strong> countly.UserDetails.Set(<span class="hljs-string">"test"</span>, <span class="hljs-string">"test"</span>);<br>
<span class="hljs-comment">//increment used value by 1</span>
<strong>await</strong> countly.UserDetails.Increment(<span class="hljs-string">"used"</span>);<br>
<span class="hljs-comment">//increment used value by provided value</span>
<strong>await</strong> countly.UserDetails.IncrementBy(<span class="hljs-string">"used"</span>, <span class="hljs-number">2</span>);<br>
<span class="hljs-comment">//multiply value by provided value</span>
<strong>await</strong> countly.UserDetails.Multiply(<span class="hljs-string">"used"</span>, <span class="hljs-number">3</span>);<br>
<span class="hljs-comment">//save maximal value</span>
<strong>await</strong> countly.UserDetails.Max(<span class="hljs-string">"highscore"</span>, <span class="hljs-number">300</span>);<br>
<span class="hljs-comment">//save minimal value</span>
<strong>await</strong> countly.UserDetails.Min(<span class="hljs-string">"best_time"</span>,<span class="hljs-number">60</span>);<br>
<span class="hljs-comment">//set value if it does not exist</span>
<strong>await</strong> countly.UserDetails.SetOnce(<span class="hljs-string">"tag"</span>, <span class="hljs-string">"test"</span>);<br>
<span class="hljs-comment">//insert value to array of unique values</span>
<strong>await</strong> countly.UserDetails.PushUnique(<span class="hljs-string">"type"</span>, <span class="hljs-string">"morning"</span>);<br>
<span class="hljs-comment">//insert value to array which can have duplicates</span>
<strong>await</strong> countly.UserDetails.Push(<span class="hljs-string">"type"</span>, <span class="hljs-string">"morning"</span>);<br>
<span class="hljs-comment">//remove value from array</span>
<strong>await</strong> countly.UserDetails.Pull(<span class="hljs-string">"type"</span>, <span class="hljs-string">"morning"</span>);

<span class="hljs-comment">//send provided values to server</span>
<strong>await</strong> countly.UserDetails.SaveAsync()<br></code></pre>
<p>
  In the end, always call
  <code><strong>await</strong> countly.UserDetails.SaveAsync();</code> to send
  them to the server.
</p>
<h2>Recording multiple update requests</h2>
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
<pre>countly.UserDetails.Max("Weight", 90);<br>countly.UserDetails.SetOnce("Distance", "10KM");<br>countly.UserDetails.Push("Mole", new string[] { "Left Cheek", "Back", "Toe" }); ;<br><strong>await</strong> countly.UserDetails.SaveAsync();</pre>
<h1>Changing Device ID</h1>
<p>
  The Countly Unity SDK persists Device ID when you provide it during initialization
  or generates a random ID when you don’t provide it. This Device ID will be used
  persistently for all future requests made from a device until you change that.
</p>
<p>
  The SDK allows you to change the Device ID at any point in time. You can use
  any of the following two methods to changing the Device ID, depending on your
  needs.
</p>
<h2>
  <span>Changing Device ID without server merge</span>
</h2>
<p>
  This method changes the Device ID and does the following other operations:
</p>
<ol>
  <li>Ends all the events that have been recorded untill now.</li>
  <li>Ends the current session.</li>
  <li>
    Updates Device ID and starts a new session with a new Device ID.
  </li>
</ol>
<p>Example:</p>
<pre><strong>await</strong> countly.Device.ChangeDeviceIDAndEndCurrentSessionAsync("New Device Id");</pre>
<h2>
  <span>Changing Device ID with server merge</span>
</h2>
<p>
  This method changes the Device ID and merges data for both Device IDs in the
  Countly server.
</p>
<p>Example:</p>
<pre><strong>await</strong> countly.Device.ChangeDeviceIDAndEndCurrentSessionAsync("New Device Id");</pre>
<h1>Push Notification</h1>
<p>
  The Countly Unity SDK supports
  <span>FCM (Firebase Cloud Messaging) for Android. By default Push Notifications are disabled. To enable them go to the Countly prefab settings and change Notification Mode in the Configuration.<br><img src="/hc/article_attachments/900003594203/mceclip0.png" alt="mceclip0.png" width="477" height="566"></span>
</p>
<p>
  <span>Use an <strong>iOS Test Token </strong>or an <strong>Android Test Token</strong> for testing purposes and in production use a <strong>Production</strong> <strong>Token</strong></span>
</p>
<h2>
  <span>Android&nbsp;</span>
</h2>
<h3 id="getting-fcm-credentials" class="anchor-heading">FCM credentials</h3>
<p>
  <span>The Countly server needs an FCM server key to send notifications through FCM. </span><span></span>
</p>
<p id="integrating-fcm-into-your-app" class="anchor-heading">
  To set it up, refer to
  <a href="https://support.count.ly/hc/en-us/articles/360037754031-Android-SDK#getting-fcm-credentials" target="_self" rel="undefined">Android documentation</a>.
</p>
<h3 class="anchor-heading">Integrating FCM into your app</h3>
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
<h3>
  <span style="font-size: 1.2em; font-weight: 600;">Changing </span><span style="font-size: 1.2em; font-weight: 600;">N</span><span style="font-size: 1.2em; font-weight: 600;">otification </span><span style="font-size: 1.2em; font-weight: 600;">Sound and I</span><span style="font-size: 1.2em; font-weight: 600;">cons</span>
</h3>
<p>
  <span>In order to change the sound and icons of the notifications, replace the sound and icons in the folder Assets/Plugins/Android/Notifications/res.&nbsp;</span>
</p>
<p>
  <span><strong>Note</strong>: The Notification channel name and description can be updated throgh the <strong>strings.xml</strong> file located in the <strong>Assets\Plugins\Android\Notifications\res\values </strong>folder.</span>
</p>
<h3>
  <span>Remove FCM Dependencies</span>
</h3>
<p>
  <span>By default, FCM dependencies are part of the <strong>SDK.</strong> To remove FCM dependencies, go to the <strong>Assets\Plugins\Android </strong>folder and delete the <strong>Notifications</strong> folder.</span>
</p>
<p>
  <span>To</span>&nbsp;add them back after removing<span>, re-import the Unity package.</span>
</p>
<h2>
  <span>iOS</span>
</h2>
<h3>Adding Scripting Define Symbols</h3>
<p>
  In Unity, go to <strong>Player Settings.&nbsp;</strong>In the
  <strong>Other Settings</strong> section, add the
  <span><strong>"COUNTLY_ENABLE_IOS_PUSH"&nbsp; </strong>symbol in </span><strong>Scripting Define Symbols.</strong><strong><img src="/hc/article_attachments/900004317706/Screenshot_2020-10-27_at_4.07.16_PM.png" alt="Screenshot_2020-10-27_at_4.07.16_PM.png"><br></strong>
</p>
<h3>
  <span>APNs Credentials</span>
</h3>
<p>
  <span>The Countly server needs the APNs <strong>Auth Key&nbsp;</strong>to send notifications. To get the APNs <strong>Auth Key&nbsp;</strong>and upload it to the County Server, refer to <a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#setting-up-apns-authentication" target="_self">iOS Documentation.</a></span>
</p>
<h3 id="configuring-ios-app" class="anchor-heading" tabindex="-1">Configuring the iOS app</h3>
<p>
  After exporting the <strong>iOS</strong> project, open the project in
  <strong>Xcode</strong>, and add <strong>Push Notifications</strong> Capability.<img src="/hc/article_attachments/900004294166/Screenshot_2020-10-26_at_3.13.25_PM.png" alt="Screenshot_2020-10-26_at_3.13.25_PM.png">
</p>
<h3>
  <span>Removing the APNs Dependencies</span>
</h3>
<p>
  <span>By default, the <strong>APNs</strong> dependencies are part of the <strong>SDK.</strong> To remove the <strong>APNs</strong> dependencies, go to the <strong>Assets\Plugins </strong>folder and delete the <strong>iOS</strong> folder. Remove the <strong>"COUNTLY_ENABLE_IOS_PUSH"</strong> symbol from <strong>Scripting Define Symbols </strong>in <strong>Player Settings.</strong></span>
</p>
<p>
  <span>To</span>&nbsp;add them back after removing<span>, re-import the Unity package and add back the <strong>"COUNTLY_ENABLE_IOS_PUSH"</strong> symbol.</span>
</p>