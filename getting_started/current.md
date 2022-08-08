<p>
  Countly provides various functionality in different SDKs targeted for mobile,
  web, desktop, server to server use cases. For a feature comparison in all SDKs,
  <a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-Installing-SDKs#feature-comparison" target="_self">please check this table</a>.
</p>
<p>
  There are common concepts in all Countly SDKs and this document is intended to
  be a universal getting started guide without getting into the implementation
  details of individual SDKs. In order to get more information on platform specific
  implementation,
  <a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-Installing-SDKs#officially-supported-sdks" target="_self">please refer to the documentation</a>
  of your SDK of choice.
</p>
<h1>User/device identification</h1>
<p>
  By default, Countly generates an anonymous identifier to uniquely identify a
  device or browser. Total users metric for any period is based on unique number
  of device ids Countly Server receives requests from. Similarly, users list in
  <a href="/hc/en-us/articles/360037630571" target="_blank" rel="noopener">User Profiles</a>
  section is a list of anonymous devices Countly Server is receiving data from.
  All data originating from a single device, including sessions, events, views
  and crashes, are grouped under these individual profiles since all the data is
  tagged with the originating device id.
</p>
<p>
  Most Countly SDKs including,
  <a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#device-id" target="_blank" rel="noopener">iOS</a>,
  <a href="https://support.count.ly/hc/en-us/articles/360037754031-Android-SDK#device-id" target="_blank" rel="noopener">Android</a>,
  <a href="https://support.count.ly/hc/en-us/articles/360037813231-React-Native-Bridge-#changing-a-device-id" target="_blank" rel="noopener">React Native</a>,
  <a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#changing-a-device-id" target="_blank" rel="noopener">Flutter</a>,&nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037441932-Web-analytics-JavaScript-#changing-device-id" target="_blank" rel="noopener">Web</a>&nbsp;offer
  a mechanism to change/update this default device id for cases where you already
  have a better identifier such as an email address or account id or you get this
  information at some point in user journey such as after user logs into your application.
  For an in depth analysis of different device/user identification strategies
  <a href="https://medium.com/@countly_dev/tracking-users-in-countly-80bbe4ed0ad6" target="_self">please check out this post</a>.
</p>
<h1>Deciding on custom user properties</h1>
<p>
  User properties play an important role not only in reporting but also in various
  other cases such as personalizing push notifications and creating conditional
  remote configuration variables.
</p>
<p>
  Most Countly SDKs send some user properties together with the session request&nbsp;
  which is triggered automatically when the app is launched, user lands on a website,
  or manually in some cases such as server to server SDK usage. These properties,
  which we call default user properties, are metadata including but not limited
  to app version, device, platform, platform version.&nbsp;
</p>
<p>
  Furthermore, there are some reserved user properties that you can choose to set,
  including name, email, organization, gender and age if you choose to store PII
  (personally identifiable information) in Countly.
</p>
<p>
  Custom user properties are similar in logic to default and reserved user properties,
  in the sense that this information is stored in user profile level. All the data
  (sessions, events, views, crashes etc.) originating from a user will get tagged
  with a historical snapshot of default, reserved and custom user properties and
  will be available to be used in reporting and features such as
  <a href="/hc/en-us/articles/360037270112" target="_blank" rel="noopener">Cohorts</a>,
  <a href="/hc/en-us/articles/360036862312" target="_blank" rel="noopener">Funnels</a>,
  <a href="/hc/en-us/articles/360037260972" target="_blank" rel="noopener">Drill</a>,
  <a href="/hc/en-us/articles/900000812986" target="_blank" rel="noopener">Retention</a>
  and
  <a href="/hc/en-us/articles/360037639931" target="_blank" rel="noopener">Formulas</a>.
</p>
<p>
  Custom user properties consist of key value pairs, where value can be a string,
  number, boolean, or an array. There are various modifiers available in the SDKs
  such as set, set once, push unique, increment, multiply in order to update these
  as you need. For example, you can store account levels of your users in an
  <strong>accountType</strong>&nbsp;custom user property that can take values
  <strong>Basic</strong> or&nbsp;<strong>Premium</strong> to later on filter &amp;
  segment all reports based on the account type of your customers.
</p>
<h1>Events</h1>
<p>
  An "event" in Countly generally represents one of the following:
</p>
<ul>
  <li>
    An action of the user such as an interaction with a single UI element, or
    set of elements
  </li>
  <li>
    An important milestone the user reaches after completing other actions, such
    as completing an application or on-boarding process&nbsp;
  </li>
  <li>
    A transaction that takes place after one or more actions of the user, such
    as a backend API returning a result
  </li>
</ul>
<p>
  It is important to note that events aren't designed to only track simple user
  interactions such as "user clicked this button". The way you define events in
  your app determines the depth of insights you can get from Countly. Tracking
  everything you possibly can or tracking very little are equally bad. An ideal
  strategy is collecting the needs of various departments in your organization
  that'll take advantage of Countly. As a common example;
</p>
<ul>
  <li>
    Product team will want to check feature usage, they'll need multiple events
    that show how users interact with various application features
  </li>
  <li>
    Customer experience &amp; success team will want to understand paths users
    go through (such as during on-boarding) and get stuck in, and will need customized
    events as milestone indicators
  </li>
  <li>
    Engineering team will want to get transactions &amp; statutes that are created
    after users' interaction with the UI layer thus they'll need events or event
    segments that they can take advantage of
  </li>
  <li>
    CXOs and managers will want to see higher level metrics or KPIs, thus this
    higher level data should exist either as dedicated events or individual ones
    to be used while constructing complex metrics using
    <a href="/hc/en-us/articles/360037639931" target="_blank" rel="noopener">Formulas</a>
  </li>
</ul>
<p>
  In its most complex form (there can of course be additional segments), an event's
  JSON representation looks like below. Only mandatory fields are
  <code>key</code> and <code>count</code> which are set when you call the recordEvent
  function in any given SDK. Optional <code>sum</code> property is useful when
  you would like to store an extra numerical value for an event, in the below example
  we used it to store kilometers for a journey. Duration property represented as
  <code>dur</code> can be explicitly set, or you can take advantage of the
  <strong>timed events concept</strong> available in most SDKs.
</p>
<pre><span>{<br>   "key": "Journey",<br>   "count": 1,<br>   "sum": 100,<br>   "dur": 3600,<br>   "segmentation": {<br>      "Route Type": "Fastest"<br>   }<br>}</span></pre>
<p>
  Now let's dive into event segments and strategies you can follow.
</p>
<h1>Deciding on event segments</h1>
<p>
  Segments are properties that add further detail and meaning to an event. Segments
  are important since most of the time you aren't only interested in how many times
  some general action happened but also will have the need to dig deeper, filter
  certain cases or group occurrences by different nuances of the action.
</p>
<p>
  From our event sample in the above section, thanks to the Route Type event segment,
  you can not only see overall journeys taking place, but also see how many of
  the journeys were planned with a fastest, shortest or eco route types offered
  in the app. Furthermore, in plugins like
  <a href="/hc/en-us/articles/360037270112" target="_blank" rel="noopener">Cohorts</a>,
  <a href="/hc/en-us/articles/360036862312" target="_blank" rel="noopener">Funnels</a>,
  <a href="/hc/en-us/articles/360037260972" target="_blank" rel="noopener">Drill</a>&nbsp;and
  <a href="/hc/en-us/articles/360037639931" target="_blank" rel="noopener">Formulas</a>
  these event segments will be available for use cases such as;
</p>
<ul>
  <li>
    Filter events where <strong>Route Type = Eco</strong> using Drill
  </li>
  <li>
    Construct 3 different funnels where final step is the Journey event in all
    but filtered to be <strong>Route Type = Eco</strong>,
    <strong>Route Type = Fastest</strong> and
    <strong>Route Type = Shortest</strong>
  </li>
  <li>
    Create a behavioral cohort of users who did have a Journey with
    <strong>Route Type = Eco</strong> at least 2 times in the last 30 days (these
    are our eco friendly personas which we can target using
    <a href="/hc/en-us/articles/360037270492" target="_blank" rel="noopener">remote config</a>
    and
    <a href="https://support.count.ly/hc/en-us/articles/360037270012-Push-notifications#sending-automated-push-notifications" target="_blank" rel="noopener">automated push notifications</a>)
  </li>
  <li>
    Construct 2 formulas in which you calculate average kilometers driven per
    journey for <strong>Route Type = Shortest</strong> and
    <strong>Route Type = Fastest</strong>
  </li>
</ul>
<p>
  As you can tell from the above reporting examples, event segment selection is
  an important part of your success with reporting &amp; visualization in Countly.
</p>
<h1>Acquiring your application key and server url</h1>
<p>
  <strong>Acquiring the application key</strong>
</p>
<p>
  <span style="font-weight: 400;">Also referred to as "appKey" or "app_key" as shorthand, the application key, is used to identify, for which application, the information that the SDK has gathered, is tracked. You receive this value by creating a new application in Countly and accessing it in its application management screen.</span>
</p>
<p>
  <span style="font-weight: 400;"><strong>Note:&nbsp;</strong>Ensure you are using the App Key (found under Management -&gt; Applications) and not the API Key. Entering the API Key will not work.</span>
</p>
<p>
  <span style="font-weight: 400;"><img src="/hc/article_attachments/9208067266585/1.png" alt="1.png"></span>
</p>
<p>
  <strong>Acquiring the server URL</strong>
</p>
<p>
  <span style="font-weight: 400;">This is basically the domain from which you are accessing your Countly server. </span><span style="font-weight: 400;">During your SDK initialization you'll see a value such as 'url', 'server url' or something similar that you need to fill in. You have to fill that value with the IP or hostname of your server. For example, if you have Countly installed on 192.168.1.1, then inside the SDK you will need to write </span><span style="font-weight: 400;"><a href="https://192.168.1.1">https://192.168.1.1</a> , if the SSL configuration is complete, or <a href="http://192.168.1.1" target="_self" rel="undefined">http://192.168.1.1</a> if there is no SSL configuration.</span><span style="font-weight: 400;"> If there is a server name associated with your IP, that server name may also be used instead (e.g. <a href="https://countly.mycompany.com)." target="_self" rel="undefined">https://countly.mycompany.com)</a></span><span style="font-weight: 400;">.</span>
</p>
<h1>Handling login/logout in your app</h1>
<p>
  For a lot of apps, there is a login option. This allows you to confirm the identity
  of your users by cross-referencing them with your own systems. That also adds
  two complications. First, multiple users can use the same app on the same device.
  The generated data would need to be assigned to the relevant user, therefore
  the device ID needs to be changed. Second, the same user can log in to multiple
  devices. Therefore you need to use the same device ID on all of that user's devices.
  To achieve that you would have an internal ID of your own system or a derivative
  value of it that you can reliably generate.
</p>
<p>
  The first time you initialize a Countly SDK, you would allow the SDK to generate
  the device ID. When the user logs in to your app, you would change the device
  ID to the new ID that you generate. If this is the first time the user logs in,
  you would change the device ID with merging. On any other follow-up logins, you
  would change the device ID without merging. This way you can assign the events
  generated by the user before the first login to the user that logs in.
</p>
<p>
  When a user logs out, you have 2 options. First, you would not change the device
  ID. This way you would also assign any follow-up events to the user that was
  last signed in, and those events would be sent as they happen. Second, if the
  SDK supports temporary ID mode, you can enter that when logout happens. This
  way you would assign any follow-up events to the user that would sign in next.
  The downside to the temporary ID approach is that no events would be sent while
  the user is not logged in. Both of these approaches not only solve a server-side
  performance issue but also eliminates the issue with inflated user counts. We
  recommend you choose the first logout option.
</p>
<p>
  A key SDK feature that allows you to do this is the ability to see the device
  ID type. The 2 important things that you want to differentiate is if the ID is
  generated by the SDK or if it's a custom ID provided by you. If the ID is generated
  by the SDK then you can assume that the user has not logged in before and when
  changing the device ID, you need to do that with merging. If the device ID is
  a custom one then you can assume that you have already changed the ID before
  and need to perform the current change without merging.
</p>
<p>Here are a few sample login implementations of this flow:</p>
<h2>Android</h2>
<pre><span>public void </span><span>Login</span>() {<br>    <span>String newId </span>= <span>"SomeValue"</span>;<br>    <span>if </span>(<span>Countly</span>.<span>sharedInstance</span>().getDeviceIDType() == <span>DeviceId</span>.<span>Type</span>.<span>DEVELOPER_SUPPLIED</span>) {<br>        <span>// an ID was provided by the host app previously<br></span><span>        // we can assume that a device ID change with merge was executed previously<br></span><span>        // now we change it without merging<br></span><span>        </span><span>Countly</span>.<span>sharedInstance</span>().changeDeviceIdWithoutMerge(<span>DeviceId</span>.<span>Type</span>.<span>DEVELOPER_SUPPLIED</span>, <span>newId</span>);<br>    } <span>else </span>{<br>        <span>// SDK generated ID<br></span><span>        // we change device ID with merge so that data is combined<br></span><span>        </span><span>Countly</span>.<span>sharedInstance</span>().changeDeviceIdWithMerge(<span>newId</span>);<br>    }<br>}</pre>
<h2>iOS</h2>
<pre class="c-mrkdwn__pre" data-stringify-type="pre">public static void login()<br> &nbsp;<wbr> &nbsp;<wbr>{<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>DeviceId.Type type = Countly.sharedInstance().getDeviceIDType();<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>if(type.equals(DeviceId.Type.DEVELOPER_SUPPLIED))<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>{<br>            Countly.sharedInstance().changeDeviceIdWithoutMerge(DeviceId.Type.DEVELOPER_SUPPLIED,<span class="hljs-string">@"usersNewID"</span>);<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>}<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>else<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>{<br>            Countly.sharedInstance().changeDeviceIdWithMerge(<span class="hljs-string">@"usersNewID"</span>);<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>}<br> &nbsp;<wbr> &nbsp;<wbr>}</pre>
<h1>
  Using the Countly SDK's with iOS and Android widgets and watches
</h1>
<p>
  With mobile devices, there are 3 different modalities that a user can interact
  with: phone app, phone widget, and watch app. When designing a product that spans
  all three worlds, the goal is usually to track the user's lifecycle across all
  of them.
</p>
<p>
  To perform this cross-modality tracking, care must be given that tracking is
  performed with the same device ID across all of them. If the device ID, to which
  the event or session is attributed, would not be the same across all devices
  and modalities then the same user would be counted as a separate person on one
  of them.
</p>
<p>
  This also means that if the user's device ID would change, this change needs
  to be synchronized across all modalities/apps.
</p>
<p>This can be achieved in 2 general approaches:</p>
<ol>
  <li>
    Performing data recording at each location separately - each modality integrates,
    configures, and initializes the Countly SDK separately. Device ID synchronization
    needs to be performed manually across all modalities. This would be accomplished
    either by using some platform-provided method to perform direct communication
    or using an outside device (for example, a server) to perform a centralized
    exchange. Alternatively, every modality needs a way to create the same device
    ID without direct cross-synchronization.
  </li>
  <li>
    Performing data recording at a central location and proxying data recording
    from each non-app modality - eliminates the need for synchronization as there
    is only one instance of the SDK initialized and configured. Device ID changes
    are immediately taken into account when they happen. Since cross-device recording
    is centralized, views and sessions need to be recorded manually. The main
    issue with this approach is that there will be times when the main app might
    be out of reach for proxy recording or might not be running.
  </li>
</ol>
<p>
  To differentiate from which modality the event came from, you can use a custom
  segmentation value that shows that. Every unique value would indicate a separate
  modality.
</p>
<p>
  <strong>Notes for native iOS integration</strong>
</p>
<p>
  The general recommendation is to have Countly integrated into each separate modality
  as that seems to present the least amount of issues. If the modalities that are
  used are from the same developer account then there should be an internal communication
  channel available to them. If they are not on the same developer account then
  an outside synchronization mechanism will need to be used.
</p>
<p>
  For additional integration details, you would also have a look at
  <a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#watchos-integration" target="_self">this</a>
  section.
</p>
<p>
  <strong>Notes for native Android integration</strong>
</p>
<p>
  Due to the way the SDK is currently designed, integrating the SDK in a widget
  will cause crashes. Therefore the recommendation is to proxy the tracking requests
  to the host application. Shared preferences could potentially be used to achieve
  this.
</p>
<p>
  The SDK would be directly integrated with the watch modality and then synchronization
  would be done with shared preferences.
</p>
<p>
  <strong>Notes for Flutter integration</strong>
</p>
<p>
  If you have a Flutter app, there doesn't seem to be an easy way to integrate
  other modalities. To achieve that you would need to create them using the native
  platform languages and integrate the native Countly SDK's. In that case, the
  recommendations from the previous sections would apply.
</p>
<h1>How to validate your Countly integration?</h1>
<p>
  After you have integrated the Countly SDK into your app or website, to the best
  of your ability, whether you see some data or not in your Countly server, you
  should normally verify your integration by checking if everything is working
  as expected, both on your Countly server and your app/website. To have the most
  optimized verification process we recommend you to go through the following steps
  for these cases of integration validation and also for debugging if you are seeing
  partial or no data at all on your server.
</p>
<h2>1. Check SDK logs</h2>
<p>
  As part of the process of integration verification, you would want to enable
  logging in the SDK and have a look at the printed-out messages. If there would
  be a warning, errors, or deprecation messages, it would indicate potential problems
  and action items that need to be fixed. Logging can be enabled during the SDK
  initialization and the way you do that differs slightly from SDK to SDK. For
  specifics on how to enable it, you would want to check the documentation of the
  specific SDK that you are using from
  <a href="https://support.count.ly/hc/en-us/sections/360007310512-SDKs">here</a>.
</p>
<p>
  After enabling SDK side logging you would want to run your app or website and
  check the debug messages that are printed in the respective console. The specific
  location of that would change depending on the platform and SDK.
</p>
<p>
  <span style="font-weight: 400;"><img src="/hc/article_attachments/9208973048217/mceclip0.png" alt="mceclip0.png"></span>
</p>
<p>
  <span style="font-weight: 400;">Check if requests are being created - this means, you need to check whether you are calling SDK methods to send information to the server and that the SDK has been implemented correctly.</span>
</p>
<p>
  <span style="font-weight: 400;">Also check if requests fail or are successfully sent to the server, because if they fail, maybe the server is not reachable from this specific network, or you made a mistake when providing the URL to the server.</span>
</p>
<h2>2. Check Request Logs</h2>
<p>
  Next, you would want to verify that your Countly server is receiving data from
  <span style="font-weight: 400;"><code>Utilities &gt; Request Logs</code></span>.
  <span style="font-weight: 400;">Should there be an issue, the request logs usually state what this problem is about, why the request was not processed, or why incoming data may be incorrect - such as sending data for the incorrect app type, sending duplicate requests, incorrectly set up parameter tampering, etc.</span>
</p>
<p>
  <img src="/hc/article_attachments/9208398657433/2.png" alt="2.png">
</p>
<h2>3. Make sure you have the correct configuration</h2>
<p>
  Here the most important thing is to verify if your 'app_key' and 'URL' values
  are entered correctly. For more information on making sure that you are using
  your correct 'app_key' and server URL, you can check out the following section
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#acquiring-your-application-key-and-server-url">here</a>.
</p>
<h2>4. Check your Countly server</h2>
<p>
  If you have checked your SDK logs and everything seems to be working fine in
  your app or website it is time to check Countly if the planned data is recorded
  as expected. As a simple test, you can simply open User Profiles in Countly to
  see if your app/website was able to connect and recognized as a user in your
  Countly server. If it is you are good to go and you can stop here on the list.
</p>
<p>
  <img src="/hc/article_attachments/9209504188057/mceclip1.png" alt="mceclip1.png">
</p>
<p>
  In case it seems like some data is not being recorded, it can be due to some
  requests being rejected related to problems with the checksum, or sometimes requests
  might be dropped if there are filtering rules set to do that. Sometimes filtering
  rules are targeting more things than planned by accident.&nbsp; For debugging
  those issues and others, keep reading.
</p>
<h2>5. Check the server for errors</h2>
<p>
  <span style="font-weight: 400;">Check <code>Management &gt; Logs &gt; Api Log</code></span><span style="font-weight: 400;"> for errors. Chances are if there is a problem/bug with a specific plugin processing information there would be new errors in the logs.</span>
</p>
<p>
  <span style="font-weight: 400;"><img src="/hc/article_attachments/9277142121497/mceclip0.png" alt="mceclip0.png"></span>
</p>
<h2>6. Check plugins</h2>
<p>
  Some plugins that might be necessary to process data and provide functionalities
  you want might not be activated or you might have accidentally disabled them.
  You can check your plugins' status from
  <span style="font-weight: 400;"><code>Management &gt; Feature Management<br></code></span>
</p>
<p>
  <strong><img src="/hc/article_attachments/9277537797401/mceclip1.png" alt="mceclip1.png"></strong>
</p>
<h2>7. Check Filtering rules</h2>
<p>
  <span style="font-weight: 400;">Events or requests may be blocked. In this case, check <code>Main menu &gt; Utilities &gt; Filtering rules</code></span><span style="font-weight: 400;"> to see whether any rules block events or any requests.</span>
</p>
<p>
  <img src="/hc/article_attachments/9279924847385/filt.png" alt="filt.png">
</p>
<h2>8. Check event limits</h2>
<p>
  <span style="font-weight: 400;">The event name limit may be exceeded (the limit is 100, by default), and may be adjusted under <code>Management &gt; Settings &gt; API &gt; Data Limits &gt; Max unique event key</code>.</span>
</p>
<p>
  <strong><img src="/hc/article_attachments/9280040279577/mceclip2.png" alt="mceclip2.png"></strong>
</p>
<h2>9. Check checksum</h2>
<p>
  Some
  <span>SDKs provide an option to send a checksum along the request data to prevent data breaches by a man-in-the-middle attack. If you have set a salt for checksum in your SDK but did not set it at your server or typed it wrongly, and vice versa, you should check your salt value from <span style="font-weight: 400;"><code>Management &gt; Applications &gt; Salt for checksum</code></span>.</span>
</p>
<p>
  <span><img src="/hc/article_attachments/9280412281497/salt.png" alt="salt.png"></span>
</p>
<h2>10. Check time zone</h2>
<p>
  <span style="font-weight: 400;">Your time zone may be different from the application’s time zone, explaining why it takes some time for you to be able to see events on the graph, something which should be available to you without delay. You can edit your time zone from <span><code>Management &gt; Applications &gt; Salt for checksum</code></span>.</span>
</p>
<p>
  <span style="font-weight: 400;"><img src="/hc/article_attachments/9280481380377/time.png" alt="time.png"></span>
</p>
<h1>How long does it take for my data to show up on Countly?</h1>
<p>
  When you are checking Countly and sending events from your app or website, you
  might realize that sometimes there is a delay for the data to show up there.
  This is an expected behavior stemming from the internal logic of the Countly
  SDKs and the potential server-side calculations.
</p>
<p>
  <strong>SDK Side Processes</strong>
</p>
<p>
  In some cases, there might just be a connection issue. Either the user is offline
  or unable to reach your server (due to server maintenance or other issues). Thus
  they would not be able to send data to the server. If during this loss of connection
  the SDK is not able to perform any network activity, it will wait for a while
  before reattempting the upload of recorded information. By default, this delay
  is 60 seconds (can be changed during init) and is tied to the session update
  tick interval.
</p>
<p>
  The second aspect that can influence this is the event queue. Before we sent
  the recorded events to the server, we try to cache them to optimize the networking.
  They are cached until their amount exceeds the threshold (by default 100, but
  can be configured), or the session update tick happens, or some other internal
  trigger happens.
</p>
<p>
  <strong>Server Side Processes</strong>
</p>
<p>
  In addition to this, there can be server-side calculations that can add additional
  delay. Depending on where you are expecting the changes to show up, the types
  and the length of the calculations involved would differ. For example, a cohort
  can take minutes up to hours to process before showing up on Countly. But most
  data would show up within seconds after reaching your Countly Server.
</p>
<h1>Is my SDK version compatible with my server?</h1>
<p>
  If you have checked your Countly server version and your SDK version you might
  have noticed that they most likely do not match. Due to the way our development
  is structured, our Countly server releases happen more often than any single
  SDK. Usually, this will lead you to see that your server version is higher than
  your SDK version, and that is fine.
</p>
<p>
  Our guidelines are that the major version of your server should be the same or
  higher than the major version of the SDK that you are using. As our versioning
  scheme for our server releases and SDKs has 3 numbers separated by dots, something
  like "22.02.3". The first two numbers are what we are calling the major version
  and those are the ones that you should be paying attention to ("22.02.X").&nbsp;
</p>
