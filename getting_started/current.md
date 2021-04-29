<p>
  Countly provides various functionality in different SDKs targeted for mobile,
  web, desktop, server to server and IoT use cases. For a feature comparison in
  all SDKs,
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
  By default Countly generates an anonymous identifier to uniquely identify a device
  or browser. Total users metric for any period is based on unique number of device
  ids Countly Server receives requests from. Similarly, users list in
  <a href="/hc/en-us/articles/360037630571" target="_blank" rel="noopener">User Profiles</a>
  section is a list of anonymous devices Countly Server is receiving data from.
  All data originating from a single device, including sessions, events, views,
  crashes, is grouped under these individual profiles since all the data is tagged
  with the originating device id.
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
  User properties play an important role not only in reporting, but also in various
  other cases such as personalizing push notifications and creating conditional
  remote configuration variables.
</p>
<p>
  Most Countly SDKs send some user properties together with the session request&nbsp;
  which is triggered automatically when the app is launched, user lands on a website,
  or manually in some cases such as server to server SDK usage. These properties,
  which we call default user properties, are meta data including but not limited
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
  <li>Filter events where Route Type = Eco using Drill</li>
  <li>
    Construct 3 different funnels where final step is the Journey event in all
    but filtered to be Route Type = Eco, Route Type = Fastest and Route Type
    = Shortest
  </li>
  <li>
    Create a behavioral cohort of users who did have a Journey with Route Type
    = Eco at least 2 times in the last 30 days (these are our eco friendly personas
    which we can target using
    <a href="/hc/en-us/articles/360037270492" target="_blank" rel="noopener">remote config</a>
    and
    <a href="https://support.count.ly/hc/en-us/articles/360037270012-Push-notifications#sending-automated-push-notifications" target="_blank" rel="noopener">automated push notifications</a>)
  </li>
  <li>
    Construct 2 formulas in which you calculate average kilometers driven per
    journey for Route Type = Shortest and Route Type = Fastest
  </li>
</ul>
<p>
  As you can tell from the above reporting examples, event segment selection is
  an important part of your success with reporting &amp; visualization in Countly.
</p>
<p>&nbsp;</p>