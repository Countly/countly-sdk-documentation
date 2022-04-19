<p>
  This document explains how to install Countly SDK for Windows desktop applications. It applies to version 21.11.0.
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <span class="wysiwyg-font-size-large"><strong>Minimum Windows version</strong></span>
  </p>
  <p>
    The Countly Windows SDK supports the following operating systems and .NET
    versions:
  </p>
  <ul>
    <li>Windows 8.1</li>
    <li>Windows 10</li>
    <li>Windows 10 Mobile</li>
    <li>.NET 3.5</li>
    <li>.NET 4.0 Client Profile</li>
    <li>.NET 4.5 and above</li>
    <li>.NET Standard 2.0</li>
  </ul>
</div>
<div class="callout callout--info">
  <p class="callout__title">
    <span class="wysiwyg-font-size-large"><strong>Older documentation</strong></span>
  </p>
  <p>
    To access the documentation for version 20.11 click&nbsp;<a href="https://countly.zendesk.com/hc/en-us/articles/4413138651161">here.</a>
  </p>
</div>
<p>
  In order to set up Countly SDK in your Windows app, follow these steps:
</p>
<ol>
  <li>
    In Solution Explorer open context menu on
    <strong>References - Manage NuGet Packages</strong>.
  </li>
  <li>Select nuget.org in Package source.</li>
  <li>
    Type <strong>Countly</strong> in search box.
  </li>
  <li>
    Select Countly Analytics from results list and click Install button.
  </li>
</ol>
<p>
  The usage of the SDK requires a connection to the server. This connection usually
  is access to the internet.
</p>
<p>
  <span class="wysiwyg-font-size-large"><strong>SDK sample app</strong></span>
</p>
<p>
  The Countly github page for this SDK contains also sample projects. You should
  be able to download them to test the basic functionality of this SDK and make
  sure you are using it correct in case you encounter any problems in your application
</p>
<p>
  The project page can be found
  <a href="https://github.com/Countly/countly-sdk-windows/">here</a>
</p>
<h1 id="sdk-integration" class="anchor-heading" tabindex="-1">SDK Integration</h1>
<p class="anchor-heading">
  Before you can use any Countly functionality, you need to call
  <code>Countly.Instance.Init</code> to initiate the SDK.
</p>
<h2 id="minimal-setup" class="anchor-heading">Minimal Setup</h2>
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
  <span>In the </span><code>CountlyConfig</code><span>&nbsp;object, you provide appKey and your Countly server URL. For more information on how to acquire you application key (appKey) and server URL, check&nbsp;<a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#acquiring-your-application-key-and-server-url%E2%80%9D" target="_self">here</a>.</span>
</p>
<p>
  <strong>Note: </strong>The SDK targets multiple profiles. Therefore for some
  of them, there are feature differences. Either with additional function calls
  or with additional fields in the CountlyConfig object.
</p>
<h3 id="providing-the-application-key" class="anchor-heading">Providing the application key</h3>
<p>
  <span>Also called "appKey" as shorthand. The application key is used to identify for which application this information is tracked. You receive this value by creating a new application in your Countly dashboard and accessing it in its application management screen.</span>
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
  In order to make sure that requests to Countly are sent correctly, you need to
  enable logging using the following:
</p>
<pre><code class="csharp hljs">    Countly.IsLoggingEnabled = <span class="hljs-literal">true</span>;</code></pre>
<p>
  You can turn it on and off in any place of your code. This will print debug messages
  and give better insight into the inner workings of the SDK.
</p>
<h2 id="sdk-data-storage" class="anchor-heading">SDK data storage</h2>
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
<h2 id="sdk-notes" class="anchor-heading" tabindex="-1">SDK notes</h2>
<h3>Additional info for Windows Store project setup</h3>
<div class="callout callout--danger">
  <p class="callout__title">
    <span class="wysiwyg-font-size-large"><strong>Windows Store build has been removed</strong></span>
  </p>
  <p>The following section of documentation will be removed soon</p>
</div>
<p>
  As the Countly SDK requires <strong>Internet (Client &amp; Server)</strong> to
  be enabled. Open Package.appxmanifest, click on Capabilities section and make
  it enabled
</p>
<p>
  Add <code>using CountlySDK;</code> in the App.xaml.cs usings section
</p>
<p>
  You need to call <code>Countly.Instance.SessionBegin();</code> each time when
  app is activated and <code>await Countly.EndSession();</code> when app is deactivated.
</p>
<p>
  That would mean adding <code>SessionBegin</code> calls to
  <code>OnLaunched</code>, <code>OnActivated</code> and <code>OnResuming</code>
  events and <code>SessionEnd</code> calls to <code>OnLaunched</code> event which
  is already prepared for you by Visual Studio in <code>App.xaml.cs</code> file.
  Add initialization code before page navigation happens.
</p>
<pre><code class="csharp">protected override void OnLaunched(LaunchActivatedEventArgs e)
{
  
...

  //create the Countly init object
  CountlyConfig cc = new CountlyConfig();
  cc.serverUrl = "http://YOUR_SERVER";
  cc.appKey = "YOUR_APP_KEY";
  cc.appVersion = "1.2.3";
  cc.application = this

  //initiate the SDK with your preferences
  await Countly.Instance.Init(cc)
  
  if (rootFrame.Content == null)
  {
    // Removes the turnstile navigation for startup.
    if (rootFrame.ContentTransitions != null)
    {
      this.transitions = new TransitionCollection();
      foreach (var c in rootFrame.ContentTransitions)
    {
      this.transitions.Add(c);
    }
  }
    
...
}</code></pre>
<p>
  Add <code>override</code> method called <code>OnActivated</code> to
  <code>App.xaml.cs</code> file and call
  <code>Countly.Instance.SessionBegin();</code> inside
</p>
<pre><code class="csharp">protected override void OnActivated(IActivatedEventArgs args)
{
  await Countly.Instance.SessionBegin();
}</code></pre>
<p>
  Subscribe to application <code>Resuming</code> method in <code>App</code> constructor.
</p>
<pre><code class="csharp">public App()
{
  this.InitializeComponent();
  this.Resuming += this.OnResuming;
  this.Suspending += this.OnSuspending;
}

private void OnResuming(object sender, object e)
{
  await Countly.Instance.SessionBegin();
}</code></pre>
<p>
  Update <code>OnSuspending</code> method created by Visual Studio in
  <code>App.xaml.cs</code> file to handle Countly deactivation logic. Make sure
  you use async/await statements, so app will not be closed before Countly receives
  <code>end session</code> event
</p>
<pre><code class="csharp">private async void OnSuspending(object sender, SuspendingEventArgs e)
{
  var deferral = e.SuspendingOperation.GetDeferral();

  await Countly.Instance.SessionEnd();

  deferral.Complete();
}</code></pre>
<h3>Additional info for UWP project setup</h3>
<p>
  It's possible to register a unhandled crash handler during SDK initialization.
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
<h1 id="crash-reporting" class="anchor-heading" tabindex="-1">Crash reporting</h1>
<h2 id="automatic-crash-handling" class="anchor-heading">Automatic crash handling</h2>
<p>
  Countly SDK has an ability to automatically collect crash reports which you can
  examine and resolve later on the server. This applies for Windows Store apps,
  on other platforms you should subscribe to unhandled exceptions handler manually.
  Exception details and device properties will be sent on next app launch.
</p>
<h2 id="handled-exceptions" class="anchor-heading">Handled exceptions</h2>
<p>
  To log handled exceptions, which are not fatal, use
  <code>Countly.RecordException;</code> the method. You can provide custom properties
  for crash providing key/value object to store for this crash report and server
  will segment values for you for the same crash.
</p>
<pre><strong>Dictionary</strong>&lt;string, string&gt; customInfo = new Dictionary&lt;string, string&gt;<br>{<br>{ "customData", "importantStuff" }<br>};<br><br><strong>Countly</strong>.RecordException(ex.Message, ex.StackTrace, customInfo);</pre>
<h2 id="crash-breadcrumbs" class="anchor-heading">Crash breadcrumbs</h2>
<p>
  Throughout your app, you can leave&nbsp;crash breadcrumbs<span>&nbsp;</span><span>Mandatory that </span>would
  describe previous steps that were taken in your app before the crash. After a
  crash happens, they will be sent together with the crash report.
</p>
<p>The following command adds a crash breadcrumb:</p>
<pre><strong>Countly</strong>.AddBreadCrumb("breadcrumb");</pre>
<h1>Events</h1>
<p>
  <span>An&nbsp;</span><a href="http://resources.count.ly/docs/custom-events"><span>event</span></a><span>&nbsp;is any type of action that you can send to a Countly instance, e.g. purchases, changed settings, view enabled, and so on, letting you get valuable information about your application.</span>
</p>
<div class="callout callout--warning">
  <h2 id="recording-events" class="anchor-heading">Recording events</h2>
  <p>
    <span>Here is a quick way to&nbsp;</span><span>record an event:</span>
  </p>
  <pre><code class="csharp">Countly.RecordEvent("event-key");</code></pre>
  <p>
    <span>Based on the example below of an event recording a&nbsp;<strong>purchase</strong>, h</span><span>ere is a quick summary of the information for each usage:</span>
  </p>
</div>
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
  First, add <code>using CountlySDK;</code> in the usings section
</p>
<h2>1. Event key and count</h2>
<pre><code class="csharp">Countly.RecordEvent("purchase", 3);</code></pre>
<h2>2. Event key, count and sum</h2>
<pre><code class="csharp">Countly.RecordEvent("purchase", 3, 0.99);</code></pre>
<h2>3. Event key and count with segmentation(s)</h2>
<pre><code class="csharp">Segmentation segmentation = new Segmentation();
segmentation.Add("country", "Germany");
segmentation.Add("app_version", "1.0");
Countly.RecordEvent("purchase", 3, segmentation);   

Countly.RecordEvent("purchase", 1, 0.99);
</code></pre>
<h2>4. Event key, count and sum with segmentation(s)</h2>
<pre><code class="csharp">Segmentation segmentation = new Segmentation();
segmentation.Add("country", "Germany");
segmentation.Add("app_version", "1.0");
Countly.RecordEvent("purchase", 3, 2.97, segmentation);
</code></pre>
<h2>5. Event key, count, sum, duration with segmentation(s)</h2>
<pre><code class="csharp">Segmentation segmentation = new Segmentation();
segmentation.Add("country", "Germany");
segmentation.Add("app_version", "1.0");
Countly.RecordEvent("purchase", 3, 2.97, 122.45, segmentation);</code></pre>
<h1>Sessions</h1>
<h2>Manual sessions</h2>
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
<h1>View tracking</h1>
<h2 id="manual-view-recording" class="anchor-heading">Manual view recording</h2>
<p>
  The SDK provides a call to record views in your application. More information
  about how to use them can be found
  <a href="https://resources.count.ly/docs/view-analytics">here</a>. You only need
  to provide the name for the view.
</p>
<pre><code class="csharp">Countly.Instance.RecordView("Some View");</code></pre>
<h1 id="device-id-management" class="anchor-heading" tabindex="-1">Device ID management</h1>
<p>
  To link events, sessions, crashes, etc to a user, a deviceId is used. It is usually
  generated by the SDK. It is then saved locally and then reused on every init
  unless the developer supplies its own device Id.
</p>
<p>
  Ideally, the same device Id would be generated on the same device when using
  the same generation method. This way it would be possible to track users on reinstalls.
</p>
<h2 id="device-id-generation" class="anchor-heading">Device ID generation</h2>
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
    winHardwareToken - [windows 8 store apps] uses the hardware identification
    token provided by the OS to generate a hash that will be used as an id. Should
    be the same on a reinstall. Very high chance of being unique
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
<h2 id="changing-device-id" class="anchor-heading">Changing device ID</h2>
<p>
  It is possible to change the device Id after the app is initiated. It can be
  done with a server-side merge and without one. In both cases, the new id will
  be used on further app launches.
</p>
<p>
  If it is done without a server-side merge, then the previous session will end
  and a new session will be started with the new id.
</p>
<p>
  With a server-side merge, the events, session information and etc will be assigned
  to the new device id.
</p>
<pre><code class="csharp">//changing without a server side merge
Countly.Instance.ChangeDeviceId("newId", false);
Countly.Instance.ChangeDeviceId("newIdAgain");

//changing with a server side merge
Countly.Instance.ChangeDeviceId("ThisIsUnique", true);</code></pre>
<h1>User location</h1>
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
<h2 id="setting-location" class="anchor-heading">Setting location</h2>
<p>
  <span>After SDK initialization, you can&nbsp;set location info.</span>
</p>
<pre><code class="csharp">//set user location
String gpsLocation = "63.445821, 10.898868";
String ipAddress = "13.56.33.12";
String country_code = null;
String city = null;

Countly.Instance.SetLocation(gpsLocation, ipAddress, country_code, city);</code></pre>
<p>
  If there are fields you don't want to set, set them to null. If you want to reset
  a field, set it to an empty string.
</p>
<p>
  If no location is provided, it will be approximated by using GeoIP.
</p>
<h2 id="disabling-location" class="anchor-heading" tabindex="-1">Disabling location</h2>
<p>
  <span>Users might want to opt-out of location tracking. To do so call:</span>
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
<h2 id="setting-predefined-values" class="anchor-heading">Setting predefined values</h2>
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
<h2 id="setting-custom-values" class="anchor-heading">Setting custom values</h2>
<p>
  The SDK gives you the flexibility to send only the custom data to Countly servers,
  even when you don’t want to send other user-related data.<span>&nbsp;<br></span>You
  can provide custom properties for user using <code>Custom</code> object
</p>
<pre><code>Countly.UserDetails.Custom.Add("city", "london");</code></pre>
<h2 id="setting-custom-values" class="anchor-heading">Setting User picture</h2>
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
<h1>User consent</h1>
<p>
  If you want to comply with GDPR or similar privacy requirements, there is functionality
  to manage user consent to features.
</p>
<p>
  More information about GDPR can be found
  <a href="https://blog.count.ly/countly-the-gdpr-how-worlds-leading-mobile-and-web-analytics-platform-can-help-organizations-5015042fab27">here</a>.
</p>
<h2 id="setup-during-init" class="anchor-heading">Setup during init</h2>
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
<h2 id="changing-consent" class="anchor-heading">Changing consent</h2>
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
<h1 class="anchor-heading" tabindex="-1">Other features</h1>
<h1 id="faq" class="anchor-heading" tabindex="-1">FAQ</h1>
<h2 id="what-information-is-collected-by-the-sdk" class="anchor-heading">What information is collected by the SDK</h2>
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
