<p>
  This document will guide you through the process of Countly SDK installation
  for Android.
</p>
<div class="callout callout--info">
  <h3 class="callout__title">Minimum Android version</h3>
  <p>
    Countly Android SDK needs a minimum of Android 2.3+ (API Level 9).
  </p>
</div>
<h1>Adding Countly SDK</h1>
<p>
  You can use Visual Studio to add Countly SDK to your project. For this, add NuGet
  packages
  <a href="https://www.nuget.org/packages/CountlySDK.Xamarin.Android/">CountlySDK.Xamarin.Android</a>
  ,<a href="https://www.nuget.org/packages/CountlySDK.Messaging.Xamarin.Android/">CountlySDK.Messaging.Xamarin.Android</a>
  or
  <a href="https://www.nuget.org/packages/CountlySDK.Messaging.FCM.Xamarin.Android/">CountlySDK.Messaging.Xamarin.Android</a>
  (if you require using push notifications in your project)
</p>
<p>
  You can use these commands for convenience to install each package:
</p>
<p>
  <strong>CountlySDK.Xamarin.Android</strong>:
</p>
<pre><code class="text">Install-Package CountlySDK.Xamarin.Android</code></pre>
<p>
  <strong>CountlySDK.Messaging.Xamarin.Android</strong>:
</p>
<pre><code class="text">Install-Package CountlySDK.Messaging.Xamarin.Android</code></pre>
<p>
  <strong>CountlySDK.Messaging.FCM.Xamarin.Android</strong>:
</p>
<pre><code class="text">Install-Package CountlySDK.Messaging.FCM.Xamarin.Android</code></pre>
<h1>Setting up Countly SDK</h1>
<p>
  First, you'll need to decide which device ID generation strategy to use. There
  are several options defined below:
</p>
<p>
  First and easiest method is, if you want Countly SDK to take care of device ID
  seamlessly, use line below. Do not put a trailing "/" at the end of the server
  URL or it won't work. Starting from the version 16.12.03, the SDK will erase
  the trailing "/" and write a warning to the log.
</p>
<pre><code class="csharp">Countly.SharedInstance().Init(this, "https://YOUR_SERVER", "YOUR_APP_KEY"); </code></pre>
<div class="callout callout--info">
  <h3 class="callout__title">Which server/host should I use inside SDK?</h3>
  <p>
    If you are using Countly Enterprise Edition trial servers use
    <code>https://try.count.ly</code>, <code>https://us-try.count.ly</code> or
    <code>https://asia-try.count.ly</code>. Basically the domain you are accessing
    your trial dashboard from.
  </p>
  <p>
    If you use Community Edition and Enterprise Edition, use your own domain
    name or IP address like
    <a href="https://example.com">https://example.com</a> or
    <a href="https://IP">https://IP</a> (if SSL is setup).
  </p>
</div>
<p>
  Second, you can specify device ID by yourself if you have one (it has to be unique
  per device):
</p>
<pre><code class="csharp">Countly.SharedInstance().Init(this, "https://YOUR_SERVER", "YOUR_APP_KEY", "YOUR_DEVICE_ID");</code></pre>
<p>
  Third, you can rely on Google Advertising ID for device ID generation.
</p>
<pre><code class="csharp">Countly.SharedInstance().Init(this, "https://YOUR_SERVER", "YOUR_APP_KEY", null, DeviceId.Type.AdvertisingId);</code></pre>
<p>Or, you can use OpenUDID:</p>
<pre><code class="csharp">Countly.SharedInstance().Init(this, "https://YOUR_SERVER", "YOUR_APP_KEY", null, DeviceId.Type.OpenUdid); </code></pre>
<p>
  For all of those different approaches,
  <code>Countly.SharedInstance().Init(...)</code> method should be called from
  your <code>Application</code> subclass (preferred), or from your main activity
  <code>OnCreate</code> method.
</p>
<p>
  In the case of OpenUDID you'll need to include the following declaration into
  your <code>AndroidManifest.xml</code>:
</p>
<pre><code class="xml">&lt;service android:name="org.openudid.OpenUDID_service"&gt;
    &lt;intent-filter&gt;
        &lt;action android:name="org.openudid.GETUDID" /&gt;
    &lt;/intent-filter&gt;
&lt;/service&gt;</code></pre>
<p>
  In the case of Google Advertising ID, please make sure that you have Google Play
  services 4.0+ included into your project. Also, note that Advertising ID silently
  falls back to OpenUDID in case it failed to get Advertising ID when Google Play
  services are not available on a device.
</p>
<p>
  After <code>Countly.sharedInstance().init(...)</code> call you'll need to add
  following calls to all your activities:
</p>
<ul>
  <li>
    Call <code>Countly.sharedInstance().onStart()</code> in onStart.
  </li>
  <li>
    Call <code>Countly.sharedInstance().onStop()</code> in onStop.
  </li>
</ul>
<p>
  If the "onStart" and "onStop" calls are not added some functionality will not
  work, for example, sessions will not be tracked. The countly "onStart" has to
  be called in the activities "onStart" function, it can not be called in "onCreate"
  or any other place otherwise the application will receive exceptions.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/a258a5e-Image1.png">
</div>
<p>
  Additionally, make sure that <em>INTERNET</em> permission is set if there's none
  in your manifest file.
</p>
<h2>Enabling logging</h2>
<p>
  If logging is enabled then our SDK will print out debug messages about its internal
  state and encountered problems.
</p>
<p>
  When advice doing this while implementing countly features in your application.
</p>
<pre><code class="csharp">Countly.SharedInstance().SetLoggingEnabled(true);</code></pre>
<p>
  <strong>Changing a device ID</strong>
</p>
<p>
  In case your application authenticates users, you can also change device ID to
  your user ID later. This helps you identify a specific user with a specific ID
  on a device she logs in, and the same scenario can also be used in cases this
  user logs in using a different way (e.g tablet, another mobile phone or web).
  In this case, any data stored in Countly server database and associated with
  temporary device ID will be transferred into user profile with device id you
  specified in the following method call:
</p>
<pre><code class="csharp">Countly.SharedInstance().ChangeDeviceId("New device ID");</code></pre>
<p>
  Whenever your authenticated user logs out, in case you want to track history
  and further activity under another Countly user, call:
</p>
<pre><code class="csharp">Countly.SharedInstance().ChangeDeviceId(DeviceId.Type.OpenUdid, null);</code></pre>
<p>
  You can also set Advertising ID as your device ID generation strategy or even
  supply your own string with <code>DeviceId.Type.DeveloperSupplied</code> type.
</p>
<p>
  <strong>Retrieving the device id and its type</strong>
</p>
<p>
  You may want to see what device id Countly is assigning for the specific device
  and what the source of that it is. For that, you may use the following calls.
  The id type is an enum with the possible values of: "DeveloperSupplied", "OpenUdid",
  "AdvertisingId".
</p>
<pre><code class="csharp">string usedId = Countly.SharedInstance().GetDeviceID();
Type idType = Countly.SharedInstance().GetDeviceIDType();</code></pre>
<p>
  <strong>Forcing HTTP POST</strong>
</p>
<p>
  If the data sent to the server is short enough, the SDK will use HTTP GET requests.
  In case you want an override so that HTTP POST is used in all cases, set the
  "HttpPostForced" property after you called "Init". You can use the same function
  to later in the app's lifecycle disable the override. This function has to be
  called every time the app starts.
</p>
<pre><code class="csharp">//the init call before the override
Countly.SharedInstance().Init(this, "https://YOUR_SERVER", "YOUR_APP_KEY", "YOUR_DEVICE_ID");
  
//enabling the override
Countly.SharedInstance().HttpPostForced = true;
  
//disabling the override
Countly.SharedInstance().HttpPostForced = false;
</code></pre>
<p>
  <strong>Parameter Tampering Protection</strong>
</p>
<p>
  You can set optional <code>salt</code> to be used for calculating checksum of
  request data, which will be sent with each request using
  <code>&amp;checksum</code> field. You need to set exactly the same
  <code>salt</code> on Countly server. If <code>salt</code> on Countly server is
  set, all requests would be checked for validity of <code>&amp;checksum</code>
  field before being processed.
</p>
<pre><code class="csharp">Countly.SharedInstance().EnableParameterTamperingProtection("salt");</code></pre>
<h3>Using Proguard</h3>
<p>
  Proguard obfuscates OpenUDID and if you use it as for your ID, then Countly can't
  generate ID anymore, and thus can't send anything. Therefore you need to exclude
  OpenUDID from being obfuscated with the following one-liner:
</p>
<pre><code class="java">-keep class org.openudid.** { *; }</code></pre>
<p>
  <strong>Note:</strong> Make sure you use App Key (found under Management -&gt;
  Applications) and not API Key. Entering API Key will not work.
</p>
<h1>Setting up events</h1>
<p>
  An<a href="http://resources.count.ly/docs/custom-events">&nbsp;event</a> is any
  type of action that you can send to a Countly instance, e.g purchase, settings
  changed, view enabled and so. This way it's possible to get much more information
  from your application compared to what is sent from Android SDK to Countly instance
  by default.
</p>
<div class="callout callout--warning">
  <h3 class="callout__title">Data passed should be in UTF-8</h3>
  <p>
    All data passed to Countly server via SDK or API should be in UTF-8.
  </p>
</div>
<p>
  As an example, we will be recording a <strong>purchase</strong> event. Here is
  a quick summary what information each usage will provide us:
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
    versions + the total duration of those events.
  </li>
</ul>
<h2>1. Event key and count</h2>
<pre><code class="java">Countly.SharedInstance().RecordEvent("purchase", 1);</code></pre>
<h2>2. Event key, count and sum</h2>
<pre><code class="csharp">Countly.SharedInstance().RecordEvent("purchase", 1, 0.99);</code></pre>
<h2>3. Event key and count with segmentation(s)</h2>
<pre><code class="csharp">Dictionary&lt;String, String&gt; segmentation = new Dictionary&lt;String, String&gt;();
segmentation.put("country", "Germany");
segmentation.put("app_version", "1.0");

Countly.SharedInstance().RecordEvent("purchase", segmentation, 1);</code></pre>
<h2>4. Event key, count and sum with segmentation(s)</h2>
<pre><code class="csharp">Dictionary&lt;String, String&gt; segmentation = new Dictionary&lt;String, String&gt;();
segmentation.put("country", "Germany");
segmentation.put("app_version", "1.0");

Countly.SharedInstance().RecordEvent("purchase", segmentation, 1, 0.99);</code></pre>
<h2>5. Event key, count, sum and duration with segmentation(s)</h2>
<pre><code class="csharp">Dictionary&lt;String, String&gt; segmentation = new Dictionary&lt;String, String&gt;();
segmentation.put("country", "Germany");
segmentation.put("app_version", "1.0");

Countly.SharedInstance().RecordEvent("purchase", segmentation, 1, 0.99, 60);</code></pre>
<p>
  Those are only a few examples with what you can do with events. You can extend
  those examples and use country, app_version, game_level, time_of_day and any
  other segmentation that will provide you valuable insights.
</p>
<h1>Timed events</h1>
<p>
  It's possible to create to create timed events by defining a start and stop moment.
</p>
<pre><code class="csharp">String eventName = "Custom event";

//start some event
Countly.SharedInstance().StartEvent(eventName);
//wait some time

//end the event 
Countly.SharedInstance().EndEvent(eventName);</code></pre>
<p>
  When ending a event you can also provide additional information. But in that
  case you have to provide segmentation, count and sum. The default values for
  those are "null", 1 and 0.
</p>
<pre><code class="csharp">String eventName = "Custom event";

//start some event
Countly.SharedInstance().StartEvent(eventName);
//wait some time

Dictionary&lt;String, String&gt; segmentation = new Dictionary&lt;String, String&gt;();
segmentation.put("wall", "orange");

//end the event while also providing segmentation information, count and sum
Countly.SharedInstance().EndEvent(eventName, segmentation, 4, 34);
</code></pre>
<h1>User location</h1>
<p>
  While integrating this SDK into your application, you might want to track your
  user location. You could use this information to better know your apps user base
  or to send them tailored push notifications based on their coordinates. There
  are 4 fields that can be provided:
</p>
<ul>
  <li>country code in the 2 letter iso standard</li>
  <li>city name (has to be set together with country code)</li>
  <li>
    Comma separate latitude and longitude values, for example, "56.42345,123.45325"
  </li>
  <li>IP address of your user</li>
</ul>
<p>
  While integrating this SDK into your application, you might want to track your
  user location. You could use this information to better know your apps user base
  or to
</p>
<pre><code class="csharp">string countryCode = "us";
string city = "Houston";
string latitude = "29.634933";
string longitude = "-95.220255";
string ipAddress = null;
Countly.SharedInstance().SetLocation(countryCode, city, latitude + "," + longitude, ipAddress);</code></pre>
<p>
  When those values are set, they will be sent every time when initiating a session.
  If they are set after a session was initiated, a separate request will also be
  sent. Except for IP address, because Countly Server processes ip address only
  when starting a session.
</p>
<p>If you don't want to set specific fields, set them to null.</p>
<p>
  Users might want to opt out of location tracking. To do that, call:
</p>
<pre><code class="csharp">//disable location
Countly.SharedInstance().DisableLocation();</code></pre>
<p>
  It will erase cached location data from device and stop further tracking.
</p>
<p>
  If, after disabling location, "setLocation" is called with any non null value,
  tracking will resume.
</p>
<h1>Attribution analytics &amp; install campaigns</h1>
<p>
  <a href="https://count.ly/attribution-analytics">Countly Attribution Analytics</a>
  allows you to measure your marketing campaign performance by attributing installs
  from specific campaigns. This feature is available for Enterprise Edition.
</p>
<p>
  In order to get more precise attribution on Android it is highly recommended
  to allow Countly to listen to <strong>INSTALL_REFERRER</strong> intent and you
  can do that by adding following XML code to your
  <strong>AndroidManifest.xml</strong> file, inside <strong>application</strong>
  tag.
</p>
<pre><code class="xml">&lt;receiver android:name="ly.count.android.sdk.ReferrerReceiver" android:exported="true"&gt;
  &lt;intent-filter&gt;
    &lt;action android:name="com.android.vending.INSTALL_REFERRER" /&gt;
  &lt;/intent-filter&gt;
&lt;/receiver&gt;</code></pre>
<p>
  Note that modifying <strong>AndroidManifest.xml</strong> file is the only thing
  you would need to change, in order to start getting data from your campaigns
  via Attribution Analytics plugin.
</p>
<p>
  For more information about how to set up your campaigns, please
  <a href="http://resources.count.ly/docs/referral-analytics">see this documentation</a>.
</p>
<h1>Getting user feedback</h1>
<p>
  Star rating integration provides a dialog for getting user's feedback about the
  application. It contains a title, simple message explaining what it is for, a
  1-to-5 star meter for getting users rating and a dismiss button in case the user
  does not want to give a rating.
</p>
<p>
  This star-rating has nothing to do with Google Play Store ratings and reviews.
  It is just for getting a brief feedback from users, to be displayed on the Countly
  dashboard. If the user dismisses star rating dialog without giving a rating,
  the event will not be recorded.
</p>
<p>
  Star-rating dialog's title, message and dismiss button text can be customized
  either through the init function or the <code>SetStarRatingDialogTexts</code>
  function. If you don't want to override one of those values, set it to "null".
</p>
<pre><code class="csharp">//set it through the init function
Countly.Init(Context, serverURL, appKey, deviceID, idMode, starRatingLimit, StarRatingCallback, "Custom title", "Custom message", "Custom dismiss button text");

//Use the designated function:
Countly.SharedInstance().SetStarRatingDialogTexts(Context, "Custom title", "Custom message", "Custom dismiss button text");
</code></pre>
<p>Star rating dialog can be displayed in 2 ways:</p>
<ul>
  <li>Manually, by developer</li>
  <li>Automatically, depending on session count</li>
</ul>
<p>
  In order to display the Star rating dialog manually, you must call the
  <code>ShowStarRating</code> function. Optionally, you can provide the callback
  functions. There is no limit on how many times star-rating dialog can be displayed
  manually.
</p>
<pre><code class="csharp">//show the star rating without a callback
Countly.SharedInstance().ShowStarRating(Context, null);

//show the star rating with a callback
Countly.SharedInstance().ShowStarRating(Context, Callback)</code></pre>
<p>
  Star rating dialog will be displayed automatically when application's session
  count reaches the specified limit, once for each new version of the application.
  This session count limit can be specified on initial configuration or through
  the <code>SetAutomaticStarRatingSessionLimit</code> function. The default limit
  is 3. Once star rating dialog is displayed automatically, it will not be displayed
  again unless there is a new app version.
</p>
<p>
  To show the automatic star rating dialog you need to pass the activity context
  during init.
</p>
<pre><code class="csharp">//set the rating limit through the init function
int starRatingLimit = 5;
Countly.Init(Context, serverURL, appKey, deviceID, IdMode, StarRatingLimit, StarRatingCallback, StarRatingTextTitle, StarRatingTextMessage, StarRatingTextDismiss);

//set it through the designated function
Countly.SharedInstance().StarRatingLimit(Context, 5);</code></pre>
<p>
  If you want to enable the automatic star rating functionality, use
  <code>SetIfStarRatingShownAutomatically</code> function. It is disabled by default.
</p>
<pre><code class="csharp">//enable automatic star rating
Countly.SharedInstance().SetIfStarRatingShownAutomatically(true);

//disable automatic star rating
Countly.SharedInstance().SetIfStarRatingShownAutomatically(false);</code></pre>
<p>
  If you want to have the star rating shown only once per app's lifetime and not
  for each new version, use the "SetStarRatingDisableAskingForEachAppVersion" function.
</p>
<pre><code class="csharp">//disable star rating for each new version
Countly.SharedInstance().SetStarRatingDisableAskingForEachAppVersion(true);

//enable star rating for each new version
Countly.SharedInstance().SetStarRatingDisableAskingForEachAppVersion(false);</code></pre>
<p>
  The star rating callback provides functions for two events.
  <code>OnRate</code> is called when the user chooses a rating. OnDismiss is called
  when the user clicks the back button, clicks outside the dialogue or clicks the
  "Dismiss" button. The callback provided in the init function is used only when
  showing the automatic star rating. For the manual star rating, only the provided
  callback will be used.
</p>
<p>
  Create a class which implements <code>CountlyStarRating.IRatingCallback</code>,
  implement the methods OnRating and OnDismiss as per need.
</p>
<pre><code class="csharp">public void OnRate(int rating) {
      //the user rated the app
    }

        public void OnDismiss() {
      //the star rating dialog was dismissed
    }</code></pre>
<p>Take an instance of it in your Activity file.</p>
<pre><code class="csharp">CountlyStarRating.RatingCallback callback = new CountlyStarRating.RatingCallback();
</code></pre>
<h1>Setting up User Profiles</h1>
<p>
  Available with Enterprise Edition, User Profiles is a tool which helps you identify
  users, their devices, event timeline and application crash information. User
  Profiles can contain any information that either you collect, or is collected
  automatically by Countly SDK.
</p>
<p>
  You can send user related information to Countly and let Countly dashboard show
  and segment this data. You may also send a notification to a group of users.
  For more information about User Profiles, see
  <a href="http://resources.count.ly/docs/user-profiles">this documentation</a>.
</p>
<p>
  To provide information about the current user, you must call the
  <code>Countly.userData.setUserData</code> function. You can call it by providing
  a bundle of only the predefined fields or call it while also providing the second
  bundle of fields with your custom keys. After you have provided user profile
  information, you must save it by calling <code>Countly.userData.save()</code>.
</p>
<pre><code class="csharp">//Update the user profile using only predefined fields
Dictionary&lt;String, String&gt; predefinedFields = new Dictionary&lt;String, String&gt;();
Countly.UserData.SetUserData(predefinedFields);
Countly.UserData.Save()


//Update the user profile using predefined and custom fields
Dictionary&lt;String, String&gt; predefinedFields = new Dictionary&lt;String, String&gt;();
Dictionary&lt;String, String&gt; customFields = new Dictionary&lt;String, String&gt;();
Countly.UserData.SetUserData(predefinedFields, customFields);
Countly.UserData.Save()</code></pre>
<p>The keys for predefined user data fields are as follows:</p>
<table>
  <tbody>
    <tr>
      <th>Key</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>name</td>
      <td>String</td>
      <td>User's full name</td>
    </tr>
    <tr>
      <td>username</td>
      <td>String</td>
      <td>User's nickname</td>
    </tr>
    <tr>
      <td>email</td>
      <td>String</td>
      <td>User's email address</td>
    </tr>
    <tr>
      <td>organization</td>
      <td>String</td>
      <td>User's organisation name</td>
    </tr>
    <tr>
      <td>phone</td>
      <td>String</td>
      <td>User's phone number</td>
    </tr>
    <tr>
      <td>picture</td>
      <td>String</td>
      <td>URL to avatar or profile picture of the user</td>
    </tr>
    <tr>
      <td>picturePath</td>
      <td>String</td>
      <td>Local path to user's avatar or profile picture</td>
    </tr>
    <tr>
      <td>gender</td>
      <td>String</td>
      <td>User's gender as M for male and F for female</td>
    </tr>
    <tr>
      <td>byear</td>
      <td>String</td>
      <td>User's year of birth as integer</td>
    </tr>
  </tbody>
</table>
<p>
  Using "" for strings or a negative number for 'byear' will effectively delete
  that property.
</p>
<p>
  For custom user properties you may use any key values to be stored and displayed
  on your Countly backend.
  <strong>Note: keys with . or $ symbols will have those symbols removed.</strong>
</p>
<h2>Modifying custom data</h2>
<p>
  Additionally you can do different manipulations on your custom data values, like
  increment current value on server or store a array of values under the same property.
</p>
<p>Below is the list of available methods:</p>
<pre><code class="csharp">//set one custom properties
Countly.UserData.SetProperty("test", "test");
//increment used value by 1
Countly.UserData.Increment("used");
//increment used value by provided value
Countly.UserData.IncrementBy("used", 2);
//multiply value by provided value
Countly.UserData.Multiply("used", 3);
//save maximal value
Countly.UserData.SaveMax("highscore", 300);
//save minimal value
Countly.UserData.SaveMin("best_time",60);
//set value if it does not exist
Countly.UserData.SetOnce("tag", "test");
//insert value to array of unique values
Countly.UserData.PushUniqueValue("type", "morning");
//insert value to array which can have duplocates
Countly.UserData.PushValue("type", "morning");
//remove value from array
Countly.UserData.PullValue("type", "morning");

//send provided values to server
Countly.UserData.Save();</code></pre>
<p>
  In the end, always call <strong>Countly.UserData.Save()</strong> to send them
  to the server.
</p>
<h1>User Consent management</h1>
<div class="callout callout--warning">
  <p>This feature is available from 18.04</p>
</div>
<p>
  To be compliant with GDPR, starting from 18.04, Countly provides ways to toggle
  different Countly features on/off depending on the given consent.
</p>
<p>
  More information about GDPR can be found
  <a href="https://blog.count.ly/countly-the-gdpr-how-worlds-leading-mobile-and-web-analytics-platform-can-help-organizations-5015042fab27">here</a>.
</p>
<p>
  By default the requirement for consent is disabled. To enable it, you have to
  call <code>SetRequiresConsent</code> with <code>true</code>, before initializing
  Countly.
</p>
<pre><code class="csharp">Countly.SharedInstance().SetRequiresConsent(true);</code></pre>
<p>
  By default, no consent is given. That means that if no consent is enabled, Countly
  will not work and no network requests, related to features, will be sent. When
  consent status of a feature is changed, that change will be sent to the Countly
  server.
</p>
<p>
  For all features, except <code>Push</code>, consent is not persistent and will
  have to be set every time before countly Init. Therefore the storage and persistence
  of given consent fall on the SDK integrator.
</p>
<p>
  Consent for features can be given and revoked at any time, but if it is given
  after Countly init, some features might work partially.
</p>
<p>
  If consent is removed, but the appropriate function can't be called before the
  app closes, it should be done at next app start so that any relevant server-side
  features could be disabled (like reverse geo IP for location)
</p>
<p>
  Feature names in the Android SDK are stored as static fields in the class called
  <code>CountlyFeatureNames</code>.
</p>
<p>
  The current features are: * <code>sessions</code> - tracking when, how often
  and how long users use your app * <code>events</code> - allow sending events
  to the server * <code>views</code> - allow tracking which views user visits *
  <code>location</code> - allow sending location information *
  <code>crashes</code> - allow tracking crashes, exceptions and errors *
  <code>attribution</code> - allow tracking from which campaign did user come *
  <code>users</code> - allow collecting/providing user information, including custom
  properties * <code>push</code> - allow push notifications *
  <code>starRating</code> - allow to send their rating and feedback
</p>
<h2>Feature groups</h2>
<p>
  Features can be grouped into groups. With this, you can give/remove consent to
  multiple features in the same call. They can be created using
  <code>createFeatureGroup</code>. Those groups are not persistent and have to
  be created on every restart.
</p>
<h2>Changing consent</h2>
<p>
  There are 3 ways of changing feature consent: * <code>GiveConsent</code>/<code>RemoveConsent</code>
  - gives or removes consent to a specific feature.
</p>
<pre><code class="csharp"> // give consent to "sessions" feature
Countly.SharedInstance().GiveConsent(new string[] { Countly.CountlyFeatureNames.Sessions });

// remove consent from "sessions" feature
Countly.SharedInstance().RemoveConsent(new string[] { Countly.CountlyFeatureNames.Sessions });</code></pre>
<ul>
  <li>
    <code>SetConsent</code> - set consent to a specific (true/false) value
  </li>
</ul>
<pre><code class="csharp"> // give consent to "sessions" feature
Countly.SharedInstance().SetConsent(new string[] {
  Countly.CountlyFeatureNames.Sessions }, true);

// remove consent from "sessions" feature
Countly.SharedInstance().SetConsent(new string[] { Countly.CountlyFeatureNames.Sessions }, false);</code></pre>
<ul>
  <li>
    <code>SetConsentFeatureGroup</code> - set consent for a feature group to
    a specific (true/false) value
  </li>
</ul>
<pre><code class="csharp"> // prepare features that should be added to the group
string[] groupFeatures = new string[] {
  Countly.CountlyFeatureNames.Sessions,
  Countly.CountlyFeatureNames.Location };

string groupName = "featureGroup1";

// give consent to "sessions" feature
Countly.SharedInstance().SetConsentFeatureGroup(groupName, true);

// remove consent from "sessions" feature
Countly.SharedInstance().SetConsentFeatureGroup(groupName, false);</code></pre>
<h1>Setting up push notifications</h1>
<div class="callout callout--danger">
  <h3 class="callout__title">
    Read this important notice before integrating push notifications
  </h3>
  <p>
    In order to use push notifications for Xamarin Android, you'll need to include
    a different version of SDK into your project. We have 3 library projects
    <code>CountlySDK..Xamarin.Android</code>,
    <code>CountlySDK.Messaging.Xamarin.Android</code> &amp;
    <code>CountlySDK.Messaging.FCM.Xamarin.Android</code> for no push integration
    needed, GCM integration &amp; FCM integration respectively. If you want messaging
    support, include second one (it also adds a dependency on "play-services-gcm")
    or third one (you'll need to add Firebase to your dependencies yourself).
  </p>
</div>
<p>
  Countly SDK versions prior to 18.04 supported only GCM notifications, while version
  18.04 implements both: GCM (<code>SDK-messaging</code> dependency) and FCM integration
  (<code>SDK-messaging-fcm</code> dependency). We recommend switching to FCM as
  soon as possible. Migration is seamless since old GCM users will continue to
  receive your notifications even after you update SDK &amp; server key.
</p>
<p>
  To upgrade SDK from GCM to FCM, you'll need to follow these steps:
</p>
<ul>
  <li>Migrate your GCM project to Firebase if not done yet.</li>
  <li>
    Remove old GCM server key from the Countly dashboard (Applications -&gt;
    Management) and add FCM server key.
  </li>
  <li>
    Update your app by including
    <a href="https://firebase.google.com/docs/android/setup">Firebase SDK into it</a>.
  </li>
  <li>
    Remove <code>CountlySDK.Messaging.Xamarin.Android</code> dependency from
    your app and add <code>CountlySDK.Messaging.FCM.Xamarin.Android</code> one.
  </li>
</ul>
<h2>Getting GCM / FCM credentials</h2>
<p>
  Countly needs server key to authenticate with GCM or FCM. In case your app is
  still not migrated to Firebase, please do that.
</p>
<p>
  Then open <a href="https://console.firebase.google.com">Firebase console</a>
  and open Project settings:
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/e000f22-Image2.png">
</div>
<p>Select Cloud Messaging tab</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/c63e6ae-Image3.png">
</div>
<p>
  Copy &amp; paste either GCM key (deprecated) or FCM key (only SDK 18.04+) into
  your application GCM/FCM credentials upload form in the Countly dashboard, hit
  Validate and eventually save changes. For GCM (deprecated) you'll also need Sender
  ID to pass into <code>InitMessaging</code> SDK call.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/695c0e0-IMage4.png">
</div>
<h2>FCM integration (recommended)</h2>
<p>
  Once you followed Google guide for
  <a href="https://docs.microsoft.com/en-us/xamarin/android/data-cloud/google-messaging/firebase-cloud-messaging">Adding Firebase to your project</a>,
  setting up Countly FCM is quite easy.
</p>
<p>
  <strong>Adding packages</strong>
</p>
<p>
  Add Nuget packages for <code>CountlySDK.Messaging.FCM.Xamarin.Android</code>
  and Xamarin.Firebase.Messaging.
</p>
<p>
  Then add <code>CountlyPush.Init()</code> call to your <code>Application</code>
  subclass or main activity <code>onCreate()</code>. Here we use
  <code>Application</code> subclass called <code>App</code>. Don't forget that
  Android O and later require the use of <code>NotificationChannel</code>s. Use
  <code>CountlyPush.ChannelId</code> for Countly-displayed notifications:
</p>
<p>
  Setting up push notifications involves a few steps that should be completed on
  Google Developers Console &amp; Firebase Console, your application and Countly
  dashboard.
</p>
<p>
  With introduction of Firebase, Google deprecated GCM in favour of Firebase Cloud
  Messaging. Current Countly Android SDK 17.05 will always use GCM. All subsequent
  versions will use Firebase instead.
</p>
<p>
  In order to use GCM with projects created before Firebase release, please read
  section <em>Legacy GCM integration</em> below. For new projects (or if legacy
  integration GCM key doesn't work), please follow these steps:
</p>
<pre><code class="csharp">protected override void OnCreate(Bundle savedInstanceState)
{
  base.OnCreate(savedInstanceState);
  if (Build.VERSION.SdkInt &gt;= Android.OS.BuildVersionCodes.O)
  {
    // Register the channel with the system; you can't change the importance
    // or other notification behaviors after this
    NotificationManager notificationManager =
      (NotificationManager)GetSystemService(NotificationService);
    if (notificationManager != null)
    {
      NotificationChannel channel = new NotificationChannel(CountlyPush.ChannelId, GetString(Resource.String.countly_channel_name), Android.App.NotificationImportance.Default);
channel.Description = GetString(Resource.String.countly_channel_description);                  notificationManager.CreateNotificationChannel(channel);
    }
  }
  Countly.SharedInstance()
    .SetLoggingEnabled(true)
    .Init(this, "http://try.count.ly", "APP_KEY");            CountlyPush.Init(Application, Countly.CountlyMessagingMode.Production);
}</code></pre>
<p>
  Please note that in <code>CountlyPush.Init()</code> you also specify the mode
  of your token - test or production. It's quite handy to separate test devices
  from production ones by changing <code>CountlyMessagingMode</code> so you could
  test notifications before sending to all users.
</p>
<pre><code class="xml">&lt;service android:name=".DemoFirebaseInstanceIdService"&gt;
    &lt;intent-filter&gt;
        &lt;action android:name="com.google.firebase.INSTANCE_ID_EVENT" /&gt;
    &lt;/intent-filter&gt;
&lt;/service&gt;</code></pre>
<p>Then create a class:</p>
<pre><code class="csharp"> [Service]
public class DemoFirebaseInstanceIdService : FirebaseInstanceIdService
{
  const string TAG = "MyFirebaseIIDService";
  public override void OnTokenRefresh()
  {
    var refreshedToken = FirebaseInstanceId.Instance.Token;
    Log.Debug(TAG, "Refreshed token: " + refreshedToken);
    SendRegistrationToServer(refreshedToken);
    CountlyPush.OnTokenRefresh(FirebaseInstanceId.Instance.Token);
  }
  void SendRegistrationToServer(string token)
  {
    // Add custom implementation, as needed.
  }
}</code></pre>
<p>
  This ensures that whenever the token is changed, it's sent to the Countly server.
</p>
<p>
  Now we need to add notification handling code. Add another service to your
  <code>AndroidManifest.xml</code>:
</p>
<pre><code class="xml">&lt;service android:name=".DemoFirebaseMessagingService"&gt;
    &lt;intent-filter&gt;
        &lt;action android:name="com.google.firebase.MESSAGING_EVENT" /&gt;
    &lt;/intent-filter&gt;
&lt;/service&gt;</code></pre>
<p>... and a class for it:</p>
<pre><code class="csharp"> [Service]
public class DemoFirebaseMessagingService : FirebaseMessagingService
{
  private static string TAG = "DemoMessagingService";
  
  public override void OnMessageReceived(RemoteMessage message)
  {
    base.OnMessageReceived(message);
    Console.WriteLine(("DemoFirebaseService", "got new message: " +
                       message.Data));
    // decode message data and extract meaningful information from it: title, body, badge, etc.
    CountlyPush.IMessage countlymessage =
      CountlyPush.DecodeMessage(message.Data);
    
    if (message != null &amp;&amp; countlymessage.Has("typ"))
    {
      // custom handling only for messages with specific "typ" keys
      countlymessage.RecordAction(this);
      return;
    }
    Intent notificationIntent = null;
    if (countlymessage.Has("anotherActivity"))
    {
      // notificationIntent = new Intent(this, AnotherActivity.class);
    }
    var result = CountlyPush.DisplayMessage(this, countlymessage,
                                            Resource.Id.Icon,
                                            notificationIntent);
    if (result == null)
    {
      Console.WriteLine(TAG, "Message wasn't sent from Countly server, so it cannot be handled by Countly SDK");
    }
    else if ((bool)result)
    {
      Console.WriteLine(TAG, "Message was handled by Countly SDK");
    }
    else
    {
      Console.WriteLine(TAG, "Message wasn't handled by Countly SDK because API level is too low for Notification support or because currentActivity is null (not enough lifecycle method calls)");
    }
  }
}</code></pre>
<p>
  This class is responsible for message handling logic. Countly provides default
  UI for your notifications which would display a <code>Notification</code> if
  your app is in background or <code>Dialog</code> if it's active. It will also
  automatically report button clicks back to the server for Actioned metric conversion
  tracking. But using it or not is completely up to you. Let's have an overview
  of <code>onMessageReceived</code> method:
</p>
<ol>
  <li>
    <p>
      It calls <code>CountlyPush.DecodeMessage()</code> to decode message from
      Countly-specific format. This way you'll have a way to access standard
      fields like badge, URL or your custom data keys.
    </p>
  </li>
  <li>
    <p>
      Then it checks if the message has <code>typ</code> custom data key and
      if it does, just records Actioned metric. Let's assume it's your custom
      notification to preload some data from remote server. Our demo app has
      a more in-depth scenario for this case.
    </p>
  </li>
  <li>
    <p>
      In case a message also has <code>anotherActivity</code> custom data key,
      it creates a <code>notificationIntent</code> to launch activity named
      <code>AnotherActivity</code>. This intent is only used as default content
      intent for user tap on a <code>Notification</code>. For
      <code>Dialog</code> case it's not used.
    </p>
  </li>
  <li>
    <p>
      Then the service calls <code>CountlyPush.DisplayMessage()</code> to perform
      standard Countly notification displaying logic - <code>Notification</code>
      if your app is in the background or not running and <code>Dialog</code>
      if it's in foreground. Note that this method takes an <code>int</code>
      resource parameter. It must be compatible with the corresponding version
      of Android notification small icon.
    </p>
  </li>
</ol>
<p>
  Apart from listed above, SDK also exposes methods
  <code>CountlyPush.DisplayNotification()</code> &amp;
  <code>CountlyPush.DisplayDialog()</code> in case you only need
  <code>Notification</code>s and don't want <code>Dialog</code> or vice versa.
</p>
<h2>Legacy GCM integration (deprecated)</h2>
<p>
  For GCM integration (<code>CountlySDK.Messaging.Xamarin.Android</code> dependency)
  you'll need Sender ID. You can get one either from Firebase console (see above),
  or, in case you haven't yet migrated to Firebase, from
  <a href="https://console.developers.google.com">Google Developers Console</a>.
  Project Number below is your Sender ID. Note that this is different from the
  Project ID.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/9725ef3-Image10.png">
</div>
<p>
  Check that GCM (Google Cloud Messaging) service is enabled for your application:
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/3154155-IMage11.png">
</div>
<p>
  As the final step, get a server token from Credentials menu of APIs &amp; auth
  section:
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/c88a415-Image12.png">
</div>
<p>
  Make sure you don't enter any IP address restrictions or make sure those restrictions
  you've entered play nice with your Countly server.
</p>
<p>
  <strong>Add extra lines in <code>AndroidManifest.xml</code></strong>
</p>
<p>
  Make sure your application requests these permissions (replace
  <code>ly.count.android.demo.messaging</code> with your app package) in the apps
  manifest file, as shown below:
</p>
<pre><code class="xml">&lt;permission android:name="ly.count.android.demo.messaging.permission.C2D_MESSAGE" android:protectionLevel="signature" /&gt;
&lt;uses-permission android:name="ly.count.android.demo.messaging.permission.C2D_MESSAGE" /&gt;</code></pre>
<p>
  Note that we use Advertising ID for device ID generation purposes in this example.
  If you want OpenUDID or have your own unique device ID, refer to
  <a href="http://github.com/Countly/countly-sdk-android">http://github.com/Countly/countly-sdk-android</a>
  documentation for details.
</p>
<p>
  And then, change the way you init Countly by adding an additional call to
  <code>initMessaging</code>:
</p>
<pre><code class="csharp">  Countly.SharedInstance().Init(this, "YOUR_SERVER", "APP_KEY", null, DeviceId.Type.AdvertisingId).InitMessaging(this, this.Class, "PROJECT_NUMBER", Countly.CountlyMessagingMode.Test);</code></pre>
<p>
  Note that we use Advertising ID for device ID generation purposes in this example.
  If you want OpenUDID or have your own unique device ID, refer to
  <a href="http://github.com/Countly/countly-sdk-android">http://github.com/Countly/countly-sdk-android</a>
  documentation for details.
</p>
<p>
  And then, change the way you init Countly by adding an additional call to
  <code>initMessaging</code>:
</p>
<pre><code class="csharp">Countly.SharedInstance()
      .Init(this, "YOUR_SERVER", "APP_KEY", null, DeviceId.Type.AdvertisingId)
      .InitMessaging(this, this.Class, "PROJECT_NUMBER", Countly.CountlyMessagingMode.Test);
</code></pre>
<p>
  Here, starting with the line <code>.InitMessaging</code>, the first parameter
  is an activity which would be started when the user clicks on notification, the
  second parameter is its class, and <code>PROJECT_NUMBER</code> is Project Number
  retrieved from your Google Developers Console. The last parameter controls whether
  this device is recorded as a test device on the Countly server, or as a production
  device. This would allow you to send messages either to test (using
  <code>.TEST</code>) or to production (using <code>.PRODUCTION</code>) users only,
  so you could separate user bases in order to make initial tests.
</p>
<p>
  Behind the scenes, Countly will add latest Google Play Services dependency and
  add some configuration options to your <code>AndroidManifest.xml</code>.
</p>
<p>
  If you want to get notified whenever a new message arrives (optional step), register
  your <code>BroadcastReceiver</code> like this:
</p>
<p>
  Create a <code>CustomBroadcastReceiver</code> class, inherit it with
  <code>BroadcastReceiver</code> abstract class found in
  <code>LY.Count.Android.Sdk.Messaging</code>. Implement the function
  <code>OnReceive</code>.
</p>
<pre><code class="csharp">public void onReceive(Context context, Intent intent) {
            var message = Intent.GetParcelableExtra(CountlyMessaging.BroadcastReceiverActionMessage);
                   }</code></pre>
<p>Update the OnResume and OnPause methods as:</p>
<pre><code class="csharp">protected void onResume()
 {
    base.onResume();

    /** Register for broadcast action if you need to be notified when Countly message received */
    messageReceiver = new CustomBroadcastReceiver();
     IntentFilter filter = new IntentFilter();
    filter.AddAction(CountlyMessaging.GetBroadcastAction(this));
    registerReceiver(messageReceiver, filter);
}

protected void onPause() 
{
    base.onPause();
    /** Don't forget to unregister receiver */
    unregisterReceiver(messageReceiver);
}</code></pre>
<h2>Automatic message handling</h2>
<p>
  Countly handles most common message handling tasks for you. For example, it generates
  and shows Notifications or Dialogs and tracks conversion rates automatically.
  In most cases you don't need to know how it works, but if you want to customize
  the behavior or exchange it with your own implementation, here is a more in depth
  explanation of what it does:
</p>
<p>
  First the received notification payload is analyzed and if it's a Countly notification
  (has <code>"c"</code> dictionary in payload), processes it. Otherwise, or if
  the notification analysis says that is a <code>Data-only</code> notification
  (you're responsible for message processing), it does nothing.
</p>
<p>
  After that it automatically makes callbacks to Countly Messaging server to calculate
  number of push notifications open and number of notifications with positive reactions.
</p>
<p>
  Here are explanations of common usage scenarios that are handled automatically:
</p>
<ul>
  <li>
    Doesn't do anything except for conversions tracking if you specify that it
    is a <code>Data-only</code> notification in the dashboard. This effectively
    sets a special flag in message payload so you could process it on your own.
  </li>
  <li>
    It displays a <code>Notification</code> whenever a message arrives and your
    application is in foreground.
  </li>
  <li>
    It displays a <code>Dialog</code> when a new message arrives and your application
    is in foreground.
  </li>
  <li>
    It displays a <code>Dialog</code> when a new message with a action arrives
    (see URL, review below), and user responds to it by swiping or tapping notification.
  </li>
  <li>
    It displays a <code>Dialog</code> on a next application launch if user didn't
    respond (tapped) to a message with a action (see URL, review below) when
    it arrived.
  </li>
</ul>
<p>
  A <code>Dialog</code> always has a message, but the button set displayed depends
  on the message type:
</p>
<ul>
  <li>
    For notifications without any actions (just a text message) it displays a
    single Cancel button;
  </li>
  <li>
    For notifications with a <strong>URL</strong> (you ask user to open a link
    to some blog post, for instance) it displays Cancel &amp; Open buttons;
  </li>
</ul>
<h2>Developer-overridden message handling</h2>
<p>
  You can also completely disable push notification handling made by Countly SDK.
  To do that just add <code>true</code> to the end of your
  <code>initMessaging()</code> call:
</p>
<pre><code class="csharp">Countly.SharedInstance()
    .Init(this, "YOUR_SERVER", "APP_KEY", null, DeviceId.Type.ADVERTISING_ID)
    .InitMessaging(this, CountlyActivity.Class, "PROJECT_NUMBER", Countly.CountlyMessagingMode.TEST, true);</code></pre>
<p>
  This parameter effectively disables any UI interactions and
  <code>Activity</code> instantiation from Countly SDK. To enable custom processing
  of push notifications you can either register your own
  <code>WakefulBroadcastReceiver</code>, or use
  <a href="http://resources.count.ly/v1.0/docs/countly-sdk-for-android#section-integrating-countly-push-into-android-app">our example with broadcast action</a>.
  Once you switched off default push notification UI, please make sure to call
  <code>CountlyMessaging.recordMessageOpen(id)</code> whenever push notification
  is delivered to your device and
  <code>CountlyMessaging.recordMessageAction(id, index)</code> whenever user positively
  reacted on your notification. <code>id</code> is a message id string you can
  get from <code>c.i</code> key of push notification payload. <code>index</code>
  is optional and used to identify type of action: 0 for tap on notification in
  drawer, 1 for first button of rich push, 2 for second one.
</p>
<h1>Setting up crash reporting</h1>
<p>
  Countly SDK for Android has an ability to collect
  <a href="http://resources.count.ly/docs/introduction-to-crash-reporting-and-analytics">crash reports</a>
  which you can examine and resolve later on the server.
</p>
<h2>Enabling crash reporting</h2>
<p>
  Following function enables crash reporting, that will automatically catch uncaught
  Java exceptions.
</p>
<pre><code class="java">Countly.SharedInstance().EnableCrashReporting();</code></pre>
<h2>Adding a custom key-value segment to a crash report</h2>
<p>
  You can add a key/value segments to crash report, like for example, which specific
  library or framework version you used in your app, so you can figure out if there
  is any correlation between specific library or other segment and crash reports.
</p>
<p>Use the following function for this purpose:</p>
<pre><code class="csharp">Countly.SharedInstance().SetCustomCrashSegments(Dictionary&lt;String, String&gt; segments);</code></pre>
<h2>Adding breadcrumbs</h2>
<p>
  Following command adds crash breadcrumb like log record to the log that will
  be send together with crash report.
</p>
<pre><code class="csharp">Countly.SharedInstance().AddCrashLog(String record);</code></pre>
<h2>Logging handled exceptions</h2>
<p>
  You can also log handled exceptions on monitor how and when they are happening
  with the following command:
</p>
<pre><code class="csharp">Countly.SharedInstance().LogException(Exception exception);</code></pre>
<h1>Additional SDK features</h1>
<h2>Testing</h2>
<p>
  You've probably noticed that we used
  <code>Countly.CountlyMessagingMode.TEST</code> in our example. That is because
  we're building the application for testing purposes for now. Countly separates
  users who run apps built for test and for release. This way you'll be able to
  test messages before sending them to all your users. When you're releasing the
  app, please use <code>Countly.CountlyMessagingMode.PRODUCTION</code>.
</p>
<h2>Push Notifications localization</h2>
<p>
  While push notification messages in Countly Messaging are properly localized,
  you can also localize the way notifications are displayed. By default, Countly
  uses your application name for a title of notification alert and the English
  word "Open" for the alert button name. If you want to customize it, pass an array
  of <code>String</code>s, where the button name is the first value, to
  <code>initMessaging</code> call:
</p>
<pre><code class="csharp">String[] pushLocalizationArray = new String[]{"Open"};
Countly.SharedInstance()
    .Init(this, "YOUR_SERVER", "APP_KEY", null, DeviceId.Type.AdvertisingId)
    .InitMessaging(this, CountlyActivity.Class, "PROJECT_ID", Countly.CountlyMessagingMode.Test, pushLocalizationArray);</code></pre>
<h2>Geolocation-aware notifications (Enterprise Edition only)</h2>
<p>
  You can send notifications to users located at predefined locations. By default,
  Countly uses geoip database in order to bind your app users to their location.
  But if your app has access to better location data, you can submit it to the
  server:
</p>
<pre><code class="java">double latitude = 12;
double longitude = 22;

Countly.SharedInstance().SetLocation(latitude, longitude);</code></pre>
<h2>View tracking</h2>
<p>
  View tracking is a means to report every screen view to Countly dashboard. In
  order to enable automatic view tracking, call:
</p>
<pre><code class="java">Countly.SharedInstance().SetViewTracking(true);</code></pre>
<div class="callout callout--warning">
  <p>Short view names available after version 17.09</p>
</div>
<p>
  t is possible to use short view names which will use the simple activity name.
  That would look like "activityname". To use this functionality, call this before
  calling init:
</p>
<pre><code class="csharp">Countly.SharedInstance().SetAutoTrackingUseShortName(true);</code></pre>
<p>
  Also you can track custom views with following code snippet:
</p>
<pre><code class="java">Countly.SharedInstance().RecordView("View name");</code></pre>
<p>
  To review the resulting data, open the dashboard and go to
  <code>Analytics &gt; Views</code>. For more information on how to use view tracking
  data to it's fullest potential, look for more information
  <a href="http://resources.count.ly/docs/view-analytics">here</a>.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/1059a04-3.PNG">
</div>
<h2>Receiving and showing badge number from push notifications</h2>
<div class="callout callout--info">
  <h3 class="callout__title">Minimum Countly Server Version</h3>
  <p>
    This feature is supported only on servers with the minimum version 16.12.2.
  </p>
</div>
<p>
  While showing badges isn't supported natively by Android, there are some devices
  and launchers that support it. Therefore you may want to implement such a feature
  in your app but not that not all devices will support badges.
</p>
<p>
  While creating a new message in the messaging overview and preparing it's content,
  there is a optional option called "Add iOS badge". You can use that to send badges
  also to Android devices.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/5fbc4a2-Ekran_Resmi_2017-01-27_07.15.34.png">
</div>
<p>
  In order to receive this badge number in your application, you have to subscribe
  to the broadcasts about received messages. There, you are informed about all
  received push notifications using Message and bundle. The badge number is sent
  with the key "badge". You can use that to extract the badge number from the received
  bundle and then use it to display badge numbers with your implementation of choice.
</p>
<p>
  In the below example we will use a badge library called CountlySDK.Badge.Xamarin.Android,
  which is used to show badges on Android. Find the
  <a href="https://www.nuget.org/packages/CountlySDK.Badge.Xamarin.Android/">CountlySDK.Badge.Xamarin.Android</a>
  NuGet package and include it in your project.
</p>
<p>
  <strong>CountlySDK.Badge.Xamarin.Android</strong>:
</p>
<pre><code class="text">Install-Package CountlySDK.Badge.Xamarin.Android -Version 1.0.1</code></pre>
<p>
  Create a CustomBroadcastReceiver class, inherit it with BroadcastReciever abstract
  class found in LY.Count.Android.Sdk.Messaging. Implement the function OnReceive.
</p>
<pre><code class="csharp">public void onReceive(Context context, Intent intent) {
        Message message = intent.getParcelableExtra(CountlyMessaging.BROADCAST_RECEIVER_ACTION_MESSAGE);
        Log.i("CountlyActivity", "Got a message with data: " + message.getData());

        //Badge related things
        Bundle data = message.getData();
        String badgeString = data.getString("badge");
        try {
            Int32.TryParse(badgeString,out int badgeCount);

            bool succeded = ShortcutBadger.ApplyCount(this, badgeCount);
            if(!succeded) {
                Toast.MakeText(this, "Unable to put badge", ToastLength.Short);
            }
        } catch (NumberFormatException exception) {
            Toast.MakeText(getApplicationContext(), "Unable to parse given badge number", ToastLength.Short);
        }
    }</code></pre>
<h2>Checking if init has been called</h2>
<p>
  In case you want to check if init has been called, you can just use the following
  function:
</p>
<pre><code class="csharp">var value = Countly.SharedInstance().IsInitialized();</code></pre>
<h2>Checking if onStart has been called</h2>
<p>
  For some applications there might a use case where the developer would like to
  check if the Countly sdk<code>onStart</code> function has been called. For that
  they can use the following call:
</p>
<pre><code class="csharp">var value = Countly.SharedInstance().HasBeenCalledOnStart;</code></pre>
<h2>Ignoring app crawlers</h2>
<p>
  Sometimes server data might be polluted with app crawlers which are not real
  users, and you would like to ignore them. Starting from the 17.05 release it's
  possible to do that filtering on the app level. The current version does that
  using device names. Internally the Countly sdk has a list for crawler device
  names, if a device name matches one from that list, no information is sent to
  the server. At the moment that list has only one entry: "Calypso AppCrawler".
  In the future we might add more crawler device names if such are reported. If
  you have encountered a crawler that is not in that list, but you would like to
  ignore, you can add it to your sdk list yourself by calling
  <code>addAppCrawlerName</code>. Currently by default the sdk is ignoring crawlers,
  if you would like to change that, use <code>ifShouldIgnoreCrawlers</code>. If
  you want to check if the current device was detected as a crawler, use
  <code>isDeviceAppCrawler</code>. Detection is done in the init function, so you
  would have to add the crawler names before that and do the check after that.
</p>
<pre><code class="csharp">//set that the sdk should ignore app crawlers
var value = Countly.SharedInstance().IfShouldIgnoreCrawlers;

//set that the sdk should not ignore app crawlers
var value = Countly.SharedInstance().IfShouldIgnoreCrawlers;

//add another app crawler device name to ignore
Countly.SharedInstance().AddAppCrawlerName("App crawler");

//returns true if this device is detected as a app crawler and false otherwise
var value = Countly.SharedInstance().IsDeviceAppCrawler();</code></pre>