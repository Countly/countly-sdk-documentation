<p>
  <span style="font-weight: 400;">Would you like to develop a new SDK for Countly? Then this guide is for you. Before starting, bear in mind that there are a lot of SDKs that Countly has already developed. Please check whether the SDK you are going to develop is not already available.</span>
</p>
<h1>
  <span style="font-weight: 400;">Integration</span>
</h1>
<h2>Initialization</h2>
<p>
  <span style="font-weight: 400;">To start making requests to the server, SDK needs 3 things: the URL of the server where you will be making requests, the app_key of the app for which you will be reporting, and your current device_id to uniquely identify this device.</span>
</p>
<p>
  <strong>Server URL</strong> -&nbsp;<span style="font-weight: 400;">The SDK needs to provide the ability for the user to specify the URL for the server where their Countly instance is installed. This be used for all requests.</span>
</p>
<p>
  <strong>App Key</strong> -&nbsp;<span style="font-weight: 400;">The App key should be provided by the SDK user. This value identifies to which dashbaord applications this request is going to be tied to. Your app should be created on the Countly server. After app creation, the server will provide an app key for the user. The same app key is used for the same app on different platforms.</span>
</p>
<p>
  <strong>Device ID</strong> -
  <span style="font-weight: 400;">A device ID is required to uniquely identify a device or user. If you have some unique user ID which you can retrieve, you may use it. If not, you may provide platform-specific device identification (as Advertising identifier in Google Play Services on Android) or use existing implementations (as OpenUDID).</span>
</p>
<h2>Init configuration</h2>
<p>
  The SDK should take a config (short for configuration) object during initialisation.
  In that config object should all the init specic fields added. All initial configuration
  should be doable through that object and if possible, no configuration should
  be done with function calls before init.
</p>
<p>
  That config object should also have the option to change all the available SDK
  tweakables like queue sizes and thresholds.
</p>
<p>
  Depending on what features are implemented in the SDK, tweakables for them would
  also be provided through the config object, for example: debug parameters, id
  generation methods, user location, consent etc.
</p>
<p>
  Depending on the SDK platform, there might be some other mandatory fields. If
  during init those are not provided, a exception can be thrown to indicate that.
</p>
<p>
  For more information of what values can be sent to the server, look
  <a href="https://api.count.ly/reference#section-additional-parameters">here</a>.
</p>
<h2>Logging / debug mode</h2>
<p>
  The SDK should have a logging mode flag. If that is enabled, the SDK should print
  logs to the console.
</p>
<p>
  If this flag is not enabled, no logs should be printed to the console.
</p>
<p>
  This flag functions independently of the log listener (described bellow).
</p>
<table style="border-collapse: collapse; height: 110px; width: 50.7143%; margin-right: auto; margin-left: auto;" border="1">
  <tbody>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 22.0476%; height: 22px;">&nbsp;</td>
      <td class="wysiwyg-text-align-center" style="width: 14.619%; height: 22px;">
        <strong>Log printed to console</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 14.0476%; height: 22px;">
        <strong>Log printed to listener</strong>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 22.0476%; height: 22px;">Nothing set</td>
      <td class="wysiwyg-text-align-center" style="width: 14.619%; height: 22px;">No</td>
      <td class="wysiwyg-text-align-center" style="width: 14.0476%; height: 22px;">No</td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 22.0476%; height: 22px;">Only flag set</td>
      <td class="wysiwyg-text-align-center" style="width: 14.619%; height: 22px;">Yes</td>
      <td class="wysiwyg-text-align-center" style="width: 14.0476%; height: 22px;">No</td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 22.0476%; height: 22px;">Only listener set</td>
      <td class="wysiwyg-text-align-center" style="width: 14.619%; height: 22px;">No</td>
      <td class="wysiwyg-text-align-center" style="width: 14.0476%; height: 22px;">Yes</td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 22.0476%; height: 22px;">Flag and listener set</td>
      <td class="wysiwyg-text-align-center" style="width: 14.619%; height: 22px;">Yes</td>
      <td class="wysiwyg-text-align-center" style="width: 14.0476%; height: 22px;">Yes</td>
    </tr>
  </tbody>
</table>
<h3>Log levels</h3>
<p>When implementing logs, the SDK should follow these levels:</p>
<ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
  <li>
    <strong>Error</strong> - this is a issues that needs attention right now.
  </li>
  <li>
    <strong>Warning</strong> - this is something that is potentially a issue.
    Maybe a deprecated usage of something, maybe consent is enabled but consent
    is not given.
  </li>
  <li>
    <strong>Info</strong> - All publicly exposed functions should log a call
    at this level to indicate that they were called. These calls should include
    the function name.
  </li>
  <li>
    <strong>Debug</strong> - this should contain logs from the internal workings
    of the SDK and it's important calls. This should include things like the
    SDK configuration options, success or fail of the current network request,
    "request queue is full" and the oldest request get's dropped, etc.
  </li>
  <li>
    <strong>Verbose</strong> - this should give a even deeper look into the SDK's
    inner working and should contain things that are more noisy and happen often.
  </li>
</ul>
<p>
  <span>No two places should have the same log message. This means that all messages should be unique. Knowing the log message and the sdk version it should be unambiguous to know which line printed that message.</span><br>
  <span>To help with being unambiguous, the log messages could include the internal "module" or "section" name from where it was called</span>
</p>
<p>
  <span class="c-mrkdwn__br" data-stringify-type="paragraph-break"></span><span>The goal is to have a good enough log coverage so that it's easy to understand what was happening with the SDK and how it was used when a SDK integrator provides his logs.</span><br>
  <span>By using log levels "info" and above it should be clear what the dev was doing with the SDK and what was the call order. </span><span>"Debug" and above should give us a good enough look into the SDK's internal state and a good overview of it's configuration.</span>
</p>
<p>
  <span>Platforms that don't have explicit log levels should print them manually at the start of the log in square brackets. Either of these variants currently seem fine (as long as it's consistent for the SDK)</span>
</p>
<ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
  <li>[ERROR], [WARNING], [INFO], [DEBUG], [VERBOSE]</li>
  <li>[Error], [Warning], [Info], [Debug], [Verbose]</li>
  <li>[error], [warning], [info], [debug], [verbose]</li>
</ul>
<p>
  <span>If there are the same amount of log levels available but with different names then the closest ones available for the platform should be picked.</span>
</p>
<p>
  <span>If there are less than 5 log levels available then multiple ones should be printed in the same log level and the appropriate tag in square brackets should be printed at the start.</span>
</p>
<p>
  <span>For example, if there are only 3 levels "error", "info", "debug". "Error" and "Warning" would be printed in the error "channel" and "debug" and "verbose" would be printed in the "debug" channel".</span>
</p>
<pre><span>E: [Error] Countly issue bla bla<br>E: [Warning] You are trying to use this feature in a deprecated way</span></pre>
<p>
  Depending on the function call, the function parameters should also be printed,
  for example event keys or for simple numerical values.
</p>
<p>
  For functions which receive a callback, a bool is enough to indicate if a callback
  was or wasn't provided.
</p>
<h3>Log listener</h3>
<p>
  In some cases there might be situations where a integrated SDK is not behaving
  as expected in a release build which is used by clients. In those cases it would
  valuable to see the inner workings of the SDK but it's not possible to access
  SDK logs. It wouldn't also be recommendable to print those logs is a published
  setting as they might leak private info to other apps on the same device.
</p>
<p>
  For this reason exists the log listener feature. During init the developer can
  setup a log listener. For example, it could be a callback. If such a listener
  is set, logs should be printed to it. For every log that is provided, there should
  be 2 values. First the string of the message that would be printed and then the
  log level of that message so that it can be used as a indication of the message
  importance.
</p>
<h2>Countly Code Generator</h2>
<p>
  If you would like to understand how SDKs work by generating mobile or web code
  for events, user profiles, crash reporting, and all other features that come
  with Countly in general, we suggest you use the
  <a href="http://code.count.ly">Countly Code Generator</a>, which is a point and
  click service that builds the necessary code for you.
</p>
<h1>Making Requests</h1>
<p>
  <span style="font-weight: 400;">The Countly server is a simple HTTP based REST API server and all SDK requests should be made to&nbsp;</span><strong>/i</strong><span style="font-weight: 400;">&nbsp;endpoint with two required parameters:&nbsp;</span><strong>app_key</strong><span style="font-weight: 400;">&nbsp;and&nbsp;</span><strong>device_id</strong><span style="font-weight: 400;">.</span>
</p>
<p>
  <span style="font-weight: 400;">Other optional parameters need to be provided based on what this request should do. You may checklist all the parameters that the Countly Server can accept in&nbsp;</span><a href="https://api.count.ly/reference#i"><span style="font-weight: 400;">/i endpoint Server API reference</span></a><span style="font-weight: 400;">.</span>
</p>
<p>
  <span style="font-weight: 400;">There are some parameters that should be added to all requests even though they are not mandatory. Together with the required parameters they form the base request. Every request sent to the server should be formed from this base request. the parameters in it are: "app_key", "device_id", "timestamp", "hour", "dow", "tz", "sdk_version". "sdk_name".</span>
</p>
<p>
  <span style="font-weight: 400;">In cases where some devices may be offline, etc., and requests should be queued, it is highly recommended you add a timestamp to each request, displaying when it was created.</span>
</p>
<div class="callout callout--info">
  <h3 class="callout__title">Encoding URI components</h3>
  <p>
    <span style="font-weight: 400;">Due to the possible use of the ‘&amp;’ and ‘?’ symbols in encoded JSON strings, SDKs should encode uri components before adding them to the request and sending it to the server.</span>
  </p>
</div>
<h2>Using GET or POST</h2>
<p>
  <span style="font-weight: 400;">By default, the preferred method is to make GET requests for the Countly servers. However, there may be some length limitation for GET requests based on specific platform or server settings. Thus, the best practice is to make a POST request when the data reaches over 2,000 characters for a single request.</span>
</p>
<p>
  <span style="font-weight: 400;">Before making each request, you will need to check if the data you are going to send is less than 2,000 characters. If so, use GET. If you have more characters, use POST.</span>
</p>
<p>
  <span style="font-weight: 400;">Additionally, the SDK should be able to switch to post completely if a user should so specify in the SDK configuration/settings.</span>
</p>
<h1>SDK storage</h1>
<p>
  <span style="font-weight: 400;">Some things in the SDK are stored persistently, for example, request queue, event queue etc. Those should be stored in the device storage.</span>
</p>
<p>
  <span style="font-weight: 400;">If possible, those persistent values should be segmented by the appKey. That means that for every appKey there should be different storage for their queues.</span><span style="font-weight: 400;"></span>
</p>
<h1>Request queue</h1>
<p>
  <span style="font-weight: 400;">(in case per app key storage is not available)</span>
</p>
<p>
  <span style="font-weight: 400;">In some cases, users might be offline, thus they are not able to make requests to the server. In other cases, the server may be down or in maintenance, thus unable to accept requests. In both cases, the SDK should handle queuing and persistently storing requests made to the Countly server and should wait for a successful response from the server before removing a request from the queue.</span>
</p>
<p>
  <span style="font-weight: 400;">Note that requests should be made in historical order, meaning you must also preserve the order of your queue.</span>
</p>
<p>
  <span style="font-weight: 400;">Simple flow on how requests should appear as follows:</span>
</p>
<ol>
  <li>
    <span style="font-weight: 400;">Initiating request - either a new event reported or session call, etc.</span>
  </li>
  <li>
    <span style="font-weight: 400;">Creating a payload - take all the parameters (including the current timestamp) and the values needed for a request and generate a payload which will be included in the HTTP request</span>
  </li>
  <li>
    <span style="font-weight: 400;">This payload is inserted into the queue (First In, First Out)</span>
  </li>
  <li>
    <span style="font-weight: 400;">All updates to the queue should be persistently stored. Based on the environment, you may directly use storage for the queue</span>
  </li>
  <li>
    <span style="font-weight: 400;">On some other thread there should be a request processor which takes the first request in the queue, applies the checksum if needed, determines the request type (GET or POST) based on the length, and makes the HTTP request</span>&nbsp;<br>
    <ul>
      <li>
        <span style="font-weight: 400;">if the request is successful, then it should be removed from the queue and the next request will be processed upon the next iteration</span>
      </li>
      <li>
        <span style="font-weight: 400;">if the request failed, the request processor should have a cool-down period, lasting a minute or so (configurable value), and it will then try the same request again until it is completed</span>
      </li>
    </ul>
  </li>
</ol>
<div class="img-container">
  <img src="https://count.ly/images/guide/PPNhED7RiGZC0StuDYBd_SDK%20queue%20flow.png">
</div>
<p>
  <span style="font-weight: 400;">There are multiple scenarios why a request might fail, so to ensure that the request is successfully delivered to the server SDK, you will need to assure the following has taken place:</span>
</p>
<ol>
  <li>
    <span style="font-weight: 400;">The HTTP response code was successful (which is any 2xx code or code between 200 &lt;= x &lt; 300)</span>
  </li>
  <li>
    <span style="font-weight: 400;">The returned request is a JSON object that contains the field "result" (there can be other fields)</span>
  </li>
</ol>
<p>
  <span style="font-weight: 400;">The server replies with a JSON object, which should have a property named "result". Usually that value will be "Success". There may be scenarios where a different "result" value is returned or where additional fields may be added. </span>
</p>
<p>
  If the response code is within the required interval and the response text is
  a JSON object which has the key "result" (the value of that entry does not matter),
  then it means the request was successfully delivered to the server and can be
  removed from the queue.
</p>
<h2>Queue size limit</h2>
<p>
  <span style="font-weight: 400;">We need to limit the queue size so that it doesn’t overflow, and so that syncing up won’t take too long if some specific server is down for too long. This limit would be in the number of stored queries, and this limit should be available for the end-user to change as the SDK settings.</span>
</p>
<p>
  <span style="font-weight: 400;">In case this limit is reached, the SDK should remove older queries and insert new ones. The default limit may change from what the SDK needs, but the suggested limit is&nbsp;</span><strong>1,000 queries</strong><span style="font-weight: 400;">.</span>
</p>
<h1>Crash reporting</h1>
<p>
  <span style="font-weight: 400;">On some platforms the automatic detection of errors and crashes is possible. In this case, your SDK may report them to the Countly server, and just as with other similar functions, this is also optional. If a crash report is not sent, it won't be displayed on the dashboard under the Crashes section. Here is more information on&nbsp;</span><a href="https://api.count.ly/reference#section-crash-analytics" target="_self">Crash reporting parameters</a><span style="font-weight: 400;">&nbsp;that you may use in your SDK.</span>
</p>
<p>
  <span style="font-weight: 400;">In regard to crashes, all information, except the app version and OS, is optional, but you should collect as much information about the device as possible to assure each crash may be more identifiable with additional data. You should also provide a way for users to log errors manually (for example, logging handled exceptions which are not fatal).</span>
</p>
<p>
  <span style="font-weight: 400;">Basically, for automatically captured errors, you should set the&nbsp;</span><strong>_nonfatal</strong><span style="font-weight: 400;">&nbsp;property to false, whereas on user logged errors the&nbsp;</span><strong>_nonfatal</strong><span style="font-weight: 400;">&nbsp;property should be true. You should also provide a way to set custom key/values to be reported as segments with crash reports, either by providing global default segments or setting separately for automatically tracked errors and user logged errors.</span>
</p>
<p>
  <span style="font-weight: 400;">Additionally, there should be a way for the SDK user to leave breadcrumbs that would be submitted together with the crash reports. In order to collect breadcrumbs as logs, create an empty array upon initialization and provide a method to add breadcrumbs as strings into that array as elements for log. Also, in the event of a crash, concatenate the array with new line symbols and submit under the&nbsp;</span><strong>_logs</strong><span style="font-weight: 400;">&nbsp;property. There is no need to persistently save those logs on a device, as we would like to have a clean log on every app start.</span>
</p>
<p>
  <span style="font-weight: 400;">The end API could look like this (but it should be totally based on the specific platform error handling):</span>
</p>
<ul>
  <li>Countly.enable_auto_error_reporting(map segments)</li>
  <li>
    Countly.log_handled_error(string title, string stack, map segments)
  </li>
  <li>
    Countly.log_unhandled_error(string title, string stack, map segments)
  </li>
  <li>Countly.add_breadcrumb(string log)</li>
</ul>
<h2>Symbolication (WIP)</h2>
<h1>Events</h1>
<p>
  <span style="font-weight: 400;">Events (or custom events) are the basic Countly reporting tool that reports when something has happened in the app. Someone clicked a button, performed a specific action, etc. All of these examples could be recorded as an event.</span>
</p>
<p>
  <span style="font-weight: 400;">Events should be provided by the SDK user who knows what's important for the app to log. Also, events may be used to report some internal Countly events starting with the&nbsp;</span><strong>[CLY]_</strong><span style="font-weight: 400;">&nbsp;prefix, which vary per feature implementation on different platforms.</span>
</p>
<p>
  <span style="font-weight: 400;">An event must contain&nbsp;</span><strong>key</strong><span style="font-weight: 400;">&nbsp;and&nbsp;</span><strong>count</strong><span style="font-weight: 400;">&nbsp;properties. If the count is not provided, it should default to&nbsp;1. Optionally, a user may also provide the&nbsp;</span><strong>sum</strong><span style="font-weight: 400;">&nbsp;property (for example, in-app purchase events), the&nbsp;</span><strong>dur</strong><span style="font-weight: 400;">&nbsp;property for recording some duration/period of time and&nbsp;</span><strong>segmentation</strong><span style="font-weight: 400;">&nbsp;as a map with keys and values for segmentation.</span>
</p>
<p>
  <span style="font-weight: 400;">More on event formatting may be found in the&nbsp;</span><a href="https://api.count.ly/reference#i%23section-events"><span style="font-weight: 400;">API Reference</span></a><span style="font-weight: 400;">.</span>
</p>
<p>
  <span style="font-weight: 400;">Here are a few examples of events:</span>
</p>
<p>
  <strong>User logged into the game</strong> * key = login * count = 1
</p>
<p>
  <strong>User completed a level in the game with a score of 500&nbsp;</strong>*
  key = level_completed * count = 1 * segmentation = {level=2, score=500}
</p>
<p>
  <strong>User purchased something in the app worth 2.99 on the main screen</strong><span style="font-weight: 400;">&nbsp;* key = purchase * count = 1 * sum = 2.99 * dur = 30 * segmentation = {screen=main}</span>
</p>
<p>
  <span style="font-weight: 400;">As you can imagine, your SDK should provide methods to cover these combinations, either by default values or by function parameter overloading, etc.:</span>
</p>
<ul>
  <li>Countly.event(string key)</li>
  <li>Countly.event(string key, int count)</li>
  <li>Countly.event(string key, double sum)</li>
  <li>Countly.event(string key, double duration)</li>
  <li>Countly.event(string key, int count, double sum)</li>
  <li>Countly.event(string key, map segmentation)</li>
  <li>Countly.event(string key, map segmentation, int count)</li>
  <li>
    Countly.event(string key, map segmentation, int count, double sum)
  </li>
  <li>
    Countly.event(string key, map segmentation, int count, double sum, double
    duration)
  </li>
</ul>
<p>
  <strong>Note</strong>: <strong>count</strong> value defaults to 1 internally
  if not specified.
</p>
<h2>Timed Events</h2>
<p>
  <span style="font-weight: 400;">In short, you may report time with the&nbsp;</span><strong>dur</strong><span style="font-weight: 400;">&nbsp;property in an event. It is good practice to allow the user to measure some periods internally using the SDK API. For that purpose, the SDK needs to provide the methods below:</span>
</p>
<ul>
  <li>
    <strong>startEvent(string key)</strong><span style="font-weight: 400;">&nbsp;- which will internally save the event key and current timestamp in the associative array/map.</span>
  </li>
  <li>
    <strong>endEvent(string key, map segmentation, int count, double sum)</strong><span style="font-weight: 400;">&nbsp;- which will take the event starting timestamp by the event key from the map, get the current timestamp and calculate the duration of the event. It will then fill it up as&nbsp;a </span><strong>dur</strong><span style="font-weight: 400;">&nbsp;property and report an event, just as you would report any regular event.</span>
  </li>
  <li>
    <strong>endEvent(string key)</strong><span style="font-weight: 400;">&nbsp;- which will simply end the event with a 1 as the count, 0 as the sum, and nil as the segmentation values.</span>
  </li>
</ul>
<p>
  <span style="font-weight: 400;">If possible, the SDK may provide a way to start multiple timed events with the same key, such as returning an event instance in the method and then calling the end method on that instance.</span>
</p>
<p>
  <span style="font-weight: 400;">If not, the following calls should be ignored: 1. events which have already started 2. events which have attempted to start again 3. events which have already ended 4. events which have attempted to end. Otherwise, they will provide an informative error.</span>
</p>
<h1>Session flow</h1>
<p>
  For SDK's to track use sessions, there are 3 kinds of calls:
</p>
<ul>
  <li>
    begin_session - indicates that a session was just started or the app came
    to the foreground
  </li>
  <li>
    end_session - indicates the the session ended or the app went to the background
  </li>
  <li>
    session_duration (update) - indicates that the session is still continuing
    and records the elapsed time since the last update or begin_session call
  </li>
</ul>
<p>SDK sessions can be managed in 2 ways:</p>
<ul>
  <li>
    automatically by the SDK (with sufficient integration) - session requests
    would be sent according to the app lifecycle together with automatic session
    update requests after periodic timeframes (60 seconds by default)
  </li>
  <li>
    manually by the developer - session requests would be triggered by the developer.
    This includes also the periodic update requests
  </li>
</ul>
<h2>Automatic session tracking</h2>
<p>
  Automatic tracking should be done according to the platforms lifecycle. For apps
  that have a visual component (not command line or server call tracking), sessions
  should be tracked when the app is visible and in the foreground. That would mean
  starting the session when the app comes into foreground and ending the it goes
  to the background.
</p>
<h2>Manual session tracking (WIP)</h2>
<p>
  <span style="font-weight: 400;">Most of the official SDKs implement automatic session handling, meaning SDK users don't need to separately bother with session calls. However, it is good practice to provide a way to disable automatic session handling and allow SDK users to make session calls themselves through methods such as:</span>
</p>
<ul>
  <li>Countly.begin_session()</li>
  <li>Countly.session_duration(int seconds)</li>
  <li>Countly.end_session(int seconds)</li>
</ul>
<p>
  <span style="font-weight: 400;">Here is the documentation showing how you may&nbsp;</span><a href="https://api.count.ly/reference#i%23section-session"><span style="font-weight: 400;">report sessions through our API</span></a><span style="font-weight: 400;">.</span>
</p>
<h2>Session API</h2>
<p>
  All these session requets are built uppon the base request which includes all
  the base params, therefore those won't be explicitly mentioned.
</p>
<h3>Starting a session</h3>
<p>
  <span style="font-weight: 400;">The SDK should then send the </span><strong>begin_session=1</strong><span style="font-weight: 400;"> param. This same request should also contain metrics parameters with the maximum metrics described on </span><a href="https://api.count.ly/reference#i"><span style="font-weight: 400;">/i page</span></a><span style="font-weight: 400;">, which may be collected from this SDK-specific environment/language. It might look something like:<br></span>
</p>
<pre><span style="font-weight: 400;">"&amp;begin_session=1&amp;metrics={...}"</span></pre>
<h3>Session update</h3>
<p>
  <span style="font-weight: 400;">Each minute of the session should be extended by sending the <strong>session_duration</strong> param with the number of seconds that passed since the previous session request (begin_session or session_duration, whichever was last). It might look something like:</span>
</p>
<pre><span style="font-weight: 400;">"&amp;session_duration=60"</span></pre>
<h3>Ending a session</h3>
<p>
  <span style="font-weight: 400;">The SDK should send the </span><strong>end_session=1</strong><span style="font-weight: 400;"> param, including the <strong>session_duration</strong> parameter with how many seconds passed since the last session request (begin_session or session_duration, whichever was last). It might look something like this:</span>
</p>
<pre><span style="font-weight: 400;">"&amp;end_session=1&amp;session_duration=15"</span></pre>
<h3>Sample uses</h3>
<p>
  <span style="font-weight: 400;">Here are a few example requests generated by different session lengths:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">2 min 30 second session</span>
    <span class="tabs-link">30 second session</span>
  </div>
  <div class="tab">
    <pre><code class="text">begin_session=1&amp;metrics={...}
session_duration=60
session_duration=60
end_session=1&amp;session_duration=30</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="text">begin_session=1&amp;metrics={...}
end_sesson=1&amp;session_duration=30</code></pre>
  </div>
</div>
<h2>Session cooldown</h2>
<p>
  <span style="font-weight: 400;">In some cases, it is difficult to know for sure if a session has ended, such as with web analytics when a user is leaving the page, and whether they will visit another page or not. This is why there is a small&nbsp;</span><em><span style="font-weight: 400;">cooldown</span></em><span style="font-weight: 400;">&nbsp;time of 15 seconds. If the end_session request is sent and then the begin_session request is sent within 15 seconds, it will be counted as the same session, and the session duration will extend this session instead of applying it to the new one.</span>
</p>
<p>
  <span style="font-weight: 400;">This makes it easier to call the end_session on each page unload without worrying about starting a new session if the user visits another page.</span>
</p>
<p>
  <span style="font-weight: 400;">If you don't need this behavior, simply pass the&nbsp;</span><strong>ignore_cooldown=true</strong><span style="font-weight: 400;">&nbsp;parameter to all the session requests and the server will not extend the session. Rather, it will always count it as a new session.</span>
</p>
<p>
  <span style="font-weight: 400;">The 15-second cooldown is a default value and may be configured on the server, so don't rely on it being 15 seconds.</span>
</p>
<h1>Recording time of data</h1>
<p>
  <span style="font-weight: 400;">To properly report and process data (especially queued data), you should also provide the time when the data was recorded. You will need to provide 3 parameters with each request:</span>
</p>
<ul>
  <li>
    <strong>timestamp</strong>:
    <span style="font-weight: 400;">13-digit UTC millisecond unique timestamp of the moment of action</span>
  </li>
  <li>
    <strong>hour</strong>:
    <span style="font-weight: 400;">Current user local hour (0 - 23)</span>
  </li>
  <li>
    <strong>dow</strong>:&nbsp;<span style="font-weight: 400;">Current user day of the week (0-Sunday, 1 - Monday, ... 6 - Saturday)</span>
  </li>
  <li>
    <strong>tz</strong>:
    <span style="font-weight: 400;">Current user time zone in minutes (120 for UTC+02, -300 for UTC-05)</span>
  </li>
</ul>
<p>
  <span style="font-weight: 400;">As multiple events may be combined in a single request, you should also provide these parameters automatically in every event object.</span>
</p>
<p>
  <span style="font-weight: 400;">The suggested millisecond timestamp should be unique, meaning if events were reported in the same timestamp, the SDK should update the millisecond timestamp in the order in which the events were reported. The pseudo-code to the unique millisecond timestamp could appear as follows:</span>
</p>
<pre><code class="javascript">//variable to hold last used timestamp
lastMsTs = 0;

function getUniqueMsTimestamp(){
  //get current timestamp in miliseconds
  ts = getMsTimestamp();
  
  //if last used timestamp is equal or greater
  if(lastMsTs &gt;= ts){
    //increase last used
    lastMsTs++;
  }
  else{
    //store current timestamp as last used
    lastMsTs = ts;
  }
  //return timestamp
  return lastMsTs;
}</code></pre>
<p>
  <span style="font-weight: 400;">If it’s impossible to use a millisecond timestamp on a specific platform, you may also use a 10-digit UTC seconds timestamp.</span>
</p>
<h1>API of the SDK</h1>
<p>
  <span style="font-weight: 400;">Depending on the SDK’s environment/language there could be a different set of features supported. Some of these features may be supported on any platform, whereas others are quite platform-specific. For example, a desktop app type may not be providing telecom operator information.</span>
</p>
<p>
  <span style="font-weight: 400;">Note that function and argument namings are only examples of what it could be. Try to follow your platform/environment/language best practices when creating and naming functions and variables.</span>
</p>
<p>
  <span style="font-weight: 400;">Here is a list of things your SDK could support:</span>
</p>
<h1>Core features</h1>
<p>
  <span style="font-weight: 400;">Core features are the minimal set of features that the SDK should support, and these features are platform-independent.</span>
</p>
<h2>Initialization</h2>
<p>
  <span style="font-weight: 400;">In its official SDKs, Countly is used as a singleton object or basically an object with a shared instance. Still, there are some parameters that need to be provided before the SDK can work. Usually, there is an "init" method which accepts the URL, app key, and device_id (or the SDK generates it itself if it’s not provided):</span>
</p>
<pre><code class="java">Countly.init(string url="https://try.count.ly", string app_key, string device_id, ...)
</code></pre>
<h2>Device metrics</h2>
<p>
  <span style="font-weight: 400;">Metrics should only be reported together with the begin_session=1 parameter on every session start. Collect as many metrics as possible or allow some values to be provided by the user upon initialization. Possible metrics are listed in the&nbsp;</span><a href="https://api.count.ly/reference#i%23section-metrics"><span style="font-weight: 400;">API Reference</span></a><span style="font-weight: 400;">.</span>
</p>
<p>
  <span style="font-weight: 400;">One thing that we should agree on is identifying platforms with the same string overall SDKs, so here is the list of how we would suggest identifying platforms for the server through the&nbsp;</span><strong>_os</strong><span style="font-weight: 400;">&nbsp;metric.</span>
</p>
<ul>
  <li>
    <strong>Android</strong> - for Android
  </li>
  <li>
    <strong>BeOS</strong> - for BeOS
  </li>
  <li>
    <strong>BlackBerry</strong> - for BlackBerry
  </li>
  <li>
    <strong>iOS</strong> - for iOS
  </li>
  <li>
    <strong>Linux</strong> - for Linux
  </li>
  <li>
    <strong>Open BSD</strong> - for Open BSD
  </li>
  <li>
    <strong>os/2</strong> - for OS/2
  </li>
  <li>
    <strong>macOS</strong> - for Mac OS X
  </li>
  <li>
    <strong>QNX</strong> - for QNX
  </li>
  <li>
    <strong>Roku</strong> - for Roku
  </li>
  <li>
    <strong>SearchBot</strong> - for SearchBots
  </li>
  <li>
    <strong>Sun OS</strong> - for Sun OS
  </li>
  <li>
    <strong>Symbian</strong> - for Symbian
  </li>
  <li>
    <strong>Tizen</strong> - for Tizen
  </li>
  <li>
    <strong>tvOS</strong> - for Apple TV
  </li>
  <li>
    <strong>Unix</strong> - for Unix
  </li>
  <li>
    <strong>Unknown</strong> - if the operating system is unknown
  </li>
  <li>
    <strong>watchOS</strong> - for Apple Watch
  </li>
  <li>
    <strong>Windows</strong> - for Windows
  </li>
  <li>
    <strong>Windows Phone</strong> for Windows Phone
  </li>
</ul>
<h2>SDK Metadata</h2>
<p>
  <span style="font-weight: 400;">The SDK should send the following metadata with every request.</span>
</p>
<ul>
  <li>SDK name:</li>
</ul>
<p>
  Query String Key: <code>sdk_name</code> Query String Value:
  <code>[language]-[origin]-[platform]</code> Example:
  <code>&amp;sdk_name=objc-native-ios</code>
</p>
<ul>
  <li>SDK version:</li>
</ul>
<p>
  Query String Key: <code>sdk_version</code> Query String Value: SDK version as
  string Example: <code>&amp;sdk_version=20.10.0</code>
</p>
<p>
  The SDK versions decode to [year].[month].[minor release number]. The SDK major
  versions&nbsp; (year, month) should follow the server versions. Those are usually
  incremented twice a year during our major releases. Minor release numbers should
  start ar "0". Major version numbers (year, month) should stay the same even if
  the SDK version is released a couple of months after the indicated date. If the
  servers version is released in October 2020 the major versions would be "20.10".
  The first version released by the SDK, that would be in sync with this server
  version, would have the version "20.10.0". If the SDK needs to release an update
  in January of 2021 and no major server release has happened, the next version
  released by the SDK will be "20.10.1".
</p>
<p>
  No zeroes should be added to the second number (indicating the month) in case
  the release happens before October.
</p>
<h2>Additional parameters</h2>
<p>
  <span style="font-weight: 400;">There are also optional, additional parameters. If you can get them on your platform, then you may append them to any/every request. However, if you can’t, it might be a good idea to allow the SDK user to optionally provide such values.</span>
</p>
<p>
  <span style="font-weight: 400;">If values are not provided, the Countly server will try to determine them automatically, based on all the other provided data.</span>
</p>
<p>
  Here is
  <a href="https://api.count.ly/reference#section-additional-parameters" target="_self">more information</a>
  on possible additional API parameters.
</p>
<h2>Reserved Segmentation keys</h2>
<p>
  <span style="font-weight: 400;">Currently, there are 9 segmentation keys that are reserved for Countly’s internal use. They should be ignored when the SDK user provides them as segmentation for any functionality. The list of keys is as follows:</span>
</p>
<ul>
  <li>name</li>
  <li>segment</li>
  <li>visit</li>
  <li>start</li>
  <li>bounce</li>
  <li>exit</li>
  <li>view</li>
  <li>domain</li>
  <li>dur</li>
</ul>
<h1>View tracking</h1>
<p>
  <span style="font-weight: 400;">Reporting views would allow you to analyze which views/screens/pages were visited by the app user as well as how long they spent on a specific view. If it is possible to automatically determine when a user visits a specific view in your platform, then you should provide an option to automatically track views. Also, it is important to provide a way to track views manually. Here is&nbsp;</span><a href="https://api.count.ly/reference#section-views" target="_self">more information on view-tracking API</a><span style="font-weight: 400;">s</span><span style="font-weight: 400;">.</span>
</p>
<p>
  <span style="font-weight: 400;">Let's start with manual view tracking, as it should be available on any platform. First, you will need to have 2 internal private properties as&nbsp;</span><strong>string lastView</strong><span style="font-weight: 400;">&nbsp;and&nbsp;</span><strong>int lastViewStartTime</strong><span style="font-weight: 400;">. Then, create an internal private method&nbsp;</span><strong>reportViewDuration</strong><span style="font-weight: 400;">, which checks if </span><strong>lastView</strong><span style="font-weight: 400;">&nbsp;is null, and if not, it should report the duration for&nbsp;</span><strong>lastView</strong><span style="font-weight: 400;"> by calculating it based off the current timestamp and&nbsp;</span><strong>lastViewStartTime</strong><span style="font-weight: 400;">.</span>
</p>
<p>
  <span style="font-weight: 400;">After those steps, provide a&nbsp;</span><strong>reportView</strong><span style="font-weight: 400;">&nbsp;method to set the view name as a string parameter inside this method call&nbsp;</span><strong>reportViewDuration</strong><span style="font-weight: 400;"> to report the duration of the previous view (if there is one). Then set the provided view name as&nbsp;</span><strong>lastView&nbsp;</strong><span style="font-weight: 400;">and the current timestamp as&nbsp;</span><strong>lastViewStartTime</strong><span style="font-weight: 400;">. Report the view as an event with the&nbsp;</span><strong>visit</strong><span style="font-weight: 400;">&nbsp;property and&nbsp;</span><strong>segment</strong><span style="font-weight: 400;">&nbsp;as your platform name. Additionally, if this is the first view a user visits in this app session, then also report the&nbsp;</span><strong>start</strong><span style="font-weight: 400;">&nbsp;property as true. You will also need to call&nbsp;</span><strong>reportViewDuration</strong><span style="font-weight: 400;"> with the app exit event.</span>
</p>
<p>
  <span style="font-weight: 400;">After manual view tracking has been implemented, you may also implement automatic view tracking (if it is available on your platform). To implement automatic view tracking, you will need to catch your platform's specific event when the view is changed and call your implemented&nbsp;</span><strong>reportView</strong><span style="font-weight: 400;">&nbsp;method with the view name.</span>
</p>
<p>
  <span style="font-weight: 400;">Additionally, you will need to implement enabling and disabling automatic view tracking, as well as status checking, despite whether automatic view tracking is currently enabled or not.</span>
</p>
<p>
  <span style="font-weight: 400;">The pseudo-code to implement view tracking could appear as follows:</span>
</p>
<pre><code class="java">class Countly {
    String lastView = null;
    int lastViewStartTime = 0;
    boolean autoViewTracking = false;
    
    private void reportViewDuration(){
        if(lastView != null){
             //create event with parameters and 
             //calculating dur as getCurrentTimestamp()-lastViewStartTime
        }
    }
    
    void onAppExit(){
        reportViewDuration();
    }
    
   void onViewChanged(String view){
      if(autoViewTracking)
          reportView(view);
   }
    
    public void reportView(String name){
        //report previous view duration
        reportViewDuration();
        lastView = name;
        lastViewStartTime = getCurrentTimestamp();
        //create event with parameters without duration
       // duration will be calculated on next view start or app exit
    }
    
    public void setAutoViewTracking(boolean enable){
        autoViewTracking = enable;
    } 
    
    public boolean getAutoViewTracking(){
        return autoViewTracking;
    }
}</code></pre>
<p>
  <span style="font-weight: 400;">Additionally, if your platform supports actions on view, such as clicks, you may report them as well. Here is more information on&nbsp;</span><a href="https://api.count.ly/reference#section-view-actions" target="_self">reporting actions for views</a><span style="font-weight: 400;">.</span>
</p>
<h2>Orientation changes</h2>
<p>Orientation change tracking requires "users" consent.</p>
<p>
  This feature sends a event of the current orientation. It is sent when the first
  screen loads and every time the orientation changes.
</p>
<h1>Device ID management</h1>
<p>
  <span style="font-weight: 400;">There are 3 main cases where the SDK user might like to provide a custom device ID to identify a device/user.</span>
</p>
<p>
  <strong>1. Tracking the same user across multiple devices</strong>
</p>
<p>
  <span style="font-weight: 400;">In this case, the app developers will need to provide their own way to identify users upon initialization. The Countly SDK needs to provide a way to set the custom device ID upon initialization and store it persistently for the next session use. If there is an already stored device ID, the Countly SDK should primarily use the stored one, unless forced to do otherwise.</span>
</p>
<p>
  <strong>2. Tracking multiple users on the same device</strong>
</p>
<p>
  <span style="font-weight: 400;">In addition to initialization, developers may need to change the device ID while the app is running. For example, when an end-user signs out and another end-user signs in. In this case, the Countly SDK needs to provide a way to change the device ID at any point while the app is running. It should replace the internally used device ID with the new one, and use it for all new requests, persistently storing it for further sessions. The Countly SDK should follow these steps:</span>
</p>
<ul>
  <li>
    <strong><span style="font-weight: 400;">Add currently recorded, but not queued, events to the request queue</span></strong>
  </li>
  <li>End the current session</li>
  <li>Clear all started timed-events</li>
  <li>
    <span style="font-weight: 400;">Change the device ID and store it persistently for further session use</span>
  </li>
  <li>
    <span style="font-weight: 400;">Begin a new session with the new device ID</span>
  </li>
</ul>
<p>
  <strong>3. Tracking an unauthenticated user who later becomes authenticated</strong>
</p>
<p>
  <span style="font-weight: 400;">Developers may need to change a device ID to their own internal user ID and merge the server-side data previously generated by a user while he/she was unauthenticated. It is similar to Case 2, but the Countly SDK will need to merge the data on the server as well. In order to make a proper transition, the Countly SDK should follow these steps:</span>
</p>
<ul>
  <li>
    <span style="font-weight: 400;">Temporarily keep the current device ID</span>
  </li>
  <li>
    <span style="font-weight: 400;">Change the device ID and store it persistently for further session use</span>
  </li>
  <li>
    <span style="font-weight: 400;">Use the&nbsp;</span><a href="https://api.count.ly/reference#section-change-id-and-merge-data" target="_self">old_device_id</a><span style="font-weight: 400;">&nbsp;API with the temporarily kept, old device ID to merge the data on the server</span>
  </li>
  <li>
    <span style="font-weight: 400;">No need to end and restart the current session or clear started timed-events</span>
  </li>
</ul>
<p>
  <span style="font-weight: 400;">To summarize, the Countly SDK should provide a proper way to change device IDs for all 3 cases.</span>
</p>
<p>
  <strong>Note:</strong>&nbsp;<span style="font-weight: 400;">If a new and current device ID is exactly the same, then the Countly SDK must ignore this change call.</span>
</p>
<h1>Push Notifications</h1>
<p>
  <span style="font-weight: 400;">Push notifications are platform-specific and not all platforms have them. However, if your platform does, you would need to register your device to the push notification server and send the token to the Countly server. For more information, please click&nbsp;</span><a href="https://api.count.ly/reference#section-push-notifications" target="_self">here</a><span style="font-weight: 400;">&nbsp;for API calls.</span>
</p>
<p>
  <span style="font-weight: 400;">From the SDK API point of view, there could be one simple function to enable push notifications for the Countly server:</span>
</p>
<pre><code class="text">Countly.enable_push()</code></pre>
<h1>Recording location</h1>
<p>
  There are 4 location related parameters that can be set in a Countly SDK. It
  is "country code" (in ISO format), "city", "location_gps" (GPS coordinates),
  "IP" address. Their params in API requests are: "country_code", "city", "location",
  "ip".
</p>
<p>
  Location information is not stored persistently (in a way that would survive
  SDK shutdowns un further inits). Location information is stored only in memory
  as variables. The SDK should cache only the latest location information.
</p>
<p>
  The SDK has a single "setLocation" request where the dev can pick and choose
  which values he wants to set. All set values are sent in a single request. The
  provided values overwrite the previously cached values. If some field was left
  out of the "setLocation" request, that means that the previously cached value
  should be erased. Only the params that are not null and not empty strings should
  be sent.
</p>
<p>
  Init should have a way to set all location values (through config): location_gps,
  city, country, ipAddress. Init config should also have a call to disable location.
  If during init location is disabled and location values have been set, the disable
  location call should take precedence.
</p>
<p>
  If there is session consent, location values set in init should be sent in the
  first "begin_session" request and cached internally. Location values set after
  init but before the first begin session request would overwrite the values set
  in init and should be sent with the first begin_session request. If there is
  no session consent or automatic session recording is disabled, location values
  set in init should be sent as a separate request that contains only location
  values and they should be cached internally.
</p>
<p>
  If during init location tracking is disabled and session consent is not given,
  empty "location" param should be sent in a independent request.
</p>
<p>
  Location values set after init and after the first "begin_session" request should
  be sent in a separate request and update the internal location value cache. This
  internal location cache should be added to every non-first "begin_session" request.
  Values set in newer "setLocation" calls overwrite the cached values from previous
  calls.
</p>
<p>
  If the location feature gets disabled or location consent is removed, the SDK
  sends a request with an empty "location" parameter.
</p>
<p>
  If location is disabled or no location consent is given, the SDK adds an empty
  location parameter to every "begin_session" request.
</p>
<p>
  If location consent is given and location gets reenabled (previously was disabled),
  we send that set location information in a separate request and save it in the
  internal location cache.
</p>
<p>
  If location consent was removed and is given back, no special action needs to
  be taken.
</p>
<p>
  If city is not paired together with country, a warning should be printed that
  they should be set together.
</p>
<p>
  When an empty "location" entry is sent to the server, it is interpreted as "disable
  location tracking for this device ID".
</p>
<p>Empty country code, city and IP address can not be sent.</p>
<p>Some sample situations for handling location:</p>
<p>
  <strong>1) dev sets location some time after init</strong><br>
  init without location<br>
  begin_session (without location)<br>
  setLocation(gps) (location request with gps)<br>
  end_session<br>
  begin_session (with location - gps)<br>
  end_session<br>
  begin_session (with location - gps)<br>
  end_session
</p>
<p>
  <strong>2) dev sets location during init and a separate call</strong><br>
  init with location (city, country)<br>
  begin_session (with location - city, country)<br>
  setLocation(gps) (location request with gps)<br>
  end_session<br>
  begin_session (with location - gps)<br>
  end_session<br>
  begin_session (with location - gps)<br>
  end_session
</p>
<p>
  <strong>3) dev sets location during init and after begin_session calls</strong><br>
  init with location (city, country)<br>
  begin_session (with location - city, country)<br>
  setLocation(gps) (location request with gps)<br>
  end_session<br>
  begin_session (with location - gps)<br>
  setLocation(ipAddress) (location request with ipAddress)<br>
  end_session<br>
  begin_session (with location - ipAddress)<br>
  end_session
</p>
<p>
  <strong>4) dev sets location before first begin_session</strong><br>
  init with location (city, country)<br>
  setLocation(gps, ipAddress) (location request with gps, ipAddress)<br>
  begin_session (with location - gps, ipAddress)<br>
  setLocation(city, country, gps2) (location request with city, country, gps2)<br>
  end_session<br>
  begin_session (with location - city, country, gps2)<br>
  end_session
</p>
<h1>Remote Config</h1>
<h2>Automatic Fetch</h2>
<p>
  <span style="font-weight: 400;">The Remote Config feature allows app developers to change the behavior and appearance of their applications at any time by creating or updating custom key-value pairs on the Countly Server.</span>
</p>
<p>
  <span style="font-weight: 400;">First off, interaction with the Countly Server for the Remote Config feature should be done after you have checked the&nbsp;</span><a href="https://api.count.ly/reference#osdk"><span style="font-weight: 400;">Remote Config API documentation</span></a><span style="font-weight: 400;">.</span>
</p>
<p>
  <span style="font-weight: 400;">There should be a flag upon initial config to enable the automatic fetching of the remote config upon SDK start. If this flag is set, the SDK will automatically fetch the remote config from the server and store it locally. A locally stored remote config should reflect the server response as is, overwriting any existing remote config. No merging or partial updating. Automatic fetching will be performed only upon SDK start, not with every begin session. There should also be a callback on the initial config to inform the developer about the results of automatic fetching the remote config.</span>
</p>
<p>
  e.g. <code>config.enableRemoteConfig = true;</code>
</p>
<h2>Manual Fetch</h2>
<p>
  <span style="font-weight: 400;">There should be a method/function to fetch the remote config manually anytime the developer would like. Just like with automatic fetch, this method will fetch the remote config from the server and store it locally. A locally stored remote config should reflect the server response as is, overwriting any existing remote config. No merging or partial updating. This method should take a callback argument to inform the developer about the results of manually fetching the remote config. Callback on initial config should not be affected by manual fetchings, as it is for automatic fetchings only.</span>
</p>
<p>
  e.g. <code>updateRemoteConfig(callback(){ })</code>
</p>
<h2>Getting Values</h2>
<p>
  <span style="font-weight: 400;">There should be a method to get remote config values for a given key. It will return the value for a given key. If the key does not exist, or the remote config has yet to be fetched, this method should return nil or null or however the platform handles the absence of values. If the server is not reachable, this method should return the last fetched and locally stored value if available.</span>
</p>
<p>
  e.g. <code>remoteConfigValueForKey(key)</code>
</p>
<h2>Keys and Omit Keys</h2>
<p>
  <span style="font-weight: 400;">There should be 2 additional methods for manual fetching: one for specifying which keys will be updated and one for specifying which keys will be ignored.</span>
</p>
<p>
  <span style="font-weight: 400;">These methods should take an array of keys as an argument, in addition to callbacks, and send requests with <code>keys=</code></span><span style="font-weight: 400;">&nbsp;or <code>omit_keys=</code></span><span style="font-weight: 400;">&nbsp;query strings. For the result of these requests, only the keys in the response should be updated in local storage, not a complete overwrite as with an automatic or standard manual fetch.</span>
</p>
<p>
  e.g. <code>updateRemoteConfigForKeysOnly(keys, callback(){ })</code> e.g.
  <code>updateRemoteConfigExceptKeys(keys, callback(){ })</code>
</p>
<p>
  <span style="font-weight: 400;">Example case: Local storage reflecting server as is (after an automatic or manual fetch):</span>
</p>
<pre><code>{
  "a": "x",
  "b": "y",
  "c": "z",
}</code></pre>
<p>
  <span style="font-weight: 400;">Calling update for specified keys only:</span>
</p>
<pre><code>updateRemoteConfigForKeysOnly(["a"], callback(){ });
</code></pre>
<p>Response:</p>
<pre><code>{
  "a": "xx",
}
</code></pre>
<p>Local storage:</p>
<pre><code>{
  "a": "xx",
  "b": "y",
  "c": "z",
}
</code></pre>
<h1>User feedback</h1>
<h2>Star Rating</h2>
<p>
  <span style="font-weight: 400;">If possible, the SDK should provide a simple 1 through 5 star-rating interface for receiving user feedback about the application. The interface will have a simple message explaining its purpose, a 1 through 5-star meter for receiving users’ ratings, and a dismiss button, in case the user does not wish to give a rating. This star rating has nothing to do with App Store/Google Play Store ratings and reviews. It is just for getting brief feedback from users to be displayed on the Countly dashboard.</span>
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/102515c-star-rating2x.png">
</div>
<p>
  <span style="font-weight: 400;">After a user gives a rating, a reserved event will be recorded with <code>[CLY]_star_rating</code></span><span style="font-weight: 400;">as the key and following as the segmentation dictionary:</span>
</p>
<ul>
  <li>
    <strong>platform:</strong> on which the application runs
  </li>
  <li>
    <strong>app_version:</strong> application's version number
  </li>
  <li>
    <strong>rating:</strong> user's 1-to-5 rating
  </li>
</ul>
<p>
  <span style="font-weight: 400;">If a user dismisses the star-rating dialog without giving a rating, an event will not be recorded. The star-rating dialog's message and dismiss button title may be customized using the properties on the initial configuration object.</span>
</p>
<pre><code class="java">CountlyConfiguration.starRatingMessage = "Custom Message";
CountlyConfiguration.starRatingDismissButtonTitle = "Custom Dismiss Button Title";</code></pre>
<p>
  <span style="font-weight: 400;">If not explicitly set, the message should read, "How would you rate the app?" and the dismiss button title will read, "Dismiss", or one of the corresponding localized versions depending on the device’s language.</span>
</p>
<p>
  <span style="font-weight: 400;">The star-rating dialog may be displayed in 2 ways:</span>
</p>
<p>
  <strong>1. Manually by the developer</strong>
</p>
<p>
  <span style="font-weight: 400;">The star-rating dialog will be displayed when the developers call the specified method, such as <code>askForStarRating</code></span><span style="font-weight: 400;">. Optionally, there will be a callback method indicating the user's 1-to-5 rating value for the developer in the event the developer would like to use the user's rating.</span>
</p>
<pre><code class="java">Countly.askForStarRating(callback);</code></pre>
<p>
  <span style="font-weight: 400;">There is no limit on how many times the star-rating dialog may be manually displayed.</span>
</p>
<p>
  <strong>2. Automatically, depending on the session count</strong>
</p>
<p>
  <span style="font-weight: 400;">The star-rating dialog will be displayed when the application's session count reaches a specified limit; once for each new version of the application. The SDK should keep track of the session count for each app version locally and compare it to the specified count on each app launch. This session count limit may be specified upon initial configuration.</span>
</p>
<pre><code class="java">CountlyConfiguration.starRatingSessionCount = 5;</code></pre>
<p>
  <span style="font-weight: 400;">Once the star-rating dialog has been displayed automatically, it will not be displayed again unless there is a new app version.</span>
</p>
<p>
  Upon initial configuration, there should be an optional flag called
  <code>starRatingDisableAskingForEachAppVersion</code> to force the star-rating
  dialog to be displayed only once per app lifetime, instead of for each new version.
</p>
<pre><code class="java">CountlyConfiguration.starRatingDisableAskingForEachAppVersion = false;</code></pre>
<h2>Surveys (WIP)</h2>
<p>
  Showing surveys or performing any of the survey related features require that
  the "feedback" consent is given.
</p>
<p>
  Currently there are 2 kinds of surveys: basic surveys and NPS. Both are shown
  using a very similar API and basicly the same processing.
</p>
<p>
  First step to showing a feedback widget is getting a list of the available surveys
  for this deviceID. That would be done with a function call named similar to "getAvailableFeedbackWidgets".
  That call takes a callback. That callback returns 2 values. The second is the
  error string. The first one a list of available survey objects(or any other mechanism
  that allows the grouping of this data). If a class is used for grouping, it should
  be named similar to "<span>CountlyPresentableFeedback". That object contains 2 values, widget id and widget type. Potential type values are currently "nps" and "survey".</span>
</p>
<p>The url to acquire all available widhets in a list is:</p>
<pre>/o/sdk?method=feedback&amp;app_key=[appKey]&amp;device_id=[deviceID]&amp;sdk_version=[sdkVersion]&amp;sdk_name=[sdkName]</pre>
<p>
  If parameter tampering is enabled, sha256 param should be added with the checksum.
</p>
<p>
  The server side will determine if there are any valid surveys for this device
  ID and return something similar to:
</p>
<pre>{"result":[{"_id":"5f8c6f959627f99e8e7de746","type":"survey"},{"_id":"5f8c6fd81ac8659e8846acf4","type":"nps"}]}</pre>
<p>
  "result" contains a JSON array of objects. The json object contains a 'id' and
  'type'. Possible type values are "survey" and "nps". Both are used to mark the
  surveys type. The id is used to construct the web view url.
</p>
<p>&nbsp;</p>
<p>
  <span>The idea is that the developer would retrieve this list of potential widgets and decide any further action he would want to make with them.</span>
</p>
<p>
  If the developer has decided on a survey to present, he would call "presentFeedbackWidget"
  and pass the chosen "CountlyFeedbackWidget<span>" object.</span>
</p>
<p>
  Using information from that object, a widget url will be constructed and presented
  in a webView or other similar mechanism. That webview will perform further survey
  interraction.
</p>
<p>Using that id we contstruct a url that looks like:</p>
<pre>//for nps<br>/feedback/nps?widget_id=[widgetID]&amp;device_id=[deviceID]&amp;app_key=[appKey]&amp;sdk_version=[sdkVersion]&amp;sdk_name=[sdkName]&amp;app_version=[appVersion]&amp;platform=[platform]<br><br>//for basic surveys<br>/feedback/survey?widget_id=[widgetID]&amp;device_id=[deviceID]&amp;app_key=[appKey]&amp;sdk_version=[sdkVersion]&amp;sdk_name=[sdkName]&amp;app_version=[appVersion]&amp;platform=[platform]<br><br>//web SDK would also pass "origin"<br>//web SDK also passes "widget_v=Web"</pre>
<p>
  The created url contains params for: widget_id, device_id, app_key, sdk_version,
  sdk_name, app_version, platform, origin (for&nbsp; web SDK). Even if parameter
  tamper protection is enabled, this url does not use the checksum param.
</p>
<p>
  That url then should be provided to a webview and shown as a alert dialog similar
  to the rating widget.&nbsp;
</p>
<p>
  If temporary device ID is enabled, feedback widgets can't be shown and a empty
  list of available widgets is returned.
</p>
<h1>User Profiles</h1>
<p>
  <span style="font-weight: 400;">Your SDK does not need to have a platform-specific way to receive user data if it isn’t possible on your platform. However, you will need to provide a way for a developer to pass this information to the SDK and send it to the Countly server.</span>
</p>
<p>
  <span style="font-weight: 400;">To do so, you may create a method to accept an object with key/regarding the user, which are&nbsp;</span><a href="https://api.count.ly/reference#section-user-details" target="_self">described here</a><span style="font-weight: 400;">, or provide a parameterized method to pass the information regarding the user. Note that all fields are optional.</span>
</p>
<p>
  <span style="font-weight: 400;">Additionally, there could be custom key values added to the user details. In this case, you would need to provide a means to set them:</span>
</p>
<ul>
  <li>Countly.user_details(map details)</li>
  <li>Countly.user_custom_details(map custom_details)</li>
</ul>
<p>
  <span style="font-weight: 400;">You may find more information on what data may be set for a user&nbsp;</span><a href="https://api.count.ly/reference#section-user-details" target="_self">by following this link</a><span style="font-weight: 400;">.</span>
</p>
<h2>Modifying custom data properties</h2>
<p>
  <span style="font-weight: 400;">You should also provide an option to modify custom user data, such as by increasing the value on the server by 1, etc. Since there are many operations you could perform with that data, it is recommended to implement a subclass for this API, which may be retrieved through the Countly instance.</span>
</p>
<p>
  <span style="font-weight: 400;">The standard methods that should be provided by the SDK are as follows (provided as pseudo-code, naming conventions may differ from platform to platform):</span>
</p>
<ul>
  <li>Countly.userData.set(string key, string value)</li>
  <li>Countly.userData.setOnce(string key, string value)</li>
  <li>Countly.userData.increment(string key)</li>
  <li>Countly.userData.incrementBy(string key, double value)</li>
  <li>Countly.userData.multiply(string key, double value)</li>
  <li>Countly.userData.max(string key, double value)</li>
  <li>Countly.userData.min(string key, double value)</li>
  <li>Countly.userData.push(string key, string value)</li>
  <li>Countly.userData.pushUnique(string key, string value)</li>
  <li>Countly.userData.pull(string key, string value)</li>
  <li>Countly.userData.save() //send data to server</li>
</ul>
<p>
  <strong>Note</strong>:&nbsp;<span style="font-weight: 400;">when reporting to the server, assure the push, pushUnique, and pull parameters can provide multiple values for the same property as an array.</span>
</p>
<p>
  Here is
  <a href="https://api.count.ly/reference#section-modifying-custom-user-data" target="_self">more information</a>
  on how to report this data to the server.
</p>
<h2>Consents</h2>
<p>
  <span style="font-weight: 400;">In case where the <code>consentRequired</code>flag is set upon initial config, remote config actions should only be executed if the "remote-config" consent is given. Additionally, if <code>sessions</code>&nbsp;consent is given, the remote config requests will have <code>metrics</code>&nbsp;</span><span style="font-weight: 400;">info, similar to begin session requests.</span>
</p>
<h2>Device ID Change</h2>
<p>
  <span style="font-weight: 400;">After a device ID change, the locally stored remote config should be cleaned, and an automatic fetch should be performed if enabled upon initial config.</span>
</p>
<h2>Salt</h2>
<p>
  <span style="font-weight: 400;">Remote config requests need to include the checksum if enabled upon initial config. As with all other requests, only the query string part will be used to calculate hash.</span>
</p>
<h1>Application Performance Monitoring</h1>
<p>
  Countly server supports multiple metrics for performance monitoring. They are
  divided into 3 groups:
</p>
<ul>
  <li>Custom traces</li>
  <li>Network request traces</li>
  <li>Device traces</li>
</ul>
<h2>Trace / Metric keys</h2>
<p>
  In some of the exposed functionality, developers can provide the metric key for
  identifying the tracked thing. There are some requirements that the key must
  meet. Those requirements will be enforced on the API endpoint, and if the key
  will be deemed invalid, the trace will be dropped. Therefore it's important to
  catch invalid keys and warn about them on the SDK side.
</p>
<p>Metric keys have a maximum length of 32 characters.&nbsp;</p>
<p>Trace keys have a maximum length of 2048 characters.</p>
<p>
  Metric names can't start with "$" and they can't have "." in them. Trace names
  can't start with "$". Those values should still be accepted. But the SDK should
  print a warning that the server will strip those characters.
</p>
<h2>API Calls</h2>
<p>
  Currently, there is no batching functionality for APM requests. Every APM data
  point/trace should be put in the request queue immediately after it is acquired.
  So that would be after a network request is finished, after a custom trace has
  ended, every time the device goes to the background or foreground, etc.
</p>
<p>
  APM data is combined into a single JSON object which is set to the "apm" param.
  So a basic request would look similar to:
</p>
<pre>/i<span style="font-weight: 400;">?app_key=app_key<br>  &amp;device_id=device_id<br>  &amp;dow=dow<br>  &amp;hour=hour<br>  &amp;timestamp=timestamp<br>  &amp;apm={ _apm_params }</span></pre>
<h2>Custom traces</h2>
<p>
  These are used as a tool to measure the performance of some running task. At
  the basic level, this function is similar to timed events. The default metric
  that gets tracked is the "duration" of the event.&nbsp; There should be a "startTrace"
  and "endTrace" call, which start and end the tracking. When ending the tracking,
  the developer has the option of providing additional metrics. Those metrics are
  String and Integer/Numeric pairs.
</p>
<p>&nbsp;Sample custom trace API request:</p>
<pre><span style="font-weight: 400;">/i?app_key=xyz<br>  &amp;device_id=pts911<br>  &amp;apm={"type":"device",<br>        "name":"forLoopProfiling_1",<br>        "apm_metrics":{"duration": 10, “memory”: 200}, <br>        "stz": 1584698900000, <br>        "etz": 1584699900000}<br>  &amp;timestamp=15847000900000</span></pre>
<h2>Network traces</h2>
<p>Sample network trace request:</p>
<pre><span style="font-weight: 400;">/i?app_key=xyz<br>  &amp;device_id=pts911<br>  &amp;apm={"type":"network",<br>        "name":"/count.ly/about",<br>        "apm_metrics":{"response_time":1330,"response_payload_size":120, "response_code": 300, "request_payload_size": 70}, <br>        "stz": 1584698900000, <br>        "etz": 1584699900000}<br>  &amp;timestamp=1584698900000</span></pre>
<h2>Device traces</h2>
<p>Sample device trace request:</p>
<pre><span style="font-weight: 400;">/i?app_key=xyz<br>  &amp;device_id=pts911<br>  &amp;apm={"type":"device",<br>        "name":"</span><span style="font-weight: 400;">app_start</span><span style="font-weight: 400;">",<br>        "apm_metrics":{"duration": 15000}, <br>        "stz": 1584698900, <br>        "etz": 1584699900}<br>  &amp;timestamp=1584698900</span></pre>
<p>&nbsp;</p>
<h1>User consent</h1>
<p>
  <span style="font-weight: 400;">GDPR compatibility is about dividing the SDK functionality into different features and allowing SDK integrators to ask for consent when using these features. Once consent has been given, only then may the SDK send newly collected (after consent is given) data to the server.</span>
</p>
<p>
  <span style="font-weight: 400;">Additionally, the user may change his/her mind during the app run and opt-out of some features. Therefore, the SDK should be able to enable or disable these features on run time.</span>
</p>
<p>
  <span style="font-weight: 400;">Consent persistence is handled by the host app and not by the SDK. In exceptional circumstances (in cases it is needed) it is possible to handle some consent values persistently inside of the SDK.</span>
</p>
<p>
  <span style="font-weight: 400;">Consent management in the SDK is done in 2 steps<br></span><span style="font-weight: 400;"></span>
</p>
<ol>
  <li>
    <span style="font-weight: 400;">consent has to first be required in the app otherwise the SDK works as if all consent is given</span>
  </li>
  <li>
    <span style="font-weight: 400;">if consent is required, it has to explicitly be given for each targeted feature</span>
  </li>
</ol>
<h2>Initial Configuration</h2>
<p>
  During SDK init there should be a flag (e.g. <code>requiresConsent</code>) to
  inform the SDK that it requires consent before doing anything.
</p>
<p>
  <span style="font-weight: 400;">If this configuration is set, the SDK should not send any data to the server without consent. Even if specific SDK methods (reporting errors, recording events, etc.) are manually called, these calls should be ignored until consent is given.</span>
</p>
<p>
  <span style="font-weight: 400;">Init should also have a function to provide an array consent that is given during startup.</span>
</p>
<h2>Exposing Available Features for Consent</h2>
<p>
  <span style="font-weight: 400;">The SDK should expose all the features it supports for consent in the form of a method, static properties, or constant strings. The developer may check which features are available during development or when creating a consent form UI.&nbsp;</span>
</p>
<p>
  Developers shouldn't have to write the consent feature strings themself. They
  should be provided either as constants or even as enums thereby eliminating the
  need for strings.
</p>
<p>
  <span style="font-weight: 400;">The following are the currently available features: </span>
</p>
<ul>
  <li>
    <code>sessions</code> -
    <span style="font-weight: 400;">tracking when, how often, and how long users use your app/website</span>
  </li>
  <li>
    <code>events</code> -
    <span style="font-weight: 400;">allow events to be sent to the server (doesn't apply to other features using event mechanisms)</span>
  </li>
  <li>
    <code>location</code> -&nbsp;<span style="font-weight: 400;">allows location information to be sent. If consent has not been given, the SDK should force send an empty location upon <code>begin_session</code></span><span style="font-weight: 400;">to prevent the server from determining location via IP addresses</span>
  </li>
  <li>
    <code>views</code> -
    <span style="font-weight: 400;">allow tracking of which views/pages a user visits</span>
  </li>
  <li>
    <code>scrolls</code> -
    <span style="font-weight: 400;">allow user scrolls for scroll heatmap to be tracked</span>
  </li>
  <li>
    <code>clicks</code> -
    <span style="font-weight: 400;">allow user clicks for heatmaps as well as link clicks to be tracked</span>
  </li>
  <li>
    <code>forms</code> -
    <span style="font-weight: 400;">allow user's form submissions to be tracked</span>
  </li>
  <li>
    <code>crashes</code> -
    <span style="font-weight: 400;">allow crashes, exceptions, and errors to be tracked</span>
  </li>
  <li>
    <code>attribution</code> -
    <span style="font-weight: 400;">allows the campaign from which a user came to be tracked</span>
  </li>
  <li>
    <code>users</code> -
    <span style="font-weight: 400;">allow collecting/providing user information, including custom properties</span>
  </li>
  <li>
    <code>push</code> - allows push notifications
  </li>
  <li>
    <code>star-rating</code> -
    <span style="font-weight: 400;">allows their rating and feedback to be sent</span>
  </li>
  <li>
    <code>accessory-devices</code> -
    <span style="font-weight: 400;">allow accessories or wearable devices, such as Apple Watches, etc. to be detected</span>
  </li>
  <li>
    <code>apm</code> -
    <span style="font-weight: 400;">allows usage of application performance monitoring features</span>
  </li>
  <li>
    <code>remote-config</code> -
    <span style="font-weight: 400;">allows downloading of remote configs from the server</span>
  </li>
  <li>
    <span style="font-weight: 400;"><code>feedback</code>- allows showing things like surveys and NPS</span>
  </li>
</ul>
<p>
  <span style="font-weight: 400;">Note that the available features may change depending on the platform.</span>
</p>
<h2>Feature Grouping (optional)</h2>
<p>
  <span style="font-weight: 400;">The SDK may also provide features grouping, allowing existing features to be put into groups and the use of these groups to give, cancel, and check consent.</span>
</p>
<p>
  <span style="font-weight: 400;">For example, a client may put "sessions","events", and "views" into one group called "activity". After which, they give their consent to "activity", the SDK should then automatically give consent to all underlying features.</span>
</p>
<pre><code class="javascript">Countly.group_features({
    activity:["sessions","events","views"],
    interaction:["scrolls","clicks","forms"]
});</code></pre>
<h2>Giving Consent</h2>
<p>
  <span style="font-weight: 400;">The SDK initial consent should be sent through the config object.</span>
</p>
<p>
  <span style="font-weight: 400;">After init there </span><span style="font-weight: 400;">should be a method for giving consent. This method should have feature names or groups as parameters. It may accept a single feature or group as well as multiple features or groups in the form of an array or variable arguments, depending on the SDK language and environment.</span>
</p>
<p>
  <span style="font-weight: 400;">At any time during app run, a user may give consent to more features after starting the SDK.</span>
</p>
<p>
  Upon receiving consent (also during init), the SDK should immediately begin collecting
  data allowed by the provided feature(s) and also begin sending the consent approval
  to the server in the form of <code>consent=&nbsp;{"feature":true}</code>. For
  the exact feature names, refer to the list above. For example, if features are
  <code>crashes</code> and <code>users</code>, then the request should contain
  <code>consent&nbsp;=&nbsp;{"crashes":true,"users":true}</code>. This may be a
  separate request, or it may be attached to any other SDK request.
</p>
<p>
  <span style="font-weight: 400;">If someone attempts to give consent for a second time, the SDK should ignore it as the consent is already given and nothing changes.</span>
</p>
<h2>Checking Consent Status</h2>
<p>
  <span style="font-weight: 400;">There should also be a method to check the current consent status for the SDK, returning true if consent was given, and false if not. Checking status for groups should return <code>true</code>&nbsp;</span><span style="font-weight: 400;">only if all the underlying features return true.</span>
</p>
<p>
  <span style="font-weight: 400;">This check should also return <code>true</code> if consent is not required.</span>
</p>
<h2>Removing Consent</h2>
<p>
  <span style="font-weight: 400;">The SDK also needs to provide a method to remove consents. It should support the same parameter options as the consent giving method.</span>
</p>
<p>
  <span style="font-weight: 400;">Upon receiving the request to remove consent, the SDK should immediately stop collecting data allowed by the provided feature(s) and also send consent removal to the server in the form of <code>consent=&nbsp;{"feature":false}</code></span>
  <span style="font-weight: 400;">. For example, if the features are crashes and users, then the request should contain <code>consent={"crashes":false,"users":false}</code>.</span>
</p>
<p>
  <span style="font-weight: 400;">This may be a separate request, or it may be attached to any other request.</span>
</p>
<p>
  <span style="font-weight: 400;">Depending on the SDK structure, the SDK may sync existing requests in the queue. Or, it may ignore requests in the queue and never send them or remove them from the queue.</span>
</p>
<p>
  <strong><span style="font-weight: 400;">Both giving consent and removing consent may be combined in a single request as well. If, for example, consent was given for crashes but removed from users, then the request should contain&nbsp;</span>consent={"crashes":true,"users":false}</strong>.
</p>
<h2>Common Flow with Required Consent</h2>
<p>
  1) The Developer sets <code>requiresConsent</code> upon initial configuration:
  <code>config.requiresConsent = true;</code>.
</p>
<p>
  2) The Developer starts the Countly SDK, but the Countly SDK does nothing related
  to user tracking, no information is queued or sent to the server.
</p>
<p>
  3) The Developer handles permissions, such as showing the popup to the user and
  asking for consent as well as persistently storing user choices.
</p>
<p>
  4) Upon receiving consent from a user or storage, the Developer calls the
  <code>giveConsent</code> method of the Countly SDK, feature names, or groups,
  depending on the permissions they managed to get.
</p>
<p>
  5) The Countly SDK starts relevant features and also sends a request to the Countly
  Server (<code>consent={"feature":true}</code>).
</p>
<p>
  6)&nbsp;<span style="font-weight: 400;">The Countly SDK checks if <code>FeatureName</code></span><span style="font-weight: 400;">has already been passed to&nbsp;the <code>giveConsent</code></span><span style="font-weight: 400;">&nbsp;method, and it ignores all repetitive calls.</span>
</p>
<p>
  7)&nbsp;<span style="font-weight: 400;">The Countly SDK does not persistently store the status of given consents and expects the developer to call the&nbsp;</span><span style="font-weight: 400;">giveConsent</span><span style="font-weight: 400;">&nbsp;method on each app launch, just as with starting the SDK.</span>
</p>
<p>
  8)&nbsp;<span style="font-weight: 400;">If the app user changes his/her mind about consents at a later time, the developer may reflect this to the Countly SDK using the <code>removeConsent</code></span><span style="font-weight: 400;">method, passing feature names or groups.</span>
</p>
<p>
  9)&nbsp;<span style="font-weight: 400;">The Countly SDK stops the relevant features and also sends a request to the Countly Server (<code>consent={"feature":false}</code></span><span style="font-weight: 400;">).</span>
</p>
<p>
  10)&nbsp;<span style="font-weight: 400;">The Countly SDK checks if feature names or groups have already been passed to the <code>removeConsent</code></span><span style="font-weight: 400;">&nbsp;method, and it ignores all repetitive calls. Or, it attempts to cancel consents never given at all.</span>
</p>
<h1>Security and privacy</h1>
<h2>Parameter tampering</h2>
<p>
  <span style="font-weight: 400;">This is one of the preventive measures of Countly. If someone in the middle intercepts the request, it would be possible to change the data in the request and make another request with other data to the server or simply make random requests to the server through the retrieved <code>app_key</code></span><span style="font-weight: 400;">.</span>
</p>
<p>
  <span style="font-weight: 400;">To prevent this from happening, the SDK should provide the option to send a checksum alongside the request data. To do so, it should be possible for the developer to provide some random string as SALT to the SDK as parameters or configuration options.</span>
</p>
<p>
  <span style="font-weight: 400;">If this SALT is provided, right before making the request, the SDK should take all the payload it is about to send (all the data after the ‘?’ symbol in GET requests, including the app_key and device_id or query string encoded body of POST requests) and make a sha256 hash of this data. You should also provide SALT, and append it as checksum256={hash}.</span>
</p>
<pre><code class="javascript">if(salt){
  data += "&amp;checksum256=" + sha256Hash(data + salt);
}</code></pre>
<p>
  <span style="font-weight: 400;">If SALT is not provided, the SDK should make ordinary requests without any checksums.</span>
</p>
<h1>Other features</h1>
<h2>Attribution (WIP)</h2>
<p>
  Attribution allows attributing installs from specific campaigns. They are tied
  together with sessions. Attribution information should be sent in the following
  situations, depending on which comes first:
</p>
<ol>
  <li>With the first begin session call</li>
  <li>
    as soon as the information is available in a separate request (this is relevant
    when there is no session consent)
  </li>
</ol>
<h2>SDK internal limits</h2>
<p>The SDK should have the following limits:</p>
<ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
  <li data-stringify-indent="0">
    "<strong data-stringify-type="bold">maxKeyLength</strong>" - 128 chars
  </li>
</ul>
<p>
  <span>Limits the maximum size of all string keys.</span><br>
  <span>"Keys" include:</span><br>
  <span>&nbsp;- event names</span><br>
  <span>&nbsp;- view names</span><br>
  <span>&nbsp;- custom trace key name (APM)</span><br>
  <span>&nbsp;- custom metric key (apm)</span><br>
  <span>&nbsp;- segmentation key (for all features)</span><br>
  <span>&nbsp;- custom user property</span><br>
  <span>&nbsp;- custom user property keys that are used for property modifiers (mul, push, pull, set, increment, etc)</span><br>
</p>
<ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
  <li data-stringify-indent="0">
    "<strong data-stringify-type="bold">maxValueSize</strong>" - 256 chars
  </li>
</ul>
<p>
  <span>Limits the size of all values in our key-value pairs.</span><br>
  <span>"Value" fields include:</span><br>
  <span>&nbsp;- segmentation value in case of strings (for all features)</span><br>
  <span>&nbsp;- custom user property string value</span><br>
  <span>&nbsp;- user profile named key (username, email, etc) string values. Except "picture" field, that has a limit of 4096 chars</span><br>
  <span>&nbsp;- custom user property modifier string values. For example, for modifiers like "push", "pull", "setOnce", etc.</span><br>
  <span>&nbsp;- breadcrumb text</span><br>
  <span>&nbsp;- manual feedback widget reporting fields (reported as event)</span><br>
  <span>&nbsp;- rating widget response (reported as event)<br></span>
</p>
<ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
  <li data-stringify-indent="0">
    "<strong data-stringify-type="bold">maxSegmentationValues</strong>" - 30
    dev entries
  </li>
</ul>
<p>
  <span>Max amount of custom (dev provided) segmentation in one event</span>
</p>
<ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
  <li data-stringify-indent="0">
    "<strong data-stringify-type="bold">maxBreadcrumbCount</strong>" - 100 entries
  </li>
</ul>
<p>
  <span>Maximum amount of breadcrumbs that can be recorded before the oldest one is deleted</span>
</p>
<ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
  <li data-stringify-indent="0">
    "<strong data-stringify-type="bold">maxStackTraceLinesPerThread</strong>"
    - default value of 30
  </li>
</ul>
<p>
  <span>limits how many stack trace lines would be recorded per thread</span>
</p>
<ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
  <li data-stringify-indent="0">
    "<strong data-stringify-type="bold">maxStackTraceLineLength</strong>" - default
    value of 200
  </li>
</ul>
<p>
  <span>limits how many characters are allowed per stack trace line. This limits also the crash message length</span>
</p>
<p>&nbsp;</p>
<p>
  <span>In addition to those 2 exposed tweakable crash related values, there would also be an internal one for "maxStackTraceThreadCount". Which would limit the maximum amount of recorded threads with a default of 30. This would be mostly just a sanity check thing as that has to be capped in some way.<span class="c-mrkdwn__br" data-stringify-type="paragraph-break"></span>In cases where stack traces can be provided as string, the maximum line count would therefore be 30*30 = 900. That string would have to be split into lines and then checked accordingly.</span>
</p>
<p>&nbsp;</p>
<p>
  Crash information like PLC crashes for iOS and native Android crashes do not
  have any limits applied to them.
</p>