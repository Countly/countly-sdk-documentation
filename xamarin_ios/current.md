<p>
  This document includes necessary information for integrating Countly iOS SDK
  in your Xamarin.iOS project.
</p>
<div class="callout callout--info">
  <h3 class="callout__title">Minimum iOS version</h3>
  <p>
    Countly iOS SDK needs a minimum of <strong>iOS 8.0</strong> ( macOS 10.9)
    ,and requires Xcode 9.0+ with Base SDK iOS 10.0+ to work.
  </p>
</div>
<h1>Integration</h1>
<p>
  To integrate CountlySdk into your application, please follow these steps:
</p>
<ul>
  <li>Start Xamarin Studio.</li>
  <li>From the File menu, select New &gt; Solution</li>
  <li>
    Add a new Xamarin.iOS project called CountlyTestNative to the solution,
  </li>
  <li>
    Install <strong>Countly Analytics for Xamarin (iOS)</strong> package from
    Nuget using command <strong>Install-Package CountlySDK.Xamarin.iOS</strong>
    into your project.
  </li>
  <li>
    In your Appdelegate, add <code>using CountlySdk</code> and inside FinishedLaunching
    add following lines at the beginning
  </li>
</ul>
<pre><code class="csharp">using CountlySdk;

namespace CountlyTestNative.iOS
{
    [Register("AppDelegate")]
    public class AppDelegate : UIApplicationDelegate
    {
             public override bool FinishedLaunching(UIApplication application,                NSDictionary launchOptions)
         {
             Countly.SharedInstance().Init();
            CountlyConfig config = new CountlyConfig();
            config.AppKey = "your_App_Key";
            config.Host = "https://YOUR_COUNTLY_SERVER";
            Countly.SharedInstance().StartWithConfig(config);
            return true;
        }
    }
}</code></pre>
<ul>
  <li>
    You need to set your app key and host on CountlyConfig object. Make sure
    you use App Key (found under Management &gt; Applications) .
  </li>
</ul>
<p>
  If you are using Countly Enterprise Edition trial servers <code>host</code> should
  be <code><a href="https://try.count.ly">https://try.count.ly</a></code>
</p>
<p>
  <span>In iOS 13 a new&nbsp;SceneSession Lifecycle is added, which causes some issues in Countly Sessions logging, here are some steps required to fix this issue:<br>1. Delete the "Application Scene Manifest" entry from the app's Info.plist<br>2. Comment or delete these methods in <strong>AppDelegate.cs:</strong></span>
</p>
<pre><span>[Export("application:configurationForConnectingSceneSession:options:")]<br> public UISceneConfiguration GetConfiguration(UIApplication application, UISceneSession connectingSceneSession, UISceneConnectionOptions options)</span></pre>
<pre><span>[Export("application:didDiscardSceneSessions:")]<br> public void DidDiscardSceneSessions(UIApplication application, NSSet&lt;UISceneSession&gt; sceneSessions)<br></span></pre>
<ul>
  <li>
    You can run your project and see first session data immediately on your Dashboard.
  </li>
</ul>
<h1>Advanced Configuration</h1>
<h2>
  <strong>Debug Mode</strong>
</h2>
<p>
  If you want to enable debug mode of Countly iOS SDK which output internal infos,
  errors and warnings into console, you can set enableDebug flag on CountlyConfig
  object before starting Countly.
</p>
<pre><code class="csharp">config.EnableDebug = true;</code></pre>
<h2>
  <strong>Additional Features</strong>
</h2>
<p>
  If you want to use additional features like <strong>PushNotifications</strong>,
  <strong>CrashReporting</strong> and <strong>AutoViewTracking</strong> you can
  specify them in <code>features</code> array on <code>CountlyConfig</code> object
  before you start:
</p>
<pre><code class="csharp">[Register("AppDelegate")
    public class AppDelegate : UIApplicationDelegate
    {
             public override bool FinishedLaunching(UIApplication application,                NSDictionary launchOptions)      
        {
            CountlyConfig config = new CountlyConfig();
            config.AppKey = "your_App_Key";
            config.Host = "https://YOUR_COUNTLY_SERVER";
            config.Features = new NSObject[] {        Constants.CLYPushNotifications,                         Constants.CLYCrashReporting, Constants.CLYAutoViewTracking };
            Countly.SharedInstance().StartWithConfig(config);
            return true;
        }
    }
}
</code></pre>
<h2>
  <strong>Device ID</strong>
</h2>
<ul>
  <li>
    <strong>Custom Device ID</strong>
  </li>
</ul>
<p>
  If you want to use custom device ID, you can set deviceID property on CountlyConfig
  object.
</p>
<pre><code class="csharp">config.DeviceID = "customDeviceID";</code></pre>
<p>
  <strong>Note:</strong> Once set, device ID will be stored persistently in device
  on the first launch, and will not change even after app delete and re-install,
  unless you change it explicitly.
</p>
<ul>
  <li>
    <strong>Changing Device ID</strong>
  </li>
</ul>
<p>
  You can use <strong>SetNewDeviceID</strong> method to change device id on runtime
  after you start Countly. If onServer bool is set to true, old device ID on server
  will be replaced with the new one, and data associated with old device ID will
  be merged automatically.
</p>
<pre><code class="csharp">  Countly.SharedInstance().SetNewDeviceID("new_device_id",true);   </code></pre>
<p>
  Otherwise, if <code>onServer</code> bool is <strong>not</strong> set, device
  will be counted as a new device on server.
</p>
<pre><code class="csharp">  Countly.SharedInstance().SetNewDeviceID("new_device_id",false);   </code></pre>
<ul>
  <li>
    <strong>Handling User Login and Logout</strong>
  </li>
</ul>
<p>
  If your app allows users to login, then logged in users can be tracked with custom
  user ID. For this , you can use UserLoggedIn() and UserLoggedOut() methods for
  changing device ID.
</p>
<p>
  UserLoggedIn() method handles switching from device ID to custom user ID for
  logged in users.
</p>
<pre><code class="csharp">   Countly.SharedInstance().UserLoggedIn("UserID");</code></pre>
<p>
  UserLoggedOut() method handles switching from custom user ID to device ID for
  logged out users. It is a method that handles resetting device ID to default
  one and starting a new session.
</p>
<pre><code class="csharp">Countly.SharedInstance().UserLoggedOut();</code></pre>
<h2>
  <strong>Forcing Device ID Initialization</strong>
</h2>
<p>
  On the first app launch, Countly iOS SDK initializes device ID as specified in
  CountlyConfig object deviceID property, and stores it persistently. After this
  point, even if you delete and re-install the app Countly iOS SDK will continue
  to use initially stored device ID, to track app re-installs. So, while developing
  if you set deviceID property to something else on consecutive app launches, it
  will have no effect. In this case, you can set
  <strong>ForceDeviceIDInitialization</strong> flag on CountlyConfig object, to
  force device ID initialization again. This will reset the initially stored device
  ID and Countly iOS SDK will work as if it is the first app launch.
</p>
<pre><code class="csharp">			config.ForceDeviceIDInitialization = true;</code></pre>
<p>
  After you start Countly with <strong>ForceDeviceIDInitialization</strong> flag
  only once while developing, you can remove that line.
  <strong>ForceDeviceIDInitialization</strong> flag is not meant for production,
  it is only for debugging purposes while developing.
</p>
<h2>
  <strong>Other Settings</strong>
</h2>
<p>
  On <code>CountlyConfig</code> object you can specify further optional settings
  such as:
</p>
<ul>
  <li>
    <strong>Update Session Period</strong>
  </li>
</ul>
<p>
  You can specify UpdateSessionPeriod on CountlyConfig object before starting Countly.
  It is used for session updating and sending events to server periodically. It’s
  default falue is 60 seconds for iOS.
</p>
<pre><code class="csharp">config.UpdateSessionPeriod = 80;</code></pre>
<ul>
  <li>
    <strong>Manual Session Handling</strong>
  </li>
</ul>
<p>
  you can set ManualSessionHandling flag on CountlyConfig object to handle sessions
  manually.
</p>
<pre><code class="csharp">config.ManualSessionHandling = true;</code></pre>
<p>
  Countly SDK for Xamarin tracks sessions automatically and sends begin_session
  request on initialization, periodical update session request on specified interval
  (60 sec by default), end_session request when app goes to background, and begin_session
  request again when app comes back to foreground.
</p>
<p>
  If <strong>ManualSessionHandling</strong> flag is set, Countly iOS SDK does not
  send these requests automatically. So, you need to call beginSession, updateSession
  and endSession methods manually after you start Countly, depending on your own
  definition of a session.
</p>
<pre><code class="csharp">Countly.SharedInstance().BeginSession();
Countly.SharedInstance().UpdateSession();
Countly.SharedInstance().EndSession();</code></pre>
<ul>
  <li>
    <strong>Event Send Threshold</strong>
  </li>
</ul>
<p>
  <strong>EventSendThreshold</strong> is used to send events requests to server
  when number of recorded custom events reach it without waiting for next update
  session request.
</p>
<pre><code class="csharp"> config.EventSendThreshold = 5;</code></pre>
<ul>
  <li>
    <strong>Stored Requests Limit</strong>
  </li>
</ul>
<p>
  <strong>StoredRequestsLimit</strong> is used to limit number of request to be
  queued. In case your Countly server is down, queued request may reach excessive
  numbers, and it may cause problems with being delivered to server and stored
  on the device. To prevent this, Countly SDK will only store requests up to limit
  value. By default this is <strong>1000</strong>.
</p>
<pre><code class="csharp"> config.StoredRequestsLimit = 5000;</code></pre>
<ul>
  <li>
    <strong>Always use POST method</strong>
  </li>
</ul>
<p>
  You can set <code>AlwaysUsePOST</code> flag on <code>CountlyConfig</code> object
  before starting Countly. It is used for sending all requests using HTTP POST
  method regardless of the data size. If set, all requests will be sent using HTTP
  POST method. Otherwise; only the requests with a file upload or data size more
  than 2048 bytes will be sent using HTTP POST method.
</p>
<pre><code class="csharp">config.AlwaysUsePOST = true;</code></pre>
<ul>
  <li>
    <p>
      <strong>Additional Info</strong>
    </p>
  </li>
  <li>
    <p>
      <strong>Custom Header Field</strong>
    </p>
  </li>
</ul>
<p>
  You can set optional <code>customHeaderFieldName</code> to be sent with every
  request. It is useful if your server requires special headers to be sent for
  security reasons. Every request sent to Countly server will have this custom
  HTTP header and its value will be what is specified in
  <code>customHeaderFieldValue</code> property.
</p>
<pre><code class="csharp">config.CustomHeaderFieldName = "X-My-Custom-Field";
config.CustomHeaderFieldValue = "my_custom_value";</code></pre>
<h3>Attribution</h3>
<p>
  You can set <code>EnableAttribution</code> flag on <code>CountlyConfig</code>
  object to enable campaign attribution. If set, IDFA (Identifier For Advertising)
  will be sent with every <code>begin_session</code> request, unless user has limited
  ad tracking in iOS Settings.
</p>
<pre><code class="csharp">config.EnableAttribution = true;</code></pre>
<h2>Zero-IDFA Fix</h2>
<p>
  With the release of iOS10, IDFA (Identifier for Advertising) value is
  <code>00000000–0000–0000–0000–000000000000</code> for all users who switched
  <code>Limit Ad Tracking</code> setting on. If you are currently using a Countly
  iOS SDK version older than v16.06.4 and upgrading; you may need to apply Zero-IDFA
  fix for persistently stored device ID and queued requests. To apply fix, you
  need to set <code>ApplyZeroIDFAFix</code> flag on <code>CountlyConfig</code>
  object:
</p>
<pre><code class="csharp">config.ApplyZeroIDFAFix = true;</code></pre>
<ul>
  <li>
    <strong>Star Rating</strong>
  </li>
</ul>
<p>
  You can set Countly iOS SDK to automatically ask users for a 1-to-5 star-rating
  for each version depending on App launch.For this, you need to set
  <strong>StarRatingSessionCount</strong> property on CountlyConfig object. When
  total number of sessions reaches starRatingSessionCount, an alert view asking
  for 1-to-5 star-rating will be displayed automatically, once for each new version
  of the app.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/0df53f4-rating-detail-white.png">
</div>
<pre><code class="csharp">config.StarRatingSessionCount = 5;</code></pre>
<p>
  If you want star-rating dialog to be displayed only once for app lifetime, you
  can set <strong>starRatingDisableAskingForEachAppVersion</strong> flag on CountlyConfig
  object.
</p>
<pre><code class="csharp"> config.StarRatingDisableAskingForEachAppVersion = true;</code></pre>
<p>
  Additionally, you can customize star-rating dialog message using
  <code>StarRatingMessage</code> property on <code>CountlyConfig</code> object.
</p>
<pre><code class="csharp"> config.StarRatingMessage = "Would you rate the app?";</code></pre>
<p>
  Additionally, you can use <strong>AskForStarRating</strong> method to ask for
  a star-rating anytime you want.
</p>
<pre><code class="csharp"> Countly.SharedInstance().AskForStarRating((obj) =&gt; Console.Write("Rating"));</code></pre>
<h1>Notes</h1>
<h2>iTunesConnect IDFA Warning</h2>
<p>
  As Countly iOS SDK source has references to IDFA and iTunesConnect checks for
  API usage, even if you are not explicitly using IDFA as device ID, you may need
  to answer <strong>Yes</strong> for "Does this app use the Advertising Identifier
  (IDFA)?" question on iTunesConnect app submit form. Please make sure you follow
  the instructions specified in
  <a href="https://developer.apple.com/library/ios/documentation/LanguagesUtilities/Conceptual/iTunesConnect_Guide/Chapters/SubmittingTheApp.html">iTunes Connect Developer Guide</a>
  - The Advertising Identifier (IDFA) section. Otherwise your app may get rejected
  due to "Improper use of IDFA" or fail to proceed on app submitting. In screenshot
  below, you can see which checkboxes to select while sending your app to the App
  Store :
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/X6rCREd0TASv2WqihkjV_idfa.png">
</div>
<p>
  If you are using an advertisement system, you might need to check "Serve advertisements
  within the app" checkbox too.
</p>
<h1>Recording Events</h1>
<p>
  Here is a quick summary on how to use custom events recording methods.
</p>
<h2>Regular Events</h2>
<p>
  In examples given below, we will be recording a event named Xamarin studio with
  different scenarios:
</p>
<p>
  <strong>Xamarin studio</strong> event occurred 1 times
</p>
<pre><code class="csharp"> Countly.SharedInstance().RecordEvent("Xamarin studio", 12);</code></pre>
<p>
  <strong>Xamarin studio</strong> event occurred 12 times
</p>
<pre><code class="csharp"> Countly.SharedInstance().RecordEvent("Xamarin studio", 12);</code></pre>
<p>
  <strong>Xamarin_ios</strong> event occured 12 times from country : India , App
  Version: 1.0 with total amount 20 and for duration .5 sec.
</p>
<pre><code class="csharp">var dict = new NSDictionary("Country", "India", "App_Version", 1.0);
 Countly.SharedInstance().RecordEvent("Xamarin_ios", dict, 12, 20, .5);</code></pre>
<h2>Timed Events</h2>
<p>
  In below examples, we will be recording a timed event called<strong> Tracking AppRating </strong>to
  track how long it takes to complete:
</p>
<ul>
  <li>
    <strong> Tracking AppRating </strong> started
  </li>
</ul>
<pre><code class="csharp">Countly.SharedInstance().StartEvent("Tracking AppRating");</code></pre>
<ul>
  <li>
    <strong> Tracking AppRating </strong> ended
  </li>
</ul>
<pre><code class="csharp"> Countly.SharedInstance().EndEvent("Tracking AppRating");</code></pre>
<p>
  Additionally, you can provide more information like segmentation, count and sum
  while ending an event.
</p>
<pre><code class="csharp">var dict = new NSDictionary("Country", "India", "App_Version", 1.0);
 Countly.SharedInstance().EndEvent("Tracking AppRating" ,dict,1 ,345);</code></pre>
<p>
  Duration of the event will be calculated automatically when
  <code>endEvent</code> method is called.
</p>
<h1>Push Notifications</h1>
<h2>Setting up Push Certificate</h2>
<p>
  Please follow
  <a href="https://resources.count.ly/docs/countly-sdk-for-ios-and-os-x#section-setting-up-push-certificate">iOS, watchOS, tvOS &amp; macOS documentation</a>
  in order to set up APN credentials in Countly.
</p>
<h2>Configuring iOS app</h2>
<p>
  Please enable Push Notifications and Remote notifications Background Mode in
  your app in Entitlement.plist and please make sure that you sign your application
  using an explicit Provisioning Profile specific to your app's bundleID.
</p>
<p>
  Specify <strong>CLYPushNotifications</strong> in features array of
  <strong>CountlyConfig</strong> object. After that, you'll need to ask for user's
  permission for push notifications using AskForNotificationPermission() method
  of Countly, at any point in the app. You need to declare a class and inherit
  with UIResponder and IUIApplicationDelegate.
</p>
<p>
  After that you need to add code given below in FinishedLaunching method. Countly
  iOS SDK will handle the rest automatically.
</p>
<pre><code class="csharp">
[Register("AppDelegate")]
public class AppDelegate : UIApplicationDelegate
{
	public override bool FinishedLaunching(UIApplication application,                 NSDictionary launchOptions)
  	{
            application.WeakDelegate = this;
            Countly.SharedInstance().Init();
            //Basic Setting for countly server
            CountlyConfig config = new CountlyConfig();
            config.AppKey = @"your_App_Key";
            config.Host = @"https://YOUR_COUNTLY_SERVER";
            config.Features = new NSObject[] { Constants.CLYPushNotifications };  
            Countly.SharedInstance().AskForNotificationPermission();
 
            return true;
    }
}</code></pre>
<h2>Rich Push Notifications (iOS10+ only)</h2>
<p>
  Rich push notifications lets you send image, video or audio attachments, as well
  as customized action buttons on iOS10+. You need to set up Notification Service
  Extension to use it. Add <strong>NotificationServiceExtension</strong> in your
  project and then navigate to NotificationService.cs file.
</p>
<p>
  You also need to add <strong>Countly Analytics for Xamarin (iOS)</strong> Nuget
  package into your project.
</p>
<p>
  And add the following line at the end of DidReceiveNotificationRequest() method
  as shown below:
</p>
<pre><code class="csharp">using CountlySdk;</code></pre>
<p>
  Please enable Push Notifications in your notificationExtension Entitlement.plist.
  You need to create an app id and provisioning profile on Apple’s website for
  your Extension. You also need to configure App Transport Security setting in
  extension's Info.plist file. Otherwise, media attachments from non-https sources
  can not be loaded.
</p>
<p>
  Please make sure that you have changed the Deployment Target version of extension
  target to 10, not 10.3. Otherwise users running iOS versions lower than Deployment
  Target value can not get rich push notifications.
</p>
<pre><code class="csharp">public override void DidReceiveNotificationRequest(UNNotificationRequest request, 
     Action contentHandler)
        {
            ContentHandler = contentHandler;
            BestAttemptContent =  
      (UNMutableNotificationContent)request.Content.MutableCopy();

            CountlyNotificationService.DidReceiveNotificationRequest(request,               contentHandler);

        }</code></pre>
<h2>Deeplinking</h2>
<p>
  Deeplinking consists of using a hyperlink that links to a specific piece of content
  within an app. You can redirect users to any custom page or view in your app,
  by specifying deeplinks as custom actions button URLs. For this, first, you need
  to create URL scheme in your project.
</p>
<p>
  To do this, select <strong>info.plist -&gt; Advanced -&gt; Url Types.</strong>.
  Enter an identifier (ly.count.countly) into Identifier field. And enter your
  app's URL (countly) scheme into URL Schemes field.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/cbf1169-ss_url_types.png">
</div>
<p>
  Then, add the method to your <strong>Appdelegate</strong>.
</p>
<p>
  In this method you can check the passed <code>url</code> for custom view navigation,
  using <code>scheme</code> and <code>host</code> properties. For example, if you
  set custom action button URLs as <code>countly://productA</code> and
  <code>countly://productB</code>, you can use something similar to this snippet:
</p>
<pre><code class="csharp">
public override bool OpenUrl(UIApplication app, NSUrl url, string sourceApp, NSObject annotation)
        {
            
            if (url.Scheme.Equals("countly"))
            {
                if (url.Host.Equals("productA"))
                {
                  // present view controller for Product A;
                }
                else if (url.Host.Equals("productB"))
                {
                  // present view controller for Product B;
                }
             }
            return true;
        }
</code></pre>
<p>
  When users tap on custom action buttons, Countly iOS SDK will open the specified
  URLs with your app's scheme. Following this, related method you added to your
  app's delegate will be called.
</p>
<h2>Advanced Setup</h2>
<ul>
  <li>
    <strong>Test Mode</strong>
  </li>
</ul>
<p>
  For Development builds, your device will be marked as test device automatically.
  So, you can send push notifications to test devices by choosing
  <strong>Test Users</strong> radio button on <strong>Create Message</strong> screen
  of Countly Dashboard.
</p>
<p>
  If you want to manually mark your device as a test device for Distribution builds
  like TestFlight or AdHoc, you can use <code>IsTestDevice</code> flag on
  <code>CountlyConfig</code> object.
</p>
<pre><code class="csharp">config.IsTestDevice = true;</code></pre>
<ul>
  <li>
    <strong>Disable Alerts Shown by Notification</strong>
  </li>
</ul>
<p>
  For disabling automatically showing of messages by
  <code>CLYPushNotifications</code> feature, you can set
  <code>doNotShowAlertForNotifications</code> flag on <code>CountlyConfig</code>
  object. If set, no message will be displayed by using default system UI in the
  app, but push open event will be recorded automatically.
</p>
<pre><code class="csharp">config.DoNotShowAlertForNotifications = true;</code></pre>
<ul>
  <li>
    <strong>Send Push Token Always</strong>
  </li>
</ul>
<p>
  Thanks to Remote Notification Background Mode of iOS, it is possible to send
  silent push notifications to users who have not given notification permission.
  But Countly iOS SDK does not send push tokens to server by default, from users
  who have not given permission for notifications. You can change this by setting
  <code>sendPushTokenAlways</code> flag of <code>CountlyConfig</code> object. If
  set, push tokens from all users regardless of their notification permission status
  will be sent to Countly server and these users will be listed as possible recipients
  on <strong>Create Message</strong> screen of Countly Dashboard. As these users
  are not able to be notified by alert, sound or badge, be advised this is useful
  only for sending data via silent notifications.
</p>
<pre><code class="csharp">config.SendPushTokenAlways = true;</code></pre>
<ul>
  <li>
    <strong>Notification Permission with Preferred Types and Callback</strong>
  </li>
</ul>
<p>
  As asking for user's permission for push notifications differ by iOS versions,
  Countly iOS SDK has a one-liner convenience method
  <code>askForNotificationPermission</code> for both iOS10 and older versions.
  It simply asks for user's permission for all available notification types. But
  if you need to specify which notification types your app will use (alert, badge,
  sound) or if you need a callback to see user's response to permission dialog
  you can use <code>AskForNotificationPermissionWithOptions()</code> method.
</p>
<pre><code class="csharp">UNAuthorizationOptions authorizationOptions = UNAuthorizationOptions.Alert | UNAuthorizationOptions.Badge | UNAuthorizationOptions.Sound;
            Countly.SharedInstance().AskForNotificationPermissionWithOptions(authorizationOptions, (arg1, arg2) =&gt; Console.WriteLine(arg1));
</code></pre>
<ul>
  <li>
    <strong>Provide Geolocation [Enterprise Edition only]</strong>
  </li>
</ul>
<p>
  Countly lets you send GeoLocation based push notifications to your users. By
  default, Countly Server uses geoip database to deduce user's location. But, if
  your app has better means of detecting location, you can send this information
  to Countly Server by using initial configuration properties or relevant methods.
</p>
<p>
  Initial configuration properties can be set on <code>CountlyConfig</code> object,
  to be sent on SDK initialization. These are:
</p>
<p>
  <code>Location</code> a CLLocationCoordinate2D struct specifying latitude and
  longitude. <code>ISOCountryCode</code> an NSString in ISO 3166-1 alpha-2 format
  country code. <code>City</code> an NSString specifying city name.
  <code>IP</code> an NSString specifying IP address in IPv4 or IPv6 format.
</p>
<pre><code class="csharp">config.ISOCountryCode = @"IN";
config.City = @"Noida";
config.Location = new CLLocationCoordinate2D(28.5986, 77.3339);
config.IP = @"255.255.255.255";</code></pre>
<p>
  GeoLocation info recording methods also can be called anytime after Countly iOS
  SDK started. Values recorded using these methods will override the values specified
  on initial configuration.
</p>
<pre><code class="csharp">Countly.SharedInstance().RecordLocation(new CLLocationCoordinate2D(28.5986, 77.3339));
Countly.SharedInstance().RecordCity(@"India", "IN");
Countly.SharedInstance().RecordIP(@"255.255.255.255");</code></pre>
<p>GeoLocation info can also be disabled:</p>
<pre><code class="csharp">Countly.SharedInstance().DisableLocationInfo();</code></pre>
<p>
  Once disabled, you can re-enable GeoLocation info by calling
  <code>RecordLocation:</code> or <code>RecordCity:</code> and
  <code>ISOCountryCode:</code> or <code>RecordIP:</code> method.
</p>
<h1>Crash Reporting</h1>
<p>
  For using Countly CrashReporting, you'll need to specify
  <strong>CLYCrashReporting</strong> in features array on
  <strong>CountlyConfig</strong> object before starting Countly.
</p>
<pre><code class="csharp"> config.Features = new NSObject[] { Constants.CLYCrashReporting };</code></pre>
<p>
  With this feature, Countly iOS SDK will generate a crash report if your application
  crashes due to an exception, and send it to Countly Server for further inspection.
  If a crash report can not be delivered to server (e.g. no internet connection,
  unavailable server), then Countly iOS SDK stores the crash report locally in
  order to try again later.
</p>
<p>
  For iOS, a crash report includes following information in addition to Countly
  Analytics already provides:
</p>
<ul>
  <li>Exception Info:</li>
  <li>Exception Name</li>
  <li>Exception Description</li>
  <li>Stack Trace</li>
  <li>
    <p>Binary Images</p>
  </li>
  <li>
    <p>Device Static Info:</p>
  </li>
  <li>Device Type</li>
  <li>Device Architecture</li>
  <li>Resolution</li>
  <li>Total RAM</li>
  <li>
    <p>Total Disk</p>
  </li>
  <li>
    <p>Device Dynamic Info:</p>
  </li>
  <li>Used RAM</li>
  <li>Used Disk</li>
  <li>Battery Level</li>
  <li>Connection Type</li>
  <li>
    <p>Device Orientation</p>
  </li>
  <li>
    <p>OS Info:</p>
  </li>
  <li>OS Name</li>
  <li>OS Version</li>
  <li>OpenGL ES Version</li>
  <li>
    <p>Jailbrake State</p>
  </li>
  <li>
    <p>App Info:</p>
  </li>
  <li>App Version</li>
  <li>App Build Number</li>
  <li>Executable Name</li>
  <li>Time Since App Launch</li>
  <li>
    <p>Background State</p>
  </li>
  <li>
    <p>Custom Info:</p>
  </li>
  <li>
    Crash logs recorded using <code>recordCrashLog:</code> method
  </li>
  <li>
    Crash segmentation specified in <code>crashSegmentation</code> property
  </li>
</ul>
<p>
  You can use <code>crashLog:</code> method to get custom logs with the crash reports.
</p>
<pre><code class="csharp"> Countly.SharedInstance().CrashLog("CrashLog");</code></pre>
<p>
  If you want to use custom crash segmentation you can set optional
  <strong>CrashSegmentation</strong> on ConfigObject:
</p>
<pre><code class="csharp">  config.CrashSegmentation = new NSDictionary("Key","value");</code></pre>
<p>
  You can records handled exception manually, besides automatically reported unhandled
  exceptions and crashes. You can also manually pass stack trace at the time of
  handled exception.
</p>
<h2>Symbolication</h2>
<div class="callout callout--info">
  <h3 class="callout__title">Enterprise Edition Feature</h3>
  <p>
    This feature is only available with
    <a href="http://count.ly/enterprise-edition">Enterprise Edition</a> subscription.
  </p>
</div>
<p>
  Symbolication is the process of converting stack trace memory addresses in crash
  reports, into human readable useful information like class/method names, file
  names and line numbers.
</p>
<p>
  In order to symbolicate memory addresses, dSYM files for each build needs to
  be uploaded to Countly Server.
</p>
<h3>Automatic dSYM Uploading</h3>
<p>
  For Automatic dSYM Uploading, you can use <code>countly_dsym_uploader</code>
  script in Countly iOS SDK from git.
</p>
<p>
  For this, go to <code>Options</code> section of your app then
  <code>Build -&gt; Custom Commands</code>, and click on (select a project operation)
  drop down icon on the top left, then choose <code>New Run Script Phase</code>
  in the list.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/e4550ac-Screen_Shot_2018-05-23_at_1.47.42_PM.png">
</div>
<p>Then, add the following snippet:</p>
<pre><code class="text">COUNTLY_DSYM_UPLOADER=$(/usr/bin/find $SRCROOT -name "countly_dsym_uploader.sh" | head -n 1)
sh "$COUNTLY_DSYM_UPLOADER" "https://YOUR_COUNTLY_SERVER" "YOUR_APP_KEY"</code></pre>
<p>
  <strong>Note:</strong> Do not forget to replace your server and app key.
</p>
<p>
  By default Xcode will generate dSYM files for Release build configuration, and
  <code>countly_dsym_uploader</code> script will handle the uploading automatically.
  You can check for the result at Report Navigator in Xcode. If dSYM upload is
  completed successfully, you will see
  <code>[Countly] dSYM upload succesfully completed.</code> message.
</p>
<h3>Manual dSYM Uploading</h3>
<p>
  In case of an error with Automatic dSYM Uploading, or just if you want to upload
  your dSYM files manually, you can use our guide for Manual dSYM Uploading
  <a href="https://resources.count.ly/v1.0/docs/crash-symbolication#section-uploading-the-symbol-file">here</a>.
  You also need to use Manual dSYM Uploading if Bitcode is enabled while uploading
  your app to the iTunes Connect.
</p>
<h1>User Profiles</h1>
<div class="callout callout--info">
  <p>
    This feature is available with
    <a href="http://count.ly/enterprise-edition">Enterprise Edition</a> subscription.
  </p>
</div>
<p>
  You can see detailed user information under User Profiles section of Countly
  Dashboard by recording user details. You can record default and custom properties
  of user details like this:
</p>
<pre><code class="csharp">//default properties
 
Countly.User.Name = "John Doe";
Countly.User.Username = "john";
Countly.User.Email = "johndoe@apple.com";
Countly.User.BirthYear = "1974";
Countly.User.Organization = "United States";
Countly.User.Gender = "F";
Countly.User.Phone = "+0123456789";
Countly.User.PictureURL = @"http://s12.postimg.org/qji0724gd/988a10da33b57631caa7ee8e2b5a9036.jpg";
Countly.User.PictureLocalPath = localImagePath;

//save
Countly.User.Save();</code></pre>
<p>
  In addition, you can use custom user details modifiers like this:
</p>
<pre><code class="csharp">Countly.User.Set(@"key101", @"value101");
Countly.User.IncrementBy(@"key102", 5);
Countly.User.Multiply(@"key102", 2);
Countly.User.Max(@"key102", 30);
Countly.User.Min(@"key102", 20);
Countly.User.Push(@"key103", "a");
Countly.User.PushUnique(@"key104", @"uniqueValue");
Countly.User.Pull(@"key103", @"b");
Countly.User.Save();

//save
Countly.User.Save();</code></pre>
<h1>View Tracking</h1>
<p>
  For using Countly <strong>AutoViewTracking</strong>, you'll need to specify
  <strong>CLYAutoViewTracking</strong> in features array on CountlyConfig object
  before starting Countly:
</p>
<pre><code class="csharp">config.Features = new NSObject[] { Constants.CLYAutoViewTracking };</code></pre>
<p>
  You can temporarily enable or disable Auto View Tracking using 'IsAutoViewTrackingEnabled'
  property.
</p>
<pre><code class="csharp">Countly.SharedInstance().IsAutoViewTrackingEnabled = true;
</code></pre>
<p>
  If Auto View Tracking feature is not enabled on initial configuration, enabling
  or disabling this property later has no effect. It will always be disabled.
</p>
<h2>Exception View Controllers</h2>
<p>
  By default, following system view controllers will be excluded from auto tracking,
  as they are not visible views but structural controllers:
</p>
<pre><code>UINavigationController
UIAlertController
UIPageViewController
UITabBarController
UIReferenceLibraryViewController
UISplitViewController
UIInputViewController
UISearchController
UISearchContainerViewController
UIApplicationRotationFollowingController
MFMailComposeInternalViewController
MFMailComposeInternalViewController
MFMailComposePlaceholderViewController
UIInputWindowController
_UIFallbackPresentationViewController
UIActivityViewController
UIActivityGroupViewController
_UIActivityGroupListViewController
_UIActivityViewControllerContentController
UIKeyboardCandidateRowViewController
UIKeyboardCandidateGridCollectionViewController
UIPrintMoreOptionsTableViewController
UIPrintPanelTableViewController
UIPrintPanelViewController
UIPrintPaperViewController
UIPrintPreviewViewController
UIPrintRangeViewController
UIDocumentMenuViewController
UIDocumentPickerViewController
UIDocumentPickerExtensionViewController
UIInterfaceActionGroupViewController
UISystemInputViewController
UIRecentsInputViewController
UICompatibilityInputViewController
UIInputViewAnimationControllerViewController
UISnapshotModalViewController
UIMultiColumnViewController
UIKeyCommandDiscoverabilityHUDViewController
</code></pre>
<p>
  In addition to these default exceptions, you can manually add your own exception
  view controllers using <code>AddExceptionForAutoViewTracking:</code> method by
  passing view controller class name or title:
</p>
<pre><code class="csharp"> Countly.SharedInstance().AddExceptionForAutoViewTracking("MyViewControllerTitle");</code></pre>
<p>
  If AutoViewTracking feature is not enabled on start configuration, enabling or
  disabling this property later has no effect.
</p>
<h2>Manual View Tracking</h2>
<p>
  In addition to AutoViewTracking, you can manually report appearance of a view
  using <code>ReportView()</code> method with views name:
</p>
<pre><code class="csharp">Countly.SharedInstance().ReportView("my View");</code></pre>
<p>
  When you report another view, duration of previous view will be calculated and
  view tracking event will be recorded automatically.
</p>
<p>
  <strong>Consents</strong>
</p>
<p>
  For compatibility with data protection regulations such as GDPR, Countly iOS
  SDK allows developers to enable/disable any feature at any time, depending on
  user consent. Currently available features with consent control are:
</p>
<p>
  <code>CLYConsentSessions</code> : <code>sessions</code>
  <code>CLYConsentEvents</code> : <code>events</code>
  <code>CLYConsentUserDetails</code> : <code>users</code>
  <code>CLYConsentCrashReporting</code> : <code>crashes</code>
  <code>CLYConsentPushNotifications</code> : <code>push</code>
  <code>CLYConsentLocation</code> : <code>location</code>
  <code>CLYConsentViewTracking</code> : <code>views</code>
  <code>CLYConsentAttribution</code> : <code>attribution</code>
  <code>CLYConsentStarRating</code> : <code>star-rating</code>
  <code>CLYConsentAppleWatch</code> : <code>accessory-devices</code>
</p>
<p>
  To utilize consents, you should set <code>RequiresConsent</code> flag is set
  on initial configuration.
</p>
<pre><code class="csharp">config.RequiresConsent = true;</code></pre>
<p>
  With this flag set, Countly iOS SDK will not collect or send any data automatically,
  as well as ignoring all manual calls. Until explicit consent is given for a feature,
  it will be inactive. After giving consent for a feature, it will be started immediately
  and kept active henceforth.
</p>
<p>
  To give consent for a feature you can use <code>GiveConsentForFeature:</code>
  method, passing the feature name:
</p>
<pre><code class="csharp">Countly.SharedInstance().GiveConsentForFeature(Constants.CLYConsentEvents);
            Countly.SharedInstance().GiveConsentForFeature(Constants.CLYAutoViewTracking);
            Countly.SharedInstance().GiveConsentForFeature(Constants.CLYConsentCrashReporting);
            Countly.SharedInstance().GiveConsentForFeature(Constants.CLYConsentLocation);
            Countly.SharedInstance().GiveConsentForFeature(Constants.CLYPushNotifications);
Countly.SharedInstance().GiveConsentForAllFeatures();</code></pre>
<p>
  Countly iOS SDK does not persistently store status of given consents. You are
  expected to handle getting consent from end-users using proper UIs depending
  on your app's context, and storing them either locally or remotely. Following
  this, you need to call giving consent methods on each app launch, just after
  starting Countly iOS SDK, depending on the permissions you managed to get from
  the end-users.
</p>
<p>
  If the end-user changes his/her mind about consents later, you need to reflect
  this to Countly iOS SDK, using <code>CancelConsentForFeature:</code> method:
</p>
<pre><code class="csharp">Countly.SharedInstance().CancelConsentForFeature(Constants.CLYPushNotifications);</code></pre>
<p>
  Or, if you want to cancel consent for all the features, you can use
  <code>CancelConsentForAllFeatures</code> convenience method:
</p>
<pre><code class="csharp">Countly.SharedInstance().CancelConsentForAllFeatures();</code></pre>
<p>
  Once consent for a feature is cancelled, that feature is stopped immediately
  and kept inactive henceforth.
</p>
<p>
  Countly iOS SDK reports consent changes to Countly Server, so Countly Server
  can do preparations or clean-up on server side as well.
</p>