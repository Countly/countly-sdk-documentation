<p>
  This documentation is for the Countly Web SDK version 25.4.X. The SDK source
  code repository can be found
  <a href="https://github.com/Countly/countly-sdk-web">here</a>.
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
      <td class="wysiwyg-text-align-center" style="width: 63.8516px; height: 36px;">
        <strong>IE</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 38.4453px; height: 36px;">
        <strong>Edge</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 55.4766px; height: 36px;">
        <strong>Firefox</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 77px; height: 36px;">
        <strong>Firefox (Android)</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 50.375px; height: 36px;">
        <strong>Opera</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 66.7578px; height: 36px;">
        <strong>Opera (Mobile)</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 49.6406px; height: 36px;">
        <strong>Safari</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 49.6406px; height: 36px;">
        <strong>Safari (iOS)</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 60.7891px; height: 36px; text-align: center; vertical-align: middle;">
        <strong>Chrome</strong>
      </td>
      <td class="wysiwyg-text-align-center" style="width: 77.0234px; height: 36px;">
        <strong>Chrome (Android)</strong>
      </td>
    </tr>
    <tr style="height: 22px; padding: 2px;">
      <td class="wysiwyg-text-align-center" style="width: 63.8516px; height: 10px;">10</td>
      <td class="wysiwyg-text-align-center" style="width: 38.4453px; height: 10px;">12</td>
      <td class="wysiwyg-text-align-center" style="width: 55.4766px; height: 10px;">21</td>
      <td class="wysiwyg-text-align-center" style="width: 77px; height: 10px;">96</td>
      <td class="wysiwyg-text-align-center" style="width: 50.375px; height: 10px;">15</td>
      <td class="wysiwyg-text-align-center" style="width: 66.7578px; height: 10px;">64</td>
      <td class="wysiwyg-text-align-center" style="width: 49.6406px; height: 10px;">6</td>
      <td class="wysiwyg-text-align-center" style="width: 49.6406px; height: 10px;">6</td>
      <td class="wysiwyg-text-align-center" style="width: 60.7891px; height: 10px;">23</td>
      <td class="wysiwyg-text-align-center" style="width: 77.0234px; height: 10px;">98</td>
    </tr>
  </tbody>
</table>
<p>
  To examine the example integrations please have a look
  <a href="#h_01HPE4EQ9TKCMJ0R2XN3BAYVND">here</a>.
</p>
<h1 id="h_01HABTQ436ACJV96Q5P2MMNGWZ">Adding the SDK to the Project</h1>
<p>
  <span style="font-weight: 400;">To track your web pages (SPA, MPA or mobile applications that consist of HTML5 views) and browser extensions, you can use Countly Web SDK.</span>
</p>
<p>
  <span style="font-weight: 400;">It is automatically hosted on your Countly server as a UMD file:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">minified</span>
    <span class="tabs-link">non-minified</span>
  </div>
  <div class="tab">
    <pre><code class="bash">https://yourdomain.com/sdk/web/countly.min.js</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="bash">https://yourdomain.com/sdk/web/countly.js</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Optionally, you may also use package managers to gain access to the SDK:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">npm</span>
    <span class="tabs-link">yarn</span>
  </div>
  <div class="tab">
    <pre><code class="bash">npm install countly-sdk-web</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="bash">yarn add countly-sdk-web</code></pre>
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
<a href="https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.js" target="_blank" rel="noopener noreferrer">cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.js</a>

// latest minified
<a href="https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.min.js" target="_blank" rel="noopener noreferrer">cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.min.js</a></code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">// 25.4.1 non minified
<a href="https://cdn.jsdelivr.net/npm/countly-sdk-web@25.4.1/lib/countly.js" target="_blank" rel="noopener noreferrer">cdn.jsdelivr.net/npm/countly-sdk-web@25.4.1/lib/countly.js</a>

// 25.4.1 minified (<span>JSDelivr</span> or Cloudflare)
<a href="https://cdn.jsdelivr.net/npm/countly-sdk-web@25.4.1/lib/countly.min.js" target="_blank" rel="noopener noreferrer">cdn.jsdelivr.net/npm/countly-sdk-web@25.4.1/lib/countly.min.js</a> <br>or<br><a href="https://cdnjs.cloudflare.com/ajax/libs/countly-sdk-web/25.4.1/countly.min.js" target="_blank" rel="noopener noreferrer">cdnjs.cloudflare.com/ajax/libs/countly-sdk-web/25.4.1/countly.min.js</a></code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Lastly as an alternative option, you may download <a href="https://github.com/Countly/countly-sdk-web/tree/master/lib">countly.min.js</a> from our GitHub repository and upload it to any server from where you would like to host it.</span>
</p>
<h1 id="h_01HABTQ436KQ0HD0G5NXFBZQR7">SDK Integration</h1>
<h2 id="h_01HABTQ4360WX3SY413Z3ZSAWZ">Minimal Setup</h2>
<p>
  <span style="font-weight: 400;">The SDK is a single UMD file which can be loaded directly to your HTML file or can be imported with a package manager to your project and bundled with your bundler to your build.</span>
</p>
<p>
  <span style="font-weight: 400;">You may use the Countly Web SDK synchronously or asynchronously. Asynchronous usage would work without blocking content loading. This would also allow you to use Countly while the Countly script has not yet been loaded. This can be done by pushing function calls into the </span><strong>Countly.q</strong><span style="font-weight: 400;"> queue, which SDK will execute after it is initialized.</span>
</p>
<p>
  Here you would also need to provide your Countly server app's application key
  and server URL. Please check
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#acquiring-your-application-key-and-server-url">here</a>
  for more information on how to acquire your application key (APP_KEY) and server
  URL.
</p>
<div class="callout callout--info">
  <p>
    You can check all the config options you can use to manipulate the SDK behaviour
    from
    <a href="/hc/en-us/articles/4409195031577#h_01HABTQ439HZN7Y6A6F07Y6G0K" target="_blank" rel="noopener noreferrer">here</a>.
  </p>
</div>
<p>
  <span style="font-weight: 400;">An example setup would look like this:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">npm/yarn</span>
    <span class="tabs-link">HTML (Async)</span>
    <span class="tabs-link">HTML (Sync)</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">import Countly from "countly-sdk-web";

Countly.init({<br>  // server credentials
  app_key: "YOUR_APP_KEY",
  url: "http://yourdomain.com"
});

// Track sessions and page views automatically (recommended)
Countly.track_sessions();
Countly.track_pageview();</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="html">&lt;!--inside &lt;head&gt;&lt;/head&gt;--&gt;
&lt;script type='text/javascript'&gt;
var Countly = Countly || {};
Countly.q = Countly.q || [];
<br>// server credentials 
Countly.app_key = "YOUR_APP_KEY"; 
Countly.url = "https://yourdomain.com";

// Track sessions and page views automatically (recommended)
Countly.q.push(['track_sessions']);
Countly.q.push(['track_pageview']);

// Load Countly script asynchronously
(function() {
  var cly = document.createElement('script'); cly.type = 'text/javascript';
  cly.async = true;
  cly.src = 'https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.min.js';
  cly.onload = function(){Countly.init()};
  var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(cly, s);
})();
&lt;/script&gt;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="html">&lt;!--inside &lt;head&gt;&lt;/head&gt;--&gt;
&lt;script type='text/javascript' src='https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.min.js'&gt;&lt;/script&gt;
&lt;script type='text/javascript'&gt;

Countly.init({<br>  // server credentials
  app_key: "YOUR_APP_KEY",
  url: "http://yourdomain.com"
});
// Track sessions and page views automatically (recommended)
Countly.track_sessions();
Countly.track_pageview();
&lt;/script&gt;</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">If </span>you are in doubt about the correctness
  of your Countly SDK integration you can learn about the verification methods
  from
  <a style="background-color: #ffffff;" href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#how-to-validate-your-countly-integration" target="blank">here</a>.
</p>
<h1 id="h_01HABTQ437271440T3QZN3DCSN">SDK Logging</h1>
<p>
  If logging is enabled, then our SDK will print out debug messages about its internal
  state (events it's recording and sending) and encountered problems.
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
    <pre><code class="html">Countly.debug = true;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
    debug:true,
    app_key:"YOUR_APP_KEY",
    url: "https://try.count.ly",
});</code></pre>
  </div>
</div>
<p>
  For more information on where to find the SDK logs you can check the documentation
  <a href="https://support.countly.com/hc/en-us/articles/900000908046-Getting-Started-with-SDKs#h_01HABSX9KXC5S8Q1NQWDZ33HXC" target="_blank" rel="noopener noreferrer">here</a>.
</p>
<h1 id="h_01HABTQ4378NGJPGEYQX8X1CWZ">Crash Reporting</h1>
<p>
  <span style="font-weight: 400;">To automatically capture and report <strong>unhandled</strong> JavaScript errors on your website (</span><span style="font-weight: 400;">You can add more information to error reports by providing an object with key/value pairs):</span>
</p>
<div class="tabs"></div>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['track_errors', {
  "your_extra_info_key": your_info
}])</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.track_errors({
  "your_extra_info_key": your_info
})</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">You can also report <strong>handled</strong> exceptions to the server. Optionally you can provide extra information (an object) with the report (or use the ones provided with the <strong>track_errors</strong>&nbsp;method as default ones).</span>
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
  Countly.q.push(['log_error', ex, extra_info]);
}</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">try{
  //do something here
}
catch(ex){
  //report error to Countly
  Countly.log_error(ex, extra_info);
}</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">You can leave breadcrumbs throughout the code on different user actions. These breadcrumbs will then be combined in a single log and reported to the server as well.</span>
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
<h2 id="h_01JK8PC8KHKZ1DF3KMKTEKFCN3">Crash Filtering</h2>
<p>
  You can omit or modify crash reports that SDK generates by crash filtering feature.
  You can provide a callback function which SDK can call when a crash report it
  prepared. Then you can modify or omit the crash according to the information
  present.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">// before init
Countly.crash_filter_callback = function (crashObject) {
      console.log("Crash object:", crashObject);
      // modify, omit or return directly
      return crashObject;
};</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
      app_key: "YOUR_APP_KEY",
      url: "https://yourdomain.com",
      crash_filter_callback: function (crashObject) {
        console.log("Crash object:", crashObject);
        // modify, omit or return directly
        return crashObject;
      }
});</code></pre>
  </div>
</div>
<p>
  The <code>crashObject</code> will include some of these
  <a href="https://support.countly.com/hc/en-us/articles/9290669873305-A-Deeper-Look-at-SDK-Concepts#h_01HJ5V4WX0XFP7FC8ETDC3B96M" target="_blank" rel="noopener noreferrer">metric</a>
  and
  <a href="https://support.countly.com/hc/en-us/articles/9290669873305-A-Deeper-Look-at-SDK-Concepts#h_01HJ5WD48B7TVTNP7TFY0646MK" target="_blank" rel="noopener noreferrer">data</a>
  info. Most important parameter is <code>_error</code>, which you can check for
  string values you are looking for. If you want to prevent sending a crash just
  return <code>null</code> from the callback. If you want to send the report as
  is then you can just directly return it. And finally you can remove/obfuscate
  sensitive information and return the modified crash object in the callback. SDK
  will send the returned object to the server.
</p>
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
    <span class="tabs-link is-active">Obfuscated</span>
    <span class="tabs-link">De-obfuscated</span>
  </div>
  <div class="tab">
    <pre>Error: Error at depth 3<br>  at cause_error (http://127.0.0.1:5501/examples/symbolication/dist/main.js:5657:13)<br>  at multiply (http://127.0.0.1:5501/examples/symbolication/dist/main.js:5651:3)<br>  at saveRecords (http://127.0.0.1:5501/examples/symbolication/dist/main.js:5648:3)<br>  at initializeCoreFunctions (http://127.0.0.1:5501/examples/symbolication/dist/main.js:5645:3)<br>  at save (http://127.0.0.1:5501/examples/symbolication/dist/main.js:5642:3)<br>  at removeHashes (http://127.0.0.1:5501/examples/symbolication/dist/main.js:5639:3)<br>  at calculateParams (http://127.0.0.1:5501/examples/symbolication/dist/main.js:5636:3)<br>  at addRecords (http://127.0.0.1:5501/examples/symbolication/dist/main.js:5633:3)<br>  at HTMLButtonElement.unhandled_error (http://127.0.0.1:5501/examples/symbolication/dist/main.js:5675:5)</pre>
  </div>
  <div class="tab is-hidden">
    <pre>Error: Error at depth 3<br>  at src/index.js:66:12<br>  at cause_error (src/index.js:59:2)<br>  at multiply (src/index.js:56:2)<br>  at saveRecords (src/index.js:53:2)<br>  at initializeCoreFunctions (src/index.js:50:2)<br>  at save (src/index.js:47:2)<br>  at removeHashes (src/index.js:44:2)<br>  at calculateParams (src/index.js:41:2)<br>  at addRecords (src/index.js:87:6)</pre>
  </div>
</div>
<p>
  When using any build tool you will need to choose an option that generates the
  source map as a separate file and not inline with the final js file (<a href="https://webpack.js.org/configuration/devtool/" target="_blank" rel="noopener">devtool</a>
  option for webpack for example). If you set it up correctly your builds will
  produce a source map file ending in <code>.map</code>, which is the source map
  file you will upload to your Countly server.
</p>
<p>
  To start Symbolicating your errors you just need to upload your source map file
  to your Countly instance via the side menu Crashes &gt; Manage Symbols. In this
  view, the source map files you have uploaded are listed. To upload one, you click
  the "Add Debug Symbol File", fill the symbol type and app version fields accordingly
  and upload your <code>.map</code> file. With your source map file uploaded, you
  can Symbolicate the crash reports for that app version on Countly. For more information,
  see
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
  <li>count - number of events (optional) (defaults to 1)</li>
  <li>sum - sum to report with the event (optional)</li>
  <li>dur - duration expressed in seconds (optional)</li>
  <li>segmentation - an object with key/value pairs (optional)</li>
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
  "key": "Survey_success",
  "count": 1,
  "sum": 0,
  "dur": 25,
  "segmentation": {
    "Answer_1": "I would love to",
    "Answer_2": 12
  }
}]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.add_event({
  "key": "Survey_success",
  "count": 1,
  "sum": 0,
  "dur": 25,
  "segmentation": {
    "Answer_1": "I would love to",
    "Answer_2": 12
  }
});</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ437SAGSADF72AW4XEM6">Timed Events</h2>
<p>
  Timed events are SDK's convenience methods to calculate the duration of an activity
  easily. There are three methods available to use to calculate the duration property
  of an event: start_event, cancel_event, and end_event.
</p>
<div class="callout callout--warning">
  <p>
    However, it's important to note that these methods operate on the memory
    layer and shouldn't be used to calculate durations in situations where a
    browser restart/refresh occurs.
  </p>
</div>
<p>
  The start_event method starts an internal timer within the SDK for a given event
  name. This timer works by taking the current timestamp and storing it in memory.
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
  The end_event method stops the timer and creates an event for the given name
  with the calculated duration and adds it to the event queue. You can also pass
  an event object to this method, and in that case, it will use the key value as
  the event name.
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
<div class="callout callout--warning">
  <p>
    If end_event is not called, no event will be sent to the server.
  </p>
</div>
<h1 id="h_01HABTQ437NA2XTXAMAXSQ9MD5">Sessions</h1>
<p>
  Sessions are the continuous time blocks that indicates the user interacts with
  your website. Each recorded interaction after a session starts will be recorded
  under that session until a new session starts.&nbsp;
</p>
<h2 id="h_01HABTQ437C35DZRN4C13RNA7K">Automatic Session Tracking</h2>
<p>
  <span style="font-weight: 400;">To leave session tracking logic to the SDK you can just call:</span>
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
  If you need a custom session logic then you can use manual session methods to:
</p>
<ul>
  <li>Starting a session at the beginning</li>
  <li>Marking the end of a session</li>
</ul>
<p>
  Only use the methods below if you aren’t planning on using the automatic session
  tracking and set the <code>use_session_cookie</code> setting to false during
  init for more granular control of the session.
</p>
<p>
  <span style="font-weight: 400;">SDK will automatically report elapsed session duration with 60 seconds intervals (this can be modified during init with <code>session_update</code> config option).</span>
</p>
<p>
  <strong>Beginning a Session</strong>
</p>
<p>To begin a session:</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['begin_session']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.begin_session();</code></pre>
  </div>
</div>
<p>
  <strong>Ending a session</strong>
</p>
<p>To end a session:</p>
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
  <span style="font-weight: 400;">SDK only provides manual views (you will need to determine when a view starts). Depending on your site's structure (MPA or SPA) you might need to modify how you track page views with the SDK.</span>
</p>
<h2 id="h_01JF056M0Y04NSX2GPN4132W9K">
  <span style="font-weight: 400;">Manual View Recording</span>
</h2>
<p>
  <span style="font-weight: 400;">All views are auto-stopped meaning there can only be one view tracked at a time and it will end at the end of a session or when another one starts.</span>
</p>
<p>
  <span style="font-weight: 400;">You can track the current page that the SDK initialized in by using the method below for MPAs. This uses <code>location.path</code> as the page name and then reports it to the server:</span>
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
  <span style="font-weight: 400;">If <code>location.path</code> as the page name is not useful for you (for Ajax updated contents and single page web applications), pass the page name as a parameter to record the new page view, for example</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['track_pageview', "pagename"]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.track_pageview("pagename");</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Here is a good example if your single-page app uses URL hash:</span>
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
  <span style="font-weight: 400;">If you are relying on the default page name assigned by the SDK you might like to ignore some URLs to exclude from tracking, such as dynamic URLs that include the user ID in the URL, internal URLs, or for any other reason. You may do so by providing another parameter with a list of strings of views to ignore or a list of regular expressions to ignore.</span>
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
  <span style="font-weight: 400;">There are cases when determining the view name requires more complex logic, and in some cases, you will need to separate the URL and the View naming. This way you give a human readable page name, yet you have the valid URL underneath them to view action maps, such as clicks and scrolls.</span>
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
<h2 id="h_01HABTQ438Y2NCA9PE3PZWSXTY">Retrieving Current Device ID</h2>
<p>
  Countly offers a convenience method (<code>get_device_id</code>) for you to get
  the current user's device ID:
</p>
<pre><code class="javascript">var id = Countly.get_device_id();</code></pre>
<p>SDK records the type of an ID. These types are:</p>
<ul>
  <li>
    <code>DEVELOPER_SUPPLIED</code>
  </li>
  <li>
    <code>SDK_GENERATED</code>
  </li>
  <li>
    <code>TEMPORARY_ID</code>
  </li>
</ul>
<p>
  <code>DEVELOPER_SUPPLIED</code> device ID means this ID was assigned by your
  internal logic. <code>SDK_GENERATED</code> device ID means the ID was generated
  randomly by the SDK, and <code>TEMPORARY_ID</code> device ID means the SDK is
  in offline mode.
</p>
<p>
  You can get the device ID type of a user by calling the
  <code>get_device_id_type</code> function:
</p>
<pre><code class="javascript">var idType = Countly.get_device_id_type();</code></pre>
<p>
  You can use the <code>DeviceIdType</code> enums to evaluate the device ID type
  you retrieved:
</p>
<pre><code class="javascript">var idType = Countly.get_device_id_type();
if (idType === Countly.DeviceIdType.SDK_GENERATED) {
  // ...do something
}
</code></pre>
<h2 id="h_01HABTQ438H09ECC7YDDKNN68R">Changing Device ID</h2>
<p>
  <span style="font-weight: 400;">You can change the device ID of a user with set_id method:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(['set_id', "newId"]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.set_id("newId");</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">This method's effect on the server will be different according to the type of the current ID stored in the SDK at the time you call it:</span>
</p>
<ul>
  <li>
    <p>
      <span style="font-weight: 400;">If current stored ID is <code>SDK_GENERATED</code> then in the server all the information recorded for that device ID will be merged to the new ID you provide and old user with the <code>SDK_GENERATED</code> ID will be erased.</span>
    </p>
  </li>
  <li>
    <p>
      <span style="font-weight: 400;">If the current stored ID is <code>DEVELOPER_SUPPLIED</code> or <code>TEMPORARY_ID</code> then in the server it will also create a new user with this new ID if it does not exist.</span>
    </p>
  </li>
</ul>
<div class="callout callout--info">
  <p>
    <span style="font-weight: 400;">If you need a more complicated logic then you will need to use this method mentioned <a href="https://support.countly.com/hc/en-us/articles/31592459504537-Web-analytics-23-12-X#h_01HABTQ438HCZ8FJVAE34W49KP" target="_blank" rel="noopener noreferrer">here</a> instead.</span>
  </p>
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
<h2 id="01JBBJ304CMXVQNECECHTHAAG0">Device ID Generation</h2>
<p>
  By default Countly generates and assigns a random device ID (UUID) to each device
  that visits your website. This ID is saved at the localstorage of the browser.
  Assuming the localstorage is not cleared, this device will be recognized with
  this stored ID from now on.
</p>
<p>Limitations to this method:</p>
<ul>
  <li>
    Multiple users using the same device would be seen as a single user
  </li>
  <li>
    When a user reaches to your website from multiple devices or browsers in
    incognito mode then all devices would be seen as separate users
  </li>
</ul>
<p>
  If these scenarios are an issue of concern to you, you can mitigate them with
  various device management strategies like:
</p>
<ul>
  <li>
    Adding a login/authentication page and assigning device ID there
  </li>
  <li>
    Entering the offline mode (mentioned above) until you identify the user and
    assigning the ID then
  </li>
</ul>
<p>
  You can also provide an ID during init to prevent the SDK from generating a random
  ID:
</p>
<pre><code class="javascript">// adding device ID here will prevent the generation of a random ID
Countly.init({
  app_key:"YOUR_APP_KEY",
  url: "https://your.server",
  device_id:"yourDeviceID",
});</code></pre>
<p>
  You can also provide an ID in the search query of the link that opens your site.
  If you use the param <code>cly_device_id</code> its value will be set as the
  device ID instead of generating a random one:
</p>
<pre><code class="javascript">// you can assign a device ID to a user through a link that you have provided to them by adding cly_device_id to your url query
yoursite.com + ?cly_device_id=yourDeviceID
</code></pre>
<p>
  If you want to erase the previously stored device ID from the storage you can
  set clear_stored_id flag to true at the init config:
</p>
<pre><code class="javascript">// this will erase the stored device ID from the local storage every time the Countly is initialized
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
<h1 id="h_01J0AYW920ZVG0T82DM4ABHXDJ">User Location</h1>
<p>
  With the SDK integrated into your website, you might want to track your user
  location. By default, the Countly Server uses the GeoIP database to deduce a
  user's location from the coming requests (you can check details of it from
  <a href="https://support.count.ly/hc/en-us/articles/4403281285913-User-Visitor-Profiles#h_01HBPA9VW7HRTFJSMHZBA0X9X4" target="_blank" rel="noopener noreferrer">here</a>).
  However the SDK provides the ability to set custom locations for your users.
</p>
<h2 id="h_01J0AYWGFJN5H3E36F8HT59RT5">Setting Location</h2>
<p>
  There are 3 location parameters that can be provided with the SDK:
</p>
<ul>
  <li>
    Country code in the two-letter, ISO standard ("jp", "gr" etc.)
  </li>
  <li>City name ("Kyoto", "Athens" etc.)</li>
  <li>Your user’s IP address</li>
</ul>
<p>
  You can provide any of these information while initializing the SDK:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">// you can directly provide the city and the country code
Countly.city = "Tokyo";
Countly.country_code = "jp";
// or you can provide the ip address
Countly.ip_address = "198.168.1.1";
     
// Initialize the SDK</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
  app_key: "YOUR_APP_KEY",
  url: "https://your.server.ly",
  //  you can directly provide the city and the country code
  city: "Tokyo",
  country_code: "jp",
  // or you can provide the ip address    
  ip_address: "198.168.1.1",
});</code></pre>
  </div>
</div>
<h1 id="h_01HABTQ438V4VMNJPJF0MQECSZ">Heatmaps</h1>
<p>
  Heatmaps feature is a web exclusive plugin that helps you to visualize user interactions
  on your website. Web SDK supports this functionality by providing user click
  and scroll information to your server. Then from your server, you can trigger
  Heatmaps overlay to visualize these click clusters and scroll zones on your website.
</p>
<p>
  To display this overlay the SDK loads certain scripts from your server. To enable
  these scripts to be loaded from somewhere else other than the Countly server
  SDK sends information to (for example your internal server), the SDK offers a
  whitelisting option during the initialization. To whitelist domains other than
  your Countly server you should provide an array of these domains, as String values,
  under the <code>heatmap_whitelist</code> flag during the initialization:
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
  <span style="font-weight: 400;">After you integrate the SDK and start sending click data, all generated heatmaps may be viewed under Analytics &gt; Heatmaps, as shown below:</span>
</p>
<div class="img-container">
  <img src="/guide-media/01GVD4RVE1CE6DH744PPPNTY00" alt="001.png">
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
  <span style="font-weight: 400;">As with Click Heatmaps, collected data is viewable under Analytics &gt; Heatmaps. You may change the heatmap type on the top bar once a view is open.</span>
</p>
<div class="img-container">
  <img src="/guide-media/01GVAYP9A9YBWPDTJK815SX5JD" alt="002.png">
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
  <span style="font-weight: 400;">Automatic Remote Config functionality is disabled by default and needs to be explicitly enabled. When automatic Remote Config is enabled, the SDK will try to fetch it upon some specific triggers. For example, after SDK initialization or changing device ID.</span>
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
  If you want to receive feedback from your users, there are a couple of ways you
  can do that in Countly. Users can leave feedback through Feedback Widgets (Surveys,
  NPS, Ratings). With the help of these widgets, you can ask your customers multiple
  questions and learn about their opinions and preferences in detail.
</p>
<div class="tabs"></div>
<h2 id="h_01HABTQ438NWHSRCMAV4RJJVWX">Feedback Widgets</h2>
<div class="callout callout--info">
  <p>
    Feedback Widgets is a
    <a href="https://countly.com/enterprise" target="_blank" rel="noopener noreferrer">Countly Enterprise</a>
    plugin.
  </p>
</div>
<p>
  It is possible to display 3 kinds of feedback widgets:
  <a href="https://support.count.ly/hc/en-us/articles/4652903481753-Feedback-Surveys-NPS-and-Ratings-#h_01HAY62C2QB9K7CRDJ90DSDM0D" target="_blank" rel="noopener">NPS</a>,
  <a href="https://support.count.ly/hc/en-us/articles/4652903481753-Feedback-Surveys-NPS-and-Ratings-#h_01HAY62C2Q965ZDAK31TJ6QDRY" target="_blank" rel="noopener">Survey</a>
  and
  <a href="https://support.count.ly/hc/en-us/articles/4652903481753-Feedback-Surveys-NPS-and-Ratings-#h_01HAY62C2R4S05V7WJC5DEVM0N" target="_blank" rel="noopener">Rating</a>.
</p>
<p>
  For more detailed information about Feedback Widgets, you can refer to
  <a href="https://support.countly.com/hc/en-us/articles/4652903481753-Feedback-Overview" target="_blank" rel="noopener noreferrer">here</a>.
</p>
<div class="callout callout--warning">
  <p>
    Before any feedback widget can be shown, you need to create them in your
    Countly dashboard.
  </p>
</div>
<p>
  To simply show available widgets to your users you can use the methods available
  through the <code>feedback</code> interface. These methods will take a single
  parameter:
</p>
<ul>
  <li>
    nameTagOrID - String value to select a widget according to its name, tag
    or ID (optional)
  </li>
</ul>
<p>
  If this value is not provided or no widget with the provided parameter can be
  found it will display the first widget available instead:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(() =&gt; { Countly.feedback.showNPS("nameTagOrID"); });<br>Countly.q.push(() =&gt; { Countly.feedback.showSurvey("nameTagOrID"); });<br>Countly.q.push(() =&gt; { Countly.feedback.showRating("nameTagOrID"); });

// or
Countly.q.push(["feedback.showNPS", "nameTagOrID"]);
Countly.q.push(["feedback.showSurvey", "nameTagOrID"]);
Countly.q.push(["feedback.showRating", "nameTagOrID"]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.feedback.showNPS("nameTagOrID");<br>Countly.feedback.showSurvey("nameTagOrID");<br>Countly.feedback.showRating("nameTagOrID");</code></pre>
  </div>
</div>
<div class="callout callout--info">
  <p>
    If you need a more complex logic to display your widgets you can check extended
    documentation from
    <a href="/hc/en-us/articles/360037441932#h_01JF06CEVMYPPTDFTTTJ2DG7F6" target="_blank" rel="noopener noreferrer">here</a>.
  </p>
</div>
<h3 id="h_01HABTQ438KSCZWEFA8GEFE07R">Manual Reporting</h3>
<p>
  Reporting Feedback Widgets manually consists of 3 main steps:
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
      const countlyFeedbackWidget = feedbackList.find(widget = widget.type === widgetType);
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
}</code></pre>
<h2 id="h_01J1YSATYHKAJ8SZMM4KW6BBRT">Consent</h2>
<p>
  If consents are enabled, to use Feedback Widgets you have to provide the 'feedback'
  and the 'star-rating' consents for it to work.
</p>
<h1 id="h_01HABTQ439MH1SD5Q76905BRWP">User Profiles</h1>
<h2 id="h_01HABTQ439KMGT58PHY4MRA1GT">User Details</h2>
<p>
  <span style="font-weight: 400;">You can provide Countly with user information like a username or email address. This will allow you to distinguish user on the "User Profiles" tab, which is available with <a href="http://count.ly/enterprise-edition">Countly Enterprise Edition</a>.</span>
</p>
<div class="callout callout--warning">
  <p>
    If a parameter is set as an empty string, it will be deleted on the server
    side.
  </p>
</div>
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
  app_key:"YOUR_APP_KEY",
  url: "https://try.count.ly",
  enable_orientation_tracking: false //this will disable orientation tracking
});</code></pre>
  </div>
</div>
<h1 id="h_01HABTQ4399MRCTWV2VT19QGGE">Application Performance Monitoring</h1>
<p>
  If you want to record some performance metrics regarding your website there are
  2 ways to report these performance traces with Countly. One way is to construct
  and report them manually. The other is using a plugin that will utilize BoomerangJS
  to collect website's performance data and report it as a performance trace.
</p>
<p>
  You can reach our example implementations of APM with BoomerangJS from the following
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
  Whether you are using Countly synchronously or asynchronously,
  <strong>you should always provide the 'duration' key and its value in apm_metrics</strong>,
  otherwise custom traces won't be recorded.
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
<p>
  This section talks about how to set up GDPR compliant consent management with
  the Countly Web SDK.
</p>
<p>
  If consent management is enabled then features of the SDK would require consent
  to be provided before start working. This way you would have full control over
  your user tracking in every part of your website.
</p>
<p>
  It should be noted that there is no persistency for consent state in the SDK
  and the developer is fully responsible for saving/keeping the state of the user's
  consent before providing it to the SDK.
</p>
<h2 id="h_01HABTQ439DN2P2CKVF8YMBCKD">Feature Names</h2>
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
    <span style="font-weight: 400;">attribution - allows direct attribution tracking</span>
  </li>
  <li>
    <span style="font-weight: 400;">users - allows user information, including custom properties, to be collected/provided</span>
  </li>
  <li>
    <span style="font-weight: 400;">star-rating - allows user rating and feedback tracking through rating widgets</span>
  </li>
  <li>
    <span style="font-weight: 400;">feedback - allows survey, nps and rating widgets usage and reporting</span>
  </li>
  <li>
    <span style="font-weight: 400;">apm - allows performance tracking of application by recording traces</span>
  </li>
  <li>
    <span style="font-weight: 400;">location - allows a user’s location (country, city area) to be recorded</span>
  </li>
  <li>
    <span style="font-weight: 400;">remote-config - allows users to download remote config from the server</span>
  </li>
</ul>
<h2 id="h_01HRECPHGKYPEZQ0HATVXJ2BPC">Setup During Init</h2>
<p>
  <span style="font-weight: 400;">To enable consent management mode ( and to disable tracking until consent is given for a specific feature), all you need to do is pass true to the </span><strong>require_consent</strong><span style="font-weight: 400;"> config flag during SDK initialization</span><span style="font-weight: 400;">.</span>
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
  app_key: "YOUR_APP_KEY",
  url: "https://your.server.ly",
  require_consent: true // this will enable consent management
});</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ4391J4A916V53AVFVP5">Changing Consent</h2>
<p>
  <span style="font-weight: 400;">Upon a visitor’s arrival to your website, you could check if you already have consent from this visitor. If not, you could present them with a popup explaining what will be tracked and allow them to consent to tracking. When a user selects the consent preferences, you should persistently store it, and on each Countly load, let Countly know for which features the user gave consent by calling the <strong>Countly.add_consent</strong> method and passing one or multiple features (as an array). </span>
</p>
<p>
  <span style="font-weight: 400;">Also you can also allow the user to change their mind regarding separate settings and when changes are going to be made you can </span><span style="font-weight: 400;">call the <strong>Countly.add_consent</strong> or <strong>Countly.remove_consent</strong> methods to allow Countly to track specific features or disable tracking for them.</span>
</p>
<p>Here is a high-level example of how it could look:</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">// to add consent {string|array}
Countly.q.push(['add_consent', feature]);

// to remove consent {string|array}
Countly.q.push(['remove_consent', feature]);
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">// to add consent {string|array}
Countly.add_consent(feature)

// to remove consent {string|array}
Countly.remove_consent(feature)</code></pre>
  </div>
</div>
<h2 id="h_01HRECNEJ906HAY7SD4CHN17QR">Feature Groups</h2>
<p>
  Depending on your website and use case, you may also want to combine some of
  the features into one using the <strong>group_features</strong> method.
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
<h1 id="h_01HW5T3ZW11W74T71BGP3N4DD2">Security and Privacy</h1>
<h2 id="h_01HW5T4GA5VER9KA2KX5V9BJ9G">Parameter Tamper Protection</h2>
<p>
  You can set an optional <code>salt</code> for the checksum calculation of request
  data which will be sent alongside each request, using the
  <code>&amp;checksum</code> field. You will need to set the exact same
  <code>salt</code> on the Countly server (Management &gt; Applications&gt; Salt
  for checksum). When the <code>salt</code> on the Countly server is set, all requests
  would be checked for the validity of the <code>&amp;checksum</code> field before
  being processed.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="JavaScript">Countly.app_key = "YOUR_APP_KEY";
Countly.url = "https://yourdomain.com";
Countly.salt = "your_salt";
// init after      
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="JavaScript">Countly.init({
  app_key: "YOUR_APP_KEY",
  url: "http://yourdomain.com",
  salt: "your_salt"
});</code></pre>
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
    <strong>disable_sdk_behavior_settings_updates</strong> -
    <span style="font-weight: 400;">set it to true to disable SDK behavior setting updates (default: false)</span>
  </li>
  <li>
    <strong>disable_backoff_mechanism</strong> -
    <span style="font-weight: 400;">set it to true to disable request backoff when server is busy logic (default: false)</span>
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
    <strong>behavior_settings</strong> - an object that includes server config
    options taken from your server (experimental!)
  </li>
  <li>
    <strong>content_whitelist</strong> - an array that includes urls to your
    other domains which can serve the Content
  </li>
  <li>
    <strong>max_breadcrumb_count</strong> -
    <span style="font-weight: 400;">the maximum amount of breadcrumbs to store for crash logs (default: 100)</span>
  </li>
  <li>
    <strong>ignore_referrers</strong> - array with referrers to ignore (default:
    none)
  </li>
  <li>
    <strong>salt</strong> - string salt for checksums (default: none)
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
    <span><strong>metrics</strong> - provide metrics override or custom metrics for this user. For more information on the specific metric keys used by Countly, check <a href="https://support.countly.com/hc/en-us/articles/9290669873305-A-Deeper-Look-at-SDK-Concepts#h_01HABT18WWYQ2QYPZY3GHZBA9B" target="_blank" rel="noopener noreferrer">here</a>.</span><span></span>
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
<h2 id="h_01HPE4EQ9TKCMJ0R2XN3BAYVND">Example Integrations</h2>
<p>
  Examples are located in
  <a href="https://github.com/Countly/countly-sdk-web/tree/master/examples">examples</a>
  folder.
</p>
<p>
  <a href="https://github.com/Countly/countly-sdk-web/tree/master/examples/Angular">Angular</a>
  folder contains a basic Angular integration.
</p>
<p>
  <a href="https://github.com/Countly/countly-sdk-web/tree/master/examples/react">react</a>
  folder contains a basic React integration.
</p>
<p>
  <a href="https://github.com/Countly/countly-sdk-web/tree/master/examples/Symbolication">Symbolication</a>
  folder covers crash integrations and reporting.
</p>
<p>
  <a href="https://github.com/Countly/countly-sdk-web/tree/master/examples/mpa">mpa</a>
  folder contains basic MPA integration.
</p>
<p>
  <a href="https://github.com/Countly/countly-sdk-web/blob/master/examples/example_apm.html">example_apm</a>
  is a simple APM integration.<br>
  <a href="https://github.com/Countly/countly-sdk-web/blob/master/examples/example_apm_async.html">example_apm_async</a>
  is a simple async APM integration.<br>
  <a href="https://github.com/Countly/countly-sdk-web/blob/master/examples/example_formdata.html">example_formdata</a>
  is a simple integration to collect data from form data.<br>
  <a href="https://github.com/Countly/countly-sdk-web/blob/master/examples/example_gdpr.html">example_gdpr</a>
  is a simple integration to show how giving consent works.<br>
  <a href="https://github.com/Countly/countly-sdk-web/blob/master/examples/example_multiple_instances.html">example_multi_instances</a>
  is a simple demonstration for multi instancing the Countly SDK.<br>
  <a href="https://github.com/Countly/countly-sdk-web/blob/master/examples/examples_feedback_widgets.html">examples_feedback_widgets</a>
  is a simple integration for feedback widgets.<br>
  <a href="https://github.com/Countly/countly-sdk-web/blob/master/examples/example_remote_config.html">example_remote_config</a>
  is a simple integration for remote config.<br>
  <a href="https://github.com/Countly/countly-sdk-web/blob/master/examples/example_sync.html">example_sync</a>
  is a sample integration for sync operations.<br>
  <a href="https://github.com/Countly/countly-sdk-web/blob/master/examples/example_web_worker.html">example_web_worker</a>
  is a sample for web worker.<br>
  <a href="https://github.com/Countly/countly-sdk-web/blob/master/examples/example_async.html">example_async</a>
  is a sample integration for async usage of the SDK.
</p>
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
    <pre><code class="javascript">//possible options are "localstorage", "cookies" and "none"
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
<pre><code class="javascript">//change the path to where you want to store local storage data
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
    <strong>cly_id_type</strong> - current user's device id type
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
});</code></pre>
  </div>
</div>
<h2 id="h_01HABTQ43ACRHQSY8263SJR14V">SDK Internal Limits</h2>
<p>
  If values or keys provided by the user exceeds certain internal limits, they
  will be truncated. Please have a look
  <a href="/hc/en-us/articles/9290669873305#sdk_internal_limits">here</a> for the
  list of properties effected by these limits.
</p>
<p>
  You can override these internal limits during initialization.
</p>
<h3 id="h_01HRY51Q9K26ZGFWJS9R87N0WQ">Key Length</h3>
<p>
  <code class="javascript">max_key_length</code> - 128 chars by default. Keys that
  exceed this limit will be truncated.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.app_key = "YOUR_APP_KEY";
Countly.url = "YOUR_SERVER_URL";
Countly.max_key_length = 50;
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
  app_key:"YOUR_APP_KEY",
  url: "YOUR_SERVER_URL",
  max_key_length: 50
});</code></pre>
  </div>
</div>
<h3 id="h_01HRY51XC20ZVT47JN7GYTAZ7D">Value Size</h3>
<p>
  <code class="javascript">max_value_size</code> - 256 chars by default. Values
  that exceed this limit will be truncated.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.app_key = "YOUR_APP_KEY";
Countly.url = "YOUR_SERVER_URL";
Countly.max_value_size = 12;
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
  app_key:"YOUR_APP_KEY",
  url: "YOUR_SERVER_URL",
  max_value_size: 12
});</code></pre>
  </div>
</div>
<h3 id="h_01HRY521MHG6HD8P7JQ0BE7S8K">Segmentation Values</h3>
<p>
  <code class="javascript">max_segmentation_values</code> - 100 dev entries by
  default. Key/value pairs that exceed this limit in a single event will be removed.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.app_key = "YOUR_APP_KEY";
Countly.url = "YOUR_SERVER_URL";
Countly.max_segmentation_values = 67;
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
  app_key:"YOUR_APP_KEY",
  url: "YOUR_SERVER_URL",
  max_segmentation_values: 67
});</code></pre>
  </div>
</div>
<h3 id="h_01HRY526FQC2R9BQRTYB1B2VF0">Breadcrumb Count</h3>
<p>
  <code class="javascript">max_breadcrumb_count</code> - 100 entries by default.
  If the limit is exceeded, the oldest entry will be removed from stored breadcrumbs.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.app_key = "YOUR_APP_KEY";
Countly.url = "YOUR_SERVER_URL";
Countly.max_breadcrumb_count = 45;
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
  app_key:"YOUR_APP_KEY",
  url: "YOUR_SERVER_URL",
  max_breadcrumb_count: 45
});</code></pre>
  </div>
</div>
<h3 id="h_01HRY52BYPANSEJ27WFFMWNR1F">Stack Trace Lines Per Thread</h3>
<p>
  <code class="javascript">max_stack_trace_lines_per_thread</code> - 30 lines by
  default. Crash stack trace lines that exceed this limit (per thread) will be
  removed.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.app_key = "YOUR_APP_KEY";
Countly.url = "YOUR_SERVER_URL";
Countly.max_stack_trace_lines_per_thread = 23;
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
  app_key:"YOUR_APP_KEY",
  url: "YOUR_SERVER_URL",
  max_stack_trace_lines_per_thread: 23
});</code></pre>
  </div>
</div>
<h3 id="h_01HRY52J9BCCYQ00XJ9PWY9PFZ">Stack Trace Line Length</h3>
<p>
  <code class="javascript">max_stack_trace_line_length</code> - 200 chars by default.
  Crash stack trace lines that exceed this limit will be truncated.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.app_key = "YOUR_APP_KEY";
Countly.url = "YOUR_SERVER_URL";
Countly.max_stack_trace_line_length = 10;
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
  app_key:"YOUR_APP_KEY",
  url: "YOUR_SERVER_URL",
  max_stack_trace_line_length: 10
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
  <pre><code class="html">// ...
// ...    
// ... Countly implementation was here
// &lt;/script&gt;

// write the correct path to the GA plugin depending on your project structure
&lt;script src="../plugin/ga_adapter/ga_adapter.js"&gt;&lt;/script&gt;

// Google Analytics implementation
&lt;script&gt;
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

// add this line into your google analytics snippet to use the GA plugin
CountlyGAAdapter();

// now Countly will recognize the GA commands like below and send them to your Countly server too
ga('create', 'UA-56295140-3', 'auto');
ga('send','event','category','action','label');
ga('send','pageview','page.html');
&lt;/script&gt;</code></pre>
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
<h2 id="h_01HABTQ4394D6BR7PJ36RYQK4R">Opt In / Opt Out</h2>
<p>
  <span style="font-weight: 400;">The Countly SDK will always be opt in by default, meaning all tracking is enabled, but you may easily disable all tracking by selecting the <strong>opt_out</strong> method. It will persistently save settings to prevent tracking after page reloads. Then if you want to opt in again you can use <strong>opt_in</strong> method to resume tracking at next page load.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">// to stop tracking user data at next page load
Countly.q.push(['opt_out']);

// to resume tracking user data at next page load
Countly.q.push(['opt_in']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">// to stop tracking user data at next page load
Countly.opt_out();

// to resume tracking user data at next page load
Countly.opt_in();</code></pre>
  </div>
</div>
<p>
  <span style="font-weight: 400;">Disabling tracking for specific users with these methods can be sufficient for testing or situations where you decide to not track a specific user's information from now on. However, should you desire more granular feature control, checkout the <a href="/hc/en-us/articles/4409195031577#h_01HABTQ439V9NNDDCW31XG086F">User Consent</a> section.</span>
</p>
<div class="callout callout--info">
  <p>
    If you would like to have opt out selected by default, combine these methods
    with the initial setting <strong>ignore_visitor</strong> on the Countly init
    object.
  </p>
</div>
<h2 id="h_01JF06CEVMYPPTDFTTTJ2DG7F6">Extended Feedback Widget Options</h2>
<p>
  If you have many widgets and the way you want to show them is intricate you can
  use the methods shown below.
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

  // Decide which widget to show. Here, the first rating widget is selected. 
  const widgetType = "rating";
  const countlyFeedbackWidget = countlyPresentableFeedback.find(widget = widget.type === widgetType);
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
<br>// Feedback widget callback function, err is for error and countlyPresentableFeedback contains an array of widget objects
function feedbackWidgetsCallback(countlyPresentableFeedback, err) {
  if (err) {
    console.log(err);
    return;
  }

  // Decide which widget to show. Here, the first rating widget is selected. 
  const widgetType = "rating";
  const countlyFeedbackWidget = countlyPresentableFeedback.find(widget =&gt; widget.type === widgetType);
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
  Note: Feedback Widgets' show policies are handled internally by the Web SDK.
</p>
<h2 id="h_01JCGK0D278963WZKBW7ZWPTDN">Extended Device ID Management</h2>
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
<h2 id="h_01JF7TA0TASABV8RSAX2PWYAZ8">Content Zone</h2>
<p>
  The Content Zone feature enhances user engagement by delivering various types
  of content blocks, such as in-app messaging, ads, or user engagement prompts.
  These content blocks are dynamically served from the content builder on the server,
  ensuring that users receive relevant and up-to-date information.
</p>
<div class="callout callout--info">
  <p>
    For learning how you can use Journeys &amp; Content Builder to create In-App
    messages you can check
    <a href="/hc/en-us/articles/18995770340380" target="_blank" rel="noopener noreferrer">this</a>
    article.
  </p>
</div>
<p>
  To start fetching content from the server, use the following method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(() =&gt; { Countly.content.enterContentZone(); });

// or
Countly.q.push(['content.enterContentZone']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.content.enterContentZone();</code></pre>
  </div>
</div>
<p>
  This call will retrieve and display any available content for the user. It will
  also regularly check if a new content is available, and if it is, will fetch
  and show it to the user.
</p>
<p>
  If you need to ask for content after a trigger you know you can use this method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(() =&gt; { Countly.content.refreshContentZone(); });

// or
Countly.q.push(['content.refreshContentZone']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.content.refreshContentZone();</code></pre>
  </div>
</div>
<p>
  When you want to exit from content zone and stop SDK from checking for available
  content you can use this method:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.q.push(() =&gt; { Countly.content.exitContentZone(); });

// or 
Countly.q.push(['content.exitContentZone']);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.content.exitContentZone();</code></pre>
  </div>
</div>
<p>
  If you need to change the frequency of content zone requests from default 30
  seconds, you can give a custom value for intervals, in seconds, during init:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">Countly.content_zone_timer_interval = 45; // seconds
     
// Initialize the SDK</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">Countly.init({
  app_key: "YOUR_APP_KEY",
  url: "https://your.server.ly",
  content_zone_timer_interval: 45, //seconds
});</code></pre>
  </div>
</div>
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
<h2 id="h_01HNANK3XPZ7429V5Z2FJ9MMZ5">What Information is Collected by the SDK?</h2>
<p>
  The data that SDKs gather to carry out their tasks and implement the necessary
  functionalities is mentioned in
  <a href="https://support.count.ly/hc/en-us/articles/9290669873305-A-deeper-look-at-SDK-concepts#h_01HJ5MD0WB97PA9Z04NG2G0AKC">here</a>
</p>