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
  <span style="font-weight: 400;">Also called "appKey" as shorthand. The application key is used to identify for which application this information is tracked. You receive this value by creating a new application in your Countly dashboard and accessing it in its application management screen.</span>
</p>
<p>
  <span style="font-weight: 400;"><strong>Note:&nbsp;</strong>Ensure you are using the App Key (found under Management -&gt; Applications) and not the API Key. Entering the API Key will not work.</span>
</p>
<p>
  <strong>Acquiring the server URL</strong>
</p>
<p>
  <span style="font-weight: 400;">If you are using Countly Enterprise Edition trial servers, use&nbsp;<code>https://try.count.ly</code>,<span>&nbsp;</span><code>https://us-try.count.ly</code><span>&nbsp;</span>or<span>&nbsp;</span><code>https://asia-try.count.ly</code>&nbsp;It is basically the domain from which you are accessing your trial dashboard.</span>
</p>
<p>
  <span style="font-weight: 400;">If you use both Community Edition and Enterprise Edition, use your own domain name or IP address, such as </span><a href="https://example.com"><span style="font-weight: 400;">https://example.com</span></a><span style="font-weight: 400;">&nbsp;or&nbsp;</span><a href="https://ip/"><span style="font-weight: 400;">https://IP</span></a><span style="font-weight: 400;">&nbsp;(if SSL has been set up).</span>
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
  Using Countly SDK's with iOS and Android widgets and watches
</h1>
<p>
  With mobile devices, there are 3 different modalities that a user can interact
  with: phone app, phone widget, and watch app. When designing a product that spans
  all three worlds, the goal is usually to track the users lifecycle across all
  of them.
</p>
<p>
  To perform this cross-modality tracking, care must be given that tracking is
  performed with the same device ID across all of them. If the device ID, to which
  the event or session is attributed, would not be the same across all devices
  then the same user would be counted as a separate person on one of the devices.
</p>
<p>
  This also means that if the users device ID would change, this change needs to
  be synchronized across all modalities/apps.
</p>
<p>This can be achieved in 2 general approaches:</p>
<ol>
  <li>
    Performing data recording at each location separately - each modality integrates,
    configures, and initializes the Countly SDK separately. Device ID synchronization
    needs to be performed manually across all modalities. Alternatively, every
    modality needs a way to create the same device ID without cross-synchronization.
  </li>
  <li>
    Performing data recording at a central location and proxying data recording
    from each non-app modality - eliminates the need for synchronization as there
    is only one instance of the SDK initialized and configured. Device ID changes
    are immediately taken into account when they happen. Since cross-device recording
    is centralized, views and sessions need to be recorded manually. Another
    potential issue is that sometimes the main app might be out of reach for
    proxy recording.
  </li>
</ol>