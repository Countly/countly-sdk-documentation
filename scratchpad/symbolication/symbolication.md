<p>
  <span>Crash Symbolication lets you symbolicate/de-obfuscate crash reports and convert them into human readable format, helping you</span>
  pinpoint where in your code a crash is originating from.
</p> 
<div class="callout callout--info">
  <span class="wysiwyg-font-size-large"><strong class="callout__title">Availability</strong></span>
  <p>
    The Symbolication plugin is available only in the Enterprise Edition.
  </p>
</div>
<h1>Understanding Crash Symbolication</h1>
<h2>What is "Symbolication"?</h2>
<p>
  <span style="font-weight: 400;">When releasing your application, you might be skipping crucial steps such as debugging information from the final binary format, obfuscating your source code, or minifying it by removing unnecessary characters. Doing all this can help make your application harder to reverse engineer, but</span><span style="font-weight: 400;"> you may then receive error stack traces that have obfuscated information in them, making it impossible to track down the source of your crash.</span>
</p>
<p>
  <span style="font-weight: 400;">Depending on the platform, your stack trace may be full of memory addresses or transformed function names. Symbolication is the process of converting them into human readable, class/method names, file names, and line numbers.</span>
</p>
<p>
  <span style="font-weight: 400;">You can watch a tutorial about how symbolication works below.</span>
</p>
<p>
  <span style="font-weight: 400;">

    <iframe src="//www.youtube-nocookie.com/embed/UAfxH41jvwc" width="560" height="315" frameborder="0" allowfullscreen=""></iframe>

  </span>
   <span style="font-weight: 400;"></span>
</p>
<div class="embed-container">
  <h3>Symbolicating iOS, Android, and JavaScript Crashes</h3>
</div>
<div class="callout callout--warning">
  <span class="wysiwyg-font-size-large"><strong class="callout__title">Save your symbol or mapping files!</strong></span>
  <p>
    For the obfuscation and minification processes to be reversible, a symbol
    or mapping file is also produced while building your application. It is imperative
    for you to keep and archive those files as the symbolication process is only
    possible with them. You will also need to archive symbol files for every
    version you would like to symbolicate.
  </p>
</div>
<p>
  <span style="font-weight: 400;">Currently, Countly supports symbolication for DexGuard and ProGuard in <a href="#h_01EYD9B1NZNNJZ0QDPHH9F20C6" target="_self">Android</a>, Apple-provided tools in <a href="#h_01EYD9BAN76H8RT3T657ECGV0P" target="_self">iOS</a> mobile applications, and source maps in <a href="#h_01EYD9BQBHX4NZ136BR8E8N5KP" target="_self">JavaScript</a> web applications. Find examples for the input and output for each one below.</span>
</p>
<h3 id="h_01EYD9B1NZNNJZ0QDPHH9F20C6">Android Symbolication Samples</h3>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Android Symbolication input sample</span>
    <span class="tabs-link">Android Symbolication output sample</span>
  </div>
  <div class="tab">
    <pre><code class="Android Symbolication input sample">java.lang.IllegalStateException: Could not execute method for android:onClick
at android.view.View$DeclaredOnClickListener.onClick(View.java:4725)
at android.view.View.performClick(View.java:5637)
at android.view.View$PerformClick.run(View.java:22429)
at android.os.Handler.handleCallback(Handler.java:751)
at android.os.Handler.dispatchMessage(Handler.java:95)
at android.os.Looper.loop(Looper.java:154)
at android.app.ActivityThread.main(ActivityThread.java:6121)
at java.lang.reflect.Method.invoke(Native Method)
at com.android.internal.os.ZygoteInit$MethodAndArgsCaller.run(ZygoteInit.java:889)
at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:779)
Caused by: java.lang.reflect.InvocationTargetException
at java.lang.reflect.Method.invoke(Native Method)
at android.view.View$DeclaredOnClickListener.onClick(View.java:4720)
... 9 more
Caused by: java.lang.Exception: Exception at the end of the call
at ly.count.android.demo.a.b(SourceFile:29)
at ly.count.android.demo.a.a(SourceFile:21)
at ly.count.android.demo.ActivityExampleCrashReporting.c(SourceFile:98)
at ly.count.android.demo.ActivityExampleCrashReporting.b(SourceFile:94)
at ly.count.android.demo.ActivityExampleCrashReporting.a(SourceFile:90)
at ly.count.android.demo.ActivityExampleCrashReporting.onClickCrashReporting10(SourceFile:82)
... 11 more</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="Android Symbolication output sample">java.lang.IllegalStateException: Could not execute method for android:onClick
at android.view.View$DeclaredOnClickListener.onClick(View.java:4725)
at android.view.View.performClick(View.java:5637)
at android.view.View$PerformClick.run(View.java:22429)
at android.os.Handler.handleCallback(Handler.java:751)
at android.os.Handler.dispatchMessage(Handler.java:95)
at android.os.Looper.loop(Looper.java:154)
at android.app.ActivityThread.main(ActivityThread.java:6121)
at java.lang.reflect.Method.invoke(Native Method)
at com.android.internal.os.ZygoteInit$MethodAndArgsCaller.run(ZygoteInit.java:889)
at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:779)
Caused by: java.lang.reflect.InvocationTargetException
at java.lang.reflect.Method.invoke(Native Method)
at android.view.View$DeclaredOnClickListener.onClick(View.java:4720)
... 9 more
Caused by: java.lang.Exception: Exception at the end of the call
at ly.count.android.demo.Utility.void DeepCall_b()(SourceFile:29)
at ly.count.android.demo.Utility.void DeepCall_a()(SourceFile:21)
at ly.count.android.demo.ActivityExampleCrashReporting.void deepFunctionCall_3()(SourceFile:98)
at ly.count.android.demo.ActivityExampleCrashReporting.void deepFunctionCall_2()(SourceFile:94)
at ly.count.android.demo.ActivityExampleCrashReporting.void deepFunctionCall_1()(SourceFile:90)
at ly.count.android.demo.ActivityExampleCrashReporting.void onClickCrashReporting10(android.view.View)(SourceFile:82)
... 11 more</code></pre>
  </div>
</div>
<p>&nbsp;</p>
<h3 id="h_01EYD9BAN76H8RT3T657ECGV0P">iOS Symbolication Samples</h3>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">iOS Symbolication input sample</span>
    <span class="tabs-link">iOS Symbolication output sample</span>
  </div>
  <div class="tab">
    <pre><code class="iOS Symbolication input sample">libsystem_platform.dylib            0x00000001826c130c _sigtramp + 36
mahya                               0x000000010006e174 mahya + 156020
mahya                               0x000000010006d060 mahya + 151648
mahya                               0x000000010006ad34 mahya + 142644
UIKit                               0x0000000189925d74  + 184
UIKit                               0x00000001898eedb8  + 128
UIKit                               0x00000001898ff2b0  + 88
UIKit                               0x000000018a1c0ff8  + 272
UIKit                               0x0000000189b5e138  + 280
UIKit                               0x0000000189b5d96c  + 1064
UIKit                               0x0000000189b5d4c4  + 60
UIKit                               0x000000018a1c0ff8  + 272
UIKit                               0x0000000189b5d400  + 436
UIKit                               0x00000001898eea40  + 672
UIKit                               0x00000001898ee364  + 1780
UIKit                               0x00000001898ec954  + 228
UIKit                               0x00000001898eab04  + 3152
UIKit                               0x0000000189b74750  + 228
UIKit                               0x000000018975ea50  + 384
UIKit                               0x0000000189b74400  + 344
UIKit                               0x0000000189768fd4  + 2480
UIKit                               0x000000018976436c  + 3192
UIKit                               0x0000000189734f80  + 340
UIKit                               0x0000000189f2ea20  + 2400
UIKit                               0x0000000189f2917c  + 4268
UIKit                               0x0000000189f295a8  + 148
CoreFoundation                      0x00000001835b142c  + 24
CoreFoundation                      0x00000001835b0d9c  + 540
CoreFoundation                      0x00000001835ae9a8  + 744
CoreFoundation                      0x00000001834deda4 CFRunLoopRunSpecific + 424
GraphicsServices                    0x0000000184f49074 GSEventRunModal + 100
UIKit                               0x0000000189799c9c UIApplicationMain + 208
mahya                               0x000000010005fe14 mahya + 97812
libdyld.dylib                       0x00000001824ed59c  + 4</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="iOS Symbolication output sample">libsystem_platform.dylib            0x00000001826c130c _sigtramp + 36
-[MHViewController countlyProductionTest] (in mahya) (MHViewController.m:620)
-[MHViewController transitionToMahya] (in mahya) (MHViewController.m:443)
-[MHViewController textFieldShouldReturn:] (in mahya) (MHViewController.m:210)
UIKit                               0x0000000189925d74  + 184
UIKit                               0x00000001898eedb8  + 128
UIKit                               0x00000001898ff2b0  + 88
UIKit                               0x000000018a1c0ff8  + 272
UIKit                               0x0000000189b5e138  + 280
UIKit                               0x0000000189b5d96c  + 1064
UIKit                               0x0000000189b5d4c4  + 60
UIKit                               0x000000018a1c0ff8  + 272
UIKit                               0x0000000189b5d400  + 436
UIKit                               0x00000001898eea40  + 672
UIKit                               0x00000001898ee364  + 1780
UIKit                               0x00000001898ec954  + 228
UIKit                               0x00000001898eab04  + 3152
UIKit                               0x0000000189b74750  + 228
UIKit                               0x000000018975ea50  + 384
UIKit                               0x0000000189b74400  + 344
UIKit                               0x0000000189768fd4  + 2480
UIKit                               0x000000018976436c  + 3192
UIKit                               0x0000000189734f80  + 340
UIKit                               0x0000000189f2ea20  + 2400
UIKit                               0x0000000189f2917c  + 4268
UIKit                               0x0000000189f295a8  + 148
CoreFoundation                      0x00000001835b142c  + 24
CoreFoundation                      0x00000001835b0d9c  + 540
CoreFoundation                      0x00000001835ae9a8  + 744
CoreFoundation                      0x00000001834deda4 CFRunLoopRunSpecific + 424
GraphicsServices                    0x0000000184f49074 GSEventRunModal + 100
UIKit                               0x0000000189799c9c UIApplicationMain + 208
main (in mahya) (main.m:16)
libdyld.dylib                       0x00000001824ed59c  + 4</code></pre>
  </div>
</div>
<p>&nbsp;</p>
<h3 id="h_01EYD9BQBHX4NZ136BR8E8N5KP">JavaScript Symbolication Samples</h3>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">JS Symbolication input sample</span>
    <span class="tabs-link">JS Symbolication output sample</span>
  </div>
  <div class="tab">
    <pre><code class="JS Symbolication input sample">ReferenceError: undefined_function is not defined
    at r (file:///home/atak/Work/Countly/sample-app/dist/main.js:2:140)
    at HTMLButtonElement.document.getElementById.onclick (file:///home/atak/Work/Countly/sample-app/dist/main.js:2:521)</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="JS Symbolication output sample">ReferenceError: undefined_function is not defined
    at undefined_function (src/index.js:30:4)
    at cause_error (src/index.js:37:10)</code></pre>
  </div>
</div>
<h1>Configuring the Server for Symbolication</h1>
<p>
  <span style="font-weight: 400;">The first step for using symbolication is installing and enabling the <a href="https://count.ly/plugins/crash-symbolication" target="_blank" rel="noopener">Symbolication plugin</a>.</span>
</p>
<p>
  To do so, in the main Countly Dashboard, go to<span>&nbsp;</span><code>Management</code><span>&nbsp;</span>&gt;<span>&nbsp;</span><code>Plugins</code><span>&nbsp;</span>and
  enable the<span>&nbsp;</span><strong>Crash Symbolication<span>&nbsp;</span></strong>toggle.
</p>
<p>
  After that, you will find<span>&nbsp;</span><strong>Manage Symbols</strong><span>&nbsp;</span>in
  the<span>&nbsp;</span><strong>Improve</strong><span>&nbsp;</span>section of your
  Countly Dashboard, under the<span>&nbsp;</span><strong>Crashes</strong><span>&nbsp;</span>category.
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/8ae1a40-2_6.png">
</div>
<div class="callout callout--warning">
  <span class="wysiwyg-font-size-large"><strong class="callout__title">Configuring iOS Symbolication</strong></span>
  <p>
    Setting up a connection to the Countly symbolication server is only needed
    for symbolicating iOS stack traces.<span class="wysiwyg-color-black"> You can <a href="#h_01EYD9RP1BVHKYM9AWDPJQV5W1" target="_self">skip it</a> if you will not be using Symbolication for iOS applications.</span>
  </p>
</div>
<p>
  <span style="font-weight: 400;"><span class="wysiwyg-color-black">For iOS applications, the ne</span>xt step is creating the connection to the Countly symbolication server. To do so, you will need a symbolication API key provided by Countly. The Countly symbolication server address is <strong>https://symbolication.count.ly</strong>. When you get your API key, you will need to set it in the server configuration screen in <code>Management</code> &gt; <code>Settings</code>, under the <strong>Crashes</strong>&nbsp;section.</span>
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/d8ca177-2_2.png">
</div>
<p>
  <span style="font-weight: 400;">After you have made sure that those fields contain valid information, click the <code>Test Connection</code> button to make sure everything is working correctly. If your provided server URL or API key is wrong or your Countly server cannot reach the symbolication server, you may diagnose it with this button.</span>
</p>
<p>
  <span style="font-weight: 400;">If everything is working correctly, you will see the alert messages in the image below.</span>
</p>
<div class="img-container wysiwyg-text-align-center">
  <img src="https://count.ly/images/guide/0cbe537-2_3.png">
</div>
<p>
  <span style="font-weight: 400;">You are now done setting up your Countly instance to use iOS Symbolication.</span>
</p>
<h1 id="h_01EYDBCXQ3W8S1548Q7RSJFJS0">Using Symbolication in Countly</h1>
<p>
  <span style="font-weight: 400;">This section will guide you when uploading a symbol file and then symbolicating your stack trace for Android and iOS.</span>
</p>
<p>
  <span style="font-weight: 400;">After enabling the Symbolication plugin, you might have noticed that additional choices have been added to your Crashes submenu items:</span>
</p>
<div class="img-container wysiwyg-text-align-center">
  <img src="https://count.ly/images/guide/f0f0fdd-2_4.png">
</div>
<ul>
  <li>
    <span style="font-weight: 400;"><strong>Overview</strong>&nbsp;takes you to the a <a href="/hc/en-us/articles/360037630331" target="_self">crash general overview.</a> </span>
  </li>
  <li>
    <span style="font-weight: 400;"><strong>Manage Symbols</strong> takes you to a screen where you can manage all the symbol files uploaded for this application. </span>
  </li>
  <li>
    <span style="font-weight: 400;"><strong>Symbolication logs</strong> is similar to the request logs, where a short history of your symbolication requests is kept and therefore, this view is only populated if there are problems with the symbolication processes.</span>
  </li>
</ul>
<h2>Uploading the Symbol File</h2>
<p>
  <span style="font-weight: 400;">Now that the connection to the symbolication server has been established and the necessary symbol files are procured, we can get to the symbolication of specific stack traces.</span>
</p>
<div class="callout callout--info">
  <span class="wysiwyg-font-size-large"><strong class="callout__title">Only one symbol file upload required</strong></span>
  <p>
    <span style="font-weight: 400;">You should only upload one symbol file per application version. Multiple symbol file uploads are not supported.</span>
  </p>
</div>
<p>
  <span style="font-weight: 400;">To upload a symbol file, open the </span><span style="font-weight: 400;"><strong>Manage Symbols </strong>section. At first it will look empty, as shown below:</span>
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/1d4f4ca-2_5.PNG">
</div>
<p>
  <span style="font-weight: 400;">There, you will have to click on the <code>Add Symbolication File</code> button, which will open a drawer with the fields described below. Note that you will need to do this for every version of your app you would like to symbolicate.</span>
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/1c033d4-2_6.png">
</div>
<p>
  <span style="font-weight: 400;"><strong>Select Type</strong>: </span><span style="font-weight: 400;">In the <code>Type</code></span><span style="font-weight: 400;">&nbsp;selection, you need to choose the platform for the symbol file you are uploading.</span>
</p>
<p>
  <span style="font-weight: 400;"><strong>Build ID</strong>: For Android, the <code>Build ID</code></span><span style="font-weight: 400;">&nbsp;field is the version name. For iOS, the <code>Build UUID</code></span><span style="font-weight: 400;"> field is your app's Build UUIDs. For JavaScript, this must match the <code>app_version</code> you use when initializing the Countly SDK in your web application.<br></span>
</p>
<p>
  <span style="font-weight: 400;">You can get <code>Build UUIDs</code>&nbsp;using the <code>dwarfdump --uuid</code> command on the dSYM file, and you may specify more than one comma-separated&nbsp;<code>Build UUID</code> for each architecture.</span>
</p>
<p>
  <span style="font-weight: 400;">Note that the Android <strong>Build ID</strong> and iOS <strong>Build UUID</strong> specified here must match your app's corresponding&nbsp; <strong>Build ID</strong>&nbsp;or <strong>Build UUID</strong>.</span>
</p>
<p>Example:</p>
<pre><code>dwarfdump --uuid CountlyTestApp-iOS.app.dSYM
UUID: AD4F5647-B2A0-3D85-8DF4-78D4DFD83296 (armv7) CountlyTestApp-iOS.app.dSYM/Contents/Resources/DWARF/CountlyTestApp-iOS
UUID: 70B0DE66-D337-3952-914D-A1E542667E20 (arm64) CountlyTestApp-iOS.app.dSYM/Contents/Resources/DWARF/CountlyTestApp-iOS
</code></pre>
<p>
  <span style="font-weight: 400;"><strong>File Upload</strong>: While choosing a Symbolication/Mapping File upon uploading the page for iOS, do not forget to zip the dSYM file before uploading. Otherwise, you will not be able to upload a dSYM file in a folder structure.</span>
</p>
<p>
  <span style="font-weight: 400;"><strong>Notes</strong>: Free text optional field.</span>
</p>
<p>
  <span style="font-weight: 400;">When everything is filled out, simply click <code>Upload file</code>.</span>
</p>
<p>
  <span style="font-weight: 400;">Again, keep in mind you should do this process for every version or build that you would like to symbolicate.</span>
</p>
<h2>Symbolicating a Crash</h2>
<p>
  <span style="font-weight: 400;">After some time has passed, you will start to see new exceptions in your <a href="https://support.count.ly/hc/en-us/articles/360037630331-Crashes#main-page" target="_self">Crashes Overview</a> dashboard. If you have uploaded the correct symbols for those versions, then you are ready to move forward with the symbolication process.</span>
</p>
<p>
  <span style="font-weight: 400;">To symbolicate a crash, you first have to go to its detailed view by clicking on the crash or on the <code>View</code> button.</span>
</p>
<p>
  <span style="font-weight: 400;"><img src="/hc/article_attachments/900005964583/Screenshot_2020-12-07_at_18.32.48.png" alt="Screenshot_2020-12-07_at_18.32.48.png"></span>
</p>
<p>
  <span style="font-weight: 400;">As shown below, the detailed crash view will be divided in two parts: the top contains the crash group stack trace, and the bottom contains entries for each specific crash and its circumstances.</span>
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/25e9662-11.png">
</div>
<p>
  <span style="font-weight: 400;">When clicking on a specific crash entry, it opens up additional information which contains a <strong>Symbolicate</strong> toggle button, assuming it's possible to symbolicate the crash (e.g. symbol file is uploaded for corresponding version). At the top of the crash group section, you may also see the <strong>Symbolicate</strong> button.</span>
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/e409ff5-2_7.PNG">
</div>
<p>
  <span style="font-weight: 400;">When you click on the <code>Symbolicate</code> button, you should see the <strong>Symbolication in progress</strong> message. When that process is complete, you should be able to see the symbolicated stack trace.</span>
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/00818f4-2_8.png">
</div>
<p>
  <span style="font-weight: 400;">The current symbolication implementation has some technical limitations, and the top crash group will show a <strong>Symbolicate</strong> button <em>only</em> after a crash from a newer app version is received. Therefore, if you would like to symbolicate crashes from a version you had before you enabled Crash Symbolication, you will have to scroll down to a specific crash entry at the bottom of the detailed crash view.</span>
</p>
