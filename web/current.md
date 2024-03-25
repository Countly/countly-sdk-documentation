<p>
  <span style="font-weight: 400;">This documentation shows how to install the Countly Web SDK and use it to track your web page in detail. It applies to the SDK version 23.12.X.</span>
</p>
<div class="callout callout--info">
  <p>
    Click
    <a href="https://support.count.ly/hc/en-us/articles/360037236571-Downloading-and-Installing-SDKs#web-sdk" target="_self" rel="undefined">here, </a>to
    access the documentation for older SDK versions.
  </p>
</div>
<p>
  Countly can run with all browsers that supports ECMAScript 5. Minimum versions
  of major internet browsers that fully support ES5 are:
</p>
<table style="border-collapse: collapse; height: 46px; padding: 2px; margin-right: auto; margin-left: auto;" border="1" cellspacing="2" cellpadding="2">
  <tbody>
    <tr class="wysiwyg-text-align-center" style="height: 36px;">
      <td class="wysiwyg-text-align-center" style="width: 28.9867%; height: 36px;">
        <strong>IE</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 1.5528%; height: 36px;">
        <strong>Edge</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 9.68603%; height: 36px;">
        <strong>Firefox</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 5.29042%; height: 36px;">
        <strong>Firefox (Android)</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10%; height: 36px;">
        <strong>Opera</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10%; height: 36px;">
        <strong>Opera (Mobile)</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10%; height: 36px;">
        <strong>Safari</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10%; height: 36px;">
        <strong>Safari (iOS)</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 10%; height: 36px; text-align: center; vertical-align: middle;">
        <strong>Chrome</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 22.4019%; height: 36px;">
        <strong>Chrome (Android)</strong>
      </td>
    </tr>
    <tr style="height: 22px; padding: 2px;">
      <td class="wysiwyg-text-align-center" style="width: 28.9867%; height: 10px;">10</td>
      <td class="wysiwyg-text-align-center" style="width: 1.5528%; height: 10px;">12</td>
      <td class="wysiwyg-text-align-center" style="width: 9.68603%; height: 10px;">21</td>
      <td class="wysiwyg-text-align-center" style="width: 5.29042%; height: 10px;">96</td>
      <td class="wysiwyg-text-align-center" style="width: 10%; height: 10px;">15</td>
      <td class="wysiwyg-text-align-center" style="width: 10%; height: 10px;">64</td>
      <td class="wysiwyg-text-align-center" style="width: 10%; height: 10px;">6</td>
      <td class="wysiwyg-text-align-center" style="width: 10%; height: 10px;">6</td>
      <td class="wysiwyg-text-align-center" style="width: 10%; height: 10px;">23</td>
      <td class="wysiwyg-text-align-center" style="width: 22.4019%; height: 10px;">98</td>
    </tr>
  </tbody>
</table>
<p>
  If you want to get the Countly Web SDK codebase locally you can go to the GitHub
  repo <a href="https://github.com/Countly/countly-sdk-web">here</a> and download
  it inside your project folder by executing the lines:
</p>
<pre><code class="javascript">git clone https://github.com/Countly/countly-sdk-web.git
</code></pre>
<p>
  Additionally to see example integrations of Countly Web SDK within some popular
  front-end frameworks, you can reach our AngularJS and ReactJS examples from
  <a href="https://github.com/Countly/countly-sdk-web/tree/master/examples/Angular">here</a>
  and
  <a href="https://github.com/Countly/countly-sdk-web/tree/master/examples/react">here</a>
  respectively.
</p>
<h1 id="h_01HABTQ436ACJV96Q5P2MMNGWZ">Adding the SDK to the Project</h1>
<p>
  <span style="font-weight: 400;">To track your web pages, you will need the Countly Web SDK (also known as the Countly JavaScript tracking library). It is automatically hosted on your Countly server as a minified UMD file (at </span><a href="http://yourdomain.com/sdk/web/countly.min.js)"><span style="font-weight: 400;">http://yourdomain.com/sdk/web/countly.min.js)</span></a><span style="font-weight: 400;"> and can be updated via the command line. This library also works well with mobile applications that consist of HTML5 views.</span>
</p>
<p>
  <span style="font-weight: 400;">Optionally, you may also use package managers to gain access to the SDK:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">npm</span>
    <span class="tabs-link">yarn</span>
  </div>
  <div class="tab">
    <pre><code class="shell">npm install countly-sdk-web</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="shell">yarn add countly-sdk-web</code></pre>
  </div>
</div>
<p>You can also reach the SDK through CDN:</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Latest</span>
    <span class="tabs-link">Specific Version</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">// latest non minified
<a href="https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.js" target="_blank" rel="noopener noreferrer">countly.js</a>

// latest minified
<a href="https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.min.js" target="_blank" rel="noopener noreferrer">countly.min.js</a></code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">// 23.6.0 non minified
<a href="https://cdn.jsdelivr.net/npm/countly-sdk-web@23.6.0/lib/countly.js" target="_blank" rel="noopener noreferrer">countly.js</a>

// 23.6.0 minified (<span>JSDelivr&nbsp;</span>or Cloudflare)
<a href="https://cdn.jsdelivr.net/npm/countly-sdk-web@23.6.0/lib/countly.min.js" target="_blank" rel="noopener noreferrer">countly.min.js</a> or <a href="https://cdnjs.cloudflare.com/ajax/libs/countly-sdk-web/23.6.0/countly.min.js" target="_blank" rel="noopener noreferrer">countly.min.js</a></code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Lastly as an alternative option, you may download <a href="https://github.com/Countly/countly-sdk-web/tree/master/lib">countly.min.js</a> from our GitHub repository and upload it to any server from where you would like to host it.</span>
</p>
<h1 id="h_01HABTQ436KQ0HD0G5NXFBZQR7">SDK Integration</h1>
<h2 id="h_01HABTQ4360WX3SY413Z3ZSAWZ">Minimal Setup</h2>
<p>
  <span style="font-weight: 400;">You may use the Countly Web SDK synchronously or asynchronously. However the asynchronous usage would benefit from working without blocking content loading. This would also allow you to use Countly while the Countly script has not yet been loaded. This can be done by pushing function calls into the </span><strong>Countly.q</strong><span style="font-weight: 400;"> queue.</span>
</p>
<p>
  <span style="font-weight: 400;">Inserting asynchronous code before closing the "<a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head" target="_blank" rel="noopener noreferrer">head tags</a>" of your website is suggested, while Synchronous code should be added towards the bottom of the page before closing the head tag. Main logic here is to make the Countly load as soon as possible to start collecting data.</span>
</p>
<p>
  Here you would also need to provide your application key and server URL. Please
  check
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#acquiring-your-application-key-and-server-url">here</a>
  for more information on how to acquire your application key (APP_KEY) and server
  URL.
</p>
<p>
  <span style="font-weight: 400;">An example setup would look like this:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="html">&lt;script type='text/javascript'&gt;
  
// Some default pre init
var Countly = Countly || {};
Countly.q = Countly.q || [];

// Provide your app key that you retrieved from Countly dashboard
Countly.app_key = "YOUR_APP_KEY";

// Provide your server IP or name.
// If you use your own server, make sure you have https enabled if you use
// https below.
Countly.url = "https://yourdomain.com";

// Start pushing function calls to queue
// Track sessions automatically (recommended)
Countly.q.push(['track_sessions']);

//track web page views automatically (recommended)
Countly.q.push(['track_pageview']);

// Load Countly script asynchronously
(function() {
var cly = document.createElement('script'); cly.type = 'text/javascript';
cly.async = true;
// Enter URL of script here (see below for other option)
cly.src = 'https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.min.js';
cly.onload = function(){Countly.init()};
var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(cly, s);
})();
&lt;/script&gt;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="html">&lt;!--Countly script--&gt;
&lt;script type='text/javascript' src='https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.min.js'&gt;&lt;/script&gt;
&lt;script type='text/javascript'&gt;

Countly.init({
// provide your app key that you retrieved from Countly dashboard
app_key: "YOUR_APP_KEY",

// Provide your server IP or name.
// If you use your own server, make sure you have https enabled if you use
// https below.  
 url: "http://yourdomain.com"

});
// track sessions automatically
Countly.track_sessions();
// track pageviews automatically
Countly.track_pageview();
&lt;/script&gt;</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">In the above-mentioned example, we used JSDelivr to retrieve the Countly JS SDK. As</span><span style="font-weight: 400;"> an alternative, you may also use one of the methods mentioned at the previous section.</span>
</p>
<p>
  <span style="font-weight: 400;">If </span>you are in doubt about the correctness
  of your Countly SDK integration you can learn about the verification methods
  from
  <a style="background-color: #ffffff;" href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#how-to-validate-your-countly-integration" target="blank">here</a>.
</p>
<h1 id="h_01HABTQ437271440T3QZN3DCSN">SDK Logging</h1>
<p>
  The first thing you should do while integrating our SDK is enabling logging.
  If logging is enabled, then our SDK will print out debug messages about its internal
  state and encountered problems.
</p>
<p>
  Set debug option to true at the Countly initialization to enable logging:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="html">//during initialization
Countly.debug = true;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="html">Countly.init({
    debug:true,
    app_key:"YOUR_APP_KEY",
    url: "https://try.count.ly",
});</code></pre>
  </div>
</div>
<p>
  For more information on where to find the SDK logs you can check the documentation
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#finding-sdk-logs" target="blank">here</a>.
</p>
<h1 id="h_01HABTQ4378NGJPGEYQX8X1CWZ">Crash Reporting</h1>
<p>
  <span style="font-weight: 400;">Countly also provides a way for tracking JavaScript errors on your websites.</span>
</p>
<p>
  <span style="font-weight: 400;">Select the following function to automatically capture and report JavaScript errors on your website:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['track_errors'])</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.track_errors()</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Additionally, you may add more segments or properties/values to track with error reports by providing an object with a key/values to add to the error reports.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['track_errors', {
  "facebook_sdk": "2.3",
  "jquery": "1.8"
}])</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.track_errors({
  "facebook_sdk": "2.3",
  "jquery": "1.8"
})</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Apart from automatically reporting unhandled errors, you may also report handled exceptions to the server, so you may figure out how to handle them later on (or if you even need to figure out how to handle them later on). Optionally, you may once again provide the custom segments to be used in the report (or use the ones provided with the&nbsp;<strong>track_error</strong>&nbsp;method as default ones).</span>
</p>
<p>
  <strong>Countly.log_error (error, segments):</strong>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">try{
  //do something here
}
catch(ex){
  //report error to Countly
  Countly.q.push(['log_error', ex]);
}</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">try{
  //do something here
}
catch(ex){
  //report error to Countly
  Countly.log_error(ex);
}</code></pre>
  </div>
</div>
<p>
  For fatal errors you can use recordError function which takes three parameters;
  first, an error object with a stack key that has the error message value, second,
  a boolean which is false to indicate the fatality of the error and lastly segments
  object (optional) for custom crash segments for any extra information that you
  want to deliver with custom key value pairs. You can use this same function for
  nonfatal errors too by just setting the boolean value to true.
</p>
<p>
  <strong>Countly.recordError(error, nonFatal, segments):</strong>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">
  const error = {stack: 'Your error message here'};
  //report fatal error to Countly
  Countly.q.push(['recordError', error, nonFatal, segments]);
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">
  const error = {stack: 'Your error message here'};
  //report fatal error to Countly
  Countly.recordError(error, nonFatal, segments);
</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">To better understand what your users did prior to receiving an error, you may leave breadcrumbs throughout the code on different user actions. These breadcrumbs will then be combined in a single log and reported to the server as well.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['add_log', "user clicked button a"]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.add_log("user clicked button a");</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ437TVKP94G5W0AEPC3S">Symbolication</h2>
<div class="callout callout--warning">
  <p>
    Crash symbolication is available for
    <a href="https://count.ly/enterprise-edition">Enterprise Edition</a> users.
  </p>
</div>
<p>
  If the js files you serve are minified, transpiled or otherwise processed from
  your source files, you can use symbolication. With symbolication, your stacktraces
  will correctly point to the lines on the source files, which will help your developers
  debug crashes and errors. Here's an example:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">JS Symbolication input sample</span>
    <span class="tabs-link">JS Symbolication output sample</span>
  </div>
  <div class="tab">
    <pre><code class="JS Symbolication input sample">ReferenceError: undefined_function is not defined
    at r (file:///home/atak/Work/Countly/sample-app/dist/main.js:2:140)
    at HTMLButtonElement.document.getElementById.onclick (file:///home/atak/Work/Countly/sample-app/dist/main.js:2:521)</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="JS Symbolication output sample">ReferenceError: undefined_function is not defined
    at undefined_function (src/index.js:30:4)
    at cause_error (src/index.js:37:10)</code></pre>
  </div>
</div>
<p>
  There are a number of JavaScript build tools and countless way to configure them
  so laying out the steps for producing a source map file for each one would take
  quite a while. We will focus on webpack for brevity and simplicity.
</p>
<p>
  When using webpack configuration, the
  <a href="https://webpack.js.org/configuration/devtool/" target="_blank" rel="noopener">devtool</a>
  option to generate project source maps, keep in mind that options used to attain
  more verbose information might take longer to build. You must choose an option
  that generates the source map as a separate file and not inline with the final
  js file. After setting this, your builds will produce a source map file ending
  in <code>.map</code>, which is the source map file you will upload to your Countly
  server.
</p>
<p>
  To start symbolicating your errors you just need to upload your source map file
  to your Countly instance via the side menu &gt; Improve &gt; Errors &gt; Manage
  Symbols. In this view, the source map files you have uploaded are listed. To
  upload one, you click the "Add Debug Symbol File", fill the symbol type and app
  version fields accordingly and upload your <code>.map</code> file. With your
  source map file uploaded, you can symbolicate the crash reports for that app
  version on Countly. For more information, see
  <a href="https://support.count.ly/hc/en-us/articles/360037261472-Crash-symbolication" target="_self">Crash Symbolication</a>
  documentation.
</p>
<h1 id="h_01HABTQ4372X2H7D62SXF5ZW8R">Events</h1>
<h2 id="h_01HABTQ4372MVVDDTW1FWVFJXF">Adding an Event</h2>
<p>
  <span style="font-weight: 400;">Events are a way to track any custom actions or other data you would like to track from your website. You may also set segments to be able to view a breakdown of the action by providing the segment values.</span>
</p>
<div class="callout callout--warning">
  <p>
    All data passed to the Countly instance via the SDK or API should be in UTF-8.
  </p>
</div>
<p>An event consists of a JavaScript object with keys:</p>
<ul>
  <li>key - the name of the event (mandatory)</li>
  <li>count - number of events (default: 1)</li>
  <li>sum - sum to report with the event (optional)</li>
  <li>
    dur - duration expressed in seconds, meant for reporting with the event (optional)
  </li>
  <li>
    segmentation - an object with key/value pairs to report with the event as
    segments
  </li>
</ul>
<p>
  <span style="font-weight: 400;">Here is an example of adding an event with all possible properties:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['add_event',{
  "key": "click",
  "count": 1,
  "sum": 1.5,
  "dur": 30,
  "segmentation": {
    "key1": "value1",
    "key2": "value2"
  }
}]);</code></pre>
  </div>
  <div class="tab is-hidden">
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
  </div>
</div>
<h2 id="h_01HABTQ437SAGSADF72AW4XEM6">Timed Events</h2>
<p>
  All events contain an optional duration property that can be set manually or
  with the help of the Countly web SDK's convenience functions. There are three
  methods available to use to calculate the duration property: start_event, cancel_event,
  and end_event.
</p>
<p>
  The expected usage of these methods involves calling start_event for a specific
  event when it begins and then calling end_event to calculate the duration and
  create the event. In case you need to cancel a previously-called start_event,
  you can call cancel_event. However, it's important to note that these methods
  operate on the memory layer and shouldn't be used to calculate durations in situations
  where a browser restart occurs.
</p>
<p>
  The start_event method is used to initiate an internal timer within the SDK for
  a given event name. This timer works by taking the current timestamp and storing
  it in memory.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['start_event', 'timedEvent']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.start_event("timedEvent")</code></pre>
  </div>
</div>
<p>
  The cancel_event method erases the timestamp associated with a given event name
  if a start_event was previously called for that event.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['cancel_event', 'timedEvent']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.cancel_event("timedEvent")</code></pre>
  </div>
</div>
<p>
  The end_event method calculates the duration value for the given event name by
  finding the time difference between when the start_event was called and the current
  time. It then creates an event for the given name with the calculated duration
  and adds it to the event queue. You can also pass an event object to this method,
  and in that case, it will use the key value as the event name.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//end event
Countly.q.push(['end_event', 'timedEvent']);

//or end event with additional data
Countly.q.push(['end_event',{
"key": "timedEvent",
"count": 1,
"sum": 1.5,
"segmentation": {
"key1": "value1",
"key2": "value2"
}
}]);</code></pre>
  </div>
  <div class="tab is-hidden">
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
  </div>
</div>
<h1 id="h_01HABTQ437NA2XTXAMAXSQ9MD5">Sessions</h1>
<h2 id="h_01HABTQ437C35DZRN4C13RNA7K">Automatic Session Tracking</h2>
<p>
  <span style="font-weight: 400;">This method will automatically track user sessions by calling begin, extend, and end session methods.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['track_sessions']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.track_sessions();</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ437J7MQ9P10ES33VHHR">Manual Sessions</h2>
<p>
  <strong>Beginning a Session</strong>
</p>
<p>
  <span style="font-weight: 400;">This method would allow you to control sessions manually. Only use this method if you aren’t planning on calling the track_sessions method and set the&nbsp;</span><em><span style="font-weight: 400;">use_session_cookie</span></em><span style="font-weight: 400;">&nbsp;setting to false for more granular control of the session.</span>
</p>
<p>
  <span style="font-weight: 400;">If&nbsp;<strong>noHeartBeat</strong>&nbsp;is true, then the Countly Web SDK will not automatically extend the session, meaning you would be the one to do it automatically.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['begin_session']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.begin_session(noHeartBeat);</code></pre>
  </div>
</div>
<p>
  <strong>Extending a session</strong>
</p>
<p>
  <span style="font-weight: 400;">The Countly SDK will extend the session itself by default (if&nbsp;<strong>noHeartBeat</strong>&nbsp;was provided in the&nbsp;<strong>begin_session</strong>), but if you have not selected this option, you may then extend it using this method and provide the seconds since the last <strong>begin_session</strong>&nbsp;or&nbsp;<strong>session_duration</strong>&nbsp;call.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['session_duration', sec]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.session_duration(sec)</code></pre>
  </div>
</div>
<p>
  <strong>Ending a session</strong>
</p>
<p>
  <span style="font-weight: 400;">When a visitor is leaving your app or website, you should end their session with this method or by optionally providing the amount of seconds since the last&nbsp;<strong>begin session</strong>&nbsp;or&nbsp;<strong>session_duration</strong>&nbsp;calls, which ever came last.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['end_session']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.end_session(sec)</code></pre>
  </div>
</div>
<h1 id="h_01HABTQ437CAD08ESRK6RMJ2FG">View Tracking</h1>
<p>
  <span style="font-weight: 400;">This method will track the current pageview by using location.path as the page name and then reporting it to the server.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['track_pageview']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.track_pageview();</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">For Ajax updated contents and single page web applications, pass the page name as a parameter to record the new page view.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['track_pageview','pagename']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.track_pageview("pagename");</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Here is a good example if your single-page app uses URL hash.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['track_pageview',location.pathname+location.hash]);

$(window).on('hashchange', function() {
Countly.q.push(['track_pageview',location.pathname+location.hash]);
});</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.track_pageview(location.pathname+location.hash);

$(window).on('hashchange', function() {
Countly.track_pageview(location.pathname+location.hash);
});</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">In some cases, you might like to ignore some URLs to exclude from tracking, such as dynamic URLs that include the user ID in the URL, internal URLs, or for any other reason. You may do so by providing another parameter with a list of strings of views to ignore or a list of regular expressions to ignore.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//Ignoring specific page
Countly.q.push(['track_pageview',["/test-page"]]);

//Ignoring multiple specific pages
Countly.q.push(['track_pageview',["/test1", "/test2", "/test3"]]);

//Ignoring all /download/{download_id} pages but not /download page
Countly.q.push(['track_pageview',["/download/*"]]);

//Ignoring specific page while providing custom values (like hash value) for page view
Countly.q.push(['track_pageview', location.pathname+location.hash,["/test-page"]]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//Ignoring specific page
Countly.track_pageview(["/test-page"]);

//Ignoring multiple specific pages
Countly.track_pageview(["/test1", "/test2", "/test3"]);

//Ignoring all /download/{download_id} pages but not /download page
Countly.track_pageview(["/download/*"]);

//Ignoring specific page while providing custom values (like hash value) for page view
Countly.track_pageview(location.pathname+location.hash, ["/test-page"]);</code></pre>
  </div>
</div>
<p>
  <span>Optionally, you may provide view segments (key/value pairs) to track them with the view (as the third parameter). There is a list of reserved segment keys that should not be used:</span>
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
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//Provide view segments
Countly.q.push(['track_pageview', null, null, {theme:"red", mode:"fullscreen"}]);<br></code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//Provide view segments
Countly.track_pageview(null, null, {theme:"red", mode:"fullscreen"});<br></code></pre>
  </div>
</div>
<h2 id="h_01HABTQ43780HVFRZME2BK1PZJ">Overriding View Name and URL Getters</h2>
<p>
  <span style="font-weight: 400;">There are cases when determining the view name requires more complex logic, and in some cases, you will need to separate the URL and the View naming. This is done so you may still have some business logic view names, yet you have the valid URL underneath them to view action maps, such as clicks and scrolls.</span>
</p>
<p>
  <span style="font-weight: 400;">To do so you may define the view name and URL getter functions. That way you won’t need to provide separate view names, rather the SDK will use this getter function to receive the proper view name and the URL you would like to use.</span>
</p>
<p>
  <span style="font-weight: 400;">Here is an example of how to create a getter for View and URL.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">View getter</span>
    <span class="tabs-link">URL getter</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.getViewName = function(){
  //get base for our view
  var view = location.pathname;
  
  //if this is a page with dynamic id, we don't need id itself
  if (view.startsWith("/id/")) {
      view = "/id";
  }
  
  //now let's beautify the name
  //remove first character which always is slash (/)
  view = view.substring(1);
  
  //split by sub paths and use spaces instead
  view = view.split("/").join(" ");
  
  //upper case first letter
  view[0].toUpperCase() + view.substring(1)
  
  //return beautified view name
  return view;
}</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.getViewUrl = function(){
  //we want to have path and query string and hash as url
  return location.pathname + location.search + location.hash;
};</code></pre>
  </div>
</div>
<h1 id="h_01HABTQ438A1RWJXN4K84XP16R">Device ID Management</h1>
<h2 id="h_01HABTQ438H09ECC7YDDKNN68R">Device ID Generation</h2>
<p>
  By default Countly generates and assigns a random device ID to each device that
  reaches your website. This can be seen as the default way to recognize and capture
  the user behavior by keeping this ID at the local storage and referring to it
  when necessary. All activity done from the same device would be recorded under
  the same device ID and for practical reasons it can be seen as a user identifier.
</p>
<p>
  Limitations to this method comes when there multiple users using the same device
  where all users using the same device would be seen as a single user, or when
  a user reaches to your website from multiple devices or browsers in incognito
  mode where all devices would be seen as separate users. If these scenarios are
  an issue of concern to you, you can mitigate them with various device management
  strategies.
</p>
<p>
  While it is possible to change an assigned ID (typically during the user login)
  and implement your own logic, as explained at the next section, there are some
  other methods that you can assign an ID to your users. Assigning an ID inside
  your initialization config or adding a query to a link that you have provided
  to your user can be named as two of these methods:
</p>
<pre><code class="javascript">
// adding device ID here will prevent the generation of a random ID
Countly.init({
    app_key:"YOUR_APP_KEY",
    url: "https://try.count.ly",
    device_id:"yourDeviceID",
});

// you can assign a device ID to a user through a link that you have provided to them by adding cly_device_id to your url query
yourUrl + ?cly_device_id=yourDeviceID
</code></pre>
<p>
  If you want to erase the previously stored device ID from the storage you can
  set clear_stored_id flag to true at the init config to do so:
</p>
<pre><code class="javascript">
// this will erase the stored device ID from the local storage every time the Countly is initialized
Countly.init({
    app_key:"YOUR_APP_KEY",
    url: "https://try.count.ly",
    clear_stored_id: true,
});
</code></pre>
<div class="callout callout--info">
  <p class="callout__title">
    <strong>Device ID Priority</strong>
  </p>
  <p>
    If you have used multiple methods to set a device ID for your users during
    your first init, Countly would fall back to the device ID priority hierarchy
    to assign the the correct ID for your user. This hierarchy is as follows:
  </p>
  <p>
    URL set ID &gt; Developer set ID &gt; Temp ID (offline mode) &gt; SDK generated
    ID
  </p>
</div>
<h2 id="h_01HABTQ438HCZ8FJVAE34W49KP">Changing Device ID</h2>
<p>
  <span style="font-weight: 400;">In some cases, you may want to change the ID of the user/device that you provided or Countly automatically generated, e.g. when a user was changed.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['change_id', "myNewId"]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.change_id("myNewId");</code></pre>
  </div>
</div>
<div class="callout callout--warning">
  <p>
    <span style="font-weight: 400;">If device ID is changed without merging and consent was enabled, all previously given consent will be removed. This means that all features will cease to function until new consent has been given again for that new device ID.</span>
  </p>
</div>
<p>
  <span style="font-weight: 400;">In some other cases, you may also need to change a user's device ID in a way so that that server will merge the data of both user IDs (both the new and existing ID you provided) on the server, e.g. when a user used the website without authenticating and recorded some data and then authenticated, and you would like to change the ID to your internal ID of this user to keep tracking it across multiple devices.</span>
</p>
<p>
  <span style="font-weight: 400;">This call will merge any data recorded for the current ID and save it as a user with a newly provided ID.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['change_id', "myNewId", true]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.change_id("myNewId", true);</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">NOTE: The call will reject invalid device ID values. A valid value is not null, not undefined, of type string and is not an empty string.</span>
</p>
<h2 id="h_01HABTQ438Q143GXWNZ096BH17">Temporary Device ID (Offline mode)</h2>
<p>
  <span style="font-weight: 400;">Some cases do exist when you would like the SDK to collect data but not send it to the server until a certain point. Additionally, this mode allows you to delay providing the device_id property until a later time.</span>
</p>
<p>
  <span style="font-weight: 400;">E.g. if you would like to track your users with a custom device_id, such as with your internal customer ID, and you may only receive that value as soon as the user logs in. Yet, you would also like to track what the user did before logging in.</span>
</p>
<p>
  <span style="font-weight: 400;">Using offline mode within this context allows you to omit the user merging and server overhead that comes with it, including any possibly skewed aggregation data.</span>
</p>
<div class="callout callout--warning">
  <p>
    <span style="font-weight: 400;">If offline mode is entered and consent was enabled, all previously given consent will be removed. This means that all features will cease to function until new consent has been given again. Therefore after entering the offline mode, you should reestablish consent again.</span>
  </p>
</div>
<p>
  <span style="font-weight: 400;">To launch the SDK in offline mode, simply provide the offline_mode config value as true. At this point you may omit providing the device_id value if you would like. </span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.debug = false;
Countly.app_key = "YOUR_APP_KEY";
Countly.url = "https://try.count.ly";
Countly.offline_mode = true;

Countly.init();</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
    debug:false,
    app_key:"YOUR_APP_KEY",
    url: "https://try.count.ly",
    offline_mode: true
});</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Or you can enable offline mode at any point later in the SDK.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['enable_offline_mode']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.enable_offline_mode();</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">If you would like to disable offline mode and optionally provide the device_id at a later time, you may do so by adhering to the following:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['disable_offline_mode', device_id]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="java">Countly.disable_offline_mode(device_id);</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ438Y2NCA9PE3PZWSXTY">Retrieving Current Device ID</h2>
<p>
  If you want to execute your functions or to implement your logic depending on
  the type of device ID that the user has Countly offers a convenience method for
  you to do so.
</p>
<p>
  You can reach the current device ID of the user with get_device_id:
</p>
<pre><code class="javascript">
// you can just check if the device ID of the user is exactly what it should be
var userId = Countly.get_device_id();
if ( userId === "expectedId" ) {
  //... do something
}  
</code></pre>
<p>
  Depending on whether a user is vising your site for the first time or might have
  just logged in to their account or for many other reasons a user can have a certain
  device ID that has a different type than another user. These types are:
</p>
<ul>
  <li>DEVELOPER_SUPPLIED device ID</li>
  <li>SDK_GENERATED device ID</li>
  <li>TEMPORARY_ID device ID</li>
</ul>
<p>
  For DEVELOPER_SUPPLIED device ID, the assignment of the ID is handled by your
  internal logic, for SDK_GENERATED device ID, the ID of the user was generated
  randomly by Countly, and for TEMPORARY_ID device ID, the user is currently offline
  and no request is being sent to the servers.
</p>
<p>
  You can reach the device ID type of a user any time you want simply by calling
  the get_device_id_type function:
</p>
<pre><code class="javascript">
// You can get and compare if the device ID type is correct, and do something after
var idType = Countly.get_device_id_type();
// here lets check if it is SDK_GENERATED. Other options are DEVELOPER_SUPPLIED and TEMPORARY_ID
if ( idType === Countly.DeviceIdType.SDK_GENERATED ) {
  //... do something
}
</code></pre>
<h1 id="h_01HABTQ438V4VMNJPJF0MQECSZ">Heatmaps</h1>
<p>
  Heatmaps feature is a web exclusive plugin that helps you to visualize user interactions
  on your website. Web SDK supports this functionality by providing user click
  and scroll information to your server. Then from your server, you can trigger
  Heatmaps overlay to visualize these click clusters and scroll zones on your website.
</p>
<p>
  To display this overlay the SDK loads certain scripts from your server. To ensure
  the source of these scripts and to enable these scripts to be loaded from somewhere
  else other than your Countly server, the SDK offers a whitelisting option during
  the initialization. To whitelist domains other than your Countly server you should
  provide an array of these domains, as String values, under the 'heatmap_whitelist'
  flag during the initialization:
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
<h2 id="h_01HABTQ438Q028VRE7KA0Y1BMA">Tracking Clicks</h2>
<p>
  <span style="font-weight: 400;">This method will automatically track clicks on the last reported view and display them on the heatmap.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['track_clicks']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.track_clicks();</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">In the event you are facing issues with viewing heatmaps, kindly go through this&nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037639651-Views-and-heatmaps#heatmaps-troubleshooting">Troubleshooting guide</a>.</span>
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <strong> Viewing heatmaps with HTTP/HTTPS content:</strong>
  </p>
  <p>
    Note that browsers do not allow loading HTTP iframe content on HTTPS websites.
    For this reason, if you are using HTTPS on your Countly instance, you will
    only be able to view HTTPS content and no HTTP page content will be visible.
  </p>
</div>
<p>
  <span style="font-weight: 400;">After you integrate the JS SDK and start sending click data, all generated heatmaps may be viewed under Analytics &gt; Page views, as shown below:</span>
</p>
<div class="img-container">
  <img src="/hc/article_attachments/9545658580121/001.png" alt="001.png">
</div>
<h2 id="h_01HABTQ438184HFAE37E78K9VP">Tracking Scrolls</h2>
<p>
  <span style="font-weight: 400;">This method will automatically track scrolls on the last reported view and display them on the heatmap.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['track_scrolls']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.track_scrolls();</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">As with Click Heatmaps, collected data is viewable under Analytics &gt; Page views. You may change the heatmap type on the top bar once a view is open.</span>
</p>
<div class="img-container">
  <img src="/hc/article_attachments/9545659738009/002.png" alt="002.png">
</div>
<h1 id="h_01HABTQ438YJDHDMKPS8X3YK99">Remote Config</h1>
<p>
  <span style="font-weight: 400;">Remote Config feature enables you to fetch data that you have created in your server. Depending on the conditions you have set, you can fetch data from your server for the specific users that fits those conditions and process the Remote Config data in anyway you want. Whether to change the background color of your site to showing a certain message, the possibilities are virtually endless. For more information on Remote Config please check <a href="https://support.count.ly/hc/en-us/articles/9895605514009-Remote-Config" target="_blank" rel="noopener">here</a>.</span>
</p>
<p>
  <span style="font-weight: 400;">While fetching Remote Config, the SDK will automatically enroll the user to A/B testing. But you are able to explicitly enroll (or not) your users to the A/B testing while fetching the remote config values or afterwards. For more information on A/B testing please check <a href="https://support.count.ly/hc/en-us/articles/4416496362393-A-B-Testing-" target="_blank" rel="noopener">here</a>.</span>
</p>
<h2 id="h_01HABTQ438MKGNJ0DCP8J8YFTG">Automatic Remote Config</h2>
<p>
  <span style="font-weight: 400;">Automatic Remote Config functionality is disabled by default and needs to be explicitly enabled. When automatic Remote Config is enabled, the SDK will try to fetch it upon some specific trigers. For example, after SDK initialization, changing device ID.</span>
</p>
<p>
  <span style="font-weight: 400;">You may enable this feature by providing to the </span><em><span style="font-weight: 400;">remote_config</span></em><span style="font-weight: 400;"> flag a callback function or by setting it to true while initializing the SDK.</span>
</p>
<p>
  <span style="font-weight: 400;">If you provide a callback, the callback will be called when the Remote Config is initially loaded and when it is reloaded if you change the device_id. This callback should have two parameters, first is for error, and second is for the Remote Config object.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">// in your Countly init script
Countly.app_key = "YOUR_APP_KEY";<br>Countly.url = "https://try.count.ly";<br>Countly.debug = true;
Countly.remote_config = true;
<br>// OR<br>
// provide a callback to be notified when configs are loaded
Countly.app_key = "YOUR_APP_KEY";<br>Countly.url = "https://try.count.ly";<br>Countly.debug = true;
Countly.remote_config = function(err, remoteConfigs){
  if (!err) {
    //we have our remoteConfigs here
    console.log(remoteConfigs);
  }
};</code></pre>
  </div>
  <div class="tab is-hidden">
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
  </div>
</div>
<h2 id="h_01HABTQ438B1KZJH5N80BB1RPW">Manual Remote Config</h2>
<p>
  <span style="font-weight: 400;">If you want, you can manually fetch the Remote Config in order to receive the latest value anytime after the initialization. To do so you have to use the </span><em><span style="font-weight: 400;">fetch_remote_config</span></em><span style="font-weight: 400;"> call. This method is also used for reloading the values for updating them according to the latest changes you made on your server.</span>
</p>
<p>
  <span style="font-weight: 400;">By using this method, you can simply load the entire object or load some specific keys or omit some specific keys in order to decrease the amount of data transfer needed, assuming the values for some of the keys are large. This call will automatically save the fetched keys internally.</span>
</p>
<h3 id="h_01HABTQ438JQZ96YKJ89P3C8P4">Fetch All Keys</h3>
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
<h3 id="h_01HABTQ438DFHHZ77E03C3H0QF">Fetch Specific Keys</h3>
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
<h3 id="h_01HABTQ4384QKB945JFQVPMJT9">Fetch All Except Specific Keys</h3>
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
<h2 id="h_01HABTQ438FY9D5GRKKBVJTV7S">Accessing Remote Config Values</h2>
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
<h2 id="h_01HABTQ438D3D1TEAHTRB8TG1M">A/B Testing</h2>
<p>
  <span style="font-weight: 400;">To do so you have to set the use_explicit_rc_api flag to true during init (by default it is <em>false</em>). This will use the new Remote Config API and enroll your users to the A/B testing if they are eligible. However if you want to use the new API without enrolling your users automatically <em>rc_automatic_optin_for_ab&nbsp;</em>flag should be set to false during init (by default it is <em>true</em>).</span>
</p>
<p>
  <span style="font-weight: 400;">If you would like to enroll user to A/B testing without going through the Remote Config API, instead you can use the call <em>enrollUserToAb&nbsp;</em>with keys (an array of string values) that you want to enroll the user to.</span>
</p>
<pre><code class="javascript">// enrolling user for 'key1' and 'key2'
Countly.enrollUserToAb(["key1","key2"]);</code></pre>
<h2 id="h_01HABTQ438QWJV6X4MDDBDBKBW">Consent</h2>
<p>
  If consents are enabled, to fetch the Remote Config data you have to provide
  the 'remote-config' consent for this feature to work.
</p>
<h1 id="h_01HABTQ438JABXJNTKRC4T9QXV">User Feedback</h1>
<p>
  If you want to receive feedback from your users there are a couple of ways you
  can do that in Countly. To get a rating or suggestion from users you can use
  rating widgets, which gives users flexibility to give a rating, leave a comment
  or reach you with an e-mail. Another way the users can leave feedback is through
  the feedback widgets (survey, nps, ratings). With the help of these widgets you
  can ask your customers multiple questions and learn about their opinions and
  preferences in detail.
</p>
<h2 id="h_01HABTQ438XGTYWGAMYGPB3F1A">Ratings</h2>
<p>
  While it can be cumbersome for a customer to fill a survey, a quick alternative
  to get user feedback is to get a numerical user rating. That can be done with
  the Countly rating widget.
</p>
<h3 id="h_01HABTQ438MQSY7Z8RPY3TQD0V">Rating Widget</h3>
<p>
  Rating widgets create a channel for users to interact, through a pop up widget.
</p>
<p>
  While it is possible to customize the text fields of rating widgets according
  to your needs, the fundamental use case of a rating widget is to enable the user
  to leave a rating feedback on scale of 1 to 5, let the user contact the developer
  through e-mail and also to let the user be able to leave some comments or suggestions
  along the way.
</p>
<p>
  With Countly, if you want, you can create a single rating widget to get feedback
  on a specific topic or you can create multiple rating widgets that can tackle
  different topics depending on your needs. Another feature that can prove useful
  is the ability to show rating widgets on command, as a popup. This can be a very
  useful tool when interlinked with a form submit button to ask your customers
  about their experience directly after submitting their form or survey.
</p>
<p>
  For rating widgets to show with proper styling and to be present on the screen
  first you have to enable them using 'enableRatingWidgets' after you have initialized
  the Countly Web SDK and gave "star-rating" consent for widgets. Then you can
  integrate the ratings widget as follows:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//after initializing and giving consent
//for a single rating widget with widget ID '5b86772f7965c435319c79ee'
Countly.q.push([
    'enableRatingWidgets',
    {'popups':['5b86772f7965c435319c79ee']}
]);

//to manually show a rating widget as a popup
Countly.q.push([
    'presentRatingWidgetWithID',
    '6gdd84asc435319c78s4'
]);
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//after initializing and giving consent
//for a rating widget with widget ID '5b86772f7965c435319c79ee'
Countly.enableRatingWidgets({
    'popups':['5b86772f7965c435319c79ee'],
});

//to manually show a rating widget as a popup'
Countly.presentRatingWidgetWithID("6181639909e272efa5f64a44");
</code></pre>
  </div>
</div>
<p>
  To see multiple rating widgets on the screen, after enabling your widgets with
  'enableRatingWidgets' you have to use 'initializeRatingWidgets' by passing multiple
  widget IDs as an argument as follows:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//after enabling rating widgets
//to show multiple rating widgets with an array of different widget IDs
Countly.q.push([
    'initializeRatingWidgets',
    ['4678wetfgb8g79gfdg9221', 'd45a5d8we4f6fs5a546ass']
]);

</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//after enabling rating widgets
//to show multiple rating widgets with an array of different widget IDs
Countly.initializeRatingWidgets(["6181435609e272efa5f64307", "619bb3737730596209194fcc"])
</code></pre>
  </div>
</div>
<h3 id="h_01HABTQ43877ZM0YG7KMXSXKNP">Manual Rating Reporting</h3>
<p>
  In case you don't want to use Countly provided feedback and rating UI where you
  may use your own UI and simply report collected data to Countly.
</p>
<p>
  To report the rating widget result manually, you need to give "star-rating" consent
  (in case consent is required).
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//user feedback
Countly.q.push(['recordRatingWidgetWithID', {
    widget_id:"1234567890",
    contactMe: true,
    rating: 5,
    email: "user@domain.com",
    comment: "Very good"
}]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//user feedback
Countly.recordRatingWidgetWithID({
    widget_id:"1234567890",
    contactMe: true,
    rating: 5,
    email: "user@domain.com",
    comment: "Very good"
});</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ438NWHSRCMAV4RJJVWX">Feedback Widget</h2>
<p>
  There are three kinds of feedback widgets available. Namely NPS, survey and ratings
  widgets. Before any feedback widget can be shown, you need to create them in
  your countly dashboard first.
</p>
<p>
  All three widgets use the same API to fetch feedbacks from the server as well
  as to display them to the end user. By default, the created widget will be appended
  to the end of the html document. In some scenarios you might prefer to have the
  widget injected in a specific element. For those scenarios we have added optional
  selectors. The first one is used for selecting an element by it's id and the
  second one is used to select the element by it's class selector. If you want
  to inject the feedback widget in a specific element, you can do so by specifying
  the element ID or the class name. You can also add custom segmentation while
  presenting a widget.
</p>
<p>
  To use feedback widgets, you need to give "feedback" consent (in case consent
  is required).
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//Fetch user's feedback widgets from the server
Countly.q.push(['get_available_feedback_widgets', feedbackWidgetsCallback]);
<br>// Feedback widget callback function, err is for error and countlyPresentableFeedback contains an array of widhet objects
function feedbackWidgetsCallback(countlyPresentableFeedback, err) {
    if (err) {
        console.log(err);
        return;
    }
  
    // Decide which which widget to show. Here the first rating widget is selected. 
    const widgetType = "rating";
    const countlyFeedbackWidget = countlyPresentableFeedback.find(widget => widget.type === widgetType);
    if (!countlyFeedbackWidget) {
      console.error(`[Countly] No ${widgetType} widget found`);
      return;
    }

    //Define the element ID and the class name (optional, pass undefined if you don't use)
    const selectorId = "targetIdSelector";
    const selectorClass = "targetClassSelector";

    // Define the segmentation (optional)
    const segmentation = { page: "home_page" };

    //Display the feedback widget to the end user
    Countly.present_feedback_widget(countlyFeedbackWidget, selectorId, selectorClass, segmentation);
}
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//Fetch user's feedback widgets from the server
Countly.get_available_feedback_widgets(feedbackWidgetsCallback);
<br>// Feedback widget callback function, err is for error and countlyPresentableFeedback contains an array of widhet objects
function feedbackWidgetsCallback(countlyPresentableFeedback, err) {
    if (err) {
        console.log(err);
        return;
    }

    // Decide which which widget to show. Here the first rating widget is selected. 
    const widgetType = "rating";
    const countlyFeedbackWidget = countlyPresentableFeedback.find(widget => widget.type === widgetType);
    if (!countlyFeedbackWidget) {
      console.error(`[Countly] No ${widgetType} widget found`);
      return;
    }
    
    //Define the element ID and the class name (optional, pass undefined if you don't use)
    const selectorId = "targetIdSelector";
    const selectorClass = "targetClassSelector";

    // Define the segmentation (optional)
    const segmentation = { page: "home_page" };
    
    //Display the feedback widget to the end user 
    Countly.present_feedback_widget(countlyFeedbackWidget, selectorId, selectorClass, segmentation);
}
</code></pre>
  </div>
</div>
<p>
  Note: Feedback widget's show policies are handled internally by the web sdk.
</p>
<h3 id="h_01HABTQ438KSCZWEFA8GEFE07R">Manual Reporting</h3>
<p>
  Reporting feedback widgets manually consists of 3 main steps:
</p>
<ol>
  <li>
    Fetching widget list from the server with 'get_available_feedback_widgets'
  </li>
  <li>
    Fetching one widget's data from that list with 'getFeedbackWidgetData'
  </li>
  <li>
    Reporting that single widget's results with 'reportFeedbackWidgetManually'
  </li>
</ol>
<p>
  At first step, by using the 'get_available_feedback_widgets' function, you can
  fetch the list of available widgets from your server as an Array of widget Objects.
  This function takes a callback as a parameter and this callback should have two
  parameters, first one for the returned list and the second one for the error.
  Inside your callback you should process this array of widget objects and pick
  one object that you want to report the results for. This array and the objects
  that you can pick would look like this:
</p>
<pre><code class="javascript">{
  "result":[
      {
        "_id":"614811419f030e44be07d82f",
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
        "_id":"614811419f030e44be07d839",
        "type":"nps",
        "name":"One response for all",
        "tg":[]
      },
      {
        "_id":"614811429f030e44be07d83d",
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
  }</code></pre>
<p>
  Here you would want to pick a widget according to its type and name or any other
  information you are looking for. For more information on this data please check
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts#interpreting-retrieved-feedback-widget-lists" target="_blank" rel="noopener">here</a>.
</p>
<p>
  At second step, by using the 'getFeedbackWidgetData' function, you can fetch
  the data of the widget of your choice. This functions has two parameters, first
  one is the widget object obtained from the first step and the second one is a
  callback with two parameters, one for the retrieved data and second one is for
  the error. Inside your callback you can process the returned object and gather
  information necessary for you to provide at the next step.
</p>
<p>
  The third and last step is the part where you would report the results for the
  widget of your choice by using the 'reportFeedbackWidgetManually' function. This
  function takes three parameters, first the widget object obtained from the first
  step, second the widget data from the second step and third the result object
  that you want to report for your widget. This result object would have different
  key/value pairs depending on the type of widget you are reporting about so you
  can reach to an in-depth explanation on how to form this object from
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305#reporting-a-feedback-widget-manually" target="_blank" rel="noopener">here</a>.
</p>
<p>
  And example implementation of the mentioned concepts can be seen here:
</p>
<pre><code class="javascript">
    // an example of getting the widget list, using it to get widget data and then recording data for it manually. widgetType can be 'nps', 'survey' or 'rating'
    function getFeedbackWidgetListAndDoThings(widgetType) {
      // get the widget list
      Countly.get_available_feedback_widgets(
        // callback function, 1st param is the feedback widget list
        function (feedbackList, err) {
          if (err) { // error handling
            console.log(err);
            return;
          }

          // find the widget object with the given widget type. This or a similar implementation can be used while using fetchAndDisplayWidget() as well
          const countlyFeedbackWidget = feedbackList.find(widget => widget.type === widgetType);
          if (!countlyFeedbackWidget) {
            console.error(`[Countly] No ${widgetType} widget found`);
            return;
          }

          // Get data with the widget object
          Countly.getFeedbackWidgetData(CountlyFeedbackWidget,
            // callback function, 1st param is the feedback widget data
            function (feedbackData, err) {
              if (err) { // error handling
                console.error(err);
                return;
              }

              const CountlyWidgetData = feedbackData;
              // record data according to the widget type
              if (CountlyWidgetData.type === 'nps') {
                Countly.reportFeedbackWidgetManually(CountlyFeedbackWidget, CountlyWidgetData, { rating: 3, comment: "comment" });
              } else if (CountlyWidgetData.type === 'survey') {
                var widgetResponse = {};
                // form the key/value pairs according to data
                widgetResponse["answ-" + CountlyWidgetData.questions[0].id] = CountlyWidgetData.questions[0].type === "rating" ? 3 : "answer";
                Countly.reportFeedbackWidgetManually(CountlyFeedbackWidget, CountlyWidgetData, widgetResponse);
              } else if (CountlyWidgetData.type === 'rating') {
                Countly.reportFeedbackWidgetManually(CountlyFeedbackWidget, CountlyWidgetData, { rating: 3, comment: "comment", email: "email", contactMe: true });
              }
            }

          );
        })
    }
       </code></pre>
<h1 id="h_01HABTQ439MH1SD5Q76905BRWP">User Profiles</h1>
<h2 id="h_01HABTQ439KMGT58PHY4MRA1GT">User Details</h2>
<p>
  <span style="font-weight: 400;">If you have any details about the user/visitor, you may provide Countly with that information. This will allow you to track every specific user on the "User Profiles" tab, which is available with <a href="http://count.ly/enterprise-edition">Countly Enterprise Edition</a>.</span>
</p>
<p>
  <span style="font-weight: 400;">The list of possible parameters you may pass:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['user_details',{
    "name": "Arturs Sosins",
    "username": "ar2rsawseen",
    "email": "test@test.com",
    "organization": "Countly",
    "phone": "+37112345678",
    //Web URL to picture
    "picture": "https://pbs.twimg.com/profile_images/1442562237/012_n_400x400.jpg", 
    "gender": "M",
    "byear": 1987, //birth year
    "custom":{
      "key1":"value1",
      "key2":"value2",
      ...
    }
}]);</code></pre>
  </div>
  <div class="tab is-hidden">
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
  </div>
</div>
<h2 id="h_01HABTQ439HW6249PJ1F6BFA0B">Modifying Custom Data</h2>
<p>
  <span style="font-weight: 400;">Additionally, you may perform different manipulations on custom data values, such as incrementing the current value on the server or storing an array of values under the same property.</span>
</p>
<p>
  <span style="font-weight: 400;">After using modifiers, don't forget to call&nbsp;<code class="javascript">userData.save</code>&nbsp;to send data to server.</span>
</p>
<p>
  <span style="font-weight: 400;">The list of available methods may be found below:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['userData.set', key, value]) //set custom property
Countly.q.push(['userData.unset', key]) //remove custom property
Countly.q.push(['userData.set_once', key, value]) //set custom property only if property does not exist
Countly.q.push(['userData.increment', key]) //increment value in key by one
Countly.q.push(['userData.increment_by', key, value]) //increment value in key by provided value
Countly.q.push(['userData.multiply', key, value]) //multiply value in key by provided value
Countly.q.push(['userData.max', key, value]) //save max value between current and provided
Countly.q.push(['userData.min', key, value]) //save min value between current and provided
Countly.q.push(['userData.push', key, value]) //add value to key as array element
Countly.q.push(['userData.push_unique', key, value]) //add value to key as array element, but only store unique values in array
Countly.q.push(['userData.pull', key, value]) //remove value from array under property with key as name
Countly.q.push(['userData.save']) //send userData to server</code></pre>
  </div>
  <div class="tab is-hidden">
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
  </div>
</div>
<h2 id="h_01HABTQ439F2RDC9ZHWC4KZPRH">Orientation Tracking</h2>
<p>
  Orientation tracking is enabled by default and will be sent if the required "user"
  consent is given (if enabled). Countly will report the device orientation once
  a session starts, and at any time the orientation changes.
</p>
<p>
  You may disable orientation tracking by providing the enable_orientation_tracking
  setting when initializing the SDK as follows.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">// in your Countly init script
Countly.enable_orientation_tracking = false;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//to disable orientation tracking
Countly.init({
    debug:false,
    app_key:"YOUR_APP_KEY",
    device_id:"1234-1234-1234-1234",
    url: "https://try.count.ly",
    enable_orientation_tracking: false //this will disable orientation tracking
});</code></pre>
  </div>
</div>
<p>
  In case you need to force reporting orientation, you may call the following method.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//user stored conversion data
Countly.q.push(['report_orientation', "portrait"]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//user stored conversion data
Countly.report_orientatio("portrait");</code></pre>
  </div>
</div>
<h1 id="h_01HABTQ4399MRCTWV2VT19QGGE">Application Performance Monitoring</h1>
<p>
  If you want to record some performance metrics regarding your website there are
  2 ways to report these performance traces. One way is to construct and report
  them manually. The other is using a plugin that will utilize BoomerangJS to collect
  website's performance data and report it as a performance trace.
</p>
<p>
  You can reach to example implementations of APM with BoomerangJS from the following
  links:<br>
  <a href="https://github.com/Countly/countly-sdk-web/blob/master/examples/example_apm_async.html" target="_blank" rel="noopener">Async Apm Example</a><br>
  <a href="https://github.com/Countly/countly-sdk-web/blob/master/examples/example_apm.html" target="_blank" rel="noopener">Sync Apm Example</a>
</p>
<h2 id="h_01HABTQ439JA7TFSMPS38DM324">Custom Traces</h2>
<p>
  To manually report trace you need to construct the trace object and call a method
  like this:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//report custom trace
Countly.q.push(["report_trace",{
    type: "device", //device or network
    name: "test call", //use name to identify trace and group them by
    stz: 1234567890123, //start timestamp in milliseconds
    etz: 1234567890123, //end timestamp in milliseconds
    apm_metrics: {
        duration: 1000 //duration of trace
    }
}]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//report custom trace
Countly.report_trace({
    type: "device", //device or network
    name: "test call", //use name to identify trace and group them by
    stz: 1234567890123, //start timestamp in milliseconds
    etz: 1234567890123, //end timestamp in milliseconds
    apm_metrics: {
        duration: 1000 //duration of trace
    }
});</code></pre>
  </div>
</div>
<p>
  Whether you are using Countly synchronously or asynchronously, you should always
  provide the 'duration' key and its value in apm_metrics, otherwise custom traces
  won't be recorded.
</p>
<h2 id="h_01HABTQ439VYQ8V9TJ2GX1J450">Automatic Device Traces</h2>
<p>
  Automatic trace reporting has two different implementation depending on if you
  are using Countly synchronously or asynchronously. Normally we would like Countly
  script to load first and BoomerangJS related scripts right after.&nbsp;
</p>
<h3 id="h_01HABTQ4391JS1EG69GBPTCQJT">Asynchronous Implementation</h3>
<p>
  To use automatic device traces in your async Countly implementation you will
  need to set <code>loadAPMScriptsAsync</code> flag to <code>true</code> in Countly
  object. This would ensure that the correct script load order is established.
  You can provide two additional flags to the Countly object. First one is the
  BoomerangJS script source path as <code>customSourceBoomerang</code> and the
  second is the countly_boomerang script source path as
  <code>customSourceCountlyBoomerang</code>. If not provided the SDK would use
  the latest CDN scripts as the source:
</p>
<pre><code class="javascript">Countly.app_key = "YOUR_APP_KEY";<br>Countly.url = "YOUR_SERVER_URL";<br>Countly.loadAPMScriptsAsync = true;<br>// Countly.customSourceBoomerang = "../somewhere/boomerang.min.js";<br>// Countly.customSourceCountlyBoomerang = "../somewhere/countly_boomerang.js";<br>// ...</code></pre>
<p>
  Also, in your Countly init script you need to call a method to start reporting
  'loading' and 'network' traces automatically:
</p>
<pre><code class="javascript">// enables APM
Countly.q.push(["track_performance"]);</code></pre>
<p>
  This method accepts a BoomerangJS config object (<a href="http://akamai.github.io/boomerang/BOOMR.html" target="_blank" rel="noopener">more information on BoomerangJS</a>)
  as an optional second parameter. If you are familiar with it, you can modify
  it on your own depending on your needs (you can find the used files
  <a href="https://github.com/Countly/countly-sdk-web/tree/master/plugin/boomerang" target="_blank" rel="noopener">here</a>).
  By default the SDK would use this configuration:
</p>
<pre><code class="javascript">{
    //page load timing
    RT:{},
    //required for automated networking traces
    instrument_xhr: true,
    captureXhrRequestResponse: true,
    AutoXHR: {
        alwaysSendXhr: true,
        monitorFetch: true,
        captureXhrRequestResponse: true
    },
    //required for screen freeze traces
    Continuity: {
        enabled: true,
        monitorLongTasks: true,
        monitorPageBusy: true,
        monitorFrameRate: true,
        monitorInteractions: true,
        afterOnload: true
    }
}</code></pre>
<h3 id="h_01HABTQ439DYQ8H3VVJE9DV7YC">Synchronous Implementation</h3>
<p>
  To automatically report traces you will need to include 2 additional files in
  your project directly after declaring the Countly script like this with the correct
  paths according to your project structure:
</p>
<pre>// Option 1: You can provide local paths<br>&lt;script type='text/javascript' src="../plugin/boomerang/boomerang.min.js"&gt;&lt;/script&gt;
&lt;script type='text/javascript' src='../plugin/boomerang/countly_boomerang.js'&gt;&lt;/script&gt;<br><br>// Option 2: Or you can use CDN for path<br>&lt;script type='text/javascript' src="https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/plugin/boomerang/boomerang.min.js"&gt;&lt;/script&gt; <br>&lt;script type='text/javascript' src="https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/plugin/boomerang/countly_boomerang.js"&gt;&lt;/script&gt;</pre>
<p>
  After that, you would call a method to start reporting 'loading' and 'network'
  traces automatically. You can optionally provide here a BoomerangJS config object
  if you are familiar with it as mentioned above at Async implementation. Default
  usage inside your Countly init script would be like this:
</p>
<pre><code class="javascript">//automatically report traces
Countly.track_performance();</code></pre>
<h1 id="h_01HABTQ439V9NNDDCW31XG086F">User Consent</h1>
<h2 id="h_01HABTQ4394D6BR7PJ36RYQK4R">Opt In / Opt Out</h2>
<p>
  <span style="font-weight: 400;">The Countly SDK will always be opt in by default, but you may easily disable all tracking by selecting&nbsp;the <strong>opt_out</strong>&nbsp;method. It will also persistently save settings and prevent tracking after page reloads. Select&nbsp;<strong>opt_in</strong> to resume tracking.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//to stop tracking user data call
Countly.q.push(['opt_out']);

//to resume tracking user data call
Countly.q.push(['opt_in']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//to stop tracking user data call
Countly.opt_out();

//to resume tracking user data call
Countly.opt_in();</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Disabling tracking for specific users is more than sufficient for most cases. However, should you desire more granular feature controls, checkout the&nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037441932-Web-analytics-JavaScript-#disable-tracking-until-given-consent">following section</a>.</span>
</p>
<div class="callout callout--info">
  <p>
    If you would like to have opt out selected by default, combine these methods
    with the initial setting <strong>ignore_visitor</strong> on the Countly init
    object.
  </p>
</div>
<p>
  <span style="font-weight: 400;">In most cases, the </span><strong>opt_out</strong><span style="font-weight: 400;">&nbsp;and&nbsp;</span><strong>opt_in</strong><span style="font-weight: 400;">&nbsp;methods are enough to disable the tracking of specific users, such as testers. However, in some cases, you may require a more granular approach.</span>
</p>
<p>
  <span style="font-weight: 400;">This section will tell you how to set up GDPR compliant consent management with the Countly Web SDK.</span>
</p>
<h2 id="h_01HABTQ439VBB36B3SACYJGJWQ">Disable Tracking Until Given Consent</h2>
<p>
  <span style="font-weight: 400;">To disable tracking until consent is given for a specific feature, all you need to do is pass true as the&nbsp;</span><strong>require_consent</strong><span style="font-weight: 400;">&nbsp;config before or during your selection of the Countly&nbsp;</span><strong>init</strong><span style="font-weight: 400;">&nbsp;method.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">// in your Countly init script
Countly.require_consent = true;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
    debug:false,
    app_key:"YOUR_APP_KEY",
    device_id:"1234-1234-1234-1234",
    url: "https://try.count.ly",
    app_version: "1.2",
    country_code: "LV",
    city: "Riga",
    ip_address: "83.140.15.1",
    require_consent: true //this will make require consent before tracking
});</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ439DN2P2CKVF8YMBCKD">Features for Consent</h2>
<p>
  <span style="font-weight: 400;">The SDK provides different features for consent. You may check all the supported features for the current SDK by checking the&nbsp;</span><strong>Countly.features</strong><span style="font-weight: 400;">&nbsp;property. Here is a list containing all the properties with ex</span>planations:
</p>
<ul>
  <li>
    <span style="font-weight: 400;">sessions - tracks when, how often, and how long users use your website</span>
  </li>
  <li>
    <span style="font-weight: 400;">events - allows your events to be sent to the server</span>
  </li>
  <li>
    <span style="font-weight: 400;">views - allows for the views/pages accessed by a user to be tracked</span>
  </li>
  <li>
    <span style="font-weight: 400;">scrolls - allows a user’s scrolls to be tracked on the heatmap</span>
  </li>
  <li>
    <span style="font-weight: 400;">clicks - allows a user’s clicks and link clicks to be tracked on the heatmap</span>
  </li>
  <li>
    <span style="font-weight: 400;">forms - allows a user’s form submissions to be tracked</span>
  </li>
  <li>
    <span style="font-weight: 400;">crashes - allows JavaScript errors to be tracked</span>
  </li>
  <li>
    <span style="font-weight: 400;">attribution - allows the campaign from which a user came to be tracked</span>
  </li>
  <li>
    <span style="font-weight: 400;">users - allows user information, including custom properties, to be collected/provided</span>
  </li>
  <li>
    <span style="font-weight: 400;">star-rating - allows user rating and feedback tracking through rating widgets</span>
  </li>
  <li>
    <span style="font-weight: 400;">feedback - allows survey, nps rating and feedback tracking through feedback widgets</span>
  </li>
  <li>
    <span style="font-weight: 400;">apm - allows performance tracking of application by recording traces</span>
  </li>
  <li>
    <span style="font-weight: 400;">location - allows a user’s location (country, city area) to be recorded</span>
  </li>
</ul>
<p>
  <span style="font-weight: 400;">This is the most granular level with control features for which consent may be given. However, depending on your website and use case, you may also want to combine some of the features into one using the&nbsp;<strong>group_features</strong>&nbsp;method.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Grouping features</span>
    <span class="tabs-link">One group for everything</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.group_features({
    activity:["sessions","events","views"],
    interaction:["scrolls","clicks","forms"]
});
//After this call Countly.add_consent("activity") to allow "sessions","events","views"
//or call Countly.add_consent("interaction") to allow "scrolls","clicks","forms"
//or call Countly.add_consent("crashes") to allow some separate feature</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.group_features({
  all:["sessions","events","views","scrolls","clicks","forms","crashes","attribution","users"]
});
//After this call Countly.add_consent("all") to allow all features</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ4391J4A916V53AVFVP5">Managing Consent</h2>
<p>
  <span style="font-weight: 400;">Upon a visitor’s arrival to your website, you should check if you already have consent from this visitor. If not, you should present them with a popup explaining what will be tracked and allow them to consent to tracking. When a user selects the consent preferences, you should persistently store it, and on each Countly load, let Countly know for which features the user gave consent by calling the&nbsp;<strong>Countly.add_consent</strong>&nbsp;method and passing one or multiple features (as an array). For example, you should also allow the user to change their mind regarding separate settings screens and when changes are going to be made there.</span>
  <span style="font-weight: 400;">Respectively call the <strong>Countly.add_consent</strong> or <strong>Countly.remove_consent</strong>&nbsp;methods to allow Countly to track specific features or disable tracking for them.</span>
</p>
<p>
  <span style="font-weight: 400;">Here is a high-level example of how it could look:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">&lt;script type='text/javascript'&gt;
  
// Some default pre init
var Countly = Countly || {};
Countly.q = Countly.q || [];

// Provide your app key that you retrieved from Countly dashboard
Countly.app_key = "YOUR_APP_KEY";

// Provide your server IP or name. Use try.count.ly or us-try.count.ly
// or asia-try.count.ly for EE trial server.
// If you use your own server, make sure you have https enabled if you use
// https below.
Countly.url = "https://yourdomain.com";

//require consent before tracking anything
Countly.require_consent = true; //this true means consent is required

//(optionally) provide custom feature tree if needed
Countly.q.push(['group_features', {
activity:["sessions","events","views"],
interaction:["scrolls","clicks","forms"]
}]);

//we can call all the helper methods we want, they won't record until consent is provided for specific features
Countly.q.push(['track_sessions']);
Countly.q.push(['track_pageview']);
Countly.q.push(['track_clicks']);
Countly.q.push(['track_links']);
Countly.q.push(['track_forms']);
Countly.q.push(['track_errors', {jquery:"1.10", jqueryui:"1.10"}]);

//Consent Management logic should be implemented and controlled by developer
//this is just a simply example of what logic it could have
if (typeof(localStorage) !== "undefined") {
var consents = localStorage.getItem("consents");
//checking if user already provided consent
if(consents){
//we already have array with consents from previous visit, let's just pass them to Countly
Countly.q.push(['add_consent', JSON.parse(consents)]);
}
else{
//user have not yet provided us a consent
//we need to display popup and ask user to give consent for specific features we want to track
//once we get response, we should store them like this
//example response
var response = ["activity", "interaction", "crashes"];
Countly.q.push(['add_consent', response]);
localStorage.setItem("consents", JSON.stringify(response));
}
} else {
// Sorry! No Web Storage support..
// we can fallback to cookie
}

// Load countly script asynchronously
(function() {
var cly = document.createElement('script'); cly.type = 'text/javascript';
cly.async = true;
// Enter url of script here (see below for other option)
cly.src = 'https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.min.js';
cly.onload = function(){Countly.init()};
var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(cly, s);
})();
&lt;/script&gt;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="html">&lt;!--Countly script--&gt;
&lt;script type='text/javascript' src='../lib/countly.js'&gt;&lt;/script&gt;
&lt;script type='text/javascript'&gt;

//initializing countly with params and passing require_consent config as true
Countly.init({
app_key: "YOUR_APP_KEY",
url: "https://try.count.ly", //your server goes here
debug:true,
require_consent: true //this true means consent is required
});

//(optionally) provide custom feature tree if needed
Countly.group_features({
activity:["sessions","events","views"],
interaction:["scrolls","clicks","forms"]
});

//we can call all the helper methods we want, they won't record until consent is provided for specific features
Countly.track_sessions();
Countly.track_pageview();
Countly.track_clicks();
Countly.track_links();
Countly.track_forms();
Countly.track_errors({jquery:"1.10", jqueryui:"1.10"});

//Consent Management logic should be implemented and controled by developer
//this is just a simply example of what logic it could have
if (typeof(localStorage) !== "undefined") {
var consents = localStorage.getItem("consents");
//checking if user already provided consent
if(consents){
//we already have array with consents from previous visit, let's just pass them to Countly
Countly.add_consent(JSON.parse(consents));
}
else{
//user have not yet provided us a consent
//we need to display popup and ask user to give consent for specific features we want to track
//once we get response, we should store them like this
//example response
var response = ["activity", "interaction", "crashes"];
Countly.add_consent(response);
localStorage.setItem("consents", JSON.stringify(response));
}
} else {
// Sorry! No Web Storage support..
// we can fallback to cookie
}</code></pre>
  </div>
</div>
<h1 id="h_01HABTQ439GYX75SVN2YEPHH82">Other Features and Notes</h1>
<h2 id="h_01HABTQ439HZN7Y6A6F07Y6G0K">SDK Config Parameters Explained</h2>
<p>
  Here are the properties you may set up upon Countly initialization:
</p>
<ul>
  <li>
    <strong>app_key</strong> - mandatory, app key for your app created in Countly
  </li>
  <li>
    <strong>device_id</strong> - to identify a visitor, will be autogenerated
    if not provided
  </li>
  <li>
    <strong>url</strong> - your Countly server URL - you may also use your own
    server URL or IP here
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
    <strong>ip_address</strong> - (optional) IP address of your visitor
  </li>
  <li>
    <strong>debug</strong> - output debug info into the console (default: false)
  </li>
  <li>
    <strong>ignore_bots</strong> - option to ignore traffic from bots (default:
    true)
  </li>
  <li>
    <strong>interval</strong> -
    <span style="font-weight: 400;">set an interval for how often inspections should be made to see if there is any data to report and then report it (default: 500 ms)</span>
  </li>
  <li>
    <strong>queue_size</strong> - the maximum amount of queued requests to store
    (default: 1000)
  </li>
  <li>
    <strong>fail_timeout</strong> -
    <span style="font-weight: 400;">set the time to wait in seconds after a failed connection to the server (default: 60 seconds)</span>
  </li>
  <li>
    <strong>inactivity_time</strong> -
    <span style="font-weight: 400;">the time limit after which a user will be considered inactive if no actions have been made. No mouse movement, scrolling, or keys pressed. Expressed in minutes (default: 20 minutes)</span>
  </li>
  <li>
    <strong>session_update</strong> -
    <span style="font-weight: 400;">how often a session should be extended, expressed in seconds (default: 60 seconds)</span>
  </li>
  <li>
    <strong>max_events</strong> - maximum amount of events to send in one batch
    (default: 100)
  </li>
  <li>
    <strong>max_logs</strong> -
    <span style="font-weight: 400;">the maximum amount of breadcrumbs to store for crash logs (default: 100)</span>
  </li>
  <li>
    <strong>ignore_referrers</strong> - array with referrers to ignore (default:
    none)
  </li>
  <li>
    <strong>ignore_prefetch</strong> -
    <span style="font-weight: 400;">ignore prefetching and pre-rendering from counting as real website visits (default: true)</span>
  </li>
  <li>
    <strong>heatmap_whitelist</strong> -
    <span style="font-weight: 400;">Array of trusted domains (as string) that can trigger heatmap script loading. By default the SDK whitelists your server url.</span>
  </li>
  <li>
    <strong>force_post</strong> -
    <span style="font-weight: 400;">force using post method for all requests (default: false)</span>
  </li>
  <li>
    <strong>ignore_visitor</strong> -
    <span style="font-weight: 400;">ignore this current visitor (default: false)</span>
  </li>
  <li>
    <strong>require_consent</strong> - P<span style="font-weight: 400;">ass true if you are implementing GDPR compatible consent management. This would prevent running any functionality without proper consent (default: false)</span>
  </li>
  <li>
    <strong>utm</strong> - o<span style="font-weight: 400;">bject instructing which UTM parameters to track (default: {"source":true, "medium":true, "campaign":true, "term":true, "content":true})</span>
  </li>
  <li>
    <strong>use_session_cookie</strong> - use cookies to track sessions (default:
    true)
  </li>
  <li>
    <strong>session_cookie_timeout</strong> -
    <span style="font-weight: 400;">how long until a cookie session should expire, expressed in minutes (default: 30 minutes)</span>
  </li>
  <li>
    <strong>remote_config</strong> -
    <span style="font-weight: 400;">enable automatic remote config fetching, provide the callback function to be notified when fetching is complete (default: false)</span>
  </li>
  <li>
    <strong>rc_automatic_optin_for_ab</strong> -
    <span style="font-weight: 400;">opts in the user for A/B testing while fetching the remote config (default: true)</span>
  </li>
  <li>
    <strong>use_explicit_rc_api</strong> -
    <span style="font-weight: 400;">set it to true to use the explicit remote config API (default: false)</span>
  </li>
  <li>
    <strong>namespace</strong> - h<span>ave a separate namespace for persistent data when using multiple trackers on the same domain</span>
  </li>
  <li>
    <strong>track_domains</strong> -
    <span>Set to false to disable domain tracking, so no domain data would be reported (default: true)</span>
  </li>
  <li>
    <span><strong>headers</strong> - object to override or add headers to all SDK requests</span>
  </li>
  <li>
    <span><strong>storage</strong> - What type of storage to use, by default uses local storage and would fallback to cookies, but you can set values "localstorage" or "cookies" to force only specific storage, or use "none" to not use any storage and keep everything in memory</span>
  </li>
  <li>
    <span><strong>metrics</strong> - provide metrics override or custom metrics for this user. For more information on the specific metric keys used by Countly, check <a href="https://support.count.ly/hc/en-us/articles/9290669873305#setting-custom-user-metrics" target="_self">here</a>.</span><span></span>
  </li>
</ul>
<p>
  <span style="font-weight: 400;">Setting up properties on the Countly Web SDK is as follows (use your own server name if not using try.count.ly below):</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.debug = false;
Countly.app_key = "YOUR_APP_KEY";
Countly.device_id = "1234-1234-1234-1234";
Countly.url = "https://try.count.ly";
Countly.app_version = "1.2";
Countly.country_code = "LV";
Countly.city = "Riga";
Countly.ip_address = "83.140.15.1";</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
    debug:false,
    app_key:"YOUR_APP_KEY",
    device_id:"1234-1234-1234-1234",
    url: "https://try.count.ly",
    app_version: "1.2",
    country_code: "LV",
    city: "Riga",
    ip_address: "83.140.15.1"
});</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ437DGBA97G3DTYD27AV">SDK Storage and Requests</h2>
<p>
  Countly Web SDK stores various information like device ID, request queue, session
  information and more in your device. This helps Countly to provide data consistency
  and enable convenience methods like offline mode.
</p>
<p>
  The default storage location of user-specific data, except the session information,
  is your browser’s local storage. Information stored here is persistent, and as
  long as it was not erased or overwritten, it will stay on your device indefinitely.
  However, Countly allows you to change this behavior by selecting persistent cookies
  as the main storage option or choosing not to store any data at all, depending
  on your needs. These storage options are mutually exclusive, meaning only one
  option can be selected at a given time.
</p>
<p>
  If cookies were selected as the main storage medium, persistent cookies have
  an expiration date and the information stored in them would be rendered obsolete
  after a while. In case of the session information, it is stored in session cookies
  and would expire when the tab or browser is closed. Lastly, if you decide not
  to store any information, all information will stay in memory and would be gone
  when the memory is cleared.
</p>
<p>These options can be selected during the initialization:</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="html">//possible options are "localstorage", "cookies" and "none"
Countly.storage = "localstorage";</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="html">//possible options are "localstorage", "cookies" and "none"
Countly.init({
  app_key:"YOUR_APP_KEY",
  url: "https://try.count.ly",
  storage: "localstorage"
});</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ439T5M3FN6CV6HHG2TX">Automatically Fill User Data</h2>
<p>
  <span style="font-weight: 400;">In most cases, you won’t know anything about your users, yet you will still want to try to collect any data possible. We provide 2 helper methods for this exact reason.</span>
</p>
<h3 id="h_01HABTQ4397KTBE8EHNMVFRQ7V">Collect User Data From Filled Forms</h3>
<p>
  <span style="font-weight: 400;">This method will look into the forms filled out by your users and will try to gather data, such as names, email addresses, usernames, etc.<br>All forms will automatically be checked, but you have the option to provide a form element if you would like to collect data only from a specific form, or select a method multiple times for different forms. Also, if you are already providing data for users, then you would not want to overwrite it. You may set the third parameter as true to indicate that data found should be stored in custom properties.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//collect data from forms
Countly.q.push(['collect_from_forms']);

//collect data from specific form
Countly.q.push(['collect_from_forms', formElement]);

//collect from forms and report as custom user properties
Countly.q.push(['collect_from_forms', document, true]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//collect data from forms
Countly.collect_from_forms();

//collect data from specific form
Countly.collect_from_forms(formElement);

//collect from forms and report as custom user properties
Countly.collect_from_forms(document, true);</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Passwords and other sensitive data will be omitted, however, if you would explicitly like to exclude some form input from being processed, just add the css class&nbsp;<strong>cly_user_ignore</strong>&nbsp;to that element. Oppositely, you may need to specify data from this input to be collected as the provided key by adding the prefixed css class&nbsp;<strong>cly_user_key</strong>. Therefore, if you would like to store data as a name, you should specify the&nbsp;<strong>cly_user_name</strong>&nbsp;css class.</span>
</p>
<pre><code class="html">&lt;form method='post' name='test_form'&gt;
  &lt;!-- data will be checked in this input --&gt;
&lt;p&gt;&lt;input type="text" name="e" value="myemail@mydomain.com"&gt;&lt;/p&gt;
  
&lt;!-- ignore this input --&gt;
&lt;p&gt;&lt;input type="text" name="e" value="notmyemail@notmydomain.com" class="cly_user_ignore"&gt;&lt;/p&gt;

&lt;!-- get customfield by class --&gt;
&lt;p&gt;&lt;input type="text" name="custom" id="custom" value="value" class="cly_user_key1"&gt;&lt;/p&gt;

&lt;p&gt;&lt;input id="submit-form" type="submit" value="Submit"&gt;&lt;/p&gt;

&lt;/form&gt;</code></pre>
<h3 id="h_01HBMZRWK6244VCE4TEHVCWP2V">Collect User Data From Facebook</h3>
<p>
  <span style="font-weight: 400;">If your website uses the Facebook JavaScript SDK, you may use this helper method to automatically collect user data from their Facebook accounts. Select the method right after Facebook SDK initialization and optionally set the object with custom properties and graph paths for values on where to receive them.</span>
</p>
<p>
  <span style="font-weight: 400;">Here is an example how to receive data from Facebook, including locations and time zones as custom properties.</span>
</p>
<pre><code class="html">&lt;script src="https://connect.facebook.net/en_US/all.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript"&gt;
FB.init({
    appId: '251676171676751',
    status: true,
    cookie: true,
    oauth: true
});

function CountlyGatherFBData(){
Countly.collect_from_facebook({"location":"location.name", "tz":"timezone"});
};

FB.getLoginStatus(function(stsResp) {
if(stsResp.authResponse) {
CountlyGatherFBData();
} else {
FB.login(function(loginResp) {
if(loginResp.authResponse) {
CountlyGatherFBData();
} else {
alert('Please authorize this application to use it!');
}
});
}
});
&lt;/script&gt;</code></pre>
<h2 id="h_01HABTQ439NRYGR6KNESQ324C1">Attribution</h2>
<p>
  <span style="font-weight: 400;">When using Countly attribution analytics, you may also report conversions to the Countly server, e.g. when a visitor purchases an item or registers on your site.</span>
</p>
<p>
  <span style="font-weight: 400;">If a user visits your website through the Countly campaign link, the campaign information will be automatically stored by default for this user and used when reporting conversion.&nbsp;</span><span style="font-weight: 400;">If conversion has not yet been reported, the campaign information will be overwritten when that user visits through another campaign link. When you report the conversion, it would report the latest campaign user used to access your website.</span>
</p>
<p>
  <span style="font-weight: 400;">However, you may also overwrite that data and provide any specific campaign ID for which you would like to report conversion.</span>
</p>
<p>
  <span style="font-weight: 400;">Conversion will not be reported if there is no stored campaign data and you have yet to provide a campaign ID.</span>
</p>
<p>
  <span style="font-weight: 400;">Note: Conversion for each user may only be reported once, all other conversions will be ignored for that same user.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//user stored conversion data
Countly.q.push(['recordDirectAttribution']);

//or provide campaign id yourself
Countly.q.push(['recordDirectAttribution', "MyCampaignID"]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//user stored conversion data
Countly.recordDirectAttribution();

//or provide campaign id yourself
Countly.recordDirectAttribution("MyCampaignID");</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ43AR08YAAFCYHP7BGEB">Track Link Clicks</h2>
<p>
  <span style="font-weight: 400;">This method will track clicks to specific links and will report events with the </span><strong>linkClick</strong><span style="font-weight: 400;">&nbsp;key as well as the link's text, ID, and URLs as segments.</span>
</p>
<p>
  <span style="font-weight: 400;">All links will automatically be tracked by default for the entire page, but you may provide the parent node as a parameter for which to track link clicks.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['track_links']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.track_links();</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">As soon as you include this one-liner coder, you will automatically be able to see the "linkClick" event in your dashboard as data flows in with the text, ID, and URLs as segments.</span>
</p>
<h2 id="h_01HABTQ43AQV3TMMG716ENREFR">Track Form Submissions</h2>
<p>
  <span style="font-weight: 400;">This method will automatically track form submissions and collect form data. It will then input values in the form and report them as a Event with the <strong>formSubmit</strong>&nbsp;key.</span>
</p>
<p>
  <span style="font-weight: 400;">All forms will automatically be tracked by default for the entire page, but you may provide the parent node as a parameter for which to track forms.</span>
</p>
<p>
  <span style="font-weight: 400;">The second parameter controls whether to collect hidden inputs or not. Hidden inputs are not collected by default.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//will not collect hidden inputs
Countly.q.push(['track_forms']);

//will collect hidden inputs
Countly.q.push(['track_forms', null, true]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//will not collect hidden inputs
Countly.track_forms();

//will collect hidden inputs
Countly.track_forms(null, true);</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ43AM1Q4PMAZJT39H8XZ">Using the Web SDK in Webview</h2>
<p>
  <span style="font-weight: 400;">If you are going to use the Web SDK in the Webview of your app, there are prerequisites that must be checked to ensure it is fully functioning. There are no known iOS issues at this moment, but some specific settings need to be enabled for Android.</span>
</p>
<p>
  <span style="font-weight: 400;">Ensure JavaScript has been enabled for your Webview</span>
</p>
<pre><code class="java">myWebView.getSettings().setJavaScriptEnabled(true);<br></code></pre>
<p>
  <span style="font-weight: 400;">Ensure local storage has been enabled</span>
</p>
<pre><code class="java">//change the path to where you want to store local storage data
myWebView.getSettings().setDomStorageEnabled(true);
myWebView.getSettings().setDatabaseEnabled(true);
if (Build.VERSION.SDK_INT &lt; Build.VERSION_CODES.KITKAT) {
    myWebView.getSettings().setDatabasePath("/data/data/" + myWebView.getContext().getPackageName() + "/databases/");
}</code></pre>
<p>
  <span style="font-weight: 400;">If you would like to use Countly both in the native app and Webview, then you would maybe also like to match the device_id between them, so the transitions may be seamless and you may continue to track events and data from both for the same user.</span>
</p>
<p>
  <span style="font-weight: 400;">In this case, there are a couple things you should do: </span>
</p>
<ol>
  <li>
    <span style="font-weight: 400;">Defer initializing Countly by putting the initialization code in some function. </span>
  </li>
  <li>
    <span style="font-weight: 400;">Do not track sessions in Webview as they are already tracked by the native app. </span>
  </li>
  <li>
    <span style="font-weight: 400;">Pass the device_id to Webview and run the initialization function once Webview has loaded.</span>
  </li>
</ol>
<pre><code class="html">&lt;!--Countly script in webview--&gt;
&lt;script type='text/javascript'&gt;
  var Countly = Countly || {};
  Countly.q = Countly.q || [];
  
  //provide countly initialization parameters
  Countly.app_key = "YOUR_APP_KEY";
  Countly.url = "http://yourdomain.com"; 
  
  //track views or anything else you want to track
  Countly.q.push(['track_pageview']);
  
  //function to initialize Countly
  function InitializeCountly(device_id) {
    
    //assign passed device_id
    Countly.device_id = device_id;
    
    //load countly script
    var cly = document.createElement('script'); cly.type = 'text/javascript'; 
    cly.async = true;
    //enter url of script here
    cly.src = 'https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.min.js';
    cly.onload = function(){Countly.init()};
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(cly, s);
  };
&lt;/script&gt;</code></pre>
<p>
  <span style="font-weight: 400;">Then, on the native app side, all you have to do is call the JavaScript functions in the Webview and pass on the device_id to complete this function.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Android</span>
    <span class="tabs-link">iOS</span>
  </div>
  <div class="tab">
    <pre><code class="java">myWebView.loadUrl("javascript:InitializeCountly('"+device_id+"');");</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="objectivec">#import "CountlyDeviceInfo.h"

NSString \*js = [NSString stringWithFormat: @"InitializeCountly('%@');", CountlyDeviceInfo.sharedInstance.deviceID];
[myWebView stringByEvaluatingJavaScriptFromString:js];</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ43AGMDVXDS3GVJS4JKT">Tracking Users with Javascript Disabled</h2>
<p>
  <span style="font-weight: 400;">In some cases, a user might have JavaScript disabled, meaning normal ways of tracking those users will prove ineffective. In such a case, you may use the transparent 1px x 1px image hosted on your Countly server as reporting the URL and report all the same&nbsp;<a href="https://api.count.ly/reference#i">parameters as all the SDKs have been described here</a>.</span>
</p>
<p>
  <span style="font-weight: 400;">Assuming your Countly is hosted at domain.com and the app_key is "12345", the default setup should look like this:</span>
</p>
<pre><code class="html">&lt;noscript&gt;&lt;img src='http://domain.com/pixel.png?app_key=12345&amp;begin_session=1'/&gt;&lt;/noscript&gt;</code></pre>
<p>
  <span style="font-weight: 400;">Simply place it anywhere in your HTML code and it should only work if JavaScript is disabled, which means SDK tracking won't work.</span>
</p>
<p>
  <span style="font-weight: 400;">This would then track how many total sessions there are in where users have JavaScript disabled. The server will attach the device_id as a no_js by default and add the user profile name as ‘No JS’, so you may easier identify how many users without JavaScript you have.</span>
</p>
<p>
  <span style="font-weight: 400;">However, as mentioned before, this accepts any parameters as a normal SDK endpoint does. Thus, if you dynamically generate data via the server, you may also dynamically generate this URL to provide information that you have about the user. That might be the device_id parameter (for identification), OS, OS version, and any other metrics or information you have, as for example</span>
</p>
<pre><code class="html">&lt;noscript&gt;&lt;img src='http://domain.com/pixel.png?app_key=12345&amp;device_id=test@test.com&amp;begin_session=1&amp;metrics={"_os":"Android", "_os_version":"4.1"}'/&gt;&lt;/noscript&gt;</code></pre>
<h2 id="h_01HABTQ43AANJH2V30NHD2NE2Y">Multiple Trackers on the Same Domain</h2>
<p>
  <span style="font-weight: 400;">Sometimes you would like to track different parts of the same domain/website as separate applications.</span>
</p>
<p>
  <span style="font-weight: 400;">If you just instantiate the Countly SDK in both places, but with different app IDs, then both of their continuous storages will clash storing information for both apps. There are times when this is exactly what you would like to have happen. Generally, it’s function will share a device_id, and although they might be storing requests together, each will be sent to a different app on the same server.</span>
</p>
<p>
  <span style="font-weight: 400;">However, there are situations where you would like to keep them completely separate. To do so you will need to provide a namespace for the different trackers to keep their local storages from clashing.</span>
</p>
<p>
  <span style="font-weight: 400;">Simply providing a&nbsp;<strong>namespace&nbsp;</strong>as the init option will suffice.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.debug = false;
Countly.app_key = "YOUR_APP_KEY";
Countly.device_id = "1234-1234-1234-1234";
Countly.url = "https://try.count.ly";
Countly.namespace = "forum";

Countly.init();</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
    debug:false,
    app_key:"YOUR_APP_KEY",
    device_id:"1234-1234-1234-1234",
    url: "https://try.count.ly",
    namespace: "forum"
});</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ43AKKXMYMADY4MDVSK3">Cross Website/Domain Tracking</h2>
<p>
  <span style="font-weight: 400;">You will need to use the same device_id value on the same user in both places to track the same user across different websites or domains.</span>
</p>
<p>
  <span style="font-weight: 400;">This may be achieved by passing the device ID as a URL parameter when transferring a user from one website/domain to the other.</span>
</p>
<p>
  <strong><span style="font-weight: 400;">Simply take the device ID value from <strong>Countly.device_id</strong>&nbsp;and pass it as a URL parameter named&nbsp;<strong>cly_device_id</strong>&nbsp;as follows:&nbsp;<a href="http://newdomain.com/?cly_device_id=your-user-device-id">http://newdomain.com/?cly_device_id=your-user-device-id.</a></span></strong>
</p>
<h2 id="h_01HABTQ43AA30412AKD86MA7RN">Tracked Cookie List and Explanations</h2>
<p>
  By default, Countly Web SDK uses local storage to keep information between page
  views, but if local storage is not available, Web SDK will try to fallback to
  cookies.
</p>
<ul>
  <li>
    <strong>cly_queue</strong> - a queue of requests that will be made to the
    server and acknowledged
  </li>
  <li>
    <strong>cly_event</strong> - a queue of events reported by SDK
  </li>
  <li>
    <strong>cly_remote_configs</strong> - cached remote config from server
  </li>
  <li>
    <strong>cly_ignore</strong> - ignore the user and do not track anything if
    this is set to true
  </li>
  <li>
    <strong>cly_id</strong> - current user's device id
  </li>
  <li>
    <strong>cly_cmp_id</strong> - last campaign id user came from
  </li>
  <li>
    <strong>cly_cmp_uid</strong> - user identifier for last campaign
  </li>
  <li>
    <strong>cly_session</strong> - timestamp when the last session started so
    we would not call begin_session on each page load
  </li>
  <li>
    <strong>cly_token</strong> - token passed for retrieving heat map data from
    the server
  </li>
  <li>
    <strong>cly_old_token</strong> - to detect token expiration and reset for
    action map data
  </li>
</ul>
<h2 id="h_01HABTQ43AX124FHNAA6RMGXPT">Multi Instancing</h2>
<p>
  You can initialize Countly multiple times at the same page with different app
  keys to send information to different apps you own and gather data with higher
  flexibility and precision. These new instances have all functionality of Countly
  but depending on your init configuration they would behave differently. You can
  attach different events to different Countly instances to send events to specific
  applications even from the same button trigger or much more. A simple integration
  example would be:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">
Countly = Countly || {};
Countly.q = Countly.q || [];

// initializing first instance, which will be global Countly
Countly.init({
  app_key: "YOUR_APP_KEY_1",
  url: "https://try.count.ly" //your server goes here
})
// report event to first app
Countly.add_event({
  key:"first_app"
});

// initialize second instance for another app 
Countly.q.push(["init", {
  app_key: "YOUR_APP_KEY_2", //must have different APP key
  url: "https://try.count.ly" //your server goes here
}])
// report event to second app asynchronously by passing app key as first argument
Countly.q.push(["YOUR_APP_KEY_2", "add_event", {
  key:"second_app"
}]);
    </code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">
// initializing first instance, which will be global Countly
Countly.init({
  app_key: "YOUR_APP_KEY_1",
  url: "https://try.count.ly" //your server goes here
})
// report event to first app
Countly.add_event({
  key:"first_app"
});

// initialize second instance for another app
var Countly2 = Countly.init({
  app_key: "YOUR_APP_KEY_2", //must have different APP key
  url: "https://try.count.ly" //your server goes here
});
// report event to second app
Countly2.add_event({
  key:"second_app"
});
    
    </code></pre>
  </div>
</div>
<h2 id="h_01HABTQ43ACRHQSY8263SJR14V">SDK Internal Limits</h2>
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
    <strong>maxSegmentationValues</strong> - 100 dev entries. Entries that exceed
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
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.debug = false;
Countly.app_key = "YOUR_APP_KEY";
Countly.device_id = "1234-1234-1234-1234";
Countly.url = "https://try.count.ly";
Countly.max_key_length = 500;
Countly.max_value_size = 12;
Countly.max_segmentation_values = 23;
Countly.max_breadcrumb_count = 80;
Countly.max_stack_trace_lines_per_thread = 50;
Countly.max_stack_trace_line_length = 300;
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
    debug:false,
    app_key:"YOUR_APP_KEY",
    device_id:"1234-1234-1234-1234",
    url: "https://try.count.ly",
    max_key_length: 500,
    max_value_size: 12,
    max_segmentation_values: 23,
    max_breadcrumb_count: 80,
    max_stack_trace_lines_per_thread: 50,
    max_stack_trace_line_length: 300
});</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ43ANW678JF8N6G72CJ3">Setting Maximum Request Queue Size</h2>
<p>
  When you initialize Countly, you can specify a value for the queue_size flag.
  This flag limits the number of requests that can be stored in the request queue
  when the Countly server is unavailable or experiencing connection problems.
</p>
<p>
  If the server is down, requests sent to it will be queued on the device. If the
  number of queued requests becomes excessive, it can cause problems with delivering
  the requests to the server, and can also take up valuable storage space on the
  device. To prevent this from happening, the queue_size flag limits the number
  of requests that can be stored in the queue.
</p>
<p>
  If the number of requests in the queue reaches the queue_size limit, the oldest
  requests in the queue will be dropped, and the newest requests will take their
  place. This ensures that the queue doesn't become too large, and that the most
  recent requests are prioritized for delivery.
</p>
<p>
  If you do not specify a value for the queue_size flag, the default setting of
  1,000 will be used.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.queue_size = 5000;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
    app_key:"YOUR_APP_KEY",
    url: "https://try.count.ly",
    queue_size: 5000
});</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ43A2MJG968002T4DJVD">UTM Tags</h2>
<p>
  If you are providing possible users links to your website, and if you would like
  to track those users who have clicked those links, you can do so by using some
  utm tags within your links and Countly web SDK would recognize and record these
  users for you.
</p>
<p>
  The web SDK offers you two options to set these tags in your links. First you
  can use the default tags that has been set to be recognized by the SDK by default.
  These tags are 'source', 'medium', 'campaign', 'term' and 'content'. If you add
  any or all of these tags into your links as query Countly would recognize and
  record them accordingly. An example usage of the default tags is as follows:
</p>
<pre><code class="javascript">
// basic structure of a link that contains all available default tags
yourUrl + ?utm_source=someValue&amp;utm_medium=someValue&amp;utm_campaign=someValue&amp;utm_term=someValue&amp;utm_content=someValue

//or you can omit tags
yourUrl + ?utm_source=someValue&amp;utm_campaign=someValue

// yourUrl is the url of your site and someValue is any string value you want to pass
</code></pre>
<p>
  Second option is to define your custom utm tags during the initialization of
  Countly and use those tags in your links. You have to provide a map of key value
  pairs where the key is the tag and the value is 'true' if you want the Countly
  to check for that key in your links:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">
Countly.app_key = "YOUR_APP_KEY";
Countly.device_id = "1234-1234-1234-1234";
// add your custom tags and set their value to true
Countly.utm = {tag1: true, tag2: true};

// then your links should look like this:
yourUrl + ?utm_tag1=someValue&amp;utm_tag2=someValue
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
    app_key:"YOUR_APP_KEY",
    device_id:"1234-1234-1234-1234",
    // add your custom tags and set their value to true
    utm: {tag1: true, tag2: true}
});

// then your links should look like this:
yourUrl + ?utm_tag1=someValue&amp;utm_tag2=someValue
</code></pre>
  </div>
</div>
<p>
  The values you have provided will be captured and stored as user properties,
  under the keys 'utm_source', 'utm_medium', 'utm_campaign', 'utm_term' and 'utm_content'
  if you have used the default tags or as 'utm_yourCustomTag1', 'utm_yourCustomTag1'...
  if you have used custom tags, together with the corresponding user when a user
  clicks that link. This will enable you to segment users in all places around
  the dashboard, where granular data is used and segmentation capabilities are
  provided.
</p>
<h2 id="h_01HABTQ43AZ2SGCM5M5MJ7YJRS">GA Adapter</h2>
<p>
  If you are using Google Universal Analytics in your website and you would also
  like to integrate Countly to your project, GA Adapter plugin can help you send
  your Google Analytics data also to your Countly server without any extra integration.
  This plugin will recognize your Google Analytics data and convert them into Countly
  events and send it to your server, so you can observe your analytics data from
  your Countly dashboard with ease.
</p>
<p>
  There are 3 steps you have to follow to enable the GA Adapter plugin:
</p>
<ol>
  <li>
    First integrate Countly into your project (You can reach details from
    <a href="https://support.count.ly/hc/en-us/articles/360037441932-Web-analytics-JavaScript-#minimal-setup">here</a>)
  </li>
  <li>
    Then declare the plugin script before your Google Analytics implementation
    block
  </li>
  <li>
    Finally, add 'CountlyGAAdapter();' into your Google Analytics snippet
  </li>
</ol>
<p>A simple implementation would look something like this:</p>
<div>
  <pre><span>// ...<br>// ... &nbsp; &nbsp;</span><br><span>// ... Countly implementation was here</span><br><span>// </span><span>&lt;/</span><span>script</span><span>&gt;</span><br><br><span>// write the correct path to the GA plugin depending on your project structure</span><br><span>&lt;</span><strong>script</strong><span> </span><span>src</span><span>=</span><span>"../plugin/ga_adapter/ga_adapter.js"</span><span>&gt;</span><span>&lt;</span><span>/</span><strong>script</strong><span>&gt;</span><br><br>// Google Analytics implementation<br><span>&lt;</span><strong>script</strong><span>&gt;</span><br><span>(</span><span>function</span><span>(</span><span>i</span><span>,</span><span>s</span><span>,</span><span>o</span><span>,</span><span>g</span><span>,</span><span>r</span><span>,</span><span>a</span><span>,</span><span>m</span><span>){</span><span>i</span><span>[</span><span>'GoogleAnalyticsObject'</span><span>]</span><span>=</span><span>r</span><span>;</span><span>i</span><span>[</span><span>r</span><span>]</span><span>=</span><span>i</span><span>[</span><span>r</span><span>]</span><span>||</span><span>function</span><span>(){</span><br><span>(</span><span>i</span><span>[</span><span>r</span><span>].</span><span>q</span><span>=</span><span>i</span><span>[</span><span>r</span><span>].</span><span>q</span><span>||</span><span>[]).</span><span>push</span><span>(</span><span>arguments</span><span>)},</span><span>i</span><span>[</span><span>r</span><span>].</span><span>l</span><span>=</span><span>1</span><span>*new</span><span> Date</span><span>();</span><span>a</span><span>=</span><span>s</span><span>.</span><span>createElement</span><span>(</span><span>o</span><span>),</span><br><span>m</span><span>=</span><span>s</span><span>.</span><span>getElementsByTagName</span><span>(</span><span>o</span><span>)[</span><span>0</span><span>];</span><span>a</span><span>.</span><span>async</span><span>=</span><span>1</span><span>;</span><span>a</span><span>.</span><span>src</span><span>=</span><span>g</span><span>;</span><span>m</span><span>.</span><span>parentNode</span><span>.</span><span>insertBefore</span><span>(</span><span>a</span><span>,</span><span>m</span><span>)</span><br><span>})(</span><span>window</span><span>,</span><span>document</span><span>,</span><span>'script'</span><span>,</span><span>'https://www.google-analytics.com/analytics.js'</span><span>,</span><span>'ga'</span><span>);</span><br><br><span>// add this line into your google analytics snippet to use the GA plugin</span><br><span>CountlyGAAdapter</span><span>();</span><br><br>// now Countly will recognize the GA commands like below and send them to your Countly server too<br><span>ga</span><span>(</span><span>'create'</span><span>,</span><span> </span><span>'UA-56295140-3'</span><span>,</span><span> </span><span>'auto'</span><span>);</span><br><span>ga</span><span>(</span><span>'send'</span><span>,</span><span>'event'</span><span>,</span><span>'category'</span><span>,</span><span>'action'</span><span>,</span><span>'label'</span><span>);</span><br><span>ga</span><span>(</span><span>'send'</span><span>,</span><span>'pageview'</span><span>,</span><span>'page.html'</span><span>);</span><br><span>&lt;/</span><strong>script</strong><span>&gt;</span></pre>
</div>
<div class="callout callout--info">
  <p>
    You can reach to an example implementation of this plugin from the following
    link:
  </p>
  <p>
    <a href="https://github.com/Countly/countly-sdk-web/blob/master/examples/example_ga_adapter.html">GA Adapter Example</a>
  </p>
</div>
<h2 id="h_01HH1BABFQ48FKWGJCX9HFMKW8">Running the SDK in Web Worker Context</h2>
<p>
  SDK can be used in a dedicated Worker if needed. Currently Module Workers are
  not supported so instead the SDK should be imported by
  <code>importScripts</code> method. It would look something like this:
</p>
<pre><code>// Path or URL
importScripts("../path/to/countly.js");</code></pre>
<p>
  After importing the Countly script in your worker, you can call the Countly methods
  as usual. However, Countly in Web Workers has limited availability. Currently
  only the manual tracking methods are supported. Moreover the SDK would not use
  persistent storage by default. But now it extends its storage methods with which
  you can provide your own storage logic to make things persistent.
</p>
<p>
  A sample worker (let's say 'worker.js') could look like this:
</p>
<pre><code>importScripts("../path/to/countly.js"); // CDN is possible

const STORE={}; // in-memory storage for worker

Countly.init({
    app_key: "YOUR_APP_KEY",
    url: "https://your.domain.countly",
    debug: true,
    storage: {
        // getItem will recieve a string key param with which it should return the item under it
        getItem: function (key) {
            return STORE[key];
        },
        // setItem will recieve two params, a string key and a value of any type, then it should store the value under the key
        setItem: function (key, value) {
            STORE[key] = value;
        },
        // removeItem will recieve a string key with which it should erase the key and any data under that key
        removeItem: function (key) {
            delete STORE[key];
        }
    }
});

onmessage = function (e) {
    console.log(`Worker: Message received from main script:[${JSON.stringify(e.data)}]`);
    
    // Get an process messages to worker
    const data = e.data.data; const type = e.data.type;

    if (type === "event") { // you can send an event
        Countly.add_event(data);
    } else if (type === "view") { // you can record a view
        Countly.track_pageview(data);
    } else if (type === "session") { // you can manually control sessions
        if (data === "begin_session") {
            Countly.begin_session();
            return;
        }
        Countly.end_session(null, true);   
    }
}</code></pre>
<p>
  In your website, an example communication can happen like this with the worker:
</p>
<pre><code>// create a worker
const myWorker = new Worker("worker.js");

// send messages to the Worker
function clickEvent() { // send event
    myWorker.postMessage({ type: "event", data: myEvent });
}
function recordView() { // track views
    myWorker.postMessage({ type: "view", data: "home_page" });
}
function beginSession() { // start a session
    myWorker.postMessage({ type: "session", data: "begin_session" });
}
function endSession() { // end a session
    myWorker.postMessage({ type: "session", data: "end_session" });
}
</code></pre>
<h1 id="h_01HABTQ43BRSHEYT75ZF6AN6F5">FAQ</h1>
<h2 id="h_01HABTQ43BDS23GY6NZ32SFCZD">Can I integrate Countly Web SDK to my TypeScript Project</h2>
<p>
  TypeScript is a strict syntactical superset of JavaScript. It helps you catch
  errors early by adding static typing to the language. It compiles down to basic
  JavaScript so it can be used anywhere JavaScript can run, whether Node.js or
  browser.
</p>
<p>
  Countly Web SDK is written in basic JavaScript so it is compatible with your
  TypeScript projects by enabling allowJs in your project's tsconfig.json file.
  However as we use javascript features that can run in the browser, your project
  must also be runnable on the browser.
</p>
<h2 id="h_01HABTQ43BR11WKJMFP8FAQDC4">Ignoring your own bots</h2>
<p>
  The default behavior of Countly Web SDK is to ignore bots crawling your site
  to provide you a more accurate user analytics data. However, Countly can't detect
  and block all bots crawling the internet as we use the userAgent string to detect
  bots and spammy bots can hide by providing conventional UserAgent. However, this
  is not the case for a bot that you have created your own.
</p>
<p>
  To include your bots to be also ignored by the Countly Web SDK you have to include
  'CountlySiteBot' in your userAgent string. This enables your SDK to recognize
  your bot as one of the bots to be ignored and the SDK would stop recording data
  for your bot.
</p>
<h2 id="h_01HABTQ43BBV94B0EJQMBQX95Q">
  Why aren’t I able to see AngularJS errors on the Countly dashboard?
</h2>
<p>
  AngularJs swallows errors by default. You will need to extend Angular's
  <code>$exceptionHandler</code> to call <code>Countly.log_error()</code>. For
  more information,
  <a href="https://www.bennadel.com/blog/2542-logging-client-side-errors-with-angularjs-and-stacktrace-js.htm">see this blog post</a>.
</p>
<h2 id="h_01HABTQ43BBK9TZJ0JQMCWTRTY">Incognito mode and ad blockers</h2>
<p>
  Incognito mode prevents the browser from storing cookies and other site data.
  Cookies are small files that websites use to track user activity, remember preferences,
  and provide personalized experiences. In incognito mode, cookies are not saved.
  This means that any information our SDK saves in the browser's local storage
  would be gone the next time the user opens their incognito browser. These things
  include things like device ID and event/request queues. Each time a person visits
  a Countly integrated website in incognito mode, they would be perceived as a
  new user. This can be mitigated by having an authentication page on your website.
</p>
<p>
  Ad blockers employ various techniques to identify and block unwanted requests,
  such as analyzing URL patterns, known tracking domains, or specific JavaScript
  code snippets. They can also detect and block requests made to known analytics
  or tracking services, making it possible for them to block requests made to the
  Countly server from our SDKs. This can result in incomplete or missing data,
  as the blocked requests may not reach the Countly server for processing. This
  is a possibility, but not all ad blockers would be blocking our requests, depending
  on their filter settings.
</p>
<p>
  To mitigate this issue to a certain extent, you can enable force using the POST
  method for all requests with the SDK. Switching to a POST request can make it
  slightly harder for ad blockers to detect and block the request, as the parameters
  are sent in the request body instead of the URL. However, it doesn't make the
  request invisible or immune to blocking. Ad blockers can still analyze network
  traffic and inspect the request headers and payload, so if your server is Countly
  hosted and the domain name is in the filter of the ad blocker, it would still
  be blocked.
</p>
