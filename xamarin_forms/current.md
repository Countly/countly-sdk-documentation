<p>
  This document includes necessary information for integrating Countly iOS SDK
  in your Xamarin.Forms project.
</p>
<div class="callout callout--info">
  <h3 class="callout__title">Minimum iOS version</h3>
  <p>
    Countly iOS SDK needs a minimum of <strong>iOS 8.0</strong> ( macOS 10.9)
    to work.
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
    Add a new Xamarin.iOS project called CountryTestDemo to the solution,
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

namespace CountlyTestDemo.iOS
{
    [Register("AppDelegate")]
    public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.
                             FormsApplicationDelegate
    {
        public override bool FinishedLaunching(UIApplication app, 
        NSDictionaryoptions)
        {
            global::Xamarin.Forms.Forms.Init();
            CountlyConfig config = new CountlyConfig();
            config.AppKey = "your_App_Key";
            config.Host = "https://YOUR_COUNTLY_SERVER";
            Countly.SharedInstance().StartWithConfig(config);
            LoadApplication(new App());
            return base.FinishedLaunching(app, options);
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
  be <code>https://try.count.ly</code>, <code>https://us-try.count.ly</code> or
  <code>https://asia-try.count.ly</code>. Basically the domain you are accessing
  your trial dashboard from.
</p>
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
<pre><code class="csharp"> public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.
                             FormsApplicationDelegate
    {
        public override bool FinishedLaunching(UIApplication app, 
        NSDictionaryoptions)
        {
            global::Xamarin.Forms.Forms.Init();
            CountlyConfig config = new CountlyConfig();
            config.AppKey = "your_App_Key";
            config.Host = "https://YOUR_COUNTLY_SERVER";
            config.Features = new NSObject[] { Constants.CLYPushNotifications,                  Constants.CLYCrashReporting, Constants.CLYAutoViewTracking };
            Countly.SharedInstance().StartWithConfig(config);
            LoadApplication(new App());
            return base.FinishedLaunching(app, options);
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
  when number of recorded events reach it without waiting for next update session
  request.
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
    <strong>Additional Info</strong>
  </li>
</ul>
<p>
  You can set additional Country, City and Location (coordinates) information to
  be sent with each session, using <code>ISOCountryCode</code>,
  <code>City</code> and <code>Location</code> properties on
  <code>CountlyConfig</code> object.
</p>
<p>
  <code>ISOCountryCode</code> should be an NSString. <code>City</code> should be
  an NSString specifying city name. <code>Location</code> should be a CLLocationCoordinate2D
  struct specifying latitude and longitude.
</p>
<pre><code class="csharp">config.ISOCountryCode = "IN";
config.City = "Noida";
config.Location = new CLLocationCoordinate2D(28.5986, 77.3339);</code></pre>
<ul>
  <li>
    <strong>Custom Header Field</strong>
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
  Here is a quick summary on how to use event recording methods.
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
<pre><code class="csharp">[Register("AppDelegate")]
public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate
    {

        public override bool FinishedLaunching(UIApplication app, NSDictionary options)
        {
            global::Xamarin.Forms.Forms.Init();
            LoadApplication(new App());
            app.WeakDelegate = new MyDelegate();

            //Basic Setting for countly server
            CountlyConfig config = new CountlyConfig();
            config.AppKey = @"your_App_Key";
            config.Host = @"https://YOUR_COUNTLY_SERVER";
            config.Features = new NSObject[] { Constants.CLYPushNotifications };  
            Countly.SharedInstance().AskForNotificationPermission();
 
            return base.FinishedLaunching(app, options);
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
  By default, Countly server uses geoip database to acquire location of a user.
  But in case your app uses Core Location services, you can provide better accuracy
  location to Countly iOS SDK by calling <code>RecordLocation()</code> method with
  coordinates acquired from Core Location. Please do not call this method on each
  location update, because this will result in too many requests sent to Countly
  server. Once or twice per app launch is enough.
</p>
<pre><code class="csharp">Countly.SharedInstance().RecordLocation(new CLLocationCoordinate2D(28.5986, 77.3339));
</code></pre>
<p>
  Note that this feature is available to set location information for push notification
  - it doesn't update user's city in User Profiles.
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
  <li>Exception Name</li>
  <li>Exception Description</li>
  <li>Stack Trace</li>
  <li>Used RAM</li>
  <li>Total RAM</li>
  <li>Used Disk</li>
  <li>Total Disk</li>
  <li>Battery Level</li>
  <li>Device Orientation</li>
  <li>Connection Type</li>
  <li>OpenGL ES Version</li>
  <li>Jailbrake State</li>
  <li>Background State</li>
  <li>Time Since Launch</li>
  <li>App Build Number</li>
  <li>App BuildUUID</li>
  <li>
    Custom Logs generated by <code>crashLog:</code> method (if any)
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
  exceptions and crashes.
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

//save
Countly.User.Save();</code></pre>
<p>
  In addition, you can use custom user details modifiers like this:
</p>
<pre><code class="csharp">Countly.User.Set("key101","value101");
Countly.User.IncrementBy("key102",5);
Countly.User.Multiply("key102",2);
Countly.User.Max("key102",30);
Countly.User.Min("key102",20);
Countly.User.Push("key103","a");
Countly.User.PushUnique("key104","uniqueValue");

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
  After this point Countly iOS SDK will automatically track appeared and disappeared
  views.
</p>
<p>
  In addition to these default exceptions, you can manually add your own exception
  view controllers using <code>AddExceptionForAutoViewTracking:</code> method by
  passing view controller class name or title:
</p>
<pre><code class="csharp"> Countly.SharedInstance().AddExceptionForAutoViewTracking("MyViewControllerTitle");</code></pre>
<p>
  You can enable or disable AutoViewTracking using
  <code>IsAutoViewTrackingEnabled</code> property.
</p>
<pre><code class="csharp">Countly.SharedInstance().IsAutoViewTrackingEnabled = true;</code></pre>
<p>
  If AutoViewTracking feature is not enabled on start configuration, enabling or
  disabling this property later has no effect.
</p>
<p>
  In addition to AutoViewTracking, you can manually report appearance of a view
  using <code>ReportView()</code> method with views name:
</p>
<pre><code class="csharp">Countly.SharedInstance().ReportView("my View");</code></pre>
<p>
  When you report another view, duration of previous view will be calculated and
  view tracking event will be recorded automatically.
</p>