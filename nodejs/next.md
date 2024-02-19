<p>
  This documentation is for the Countly NodeJS SDK version 22.06.X. The SDK source
  code repository can be found
  <a href="https://github.com/Countly/countly-sdk-nodejs" target="_blank" rel="noopener noreferrer">here.</a>
</p>
<div class="callout callout--info">
  <p>
    Click
    <a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-and-Installing-SDKs#h_01H9QCP8G7S1YR45QYHX6DQJ4D" target="_self" rel="undefined">here, </a>to
    access the documentation for older SDK versions.
  </p>
</div>
<p>
  Countly NodeJS runs with the following node versions, and up:
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
  To examine the example integrations, please have a look
  <a href="#h_01HPK9ZBQXA5AYYG2CVHWWWVHB">here.</a>
</p>
<h1 id="h_01HABTSEDFXYDEN0QDRY7DEVR7">Adding the SDK to the project</h1>
<p>
  You can reach Countly NodeJS SDK npm package
  <a href="https://www.npmjs.com/package/countly-sdk-nodejs">here</a>. To add it
  to your project, you would use a command similar to these with your preferred
  package manager:
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
  After this, you can import and use Countly as you wish inside your project as
  described below.
</p>
<h1 id="h_01HABTSEDFJ0AZN0699VJPKZJX">SDK Integration</h1>
<h2 id="h_01HABTSEDFVJHWVBK7YJKB7CSZ">Minimal Setup</h2>
<p>
  Wherever you want to integrate Countly NodeJS SDK, you should import 'countly-sdk-nodejs'
  and initialize Countly. Here, you would also need to provide your application
  key and server URL. Please check
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KX44C9SF48WRPQNCP3">here</a>
  for more information on how to acquire your application key (APP_KEY) and server
  URL.
</p>
<p>Example basic setup would look like this:</p>
<pre><code class="javascript">var Countly = require('countly-sdk-nodejs');

Countly.init({
  app_key: "YOUR-APP-KEY",
  url: "https://your_server_url/"
});</code></pre>
<div class="callout callout--info">
  <p>
    If you are in doubt about the correctness of your Countly SDK integration
    you can learn about the verification methods from
    <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#h_01HABSX9KXE6YKVETHDWPP8J3K" target="blank">here</a>.
  </p>
</div>
<h2 id="h_01HABTSEDFRBJ54MX797V7QV2K">SDK Data Storage</h2>
<p>
  Countly stores information like requests, events and device ID locally as JSON
  objects before using it to ensure data consistency. Default location of this
  stored data is at the base of your project under a folder called Data. You can
  change the location or file name during the initialization by using the storage_path
  flag:
</p>
<pre><code class="javascript">var Countly = require('countly-sdk-nodejs');

Countly.init({
  app_key: "YOUR-APP-KEY",
  url: "https://your_server_url/",
  // by default it is "../data/"
  storage_path: "../your_storage/path" 
});</code></pre>
<h1 id="h_01HABTSEDFSJWTK0GZKKTYSBMK">SDK Logging</h1>
<p>
  If you encounter a problem or want to see if everything is working smoothly just
  turning on the logs during the initialization is all you really need. You can
  do so by setting the debug flag as true, during the init. This way you can see
  the inner workings of the Countly from your console.
</p>
<pre><code class="javascript">var Countly = require('countly-sdk-nodejs');

Countly.init({
  app_key: "YOUR-APP-KEY",
  url: "https://your_server_url/",
  debug: true
});</code></pre>
<p>
  But sometimes you might want to see the logs only for a small time frame or some
  particular operation. In those situations, you can simply use setLoggingEnabled
  function to turn the logs on or off as you wish, just like this:
</p>
<pre><code class="javascript">//to turn on the logs
Countly.setLoggingEnabled(true);

//some code in between
//&lt;...&gt;

//to turn off the logs
Countly.setLoggingEnabled(false);</code></pre>
<h1 id="h_01HABTSEDF3VWA2BT8QJQH6NJ7">Crash reporting</h1>
<p>
  Countly also provides a way to track NodeJS errors on your server.
</p>
<p>
  To automatically capture and report Javascript errors on your server, call the
  following function:
</p>
<pre><code class="javascript">Countly.track_errors()</code></pre>
<p>
  You can additionally, add more segments or properties/values to track with error
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
  as default ones).
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
<h1 id="h_01HABTSEDFRP0KEF7CKVC9F0EN">Events</h1>
<h2 id="h_01HABTSEDFBFYNW9KRYV3E4WNS">Adding an event</h2>
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
  <strong>Data passed should be in UTF-8</strong>
  <p>
    All data passed to Countly instance via SDK or API should be in UTF-8.
  </p>
</div>
<h2 id="h_01HABTSEDFJK3D4ZZ1SGQT5N3E">Timed Events</h2>
<p>
  You can report time or duration with every event by providing
  <strong>dur</strong> property of the events object. But if you want, you can
  also let Web SDK to track duration of some specific event for you, you can use
  <strong>start_event</strong> and <strong>end_event</strong> methods.
</p>
<p>
  First, you can start tracking event time by providing name of the event (which
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
<h1 id="h_01HABTSEDFMAR3E3AT8DGSRZ98">Session</h1>
<h2 id="h_01HABTSEDF4A4P0ZKPFN0MNXYR">Beginning a session</h2>
<p>
  This method would allow you to control sessions manually. Use it only, if you
  don't call track_sessions method.
</p>
<p>
  If <strong>noHeartBeat</strong> is true, then Countly SDK won't extend session
  automatically, and you will need to do that manually.
</p>
<pre><code class="javascript">Countly.begin_session(noHeartBeat);</code></pre>
<h2 id="h_01HABTSEDFV69Z7DB61R3HYK5N">Extending a session</h2>
<p>
  By default (if <strong>noHeartBeat</strong> was not provided in
  <strong>begin_session</strong>) Countly SDK will extend session itself, but if
  you chose not to, then you can extend is using this method and provide seconds
  since last call <strong>begin_session</strong> or
  <strong>session_duration</strong> call, whatever was the last one.
</p>
<pre><code class="javascript">Countly.session_duration(sec)</code></pre>
<h2 id="h_01HABTSEDFZ22Z8Q8SH0DDMRGS">Ending a session</h2>
<p>
  When visitor is leaving your app or website, you should end his session with
  this method, optionally providing amount of seconds since last
  <strong>begin session</strong> or <strong>session_duration</strong> calls, whatever
  was the last one.
</p>
<pre><code class="javascript">Countly.end_session(sec)</code></pre>
<h1 id="h_01HABTSEDGBS3Z9EX21HVYSCVS">View tracking</h1>
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
<h1 id="h_01HABTSEDGC162BVG9Y5PZY0YE">Device ID management</h1>
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
  for e.g., when user used website without authenticating and have recorded some
  data, and then authenticated and you want to change ID to your internal id of
  this user, to keep tracking it across multiple devices.
</p>
<p>
  This call will merge any data recorded for current ID and save it as user with
  new provided ID.
</p>
<pre><code class="javascript">Countly.change_id("myNewId", true);</code></pre>
<h1 id="h_01HABTSEDG6E0VY2C0FHBGVMGV">Remote Config</h1>
<p>
  <span style="font-weight: 400;">Remote Config feature enables you to fetch data that you have created in your server. Depending on the conditions you have set, you can fetch data from your server for the specific users that fits those conditions and process the Remote Config data in anyway you want. Whether to change the background color of your site to showing a certain message, the possibilities are virtually endless. For more information on Remote Config please check <a href="https://support.count.ly/hc/en-us/articles/9895605514009-Remote-Config" target="_blank" rel="noopener">here</a>.</span><span style="font-weight: 400;"></span>
</p>
<h2 id="h_01HABTSEDGR7ACMEZQA35GFTTW">Automatic Remote Config</h2>
<p>
  <span style="font-weight: 400;">Automatic Remote Config functionality is disabled by default and needs to be explicitly enabled. When automatic Remote Config is enabled, the SDK will try to fetch it upon some specific triggers. For example, after SDK initialization, changing device ID.</span>
</p>
<p>
  <span style="font-weight: 400;">You may enable this feature by providing to the </span><em><span style="font-weight: 400;">remote_config</span></em><span style="font-weight: 400;"> flag a callback function or by setting it to true while initializing the SDK.</span>
</p>
<p>
  <span style="font-weight: 400;">If you provide a callback, the callback will be called when the Remote Config is initially loaded and when it is reloaded if you change the device_id. This callback should have two parameters, first is for error, and second is for the Remote Config object.</span>
</p>
<pre><code class="javascript">// in your Countly init script
Countly.init({
  app_key:"YOUR_APP_KEY",
  url: "https://try.count.ly",<br>  debug: true,
  remote_config: true 
});<br><br>// OR

// provide a callback to be notified when configs are loaded
Countly.init({
  app_key:"YOUR_APP_KEY",
  url: "https://try.count.ly",<br>  debug: true,
  remote_config: function(err, remoteConfigs){
    if (!err) {
      //we have our remoteConfigs here
      console.log(remoteConfigs);
    }
  }
});</code></pre>
<h2 id="h_01HABTSEDGQV4P1MM5W7HABRCE">Manual Remote Config</h2>
<p>
  <span style="font-weight: 400;">If you want, you can manually fetch the Remote Config in order to receive the latest value anytime after the initialization. To do so you have to use the </span><em><span style="font-weight: 400;">fetch_remote_config</span></em><span style="font-weight: 400;"> call. This method is also used for reloading the values for updating them according to the latest changes you made on your server.</span>
</p>
<p>
  <span style="font-weight: 400;">By using this method, you can simply load the entire object or load some specific keys or omit some specific keys in order to decrease the amount of data transfer needed, assuming the values for some of the keys are large. This call will automatically save the fetched keys internally.</span>
</p>
<h3 id="h_01HABTSEDGVWNJFBFXNFD5AS9K">Fetch All Keys</h3>
<p>
  Here you so not need to provide any parameters to the call but providing a callback
  is the recommended practice.
  <span style="font-weight: 400;">This callback should have two parameters, first is for error, and second is for the Remote Config object.</span>
</p>
<pre><code class="javascript">// load the whole configuration object with a callback
Countly.fetch_remote_config(function(err, remoteConfigs){
  if (!err) {
    console.log(remoteConfigs);<br>  // or do something else here if you want with remoteConfigs object
  }<br>});<br><br>// or whole configuration object with no params
Countly.fetch_remote_config();</code></pre>
<h3 id="h_01HABTSEDG5EKWQAJS4ZBJFDN9">Fetch Specific Keys</h3>
<p>
  Here the keys should be provided as string values in an array, as the first parameter
  in <em>fetch_remote_config</em> call. You can provide a callback function as
  a second parameter.
  <span style="font-weight: 400;">This callback should have two parameters, first is for error, and second is for the Remote Config object.</span>
</p>
<pre><code class="javascript">// load specific keys only, as `key1` and `key2`
Countly.fetch_remote_config(["key1","key2"], function(err, remoteConfigs){
  if (!err) {
    console.log(remoteConfigs);<br>    // or do something else here if you want with remoteConfigs object
  }
});<br><br></code></pre>
<h3 id="h_01HABTSEDG0NX9JDM5XT7CGHTB">Fetch All Except Specific Keys</h3>
<p>
  Here the first parameter should be set to 'null' or 'undefined' and the keys
  that you want to omit must be provided as the second parameter as an array of
  keys as string. As a third parameter you can provide a callback function.
  <span style="font-weight: 400;">This callback should have two parameters, first is for error, and second is for the Remote Config object.</span>
</p>
<pre><code class="javascript">// load all key values except specific keys, as `key1` and `key2'
Countly.fetch_remote_config(null, ["key1","key2"], function(err, remoteConfigs){
  if (!err) {
    console.log(remoteConfigs);<br>    // or do something else here if you want with remoteConfigs object
  }
});</code></pre>
<h2 id="h_01HABTSEDG68FV1AGWAMPM9XP7">Accessing Remote Config Values</h2>
<p>
  <span style="font-weight: 400;">You may call </span><em><span style="font-weight: 400;">get_remote_config</span></em><span style="font-weight: 400;"> each time you would like to receive the Remote Config object of a value for a specific key or all keys from your local storage.</span>
</p>
<p>
  <span style="font-weight: 400;">This method should be called once the Remote Config have been successfully loaded, or it will simply return an empty object or undefined values.</span>
</p>
<pre><code class="javascript">//get whole Remote Config object
var remoteConfig = Countly.get_remote_config();

//or get value for specific key like 'test'
var test = Countly.get_remote_config("test");</code><code class="javascript"></code></pre>
<h2 id="h_01HABTSEDGWZWG88ZMC5YAZY9G">A/B Testing</h2>
<p>
  While fetching Remote Config, the SDK will automatically enroll the user to A/B
  testing. For more information on A/B testing please check
  <a href="https://support.count.ly/hc/en-us/articles/4416496362393-A-B-Testing-" target="_blank" rel="noopener">here</a>.
</p>
<h2 id="h_01HABTSEDGB39R2HAXPYK2AM4G">Consent</h2>
<p>
  If consents are enabled, to fetch the Remote Config data you have to provide
  the 'remote-config' consent for this feature to work.
</p>
<h1 id="h_01HABTSEDG3ZAZTK7ARF28M1FH">User feedback</h1>
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
<h1 id="h_01HABTSEDG0TDK1PCNWM8QENG0">User profiles</h1>
<h2 id="h_01HABTSEDG9HV99DN895KFJRCY">User details</h2>
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
<h2 id="h_01HABTSEDGZJXM38TNGRZDK69F">Modifying custom data</h2>
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
<h1 id="h_01HABTSEDGD3AXBPQCKMA0PN95">Application Performance Monitoring</h1>
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
<h1 id="h_01HABTSEDHGNE0G3EBG6XX39ZE">Other features and notes</h1>
<h2 id="h_01HAXVDTRGE7AP3385T2HSWWT0">SDK Config Parameters Explained</h2>
<p>
  Here are the properties you can setup on Countly initialization
</p>
<ul>
  <li>
    <strong>app_key</strong> - mandatory, App key for your app created in Countly.
  </li>
  <li>
    <strong>device_id</strong> - To identify a visitor, will be auto generated
    if not provided.
  </li>
  <li>
    <strong>url</strong> - Your Countly server url (default: "https://cloud.count.ly"),
    you must use your own server URL here.
  </li>
  <li>
    <strong>app_version</strong> - (optional) The version of your app or website.
  </li>
  <li>
    <strong>country_code</strong> - (optional) Country code for your visitor.
  </li>
  <li>
    <strong>city</strong> - (optional) Name of the city of your visitor.
  </li>
  <li>
    <strong>ip_address</strong> - (optional) IP address of your visitor.
  </li>
  <li>
    <strong>debug</strong> - output debug info into console (default: false).
  </li>
  <li>
    <strong>interval</strong> - set an interval how often to check if there is
    any data to report and report it (default: 500 ms).
  </li>
  <li>
    <strong>fail_timeout</strong> - set time in seconds to wait after failed
    connection to server (default: 60 seconds).
  </li>
  <li>
    <strong>session_update</strong> - how often in seconds should session be
    extended (default: 60 seconds).
  </li>
  <li>
    <strong>max_events</strong> - maximum amount of events to send in one batch
    (default: 10).
  </li>
  <li>
    <strong>force_post</strong> - force using post method for all requests (default:
    false)
  </li>
  <li>
    <strong>storage_path</strong> - where SDK would store data, including id,
    queues, etc (default: "../data/").
  </li>
  <li>
    <strong>require_consent</strong> - pass true if you are implementing GDPR
    compatible consent management. It would prevent running any functionality
    without proper consent (default: false).
  </li>
  <li>
    <strong>remote_config</strong> - Enable automatic remote config fetching,
    provide callback function to be notified when fetching done (default: false).
  </li>
  <li>
    <strong>http_options</strong> - function to get http options by reference
    and overwrite them, before running each request.
  </li>
  <li>
    <strong>max_logs</strong> - maximum amount of breadcrumbs to store for crash
    logs (default: 100)
  </li>
  <li>
    <strong>metrics</strong> - provide metrics override or custom metrics for
    this user. For more information on the specific metric keys used by Countly,
    check
    <a href="https://support.count.ly/hc/en-us/articles/9290669873305#h_01HABT18WWYQ2QYPZY3GHZBA9B" target="_self">here</a>.
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
<h2 id="h_01HPK9ZBQXA5AYYG2CVHWWWVHB">Example Integrations</h2>
<p>
  <a href="https://github.com/Countly/countly-sdk-nodejs/blob/master/examples/apm_example.js">apm_example</a>
  is a simple APM integration.<br>
  <a href="https://github.com/Countly/countly-sdk-nodejs/blob/master/examples/bulk_import_example.js">bulk_import_example</a>
  is a simple bulk import example.<br>
  <a href="https://github.com/Countly/countly-sdk-nodejs/blob/master/examples/example.js">example</a>
  covers most of the functionalities.<br>
  <a href="https://github.com/Countly/countly-sdk-nodejs/blob/master/examples/multi-process.js">multi-process</a>
  is a simple demonstration for multi-instancing the Countly SDK.
</p>
<h2 id="h_01HABTSEDHW6BSYV7VT45G2KFZ">SDK Internal Limits</h2>
<p>
  Countly is highly customizable and let's you take a huge part at the control
  of the system in multiple ways. From customizing segmentation values to changing
  event keys. Great liberty comes with the cost of great responsibility. As a sanity
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
  To change these default values, all you have to do is to set the properties during
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
<h2 id="h_01HAXVDTRGNHGD4SW5XH7NBE8W">Setting Maximum Request Queue Size</h2>
<p>
  When you initialize Countly, you can specify a value for the queueSize flag.
  This flag limits the number of requests that can be stored in the request queue
  when the Countly server is unavailable or experiencing connection problems.
</p>
<p>
  If the server is down, requests sent to it will be queued on the device. If the
  number of queued requests becomes excessive, it can cause problems with delivering
  the requests to the server, and can also take up valuable storage space on the
  device. To prevent this from happening, the queueSize flag limits the number
  of requests that can be stored in the queue.
</p>
<p>
  If the number of requests in the queue reaches the queueSize limit, the oldest
  requests in the queue will be dropped, and the newest requests will take their
  place. This ensures that the queue doesn't become too large, and that the most
  recent requests are prioritized for delivery.
</p>
<p>
  If you do not specify a value for the queueSize flag, the default setting of
  1,000 will be used.
</p>
<div class="javascript">
  <pre><code class="javascript">Countly.init({
  app_key:"YOUR_APP_KEY",
  url: "https://try.count.ly",
  queueSize: 5000
});</code></pre>
</div>
<h2 id="h_01HAXVDTRK5DCMFC9FKEDKD529">Attribution</h2>
<p>
  When using Countly attribution analytics, you can also report conversion to Countly
  server, for e.g., when visitor purchased something or registered.
</p>
<p>
  Note: that conversion for each user may be reported only once, all other conversions
  will be ignored for this same user
</p>
<pre><code class="javascript">//or provide campaign id yourself
Countly.report_conversion("MyCampaignID");</code></pre>
<h2 id="h_01HAXVDTRKE32GSAT0EJ4MF7G1">Make raw request</h2>
<p>
  If you are switching between users a lot, or changing some other data, which
  is hard to handle over multiple processes, etc. You can simply make a raw request
  with all possible SDK parameters described in
  <a href="https://api.count.ly/reference/i">API reference</a>
</p>
<pre><code class="javascript">Countly.request({
  app_key:"somekey", 
  devide_id:"someid", 
  events:"[{'key':'val','count':1}]", 
  metrics:"{'_os':'Linux'}",
  begin_session:1
});</code></pre>
<h1 id="h_01HNANT8H3P3W2PXB0CCY2FNBW">FAQ</h1>
<h2 id="h_01HNANK3XPZ7429V5Z2FJ9MMZ5">What Information is Collected by the SDK?</h2>
<p>
  The data that SDKs gather to carry out their tasks and implement the necessary
  functionalities is mentioned in
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts#h_01HJ5MD0WB97PA9Z04NG2G0AKC">here</a>
</p>
