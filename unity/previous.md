<p>
  This document explains how to download, setup and use Unity SDK for Countly.
  You can
  <a href="http://github.com/countly/countly-sdk-unity">download latest release from Github</a>.
</p>
<p>
  Following are some of the key assumptions being considered while developing the
  SDK. Please take into account following considerations before integrating this
  SDK:
</p>
<ol>
  <li>This SDK is developed in Unity 2018 2.7f1</li>
  <li>Scripting version is based on .NET 4.x equivalent</li>
  <li>API Compatibility Level is based on .NET 4.x</li>
</ol>
<h1>Integration</h1>
<ol>
  <li>
    Clone/download the source code from github-
    <a href="https://github.com/Countly/countly-sdk-unity">https://github.com/Countly/countly-sdk-unity</a>
  </li>
  <li>Unzip the package (if you have downloaded ZIP file).</li>
  <li>
    Look for a folder named “Assets”. Copy all the contents of “Assets” folder
    and paste it inside your app’s Assets folder. Unity will import the new assets
    now.
  </li>
  <li>
    Now, update the following player settings: a. Package Name: App's Bundle
    ID b. Scripting Runtime Version: .NET 4x Equivalent
  </li>
  <li>
    Create an account on Firebase (firebase.google.com). Go to Firebase Console
    (<a href="https://console.firebase.google.com/).">https://console.firebase.google.com/).</a>
    Create a new project.
  </li>
  <li>
    Add your app (Android/iOS) to the project created in Step 4. Specify the
    same package name that you specified in Unity Editor for your app.
  </li>
  <li>
    Register your app and download <code>google-services.json</code> for Android
    or <code>GoogleService-Info.plist</code> for iOS file, at Step 2 of the registration
    process. We do not need to proceed after step 2. So, leave the further steps.
  </li>
  <li>
    Place the file downloaded under your app's <code>Assets</code> folder.
  </li>
  <li>
    Run <code>Android Resolver</code> in case of Android from
    <code>Assets</code> &gt; <code>Play Service Resolver</code> &gt;
    <code>Android Resolver</code> =&gt; <code>Resolve</code>. For iOS we don’t
    need to do anything.
  </li>
  <li>
    Attach <code>AppInitScript.cs</code> file to the main scene of your Unity
    application.
  </li>
</ol>
<p>
  Note that a script named “Testing.cs” under folder “Assets\Scripts\Main\Testing”
  contains examples to test all the features of the SDK. You can take reference
  from this script to know how to utilize each feature of the SDK.
</p>
<h1>Initializing the SDK</h1>
<p>
  To initialize Countly Unity SDK, use following two methods with appropriate parameters.
  Note that the following two methods should be added inside your application start
  event, in the exact order with method <code>Begin</code> being called before
  method <code>SetDefaults</code>.
</p>
<p>
  <strong>Begin method</strong>
</p>
<pre><code class="csharp">Countly.Begin(string serverUrl, string appKey, string deviceId = null);</code></pre>
<p>
  <strong>serverUrl:</strong> Required <strong>Type:</strong> string
  <strong>Description:</strong> The URL of the Countly Server where you are going
  to post our requests. <strong>Example:</strong>
  <a href="https://us-try.count.ly/">https://us-try.count.ly/</a>
</p>
<p>
  <strong>appKey:</strong> Required <strong>Type:</strong> string
  <strong>Description:</strong> The “App Key” for the app that you created on Countly
  Server. <strong>Example:</strong> 124qw3er5u678qwef88d6123456789qwertyui123
</p>
<p>
  <strong>deviceId:</strong> Optional <strong>Type:</strong> string
  <strong>Description:</strong> Your Device ID. It is an optional parameter.
  <strong>Example:</strong> f16e5af2-8a2a-4f37-965d-qwer5678ui98
</p>
<p>
  If you do not provide device ID during initialization, SDK will generate a Device
  ID on its own and use this Device ID for all future requests made to the Countly
  server. This Device ID is persisted by the SDK per device.
</p>
<p>
  If you provide a device ID to the SDK and later you are initializing the SDK
  again with a different device ID, the old Device ID will be used by the SDK and
  not the new one because the priority is as follows:
</p>
<p>
  <em>Cached Device ID &gt; Provided Device ID Upon Initialization &gt; SDK Generated Device ID</em>
</p>
<div class="callout callout--info">
  <h3 class="callout__title">Which server/host name should I use inside SDK?</h3>
  <p>
    If you are using Countly Enterprise Edition trial servers, use corresponding
    server name, e.g <a href="https://try.count.ly,">https://try.count.ly,</a>
    <a href="https://us-try.count.ly">https://us-try.count.ly</a> or
    <a href="https://asia-try.count.ly">https://asia-try.count.ly</a>
  </p>
  <p>
    If you use Community Edition and Enterprise Edition, use your own domain
    name.
  </p>
</div>
<p>
  <strong>SetDefaults</strong>
</p>
<p>
  This method takes as input an instance of <code>CountlyConfigModel</code> class.
  The constructor for <code>CountlyConfig</code> model takes following list of
  parameters (the default values are mentioned alongside each one of them):
</p>
<ol>
  <li>string salt = NULL</li>
  <li>bool enablePost = false</li>
  <li>bool enableConsoleErrorLogging = false</li>
  <li>bool ignoreSessionCooldown = false</li>
  <li>bool enableManualSessionHandling = false</li>
  <li>int sessionDuration = 60</li>
  <li>int eventThreshold = 100</li>
  <li>int storedRequestLimit = 1000</li>
  <li>int totalBreadcrumbsAllowed = 100</li>
  <li>TestMode? notificationMode = NULL</li>
  <li>bool enableAutomaticCrashReporting = true</li>
</ol>
<p>Below you can find details of each method.</p>
<p>
  <strong>salt:</strong> Used to prevent parameter tampering.
  <strong>Type:</strong> string
</p>
<p>
  <strong>enablePost:</strong> When set to true, all requests made to the Countly
  Server will be done using HTTP POST. Otherwise, SDK sends all requests using
  HTTP GET method. In some cases, if the data to be sent exceeds 1800 characters
  limit, the SDK uses POST method. <strong>Type:</strong> bool
</p>
<p>
  <strong>enableConsoleErrorLogging:</strong> This parameter is only useful when
  you are debugging your application in Unity Editor. When set to true, it basically
  turns on Error Logging on Unity Console window <strong>Type:</strong> bool
</p>
<p>
  <strong>ignoreSessionCooldown:</strong> To turn on/off session cooldown behavior
  as mentioned in the development-guide <strong>Type:</strong> bool
</p>
<p>
  <strong>enableManualSessionHandling: </strong>To turn on/off manual session handling
  in the application. <strong>Type:</strong> bool
</p>
<p>
  <strong>sessionDuration:</strong> To set the interval (in seconds) after which
  the application will automatically extend the session provided manual session
  is disabled. This interval is also used to process requests in queue. The default
  value is 60 (seconds). <strong>Type:</strong> bool
</p>
<p>
  <strong>eventThreshold:</strong> To set a threshold value that limits the number
  of events that can be recorded internally by the system before they all can be
  sent together in one request. Once the threshold limit is reached, the system
  groups all recorded events and send them to the server. The default value is
  100 (events). <strong>Type:</strong> int
</p>
<p>
  <strong>totalBreadcrumbsAllowed:</strong> To set a threshold value that limits
  the number of requests that can be stored internally by the system. The system
  processes these requests after every sessionDuration interval has passed. The
  default value is 1000 (requests). <strong>Type:</strong> int
</p>
<p>
  <strong>notificationMode (Optional):</strong> When null, SDK disables Push Notification
  for the device. Otherwise, when provided an appropriate value from the enum TestMode,
  SDK uses the supplied mode for sending Push Notifications.
  <strong>Type:</strong> Enum of type TestMode
</p>
<p>
  <strong>enableAutomaticCrashReporting (Optional):</strong> This is used to turn
  on/off automatic crash reporting. When set to true, SDK will catch exceptions
  and automatically report them to the Countly server, otherwise not.
  <strong>Type:</strong> bool
</p>
<pre><code class="csharp">var configObj = new CountlyConfigModel(null, false, false, false, false, 60, 100, 1000, 100, TestMode.TestToken, false);
await Countly.SetDefaults(configObj);
</code></pre>
<h1>Session handling</h1>
<p>
  Unity SDK can handle sessions in two ways: Automatic session handling and manual
  session handling. If you are in doubt, use automatic session handling.
</p>
<h3>Automatic Session Handling</h3>
<p>
  <strong>Begin Session:</strong> SDK is responsible for automatically handling
  Countly session in your app. As soon as you call the initialization methods (Begin
  and SetDefaults) in your app start event, SDK will start the session automatically
  (only when you set <code>enableManualSessionHandling</code> to true during initialization).
</p>
<p>
  <strong>Update Session:</strong> SDK is responsible for automatically extending
  the session after every 60 seconds (default value). This value is configurable
  during initialization using parameter sessionDuration. It cannot be modified
  any time after initialization.
</p>
<p>
  Note that in iOS, session will not extend when the app is in background. As soon
  as user switches back to the app, session extension will resume. In Android,
  session will extend on both occasions: foreground and background.
</p>
<p>
  <strong>End Session:</strong> SDK is responsible for automatically ending the
  session whenever user quits the application.
</p>
<p>
  Session will be ended automatically when user calls Application.Quit() method
  available in Unity.
</p>
<h3>Manual Session Handling</h3>
<p>
  This is used when you want to start a session on your app manually.
</p>
<p>
  <strong>Begin Session:</strong> Starts the session manually. You need to call
  the following method:
</p>
<pre><code class="csharp">Countly.BeginSessionAsync();</code></pre>
<p>
  <strong>Update Session:</strong> Extends the session manually. You need to call
  following method:
</p>
<pre><code class="csharp">Countly.ExtendSessionAsync();</code></pre>
<p>
  <strong>End Session:</strong> Ends the session manually. You need to call the
  following method:
</p>
<pre><code class="csharp">Countly.EndSessionAsync()</code></pre>
<h1>Optional parameters</h1>
<p>
  Countly servers recognize the location of the user’s device from their IP address.
  However, you can also specify user’s location manually using the following methods.
</p>
<p>
  <strong>Note:</strong> You need to use the following methods in conjunction to
  specify the exact location manually. Also, IP address can be left out intentionally
  when you want to specify a location but don’t have access to user’s IP address.
  This is because Countly server gives priority to IP address. So, if you’ve specified
  country, city and coordinates of a different location and IP address of a different
  location, Countly server will choose the location from the IP address.
</p>
<h3>Setting country code</h3>
<p>
  In order set the country, you need to call method <code>SetCountryCode</code>.
</p>
<p>
  Syntax: <code>Countly.SetCountryCode(string country_code);</code>
</p>
<p>
  <strong>country_code (required)</strong> Type: string Desc: It takes an ISO Country
  Code in string format, as parameter. Ex:
  <code>Countly.SetCountryCode(“au”);</code>
</p>
<h3>Setting city</h3>
<p>
  In order to set the city, you need to call method <code>SetCity.</code>
</p>
<p>Syntax: Countly.SetCity(string cityname);</p>
<p>
  <strong>cityname (required)</strong> Type: string Desc: It takes name of the
  city in string format, as parameter. Ex:
  <code>Countly.SetCity(“Berlin”);</code>
</p>
<h3>Setting location</h3>
<p>
  In order to set the coordinates, you need to use method
  <code>SetLocation</code>. Syntax:
  <code>SetLocation(double latitude, double longitude);</code>
</p>
<p>There are two parameters, latitude and longitude:</p>
<p>
  <strong>latitude and longitude (required)</strong> Type: double Ex:
  <code>Countly.SetLocation(34.9285,138.6007);</code>
</p>
<h3>Setting IP address</h3>
<p>
  You can choose to set (overwrite) the IP address of the user’s device. In order
  to set the IP Address, you need to first get user’s device IP Address and then
  use method <code>SetIPAddress</code>.
</p>
<p>
  Syntax: <code>Countly.SetIPAddress(string ip_address);</code>
</p>
<p>
  <strong>ip_address (required) </strong> Type: string Desc: It takes IP address
  of the user’s device. Ex:
  <code>Countly.SetIPAddress(“SOME_IP_ADDRESS”);</code>
</p>
<h3>Disabling location</h3>
<p>
  This will completely remove and disable everything that has been previously set
  in context of location like country, city, location and IP address.
</p>
<p>Parameter(s): None Ex: `Countly.DisableLocation();``</p>
<h3>Events</h3>
<p>
  Unity SDK allows you to report custom events. An event can be anything which
  is a user action, e.g button click, hover, purchases or level passing information.
  You can report any type of events to the Countly server.
</p>
<p>
  Unity SDK helps record as many events as you can (you can set a threshold limit
  during initialization), and the system will send them automatically to the server
  once the threshold limit is reached. By default, Countly tracks only up to 500
  events, however this is also configurable.
</p>
<p>
  <strong>Note:</strong> You need to first set the threshold value that decides
  the number of events that can be recorded by the system, i.e.,
  <code>EventSendThreshold</code> value, during initialization. The default value
  is 100. Once SDK records this much events, SDK will send all collected events
  at once in a single request.
</p>
<p>Below you can find methods for sending custom events.</p>
<p>
  <strong>Recording an event:</strong> You can record an event by providing the
  event name. The event will not be reported to the Countly server immediately
  and will be reported to the server once the threshold limit is reached.
</p>
<p>
  <strong>Syntax: <code>Countly.RecordEventAsync(string key);</code></strong> key:
  required Type: string Desc: The name of the event. Example:
  <code>Countly.RecordEventAsync(“Game_Level_X_Started”);</code>
</p>
<p>
  <strong>Recording an event (overload):</strong> This is an overload to the method
  we defined above. We can provide other information related to the particular
  event with this overload method.
</p>
<p>
  Syntax:
  <code>Countly.RecordEventAsync(string key, IDictionary&lt;string, object&gt; segmentation,
int? count = 1, double? sum = 0, double? duration = null)</code>
</p>
<p>Parameter(s):</p>
<p>
  <strong>key (required)</strong> Type: string Desc: The name of the event.
</p>
<p>
  <strong>segmentation (optional)</strong> Type: IDictionary&lt;string, object&gt;
  Desc: Payload data to be sent along with the event
</p>
<p>
  <strong>count (optional)</strong> Type: integer Desc: Default value is 1
</p>
<p>
  <strong>sum (optional)</strong> Type: double Duration: Optional Type: double
</p>
<p>Example:</p>
<pre><code class="csharp">Countly.RecordEventAsync("Game_Level_X_Started",
				new Dictionary&lt;string, object&gt;
                        { 
				{ "Time Spent", "1234455"}, 
			{ "Retry Attempts", "10"}
			});
</code></pre>
<h1>Crash Reporting</h1>
<p>
  Unity SDK has the option to send crash reports to your Countly service. This
  can be done in two ways, automatic and manual.
</p>
<h3>Automatic crash reporting</h3>
<p>
  Countly Unity SDK automatically reports uncaught exceptions/crashes, in the application,
  to the Countly server.
</p>
<h3>Manual Crash Reporting</h3>
<p>
  Apart from automatically reporting crashes/uncaught exceptions to the Countly
  server, the SDK allows you to report your custom errors by using method
  <code>SendCrashReportAsync</code>.
</p>
<p>Syntax:</p>
<pre><code class="csharp">Countly.SendCrashReportAsync(string message, string stackTrace, LogType type, IDictionary&lt;string, object&gt; segments = null)
</code></pre>
<p>Parameters:</p>
<p>
  <strong>message (required)</strong> Type: string Desc: Complete error message.
</p>
<p>
  <strong>stackTrace (required)</strong> Type: string Desc: Complete stack trace
  of the exception.
</p>
<p>
  <strong> type (required)</strong> Type: A value of enum LogType, defined under
  UnityEngine namespace. Desc: You can choose from the various values defined in
  the enum LogType.
</p>
<p>
  <strong>segments (optional)</strong> Type: IDictionary&lt;string, object&gt;
  Desc: Custom data in key-value pairs of string and object. This data will be
  posted to the Countly server along with the exception details.
</p>
<p>
  <strong>Using breadcrumbs</strong>
</p>
<p>
  Additionally, SDK allows you to leave breadcrumbs that would be submitted together
  with the crash reports. These breadcrumbs are added automatically and sent along
  with the crash report (for both automatically caught and manually caught exceptions).
</p>
<p>
  You can add breadcrumbs in the SDK using method <code>AddBreadcrumbs</code>.
  A breadcrumb is a string with at most 1000 character and this cannot be modified.
  We can add a maximum of 100 breadcrumbs (as it is default value) in the system.
  However, we can modify this during initialization with parameter
  <code>totalBreadcrumbsAllowed</code>.
</p>
<p>
  Syntax: <code>Countly.AddBreadcrumbs(string breadcrumb);</code> Parameter(s):
  breadcrumb: A string value Type: String
</p>
<h1>Setting up views</h1>
<p>Manual View (Screen) Tracking</p>
<p>
  Countly Unity SDK supports manual view (screen) tracking. With this feature,
  you can report what views a user did, and for how long. Thus, whenever there
  is a screen switch in your app, you can report it to Countly server by using
  following method:
</p>
<p>
  Syntax: `Countly.ReportViewAsync(string name, bool hasSessionBegunWithView =
  false);``
</p>
<p>Parameter(s):</p>
<p>
  name (required) Type: string Desc: The name of the view to be reported.
</p>
<p>
  hasSessionBegunWithView (optional) Type: bool Desc: Set it to true to indicate
  that the session started with this view
</p>
<p>
  Ex: <code>Countly.ReportViewAsync(“LoginScreen”);</code>
</p>
<h1>View Actions</h1>
<p>
  Additionally, it is possible to report actions taken on views to display on heat
  maps or any other purpose. For that, you need to use method ReportActionAsync.
</p>
<p>
  Syntax:
  <code>Countly.ReportActionAsync(string type, int x, int y, int width, int height);</code>
</p>
<p>Parameter(s):</p>
<p>
  type: action type, as click, touch, longpress, etc x: x coordinate of action
  y: y coordinate of action width: width of the screen height: height of the screen
</p>
<p>
  Ex: <code>Countly.ReportActionAsync("Touch", 0, 0, 50, 50);</code>
</p>
<h1>Star rating</h1>
<p>
  When a user rates your application, you can report it to the Countly server using
  method <code>ReportStarRatingAsync</code>. For this, you can optionally set Countly
  Unity SDK to automatically ask users for a 1-to-5 star-rating, depending on app
  launch count for each version.
</p>
<p>
  Syntax:
  <code>Countly.ReportStarRatingAsync(string platform, string app_version, int rating);</code>
</p>
<p>Parameter(s):</p>
<p>
  platform: platform on which application runs app_version: application's version
  number rating: user's 1-to-5 rating
</p>
<p>
  Ex: <code>Countly.ReportStarRatingAsync("android", "0.1", 3);</code>
</p>
<h1>User Profiles</h1>
<p>
  Countly Unity SDK allows you to upload specific data related to a user to Countly
  server. SDK allows you to set following predefined data for a particular user:
</p>
<ol>
  <li>Name: Full name of the user</li>
  <li>Username: Username of the user</li>
  <li>Email: Email address of the user</li>
  <li>Organization: Organization the user is working in</li>
  <li>Phone: Phone number</li>
  <li>Picture Url: Web based Url for user’s profile</li>
  <li>
    Gender: Gender of the user (use only single char like ‘M’ for Male and ‘F’
    for Female)
  </li>
  <li>Birth year: Birth year of the user</li>
</ol>
<p>
  Apart from the above data, you can also add your own custom data for a user.
  SDK allows you to upload user details using following methods. You may choose
  one of the following methods as per your requirement.
</p>
<h3>Setting user details</h3>
<p>
  You can set all the details (specified above) of a user along with some custom
  data using method <code>SetUserDetailsAsync</code>.
</p>
<p>
  Syntax: <code>SetUserDetailsAsync();</code> Parameter(s): None This method is
  an instance method and not a static method. It doesn’t take any parameters. You
  first need to create an instance of class <code>CountlyUserDetailsModel</code>.
  The constructor for this class takes following number of parameters:
</p>
<ol>
  <li>Name: String</li>
  <li>Username: String</li>
  <li>Email: String</li>
  <li>Organization: String</li>
  <li>Phone: String</li>
  <li>Gender: String</li>
  <li>Birth year: String</li>
  <li>
    Custom: String. It is a json string containing key-value pairs. It is used
    to send custom data.
  </li>
</ol>
<p>Example:</p>
<pre><code class="csharp">var userDetails = new CountlyUserDetailsModel(
                                "Full Name", "username", "useremail@email.com", "Organization",
                                "222-222-222",              
		        "http://webresizer.com/images2/bird1_after.jpg", 
        "M", "1986",
                                new Dictionary&lt;string, object&gt;
                                {
                                    { "Hair", "Black" },
                                    { "Race", "Asian" },
                                });
await userDetails.SetUserDetailsAsync();</code></pre>
<h3>Setting custom user details</h3>
<p>
  SDK allows you the flexibility to send only custom data to Countly servers when
  you don’t want to send other user related data. Similar to the above method,
  it is also an instance method and not a static method. So, you first need to
  create an instance of class <code>CountlyUserDetailsModel</code>. All the parameters
  expected in the constructor remain the same. You can leave all parameters as
  NULL and just provide the custom data segment for sending custom data to the
  Countly server.
</p>
<p>
  Syntax: <code>SetCustomUserDetailsAsync();</code> Parameter(s): None
</p>
<pre><code class="csharp">var userDetails = new CountlyUserDetailsModel(
                                new Dictionary&lt;string, object&gt;
                                {  
			{ "Nationality", "Indian" },
                                    { "Height", "5.8" },
                                    { "Mole", "Lower Left Cheek" } 
		         });
await userDetails.SetCustomUserDetailsAsync();

</code></pre>
<h3>Modifying Custom Data Properties</h3>
<p>
  Apart from setting user details (<code>SetUserDetailsAsync</code>) and custom
  user details (<code>SetCustomUserDetailsAsync</code>), SDK allows you to set/modify
  specific custom data properties. The system records multiple properties at once
  and reports them (updates to the server) when you want.
</p>
<p>
  Below are some of the methods available in the SDK. All these methods are static
  methods and defined in the class <code>CountlyUserDetailsModel</code>.
</p>
<p>
  <strong>Set:</strong> Sets a value to the provided key. Syntax:
  <code>CountlyUserDetailsModel.SetOnce(string key, string value);</code>
</p>
<p>
  Parameter(s): <strong>key:</strong> Name of the property to be updated
  <strong>value:</strong> Value to be updated with
</p>
<p>
  Example: <code>CountlyUserDetailsModel.Set("Weight", "80");</code>
  <code>CountlyUserDetailsModel.Save();</code>
</p>
<p>
  <strong>SetOnce:</strong> Sets value to key, only if property was not defined
  before for this user Syntax:
  <code>CountlyUserDetailsModel.SetOnce(string key, string value);</code>
</p>
<p>Parameter(s): Already defined above.</p>
<p>
  Example: <code>CountlyUserDetailsModel.SetOnce("Weight", "90");</code>
  <code>CountlyUserDetailsModel.Save();</code>
</p>
<p>
  In the above example, Weight will not be updated with value “90” if you’ve already
  updated Weight with a certain value.
</p>
<p>
  <strong>Increment:</strong> To increment value on server by 1 (if no value on
  server, assumes it is 0)
</p>
<p>
  Syntax: <code>CountlyUserDetailsModel.Increment(string key);</code>
</p>
<p>Parameter(s): Already defined above.</p>
<p>
  Example: <code>CountlyUserDetailsModel.Increment("Weight");</code>
  <code>CountlyUserDetailsModel.Save();</code>
</p>
<p>
  Increment By: To increment value on server by provided value (if no value on
  server, assumes it is 0)
</p>
<p>
  <strong>Syntax:</strong>
  <code>CountlyUserDetailsModel.IncrementBy(string key, double value);</code>
</p>
<p>Parameter(s): Already defined above.</p>
<p>
  Ex: <code>CountlyUserDetailsModel.IncrementBy("Weight", 1);</code>
  <code>CountlyUserDetailsModel.Save();</code>
</p>
<p>
  <strong>Multiply:</strong> To multiply value on server by provided value (if
  no value on server, assumes it is 0)
</p>
<p>
  Syntax:
  <code>CountlyUserDetailsModel.Multiply(string key, double value);</code>
</p>
<p>Parameter(s): Already defined above.</p>
<p>
  Ex: <code>CountlyUserDetailsModel.Multiply("Weight", 2);</code>
  <code>CountlyUserDetailsModel.Save();</code>
</p>
<p>
  <strong>Max:</strong> To store maximal value from the one on server and provided
  value (if no value on server, uses provided value)
</p>
<p>
  Syntax: <code>CountlyUserDetailsModel.Max(string key, double value);</code>
</p>
<p>Parameter(s): Already defined above.</p>
<p>
  Ex: <code>CountlyUserDetailsModel.Max("Weight", 90);</code>
  <code>CountlyUserDetailsModel.Save();</code>
</p>
<p>
  <strong>Min:</strong> To store minimal value from the one on server and provided
  value (if no value on server, uses provided value).
</p>
<p>
  Syntax: <code>CountlyUserDetailsModel.Min(string key, double value);</code>
</p>
<p>Parameter(s): Already defined above.</p>
<p>
  Ex: <code>CountlyUserDetailsModel.Min("Weight", 40);</code>
  <code>CountlyUserDetailsModel.Save();</code>
</p>
<p>
  <strong>Push:</strong> Add one or many values to array property (can have multiple
  same values, if property is not array, converts it to array).
</p>
<p>
  Syntax: <code>CountlyUserDetailsModel.Push(string key, string[] value);</code>
</p>
<p>
  Parameter(s): value: A string array containing list of values that you want to
  set for the provided key.
</p>
<p>
  Ex:
  <code>CountlyUserDetailsModel.Push("Mole", new string[] { "Left Cheek", "Back", "Toe" });</code>
  <code>CountlyUserDetailsModel.Save();</code>
</p>
<p>
  <strong>Push Unique:</strong> Add one or many values to array property (will
  only store unique values in array, if property is not array, converts it to array).
</p>
<p>
  Syntax:
  <code>CountlyUserDetailsModel.PushUnique(string key, string[] value);</code>
</p>
<p>Parameter(s): Already defined above.</p>
<p>
  Ex:
  <code>CountlyUserDetailsModel.PushUnique("Mole", new string[] { "Right Leg", "Right Leg" });</code>
  <code>CountlyUserDetailsModel.Save();</code>
</p>
<p>
  <strong>Pull:</strong> Remove one or many values from array property (only removes
  value from array properties)
</p>
<p>
  Syntax: <code>CountlyUserDetailsModel.Pull(string key, string[] value);</code>
</p>
<p>Parameter(s): Already defined above.</p>
<p>
  Ex:
  <code>CountlyUserDetailsModel.Pull("Mole", new string[] { "Right Leg", "Back" });</code>
  <code>CountlyUserDetailsModel.Save();</code>
</p>
<h3>Recording multiple update requests</h3>
<p>
  Apart from updating a single property in one request, you can modify multiple
  (unique) properties in one single request. This way, you can increment Weight
  and multiply Height in the same request. Similarly, you can record N number of
  modify requests and Save them all together in one single request instead of multiple
  requests.
</p>
<p>
  In order record a “modify custom user detail” request, you just need to call
  the particular methods but DO NOT call “Save” method immediately after each method.
  <code>CountlyUserDetailsModel.Save()</code> method immediately posts all modify
  requests recorded yet.
</p>
<p>
  Note that if you are going to modify multiple properties in one request, make
  sure you properties are unique, i.e., a property shouldn’t be modified more than
  once in a single request. However, if you record a property more than once, only
  the latest modifier will be posted to the server.
</p>
<p>Example:</p>
<pre><code class="csharp">CountlyUserDetailsModel.Max("Weight", 190);
CountlyUserDetailsModel.Multiply("Weight", 190);
CountlyUserDetailsModel.Min("Height", 5.5);
CountlyUserDetailsModel.Push("Mole", new string[] { "Left Cheek", "Back", "Toe" });
CountlyUserDetailsModel.Save();</code></pre>
<p>
  You can record N number of modify requests and call “Save” when you want to post
  all events recorded before calling “Save” method.
</p>
<p>
  Note: In the above example, you can see Max and Multiply are modifying the same
  property “Weight”. Therefore in such a scenario, only Multiply request will pushed
  to the server and Max request will not.
</p>
<h1>Push Notifications</h1>
<p>
  This section requires setting up either APNS (Apple Push Notification Services)
  or FCM (Firebase Cloud Services). For APNS, you need to get push credentials
  and upload to Countly.
  <a href="https://resources.count.ly/docs/countly-sdk-for-ios-and-os-x#section-push-notifications">This document</a>
  explains how to retrieve and upload push credentials for APNS. If you are developing
  for Android, please
  <a href="https://resources.count.ly/docs/countly-sdk-for-android#section-setting-up-push-notifications">read this documentation</a>
  and follow instructions to setup for GCM/FCM.
</p>
<p>
  After setting up push notification credentials, you must initialize Push Notification
  for Countly Unity SDK. However, SDK already does it for you so, you don’t have
  to initialize it separately. At the beginning of this documentation, go to “initialization”
  process (method SetDefaults) where we init the Countly Unity SDK. In that method,
  you can see we have a parameter (last one) named TEST_MODE.
</p>
<ul>
  <li>
    If you don’t want to enable Push Notification for your application, you can
    pass NULL to this parameter during initialization.
  </li>
  <li>
    If you want to enable Push Notification for your application, you can provide
    any of the suitable value from the enum TestMode under namespace Assets.Scripts.Enums.
  </li>
</ul>
<p>
  So, the SDK already initializes Push Notification for you. But, if you’ve disabled
  Push Notification during initialization and you want to enable anytime after
  that, you can do that by using following method EnablePush.
</p>
<p>
  Syntax: <code>Countly.EnablePush(TestMode mode);</code>
</p>
<p>Parameter(s): Explained above.</p>
<p>
  <strong>Key Points:</strong>
</p>
<ol>
  <li>
    Push Notification with banner image in the background is only supported for
    Android platform. Banner image is not supported on iOS platform.
  </li>
  <li>
    Push Notifications will only appear when the app is in Foreground. As soon
    as user switches to another application and your app is in background, your
    session will end and you’ll have to initialize Push Notification again on
    your AppStart or OnFocus event, if you haven’t initialized it in the SetDefaults
    method of the SDK by passing TestMode parameter.
  </li>
  <li>
    For platforms Android and iOS, the notification icon can be set as follows:
    For Android, place the notification icons under folder “Assets\Plugins\Android\res”
    for different screen densities. The name of the icon must be “notification_icon”.
    A sample PNG file is placed under the folder “drawable”. For iOS, iOS platform
    will basically pick your app icon as the default push notification icon.
    So, you don’t need to do anything for iOS platform.
  </li>
</ol>
<h1>Changing Device ID</h1>
<p>
  Countly Unity SDK persists Device ID which you provide during initialization
  or generates a random ID, if you don’t provide it. This Device ID will be used
  persistently for all future requests made from a device until you change that.
</p>
<p>
  The SDK allows you to change the Device ID at any point of time. You can use
  following any of the following two methods for changing Device ID, depending
  upon your scenario.
</p>
<p>
  <strong> Change device ID &amp; end current session:</strong>
</p>
<p>
  This method changes the Device ID and does following other operations:
</p>
<ol>
  <li>Ends all the events that have been recorded till now.</li>
  <li>Ends current session.</li>
  <li>
    Updates Device ID and starts new session with new Device ID.
  </li>
</ol>
<p>
  Syntax:
  <code>Countly.ChangeDeviceIDAndEndCurrentSessionAsync(string deviceId);</code>
</p>
<p>
  Parameter(s): <strong>deviceId:</strong> Required
  <strong>Type: string </strong>Desc:** The new device id
</p>
<p>
  Ex:
  <code>Countly.ChangeDeviceIDAndEndCurrentSessionAsync(“NEW_DEVICE_ID”);</code>
</p>
<p>
  <strong> Change Device ID And Merge Session Data </strong>
</p>
<p>
  This method changes the Device ID and merges data for both Device IDs on the
  Countly server.
</p>
<p>
  Syntax:
  <code>Countly.ChangeDeviceIDAndMergeSessionDataAsync(string deviceId);</code>
</p>
<p>
  Parameter(s): Explained above. Ex:
  <code>Countly.ChangeDeviceIDAndMergeSessionDataAsync(“NEW_DEVICE_ID”);</code>
</p>