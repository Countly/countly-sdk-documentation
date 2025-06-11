<p>
  This documentation is for the Countly iOS SDK version 25.4.X. The SDK source
  code repository can be found
  <a href="https://github.com/Countly/countly-sdk-ios">here</a>.
</p>
<p>
  Click
  <a href="/hc/en-us/articles/360037236571#h_01H9QCP8G7Y97Y1T51TGGNDMNP" target="_self" rel="undefined">here, </a>to
  access the documentation for older SDK versions.
</p>
<p>
  The Countly iOS SDK supports minimum <code>Deployment Target</code>
  <strong>iOS 10.0</strong> (watchOS 4.0, tvOS 10.0, macOS 10.14), and it requires
  Xcode 13.0+.
</p>
<p>
  To examine the example integrations please have a look
  <a href="#h_01HPE2F8MYP82AZ29EV7N8HQJ3">here</a>.
</p>
<h1 id="h_01HAVHW0RNNZT7742WNX46GS1R">Adding the SDK to the project</h1>
<p>
  To add the Countly iOS SDK into your project, you can choose one of the following
  options:
</p>
<p>
  - Download the Countly iOS SDK source files directly from
  <a href="https://www.github.com/countly/countly-sdk-ios">GitHub</a>, add all
  <code>.h</code> and <code>.m</code> files in the <code>countly-ios-sdk</code>
  folder of your project on Xcode.
</p>
<p>
  - Clone the Countly iOS SDK
  <a href="https://github.com/Countly/countly-sdk-ios.git">repo</a> as a Git submodule.
</p>
<p>
  - Using
  <a href="#h_01HAVHW0RTQ6WN8CYVNVZQ5TEP">Swift Package Manager (SPM)</a>
</p>
<p>
  - Using <a href="#h_01HAVHW0RTQGRSE9ZRVQSAXJ74">Carthage</a>
</p>
<p>
  - Using <a href="#h_01HAVHW0RTXSFZD8R6QMX0GWPN">CocoaPods</a>
</p>
<h1 id="h_01HAVHW0RNQWE9PRRXT9HXFKMJ">SDK Integration</h1>
<h2 id="h_01HAVHW0RNVDW2E2F83R8E6PSB">Minimal Setup</h2>
<p>
  In your application delegate, import <code>Countly.h</code>, and
  <span style="font-weight: 400;">add the following lines at the beginning inside</span><code>application:didFinishLaunchingWithOptions:</code>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">#import "Countly.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  CountlyConfig* config = CountlyConfig.new;
  config.appKey = @"YOUR_APP_KEY";
  config.host = @"https://YOUR_COUNTLY_SERVER";
  [Countly.sharedInstance startWithConfig:config];

  // your code

  return YES;
}
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -&gt; Bool
{
  let config: CountlyConfig = CountlyConfig()
  config.appKey = "YOUR_APP_KEY"
  config.host = "https://YOUR_COUNTLY_SERVER"
  Countly.sharedInstance().start(with: config)
  
  // your code

  return true
}</code></pre>
  </div>
</div>
<p>
  <strong>Note:</strong> Make sure you start Countly iOS SDK on the main thread.
</p>
<p>
  <span style="font-weight: 400;">Set your app key and host on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object. Please check <a href="/hc/en-us/articles/900000908046#h_01HABSX9KX44C9SF48WRPQNCP3">here</a> for more information about acquiring application key (APP_KEY) and server URL.</span>
</p>
<p>
  <span style="font-weight: 400;">You can run your project and see the first session data immediately displayed on your Countly Server dashboard.</span>
</p>
<div class="callout callout--info">
  <p>
    If you are in doubt about the correctness of your Countly SDK integration,
    you can learn about the verification methods from
    <a href="/hc/en-us/articles/900000908046#h_01HABSX9KXE6YKVETHDWPP8J3K" target="blank">here</a>.
  </p>
</div>
<h2 id="h_01HAVHW0RNECF2W03GPMKS3E6K">Additional Features</h2>
<p>
  If you would like to use additional features, such as
  <strong>PushNotifications</strong>, <strong>CrashReporting,</strong> and
  <strong>AutoViewTracking,</strong>
  <span style="font-weight: 400;"> you can specify them in the <code>features</code></span><span style="font-weight: 400;"> array on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object before you start:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  CountlyConfig* config = CountlyConfig.new;
  config.appKey = @"YOUR_APP_KEY";
  config.host = @"https://YOUR_COUNTLY_SERVER";

  //You can specify additional features you want here
  config.features = @[CLYPushNotifications, CLYCrashReporting, CLYAutoViewTracking];

  [Countly.sharedInstance startWithConfig:config];

  // your code

  return YES;
}</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -&gt; Bool
{
  let config: CountlyConfig = CountlyConfig()
  config.appKey = "YOUR_APP_KEY"
  config.host = "https://YOUR_COUNTLY_SERVER"

  //You can specify additional features you want here
  config.features = [CLYPushNotifications, CLYCrashReporting, CLYAutoViewTracking]

  Countly.sharedInstance().start(with: config)

  // your code

  return true
}</code></pre>
  </div>
</div>
<p>Available additional features per platform:</p>
<pre>iOS<br>  CLYPushNotifications<br>  CLYCrashReporting<br>  CLYAutoViewTracking<br><br>watchOS<br>  CLYCrashReporting<br><br>tvOS<br>  CLYCrashReporting<br>  CLYAutoViewTracking<br><br>macOS<br>  CLYPushNotifications<br>  CLYCrashReporting</pre>
<h2 id="h_01HAVHW0RNPY4C22J98XT6T4NN">SDK Data Storage</h2>
<p>
  The Countly iOS SDK uses <code>NSUserDefaults</code> and a simple data file named
  <code>Countly.dat</code> under <code>NSApplicationSupportDirectory</code> (<code>NSCachesDirectory</code>
  for tvOS).
</p>
<div class="callout callout--info">
  <strong>Countly Code Generator</strong>
  <p>
    <a href="https://countly.github.io/countly-code-generator/">The Countly Code Generator</a>
    can be used to generate Countly iOS SDK code snippets effortlesly. You can
    provide values for your events, user profiles, or just start with basic integration.
    It will generate the necessary code for you.
  </p>
</div>
<h1 id="h_01HAVHW0RNQ9ZX3KMX09DDFETR">SDK Logging / Debug Mode</h1>
<p>
  <span style="font-weight: 400;">If you would like to enable the Countly iOS SDK to debug mode, which logs internal info, errors, and warnings into your console, you can set the <code>enableDebug</code></span><span style="font-weight: 400;"> flag on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object before starting Countly.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.enableDebug = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.enableDebug = true</code></pre>
  </div>
</div>
<p>
  Internal logging works only for Development environment where
  <code>DEBUG</code> flag is set in target's Build settings. But if you still can
  not see the SDK logs you have to make sure your XCode is configured correctly
  by going to Product &gt; Scheme &gt; Edit Scheme in your XCode and selecting
  Run from the menu at the left-hand side. There you should click on Arguments
  tab and make sure "OS_ACTIVITY_MODE" argument is set to "disable".
</p>
<p>
  For more information on where to find the SDK logs you can check the documentation
  <a href="/hc/en-us/articles/900000908046#h_01HABSX9KXC5S8Q1NQWDZ33HXC" target="blank">here</a>.
</p>
<h3 id="h_01HAVHW0RNY5T2XH6J8HYYJ2MF">Logger Delegate</h3>
<p>
  For receiving the Countly iOS SDK's internal logs even in production builds,
  you can set <code>loggerDelegate</code> property on the
  <code>CountlyConfig</code> object. If set, the Countly iOS SDK will forward its
  internal logs to this delegate object regardless of <code>enableDebug</code>
  initial config value.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.loggerDelegate = self; //or any other object to act as CountlyLoggerDelegate</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.loggerDelegate = self //or any other object to act as CountlyLoggerDelegate</code></pre>
  </div>
</div>
<p>
  <code>internalLog:</code> method declared as <code>required</code> in
  <code>CountlyLoggerDelegate</code> protocol will be called with log
  <code>NSString</code>.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">// CountlyLoggerDelegate protocol method
- (void)internalLog:(NSString *)log
{

}
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">// CountlyLoggerDelegate protocol method
func internalLog(_ log: String)
{

}
</code></pre>
  </div>
</div>
<h1 id="h_01HAVHW0RNQ5ESJGQW3FFQBDHV">Crash Reporting</h1>
<h2 id="h_01HAVHW0RNZJFE1FFPKJRCEFWA">Automatic Crash Handling</h2>
<p>
  <span style="font-weight: 400;">For Countly Crash Reporting, you'll need to specify <code>CLYCrashReporting</code> in <code>features</code></span><span style="font-weight: 400;"> array on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object before starting Countly.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.features = @[CLYCrashReporting];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.features = [CLYCrashReporting]</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">With this feature, the Countly iOS SDK will generate a crash report if your application crashes due to an exception and send it to the Countly Server for further inspection. If a crash report cannot be delivered to the server (e.g. no internet connection, unavailable server) at the time of the crash, the Countly iOS SDK will then store the crash report locally in order to make another attempt at a later time.</span>
</p>
<h2 id="h_01HAVHW0RNJ4KRJ6NY8GBXFN93">Handled Exceptions</h2>
<p>
  <span style="font-weight: 400;">The SDK provides functionality to manually report exceptions:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSException* myException = [NSException exceptionWithName:@"MyException" reason:@"MyReason" userInfo:@{@"key":@"value"}];

[Countly.sharedInstance recordException:myException];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let myException : NSException = NSException.init(name:NSExceptionName(rawValue: "MyException"), reason:"MyReason", userInfo:["key":"value"])

Countly.sharedInstance().recordException(myException)</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">By default, the reported exception will be marked as "fatal". Though you may want to override it and record a non fatal exception:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span><span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSException* myException = [NSException exceptionWithName:@"MyException" reason:@"MyReason" userInfo:@{@"key":@"value"}];

[Countly.sharedInstance recordException:myException isFatal:NO];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let myException : NSException = NSException.init(name:NSExceptionName(rawValue: "MyException"), reason:"MyReason", userInfo:["key":"value"])

Countly.sharedInstance().recordException(myException, isFatal: false)</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">There is also an extended call where you can pass the fatality information, stack trace and segmentation:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSException* myException = [NSException exceptionWithName:@"MyException" reason:@"MyReason" userInfo:@{@"key":@"value"}];
<br>NSDictionary* segmentation = @{@"country": @"Germany", @"app_version": @"1.0", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]};<br><br>[Countly.sharedInstance recordException:myException isFatal:YES stackTrace:[NSThread callStackSymbols] segmentation:segmentation];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let myException : NSException = NSException.init(name:NSExceptionName(rawValue: "MyException"), reason:"MyReason", userInfo:["key":"value"])
<br>let segmentation : Dictionary&lt;String, Any&gt; = ["country": "Germany", "app_version": "1.0", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]]<br>
Countly.sharedInstance().recordException(myException, isFatal: true, stackTrace: Thread.callStackSymbols, segmentation:segmentation)</code><code class="swift"></code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RNWF4H0MASN3MD1Y8S">Record Swift Error</h2>
<p>
  The SDK offers a call to
  <span style="font-weight: 400;">record swift errors:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span><span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre>[Countly.sharedInstance recordError:@"ERROR_NAME" stackTrace:[NSThread callStackSymbols]];</pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().recordError("ERROR_NAME", stackTrace: Thread.callStackSymbols)<br></code><code class="swift"></code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">There is also an extended version where you can pass fatality information, stack trace and segmentation:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span><span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSDictionary* segmentation = @{@"country":@"Germany", @"app_version":@"1.0", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]};<br><br>[Countly.sharedInstance recordError:@"ERROR_NAME" isFatal:YES stackTrace:[NSThread callStackSymbols] segmentation:segmentation];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let myException : NSException = NSException.init(name:NSExceptionName(rawValue: "MyException"), reason:"MyReason", userInfo:["key":"value"])
<br>let segmentation : Dictionary&lt;String, Any&gt; = ["country": "Germany", "app_version": "1.0", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]]<br>
Countly.sharedInstance().recordError("ERROR_NAME", isFatal: true, stackTrace: Thread.callStackSymbols, segmentation:segmentation)</code><code class="swift"></code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RNEA508VPZ6G800RDK">Crash Breadcrumbs</h2>
<p>
  <span style="font-weight: 400;">You can use the <code>recordCrashLog:</code></span>
  <span style="font-weight: 400;">method to receive custom logs with the crash reports. Logs generated by the <code>recordCrashLog:</code></span><span style="font-weight: 400;">method are stored in a non-persistent structure and are delivered to the Countly Server only for a crash.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance recordCrashLog:@"This is a custom crash log."];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().recordCrashLog("This is a custom crash log.")</code></pre>
  </div>
</div>
<p>
  There is a limit for the number of crash logs to be stored on the device. Have
  a look <a href="#h_01HAVHW0RSESJ7AQ3XCKCA48X2">here</a> to configure its limit.
</p>
<h2 id="h_01HAVHW0RN0T1600A6B514XSNM">Crash Report Contents</h2>
<p>A crash report includes the following information:</p>
<h3 id="h_01HAVHW0RNZTJTKQTDWYSRMD1R">Default Crash Report Information</h3>
<pre><code>- Exception Info:
  * Exception Name
  * Exception Description
  * Stack Trace
  * Binary Images

- Device Static Info:
  * Device Type
  * Device Architecture
  * Resolution
  * Total RAM
  * Total Disk

- Device Dynamic Info:
  * Used RAM
  * Used Disk
  * Battery Level
  * Connection Type
  * Device Orientation

- OS Info:
  * OS Name
  * OS Version
  * OpenGL ES Version
  * Jailbrake State

- App Info:
  * App Version
  * App Build Number
  * Executable Name
  * Time Since App Launch
  * Background State

- Custom Info:
  * Crash logs recorded using `recordCrashLog:` method
  * Crash segmentation specified in `crashSegmentation` property
</code></pre>
<h3 id="h_01HAVHW0RNYQWZB8DXQS8YH6C2">Custom Crash Segmentation</h3>
<p>
  <span style="font-weight: 400;">If you would like to use custom crash segmentation, you can set the optional <code>crashSegmentation</code></span>
  dictionary on the <code>CountlyConfig</code>
  <span style="font-weight: 400;">object.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.crashSegmentation = @{@"key": @"value", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]};</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.crashSegmentation = ["key": "value", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]]</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RNB7HWT8W9XRYRKBYZ">Crash Filtering</h2>
<p>
  There might be cases where a crash could contain sensitive information. For such
  situations, there is a crash filtering option that can discard or modify a crash.
</p>
<p>
  To filter a crash you should provide a callback to the config object using the
  <code class="objectivec">crashes.setCrashFilterCallback</code> method during
  initialization. This callback will be called every time a crash is recorded.
</p>
<p>
  The callback receives a <code>CountlyCrashData</code> object, which contains
  all the information about the crash that would be sent to the server:
</p>
<pre><code class="objectivec">@interface CountlyCrashData : NSObject

@property (nonatomic, copy, nonnull) NSString *stackTrace;
@property (nonatomic, copy, nonnull) NSString *name;
@property (nonatomic, copy, nonnull) NSString *crashDescription;
@property (nonatomic, assign) BOOL fatal;
@property (nonatomic, copy, nonnull) NSMutableArray&lt;NSString *&gt; *breadcrumbs;
@property (nonatomic, copy, nonnull) NSMutableDictionary&lt;NSString *, id&gt; *crashSegmentation;
@property (nonatomic, copy, nonnull) NSMutableDictionary&lt;NSString *, id&gt; *crashMetrics;

@end</code></pre>
<p>
  - <strong>stackTrace</strong>: Concatenated stack trace with new lines.
</p>
<p>
  - <strong>name</strong>: Reason of the crash. (used for grouping)
</p>
<p>
  - <strong>crashDescription</strong>: Dev provided name or captured description
  of the crash.
</p>
<p>
  - <strong>crashSegmentation</strong>: Combination of automatic crash report segmentation
  and segmentation given while recording the crash.
</p>
<p>
  - <strong>breadcrumbs</strong>: List of recorded breadcrumbs.
</p>
<p>
  - <strong>fatal</strong>: Indicates whether or not a crash is unhandled.
</p>
<p>
  - <strong>crashMetric</strong>: Crash related
  <a href="/hc/en-us/articles/9290669873305#h_01HJ5V4WX0XFP7FC8ETDC3B96M">metrics</a>
  recorded by the SDK.
</p>
<p>
  You can modify or filter the crash using the getter and setter methods provided
  by the CountlyCrashData. After modifying the crash, to send the crash to the
  server, you should return 'false.' If the callback returns 'true' the crash will
  be discarded:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objective">#import "Countly.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  CountlyConfig *config = CountlyConfig.new;
  config.appKey         = @"YOUR_APP_KEY";
  config.host           = @"https://YOUR_COUNTLY_SERVER";

  [config.crashes setCrashFilterCallback:^BOOL(CountlyCrashData *crash) {
    if (!crash)
    {
      return NO;
    }

    // You may want to omit a secret from the stack trace to protect it
    NSString *stackTrace = crash.stackTrace;
    stackTrace           = [stackTrace stringByReplacingOccurrencesOfString:@"secret" withString:@"*****"];
    crash.stackTrace     = stackTrace;

    // Or if crash segmentation contains a secret key, it can be omitted
    NSMutableDictionary *crashSegmentation = [crash.crashSegmentation mutableCopy];
    if (crashSegmentation[@"secret"])
    {
      // You can change if a crash is handled or not
      crash.fatal = NO;
      // The secret value could be overridden easily to protect it
      crashSegmentation[@"secret"] = @"*****";
    }
    crash.crashSegmentation = crashSegmentation;

    // Maybe when reporting crashes, only a device permitted to report the crashes for testing or debugging
    NSDictionary *crashMetrics = crash.crashMetrics;
    NSString     *device       = crashMetrics[@"_device"];
    if ([device isKindOfClass:[NSString class]])
    {
      // If metrics has a device other than an iOS, discard crash
      return ![device isEqualToString:@"iOS"];
    }
    else
    {
      // If value not found or not a string, discard the crash
      return YES;
    }
  }];

  [Countly.sharedInstance startWithConfig:config];

  return YES;
}</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">import Countly

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) - Bool
{
  let config: CountlyConfig = CountlyConfig()
  config.appKey = "YOUR_APP_KEY"
  config.host = "https://YOUR_COUNTLY_SERVER"
  
  let crashFilterBlock: (CountlyCrashData?) - Bool = { crash in
    guard let crash = crash else { 
      return false 
    }
   
    // You may want to omit a secret from the stack trace to protect it
    var stackTrace = crash.stackTrace 
    stackTrace = stackTrace.replacingOccurrences(of: "secret", with: "*****") 
    crash.stackTrace = stackTrace
  
    // or if crash segmentation contains a secret key, it can be omitted
    var crashSegmentation = crash.crashSegmentation 
    if crashSegmentation["secret"] != nil {
      // You can change if a crash is handled or not crash.fatal = false
      // The secret value could be overridden easily to protect it
      crashSegmentation["secret"] = "*****"
    }
  
    // Maybe when reporting crashes, only a device permitted to report the crashes for testing or debugging
    let crashMetrics = crash.crashMetrics
    if let device = crashMetrics["_device"] as? String {
      // if metrics has a device other than an iOS, discard crash
      return device != "iOS" 
    } else {
        // if value not found or not a string, discard the crash
        return true
    }
  }
  
  config.crashes().crashFilterCallback = crashFilterBlock
  Countly.sharedInstance().start(with: config)

  return true
}</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RNV95SB7MH171A9209">PLCrashReporter</h2>
<p>
  As an alternative to Countly iOS SDK's own exception and signal handling mechanism
  based on
  <span style="font-weight: 400;"><code>NSSetUncaughtExceptionHandler()</code></span>
  and <span style="font-weight: 400;"><code>signal()</code></span> functions, you
  can optionally use the more advanced
  <a href="https://github.com/microsoft/plcrashreporter" target="_self">PLCrashReporter</a>
  as well.
</p>
<p>
  For using PLCrashReporter instead of default crash handling mechanism you can
  set
  <span style="font-weight: 400;"><code>shouldUsePLCrashReporter</code> flag on the <code>CountlyConfig</code> object.</span>
</p>
<p>
  If set, Countly iOS SDK will be using PLCrashReporter dependency for creating
  crash reports.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.shouldUsePLCrashReporter = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.shouldUsePLCrashReporter = true</code><span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif; background-color: #ffffff;"> </span></pre>
  </div>
</div>
<p>
  And PLCrashReporter framework dependency should be added to your project manually
  from
  <a href="https://github.com/microsoft/plcrashreporter/releases" target="_self">its GitHub releases page</a>
  or via CocoaPods using <code>Countly-PL.podspec</code> instead of default
  <code>Countly.podspec</code>.
</p>
<p>
  Existence of PLCrashReporter dependency will be checked using
  <span style="font-weight: 400;"><code>__has_include(&lt;CrashReporter/CrashReporter.h&gt;)</code> preprocessor macro.</span>
</p>
<p>
  <strong>Note:</strong> <code>Countly-PL.podspec</code>automatically manages the
  PLCrashReporter dependencies. However, if you encounter an error related to PLCrashReporter
  when using CocoaPods, you can resolve it by adding the following to your Podfile:
</p>
<pre>post_install do |installer|<br> installer.pods_project.targets.each do |target|<br>  target.build_configurations.each do |config|<br>   if target.name == "Countly"<br>       config.build_settings['OTHER_LDFLAGS'] ||= ['$(inherited)']<br>       config.build_settings['OTHER_LDFLAGS'] &lt;&lt; '-framework "CrashReporter"'<br><br>       config.build_settings['LIBRARY_SEARCH_PATHS'] ||= ['$(inherited)']<br>       config.build_settings['LIBRARY_SEARCH_PATHS'] &lt;&lt; "${PODS_XCFRAMEWORKS_BUILD_DIR}/PLCrashReporter"<br>       config.build_settings['FRAMEWORK_SEARCH_PATHS'] ||= ['$(inherited)']<br>       config.build_settings['FRAMEWORK_SEARCH_PATHS'] &lt;&lt; "${PODS_XCFRAMEWORKS_BUILD_DIR}/PLCrashReporter"<br>     end<br>   end<br> end<br>end</pre>
<p>
  <strong>Note:</strong> PLCrashReporter option is available only for iOS apps.
</p>
<p>
  <strong>Note:</strong> Currently, tested and supported PLCrashReporter version
  is 1.5.1.
</p>
<h3 id="h_01HAVHW0RNMWF61PZDQ35BZ982">PLCrashReporter Signal Handler Type</h3>
<p>
  PLCrashReporter has two different signal handling implementations with different
  traits:
</p>
<p>
  1) BSD:
  <span style="font-weight: 400;"><code>PLCrashReporterSignalHandlerTypeBSD</code></span>
</p>
<p>
  2) Mach:
  <span style="font-weight: 400;"><code>PLCrashReporterSignalHandlerTypeMach</code></span>
</p>
<p>
  For more information about PLCrashReporter please see:
  <span>https://github.com/microsoft/plcrashreporter</span>
</p>
<p>
  By default, BSD type will be used. For using Mach type signal handler with PLCrashReporter
  you can set <code>shouldUseMachSignalHandler</code> flag on the
  <code>CountlyConfig</code> object.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.shouldUseMachSignalHandler = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.shouldUseMachSignalHandler = true</code><span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif; background-color: #ffffff;"> </span></pre>
  </div>
</div>
<h3 id="h_01HAVHW0RNRV22QBWVJ17MA4ZQ">PLCrashReporter Callback Blocks</h3>
<p>
  There is a
  <span style="font-weight: 400;"><code>crashOccuredOnPreviousSessionCallback</code></span>
  block to be executed when the app is launched again following a crash which is
  detected by PLCrashReporter on the previous session. It has an
  <span style="font-weight: 400;"><code>NSDictionary</code></span> parameter that
  represents crash report object. If<span> <span style="font-weight: 400;"><code>shouldUsePLCrashReporter</code></span></span>
  flag is not set on initial config, this block will never be executed. You can
  set it
  <span style="font-weight: 400;">on the <code>CountlyConfig</code> object:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.crashOccuredOnPreviousSessionCallback = ^(NSDictionary * crashReport)
{  
  NSLog(@"crash report: %@", crashReport);
};</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.crashOccuredOnPreviousSessionCallback =<br>{<br>  (crashReport: [AnyHashable: Any]) in print("crash report: \(crashReport)")<br>}</code></pre>
  </div>
</div>
<p>
  There is also another
  <span style="font-weight: 400;"><code>shouldSendCrashReportCallback</code></span>
  block to be executed to decide whether the crash report detected by PLCrashReporter
  on the previous session should be sent to Countly Server or not. If not set,
  crash report will be sent to Countly Server by default. If set, crash report
  will be sent to Countly Server only if
  <span style="font-weight: 400;"><code>YES</code></span> is returned. It has an
  <span style="font-weight: 400;"><code>NSDictionary</code></span> parameter that
  represents crash report object. If<span> <span style="font-weight: 400;"><code>shouldUsePLCrashReporter</code></span></span>
  flag is not set on initial config, this block will never be executed. You can
  set it
  <span style="font-weight: 400;">on the <code>CountlyConfig</code> object:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.shouldSendCrashReportCallback = ^(NSDictionary * crashReport)
{                                                                                                                              NSLog(@"crash report: %@", crashReport);
  return YES;    //NO;
};</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.shouldSendCrashReportCallback =<br>{<br>  (crashReport: [AnyHashable: Any]) in print("crash report: \(crashReport)")<br>  return true    //false<br>}</code><span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif; background-color: #ffffff;"> </span></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RN851W5J4BQX3FN938">Symbolication</h2>
<div class="callout callout--info">
  <strong>Enterprise Edition Feature</strong>
  <p>
    This feature is only available with an
    <a href="https://countly.com/enterprise">Enterprise Edition</a> and built-in
    <a href="https://countly.com/flex">Flex</a>.
  </p>
</div>
<p>
  <span style="font-weight: 400;">Symbolication is the process of converting stack trace memory addresses in crash reports into human-readable, useful information, such as class/method names, file names, and line numbers.</span>
</p>
<p>
  In order to symbolicate memory addresses, the dSYM files for each build need
  to be uploaded to the Countly Server.
</p>
<h3 id="h_01HAVHW0RPA8NXVET4EVGWDFNQ">Automatic dSYM Uploading</h3>
<p>
  <span style="font-weight: 400;">For Automatic dSYM Uploading, you can use the <code>countly_dsym_uploader</code></span><span style="font-weight: 400;"> script in the Countly iOS SDK.</span>
</p>
<p>
  To do so, go to the <code>Build Phases</code>
  <span style="font-weight: 400;">section of your app target and click on the plus ( + ) icon on the top left, then choose</span>
  <code>New Run Script Phase</code>from the list.
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/6dcebf7-Screen_Shot_2017-09-11_at_12.23.12.png">
</div>
<p>Then, add the following snippet:</p>
<pre><code class="shell">COUNTLY_DSYM_UPLOADER=$(/usr/bin/find $SRCROOT -name "countly_dsym_uploader.sh" | head -n 1)
sh "$COUNTLY_DSYM_UPLOADER" "https://YOUR_COUNTLY_SERVER" "YOUR_APP_KEY"</code></pre>
<p>
  Starting from <strong>Xcode 15</strong> you would need to add an
  <code>Input Files</code> entry to the <code>Run Script</code> section like this:
</p>
<pre><span>${DWARF_DSYM_FOLDER_PATH}/${DWARF_DSYM_FILE_NAME}/Contents/Resources/DWARF/${PRODUCT_NAME}</span></pre>
<p>
  <span>This will make sure the symbolication folder is usable for the script.</span>
</p>
<p>
  <span style="font-weight: 400;">Next, select the checkbox</span><code>Run script only when installing</code>.
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/2e1174c-db851a5-Screen_Shot_2017-09-11_at_12.31.14.png">
</div>
<p>
  <strong>Note:</strong> Do not forget to replace your server and app key.
</p>
<p>
  <span style="font-weight: 400;">By default, Xcode will generate dSYM files for the Release build configuration, and the <code>countly_dsym_uploader</code></span><span style="font-weight: 400;"> script will handle the uploading automatically. You can check for the results on the Report Navigator within Xcode. If the dSYM upload has completed successfully, you will see the<code>[Countly] dSYM upload successfully completed.</code></span><span style="font-weight: 400;">message.</span>
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/4ac2acd-update-img.png">
</div>
<p>
  <span style="font-weight: 400;">If there are any errors while uploading the dSYM file, you can see these error messages in the Report Navigator. Some of the possible error reasons include: the dSYM file not being created due to build configurations, the dSYM file being created at a non-default location, wrong App ID and/or Countly Server address, or network unavailability.</span>
</p>
<h3 id="h_01HAVHW0RP2HVF94RFG0TJY063">Manual dSYM Uploading</h3>
<p>
  <span style="font-weight: 400;">In case of an error with Automatic dSYM Uploading, or if you would like to upload your dSYM files manually, you can use our guide for Manual dSYM Uploading </span><a href="/hc/en-us/articles/360037261472#h_01HBP9RH2Q5M0YMR2YS4QVVRK8"><span style="font-weight: 400;">here</span></a><span style="font-weight: 400;">. You will also need to use Manual dSYM Uploading if Bitcode is enabled while uploading your app to App Store Connect.</span>
</p>
<h3 id="h_01HAVHW0RPB0WB207T16B54NGP">Bitcode Enabled Apps</h3>
<p>
  <span style="font-weight: 400;">If Bitcode is enabled in your project while uploading your app to App Store Connect, Apple re-compiles your app to optimize it for specific devices. When Apple re-compiles your app, a new dSYM file is generated for the new build, and the dSYM file on your machine will not work for symbolication. So, you will need to receive this new dSYM file manually, then upload it to the Countly Server. In order to get the new dSYM file, you can use App Store Connect or Xcode Organizer.</span>
</p>
<p>
  <span style="font-weight: 400;">Using App Store Connect: 1. Login to <code>App Store Connect</code></span><span style="font-weight: 400;">. 2. Go to the <code>Activity</code></span><span style="font-weight: 400;">tab. 3. Select your app's <code>Version</code> and <code>Build</code></span><span style="font-weight: 400;"> 4. Under <code>General Information</code> click on <code>Download dSYM</code></span><span style="font-weight: 400;">. 5. If the downloaded file does not have any extension, add <code>.zip</code></span><span style="font-weight: 400;"> and unarchive to see its content.</span>
</p>
<p>
  <span style="font-weight: 400;">Using Xcode: 1. Open <code>Organizer</code></span><span style="font-weight: 400;"> in Xcode. 2. Go to the <code>Archives</code></span><span style="font-weight: 400;"> tab. 3. Select your app from the list on the left and select the archive. 4. Click on <code>Download dSYMs...</code>.</span><span style="font-weight: 400;"> 5. Xcode inserts the downloaded .dSYM files into the selected archive.</span>
</p>
<p>
  <span style="font-weight: 400;">For more information regarding downloading dSYM files from Apple, please see Apple's documentation </span><a href="https://help.apple.com/xcode/mac/current/#/devef5928039"><span style="font-weight: 400;">here</span></a><span style="font-weight: 400;">.</span>
</p>
<p>
  <span style="font-weight: 400;">After you receive your dSYM file from Apple, you can use our Manual dSYM Uploading </span><a href="/hc/en-us/articles/360037261472#h_01HBP9RH2Q5M0YMR2YS4QVVRK8"><span style="font-weight: 400;">guide</span></a><span style="font-weight: 400;">.</span>
</p>
<h3 id="h_01HAVHW0RPGRH26TX797Y456S7">How to Use Symbolication</h3>
<p>
  <span style="font-weight: 400;">Once your dSYM file has been uploaded to the Countly Server, you can symbolicate your crash reports coming from that build on the <code>Crashes</code></span><span style="font-weight: 400;">panel of your Countly Server.</span>
</p>
<p>
  <span style="font-weight: 400;">A crash report symbolicated stack trace appears as follows:</span>
</p>
<p>Before symbolication:</p>
<pre><code>YourAppName                               0x000000010006e174 YourAppName + 156020
YourAppName                               0x000000010006d060 YourAppName + 151648
YourAppName                               0x000000010006ad34 YourAppName + 142644
</code></pre>
<p>After symbolication:</p>
<pre><code>-[MHViewController countlyProductionTest] (in YourAppName) (MHViewController.m:620)
-[MHViewController transitionToMahya] (in YourAppName) (MHViewController.m:443)
-[MHViewController textFieldShouldReturn:] (in YourAppName) (MHViewController.m:210)</code></pre>
<p>
  <span style="font-weight: 400;">For more information about how to use the Symbolication feature on the Countly Server, please see our Symbolication documentation </span><a href="/hc/en-us/articles/360037261472"><span style="font-weight: 400;">here</span></a><span style="font-weight: 400;">.</span>
</p>
<h1 id="h_01HAVHW0RP28BREFV5E1HC97DM">Events</h1>
<p>
  <span style="font-weight: 400;">Here is a quick summary on how to use event recording methods:</span>
</p>
<h2 id="h_01HAVHW0RPGPE3GSB8PH88CNAC">Recording Events</h2>
<p>
  <span style="font-weight: 400;">We have recorded an event named </span><strong>purchase</strong><span style="font-weight: 400;"> with different scenarios in the examples below:</span>
</p>
<ul>
  <li>
    <strong>purchase</strong> event occurred <strong>1</strong> time
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance recordEvent:@"purchase"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().recordEvent("purchase")</code></pre>
  </div>
</div>
<ul>
  <li>
    <strong>purchase</strong> event occurred <strong>3</strong> times
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance recordEvent:@"purchase" count:3];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().recordEvent("purchase", count:3)</code></pre>
  </div>
</div>
<ul>
  <li>
    <strong>purchase</strong> event occurred <strong>1</strong> times with the
    total amount of <strong>3.33</strong>
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance recordEvent:@"purchase" sum:3.33];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().recordEvent("purchase", sum:3.33)</code></pre>
  </div>
</div>
<ul>
  <li>
    <strong>purchase</strong> event occurred <strong>3</strong> times with the
    total amount of <strong>9.99</strong>
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance recordEvent:@"purchase" count:3 sum:9.99];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().recordEvent("purchase", count:3, sum:3.33)</code></pre>
  </div>
</div>
<ul>
  <li>
    <strong>purchase</strong> event occurred <strong>1</strong> time from
    <strong>country</strong> : <strong>Germany</strong>, on
    <strong>app_version</strong> : <strong>1.0</strong>
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSDictionary* dict = @{@"country":@"Germany", @"app_version":@"1.0", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]};

[Countly.sharedInstance recordEvent:@"purchase" segmentation:dict];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let dict : Dictionary&lt;String, Any&gt; = ["country":"Germany", "app_version":"1.0", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]]

Countly.sharedInstance().recordEvent("purchase", segmentation:dict)</code></pre>
  </div>
</div>
<ul>
  <li>
    <strong>purchase</strong> event occurred <strong>2</strong> times from
    <strong>country</strong> : <strong>Germany</strong>, on
    <strong>app_version</strong> : <strong>1.0</strong>
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSDictionary* dict = @{@"country": @"Germany", @"app_version": @"1.0", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]};

[Countly.sharedInstance recordEvent:@"purchase" segmentation:dict count:2];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let dict : Dictionary&lt;String, Any&gt; = ["country": "Germany", "app_version": "1.0", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]]

Countly.sharedInstance().recordEvent("purchase", segmentation:dict, count:2)</code></pre>
  </div>
</div>
<ul>
  <li>
    <strong>purchase</strong> event occurred <strong>2</strong> times with the
    total amount of <strong>6.66</strong>, from <strong>country</strong>:
    <strong>Germany</strong>, on <strong>app_version</strong> :
    <strong>1.0</strong>
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSDictionary* dict = @{@"country": @"Germany", @"app_version": @"1.0", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]};

[Countly.sharedInstance recordEvent:@"purchase" segmentation:dict count:2 sum:6.66];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let dict : Dictionary&lt;String, Any&gt; = ["country": "Germany", "app_version": "1.0", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]]

Countly.sharedInstance().recordEvent("purchase", segmentation:dict, count:2, sum:6.66)</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RP1HTEJMH0MDBHSE5J">Timed Events</h2>
<p>
  <span style="font-weight: 400;">In the examples below, we recorded a timed event called </span><strong>level24</strong><span style="font-weight: 400;"> to track how long it takes to complete:</span>
</p>
<ul>
  <li>
    <strong>level24</strong> started
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance startEvent:@"level24"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().startEvent("level24")</code></pre>
  </div>
</div>
<ul>
  <li>
    <strong>level24</strong> ended
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance endEvent:@"level24"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().endEvent("level24")</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Additionally, you can provide more information, such as the segmentation, count, and sum while ending an event.</span>
</p>
<ul>
  <li>
    <strong>level24</strong> ended <em>1</em> time with the total point of
    <strong>34578</strong>, from <strong>country</strong> :
    <strong>Germany</strong>, on <strong>app_version</strong> :
    <strong>1.0</strong>
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSDictionary* dict = @{@"country": @"Germany", @"app_version": @"1.0", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]};

[Countly.sharedInstance endEvent:@"level24" segmentation:dict count:1 sum:34578];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let dict : Dictionary&lt;String, Any&gt; = ["country": "Germany", "app_version": "1.0", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]]

Countly.sharedInstance().endEvent("level24", segmentation:dict, count:1, sum:34578)</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">The duration of the event will be calculated automatically when the <code>endEvent</code></span><span style="font-weight: 400;"> method is called.</span>
</p>
<p>
  You can also cancel a started timed event using <code>cancelEvent</code> method:
</p>
<div class="tabs-menu">
  <span class="tabs-link is-active">Objective-C</span>
  <span class="tabs-link">Swift</span>
</div>
<div class="tabs">
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance cancelEvent:@"level24"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().cancelEvent("level24")</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Or, if you are measuring the duration of an event yourself, you can record it directly as follows:</span>
</p>
<ul>
  <li>
    <strong>level24</strong> took 344 seconds to complete:
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance recordEvent:@"level24" duration:344];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().recordEvent("level24", duration:344)</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Additionally, you can provide more information such as the segmentation, count, and sum.</span>
</p>
<ul>
  <li>
    <strong>level24</strong> took 344 seconds to complete <strong>2</strong>
    times with the total point of <strong>34578</strong>, from
    <strong>country</strong> : <strong>Germany</strong>, on
    <strong>app_version</strong> : <strong>1.0</strong>
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSDictionary* dict = @{@"country": @"Germany", @"app_version": @"1.0", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]};

[Countly.sharedInstance recordEvent:@"level24" segmentation:dict count:2 sum:34578 duration:344];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let dict : Dictionary&lt;String, Any&gt; = ["country": "Germany", "app_version": "1.0", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]]

Countly.sharedInstance().recordEvent("level24", segmentation:dict, count:2, sum:34578, duration:344)</code></pre>
  </div>
</div>
<div class="callout callout--warning">
  <strong>Event Names and Segmentation</strong>
  <p>
    Event names must be non-zero length valid <code>NSString</code> and segmentation
    must be an <code>NSDictionary</code> which
    <strong>does not contain any custom objects</strong>, as it will be converted
    to JSON.
  </p>
</div>
<h1 id="h_01HAVHW0RPNX1XDJN28R04FAW0">Sessions</h1>
<h2 id="h_01HAVHW0RP9NFD6V5758067CSF">Automatic Session Tracking</h2>
<p>
  <span style="font-weight: 400;">By default, the Countly iOS SDK tracks sessions automatically and sends the <code>begin_session</code></span><span style="font-weight: 400;">request upon initialization, the <code>end_session</code></span><span style="font-weight: 400;"> request when the app goes to the background, and the <code>begin_session</code></span><span style="font-weight: 400;"> request again when the app comes back to the foreground. In addition, the Countly iOS SDK automatically sends a periodical (60 sec by default) update session request while the app is in the foreground.</span>
</p>
<h2 id="h_01HAVHW0RP6004R2GGN304V36H">Manual Sessions</h2>
<p>
  <span style="font-weight: 400;">You can set the <code>manualSessionHandling</code></span><span style="font-weight: 400;"> flag on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object before starting Countly to handle sessions manually.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.manualSessionHandling = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.manualSessionHandling = true</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">If the <code>manualSessionHandling</code></span><span style="font-weight: 400;"> flag is set, the Countly iOS SDK does not send the previously mentioned requests automatically, meaning you will need to manually call the <code>beginSession</code></span><span style="font-weight: 400;">, <code>updateSession</code> and <code>endSession</code></span><span style="font-weight: 400;"> methods after you start Countly, depending on your own definition of a session.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance beginSession];
[Countly.sharedInstance updateSession];
[Countly.sharedInstance endSession];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().beginSession()
Countly.sharedInstance().updateSession()
Countly.sharedInstance().endSession()</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RP7ZXRMQ1Z8BVETVM6">Update Session Period</h2>
<p>
  <span style="font-weight: 400;">You can specify the <code>updateSessionPeriod</code></span><span style="font-weight: 400;"> on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object before starting Countly. It is used for session updating and periodically sending queued events to the server. If the <code>updateSessionPeriod</code></span><span style="font-weight: 400;"> is not explicitly set, the default setting will be at </span><strong>60 seconds</strong><span style="font-weight: 400;"> for iOS, tvOS &amp; macOS, and </span><strong>20 seconds</strong><span style="font-weight: 400;"> for watchOS.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.updateSessionPeriod = 300;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.updateSessionPeriod = 300</code></pre>
  </div>
</div>
<h1 id="h_01HAVHW0RPKXBCWY438V198Q6A">View Tracking</h1>
<h2 id="h_01HAVHW0RP2Z0AZS62NM78RMHH">Automatic Views</h2>
<p>
  <span style="font-weight: 400;">To enable automatic view tracking, you will need to </span><span style="font-weight: 400;">set the <code>enableAutomaticViewTracking</code></span><span style="font-weight: 400;"> flag on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object before starting Countly.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.enableAutomaticViewTracking = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.enableAutomaticViewTracking = true</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">After this step, the Countly iOS SDK will automatically track views by simply intercepting the <code>viewDidAppear:</code></span><span style="font-weight: 400;"> method of the <code>UIViewController</code></span><span style="font-weight: 400;">class and reporting which view is displayed with the view name and duration. If the view controller's <code>title</code></span><span style="font-weight: 400;"> property is set, it would be reported as the view name</span><span style="font-weight: 400;">. Otherwise, the view name will be the view controller's class name.</span>
</p>
<h3 id="h_01HAVHW0RPV53JK8JRKCCWRH3Q">Automatic View Exceptions</h3>
<h4 id="h_01HAVHW0RP6JNX0Y3PV09EPE1G">Default Exceptions for Automatic View Tracking</h4>
<p>
  <span style="font-weight: 400;">Following system view controllers will be excluded by default from automatic view tracking, as they are not visible to the user but rather structural controllers:</span>
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
<h4 id="h_01HAVHW0RPGY5061NGG4PNY0N8">Custom Exceptions for Automatic View Tracking</h4>
<p>
  <span style="font-weight: 400;">In addition to these default exceptions, you can manually set an exclusion list of the view controllers you don't want to track by using the <code>automaticViewTrackingExclusionList</code> array on the <code>CountlyConfig</code> object before starting Countly</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.automaticViewTrackingExclusionList = @[NSStringFromClass(MyViewController.class), @"MyViewControllerName"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="objectivec">config.automaticViewTrackingExclusionList = [NSStringFromClass(MyViewController.class), "MyViewControllerName"];</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">View controller class names or titles from this list will be ignored by automatic view tracking and their appearances will not be reported. Adding an already excluded view controller class name or title a second time will have no effect.</span>
</p>
<h4 id="h_01HAVHW0RPH12WWV3P3X6N8WKS">Customizing Auto View Tracking View Names</h4>
<p>
  You can utilize <code>CountlyAutoViewTrackingName</code> protocol to customize
  view names used by Auto View Tracking.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">//Make your view controller to conform CountlyAutoViewTrackingName protocol.
@interface MyViewController : UIViewController @end 
//and implement countlyAutoViewTrackingName method to return custom view name to be used by Auto View Tracking.
- (NSString *)countlyAutoViewTrackingName { return @"This is overridden custom view name"; }</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">//Make your view controller to conform CountlyAutoViewTrackingName protocol. 
class MyViewController: UIViewController, CountlyAutoViewTrackingName 
//and implement countlyAutoViewTrackingName function to return custom view name to be used by Auto View Tracking.
func countlyAutoViewTrackingName() -&gt; String { return "This is overridden custom view name" }</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RPC3YZRVR3TADBQ0QF">Manual View Recording</h2>
<div class="callout callout--warning">
  <p>
    Please be aware that if auto view tracking is enabled, manual view tracking
    will not be taken into account.
  </p>
</div>
<p>
  If you want to have full control over your view tracking you can use manual view
  recording methods.
</p>
<h3 id="h_01HFDVX9G293G57VFBANCB4GN6">Auto Stopped Views</h3>
<p>
  <span style="font-weight: 400;">A view initiated with auto stopped view method is designed to be automatically stopped when this method is called again. You should use <code>startAutoStoppedView:</code></span><span style="font-weight: 400;">method with a view name. This method begins tracking a view and returns a unique identifier.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.views startAutoStoppedView:@"MyView"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().views.startAutoStoppedView("MyView")</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">You can also specify the custom segmentation key-value pairs while starting views:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.views startAutoStoppedView:@"MyView" segmentation:@{@"key": @"value", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().views.startAutoStoppedView("MyView", segmentation: ["key": "value", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]])</code></pre>
  </div>
</div>
<h3 id="h_01HFDVXW74N8XR9TXQA8K7K3F8">Regular Views</h3>
<p>
  Opposed to "auto stopped views", with regular views you can have multiple of
  them started at the same time, and then you can control them independently. You
  can manually start a view using the <code>startView:</code><span style="font-weight: 400;">method with a view name. This will <span>start tracking a view and return a unique identifier</span>, and the view will remain active until explicitly stopped using <code>stopViewWithName:</code> or <code>stopViewWithID:</code> </span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.views startView:@"MyView"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().views.startView("MyView")</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">You can also specify the custom segmentation key-value pairs while starting views:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.views startView:@"MyView" segmentation:@{@"key": @"value", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().views.startView("MyView", segmentation: ["key": "value", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]])</code></pre>
  </div>
</div>
<h3 id="h_01HFDVY8YAXBP812A870NAZ6Q2">Stopping Views</h3>
<p>
  If there are multiple views with the same name (they would have different identifiers)
  but if you try to stop one with that name the SDK would close one of those randomly.
</p>
<p>
  You can stop view tracking by its name using
  <span style="font-weight: 400;"><code>stopViewWithName:</code></span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.views stopViewWithName:@"MyView"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().views.stopViewWithName("MyView")</code></pre>
  </div>
</div>
<p>
  This function allows you to manually stop the tracking of a view identified by
  its name.<span style="font-weight: 400;"><br>You can also specify the custom segmentation key-value pairs while stopping views:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.views stopViewWithName:@"MyView" segmentation:@{@"key": @"value", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().views.stopViewWithName("MyView", segmentation: ["key": "value", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]])</code></pre>
  </div>
</div>
<p>
  You can also stop view tracking by its unique idetifier using
  <span style="font-weight: 400;"><code>stopViewWithID:</code></span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.views stopViewWithID:@"VIEW_ID"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().views.stopViewWithID("VIEW_ID")</code></pre>
  </div>
</div>
<p>
  This function allows you to manually stop the tracking of a view identified by
  its <span>unique identifier.</span><br>
  <span style="font-weight: 400;">You can also specify the custom segmentation key-value pairs while stopping views:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.views stopViewWithID:@"VIEW_ID" segmentation:@{@"key": @"value", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().views.stopViewWithID("VIEW_ID", segmentation: ["key": "value", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]])</code></pre>
  </div>
</div>
<p>
  You can stop all views tracking using
  <span style="font-weight: 400;"><code>stopAllViews:</code></span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.views stopAllViews:@{@"key": @"value"}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().views.stopAllViews(["key": "value"])</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;"><span>This function stops the tracking of all views.</span><br></span>
</p>
<h3 id="h_01HFDVYJHTJKNHSYQAVYRRPPJE">Pausing and Resuming Views</h3>
<p>
  <span style="font-weight: 400;"></span>The iOS SDK allows you to start multiple
  views at the same time. If you are starting multiple views at the same time it
  might be necessary for you to pause some views while others are still continuing.
  This can be achieved by using the unique identifier you get while starting a
  view.
</p>
<p>
  You can pause view tracking by its unique identifier using
  <span style="font-weight: 400;"><code>pauseViewWithID:</code></span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.views pauseViewWithID:@"VIEW_ID"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().views.pauseViewWithID("VIEW_ID")</code></pre>
  </div>
</div>
<p>
  <span>This function temporarily pauses the tracking of a view identified by its unique identifier.</span>
</p>
<p>
  You can resume view tracking by its unique identifier using<span style="font-weight: 400;"> <code>resumeViewWithID:</code></span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.views resumeViewWithID:@"VIEW_ID"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().views.resumeViewWithID("VIEW_ID")</code></pre>
  </div>
</div>
<p>
  This function resumes the tracking of a previously paused view identified by
  its unique identifier.
</p>
<h3 id="h_01HHPQ3RAKXJ5SSV6S4KZGPSXJ">
  <span>Adding Segmentation to Started Views</span><span></span>
</h3>
<p>
  <span><span style="font-weight: 400;">You can also add segmentation to already started views using view name or view ID:<br></span></span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSString * viewID = [Countly.sharedInstance.views startView:@"VIEW_NAME"];
[Countly.sharedInstance.views addSegmentationToViewWithID:viewID segmentation:@{@"key": @"value", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]}];
      
[Countly.sharedInstance.views addSegmentationToViewWithName:@"VIEW_NAME" segmentation:@{@"key": @"value", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let viewID = Countly.sharedInstance().views().startView("MyView");
Countly.sharedInstance().views().addSegmentationToViewWithID(withID: viewID, segmentation: ["key": "value", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]])
      
Countly.sharedInstance().views().addSegmentationToViewWithName(withName: "MyView", segmentation: ["key": "value", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]])</code></pre>
  </div>
</div>
<h2 id="h_01HFDVW0B9P67GT7PWD4EB1J1A">Global View Segmentation</h2>
<p>
  You can set global segmentation for views by using<span style="font-weight: 400;"> <code>setGlobalViewSegmentation:</code></span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.views setGlobalViewSegmentation:@{@"key": @"value"}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().views.setGlobalViewSegmentation(["key": "value"])</code></pre>
  </div>
</div>
<p>
  You can also update global segmentation values for views by using<span style="font-weight: 400;"> <code>updateGlobalViewSegmentation:</code></span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.views updateGlobalViewSegmentation:@{@"key": @"value", @"arrayKey": @[@"one", @2, @3.14], @"int": @5, @"bool": @YES, @"double": @3.14, @"intArr": @[@4, @5, @6]}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().views.updateGlobalViewSegmentation(["key": "value", "arrayKey": ["one", 2, 3.14], "int": 5, "bool": true, "double": 3.14, "intArr": [4, 5, 6]])</code></pre>
  </div>
</div>
<h1 id="h_01HAVHW0RPRWDT82DVYT4ABT9V">Device ID Management</h1>
<p>
  <span style="font-weight: 400;">It is a persistently stored random <code>NSUUID</code></span><span style="font-weight: 400;"> string.</span>
</p>
<p>
  <span style="font-weight: 400;">If you would like to use a custom device ID, you can set the <code>deviceID</code></span><span style="font-weight: 400;"> property on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object. If the <code>deviceID</code></span><span style="font-weight: 400;"> property is not set explicitly, a </span>default
  device ID<span style="font-weight: 400;"> will be used depending on the platform.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.deviceID = @"customDeviceID";  //Optional custom device ID</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.deviceID = "customDeviceID"  //Optional custom device ID</code></pre>
  </div>
</div>
<p>
  <strong>Note:</strong>
  <span style="font-weight: 400;">Once set, the device ID will be persistently stored on the device after the first app launch, and the <code>deviceID</code></span><span style="font-weight: 400;"> property will be ignored on the following app launches, until the app is deleted and re-installed or a <code>resetStoredDeviceID</code></span><span style="font-weight: 400;"> flag is set. For further details, please check the </span><a href="/hc/en-us/articles/4409195031577#h_01HAVHW0RPQ7A17R8H6RZCMWXP">Resetting Stored Device ID</a><span style="font-weight: 400;"> section below.</span>
</p>
<h2 id="h_01HAVHW0RP2DPTREKXC0Q8T6QA">Changing Device ID</h2>
<div class="callout callout--warning">
  <p>
    If you need a more complicated logic or using the SDK version 24.7.0 and
    below then you will need to use this method mentioned
    <a href="#h_01JCGJ63WGHR3V9XZQT89JVYFQ">here</a>
  </p>
</div>
<p>
  <span style="font-weight: 400;">You can change the device ID on runtime <strong>after you start Countly</strong>. You can either allow the device to be counted as a new device or merge existing data on the server.<br><br>To set a new device ID based on the current device ID type, use the <code>setID:</code> method. If the current device ID type is <code>CLYDeviceIDTypeCustom</code>, it will be counted as a new device; otherwise, it will merge existing data on the server. With <code>setID:</code>, the SDK will automatically handle whether to merge the device ID or not.<br></span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">//Automatically handle whether to merge the device ID or not.
[Countly.sharedInstance setID:@"new_device_id"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">//Automatically handle whether to merge the device ID or not.<br>Countly.sharedInstance().setID("new_device_id")</code></pre>
  </div>
</div>
<div class="callout callout--warning">
  <strong>Consent Reset on Device ID Change</strong>
  <p>
    <span style="font-weight: 400;">If device ID is changed again from a developer provided ID and <code>requiresConsent</code> flag was enabled, all previously given consents will be removed. This means that all features will cease to function until new consent has been given again for the new device ID.</span>
  </p>
</div>
<h2 id="h_01HAVHW0RPA7ADFJ2Y97HNPPH5">Temporary Device ID</h2>
<div class="callout callout--warning">
  <p>
    If you need a more complicated logic or using the SDK version 24.7.0 and
    below then you will need to use this method mentioned
    <a href="#h_01JCGJD8TNSSNPV5DTYXEEFZX5">here</a>
  </p>
</div>
<p>
  You can use temporary device ID mode for keeping all requests on hold until the
  real device ID is set later. You can enable it by calling
  <code>enableTemporaryDeviceIDMode</code> on initial configuration:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[config enableTemporaryDeviceIDMode];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.enableTemporaryDeviceIDMode();</code></pre>
  </div>
</div>
<p>
  Or by calling<code>enableTemporaryDeviceIDMode</code>any time:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance enableTemporaryDeviceIDMode];<br></code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().enableTemporaryDeviceIDMode()</code></pre>
  </div>
</div>
<p>
  As long as the SDK is in temporary device ID mode, all requests will be on hold
  but they will be persistently stored.
</p>
<p>
  When in temporary device ID mode, method calls for presenting feedback widgets
  and updating remote config will be ignored.
</p>
<p>
  Later, when the real device ID is set using
  <span style="font-weight: 400;"> <code>setID:</code></span> method, all requests
  which have been kept on hold until that point will start with the real device
  ID:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance setID:@"new_device_id"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().setID("new_device_id")</code></pre>
  </div>
</div>
<div class="callout callout--warning">
  <strong>Consent Reset on Temporary Device ID Mode</strong>
  <p>
    <span style="font-weight: 400;">If the SDK goes into Temporary Device ID mode and <code>requiresConsent</code> flag was enabled, all previously given consents will be removed. Therefore after entering the Temporary Device ID mode, you should reestablish consent again.</span>
  </p>
</div>
<h2 id="h_01HAVHW0RP65R779Y3869HFTND">Retrieving Current Device ID</h2>
<p>
  You can use <code>deviceID</code>method to get current device ID:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance deviceID];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().deviceID()</code></pre>
  </div>
</div>
<p>
  It can be used for handling data export and/or removal requests as part of your
  app's data privacy compliance.
</p>
<p>
  You can use <code>deviceIDType</code> method which returns a
  <code>CLYDeviceIDType</code> to get current device ID type:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance deviceIDType];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().deviceIDType()</code></pre>
  </div>
</div>
<p>
  Device ID type can be one of the following:<br>
  <code>CLYDeviceIDTypeCustom</code> : Custom device ID set by app developer.<br>
  <code>CLYDeviceIDTypeTemporary</code> : Temporary device ID.<br>
  <code>CLYDeviceIDTypeIDFV</code> : Default device ID type used by the SDK on
  iOS and tvOS.<br>
  <code>CLYDeviceIDTypeNSUUID</code> : Default device ID type used by the SDK on
  watchOS and macOS.
</p>
<h2 id="h_01HAVHW0RPQ7A17R8H6RZCMWXP">Resetting Stored Device ID</h2>
<p>
  <span style="font-weight: 400;">In order to handle device ID changes for logged-in and logged-out users, the device ID specified in the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object of the <code>deviceID</code></span><span style="font-weight: 400;"> property (or the default device ID, if not specified) will be persistently stored as well as the device ID passed to the <code>changeDeviceIDWithMerge:</code> or <code>changeDeviceIDWithoutMerge:</code> </span><span style="font-weight: 400;">method at any time upon the first app launch. By this point, until you delete and re-install the app, the Countly iOS SDK will continue to use the stored device ID and ignore the <code>deviceID</code></span><span style="font-weight: 400;"> property. So, if you set the <code>deviceID</code></span><span style="font-weight: 400;"> property to something different upon future app launches during development, it will have no effect. In this case, you can set the <code>resetStoredDeviceID</code></span><span style="font-weight: 400;"> flag on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object in order to reset the stored device ID. This will reset the initially stored device ID and the Countly iOS SDK will work as if it is the first app launch.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.resetStoredDeviceID = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.resetStoredDeviceID = true</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">After you start Countly once with the <code>resetStoredDeviceID</code></span><span style="font-weight: 400;"> flag while developing, you can remove that line. The <code>resetStoredDeviceID</code></span><span style="font-weight: 400;"> flag is not meant for production. It is only for debugging purposes while performing development and not being able to delete and re-install the app.</span>
</p>
<h1 id="h_01HAVHW0RQD3WBN560GAKTB77T">Push Notifications</h1>
<p>
  Countly gives you the ability to send Push Notifications to your users using
  your app with the iOS SDK integration. For more information on how to best use
  this feature you can check
  <a href="/hc/en-us/articles/4405405459225" target="_blank" rel="noopener noreferrer">this</a>
  article.
</p>
<p>
  To make this feature work you will need to make some configurations both in your
  app and at your Countly server.
</p>
<p>
  <strong><span style="font-weight: 400;">First, you will need to acquire Push Notification credentials from Apple. (If you don't have them you can check <a href="/hc/en-us/articles/360037753511#h_01HNF5NPFR0W8WJ1BW8WVXJ5AB">this</a> article to learn how you can do it.)</span></strong>
</p>
<p>
  <span style="font-weight: 400;">Then you would need to upload these credentials&nbsp;to your Countly server. You can refer to <a href="/hc/en-us/articles/360037753511#h_01HNF5QRPJGG0GKMMH2SZWVK85">this</a> article for learning how you can do that.</span>
</p>
<p>
  <span style="font-weight: 400;">Lastly you will need to integrate and enable the feature in your SDK as explained below.</span>
</p>
<h2 id="h_01HAVHW0RQCDBB56915BMJTP5H">Integration</h2>
<p>
  <span style="font-weight: 400;">Using Countly Push Notifications on iOS apps is pretty straightforward. First, integrate the Countly iOS SDK as usual, if you still have yet to do so.</span>
</p>
<p>
  <span style="font-weight: 400;">Then, under the </span><strong>Capabilities</strong><span style="font-weight: 400;"> section of Xcode, enable </span><strong>Push Notifications</strong><span style="font-weight: 400;"> and the </span><strong>Remote notifications Background Mode</strong><span style="font-weight: 400;"> for your target, as shown in the screenshot below:</span>
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/0359527-push_xcode.png">
</div>
<h2 id="h_01HAVHW0RQSFQYGK10F4REYQNG">Enabling Push</h2>
<p>
  <span style="font-weight: 400;">Now, start Countly in the <code>application:didFinishLaunchingWithOptions:</code> </span><span style="font-weight: 400;">method of your app with the following configuration. Do not forget to specify <code>CLYPushNotifications</code></span><span style="font-weight: 400;"> in the <code>features</code> </span><span style="font-weight: 400;">array on the <code>CountlyConfig</code> </span><span style="font-weight: 400;">object. Then you'll need to ask for user's permission for push notifications using the Countly <code>askForNotificationPermission</code></span><span style="font-weight: 400;"> method at any point in the app. The Countly iOS SDK will automatically handle the rest. No need to call any other method for registering when a device token is generated, or a push notification is received.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">#import "Countly.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  //Start Countly with CLYPushNotifications feature as follows
  CountlyConfig* config = CountlyConfig.new;
  config.appKey = @"YOUR_APP_KEY";
  config.host = @"https://YOUR_COUNTLY_SERVER";
  config.features = @[CLYPushNotifications];
  //config.pushTestMode = CLYPushTestModeDevelopment;
  [Countly.sharedInstance startWithConfig:config];


  //Ask for user's permission for Push Notifications (not necessarily here)
  //You can do this later at any point in the app after starting Countly
  [Countly.sharedInstance askForNotificationPermission];

  // your code

  return YES;
}</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -&gt; Bool
{
  //Start Countly with CLYPushNotifications feature as follows
  let config: CountlyConfig = CountlyConfig()
  config.appKey = "YOUR_APP_KEY"
  config.host = "https://YOUR_COUNTLY_SERVER"
  config.features = [CLYPushNotifications]
  //config.pushTestMode = CLYPushTestModeDevelopment
  Countly.sharedInstance().start(with: config)

  //Ask for user's permission for Push Notifications (not necessarily here)
  //You can do this later at any point in the app after starting Countly
  Countly.sharedInstance().askForNotificationPermission()

  // your code

  return true
}</code></pre>
  </div>
</div>
<p>
  <strong>Note:</strong><span style="font-weight: 400;"> Ensure you code-sign your application using the </span><strong>explicit Provisioning Profile</strong><span style="font-weight: 400;"> specific to your </span><strong>app's bundleID</strong><span style="font-weight: 400;"> with an </span><span style="font-weight: 400;">aps-environment</span><span style="font-weight: 400;"> key in it. You can get it from the </span><a href="https://developer.apple.com/account/ios/profile/landing"><strong>iOS Provisioning Profiles</strong></a><span style="font-weight: 400;"> section of the Apple Developer website. Be advised, wildcard (*) profiles or profiles <code>aps-environment</code></span><span style="font-weight: 400;"> key do not work with APNs, and the device can not receive a push token.</span>
</p>
<p>
  <strong>Note: </strong>Please make sure you <strong>do not set</strong>
  <code>UNUserNotificationCenter.currentNotificationCenter</code>'s delegate manually,
  as Countly iOS SDK will be acting as the delegate.
</p>
<p>
  <strong>Note:</strong>
  <span style="font-weight: 400;">To see how to send push notifications using the Countly Server, please check our</span>
  <a href="/hc/en-us/articles/360037270012">Push Notifications documentation</a>.
</p>
<h2 id="h_01HNF5NAJ40CEETJNZFDT5CPJ7">Removing Push</h2>
<p>
  To disable push notifications in your app and avoid App Store Connect warnings,
  you can define the macro "COUNTLY_EXCLUDE_PUSHNOTIFICATIONS" in your project's
  preprocessor macros setting. The location of this setting will vary depending
  on the development environment you are using.
</p>
<p>
  For example, in Xcode, you can define this macro by navigating to the project
  settings, selecting the build target, and then selecting the "Build Settings"
  tab. Under the "Apple LLVM - Preprocessing" section, you will find the "Preprocessor
  Macros" where you can add the macro "COUNTLY_EXCLUDE_PUSHNOTIFICATIONS" to the
  Debug and/or Release fields. This will exclude push notifications from the build
  and avoid the App Store Connect warnings.
</p>
<h2 id="h_01HAVHW0RQG8PK3Z0KFW0D4Y2K">Deep links</h2>
<p>
  <span style="font-weight: 400;">When you send a push notification with custom actions buttons, you can redirect users to any custom page or view in your app by specifying deep links as custom actions button URLs. To do so, you will first need to create a URL scheme (e.g. : <code>myapp://</code></span><span style="font-weight: 400;">) in your project.</span>
</p>
<p>
  <span style="font-weight: 400;">To do so, select your app target in Xcode and open the <code>Info</code></span><span style="font-weight: 400;"> tab. Then, open the <code>URL Types</code></span><span style="font-weight: 400;"> section by clicking the horizontal arrow, and click the plus <code>+</code></span><span style="font-weight: 400;"> sign there.</span>
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/cbf1169-ss_url_types.png">
</div>
<p>
  <span style="font-weight: 400;">Enter an identifier (preferably in reverse domain format) into the <code>Identifier</code></span><span style="font-weight: 400;"> field and enter your app's URL scheme (without <code>://</code></span><span style="font-weight: 400;">part) into the <code>URL Schemes</code></span><span style="font-weight: 400;"> field. Optionally, you can set an <code>Icon</code></span><span style="font-weight: 400;">. You can leave the <code>Role</code></span><span style="font-weight: 400;"> field as whatever its default value is. When you are done, you can confirm that your new URL scheme has been added to your app's <code>Info.plist</code></span><span style="font-weight: 400;"> file. It should look like this:</span>
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/273fd0d-ss2.png">
</div>
<p>
  <span style="font-weight: 400;">After setting up the URL scheme, you should add the <code>application:openURL:options:</code></span><span style="font-weight: 400;"> method to your app delegate:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary&lt;UIApplicationOpenURLOptionsKey, id&gt; *)options
{
  //handle URL here to navigate to custom views

  return YES;
}</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -&gt; Bool
{
  //handle URL here to navigate to custom views

  return true
}</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">If your app's deployment target is lower than iOS9, you should add the <code>application:openURL:sourceApplication:annotation:</code></span><span style="font-weight: 400;"> method instead:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(nullable NSString *)sourceApplication annotation:(id)annotation
{
  //handle URL here to navigate to custom views

  return YES;
}</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -&gt; Bool
{
  //handle URL here to navigate to custom views

  return true
}</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Then in this method, you can check the passed <code>url</code></span><span style="font-weight: 400;"> for custom view navigation using the<code>scheme</code></span><span style="font-weight: 400;"> and <code>host</code></span><span style="font-weight: 400;"> properties. For example, if you set the custom action button URLs as <code>countly://productA</code></span><span style="font-weight: 400;"> and <code>countly://productB</code></span><span style="font-weight: 400;">, you can use something similar to this snippet:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">if ([url.scheme isEqualToString: @"countly"])
{
  if ([url.host isEqualToString: @"productA"])
  {
    // present view controller for Product A;
  }
  else if ([url.host isEqualToString: @"productB"])
  {
    // present view controller for Product B;
  }

 // or you can use host property directly
}</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">if (url.scheme == "countly")
{
  if (url.host == "productA")
  {
    // present view controller for Product A;
  }
  else if (url.host == "productB")
  {
    // present view controller for Product B;
  }

  // or you can use host property directly
}</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">When users tap on the custom action buttons, the Countly iOS SDK will open the specified URLs with your app's scheme. Following this, the related method you added to your app's delegate will be called.</span>
</p>
<h2 id="h_01HAVHW0RQBBY1K3EFHSSH6WFF">Rich Media</h2>
<p>
  <span style="font-weight: 400;">Rich push notifications allow you to send image, video, or audio attachments as well as customized action buttons on iOS10+. You will need to set up the Notification Service Extension to use it.</span>
</p>
<p>
  While the main project file is selected, please click the
  <code>Editor &gt; Add Target...</code> menu in Xcode, and add a
  <code>Notification Service Extension</code> target.
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/f62249f-screen-1.png">
</div>
<p>
  <span style="font-weight: 400;">Use the <code>Product Name</code> field of the Notification Service Extension target as you wish (for example: CountlyNSE) and ensure the <code>Team</code> is also selected.</span>
</p>
<p>
  <strong>Note:</strong>
  <span style="font-weight: 400;">If Xcode asks a question about activating the scheme for a newly added Notification Service Extension target, you can select</span>
  <code>Cancel</code>.
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/17d2fec-screen-2.png">
</div>
<p>
  Under the <code>Build Phases</code> &gt; <code>Compile Sources</code>
  <span style="font-weight: 400;">section of a newly added extension target, click the</span><code style="font-size: 15px;">+</code>
  sign.
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/1255590-screen-3_arrow.png">
</div>
<p>
  Select <code>CountlyNotificationService.m</code> from the list.
</p>
<p>
  <strong>Note:</strong>
  <span style="font-weight: 400;">If you cannot see the <code>CountlyNotificationService.m</code></span><span style="font-weight: 400;"> file because you are using CocoaPods or Carthage for integration, please locate it yourself (probably under the <code>Pods</code></span><span style="font-weight: 400;"> folder) and add it to your project manually.</span>
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/2def469-screen_4.png">
</div>
<p>
  Then find the <code>NotificationService.m</code> file (<code>NotificationService.swift</code>
  in Swift projects)
  <span style="font-weight: 400;">in the extension target. It is a default template file added automatically by Xcode. Import <code>CountlyNotificationService.h</code></span><span style="font-weight: 400;"> inside this file.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">#import "CountlyNotificationService.h"</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">// No need to import files for Swift projects</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Then add the following line at the end of the </span>
  <code>didReceiveNotificationRequest:withContentHandler:</code> method as shown
  below:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">- (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent * _Nonnull))contentHandler
{
  self.contentHandler = contentHandler;
  self.bestAttemptContent = [request.content mutableCopy];

  //delete existing template code, and add this line
  [CountlyNotificationService didReceiveNotificationRequest:request withContentHandler:contentHandler];
}
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">override func didReceive(_ request: UNNotificationRequest, withContentHandler contentHandler: @escaping (UNNotificationContent) -&gt; Void)
{
  self.contentHandler = contentHandler
  bestAttemptContent = (request.content.mutableCopy() as? UNMutableNotificationContent)

  //delete existing template code, and add this line
  CountlyNotificationService.didReceive(request, withContentHandler: contentHandler);
}</code></pre>
  </div>
</div>
<p>
  <strong>Note:</strong>
  <span style="font-weight: 400;">Please ensure you also configure the <code>App Transport Security</code></span><span style="font-weight: 400;"> setting in the extension's <code>Info.plist</code></span><span style="font-weight: 400;"> file just as with the main application. Otherwise, media attachments from non-https sources cannot be loaded.</span>
</p>
<p>
  <strong>Note:</strong>
  <span style="font-weight: 400;">Please ensure you check that the <code>Deployment Target</code></span><span style="font-weight: 400;"> version of the extension target is <code>10</code></span><span style="font-weight: 400;">, not 10.3 (or whatever minor version Xcode set automatically). Otherwise, users running iOS versions lower than the <code>Deployment Target</code></span><span style="font-weight: 400;"> value will not be able to get rich push notifications.</span>
</p>
<h2 id="h_01HAVHW0RQY6P4DBXNGBFZPKQE">
  Provisional Permission for Push Notifications (iOS 12+ only)
</h2>
<p>
  <span style="font-weight: 400;">iOS12 has a new feature called Provisional Permission for push notifications, and it is granted by default for all users. Without showing the notification permission dialog and without requiring users to accept anything, it allows you to send notifications to the users.</span>
</p>
<p>
  <span style="font-weight: 400;">However, these notifications vary slightly, they do not actually notify the users. There are no alerts, no banners, no sounds, no badges. Nothing informing the users at the moment of notification delivery. Instead, these notifications go directly to the Notification Center and they silently pile up in the list. Only when the user goes to the Notification Center and checks the list, the user becomes aware of them.</span>
</p>
<p>
  To utilize Provisional Permission for push notifications (while requesting for
  notification permission types), you pass a new type, called
  <code>UNAuthorizationOptionProvisional</code>.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">UNAuthorizationOptions authorizationOptions = UNAuthorizationOptionProvisional;

[Countly.sharedInstance askForNotificationPermissionWithOptions:authorizationOptions completionHandler:^(BOOL granted, NSError *error)
{
  NSLog(@"granted: %d", granted);
  NSLog(@"error: %@", error);
}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let authorizationOptions : UNAuthorizationOptions = [.provisional]

Countly.sharedInstance().askForNotificationPermission(options: authorizationOptions, completionHandler:
{ (granted : Bool, error : Error?) in
  print("granted: \(granted)")
  print("error: \(error)")
})</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">If this is the only notification permission type for which you ask, there will be no permission dialog and it will be granted by default. Then, later on, the Notification Center users can swipe on these provisional notifications and cancel the provisional permission anytime they please. The notification permission level then changes to the <code>UNAuthorizationStatusDenied</code></span><span style="font-weight: 400;"> from the <code>UNAuthorizationStatusProvisional</code></span><span style="font-weight: 400;"> state. This functions is a kind of opt-out.</span>
</p>
<h2 id="h_01HAVHW0RQSSB4M60SRFCEA596">How Push Notifications Work in Countly</h2>
<p>
  <span style="font-weight: 400;">When a push notification is received, the Countly iOS SDK handles everything automatically.</span>
</p>
<p>
  <span style="font-weight: 400;">First, it checks if the notification payload has the Countly specific dictionary (<code>c</code></span><span style="font-weight: 400;"> key) and the notification ID inside it (<code>i</code></span><span style="font-weight: 400;">key). If the Countly specific dictionary is present, it processes the notification. Otherwise, it does nothing. In both cases, the Countly iOS SDK forwards the notification to the default application delegate implementation for manual handling.</span>
</p>
<p>
  <span style="font-weight: 400;">The processing of the notification payload depends on the iOS version, the application’s status (background or foreground) at the time of notification reception, and the notification payload's content.</span>
</p>
<p>
  <span style="font-weight: 400;">If there is a media attachment or custom action buttons, the Notification Service Extension handles everything automatically. Users can view these notifications via their device’s 3D Touch or by swiping up on older devices.</span>
</p>
<p>
  <span style="font-weight: 400;">When the app is not in the foreground, it waits for the user's interaction (e.g. tapping the actual notification or one of the custom action buttons). After the user's interaction, it automatically records a specific event indicating that that user has opened the push notification. If the user tapped one of the custom action buttons, it also records another specific event with button index segmentation and redirects them to the specified URL for that action.</span>
</p>
<p>
  When the app is in foreground, it uses
  <code>UNNotificationPresentationOptionAlert</code> mode on iOS10+ to present
  a default notification banner and it uses the system
  <code>UIAlertController</code> on older iOS versions and
  <span style="font-weight: 400;">directly records push-opened events.</span>
</p>
<p>
  <span style="font-weight: 400;">You can view the detailed flow in this chart (download the chart for a larger view):</span>
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/0176050-diagram-3.png">
</div>
<h2 id="h_01HAVHW0RQT4Z1ZS28WHTGKNE7">Advanced Setup</h2>
<h3 id="h_01HAVHW0RQWTV4XM00GRAS3ZW6">Test Mode</h3>
<p>
  For Development builds (where the project is code signed with an iOS Development
  Provisioning Profile), you should set
  <code class="objectivec">pushTestMode</code>as
  <code class="objectivec">CLYPushTestModeDevelopment</code>on
  <code>CountlyConfig</code> object.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.pushTestMode = CLYPushTestModeDevelopment;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.pushTestMode = CLYPushTestModeDevelopment</code></pre>
  </div>
</div>
<p>
  For TestFlight or AdHoc Distribution builds (where the project is code signed
  with an iOS Distribution Provisioning Profile), you should set
  <code class="objectivec">pushTestMode</code>as
  <code class="objectivec">CLYPushTestModeTestFlightOrAdHoc</code>on
  <code>CountlyConfig</code> object.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.pushTestMode = CLYPushTestModeTestFlightOrAdHoc;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.pushTestMode = CLYPushTestModeTestFlightOrAdHoc</code></pre>
  </div>
</div>
<p>
  So, you can send test push notifications to test devices on Countly Server Create
  Message screen.
</p>
<p>
  <strong>Note:</strong> For App Store production builds, no need to set
  <code class="objectivec">pushTestMode</code>on <code>CountlyConfig</code> object
  at all.
</p>
<h3 id="h_01HAVHW0RQPGNC7YD09Q3Z41MK">Disabling Alerts Shown by Notifications</h3>
<p>
  <span style="font-weight: 400;">To disable messages from automatically being shown by the <code>CLYPushNotifications</code></span><span style="font-weight: 400;"> feature while the app is in the foreground, you can set the <code>doNotShowAlertForNotifications</code></span><span style="font-weight: 400;"> flag on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object. If set, no message will be displayed by using the default system UI in the app, but push-open events will be recorded automatically.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.doNotShowAlertForNotifications = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.doNotShowAlertForNotifications = true</code></pre>
  </div>
</div>
<h3 id="h_01HAVHW0RQRHJ27TXHTTZ0F82M">Manually Handling Notifications</h3>
<p>
  <span style="font-weight: 400;">If you would like to do additional custom work when a push notification is received, all you need to do is implement the default push-related methods in your application delegate (e.g. <code>AppDelegate.m</code></span><span style="font-weight: 400;">). After finishing its internal work, the Countly iOS SDK will push forward the related method calls to the default implementations on the application delegate.</span>
</p>
<p>
  <span style="font-weight: 400;">Please ensure you </span><strong>do not set </strong><span style="font-weight: 400;">the<code>UNUserNotificationCenter.currentNotificationCenter</code></span><span style="font-weight: 400;">'s delegate manually, as the Countly iOS SDK will be acting as the delegate. All you need to do is directly add the<code>UNUserNotificationCenterDelegate</code></span><span style="font-weight: 400;"> methods to your application delegate class.</span>
</p>
<p>
  <span style="font-weight: 400;">Inside the push notification <code>userInfo</code></span><span style="font-weight: 400;">dictionary you can find all the necessary information under the Countly Payload dictionary specified by the <code>c</code> (<code>kCountlyPNKeyCountlyPayload</code>)</span><span style="font-weight: 400;"> key. The array of the custom action buttons is specified by the<code>b</code> (<code>kCountlyPNKeyButtons</code></span><span style="font-weight: 400;">) key here, and each custom action button's title and action URL is specified by the<code>t</code> (<code>kCountlyPNKeyActionButtonTitle</code>) and <code>l</code> (<code>kCountlyPNKeyActionButtonURL</code>)</span><span style="font-weight: 400;"> keys, respectively. Here is an example of the Countly Push Notification Payload:</span>
</p>
<pre><code class="json">{
  "aps":
  {
    "alert": "this is notification text",
    //or     {"title": "title string", "body": "message string"}, //if title is set separately
        "sound": "sound_name", //if sound is set
        "badge": 123, //if badge is set
        "content-available": 1, //if data only flag is set
        "mutable-content": 1, //if buttons or media attachment is set
  },

  "c":
  {
    "i": "100001", //notification ID
    "l": "https://example.com/defaultlink", //if default link is set
        "a": "https://rich.media.url.jpg", //if media attachment is  set
    "b": //if buttons is set
    [
      {
        "t": "Custom Action Button Title 1", //button title
        "l": "https://example.com/test1", //button link
      },
      {
        "t": "Custom Action Button Title 2",
        "l": "https://example.com/test2",
      },
    ],
  },

  //any other custom data if set
}</code></pre>
<p>
  <span style="font-weight: 400;">You can create your own custom UI to display notification messages and custom action buttons according to your needs, along with URLs to redirect users when action is taken. Once users take action by clicking your custom buttons, you will need to manually report this event using this method:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSDictionary* userInfo;     // notification dictionary
NSInteger buttonIndex = 1;  // clicked button index
                            // 1 for first action button
                            // 2 for second action button
                            // 0 for default action
[Countly.sharedInstance recordActionForNotification:userInfo clickedButtonIndex:buttonIndex];
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let userInfo : Dictionary&lt;String, AnyObject&gt; = Dictionary() // notification dictionary
let buttonIndex : Int = 1  // clicked button index
                           // 1 for first action button
                           // 2 for second action button
                           // 0 for default action

Countly.sharedInstance().recordAction(forNotification:userInfo, clickedButtonIndex:buttonIndex)</code></pre>
  </div>
</div>
<h3 id="h_01HAVHW0RRY04DQTV3QNZ23N0Y">Always Sending Push Tokens</h3>
<p>
  <span style="font-weight: 400;">Thanks to iOS’ Remote Notification Background Mode, silent push notifications can be sent to users who have not given notification permission. However, the Countly iOS SDK does not send push tokens to the server by default from users who have not given permission for notifications. You can change this by setting the <code>sendPushTokenAlways</code> flag on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object. If set, push tokens from all users, regardless of their notification permission status, will be sent to the Countly Server and these users will be listed as possible recipients on the </span><strong>Create Message</strong><span style="font-weight: 400;"> screen of the Countly Dashboard. Be advised; these users can not be notified by an alert, sound, or badge. This is useful only for sending data via silent notifications.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.sendPushTokenAlways = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.sendPushTokenAlways = true</code></pre>
  </div>
</div>
<h3 id="h_01HAVHW0RRGZ4PQF3CJZWT6B0F">Notification Permission with Preferred Types and Callback</h3>
<p>
  <span style="font-weight: 400;">As asking for users’ permission for push notifications differ by iOS versions, the Countly iOS SDK has a one-liner convenience method, <code>askForNotificationPermission</code></span><span style="font-weight: 400;">,</span><span style="font-weight: 400;"> which does this for both iOS10 and older versions. It simply asks for a user's permission for all available notification types. However, if you need to specify which notification types your app will use (alert, badge, sound) or if you need a callback to see a user's response to the permission dialog, you can use the</span><code>askForNotificationPermissionWithOptions:completionHandler:</code>
  method.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">UNAuthorizationOptions authorizationOptions = UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert;

[Countly.sharedInstance askForNotificationPermissionWithOptions:authorizationOptions completionHandler:^(BOOL granted, NSError *error)
{
  NSLog(@"granted: %d", granted);
  NSLog(@"error: %@", error);
}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let authorizationOptions : UNAuthorizationOptions = [.badge, .alert, .sound]

Countly.sharedInstance().askForNotificationPermission(options: authorizationOptions, completionHandler:
{ (granted : Bool, error : Error?) in
  print("granted: \(granted)")
  print("error: \(error)")
})</code></pre>
  </div>
</div>
<h3 id="h_01HAVHW0RRMFYJR65NV0B5H3HS">Custom Alert Sounds</h3>
<p>
  The playing of notification sounds is handled by iOS, so all limitations would
  also be dictated by it. At the time of writing, audio data formats supported
  by iOS are: Linear PCM, MA4 (IMA/ADPCM), µLaw, aLaw. And that data needs to be
  packaged in aiff, wav, or caf file formats.
</p>
<p>
  More information can be found
  <a href="https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/SupportingNotificationsinYourApp.html#//apple_ref/doc/uid/TP40008194-CH4-SW1" target="_self">here</a>
  under "Preparing Custom Alert Sounds" section.
</p>
<p>
  You have to add that audio file to your application target. If you have added
  an audio file called "exampleSound.wav" to your project, when sending a push
  notification, you should enter "exampleSound.wav" inside the "Send sound" field
  on Countly Server push notifications dashboard.
</p>
<h3 id="h_01HAVHW0RRM96KAW3PMYCQKJN0">macOS launchNotification</h3>
<p>
  <code>launchNotification</code> property on initial configuration needs to be
  set in <span><code>applicationDidFinishLaunching:</code></span> method of macOS
  apps that use <code><span>CLYPushNotifications</span></code> feature, in order
  to handle app launches by push notification click.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.launchNotification = notification;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.launchNotification = notification</code></pre>
  </div>
</div>
<h2 id="h_01HNF5NAJ41Y4YT87PGV5HKE39">Setting up Credentials</h2>
<h3 id="h_01HNF5NPFR0W8WJ1BW8WVXJ5AB">
  <strong><span style="font-weight: 400;">Acquiring Credentials</span></strong>
</h3>
<p>
  <strong><span style="font-weight: 400;">There are two ways you can acquire Push Notification credentials from Apple:</span></strong>
</p>
<ul>
  <li>APNs Auth Key (preferred method)</li>
  <li>Universal (Sandbox + Production) Certificate</li>
</ul>
<h4 id="h_01HAVHW0RQGBSB4VVFJMK2EB8K">Getting an APNs Auth Key</h4>
<p>
  <span style="font-weight: 400;">APNs Auth Key is the preferred authentication method on APNs for a number of reasons, including less issues faced during configuration and the fact that it can reuse the same connection with multiple apps.</span>
</p>
<p>
  <span style="font-weight: 400;">First go to the </span><a href="https://developer.apple.com/account/ios/authkey/create"><span style="font-weight: 400;">Create a New Key</span></a><span style="font-weight: 400;"> section on the Apple Developer website to get an APNs Auth Key.</span>
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/1df7566-af33314-Screenshot_2017-09-20_14.38.56.png">
</div>
<p>
  Check the <code>APNs</code> option and create your key.
</p>
<p>
  <span style="font-weight: 400;">Then download your key and store it in a safe place, you won't be able to download it again.</span><span style="font-weight: 400;"><br></span><span style="font-weight: 400;">You'll also need some identifiers to upload a key file to Countly:</span>
</p>
<ul>
  <li>
    <p>
      <code>Key ID</code> (filled automatically if you kept the original Auth
      Key filename, otherwise visible on the key details panel)
    </p>
  </li>
  <li>
    <p>
      <code>Team ID</code> (see
      <a href="https://developer.apple.com/account/#/membership/">Membership</a>
      section)
    </p>
  </li>
  <li>
    <p>
      <code>Bundle ID</code> (see
      <a href="https://developer.apple.com/account/ios/identifier/bundle">App IDs</a>
      section)
    </p>
  </li>
</ul>
<h4 id="h_01HAVHW0RQPP7Z6CQJ5V0HS7MC">Getting APNs Universal (Sandbox + Production) Certificate</h4>
<p>
  <span style="font-weight: 400;">Please go to the </span><strong>Certificates</strong><span style="font-weight: 400;"> section on the </span><a href="https://developer.apple.com/account/ios/certificate/"><strong>Certificates, Identifiers &amp; Profiles</strong></a><span style="font-weight: 400;"> page on the Apple Developer website. Click the plus sign and select the </span><strong>Apple Push Notification service SSL (Sandbox &amp; Production)</strong><span style="font-weight: 400;"> type. Follow the instructions. Once you are done, download it and double click to add it to your Keychain.</span>
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/2248a72-1009cff-push_addcert.png">
</div>
<p>
  <span style="font-weight: 400;">Next, you'll need to export your push certificate into </span><strong>p12</strong><span style="font-weight: 400;"> format. Please open the </span><strong>Keychain Access</strong><span style="font-weight: 400;"> app, select the </span><strong>login</strong><span style="font-weight: 400;"> keychain, and the </span><strong>My Certificates</strong><span style="font-weight: 400;"> category. Search for your app ID and find the certificate starting with the </span><strong>Apple Push Services</strong><span style="font-weight: 400;">. Select both the certificate and its private key as shown in the screenshot below. Right click and choose </span><strong>Export 2 items...</strong><span style="font-weight: 400;"> and save it. You're free to name the p12 file as you wish and to set up a passphrase or leave it empty.</span>
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/94d763b-push_p12.png">
</div>
<h3 id="h_01HNF5QRPJGG0GKMMH2SZWVK85">
  <span style="font-weight: 400;">Setting up the Dashboard</span>
</h3>
<p>
  <span style="font-weight: 400;">Once you’ve downloaded </span><strong>your Auth Key</strong><span style="font-weight: 400;"> or exported </span><strong>your certificate</strong><span style="font-weight: 400;">, you will need to upload it to your Countly Server. Please go to <code>Management</code> &gt; <code>Applications</code> &gt; <code>Your App</code></span><span style="font-weight: 400;">.</span><span style="font-weight: 400;"> Scroll down to <strong>App settings</strong> </span><span style="font-weight: 400;">and upload your Auth Key or exported certificate under the <strong>iOS settings</strong></span><span style="font-weight: 400;"> section.</span>
</p>
<div class="img-container">
  <img src="/guide-media/01GVD4NGFQ4RR2VYHWBK04M12E" alt="001.png">
</div>
<p>
  <span style="font-weight: 400;">After filling all the required fields, click the </span><span style="font-weight: 400;"><strong>Save changes </strong></span><span style="font-weight: 400;">button. Countly will check the validity of the credentials by initiating a test connection to the APNs.</span>
</p>
<h1 id="h_01HAVHW0RRSPH1W989GXSPR3HY">User Location</h1>
<div class="callout callout--info">
  <strong>Enterprise Edition Feature</strong>
  <p>
    This feature is only available with an
    <a href="https:/countly.com/enterprise">Enterprise Edition</a> and built-in
    <a href="https://countly.com/flex">Flex</a>.
  </p>
</div>
<h2 id="h_01HAVHW0RRKP4VMJHP538EDXRM">Setting Location</h2>
<p>
  <span style="font-weight: 400;">Countly allows you to send GeoLocation-based push notifications to your users. By default, the Countly Server uses the GeoIP database to deduce a user's location. However, if your app has a better mean of detecting location, you can send this information to the Countly Server by using the initial configuration properties or relevant methods.</span>
</p>
<p>
  <span style="font-weight: 400;">Initial configuration properties can be set on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object to be sent upon SDK initialization. These include:</span>
</p>
<ul>
  <li>
    <code>location</code>: a CLLocationCoordinate2D struct specifying latitude
    and longitude
  </li>
  <li>
    <code>ISOCountryCode</code> an NSString in ISO 3166-1 alpha-2 format country
    code
  </li>
  <li>
    <code>city</code> an NSString specifying city name
  </li>
  <li>
    <code>IP</code> an NSString specifying an IP address in IPv4 or IPv6 format
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.location = (CLLocationCoordinate2D){35.6895,139.6917};

config.city = @"Tokyo";

config.ISOCountryCode = @"JP";

config.IP = @"255.255.255.255"</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.location = CLLocationCoordinate2D(latitude:35.6895, longitude: 139.6917)

config.city = "Tokyo"

config.ISOCountryCode = "JP"

config.IP = "255.255.255.255"</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">GeoLocation info recording methods can also be called at any time after the Countly iOS SDK has started. Values recorded using these methods will override the values specified upon initial configuration.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance recordLocation:(CLLocationCoordinate2D){35.6895,139.6917} city:@"Tokyo" ISOCountryCode:@"JP" IP:@"255.255.255.255"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().recordLocation(CLLocationCoordinate2D(latitude:33.6895, longitude:139.6917), city:"Tokyo", ISOCountryCode:"JP", IP:"255.255.255.255");</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Preferably you should use either location coordinate or city and country code pair.</span>
</p>
<h2 id="h_01HAVHW0RR7HA43KJ79QKR9C8S">Disabling Location</h2>
<p>
  <span>Also during init, you can disable location:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.disableLocation = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.disableLocation = true</code></pre>
  </div>
</div>
<p>GeoLocation info can also be disabled after init:</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance disableLocationInfo];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().disableLocationInfo;</code></pre>
  </div>
</div>
<p>
  Once disabled, you can re-enable GeoLocation info by calling the
  <code>recordLocation:</code> method.
</p>
<h1 id="h_01HAVHW0RRBKC5DT7Z5HYY70KQ">Remote Config</h1>
<p>
  <span style="font-weight: 400;">Remote config allows you to modify how your app functions or looks by requesting key-value pairs from your Countly server. The returned values may be modified based on the user properties. For more details, please see the </span><a href="/hc/en-us/articles/360037270492"><span style="font-weight: 400;">Remote Config documentation</span></a><span style="font-weight: 400;">.</span>
</p>
<p>
  Once downloaded, Remote config values will be saved persistently and available
  on your device between app restarts unless they are erased.
</p>
<p>
  <span style="font-weight: 400;">The two ways of acquiring remote config data are enabling automatic download triggers or manual requests.</span>
</p>
<p>
  If a full download of remote config values is performed, the previous list of
  values is replaced with the new one. If a partial download is performed, only
  the retrieved keys are updated, and values that are not part of that download
  stay as they were. A previously valid key may return no value after a full download.
</p>
<h2 id="h_01HD1JFPK6JV13N5JHST2SFHPM">Downloading Values</h2>
<div>
  <h3 id="h_01HD1JFSP96MQNGMVX29270QRN">
    <span>Automatic Remote Config Triggers</span>
  </h3>
  <p>
    <span style="font-weight: 400;">Automatic remote config triggers have been turned off by default; therefore, no remote config values will be requested without developer intervention.</span>
  </p>
  <p>
    <span style="font-weight: 400;">The automatic download triggers that would trigger a full value download are:</span>
  </p>
  <ul>
    <li>
      <span style="font-weight: 400;">when the SDK has finished initializing</span>
    </li>
    <li>
      <span style="font-weight: 400;">after the device ID is changed without merging</span>
    </li>
    <li>
      <span style="font-weight: 400;">when user gets out of temp ID mode</span>
    </li>
    <li>
      <span style="font-weight: 400;">when 'remote-config' consent is given after it had been removed before (if consents are enabled)</span>
    </li>
  </ul>
  <p>
    To enable the automatic triggers, you have to call
    <code class="objectivec">enableRemoteConfigAutomaticTriggers</code> on the
    configuration object you will provide during init.
  </p>
  <div class="tabs">
    <div class="tabs-menu">
      <span class="tabs-link is-active">Objective-C</span>
      <span class="tabs-link">Swift</span>
    </div>
    <div class="tab">
      <pre><code class="objectivec">config.enableRemoteConfigAutomaticTriggers = YES;
</code></pre>
    </div>
    <div class="tab is-hidden">
      <pre><code class="swift">config.enableRemoteConfigAutomaticTriggers = true</code></pre>
    </div>
  </div>
</div>
<p>
  Another thing you can do is to enable value caching with the
  <code class="objectivec">enableRemoteConfigValueCaching</code> flag. If all values
  were not updated, you would have metadata indicating if a value belongs to the
  old or current user.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.enableRemoteConfigValueCaching = YES;
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.enableRemoteConfigValueCaching = true</code></pre>
  </div>
</div>
<h3 id="h_01HAVHW0RRRC868GCFYXSND84J">Manual Calls</h3>
<p>
  There are three ways to trigger remote config value download manually:
</p>
<ul>
  <li>
    <span style="font-weight: 400;">Manually downloading all keys</span>
  </li>
  <li>
    <span style="font-weight: 400;">Manually downloading specific keys</span>
  </li>
  <li>Manually downloading, omitting (everything except) keys.</li>
</ul>
<p>
  <span style="font-weight: 400;">Each of these calls also has an optional parameter that you can provide a RCDownloadCallback to, which would be triggered when the download attempt has finished.</span>
</p>
<p>
  <span style="font-weight: 400;"><code class="java">downloadKeys</code></span><span style="font-weight: 400;">&nbsp;is</span><span style="font-weight: 400;"> the same as the automatically triggered update - it replaces all stored values with the ones from the server (all locally stored values are deleted and replaced with new ones).</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.remoteConfig downloadKeys:^(CLYRequestResult _Nonnull response, NSError * _Nonnull error, BOOL fullValueUpdate, NSDictionary&lt;NSString *,CountlyRCData *&gt; * _Nonnull downloadedValues) {<br>   //...<br>}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().remoteConfig.downloadKeys { response, error, fullValueUpdate, downloadedValues in
   //...
}
</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Or you might only want to update specific key values. To do so, you will need to call <code class="dart">downloadSpecificKeys</code> to downloads new values for the wanted keys. Those are provided with a String array.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.remoteConfig downloadSpecificKeys:NSArray *keys completionHandler:^(CLYRequestResult _Nonnull response, NSError * _Nonnull error, BOOL fullValueUpdate, NSDictionary&lt;NSString *,CountlyRCData *&gt; * _Nonnull downloadedValues) {<br>   //...<br>}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().remoteConfig.downloadSpecificKeys(keys, completionHandler: { response, error, fullValueUpdate, downloadedValues in<br>   //...<br>})
</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Or you might want to update all the values except a few defined keys. To do so,&nbsp; call <code class="dart">downloadOmittingKeys</code> would update all values except the provided keys</span><span style="font-weight: 400;">. The keys are provided with a String array.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.remoteConfig downloadOmittingKeys:NSArray *omitKeys completionHandler:^(CLYRequestResult _Nonnull response, NSError * _Nonnull error, BOOL fullValueUpdate, NSDictionary&lt;NSString *,CountlyRCData *&gt; * _Nonnull downloadedValues) {<br>   //...<br>}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance.remoteConfig.downloadOmittingKeys(omitKeys, completionHandler: { response, error, fullValueUpdate, downloadedValues in<br>   //...<br>})
</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">When making requests with an "inclusion" or "exclusion" array, if those arrays are empty or null, they will function the same as an update all request and will update all the values. This means it will also erase all keys not returned by the server.</span>
</p>
<h2 id="h_01HD1JPJG42365WYPKQT7WFA11">Accessing Values</h2>
<p>
  To get a stored value, call <code class="dart">getValue</code> with the specified
  key. This returns an CountlyRCData object that contains the value of the key
  and the metadata about that value's owner. If value in CountlyRCData was
  <code>null</code>
  <span style="font-weight: 400;">then no value was found or the value was <code>null</code>.</span>
  &nbsp;
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">id value_1 = [Countly.sharedInstance.remoteConfig getValue:@"key_1"].value;<br>id value_2 = [Countly.sharedInstance.remoteConfig getValue:@"key_2"].value;<br>id value_3 = [Countly.sharedInstance.remoteConfig getValue:@"key_3"].value;<br>id value_4 = [Countly.sharedInstance.remoteConfig getValue:@"key_4"].value;<br><br>int intValue = [value_1 isKindOfClass:[NSNumber class]] ? [(NSNumber *)value_1 intValue] : 0;<br>double doubleValue = [value_2 isKindOfClass:[NSNumber class]] ? [(NSNumber *)value_2 doubleValue] : 0.0;<br>NSArray *jArray = [value_3 isKindOfClass:[NSArray class]] ? (NSArray*)value_3 : @[];<br>NSDictionary *jObj = [value_4 isKindOfClass:[NSDictionary class]] ? (NSDictionary*)value_4 : @{};</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let value_1 = Countly.sharedInstance().remoteConfig.getValue("key_1")?.value
let value_2 = Countly.sharedInstance().remoteConfig.getValue("key_2")?.value
let value_3 = Countly.sharedInstance().remoteConfig.getValue("key_3")?.value
let value_4 = Countly.sharedInstance().remoteConfig.getValue("key_4")?.value

let intValue = value_1 as? Int ?? 0
let doubleValue = value_2 as? Double ?? 0.0
let jArray = value_3 as? [Any] ?? []
let jObj = value_4 as? [String: Any] ?? [:]
</code></pre>
  </div>
</div>
<p>
  If you want to get all values together you can use
  <code class="dart">getAllValues</code> which returns an NSDictionary&lt;NSString
  *, CountlyRCData*&gt;.
  <span style="font-weight: 400;">The SDK does not know the returned value type, so, it will return the <code>Any</code></span><span style="font-weight: 400;">. The developer then needs to cast it to the appropriate type. The returned values may also be <code>JSONArray</code></span><span style="font-weight: 400;">,&nbsp;</span><code>JSONObject</code>,
  or just a simple value, such as <code>NSNumber</code>.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSDictionary&lt;NSString*, CountlyRCData*&gt; *allValues = [Countly.sharedInstance.remoteConfig getAllValues];<br><br>int intValue = [(NSNumber *)allValues[@"key_1"] intValue];<br>double doubleValue = [(NSNumber *)allValues[@"key_2"] doubleValue];<br>NSArray*jArray = (NSArray *)allValues[@"key_3"];<br>NSDictionary*jObj = (NSDictionary *)allValues[@"key_4"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let allValues = Countly.sharedInstance().remoteConfig.getAllValues()<br>
let intValue = (allValues["key_1"] as? NSNumber)?.intValue ?? 0
let doubleValue = (allValues["key_2"] as? NSNumber)?.doubleValue ?? 0.0
let jArray = allValues["key_3"] as? [Any] ?? []
let jObj = allValues["key_4"] as? [String: Any] ?? [:]
</code></pre>
  </div>
</div>
<p>
  CountlyRCData object has two keys: value (Any) and isCurrentUsersData (Bool).
  Value holds the data sent from the server for the key that the CountlyRCData
  object belongs to. The isCurrentUsersData is only false when there was a device
  ID change, but somehow (or intentionally) a remote config value was not updated.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">@interface CountlyRCData : NSObject

@property (nonatomic) id value;
@property (nonatomic) BOOL isCurrentUsersData;

@end
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">class CountlyRCData {
  var value: Any
  var isCurrentUsersData: Bool
}
</code></pre>
  </div>
</div>
<h2 id="01HD1JH3R29EMPWD00YEEYSDHE">Clearing Stored Values</h2>
<p>
  <span style="font-weight: 400;">At some point, you might like to erase all the values downloaded from the server. You will need to call one function to do so.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.remoteConfig clearAll];
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().remoteConfig.clearAll()
</code></pre>
  </div>
</div>
<h2 id="01HD1JK8Y931787C8YXQYK4D1A">Global Download Callbacks</h2>
<p>
  Also, you may provide callback functions to be informed when the request is finished
  with <code class="objectivec">remoteConfigRegisterGlobalCallback</code>method
  during SDK initialization:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[config remoteConfigRegisterGlobalCallback:^(CLYRequestResult _Nonnull response, NSError * _Nonnull error, BOOL fullValueUpdate, NSDictionary&lt;NSString *,CountlyRCData *&gt; * _Nonnull downloadedValues) {<br>    // ...<br>}]
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.remoteConfigRegisterGlobalCallback { response, error, fullValueUpdate, downloadedValues in
    // ...
}</code></pre>
  </div>
</div>
<p>
  RCDownloadCallback is called when the remote config download request is finished,
  and it would have the following parameters:
</p>
<ul>
  <li>
    <code class="objectivec">response</code>: CLYRequestResult Enum (either CLYResponseError<span>, CLYResponseSuccess or CLYResponseNetworkIssue</span>)
  </li>
  <li>
    <code class="objectivec">error</code>: NSError (error message. "null" if
    there is no error)
  </li>
  <li>
    <code class="objectivec">fullValueUpdate</code>: BOOL ("true" - all values
    updated, "false" - a subset of values updated)
  </li>
  <li>
    <code class="objectivec">downloadedValues</code>: NSDictionary&lt;NSString
    *,CountlyRCData*&gt; (the whole downloaded remote config values)
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">typedef void (^RCDownloadCallback)(CLYRequestResult response, NSError *_Nullable error, BOOL fullValueUpdate, NSDictionary&lt;NSString*, CountlyRCData *&gt;* downloadedValues);
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">typealias RCDownloadCallback = (CLYRequestResult, Error?, Bool, [String: CountlyRCData]?) -&gt; Void
</code></pre>
  </div>
</div>
<p>
  <code class="objectivec">downloadedValues</code> would be the downloaded remote
  config data where the keys are remote config keys, and their value is stored
  in CountlyRCData class with metadata showing to which user data belongs. The
  data owner will always be the current user if caching is not enabled.
</p>
<p>
  You can also register (or remove) RCDownloadCallbacks to do different things
  after the SDK initialization. You can register callbacks multiple times:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">// register a callback
[Countly.sharedInstance.remoteConfig registerDownloadCallback:^(CLYRequestResult _Nonnull response, NSError *_Nonnull error, BOOL fullValueUpdate, NSDictionary&lt;NSString *,CountlyRCData*&gt; * _Nonnull downloadedValues) {
   //...
}];

// remove a callback
[Countly.sharedInstance.remoteConfig removeDownloadCallback:^(CLYRequestResult _Nonnull response, NSError *_Nonnull error, BOOL fullValueUpdate, NSDictionary&lt;NSString *,CountlyRCData*&gt; * _Nonnull downloadedValues) {
   //...
}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">// register a callback
Countly.sharedInstance().remoteConfig.removeDownloadCallback{ response, error, fullValueUpdate, downloadedValues in
   //...
}

// remove a callback
Countly.sharedInstance().remoteConfig.removeDownloadCallback{ response, error, fullValueUpdate, downloadedValues in
   //...
}
</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RRC18XJXE2N7R89CT0">A/B Testing</h2>
<p>
  You can enroll your users into into A/B tests for certain keys or remove them
  from some or all existing A/B tests available.
</p>
<div>
  <h3 id="h_01HD1JPJG4G9TFTF6M42SCGPFP">
    <span>Enrollment on Download</span>
  </h3>
  <p>
    You can enroll to available experiments when downloading the Remote Config
    values automatically. To do this you should call
    <code>enrollABOnRCDownload</code> method on the configuration object you
    pass for the initialization:
  </p>
  <pre><code class="objectivec">config.enrollABOnRCDownload= YES;</code></pre>
  <div>
    <div>
      <h3 id="h_01HD1JPQ091MP8WRBZMBMZC3HD">
        <span>Enrollment on Access</span>
      </h3>
      <p>
        <span>You can also enroll to A/B tests while getting RC values from storage. You can use <code>getValueAndEnroll</code> while getting a single value and <code>getAllValuesAndEnroll</code> while getting all values to enroll to the keys that exist. If no value was stored for those keys these functions would not enroll the user. Both of these functions works the same way with their non-enrolling variants, namely; <code>getValue</code> and <code>getAllValues</code>.</span>
      </p>
      <div>
        <div>
          <h3 id="h_01HD1JPTMT7XGM3KW1WBE97VBN">
            <span>Enrollment on Action</span>
          </h3>
          <p>
            To enroll a user into the A/B tests for the given keys you
            use the following method:
          </p>
          <div class="tabs">
            <div class="tabs-menu">
              <span class="tabs-link is-active">Objective-C</span>
              <span class="tabs-link">Swift</span>
            </div>
            <div class="tab">
              <pre><code class="objectivec">[Countly.sharedInstance.remoteConfig enrollIntoABTestsForKeys:NSArray *keys];
</code></pre>
            </div>
            <div class="tab is-hidden">
              <pre><code class="swift">Countly.sharedInstance().remoteConfig.enrollIntoABTests(forKeys: keys as [String])
</code></pre>
            </div>
          </div>
          <p>
            Here the keys array is the mandatory parameter for this method
            to work.
          </p>
          <div>
            <div>
              <h3 id="h_01HD1JPX82PR2HXKMZ2E68YATS">
                <span>Exiting A/B Tests</span>
              </h3>
              <p>
                If you want to remove users from A/B tests of certain
                keys you can use the following function:
              </p>
              <div class="tabs">
                <div class="tabs-menu">
                  <span class="tabs-link is-active">Objective-C</span>
                  <span class="tabs-link">Swift</span>
                </div>
                <div class="tab">
                  <pre><code class="objectivec">[Countly.sharedInstance.remoteConfig exitABTestsForKeys:NSArray *keys];
</code></pre>
                </div>
                <div class="tab is-hidden">
                  <pre><code class="swift">Countly.sharedInstance().remoteConfig.exitABTestsForKeys(forKeys: keys as [String])
</code></pre>
                </div>
              </div>
              <p>
                Here if no keys are provided it would remove the
                user from all A/B tests instead.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
<h1 id="h_01HAVHW0RRN4E332BBZ3TVDDPF">User Feedback</h1>
<p>
  There are two ways to receive user feedback: the Star Rating Dialog and the Feedback
  Widgets (Survey, NPS, Rating).
</p>
<p>
  The Star Rating Dialog allows users to give feedback as a rating from 1 to 5.
  Feedback Widgets allow for even more textual feedback from users.
</p>
<h2 id="h_01HAVHW0RR1P4DMGKA4XVM64V7">Star Rating Dialog</h2>
<p>
  <span style="font-weight: 400;">Optionally, you can set the Countly iOS SDK to automatically ask users for a 1 to 5-star rating, depending on the app launch count for each version. To do so, you will need to set the <code>starRatingSessionCount</code></span><span style="font-weight: 400;"> property on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object. When the total number of sessions reaches the <code>starRatingSessionCount</code></span><span style="font-weight: 400;">, an alert view asking for a 1 to 5-star rating will be displayed automatically, once for each new version of the app.</span>
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/0df53f4-rating-detail-white.png">
</div>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.starRatingSessionCount = 10;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.starRatingSessionCount = 10</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">If you would like the star-rating dialog to only be displayed once per app lifetime, instead of for each new version, you can set the <code>starRatingDisableAskingForEachAppVersion</code></span><span style="font-weight: 400;"> flag on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.starRatingDisableAskingForEachAppVersion = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.starRatingDisableAskingForEachAppVersion = true</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Additionally, you can customize the star-rating dialog message using the <code>starRatingMessage</code></span>
  property on the <code>CountlyConfig</code><span style="font-weight: 400;">object. If you do not explicitly specify this property, the message will read, "</span><em><span style="font-weight: 400;">How would you rate the app?</span></em><span style="font-weight: 400;">" or a corresponding localized version depending on the device language. Currently supported localizations: English, Turkish, Japanese, Chinese, Russian, Czech, Latvian, and Bengali.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.starRatingMessage = @"Please rate our app?";</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.starRatingMessage = "Please rate our app?"
config.starRatingDismissButtonTitle = "No, thanks."</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Additionally, you can set the <code>starRatingCompletion</code></span><span style="font-weight: 400;">block property on the <code>CountlyConfig</code></span><span style="font-weight: 400;">object to be executed after the star-rating dialog has been automatically shown. The completion block has a single NSInteger parameter that indicates the 1 to 5-star rating given by the user. If the user dismissed the dialog without giving a rating, the value for this rating will be 0, and it will not be reported to the server.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.starRatingCompletion = ^(NSInteger rating)
{
  NSLog(@"rating %d",(int)rating);
};</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.starRatingCompletion = { (rating : Int) in print("rating \(rating)") }</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Additionally, you can use the <code>askForStarRating:</code></span><span style="font-weight: 400;"> method to ask for a star rating anytime you would like. It displays the 1 to 5-star rating dialog manually and executes the completion block after the user's action. The completion block takes a single NSInteger parameter that indicates the 1 to 5-star rating given by the user. If the user dismissed the dialog without giving a rating, the value for this rating will be 0, and it will not be reported to the server. Manually asking for a star rating does not affect the automatically requested nature of the star rating.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance askForStarRating:^(NSInteger rating)
{
  NSLog(@"rating %li",(long)rating);
}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().ask(forStarRating:{ (rating : Int) in print("rating \(rating)") })</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RR6N7WKDSA1GRJXBJ1">Feedback Widget</h2>
<div class="callout callout--info">
  <p>
    Feedback Widgets is a
    <a href="https://countly.com/enterprise" target="_blank" rel="noopener noreferrer">Countly Enterprise</a>
    plugin.
  </p>
</div>
<p>
  It is possible to display 3 kinds of feedback widgets:
  <a href="/hc/en-us/articles/4652903481753#h_01HAY62C2QB9K7CRDJ90DSDM0D" target="_blank" rel="noopener">NPS</a>,
  <a href="/hc/en-us/articles/4652903481753#h_01HAY62C2Q965ZDAK31TJ6QDRY" target="_blank" rel="noopener">Survey</a>
  and
  <a href="/hc/en-us/articles/4652903481753#h_01HAY62C2R4S05V7WJC5DEVM0N" target="_blank" rel="noopener">Rating</a>.
  All widgets are shown as webviews and should be approached using the same methods.
</p>
<p>
  For more detailed information about Feedback Widgets, you can refer to
  <a href="/hc/en-us/articles/4652903481753" target="_blank" rel="noopener noreferrer">here</a>.
</p>
<div class="callout callout--warning">
  <p>
    Before any feedback widget can be shown, you need to create them in your
    Countly dashboard.
  </p>
</div>
<p>
  When the widgets are created, you need to use 2 calls in your SDK: one to get
  all available widgets for a user and another to display a chosen widget.
</p>
<p>To get your available widget list, use the call below.</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">
[Countly.sharedInstance getFeedbackWidgets:^(NSArray * feedbackWidgets, NSError * error)
{
  if (error)
  {
    NSLog(@"Getting widgets list failed. Error: %@", error);
  }
  else
  {
    NSLog(@"Getting widgets list successfully completed. %@", [feedbackWidgets description]);
  }
}];
    </code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">
Countly.sharedInstance().getFeedbackWidgets
{ (feedbackWidgets: [CountlyFeedbackWidget], error) in
  if (error != nil)
  {
    print("Getting widgets list failed. \n \(error!.localizedDescription) \n \((error! as NSError).userInfo)")
  }
  else
  {
    print("Getting widgets list successfully completed. \(String(describing: feedbackWidgets))")
  }
}</code></pre>
  </div>
</div>
<p>
  When feedback widgets are fetched successfully, <code>completionHandler</code>
  will be executed with an array of <code>CountlyFeedbackWidget</code> objects.
  Otherwise, <code>completionHandler</code> will be executed with an
  <code>NSError</code>.
</p>
<p>
  Calls to this method will be ignored and <code>completionHandler</code> will
  not be executed if:<br>
  - Consent for <code>CLYConsentFeedback</code> is not given, while
  <code>requiresConsent</code> flag is set on initial configuration.<br>
  - Current device ID is <code>CLYTemporaryDeviceID</code>.
</p>
<p>
  Once you get the list, you can inspect <code>CountlyFeedbackWidget</code> objects
  in it, by checking their <code>type</code>, <code>ID</code>, and
  <code>name</code> properties to decide which one to display. And when you decide,
  you can use <code>present</code> method on <code>CountlyFeedbackWidget</code>
  object to display it.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">CountlyFeedbackWidget * aFeedbackWidget = feedbackWidgets.firstObject; //assuming we want to display the first one in the list
[aFeedbackWidget present];
    </code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let aFeedbackWidget : CountlyFeedbackWidget? = feedbackWidgets?.first //assuming we want to display the first one in the list
aFeedbackWidget?.present()
    </code></pre>
  </div>
</div>
<p>Optionally you can pass appear and dismiss callback blocks:</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">CountlyFeedbackWidget * aFeedbackWidget = feedbackWidgets.firstObject; //assuming we want to display the first one in the list
[aFeedbackWidget presentWithAppearBlock:^
{
  NSLog(@"Appeared!");
}
andDismissBlock:^
{
  NSLog(@"Dismissed!");
}];
    </code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let aFeedbackWidget : CountlyFeedbackWidget? = feedbackWidgets?.first //assuming we want to display the first one in the list
aFeedbackWidget?.present(appear:
{
  print("Appeared.")
},
andDismiss:
{
  print("Dismissed.")
})
    </code></pre>
  </div>
</div>
<h3 id="h_01HAVHW0RRR7N3A283E2YQQT1Z">Manual Reporting</h3>
<p>
  Optionally you can fetch feedback widget data and create your own UI using:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">
CountlyFeedbackWidget * aFeedbackWidget = feedbackWidgets.firstObject; //assuming we want to display the first one in the list
[aFeedbackWidget getWidgetData:^(NSDictionary * widgetData, NSError * error)
{
  if (error)
  {
    NSLog(@"Getting widget data failed. Error: %@", error);
  }
  else
  {
    NSLog(@"Getting widget data successfully completed. %@", [widgetData description]);
  }
}];
    </code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">
let aFeedbackWidget : CountlyFeedbackWidget? = feedbackWidgets?.first //assuming we want to display the first one in the list
aFeedbackWidget?.getData
{ (widgetData: [AnyHashable: Any]?, error: Error?) in
  if (error != nil)
  {
    print("Getting widget data failed. Error \(error.debugDescription)")
  }
  else
  {
    print("Getting widget data successfully completed. \(String(describing: widgetData))")
  }
}    </code></pre>
  </div>
</div>
<p>
  And once you are done with your custom feedback widget UI you can record the
  result:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">
[aFeedbackWidget recordResult:resultDictionary];
// or
[aFeedbackWidget recordResult:nil]; // if user dismissed the feedback widget without completing it
    </code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">
aFeedbackWidget.recordResult(resultDictionary)
// or
aFeedbackWidget.recordResult(nil) // if user dismissed the feedback widget without completing it
</code></pre>
  </div>
</div>
<p>
  For more information regarding how to structure the result dictionary, you would
  look <a href="/hc/en-us/articles/9290669873305" target="_self">here</a>.
</p>
<h1 id="h_01HAVHW0RRRH4M1Y4CDJSHGERJ">User Profiles</h1>
<div class="callout callout--info">
  <strong>Enterprise Edition Feature</strong>
  <p>
    This feature is only available with an
    <a href="https://countly.com/enterprise">Enterprise Edition</a> and built-in
    <a href="https://countly.com/flex">Flex</a>.
  </p>
</div>
<p>
  <span style="font-weight: 400;">You can see detailed user information under the User Profiles section of the Countly Dashboard by recording user properties.</span>
</p>
<p>
  Note: If a property is set as an empty string, it will be deleted from the user
  on the server side.
</p>
<h2 id="h_01HAVHW0RRSN6J76K5N88M15TQ">Default User Properties</h2>
<p>
  <span style="font-weight: 400;">You can record default user detail properties by adhering to the following:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">//default properties
Countly.user.name = @"John Doe";
Countly.user.username = @"johndoe";
Countly.user.email = @"john@doe.com";
Countly.user.birthYear = @1970;
Countly.user.organization = @"United Nations";
Countly.user.gender = @"M";
Countly.user.phone = @"+0123456789";

//profile photo
Countly.user.pictureURL = @"https://s12.postimg.org/qji0724gd/988a10da33b57631caa7ee8e2b5a9036.jpg";
//or local image on the device
Countly.user.pictureLocalPath = localImagePath;

//save
[Countly.user save];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">//default properties
Countly.user().name = "John Doe" as CountlyUserDetailsNullableString
Countly.user().username = "johndoe" as CountlyUserDetailsNullableString
Countly.user().email = "john@doe.com" as CountlyUserDetailsNullableString
Countly.user().birthYear = 1970 as CountlyUserDetailsNullableNumber
Countly.user().organization = "United Nations" as CountlyUserDetailsNullableString
Countly.user().gender = "M" as CountlyUserDetailsNullableString
Countly.user().phone = "+0123456789" as CountlyUserDetailsNullableString

//profile photo
Countly.user().pictureURL = "https://s12.postimg.org/qji0724gd/988a10da33b57631caa7ee8e2b5a9036.jpg" as CountlyUserDetailsNullableString
//or local image on the device
Countly.user().pictureLocalPath = localImagePath as CountlyUserDetailsNullableString

//save
Countly.user().save()</code></pre>
  </div>
</div>
<p>
  <strong>Note:</strong>
  <span style="font-weight: 400;">Local images specified on the <code>pictureLocalPath</code></span><span style="font-weight: 400;"> property will not be persisted exclusively. If a request fails and is retried later, the local image is expected to still be present on the exact same path. Otherwise, the upload will be aborted.</span>
</p>
<h2 id="h_01HAVHW0RRJSVXADXPHXMQA4VW">Custom User Properties</h2>
<p>
  <span style="font-weight: 400;">You can record custom user detail properties by adhering to the following:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">//custom properties
Countly.user.custom = @{@"testkey1": @"testvalue1", @"testkey2": @"testvalue2"};

//save
[Countly.user save];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">//custom properties
Countly.user().custom = ["testkey1": "testvalue1", "testkey2": "testvalue2"] as CountlyUserDetailsNullableDictionary

//save
Countly.user().save()</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RR4ATCM2HFP0XZNVQ5">Custom User Property Modifiers</h2>
<p>
  <span style="font-weight: 400;">Also, you can use custom user property modifiers, such as the following:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.user set:@"key101" value:@"value101"];
[Countly.user setOnce:@"key101" value:@"value101"];
[Countly.user unSet:@"key101"];

[Countly.user increment:@"key102"];
[Countly.user incrementBy:@"key102" value:5];
[Countly.user multiply:@"key102" value:2];

[Countly.user max:@"key102" value:30];
[Countly.user min:@"key102" value:20];

[Countly.user push:@"key103" value:@"singlevalue"];
[Countly.user push:@"key103" values:@[@"a",@"b",@"c",@"d"]];
[Countly.user pull:@"key103" value:@"b"];
[Countly.user pull:@"key103" values:@[@"a",@"d"]];

[Countly.user pushUnique:@"key104" value:@"uniqueValue"];
[Countly.user pushUnique:@"key104" values:@[@"uniqueValue2",@"uniqueValue3"]];

//save
[Countly.user save];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.user().set("key101", value:"value101")
Countly.user().setOnce("key101", value:"value101")
Countly.user().unSet("key101")

Countly.user().increment("key102")
Countly.user().increment(by:"key102", value:5)
Countly.user().multiply("key102", value:2)

Countly.user().max("key102", value:30)
Countly.user().min("key102", value:20)

Countly.user().push("key103", value:"singlevalue")
Countly.user().push("key103", values:["a","b","c","d"])
Countly.user().pull("key103", value:"b")
Countly.user().pull("key103", values:["a","d"])

Countly.user().pushUnique("key104", value:"uniqueValue")
Countly.user().pushUnique("key104", values:["uniqueValue2","uniqueValue3"])

//save
Countly.user().save()</code></pre>
  </div>
</div>
<p>
  <strong>Note:</strong>Once saved, all properties on <code>Countly.user</code>
  will be cleared.
</p>
<p>
  <strong>Note:</strong>You can start setting user properties even before starting
  the Countly iOS SDK. They will be saved automatically when the SDK is started.
</p>
<h2 id="h_01HAVHW0RRY8CC2GFKN97RME88">Orientation Tracking</h2>
<p>
  <span style="font-weight: 400;">You can set the <code>enableOrientationTracking</code></span><span style="font-weight: 400;"> flag on the<code>CountlyConfig</code></span><span style="font-weight: 400;"> object before starting Countly. This flag is used for enabling automatic user interface orientation tracking. If set, user interface orientation tracking feature will be enabled and an event will be sent whenever user interface orientation changes. Orientation event will not be sent if consent for <code>CLYConsentUserDetails</code> is not given while <code>requiresConsent</code> flag is set on initial configuration. Automatic user interface orientation tracking is enabled by default. For disabling it, please set this flag to <code>NO<code>.
</code></code></span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.enableOrientationTracking = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.enableOrientationTracking = true</code></pre>
  </div>
</div>
<h1 id="h_01HAVHW0RSZQSMA1D7JWQ9WMT4">Application Performance Monitoring</h1>
<p>
  Performance Monitoring feature allows you to analyze your application's performance
  on various aspects. For more details please see
  <a href="/hc/en-us/articles/900000819806" target="_self">Performance Monitoring documentation</a>.
</p>
<p>
  Here is how you can utilize Performance Monitoring feature in your iOS apps:
</p>
<h2 id="h_01HAVHW0RS1P1F4FX14M9QD3NW">App Background and Foreground Time</h2>
<p>
  You need to enable App Background and Foreground Time tracking feature on the
  initial configuration:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.apm.enableForegroundBackgroundTracking = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.apm().enableForegroundBackgroundTracking = true</code></pre>
  </div>
</div>
<p>
  With this, Countly iOS SDK will start measuring the app foreground time, app
  background time.
</p>
<h2 id="01HN2RN10EXG8AMJPBV07AR3NW">App Start Time</h2>
<p>
  Currently iOS SDK support manual app start time tracking. For the app start time
  to be recorded, you need to set
  <code class="objectivec">enableAppStartTimeTracking</code> and
  <code class="objectivec">enableManualAppLoadedTrigger</code>&nbsp;on the initial
  configuration:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.apm.enableAppStartTimeTracking = YES;<br>config.apm.enableManualAppLoadedTrigger = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.apm().enableAppStartTimeTracking = true<br>config.apm().enableManualAppLoadedTrigger = true</code></pre>
  </div>
</div>
<p>
  And then you need to call <code>appLoadingFinished</code> method.
</p>
<p>
  It calculates and records the app launch time for performance monitoring.<br>
  It should be called when the app is loaded and it successfully displayed its
  first user-facing view. E.g. <code>viewDidAppear:</code> method of the root view
  controller or whatever place is suitable for the app's flow. Time passed since
  the app has started to launch will be automatically calculated and recorded for
  performance monitoring. App launch time can be recorded only once per app launch.
  So, the second and following calls to this method will be ignored.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance appLoadingFinished];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().appLoadingFinished()</code></pre>
  </div>
</div>
<p>
  If you also want to manipulate the app launch starting time instead of using
  the SDK calculated value then you will need to call a third method on the config
  object with the timestamp (in milliseconds) of that time you want:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">long long timestamp = floor(NSDate.date.timeIntervalSince1970 * 1000) - 500;<br>[config.apm setAppStartTimestampOverride:timestamp];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">long long timestamp = floor(NSDate.date.timeIntervalSince1970 * 1000) - 500;<br>config.apm().setAppStartTimestampOverride(timestamp)</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RS4Q2FT2ZN6VV4A8CP">Manual Network Traces</h2>
<p>
  You can record manual network traces using the<code><span>recordNetworkTrace</span>:<span>requestPayloadSize</span>:<span>responsePayloadSize</span>:<span>responseStatusCode</span>:<span>startTime</span>:<span>endTime</span>:</code>
  method.
</p>
<p>
  A network trace is a collection of measured information about a network request.<br>
  When a network request is completed, a network trace can be recorded manually
  to be analyzed in the Performance Monitoring feature later with the following
  parameters:
</p>
<p>
  - <code>traceName</code>: A non-zero length valid string<br>
  - <code>requestPayloadSize</code>: Size of the request's payload in bytes<br>
  - <code>responsePayloadSize</code>: Size of the received response's payload in
  bytes<br>
  - <code>responseStatusCode</code>: HTTP status code of the received response<br>
  - <code>startTime</code>: UNIX time stamp in milliseconds for the starting time
  of the request<br>
  - <code>endTime</code>: UNIX time stamp in milliseconds for the ending time of
  the request
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance recordNetworkTrace:@"/test/endpoint" requestPayloadSize:3445 responsePayloadSize:1290 responseStatusCode:200 startTime:1593418666954 endTime:1593418667384];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre>Countly.sharedInstance().recordNetworkTrace("/test/api", requestPayloadSize:3445, responsePayloadSize:1290, responseStatusCode:200, startTime:1593418666954, endTime:1593418667384)</pre>
  </div>
</div>
<h2 id="h_01HAVHW0RS8M0ZKHGB72ATGA28">Custom Traces</h2>
<p>
  You can also measure any operation you want and record it using custom traces.
  First, you need to start a trace by using the
  <code class="objectivec">startCustomTrace</code> method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance startCustomTrace:@"unzipping_saved_files"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre>Countly.sharedInstance().startCustomTrace("unzipping_saved_files")</pre>
  </div>
</div>
<p>
  Then you can end it using the
  <code class="objectivec">endCustomTrace:metrics:</code>method, optionally passing
  any metrics as key-value pairs:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance endCustomTrace:@"unzipping_saved_files" metrics:@{@"total_file_size": @1655700}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre>Countly.sharedInstance().startCustomTrace("unzipping_saved_files", metrics:["total_file_size": 1655700])</pre>
  </div>
</div>
<p>
  The duration of the custom trace will be automatically calculated on ending.
  Trace names should be non-zero length valid strings. Trying to start a custom
  trace with the already started name will have no effect. Trying to end a custom
  trace with already ended (or not yet started) name will have no effect.
</p>
<p>
  You can also cancel any custom trace you started, using
  <code class="objectivec">cancelCustomTrace:</code>method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance cancelCustomTrace:@"unzipping_saved_files"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre>Countly.sharedInstance().cancelCustomTrace("unzipping_saved_files")</pre>
  </div>
</div>
<p>
  Additionally, if you need you can cancel all custom traces you started, using
  the <code class="objectivec">clearAllCustomTraces</code>method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <div class="tabs">
      <div class="tabs-menu">
        <span class="tabs-link is-active">Objective-C</span>
        <span class="tabs-link">Swift</span>
      </div>
      <div class="tab">
        <pre><code class="objectivec">[Countly.sharedInstance clearAllCustomTraces];</code></pre>
      </div>
      <div class="tab is-hidden">
        <pre>Countly.sharedInstance().clearAllCustomTraces()</pre>
      </div>
    </div>
    <p>
      <strong>Note:</strong> All previously started custom traces are automatically
      cleaned when:<br>
      - Consent for <code>CLYConsentPerformanceMonitoring</code> is canceled.<br>
      - A new app key is set using the <code>setNewAppKey:</code> method.
    </p>
  </div>
</div>
<h1 id="h_01HAVHW0RSD3G39KNP8ZP9WD69">User Consent</h1>
<p>
  For compatibility with data protection regulations, such as GDPR, the Countly
  iOS SDK allows developers to enable/disable any feature at any time depending
  on user consent.
</p>
<p>
  More information about GDPR can be found
  <a href="https://medium.com/countly/countly-the-gdpr-how-worlds-leading-mobile-and-web-analytics-platform-can-help-organizations-5015042fab27">here</a>.
</p>
<h2 id="h_01HJ63TKKEMWYHN1P23DP14PHB">
  <span>Feature Names</span>
</h2>
<p>
  Currently, available features with consent control are as follows:
</p>
<pre>CLYConsentSessions<br>
CLYConsentEvents<br>
CLYConsentUserDetails<br>
CLYConsentCrashReporting<br>
CLYConsentPushNotifications<br>
CLYConsentLocation<br>
CLYConsentViewTracking<br>
CLYConsentAttribution<br>
CLYConsentPerformanceMonitoring<br>
CLYConsentFeedback<br>
CLYConsentRemoteConfig<br>
CLYConsentContent</pre>
<h2 id="h_01HAVQDM5V9TH7NQNWADXD7BS6">Setup During Init</h2>
<p>
  The requirement for consent is disabled by default. To enable it, you will have
  to set the <code>requiresConsent</code> flag <code>true</code> upon initial configuration
  to utilize consents.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.requiresConsent = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.requiresConsent = true</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">With this flag set, the Countly iOS SDK will not automatically collect or send any data and will ignore all manual calls. Until explicit consent is given for a feature, it will remain inactive. After consent for a feature is given, it will launch immediately and will remain active.<br>You can provide specific consents during initialization </span><span style="font-weight: 400;">by using the <code>consents</code>&nbsp;array on the <code>CountlyConfig</code> object before starting Countly</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.consents = @[CLYConsentSessions, CLYConsentEvents];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="objectivec">config.consents = [CLYConsentSessions, CLYConsentEvents];</code></pre>
  </div>
</div>
<p>
  Or, if you would like to give consent for all the features during initialization,
  you can set
  <span style="font-weight: 400;"><code>enableAllConsents</code> flag</span>:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <div class="tabs">
      <div class="tabs-menu">
        <span class="tabs-link is-active">Objective-C</span>
        <span class="tabs-link">Swift</span>
      </div>
      <div class="tab">
        <pre><code class="objectivec">config.enableAllConsents = YES;</code></pre>
      </div>
      <div class="tab is-hidden">
        <pre><code class="swift">config.enableAllConsents = true</code>&nbsp;</pre>
      </div>
    </div>
    <div>
      <h2 id="h_01HJ64PSQB64HGN27MYJFEV13M">
        <span>Changing Consent</span>
      </h2>
    </div>
  </div>
</div>
<p>
  <span style="font-weight: 400;">You can also change the consents after initializing the SDK.<br>To give consent for a feature, you can use the <code>giveConsentForFeature:</code></span><span style="font-weight: 400;">method by passing the feature name:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance giveConsentForFeature:CLYConsentSessions];
[Countly.sharedInstance giveConsentForFeature:CLYConsentEvents];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().giveConsent(forFeature: CLYConsentSessions)
Countly.sharedInstance().giveConsent(forFeature: CLYConsentEvents)</code></pre>
  </div>
</div>
<p>
  Or, you can give consent for more than one feature at a time using the
  <code>giveConsentForFeatures:</code>method or <code>consents</code> property
  on the <code>CountlyConfig</code> object, by passing the feature names as an
  <code>NSArray</code>:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance giveConsentForFeatures:@[CLYConsentSessions, CLYConsentEvents];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().giveConsent(forFeatures: [CLYConsentSessions, CLYConsentEvents])</code></pre>
  </div>
</div>
<p>
  Or, if you would like to give consent for all the features, you can use the
  <code>giveAllConsents</code>convenience method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance giveAllConsents];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().giveAllConsents()</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">The Countly iOS SDK does not persistently store the status of given consents. You are expected to handle receiving consent from end-users using proper UIs depending on your app's context. You are also expected to store them either locally or remotely. Following this step, you will need to call the ‘giving consent’ methods on each app launch, right after starting the Countly iOS SDK depending on the permissions you managed to get from the end-users.</span>
</p>
<p>
  <span style="font-weight: 400;">If the end-user changes his/her mind about consents at a later time, you will need to reflect this in the Countly iOS SDK using the <code>cancelConsentForFeature:</code></span><span style="font-weight: 400;">method:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance cancelConsentForFeature:CLYConsentSessions];
[Countly.sharedInstance cancelConsentForFeature:CLYConsentEvents];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().cancelConsent(forFeature: CLYConsentSessions)
Countly.sharedInstance().cancelConsent(forFeature: CLYConsentEvents)</code></pre>
  </div>
</div>
<p>
  Or, you can cancel consent for more than one feature at a time using the
  <code>cancelConsentForFeatures:</code>method by passing the feature names as
  an <code>NSArray</code>:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance cancelConsentForFeatures:@[CLYConsentSessions, CLYConsentEvents];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().cancelConsent(forFeatures: [CLYConsentSessions, CLYConsentEvents])</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Or, if you would like to cancel consent for all the features, you can use the <code>cancelConsentForAllFeatures</code></span><span style="font-weight: 400;">convenience method:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance cancelConsentForAllFeatures];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().cancelConsentForAllFeatures()</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Once consent for a feature has been cancelled, that feature is stopped immediately and kept inactive from that point onward.</span>
</p>
<p>
  <span style="font-weight: 400;">The Countly iOS SDK reports consent changes to the Countly Server, so that the Countly Server can make preparations, or clean-up on the server side as well.</span>
</p>
<h1 id="h_01HAVHW0RS0GVN3HY2JNXCJN01">Security and Privacy</h1>
<p>
  <span style="font-weight: 400;">You can specify extra security features on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object:</span>
</p>
<h2 id="h_01HAVHW0RSSS6ZX8ZXY9M87NKS">Parameter Tamper Protection</h2>
<p>
  <span style="font-weight: 400;">You can set the optional <code>secretSalt</code></span><span style="font-weight: 400;"> to be used for calculating the checksum of the request data which will be sent with each request using the <code>&amp;checksum256</code></span><span style="font-weight: 400;"> field. You will need to set the exact same <code>secretSalt</code></span><span style="font-weight: 400;">on the Countly Server. If the <code>secretSalt</code></span><span style="font-weight: 400;">on the Countly Server is set, all requests would be checked for validity of the <code>&amp;checksum256</code></span><span style="font-weight: 400;">field before being processed.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.secretSalt = @"mysecretsalt";</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.secretSalt = "mysecretsalt"</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RSD7WAN6T2EBBT7NHM">SSL Certificate Pinning</h2>
<p>
  <span style="font-weight: 400;">You can use optional <code>pinnedCertificates</code></span><span style="font-weight: 400;"> on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object for specifying bundled certificates to be used for public key pinning. Certificates from your Countly Server must be DER encoded and should have a <code>.der</code>, <code>.cer</code> or <code>.crt</code></span><span style="font-weight: 400;"> extension. They must also be added to your project and be included in the Copy Bundles Resources.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.pinnedCertificates = @[@"mycertificate.cer"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.pinnedCertificates = ["mycertificate.cer"]</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RSVZ8YYBMCN0EQ313W">Using a Self Signed-Server Certificate</h2>
<p>
  <span style="font-weight: 400;">You can set the <code>shouldIgnoreTrustCheck</code></span><span style="font-weight: 400;"> flag on the<code>CountlyConfig</code></span><span style="font-weight: 400;"> object before starting Countly. </span>
</p>
<p>
  This flag is used for ignoring all SSL trust check for pinned certificates by
  setting server trust as an exception.
</p>
<p>
  It can be used for self-signed certificates and works only for Development environment
  where <code>DEBUG</code> flag is set in target's build settings.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.shouldIgnoreTrustCheck = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.shouldIgnoreTrustCheck = true</code></pre>
  </div>
</div>
<h1 id="h_01HAVHW0RS3Z70B11ATKPVWYRH">Other Features and Notes</h1>
<h2 id="h_01HAVHW0RS8A28ZR4NNFVBTYFW">Changing Host and App Key</h2>
<h3 id="h_01HAVHW0RSTYDA6WQMK6X92ZC1">App Key</h3>
<h4 id="h_01HAVHW0RSNE3XTRZK1GNFG222">Changing App Key</h4>
<p>
  You can configure the current app key after you started the SDK using
  <code>setNewAppKey:</code>method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance setNewAppKey:@"NewAppKey"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().setNewAppKey("NewAppKey")</code></pre>
  </div>
</div>
<p>
  The new app key will be used for all the new requests after setting it. Requests
  already queued previously, will keep using the old app key. Before switching
  to new app key, this method suspends the SDK and resumes it immediately after
  the new key is set. The new app key needs to be a non-zero length string, otherwise
  the method call is ignored. <code>recordPushNotificationToken</code> and
  <code>updateRemoteConfigWithCompletionHandler:</code> methods may need to be
  manually called again after the app key change.
</p>
<h4 id="h_01HAVHW0RS4FSGF78WJJ2Y21G7">Replacing App Keys in Queue</h4>
<p>
  You can replace different app keys in the request queue with the current app
  key using <code>replaceAllAppKeysInQueueWithCurrentAppKey</code>method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance replaceAllAppKeysInQueueWithCurrentAppKey];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().replaceAllAppKeysInQueueWithCurrentAppKey()</code></pre>
  </div>
</div>
<p>
  In request queue, if there are any request whose app key is different than the
  current app key, these requests' app key will be replaced with the current app
  key.
</p>
<h4 id="h_01HAVHW0RSCXQESJD4G6S5AQA2">Removing App Keys from Queue</h4>
<p>
  You can remove requests whose app key is different than the current app key in
  the request queue using <code>removeDifferentAppKeysFromQueue</code>method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance removeDifferentAppKeysFromQueue];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().removeDifferentAppKeysFromQueue()</code></pre>
  </div>
</div>
<h3 id="h_01HAVHW0RSW5CZCMYF50V4MQJE">Host</h3>
<h4 id="h_01HAVHW0RSG07YWY5979AWDFRY">Changing Host</h4>
<p>
  You can configure the host even after you started the SDK using
  <code>setNewHost:</code>method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance setNewHost:@"https://example.com"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().setNewHost("https://example.com")</code></pre>
  </div>
</div>
<p>
  Requests that are already queued before changing the host will also be using
  the new host. The new host needs to be a non-zero length string, otherwise it
  is ignored. <code>recordPushNotificationToken</code> and
  <code>updateRemoteConfigWithCompletionHandler:</code> methods may need to be
  manually called again after the host change.
</p>
<p>
  <span style="font-weight: 400;">You can further specify your optional settings on the <code>CountlyConfig</code></span><span style="font-weight: 400;">:</span>
</p>
<h2 id="h_01HPE2F8MYP82AZ29EV7N8HQJ3">Example Integrations</h2>
<p>
  The Countly iOS example integrations are located
  <a href="https://github.com/Countly/countly-sample-ios">here</a>.
</p>
<p>
  <a href="https://github.com/Countly/countly-sample-ios/tree/master/ios-swift">ios-swift</a>
  project is written in Swift and covers basic functionalities.
</p>
<p>
  <a href="https://github.com/Countly/countly-sample-ios/tree/master/ios">ios</a>
  project is written in Objective-C and covers most of the functionalities
</p>
<p>
  <a href="https://github.com/Countly/countly-sample-ios/tree/master/macos">macos</a>
  project is written in Objective-C and covers basic functionalities.
</p>
<p>
  <a href="https://github.com/Countly/countly-sample-ios/tree/master/tvos">tvos</a>
  project is written in Objective-C and covers basic functionalities.
</p>
<p>
  <a href="https://github.com/Countly/countly-sample-ios/tree/master/watchos">watchos</a>
  project is written in Objective-C and covers basic functionalities.
</p>
<h2 id="h_01HAVHW0RSVHW5X7F0QA5BQJWR">Event Send Threshold</h2>
<p>
  <span style="font-weight: 400;">You can specify the <code>eventSendThreshold</code></span><span style="font-weight: 400;"> on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object before starting Countly. It is used to send </span><strong>events</strong><span style="font-weight: 400;"> requests to the server when the number of recorded events reaches the threshold without waiting for the next update session request. If the <code>eventSendThreshold</code></span><span style="font-weight: 400;"> is not explicitly set, the default setting will be at </span><strong>10</strong><span style="font-weight: 400;"> for iOS, tvOS &amp; macOS, and </span><strong>3</strong><span style="font-weight: 400;"> for watchOS.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.eventSendThreshold = 5;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.eventSendThreshold = 5</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RS3K48SBK4N6X7JV2G">Setting Maximum Request Queue Size</h2>
<p>
  You can specify the <code>storedRequestsLimit</code> on the
  <code>CountlyConfig</code> object before starting Countly. It is used to limit
  the number of requests in the request queue when there is a Countly Server connection
  problem. If your Countly Server is down, queued requests can reach excessive
  numbers, causing delivery problems to the server and requests stored on the device.
  To prevent this from happening, the Countly iOS SDK will only store requests
  up to the <code>storedRequestsLimit</code>. If the number of stored requests
  reaches the <code>storedRequestsLimit</code>, the Countly iOS SDK will start
  to drop the oldest requests, storing the newest ones in their place. If the
  <code>storedRequestsLimit</code> is not explicitly set, the default setting will
  be at <strong>1,000</strong>.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.storedRequestsLimit = 5000;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.storedRequestsLimit = 5000</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RSESJ7AQ3XCKCA48X2">Always using the POST method</h2>
<p>
  <span style="font-weight: 400;">You can set the <code>alwaysUsePOST</code></span><span style="font-weight: 400;"> flag on the<code>CountlyConfig</code></span><span style="font-weight: 400;"> object before starting Countly. This flag is used for sending all requests using the HTTP POST method, regardless of their data size. If set, all requests will be sent using the HTTP POST method. Otherwise, only the requests with a file upload or data size of more than 2,048 bytes will be sent using the HTTP POST method.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.alwaysUsePOST = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.alwaysUsePOST = true</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RSY3ZX1QB701E8XS44">Custom URLSessionConfiguration</h2>
<p>
  For additional networking settings, you can optionally set a custom
  <span style="font-weight: 400;"><code>URLSessionConfiguration</code></span>
  <span style="font-weight: 400;">on the <code>CountlyConfig</code></span><span style="font-weight: 400;"> object,</span>
  to be used with all requests sent to Countly Server.
</p>
<p>
  <span>If <span style="font-weight: 400;"><code>URLSessionConfiguration</code> is </span>not set, <span style="font-weight: 400;"><code>NSURLSessionConfiguration</code>'s <code>defaultSessionConfiguration</code></span></span><span> will be used by default.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.URLSessionConfiguration = NSURLSessionConfiguration.ephemeralSessionConfiguration;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre>config.URLSessionConfiguration = URLSessionConfiguration.ephemeral</pre>
  </div>
</div>
<p>
  In addition to the initial configuration, you can also change URLSessionConfiguration
  later using:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance setNewURLSessionConfiguration:newURLSessionConfiguration];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre>Countly.sharedInstance().setNewURLSessionConfiguration(newURLSessionConfiguration)</pre>
  </div>
</div>
<h2 id="h_01HAVHW0RSMH9JXDSWXR3H7A4Z">Custom Metrics</h2>
<p>
  For overriding default metrics or adding extra ones that are sent with
  <span style="font-weight: 400;"><code><span>begin_session</span></code></span>
  requests, you can use
  <span style="font-weight: 400;"><code><span>customMetrics</span></code><span>dictionary on the </span><code>CountlyConfig</code><span> </span><span>object.</span></span>
</p>
<p>
  Custom metrics should be an
  <span style="font-weight: 400;"><code><span>NSDictionary</span></code></span><span>,</span>
  with keys and values are both
  <span style="font-weight: 400;"><code><span>NSString</span></code></span> 's
  only.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.customMetrics = @{@"key": @"value"};</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.customMetrics = ["key": "value"];</code></pre>
  </div>
</div>
<div class="tabs-menu">
  <p>
    For overriding default metrics, keys should be
    <span>one of the <span style="font-weight: 400;"><code>CLYMetricKey</code></span> </span>'s:
  </p>
  <pre>CLYMetricKeyDevice<br>CLYMetricKeyOS<br>CLYMetricKeyOSVersion<br>CLYMetricKeyAppVersion<br>CLYMetricKeyCarrier<br>CLYMetricKeyResolution<br>CLYMetricKeyDensity<br>CLYMetricKeyLocale<br>CLYMetricKeyHasWatch<br>CLYMetricKeyInstalledWatchApp</pre>
</div>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.customMetrics = @{CLYMetricKeyAppVersion: @"1.2.3"};</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.customMetrics = [CLYMetricKeyAppVersion: "1.2.3"];</code></pre>
  </div>
</div>
<h2 id="h_01HTPANJCZGDCJS92XQZV69AY7">SDK Internal Limits</h2>
<p>
  Countly SDKs have internal limits to prevent users from unintentionally sending
  large amounts of data to the server. If these limits are exceeded, the data will
  be truncated to keep it within the limit. You can check the exact parameters
  these limits effect from
  <a href="/hc/en-us/articles/9290669873305#sdk_internal_limits" target="_blank" rel="noopener noreferrer">here</a>.
</p>
<h3 id="h_01HTPANJCZTKQVAMJ1A2YSYGNE">Key Length</h3>
<p>
  Limits the maximum size of all user set keys (default: 128 chars):
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[config.sdkInternalLimits setMaxKeyLength:150];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.sdkInternalLimits().setMaxKeyLength(150);</code></pre>
  </div>
</div>
<h3 id="h_01HTPANJCZCDKSFEM7NHK4PYPZ">Value Size</h3>
<p>
  Limits the size of all user set string segmentation (or their equivalent) values
  (default: 256 chars):
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[config.sdkInternalLimits setMaxValueSize:200];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.sdkInternalLimits().setMaxValueSize(200);</code></pre>
  </div>
</div>
<h3 id="h_01HTPANJCZRWRYPYQM1RQF4V0S">Segmentation Values</h3>
<p>
  Limits the amount of user set segmentation key-value pairs (default: 100 entries):
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[config.sdkInternalLimits setMaxSegmentationValues:120];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.sdkInternalLimits().setMaxSegmentationValues(120);</code></pre>
  </div>
</div>
<h3 id="h_01HTPANJCZ4VVWKTEEYYJ9D050">Breadcrumb Count</h3>
<p>
  Limits the amount of user set breadcrumbs that can be recorded (default: 100
  entries, exceeding this deletes the oldest one):
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[config.sdkInternalLimits setMaxBreadcrumbCount:120];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.sdkInternalLimits().setMaxBreadcrumbCount(120);</code></pre>
  </div>
</div>
<h3 id="h_01HTPANJCZT9A7GMK5D8EQXSPY">Stack Trace Lines Per Thread</h3>
<p>
  Limits the stack trace lines that would be recorded per thread (default: 30 lines):
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[config.sdkInternalLimits setMaxStackTraceLinesPerThread:50];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.sdkInternalLimits().setMaxStackTraceLinesPerThread(50);</code></pre>
  </div>
</div>
<h3 id="h_01HTPANJCZPFVMF36BZSNNQWFX">Stack Trace Line Length</h3>
<p>
  Limits the characters that are allowed per stack trace line (default: 200 chars):
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[config.sdkInternalLimits setMaxStackTraceLineLength:300];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.sdkInternalLimits().setMaxStackTraceLineLength(300);</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RSTYHES6WSX8Z80BQ6">Attribution</h2>
<h3 id="h_01HAVHW0RSD4315V1VW115EWVS">Direct Attribution</h3>
<p>
  You can record direct attribution with campaign type and data.<br>
  Currently supported campaign types are <code>countly</code> and
  <code>_special_test</code>.<br>
  Campaign data has to be JSON string in
  <code>{"cid":"CAMPAIGN_ID", "cuid":"CAMPAIGN_USER_ID"}</code> format.<br>
  Calls to this method will be ignored if consent for
  <code>CLYConsentAttribution</code> is not given, while
  <code>requiresConsent</code> flag is set on initial configuration.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSString* campaignData = @"{\"keyA\":\"valueA\",\"keyB\":\"valueB\"}";
[Countly.sharedInstance recordDirectAttributionWithCampaignType:@"countly" andCampaignData:campaignData];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let campaignData = "{\"keyA\":\"valueA\",\"keyB\":\"valueB\"}"
Countly.sharedInstance().recordDirectAttribution(withCampaignType: "countly", andCampaignData: campaignData)</code></pre>
  </div>
</div>
<h3 id="h_01HAVHW0RTE42W5VGDKMNPSNN3">Indirect Attribution</h3>
<p>
  You can record indirect attribution with given key-value pairs.<br>
  Keys could be a predefined <code>CLYAttributionKeyIDFA</code> or
  <code>CLYAttributionKeyADID</code> or any non-zero length valid string.<br>
  Calls to this method will be ignored if consent for
  <code>CLYConsentAttribution</code> is not given, while
  <code>requiresConsent</code> flag is set on initial configuration.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance recordIndirectAttribution:@{CLYAttributionKeyADID: @"value", @"key1": @"value1", @"key2": @"value2"}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().recordIndirectAttribution([CLYAttributionKey.ADID.rawValue: "value", "key1": "value1", "key2": "value2"])</code></pre>
  </div>
</div>
<p>
  For obtaining IDFA please see:
  <a href="https://developer.apple.com/documentation/adsupport/asidentifiermanager/1614151-advertisingidentifier?language=objc">https://developer.apple.com/documentation/adsupport/asidentifiermanager/1614151-advertisingidentifier?language=objc</a>
</p>
<p>
  And for App Tracking Transparency permission required on iOS 14.5+ please see:
  <a href="https://developer.apple.com/documentation/apptrackingtransparency?language=objc">https://developer.apple.com/documentation/apptrackingtransparency?language=objc</a>
</p>
<h2 id="h_01JXEX7QAQ3CGTE7QE9SR5GACD">Interacting with the Internal Request Queue</h2>
<p>
  When recording events or user activities, requests are not always sent to the
  server immediately. They may be batched together for efficiency or delayed due
  to lack of network connectivity.
</p>
<p>
  Currently, there are two ways to interact with this internal request queue:
</p>
<p>
  You can force the SDK to try to send the requests immediately:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance attemptToSendStoredRequests];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().attemptToSendStoredRequests()</code></pre>
  </div>
</div>
<p>
  This approach bypasses the SDK’s internal scheduling mechanisms and initiates
  an immediate attempt to send all queued requests.
</p>
<p>
  In certain situations, you may need to delete all stored requests from the queue.
  To do so, invoke the following method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance flushQueues];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().flushQueues()</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RTA5BP4D191447F3TT">Direct Request</h2>
<p>
  The <code>addDirectRequest</code> method allows you to send custom key/value
  pairs directly to your Countly server. This method accepts a dictionary with
  string key/value pairs as its parameter. In order to use this method effectively,
  you will need to convert any data that you wish to send (such as dictionaries
  or arrays) into a URL encoded string before passing it to the method.
</p>
<p>
  Here is a detailed example usage of <code>addDirectRequest</code>:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec" data-stringify-type="pre">- (void) sendDirectRequest {
  NSMutableDictionary *requestMap = [[NSMutableDictionary alloc] init];
  requestMap[@"city"] = @"Istanbul";
  requestMap[@"country_code"] = @"TR";
  requestMap[@"ip_address"] = @"41.0082,28.9784";

  NSMutableDictionary *event = [[NSMutableDictionary alloc] init];
  event[@"key"] = @"test";
  event[@"count"] = @"201";
  event[@"sum"] =  @"2010";
  event[@"dur"] = @"2010";

  NSMutableDictionary *ffJson = [[NSMutableDictionary alloc] init];
  ffJson[@"type"] = @"FF";
  ffJson[@"start_time"] = [NSNumber numberWithInt:123456789];
  ffJson[@"end_time"] = [NSNumber numberWithInt:123456789];


  NSMutableDictionary *skipJson = [[NSMutableDictionary alloc] init];
  skipJson[@"type"] = @"skip";
  skipJson[@"start_time"] = [NSNumber numberWithInt:123456789];
  skipJson[@"end_time"] = [NSNumber numberWithInt:123456789];

  NSMutableDictionary *resumeJson = [[NSMutableDictionary alloc] init];
  resumeJson[@"type"] = @"resume_play";
  resumeJson[@"start_time"] = [NSNumber numberWithInt:123456789];
  resumeJson[@"end_time"] = [NSNumber numberWithInt:123456789];

  NSMutableArray *trickPlay = [[NSMutableArray alloc] init];
  [trickPlay addObject:ffJson];
  [trickPlay addObject:skipJson];
  [trickPlay addObject:resumeJson];


  NSMutableDictionary *segmentation = [[NSMutableDictionary alloc] init];
  segmentation[@"trickplay"] =  trickPlay;
  event[@"segmentation"] = segmentation;

  NSMutableArray *events = [[NSMutableArray alloc] init];
  [events addObject:event];

  NSString *eventsString = [self toString:events];

  requestMap[@"events"]  = eventsString.cly_URLEscaped;
  [Countly.sharedInstance addDirectRequest:requestMap];   
}

- (NSString *) toString: (id) dictionaryOrArrayToOutput  {
  NSError *error;
  NSData *jsonData = [NSJSONSerialization dataWithJSONObject:dictionaryOrArrayToOutput
                                                     options:0
                                                       error:&amp;error];
  NSString *jsonString = @"";
  if (! jsonData) {
    NSLog(@"Got an error: %@", error);

  } else {
    jsonString = [[NSString alloc] initWithData:jsonData encoding:NSUTF8StringEncoding];
  }
  return jsonString;
}</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">func sendDirectRequest() {
    var requestMap = [String: Any]()
    requestMap["city"] = "Istanbul"
    requestMap["country_code"] = "TR"
    requestMap["ip_address"] = "41.0082,28.9784"

    var event = [String: Any]()
    event["key"] = "test"
    event["count"] = "201"
    event["sum"] =  "2010"
    event["dur"] = "2010"

    var ffJson = [String: Any]()
    ffJson["type"] = "FF"
    ffJson["start_time"] = NSNumber(value: 123456789)
    ffJson["end_time"] = NSNumber(value: 123456789)

    var skipJson = [String: Any]()
    skipJson["type"] = "skip"
    skipJson["start_time"] = NSNumber(value: 123456789)
    skipJson["end_time"] = NSNumber(value: 123456789)

    var resumeJson = [String: Any]()
    resumeJson["type"] = "resume_play"
    resumeJson["start_time"] = NSNumber(value: 123456789)
    resumeJson["end_time"] = NSNumber(value: 123456789)

    var trickPlay = [[String: Any]]()
    trickPlay.append(ffJson)
    trickPlay.append(skipJson)
    trickPlay.append(resumeJson)

    var segmentation = [String: Any]()
    segmentation["trickplay"] =  trickPlay
    event["segmentation"] = segmentation

    var events = [[String: Any]]()
    events.append(event)

    let eventsString = toString(dictionaryOrArrayToOutput: events)

    if let eventsEscaped = eventsString.addingPercentEncoding(withAllowedCharacters: .urlQueryAllowed) {
        requestMap["events"] = eventsEscaped
        Countly.sharedInstance()?.addDirectRequest(requestMap)
    }
}

func toString(dictionaryOrArrayToOutput: Any) - String {
    var jsonString = ""
    do {
        let jsonData = try JSONSerialization.data(withJSONObject: dictionaryOrArrayToOutput, options: [])
        jsonString = String(data: jsonData, encoding: .utf8) ?? ""
    } catch let error {
        print("Got an error: \(error)")
    }
    return jsonString
}

    </code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RTPMZFEQGNNNR3ERYK">watchOS Integration</h2>
<p>
  <span style="font-weight: 400;">Just like iPhones and iPads, collecting and analyzing usage statistics and analytics data from an Apple Watch is the key for offering a better experience. Fortunately, the Countly iOS SDK has watchOS support. Here you can find out how to use the Countly iOS SDK in your watchOS apps:</span>
</p>
<p>
  <strong>1.</strong>
  <span style="font-weight: 400;">First, open a new or your existing Xcode project and add a new target by clicking the + icon at the bottom of the Projects and Targets List. (You can skip to the step 4 if your project already has a Watch App, or you can visit </span><a href="https://apple.co/1PnD1uT"><span style="font-weight: 400;">https://apple.co/1PnD1uT</span></a><span style="font-weight: 400;"> for more information)</span>
</p>
<p>
  <strong>2.</strong>
  <span style="font-weight: 400;">Select the target template WatchKit App under the watchOS &gt; Application section. Do not choose the WatchKit App for watchOS 1. In order to keep things simple, do not include the Notification scene, Glance scene, or Complication.</span>
</p>
<p>
  <strong>3.</strong>
  <span style="font-weight: 400;">If Xcode asks whether you would like to activate the WatchKit App scheme, click Activate.</span>
</p>
<p>
  <strong>4.</strong>
  <span style="font-weight: 400;">Now it is time to add the Countly iOS SDK to your project. After cloning the Countly iOS SDK anywhere you would like, Drag&amp;Drop <code>.h</code> and <code>.m</code> files in <code>countly-sdk-ios</code></span><span style="font-weight: 400;"> folder into your Xcode project, and in the following dialog, please ensure the iPhone app target and </span><strong>WatchKit Extension</strong><span style="font-weight: 400;"> target (not WatchKit App) have been selected as well as the </span><strong>Copy items if needed</strong><span style="font-weight: 400;"> checkbox.</span>
</p>
<div class="img-container">
  <img src="https://archive.count.ly/images/guide/SvLcZmJTQPKXYWtkXdLn_hcHj93L.png">
</div>
<p>
  <strong>5.</strong> Import <code>Countly.h</code> into
  <code>ExtensionDelegate.m</code>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">#import "Countly.h"</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">// No need to import files for Swift projects</code></pre>
  </div>
</div>
<p>
  <strong>6.</strong> Add the Countly starting code into the
  <code>applicationDidFinishLaunching</code> method of<code>ExtensionDelegate.m</code>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">CountlyConfig* config = CountlyConfig.new;
config.appKey = @"YOUR_APP_KEY";
config.host = @"https://YOUR_COUNTLY_SERVER";
[Countly.sharedInstance startWithConfig:config];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let config: CountlyConfig = CountlyConfig()
config.appKey = "YOUR_APP_KEY"
config.host = "https://YOUR_COUNTLY_SERVER"
Countly.sharedInstance().start(with: config)</code></pre>
  </div>
</div>
<p>
  <strong>7.</strong> Add suspend code into the
  <code>applicationWillResignActive</code> method of
  <code>ExtensionDelegate.m</code>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance suspend];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().suspend()</code></pre>
  </div>
</div>
<p>
  <strong>8.</strong> Add resume code into the
  <code>applicationDidBecomeActive</code> method of
  <code>ExtensionDelegate.m</code>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance resume];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().resume()</code></pre>
  </div>
</div>
<p>
  <strong>9.</strong>
  <span style="font-weight: 400;">After adding these three lines of code into the related extension delegate methods, try building the project. Everything should be OK now. If you run the watchOS app, you can see the session on your Countly dashboard.</span>
</p>
<p>
  <span style="font-weight: 400;">Now you are ready to track your watchOS app with Countly.</span>
</p>
<p>
  <span style="font-weight: 400;">By the way, the session concept on watchOS is slightly different than the one on the iOS, as watchOS apps are intended for brief user interaction. So, there are two values you might need to adjust depending on your watch apps’ use cases.</span>
</p>
<ul>
  <li>
    <span style="font-weight: 400;">The first value is <code>updateSessionPeriod</code></span><span style="font-weight: 400;">. Its default value is </span><strong>20</strong><span style="font-weight: 400;"> seconds for watchOS and </span><strong>60</strong><span style="font-weight: 400;"> seconds for iOS. This value determines how often session updating requests will be sent to the server while the app is in use.</span>
  </li>
  <li>
    <span style="font-weight: 400;">The second value is <code>eventSendThreshold</code></span><span style="font-weight: 400;">, which is </span><strong>3</strong><span style="font-weight: 400;"> for watchOS and </span><strong>10</strong><span style="font-weight: 400;"> for iOS by default. The Countly iOS SDK waits for the number of recorded unique events to reach this threshold to deliver them to the server until the next session updating kicks in. Considering the fact that Apple Watch is designed to be used for short sessions, these values generally seem appropriate. However, you can change them depending on your watchOS app’s scenario.</span>
  </li>
</ul>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.updateSessionPeriod = 15;
config.eventSendThreshold = 1;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.updateSessionPeriod = 15
config.eventSendThreshold = 1</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RT4ZHQVYMK1GV1WW2T">Automatic Reference Counting (ARC)</h2>
<p>
  <span style="font-weight: 400;">The Countly iOS SDK uses Automatic Reference Counting (ARC). If you are integrating the Countly iOS SDK into a non-ARC project, you should add the<code>-fobjc-arc</code></span><span style="font-weight: 400;"> compiler flag to all Countly iOS SDK implementation (<code>*.m</code></span><span style="font-weight: 400;">) files found under <code>Target</code> &gt; <code>Build Phases</code> &gt; <code>Compile Sources</code></span><span style="font-weight: 400;">.</span>
</p>
<h2 id="h_01HAVHW0RTCEGRMYGJX0C4HCX4">App Transport Security (ATS)</h2>
<p>
  <span style="font-weight: 400;">With </span><strong>App Transport Security</strong><span style="font-weight: 400;"> introduced in iOS 9, connections to non-HTTPS servers which does not meet some requirements will fail with the following error: <code>Error: Error Domain=NSURLErrorDomain Code=-1022 "The resource could not be loaded because the App Transport Security policy requires the use of a secure connection."</code>. You can see details of the requirements </span><a href="https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14"><span style="font-weight: 400;">here</span></a><span style="font-weight: 400;">. If your Countly Server instance does not meet these requirements, you can need to add the <code>NSAppTransportSecurity</code></span><span style="font-weight: 400;"> key into your targets' <code>Info.plist</code></span><span style="font-weight: 400;"> files, with <code>NSAllowsArbitraryLoads</code> or <code>NSExceptionDomains</code></span><span style="font-weight: 400;"> as the value, to communicate with your Countly Server.</span>
</p>
<h2 id="h_01HAVHW0RT9DP8543XYWP278JC">Swift Projects</h2>
<p>
  <span style="font-weight: 400;">For using Countly on Swift based projects, please ensure your Bridging Header File is configured properly for each target. Then import the <code>Countly.h</code></span><span style="font-weight: 400;"> file into the Bridging Header file, after which you can seamlessly use the Countly methods in your Swift projects.</span>
</p>
<p>
  <span style="font-weight: 400;">For Notification Service Extension targets, import <code>CountlyNotificationService.h</code></span><span style="font-weight: 400;"> into the Bridging Header file.</span>
</p>
<p>
  <span style="font-weight: 400;">You can view more details on how to create a Bridging Header file </span><a href="https://developer.apple.com/library/content/documentation/Swift/Conceptual/BuildingCocoaApps/MixandMatch.html#//apple_ref/doc/uid/TP40014216-CH10-ID126"><span style="font-weight: 400;">here</span></a><span style="font-weight: 400;">.</span>
</p>
<h2 id="h_01HAVHW0RTK6MM64GQJB5Y6N7B">Updating the Countly iOS SDK</h2>
<p>
  <span style="font-weight: 400;">Before upgrading to a new version of the Countly iOS SDK, do not forget to remove the existing files from your project first. Then, while adding the new Countly iOS SDK files again, please ensure you have chosen the targets correctly and select the "Copy items if needed" checkbox.</span>
</p>
<h2 id="h_01HAVHW0RTXSFZD8R6QMX0GWPN">CocoaPods</h2>
<div class="callout callout--warning">
  <strong>CocoaPods Support</strong>
  <p>
    While the Countly iOS SDK supports integration via CocoaPods, we can not
    be able to help you with issues stemming from the CocoaPods itself, especially
    for some advanced use-cases.
  </p>
</div>
<p>
  <span style="font-weight: 400;">You can integrate the Countly iOS SDK using CocoaPods. For more information, please see the </span><a href="https://cocoapods.org/pods/Countly"><span style="font-weight: 400;">Countly CocoaPods page</span></a><span style="font-weight: 400;">. Please ensure you have the latest version of CocoaPods and your local spec repo is updated. For Notification Service Extension targets, please ensure your Podfile uses something similar to the following sub specs:</span>
</p>
<pre><code class="ruby">target 'MyMainApp' do
  platform :ios,'10.0'
  pod 'Countly'
end

target 'CountlyNSE' do
  platform :ios,'10.0'
  pod 'Countly/NotificationService'
end</code></pre>
<p>
  For Swift projects with Notification Service Extension, please see:
  <a href="https://github.com/Countly/countly-sample-ios/issues/13#issuecomment-408652426">https://github.com/Countly/countly-sample-ios/issues/13#issuecomment-408652426</a>
</p>
<p>
  <span style="font-weight: 400;">For Crash Reporting automatic dSYM uploading, please manually add the </span><a href="https://github.com/Countly/countly-sdk-ios/blob/master/countly_dsym_uploader.sh"><span style="font-weight: 400;">dSYM uploader script</span></a><span style="font-weight: 400;"> to your project.</span>
</p>
<h2 id="h_01HAVHW0RTQGRSE9ZRVQSAXJ74">Carthage</h2>
<p>
  <span style="font-weight: 400;">You can integrate the Countly iOS SDK using Carthage, just add the following to your project's Cartfile:</span>
</p>
<pre><code class="text">github "Countly/countly-sdk-ios"</code></pre>
<h2 id="h_01HAVHW0RTQ6WN8CYVNVZQ5TEP">Swift Package Manager (SPM)</h2>
<p>
  You can integrate the Countly iOS SDK with Swift Package Manager (SPM) using
  https://github.com/Countly/countly-sdk-ios.git repository URL. Open your XCode
  and go to File &gt; Add Packages and enter the URL into the search bar. From
  here you can add the package by targeting the master branch.
</p>
<h2 id="h_01J7191100003PJ0HZHYR8GS5B">Content Zone</h2>
<p>
  The Content Zone feature enhances user engagement by delivering various types
  of content blocks, such as in-app messaging, ads, or user engagement prompts.
  These content blocks are dynamically served from the content builder on the server,
  ensuring that users receive relevant and up-to-date information.
</p>
<div class="callout callout--info">
  <p>
    For learning how you can use Journeys &amp; Content Builder to create In-App
    messages you can check
    <a href="/hc/en-us/articles/18995770340380" target="_blank" rel="noopener noreferrer">this</a>
    article.
  </p>
</div>
<p>
  To start fetching content from the server, use the following method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.content enterContentZone];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().content().enterContentZone();</code></pre>
  </div>
</div>
<p>
  This call will retrieve and display any available content for the user. It will
  also regularly check if a new content is available, and if it is, will fetch
  and show it to the user.
</p>
<p>
  This regular check happens in every 30 seconds by default. It could be configurable
  while initializing the SDK through and it must be greater than 15 seconds.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.content.zoneTimerInterval = 60;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="objectivec">config.content.zoneTimerInterval = 60</code></pre>
  </div>
</div>
<p>
  When you want to exit from content zone and stop SDK from checking for available
  content you can use this method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.content exitContentZone];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().content().exitContentZone();</code></pre>
  </div>
</div>
<p>
  To get informed when a user closes a content you can register a global content
  callback during SDK initialization:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[config.content setGlobalContentCallback:^(ContentStatus contentStatus, NSDictionary&lt;NSString *,id&gt; * _Nonnull contentData) {
      // do sth
    }];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.content().setGlobalContentCallback { contentStatus, contentData in
      // do something
    }</code></pre>
  </div>
</div>
<p>
  The `contentStatus` will indicate either `COMPLETED` or `CLOSED`.
</p>
<h2 id="h_01J719HZ10E9XGED23ZR74MWTA">Experimental Config</h2>
<p>
  The ConfigExperimental interface provides experimental configuration options
  for enabling advanced features like view name recording and visibility tracking.
  These features are currently in a testing phase and might change in future versions.
</p>
<p>This class allows enabling two experimental features:</p>
<ul>
  <li>Previous Name Recording</li>
  <li>Visibility Tracking</li>
</ul>
<p>
  When you enable previous name recording, it will add previous view name to the
  view segmentations (cly_pvn) and previous event name to the event segmentations
  (cly_pen).
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.experimental.enablePreviousNameRecording = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.experimental().enablePreviousNameRecording = true;</code></pre>
  </div>
</div>
<p>
  When you enable visibility tracking, it will add a parameter (cly_v) to each
  recorded event's segmentation about the visibility of the app at the time of
  its recording.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.experimental.enableVisibiltyTracking = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.experimental().enableVisibiltyTracking = true;</code></pre>
  </div>
</div>
<h2 id="h_01HAVHW0RT6Z24NQTD85KJP50H">A/B Testing Variant Information</h2>
<p>
  You can access all the A/B test variants for your Countly application within
  your mobile app. This information can be useful while testing your app with different
  variants. There are four calls you can use for fetching, accessing, and enrolling
  for your variants.
</p>
<h3 id="h_01HAVHW0RTBN3VQ8BPQW9D6BQN">Fetching Test Variants</h3>
<p>
  You can fetch a map of all A/B testing parameters (keys) and variants associated
  with it:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.remoteConfig testingDownloadVariantInformation:^(CLYRequestResult _Nonnull response, NSError *_Nonnull error) {
   // do sth
}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().remoteConfig.testingDownloadVariantInformation({ response, error in
   // do something
})</code></pre>
  </div>
</div>
<p>
  You must provide a callback to be called when the fetching process ends. Depending
  on the situation, this would return a RequestResponse Enum (Success, NetworkIssue,
  or Error) as the first parameter and a String error as the second parameter if
  there was an error ("null" otherwise).
</p>
<h3 id="h_01HAVHW0RTZN98VHNS4NYP16J1">Accessing Fetched Test Variants</h3>
<p>
  When test variants are fetched, they are stored in memory. As it is not stored
  persistently if the memory is erased (like in the case of an app restart), you
  must fetch the variants again. So a common flow is to use the fetched values
  right after fetching them. To access all fetched values, you can use:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSDictionary*allVariants = [Countly.sharedInstance.remoteConfig testingGetAllVariants];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let allVariants = Countly.sharedInstance().remoteConfig.testingGetAllVariants()
</code></pre>
  </div>
</div>
<p>
  This would return a dictionary where a test's parameter is associated with all
  variants under that parameter. The parameter would be the key, and its value
  would be a String Array of variants. For example:
</p>
<pre><code class="java">{
  "key_1" : ["variant_1", "variant_2"],
  "key_2" : ["variant_3"]
}
</code></pre>
<p>Or instead you can get the variants of a specific key:</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">NSArray* variants = [Countly.sharedInstance.remoteConfig testingGetVariantsForKey:key];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">let variants = Countly.sharedInstance().remoteConfig.testingGetVariants(for: key) as NSArray
</code></pre>
  </div>
</div>
<p>
  This would only return a String array of variants for that specific key. If no
  variants were present for a key, it would return an empty array. A typical result
  would look like this:
</p>
<pre><code class="java">["variant_1", "variant_2"]
</code></pre>
<h3 id="h_01HAVHW0RTE8E7S9NNFCAEQT2Z">Enrolling For a Variant</h3>
<p>
  After fetching A/B testing parameters and variants from your server, you next
  would like to enroll the user to a specific variant. To do this, you can use
  the following method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance.remoteConfig testingEnrollIntoVariant:key variantName:variantName completionHandler:^(CLYRequestResult _Nonnull response, NSError *_Nonnull error) {
   // do sth
}];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().remoteConfig.testingEnroll(intoVariant: key, variantName: variantName) { response, error in
   // do sth
}</code></pre>
  </div>
</div>
<p>
  Here the 'valueKey' would be the parameter of your A/B test, and 'variantName'
  is the variant you have fetched and selected to enroll for. The callback function
  is mandatory and works the same way as explained above in the Fetching Test Variants
  section.
</p>
<h2 id="h_01HD3ZJYNBDW19BCE6NM12HM7T">Drop Old Requests</h2>
<p>
  If you are concerned about your app being used sparsely over a long time frame,
  old requests inside the request queue might not be important. If, for any reason,
  you don't want to get data older than a certain timeframe, you can configure
  the SDK to drop old requests:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.setRequestDropAgeHours(10);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.setRequestDropAgeHours(10)</code></pre>
  </div>
</div>
<p>
  By using the <code>setRequestDropAgeHours</code> method while configuring the
  SDK initialization options, you can set a timeframe (in hours) after which the
  requests would be removed from the request queue. For example, by setting this
  option to 10, the SDK would ensure that no request older than 10 hours would
  be sent to the server.
</p>
<h2 id="h_01JCGJ63WGHR3V9XZQT89JVYFQ">Extended Device ID Management</h2>
<p>
  <span style="font-weight: 400;">You can use the <code>changeDeviceIDWithMerge:</code> or <code>changeDeviceIDWithoutMerge:</code></span><span style="font-weight: 400;"> method to change the device ID on runtime </span><strong>after you start Countly</strong><span style="font-weight: 400;">. You can either allow the device to be counted as a new device or merge existing data on the server.</span>
</p>
<p>
  <span style="font-weight: 400;">With this method <code>changeDeviceIDWithMerge:</code> the old device ID on the server will be replaced with the new one, and data associated with the old device ID will be merged automatically.<br>With <code>changeDeviceIDWithoutMerge:</code> a new device ID created on the server.</span>
</p>
<div class="callout callout--warning">
  <p>
    <strong>Performance risk.</strong> Changing device id with server merging
    results in huge load on server as it is rewriting all the user history. This
    should be done only once per user.
  </p>
</div>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">//change and merge on server
[Countly.sharedInstance changeDeviceIDWithMerge:@"new_device_id"];

//no replace and merge on server, device will be counted as new
[Countly.sharedInstance changeDeviceIDWithoutMerge:@"new_device_id"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">//replace and merge on server
Countly.sharedInstance().changeDeviceIDWithMerge("new_device_id")

//no replace and merge on server, device will be counted as new
Countly.sharedInstance().changeDeviceIDWithoutMerge("new_device_id")</code></pre>
  </div>
</div>
<h3 id="h_01JCGJD8TNSSNPV5DTYXEEFZX5">
  <span style="font-weight: 400;">Temporary Device ID</span>
</h3>
<p>
  You can use temporary device ID mode for keeping all requests on hold until the
  real device ID is set later. It can be enabled by setting
  <code>deviceID</code> on initial configuration as<code>CLYTemporaryDeviceID</code>:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">config.deviceID = CLYTemporaryDeviceID;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">config.deviceID = CLYTemporaryDeviceID</code></pre>
  </div>
</div>
<p>
  Or by passing as an argument for <code>deviceID</code> parameter on
  <code>changeDeviceIDWithoutMerge:</code>any time:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance changeDeviceIDWithoutMerge:CLYTemporaryDeviceID];<br></code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().changeDeviceIDWithoutMerge(CLYTemporaryDeviceID)</code></pre>
  </div>
</div>
<p>
  As long as the device ID value is <code>CLYTemporaryDeviceID</code>, the SDK
  will be in temporary device ID mode and all requests will be on hold, but they
  will be persistently stored.
</p>
<p>
  Later, when the real device ID is set using
  <span style="font-weight: 400;"> <code>changeDeviceIDWithMerge:</code> or <code>changeDeviceIDWithoutMerge:</code></span><span style="font-weight: 400;"></span>
  method, all requests which have been kept on hold until that point will start
  with the real device ID:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Objective-C</span>
    <span class="tabs-link">Swift</span><span style="background-color: #e9ebed; font-family: monospace, monospace; font-size: 13px; white-space: pre;"></span>
  </div>
  <div class="tab">
    <pre><code class="objectivec">[Countly.sharedInstance changeDeviceIDWithMerge:@"new_device_id"];<br><br>[Countly.sharedInstance changeDeviceIDWithoutMerge:@"new_device_id"];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="swift">Countly.sharedInstance().changeDeviceIDWithMerge("new_device_id")<br><br>Countly.sharedInstance().changeDeviceIDWithoutMerge("new_device_id")</code></pre>
  </div>
</div>
<p>
  <strong>Note:</strong> When setting real device ID while the current device ID
  is <code>CLYTemporaryDeviceID</code>, with merge or without merge&nbsp;does not
  matter.
</p>
<h1 id="frequently-asked-questions" class="anchor-heading" tabindex="-1">
  <span>FAQ</span>
</h1>
<p>
  This section highlights the most frequently asked questions and any troubleshooting
  queries you may face while integrating the Countly iOS SDK into your iOS, watchOS,
  tvOS, or macOS applications.
</p>
<h2 id="h_01HAVHW0RTVQS0Q754MQMZ6N9X">
  <span class="wysiwyg-color-black">What platforms does Countly iOS SDK support?</span>
</h2>
<p>
  <span class="wysiwyg-color-black">Even though its official name is Countly iOS SDK, it supports all Apple platforms (macOS, tvOS, and watchOS), in addition to iOS. You can use the same SDK for all kinds of projects with different sets of features available for each platform. You can also see how to integrate it into your projects by <a href="https://github.com/Countly/countly-sample-ios">checking our sample apps here</a>.</span>
</p>
<h2 id="h_01HAVHW0RTB1QKKPGRB97AYNZ9">
  <span class="wysiwyg-color-black">Which features are available for each platform?</span>
</h2>
<p>
  <span class="wysiwyg-color-black">In addition to Analytics, Events, and User Profiles features, Countly iOS SDK has Push Notifications, Crash Reporting, Auto View Tracking, Remote Config, and Star-Rating features. Availability of these features for platforms are as follows:</span>
</p>
<ul>
  <li>
    <p>
      <span class="wysiwyg-color-black">iOS</span><br>
      <span class="wysiwyg-color-black"><code>Analytics</code>, <code>Custom Events</code>, <code>User Profiles</code>, <code>Push Notifications</code>, <code>Crash Reporting</code>, <code>Auto View Tracking</code>, <code>Star-Rating</code>, <code>Remote Config</code>, </span>
    </p>
  </li>
  <li>
    <p>
      <span class="wysiwyg-color-black">macOS</span><br>
      <span class="wysiwyg-color-black"><code>Analytics</code>, <code>Custom Events</code>, <code>User Profiles</code>, <code>Push Notifications</code>,<code>Crash Reporting</code>, <code>Remote Config</code>, </span>
    </p>
  </li>
  <li>
    <p>
      <span class="wysiwyg-color-black">tvOS</span><br>
      <span class="wysiwyg-color-black"><code>Analytics</code>, <code>Custom Events</code>, <code>User Profiles</code>, <code>Auto View Tracking</code>,<code>Crash Reporting</code>, <code>Remote Config</code>, </span>
    </p>
  </li>
  <li>
    <p>
      <span class="wysiwyg-color-black">watchOS</span><br>
      <span class="wysiwyg-color-black"><code>Analytics</code>, <code>Custom Events</code>, <code>User Profiles</code>, <code>Crash Reporting</code>,<code>Remote Config</code>, </span>
    </p>
  </li>
</ul>
<h2 id="h_01HAVHW0RTFFZZ203T8BBSX3XZ">
  <span class="wysiwyg-color-black">Can I integrate Countly iOS SDK using CocoaPods?</span>
</h2>
<p>
  <span class="wysiwyg-color-black">We keep our <code>Countly.podspec</code> file up-to-date, so you can integrate Countly iOS SDK using CocoaPods. But, please make sure you <a href="#h_01HAVHW0RTXSFZD8R6QMX0GWPN">read our notes</a> to avoid issues.</span>
</p>
<h2 id="h_01HAVHW0RTR6D4DH3VNENYY5C4">
  <span class="wysiwyg-color-black">How can I tell which Countly iOS SDK version I am using?</span>
</h2>
<p>
  <span class="wysiwyg-color-black">You can check for <code>kCountlySDKVersion</code> constant in Countly iOS SDK source. It is defined as <code>NSString* const kCountlySDKVersion = @"18.08";</code></span>
</p>
<h2 id="h_01HAVHW0RTGZSGY2SKAE3EXDSQ">
  <span class="wysiwyg-color-black">What is the difference between Default properties and Custom properties of User Profiles?</span>
</h2>
<p>
  <span class="wysiwyg-color-black">User Profiles <em>(only available in Enterprise Edition)</em> has two kinds of properties: Default properties and Custom properties.</span>
</p>
<p>
  <span class="wysiwyg-color-black">Default properties are predefined fields like <code>name</code>, <code>username</code>, <code>email</code>, <code>birth year</code>, <code>organization</code>, <code>gender</code>, <code>phone number</code> and <code>profile picture</code>. They are displayed in their own place in User Profiles section. You can set them using default properties on <code>Countly.user</code> singleton ( Ex: <code>Countly.user.email = @"john@doe.com";</code> ) and record them using <code>[Countly.user save];</code> method.</span>
</p>
<p>
  <span class="wysiwyg-color-black">Custom properties are custom defined key-value pairs. You can set them using <code>Countly.user.custom</code> dictionary ( Ex: <code>Countly.user.custom = @{@"testkey1":@"testvalue1", @"testkey2":@"testvalue2"};</code> ) and record them using <code>[Countly.user save];</code> method as well.</span>
</p>
<p>
  <span class="wysiwyg-color-black">In addition to this, you can use Custom Property Modifiers to set, unset or modify Custom Properties and record your changes using <code>[Countly.user save];</code> method again.</span>
</p>
<p>
  <span class="wysiwyg-color-black">For details please see <a href="#h_01HAVHW0RRRH4M1Y4CDJSHGERJ">User Profiles documentation</a>.</span>
</p>
<h2 id="h_01HAVHW0RTF435Z2N9WTK4BEBD">
  <span class="wysiwyg-color-black">How can I handle logged in and logged out users?</span>
</h2>
<p>
  <span class="wysiwyg-color-black">When a user logs in on your app and you have a uniquely identifiable string for that user (like user ID or email address), you can use it instead of device ID to track all info afterwards, without losing all the data generated by that user so far. You can use <span style="font-weight: 400;"><code>changeDeviceIDWithMerge:</code></span>method ( Ex: <code>[Countly.sharedInstance changeDeviceIDWithMerge:@"user123@example.com"];</code> ). This will replace previously used device ID on device, and merge all existing data on server.</span>
</p>
<h2 id="h_01HAVHW0RT68DJT106RB577FXG">
  <span class="wysiwyg-color-black">Why are events not displayed on Countly Server dashboard?</span>
</h2>
<p>
  <span class="wysiwyg-color-black">Events are queued but not sent to server until next <code>updateSessionPeriod</code> (60 seconds by default) or <code>eventSendThreshold</code> (10 by default) is reached. So, a little delay may be expecting in displaying events on Countly Server dashboard, while still seeing session data immediately.</span>
</p>
<p>
  <span class="wysiwyg-color-black">In addition to this, Countly iOS SDK sends previously stored requests, if any, followed by a <code>begin_session</code> request, when it starts. If your app records any events meanwhile, these events will be queued and sent to server when all previously queued requests are successfully completed.</span>
</p>
<h2 id="h_01HAVHW0RTFTH1ZZVAEEBTHP4P">
  <span class="wysiwyg-color-black">Is it possible to use Countly iOS SDK with another crash SDK?</span>
</h2>
<p>
  <span class="wysiwyg-color-black">In iOS there can only be one uncaught exception handler. Even though it is possible to save the previous handler and pass the uncaught exception to the previous handler as well, it is not safe to assume that it will work in all cases. We do not know how other SDKs are implemented or whether iOS will give enough time for the all the handlers to do their work before terminating the app, hence, we advise to use Countly as the only crash handler.</span>
</p>
<h2 id="h_01HAVHW0RT7FTCGJN48SMJ4FEG">
  <span class="wysiwyg-color-black">Why are my test crashes not reported?</span>
</h2>
<p>
  <span class="wysiwyg-color-black">If you are running your app with Xcode debugger attached while forcing a test crash, Countly iOS SDK cannot handle the crash as debugger will be intercepting. Please make sure you run your app without Xcode debugger attached.</span>
</p>
<h2 id="h_01HAVHW0RT8HE0A761YAPH8QS9">
  <span class="wysiwyg-color-black">How can I manually record push notification custom button actions?</span>
</h2>
<p>
  <span class="wysiwyg-color-black">If you have set <code>doNotShowAlertForNotifications</code> flag on initial configuration object to handle push notifications manually, you can create your own custom UI to show notification message and action buttons. For this, just implement <code>- (void) application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler</code> method in your application's delegate. For details of handling notification manually, please see <a href="#h_01HAVHW0RQRHJ27TXHTTZ0F82M">Handling Notifications Manually</a> section.</span>
</p>
<h2 id="h_01HAVHW0RTVFVX2KYZBY7NS2G4">
  <span class="wysiwyg-color-black">How can I get rid of compiler warning "No rule to process file"?</span>
</h2>
<p>
  <span class="wysiwyg-color-black">If you get <code>Warning: no rule to process file '../countly-sdk-ios/README.md' of type net.daringfireball.markdown for architecture arm64</code> in Xcode, it means <code>README.md</code> (and/or <code>CHANGELOG.md</code>) file is added to <code>Build Phases &gt; Compile Sources</code> in your target. Please remove <code>README.md</code> from <code>Compile Sources</code> list.</span>
</p>
<h2 id="h_01HAVHW0RT6JAKSEHA94YWJW23">
  <span class="wysiwyg-color-black">How is Countly affected by Apple's App Tracking Transparency changes?</span>
</h2>
<p>
  <span class="wysiwyg-color-black">As Countly is not and has never been doing any tracking, it is not affected by Apple's App Tracking Transparency changes. </span>
</p>
<p>
  <span class="wysiwyg-color-black">Definition of "tracking" by Apple's User Privacy and Data Use guidelines:</span>
</p>
<p>
  <span class="wysiwyg-color-black">“Tracking” refers to linking data collected from your app about a particular end-user or device, such as a user ID, device ID, or profile, with Third-Party Data for targeted advertising or advertising measurement purposes, or sharing data collected from your app about a particular end-user or device with a data broker.</span>
</p>
<p>
  <span class="wysiwyg-color-black">For further information please see <a href="https://developer.apple.com/app-store/app-privacy-details/">App Privact Details section on Apple Developer website.</a></span>
</p>
<h2 id="h_01HAVHW0RTSD5QRRH7T24Q2RP0">
  <span class="wysiwyg-color-black">What is the average data size of a Countly iOS SDK request sent to Countly Server?</span>
</h2>
<p>
  <span class="wysiwyg-color-black">While there are several types of requests that Countly iOS SDK sends to Countly Server, the most common ones are:</span>
</p>
<ul>
  <li>
    <span class="wysiwyg-color-black">Begin Session Request: It is sent on every app launch (and session start after coming back from the background), and it includes basic metrics.</span><br>
    <span class="wysiwyg-color-black">An example Begin Session request (<code>498 bytes</code>) :</span>
  </li>
</ul>
<pre><span class="wysiwyg-color-black"><code>http://mycountlyserver.com/i?app_key=0000000000000000000000000000000000000000
&amp;device_id=00000000-0000-0000-0000-000000000000
&amp;timestamp=1534402860000&amp;hour=16&amp;dow=5&amp;tz=540
&amp;sdk_version=18.08&amp;sdk_name=objc-native-ios
&amp;begin_session=1
&amp;metrics=%7B%22_device%22%3A%22iPhone9%2C1%22%2C%22_os%22%3A%22iOS%22%2C%22_os_version%22%3A%2211.4.1%22%2C%22_locale%22%3A%22en_JP%22%2C%22_density%22%3A%22%402x%22%2C%22_resolution%22%3A%22750x1334%22%2C%22_app_version%22%3A%221.0%22%2C%20%22_carrier%22%3A%22NTT%22%7D
</code></span></pre>
<ul>
  <li>
    <span class="wysiwyg-color-black">Update Session Request: It is sent every 60 seconds by default, but it depends on Countly iOS SDK initial configuration.</span><br>
    <span class="wysiwyg-color-black">An example Update Session request (<code>233 bytes</code>) :</span>
  </li>
</ul>
<pre><span class="wysiwyg-color-black"><code>http://mycountlyserver.com/i?app_key=0000000000000000000000000000000000000000
&amp;device_id=00000000-0000-0000-0000-000000000000
&amp;timestamp=1534402920000&amp;hour=16&amp;dow=5&amp;tz=540
&amp;sdk_version=18.08&amp;sdk_name=objc-native-ios
&amp;session_duration=60
</code></span></pre>
<ul>
  <li>
    <span class="wysiwyg-color-black">End Session Request: It is sent at the end of a session, when the app goes to background or terminates.</span><br>
    <span class="wysiwyg-color-black">An example End Session request (<code>247 bytes</code>) :</span>
  </li>
</ul>
<pre><span class="wysiwyg-color-black"><code>http://mycountlyserver.com/i?app_key=0000000000000000000000000000000000000000
&amp;device_id=00000000-0000-0000-0000-000000000000
&amp;timestamp=1534402956000&amp;hour=16&amp;dow=5&amp;tz=540
&amp;sdk_version=18.08&amp;sdk_name=objc-native-ios
&amp;session_duration=36
&amp;end_session=1
</code></span></pre>
<ul>
  <li>
    <span class="wysiwyg-color-black">Other Requests For Events, User Details, Push Notifications, Crash Reporting, View Tracking, Feedbacks, Consents, and some other features: Countly iOS SDK sends various requests with various data sizes. Frequency and size of these requests depend on Countly iOS SDK initial configuration and your app's use cases, as well as the end user.</span>
  </li>
</ul>
<h2 id="h_01HAVHW0RT0WGM2365JVMT956J">
  <span class="wysiwyg-color-black">What Information is Collected by the SDK?</span>
</h2>
<p>
  The following description mentions data that is collected by SDK's to perform
  their functions and implement the required features. Before any of it is sent
  to the server, it is stored locally. For further information please have a look
  to the
  <a href="/hc/en-us/articles/9290669873305#h_01HJ5MD0WB97PA9Z04NG2G0AKC">collected informations</a>
  for all SDKs.
</p>
<p>
  Further, if Apple Watch feature is enabled: - Paired Apple Watch Presence - watchOS
  App Install Status
</p>
<h2 id="h_01HAVHW0RT38RQQER1X1FAKE0Z">Why are push notification action events not reported?</h2>
<p>
  Notification action event is recorded when a user interacts with the notification
  and system calls <code>didReceiveNotificationResponse:</code> method.
</p>
<p>
  If you tap on the notification, but still do not get any action events, please
  check for the following possible problem points:
</p>
<ol>
  <li>
    You are setting
    <code>UNUserNotificationCenter.currentNotificationCenter</code>'s delegate
    manually at some point, so Countly iOS SDK can not handle the notification.
  </li>
  <li>
    <code>requiresConsent</code> Flag is enabled on initial config, but consent
    for Push Notifications feature is not granted (Note that this has nothing
    to do with iOS notification permission).
  </li>
  <li>
    Notification is not coming from Countly and it does not have any value for
    <code>kCountlyPNKeyNotificationID = @"i"</code> key in it
  </li>
</ol>
