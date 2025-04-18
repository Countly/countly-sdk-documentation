<p>
  Countly provides various functionality in different SDKs targeted for mobile,
  web, desktop, and server-to-server use cases. For a feature comparison in all
  SDKs,
  <a href="/hc/en-us/articles/360037236571#h_01H9QCP8G52MSJGQZCFGV0HMWM" target="_self">please check this table</a>.
</p>
<p>
  There are common concepts in all Countly SDKs, and this document is intended
  to be a universal getting started guide without getting into the implementation
  details of individual SDKs. To get more information on platform-specific implementation,
  <a href="/hc/en-us/articles/360037236571#h_01H9QCP8G5Y9PZJGERZ4XWYDY9" target="_self">please refer to the documentation</a>
  of the SDK of your choice.
</p>
<h1 id="h_01HABSX9KWA69NQG6P31P1EW33">User/Device Identification</h1>
<p>
  By default, Countly generates an anonymous identifier to uniquely identify a
  device or browser. The total users metric for any period is based on a unique
  number of device ids the Countly Server receives requests from. Similarly, users
  list in
  <a href="/hc/en-us/articles/4403281285913" target="_blank" rel="noopener">User Profiles</a>.
  The section lists anonymous devices from which the Countly Server is receiving
  data. All data originating from a single device, including sessions, events,
  views, and crashes, are grouped under these individual profiles since all the
  data is tagged with the originating device id.
</p>
<p>
  Most Countly SDKs, including
  <a href="/hc/en-us/articles/360037753511#h_01HAVHW0RP2DPTREKXC0Q8T6QA" target="_blank" rel="noopener">iOS</a>,
  <a href="/hc/en-us/articles/360037754031#h_01HAVQDM5TPKRQAZGXW73GBM90" target="_blank" rel="noopener">Android</a>,
  <a href="/hc/en-us/articles/360037813231#h_01HAVQNJQR1HPTNTJ711DVNFD1" target="_blank" rel="noopener">React Native</a>,
  <a href="/hc/en-us/articles/360037944212#h_01H930GAQ682G16Z7M570XKSPD" target="_blank" rel="noopener">Flutter</a>,
  and
  <a href="/hc/en-us/articles/360037441932#h_01HABTQ438HCZ8FJVAE34W49KP" target="_blank" rel="noopener">Web</a>,
  offer a mechanism to change/update this default device id for cases where you
  already have a better identifier, such as an email address or account id or you
  get this information at some point in user journey such as after user logs into
  your application. For an in-depth analysis of different device/user identification
  strategies,
  <a href="/hc/en-us/articles/900002449486" target="_self">please check out this post</a>.
</p>
<h1 id="h_01HABSX9KW1JT1N5C7C4D6NMBY">Deciding on Custom User Properties</h1>
<p>
  User properties play an important role not only in reporting but also in various
  other cases, such as personalizing push notifications and creating conditional
  remote configuration variables.
</p>
<p>
  Most Countly SDKs send some user properties together with the session request
  triggered automatically when the app is launched, the user lands on a website,
  or manually in some cases, such as server-to-server SDK usage. These properties,
  which we call default user properties, are metadata, including but not limited
  to the app version, device, platform, and platform version.
</p>
<p>
  Furthermore, there are some reserved user properties that you can choose to set,
  including name, email, organization, gender, and age if you choose to store PII
  (personally identifiable information) in Countly.
</p>
<p>
  Custom user properties are similar in logic to default and reserved user properties
  in the sense that this information is stored at the user profile level. All the
  data (sessions, events, views, crashes, etc.) originating from a user will get
  tagged with a historical snapshot of default, reserved, and custom user properties
  and will be available to be used in reporting and features such as
  <a href="/hc/en-us/articles/4405086657049" target="_blank" rel="noopener">Cohorts</a>,
  <a href="/hc/en-us/articles/4437429216409" target="_blank" rel="noopener">Funnels</a>,
  <a href="/hc/en-us/articles/4444087015065" target="_blank" rel="noopener">Drill</a>,
  <a href="/hc/en-us/articles/4414450842009" target="_blank" rel="noopener">Retention</a>,
  and
  <a href="/hc/en-us/articles/4405186350105" target="_blank" rel="noopener">Formulas</a>.
</p>
<p>
  Custom user properties consist of key-value pairs, where the value can be a string,
  number, boolean, or array. There are various modifiers available in the SDKs,
  such as 'set,' 'set once,' 'push unique,' 'increment,' and 'multiply' to update
  these as needed. For example, you can store account levels of your users in an
  <strong>accountType</strong>&nbsp;custom user property that can take values
  <strong>Basic</strong> or&nbsp;<strong>Premium</strong> to later on filter &amp;
  segment all reports based on the account type of your customers.
</p>
<h1 id="h_01HABSX9KX2PKHQWQSJMX083Q6">Events</h1>
<p>
  An "event" in Countly generally represents one of the following:
</p>
<ul>
  <li>
    An action of the user, such as an interaction with a single UI element or
    set of elements.
  </li>
  <li>
    An important milestone the user reaches after completing other actions, such
    as completing an application or onboarding process.&nbsp;
  </li>
  <li>
    A transaction that takes place after one or more actions of the user, such
    as a backend API returning a result.
  </li>
</ul>
<p>
  It is important to note that events aren't designed only to track simple user
  interactions such as "user clicked this button." The way you define events in
  your app determines the depth of insights you can get from Countly. Tracking
  everything you possibly can or tracking very little is equally bad. An ideal
  strategy is collecting the needs of various departments in your organization
  that'll take advantage of Countly. As a common example;
</p>
<ul>
  <li>
    The Product team will want to check feature usage; they will need multiple
    events that show how users interact with various application features.
  </li>
  <li>
    The customer experience &amp; success team will want to understand the paths
    users go through (such as during onboarding) and get stuck in and will need
    customized events as milestone indicators.
  </li>
  <li>
    The Engineering team will want to get transactions &amp; statutes that are
    created after users' interaction with the UI layer. Thus, they'll need events
    or event segments that they can take advantage of.
  </li>
  <li>
    CXOs and managers will want to see higher-level metrics or KPIs; thus this
    higher-level data should exist either as dedicated events or as individual
    ones to be used while constructing complex metrics using
    <a href="/hc/en-us/articles/4405186350105" target="_blank" rel="noopener">Formulas</a>.
  </li>
</ul>
<p>
  In its most complex form (there can, of course, be additional segments), an event's
  JSON representation looks like below. The only mandatory fields are
  <code>key</code> and <code>count</code> which are set when you call the recordEvent
  function in any given SDK. Optional <code>sum</code> property is useful when
  you would like to store an extra numerical value for an event; in the below example,
  we used it to store kilometers for a journey. The duration property represented
  as <code>dur</code> can be explicitly set, or you can take advantage of the
  <strong>timed events concept</strong> available in most SDKs.
</p>
<pre><span>{<br>   "key": "Journey",<br>   "count": 1,<br>   "sum": 100,<br>   "dur": 3600,<br>   "segmentation": {<br>      "Route Type": "Fastest"<br>   }<br>}</span></pre>
<p>
  Now let's dive into event segments and strategies you can follow.
</p>
<h1 id="h_01HABSX9KXG2XKEW7JD55K8WNA">Deciding on Event Segments</h1>
<p>
  Segments are properties that add further detail and meaning to an event. Segments
  are important since, most of the time, you aren't only interested in how many
  times some general action happened but also will need to dig deeper and filter
  certain cases or group occurrences by different nuances of the action.
</p>
<p>
  From our event sample in the above section, thanks to the Route Type event segment,
  you can not only see overall journeys taking place but also see how many journeys
  were planned with the fastest, shortest, or eco route types offered in the app.
  Furthermore, plugins like
  <a href="/hc/en-us/articles/4405086657049" target="_blank" rel="noopener">Cohorts</a>,
  <a href="/hc/en-us/articles/4437429216409" target="_blank" rel="noopener">Funnels</a>,
  <a href="/hc/en-us/articles/4444087015065" target="_blank" rel="noopener">Drill</a>,
  and
  <a href="/hc/en-us/articles/4405186350105" target="_blank" rel="noopener">Formulas</a>.
  these event segments will be available for use cases such as;
</p>
<ul>
  <li>
    Filter events where <strong>Route Type = Eco</strong> using Drill.
  </li>
  <li>
    Construct three different funnels where the final step is the Journey event
    in all but filtered to be <strong>Route Type = Eco</strong>,
    <strong>Route Type = Fastest,</strong> and
    <strong>Route Type = Shortest.</strong>
  </li>
  <li>
    Create a behavioral cohort of users who did have a Journey with
    <strong>Route Type = Eco</strong> at least two times in the last 30 days
    (these are our eco-friendly personas, which we can target using
    <a href="/hc/en-us/articles/9895605514009" target="_blank" rel="noopener">remote config</a>
    and
    <a href="/hc/en-us/articles/4405405459225" target="_blank" rel="noopener">push notifications</a>).
  </li>
  <li>
    Construct two formulas in which you calculate the average kilometers driven
    per journey for <strong>Route Type = Shortest</strong> and
    <strong>Route Type = Fastest.</strong>
  </li>
</ul>
<p>
  As you can tell from the above reporting examples, event segment selection is
  an important part of your success with reporting &amp; visualization in Countly.
</p>
<h1 id="h_01HABSX9KX44C9SF48WRPQNCP3">Acquiring Your Application Key and Server URL</h1>
<p>
  <strong>Acquiring the Application Key</strong>
</p>
<p>
  <span style="font-weight: 400;">Also referred to as "appKey" or "app_key" as shorthand, the application key is used to identify the application for which the information has been gathered by the SDK. It is also tracked. You receive this value by creating a new application in Countly and accessing it on its application management screen.</span>
</p>
<p>
  <span style="font-weight: 400;"><strong>Note:&nbsp;</strong>Ensure you are using the App Key (found under <strong>Management -&gt; Applications</strong>) and not the API Key. Entering the API Key will not work.</span>
</p>
<p>
  <img src="/guide-media/01GVC1KFSK5GH4QF3XNTMWRWXE" alt="001.png">
</p>
<p>
  <strong>Acquiring the Server URL</strong>
</p>
<p>
  <span style="font-weight: 400;">This is the domain from which you are accessing your Countly server. </span><span style="font-weight: 400;">During your SDK initialization, you'll see a value such as 'url', 'server url,' or something similar that you need to fill in. You have to fill that value with the IP or hostname of your server. For example, if you have Countly installed on 192.168.1.1, then inside the SDK, you will need to write </span>
  <span style="font-weight: 400;"><a href="https://192.168.1.1">https://192.168.1.1</a> , if the SSL configuration is complete, or <a href="http://192.168.1.1" target="_self" rel="undefined">http://192.168.1.1</a> if there is no SSL configuration.</span><span style="font-weight: 400;"> If there is a server name associated with your IP, that server name may also be used instead (e.g. <a href="https://countly.mycompany.com)." target="_self" rel="undefined">https://countly.mycompany.com)</a></span><span style="font-weight: 400;">.</span>
</p>
<h1 id="h_01HABSX9KX61TSEGKY47F43KP3">Handling Login/Logout in Your App</h1>
<p>
  Many apps use a login feature to verify user identities and connect them to your
  systems. This introduces two main challenges: managing data for multiple users
  on the same device and ensuring a consistent ID for a single user across multiple
  devices. To handle this, you’ll use a unique internal ID from your system.
</p>
<p>
  The first time you initialize a Countly SDK, you would allow the SDK to generate
  the device ID. When the user logs in to your app, you will change the device
  ID to the new ID that you generate. You would also want to change the device
  ID on any follow-up logins. This way, you can assign the events generated by
  the user before the first login to the user that logs in.
</p>
<p>
  When you first initialize the Countly SDK, it generates a default device ID.
  Upon user login, you’ll update this to your generated ID and do so for subsequent
  logins to accurately link events to the right user. For logouts, you have two
  options: keep the current device ID, so events continue being assigned to the
  last user, or switch to a temporary ID mode (if supported), which pauses event
  tracking until a new user logs in. We generally recommend keeping the device
  ID for smooth performance and accurate user counts.
</p>
<p>
  Most Countly SDKs offer a 'setId' function to simplify this process, automatically
  managing device ID changes. For more advanced needs, check out the SDK's detailed
  documentation.
</p>
<p>
  <button class="article-unsubscribe" style="padding: 10px 20px;" onclick="window.open('/hc/en-us/articles/360037754031#h_01HAVQDM5TPKRQAZGXW73GBM90', '_blank')">Android</button>
  <button class="article-unsubscribe" style="padding: 10px 20px;" onclick="window.open('/hc/en-us/articles/360037753511#h_01HAVHW0RP2DPTREKXC0Q8T6QA', '_blank')">iOS</button>
  <button class="article-unsubscribe" style="padding: 10px 20px;" onclick="window.open('/hc/en-us/articles/360037441932#h_01HABTQ438H09ECC7YDDKNN68R', '_blank')">Web</button>
  <button class="article-unsubscribe" style="padding: 10px 20px;" onclick="window.open('/hc/en-us/articles/360037813231#h_01HAVQNJQR1HPTNTJ711DVNFD1', '_blank')">React Native</button>
  <button class="article-unsubscribe" style="padding: 10px 20px;" onclick="window.open('/hc/en-us/articles/360037944212#h_01H930GAQ682G16Z7M570XKSPD', '_blank')">Flutter</button>
</p>
<p>
  <button class="article-unsubscribe" style="padding: 10px 20px;" onclick="window.open('/hc/en-us/articles/360037813891#h_01HABV0K6CZSJPRK4RYG23YH7F', '_blank')">Java</button>
  <button class="article-unsubscribe" style="padding: 10px 20px;" onclick="window.open('/hc/en-us/articles/360037754691#h_01HABTXQF9N0EKQNJ65GX4DMRA', '_blank')">Windows</button>
  <button class="article-unsubscribe" style="padding: 10px 20px;" onclick="window.open('/hc/en-us/articles/360037813851#h_01HABTZ3151FMVABED60J1FB2Y', '_blank')">Unity</button>
  <button class="article-unsubscribe" style="padding: 10px 20px;" onclick="window.open('/hc/en-us/articles/360037442892#h_01JBXH7RBD0G8QM2FV7EBE6488', '_blank')">NodeJS</button>
</p>
<h1 id="h_01HABSX9KXE6YKVETHDWPP8J3K">How to Validate Your Countly Integration?</h1>
<p>
  After you have integrated the Countly SDK into your app or website, to the best
  of your ability, whether you see some data or not in your Countly server, you
  should normally verify your integration by checking if everything is working
  as expected, both on your Countly server and your app/website. To have the most
  optimized verification process, we recommend you go through the following steps
  for these cases of integration validation and also for debugging if you are seeing
  partial or no data at all on your server.
</p>
<h2 id="h_01HABSX9KXNHYXSPRJAT5Y3HNV">1. Check SDK Logs</h2>
<p>
  As part of the process of integration verification, you would want to enable
  logging into the SDK and have a look at the printed-out messages. If there were
  a warning, errors, or deprecation messages, it would indicate potential problems
  and action items that need to be fixed. Logging can be enabled during the SDK
  initialization, and the way you do that differs slightly from SDK to SDK. For
  specifics on how to enable it, you would want to check the documentation of the
  specific SDK that you are using from
  <a href="/hc/en-us/sections/360007310512">here</a>.
</p>
<p>
  After enabling SDK side logging, you would want to run your app or website and
  check the debug messages that are printed in the respective console. The specific
  location of that would change depending on the platform and SDK.
</p>
<p>
  <img src="/guide-media/01GVBGCQ4HAR5Z4K4MVEK32NR5" alt="002.png">
</p>
<p>
  <span style="font-weight: 400;">Check if requests are being created - this means you need to check whether you are calling SDK methods to actually send information to the server and that the SDK has been implemented correctly.</span>
</p>
<p>
  <span style="font-weight: 400;">Also, check if requests fail or are successfully sent to the server because if they fail, maybe the server is not reachable from this specific network, or you made a mistake when providing the URL to the server.</span>
</p>
<h2 id="h_01HABSX9KXG4X1GHAHGYH0KD5H">2. Check Incoming Data Logs</h2>
<p>
  Next, you would want to verify that your Countly server is receiving data from
  <span style="font-weight: 400;"><code>Utilities &gt; Incoming Data Logs</code></span>.
  <span style="font-weight: 400;">Should there be an issue, the request logs usually state what this problem is about, why the request was not processed, or why incoming data may be incorrect - such as sending data for the incorrect app type, sending duplicate requests, incorrectly setting up parameter tampering, etc.</span>
</p>
<p>
  <img src="/guide-media/01GSPV01NM0J5M7QS37M1ZX7RH" alt="003.png">
</p>
<h2 id="h_01HABSX9KXWWQ5RJAANWQW9TZ5">3. Make Sure You Have the Correct Configuration</h2>
<p>
  Here the most important thing is to verify if your 'app_key' and 'URL' values
  are entered correctly. For more information on making sure that you are using
  your correct 'app_key' and server URL, you can check out the following section
  <a href="/hc/en-us/articles/900000908046#h_01HABSX9KX44C9SF48WRPQNCP3">here</a>.
</p>
<h2 id="h_01HABSX9KX0S0QZQRNRBDXMADX">4. Check Your Countly Server</h2>
<p>
  If you have checked your SDK logs and everything seems to be working fine in
  your app or website, it is time to check Countly if the planned data is recorded
  as expected. As a simple test, you can simply open User Profiles in Countly to
  see if your app/website was able to connect and recognized as a user in your
  Countly server. If it is, you are good to go, and you can stop here on the list.
</p>
<p>
  <img src="/guide-media/01GVCKHJW3QZ4DTYW225P9Z0N8" alt="004.png">
</p>
<p>
  In case it seems like some data is not being recorded, it can be due to some
  requests being rejected related to problems with the checksum, or sometimes requests
  might be dropped if there are filtering rules set to do that. Sometimes filtering
  rules target more things than planned by accident. For debugging those issues
  and others, keep reading.
</p>
<h2 id="h_01HABSX9KXMSY6FYE5FM3AKWJ5">5. Check the Server for Errors</h2>
<p>
  <span style="font-weight: 400;">Check <code>Management &gt; Logs &gt; Api Log</code></span><span style="font-weight: 400;"> for errors. Chances are, if there is a problem/bug with a specific plugin processing information, there would be new errors in the logs.</span>
</p>
<p>
  <img src="/guide-media/01GVE6545N52SYETHG37K09YRG" alt="005.png">
</p>
<h2 id="h_01HABSX9KXNRDQBPWD59WNT11E">6. Check Plugins</h2>
<p>
  Some plugins that might be necessary to process data and provide functionalities
  you want might not be activated, or you might have accidentally disabled them.
  You can check your plugins' status from
  <span style="font-weight: 400;"><code>Management &gt; Feature Management</code><br></span>
</p>
<p>
  <img src="/guide-media/01GVDG0MQC6JS6JCMA3VRHH5X8" alt="006.png">
</p>
<h2 id="h_01HABSX9KXP2A8SC8GSTXSAPZ7">7. Check Filtering Rules</h2>
<p>
  <span style="font-weight: 400;">Events or requests may be blocked. In this case, check <code>Main menu&gt; Utilities &gt; Filtering rules</code></span><span style="font-weight: 400;"> to see whether there are any rules that block events or any requests.</span>
</p>
<p>
  <img src="/guide-media/01GVBGCRTDDND3BXXKN0XDP6ZA" alt="007.png">
</p>
<h2 id="h_01HABSX9KXN1T9ADXF3384ED3Y">8. Check Event Limits</h2>
<p>
  <span style="font-weight: 400;">The event name limit may be exceeded (the limit is 100, by default), and may be adjusted under <code>Management &gt; Settings &gt; API &gt; Data Limits&gt; Max unique event key</code>.</span>
</p>
<p>
  <img src="/guide-media/01GVCTF7AJCPNWYSMZKS7TYZ6R" alt="008.png">
</p>
<h2 id="h_01HABSX9KX1Q3KH8WMW3E77Z7W">9. Check Checksum</h2>
<p>
  Some
  <span>SDKs provide an option to send a checksum along the request data to prevent data breaches by a middleman. If you have set a salt for checksum in your SDK but did not set it at your server or mistyped it, and vice-versa, you should check your salt value from <span style="font-weight: 400;"><code>Management &gt; Applications &gt; Salt for checksum</code></span>.</span>
</p>
<p>
  <img src="/guide-media/01GVD4ND93MEXXJD0199N3ZHEZ" alt="009.png">
</p>
<h2 id="h_01HABSX9KXH4ABVRE3YADZA7J3">10. Check Time Zone</h2>
<p>
  <span style="font-weight: 400;">Your time zone may be different from the application’s time zone, explaining why it takes some time for you to be able to see events on the graph, something that should be available to you without delay. You can edit your time zone from <span><code>Management &gt; Applications &gt; Edit &gt; Select Time Zone</code></span>.</span>
</p>
<p>
  <img src="/guide-media/01GVAYP7QTW87W4Y1V2NT3Y3JF" alt="010.png">
</p>
<h1 id="h_01HABSX9KX8X421H9SSG0YDX7G">How Long Does It Take for My Data to Show Up on Countly?</h1>
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
  they would not be able to send data to the server. If, during this loss of connection,
  the SDK is not able to perform any network activity, it will wait for a while
  before reattempting the upload of recorded information. By default, this delay
  is 60 seconds (can be changed during init) and is tied to the session update
  tick interval.
</p>
<p>
  The second aspect that can influence this is the event queue. Before we send
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
<h1 id="h_01HABSX9KXMBCY10P5W8Z3YK4N">Is My SDK Version Compatible with My Server?</h1>
<p>
  If you have checked your Countly server and SDK versions, you might have noticed
  that they most likely do not match. Due to the way our development is structured,
  our Countly server releases happen more often than any single SDK. Usually, this
  will lead you to see that your server version is higher than your SDK version,
  and that is fine.
</p>
<p>
  Our guidelines are that the major version of your server should be the same or
  higher than the major version of the SDK you are using. Our versioning scheme
  for our server releases and SDKs has three numbers separated by dots, something
  like "22.02.3". The first two numbers are what we call the major version, and
  those are the ones that you should be paying attention to ("22.02.X").
</p>
<h1 id="h_01HABSX9KXC5S8Q1NQWDZ33HXC">Finding SDK Logs</h1>
<p>
  Ensure you have enabled SDK logs before proceeding with this process. For guidance
  on how to enable logs, refer to the
  <a href="/hc/en-us/sections/360007310512" target="_blank" rel="noopener">SDK documentation's</a>
  "Logging" or "Debug Mode" section.
</p>
<h2 id="h_01HABSX9KXC03DBM7JFA0CXW3Q">Apple Devices:</h2>
<ol>
  <li>Launch your application through Xcode.</li>
  <li>Access the Output tab (annotated as 1).</li>
  <li>Filter the logs by typing in "countly" (annotated as 2).</li>
</ol>
<p>
  <img src="/guide-media/01GVB6856FZT71BBAFJE754S09" alt="011.png">
</p>
<h2 id="h_01HABSX9KXS2ND6YQKFVC1PRWZ">Android Devices:</h2>
<ol>
  <li>Run your application on Android Studio.</li>
  <li>Open the Logcat tab (annotated as 1).</li>
  <li>Filter the logs by typing in "countly" (annotated as 2).</li>
</ol>
<p>
  <img src="/guide-media/01GVCKJ63A47W3426P5ABTF8T1" alt="012.png">
</p>
<h2 id="h_01HABSX9KXATKB9TQ36WBD7QAC">Web Browser:</h2>
<ol>
  <li>Open your website in a browser.</li>
  <li>Open the developer tools (typically by pressing F12).</li>
  <li>Select the Console tab (annotated as 1).</li>
  <li>
    Enable all log levels to view the SDK logs (annotated as 2).
  </li>
</ol>
<p>
  <img src="/guide-media/01GVBGM81XJNKR008JE3E1EF2B" alt="013.png">
</p>
<h1 id="h_01HST5HJHQ9APXY4KZ7R29A9ZQ">Best Practices for SDK Integration</h1>
<h2 id="h_01HST5HJHQRQV7TTF13BFD7XMG">SDK Integration to Constantly Running Platforms</h2>
<p>
  SDK integration to constantly running platforms, like servers or OSes, shares
  the same principles with other platforms; however, due to the continuous activity
  on these platforms, automatic session tracking can become a hinderance.
</p>
<p>
  Frequent session update calls to your Countly server can put a strain on its
  ability digest data and responsiveness. To mitigate this problem, we suggest
  reducing the frequency of your session update requests to the bare minimum.
</p>
<p>
  A 4-hour session update request interval is a recommended starting point to mitigate
  most issues. This value should be set at the init configuration object of your
  SDK and should also be changed at your server's Management &gt; Settings &gt;
  API &gt; Data Limits &gt; Maximal Session Duration section. You can reach the
  SDK-specific configuration settings from the corresponding documentation of your
  SDK
  <a href="/hc/en-us/sections/360007310512" target="_blank" rel="noopener">here</a>
</p>