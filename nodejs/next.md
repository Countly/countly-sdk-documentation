<p>
  This documentation shows how to use Countly NodeJS SDK to track your nodejs running
  device or server, like tracking your API. It applies to the SDK version 22.02.0.
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <span class="wysiwyg-font-size-large"><strong>Older documentation</strong></span>
  </p>
  <p>
    To access the documentation for version 20.11 and older, click
    <a href="https://support.count.ly/hc/en-us/articles/4410672825881" target="blank">here</a>.
  </p>
</div>
<p>
  Countly NodeJS runs with the following node versions and up:
</p>
<table style="border-collapse: collapse; width: 100%;" border="1">
  <tbody>
    <tr>
      <td class="wysiwyg-text-align-center" style="width: 20%;" colspan="5">Node Versions</td>
    </tr>
    <tr>
      <td class="wysiwyg-text-align-center" style="width: 20%;">^18</td>
      <td class="wysiwyg-text-align-center" style="width: 20%;">^17</td>
      <td class="wysiwyg-text-align-center" style="width: 20%;">^16</td>
      <td class="wysiwyg-text-align-center" style="width: 20%;">^14.15</td>
      <td class="wysiwyg-text-align-center" style="width: 20%;">^12.22</td>
    </tr>
  </tbody>
</table>
<p>
  Before starting, for those who have examined our mobile SDKs - we can tell that
  events or tags that are used in mobile SDKs are quite similar to those we use
  in Javascript code. For example, it's possible to modify custom property values
  of user details, with modification commands like inc, mul, max, or min. Likewise,
  any event can be sent with segmentation easily.
</p>
<h1>Adding the SDK to the project</h1>
<p>
  To add the SDK to your project, you would use a command similar to these:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">npm</span>
    <span class="tabs-link">yarn</span>
  </div>
  <div class="tab">
    <pre><code class="shell">npm install countly-sdk-nodejs</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="shell">yarn add countly-sdk-nodejs</code></pre>
  </div>
</div>
<p>Example setup would look like this:</p>
<pre><code class="javascript">var Countly = require('countly-sdk-nodejs');

Countly.init({
    app_key: "{YOUR-API-KEY}",
    url: "https://API_HOST/",
    debug: true
});


Countly.begin_session();</code></pre>
<p>
  For more information on how to acquire your application key (APP_KEY) and server
  URL, please check
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#acquiring-your-application-key-and-server-url">here</a>.
</p>
<p>Now you can make event calls like:</p>
<pre><code class="javascript">Countly.add_event({
    "key": "in_app_purchase",
    "count": 3,
    "sum": 2.97,
    "dur": 1000,
    "segmentation": {
        "app_version": "1.0",
        "country": "Germany"
    }
});</code></pre>
<h2>Setup properties</h2>
<p>
  Here are the properties you can setup on Countly initialization
</p>
<ul>
  <li>
    <strong>app_key</strong> - mandatory, app key for your app created in Countly
  </li>
  <li>
    <strong>device_id</strong> - to identify a visitor, will be auto generated
    if not provided
  </li>
  <li>
    <strong>url</strong> - your Countly server url (default: "https://cloud.count.ly"),
    you must use your own server URL here
  </li>
  <li>
    <strong>app_version</strong> - (optional) the version of your app or website
  </li>
  <li>
    <strong>country_code</strong> - (optional) country code for your visitor
  </li>
  <li>
    <strong>city</strong> - (optional) name of the city of your visitor
  </li>
  <li>
    <strong>ip_address</strong> - (optional) ip address of your visitor
  </li>
  <li>
    <strong>debug</strong> - output debug info into console (default: false)
  </li>
  <li>
    <strong>interval</strong> - set an interval how often to check if there is
    any data to report and report it (default: 500 ms)
  </li>
  <li>
    <strong>fail_timeout</strong> - set time in seconds to wait after failed
    connection to server (default: 60 seconds)
  </li>
  <li>
    <strong>session_update</strong> - how often in seconds should session be
    extended (default: 60 seconds)
  </li>
  <li>
    <strong>max_events</strong> - maximum amount of events to send in one batch
    (default: 10)
  </li>
  <li>
    <strong>force_post</strong> - force using post method for all requests (default:
    false)
  </li>
  <li>
    <strong>storage_path</strong> - where SDK would store data, including id,
    queues, etc (default: "../data/")
  </li>
  <li>
    <strong>require_consent</strong> - pass true if you are implementing GDPR
    compatible consent management. It would prevent running any functionality
    without proper consent (default: false)
  </li>
  <li>
    <strong>remote_config</strong> - Enable automatic remote config fetching,
    provide callback function to be notified when fetching done (default: false)
  </li>
  <li>
    <strong>http_options</strong> - function to get http options by reference
    and overwrite them, before running each request
  </li>
  <li>
    <strong>max_logs</strong> - maximum amount of breadcrumbs to store for crash
    logs (default: 100)
  </li>
  <li>
    <strong>metrics</strong> - provide for this user/device, or else will try
    to collect what's possible
  </li>
</ul>
<p>
  Setting up properties in Countly NodeJS SDK is as follows (if you have your own
  server, use it instead of try.count.ly):
</p>
<pre><code class="javascript">Countly.init({
    debug:false,
    app_key:"YOUR_APP_KEY",
    device_id:"1234-1234-1234-1234",
    url: "https://try.count.ly",
    app_version: "1.2",
    country_code: "LV",
    city: "Riga",
    ip_address: "83.140.15.1",
    http_options: function(options){
        options.headers["user-agent"] = "Test";
    },
    metrics:{
        _os: "Ubuntu",
        _os_version: "16.04",
        _device: "aws-server"
    }
});</code></pre>
<p>
  Sometimes just turning on the logs during the initialization is all you really
  need. But sometimes you might want to see the logs only for a small time frame
  or some particular operation. In those situations you can simply use setLoggingEnabled
  function to turn the logs on or off as you wish, just like this:
</p>
<pre><code class="javascript">//to turn on the logs
Countly.setLoggingEnabled(true);

//some code in between
//&lt;...&gt;

//to turn off the logs
Countly.setLoggingEnabled(false);</code></pre>
<h1>Crash reporting</h1>
<p>
  Countly also provides a way to track NodeJS errors on your server.
</p>
<p>
  To automatically capture and report Javascript errors on your server, call the
  following function:
</p>
<pre><code class="javascript">Countly.track_errors()</code></pre>
<p>
  You can additionally add more segments or properties/values to track with error
  reports, by providing an object with key/values to add to error reports.
</p>
<pre><code class="javascript">Countly.track_errors({
  "facebook_sdk": "2.3",
  "jquery": "1.8"
})</code></pre>
<p>
  Apart from reporting unhandled errors automatically, you can also report handled
  exceptions to server too, so you can figure out how and even if you need to handle
  them later on. And optionally you can again provide custom segments to be used
  in the report (or use the ones provided with <strong>track_error</strong> method
  as default ones)
</p>
<p>
  <strong>Countly.log_error(error, segments);</strong>
</p>
<pre><code class="javascript">try{
  //do something here
}
catch(ex){
  //report error to Countly
  Countly.log_error(ex);
}</code></pre>
<p>
  To better understand what happened prior to getting an error, you can leave out
  breadcrumbs through out the code, on different actions. This breadcrumb will
  be then combined in single log and reported to server too.
</p>
<pre><code class="javascript">Countly.add_log("user clicked button a");</code></pre>
<h1>Events</h1>
<h2>Adding an event</h2>
<p>
  An event is a way to track any custom actions or other data you want to track
  from your website. You can also provide segments to be able to view breakdown
  of action by provided segment values.
</p>
<p>
  An event consists of Javascript object with keys: * key - the name of the event
  (mandatory) * count - number of events (default: 1) * sum - sum to report with
  event (optional) * dur - duration to report with event (optional) * segmentation
  - an object with key/value pairs to report with event as segments
</p>
<p>
  Here is an example of adding an event with all possible properties:
</p>
<pre><code class="javascript">Countly.add_event({
  "key": "click",
  "count": 1,
  "sum": 1.5,
  "dur": 30,
  "segmentation": {
    "key1": "value1",
    "key2": "value2"
  }
});</code></pre>
<div class="callout callout--warning">
  <p class="callout__title">
    <span class="wysiwyg-font-size-large"><strong>Data passed should be in UTF-8</strong></span>
  </p>
  <p>
    All data passed to Countly instance via SDK or API should be in UTF-8.
  </p>
</div>
<h2>Timed Events</h2>
<p>
  You can report time or duration with every event by providing
  <strong>dur</strong> property of the events object. But if you want, you can
  also let Web SDK to track duration of some specific event for you, you can use
  <strong>start_event</strong> and <strong>end_event</strong> methods.
</p>
<p>
  Firstly you can start tracking event time by providing name of the event (which
  later on will be used as key for event object)
</p>
<pre><code class="javascript">Countly.start_event("timedEvent")</code></pre>
<p>
  Countly will internally mark the start of event and will wait until you end event
  with <strong>end_event</strong> method, setting up <strong>dur</strong> property
  based on how much time has passed since <strong>start_event</strong> for same
  event name was called.
</p>
<pre><code class="javascript">//end event
Countly.end_event("timedEvent")

//or end event with additional data
Countly.end_event({
  "key": "timedEvent",
  "count": 1,
  "sum": 1.5,
  "segmentation": {
    "key1": "value1",
    "key2": "value2"
  }
});</code></pre>
<h1>Session</h1>
<h2>Beginning a session</h2>
<p>
  This method would allow you to control sessions manually. Use it only, if you
  don't call track_sessions method.
</p>
<p>
  If <strong>noHeartBeat</strong> is true, then Countly SDK won't extend session
  automatically, and you would need to do that manually.
</p>
<pre><code class="javascript">Countly.begin_session(noHeartBeat);</code></pre>
<h2>Extending a session</h2>
<p>
  By default (if <strong>noHeartBeat</strong> was not provided in
  <strong>begin_session</strong>) Countly SDK will extend session itself, but if
  you chose not to, then you can extend is using this method and provide seconds
  since last call <strong>begin_session</strong> or
  <strong>session_duration</strong> call, whatever was the last one.
</p>
<pre><code class="javascript">Countly.session_duration(sec)</code></pre>
<h2>Ending a session</h2>
<p>
  When visitor is leaving your app or website, you should end his session with
  this method, optionally providing amount of seconds since last
  <strong>begin session</strong> or <strong>session_duration</strong> calls, whatever
  was the last one.
</p>
<pre><code class="javascript">Countly.end_session(sec)</code></pre>
<h1>View tracking</h1>
<p>
  This method allows you to track different parts of your application, called views.
  You can track how much time is spent on each part of the application.
</p>
<pre><code class="javascript">Countly.track_view("viewname");</code></pre>
<p>
  And optionally, as the third parameter, you can provide view segments (key/value
  pairs) to track together with the view. There is a list of reserved segment keys
  that should not be used:
</p>
<ul>
  <li>start</li>
  <li>visit</li>
  <li>bounce</li>
  <li>end</li>
  <li>name</li>
  <li>domain</li>
  <li>view</li>
  <li>segment</li>
  <li>platform</li>
</ul>
<pre><code class="javascript">//Provide view segments
Countly.track_view("viewname", {theme:"red", mode:"fullscreen"});</code></pre>
<h1>Device ID management</h1>
<p>
  In some cases you may want to change the ID of the user/device that you provided
  or Countly generated automatically, for example, when user was changed.
</p>
<pre><code class="javascript">Countly.change_id("myNewId");</code></pre>
<div class="callout callout--warning">
  <p>
    <span style="font-weight: 400;">If device ID is changed without merging and consent was enabled, all previously given consent will be removed. This means that all features will cease to function until new consent has been given again for that new device ID.</span>
  </p>
</div>
<p>
  In some cases, you may also need to change user's device ID in a way, that server
  will merge data of both user IDs (existing and new ID you provided) on the server,
  eg when user used website without authenticating and have recorded some data,
  and then authenticated and you want to change ID to your internal id of this
  user, to keep tracking it across multiple devices.
</p>
<p>
  This call will merge any data recorded for current ID and save it as user with
  new provided ID.
</p>
<pre><code class="javascript">Countly.change_id("myNewId", true);</code></pre>
<h1>User feedback</h1>
<p>
  If there is any way you can get some user feedback, there is not a simple method
  to report collected data to Countly.
</p>
<pre><code class="javascript">//user feedback
Countly.report_feedback({
    widget_id:"1234567890",
    contactMe: true,
    rating: 5,
    email: "user@domain.com",
    comment: "Very good"
});</code></pre>
<p>&nbsp;</p>
<h1>User profiles</h1>
<h2>User details</h2>
<p>
  If you have any details about the user/visitor, you can provide Countly with
  that information. This will allow you track each and specific user on "User Profiles"
  tab, which is available with
  <a href="http://count.ly/enterprise-edition">Countly Enterprise Edition</a>.
</p>
<p>The list of possible parameters you can pass is:</p>
<pre><code class="javascript">Countly.user_details({
    "name": "Arturs Sosins",
    "username": "ar2rsawseen",
    "email": "test@test.com",
    "organization": "Countly",
    "phone": "+37112345678",
    //Web URL pointing to user picture
    "picture": "https://pbs.twimg.com/profile_images/1442562237/012_n_400x400.jpg", 
    "gender": "M",
    "byear": 1987, //birth year
    "custom":{
      "key1":"value1",
      "key2":"value2",
      ...
    }
 });</code></pre>
<h2>Modifying custom data</h2>
<p>
  Additionally you can do different manipulations on custom data values, like increment
  current value on server or store array of values under same property.
</p>
<p>Below is the list of available methods:</p>
<pre><code class="javascript">Countly.userData.set(key, value) //set custom property
Countly.userData.set_once(key, value) //set custom property only if property does not exist
Countly.userData.increment(key) //increment value in key by one
Countly.userData.increment_by(key, value) //increment value in key by provided value
Countly.userData.multiply(key, value) //multiply value in key by provided value
Countly.userData.max(key, value) //save max value between current and provided
Countly.userData.min(key, value) //save min value between current and provided
Countly.userData.push(key, value) //add value to key as array element
Countly.userData.push_unique(key, value) //add value to key as array element, but only store unique values in array
Countly.userData.pull(key, value) //remove value from array under property with key as name
Countly.userData.save() //send userData to server</code></pre>
<h1>Application Performance Monitoring</h1>
<p>
  You can report a trace using <strong>report_trace</strong> method. Contents of
  it depend on which trace you report.
</p>
<p>Here is an example of how to report network trace:</p>
<pre><code class="javascript">//report network trace
Countly.report_trace({
    type: "network", //device or network
    name: "/some/endpoint", //use name to identify trace and group them by
    stz: 1234567890123, //start timestamp in miliseconds
    etz: 1234567890123, //end timestamp in miliseconds
    app_metrics: {
        response_time: 1000,
        response_code: 200,
        response_payload_size: 12345,
        request_payload_size: 5432
    }
});</code></pre>
<p>&nbsp;And here is an example of device trace:</p>
<pre><code class="javascript">//user built in method to report app start time
Countly.report_app_start();

//or report device trace manually
Countly.report_trace({
    type: "device", //device or network
    name: "My App", //use name to identify trace and group them by
    stz: 1234567890123, //start timestamp in miliseconds
    etz: 1234567890123, //end timestamp in miliseconds
    app_metrics: {
        duration: 1000,
    }
});</code></pre>
<p>Or you can report any custom traces to provide duration:</p>
<pre><code class="javascript">//or report device trace manually
Countly.report_trace({
    type: "device", //device or network
    name: "Some process we launched", //use name to identify trace and group them by
    stz: 1234567890123, //start timestamp in miliseconds
    etz: 1234567890123, //end timestamp in miliseconds
    app_metrics: {
        duration: 1000,
    }
});</code></pre>
<h1>Other features and notes</h1>
<h2>Attribution</h2>
<p>
  When using Countly attribution analytics, you can also report conversion to Countly
  server, like for example when visitor purchased something or registered.
</p>
<p>
  Note: that conversion for each user may be reported only once, all other conversions
  will be ignored for this same user
</p>
<pre><code class="javascript">//or provide campaign id yourself
Countly.report_conversion("MyCampaignID");</code></pre>
<h2>Make raw request</h2>
<p>
  Sometimes if you are switching between users a lot, or changing some other data,
  which is hard to handle over multiple processes, etc. You can simply make a raw
  request with all possible SDK parameters described in
  <a href="http://resources.count.ly/docs/i">API reference</a>
</p>
<pre><code class="javascript">Countly.request({
  app_key:"somekey", 
  devide_id:"someid", 
  events:"[{'key':'val','count':1}]", 
  metrics:"{'_os':'Linux'}",
  begin_session:1
});</code></pre>
<h2>SDK Internal Limits</h2>
<p>
  Countly is highly customizable and let's you take a huge part at the control
  of the system in multiple ways. From customizing segmentation values to changing
  event keys great liberty comes with the cost of great responsibility. As a sanity
  check measure Countly relies on internal limits to get a hold of the free flow
  of values, keys, character and more. These internal limits are again customizable
  at initialization and current limits and their default values are as follows:
</p>
<ul>
  <li>
    <strong>maxKeyLength</strong> - 128 chars. Keys that exceed this limit will
    be truncated.
  </li>
  <ul>
    This is used for setting the maximum size of all string keys including:
    <li>- event names</li>
    <li>- view names</li>
    <li>- custom trace key name (APM)</li>
    <li>- custom metric key (apm)</li>
    <li>- segmentation key (for all features)</li>
    <li>- custom user property</li>
    <li>
      - custom user property keys that are used for property modifiers (mul,
      push, pull, set, increment, etc)
    </li>
  </ul>
  <li>
    <strong>maxValueSize</strong> - 256 chars. Values that exceed this limit
    will be truncated.
  </li>
  <ul>
    This is used for setting the maximum size of all values in key-value pairs
    including:
    <li>- segmentation value in case of strings (for all features)</li>
    <li>- custom user property string value</li>
    <li>
      - user profile named key (username, email, etc) string values. Except
      "picture" field, that has a limit of 4096 chars
    </li>
    <li>
      - custom user property modifier string values. For example, for modifiers
      like "push", "pull", "setOnce", etc.
    </li>
    <li>- breadcrumb text</li>
    <li>
      - manual feedback widget reporting fields (reported as event)
    </li>
    <li>- rating widget response (reported as event)</li>
  </ul>
  <li>
    <strong>maxSegmentationValues</strong> - 30 dev entries. Entries that exceed
    this limit will be removed.<br>
    To set the maximum amount of custom segmentation that can be recorded in
    one event.
  </li>
  <li>
    <strong>maxBreadcrumbCount</strong> - 100 entries. If the limit is exceeded,
    the oldest entry will be removed.<br>
    To limit the amount of breadcrumbs that can be recorded before the oldest
    one is deleted from the logs.
  </li>
  <li>
    <strong>maxStackTraceLinesPerThread</strong> - 30 lines. Lines that exceed
    this entry will be removed.<br>
    Sets the maximum number of stack trace lines that can be recorded per thread.
  </li>
  <li>
    <strong>maxStackTraceLineLength</strong> - 200 chars. Lines that exceed this
    limit will be truncated.<br>
    This can set the maximum number of characters that is allowed per stack trace
    line. This also limits the crash message length.
  </li>
</ul>
<p>
  To change these default values all you have to do is to set the properties during
  the initialization:
</p>
<pre><code class="javascript">Countly.init({
    app_key:"YOUR_APP_KEY",
    url: "https://try.count.ly",
    max_key_length: 500,
    max_value_size: 12,
    max_segmentation_values: 23,
    max_breadcrumb_count: 80,
    max_stack_trace_lines_per_thread: 50,
    max_stack_trace_line_length: 300
});</code></pre>
<p>&nbsp;</p>
