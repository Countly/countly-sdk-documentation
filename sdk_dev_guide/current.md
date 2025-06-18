<p>
  <span>Would you like to develop a new SDK for Countly? Then this guide is for you. Before starting, bear in mind that there are a lot of SDKs that Countly has already developed. Please check whether the SDK you are going to develop is not already available.</span>
</p>
<h1 id="01H821RTQ1G58MJXF4JFX5HVF5">
  <span>Integration</span>
</h1>
<h2 id="01H821RTQ15HRMMKHQY49NFYV8">Initialization</h2>
<p>
  <span>To start making requests to the server, SDK needs 3 things: the URL of the server where you will be making requests, the app_key of the app for which you will be reporting, and your current device_id to uniquely identify this device.</span>
</p>
<p>
  <strong>Server URL</strong> -&nbsp;<span>The SDK needs to provide the ability for the user to specify the URL for the server where their Countly instance is installed. This be used for all requests.</span>
</p>
<p>
  <strong>App Key</strong> -&nbsp;<span>The App key should be provided by the SDK user. This value identifies to which dashboard applications this request is going to be tied to. Your app should be created on the Countly server. After app creation, the server will provide an app key for the user. The same app key is used for the same app on different platforms.</span>
</p>
<p>
  <strong>Device ID</strong> -
  <span>A device ID is required to uniquely identify a device or user. If you have some unique user ID which you can retrieve, you may use it. If not, you may provide platform-specific device identification (as Advertising identifier in Google Play Services on Android) or use existing implementations (as OpenUDID). More info about device ID is described <a href="#h_01GYC4S9JM2F2WDDFSBEF2TBJ0" target="_self">here</a>.</span>
</p>
<h2 id="01H821RTQ1NM9W4N116BKF3FAW">Init Configuration</h2>
<p>
  The SDK should take a config (short for configuration) object during initialization.
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
  during init those are not provided, an exception can be thrown to indicate that.
</p>
<p>
  For more information of what values can be sent to the server, look
  <a href="https://api.count.ly/reference/i#additional-parameters">here</a>.
</p>
<h2 id="01H821RTQ1QTT7ZCDHN207MS9W">Logging / Debug Mode</h2>
<p>
  The SDK should have a logging mode flag. If that is enabled, the SDK should print
  logs to the console.
</p>
<p>
  If this flag is not enabled, no logs should be printed to the console.
</p>
<p>
  This flag functions independently of the log listener (described below).
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
<h3 id="01H822TC8FN7N2AHT7C6TJKR95">Log Messages</h3>
<p>
  <span>No two places should have the same log message. This means that all messages should be unique. Knowing the log message and the sdk version it should be unambiguous to know which line printed that message.</span><br>
  <span>To help with being unambiguous, the log messages could include the internal "module" or "section" name from where it was called. If the function called is part of the public API of the SDK, that log should include the function name.</span>
</p>
<pre><span>[ModuleName] functionName, Some message</span></pre>
<p>
  <span>If there is a message tag/group mechanism on the platform then the tag name "Countly" should be used. If there is no tag/group mechanism available then the name "Countly" should be added to each message.</span>
</p>
<pre><span>[Countly] [ModuleName] functionName, Some message</span></pre>
<p>
  <span>All calls, that can be called by developers, should produce a log message to indicate what is being called.</span><span></span>
</p>
<p>
  <span class="c-mrkdwn__br" data-stringify-type="paragraph-break"></span><span>The goal is to have a good enough log coverage so that it's easy to understand what was happening with the SDK and how it was used when a SDK integrator provides his logs.</span>
</p>
<h3 id="01H821RTQ1T2MJ9CRTCBM50ADE">Log Levels</h3>
<p>When implementing logs, the SDK should follow these levels:</p>
<ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
  <li>
    <strong>Error</strong> - this is an issue that needs attention right now.
    E.g.:
    <ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
      <li>try-catch block errors</li>
      <li>missing `url` or `app_key`</li>
    </ul>
  </li>
  <li>
    <strong>Warning</strong> - this is something that is potentially an issue.
    E.g.:
    <ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
      <li>deprecated methods</li>
      <li>wrong parameters provided</li>
      <li>SDK is not initialized yet</li>
    </ul>
  </li>
  <li>
    <strong>Info</strong> - informs about the usual working of the SDK. E.g.:
    <ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
      <li>public method calls</li>
      <li>provided init config options</li>
      <li>initializations of modules</li>
    </ul>
  </li>
  <li>
    <strong>Debug</strong> - this should contain logs from the internal workings
    of the SDK. E.g.:
    <ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
      <li>request success response</li>
      <li>failed request</li>
      <li>unique inner function checks</li>
    </ul>
  </li>
  <li>
    <strong>Verbose</strong> - this should give an even deeper look into the
    SDK's inner working (noisy). E.g.:
    <ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
      <li>No consent given</li>
    </ul>
  </li>
</ul>
<p>
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
<pre><span>E: [Error] [Countly] [ModuleName] functionName, Countly issue bla bla<br>E: [Warning] [Countly] [ModuleName] functionName, You are trying to use this feature in a deprecated way</span></pre>
<p>
  Depending on the function call, the function parameters should also be printed,
  and they should be enclosed in closed brackets. For example event keys or for
  simple numerical values.
</p>
<pre><span>I: [Info] [Countly] [ModuleEvent] recordEvent, event is being recorded key: [Login], count: [2], segmentation: [{"isLoggedIn":true, "name":"Something"}]</span></pre>
<p>
  For functions which receive a callback, a bool is enough to indicate if a callback
  was or wasn't provided.
</p>
<h3 id="01H821RTQ1ZGEREGB01N0H966G">Log Listener</h3>
<p>
  In some cases there might be situations where an integrated SDK is not behaving
  as expected in a release build which is used by clients. In those cases it would
  be valuable to see the inner workings of the SDK but it's not possible to access
  SDK logs. It wouldn't also be recommendable to print those logs is a published
  setting as they might leak private info to other apps on the same device.
</p>
<p>
  For this reason exists the log listener feature. During init the developer can
  setup a log listener. For example, it could be a callback. If such a listener
  is set, logs should be printed to it. For every log that is provided, there should
  be 2 values. First the string of the message that would be printed and then the
  log level of that message so that it can be used as an indication of the message
  importance.
</p>
<h2 id="01H821RTQ1C5CTQK92KYAD4GBH">Countly Code Generator</h2>
<p>
  If you would like to understand how SDKs work by generating mobile or web code
  for events, user profiles, crash reporting, and all other features that come
  with Countly in general, we suggest you use the
  <a href="https://countly.github.io/countly-code-generator/">Countly Code Generator</a>,
  which is a point and click service that builds the necessary code for you.
</p>
<h1 id="01H821RTQ18DVPGH41Y03VD7G4">SDK Storage and Requests</h1>
<h2 id="01H821RTQ1ZMTGHAF6MHDX41MD">Making Requests</h2>
<p>
  <span>The Countly server is a simple HTTP-based REST API server, and all SDK requests should be made to </span><strong>/i</strong><span>&nbsp;endpoint with two required parameters:&nbsp;</span><strong>app_key</strong><span>&nbsp;and&nbsp;</span><strong>device_id</strong><span>.</span>
</p>
<p>
  <span>Other optional parameters need to be provided based on what this request should do. You may checklist all the parameters that the Countly Server can accept in&nbsp;</span><a href="https://api.count.ly/reference/i"><span>/i endpoint Server API reference</span></a><span>.</span>
</p>
<p>
  <span>There are some parameters that should be added to all requests, even though they are not mandatory. Together with the required parameters, they form the base request. Every request sent to the server should be formed from this base request. The parameters in this base request are: </span>
</p>
<ul>
  <li>
    <span>"app_key" - the application key for this countly app (retrievable on the dashboard)</span>
  </li>
  <li>
    <span>"device_id" - the current user's device ID</span>
  </li>
  <li>
    <span>"timestamp" - the timestamp in ms of when this request is created</span>
  </li>
  <li>
    <span>"hour" - the hour of the timestamp</span>
  </li>
  <li>
    <span>"dow" - the day of the week for this timestamp. 0 - sunday, ... , 6 - saturday.</span>
  </li>
  <li>
    <span>"tz" - this device's timezone offset</span>
  </li>
  <li>
    <span>"sdk_version" - the SDK's version</span>
  </li>
  <li>
    <span>"sdk_name" - the SDK's name</span>
  </li>
</ul>
<p>
  <span>In cases where some devices may be offline, etc., and requests should be queued, it is highly recommended you add a timestamp to each request, displaying when it was created.</span>
</p>
<div class="callout callout--info">
  <h3 id="01H821RTQ1M9DQRPT8FJ9TTBFK" class="callout__title">Encoding URI Components</h3>
  <p>
    <span>Due to the possible use of the ‘&amp;’ and ‘?’ symbols in encoded JSON strings, SDKs should encode uri components before adding them to the request and sending it to the server.</span>
  </p>
</div>
<h3 id="01H821RTQ1D25TAE687RNRS3NR">Using GET or POST</h3>
<p>
  <span>By default, the preferred method is to make GET requests for the Countly servers. However, there may be some length limitations for GET requests based on specific platform or server settings. Thus, the best practice is to make a POST request when the data reaches over 2,000 characters for a single request.</span>
</p>
<p>
  <span>Before making each request, you will need to check if the data you are going to send is less than 2,000 characters. If so, use GET. If you have more characters, use POST.</span>
</p>
<p>
  <span>Additionally, the SDK should be able to switch to post completely if a user should so specify in the SDK configuration/settings.</span>
</p>
<p>
  <span>When making POST requests, the used content type should be "application/x-www-form-urlencoded".</span>
</p>
<h3 id="01H821RTQ1KQ1PR0XHNZXCWCYD">SDK Metadata</h3>
<p>
  <span>The SDK should send the following metadata with every request.</span>
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
  start at "0". Major version numbers (year, month) should stay the same even if
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
<h2 id="01H821RTQ2YX94108QAANP2R8J">Storage</h2>
<p>
  <span>Some things in the SDK are stored persistently, for example, request queue, event queue etc. Those should be stored in the device storage.</span>
</p>
<p>
  <span>If possible, those persistent values should be segmented by the appKey. That means that for every appKey there should be different storage for their queues.</span><span></span>
</p>
<h2 id="01H821RTQ2YD4C2V3AD4RKRJXA">Request Queue</h2>
<p>
  <span>In some cases, users might be offline, thus they are not able to make requests to the server. In other cases, the server may be down or in maintenance, thus unable to accept requests. In both cases, the SDK should handle queuing and persistently storing requests made to the Countly server and should wait for a successful response from the server before removing a request from the queue.</span>
</p>
<p>
  <span>Note that requests should be made in historical order, meaning you must also preserve the order of your queue.</span>
</p>
<p>
  <span>Simple flow on how requests should appear as follows:</span>
</p>
<ol>
  <li>
    <span>Initiating request - either a new event reported or session call, etc.</span>
  </li>
  <li>
    <span>Creating a payload - take all the parameters (including the current timestamp) and the values needed for a request and generate a payload which will be included in the HTTP request</span>
  </li>
  <li>
    <span>This payload is inserted into the queue (First In, First Out)</span>
  </li>
  <li>
    <span>All updates to the queue should be persistently stored. Based on the environment, you may directly use storage for the queue</span>
  </li>
  <li>
    <span>On some other thread there should be a request processor which takes the first request in the queue, applies the checksum if needed, determines the request type (GET or POST) based on the length, and makes the HTTP request</span>&nbsp;<br>
    <ul>
      <li>
        <span>if the request is successful (defined below), then it should be removed from the queue and the next request will be processed upon the next iteration</span>
      </li>
      <li>
        <span>if the request failed, the request processor should have a cool-down period, lasting a minute or so (configurable value), and it will then try the same request again until it is completed</span>
      </li>
    </ul>
  </li>
</ol>
<div class="img-container">
  <img src="https://count.ly/images/guide/PPNhED7RiGZC0StuDYBd_SDK%20queue%20flow.png">
</div>
<p>
  <span>There are multiple scenarios why a request might fail, so to ensure that the request is successfully delivered to the server SDK, you will need to assure the following has taken place:</span>
</p>
<ol>
  <li>
    <span>The HTTP response code was successful (which is any 2xx code or code between 200 &lt;= x &lt; 300)</span>
  </li>
  <li>
    <span>The returned request is a JSON object</span>
  </li>
  <li>
    <span>That JSON object contains the field "result" (there can be other fields)</span>
  </li>
</ol>
<p>
  <span>When sending request to a Countly server, it would respond with a JSON object, which should have a property named "result". Usually that value will be "Success". There may be scenarios where a different "result" value is returned or where additional fields may be added.</span>
</p>
<p>
  <span>If the previously described things are "true", </span>then it means the
  request was successfully delivered to the server and can be removed from the
  queue.
</p>
<h3 id="01H821RTQ2CA0ARFHWBSS89BZH">Queue Size Limit</h3>
<p>
  <span>We need to limit the queue size so that it doesn’t overflow, and so that syncing up won’t take too long if some specific server is down for too long. This limit would be in the number of stored queries, and this limit should be available for the end-user to change as the SDK settings.</span>
</p>
<p>
  <span>In case this limit is reached, the SDK should remove older queries and insert new ones. The default limit may change from what the SDK needs, but the suggested limit is&nbsp;</span><strong>1,000 queries</strong><span>.</span>
</p>
<h2 id="01H821RTQ2GJ97A0QH0FE86ZBM">Event Queue</h2>
<p>
  Similary to the request queue, each SDK should also have the event queue. It
  is used for the purposes of combining multiple events together and decreasing
  the total request amount.
</p>
<p>This queue is also FIFO, and has a maximum size.</p>
<h2 id="01H821RTQ20F1BWE1KPCXYJZ5A">Other Storage</h2>
<p>
  Some other features might also require storage to store some things persistently
  (remote config, etc).
</p>
<p>Those would have their own storage format.</p>
<h2 id="01H821RTQ28RTWMDKM06XPTM50">Recording Time of Data</h2>
<p>
  <span>To properly report and process data (especially queued data), you should also provide the time when the data was recorded. You will need to provide 3 parameters with each request:</span>
</p>
<ul>
  <li>
    <strong>timestamp</strong>:
    <span>13-digit UTC millisecond unique timestamp of the moment of action</span>
  </li>
  <li>
    <strong>hour</strong>: <span>Current user local hour (0 - 23)</span>
  </li>
  <li>
    <strong>dow</strong>:&nbsp;<span>Current user day of the week (0-Sunday, 1 - Monday, ... 6 - Saturday)</span>
  </li>
  <li>
    <strong>tz</strong>:
    <span>Current user time zone in minutes (120 for UTC+02, -300 for UTC-05)</span>
  </li>
</ul>
<p>
  <span>As multiple events may be combined in a single request, you should also provide these parameters automatically in every event object.</span>
</p>
<p>
  <span>The suggested millisecond timestamp should be unique, meaning if events were reported in the same timestamp, the SDK should update the millisecond timestamp in the order in which the events were reported. The pseudo-code to the unique millisecond timestamp could appear as follows:</span>
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
  <span>If it’s impossible to use a millisecond timestamp on a specific platform, you may also use a 10-digit UTC seconds timestamp.</span>
</p>
<h1 id="01H821RTQ2JRCPX43EYJ7PABWB">General SDK Structure Overview</h1>
<p>
  <span>Depending on the SDK’s environment/language, a different set of features could be supported. Some of these features may be supported on any platform, whereas others are quite platform-specific. For example, a desktop app may not provide telecom operator information.</span>
</p>
<p>
  <span>Note that function and argument namings are only examples of what it could be. Try to follow your platform/environment/language best practices when creating and naming functions and variables.</span>
</p>
<p>
  <span>Core features are the minimal set of features that the SDK should support, and these features are platform-independent.</span>
</p>
<h2 id="01H821RTQ2D8GVP71K49AQ5KB3">Initialization</h2>
<p>
  <span>In its official SDKs, Countly is used as a singleton object or basically an object with a shared instance. Still, there are some parameters that need to be provided before the SDK can work. Usually, there is an "init" method that accepts the URL, app key, and device_id (or the SDK generates it itself if it’s not provided):</span>
</p>
<pre><code class="java">Countly.init(string url="https://try.count.ly", string app_key, string device_id, ...)
</code></pre>
<h1 id="01H821RTQ20M61EKN76EY6RJ84">Crash Reporting</h1>
<p>
  <span>On some platforms, the automatic detection of errors and crashes is possible. In this case, your SDK may report them to the Countly server, and this is also optional as with other similar functions. If a crash report is not sent, it won't be displayed on the dashboard under the Crashes section. Here is more information on </span><a href="https://api.count.ly/reference/i#crash-analytics" target="_self">Crash reporting parameters</a><span>&nbsp;that you may use in your SDK.</span>
</p>
<p>
  <span>In regard to crashes, all information, except the app version and OS, is optional, but you should collect as much information about the device as possible to assure each crash may be more identifiable with additional data. You should also provide a way for users to log errors manually (for example, logging handled exceptions which are not fatal).</span>
</p>
<p>
  <span>Basically, for automatically captured errors, you should set the&nbsp;</span><strong>_nonfatal</strong><span>&nbsp;property to false, whereas on user logged errors the&nbsp;</span><strong>_nonfatal</strong><span>&nbsp;property should be true. You should also provide a way to set custom key/values to be reported as segments with crash reports, either by providing global default segments or setting separately for automatically tracked errors and user logged errors.</span>
</p>
<p>
  <span>Additionally, there should be a way for the SDK user to leave breadcrumbs that would be submitted together with the crash reports. In order to collect breadcrumbs as logs, create an empty array upon initialization and provide a method to add breadcrumbs as strings into that array as elements for log. Also, in the event of a crash, concatenate the array with new line symbols and submit under the&nbsp;</span><strong>_logs</strong><span>&nbsp;property. There is no need to persistently save those logs on a device, as we would like to have a clean log on every app start.</span>
</p>
<p>
  <span>The end API could look like this (but it should be totally based on the specific platform error handling):</span>
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
<h2 id="h_01HVK6Q069F0FMF81J1TEDGBJB">Crash Filtering</h2>
<p>
  There should be a way to filter and edit the crash report before sending it to
  the server. To do this, a callback should be registered while initializing the
  SDK.
</p>
<pre><code class="java">config.crashes.setCrashFilterCallback(callback);
Countly.sharedInstance().init(config);</code></pre>
<p>
  This callback will take a "CrashData" object containing all crash-related data
  and modify or omit it. If "true" is returned from the callback, the crash must
  be omitted.
</p>
<pre><code class="java">interface CrashFilterCallback {
    boolean filterCrash(CrashData crash);
}</code><code class="java"></code></pre>
<p>The crash data object must contain:</p>
<ul>
  <li>Stack trace string that is concatenated with new lines.</li>
  <li>List of breadcrumbs</li>
  <li>Crash metrics</li>
  <li>Crash segmentation</li>
  <li>Crash Name (iOS only)</li>
  <li>Crash Description (iOS only)</li>
  <li>Whether or not a crash is unhandled (fatal)</li>
</ul>
<p>
  While preparing "CrashData", SDK internal limits should be applied to the
  <strong>stack trace</strong>, <strong>crash segmentation</strong>, and
  <strong>breadcrumbs</strong>.
</p>
<p>
  All of those attributes can be modified. "CrashData" must provide setters and
  getters to achieve that.
</p>
<p>
  Setters mustn't accept invalid values like null, undefined, etc.
</p>
<p>
  Also, there must be a way to report which fields have been modified for the server.
</p>
<p>
  A metric for crashes will be calculated as an integer of "_ob" bits. If some
  fields changed while filtering, bits must be set as:
</p>
<ul>
  <li>
    01000000 for description -&gt; "_ob" metric will be 64 (iOS only)
  </li>
  <li>00100000 for name -&gt; "_ob" metric will be 32 (iOS only)</li>
  <li>00010000 for stack trace -&gt; "_ob" metric will be 16</li>
  <li>
    00001000 for crash segmentation -&gt; "_ob" metric will be 8
  </li>
  <li>00000100 for breadcrumbs -&gt; "_ob" metric will be 4</li>
  <li>00000010 for crash metrics -&gt; "_ob" metric will be 2</li>
  <li>00000001 for unhandled -&gt; "_ob" metric will be 1</li>
</ul>
<p>
  For example, if crash segmentation, unhandled, and stack trace is changed, the
  "_ob" metric must be 25.
</p>
<p>
  After the crash filtering is completed, SDK internal limits must be applied to
  the <strong>stack trace</strong>, <strong>crash segmentation</strong>, and
  <strong>breadcrumbs</strong>. Unsupported data types must also be removed from
  crash metrics.
</p>
<p>
  The "_ob" metric calculation must not be affected by SDK internal limit changes.
  It must only indicate whether or not the developer modified that field.
</p>
<p>
  The "_ob" metric must be appended to the crash metrics and sent to the server.
</p>
<h2 id="01H821RTQ27DWNCPTRG2126NA2">Symbolication (WIP)</h2>
<h1 id="01H821RTQ2JN3F965RM2VT8A2G">Events</h1>
<p>
  Events are the basic Countly data reporting tool that conveys something has happened
  in the app. Common examples are: someone clicked a button, performed a specific
  action, etc.
</p>
<p>Events can be grouped under two categories:</p>
<ul>
  <li>Internal Events</li>
  <li>Developer provided Events</li>
</ul>
<p>
  Internal Events has a <strong>[CLY]_</strong> prefix for its
  <strong>key</strong> and used for providing a <strong>specific</strong> kind
  of information (a feature) to the server. For example Views feature is reported
  as an internal Event and will be displayed at a unique section on the server
  (Analytics &gt; Page Views).
</p>
<p>
  Developer provided Events can be about any kind of information (<strong>non specific</strong>).
  So all developer provided Events will have an aggregate display section (Events
  &gt; All Events).&nbsp;
</p>
<p>An Event would have the following properties:</p>
<ul>
  <li>key - Mandatory, non empty string</li>
  <li>count - Mandatory, integer, minimum 1</li>
  <li>sum - Optional value, double, can be negative</li>
  <li>dur - Optional value, double, minimum 0</li>
  <li>segmentation - Optional, object with key-value pairs</li>
</ul>
<p>
  More on Event formatting can be found in the
  <a href="https://api.count.ly/reference/i#events">API Reference</a>.
</p>
<p>Here are some examples:</p>
<p>
  <strong>User logged into the game:</strong>
</p>
<pre>{ key: 'login', count: 1 }</pre>
<p>
  <strong>User completed a level in the game with a score of 500:</strong>
</p>
<pre>{ key: 'level_completed', count: 1, segmentation: { level: 2, score: 500 } }</pre>
<p>
  <strong>User purchased something in the app worth 2.99 on the main screen:</strong>
</p>
<pre>{ key: 'purchase', count: 1, sum: 2.99, dur: 30, segmentation: { screen: 'main' } }</pre>
<p>
  As you can imagine, your SDK should provide methods to cover these combinations,
  either by default values or by function parameter overloading, etc.:
</p>
<ul>
  <li>Countly.events.recordEvent(string key)</li>
  <li>Countly.events.recordEvent(string key, int count)</li>
  <li>Countly.events.recordEvent(string key, double sum)</li>
  <li>Countly.events.recordEvent(string key, double duration)</li>
  <li>
    Countly.events.recordEvent(string key, int count, double sum)
  </li>
  <li>Countly.events.recordEvent(string key, map segmentation)</li>
  <li>
    Countly.events.recordEvent(string key, map segmentation, int count)
  </li>
  <li>
    Countly.events.recordEvent(string key, map segmentation, int count, double
    sum)
  </li>
  <li>
    Countly.events.recordEvent(string key, map segmentation, int count, double
    sum, double duration)
  </li>
</ul>
<p>
  <strong>Note</strong>: <strong>count</strong> value defaults to 1 internally
  if not provided as it is mandatory.
</p>
<h2 id="01H821RTQ2TT1GSM7YTBEN4F21">Internal Events</h2>
<p>
  The call for recording events should support recording Countly internal events.
  If consent is required then the ability to record them should be governed only
  by their respective feature consents. The ability to record internal events is
  in no way influenced by the " event" consent. If consent for some feature is
  given and "recordEvent" is used to record that features internal event, it should
  be recorded even if no "event" consent is given. If for some feature consent
  is not given and "recordEvent" is used to record it's internal event, it should
  not be recorded even if "event" consent is given. If no consent is required,
  they should be recorded as well.
</p>
<p>
  At the current moment there are the following internal events and their respective
  required consent:
</p>
<ul>
  <li>
    <strong>[CLY]_nps</strong> - "feedback" consent
  </li>
  <li>
    <strong>[CLY]_survey</strong> - "feedback" consent
  </li>
  <li>
    <strong>[CLY]_star_rating</strong> - "star_rating" consent
  </li>
  <li>
    <strong>[CLY]_view</strong> - "view" consent
  </li>
  <li>
    <strong>[CLY]_orientation</strong> - "users" consent
  </li>
  <li>
    <strong>[CLY]_push_action</strong> - "push" consent
  </li>
  <li>
    <strong>[CLY]_action</strong> - "clicks" or "scroll" consent
  </li>
</ul>
<p>Example 1:</p>
<ol>
  <li>event consent is given, but 'view' consent is not given</li>
  <li>dev calls "recordEvent('[CLY]_view')</li>
  <li>event is not recorded</li>
</ol>
<p>Example 2:</p>
<ol>
  <li>event consent is given, and 'view' consent is also given</li>
  <li>dev calls "recordEvent('[CLY]_view')</li>
  <li>event is recorded</li>
</ol>
<p>Example 3:</p>
<ol>
  <li>event consent is not given, but 'view' consent is given</li>
  <li>dev calls "recordEvent('[CLY]_view')</li>
  <li>event is recorded</li>
</ol>
<h2 id="01H821RTQ26ND225EPAXZPHS8B">Timed Events</h2>
<p>
  In short, you may report time with the&nbsp;<strong>dur</strong>&nbsp;property
  in an event. It is good practice to allow the user to measure some periods internally
  using the SDK API. For that purpose, the SDK needs to provide the methods below:
</p>
<ul>
  <li>
    <strong>startEvent(string key)</strong>&nbsp;- which will internally save
    the event key and current timestamp in the associative array/map.
  </li>
  <li>
    <strong>endEvent(string key, map segmentation, int count, double sum)</strong>&nbsp;-
    which will take the event starting timestamp by the event key from the map,
    get the current timestamp and calculate the duration of the event. It will
    then fill it up as&nbsp;a <strong>dur</strong>&nbsp;property and report an
    event, just as you would report any regular event.
  </li>
  <li>
    <strong>endEvent(string key)</strong>&nbsp;- which will simply end the event
    with a 1 as the count, 0 as the sum, and nil as the segmentation values.
  </li>
</ul>
<p>
  If possible, the SDK may provide a way to start multiple timed events with the
  same key, such as returning an event instance in the method and then calling
  the end method on that instance.
</p>
<p>
  If not, the following calls should be ignored: 1. events which have already started
  2. events which have attempted to start again 3. events which have already ended
  4. events which have attempted to end. Otherwise, they will provide an informative
  error.
</p>
<h1 id="01H821RTQ2TZF21BH3ZSR8XHNW">Device Metrics</h1>
<p>
  <span>Metrics should only be reported together with the begin_session=1 parameter on every session start. Collect as many metrics as possible or allow some values to be provided by the user upon initialization. Possible metrics are listed in the&nbsp;</span><a href="https://api.count.ly/reference/i#metrics"><span>API Reference</span></a><span>.</span>
</p>
<p>
  <span>One thing that we should agree on is identifying platforms with the same string overall SDKs, so here is the list of how we would suggest identifying platforms for the server through the&nbsp;</span><strong>_os</strong><span>&nbsp;metric.</span>
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
<h1 id="01H821RTQ2PBMNS9Y0ASD9A6E7">Session Flow</h1>
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
<h2 id="01H821RTQ2DTYYJPMQ33PBQ6PG">Automatic Session Tracking</h2>
<p>
  Automatic tracking should be done according to the platforms lifecycle. For apps
  that have a visual component (not command line or server call tracking), sessions
  should be tracked when the app is visible and in the foreground. That would mean
  starting the session when the app comes into foreground and ending the it goes
  to the background.
</p>
<h2 id="01H821RTQ23WZFKH76EXFHN456">Manual Session Tracking (WIP)</h2>
<p>
  <span>Most of the official SDKs implement automatic session handling, meaning SDK users don't need to separately bother with session calls. However, it is good practice to provide a way to disable automatic session handling and allow SDK users to make session calls themselves through methods such as:</span>
</p>
<ul>
  <li>Countly.begin_session()</li>
  <li>Countly.session_duration(int seconds)</li>
  <li>Countly.end_session(int seconds)</li>
</ul>
<p>
  <span>Here is the documentation showing how you may&nbsp;</span><a href="https://api.count.ly/reference/i#session"><span>report sessions through our API</span></a><span>.</span>
</p>
<h2 id="01H821RTQ2EHYPRRZ9H9CPZH7T">Session API</h2>
<p>
  All these session requets are built uppon the base request which includes all
  the base params, therefore those won't be explicitly mentioned.
</p>
<h3 id="01H821RTQ2GGYNVHKPW17BBMW4">Starting a Session</h3>
<p>
  <span>The SDK should then send the </span><strong>begin_session=1</strong><span> param. This same request should also contain metrics parameters with the maximum metrics described on </span><a href="https://api.count.ly/reference/i"><span>/i page</span></a><span>, which may be collected from this SDK-specific environment/language. It might look something like:<br></span>
</p>
<pre><span>"&amp;begin_session=1&amp;metrics={...}"</span></pre>
<h3 id="01H821RTQ37TYR08W9RYQWN3KQ">Session Update</h3>
<p>
  <span>Each minute of the session should be extended by sending the <strong>session_duration</strong> param with the number of seconds that passed since the previous session request (begin_session or session_duration, whichever was last). It might look something like:</span>
</p>
<pre><span>"&amp;session_duration=60"</span></pre>
<h3 id="01H821RTQ3MYH265462NQMHNBT">Ending a Session</h3>
<p>
  <span>The SDK should send the </span><strong>end_session=1</strong><span> param, including the <strong>session_duration</strong> parameter with how many seconds passed since the last session request (begin_session or session_duration, whichever was last). It might look something like this:</span>
</p>
<pre><span>"&amp;end_session=1&amp;session_duration=15"</span></pre>
<h3 id="01H821RTQ3T4K0EMQWE7D4JWEZ">Sample Uses</h3>
<p>
  <span>Here are a few example requests generated by different session lengths:</span>
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
<h2 id="01H821RTQ3ZVV6YVP2FHVE6DKE">Session Cooldown</h2>
<p>
  <span>In some cases, it is difficult to know for sure if a session has ended, such as with web analytics when a user is leaving the page, and whether they will visit another page or not. This is why there is a small&nbsp;</span><em><span>cooldown</span></em><span>&nbsp;time of 15 seconds. If the end_session request is sent and then the begin_session request is sent within 15 seconds, it will be counted as the same session, and the session duration will extend this session instead of applying it to the new one.</span>
</p>
<p>
  <span>This makes it easier to call the end_session on each page unload without worrying about starting a new session if the user visits another page.</span>
</p>
<p>
  <span>If you don't need this behavior, simply pass the&nbsp;</span><strong>ignore_cooldown=true</strong><span>&nbsp;parameter to all the session requests and the server will not extend the session. Rather, it will always count it as a new session.</span>
</p>
<p>
  <span>The 15-second cooldown is a default value and may be configured on the server, so don't rely on it being 15 seconds.</span>
</p>
<h1 id="01H821RTQ3A76M4SDM49BZPAYH">View Tracking</h1>
<p>
  <span>Reporting views would allow you to analyze which views/screens/pages were visited by the app user as well as how long they spent on a specific view. If it is possible to automatically determine when a user visits a specific view in your platform, then you should provide an option to automatically track views. Also, it is important to provide a way to track views manually.&nbsp;</span>
</p>
<h2 id="01H821RTQ3WPFFJBM5CP953JA6">
  <span>View Structure</span>
</h2>
<p>
  <span>View information is packaged into events. There are 2 kinds of events:&nbsp;</span>
</p>
<ul>
  <li>
    <span>an event to indicate that a view was entered</span>
  </li>
  <li>
    an event to send the duration of the view and indicate that the view was
    exited
  </li>
</ul>
<p>
  All view-related events use the event key "[CLY]_view" and are dependent on the
  consent key "views".
</p>
<p>All view events are sent with a "count" of 1.</p>
<p>
  The duration field "dur" is used when reporting view duration. It should contain
  the view duration in seconds.
</p>
<p>There are 5 potential segmentation values:</p>
<ul>
  <li>
    "name" - string value of the view name, for example, "View_1"
  </li>
  <li>
    "segment" - string value of the SDK platform name, for example, "Android"
  </li>
  <li>
    "visit" - if the view was entered, this property should be set with the value
    "1"
  </li>
  <li>
    "start" - if the view was entered and it was the first view of a session
    this property should be set with "1"
  </li>
  <li>
    "_idv" - the unique identifier of this view-session. This should be set to
    the String concatenation of 8 base64 characters created from 6 bytes of randomness
    (ideally crypto safe) and timestamp in ms.
  </li>
</ul>
<p>
  A sample event for reporting the first view would look like this:
</p>
<pre>events=[<br>    {<br>        <span>"key"</span>: <span>"[CLY]_view"</span>,<br>        <span>"count"</span>: <span>1</span>,<br>        <span>"segmentation"</span>: {<br>            <span>"name"</span>: <span>"view1"</span>,<br>            <span>"segment"</span>: <span>"Android"</span>,<br>            <span>"visit"</span>: <span>1</span>,<br>            <span>"start"</span>: <span>1,<br>            "_idv": "f0e8f5db5e5d9e7b9a45d3916b93e43dd091153fdfb6c9a6f"<br></span><span>        </span>}<br>    }<br>]</pre>
<p>
  <span>Sample event for reporting this view's duration:</span>
</p>
<pre>events=[<br>    {<br>        <span>"key"</span>: <span>"[CLY]_view"</span>,<br>        <span>"count"</span>: <span>1</span>,<br>        <span>"dur"</span>: <span>30</span>,<br>        <span>"segmentation"</span>: {<br>            <span>"name"</span>: <span>"view1"</span>,<br>            <span>"segment"</span>: <span>"Android",<br>            "_idv": "f0e8f5db5e17ad5ce5cf53916b93e43dd091153fdfb6c9a6f"<br></span><span>        </span>}<br>    }<br>]</pre>
<p>
  <span>Here is&nbsp;<a href="https://api.count.ly/reference/i#views" target="_self">more information on view-tracking API</a>s.</span>
</p>
<h2 id="01H821RTQ35WBYP7P6KZKQSXJF">
  <span>View Manual Reporting</span>
</h2>
<p>
  <span>The following section will describe a sample implementation of manual views.</span>
</p>
<p>
  <span>First, you will need to have 2 internal private properties as </span><strong>string lastView</strong><span>&nbsp;and&nbsp;</span><strong>int lastViewStartTime</strong><span>. Then, create an internal private method&nbsp;</span><strong>reportViewDuration</strong><span>, which checks if </span><strong>lastView</strong><span>&nbsp;is null, and if not, it should report the duration for&nbsp;</span><strong>lastView</strong><span> by calculating it based off the current timestamp and&nbsp;</span><strong>lastViewStartTime</strong><span>.</span>
</p>
<p>
  <span>After those steps, provide a&nbsp;</span><strong>reportView</strong><span>&nbsp;method to set the view name as a string parameter inside this method call&nbsp;</span><strong>reportViewDuration</strong><span> to report the duration of the previous view (if there is one). Then set the provided view name as&nbsp;</span><strong>lastView&nbsp;</strong><span>and the current timestamp as&nbsp;</span><strong>lastViewStartTime</strong><span>. Report the view as an event with the&nbsp;</span><strong>visit</strong><span>&nbsp;property and&nbsp;</span><strong>segment</strong><span>&nbsp;as your platform name. Additionally, if this is the first view a user visits in this app session, then also report the&nbsp;</span><strong>start</strong><span>&nbsp;property as true. You will also need to call&nbsp;</span><strong>reportViewDuration</strong><span> with the app exit event.</span>
</p>
<p>
  <span>After manual view tracking has been implemented, you may also implement automatic view tracking (if it is available on your platform). To implement automatic view tracking, you will need to catch your platform's specific event when the view is changed and call your implemented&nbsp;</span><strong>reportView</strong><span>&nbsp;method with the view name.</span>
</p>
<p>
  <span>Additionally, you will need to implement enabling and disabling automatic view tracking, as well as status checking, despite whether automatic view tracking is currently enabled or not.</span>
</p>
<p>
  <span>The pseudo-code to implement view tracking could appear as follows:</span>
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
  <span>Additionally, if your platform supports actions on view, such as clicks, you may report them as well. Here is more information on&nbsp;</span><a href="https://api.count.ly/reference/i#view-actions" target="_self">reporting actions for views</a><span>.</span>
</p>
<h1 id="h_01GYC4S9JM2F2WDDFSBEF2TBJ0">Device ID Management</h1>
<p>
  During the first SDK initilization, the SDK should acquire a device ID. It is
  a String value. that will identify the user.
</p>
<p>
  Device ID is either generated by the SDK or provided by the integrator as part
  of init configuration.
</p>
<p>
  If on a specific platform there are multiple ways a device ID could be generated,
  it should be possible to specify which method should be used.
</p>
<p>
  To understand which configuration options take precedence during init, have a
  look at the bellow
  <a href="#h_01GYC5WK7X17JTDEJEWMYFTYSA" target="_self">table</a>.
</p>
<p>
  Whatever value is acquired, it should be stored persistently.&nbsp;
</p>
<p>
  If another value was already acquired before, that one should be used unless
  a "clear stored device ID" flag is used.<span></span>
</p>
<p>
  When acquiring a device ID, the SDK should take note of the source of the ID.
  It should know if it is SDK generated or provided by the developer.
</p>
<h2 id="h_01GYC5WK7X17JTDEJEWMYFTYSA">
  <span>Device ID State Management During Init</span>
</h2>
<p>
  <span>There are different state combinations possible during init. This table covers all possible combinations and should be looked as a "truth table" of how the SDK should function.</span>
</p>
<table style="border-collapse: collapse; width: 96.6123%; height: 582px;" border="1">
  <tbody>
    <tr style="height: 10px;">
      <td class="wysiwyg-text-align-center" style="height: 10px; width: 19.9116%;" colspan="3">
        <span class="wysiwyg-font-size-medium">Stored Device ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="height: 10px; width: 31.1749%;" colspan="3">
        <span class="wysiwyg-font-size-medium">Provided ID During Init</span>
      </td>
      <td class="wysiwyg-text-align-center" style="height: 10px; width: 108.455%;" colspan="2">
        <span class="wysiwyg-font-size-medium">Action Taken by SDK</span>
      </td>
    </tr>
    <tr style="height: 44px;">
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 44px; text-align: center; vertical-align: middle; padding: 2px;" colspan="2">
        <span class="wysiwyg-font-size-small">Non-Temp ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 44px; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-small">Temp ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 44px; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-small">Custom ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 44px; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-small">Temp ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 44px; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-small">URL Provided</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 44px; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-small">'clear Stored Device ID' flag is not set</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; height: 44px; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-small">'clear Stored Device ID' flag is set</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 19.9116%; height: 22px;" colspan="3">
        <font size="2">
          <span class="wysiwyg-font-size-small">First Init</span>
        </font>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; background-color: #f0c0d9; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">SDK generates ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; height: 22px; text-align: center; vertical-align: middle; padding: 2px; background-color: #f0c0d9;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">SDK generates ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 19.9116%; height: 22px;" colspan="3">
        <font size="2">
          <span class="wysiwyg-font-size-small">First Init</span>
        </font>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-color-green110">⬤</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; background-color: #b5f0b4; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets custom ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #b5f0b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets custom ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="height: 22px; width: 19.9116%;" colspan="3">
        <font size="2">
          <span class="wysiwyg-font-size-small">First Init</span>
        </font>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; background-color: #e6cdf0; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Enters Temp mode</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #e6cdf0;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Enters Temp mode</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 19.9116%; height: 22px;" colspan="3">
        <font size="2">
          <span class="wysiwyg-font-size-small">First Init</span>
        </font>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; background-color: #f0e9b4; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="height: 22px; width: 19.9116%;" colspan="3">
        <font size="2">
          <span class="wysiwyg-font-size-small">First Init</span>
        </font>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; background-color: #b5f0b4; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets custom ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #b5f0b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets custom ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 19.9116%; height: 22px;" colspan="3">
        <font size="2">
          <span class="wysiwyg-font-size-small">First Init</span>
        </font>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; background-color: #f0e9b4; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
      <td class="wysiwyg-text-align-justify" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 19.9116%; height: 22px;" colspan="3">
        <font size="2">
          <span class="wysiwyg-font-size-small">First Init</span>
        </font>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; background-color: #f0e9b4; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 19.9116%; height: 22px;" colspan="3">
        <font size="2">
          <span class="wysiwyg-font-size-small">First Init</span>
        </font>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <font size="2">
          <span class="wysiwyg-color-green110">⬤</span>
        </font>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; background-color: #f0e9b4; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-color-green110">⬤</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">&nbsp;-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; background-color: #c8c0f0; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Uses Stored ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #f0c0d9;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">SDK generates ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-color-green110">⬤</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-&nbsp;</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #c8c0f0;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Uses Stored ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; height: 22px; text-align: center; vertical-align: middle; padding: 2px; background-color: #b5f0b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets custom ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-color-green110">⬤</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-&nbsp;</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; background-color: #c8c0f0; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Uses Stored ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #fff2cc;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Enters Temp mode</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #c8c0f0;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Uses Stored ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; height: 22px; text-align: center; vertical-align: middle; padding: 2px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-color-green110">⬤</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">&nbsp;-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; text-align: center; vertical-align: middle; padding: 2px; background-color: #c8c0f0;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Uses Stored ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #b5f0b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets custom ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span><span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><br></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #c8c0f0;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Uses Stored ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span><span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><br></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; background-color: #c8c0f0; text-align: center; vertical-align: middle; padding: 2px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Uses Stored ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span><span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><br></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #c8c0f0;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Uses Stored ID</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">&nbsp;-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #e6cdf0;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Stays in Temp mode</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; height: 22px; text-align: center; vertical-align: middle; padding: 2px; background-color: #f0c0d9;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">SDK generates ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-&nbsp;</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #b5f0b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets custom ID,<br>exits Temp mode </span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #b5f0b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets custom ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">-</td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-&nbsp;</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #e6cdf0;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Stays in Temp mode</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #e6cdf0;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Enters Temp mode</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-color-green110">⬤</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL provided ID,<br>exits Temp mode</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">&nbsp;-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; text-align: center; vertical-align: middle; padding: 2px; background-color: #b5f0b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets custom ID,<br>exits Temp mode</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #b5f0b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets custom ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; text-align: center; vertical-align: middle; padding: 2px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL provided ID, exits Temp mode</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; height: 22px; text-align: center; vertical-align: middle; padding: 2px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; text-align: center; vertical-align: middle; padding: 2px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL provided ID, exits Temp mode</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; height: 22px; text-align: center; vertical-align: middle; padding: 2px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td class="wysiwyg-text-align-center" style="width: 9.84283%; height: 22px;" colspan="2">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">-</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0688%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.5207%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.6248%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10.0294%; height: 22px;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small"><span class="wysiwyg-color-green110">⬤</span></span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 25.1522%; height: 22px; text-align: center; vertical-align: middle; padding: 2px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL provided ID, exits Temp mode</span>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 83.303%; text-align: center; vertical-align: middle; padding: 2px; height: 22px; background-color: #f0e9b4;">
        <span class="wysiwyg-font-size-medium wysiwyg-font-size-small">Sets URL Provided ID</span>
      </td>
    </tr>
  </tbody>
</table>
<h2 id="01H821RTQ48YFVRR5TMTJTZ3R0">Changing Device ID</h2>
<p>
  <span>In addition to initialization, developers may need to change the device ID while the app is running. For example, when an end-user signs out and another end-user signs in. In this case, the Countly SDK needs to provide a way to change the device ID at any point while the app is running. </span>
</p>
<p>
  <span>This change can be done with either with a server side merge or without it.</span>
</p>
<p>
  <span><strong>Note:</strong>&nbsp;If a new and current device ID is exactly the same, then the Countly SDK must ignore this change call.</span>
</p>
<p>
  <span>When changing device ID, it has to be done to a valid value. Making the SDK regenerate a new device ID should not be possible by providing an invalid value. If an invalid value (empty or null) is provided, the request is ignored and it prints a warning.</span>
</p>
<h3 id="01H821RTQ4XQDC3C24T8G7AAZX">
  <span>Changing ID Without Merging</span>
</h3>
<p>
  <span>It should replace the internally used device ID with the new one, and use it for all new requests, persistently storing it for further sessions. The Countly SDK should follow these steps:</span>
</p>
<ul>
  <li>
    <strong><span>Add currently recorded, but not queued, events to the request queue</span></strong>
  </li>
  <li>End the current session</li>
  <li>Clear all started timed-events</li>
  <li>
    <span>Change the device ID and store it persistently for further session use</span>
  </li>
  <li>
    <span>Begin a new session with the new device ID</span><span></span><span></span>
  </li>
</ul>
<h3 id="01H821RTQ4RPFFQJ9YFTNCNNQ1">
  <span>Changing ID With Merging</span>
</h3>
<p>
  <span>Developers may need to change a device ID to their own internal user ID and merge the server-side data previously generated by a user while he/she was unauthenticated. It is similar to "Changing ID without merging", but the Countly SDK will need to merge the data on the server as well. In order to make a proper transition, the Countly SDK should follow these steps:</span>
</p>
<ul>
  <li>
    <span>Temporarily keep the current device ID</span>
  </li>
  <li>
    <span>Change the device ID and store it persistently for further session use</span>
  </li>
  <li>
    <span>Use the&nbsp;</span><a href="https://api.count.ly/reference/i#change-id-and-merge-data" target="_self">old_device_id</a><span>&nbsp;API with the temporarily kept, old device ID to merge the data on the server</span>
  </li>
  <li>
    <span>No need to end and restart the current session or clear started timed-events</span>
  </li>
</ul>
<h2 id="01H821RTQ4Z7ZBN3SE64VW17GM">Retrieving the Current Device ID and Type</h2>
<p>
  There should be a call that returns the currently used device ID. It would be
  named similar to "GetDeviceId()".
</p>
<p>
  There should also be a call that returns the current device ID type. A "type"
  identifies the source of that device ID. The call would be named similar to "GetDeviceIdType()".
</p>
<p>
  There are 3 device ID types:<br>
  * SDK_GENERATED - this ID was generated by the SDK.<br>
  * DEVELOPER_SUPPLIED - this ID was provided by the developer. Either during init
  or by changing the device ID after init.<br>
  * TEMPORARY_ID - the SDK is in the temporary ID mode.
</p>
<h2 id="01H821RTQ4RSS9KH1YZHVSFRMJ">Temporary ID Mode (WIP)</h2>
<p>
  It's a mode that the SDK can enter. While in it, no requests, that are created
  under it, would be sent to the server. All data would be recorded under a temporary
  ID tag. Once a real device ID is acquired, that temporary tag would be replaced
  with the new device ID and they would be sent to the server.
</p>
<h1 id="01H821RTQ4N0QMR49CM619Z3ZE">Push Notifications</h1>
<p>
  <span>Push notifications are platform-specific and not all platforms have them. However, if your platform does, you would need to register your device to the push notification server and send the token to the Countly server. For more information, please click&nbsp;</span><a href="https://api.count.ly/reference/i#push-notifications" target="_self">here</a><span>&nbsp;for API calls.</span>
</p>
<p>
  <span>From the SDK API point of view, there could be one simple function to enable push notifications for the Countly server:</span>
</p>
<pre><code class="text">Countly.enable_push()</code></pre>
<h2 id="01H821RTQ5E9ADZZBRH6FWGQNX">Actioned Events</h2>
<p>
  When recording actioned events, one of the segmentation values recorded is the
  platform value. It is recorded with the key "p". The platform is then recorded
  with one unique character. Each platform needs to have it's own unique value.
  The currently used ones are the following:
</p>
<ul>
  <li>"a" - Android</li>
  <li>"i" - iOS</li>
  <li>"m" - macOS</li>
</ul>
<h2 id="01H821RTQ5YWFTQ776SZWR9RSB">Platform Specific Notes</h2>
<h3 id="01H821RTQ5M2PDNV8VA4BQEM3P">Additional Intent Redirection Checks (Android)</h3>
<p>
  <span>To increase platform security and limit exploits, google has enforced additional requirements for push notification that require additional checks for push intents. More info can be found <a href="https://support.google.com/faqs/answer/9267555?hl=en" target="_blank" rel="noopener">here</a>.</span>
</p>
<p>
  <span>These additional checks should be optional and there should be a way to enable the during init/push setup. Something like this:</span>
</p>
<pre><span>CountlyPush</span>.<span>useAdditionalIntentRedirectionChecks </span>= <span>true</span>;<br><span></span></pre>
<p>
  If these are enabled then the SDK will enforce additional security checks.
</p>
<p>
  As additional parameters there would a one or multiple allow lists to provide
  details of what kind of packages or activities are allowed.
  <span>There should be a way to enable the during init/push setup.</span>
</p>
<p>Providing that information could look something like this:</p>
<pre><span>List</span>&lt;<span>String</span>&gt; <span>allowedClassNames </span>= <span>new </span>ArrayList&lt;&gt;();<br><span>allowedClassNames</span>.add(<span>"MainActivity"</span>);<br><span>List</span>&lt;<span>String</span>&gt; <span>allowedPackageNames </span>= <span>new </span>ArrayList&lt;&gt;();<br><span>allowedPackageNames</span>.add(getPackageName());<br><br><span>CountlyConfigPush countlyConfigPush </span>= <span>new </span>CountlyConfigPush(<span>this</span>, <span>Countly</span>.<span>CountlyMessagingMode</span>.<span>PRODUCTION</span>)<br>.setAllowedIntentClassNames(<span>allowedClassNames</span>)<br>.setAllowedIntentPackageNames(<span>allowedPackageNames</span>);<br><span>CountlyPush</span>.<span>init</span>(<span>countlyConfigPush</span>);</pre>
<h1 id="01H821RTQ54ZMXGFNVRVMWY99P">Recording Location</h1>
<p>
  SDKs should be able to send location information to the server. This information
  can include:
</p>
<ul>
  <li>Country code</li>
  <li>City name</li>
  <li>Latitude and longitude values</li>
  <li>IP address</li>
</ul>
<p>
  Product Information:
  <a href="/hc/en-us/articles/4431589003545#h_01HAWAJ8QP38V2Q54RKAG9WRHN" target="_blank" rel="noopener noreferrer">Product Documentation</a>
  |
  <a href="/hc/en-us/articles/4404570865433#h_01HCD3STXGT4RFT3MM4PF3XCCN" target="_blank" rel="noopener noreferrer">Other Uses</a>
  |
  <a href="/hc/en-us/articles/4403281285913#h_01HBPA9VW7HRTFJSMHZBA0X9X4" target="_blank" rel="noopener noreferrer">Further Server Logic</a>
</p>
<h2 id="h_01JBXS3NT6PCW066JQMKP7706E">
  <span class="wysiwyg-font-size-x-large">Exposed Methods</span>
</h2>
<p id="h_01JBXS3RF5Y42D1CVQWRH29F5D">
  <strong>Config Methods</strong>
</p>
<pre>CountlyConfig.<strong>setLocation</strong>(countryCode, city, gpsCoordinates, ipAddress)</pre>
<pre>CountlyConfig.<strong>setDisableLocation</strong>()</pre>
<p id="h_01JBXS3WH145H8APDN41QP6MCX">
  <strong>Instance Methods</strong>
</p>
<pre>CountlyInstance.<strong>setLocation</strong>(countryCode, city, gpsCoordinates, ipAddress)</pre>
<pre>CountlyInstance.<strong>disableLocation</strong>(countryCode, city, gpsCoordinates, ipAddress)</pre>
<h2 id="h_01JBXS7XFB86RGGCVWHH4S7FW9">
  <span class="wysiwyg-font-size-x-large">Implementation Details</span>
</h2>
<p>
  For config method <strong>setLocation</strong>:
</p>
<pre>CountlyConfig.<strong>setLocation</strong>(countryCode, city, gpsCoordinates, ipAddress)<br><br><strong>// Valid values</strong><br>All non empty String values are valid.<br>All nullable. Only non null, non empty String values are used.<br>Non valid values are warned and ignored.<br><br><strong>// Logic</strong><br>Overrides the internal location cache with given values.<br>Warns if city is not coupled with country.</pre>
<p>
  For config method <strong>setDisableLocation</strong>:
</p>
<pre>CountlyConfig.<strong>setDisableLocation</strong>()<br><br><strong>// Logic</strong><br>Sets location tracking off (in a variable) regardless of setLocation.</pre>
<p>
  For instance method <strong>setLocation</strong>:
</p>
<pre>CountlyInstance.<strong>setLocation</strong>(countryCode, city, gpsCoordinates, ipAddress)<br><br><strong>// Valid values</strong><br>All non empty String values are valid.<br>All nullable. Only non null, non empty String values are used.<br>Non valid values are warned and ignored. <br><br><strong>// Logic</strong><br>Can be called before and after init.<br>Before init: <br>   - overrides the internal location cache with given values. <br>After init: <br>   - Re-enables location tracking (if disabled)<br>   - overrides the internal location cache with given values.<br>   - records a location request to request queue (omitting IP address) if:<br>      - (a session has started) <strong>and</strong> (auto sessions are on)<br>      - (no session consent given) <strong>or</strong> (auto sessions are off)<br>      - re-enabled location tracking <br>Warns if city is not coupled with country.</pre>
<p>
  For instance method <strong>disableLocation</strong>:
</p>
<pre>CountlyInstance.<strong>disableLocation</strong>()<br><br><strong>// Logic</strong><br>Sets location tracking off.<br>Records an empty location (location="") request to request queue</pre>
<p>Automatic Begin Session requests should behave like this:</p>
<pre>1. Should add cached location information to itself if:<br>   - (location consent given) <strong>and</strong> (location tracking is on)<br>2. Should add location="" to itself if:<br>   - (no location consent) <strong>or</strong> (location tracking off)</pre>
<p>
  SDK records an empty location (location="") request to request queue:
</p>
<pre>1. At the end of init if:<br>   - (no location consent <strong>or</strong> location tracking off) <strong>and</strong> (no session consent)</pre>
<p>Consent removal/addition will have this implications:</p>
<pre>Location consent removal:<br>   - records an empty location (location="") request to request queue<br>Location consent given:<br>   - no action</pre>
<h3 id="h_01JC2J9JAAJ42RNRKSZXWGFHSH">
  <span class="wysiwyg-font-size-large">Networking and Params</span>
</h3>
<p>Four location parameter that can be sent to server are:</p>
<pre>country_code : Country code in the two-letter, ISO standard<br>city : City name<br>location : Latitude and longitude values separated by a comma, e.g. "56.42345,123.45325"<br>ip : IP address</pre>
<p>
  Location requests are sent to the <strong>"/i"</strong> endpoint.
</p>
<p>
  Location requests should be sent through the<strong> request queue</strong>.
</p>
<p>
  Empty country code, city and IP address can not be sent (simply omitted).
</p>
<pre><strong>// Common way to send all</strong><br>serverURL + /i? + <br>country_code="us" +<br>&amp;city="panama" +<br>&amp;location="56.42345,123.45325" +<br>&amp;ip="0.0.0.0" +<br>...remaining common params<br><br><strong>// Incase of empty location requests:</strong><br>serverURL + /i? + <br>&amp;location="" +<br>...remaining common params</pre>
<h3 id="h_01JBXS49HVS4NHYNS3ZYBVK0QH">
  <span class="wysiwyg-font-size-large">Storage</span>
</h3>
<p>
  Location information is not stored persistently (in a way that would survive
  SDK shutdowns and further inits). Location information is stored only in memory
  as variables. The SDK should cache only the latest location information meaning
  <strong>the provided values overwrite the previously cached values totally (meaning non valid/non provided values clears the cache for those values too.)</strong>.
</p>
<h3 id="h_01JBXVYT8VS83Y1XN8HBXHGNFG">
  <span class="wysiwyg-font-size-large">Consent</span>
</h3>
<p>
  Feature depends on `Location` consent but `session` consent also affects its
  behavior.
</p>
<h2 id="h_01HH0D7S3TEVYNXWE8S5C1NNXZ">
  <span class="wysiwyg-font-size-x-large">Test scenarios</span>
</h2>
<p>Some sample situations for handling location:</p>
<p>
  <strong>1) Dev Sets Location Sometime After Init</strong><br>
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
  <strong>2) Dev Sets Location During Init and a Separate Call</strong><br>
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
  <strong>3) Dev Sets Location During Init and After begin_session Calls</strong><br>
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
  <strong>4) Dev Sets Location Before First begin_session</strong><br>
  init with location (city, country)<br>
  setLocation(gps, ipAddress) (location request with gps, ipAddress)<br>
  begin_session (with location - gps, ipAddress)<br>
  setLocation(city, country, gps2) (location request with city, country, gps2)<br>
  end_session<br>
  begin_session (with location - city, country, gps2)<br>
  end_session
</p>
<h1 id="01H821RTQ5R9W3JXKNXAFAMQJT">Heatmaps</h1>
<p>
  Heatmaps is a plugin, exclusive to Web SDK, that can display the amalgamation
  of click and the scroll behavior of the users by attaching an overlay on the
  website that the Countly has integrated. Click and scroll behavior information
  is provided by the SDK and recorded as an event, internally, then send into the
  event queue, <strong>if click or/and scroll tracking is enabled</strong>. Automatic
  click and scroll tracking should be able to be enabled after init:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['track_scrolls']);
Countly.q.push(['track_clicks']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.track_scrolls();
Countly.track_clicks();</code></pre>
  </div>
</div>
<p>
  A user should be able to go to the Heatmaps section in their server and click
  on a heatmap from the available list of views. When a user clicks any view from
  that list the server generates a token and directs the user to that view. Server
  would provide the token and the necessary scripts to load as the heatmaps overlay,
  by setting the name property of the browser's window interface or the URL hash
  property to an SDK recognizable message which then should be parsed and used
  by the SDK to load the necessary scripts for the heatmaps overlay. Message starts
  with 'cly:' and includes 'app_key','token','purpose' and 'url' properties as
  a JSON object.
</p>
<p>
  To prevent any XSS attempts, the SDK should provide an option to the developer
  to give a list of trustable domains (a whitelist per se) for which the SDK would
  load the provided scripts from and would reject to load scripts from domains
  out of this list. By default the Countly server URL would be included in this
  list. List should be provided by the user during init, under the 'heatmap_whitelist'
  flag as an array of stings.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.app_key = "YOUR_APP_KEY";
Countly.url = "https://try.count.ly";
Countly.heatmap_whitelist = ["https://you.domain1.com", "https://you.domain2.com"];

</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
    app_key:"YOUR_APP_KEY",
    url: "https://try.count.ly",
    heatmap_whitelist: ["https://you.domain1.com", "https://you.domain2.com"]
});</code></pre>
  </div>
</div>
<h2 id="01H821RTQ5AF7MR50N4HJJHRRF">Tracking Clicks</h2>
<p>A sample click event:</p>
<pre>{<br>  "key":"[CLY]_action",<br>  "count":1,<br>  "segmentation":{<br>    "type":"click",<br>    "x":120,<br>    "y":200,<br>    "width":1920,<br>    "height":1200,<br>    "view":"https://sth.com"<br>  }<br>}</pre>
<p>
  For click tracking it is better to set a cool-down period of 1 second after a
  click has been recorded to reduce the traffic before another click can be tracked.
</p>
<h2 id="01H821RTQ5JNSJJKK1B8DX3WJ4">Tracking Scrolls</h2>
<p>A sample scroll event:</p>
<pre>{<br>  "key":"[CLY]_action",<br>  "count":1,<br>  "segmentation":{<br>    "type":"scroll",<br>    "y":500,<br>    "width":1920,<br>    "height":1200,<br>    "view":"https://sth.com"<br>  }<br>}</pre>
<p>
  Scroll height must be stored internally in memory and with each new scroll within
  the same view this value must be referred to again to find the max scroll height.
  When a new view happens or the site is closed this max value must be recorded
  as the 'y' value like shown. You would not record the 'x' value.
</p>
<h2 id="01H821RTQ5FPAQS3EGH55622S9">Consent</h2>
<p>
  Both click and scroll tracking is subject to provided consent, namely "clicks"
  and "scrolls". If consents are enabled, user actions like clicks and scrolls
  should only be collected if the consent is provided, else they should be ignored.
</p>
<h1 id="01H821RTQ5EJN3V9GAP9FE6BK6">Remote Config</h1>
<p>
  A/B testing and Remote Config are different features, but their SDK-related integration
  is interlinked.
</p>
<p>
  The SDK's core utility for Remote Config and A/B testing is fetching some values
  from the server. Only the server decides which values to serve.
</p>
<h2 id="h_01JC374GVGQ2G5XGKDGATX3NE0">Remote Config</h2>
<p>
  Downloaded remote config values have to be stored persistently.
</p>
<p>
  Product Information:
  <a href="/hc/en-us/articles/9895605514009" target="_blank" rel="noopener noreferrer">Product Documentation</a>
</p>
<h3 id="h_01JC3775J4KWS2R6NXM2YN3GHY">Exposed Methods</h3>
<p>
  <strong>Config Methods</strong>
</p>
<pre>CountlyConfig.<strong>enableRemoteConfigAutomaticTriggers</strong>()</pre>
<pre>CountlyConfig.<strong>enableRemoteConfigValueCaching</strong>()</pre>
<pre>CountlyConfig.<strong>remoteConfigRegisterGlobalCallback</strong>(callback: RCDownloadCallback)</pre>
<p>
  <strong>Instance Methods</strong>
</p>
<pre>CountlyInstance.<strong>downloadOmittingKeys</strong>(keysToOmit: Array&lt;String&gt;, callback: RCDownloadCallback)</pre>
<pre>CountlyInstance.<strong>downloadSpecificKeys</strong>(keysToInclude: Array&lt;String&gt;, callback: RCDownloadCallback)</pre>
<pre>CountlyInstance.<strong>downloadAllKeys</strong>(callback: RCDownloadCallback)</pre>
<pre>Map&lt;String, RCData&gt; CountlyInstance.<strong>getValues</strong>()</pre>
<pre>RCData CountlyInstance.<strong>getValue</strong>(key: String)</pre>
<pre>CountlyInstance.<strong>registerDownloadCallback</strong>(callback: RCDownloadCallback)</pre>
<pre>CountlyInstance.<strong>removeDownloadCallback</strong>(callback: RCDownloadCallback)</pre>
<pre>CountlyInstance.<strong>clearAll</strong>()</pre>
<h3 id="h_01JC39FGVSK8R4RHW2XC71GRWF">Implementation Details</h3>
<p>
  For config method <strong>enableRemoteConfigAutomaticTriggers</strong>
</p>
<pre>CountlyConfig<strong>.enableRemoteConfigAutomaticTriggers()<br><br>// Logic<br><br></strong>Enables automatic download of the remote config values (in a variable)<br>This will trigger remote config values to be downloaded in those situations:<br>- After a device id change, values first cache cleared then downloaded again<br>- After exiting from temporary device id mode, values are downloaded<br>- After enrolling into a variant, values are cache cleared and downloaded again<br>- After remote config consent is given after init, values are downloaded<br>- After init is finished if we are not in the temporary id mode, values are downloaded</pre>
<p>
  For config method <strong>enableRemoteConfigValueCaching</strong>
</p>
<pre>CountlyConfig<strong>.enableRemoteConfigValueCaching()<br><br>// Logic<br><br></strong>Enables caching of remote config values. When this is enabled all remote-config values<br>are not deleted.</pre>
<p>
  For config method <strong>remoteConfigRegisterGlobalCallback</strong>
</p>
<pre>CountlyConfig.<strong>remoteConfigRegisterGlobalCallback</strong>(callback: RCDownloadCallback)<br><br><strong>// Valid values<br></strong>Value is not nullable, when null value is given it warns<br><br><strong>// Logic<br></strong>Notifies the developer about remote config values update process. <br>- If any error is encountered while downloading, the error is returned<br>- On a successful download, downloaded values are returned</pre>
<p>
  The callback's signature is <strong>RCDownloadCallback. </strong>And its callback
  method is
</p>
<pre>RCDownloadCallback {
  void callback(RequestResult requestResult, String error, boolean fullValueUpdate, Map&lt;String, RCData&gt; downloadedValues)
}

// <strong>Parameters</strong><br>- requestResult, one of the values <strong>Success, NetworkIssue, Error</strong> indicates result of the download<br>- error, error message. If it is null, it means there is no error<br>- fullValueUpdate, "true" - all values updated, "false" - a subset of values updated<br>- downloadedValues, the whole downloaded RC set, the delta<br><br>RCData will be mentioned in the Storage section.</pre>
<p>
  For instance method <strong>downloadAllKeys</strong>
</p>
<pre>CountlyInstance.<strong>downloadAllKeys</strong>(callback: RCDownloadCallback)<br><br><strong>// Valid values</strong><br>All nullable, only non null values are accepted<br>Non valid values are warned and ignored<br><br><strong>// Logic<br></strong>Before preparing the request, the function will do some checks<br>- If no device id exists, the call is omitted. Given and registered callbacks are notified.<br>- If temporary device id enabled or request queue is containing temporary id requests, <br>  Given and registered callbacks are notified.<br><br>After those checks, SDK will prepare the fetch request using the device metrics.<br>Then it will send the request immediately without adding it to the request queue.<br>- If any error encountered while request sent or retrieved, given and registered <br>  callbacks are notified.<br><br>The function will parse the response and notify the given and registered callbacks.<br>And the remote config store is updated. We clear all values. If remote config value caching<br>is enabled we cache them rather than clearing them.</pre>
<p>
  For instance method <strong>downloadOmittingKeys</strong>
</p>
<pre>CountlyInstance.<strong>downloadOmittingKeys</strong>(keysToInclude: Array&lt;String&gt;, callback: RCDownloadCallback)<br><br><strong>// Valid values</strong><br>All nullable, only non null and not empty values are accepted<br>Non valid values are warned and ignored<br><br><strong>// Logic<br></strong>- If keysToOmit is not empty, a parameter will be added to omit some keys to the remote <br>config fetch request. The server will return all values except omitted ones.<br>- If the keysToOmit is empty, this function will behave like downloading all values.<br><br>We only update the keys in the storage that are changed.</pre>
<p>
  For instance method <strong>downloadSpecificKeys</strong>
</p>
<pre>CountlyInstance.<strong>downloadSpecificKeys</strong>(keysToInclude: Array&lt;String&gt;, callback: RCDownloadCallback)<br><br><strong>// Valid values</strong><br>All nullable, only non null and not empty values are accepted<br>Non valid values are warned and ignored<br><br><strong>// Logic<br></strong>- If keysToInclude is not empty, a parameter will be added to include some keys to the remote <br>config fetch request. Server will return only specified values.<br>- If the keysToInclude is empty, this function will behave like downloading all values.<br><br>We only update the keys in the storage that are changed.</pre>
<p>
  For instance method <strong>getValues</strong>
</p>
<pre>Map&lt;String, RCData&gt; CountlyInstance.<strong>getValues</strong>()<br><br><strong>// Logic<br></strong>This will get all saved remote config values from the storage</pre>
<p>
  For instance method <strong>getValue</strong>
</p>
<pre>RCData CountlyInstance.<strong>getValue</strong>(key: String)<br><br><strong>// Valid values</strong><br>Only non null and not empty key is accepted<br>If non valid key is given, the call will be omitted.<br><br><strong>// Logic<br></strong>This will get the remote config value of the given key if it exists</pre>
<p>
  For instance method <strong>registerDownloadCallback</strong>
</p>
<pre>CountlyInstance.<strong>registerDownloadCallback</strong>(callback: RCDownloadCallback)<br><br><strong>// Valid values</strong><br>Only non null callback is accepted<br><br><strong>// Logic<br></strong>This will add the given callback to the internal callback list</pre>
<p>
  For instance method <strong>removeDownloadCallback</strong>
</p>
<pre>CountlyInstance.<strong>removeDownloadCallback</strong>(callback: RCDownloadCallback)<br><br><strong>// Valid values</strong><br>Only non null callback is accepted<br><br><strong>// Logic<br></strong>This will remove given callback from the internal callback list</pre>
<p>
  For instance method <strong>clearAll</strong>
</p>
<pre>CountlyInstance.<strong>clearAll</strong>()<br><br><strong>// Logic<br></strong>This will clear all remote config storage; caching is not important here</pre>
<h4 id="h_01JCD7PS7J57JCR69A9CDTY7F9">Networking and Params</h4>
<p>Remote config fetch request might consist of 4 parameters:</p>
<pre>keys: json array of specific keys<br>omit_keys: json array of omitted keys<br>method: this is always "rc"<br>metrics: this is session metrics and they are added if session consent is given</pre>
<p>
  method parameters is always sent with remote config fetch request.
</p>
<p>keys and omit_keys are optional.</p>
<p>
  Remote config fetch requests are sent to the "<strong>/i</strong>" endpoint.
</p>
<p>
  Remote config fetch requests are <strong>directly</strong> sent to the server,
  they will not be added to the request queue.
</p>
<pre>// <strong>Common way to send all<br></strong>serverURL + /i? +<br>method=rc +<br>&amp;keys=["url", "limit"] +<br>&amp;omit_keys=["money"] +<br>&amp;metrics=session metrics + // if session consent is given<br>...remaining common params<br><br>// <strong>No key parameters only required ones<br></strong>serverURL + /i? +<br>method=rc +<br>&amp;metrics=session metrics + // if session consent is given<br>...remaining common params</pre>
<p>Response would look like this:</p>
<pre>{
  "key": "value",
  "key1": "value2"
}</pre>
<h4 id="h_01JCD7QBDDJ36X6TRZZNNEAB80">Storage</h4>
<p>
  Remote config values are stored persistently. And they should have a structure.
</p>
<p>
  There might be a remote config key-value store structure that is keeping track
  of the remote config values.
</p>
<p>
  Any key-value storage is accepted. For reference JSON could be used.
</p>
<pre><code class="json">{
  "key": {
    "v": "value",
    "c": 0
  }
}</code></pre>
<p>
  c parameter indicates cache. When a remote config value is cached, c value must
  be 0. 1 means it is fresh, new value.<br>
  RCData object contains two fields:
</p>
<pre>value: any type<br>isCurrentUsersData: boolean</pre>
<p>
  isCurrentUsersData parameter is calculated like this; if the value is cached
  it is old user's data, false. If the value is fresh, just downloaded, then it
  is true.
</p>
<h4 id="h_01JCD7QN4C8JCD0GYHPF4XAXPM">Consent</h4>
<p>
  The feature depends on "remote-config" consent, and "session" consent affects
  the remote config fetch request.
</p>
<p>
  If consent is given, it will trigger remote config values to be downloaded if
  consents are enabled.
</p>
<p>
  If consent is revoked and remote config storage is not cleared, they will stay
  as they are.
</p>
<h2 id="h_01JCDT069MW1MNJDDRWGWZBRWT">A/B Testing</h2>
<p>
  Users can participate in AB tests. For that to happen, they must enroll in those
  tests (keys) with specific requests.
</p>
<p>
  Product Information:
  <a href="/hc/en-us/articles/4416496362393" target="_blank" rel="noopener noreferrer">Product Documentation</a>
</p>
<h3 id="h_01JCDT069MHCV9J7DAJVES43TT">Exposed Methods</h3>
<p>
  <strong>Config Methods</strong>
</p>
<pre>CountlyConfig.<strong>enrollABonRCDownload</strong>()</pre>
<p>
  <strong>Instance Methods</strong>
</p>
<pre>Map&lt;String, RCData&gt; CountlyInstance.<strong>getAllValuesAndEnroll</strong>()</pre>
<pre>RCData CountlyInstance.<strong>getValueAndEnroll</strong>(key: String)</pre>
<pre>CountlyInstance.<strong>enrollIntoABTestsForKeys</strong>(keys: Array&lt;String&gt;)</pre>
<pre>CountlyInstance.<strong>exitABTestsForKeys</strong>(keys: Array&lt;String&gt;)</pre>
<pre>Map&lt;String, String[]&gt; CountlyInstance.<strong>testingGetAllVariants</strong>()</pre>
<pre>Map&lt;String, ExperimentInformation&gt; CountlyInstance.<strong>testingGetAllExperimentInfo</strong>()</pre>
<pre>String[] CountlyInstance.<strong>testingGetVariantsForKey</strong>(key: String)</pre>
<pre>CountlyInstance.<strong>testingDownloadVariantInformation</strong>(completionCallback: RCVariantCallback)</pre>
<pre>CountlyInstance.<strong>testingDownloadExperimentInformation</strong>(completionCallback: RCVariantCallback)</pre>
<pre>CountlyInstance.<strong>testingEnrollIntoVariant</strong>(keyName: String, variantName: String, completionCallback: RCVariantCallback)</pre>
<h3 id="h_01JCDT069ME05YAEQEE24S86TM">Implementation Details</h3>
<p>
  For config method <strong>enrollABonRCDownload</strong>
</p>
<pre>CountlyConfig<strong>.enrollABonRCDownload()<br><br>// Logic<br><br></strong>Enables automatic enrolling to the remote config keys while fetching.<br>This will trigger adding a parameter to the remote config fetch request<code></code></pre>
<p>
  For instance method <strong>getAllValuesAndEnroll</strong>
</p>
<pre>Map&lt;String, RCData&gt; CountlyInstance.<strong>getAllValuesAndEnroll</strong>()<br><br><strong>// Logic<br></strong>This will get all saved remote config values from the storage and<br>will call the enrollIntoABTestsForKeys method.</pre>
<p>
  For instance method <strong>getValueAndEnroll</strong>
</p>
<pre>RCData CountlyInstance.<strong>getValueAndEnroll</strong>(key: String)<br><br><strong>// Valid values</strong><br>Only non null and not empty key is accepted<br>If non valid key is given, the call will be omitted.<br><br><strong>// Logic<br></strong>This will get the remote config value of the given key if it exists and<br>will call the enrollIntoABTestsForKeys method for the specified key if the key exist.</pre>
<p>
  For instance method <strong>enrollIntoABTestsForKeys</strong>
</p>
<pre>CountlyInstance.<strong>enrollIntoABTestsForKeys</strong>(keys: Array&lt;String&gt;)<br><br><strong>// Valid values</strong><br>Only non null and not empty keys are accepted<br>Non valid keys are warned and ignored<br><br><strong>// Logic<br></strong>This call will enroll user to the AB tests for the specified keys.<br>- If keys are null or empty call will be omitted.<br>- If temporary device id enabled or request queue is containing temporary id requests or <br>device id is not reachable at the moment function is called, call will be omitted. </pre>
<p>
  For instance method <strong>exitABTestsForKeys</strong>
</p>
<pre>CountlyInstance.<strong>exitABTestsForKeys</strong>(keys: Array&lt;String&gt;)<br><br><strong>// Valid values</strong><br>Keys could be nullable<br><br><strong>// Logic<br></strong>This call will exit user from the AB tests for the specified keys.<br>- If keys are null or keys are empty, it means exiting from all of AB tests.<br>- If temporary device id enabled or request queue is containing temporary id requests or <br>device id is not reachable at the moment function is called, call will be omitted. </pre>
<p>
  For instance method <strong>testingGetAllVariants</strong>
</p>
<pre>Map&lt;String, String[]&gt; CountlyInstance.<strong>testingGetAllVariants</strong>()<br><br><strong>// Logic<br></strong>Before using this function, variants must be downloaded.<br>This function will return all variants.</pre>
<p>
  For instance method <strong>testingGetAllExperimentInfo</strong>
</p>
<pre>Map&lt;String, ExperimentInfo&gt; CountlyInstance.<strong>testingGetAllExperimentInfo</strong>()<br><br><strong>// Logic<br></strong>Before using this function, experiment informations must be downloaded.<br>This function will return all experiment informations.<br><br>ExperimentInfo will be mentioned in the Storage section.</pre>
<p>
  For instance method <strong>testingGetVariantsForKey</strong>
</p>
<pre>String[] CountlyInstance.<strong>testingGetVariantsForKey</strong>(key: String)<br><br><strong>// Valid values</strong><br>Only non null and not empty key is accepted<br>If non valid key is given, the call will be omitted.<br><br><strong>// Logic<br></strong>Before using this function, variants must be downloaded.<br>This function will return the variants for the given key.<br>- If no variants found for the specified key, null is returned.</pre>
<p>
  For instance method <strong>testingDownloadVariantInformation</strong>
</p>
<pre>CountlyInstance.<strong>testingDownloadVariantInformation</strong>(completionCallback: RCVariantCallback)<br><br><strong>// Valid values</strong><br>Callback is nullable<br><br><strong>// Logic<br></strong>This function will download variants from the server.<br>- If temporary device id enabled or request queue is containing temporary id requests or <br>device id is not reachable at the moment function is called, call will be omitted and callback<br>is notified.<br><br>After those checks, SDK will prepare the variant fetch request.<br>Then it will send the request immediately without adding it to the request queue.<br>- If any error encountered while request sent or retrieved, given callback is notified.<br><br>The function will parse the response and replace all variant with the fresh downloaded values.</pre>
<p>
  The completionCallback's signature is <strong>RCVariantCallback. </strong>And
  its callback method is
</p>
<pre>RCVariantCallback {
  void <strong>callback</strong>(<strong>RequestResult</strong> requestResult, <strong>String</strong> error)
}

<strong>// Parameters</strong><br>- requestResult, one of the values <strong>Success, NetworkIssue, Error</strong> indicates result of the download<br>- error, error message. If it is null, it means there is no error</pre>
<p>
  For instance method <strong>testingDownloadExperimentInformation</strong>
</p>
<pre>CountlyInstance.<strong>testingDownloadExperimentInformation</strong>(completionCallback: RCVariantCallback)<br><br><strong>// Valid values</strong><br>Callback is nullable<br><br><strong>// Logic<br></strong>This function will download experiments from the server.<br>- If temporary device id enabled or request queue is containing temporary id requests or <br>device id is not reachable at the moment function is called, call will be omitted and callback<br>is notified.<br><br>After those checks, SDK will prepare the experiment fetch request.<br>Then it will send the request immediately without adding it to the request queue.<br>- If any error encountered while request sent or retrieved, given callback is notified.<br><br>The function will parse the response and replace all experiments with the fresh downloaded values.</pre>
<p>
  For instance method <strong>testingEnrollIntoVariant</strong>
</p>
<pre>CountlyInstance.<strong>testingEnrollIntoVariant</strong>(keyName: String, variantName: String, completionCallback: RCVariantCallback)<br><br><strong>// Valid values</strong><br>keyName and variantName are not nullable and not empty. <br>completionCallback is nullable.<br>If non valid values are given they are warned and call will be omitted.<br><br><strong>// Logic<br></strong>This function do some checks before enrolling into specified variant<br>- If temporary device id enabled or request queue is containing temporary id requests or <br>device id is not reachable at the moment function is called, call will be omitted and callback<br>is notified.<br><br>After those checks, SDK will prepare the enrolling into variant request.<br>Then it will send the request immediately without adding it to the request queue.<br>- If any error encountered while request sent or retrieved, given callback is notified.<br><br>If the request is successful, the function will trigger downloading remote config values<br>with clearing all remote config values from the storage. And the callback is notified with<br>a Success.</pre>
<h4 id="h_01JCDT069M3VGXFQTBBR9XDPR0">Networking and Params</h4>
<p>
  If the configuration <strong>enrollABonRCDownload</strong> is called the SDK
  will add a parameter to the remote config values fetch request:
  <strong>oi=1</strong>
</p>
<pre>// <strong>a remote config fetch request</strong><br>serverURL + /i? +<br>method=rc +<br>...other remote config fetch request params if any +<br><strong>&amp;oi=1</strong> +<br>...remaining common params</pre>
<p>
  Here is a casual fetching all variants request, it does not have any other parameter
  than method:
</p>
<pre>// <strong>a variants fetch request</strong><br>serverURL + /i? +<br>method=ab_fetch_variants +<br>...remaining common params</pre>
<p>And the response would look like this:</p>
<pre><code class="json">{
  "key1": [
    {
      "name": "variant1",
      "value": "value1"
    },
    {
      "name": "variant2",
      "value": "value2"
    }
  ],
  "key2": [
    {
      "name": "variant1",
      "value": "value1"
    }
  ]
}</code></pre>
<p>
  Here is a casual fetching all experiment informations request, it does not have
  any other parameter than method:
</p>
<pre>// <strong>a experiment information fetch request</strong><br>serverURL + /i? +<br>method=ab_fetch_experiments +<br>...remaining common params</pre>
<p>
  And the response would look like this, this will return a json array:
</p>
<pre><code class="json">[
  {
    "id": "experiment_id_1",
    "name": "Experiment Name 1",
    "description": "Description for Experiment 1",
    "currentVariant": "variant_A",
    "variants": {
      "variant_A": {
        "property_key_1": "property_value_1",
        "property_key_2": "property_value_2"
      },
      "variant_B": {
        "property_key_1": "property_value_3",
        "property_key_2": "property_value_4"
      }
    }
  },
  {
    "id": "experiment_id_2",
    "name": "Experiment Name 2",
    "description": "Description for Experiment 2",
    "currentVariant": "variant_B",
    "variants": {
      "variant_A": {
        "property_key_1": "property_value_5",
        "property_key_2": "property_value_6"
      },
      "variant_B": {
        "property_key_1": "property_value_7",
        "property_key_2": "property_value_8"
      }
    }
  }
]</code></pre>
<p>Here is a casual enrolling into a variant request:</p>
<pre>// <strong>an enrolling into a variant request</strong><br>serverURL + /i? +<br>method=ab_enroll_variant +<br>&amp;key=keyName +<br>&amp;variant=variantName +<br>...remaining common params<code class="json"></code></pre>
<h4 id="h_01JCDT069MRV9XMBV28T1W74H8">Storage</h4>
<p>
  AB Testing is not stored persistently. Variants and experiment informations are
  stored in memory in a key-value pair structure like Map.
</p>
<p>
  Variants are stored in a string and string array structured map where key is
  remote config key name and value is variants name that is specified for that
  remote config key.
</p>
<pre>// Key-value structure<br>key1: [variant1, variant2]<br>key2: [variant3, variant4]</pre>
<p>
  Experiment informations are stored in a string and ExperimentInfo structured
  map where key is experiment id and value is ExperimentInfo structure:
</p>
<pre>ExperimentInfo:<br>  <strong>experimentID</strong>: id of the experiment, string<br>  <strong>experimentName</strong>: name of the experiment, string<br>  <strong>experimentDescription</strong>: description of the experiment, string<br>  <strong>currentVariant</strong>: active variant for that experiment, string<br>  <strong>variants</strong>: variants for that experiment which is a string and string array key-value<br>    structure like key is remote config key name and value is variants name that is <br>    specified for that remote config key</pre>
<h4 id="h_01JCDT069M1ZTGCJP0WRJA6KHR">Consent</h4>
<p>The feature depends on "remote-config" consent.</p>
<p>If consent is revoked, in memory values are not cleared.</p>
<h1 id="01H821RTQ689TVKC3WBTZ610X7">User Feedback</h1>
<h2 id="01H821RTQ6WTDZPVQ9GDX3M5QR">Star Rating</h2>
<p>
  <span>If possible, the SDK should provide a simple 1 to 5 star-rating interface for receiving user feedback about the application. The interface will have a simple message explaining its purpose, a 1 through 5-star meter for receiving users’ ratings, and a dismiss button in case the user does not wish to give a rating. This star rating has nothing to do with App Store/Google Play Store ratings and reviews. It is just for getting brief feedback from users to be displayed on the Countly dashboard.</span>
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/102515c-star-rating2x.png">
</div>
<p>
  <span>After a user gives a rating, a reserved event will be recorded with <code>[CLY]_star_rating</code></span><span>as the key and following as the segmentation dictionary:</span>
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
  <span>If a user dismisses the star-rating dialog without giving a rating, an event will not be recorded. The star-rating dialog's message and dismiss button title may be customized using the properties on the initial configuration object.</span>
</p>
<pre><code class="java">CountlyConfiguration.starRatingMessage = "Custom Message";
CountlyConfiguration.starRatingDismissButtonTitle = "Custom Dismiss Button Title";</code></pre>
<p>
  <span>If not explicitly set, the message should read, "How would you rate the app?" and the dismiss button title will read, "Dismiss" or one of the corresponding localized versions depending on the device’s language.</span>
</p>
<p>
  <span>The star-rating dialog may be displayed in 2 ways:</span>
</p>
<p>
  <strong>1. Manually by the Developer</strong>
</p>
<p>
  <span>The star-rating dialog will be displayed when the developers call the specified method, such as <code>askForStarRating</code></span><span>. Optionally, there will be a callback method indicating the user's 1-to-5 rating value for the developer if the developer wants to use the rating.</span>
</p>
<pre><code class="java">Countly.askForStarRating(callback);</code></pre>
<p>
  <span>There is no limit on how many times the star-rating dialog may be manually displayed.</span>
</p>
<p>
  <strong>2. Automatically, Depending on the Session Count</strong>
</p>
<p>
  <span>The star-rating dialog will be displayed when the application's session count reaches a specified limit, once for each new version of the application. The SDK should keep track of the session count for each app version locally and compare it to the specified count on each app launch. This session count limit may be specified upon initial configuration.</span>
</p>
<pre><code class="java">CountlyConfiguration.starRatingSessionCount = 5;</code></pre>
<p>
  <span>Once the star-rating dialog has been displayed automatically, it will not be displayed again unless there is a new app version.</span>
</p>
<p>
  Upon initial configuration, there should be an optional flag called
  <code>starRatingDisableAskingForEachAppVersion</code> to force the star-rating
  dialog to be displayed only once per app lifetime instead of for each new version.
</p>
<pre><code class="java">CountlyConfiguration.starRatingDisableAskingForEachAppVersion = false;</code></pre>
<h2 id="01H821RTQ6HKZAR27VX54Z2JJS">Rating Widgets</h2>
<h3 id="01H821RTQ680XHC86VDS4JDWSW">Automatic Rating Widgets</h3>
<p>
  Automatic widgets are integrated with custom HTML. That is either injected into
  the page (web) or shown in a webView (mobile).
</p>
<p>
  To present such a widget, you would have the following call:
</p>
<pre><span>presentRatingWidgetWithID</span>(S<span>tring </span>widgetId, <span>String </span>closeButtonText, <span>RatingWidgetCallback </span>callback)</pre>
<p>
  It takes the ID of the widget, the custom close button text, and a callback.
</p>
<h3 id="01H821RTQ68DR1MX4PC2FMA1NV">Manual Rating Widgets</h3>
<p>
  In case a developer wants to use their custom UI, they can report the result
  manually.
</p>
<p>They would use the following call:</p>
<p>
  <span>That function should be called "recordRatingWidgetWithID" and it should have the following parameters:</span><br>
  <span>"(String widgetId, int rating, String email, String comment, boolean userCanBeContacted)"</span>
</p>
<p>
  <span>"recordRatingWidgetWithID" should record an event with the internal key "[CLY]_star_rating". The event should have the following segmentation:</span>
</p>
<ul>
  <li>
    <span>"platform" - current platform</span>
  </li>
  <li>
    <span>"app_version" - current app version</span>
  </li>
  <li>
    <span>"rating" - provided rating result. In the range from 1 to 5. (Mandatory)</span>
  </li>
  <li>
    <span>"widget_id" - provided widget ID. (Mandatory)</span>
  </li>
  <li>
    <span>"contactMe" - provided value.</span>
  </li>
  <li>
    "email" - <span>provided value.</span>
  </li>
  <li>
    "comment" - <span>provided value.</span>
  </li>
</ul>
<p>
  <span>Basic filtering (type checks) on the provided values should be performed. Mandatory values must be provided. Invalid widget ID's (non string or empty values) should not be accepted. Rating value should be modified, if necessary, so that it lies within the acceptable range of [1,5].</span>
</p>
<h2 id="01H821RTQ6567XRJNZ6A13JYVE">Feedback Widgets</h2>
<p>
  The Feedback Widgets feature is a way to gather insights and opinions from users.
  Showing Feedback Widgets or performing any of the Feedback Widget-related features
  requires <code>feedback</code> consent.
</p>
<p>
  Before any Feedback Widgets can be shown, they need to be created in the Countly
  Dashboard.
</p>
<p>
  The Feedback Widgets API provides access to three types of widgets:
</p>
<ul>
  <li>
    <strong>Surveys: </strong>A list of questions supporting various answer formats
    such as multiple-choice, textbox, and rating scales.
  </li>
  <li>
    <strong>Ratings: </strong>Collects user feedback using a 1-5 rating scale.
    Has an option to leave a comment, and lea to leave an email for future contact.
  </li>
  <li>
    <strong>NPS (Net Promoter Score): </strong>Questions on a scale from 0-10,
    with customization options for follow-up questions.
  </li>
</ul>
<p>
  They are shown using a very similar server API and basically the same processing.
  This is also an alternative method to use rating widgets, which are also now
  included in this newer SDK API. Refer to the
  <a href="/hc/en-us/articles/4652903481753" target="_blank" rel="noopener noreferrer">Feedback User Guide</a>
  for more detailed information about Feedback Widgets.
</p>
<p>Feedback widgets can be used through three methods:</p>
<ul>
  <li>
    <p>
      <strong>Automatic Server Rendered Widget: </strong>The server rendered
      widget is inserted in the web page or the UI, using a WebView, by the
      SDK.
    </p>
  </li>
  <li>
    <p>
      <strong>Manually Rendered and Reported Widget: </strong>The client app
      builds a custom UI, and the results are reported to the SDK manually.
      Used in cases where the developer wants to use a custom UI.
    </p>
  </li>
  <li>
    <p>
      <strong>Server Rendered Widget in a Custom WebView: </strong>The SDK
      builds a required URL to be used in a WebView. This would then be used
      in the WebView of the client app of choice.
    </p>
  </li>
</ul>
<h3 id="01H821RTQ6RS3BAEPWF1EGD07R">Retrieving the List of Eligible Widgets</h3>
<p>
  The first step to showing a feedback widget is getting a list of the available
  widgets for this device ID. That would be done with a function named similar
  to <code>getAvailableFeedbackWidgets</code>. That call takes a callback. That
  callback returns 2 values. The second is the error string. The first one is a
  list of available widget objects (or any other mechanism that allows the grouping
  of this data). If a class is used for grouping, it should be named similar to
  <code>CountlyPresentableFeedback</code>. That object contains 4 core values (widget
  id (_id), widget type (type), widget name (name), tags (tg)) and 1 optional value
  (UI info (appearance)). Potential type values are currently "nps", "survey" and
  "rating".
</p>
<p>The URL to acquire all available widgets in a list is:</p>
<pre>/o/sdk?method=feedback&amp;app_key=[appKey]&amp;device_id=[deviceID]&amp;sdk_version=[sdkVersion]&amp;sdk_name=[sdkName]</pre>
<p>
  If parameter tampering is enabled, the sha256 param should be added with the
  checksum.
</p>
<p>
  If a temporary device ID is enabled, feedback widgets can't be shown, so an empty
  list of available widgets is returned.
</p>
<p>
  The server side will determine if there are any valid surveys for this device
  ID and return something similar to:
</p>
<pre>{
  "result":[
      {
        "_id":"614871419f030e44be07d82f",
        "type":"rating",
        "appearance":{
          "position":"mleft",
          "bg_color":"#fff",
          "text_color":"#ddd",
          "text":"Feedback"
          },
        "tg":["/"],
        "name":"Leave us a feedback"
      },
      {
        "_id":"614871419f030e44be07d839",
        "type":"nps",
        "name":"One response for all",
        "tg":[]
      },
      {
        "_id":"614871429f030e44be07d83d",
        "type":"survey",
        "appearance":{
          "position":"bLeft",
          "show":"uSubmit",
          "color":"#0166D6",
          "logo":null,
          "submit":"Submit",
          "previous":"Previous",
          "next":"Next"
          },
        "name":"Product Feedback example",
        "tg":[]
      }
    ]
  }</pre>
<p>
  <code>result</code> contains a JSON Array of widget Objects. The _id is used
  to construct the web view URL. Tags (the <code>tg</code> key) returns an Array
  of String values. This is information provided by the creator of the widget and
  can be used for various reasons. However the main goal is to provide versioning
  or a whitelist of domains to present the widget, and its implementation is left
  to the developer.
</p>
<p>
  The idea is that the developer would retrieve this list of potential widgets
  and decide any further action he would want to take with them with respect to
  the information provided.
</p>
<h3 id="h_01HQ1DNQK44EXDC5RD465GB1NE">Constructing WebView URL</h3>
<p>
  Constructing a WebView URL requires calling the related method by passing a
  <code>CountlyFeedbackWidget</code> object. Using information from that object,
  a widget URL will be constructed.
</p>
<p>
  Constructed URL using the widget ID (<code>_id</code> value) looks like this:
</p>
<pre>//for nps
/feedback/nps?widget_id=[widgetID]&amp;device_id=[deviceID]&amp;app_key=[appKey]&amp;sdk_version=[sdkVersion]&amp;sdk_name=[sdkName]&amp;app_version=[appVersion]&amp;platform=[platform]

//for basic surveys
/feedback/survey?widget_id=[widgetID]&amp;device_id=[deviceID]&amp;app_key=[appKey]&amp;sdk_version=[sdkVersion]&amp;sdk_name=[sdkName]&amp;app_version=[appVersion]&amp;platform=[platform]

//for ratings
/feedback/rating?widget_id=[widgetID]&amp;device_id=[deviceID]&amp;app_key=[appKey]&amp;sdk_version=[sdkVersion]&amp;sdk_name=[sdkName]&amp;app_version=[appVersion]&amp;platform=[platform]

//web SDK would also pass "origin"
//web SDK also passes "widget_v=Web"</pre>
<p>
  The created URL contains params for widget_id, device_id, app_key, sdk_version,
  sdk_name, app_version, platform, and origin (for Web SDK).
</p>
<p>
  Even if parameter tamper protection is enabled, this URL
  <strong>does not</strong> use the checksum param!
</p>
<p>
  That URL should then be provided to a WebView and shown as an alert dialog similar
  to the rating widget.
</p>
<h3 id="01HQ5E6TCV5BG1EWH2E3YD7BF1">Automatic Feedback Widgets</h3>
<p>Automatic Feedback Widget reporting has 3 steps:</p>
<ol>
  <li>Retrieve a list of available widgets and pick one.</li>
  <li>
    Presenting the widget with <code>presentFeedbackWidget</code> call.
  </li>
  <li>Handling the callbacks.</li>
</ol>
<p>
  As explained in the 'Retrieving the List of Eligible Widgets' section, the first
  step uses the <code>getAvailableFeedbackWidgets</code> function to communicate
  with the Countly server and obtain a list of available widgets based on the specific
  device. This list contains information about each widget, such as its ID, type,
  name, and tags.
</p>
<p>
  Once the list is retrieved and the developer decides upon the widget they are
  going to use, as explained in the 'Constructing the WebView URL' section, they
  would call <code>presentFeedbackWidget</code> method and pass the chosen widget
  (<code>CountlyFeedbackWidget</code>) object.
</p>
<p>
  It should be possible to provide 2 optional callbacks to the
  <code>presentFeedbackWidget</code> call:
</p>
<ol>
  <li>
    a callback (potentially named <code>widgetShown</code>) that is called when
    the widget is successfully presented (currently that would mean that there
    were no issues/errors while trying to show the dialog with the WebView).
    Also, we aren't verifying if the WebView is showing a working widget. If
    there are any issues during the display of the widget, this callback will
    return an error message.
  </li>
  <li>
    a callback (potentially named <code>widgetClosed</code>) that is called when
    the widget/dialog is closed (for mobile SDKs and for the web SDK that would
    mean slightly different things, but the main point is to have the host app/site
    notified of when the "feedback process" is over). If there are any issues
    during the closing of the widget, this callback will return an error message.
  </li>
</ol>
<h3 id="01H821RTQ6VMWG2GBHZHBYZ4DB">Manual Feedback Widgets</h3>
<p>Manual feedback widget reporting has 3 steps:</p>
<ol>
  <li>
    Retrieve a list of available widgets and pick one. This is the same initial
    step with the automatic feedback widgets and reuses the same call to retrieve
    them.
  </li>
  <li>
    Download widget data from the server (for that single widget with the information
    that has been retrieved from the previous step).
  </li>
  <li>
    Report the feedback result (for that single widget according to that data
    from the previous step).
  </li>
</ol>
<p>
  As mentioned before, the first step uses
  <code>getAvailableFeedbackWidgets</code> function, which is also used for automatic
  feedback widgets. After inspecting the returned list, the developer would select
  one widget he would want to report from the list of widgets, and then he would
  use this as the <code>CountlyFeedbackWidget</code> object.
</p>
<p>
  The second step uses the <code>CountlyFeedbackWidget</code> object from the previous
  step and calls <code>getFeedbackWidgetData</code> function. This function call
  accepts the <code>CountlyFeedbackWidget</code> object and a callback. That callback
  returns 2 values - the retrieved <code>CountlyWidgetData</code> JSON and an error
  message string. The string is used in case there are some issues with this call.
</p>
<p>
  The returned <code>CountlyWidgetData</code> JSON is the response from making
  a server request. That request is done outside of the request queue (so a direct
  request). Using the <strong>widget ID</strong> and
  <strong>widget type</strong> information from the provided
  <code>CountlyFeedbackWidget</code> object, we construct a URL similar to:
</p>
<pre>//for nps
/o/surveys/nps/widget?widget_id=[widgetID]&amp;shown=1&amp;sdk_version=[sdkVersion]&amp;sdk_name=[sdkName]&amp;app_version=[appVersion]&amp;platform=[platform]

//for basic surveys
/o/surveys/survey/widget?widget_id=[widgetID]&amp;shown=1&amp;sdk_version=[sdkVersion]&amp;sdk_name=[sdkName]&amp;app_version=[appVersion]&amp;platform=[platform]

//for rating widgets
/o/surveys/rating/widget?widget_id=[widgetID]&amp;shown=1&amp;sdk_version=[sdkVersion]&amp;sdk_name=[sdkName]&amp;app_version=[appVersion]&amp;platform=[platform]</pre>
<p>
  Performing a request on that URL should return JSON describing the widget, which
  should then be returned as <strong>a parsed JSON object</strong>.
</p>
<p>
  After this step, the developer has all the information he needs to create the
  widget and all the information required to prepare a response (namely the
  <code>widgetResult</code> object) to "report" the filled widget.
</p>
<p>
  The developer would look at
  <a href="/hc/en-us/articles/9290669873305#h_01HABT18WT0D08H8DR2BAD77T2" target="_blank" rel="noopener noreferrer">this</a>
  document to better understand how to interpret the widget type and data to fill
  out the <code>widgetResult</code> object. Depending on the type of the widget
  being reported this object would have different key/value pairs.
</p>
<p>
  At the third step, the developer would call the
  <code>reportFeedbackWidgetManually</code> function to report the result. This
  call requires 3 fields/values/parameters: <code>CountlyFeedbackWidget</code>
  object from the first step, <code>CountlyWidgetData</code> object from the second
  step and the ,<code>widgetResult</code> object that has been formed and provided
  by the developer. If the <code>widgetResult</code> is set to "null" then that
  means that the widget was closed without filling it out (this still requires
  an event to be created).
</p>
<p>
  <code>CountlyFeedbackWidget</code> object is used for obtaining widget id and
  type, while <code>CountlyWidgetData</code> object is used to verify the correctness
  of the reported <code>widgetResult</code>. For now, this second step is optional,
  but might become mandatory in the future, therefore both fields should be required
  from the start.
</p>
<p>
  The reported widget result should be recorded as an <strong>event</strong> and
  must be put into the event queue. This event must have the "[CLY]_nps"(for nps),
  "[CLY]_survey"(for survey) or "[CLY]_star_rating"(for rating) key respective
  to the type of the reported widget. That event should have the following segmentation:
</p>
<ul>
  <li>
    <code>platform</code> - SDK platform
  </li>
  <li>
    <code>app_version</code> - host app version
  </li>
  <li>
    <code>widget_id</code> - respective widget ID
  </li>
</ul>
<p>
  In addition to this segmentation which identifies the widget, the contents of
  the provided <code>widgetResult</code> object should be merged into this event's
  segmentation. If the <code>widgetResult</code> was provided null and so the widget
  was reported as closed, you should additionally add the following segmentation
  value:
</p>
<ul>
  <li>
    <code>closed</code> - with the value of "1"
  </li>
</ul>
<p>
  After this event has been added to the event queue, the event queue should be
  forcefully combined into a request, even if the event count is under the threshold.
  This way the event is sent as soon as possible to the server and marks the widget
  as "completed" for that specific user.
</p>
<h3 id="h_01HQMX59RNK27XW4S8HDMXBYC9">API and Data Structures Exposed by the SDK</h3>
<p>
  Provided functionality should require <code>Feedback</code> consent.
</p>
<p>
  Not all platforms can support methods to present the widget.
</p>
<p>
  If supported by the platform, the 'Feedback' interface should expose the following
  functions:
</p>
<pre><code>// Retrieves the list of available Feedback Widgets
void getAvailableFeedbackWidgets(RetrieveFeedbackWidgets callback);
  
// Displays a specific widget
void presentFeedbackWidget(CountlyFeedbackWidget widgetInfo, Context context, String closeButtonText, FeedbackCallback devCallback);
  
// Retrieves a specific widget's data as a JSONObject
void getFeedbackWidgetData(CountlyFeedbackWidget widgetInfo, RetrieveFeedbackWidgetData callback);
  
// Manually reports a widget's results
void reportFeedbackWidgetManually(CountlyFeedbackWidget widgetInfo, JSONObject widgetData, Map&lt;string, object&gt; widgetResult);
  
// Construct URL for the chosen feedback widget
string constructFeedbackWidgetUrl(CountlyFeedbackWidget chosenWidget);</code></pre>
<p>
  Retrieved CountlyFeedbackWidget object would look like this:
</p>
<pre><code class="java hljs"><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">CountlyFeedbackWidget</span> </span>{
  <span class="hljs-keyword">public</span> String widgetId;
  <span class="hljs-keyword">public</span> FeedbackWidgetType type;
  <span class="hljs-keyword">public</span> String name;
  <span class="hljs-keyword">public</span> String[] tags;
}</code></pre>
<p>
  The <code>RetrieveFeedbackWidgets</code>callback (used for
  <code>getAvailableFeedbackWidgets</code>) returns a list of CountlyFeedbackWidget
  objects as the first parameter and an error string as the second.
</p>
<p>
  The <code>RetrieveFeedbackWidgetData</code>callback (used for the
  <code>getFeedbackWidgetData</code>) returns the widget data as the first parameter
  and an error string as the second parameter. The data is returned in a JSON Object.
  Check
  <a href="/hc/en-us/articles/9290669873305#h_01HABT18WT0D08H8DR2BAD77T2" target="_blank" rel="noopener noreferrer">here</a>
  for example data structures returned.
</p>
<p>
  The <code>FeedbackCallback</code> callback (used for
  <code>presentFeedbackWidget</code>) returns an error string. The error is "null"
  in case there were no issues.
</p>
<p>There are no Init time config options for this feature.</p>
<h1 id="01H821RTQ6JDWE5B09F33H03WY">User Profiles</h1>
<p>
  <span>Your SDK does not need to have a platform-specific way to receive user data if it isn’t possible on your platform. However, you will need to provide a way for a developer to pass this information to the SDK and send it to the Countly server.</span>
</p>
<p>
  <span>To do so, you may create a method to accept an object with key/regarding the user, which are </span><a href="https://api.count.ly/reference/i#user-details" target="_self">described here</a><span>, or provide a parameterized method to pass the information regarding the user. Note that all fields are optional.</span>
</p>
<p>
  <span>Additionally, there could be custom key values added to the user details. In this case, you would need to provide a means to set them:</span>
</p>
<ul>
  <li>Countly.user_details(map details)</li>
  <li>Countly.user_custom_details(map custom_details)</li>
</ul>
<p>
  <span>You may find more information on what data may be set for a user </span><a href="https://api.count.ly/reference/i#user-details" target="_self">by following this link</a><span>.</span>
</p>
<p>
  If a "null" value is set to a user property, the SDK should ignore the value
  and print a warning.
</p>
<p>
  If an empty string is provided as a value then that should lead to the deletion
  of the user property on the server side. This should trigger the SDK to send
  a JSON null value assigned to the property.
</p>
<h2 id="01H821RTQ64NDJ9KHTM0B34MJK">Modifying Custom Data Properties</h2>
<p>
  <span>You should also provide an option to modify custom user data, such as by increasing the value on the server by 1, etc. Since there are many operations you could perform with that data, it is recommended to implement a subclass for this API, which may be retrieved through the Countly instance.</span>
</p>
<p>
  <span>The standard methods that should be provided by the SDK are as follows (provided as pseudo-code, naming conventions may differ from platform to platform):</span>
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
  <strong>Note</strong>:&nbsp;<span>when reporting to the server, assure the push, pushUnique, and pull parameters can provide multiple values for the same property as an array.</span>
</p>
<p>
  Here is
  <a href="https://api.count.ly/reference/i#modifying-custom-user-data" target="_self">more information</a>
  on how to report this data to the server.
</p>
<h2 id="01H821RTQ68NQXPHR6Q6M4NJ1Y">Orientation Changes</h2>
<p>
  This feature sends an event of the current orientation. It is sent when the first
  screen loads and every time the orientation changes.
</p>
<p>
  Orientation tracking is enabled by default if the required consent is given.
</p>
<p>
  Orientation tracking can be disabled during init. The config variable would be
  named similar to "<span>enableOrientationTracking" which then would receive a "false" value to turn orientation tracking off.</span>
</p>
<p>Orientation change tracking requires "users" consent.</p>
<p>
  When recording the orientation event, you should use the key "[CLY]_orientation".
  You would set the count to "1" and provide a single segmentation value. The key
  for that value is "mode" and the value is "portrait" if the current orientation
  is portrait mode or "landscape" if the current orientation is landscape mode.
</p>
<h1 id="01H821RTQ60H46MJ0HFB6WB60D">Application Performance Monitoring</h1>
<p>
  Countly server supports multiple metrics for performance monitoring. They are
  divided into 3 groups:
</p>
<ul>
  <li>Custom traces</li>
  <li>Network request traces</li>
  <li>Device traces</li>
</ul>
<h2 id="01H821RTQ6N7TWRG1FZXQ9E9HW">Trace / Metric keys</h2>
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
<h2 id="01H821RTQ6X2624ZK1FKJ1GC26">API Calls</h2>
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
<pre>/i<span>?app_key=app_key<br>  &amp;device_id=device_id<br>  &amp;dow=dow<br>  &amp;hour=hour<br>  &amp;timestamp=timestamp<br>  &amp;apm={ _apm_params }</span></pre>
<h2 id="01H821RTQ6P6YVK5A07RH9Z0CE">Custom Traces</h2>
<p>
  These are used as a tool to measure the performance of some running task. At
  the basic level, this function is similar to timed events. The default metric
  that gets tracked is the "duration" of the event.&nbsp; There should be a "startTrace"
  and "endTrace" call, which start and end the tracking. When ending the tracking,
  the developer has the option of providing additional metrics. Those metrics are
  String and Integer/Numeric pairs.
</p>
<p>&nbsp;Sample custom trace API request:</p>
<pre><span>/i?app_key=xyz<br>  &amp;device_id=pts911<br>  &amp;apm={"type":"device",<br>        "name":"forLoopProfiling_1",<br>        "apm_metrics":{"duration": 10, “memory”: 200}, <br>        "stz": 1584698900000, <br>        "etz": 1584699900000}<br>  &amp;timestamp=15847000900000</span></pre>
<h2 id="01H821RTQ6VQ552GKTX5Q8TBZX">Network Traces</h2>
<p>Sample network trace request:</p>
<pre><span>/i?app_key=xyz<br>  &amp;device_id=pts911<br>  &amp;apm={"type":"network",<br>        "name":"/count.ly/about",<br>        "apm_metrics":{"response_time":1330,"response_payload_size":120, "response_code": 300, "request_payload_size": 70}, <br>        "stz": 1584698900000, <br>        "etz": 1584699900000}<br>  &amp;timestamp=1584698900000</span></pre>
<h2 id="01H821RTQ6BNZHZNM8AHTV8BZP">Device Traces</h2>
<p>Sample device trace request:</p>
<pre><span>/i?app_key=xyz<br>  &amp;device_id=pts911<br>  &amp;apm={"type":"device",<br>        "name":"</span><span>app_start</span><span>",<br>        "apm_metrics":{"duration": 15000}, <br>        "stz": 1584698900, <br>        "etz": 1584699900}<br>  &amp;timestamp=1584698900</span></pre>
<p>&nbsp;</p>
<h1 id="01H821RTQ72HHY8E4AD9NCYE8E">User Consent</h1>
<p>
  <span>GDPR compatibility is about dividing the SDK functionality into different features and allowing SDK integrators to ask for consent when using these features. Once consent has been given, the SDK may only send newly collected (after consent is given) data to the server.</span>
</p>
<p>
  <span>Additionally, the user may change his/her mind during the app run and opt-out of some features. Therefore, the SDK should be able to enable or disable these features on run time.</span>
</p>
<p>
  <span>Consent persistence is handled by the host app and not by the SDK. In exceptional circumstances (in cases it is needed) it is possible to handle some consent values persistently inside of the SDK.</span>
</p>
<p>
  <span>Consent management in the SDK is done in 2 steps<br></span><span></span>
</p>
<ol>
  <li>
    <span>consent has to first be required in the app otherwise, the SDK works as if all consent is given</span>
  </li>
  <li>
    <span>if consent is required, it has to explicitly be given for each targeted feature</span>
  </li>
</ol>
<h2 id="01H821RTQ7CS4N3G4Q9AXQC904">Initial Configuration</h2>
<p>
  During SDK init there should be a flag (e.g. <code>requiresConsent</code>) to
  inform the SDK that it requires consent before doing anything.
</p>
<p>
  <span>If this configuration is set, the SDK should not send any data to the server without consent. Even if specific SDK methods (reporting errors, recording events, etc.) are manually called, these calls should be ignored until consent is given.</span>
</p>
<p>
  <span>Init should also have a function to provide an array consent that is given during startup.</span>
</p>
<h2 id="01H821RTQ7K4X2AC3391381E95">Exposing Available Features for Consent</h2>
<p>
  <span>The SDK should expose all the features it supports for consent in the form of a method, static properties, or constant strings. The developer may check which features are available during development or when creating a consent form UI.&nbsp;</span>
</p>
<p>
  Developers shouldn't have to write the consent feature strings themself. They
  should be provided either as constants or even as enums thereby eliminating the
  need for strings.
</p>
<p>
  <span>The following are the currently available features: </span>
</p>
<ul>
  <li>
    <code>sessions</code> -
    <span>tracking when, how often, and how long users use your app/website</span>
  </li>
  <li>
    <code>events</code> -
    <span>allow events to be sent to the server (doesn't apply to other features using event mechanisms)</span>
  </li>
  <li>
    <code>location</code> -&nbsp;<span>allows location information to be sent. If consent has not been given, the SDK should force send an empty location upon <code>begin_session</code></span><span>to prevent the server from determining location via IP addresses</span>
  </li>
  <li>
    <code>views</code> -
    <span>allow tracking of which views/pages a user visits</span>
  </li>
  <li>
    <code>scrolls</code> -
    <span>allow user scrolls for scroll heatmap to be tracked</span>
  </li>
  <li>
    <code>clicks</code> -
    <span>allow user clicks for heatmaps as well as link clicks to be tracked</span>
  </li>
  <li>
    <code>forms</code> -
    <span>allow user's form submissions to be tracked</span>
  </li>
  <li>
    <code>crashes</code> -
    <span>allow crashes, exceptions, and errors to be tracked</span>
  </li>
  <li>
    <code>attribution</code> -
    <span>allows the campaign from which a user came to be tracked</span>
  </li>
  <li>
    <code>users</code> -
    <span>allow collecting/providing user information, including custom properties</span>
  </li>
  <li>
    <code>push</code> - allows push notifications
  </li>
  <li>
    <code>star-rating</code> -
    <span>allows their rating and feedback to be sent</span>
  </li>
  <li>
    <code>accessory-devices</code> -
    <span>allow accessories or wearable devices, such as Apple Watches, etc. to be detected</span>
  </li>
  <li>
    <code>apm</code> -
    <span>allows usage of application performance monitoring features</span>
  </li>
  <li>
    <code>remote-config</code> -
    <span>allows downloading of remote configs from the server</span>
  </li>
  <li>
    <span><code>feedback</code>- allows showing things like surveys and NPS</span>
  </li>
</ul>
<p>
  <span>Note that the available features may change depending on the platform.</span>
</p>
<h2 id="01H821RTQ78JF1ANB1K482NQE0">Feature Grouping (optional)</h2>
<p>
  <span>The SDK may also provide feature grouping, allowing existing features to be put into groups and the use of these groups to give, cancel, and check consent.</span>
</p>
<p>
  <span>For example, a client may put "sessions", "events," and "views" into one group called "activity". After which, they give their consent to "activity", the SDK should then automatically give consent to all underlying features.</span>
</p>
<pre><code class="javascript">Countly.group_features({
    activity:["sessions","events","views"],
    interaction:["scrolls","clicks","forms"]
});</code></pre>
<h2 id="01H821RTQ715V2V2RKC9SYBFYE">Giving Consent</h2>
<p>
  <span>The SDK initial consent should be sent through the config object.</span>
</p>
<p>
  <span>After init there </span><span>should be a method for giving consent. This method should have feature names or groups as parameters. It may accept a single feature or group as well as multiple features or groups in the form of an array or variable arguments, depending on the SDK language and environment.</span>
</p>
<p>
  <span>At any time during the app run, a user may give consent to more features after starting the SDK.</span>
</p>
<p>
  Upon receiving consent (also during init), the SDK should immediately begin collecting
  data allowed by the provided feature(s) and also begin sending the consent approval
  to the server in the form of <code>consent=&nbsp;{"feature":true}</code>. For
  the exact feature names, refer to the list above.
</p>
<p>
  When consent is given, the update request should sent the current state of consent
  values and not only the given "delta". This may be a separate request, or it
  may be attached to any other SDK request.
</p>
<p>
  <span>If someone attempts to give consent for a second time, the SDK should ignore it as the consent is already given and nothing changes.</span>
</p>
<h2 id="01H821RTQ7XHKNWRBHN0ZW49N9">Checking Consent Status</h2>
<p>
  <span>There should also be a method to check the current consent status for the SDK, returning true if consent was given, and false if not. Checking status for groups should return <code>true</code>&nbsp;</span><span>only if all the underlying features return true.</span>
</p>
<p>
  <span>This check should also return <code>true</code> if consent is not required.</span>
</p>
<h2 id="01H821RTQ7AM6MBCDYTFAZ0HK4">Removing Consent</h2>
<p>
  <span>The SDK also needs to provide a method to remove consents. It should support the same parameter options as the consent giving method.</span>
</p>
<p>
  <span>Upon receiving the request to remove consent, the SDK should immediately stop collecting data allowed by the provided feature(s) and also send consent removal to the server in the form of <code>consent=&nbsp;{"feature":false}</code></span>
  <span>. </span>
</p>
<p>
  When consent is removed, the update request should sent the current state of
  consent values and not only the given "delta". This may be a separate request,
  or it may be attached to any other SDK request.
</p>
<p>
  <span>Depending on the SDK structure, the SDK may sync existing requests in the queue. Or, it may ignore requests in the queue and never send them or remove them from the queue.</span>
</p>
<p>
  <strong><span>Both giving consent and removing consent may be combined in a single request as well. If, for example, consent was given for crashes but removed from users, then the request should contain&nbsp;</span>consent={"crashes":true,"users":false}</strong>.
</p>
<h2 id="01H821RTQ77ER5XPWMCADD7NFX">Common Flow with Required Consent</h2>
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
  6)&nbsp;<span>The Countly SDK checks if <code>FeatureName</code></span><span>has already been passed to&nbsp;the <code>giveConsent</code></span><span>&nbsp;method, and it ignores all repetitive calls.</span>
</p>
<p>
  7)&nbsp;<span>The Countly SDK does not persistently store the status of given consents and expects the developer to call the&nbsp;</span><span>giveConsent</span><span>&nbsp;method on each app launch, just as with starting the SDK.</span>
</p>
<p>
  8)&nbsp;<span>If the app user changes his/her mind about consents at a later time, the developer may reflect this to the Countly SDK using the <code>removeConsent</code></span><span>method, passing feature names or groups.</span>
</p>
<p>
  9)&nbsp;<span>The Countly SDK stops the relevant features and also sends a request to the Countly Server (<code>consent={"feature":false}</code></span><span>).</span>
</p>
<p>
  10)&nbsp;<span>The Countly SDK checks if feature names or groups have already been passed to the <code>removeConsent</code></span><span>&nbsp;method, and it ignores all repetitive calls. Or, it attempts to cancel consents never given at all.</span>
</p>
<h1 id="01H821RTQ7SM8P0181NDD3MSZV">Security and Privacy</h1>
<h2 id="01H821RTQ7RN8GPAY3305Q19XS">Parameter Tampering</h2>
<p>
  <span>This is one of the preventive measures of Countly. If someone in the middle intercepts the request, it would be possible to change the data in the request and make another request with other data to the server or simply make random requests to the server through the retrieved <code>app_key</code></span><span>.</span>
</p>
<p>
  <span>To prevent this from happening, the SDK should provide the option to send a checksum alongside the request data. To do so, it should be possible for the developer to provide some random string as SALT to the SDK as parameters or configuration options.</span>
</p>
<p>
  <span>If this SALT is provided, right before making the request, the SDK should take all the payload it is about to send (all the data after the ‘?’ symbol in GET requests, including the app_key and device_id or query string encoded body of POST requests) and make a sha256 hash of this data. You should also provide SALT, and append it as checksum256={hash}.</span>
</p>
<pre><code class="javascript">if(salt){
  data += "&amp;checksum256=" + sha256Hash(data + salt);
}</code></pre>
<p>
  <span>If SALT is not provided, the SDK should make ordinary requests without any checksums.</span>
</p>
<h1 id="01H821RTQ7GNGHSMJGP10YQXWZ">Other Features</h1>
<h2 id="01H821RTQ7QP861SSC3JS3V236">Attribution</h2>
<p>
  Attribution allows attributing installs from specific campaigns.
</p>
<p>
  There are 2 forms of attribution: directAttribution and indirectAttribution.
</p>
<p>
  There should be a way to provide them during init and there should be a way to
  provide them after init.
</p>
<p>
  These values should be sent when they are provided in a separate request.
</p>
<p>This requires attribution consent.</p>
<h3 id="01H821RTQ74RBDQVEDWMWWV9Z8">Direct Attribution</h3>
<p>
  With this the dev is able to provide 2 String values: "Campaign type" and "Campaign
  data". The "type" determines for what purpose the attribution data is provided.
  Depending on the type, the expected data will differ, but usually that will be
  a string representation of a json object.
</p>
<p>
  Currently there is only one type "countly". That type expected the data to look
  like following: '<span>{cid:"[PROVIDED_CAMPAIGN_ID]", cuid:"[PROVIDED_CAMPAIGN_USER_ID]"}'. The inserted values would be retrieved from install attribution.</span>
</p>
<p>
  This feature is currently setup in a way to give more flexibility in the future.
  For now it will be only possible to record install attribution by handling twp
  special cases. In the future this feature will be generalised and a new param
  will be added.
</p>
<p>
  If the provided type is "countly" then the first special case will be executed.
  The data string is an stringified json that has 2 values "cid" or Campaign ID
  and "cuid" or Campaign user ID.
</p>
<p>Non valid or empty string should produce an error log.</p>
<p>
  The "Campaign ID" value is mandatory. If this has no valid value, an error log
  should be printed and execution should be aborted.
</p>
<p>
  The "Campaign user ID" value is optional and if it is missing or invalid, only
  the "Campaign ID" value should be sent.
</p>
<p>
  The call to record this value should be named something similar to "recordDirectAttribution".
</p>
<p>The param for the campaign ID should be added as:</p>
<pre><span>"&amp;campaign_id=[PROVIDED_CAMPAIGN_ID]"</span></pre>
<p>The param for the campaign user ID should be added as:</p>
<pre><span>"&amp;campaign_user=[PROVIDED_CAMPAIGN_USER_ID]"</span></pre>
<p>
  If the provided type is "_special_test" then the second special case will be
  executed. If the provided data is not null or empty then it will be processed.&nbsp;
</p>
<p>
  A request will be created. The provided value should be HTTP encoded and then
  set to the parameter "attribution_data" and then sent.
</p>
<pre>"&amp;<span>attribution_data=[ENCODED_CAMPAIGN_DATA]"</span></pre>
<h3 id="01H821RTQ7Z09FDXQE62YBGFVC">Indirect Attribution</h3>
<p>
  With this the dev is able to provide a map/dictionary of String to String values.
  This allows multiple values to be provided.
</p>
<p>
  Common values that would be provided here would be IDFA (for iOS) and AdvertisingId
  (for Android).
</p>
<p>
  Each usable value will have a predefined key that has to be used. IDFA will need
  to be provided with the "idfa" key and Advertising ID will need to be provided
  with the "adid" key. These keys have to the be provided by the SDK as "constant"
  variables or some other convenient way where the developer is not setting the
  final key manually.
</p>
<p>
  The pseudo code for recording indirect attribution would look something like
  this:
</p>
<pre><span>Map</span>&lt;<span>String</span>, <span>String</span>&gt; <span>attributionValues </span>= <span>new </span>HashMap&lt;&gt;();<br><span>attributionValues</span>.put(<span>AttributionIndirectKey</span>.<span>AdvertisingID</span>, getAdvertisingID());<br><span>Countly</span>.recordIndirectAttribution(<span>attributionValues</span>);</pre>
<p>
  The map/dictionary with valid key-value pairs will then be transformed into a
  json object which will set to the "aid" param and then immedietelly sent to the
  server.
</p>
<p>
  Each key-value pair should be validated. If the key or value is either null,
  undefined or empty string, that key-value pair should be removed from the map/dictionary
  and an error message should be printed.
</p>
<p>
  It should not be validated if the provided keys are part of our officially supported
  ones ("idfa" and "adid" at the time of writing). Just that the keys and their
  values are legitamate values.
</p>
<p>
  If after the validation no valid value is left another error log should be printed
  and the execution of this call should not continue.
</p>
<p>
  The call to record this value should be named something similar to "recordIndirectAttribution".
</p>
<p>The param in the request would look something like like:</p>
<pre><span>&amp;aid=</span><span>{</span><span>"</span><span>adid</span><span>"</span><span>:[PROVIDED_ATTRIBUTION_ID], "idfa":[PROVIDED_IDFA_VALUE]</span><span>}</span></pre>
<p>Or:</p>
<pre><span>&amp;aid=</span><span>{</span><span>"</span><span>adid</span><span>"</span><span>:[PROVIDED_ATTRIBUTION_ID]</span><span>}</span></pre>
<p>Or:</p>
<pre><span>&amp;aid=</span><span>{"idfa":[PROVIDED_IDFA_VALUE]</span><span>}</span></pre>
<p>Or:</p>
<pre><span>&amp;aid=</span><span>{"rndid":[SOME_OTHER_ID_VALUE]</span><span>}</span></pre>
<h2 id="01H821RTQ7AZ6J858BHP4883ZC">SDK Internal Limits</h2>
<p>The SDK should have the following limits:</p>
<ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
  <li data-stringify-indent="0">
    "<strong data-stringify-type="bold">maxKeyLength</strong>" - 128 chars
  </li>
</ul>
<p>
  <span>Limits the maximum size of all string keys.</span><br>
  <span>"Keys" include:</span><br>
  <span> - event names</span><br>
  <span> - view names</span><br>
  <span> - custom trace key name (APM)</span><br>
  <span> - custom metric key (APM)</span><br>
  <span> - segmentation key (for all features)</span><br>
  <span> - custom user property</span><br>
  <span> - custom user property keys that are used for property modifiers (mul, push, pull, set, increment, etc)</span>
</p>
<ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
  <li data-stringify-indent="0">
    "<strong data-stringify-type="bold">maxValueSize</strong>" - 256 chars
  </li>
</ul>
<p>
  <span>Limits the size of all values in our key-value pairs.</span><br>
  <span>"Value" fields include:</span><br>
  <span> - segmentation value in case of strings (for all features)</span><br>
  <span> - custom user property string value</span><br>
  <span> - user profile named key (username, email, etc) string values. Except the "picture" field, which has a limit of 4096 chars</span><br>
  <span> - custom user property modifier string values. For example, for modifiers like "push," "pull," "setOnce", etc.</span><br>
  <span> - breadcrumb text</span><br>
  <span> - manual feedback widget reporting fields (reported as an event)</span><br>
  <span> - rating widget response (reported as an event)<br></span>
</p>
<ul class="p-rich_text_list p-rich_text_list__bullet" data-stringify-type="unordered-list" data-indent="0">
  <li data-stringify-indent="0">
    "<strong data-stringify-type="bold">maxSegmentationValues</strong>" - 100
    developer-supplied entries
  </li>
</ul>
<p>
  <span>Max amount of custom (dev-provided) segmentation in:</span>
</p>
<p>
  <span>- Event segmentation</span>
</p>
<p>
  <span>- View segmentation</span>
</p>
<p>
  <span>- Global view segmentation</span>
</p>
<p>
  <span>- Custom (Global) crash segmentation</span>
</p>
<p>
  <span>- Crash segmentation</span>
</p>
<p>
  <span>- Custom APM Metrics</span>
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
  <span>limits how many characters are allowed per stack trace line. This also limits the crash message length.</span>
</p>
<p>
  <span> Besides those 2 exposed tweakable crash-related values, there would also be an internal one for "maxStackTraceThreadCount." Which would limit the maximum number of recorded threads by a default of 50. This would be mostly just a sanity check, as that has to be capped somehow. <span class="c-mrkdwn__br" data-stringify-type="paragraph-break"></span>In cases where stack traces can be provided as a string, the maximum line count would be 50*30 = 1500. That string would have to be split into lines and then checked accordingly.</span>
</p>
<p>
  Crash information like PLC crashes for iOS, and native Android crashes do not
  have any limits applied to them.
</p>
<h2 id="01H821RTQ8PWHE34M7R8RFAT3S">Changing the Server URL</h2>
<p>
  This feature adds the ability to change the server URL after the SDK is initialised.
</p>
<p>
  This should in memory overwrite the current URL. Basic URL validation should
  be performed on the provided URL.
</p>
<p>
  After the URL is changed, all previously saved events and requests should be
  sent to the new URL.
</p>
<h1 id="01H821RTQ8VNSA06563GDH4XKC">Markdown Linting</h1>
<p>
  To ensure the formatting of the code is uniform across all platforms, certain
  linting tools can be used. Currently for markdown files "markdownlint" would
  be used.
</p>
<h2 id="01H821RTQ8ZRB2WX665K2M5CCY">Installation</h2>
<p>
  You can add markdownlint to your project with the following line of code using
  the npm:
</p>
<p>
  <code>
npm install markdownlint --save-dev
</code>
</p>
<p>
  Another way to add it to your project would be to download its extension in VSC.
</p>
<h2 id="01H821RTQ8S380YYHHCXXAJ548">Rules</h2>
<p>
  Markdownlint, has multiple rules that can be modified/defined from a config file
  called ".markdownlint.json". This file must be created at the root of the project
  and should have a structure similar to this:
</p>
<pre><code>{<br>    "MD001": true, /*Heading levels should increase one at a time*/<br>    "MD002": false, /*First heading should be h1*/<br>    "MD003": true, /*Use only one heading style in a document*/<br>    "MD004": true, /*Only one unordered list style should be used*/<br>    "MD005": true, /*List items should have same indentation at same level*/<br>    "MD006": true, /*Top level list items should not be indented*/<br>    "MD007": { "indent": 2 }, /*Indent level as space*/<br>    "MD009": false, /*No white space at the end*/<br>    "MD010": false, /*No hard tab indentation*/<br>    "MD011": true, /*link syntax should not be reversed like (a)[a.com]*/<br>    "MD012": { "maximum": 1 }, /*No more than 1 blank line*/<br>    "MD013": { "line_length": 300 }, /*Max line length*/<br>    "MD014": false, /*Dollar sign should not be used consecutively for shell commands*/<br>    "MD018": true, /*There should be a space after heading hash*/<br>    "MD019": true, /**There should not be multiple spaces after heading hash*/<br>    "MD020": true, /*Closed atx style heading should have 1 space inside hashes*/<br>    "MD021": true, /*Closed atx style heading should note have multiple space inside hashes*/<br>    "MD022": false, /*Before and after a heading should be a blank line*/<br>    "MD023": true, /*Heading should not be indented*/<br>    "MD024": true, /*No duplicate sibling headings*/<br>    "MD025": true, /*Only one h1*/<br>    "MD026": true, /*No punctuation at the end of a heading except '?'*/<br>    "MD027": true, /*No more than 1 space after blockquote symbol*/<br>    "MD028": true, /*No separation of blockquotes with a blank line*/<br>    "MD029": true, /*Ordered list should be ordered and start with  or 1*/<br>    "MD030": true, /*Only one space between the list marker and text*/<br>    "MD031": true, /*Before and after a fenced code block should be a blank line*/<br>    "MD032": false, /*Before and after a list should be a blank line*/<br>    "MD033": false, /*No raw HTML*/<br>    "MD034": false, /*URL should be surrounded with brackets*/<br>    "MD035": true, /*No inconsistent horizontal rules; ---, *** */<br>    "MD036": true, /*No emphasis instead of heading*/<br>    "MD037": true, /*No space between emphasis market and the text*/<br>    "MD038": true, /*No space between backtick and text*/<br>    "MD039": true, /*No space inside link text*/<br>    "MD040": true, /*Fenced code blocks should have a language declared*/<br>    "MD041": false, /*First line in a file should be h1*/<br>    "MD042": true, /*No empty links*/<br>    "MD043": false, /*Declare a heading structure*/<br>    "MD044": true, /*Proper names should have the correct capitalization*/<br>    "MD045": true, /*Images should have alt text*/<br>    "MD046": true, /*Use indent or code fence alone*/<br>    "MD047": true, /*Files should end with a single newline character */<br>    "MD048": true, /*Code fence style should be uniform*/<br>    "MD049": true, /*Emphasis style should be consistent*/<br>    "MD050": true, /*Strong style should be consistent*/<br>    "MD051": true, /*Link fragments should correspond to a heading*/<br>    "MD052": true, /*Reference links and images should use a label that is defined*/<br>    "MD053": true /* Link and image reference definitions should be needed*/<br>}
</code></pre>
<p>
  To exclude certain files from being analyzed you can create a ".markdownlintignore"
  at the project root and add directories that you want to exclude from the analysis:
</p>
<pre><code>// to exclude node_modules folder<br>/node_modules/
</code></pre>
<h2 id="01H821RTQ8Y1HXSY2HDDK8AGD1">Usage</h2>
<p>
  Then you can add the following text to your npm scripts in your package.json
  file:
</p>
<p>
  <code>"lintMD": "markdownlint **/*.md --fix"</code>
</p>
<p>
  This way you can use the markdown linter with the following code at your project
  root:
</p>
<p>
  <code>npm run lintMD</code>
</p>
<p>
  Instead, if you have only installed the VSC extension you can simply right click
  on your markdown file and press 'Format Document' for ease of use. Or if you
  want to automatically format when saving or pasting into a Markdown document,
  configure Visual Studio Code's editor.formatOnSave or editor.formatOnPaste settings
  like so:
</p>
<p>
  <code>
"[markdown]": {
    "editor.formatOnSave": true,
    "editor.formatOnPaste": true
},
</code>
</p>
<h1 id="01H821RTQ83FE200Z8NARD5GCJ">Experimental</h1>
<p>
  This section describes features that are under development and in a prototype
  phase
</p>
<h2 id="h_01HPM01NK3F2VHHXJ07P53QF55">SDK Health Checks</h2>
<p>
  These are a collection of different metrics and helpers that would give better
  insight into the state of the SDK integration.
</p>
<h3 id="h_01HPM01NK3HSSW3XXSKYXRQR0B">Health Information with Instant Request</h3>
<p>
  During SDK operation, various metrics regarding its usage should be collected.
  Those collected metrics should then be periodically sent.
</p>
<p>
  The trigger for sending the collected metrics is the end of SDK initialization.
  At that point, the SDK should send overall health metrics collected since the
  last time the health metrics were successfully sent.
</p>
<p>
  Metrics should be stored persistently. Upon successful transmission, the stored
  metrics should be cleared.
</p>
<p>Metrics should be sent as an instant request.</p>
<p>There is no way to disable health checks.</p>
<p>
  The health check tracking, serialization, deserialization, etc., functionality
  should be contained within an independent module designed so it can be easily
  tested.
</p>
<p>
  Health metrics should not be saved after every change to a metric. They should
  be changed after the following triggers:
</p>
<ul>
  <li>Session update timer - for a periodic save</li>
  <li>
    Session ended - as a proxy that the app/page is about to be closed
  </li>
  <li>
    Any other platform mechanisms that would indicate that the app is about to
    be closed or killed
  </li>
</ul>
<p>
  Here is a list of metrics that need to be tracked. They are identified by the
  JSON key that should be used when sending these health metrics:
</p>
<ul dir="auto">
  <li>
    <p dir="auto">
      <strong>el</strong> (Integer) - The amount of error-level SDK logs triggered
    </p>
  </li>
  <li>
    <p dir="auto">
      <strong>wl</strong> (Integer) - The amount of warning-level SDK logs
      triggered&nbsp;
    </p>
  </li>
  <li>
    <p dir="auto">
      <strong>sc</strong> (Integer) - The status code of the last failed request&nbsp;
    </p>
  </li>
  <li>
    <p dir="auto">
      <strong>em</strong> (String) - The first 1000 characters of the response
      returned by the last failed request
    </p>
  </li>
  <li>
    <p dir="auto">
      <strong>bom</strong> (Integer) - The amount of backoff mechanism triggered
    </p>
  </li>
  <li>
    <p dir="auto">
      <strong>cbom</strong> (Integer) - The maximum amount of consecutive backoff
      mechanism triggered
    </p>
  </li>
</ul>
<p>
  The module should expose the following methods for tracking, saving, and creating
  the param:
</p>
<pre>//increments the "wl" counter
void logWarning()

//increment the "el" counter
void logError()

//update the "sc" and "em" values
void logFailedNetworkRequest(integer statusCode, string errorResponse)

//increment the "bom" counter
//increment the "cbom_counter" counter
// called when a request backed off excluding immediate requests
void logBackoffRequest()
  
//get max of "cbom, cbom_counter"
//reset "cbom_counter"
// called when a request not backed off excluding immediate requests
void logConsecutiveBackoffRequest()

//counters should be cleared, and the state should be saved
void clearAndSave()

//state should be saved
void saveState()
</pre>
<p>
  The health check request contains the base params, the regular metric param with
  only the app version, and the metric information under the "hc" param. The request
  should be sent to the "/i" endpoint. Health check metrics should be sent as a
  JSON. Each metric would be setting its key-value pair in there.
</p>
<pre><code>// the relevant parts:
https://countly.server/i?hc={"el":12,"wl": 22,"sc":300,"em": "some_error", "bom": 13, "cbom": 3 }&amp;metrics={app_version:2}...</code></pre>
<p>
  The request is considered sent successfully as per the regular SDK interpretations
  of success.
</p>
<h3 id="h_01HPM01NK3QJ1MPWC5WQFH9125">Request Parameters for Health Check</h3>
<p>
  This gives insight into how full is the request queue for the specific device.
</p>
<p>
  With every request sent, the SDK also adds a parameter showing how many requests
  are in the stored request queue.
</p>
<p>
  The integer value of this is set under the param "rr." This param is not stored
  in the RQ but is added just before sending the request:
</p>
<pre>// the relevant parts:
https://countly.server/*?...&amp;rr=23...</pre>
<p>
  If tamper protection (salting) is enabled, this parameter should also be included
  in the checksum calculation.
</p>
<h1 id="h_01JRT094QEGTG0BXBN2MTT82D7">Server Config</h1>
<p>
  SDK should provide a way for server to provide a configuration. This configuration
  can effect which internal limits are used and which features are allowed to work.
</p>
<p>
  Server UI URL for the UI (Management -&gt; SDK):<br>
  <a class="c-link" href="https://xxx.count.ly/dashboard#/manage/sdk/configurations" target="_blank" rel="noopener" data-stringify-link="https://xxx.count.ly/dashboard#/manage/sdk/configurations" data-sk="tooltip_parent">https://xxx.count.ly/dashboard#/manage/sdk/configurations</a>
</p>
<p>
  <strong>API Endpoint</strong>
</p>
<p>
  Server Example Endpoint:<br>
  <a class="c-link" href="https://xxx.count.ly/o/sdk?app_key=3d8b79s4fc4ba5f0bf9c182656c34b37d8d1b830d&amp;device_id=1&amp;method=sc" target="_blank" rel="noopener" data-stringify-link="https://xxx.count.ly/o/sdk?app_key=3d8bs94fc4ba5f0bf9c182656c34b37d8d1b830d&amp;device_id=1&amp;method=sc" data-sk="tooltip_parent">https://xxx.count.ly/o/sdk?app_key=123&amp;device_id=1&amp;method=sc</a>
</p>
<p>Server configuration response has the following format:</p>
<pre>{<br>"v": 1, <br>"t": 1742459739383,<br>"c": {<br>    "tracking": false,<br>    "networking": false,<br>    // ...<br>  }<br>}</pre>
<p>
  <span class="c-mrkdwn__br" aria-label="" data-stringify-type="paragraph-break"><strong>v</strong> - current schema version</span><br>
  <span class="c-mrkdwn__br" aria-label="" data-stringify-type="paragraph-break"><strong>t</strong> - timestamp (at the time of creation)</span><br>
  <span class="c-mrkdwn__br" aria-label="" data-stringify-type="paragraph-break"><strong>c</strong> - config object (key value pairs)</span>
</p>
<p>
  <strong>Behavior</strong>
</p>
<p>
  During init and every X hours SDK tries to acquire the config and stores it persistently
  locally.
</p>
<p>
  When initializing the SDK, if there is a persistent config stored, it will be
  used. The SDK will still try to get a up to date version of the config at the
  end of initialization. Once the up to date version has been acquired, it is stored
  persistently and the SDK reconfigures itself to reflect the new configuration.
  Summary of SDK side precedence of the config values will be:
</p>
<pre class="c-mrkdwn__pre" data-stringify-type="pre">SDK's Default &lt; Dev Set Config &lt; Dev Set Server Config &lt; Stored Server Config</pre>
<table dir="ltr" style="width: 548px; border-collapse: collapse; border: none;" border="1" cellspacing="0" cellpadding="0" data-sheets-root="1" data-sheets-baot="1">
  <colgroup>

    <col width="100">

    <col width="100">

    <col width="100">

    <col width="107">

  </colgroup>
  <tbody>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 327.125px;" colspan="3" rowspan="1">
        <strong>Init Time Status</strong>
      </td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 206.475px;">
        <strong>Initial Behavior</strong>
      </td>
    </tr>
    <tr style="height: 21px;">
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 91.8375px;">Stored SC</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 115.925px;">Provided SC</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 105.762px;">Temp ID</td>
      <td style="padding: 2px 3px; vertical-align: bottom; width: 206.475px;">&nbsp;</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 91.8375px;">●</td>
      <td style="padding: 2px 3px; vertical-align: bottom; width: 115.925px;">&nbsp;</td>
      <td style="padding: 2px 3px; vertical-align: bottom; width: 105.762px;">&nbsp;</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 206.475px;">Uses Stored SC</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 91.8375px;">●</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 115.925px;">●</td>
      <td style="padding: 2px 3px; vertical-align: bottom; width: 105.762px;">&nbsp;</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 206.475px;">Uses Stored SC</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 91.8375px;">●</td>
      <td style="padding: 2px 3px; vertical-align: bottom; width: 115.925px;">&nbsp;</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 105.762px;">●</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 206.475px;">Uses Stored SC</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 91.8375px;">●</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 115.925px;">●</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 105.762px;">●</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 206.475px;">Uses Stored SC</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 91.8375px;">&nbsp;</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 115.925px;">●</td>
      <td style="padding: 2px 3px; vertical-align: bottom; width: 105.762px;">&nbsp;</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 206.475px;">Uses Provided SC</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 91.8375px;">&nbsp;</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 115.925px;">●</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 105.762px;">●</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 206.475px;">Uses Provided SC</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 91.8375px;">&nbsp;</td>
      <td style="padding: 2px 3px; vertical-align: bottom; width: 115.925px;">&nbsp;</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 105.762px;">●</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 206.475px;">Uses User C</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 91.8375px;">&nbsp;</td>
      <td style="padding: 2px 3px; vertical-align: bottom; width: 115.925px;">&nbsp;</td>
      <td style="padding: 2px 3px; vertical-align: bottom; width: 105.762px;">&nbsp;</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 206.475px;">Uses User C</td>
    </tr>
  </tbody>
</table>
<p>
  After this initial behavior SDK should get the server config again to be up-to-date
  and save it. If that request fails or the config is invalid it should keep using
  what it has.
</p>
<p>
  <strong>Affected Options</strong>
</p>
<p>
  Server and SDK has default values for every config option keys.<br>
  If user changes a setting in server, response would include that option with
  new value. If no value is sent for a configuration (meaning <strong>c</strong>
  is empty), then that means that the SDK has to use its own default or the value
  provided by the developer.
</p>
<p>Server config keys and their default values are:</p>
<table dir="ltr" style="width: 579px; border-collapse: collapse; border: none; height: 506px;" border="1" cellspacing="0" cellpadding="0" data-sheets-root="1" data-sheets-baot="1">
  <colgroup>

    <col width="187">

    <col width="110">

    <col width="141">

  </colgroup>
  <tbody>
    <tr style="height: 21px;">
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">
        <strong>Feature Name</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">
        <strong>Key</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 179.35px; height: 22px;">
        <strong>Default Val</strong>
      </td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Allow all tracking</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">tracking</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">TRUE</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Allow sending requests</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">networking</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">TRUE</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Request queue size</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">rqs</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">1000 requests</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Event queue size (or batch)</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">eqs</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">100 events</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Session update interval</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">sui</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">60 seconds</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Allow session tracking</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">st</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">TRUE</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Allow crash tracking</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">crt</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">TRUE</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Allow location tracking</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">lt</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">TRUE</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Allow view tracking</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">vt</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">TRUE</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Key length limit</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">lkl</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">128 chars</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Value size limit</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">lvs</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">256 chars</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Segmentation values count limit</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">lsv</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">100 key/values</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Breadcrumb count limit</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">lbc</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">100 breadcrumbs</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Stack trace line count limit</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">ltlpt</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">30 lines</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Stack trace line length limit</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">ltl</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">200 chars</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Allow custom event tracking</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">cet</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">TRUE</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Enter Content Zone after init</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">ecz</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">FALSE</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Content Zone request interval</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">czi</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">30 seconds</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Consent required</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">cr</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">FALSE</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Server config update interval</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">scui</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">4 hours</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Allow Refresh Content Zone</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">rcz</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">TRUE</td>
    </tr>
    <tr style="height: 21px;">
      <td style="padding: 2px 3px; vertical-align: bottom; width: 240.05px; height: 22px;">Drop old request time</td>
      <td class="wysiwyg-text-align-center" style="padding: 2px 3px; vertical-align: bottom; width: 138.4px; height: 22px;">dort</td>
      <td style="padding: 2px 3px; vertical-align: bottom; text-align: center; width: 179.35px; height: 22px;">0 (disabled)</td>
    </tr>
  </tbody>
</table>
<h1 id="01H821RTQ8E32MD3GHXYVV4WCZ">Legacy Features</h1>
<h2 id="01H821RTQ8R9M4X5A2XA17HH61">Remote Config (Legacy)</h2>
<p>
  <span>First off, interaction with the Countly Server for the Remote Config feature should be done after you have checked the available API information. The </span><a href="https://api.count.ly/reference/osdk"><span>Remote Config API documentation</span></a><span> for legacy remote config API</span>
  includes information about an earlier implementation. This legacy API uses 'method=fetch_remote_config'
  inside the request URL while fetching the remote config object <em>and</em> enrolling
  the user to A/B testing automatically.
</p>
<p>
  The latest API, on the other hand, fetches the remote config object while giving
  us the ability to enroll the user in the A/B testing or not. This can be done
  by utilizing 'method=rc' and 'oi=1'(opting in/enrolling the user) or 'oi=0'(opting
  out/not enrolling the user) in the request URL.
</p>
<p>
  There is also another API that is used for enrolling the user to A/B testing
  for the selected remote config keys without fetching the remote config object.
  This can be done by using the 'method=ab' in your request URL.
</p>
<p>Their usage can be seen below:</p>
<pre><code>// legacy API
o/sdk?method=fetch_remote_config&amp;metrics=...&amp;app_key=app_key&amp;device_id=device_id...(optional params: keys, omit_keys)

// latest API for remote config
o/sdk?method=rc&amp;metrics=...&amp;app_key=app_key&amp;device_id=device_id...(optional params: keys, omit_keys, oi)

// enrolling users
o/sdk?method=ab&amp;keys=...&amp;app_key=app_key&amp;device_id=device_id
</code></pre>
<p>
  There are currently 2 init time config flag associated with these APIs:
  <em>rcAutoOptinAb</em> (true by default) and <em>useExplicitRcApi</em> (false
  by default). These flags enable users to change between APIs and control the
  A/B testing enrolling process. <em>useExplicitRcApi</em> lets the user use the
  latest API if it is set to true. <em>rcAutoOptinAb</em> decides if auto enrolling
  (oi=1) must be on or not (oi=1) when using the latest API. Setting it to false
  should automatically trigger the usage of the latest API and should log a warning
  to the user.
</p>
<h2 id="01H821RTQ843R82K27AE6V09V9">Automatic Fetch</h2>
<p>
  <span>The Remote Config feature allows app developers to change the behavior and appearance of their applications at any time by creating or updating custom key-value pairs on the Countly Server.</span>
</p>
<p>
  <span>There should be a flag upon initial config to enable the automatic fetching of the remote config upon SDK start. If this flag is set, the SDK will automatically fetch the remote config from the server and store it locally. A locally stored remote config should reflect the server response as is, overwriting any existing remote config. No merging or partial updating. Automatic fetching will be performed only upon SDK start, not with every begin session. There should also be a callback on the initial config to inform the developer about the results of automatic fetching the remote config.</span>
</p>
<p>
  e.g. <code>config.enableRemoteConfig = true;</code>
</p>
<h2 id="01H821RTQ8QMZHEBPQTH1TEENH">Manual Fetch</h2>
<p>
  <span>There should be a method/function to fetch the remote config manually anytime the developer would like. Just like with automatic fetch, this method will fetch the remote config from the server and store it locally. A locally stored remote config should reflect the server response as is, overwriting any existing remote config. No merging or partial updating. This method should take a callback argument to inform the developer about the results of manually fetching the remote config. Callback on initial config should not be affected by manual fetchings, as it is for automatic fetchings only.</span>
</p>
<p>
  e.g. <code>updateRemoteConfig(callback(){ })</code>
</p>
<h2 id="01H821RTQ8PZJWW6459JAM8D6W">Getting Values</h2>
<p>
  <span>There should be a method to get remote config values for a given key. It will return the value for a given key. If the key does not exist, or the remote config has yet to be fetched, this method should return nil or null or however the platform handles the absence of values. If the server is not reachable, this method should return the last fetched and locally stored value if available.</span>
</p>
<p>
  e.g. <code>remoteConfigValueForKey(key)</code>
</p>
<h2 id="01H821RTQ822HR5EB6F9TYDR0T">Keys and Omit Keys</h2>
<p>
  <span>There should be 2 additional methods for manual fetching: one for specifying which keys will be updated and one for specifying which keys will be ignored.</span>
</p>
<p>
  <span>These methods should take an array of keys as an argument, in addition to callbacks, and send requests with <code>keys=</code></span><span>&nbsp;or <code>omit_keys=</code></span><span>&nbsp;query strings. For the result of these requests, only the keys in the response should be updated in local storage, not a complete overwrite as with an automatic or standard manual fetch.</span>
</p>
<p>
  e.g. <code>updateRemoteConfigForKeysOnly(keys, callback(){ })</code> e.g.
  <code>updateRemoteConfigExceptKeys(keys, callback(){ })</code>
</p>
<p>
  <span>Example case: Local storage reflecting server as is (after an automatic or manual fetch):</span>
</p>
<pre><code>{
  "a": "x",
  "b": "y",
  "c": "z",
}</code></pre>
<p>
  <span>Calling update for specified keys only:</span>
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
<h2 id="01H821RTQ8H0HJ4EBGMH3XX2FB">A/B Testing</h2>
<p>
  There should be a call to enroll users in the A/B testing without triggering
  any other action. This call should be named something similar to
  <em>enrollUserToAb</em> and should have one parameter named <em>keys</em>. This
  parameter should be an array of string key values. If an empty array or no value
  at all is provided the function should be terminated and should give an error
  log to the developer. Else the <em>keys</em> should be stringified and added
  to the request as 'keys=stringified_values_here'. The response can be parsed
  and put out as a log. If all is good the response's result field should return
  something like "Successfully enrolled the user to given keys".
</p>
<h2 id="01H821RTQ8VYEGXZA4K0QJ6Q5R">Consents</h2>
<p>
  <span>In case where the <code>consentRequired</code>flag is set upon initial config, remote config actions should only be executed if the "remote-config" consent is given. Additionally, if <code>sessions</code>&nbsp;consent is given, the remote config requests will have <code>metrics</code>&nbsp;</span><span>info, similar to begin session requests.</span>
</p>
<h2 id="01H821RTQ8QPZMM69K8HYBPQW7">Device ID Change</h2>
<p>
  <span>After a device ID change, the locally stored remote config should be cleaned, and an automatic fetch should be performed if enabled upon initial config.</span>
</p>
<h2 id="01H821RTQ8P17JFY9MQTQP11AG">Salt</h2>
<p>
  <span>Remote config requests need to include the checksum if enabled upon initial config. As with all other requests, only the query string part will be used to calculate hash.</span>
</p>