<p>
  This documentation shows how to use Countly NodeJS SDK to track your nodejs running
  device or server, like tracking your API.
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
<p>
  Before starting, for those who have examined our mobile SDKs - we can tell that
  custom events or tags that are used in mobile SDKs are quite similar to those
  we use in Javascript code. For example, it's possible to modify custom property
  values of user details, with modification commands like inc, mul, max, or min.
  Likewise, any custom events can be sent with segmentation easily.
</p>
<div class="callout callout--info">
  <h3 class="callout__title">What is an APP KEY?</h3>
  <p>
    You'll see APP_KEY definition above. This key is generated automatically
    when you create a website for tracking on Countly dashboard. Note that APP
    KEY is different from API KEY, which is used to send data via API calls.
  </p>
  <p>
    To retrieve your APP_KEY, go to Management -&gt; Applications and select
    your app, and you will see App Key field
  </p>
</div>
<div class="img-container">
  <img src="https://count.ly/images/guide/XmwUJ7VZSF2GConV76xY_app_key.png">
</div>
<h1>Setting up</h1>
<p>Example setup would look like this:</p>
<pre><code class="javascript">var Countly = require('countly-sdk-nodejs');

Countly.init({
    app_key: "{YOUR-API-KEY}",
    url: "https://API_HOST/",
    debug: true
});


Countly.begin_session();</code></pre>
<div class="callout callout--info">
  <h3 class="callout__title">Which API HOST name should I use to send data to?</h3>
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
<p>Now you can make custom event calls like:</p>
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
<h1>Setup properties</h1>
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
<h1>Helper methods</h1>
<p>
  Helper methods created to allow you easily track most common actions
</p>
<h3>Track Views</h3>
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
<h3>Report conversion</h3>
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
<h3>Make raw request</h3>
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
<h1>Custom Events</h1>
<h3>Adding an event</h3>
<p>
  Custom event is a way to track any custom actions or other data you want to track
  from your website. You can also provide segments to be able to view breakdown
  of action by provided segment values.
</p>
<p>
  Custom event consists of Javascript object with keys: * key - the name of the
  event (mandatory) * count - number of events (default: 1) * sum - sum to report
  with event (optional) * dur - duration to report with event (optional) * segmentation
  - an object with key/value pairs to report with event as segments
</p>
<p>
  Here is an example of adding a custom event with all possible properties:
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
  <h3 class="callout__title">Data passed should be in UTF-8</h3>
  <p>
    All data passed to Countly instance via SDK or API should be in UTF-8.
  </p>
</div>
<h3>Timed Events</h3>
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
<h1>User Profiles and Custom data</h1>
<h3>User details</h3>
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
<h3>Modifying custom data</h3>
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
<h1>Tracking Javascript errors</h1>
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
<h1>Other methods</h1>
<h3>Changing Device ID</h3>
<p>
  In some cases you may want to change the ID of the user/device that you provided
  or Countly generated automatically, for example, when user was changed.
</p>
<pre><code class="javascript">Countly.change_id("myNewId");</code></pre>
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
<h1>Tracking a session</h1>
<h3>Beginning a session</h3>
<p>
  This method would allow you to control sessions manually. Use it only, if you
  don't call track_sessions method.
</p>
<p>
  If <strong>noHeartBeat</strong> is true, then Countly SDK won't extend session
  automatically, and you would need to do that manually.
</p>
<pre><code class="javascript">Countly.begin_session(noHeartBeat);</code></pre>
<h3>Extending a session</h3>
<p>
  By default (if <strong>noHeartBeat</strong> was not provided in
  <strong>begin_session</strong>) Countly SDK will extend session itself, but if
  you chose not to, then you can extend is using this method and provide seconds
  since last call <strong>begin_session</strong> or
  <strong>session_duration</strong> call, whatever was the last one.
</p>
<pre><code class="javascript">Countly.session_duration(sec)</code></pre>
<h3>Ending a session</h3>
<p>
  When visitor is leaving your app or website, you should end his session with
  this method, optionally providing amount of seconds since last
  <strong>begin session</strong> or <strong>session_duration</strong> calls, whatever
  was the last one.
</p>
<pre><code class="javascript">Countly.end_session(sec)</code></pre>
<h1>Performance monitoring</h1>
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
<h2>Report feedback</h2>
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