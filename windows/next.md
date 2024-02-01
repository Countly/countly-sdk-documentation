<p>
  This documentation is for the Countly Windows SDK version 24.1.X. The SDK source
  code repository can be found
  <a href="https://github.com/Countly/countly-sdk-windows" target="_blank" rel="noopener noreferrer">here.</a>
</p>
<div class="callout callout--info">
  <p>
    Click
    <a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-and-Installing-SDKs#h_01H9QCP8G8HMBBT2NPHFJPJ3KX" target="_self" rel="undefined">here, </a>to
    access the documentation for older SDK versions.
  </p>
</div>
<div>
  <p>
    The Countly Windows SDK implements the following explicit flavors:
  </p>
  <ul>
    <li>.NET Standard 2.0</li>
    <li>
      <span>.NET Framework 3.5</span>
    </li>
    <li>
      <span>.NET Framework 4.5</span>
    </li>
  </ul>
</div>
<p>
  To examine example integrations please have a look
  <a href="#h_01HNFMRRC2N7DE6WB88PJ8DXA4">here.</a>
</p>
<h1 id="h_01HABTXQF7822Y2MQ0PHE8ARYH">Adding the SDK to the Project</h1>
<p>
  <span>To install the package, you can use either the NuGet Package Manager or the Package Manager Console. When you install a package, NuGet records the dependency, either in your project file or a </span><code>packages.config</code><span> file (depending on the project format).</span>
</p>
<ol>
  <li>
    In Solution Explorer, right-click <strong>References</strong> and choose
    <strong>Manage NuGet Packages</strong>.<img src="/guide-media/01GVCYFBRGSZYF4M2CSKYHNDKH" alt="image-NuGet-packages.png">
  </li>
  <li>
    <span>Choose "nuget.org" as the </span><strong>Package source</strong><span>, select the </span><strong>Browse</strong><span> tab, search for </span><strong>Countly</strong><span>, select that package in the list, and select </span><strong>Install</strong><span>:<img src="/guide-media/01GVCYFDE9NW6731PFC2C4BMPW" alt="mceclip0.png"></span>
  </li>
  <li>
    <p>Accept any license prompts.</p>
  </li>
</ol>
<h1 id="h_01HABTXQF7MZ5YDN38PTFQ6B4K">SDK Integration</h1>
<p class="anchor-heading">
  Before you can use any Countly functionality, you need to call
  <code>Countly.Instance.Init</code> to initiate the SDK.
</p>
<h2 id="h_01HABTXQF7GE3ZK9NC41QE68ME">Minimal Setup</h2>
<p>
  <span>The shortest way to initiate the SDK is with this call:</span>
</p>
<pre><code class="csharp">//create the Countly init object
CountlyConfig cc = new CountlyConfig();
cc.serverUrl = "https://xxx.count.ly";
cc.appKey = "YOUR_APP_KEY";
cc.appVersion = "1.2.3";

//initiate the SDK with your preferences
Countly.Instance.Init(cc);</code></pre>
<p>
  <span>In the </span><code>CountlyConfig</code><span> object, you provide appKey and your Countly server URL. Please check <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KX44C9SF48WRPQNCP3">here</a> for more information on how to acquire your application key (APP_KEY) and server URL.</span>
</p>
<p>
  <strong>Note: </strong>The SDK targets multiple profiles. Therefore for some
  of them, there are feature differences. Either with additional function calls
  or with additional fields in the CountlyConfig object.
</p>
<div class="callout callout--info">
  <p>
    If you are in doubt about the correctness of your Countly SDK integration
    you can learn about the verification methods from
    <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KXE6YKVETHDWPP8J3K" target="blank">here</a>.
  </p>
</div>
<h2 id="h_01HABTXQF7QV573QQXWM8HWVX3">SDK Logging / Debug Mode</h2>
<p>
  <span>The first thing you should do while integrating our SDK is to enable logging. If logging is enabled, then our SDK will print out debug messages about its internal state and encounter problems.</span>
  To enable logging you need to do the following two steps:
</p>
<p>
  <strong>Step 1</strong>: Enable SDK logging using the following call:
</p>
<pre><code class="csharp hljs">    Countly.IsLoggingEnabled = <span class="hljs-literal">true</span>;</code></pre>
<p>You can turn it on and off in any place of your code.</p>
<p>
  <strong>Step 2</strong>:
  <span>Go to project properties, select the 'Build' tab and make sure the following things are correct.</span>
</p>
<ul>
  <li>Configuration: Debug</li>
  <li>"Define DEBUG constant" is checked</li>
</ul>
<p>
  <img src="/guide-media/01GVCPMRRT2Q54RB6JHN86D4C0" alt="mceclip1.png">
</p>
<p>
  Log messages written in the application will show up in 'Output' windows.
</p>
<p>
  <img src="/guide-media/01GVBACGEX9MG9X2GKY88G83GS" alt="mceclip4.png">
</p>
<h2 id="h_01HABTXQF79D0GQFAPY6K8C37H">SDK Data Storage</h2>
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
<h2 id="h_01HABTXQF7WJC67B24Q8DGE9PF">SDK Notes</h2>
<h3 id="h_01HABTXQF7K6MEWFKJR5D5GVPR">Additional Info for UWP Project Setup</h3>
<p>
  It's possible to register an unhandled crash handler during SDK initialization.
  To do that, you need to provide a link to your application.
</p>
<pre><code class="csharp">var cc = new CountlyConfig
{
  serverUrl = "SERVER_URL",
  appKey = "APP_KEY",
  appKey = "XXXXXXXXXXXXXXXXXXXXXXXXXXXX",
  appVersion = "1.2.3",
  application = referenceToApplication //provide link to your application
};

await Countly.Instance.Init(cc);</code></pre>
<h1 id="h_01HABTXQF82Z61FH639NC5FGSV">Crash Reporting</h1>
<p>
  <span>The Countly SDK for Windows can collect </span><a href="http://resources.count.ly/docs/introduction-to-crash-reporting-and-analytics"><span>Crash Reports</span></a><span>,</span><span> which you may examine and resolve later on the server.</span>
</p>
<h2 id="h_01HABTXQF8Y0RYTXQBPQB8S4T5">Automatic Crash Handling</h2>
<p>
  Automatic crash handling is possible if the project type / platform target supports
  a unhandled exception handler.
</p>
<p>
  In that case you would subscribe to that and report the collected errors/exception
  to the Countly SDK.
</p>
<p>
  Exception details and device properties would be sent on the next app launch.
</p>
<h2 id="h_01HABTXQF8WV6H2G2XNWXNTFBT">Handled Exceptions</h2>
<p>
  <span>You might catch an exception or similar error during your app’s runtime. </span><span>You may also log these handled exceptions to monitor how and when they are happening. </span><span>To log exceptions use the following code snippet:</span>
</p>
<pre><code class="csharp">Dictionary&lt;string, string&gt; customInfo = new Dictionary&lt;string, string&gt;{
  { "customData", "importantStuff" }
};

try {
  throw new Exception("It is an exception");
} catch (Exception ex) {
  Countly.RecordException(ex.Message, ex.StackTrace, customInfo, false);
}</code></pre>
<p>Here is the detail of the parameters:</p>
<ul>
  <li>
    <strong>error -</strong><span> A</span> string that contains a detailed description
    of the exception.
  </li>
  <li>
    <strong>stackTrace -</strong><span> </span>A string that describes the contents
    of the call stack.
  </li>
  <li>
    <strong>customInfo -<span> </span></strong>Custom key/values to be reported.
  </li>
  <li>
    <strong>unhandled -</strong> (bool) Set false if the error is fatal.
  </li>
</ul>
<p>
  <span>If you have handled an exception and it turns out to be fatal to your app, you may use the following calls:</span>
</p>
<pre><code><strong>Countly</strong>.RecordUnhandledException(ex.Message, ex.StackTrace, customInfo, true);</code></pre>
<h2 id="h_01HABTXQF8XYTZNNY07Z52XPDR">Crash Breadcrumbs</h2>
<p>
  Throughout your app, you can leave crash breadcrumbs
  <span>Mandatory that </span>would describe previous steps that were taken in
  your app before the crash. After a crash happens, they will be sent together
  with the crash report.
</p>
<p>The following command adds a crash breadcrumb:</p>
<pre><code class="csharp">Countly.Instance.AddCrashBreadCrumb("breadcrumb");</code></pre>
<h2 id="h_01HABTXQF8BRT1FY1PR381RVJV">Consent</h2>
<p>
  This feature uses <code>Crashes</code><span> consent. No additional crash logs will be recorded if consent is required and not given.</span>
</p>
<h1 id="h_01HABTXQF8MKDPZ7J8JRS7AAEJ">Events</h1>
<p>
  <span>An </span><a href="http://resources.count.ly/docs/custom-events"><span>event</span></a><span> is any type of action that you can send to a Countly instance, e.g. purchases, changed settings, view enabled, and so on, letting you get valuable information about your application.</span>
</p>
<p>
  <span>There are a couple of values that can be set when recording an event. The main one is the <strong>key</strong> property which would be the identifier/name for that event. For example, in case a user purchased an item in a game, you could create an event with the key 'purchase'.</span>
</p>
<p>
  <span>Optionally there are also other properties that you might want to set:</span>
</p>
<ul>
  <li>
    <strong>Count -</strong> a whole numerical value that marks how many times
    this event has happened. The default value for that is <strong>1</strong>.
  </li>
  <li>
    <strong>Sum -</strong> This value would be summed across all events in the
    dashboard. F<span>or example, in-app purchase events sum of purchased items. Its default value is <strong>null</strong>.</span>
  </li>
  <li>
    <strong>Duration - </strong>Used to record and track the duration of events.
    The default value is<span> </span><strong>null</strong>.
  </li>
  <li>
    <strong>Segmentation- </strong>A value where you can provide custom segmentation
    for your events to track additional information. It is a key and value map.
    The accepted data types for the value are <span>"String".</span>
  </li>
</ul>
<h2 id="h_01HABTXQF8CACQNG6DNTEMRJA2">Recording Events</h2>
<p>
  <span>Here is a quick way to </span><span>record an event:</span>
</p>
<pre><code class="csharp">Countly.RecordEvent("event-key");</code></pre>
<p>
  <span>Based on the example below of an event recording a <strong>purchase</strong>, h</span><span>ere is a quick summary of the information for each usage:</span>
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
<h2 id="h_01HABTXQF92CFPQMRB9MV411MM">Timed Events</h2>
<p>
  Timed events are events which gives you the ability to calculate the duration
  it takes for an event to take place with respect to any arbitrary point you choose.
  Timed events must be handled manually, where they need a call to start the event
  and another call to end the event. First call is used to start an internal timer
  which would continue counting until the second call is used to stop it and record
  the duration. This second call would end the timer, create an event with the
  given name and the with the duration from the timer and send it to the event
  queue. If this second call has not been called or if the app has been closed
  before calling it, no event would be created. As the timer is stored at the memory
  of the device, if you close the app before ending the event, you will have to
  start all over when you open the app later again.
</p>
<pre><code class="csharp">string eventName = "Some event";

//start some event with the event name "Some event"
Countly.Instance.StartEvent(eventName);
//wait some time

//end the event with the same event name "Some event"
Countly.Instance.EndEvent(eventName);</code></pre>
<p>
  <span>You may also provide additional information when ending an event. In that case, you can provide the segmentation, count, or sum values. The default values for those are "null", 1, and 0.</span>
</p>
<pre><code class="csharp">string eventName = "Some event";

//start some event
Countly.Instance.StartEvent(eventName);
//wait some time

Segmentation segmentation = new Segmentation();
segmentation.Add("wall", "orange");

//end the event while also providing segmentation information
Countly.Instance.EndEvent(eventName, segmentation);
</code></pre>
<p>Here are other options to end timed events:</p>
<pre><code class="csharp">//end the event while providing segmentation information and count
Countly.Instance.EndEvent("timed-event", segmentation, 4);<br><br>//end the event while providing segmentation information, count and sum
Countly.Instance.EndEvent("timed-event", segmentation, 4, 10);</code></pre>
<p>
  You may cancel an already started timed event in case it is not needed anymore:
</p>
<pre><code class="csharp">//start some event
Countly.Instance.StartEvent(eventName);
//wait some time

//cancel the event
Countly.Instance.CancelEvent(eventName);</code></pre>
<h2 id="h_01HABTXQF9ZWR02CQHMJ74Y497">Consent</h2>
<p>
  <span>This feature uses <code>Events</code> consent. </span><span>No additional events will be recorded if consent is required and not given.</span>
</p>
<p>
  <span>When consent is removed, all previously started timed events will be cancelled.</span>
</p>
<h1 id="h_01HABTXQF9T19CW94K1JKR0T4S">Sessions</h1>
<h2 id="h_01HABTXQF9W6WKTVV7X61DCC7Q">Manual Sessions</h2>
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
<h1 id="h_01HABTXQF9CRMPFGV4SVBTDZ7A">View Tracking</h1>
<h2 id="h_01HABTXQF9ND3P0REY072BVGFA">Manual View Recording</h2>
<p>
  The SDK provides a call to record views in your application. More information
  about how to use them can be found
  <a href="https://resources.count.ly/docs/view-analytics">here</a>. You only need
  to provide the name for the view.
</p>
<pre><code class="csharp">Countly.Instance.RecordView("Some View");</code></pre>
<h1 id="h_01HABTXQF9BT70PJB4WDD4DEA8">Device ID Management</h1>
<p>
  To link events, sessions, crashes, etc to a user, a deviceId is used. It is usually
  generated by the SDK. It is then saved locally and then reused on every init
  unless the developer supplies its own device Id.
</p>
<p>
  Ideally, the same device Id would be generated on the same device when using
  the same generation method. This way it would be possible to track users on reinstalls.
</p>
<h2 id="h_01HABTXQF98TYMFMDYV6H6NG0S">Device ID Generation</h2>
<p>
  The SDK supports multiple ways for generating that ID, each with its pro's and
  cons and some limited to a specific compilation target:
</p>
<ul>
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
<h2 id="h_01HABTXQF9N0EKQNJ65GX4DMRA">Changing Device ID</h2>
<p>
  <span>In case your application authenticates users, you might want to change the ID to the one in your backend after he has logged in. This helps you identify a specific user with a specific ID on a device he logs in, and the same scenario can also be used in cases this user logs in using a different way (e.g another tablet, another mobile phone, or web). In this case, any data stored in your Countly server database associated with the current device ID will be transferred (merged) into the user profile with the device id you specified in the following method call:</span>
</p>
<pre><code class="csharp">Countly.Instance.ChangeDeviceId("new-device-id", true);</code></pre>
<p>
  <span>You might want to track information about another separate user that starts using your app (changing apps account), or your app enters a state where you no longer can verify the identity of the current user (user logs out). In that case, you can change the current device ID to a new one without merging their data. You would call:</span>
</p>
<pre><code class="csharp">Countly.Instance.ChangeDeviceId("new-device-id", false);</code></pre>
<p>
  <span>Doing it this way, will not merge the previously acquired data with the new id.</span>
</p>
<div class="callout callout--warning">
  <p>
    <span style="font-weight: 400;">If the device ID is changed without merging and consent was enabled, all previously given consent will be removed. This means that all features will cease to function until new consent has been given again for that new device ID.</span>
  </p>
</div>
<p>
  <span>Do note that every time you change your deviceId without a merge, it will be interpreted as a new user. Therefore implementing id management in a bad way could inflate the users count by quite a lot.</span>
</p>
<h2 id="h_01HABTXQF9503C704R080YHTW2">Retrieving Current Device ID</h2>
<p>
  You may want to see what device id Countly is assigning for the specific device.
  For that, you may use the following calls.
</p>
<pre><code class="java hljs">string usedId = await Countly.GetDeviceId();</code></pre>
<h1 id="h_01HABTXQF9MFA0FMGZM3NA6M7R">User Location</h1>
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
<h2 id="h_01HABTXQF9H5DVANBT6M9392CA">Setting Location</h2>
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
<h2 id="h_01HABTXQF9PCKAN9GTXXYHBAAJ">Disabling Location</h2>
<p>
  Users might want to opt-out of location tracking. To do so call:
</p>
<pre><code class="csharp">//disable location tracking
Countly.Instance.DisableLocation();</code></pre>
<p>This will also erase all location info server side.</p>
<h1 id="h_01HABTXQF9JJKC5F91FNMKHNT5">User Profiles</h1>
<div class="callout callout--info">
  <p>
    This feature is available with an
    <a href="http://count.ly/enterprise-edition">Enterprise Edition</a> subscription.
    <span>For information about User Profiles, review </span><a href="http://resources.count.ly/docs/user-profiles"><span>this documentation</span></a><span>.</span>
  </p>
</div>
<h2 id="h_01HABTXQF97FBAZ6G2CV89E6DE">Setting Predefined Values</h2>
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
<pre><code class="csharp">// set name to John
Countly.UserDetails.Name = "John";
// remove name
Countly.UserDetails.Name = "null";</code></pre>
<h2 id="h_01HABTXQFAE25QX52WCAG0Y15M">Setting Custom Values</h2>
<p>
  The SDK gives you the flexibility to send only the custom data to Countly servers,
  even when you don’t want to send other user-related data.<span> <br></span>You
  can provide custom properties for user using <code>Custom</code> object
</p>
<pre><code>Countly.UserDetails.Custom.Add("city", "london");</code></pre>
<h2 id="h_01HABTXQFA5N0RPJ216SVSXK2B">Setting User Picture</h2>
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
<h1 id="h_01HABTXQFA0BSMZM04KRSMDVAP">User Consent</h1>
<p>
  If you want to comply with GDPR or similar privacy requirements, there is functionality
  to manage user consent to features.
</p>
<p>
  More information about GDPR can be found
  <a href="https://medium.com/countly/countly-the-gdpr-how-worlds-leading-mobile-and-web-analytics-platform-can-help-organizations-5015042fab27">here</a>.
</p>
<h2 id="h_01HABTXQFAP9PK4A5DBEXYNBK5">Setup During Init</h2>
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
  initializing countly. Therefore, the storage and persistence of given consent
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
<h2 id="h_01HABTXQFA70V164HWZN0FHRNE">Changing Consent</h2>
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
<h1 id="h_01HABTXQFAD7RRPHNVJT9XDF6X">Other Features and Notes</h1>
<h2 id="h_01HABTXQFA9FYPT9FFRADPMMF8">SDK Config Parameters Explained</h2>
<p>
  <span>To change the Configuration, update the values of parameters in the "<code class="csharp">CountlyConfig</code></span>
  <span>object. Here are the details of the optional parameters:</span>
</p>
<p>
  <span><strong>developerProvidedDeviceId - </strong>(Optional, string) Your Device ID. It is an optional parameter. <strong>Example:</strong> f16e5af2-8a2a-4f37-965d-qwer5678ui98.</span>
</p>
<p>
  <span><strong>consentRequired- </strong>(Optional, bool) This is useful during the app run when the user wants to opt-out of SDK features.</span>
</p>
<p>
  <span><strong>sessionUpdateInterval -</strong> (Optional, int) Sets the interval (in seconds) after which the application will automatically extend the session. The default value is<strong> 60 </strong>(seconds).</span>
</p>
<h2 id="h_01HNFMRRC2N7DE6WB88PJ8DXA4">Example Integrations</h2>
<p>
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/net35">net35</a>
  solution contains 3 project that are implemented with Net Framework 3.5<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/net35/CountlySample">CountlySample</a>
  project is a console application that covers most of the functionalities.<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/net35/CountlySampleWindowsForm">CountlySampleWindowsForm</a>
  project is a Windows Form application that covers basic<br>
  functionalities.<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/net35/CountlyTestBackendMode">CountlyTestBackendMode</a>
  project is a Windows Form application that covers events in<br>
  Backend Mode.
</p>
<p>
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/net45">net45</a>
  solution contains 6 project that are implemented with Net Framework 4.5<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/net45/CountlySampleAspNet">CountlySampleAspNet</a>
  project is a AspNet application that covers basic functionalities.<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/net45/CountlySampleAspNetMVC">CountlySampleAspNetMVC</a>
  project is a AspNet MVC application that covers basic<br>
  functionalities.<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/net45/CountlySampleWPF">CountlySampleWPF</a>
  project is a WPF application that covers basic functionalities.<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/net45/countlySampleConsole">countlySampleConsole</a>
  project is a console application that covers most of the functionalities.<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/net45/CountlySampleWIndowsForm">CountlySampleWindowsForm</a>
  project is a Windows Form application that covers basic<br>
  functionalities.<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/net45/CountlyTestBackendMode">CountlyTestBackendMode</a>
  project is a Windows Form application that covers events in<br>
  Backend Mode.
</p>
<p>
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/netstd">netstd</a>
  solution contains 5 project that are implemented with Net Standard 2.0<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/netstd/CountlySampleWPF">CountlySampleWPF</a>
  project is a WPF application that covers basic functionalities.<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/netstd/CountlySampleUWP">CountlySampleUWP</a>
  project is a UWP application that covers basic functionalities.<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/netstd/CountlyTestBackendMode">CountlyTestBackendMode</a>
  project is a Windows Form application that covers events in<br>
  Backend Mode<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/netstd/MauiSampleApp">MauiSampleApp</a>
  project is a MAUI application that covers basic functionalities.<br>
  -
  <a href="https://github.com/Countly/countly-sdk-windows/tree/master/netstd/MauiSampleAppNativeIntegrations">MauiSampleAppNativeIntegrations</a>
  projects is a MAUI application demonstration of native crash reporting
</p>
<h2 id="h_01HABTXQFAHAQTRDWQ0YVM3VX4">SDK Internal Limits</h2>
<p>
  SDK does have configurable fields to manipulate the internal SDK value and key
  limits. If values or keys provided by the user, would exceed the limits, they
  would be truncated. Here are the details of these configurable fields:
</p>
<p>
  <span><strong>MaxKeyLength - </strong>(int) Maximum size of all string keys. The default value is <strong>128</strong>. </span>
</p>
<p>
  <span><strong>MaxValueLength - </strong>(int) Maximum size of all values in our key-value pairs. The default value is <strong>256</strong>. </span>
</p>
<p>
  <span><strong>MaxSegmentationValues - </strong>(int) Max amount of custom (dev provided) segmentation in one event. The default value is <strong>256</strong>. </span>
</p>
<p>
  <span><strong>MaxStackTraceLinesPerThread - </strong>(int) Limits how many stack trace lines would be recorded per thread. The default value is <strong>30</strong>. </span>
</p>
<p>
  <span><strong>MaxStackTraceLineLength - </strong>(int) Limits how many characters are allowed per stack trace line. The default value is <strong>200</strong>.</span>
</p>
<p>
  <span><strong>MaxBreadcrumbCount - </strong>(int)maximum amount of breadcrumbs. The default value is <strong>100</strong>.</span>
</p>
<h2 id="h_01HJT9W4R283JCJNXZJM0C42VQ">Custom Metrics</h2>
<div class="callout callout--warning">
  <p>This functionality is available since SDK version 24.1.0.</p>
</div>
<p>
  During some specific circumstances, like beginning a session or requesting remote
  config, the SDK is sending device metrics.
</p>
<p>
  It is possible for you to either override the sent metrics (like the application
  version for some specific variant) or provide either your own custom metrics.
  If you are providing your own custom metrics, you would need your own custom
  plugin server-side which would interpret it appropriately. If there is no plugin
  to handle those custom values, they will be ignored.
</p>
<div>
  <pre><code class="csharp">IDictionary&lt;string, string&gt; metricOverride = new Dictionary&lt;string, string&gt;();
metricOverride["SomeKey"] = "123";
metricOverride["_locale"] = "xx_yy";

//create the Countly init object 
CountlyConfig cc = new CountlyConfig(); 
cc.serverUrl = "http://YOUR_SERVER"; 
cc.appKey = "YOUR_APP_KEY";
cc.SetMetricOverride(metricOverride);

//initiate the SDK with your preferences 
Countly.Instance.Init(cc);
</code></pre>
</div>
<p>
  For more information on the specific metric keys used by Countly, check
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305#h_01HABT18WWYQ2QYPZY3GHZBA9B" target="_self">here</a>.
</p>
<h2 id="h_01HHHE4NG1BWB112A9F7AYF93M">
  <span>Backend Mode</span>
</h2>
<p>
  <span>Backend mode allows sending requests with minimal SDK overhead and with the ability to control to which device ID to attribute the recorded data on a per data point level.</span>
</p>
<p>
  <span>This feature allows also a fine grain control over to which Countly app the data should be sent.</span>
</p>
<p>
  <span>Backend mode is mainly intended for server/backend use cases.</span>
</p>
<p>
  <span>When backend mode is enabled other SDK calls will be ignored. </span>
</p>
<p>
  <span>When in backend mode, nothing is saved persistently and everything is stored only in memory.</span>
</p>
<p>
  <span>The backend mode does not have checksum ability.</span>
</p>
<h3 id="h_01HHHV17XPBGMMDAM2HW82QX65">
  <span>Enabling Backend Mode</span>
</h3>
<p>
  <span>To enable backend mode you need to call "EnableBackendMode" :</span>
</p>
<pre><code class="csharp">CountlyConfig cc = new CountlyConfig();
cc.serverUrl = "YOUR_SERVER_URL";
cc.appKey = "ONE_OF_YOUR_APP_KEYS";
cc.appVersion = "APP_VERSION";
cc.EnableBackendMode();
await Countly.Instance.Init(cc);</code></pre>
<p>You would also provide the default appKey.</p>
<p>
  For more information on backend mode configuration options, check bellow.
</p>
<h3 id="h_01HHHV1KDXJNM5FJ8T9KHRB0ZZ">
  <span>Recording Data</span>
</h3>
<p>
  <span>For each call, deviceId parameter is mandatory and should be provided. appKey parameter is optional. However, if multi app recording is intended it should be provided. </span>
</p>
<p>
  <span>If app key is not provided, it fallbacks to given app key while initializing.</span>
</p>
<h4 id="h_01HJQQ9QE1Y5BS2YKW5FYQYPVF">
  <span>Crash Reporting</span>
</h4>
<p>
  <span>To report a crash with backend mode this method should be called:</span>
</p>
<pre><code class="csharp">Countly.Instance.BackendMode().RecordException(string deviceId, string error, string stackTrace = null, IList&lt;string&gt; breadcrumbs = null, IDictionary&lt;string, object&gt; customInfo = null, IDictionary&lt;string, string&gt; metrics = null, bool unhandled = false, string appKey = null, long timestamp = 0);</code></pre>
<p>
  <span>For this function to work, only error parameter is required. </span>
</p>
<p>
  <span>Keep in mind that if you want to send data for a device ID or app key that differs from the ones given during the SDK initialization, you must provide them in the function. Here is a minimal call:</span>
</p>
<pre><code class="csharp">Countly.Instance.BackendMode().RecordException(DEVICE_ID, "Exception");</code></pre>
<p>
  <span>Because there is a possibility to multi device recording, metrics also should be provided if metric recording is intended. Here is the supported metric keys:</span>
</p>
<pre><span>"_os", "_os_version", "_ram_total", "_ram_current", "_disk_total", "_disk_current", "_online", "_muted", "_resolution", "_app_version", "_manufacture", "_device", "_orientation", "_run"</span></pre>
<p>
  <span>Optional values:</span>
</p>
<p>
  <span> - <strong>stackTrace</strong>: if not provided it will be not sent to the server</span>
</p>
<p>
  <span> - <strong>breadcrumbs</strong>: if not provided it will be not sent to the server</span>
</p>
<p>
  <span> - <strong>customInfo</strong>: custom segmentation of a crash, if not provided it will be not sent to the server. Supported values for the custom info are int, float, double, long, string and bool.</span>
</p>
<p>
  <span> - <strong>metrics</strong>: if not provided it will be not sent to the server</span>
</p>
<p>
  <span> - <strong>unhandled</strong>: if not provided it will be recorded as a handled crash. If unhandled crash reporting is intended true value should be passed to the parameter, ex. unhandled: true</span>
</p>
<p>
  <span> - <strong>timestamp</strong>: if not provided, it will be set as current timestamp, ex. timestamp: 1703752478530</span>
</p>
<p>
  <span>Here is a set of examples:</span>
</p>
<pre><code class="csharp">// unhandled crash reporting with metrics
var metrics = new Dictionary&lt;string, string&gt;(){
  {"_os", "Windows"},
  {"_os_version", "Windows10NT"},
  {"_run", "5678"},
  {"_bat", "67"},
  {"_ram_total", "1024"},
};

Countly.Instance.BackendMode().RecordException(DEVICE_ID, "Exception", unhandled: true, metrics: metrics, appKey: APP_KEY);

// crash reporting with all params provided and custom segmentation
var customSegmentation = new Dictionary&lt;string, string&gt;(){
  {"level", 65},
  {"build_version", "45fA2022"},
  {"critical_point", -5.4E-79},
  {"timestamp", 1703752478530},
  {"done", true},
  {"percent", 0.67}
};
var stackTrace = ... // gather stack trace
var breadCrumbs = new List&lt;string&gt; { "Before Init", "After Init" };
  
Countly.Instance.BackendMode().RecordException(DEVICE_ID, "Exception", stackTrace, breadCrumbs, customSegmentation, metrics, appKey: APP_KEY);
  
// if needed you can also provide timestamp of the exception by adding timestamp to the call, if you do not provide it will be set as current timestamp
Countly.Instance.BackendMode().RecordException(DEVICE_ID, "Exception", appKey: APP_KEY, timestamp: 1703752478530);
</code></pre>
<h4 id="h_01HHHEEY3AHKR4XQD22DF8JQKJ">
  <span>Events</span>
</h4>
<p>
  <span>To record an event with backend mode this method should be called:</span>
</p>
<pre><span>Countly.Instance.BackendMode().RecordEvent(string deviceId, string eventKey, Segmentation segmentations = null, int count = 1, double? sum = null, long? duration = null, string appKey = null, long timestamp = 0);</span></pre>
<p>
  Here are some examples for recording event with the backend mode:
</p>
<pre><code class="csharp">BackendMode bm = Countly.Instance.BackendMode(); // for convenient calling
bm.RecordEvent("device1", "event1", appKey: "app1");
Segmentation segmentation = new Segmentation();
segmentation.Add("uid", "2873673");
long timestamp = 1702467348;
bm.RecordEvent("device2", "event2", segmentation, 2, 8.02, 30, "app2", timestamp);
bm.RecordEvent("device3", "event3", segmentation, appKey: "app3"); // timestamp will be set as current timestamp </code></pre>
<h4 id="h_01HJQSGRAM1WV3N6VBVS74EADS">Sessions</h4>
<p>
  Also sessions can be tracked with the Backend Mode. There are "BeginSession",
  "UpdateSession" and "EndSession" methods.
</p>
<p>
  <strong>Begin Session</strong>
</p>
<pre><code class="csharp">Countly.Instance.BackendMode().BeginSession(string deviceId, string appKey = null, IDictionary&lt;string, string&gt; metrics = null, IDictionary&lt;string, string&gt; location = null, long timestamp = 0);</code></pre>
<p>
  If no metrics are provided for the BeginSession, it fallbacks to internal metrics
  collected from the current device.
</p>
<p>
  Location can be also tracked with providing location parameter of the function.
  A device's location information can only be tracked with BeginSession call in
  backend mode.
</p>
<p>
  If language and country information would like to be tracked, _locale metric
  must be provided with the BeginSession method.
</p>
<p>Here are examples about BeginSession method.</p>
<pre><code class="csharp">// minimal call to the BeginSession, this fallbacks to internal metrics and app key
Countly.Instance.BackendMode().BeginSession(DEVICE_ID);

// With custom metrics, location and custom timestamp (timestamp is optional, if not provided, it will be set as current)
var metrics = new Dictionary&lt;string, string&gt;(){
  {"_os", "Windows"},
  {"_os_version", "Windows10NT"},
  {"_locale", "en-US"},
  {"_resolution", "256x256"},
  {"_device", "ETab 4"},
  {"_carrier", "X-mobile"},
  {"_app_version", "1.0"},
};

var location = new Dictionary&lt;string, string&gt;(){
  {"location", "-0.3720234014105792,-159.99741809049596"},
  {"ip", "1.1.1.1"},
  {"city", "New York"},
  {"country_code", "DEU"} // iso country code
};
Countly.Instance.BackendMode().BeginSession(DEVICE_ID, APP_KEY, metrics, location, 1703752478530);</code></pre>
<p>
  <strong>Update Session</strong>
</p>
<p>
  Duration is in seconds and required to call update session method.
</p>
<pre><code class="csharp">Countly.Instance.BackendMode().UpdateSession(string deviceId, int duration, string appKey = null, long timestamp = 0);</code></pre>
<p>Here are examples about UpdateSession method.</p>
<pre><code class="csharp">// minimal call to the UpdateSession, this fallbacks to internal metrics and app key
Countly.Instance.BackendMode().UpdateSession(DEVICE_ID, 60);

// with custom timestamp
Countly.Instance.BackendMode().UpdateSession(DEVICE_ID, 45, APP_KEY, 1703752478530);</code></pre>
<p>
  <strong>End Session</strong>
</p>
<p>
  Duration is in seconds and required. If it is negative, it will be not sent
</p>
<pre><code class="csharp">Countly.Instance.BackendMode().EndSession(string deviceId, int duration, string appKey = null, long timestamp = 0);</code></pre>
<p>Here are examples about EndSession method.</p>
<pre><code class="csharp">// minimal call to the EndSession, this fallbacks to internal metrics and app key
Countly.Instance.BackendMode().EndSession(DEVICE_ID, -1);

// with custom timestamp and duration
Countly.Instance.BackendMode().EndSession(DEVICE_ID, 45, APP_KEY, 1703752478530);</code></pre>
<h4 id="h_01HJQWCX2D7MN5VJDA7VNXVWRW">View Tracking</h4>
<p>
  The Windows SDK backend mode provides manual reporting of views. There is no
  automatic handling of views internally.
</p>
<p>The SDK provides two functions; StartView and StopView</p>
<p>
  <strong>Start View</strong>
</p>
<pre><code class="csharp">Countly.Instance.BackendMode().StartView(string deviceId, string name, Segmentation segmentations = null, string segment = null, string appKey = null, bool firstView = false, long timestamp = 0);</code></pre>
<p>
  name and segment parameters are required. They should not be empty or null.
</p>
<p>Segment is platform for devices or domain for websites.</p>
<p>
  If a view is first view in the session or in the design of your flow, firstView
  parameter must be provided as true. Default is false.
</p>
<p>Here are examples about StartView method.</p>
<pre><code class="csharp">// minimal call to the StartView
Countly.Instance.BackendMode().StartView(DEVICE_ID, "Login", segment: "Desktop");

Segmentation segmentation = new Segmentation();
segmentation.Add("email", "test@test.test");
segmentation.Add("campaign_user", "true");

// with segmentation, firstView and timestamp
Countly.Instance.BackendMode().StartView(DEVICE_ID, "Login", segmentation, "Desktop", APP_KEY, true, 1703752478530);</code></pre>
<p>
  <strong>Stop View</strong>
</p>
<pre><code class="csharp">Countly.Instance.BackendMode().StopView(string deviceId, string name, long duration, Segmentation segmentations = null, string segment = null, string appKey = null, long timestamp = 0);</code></pre>
<p>
  name, segment and duration parameters are required. They should not be empty
  or null.
</p>
<p>Segment is platform for devices or domain for websites.</p>
<p>Duration in seconds and cannot be less then 0</p>
<p>Here are examples about StopView method.</p>
<pre><code class="csharp">// minimal call to the StopView
Countly.Instance.BackendMode().StopView(DEVICE_ID, "Logout", 34, segment: "Android");

Segmentation segmentation = new Segmentation();
segmentation.Add("last_seen", "1994-11-05T13:15:30Z");
segmentation.Add("campaign_user", "false");

// with segmentation and timestamp
Countly.Instance.BackendMode().StopView(DEVICE_ID, "Logout", 56, segmentation, "Gear", APP_KEY, 1703752478530);</code></pre>
<h4 id="h_01HJQXEQHXV7YFT3FGCFRQ36D7">Device ID Management</h4>
<p>
  It is possible manage device ids with the Windows SDK backend mode.
</p>
<p>
  <strong>Change Device ID With Merge</strong>
</p>
<pre><code class="csharp">Countly.Instance.BackendMode().ChangeDeviceIdWithMerge(string newDeviceId, string oldDeviceId, string appKey = null, long timestamp = 0);</code></pre>
<p>newDeviceId is required, should not be empty or null</p>
<p>Here are examples about ChangeDeviceIdWithMerge method.</p>
<pre><code class="csharp">// minimal call to the ChangeDeviceIdWithMerge, this fallbacks to internal app key
Countly.Instance.BackendMode().ChangeDeviceIdWithMerge(NEW_ID, OLD_ID);

// with custom timestamp
Countly.Instance.BackendMode().ChangeDeviceIdWithMerge(NEW_ID, OLD_ID, APP_KEY, 1703752478530);</code></pre>
<h4 id="h_01HJQZ3PMJXQ7CBN2FFPCYWXRR">User Profiles</h4>
<p>
  It is possible manage user properties and custom details with the Windows SDK
  backend mode.
</p>
<pre><code class="csharp">Countly.Instance.BackendMode().RecordUserProperties(string deviceId, IDictionary&lt;string, object&gt; userProperties, string appKey = null, long timestamp = 0);</code></pre>
<p>
  userProperties are required and should not be empty. Current supported data types
  for the values are: string, int, long, double, float and bool
</p>
<p>
  Here is the supported predefined keys for user properties. Other than these keys,
  everything will be a custom property.
</p>
<pre>"name", "username", "email", "organization", "phone", "gender", "byear", "picture"</pre>
<p>
  To set the picture correctly, only URL of the picture should be provided
</p>
<p>Here are examples about RecordUserProperties method.</p>
<pre><code class="csharp">// minimal call to the RecordUserProperties, this fallbacks to internal app key
var userProperties = new Dictionary&lt;string, object&gt;(){
   {"name", "John"},
   {"username", "Dohn"},
   {"organization", "Fohn"},
   {"email", "johnjohn@john.jo"},
   {"phone", "+123456789"},
   {"gender", "Unkown"},
   {"byear", 1969},
   {"picture", "http://someurl.png"}
};
Countly.Instance.BackendMode().RecordUserProperties(DEVICE_ID, userProperties);

// with custom timestamp and custom properties
userProperties["int"] = 5;
userProperties["long"] = 1044151383000;
userProperties["float"] = 56.45678;
userProperties["string"] = "value";
userProperties["double"] = -5.4E-79;
userProperties["invalid"] = new List&lt;string&gt;(); // this will be eliminated
userProperties["action"] = "{$push: \"black\"}";
userProperties["nullable"] = null; // this will be eliminated
userProperties["marks"] = "{$inc: 1}";
userProperties["point"] = "{$mul: 1.89}"
userProperties["gpa"] = "{$min: 1.89}"
userProperties["gpa"] = "{$max: 1.89}"
userProperties["name"] = "{$setOnce: \"Name\"}"
userProperties["permissions"] = "{$pull: [\"Create\", \"Update\"]}"
userProperties["langs"] = "{$push: [\"Python\", \"Ruby\", \"Ruby\"]}" // this will create two 'Ruby' entry
userProperties["langs"] = "{$addToSet: [\"Python\", \"Python\"]}" // this will create only one 'Python' entry

Countly.Instance.BackendMode().RecordUserProperties(DEVICE_ID, userProperties, APP_KEY, 1703752478530);</code></pre>
<p>
  You may also perform certain manipulations to your custom property values, such
  as incrementing the current value on a server by a certain amount or storing
  an array of values under the same property.
</p>
<p>
  The keys for predefined modification operations are as follows:
</p>
<div class="table-container">
  <table style="width: 752px; height: 220px;">
    <tbody>
      <tr style="height: 22px;">
        <th style="width: 95.1875px; height: 22px;">Key</th>
        <th style="width: 259.859px; height: 22px;">Description</th>
        <th style="width: 386.953px; height: 22px;">Example Usage</th>
      </tr>
      <tr style="height: 44px;">
        <td style="width: 87.1875px; height: 44px;">$inc</td>
        <td style="width: 251.859px; height: 44px;">
          <span>increment value by provided value</span>
        </td>
        <td style="width: 378.953px; height: 44px;">
          <span><code class="csharp">props["age"] = "{$inc: 5}"</code></span>
        </td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 87.1875px; height: 22px;">$mul</td>
        <td style="width: 251.859px; height: 22px;">
          <span>multiply value by the provided value</span>
        </td>
        <td style="width: 378.953px; height: 22px;">
          <span><code class="csharp">props["point"] = "{$mul: 1.89}"</code></span>
        </td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 87.1875px; height: 22px;">$min</td>
        <td style="width: 251.859px; height: 22px;">
          <span>sets minimum value between given and existing</span>
        </td>
        <td style="width: 378.953px; height: 22px;">
          <span><code class="csharp">props["gpa"] = "{$min: 1.89}"</code></span>
        </td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 87.1875px; height: 22px;">$max</td>
        <td style="width: 251.859px; height: 22px;">
          <span>sets maximum value between given and existing</span>
        </td>
        <td style="width: 378.953px; height: 22px;">
          <span><code class="csharp">props["gpa"] = "{$max: 1.89}"</code></span>
        </td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 87.1875px; height: 22px;">$setOnce</td>
        <td style="width: 251.859px; height: 22px;">
          <span>set value if it does not exist</span>
        </td>
        <td style="width: 378.953px; height: 22px;">
          <span><code class="csharp">props["name"] = "{$setOnce: \"Name\"}"</code></span>
        </td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 87.1875px; height: 22px;">$pull</td>
        <td style="width: 251.859px; height: 22px;">
          <span>remove values from an array prop</span>
        </td>
        <td style="width: 378.953px; height: 22px;">
          <span><code class="csharp">props["permissions"] = "{$pull: [\"Create\", \"Update\"]}"</code></span>
        </td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 87.1875px; height: 22px;">$push</td>
        <td style="width: 251.859px; height: 22px;">
          <span>insert values to an array prop, same values can be added</span>
        </td>
        <td style="width: 378.953px; height: 22px;">
          <span><code class="csharp">props["langs"] = "{$push: [\"Python\", \"Ruby\"]}"</code></span>
        </td>
      </tr>
      <tr style="height: 22px;">
        <td style="width: 87.1875px; height: 22px;">$addToSet</td>
        <td style="width: 251.859px; height: 22px;">
          <span>insert values to an array of unique values, same values are ignored</span>
        </td>
        <td style="width: 378.953px; height: 22px;">
          <span><code class="csharp">props["langs"] = "{$addToSet: [\"Python\", \"Python\"]}"</code></span>
        </td>
      </tr>
    </tbody>
  </table>
</div>
<h4 id="h_01HJR0QPH5KYCS80XYZMDE068R">Direct Requests</h4>
<p>
  The Windows SDK has ability to send direct/custom requests to the server.
</p>
<pre><code class="csharp">Countly.Instance.BackendMode().RecordDirectRequest(string deviceId, IDictionary&lt;string, string&gt; paramaters, string appKey = null, long timestamp = 0);</code></pre>
<p>Parameters should not be empty</p>
<p>Here are examples about RecordDirectRequest method.</p>
<p>
  The internal keys are not overridden by the given key values.
</p>
<pre><code class="csharp">// minimal call to the RecordDirectRequest, this fallbacks to internal app key
var parameters = new Dictionary&lt;string, string&gt;(){
   {"begin_session", "1"},
   {"metrics", ... }, // metrics to provide
   {"location", "-0.3720234014105792,-159.99741809049596" },
   {"sdk_custom_version", "24.1.0:04"},
   {"user_id", "123456789"},
   {"onesignal_id", "..."}
};
Countly.Instance.BackendMode().RecordDirectRequest(DEVICE_ID, parameters);

// with custom timestamp
Countly.Instance.BackendMode().RecordDirectRequest(DEVICE_ID, parameters, APP_KEY, 1703752478530);</code></pre>
<h3 id="h_01HHHTMR50NHVM1X61ZFCF7002">Configuring Backend Mode</h3>
<p>
  When backend mode is enabled, the SDK will apply limits to request queue and
  to the event queue. Default limit for the maximum amount of entries that the
  request queue can hold is 1000. When exceeding that count, the oldest request
  will be deleted.
</p>
<p>
  Events are sent periodically (every 60 seconds we would try to send all stored
  events), and a subsection of events can be sent based on different triggers.
</p>
<p>
  For a single device ID the default "sending" threshold is 10 events.
</p>
<p>
  For all events targeted for a single app, the default "sending" threshold is
  1000 events.
</p>
<p>
  For all stored events for a target countly server the default "sending" threshold
  is 10000.
</p>
<p>
  These limits can be changed with these additional config calls:
</p>
<pre><code class="csharp">cc.SetMaxRequestQueueSize(1000); // sets request queue max size as 1000
cc.SetEventQueueSizeToSend(100); // sets event queue size per device
cc.SetBackendModeAppEQSizeToSend(1000): // sets event queue size per app
cc.SetBackendModeServerEQSizeToSend(10000): // sets event queue size for server</code></pre>
<h1 id="h_01HABTXQFAA2KJMX7VB5F0HF31">FAQ</h1>
<h2 id="h_01HABTXQFAM9J70KBWZYBQVTB4">What Information Is Collected by the SDK?</h2>
<p>
  The following description mentions data that is collected by SDK to perform their
  functions and implement the required features. Before any of it is sent to the
  server, it is stored locally. For further information please have a look
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts#h_01HJ5MD0WB97PA9Z04NG2G0AKC">here</a>.
</p>
<p>
  * When events are recorded, the following information collected:<br>
  - Time of event<br>
  - Current hour<br>
  - Current day of week<span></span>
</p>
<p>
  <span>Any other information like data in events, location, user profile information, or other manual requests depends on what the developer decides to provide and is not collected by the SDK itself.</span>
</p>
<h2 id="h_01HABTXQFAK87HNC49QE27H2PP">Is Windows SDK Compatible With .Net Maui</h2>
<p>
  .NET Multi-platform App UI (.NET MAUI) is a cross-platform framework for creating
  native mobile and desktop apps with C# and XAML. It is compatible with .NET 6
  runtime (or rather .NET Core 5). All .NET Core versions (2.0 and above) are compatible
  with .NET Standard 2.0 libraries.
</p>
<p>
  As one of our Windows SDK flavors targets '.NET Standard' you should be able
  to use our Windows SDK in your .Net Maui applications without any hurdle.
</p>
<p>
  However there a couple of issues to touch upon. On .NET MAUI applications, when
  an uncaught exception happens the <code>AppDomain.UnhandledException</code> event
  occurs. As it is a cross-platform framework this effects the each platform you
  target differently and each one should need. For Android applications all exceptions
  should go through the
  <code>Android.Runtime.AndroidEnvironment.UnhandledExceptionRaiser</code> event
  instead of the <code>AppDomain.CurrentDomain.UnhandledException</code> event.
  And for iOS and Mac Catalyst, handling of the <code>UnwindNativeCode</code> value
  is necessary.
</p>
<p>
  So for reporting native crashes using
  <a class="editor-rtfLink" href="https://gist.github.com/mattjohnsonpint/7b385b7a2da7059c4a16562bc5ddb3b7" target="_blank" rel="noopener">this</a>
  class in your project would provide a handler that would work on major platforms
  with the mentioned logic. To handle uncaught exceptions correctly we catch iOS
  and Android errors at lines
  <a class="editor-rtfLink" href="https://gist.github.com/mattjohnsonpint/7b385b7a2da7059c4a16562bc5ddb3b7#file-mauiexceptions-cs-L29" target="_blank" rel="noopener">29</a>
  and
  <a class="editor-rtfLink" href="https://gist.github.com/mattjohnsonpint/7b385b7a2da7059c4a16562bc5ddb3b7#file-mauiexceptions-cs-L40" target="_blank" rel="noopener">40</a>
  respectively. After catching them, we route all unhandled exceptions from different
  platforms through
  <a href="https://gist.github.com/mattjohnsonpint/7b385b7a2da7059c4a16562bc5ddb3b7#file-mauiexceptions-cs-L8" target="_self">this</a>
  event handler.
</p>
<p>Usage:</p>
<pre><code class="csharp">MauiExceptions.UnhandledException += (sender, args) =&gt;
{
 Countly.RecordException(args.ExceptionObject.ToString(), null, null, true).Wait();
};</code></pre>
<p>
  <span data-preserver-spaces="true">Windows SDK <a href="https://github.com/Countly/countly-sdk-windows/" target="_self">GitHub</a> page contains a sample project to test the basic functionality.</span>
</p>
