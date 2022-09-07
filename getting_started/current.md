<p>
  &nbsp;Countly provides various functionality in different SDKs targeted for mobile,
  &nbsp;web, desktop, server to server use cases. For a feature comparison in all
  SDKs, &nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-Installing-SDKs#feature-comparison" target="_self">please check this table</a>.
</p>
<p>
  &nbsp;There are common concepts in all Countly SDKs, and this document is intended
  to &nbsp;be a universal getting started guide without getting into the implementation
  &nbsp;details of individual SDKs. To get more information on platform-specific
  &nbsp;implementation, &nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-Installing-SDKs#officially-supported-sdks" target="_self">please refer to the documentation</a>
  &nbsp;of your SDK of choice.
</p>
<h1>User/device identification</h1>
<p>
  &nbsp;By default, Countly generates an anonymous identifier to uniquely identify
  a device or browser. The total users metric for any period is based on a unique
  number &nbsp;of device ids the Countly Server receives requests from. Similarly,
  users list in &nbsp;<a href="/hc/en-us/articles/360037630571" target="_blank" rel="noopener">User Profiles</a>
  &nbsp;The section lists anonymous devices from which the Countly Server is receiving
  data. &nbsp;All data originating from a single device, including sessions, events,
  views &nbsp;and crashes, are grouped under these individual profiles since all
  the data is &nbsp;tagged with the originating device id.
</p>
<p>
  &nbsp;Most Countly SDKs including, &nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#ddevice-id" target="_blank" rel="noopener">iOS</a>,
  &nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037754031-Android-SDK#device-id" target="_blank" rel="noopener">Android</a>,
  &nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037813231-React-Native-Bridge-#changing-a-device-id" target="_blank" rel="noopener">React Native</a>,
  &nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037944212-Flutter#changing-a-device-id" target="_blank" rel="noopener">Flutter</a>,&nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037441932-Web-analytics-JavaScript-#changing-device-id" target="_blank" rel="noopener">Web</a>&nbsp;offer
  &nbsp;a mechanism to change/update this default device id for cases where you
  already &nbsp;have a better identifier such as an email address or account id
  or you get this &nbsp;information at some point in user journey such as after
  user logs into your application. &nbsp;For an in-depth analysis of different
  device/user identification strategies &nbsp;<a href="https://medium.com/@countly_dev/tracking-users-in-countly-80bbe4ed0ad6" target="_self">please check out this post</a>.
</p>
<h1>Deciding on custom user properties</h1>
<p>
  &nbsp;User properties play an important role not only in reporting but also in
  various &nbsp;other cases such as personalizing push notifications and creating
  conditional &nbsp;remote configuration variables.
</p>
<p>
  &nbsp;Most Countly SDKs send some user properties together with the session request&nbsp;
  &nbsp;triggered automatically when the app is launched, the user lands on a website,
  &nbsp;or manually in some cases such as server-to-server SDK usage. These properties,
  &nbsp;which we call default user properties, are metadata, including but not
  limited &nbsp;to the app, device, platform, and platform.&nbsp;
</p>
<p>
  &nbsp;Furthermore, there are some reserved user properties that you can choose
  to set, &nbsp;including name, email, organization, gender and age if you choose
  to store PII &nbsp;(personally identifiable information) in Countly.
</p>
<p>
  &nbsp;Custom user properties are similar in logic to default and reserved user
  properties, &nbsp;in the sense that this information is stored at the user profile
  level. All the data &nbsp;(sessions, events, views, crashes etc.) originating
  from a user will get tagged &nbsp;with a historical snapshot of default, reserved,
  and custom user properties and &nbsp;will be available to be used in reporting
  and features such as &nbsp;<a href="/hc/en-us/articles/360037270112" target="_blank" rel="noopener">Cohorts</a>,
  &nbsp;<a href="/hc/en-us/articles/360036862312" target="_blank" rel="noopener">Funnels</a>,
  &nbsp;<a href="/hc/en-us/articles/360037260972" target="_blank" rel="noopener">Drill</a>,
  &nbsp;<a href="/hc/en-us/articles/900000812986" target="_blank" rel="noopener">Retention</a>
  &nbsp;and &nbsp;<a href="/hc/en-us/articles/360037639931" target="_blank" rel="noopener">Formulas</a>.
</p>
<p>
  &nbsp;Custom user properties consist of key-value pairs, where the value can
  be a string, &nbsp;number, boolean, or array. There are various modifiers available
  in the SDKs, &nbsp;Such as set, set once, push unique, increment, and multiply
  to update these &nbsp;as needed. For example, you can store account levels of
  your users in an &nbsp;<strong>accountType</strong>&nbsp;custom user property
  that can take values &nbsp;<strong>Basic</strong> or&nbsp;<strong>Premium</strong>
  to later on filter &amp; &nbsp;segment all reports based on the account type
  of your customers.
</p>
<h1>Events</h1>
<p>
  &nbsp;An "event" in Countly generally represents one of the following:
</p>
<ul>
  &nbsp;
  <li>
    &nbsp;&nbsp;&nbsp;An action of the user, such as an interaction with a single
    UI element, or &nbsp;&nbsp;&nbsp;set of elements &nbsp;
  </li>
  &nbsp;
  <li>
    &nbsp;&nbsp;&nbsp;An important milestone the user reaches after completing
    other actions, such &nbsp;&nbsp;&nbsp;as completing an application or onboarding
    process&nbsp; &nbsp;
  </li>
  &nbsp;
  <li>
    &nbsp;&nbsp;&nbsp;A transaction that takes place after one or more actions
    of the user, such &nbsp;&nbsp;&nbsp;as a backend API returning a result &nbsp;
  </li>
</ul>
<p>
  &nbsp;It is important to note that events aren't designed only to track simple
  user &nbsp;interactions such as "user clicked this button". The way you define
  events in &nbsp;your app determines the depth of insights you can get from Countly.
  Tracking &nbsp;everything you possibly can or tracking very little is equally
  bad. An ideal &nbsp;strategy is collecting the needs of various departments in
  your organization &nbsp;that'll take advantage of Countly. As a common example;
</p>
<ul>
  &nbsp;
  <li>
    &nbsp;&nbsp;&nbsp;The Product team will want to check feature usage; they
    will need multiple events &nbsp;&nbsp;&nbsp;that show how users interact
    with various application features &nbsp;
  </li>
  &nbsp;
  <li>
    &nbsp;&nbsp;&nbsp;Customer experience &amp; success team will want to understand
    the paths users &nbsp;&nbsp;&nbsp;go through (such as during onboarding)
    and get stuck in, and will need customized &nbsp;&nbsp;&nbsp;events as milestone
    indicators &nbsp;
  </li>
  &nbsp;
  <li>
    &nbsp;&nbsp;&nbsp;The Engineering team will want to get transactions &amp;
    statutes that are created &nbsp;&nbsp;&nbsp;after users' interaction with
    the UI layer thus, they'll need events or event &nbsp;&nbsp;&nbsp;segments
    that they can take advantage of &nbsp;
  </li>
  &nbsp;
  <li>
    &nbsp;&nbsp;&nbsp;CXOs and managers will want to see higher-level metrics
    or KPIs; thus this &nbsp;&nbsp;&nbsp;higher-level data should exist either
    as dedicated events or as individual ones &nbsp;&nbsp;&nbsp;to be used while
    constructing complex metrics using &nbsp;&nbsp;&nbsp;<a href="/hc/en-us/articles/360037639931" target="_blank" rel="noopener">Formulas</a>
    &nbsp;
  </li>
</ul>
<p>
  &nbsp;In its most complex form (there can, of course, be additional segments),
  an event's &nbsp;JSON representation looks like below. Only mandatory fields
  are &nbsp;<code>key</code> and <code>count</code> which are set when you call
  the recordEvent &nbsp;function in any given SDK. Optional <code>sum</code> property
  is useful when &nbsp;you would like to store an extra numerical value for an
  event; in the below example, &nbsp;we used it to store kilometers for a journey.
  Duration property represented as &nbsp;<code>dur</code> can be explicitly set,
  or you can take advantage of the &nbsp;<strong>timed events concept</strong>
  available in most SDKs.
</p>
<pre><span>{<br> &nbsp; "key": "Journey",<br> &nbsp; "count": 1,<br> &nbsp; "sum": 100,<br> &nbsp; "dur": 3600,<br> &nbsp; "segmentation": {<br>&nbsp; &nbsp; &nbsp; "Route Type": "Fastest"<br> &nbsp; }<br>}</span></pre>
<p>
  &nbsp;Now let's dive into event segments and strategies you can follow.
</p>
<h1>Deciding on event segments</h1>
<p>
  &nbsp;Segments are properties that add further detail and meaning to an event.
  Segments &nbsp;are important since most of the time you aren't only interested
  in how many times &nbsp;some general action happened but also will need to dig
  deeper, filter &nbsp;certain cases or group occurrences by different nuances
  of the action.
</p>
<p>
  &nbsp;From our event sample in the above section, thanks to the Route Type event
  segment, &nbsp;you can not only see overall journeys taking place but also see
  how many journeys were planned with the fastest, shortest or eco route types
  offered &nbsp;in the app. Furthermore, plugins like &nbsp;<a href="/hc/en-us/articles/360037270112" target="_blank" rel="noopener">Cohorts</a>,
  &nbsp;<a href="/hc/en-us/articles/360036862312" target="_blank" rel="noopener">Funnels</a>,
  &nbsp;<a href="/hc/en-us/articles/360037260972" target="_blank" rel="noopener">Drill</a>&nbsp;and
  &nbsp;<a href="/hc/en-us/articles/360037639931" target="_blank" rel="noopener">Formulas</a>
  &nbsp;these event segments will be available for use cases such as;
</p>
<ul>
  &nbsp;
  <li>
    &nbsp;&nbsp;&nbsp;Filter events where <strong>Route Type = Eco</strong> using
    Drill &nbsp;
  </li>
  &nbsp;
  <li>
    &nbsp;&nbsp;&nbsp;Construct 3 different funnels where the final step is the
    Journey event in all &nbsp;&nbsp;&nbsp;but filtered to be
    <strong>Route Type = Eco</strong>, &nbsp;&nbsp;&nbsp;<strong>Route Type = Fastest</strong>
    and &nbsp;&nbsp;&nbsp;<strong>Route Type = Shortest</strong> &nbsp;
  </li>
  &nbsp;
  <li>
    &nbsp;&nbsp;&nbsp;Create a behavioral cohort of users who did have a Journey
    with &nbsp;&nbsp;&nbsp;<strong>Route Type = Eco</strong> at least 2 times
    in the last 30 days (these &nbsp;&nbsp;&nbsp;are our eco-friendly personas,
    which we can target using &nbsp;&nbsp;&nbsp;<a href="/hc/en-us/articles/360037270492" target="_blank" rel="noopener">remote config</a>
    &nbsp;&nbsp;&nbsp;and &nbsp;&nbsp;&nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037270012-Push-notifications#sending-automated-push-notifications" target="_blank" rel="noopener">automated push notifications</a>)
    &nbsp;
  </li>
  &nbsp;
  <li>
    &nbsp;&nbsp;&nbsp;Construct 2 formulas in which you calculate the average
    kilometers driven per &nbsp;&nbsp;&nbsp;journey for
    <strong>Route Type = Shortest</strong> and &nbsp;&nbsp;&nbsp;<strong>Route Type = Fastest</strong>
    &nbsp;
  </li>
</ul>
<p>
  &nbsp;As you can tell from the above reporting examples, event segment selection
  is &nbsp;an important part of your success with reporting &amp; visualization
  in Countly.
</p>
<h1>Acquiring your application key and server url</h1>
<p>
  &nbsp;<strong>Acquiring the application key</strong>
</p>
<p>
  &nbsp;<span style="font-weight: 400;">Also referred to as "appKey" or "app_key" as shorthand, the application key is used to identify for which application, the information that the SDK has gathered, is tracked. You receive this value by creating a new application in Countly and accessing it on its application management screen.</span>
</p>
<p>
  &nbsp;<span style="font-weight: 400;"><strong>Note:&nbsp;</strong>Ensure you are using the App Key (found under Management -&gt; Applications) and not the API Key. Entering the API Key will not work.</span>
</p>
<p>
  &nbsp;<img src="/hc/article_attachments/9327716473881/001.png" alt="001.png">
</p>
<p>
  &nbsp;<strong>Acquiring the server URL</strong>
</p>
<p>
  &nbsp;<span style="font-weight: 400;">This is the domain from which you are accessing your Countly server. </span><span style="font-weight: 400;">During your SDK initialization you'll see a value such as 'url', 'server url' or something similar that you need to fill in. You have to fill that value with the IP or hostname of your server. For example, if you have Countly installed on 192.168.1.1, then inside the SDK you will need to write </span><span style="font-weight: 400;"><a href="https://192.168.1.1">https://192.168.1.1</a> , if the SSL configuration is complete, or <a href="http://192.168.1.1" target="_self" rel="undefined">http://192.168.1.1</a> if there is no SSL configuration.</span><span style="font-weight: 400;"> If there is a server name associated with your IP, that server name may also be used instead (e.g. <a href="https://countly.mycompany.com)." target="_self" rel="undefined">https://countly.mycompany.com)</a></span><span style="font-weight: 400;">.</span>
</p>
<h1>Handling login/logout in your app</h1>
<p>
  &nbsp;For a lot of apps, there is a login option. This allows you to confirm
  the identity &nbsp;of your users by cross-referencing them with your systems.
  That also adds &nbsp;two complications. First, multiple users can use the same
  app on the same device. &nbsp;The generated data would need to be assigned to
  the relevant user; therefore, &nbsp;the device ID needs to be changed. Second,
  the same user can log in to multiple &nbsp;devices. Therefore you need to use
  the same device ID on all of that user's devices. &nbsp;To achieve that, you
  would have an internal ID of your system or a derivative &nbsp;value that you
  can reliably generate.
</p>
<p>
  &nbsp;The first time you initialize a Countly SDK, you would allow the SDK to
  generate &nbsp;the device ID. When the user logs in to your app, you will change
  the device &nbsp;ID to the new ID that you generate. If this is the first time
  the user logs in, &nbsp;you will change the device ID with merging. You &nbsp;would
  change the device ID without merging on any follow-up logins. This way, you can
  assign the events &nbsp;generated by the user before the first login to the user
  that logs in.
</p>
<p>
  &nbsp;When a user logs out, you have 2 options. First, you would not change the
  device This way, you would also assign any follow-up events to the last user
  signed in, and those events would be sent as they happen. Second, if the &nbsp;SDK
  supports temporary ID mode; you can enter that when logout happens. This &nbsp;way,
  you would assign follow-up events to the user who would sign in next. &nbsp;The
  downside to the temporary ID approach is that no events would be sent while &nbsp;the
  user is not logged in. Both of these approaches not only solve a server-side
  &nbsp;performance issue but also eliminates the issue with inflated user counts.
  We &nbsp;recommend you choose the first logout option.
</p>
<p>
  &nbsp;A key SDK feature that allows you to do this is the ability to see the
  device &nbsp;ID type. The 2 important things that you want to differentiate are
  if the ID is &nbsp;generated by the SDK or if it's a custom ID provided by you.
  If the ID is generated &nbsp;by the SDK, then, you can assume that the user has
  not logged in before and when &nbsp;changing the device ID, you need to do that
  with merging. If the device ID is &nbsp;a custom one, then you can assume that
  you have already changed the ID before &nbsp;and need to perform the current
  change without merging.
</p>
<p>Here are a few sample login implementations of this flow:</p>
<h2>Android</h2>
<pre><span>public void </span><span>Login</span>() {<br>&nbsp; &nbsp; <span>String newId </span>= <span>"SomeValue"</span>;<br>&nbsp; &nbsp; <span>if </span>(<span>Countly</span>.<span>sharedInstance</span>().getDeviceIDType() == <span>DeviceId</span>.<span>Type</span>.<span>DEVELOPER_SUPPLIED</span>) {<br>&nbsp; &nbsp; &nbsp; &nbsp; <span>// an ID was provided by the host app previously<br></span><span>&nbsp; &nbsp; &nbsp; &nbsp; // we can assume that a device ID change with merge was executed previously<br></span><span>&nbsp; &nbsp; &nbsp; &nbsp; // now we change it without merging<br></span><span>&nbsp; &nbsp; &nbsp; &nbsp; </span><span>Countly</span>.<span>sharedInstance</span>().changeDeviceIdWithoutMerge(<span>DeviceId</span>.<span>Type</span>.<span>DEVELOPER_SUPPLIED</span>, <span>newId</span>);<br>&nbsp; &nbsp; } <span>else </span>{<br>&nbsp; &nbsp; &nbsp; &nbsp; <span>// SDK generated ID<br></span><span>&nbsp; &nbsp; &nbsp; &nbsp; // we change device ID with merge so that data is combined<br></span><span>&nbsp; &nbsp; &nbsp; &nbsp; </span><span>Countly</span>.<span>sharedInstance</span>().changeDeviceIdWithMerge(<span>newId</span>);<br>&nbsp; &nbsp; }<br>}</pre>
<h2>iOS</h2>
<pre class="c-mrkdwn__pre" data-stringify-type="pre">public static void login()<br> &nbsp;<wbr> &nbsp;<wbr>{<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>DeviceId.Type type = Countly.sharedInstance().getDeviceIDType();<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>if(type.equals(DeviceId.Type.DEVELOPER_SUPPLIED))<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>{<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Countly.sharedInstance().changeDeviceIdWithoutMerge(DeviceId.Type.DEVELOPER_SUPPLIED,<span class="hljs-string">@"usersNewID"</span>);<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>}<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>else<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>{<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Countly.sharedInstance().changeDeviceIdWithMerge(<span class="hljs-string">@"usersNewID"</span>);<br> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr> &nbsp;<wbr>}<br> &nbsp;<wbr> &nbsp;<wbr>}</pre>
<h1>
  &nbsp;Using the Countly SDK's with iOS and Android widgets and watches
</h1>
<p>
  &nbsp;With mobile devices, there are 3 different modalities that a user can interact
  &nbsp;with: phone app, phone widget, and watch app. When designing a product
  that spans &nbsp;all three worlds, the goal is to track the user's lifecycle
  across all &nbsp;of them.
</p>
<p>
  &nbsp;To perform this cross-modality tracking, care must be given that tracking
  is &nbsp;performed with the same device ID across all of them. If the device
  ID to which &nbsp;the event or session is attributed would not be the same across
  all devices &nbsp;and modalities, then the same user would be counted as a separate
  person on one &nbsp;of them.
</p>
<p>
  &nbsp;This also means that if the user's device ID changes, this change needs
  &nbsp;to be synchronized across all modalities/apps.
</p>
<p>This can be achieved in 2 general approaches:</p>
<ol>
  &nbsp;
  <li>
    &nbsp;&nbsp;&nbsp;Performing data recording at each location separately -
    each modality integrates, &nbsp;&nbsp;&nbsp;configures, and initializes the
    Countly SDK separately. Device ID synchronization &nbsp;&nbsp;&nbsp;needs
    to be performed manually across all modalities. This would be accomplished
    &nbsp;&nbsp;&nbsp;either by using some platform-provided method to perform
    direct communication &nbsp;&nbsp;&nbsp;or using an external device (for example,
    a server) to perform a centralized &nbsp;&nbsp;&nbsp;exchange. Alternatively,
    every modality needs a way to create the same device &nbsp;&nbsp;&nbsp;ID
    without direct cross-synchronization. &nbsp;
  </li>
  &nbsp;
  <li>
    &nbsp;&nbsp;&nbsp;Performing data recording at a central location and proxying
    data recording &nbsp;&nbsp;&nbsp;from each non-app modality eliminates the
    need for synchronization as only one instance of the SDK is initialized and
    configured. Device ID changes &nbsp;&nbsp;&nbsp;are immediately taken into
    account when they happen. Since cross-device recording &nbsp;&nbsp;&nbsp;is
    centralized, views and sessions must be recorded manually. The main &nbsp;&nbsp;&nbsp;issue
    with this approach is that there will be times when the main app might &nbsp;&nbsp;&nbsp;be
    out of reach for proxy recording or might not be running. &nbsp;
  </li>
</ol>
<p>
  &nbsp;To differentiate from which modality the event came from, you can use a
  custom &nbsp;segmentation value that shows that. Every unique value would indicate
  a separate &nbsp;modality.
</p>
<p>
  &nbsp;<strong>Notes for native iOS integration</strong>
</p>
<p>
  &nbsp;The general recommendation is to have Countly integrated into each separate
  modality &nbsp;as that seems to present the least amount of issues. If the modalities&nbsp;
  &nbsp;used are from the same developer account, then an internal communication
  &nbsp;channel should be available to them. If they are not on the same developer
  account,&nbsp; &nbsp;an outside synchronization mechanism will need to be used.
</p>
<p>
  &nbsp;For additional integration details, you would also have a look at &nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#watchos-integration" target="_self">this</a>
  &nbsp;section.
</p>
<p>
  &nbsp;<strong>Notes for native Android integration</strong>
</p>
<p>
  &nbsp;Due to the way the SDK is currently designed, integrating the SDK in a
  widget &nbsp;will cause crashes. Therefore the recommendation is to proxy the
  tracking requests &nbsp;to the host application. Shared preferences could potentially
  be used to achieve &nbsp;this.
</p>
<p>
  &nbsp;The SDK would be directly integrated with the watch modality, and then
  synchronization &nbsp;would be done with shared preferences.
</p>
<p>
  &nbsp;<strong>Notes for Flutter integration</strong>
</p>
<p>
  &nbsp;If you have a Flutter app, there doesn't seem to be an easy way to integrate
  &nbsp;other modalities. To achieve that, you would need to create them using
  the native &nbsp;platform languages and integrate the native Countly SDK's. In
  that case, the &nbsp;recommendations from the previous sections would apply.
</p>
<h1>How to validate your Countly integration?</h1>
<p>
  &nbsp;After you have integrated the Countly SDK into your app or website, to
  the best &nbsp;of your ability, whether you see some data or not in your Countly
  server, you &nbsp;should normally verify your integration by checking if everything
  is working &nbsp;as expected, both on your Countly server and your app/website.
  To have the most &nbsp;optimized verification process, we recommend you to go
  through the following steps &nbsp;for these cases of integration validation and
  also for debugging if you are seeing &nbsp;partial or no data at all on your
  server.
</p>
<h2>1. Check SDK logs</h2>
<p>
  &nbsp;As part of the process of integration verification, you would want to enable
  &nbsp;logging in to the SDK and have a look at the printed-out messages. If there
  were a warning, errors, or deprecation messages, it would indicate potential
  problems &nbsp;and action items that need to be fixed. Logging can be enabled
  during the SDK &nbsp;initialization, and the way you do that differs slightly
  from SDK to SDK. For &nbsp;specifics on how to enable it, you would want to check
  the documentation of the &nbsp;specific SDK that you are using from &nbsp;<a href="https://support.count.ly/hc/en-us/sections/360007310512-SDKs">here</a>.
</p>
<p>
  &nbsp;After enabling SDK side logging, you would want to run your app or website
  and &nbsp;check the debug messages that are printed in the respective console.
  The specific &nbsp;location of that would change depending on the platform and
  SDK.
</p>
<p>
  &nbsp;<img src="/hc/article_attachments/9327716376601/002.png" alt="002.png">
</p>
<p>
  &nbsp;<span style="font-weight: 400;">Check if requests are being created - this means you need to check whether you are calling SDK methods to actually send information to the server and that the SDK has been implemented correctly.</span>
</p>
<p>
  &nbsp;<span style="font-weight: 400;">Also, check if requests fail or are successfully sent to the server because if they fail, maybe the server is not reachable from this specific network, or you made a mistake when providing the URL to the server.</span>
</p>
<h2>2. Check Request Logs</h2>
<p>
  &nbsp;Next, you would want to verify that your Countly server is receiving data
  from &nbsp;<span style="font-weight: 400;"><code>Utilities &gt; Request Logs</code></span>.
  &nbsp;<span style="font-weight: 400;">Should there be an issue, the request logs usually state what this problem is about, why the request was not processed, or why incoming data may be incorrect - such as sending data for the incorrect app type, sending duplicate requests, incorrectly set-up parameter tampering, etc.</span>
</p>
<p>
  &nbsp;<img src="/hc/article_attachments/9327716734617/003.png" alt="003.png">
</p>
<h2>3. Make sure you have the correct configuration</h2>
<p>
  &nbsp;Here the most important thing is to verify if your 'app_key' and 'URL'
  values &nbsp;are entered correctly. For more information on making sure that
  you are using &nbsp;your correct 'app_key' and server URL, you can check out
  the following section &nbsp;<a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#acquiring-your-application-key-and-server-url">here</a>.
</p>
<h2>4. Check your Countly server</h2>
<p>
  &nbsp;If you have checked your SDK logs and everything seems to be working fine
  in &nbsp;your app or website, it is time to check Countly if the planned data
  is recorded &nbsp;as expected. As a simple test, you can simply open User Profiles
  in Countly to &nbsp;see if your app/website was able to connect and recognized
  as a user in your &nbsp;Countly server. If it is, you are good to go, and you
  can stop here on the list.
</p>
<p>
  &nbsp;<img src="/hc/article_attachments/9327773628825/004.png" alt="004.png">
</p>
<p>
  &nbsp;In case it seems like some data is not being recorded, it can be due to
  some &nbsp;requests being rejected related to problems with the checksum or sometimes
  requests &nbsp;might be dropped if there are filtering rules set to do that.
  Sometimes filtering &nbsp;rules target more things than planned by accident.&nbsp;
  For debugging &nbsp;those issues and others, keep reading.
</p>
<h2>5. Check the server for errors</h2>
<p>
  &nbsp;<span style="font-weight: 400;">Check <code>Management &gt; Logs &gt; Api Log</code></span><span style="font-weight: 400;"> for errors. Chances are, if there is a problem/bug with a specific plugin processing information, there would be new errors in the logs.</span>
</p>
<p>
  &nbsp;<img src="/hc/article_attachments/9327773899289/005.png" alt="005.png">
</p>
<h2>6. Check plugins</h2>
<p>
  &nbsp;Some plugins that might be necessary to process data and provide functionalities
  &nbsp;you want might not be activated, or you might have accidentally disabled
  them. &nbsp;You can check your plugins' status from &nbsp;<span style="font-weight: 400;"><code>Management &gt; Feature Management<br></code></span>
</p>
<p>
  &nbsp;<img src="/hc/article_attachments/9327717115161/006.png" alt="006.png">
</p>
<h2>7. Check Filtering rules</h2>
<p>
  &nbsp;<span style="font-weight: 400;">Events or requests may be blocked. In this case, check <code>Main menu&gt; Utilities &gt; Filtering rules</code></span><span style="font-weight: 400;"> to see whether there are any rules that block events or any requests.</span>
</p>
<p>
  &nbsp;<img src="/hc/article_attachments/9327774197657/007.png" alt="007.png">
</p>
<h2>8. Check event limits</h2>
<p>
  &nbsp;<span style="font-weight: 400;">The event name limit may be exceeded (the limit is 100, by default), and may be adjusted under <code>Management &gt; Settings &gt; API &gt; Data Limits&gt; Max unique event key</code>.</span>
</p>
<p>
  &nbsp;<img src="/hc/article_attachments/9327774290713/008.png" alt="008.png">
</p>
<h2>9. Check checksum</h2>
<p>
  &nbsp;Some &nbsp;<span>SDKs provide an option to send a checksum along the request data to prevent data breach by a middleman. If you have a set a salt for checksum in your SDK but did not set it at your server or typed it wrongly, and vise versa, you should check your salt value from <span style="font-weight: 400;"><code>Management &gt; Applications &gt; Salt for checksum</code></span>.</span>
</p>
<p>
  &nbsp;<img src="/hc/article_attachments/9327717836441/009.png" alt="009.png">
</p>
<h2>10. Check time zone</h2>
<p>
  &nbsp;<span style="font-weight: 400;">Your time zone may be different from the application’s time zone, explaining why it takes some time for you to be able to see events on the graph, something which should be available to you without delay. You can edit your time zone from <span><code>Management &gt; Applications &gt; Salt for checksum</code></span>.</span>
</p>
<p>
  &nbsp;<img src="/hc/article_attachments/9327717905689/010.png" alt="010.png">
</p>
<h1>How long does it take for my data to show up on Countly?</h1>
<p>
  &nbsp;When you are checking Countly and sending events from your app or website,
  you &nbsp;might realize that sometimes there is a delay for the data to show
  up there. &nbsp;This is an expected behavior stemming from the internal logic
  of the Countly &nbsp;SDKs and the potential server-side calculations.
</p>
<p>
  &nbsp;<strong>SDK Side Processes</strong>
</p>
<p>
  &nbsp;In some cases, there might just be a connection issue. Either the user
  is offline &nbsp;or unable to reach your server (due to server maintenance or
  other issues). Thus &nbsp;they would not be able to send data to the server.
  If, during this loss of connection, &nbsp;the SDK is not able to perform any
  network activity, it will wait for a while &nbsp;before reattempting the upload
  of recorded information. By default, this delay &nbsp;is 60 seconds (can be changed
  during init) and is tied to the session update &nbsp;tick interval.
</p>
<p>
  &nbsp;The second aspect that can influence this is the event queue. Before we
  sent &nbsp;the recorded events to the server, we try to cache them to optimize
  the networking. &nbsp;They are cached until their amount exceeds the threshold
  (by default 100, but &nbsp;can be configured), or the session update tick happens,
  or some other internal &nbsp;trigger happens.
</p>
<p>
  &nbsp;<strong>Server Side Processes</strong>
</p>
<p>
  &nbsp;In addition to this, there can be server-side calculations that can add
  additional &nbsp;delay. Depending on where you are expecting the changes to show
  up, the types &nbsp;and the length of the calculations involved would differ.
  For example, a cohort &nbsp;can take minutes up to hours to process before showing
  up on Countly. But most &nbsp;data would show up within seconds after reaching
  your Countly Server.
</p>
<h1>Is my SDK version compatible with my server?</h1>
<p>
  &nbsp;If you have checked your Countly server and SDK versions, you might &nbsp;have
  noticed that they most likely do not match. Due to the way our development &nbsp;is
  structured, our Countly server releases happen more often than any single &nbsp;SDK.
  Usually, this will lead you to see that your server version is higher than &nbsp;your
  SDK version, and that is fine.
</p>
<p>
  &nbsp;Our guidelines are that the major version of your server should be the
  same or &nbsp;higher than the major version of the SDK you are using. Our versioning
  &nbsp;scheme for our server releases and SDKs has 3 numbers separated by dots,
  something &nbsp;like "22.02.3". The first two numbers are what we call the major
  version &nbsp;and those that you should be paying attention to ("22.02.X").&nbsp;
</p>