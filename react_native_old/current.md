<div class="callout callout--info">
  <h3 class="callout__title">This is an unmaintained SDK</h3>
  <p>
    You are suggested to use React Native (bridge) SDK instead. This SDK will
    be declared as end-of-life very soon.
  </p>
</div>
<p>
  This tutorial shows you how to include Countly SDK in your React Native application.
  It is based on the following:
</p>
<ul>
  <li>react-native-cli: 2.0.1</li>
  <li>react-native: 0.49.1</li>
</ul>
<p>
  There are other ways to create a react Native application. Our SDK works with
  all methods, but in this document we are going to show react-native cli.
</p>
<h1>Creating a new application</h1>
<p>
  Before creating a new application, please
  <a href="https://facebook.github.io/react-native/docs/getting-started.html">look at the documentation here</a>.
  Make sure you click the tab called
  <code>Building Projects with Native Code</code> and follow instructions.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/8dad77e-1.png">
</div>
<p>
  Enter following commands to install <code>react-native-cli</code> and configure
  your environment.
</p>
<pre><code class="shell">npm install -g react-native-cli     # Install React Native
react-native init AwesomeProject    # Create a new project

cd AwesomeProject                   # Go to that directory
react-native run-android # OR       # Run the android project
react-native run-ios                # Run the iOS project

# New terminal
adb reverse tcp:8081 tcp:8081       # Link Android port
npm start                           # Run the build server</code></pre>
<h1>Installing the SDK</h1>
<p>
  Run the following snippet in the root of your react native project to install
  the npm dependencies and link the native libraries.
</p>
<pre><code class="shell"># Add dependencies
npm install --save react-native-device-info
npm i react-native-background-timer --save
npm i react-native-restart
react-native link

# Include the Countly Class in the file that you want to use.
npm install --save countly-sdk-react-native
</code></pre>
<p>
  You can also review example usage of SDK
  <a href="https://github.com/Countly/countly-sdk-react-native/blob/update/index.android.js">for Android</a>
  and
  <a href="https://github.com/Countly/countly-sdk-react-native/blob/update/index.ios.js">for iOS</a>.
</p>
<h1>SDK Usage</h1>
<p>
  Please see below on how to initialize and start Countly SDK.
</p>
<pre><code class="javascript">// In your javascript code 

import Countly from 'countly-sdk-react-native';

Countly.isDebug = true; // Set to true to see the logs

// example for initalization and start session in first go. 

// deviceId is optional field. If you are using a service 
// different from try.count.ly (e.g your own or another test
// server by Countly), mention it below. Double check http 
// or https connectivity.

Countly.begin("https://try.count.ly","app_key","deviceId")
  .then((result) =&gt; {
    // do your stuff on session start
  })
  .catch((err) =&gt; {
    // returns cause of failed initialization
  });

// From second session and further start session
Countly.start()
  .then((result) =&gt; {
    // do your stuff on session start
  })
  .catch((err) =&gt; {
    // returns cause of failing operation
  });

// stop session
Countly.stop().then((result) =&gt; {
  // session stops successfully
});
</code></pre>
<p>
  <strong>NOTE:</strong> <code>Countly.begin</code> method will automatically start
  the session for the first time. <code>Countly.stop</code> method can be called
  on any events on which you want to end the current session. If you have called
  the <code>Countly.stop</code> method to end the session, then you need to call
  <code>Countly.start</code> method to start new session else you need not worry
  about <code>Countly.start</code> method as <code>Countly.begin</code> will automatically
  start the session.
</p>
<p>
  If you want to initialize and start session separately you can do like shown
  below.
</p>
<pre><code class="javascript">// In your javascript code 

import Countly from 'countly-sdk-react-native';

// example for initializing countly
Countly.isDebug = true; // Set to true to see the logs

// deviceId is an optional field.

Countly.init("https://try.count.ly","app_key","deviceId")
  .then((result) =&gt; {
    // Now start session
    Countly.start()
      .then((result) =&gt; {
        // do your stuff
      })
      .catch((err) =&gt; {
        // reason for failure
      });
  })
  .catch((err) =&gt; {
    // reason for failure
  });
  </code></pre>
<p>
  If you omit deviceID above, automatically generated deviceID will be used. If
  you provide a deviceID, then it will take that as DeviceId. For example, you
  can use hashed value of user's email as a deviceID.
</p>
<h1>Sending custom events</h1>
<p>
  You can send custom events with segmentations using following examples.
</p>
<p>Example for sending a basic event:</p>
<pre><code class="javascript">var event = {"key":"basic_event","count":1};
Countly.recordEvent(event);</code></pre>
<p>Example for sending event with sum:</p>
<pre><code class="javascript">var event = {"key":"event_sum","count":1,"sum":"0.99"};
Countly.recordEvent(event);</code></pre>
<p>
  Example for sending event with a segmentation value (in this case, Germany and
  Age):
</p>
<pre><code class="javascript">var event = {"key":"event_segment","count":1};
event.segmentation = {"Country" : "Germany", "Age" : "28"};
Countly.recordEvent(event);</code></pre>
<p>Example for sending event with segmentation value and sum:</p>
<pre><code class="javascript">var event = {"key":"event_segment_sum","count":1,"sum":"0.99"};
event.segmentation = {"Country" : "Turkey", "Age" : "28"};

Countly.recordEvent(event);</code></pre>
<p>
  Example for sending a timed event. It tracks how long a specific event takes
  to complete. If you send a timed event, then under Countly dashboard you will
  see its duration (in seconds).
</p>
<pre><code class="javascript">Countly.startEvent("timedEvent");
Countly.endEvent("timedEvent");</code></pre>
<p>
  Duration of the event will be calculated automatically when
  <code>endEvent</code> method is called.
</p>
<h1>Push Notifications</h1>
<p>
  This section requires setting up either APNS (Apple Push Notification Services)
  or FCM (Firebase Cloud Services). For APNS, you need to get push credentials
  and upload to Countly.
  <a href="https://resources.count.ly/docs/countly-sdk-for-ios-and-os-x#section-push-notifications">This document</a>
  explains how to retrieve and upload push credentials for APNS.
</p>
<p>
  First, install react-native-firebase plugin to implement push notifications.
</p>
<pre><code class="shell">npm install --save react-native-firebase

// Link Firebase
react-native link react-native-firebase</code></pre>
<p>
  If you are developing in android you would require to setup FCM in android. You
  can follow the below given steps to guide you through.
</p>
<ol>
  <li>Setup google-services.json</li>
  <li>
    A google-services.json file contains all of the information required by the
    Firebase Android SDK to connect to your Firebase project. To automatically
    generate the json file, follow the instructions on the Firebase console to
    "Add Firebase to your app".
  </li>
</ol>
<p>
  Once downloaded, place this file in the root of your project at android/app/google-services.json.
  In order for Android to parse this file, add the google-services gradle plugin
  as a dependency to your project in the project level build.gradle file (android/build.gradle):
</p>
<pre><code class="javascript">buildscript {
    repositories {
        google()  // &lt; Check this line exists and is above jcenter.
        jcenter()
    }
    dependencies {
      ...
        classpath 'com.android.tools.build:gradle:3.2.0' // Just to make sure.
        classpath 'com.google.gms:google-services:4.0.1'
      ...
    }
}</code></pre>
<p>
  Now setup gradle dependencies in your android/app/build.gradle file :
</p>
<pre><code class="java">dependencies {
    ...
    //These should be already present in your gradle file.
  	implementation project(':react-native-firebase')
    
    //Add these lines
    implementation "com.google.android.gms:play-services-base:16.0.1"
    implementation "com.google.firebase:firebase-core:16.0.6"
    implementation "com.google.firebase:firebase-messaging:17.3.4"
}

//Make sure you put this to the bottom most of your build.gradle
apply plugin: 'com.google.gms.google-services'
</code></pre>
<p>
  Now go to your MainApplication.java and add these imports if not present.
</p>
<pre><code class="java">//add these imports if not present.  
import io.invertase.firebase.RNFirebasePackage;
import io.invertase.firebase.messaging.RNFirebaseMessagingPackage; 
import io.invertase.firebase.notifications.RNFirebaseNotificationsPackage; 

...
  
@Override
protected List getPackages() {
  return Arrays.asList(
 new MainReactPackage(),
    //Make sure these files are present
 new RNFirebasePackage(),
 new RNFirebaseMessagingPackage(),
 new RNFirebaseNotificationsPackage()
 );                               
}</code></pre>
<p>Add these lines to your Android Manifest file</p>
<pre><code class="xml">...
 &lt;uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" /&gt;
  &lt;uses-permission android:name="android.permission.VIBRATE" /&gt;
    &lt;uses-permission android:name="android.permission.INTERNET" /&gt;
    &lt;uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW"/&gt;
....

  &lt;application&gt;
    ......

 &lt;service android:name="io.invertase.firebase.messaging.RNFirebaseMessagingService"
                  android:enabled="true"
                  android:exported="true"&gt;
              &lt;intent-filter&gt;
                &lt;action android:name="com.google.firebase.MESSAGING_EVENT" /&gt;
              &lt;/intent-filter&gt;
            &lt;/service&gt;
            &lt;service android:name="io.invertase.firebase.messaging.RNFirebaseInstanceIdService"&gt;
              &lt;intent-filter&gt;
                &lt;action android:name="com.google.firebase.INSTANCE_ID_EVENT"/&gt;
              &lt;/intent-filter&gt;
            &lt;/service&gt;
           &lt;service android:name="io.invertase.firebase.messaging.RNFirebaseBackgroundMessagingService" /&gt;
&lt;/application&gt;
</code></pre>
<p>Add these lines in settings.gradle:</p>
<pre><code class="java">include ':react-native-firebase'                       
project(':react-native-firebase').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-firebase/android')
</code></pre>
<p>
  Now go again to your android/app/build.gradle and add this line:
</p>
<pre><code class="text">dependencies {
  compile project(':react-native-firebase')
  ...
}</code></pre>
<p>
  If your Installing in iOS, follow the given steps to guide you through. but before
  we proceed please make sure you have generated your certificates properly.
</p>
<ol>
  <li>Setup GoogleService-Info.plist</li>
  <li>
    A GoogleService-Info.plist file contains all of the information required
    by the Firebase iOS SDK to connect to your Firebase project. To automatically
    generate the plist file, follow the instructions on the Firebase console
    to "Add Firebase to your app".
  </li>
</ol>
<p>
  Once downloaded, add the file to your iOS app using 'File &gt; Add Files to "[YOUR
  APP NAME]"…' in XCode.
</p>
<ol>
  <li>Initialize Firebase</li>
  <li>
    To initiaize the native SDK in your app, add the following to your ios/[YOUR
    APP NAME]/AppDelegate.h file:
  </li>
</ol>
<pre><code class="objectivec">//At the begining of your file
#import 
...
//At the beginning of the didFinishLaunchingWithOptions:(NSDictionary *)launchOptions method add the following line:
[FIRApp configure];
...
</code></pre>
<p>
  Now, Install Firebase Library using cocoapods. For this, go to your IOS project
  and run command <code>pod init</code> and then add Firebase/Core and Firebase/Messaging
  as shown below:
</p>
<pre><code class="objectivec">
# Uncomment the next line to define a global platform for your project
platform :ios, '9.0'

target 'ReactPushNotifications' do
  # Uncomment the next line if you're using Swift or would like to use dynamic frameworks
  # use_frameworks!

  # Pods for ReactPushNotifications - Add these lines
  pod 'Firebase/Core'
  pod 'Firebase/Messaging'

  target 'ReactPushNotificationsTests' do
    inherit! :search_paths
    # Pods for testing
  end

end
</code></pre>
<p>
  Now open your project on Xcode from and goto Capabilities and do the following:
</p>
<ol>
  <li>Turn on Push Notifications</li>
  <li>Turn on Background modes</li>
  <li>Check Remote notifications</li>
</ol>
<p>
  Now, go to Build Phases. Click on the “+” under “Link Binary With Libraries”
  to add a new library. Add UserNotifications.framework. This framework is required
  since iOS 10 for push notifications handling. Go to Build Settings, find Header
  Search Path, double click its value and press “+” button. Add following line
  there.
</p>
<pre><code class="text">$(SRCROOT)/../node_modules/react-native-firebase/ios/RNFirebase
</code></pre>
<p>Go to AppDelegate.h and add those lines:</p>
<pre><code class="objectivec">#import &lt;UIKit/UIKit.h&gt;
#import &lt;UserNotifications/UserNotifications.h&gt;

@interface AppDelegate : UIResponder &lt;UIApplicationDelegate, UNUserNotificationCenterDelegate&gt;

@property (nonatomic, strong) UIWindow *window;

@end</code></pre>
<p>Now Add Firebase package in your AppDelegate.m as follows:</p>
<pre><code class="objectivec">#import "AppDelegate.h"
//Add these lines
#import 
#import "RNFirebaseNotifications.h"
#import "RNFirebaseMessaging.h"

#import &lt;React/RCTBundleURLProvider.h&gt;
#import &lt;React/RCTRootView.h&gt;

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
 [FIRApp configure];
 [[UNUserNotificationCenter currentNotificationCenter] setDelegate:self];
 [RNFirebaseNotifications configure];

 NSURL *jsCodeLocation;

 #ifdef DEBUG
   jsCodeLocation = [[RCTBundleURLProvider sharedSettings] jsBundleURLForBundleRoot:@"index" fallbackResource:nil];
 #else
   jsCodeLocation = [[NSBundle mainBundle] URLForResource:@"main" withExtension:@"jsbundle"];
 #endif

 RCTRootView *rootView = [[RCTRootView alloc] initWithBundleURL:jsCodeLocation
                                                     moduleName:@"FCMPushTest"
                                              initialProperties:nil
                                                  launchOptions:launchOptions];
 rootView.backgroundColor = [[UIColor alloc] initWithRed:1.0f green:1.0f blue:1.0f alpha:1];

 self.window = [[UIWindow alloc] initWithFrame:[UIScreen mainScreen].bounds];
 UIViewController *rootViewController = [UIViewController new];
 rootViewController.view = rootView;
 self.window.rootViewController = rootViewController;
 [self.window makeKeyAndVisible];
 return YES;
}

- (void)application:(UIApplication *)application didReceiveRemoteNotification:(nonnull NSDictionary *)userInfo
fetchCompletionHandler:(nonnull void (^)(UIBackgroundFetchResult))completionHandler{
 [[RNFirebaseNotifications instance] didReceiveRemoteNotification:userInfo fetchCompletionHandler:completionHandler];
}

- (void)application:(UIApplication *)application didRegisterUserNotificationSettings:(UIUserNotificationSettings *)notificationSettings {
 [[RNFirebaseMessaging instance] didRegisterUserNotificationSettings:notificationSettings];
}

-(void) userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void (^)(void))completionHandler {
 [[RNFirebaseMessaging instance] didReceiveRemoteNotification:response.notification.request.content.userInfo];
 completionHandler();
}


@end
</code></pre>
<p>
  For push notification action support in iOS device, install this plugin (<a href="https://github.com/nodexpertsdev/react-native-ios-notification-actions">https://github.com/nodexpertsdev/react-native-ios-notification-actions</a>)
  and follow the instructions to setup push notification action. This step should
  only be performed for iOS project only else it will generate an error.
</p>
<pre><code class="text"># For push notifications action support in iOS

npm install --save https://github.com/nodexpertsdev/react-native-ios-notification-actions
react-native link

# Note: string you set in the identifier of 
# NotificationActions.category must match to the 'category' 
# of the push notification payload
</code></pre>
<p>To initialize push notification, use the following:</p>
<pre><code class="javascript">// To initialize the push notification.
// For Android we have two types of users i.e test and production users
// For test mode use Countly.TEST
// For production mode use Countly.PRODUCTION

// For IOS we have three types of users 
// For adhoc mode use Countly.ADHOC
// For test mode use Countly.TEST
// For production mode use Countly.PRODUCTION
// Add this import at the top
import firebase from 'react-native-firebase';

// example within an App compontent
componentDidMount(){
   ///For android only --start
  if (Platform.OS === 'android') {
  const channel = new firebase.notifications.Android.Channel('your_channel_id', 'your_channel_name', firebase.notifications.Android.Importance.Max)
          .setDescription('Your_channel_description');
  firebase.notifications().android.createChannel(channel);
  }
///For android only --END
 Countly.initMessaging(Countly.DEVELOPMENT,'your_channel_id');
} 

// For unregistering listeners
componentWillUnmount() {
    Countly.UnmountNotificationListeners();
}
// If you have not installed the dependencies and use above config settings your app will start crashing.
//For handlink the deep linking data you can get your Actions link here as mentioned below.
constructor(props) {
  super(props);
  Countly.deepLinkHandler = {
        handler1: url =&gt; console.log(url), //Here you would get your action url's
      }
  
  // for getting json from data-only message /data
   Countly.jsonHandler = {
        handler: json =&gt; console.log(json), 
      }
}</code></pre>
<p>
  Countly.initMessaging retrieve token from APNS/FCM and then pass it to Countly
  server. After getting the token, your dashboard is ready to send push notifications
  to that device.
</p>
<p>
  Add below lines in index.js for enabling background messaging.
</p>
<pre><code class="javascript">import Countly from 'countly-sdk-react-native';

const id = 'your_channel_id';


AppRegistry.registerHeadlessTask('RNFirebaseBackgroundMessage', () =&gt; {
  return message =&gt; Countly.bgMessaging(message, id);
});</code></pre>
<h1>User Profiles</h1>
<div class="callout callout--info">
  <h3 class="callout__title">Enterprise Edition Feature</h3>
  <p>
    This feature is only available with Enterprise Edition subscription.
  </p>
</div>
<p>
  You can see detailed user information under User Profiles section of Countly
  dashboard by recording user details. You can record default and custom properties
  of user details like this:
</p>
<pre><code class="javascript">Countly.setUserData({
    "name": "Name Surname",
    "username": "xyz",
    "email": "xyz@gmail.com",
    "organization": "XYZ Technologies",
    "phone": "9999999999",
    //Web URL to picture
    "picture": "https://URL/file/pic250x250.png",
    "gender": "M", //M or F
    "byear": 1989, //birth year
    "custom": {
        "key1": "value1",
        "key2": "value2"
    }
});</code></pre>
<p>
  In addition, you can use custom user details modifiers like this:
</p>
<pre><code class="javascript">Countly.userData.setProperty("setPropertyKey", "setPropertyKeyValue");
Countly.userData.increment("incrementKey");
Countly.userData.incrementBy("incrementByKey", 10);
Countly.userData.multiply("multiplyKey", 20);
Countly.userData.saveMax("saveMaxKey", 100);
Countly.userData.saveMin("saveMinKey", 50);
Countly.userData.setOnce("setOnceKey", 200);</code></pre>
<h1>Manual Tracking of View (Screen)</h1>
<p>
  You can record (track) view as well as the time for which user has visited the
  particular screen.
</p>
<pre><code class="javascript">// Example for recording view
Countly.recordView(ViewName); // ViewName will be your screen name</code></pre>
<p>
  You can also track (record) the action performed on the view.
</p>
<pre><code class="javascript">// To record an action:
Countly.recordViewActions(actionType, touchCoordinate);

// where actionType may be 'touch', 'swipe' etc... and 
// TouchCoordinate is the x, y axis of touch point.</code></pre>
<h1>Crash Reporting</h1>
<p>
  Countly can send automated crash reporting to a Countly server. Below you can
  see how to enable it.
</p>
<p>First, add dependencies to your application:</p>
<pre><code class="shell">npm i react-native-exception-handler --save
npm i react-native-restart
react-native link </code></pre>
<p>
  Then, outside the root component add the following and enable crash reporting
  feature.
</p>
<pre><code class="javascript">// Outside the root component add the following line.
// Setting first parameter to true will enable crash 
// reporting in production mode.

Countly.enableCrashReporting(true); </code></pre>
<p>
  In order to enable the crash reporting in development mode, use the following
  line. Here, second parameter is optional which will be false by default. It is
  recommended not to use crash reporting in development mode - it is used to hide
  the internal error from user and send the issue to the developer.
</p>
<pre><code class="javascript">Countly.enableCrashReporting(true, true); </code></pre>
<p>
  If the crash occurred, SDK sends the crash data to Countly and shows an alert
  box having the crash message and a Restart button. Restart button will restart
  the application.
</p>
<p>
  If you want to customize the default alert box functionality and message you
  can do so by changing in config variable as shown below.
</p>
<pre><code class="javascript">// Config variable to customize default alert box.

Countly.defaultAlert = {
// default value will be false.
      enable: false, 
// Title of the alert box
      title: 'Application Error', 
// Message in alert box
      message: 'Application will be restarted', 
// Alert box button title
      buttonTitle: 'Restart', 
// Default method will restart the application. 
// You can change the methods according your requirement.
      onClick: () =&gt; this.restartApp(), 
    };</code></pre>
<p>
  Further, if you think that you want to create your own custom crash log method
  you can do so by following the below instructions.
</p>
<pre><code class="javascript">// create your custom method

const crashMethod = () =&gt; {
// This is optional. If you want to send your custom 
// data to the dashboard with crashLog Data, use this:
  const crash = { 'customData': test } 

// Required. This is required if you do not call this 
// method Countly will not send the crash log to the dashboard.
  Countly.addCrashLog(crash); 
  
  /* Do your stuff */
  
}

// Then assign this function in the Countly config show below.

// This will disable default crash method and enable your crash method.
Countly.customCrashLog = crashMethod; </code></pre>
<div class="callout callout--info">
  <h3 class="callout__title">Important note</h3>
  <p>
    All crash method definition and crash config assignment will be done in root
    component file of your application (which will be index.js/ index.android.js/
    index.ios.js/ App.js) and outside the React class.
  </p>
</div>
<h1>Parameter Tampering</h1>
<p>
  This is one of the preventive measures of Countly. If someone in the middle intercepts
  the request, it would be possible to change the data in the request and make
  another request with other data to the server, or simply make random requests
  to the server through retrieved App Key.
</p>
<p>
  To prevent that, SDK provides an option to send a checksum along the request
  data. For this, you should provide a random string as SALT to SDK as parameter
  or configuration options.
</p>
<p>
  You can set optional <code>secretSalt</code> to be used for calculating checksum
  of request data, which will be sent with each request using
  <code>&amp;checksum256</code> field. You need to set exactly the same secretSalt
  on Countly under
  <code>Management &gt; Applications&gt;"your_app"&gt;Salt  for checksum</code>.
  If <code>secretSalt</code> on Countly Server is set, all requests would be checked
  for validity of <code>&amp;checksum256</code> field before being processed.
</p>
<pre><code class="shell">npm install crypto-js;</code></pre>
<p>and from your app use below lines to set your secret salt</p>
<pre><code class="text">// set salt in Countly SDK config
Countly.secretSalt = 'XYZ';</code></pre>
<p>
  If SALT is not provided, SDK makes ordinary requests without any checksums.
</p>
<h1>Star Rating</h1>
<p>
  For the rating purpose of your application, you can use star rating component
  of Countly by implementing steps.
</p>
<pre><code class="shell">// Dependency to use Countly Star Rating feature

npm install --save react-native-modal
react-native link
</code></pre>
<p>For importing star rating component from Countly:</p>
<pre><code class="javascript">import { StarRating } from 'countly-sdk-react-native';</code></pre>
<p>Then use star rating component as follows:</p>
<pre><code class="html"> this.setState({isVisible: false})} // required
/&gt;
  
// Default values for optional field:
// noOfStars = 5
// message = 'How would you rate the app?'
// dismissButtonTitle = Dismiss</code></pre>
<h1>Other SDK usage scenarios</h1>
<h3>Using custom device ID</h3>
<p>
  If you want to use custom device ID, you can change it as follows. Note that
  once set, device ID will be persistently stored in device on the first launch,
  and will not change even after app delete and re-install, unless you change it
  explicitly.
</p>
<pre><code class="javascript">Countly.changeDeviceId("654321");</code></pre>
<h3>Change DeviceId on server</h3>
<p>
  If you want to change the device ID on Countly server, follow steps below.
</p>
<pre><code class="javascript">// First parameter is onServer
let onServer = ture;

// Then call the setNewDeviceId method to set the new Device Id
Countly.setNewDeviceId(onServer, newDeviceId);

// By default the onServer method will be false. Both the parameters are required.

// If onServer is false then current session will be end and the new session starts with new DeviceId.

// If onServer is true than the new session metrics will contain new DeviceId and the old deviceId data will be merged with the new DeviceId.</code></pre>
<h3>Force SDK to make POST request by default</h3>
<pre><code class="javascript">// Call method setHttpPostForced with parameter true, as shown below

Countly.setHttpPostForced(true);</code></pre>
<h3>SSL Certificate Pinning</h3>
<p>
  To secure the request from "Man in the Middle" attack, you can implement SSL
  Certificate Pinning in your application. Below are the steps to implement SSL
  Certificate Pinning.
</p>
<pre><code class="shell">// Install dependencies
npm i react-native-pinch

// Link the libraries using the following command
react-native link react-native-pinch</code></pre>
<p>
  After that, you need to put the SSL certificate file (having the extension
  <code>.cer</code>) into <code>src/main/assets/</code> for Android and for iOS
  place your <code>.cer</code> files in your iOS Project. Don't forget to add them
  in your Build Phases &gt; Copy Bundle Resources, in Xcode.
</p>
<p>
  Then you need to set the name of the <code>.cer</code> file in
  <code>Countly.cerFileName</code> config flag as shown below.
</p>
<pre><code class="javascript">// Notice the file name you should set to the config flag 
// doesn't have an extension.

Countly.cerFileName = "fileName";</code></pre>
<p>
  <strong>Note:</strong> If you set the file name in the
  <code>Countly.cerFileName</code> flag and forgot to put the file at the required
  location, Countly SDK will stop sending the request to the dashboard. Also, the
  SSL certificate must be globally accepted and not be self-signed.
</p>
<p>
  If you face any challenges to implement, there is a working demo / example
  <a href="https://github.com/Countly/countly-sdk-react-native/blob/master/App.js">in this repository</a>.
</p>
<p>
  We welcome all issues and bug reports -
  <a href="https://github.com/Countly/countly-sdk-react-native/issues">please send them here</a>
  and we will respond very quickly.
</p>