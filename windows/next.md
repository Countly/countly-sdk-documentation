<p>
  This document explains how to install Countly SDK for Windows desktop applications.
  It applies to version 22.02.X.
</p>
<div class="callout callout--info">
  <p>
    To access the documentation for version 21.11 click&nbsp;<a href="/hc/en-us/articles/11428429151513">here.</a>
  </p>
</div>
<div>
  <p>The Countly Windows SDK implements the following flavors:</p>
  <ol>
    <li>
      <span>Universal Windows Platform</span>
    </li>
    <li>
      <span>.NET Standard, Version=2.0</span>
    </li>
    <li>
      <span>.NET Portable, Version=4.5</span>
    </li>
    <li>.NET Framework, Version=v3.5</li>
    <li>.NET Framework, Version=v4.0, Profile=Client</li>
  </ol>
</div>
<p>
  The Countly GitHub page for this SDK contains also sample projects. You should
  be able to download them to test the basic functionality of this SDK and make
  sure you are using it correctly in case you encounter any problems in your application
</p>
<p>
  The project page can be found
  <a href="https://github.com/Countly/countly-sdk-windows/">here</a>
</p>
<h1>Adding the SDK to the Project</h1>
<p>
  <span>To install the package, you can use either the NuGet Package Manager or the Package Manager Console. When you install a package, NuGet records the dependency in either your project file or a&nbsp;</span><code>packages.config</code><span>&nbsp;file (depending on the project format).</span>
</p>
<ol>
  <li>
    In Solution Explorer, right-click<span>&nbsp;</span><strong>References</strong><span>&nbsp;</span>and
    choose<span>&nbsp;</span><strong>Manage NuGet Packages</strong>.<img src="/hc/article_attachments/6536931626649/image-NuGet-packages.png" alt="image-NuGet-packages.png">
  </li>
  <li>
    <span>Choose "nuget.org" as the&nbsp;</span><strong>Package source</strong><span>, select the&nbsp;</span><strong>Browse</strong><span>&nbsp;tab, search for&nbsp;</span><strong>Countly</strong><span>, select that package in the list, and select&nbsp;</span><strong>Install</strong><span>:<img src="/hc/article_attachments/6537196195481/mceclip0.png" alt="mceclip0.png"></span>
  </li>
  <li>
    <p>
      Accept any license prompts.<span></span>
    </p>
  </li>
</ol>
<h1>SDK Integration</h1>
<p class="anchor-heading">
  Before you can use any Countly functionality, you need to call
  <code>Countly.Instance.Init</code> to initiate the SDK.
</p>
<h2>Minimal Setup</h2>
<p>
  <span>The shortest way to initiate the SDK is with this call:</span>
</p>
<pre><code class="csharp">//create the Countly init object
CountlyConfig cc = new CountlyConfig();
cc.serverUrl = "http://YOUR_SERVER";
cc.appKey = "YOUR_APP_KEY";
cc.appVersion = "1.2.3";

//initiate the SDK with your preferences
Countly.Instance.Init(cc);</code></pre>
<p>
  <span>In the </span><code>CountlyConfig</code><span>&nbsp;object, you provide appKey and your Countly server URL. For more information on how to acquire you application key (appKey) and server URL, check&nbsp;<a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#acquiring-your-application-key-and-server-url" target="_self" rel="undefined">here</a>.</span>
</p>
<p>
  <strong>Note: </strong>The SDK targets multiple profiles. Therefore for some
  of them, there are feature differences. Either with additional function calls
  or with additional fields in the CountlyConfig object.
</p>
<div class="callout callout--info">
  <p>
    If you are in doubt about the correctness of your Countly SDK integration
    you can learn about methods to verify it from
    <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#how-to-validate-your-countly-integration" target="blank">here</a>.
  </p>
</div>
<h2>SDK Logging / Debug Mode</h2>
<p>
  <span>The first thing you should do while integrating our SDK is enable logging. If logging is enabled, then our SDK will print out debug messages about its internal state and encounter problems.</span>
  To enable logging you need to do the following two steps:
</p>
<p>
  <strong>Step 1</strong>: Enable SDK logging using the following call:
</p>
<pre><code class="csharp hljs">    Countly.IsLoggingEnabled = <span class="hljs-literal">true</span>;</code></pre>
<p>You can turn it on and off in any place of your code.&nbsp;</p>
<p>
  <strong>Step 2</strong>:
  <span>Go to project properties, select the 'Build' tab and make sure the following things are correct.</span>
</p>
<ul>
  <li>Configuration: Debug</li>
  <li>"Define DEBUG constant" is checked</li>
</ul>
<p>
  <img src="/hc/article_attachments/6537183236249/mceclip1.png" alt="mceclip1.png">
</p>
<p>
  Log messages written in the application will show up in 'Output' windows.
</p>
<p>
  <img src="/hc/article_attachments/6537211113369/mceclip4.png" alt="mceclip4.png">
</p>
<h2>SDK Data Storage</h2>
<p>
  Cached requests and other SDK relevant information is stored in files in a named
  folder. All platform targets except .net40 call that folder "countly", .net40
  calls that folder "countly_data".
</p>
<p>
  All platform targets except .net35 will use
  <a href="https://docs.microsoft.com/en-us/dotnet/standard/io/isolated-storage">IsolatedStorage</a>
  for that. .net35 will store that named folder in the same folder as the executable
  by default.
</p>
<p>
  If there are permission limitations for your app targeting .net35, then there
  is a call where you can change the path for the named storage folder. You can
  change that by using this:
</p>
<pre><code class="csharp">Countly.SetCustomDataPath("C:\path\to\new\folder\");</code></pre>
<h2>SDK Notes</h2>
<h3>Additional Info for UWP Project Setup</h3>
<p>
  It's possible to register an unhandled crash handler during SDK initialization.
  To do that, you need to provide a link to your application.
</p>
<pre><code class="csharp">var cc = new CountlyConfig
{
  serverUrl = "SERVER_URL",
  appKey = "APP_KEY",
  appKey = "XXXXXXXXXXXXXXXXXXXXXXXXXXXX
  appVersion = "1.2.3",
  application = referenceToApplication //provide link to your application
};

await Countly.Instance.Init(cc);</code></pre>
<h1>Crash Reporting</h1>
<p>
  <span>The Countly SDK for Windows can collect&nbsp;</span><a href="http://resources.count.ly/docs/introduction-to-crash-reporting-and-analytics"><span>Crash Reports</span></a><span>,</span><span>&nbsp;which you may examine and resolve later on the server.</span>
</p>
<h2>Automatic Crash Handling</h2>
<p>
  Countly SDK has the ability to automatically collect crash reports which you
  can examine and resolve later on the server. You should subscribe to the unhandled
  exceptions handler manually. Exception details and device properties will be
  sent on the next app launch.
</p>
<h2>Handled Exceptions</h2>
<p>
  <span>You might catch an exception or similar error during your app’s runtime. </span><span>You may also log these handled exceptions to monitor how and when they are happening.&nbsp;</span><span>To log exceptions use the following code snippet:</span>
</p>
<pre><code><strong>Dictionary</strong>&lt;string, string&gt; customInfo = new Dictionary&lt;string, string&gt;<br>{<br>{ "customData", "importantStuff" }<br>};<br><br>try {<br>    throw new Exception("It is an exception");<br>} catch (Exception ex) {<br><strong>    Countly</strong>.RecordException(ex.Message, ex.StackTrace, customInfo, false);<br>}</code></pre>
<p>Here is the detail of the parameters:</p>
<ul>
  <li>
    <strong>error -</strong><span> A</span>&nbsp;string that contains a detailed
    description of the exception.
  </li>
  <li>
    <strong>stackTrace -</strong><span> </span>A string that describes the contents
    of the call stack.
  </li>
  <li>
    <strong>customInfo -<span> </span></strong>Custom key/values to be reported.
  </li>
  <li>
    <strong>unhandled -</strong>&nbsp; (bool) Set false if the error is fatal.
  </li>
</ul>
<p>
  <span>If you have handled an exception and it turns out to be fatal to your app, you may use the following calls:</span>
</p>
<pre><code><strong>Countly</strong>.RecordUnhandledException(ex.Message, ex.StackTrace, customInfo, true);</code></pre>
<h2>Crash Breadcrumbs</h2>
<p>
  Throughout your app, you can leave&nbsp;crash breadcrumbs<span>&nbsp;</span><span>Mandatory that </span>would
  describe previous steps that were taken in your app before the crash. After a
  crash happens, they will be sent together with the crash report.
</p>
<p>The following command adds a crash breadcrumb:</p>
<pre><code>Countly.Instance.AddCrashBreadCrumb("breadcrumb");</code></pre>
<h2>Consent</h2>
<p>
  This feature uses<span>&nbsp;</span><code>Crashes</code><span>&nbsp;consent. No additional crash logs will be recorded if consent is required and not given.</span>
</p>
<h1>Events</h1>
<p>
  <span>An&nbsp;</span><a href="http://resources.count.ly/docs/custom-events"><span>event</span></a><span>&nbsp;is any type of action that you can send to a Countly instance, e.g. purchases, changed settings, view enabled, and so on, letting you get valuable information about your application.</span>
</p>
<p>
  <span>There are a couple of values that can be set when recording an event. The main one is the&nbsp;<strong>key</strong>&nbsp;property which would be the identifier/name for that event.&nbsp; For example, in case a user purchased an item in a game, you could create an event with the key 'purchase'.</span>
</p>
<p>
  <span>Optionally there are also other properties that you might want to set:</span>
</p>
<ul>
  <li>
    <strong>Count -</strong>&nbsp; a whole numerical value that marks how many
    times this event has happened. The default value for that is<span>&nbsp;</span><strong>1</strong>.
  </li>
  <li>
    <strong>Sum -</strong><span>&nbsp;</span>This value would be summed across
    all events in the dashboard. F<span>or example, in-app purchase events sum of purchased items. Its default value is <strong>null</strong>.</span>
  </li>
  <li>
    <strong>Duration -<span>&nbsp;</span></strong>Used to record and track the
    duration of events. The default value is<span> </span><strong>null</strong>.
  </li>
  <li>
    <strong>Segmentation-<span>&nbsp;</span></strong>A value where you can provide
    custom segmentation for your events to track additional information. It is
    a key and value map. The accepted data types for the value are<span>&nbsp;</span><span>"String".&nbsp;</span>
  </li>
</ul>
<h2>Recording Events</h2>
<p>
  <span>Here is a quick way to&nbsp;</span><span>record an event:</span>
</p>
<pre><code class="csharp">Countly.RecordEvent("event-key");</code></pre>
<p>
  <span>Based on the example below of an event recording a&nbsp;<strong>purchase</strong>, h</span><span>ere is a quick summary of the information for each usage:</span>
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
    versions.
  </li>
</ul>
<p>
  <strong>1. Event key and count</strong>
</p>
<pre><code class="csharp">await Countly.RecordEvent("purchase", 3);</code></pre>
<p>
  <strong>2.</strong> <strong>Event key, count, and sum</strong>
</p>
<pre><code class="csharp">await Countly.RecordEvent("purchase", 3, 0.99);</code></pre>
<p>
  <strong>3. Event key and count with segmentation(s)</strong>
</p>
<pre><code class="csharp">Segmentation segmentation = new Segmentation();
segmentation.Add("country", "Germany");
segmentation.Add("app_version", "1.0");
await Countly.RecordEvent("purchase", 3, segmentation);
</code></pre>
<p>
  <strong>4. Event key, count, and sum with segmentation(s)</strong>
</p>
<pre><code class="csharp">Segmentation segmentation = new Segmentation();
segmentation.Add("country", "Germany");
segmentation.Add("app_version", "1.0");
await Countly.RecordEvent("purchase", 3, 2.97, segmentation);
</code></pre>
<p>
  <strong>5. Event key, count, sum, duration with segmentation(s)</strong>
</p>
<pre><code class="csharp">Segmentation segmentation = new Segmentation();
segmentation.Add("country", "Germany");
segmentation.Add("app_version", "1.0");
await Countly.RecordEvent("purchase", 3, 2.97, 122.45, segmentation);</code></pre>
<p>
  <span>These are only a few examples of what you can do with Events. You may go beyond those examples and use country, app_version, time_of_day, and any other segmentation of your choice that will provide you with valuable insights.</span>
</p>
<h2>Timed Events</h2>
<p>
  Timed events are events which gives you the ability to calculate the duration
  it takes for the event to take place with respect to any arbitrary point you
  choose. Timed events must be handled manually, where they need a call to start
  the event and another call to end the event. First call is used to start an internal
  timer which would continue counting until the second call is used to stop it
  and record the duration. This second call would end the timer, create an event
  with the given name and the with the duration from the timer and send it to the
  event queue. If this second call has not been called or if the app has been closed
  before calling it, no event would be created. As the timer is stored at the memory
  of the device, if you close the app before ending the event, you would have to
  start all over when you open the app later again.
</p>
<pre><code class="java">string eventName = "Some event";

//start some event with the event name "Some event"
Countly.Instance.StartEvent(eventName);
//wait some time

//end the event with the same event name "Some event"
Countly.Instance.EndEvent(eventName);</code></pre>
<p>
  <span>You may also provide additional information when ending an event. In that case, you can provide the segmentation, count, or sum values. The default values for those are "null", 1, and 0.</span>
</p>
<pre><code class="java">string eventName = "Some event";

//start some event
Countly.Instance.StartEvent(eventName);
//wait some time

Segmentation segmentation = new Segmentation();
segmentation.Add("wall", "orange");

//end the event while also providing segmentation information
Countly.Instance.EndEvent(eventName, segmentation);
</code></pre>
<p>Here are other options to end timed events:</p>
<pre><code class="java">//end the event while providing segmentation information and count
Countly.Instance.EndEvent("timed-event", segmentation, 4);<br><br>//end the event while providing segmentation information, count and sum
Countly.Instance.EndEvent("timed-event", segmentation, 4, 10);</code></pre>
<p>
  You may cancel an already started timed event in case it is not needed anymore:
</p>
<pre><code class="java">//start some event
Countly.Instance.StartEvent(eventName);
//wait some time

//cancel the event
Countly.Instance.CancelEvent(eventName);</code></pre>
<h2>Consent</h2>
<p>
  <span>This feature uses&nbsp;<code>Events</code>&nbsp;consent.&nbsp;</span><span>No additional events will be recorded if consent is required and not given.</span>
</p>
<p>
  <span>When consent is removed, all previously started timed events will be cancelled.</span>
</p>
<h1>Sessions</h1>
<h2>Manual Sessions</h2>
<p>
  After you have initiated the SDK, call
  <code>Countly.Instance.SessionBegin()</code> when you want to start tracking
  the user session. Usually, that is called in the entry point of the app.
</p>
<p>
  Call <code>Countly.Instance.SessionEnd()</code> before the app is closed to mark
  the end of the apps session.
</p>
<p>
  The SDK will send an update request every 60 seconds, to track how long the session
  is.
</p>
<p>
  That time is tracked using an internal timer. Some usage scenarios (like using
  the SDK in a console application) can prevent the timer from working. In those
  circumstances, you can manually call
  <code>Countly.Instance.SessionUpdate(elapsedTime)</code> to track the passage
  of time. You should still call it about every minute.
</p>
<pre><code class="csharp">//start the user session
Countly.Instance.SessionBegin();

//end the user session
Countly.Instance.SessionEnd();

//update the session manually
int elapsedTime = 60;//elapsed time in seconds
Countly.Instance.SessionUpdate(elapsedTime);</code></pre>
<h1>View Tracking</h1>
<h2>Manual View Recording</h2>
<p>
  The SDK provides a call to record views in your application. More information
  about how to use them can be found
  <a href="https://resources.count.ly/docs/view-analytics">here</a>. You only need
  to provide the name for the view.
</p>
<pre><code class="csharp">Countly.Instance.RecordView("Some View");</code></pre>
<h1>Device ID Management</h1>
<p>
  To link events, sessions, crashes, etc to a user, a deviceId is used. It is usually
  generated by the SDK. It is then saved locally and then reused on every init
  unless the developer supplies its own device Id.
</p>
<p>
  Ideally, the same device Id would be generated on the same device when using
  the same generation method. This way it would be possible to track users on reinstalls.
</p>
<h2>Device ID Generation</h2>
<p>
  The SDK supports multiple ways for generating that ID, each with its pro's and
  cons and some limited to a specific compilation target:
</p>
<ul>
  <li>
    <strong>cpuId</strong> - [net35, net40] (we recommend against using this)
    uses the OS-provided CPU id info to generate a hash that is used as an id.
    It should be possible to generate the same id on a reinstall if the CPU stays
    the same. On virtual machines and Windows 10 devices are not guaranteed to
    be unique and generate the same id and therefore device id conflicts
  </li>
  <li>
    <strong>multipleWindowsFields</strong> - [net35, net40] uses multiple OS-provided
    fields (CPU id, disk serial number, windows serial number, windows username,
    mac address) to generate a hash that would be used as the device Id. This
    method should regenerate the same id on a reinstall, provided those source
    fields do not change
  </li>
  <li>
    <strong>windowsGUID</strong> - [all platforms] generates a random GUID that
    will be used as a device id. Very high chance of being unique. Will generate
    a new id on a reinstall.
  </li>
  <li>
    <strong>developerSupplied</strong> - The device Id was provided by the developer.
    Used in cases where developers want to use an id tied to their internal systems/servers.
  </li>
</ul>
<p>
  Device id and generation method can be provided during SDK init. Those values
  can also bet not set, then the default method for that target will be used.
</p>
<pre><code class="csharp">//create the Countly init object
CountlyConfig cc = new CountlyConfig();
cc.serverUrl = "http://YOUR_SERVER";
cc.appKey = "YOUR_APP_KEY";
cc.appVersion = "1.2.3";
cc.developerProvidedDeviceId = "use@email.com";

//initiate the SDK with your preferences
Countly.Instance.Init(cc);</code></pre>
<h2>Changing Device ID</h2>
<p>
  <span>In case your application authenticates users, you might want to change the ID to the one in your backend after he has logged in. This helps you identify a specific user with a specific ID on a device he logs in, and the same scenario can also be used in cases this user logs in using a different way (e.g another tablet, another mobile phone, or web). In this case, any data stored in your Countly server database associated with the current device ID will be transferred (merged) into the user profile with the device id you specified in the following method call:</span>
</p>
<pre><span style="font-weight: 400;"><code class="java"><span class="pl-c1">Countly.Instance</span><span>.ChangeDeviceId("new-device-id", true);</span></code></span></pre>
<p>
  <span>You might want to track information about another separate user that starts using your app (changing apps account), or your app enters a state where you no longer can verify the identity of the current user (user logs out). In that case, you can change the current device ID to a new one without merging their data. You would call:</span>
</p>
<pre><span style="font-weight: 400;"><code class="java"><span class="pl-c1">Countly.Instance</span><span>.ChangeDeviceId("new-device-id", false);</span></code></span></pre>
<p>
  <span>Doing it this way, will not merge the previously acquired data with the new id.</span><span></span><span></span>
</p>
<div class="callout callout--warning">
  <p>
    <span style="font-weight: 400;">If the device ID is changed without merging and consent was enabled, all previously given consent will be removed. This means that all features will cease to function until new consent has been given again for that new device ID.</span>
  </p>
</div>
<p>
  <span>Do note that every time you change your deviceId without a merge, it will be interpreted as a new user. Therefore implementing id management in a bad way could inflate the users count by quite a lot.</span>
</p>
<h2>Retrieving Current Device ID</h2>
<p>
  You may want to see what device id Countly is assigning for the specific device.
  For that, you may use the following calls.
</p>
<pre><code class="java hljs">string usedId = await Countly.GetDeviceId();</code></pre>
<h1>User Location</h1>
<p>
  While integrating this SDK into your application, you might want to track your
  user location. You could use this information to better know your app’s user
  base. There are 4 fields that can be provided:
</p>
<ul>
  <li>Country code (two-letter ISO standard).</li>
  <li>City name (must be set together with the country code).</li>
  <li>
    Latitude and longitude values separated by a comma, e.g. "56.42345,123.45325".
  </li>
  <li>Your user’s IP address.</li>
</ul>
<h2>Setting Location</h2>
<div class="callout callout--warning">
  <p>
    Note that the IP address will only be updated if it was set during the init
    process.
  </p>
</div>
<p>
  During init, you can set location info in the configuration:
</p>
<pre>config.SetLocation(countryCode, city, gpsCoordinates, ipAddress);</pre>
<p>
  After SDK initialization, this location info will be sent to the server at the
  start of the user session. Use <code>SetLocation</code> method to disable or
  set the location at any time after the SDK Init call.
</p>
<p>For example:</p>
<pre><code class="csharp">//set user location
String gpsLocation = "63.445821, 10.898868";
String ipAddress = "13.56.33.12";
String country_code = "us";
String city = null;

Countly.Instance.SetLocation(gpsLocation, ipAddress, country_code, city);</code></pre>
<p>
  If there are fields you don't want to set, set them to null. If you're going
  to reset a field, set it to an empty string.
</p>
<p>
  If no location is provided, it will be approximated by using GeoIP.
</p>
<h2>Disabling Location</h2>
<p>
  Users might want to opt-out of location tracking. To do so call:
</p>
<pre><code class="csharp">//disable location tracking
Countly.Instance.DisableLocation();</code></pre>
<p>This will also erase all location info server side.</p>
<h1>User Profiles</h1>
<div class="callout callout--info">
  <p>
    This feature is available with an
    <a href="http://count.ly/enterprise-edition">Enterprise Edition</a> subscription.
    <span>For information about User Profiles, review&nbsp;</span><a href="http://resources.count.ly/docs/user-profiles"><span>this documentation</span></a><span>.</span>
  </p>
</div>
<h2>Setting Predefined Values</h2>
<p>
  The SDK allows you to upload specific data related to a user to the Countly server.
  You may set the following predefined data for a particular user:
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
    <strong>Picture</strong>: Web-based Url for the user’s profile.
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
  You can save info about user tracking data is related to. Countly provides
  <code>Countly.UserDetails</code> an object that exposes user-related properties
</p>
<p>
  Each time you change a property value, Countly syncs it with a server. If you
  set value as <code>null</code>, you will delete the property.
</p>
<p>Example:</p>
<pre><code>Countly.UserDetails.Name = "John";</code>// set name to John<br><code>Countly.UserDetails.Name = "null";</code> // remove name</pre>
<h2>Setting Custom Values</h2>
<p>
  The SDK gives you the flexibility to send only the custom data to Countly servers,
  even when you don’t want to send other user-related data.<span>&nbsp;<br></span>You
  can provide custom properties for user using <code>Custom</code> object
</p>
<pre><code>Countly.UserDetails.Custom.Add("city", "london");</code></pre>
<h2>Setting User Picture</h2>
<p>
  Additionally, you can upload a picture of the user to the server. Accepted picture
  formats are .png, .gif and .jpeg and picture will be resized to maximal 150x150
  dimensions.
</p>
<pre><code>Countly.UserDetails.UploadUserPicture(picture_stream);</code></pre>
<p>
  <strong>Note</strong>: dots (.) and dollar signs ($) in key names will be stripped
  out.
</p>
<h1>User Consent</h1>
<p>
  If you want to comply with GDPR or similar privacy requirements, there is functionality
  to manage user consent to features.
</p>
<p>
  More information about GDPR can be found
  <a href="https://blog.count.ly/countly-the-gdpr-how-worlds-leading-mobile-and-web-analytics-platform-can-help-organizations-5015042fab27">here</a>.
</p>
<h2>Setup During Init</h2>
<p>
  By default the requirement for consent is disabled. To enable it, you have to
  do it with the CountlyConfig object by setting <code>consentRequired</code> to
  <code>true</code>.
</p>
<pre><code class="csharp">//create the Countly init object
CountlyConfig cc = new CountlyConfig();
cc.serverUrl = "http://YOUR_SERVER";
cc.appKey = "YOUR_APP_KEY";

//enable consent
cc.consentRequired = true;

//initiate the SDK with your preferences
Countly.Instance.Init(cc);</code></pre>
<p>
  By default, no consent is given. That means that if no consent is enabled, Countly
  will not work and no network requests, related to features, will be sent. When
  the consent status of a feature is changed, that change will be sent to the Countly
  server.
</p>
<p>
  Consent for features is not persistent and will have to be set every time while
  initializing countly. Therefore the storage and persistence of given consent
  fall on the SDK integrator.
</p>
<p>
  Feature names in this SDK are stored as an enum called
  <code>ConsentFeatures</code>.
</p>
<p>Features currently supported by this SDK are:</p>
<ul>
  <li>
    sessions - tracking when, how often and how long users use your app
  </li>
  <li>events - allow sending events to the server</li>
  <li>location - allow sending location information</li>
  <li>crashes - allow tracking crashes, exceptions, and errors</li>
  <li>
    users - allow collecting/providing user information, including custom properties
  </li>
</ul>
<p>
  <span>In case consent is required, you may give consent to features before the SDK Init call. These features consents are not persistent and must be given on every restart.</span>
</p>
<pre><code class="csharp">//create the Countly init object
CountlyConfig cc = new CountlyConfig();
cc.serverUrl = "http://YOUR_SERVER";
cc.appKey = "YOUR_APP_KEY";

//enable consent
cc.consentRequired = true;

//set consent features
Dictionary&lt;ConsentFeatures, bool&gt; consent = new Dictionary&lt;ConsentFeatures, bool&gt;();
consent.Add(ConsentFeatures.Crashes, true);
consent.Add(ConsentFeatures.Events, false);
consent.Add(ConsentFeatures.Location, true);
consent.Add(ConsentFeatures.Sessions, false);
consent.Add(ConsentFeatures.Users, false);
cc.givenConsent = consent;

//initiate the SDK with your preferences
Countly.Instance.Init(cc);</code></pre>
<h2>Changing Consent</h2>
<p>
  Consent can also be changed at any other moment in the app after init:
</p>
<pre><code class="csharp">//preparing consent features
Dictionary&lt;ConsentFeatures, bool&gt; consent = new Dictionary&lt;ConsentFeatures, bool&gt;();
consent.Add(ConsentFeatures.Crashes, true);
consent.Add(ConsentFeatures.Events, false);
consent.Add(ConsentFeatures.Location, true);

//changing consent
Countly.Instance.SetConsent(consent);</code></pre>
<h1>Other Features and Notes</h1>
<h2>SDK Config Parameters Explained</h2>
<p>
  <span>To change the Configuration, update the values of parameters in the "<code class="csharp">CountlyConfig</code></span><strong><span>&nbsp;</span></strong><span>object. Here are the details of the optional parameters:</span><span></span>
</p>
<p>
  <span><strong>developerProvidedDeviceId -&nbsp;</strong>(Optional, string) Your Device ID. It is an optional parameter.&nbsp;<strong>Example:</strong>&nbsp;f16e5af2-8a2a-4f37-965d-qwer5678ui98.</span>
</p>
<p>
  <span><strong>consentRequired-&nbsp;</strong>(Optional, bool)&nbsp;This is useful&nbsp;during the app run when the user wants to opt-out of SDK features.</span>
</p>
<p>
  <span><strong>sessionUpdateInterval -</strong>&nbsp;(Optional, int)&nbsp;Sets the interval (in seconds) after which the application will automatically extend the session. The default value is<strong>&nbsp;60&nbsp;</strong>(seconds).</span>
</p>
<h2>SDK Internal Limits</h2>
<p>
  SDK does have configurable fields to manipulate the internal SDK value and key
  limits. If values or keys provided by the user, would exceed the limits, they
  would be truncated. Here are the details of these configurable fields:<span></span>
</p>
<p>
  <span><strong>MaxKeyLength -&nbsp;</strong>(int) Maximum size of all string keys. The default value is&nbsp;<strong>128</strong>.&nbsp;</span>
</p>
<p>
  <span><strong>MaxValueLength - </strong>(int) Maximum size of all values in our key-value pairs. The default value is <strong>256</strong>.&nbsp;</span>
</p>
<p>
  <span><strong>MaxSegmentationValues - </strong>(int) Max amount of custom (dev provided) segmentation in one event. The default value is <strong>256</strong>.&nbsp;</span>
</p>
<p>
  <span><strong>MaxStackTraceLinesPerThread - </strong>(int) Limits how many stack trace lines would be recorded per thread. The default value is <strong>30</strong>.&nbsp;</span>
</p>
<p>
  <span><strong>MaxStackTraceLineLength - </strong>(int) Limits how many characters are allowed per stack trace line. The default value is <strong>200</strong>.</span>
</p>
<p>
  <span><strong>MaxBreadcrumbCount - </strong>(int)maximum amount of breadcrumbs. The default value is <strong>100</strong>.</span>
</p>
<h1>FAQ</h1>
<h2>What Information Is Collected by the SDK</h2>
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
  - Screen resolution<br>
  - Screen density<br>
  - OS name<br>
  - OS version<br>
  - App version<br>
  <span>- Locale identifier</span>
</p>
<p>
  * When events are recorded, the following information collected:<br>
  - Time of event<br>
  - Current hour<br>
  - Current day of week
</p>
<p>
  <span>* If crash tracking is enabled, it will collect the following information at the time of the crash:<br>- OS name<br>- OS version</span><br>
  <span>- Device resolution<br>- App version<br>- Time of the crash<br>- Crash stack trace<br>- Error description<br>- Total RAM</span><br>
  <span>- If there is a network connection<br></span>
</p>
<p>
  <span>Any other information like data in events, location, user profile information, or other manual requests depends on what the developer decides to provide and is not collected by the SDK itself.</span>
</p>
