<p>
  <span style="font-weight:400">This documentation shows how to install the Countly JS tracker and use Countly to track your web page in detail. It applies to the SDK version 20.11.</span>
</p>
<div class="callout callout--info">
  <p class="callout__title">
    <span class="wysiwyg-font-size-large"><strong>Older documentation</strong></span>
  </p>
  <p>
    To access the documentation for version 20.04 and older, click
    <a href="https://support.count.ly/hc/en-us/articles/900003463646" target="blank">here</a>.
  </p>
</div>
<p>
  <span style="font-weight:400">In order to track your web server pages, you will need the Countly JavaScript tracking library. This library comes ready &amp; automatically hosted on your Countly server (at&nbsp;</span><a href="http://yourdomain.com/sdk/web/countly.min.js)"><span style="font-weight:400">http://yourdomain.com/sdk/web/countly.min.js)</span></a><span style="font-weight:400">&nbsp;and can be updated via command line. This library also works well with mobile applications that consist of HTML5 views.</span>
</p>
<p>
  <span style="font-weight:400">Optionally, you may also use package managers to gain access to the library (however, you should not have to as it already comes ready):</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">npm</span>
    <span class="tabs-link">bower</span> <span class="tabs-link">yarn</span>
  </div>
  <div class="tab">
    <pre><code class="shell">npm install countly-sdk-web</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="shell">bower install countly-sdk-web</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="shell">yarn add countly-sdk-web</code></pre>
  </div>
</div>
<p>
  <span style="font-weight:400">Before we begin, the following information is meant for those who have examined our mobile SDKs - we can tell that custom events or tags that are used in mobile SDKs are quite similar to those we use in JavaScript code. For example, it's possible to modify custom property values of user details with modification commands, such as inc, mul, max, or min. Likewise, any custom events can be easily sent with segmentation.</span>
</p>
<div class="callout callout--info">
  <h3 class="callout__title">What is an APP KEY?</h3>
  <p>
    You'll see the APP_KEY definition above. This key is generated automatically
    when you create a website for tracking on the Countly dashboard. Note that
    an APP KEY is different than the API KEY, which is used to send data via
    API calls.
  </p>
  <p>
    To retrieve your APP_KEY, go to Management -&gt; Applications and select
    your app. Then you will see the App Key field.
  </p>
</div>
<div class="img-container">
  <img src="https://count.ly/images/guide/XmwUJ7VZSF2GConV76xY_app_key.png">
</div>
<h1>Setting up (Recommended asynchronous usage)</h1>
<p>
  <span style="font-weight:400">You may use the Countly Web SDK asynchronously without blocking content loading. It may also be used if the Countly script has not yet been loaded by pushing function calls into the&nbsp;</span><strong>Countly.q</strong><span style="font-weight:400">&nbsp;queue or synchronously allowing the script to load before executing any functions.</span>
</p>
<p>
  <span style="font-weight:400">Inserting asynchronous code before closing the tag is suggested, while Synchronous code should be added towards the bottom of the page before closing the tag.</span>
</p>
<p>
  <span style="font-weight:400">An example setup would look like this:</span>
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

// Provide your server IP or name. Use try.count.ly or us-try.count.ly 
// or asia-try.count.ly for EE trial server.
// If you use your own server, make sure you have https enabled if you use
// https below.
Countly.url = "https://yourdomain.com"; 

// Start pushing function calls to queue
// Track sessions automatically (recommended)
Countly.q.push(['track_sessions']);
  
//track web page views automatically (recommended)
Countly.q.push(['track_pageview']);
  
// Uncomment the following line to track web heatmaps (Enterprise Edition)
// Countly.q.push(['track_clicks']);

// Uncomment the following line to track web scrollmaps (Enterprise Edition)
// Countly.q.push(['track_scrolls']);
  
// Load Countly script asynchronously
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
&lt;script type='text/javascript' src='https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.min.js'&gt;&lt;/script&gt;
&lt;script type='text/javascript'&gt;

Countly.init({
// provide your app key that you retrieved from Countly dashboard
  	app_key: "YOUR_APP_KEY",

// Provide your server IP or name. Use try.count.ly or us-try.count.ly 
// or asia-try.count.ly for EE trial server.
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
  <span style="font-weight:400">In the above-mentioned example, we used JSDelivr to retrieve the Countly JS SDK. There are two options available here: using Cloudflare (CDNjs) or JSDelivr (both of which are highly available CDNs). If you would like to use CDNjs, here is the line you should be using instead of the one above.</span>
</p>
<pre><code class="text">// Note: You should change 19.2.1 below to the version 
// of the latest JS SDK to make sure you use latest version.
// Latest version is here: 
// https://github.com/Countly/countly-sdk-web/releases

https://cdnjs.cloudflare.com/ajax/libs/countly-sdk-web/19.2.1/countly.min.js</code></pre>
<p>
  <span style="font-weight:400">As an alternative, you may also use<code>/sdk/web/countly.min.js</code></span><span style="font-weight:400">&nbsp;to get this SDK directly from your Countly server.</span>
</p>
<p>
  <span style="font-weight:400">As the third alternative option, you may download&nbsp;</span><a href="https://github.com/Countly/countly-sdk-web/tree/master/lib"><span style="font-weight:400">countly.min.js</span></a><span style="font-weight:400">&nbsp;from our Github repository and upload it to any server from where you would like to host it. You would only need to point this minified JS tracker lib in your small code above. This should ideally be done if none of the above-mentioned methods work in your specific use-case.</span>
</p>
<p>
  <span style="font-weight:400">Then you will be able to make custom event calls such as:</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="html">&lt;script type='text/javascript'&gt;
//send event on button click
function clickEvent(ob){
	Countly.q.push(['add_event',{
		key:"asyncButtonClick", 
		segmentation: {
			"id": ob.id
		}
	}]);
}
&lt;/script&gt;
&lt;input type="button" id="asyncTestButton" onclick="clickEvent(this)" value="Test Button"&gt;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="html">&lt;script type='text/javascript'&gt;
  //send event on button click
  function clickEvent(ob){
    Countly.add_event({
      key:"buttonClick", 
      segmentation: {
        "id": ob.id
      }
    });
  }
&lt;/script&gt;
&lt;input type="button" id="testButton" onclick="clickEvent(this)" value="Test Button"&gt;</code></pre>
  </div>
</div>
<div class="callout callout--info">
  <h3 class="callout__title">
    Why aren’t I able to see AngularJS errors on the Countly dashboard?
  </h3>
  <p>
    AngularJs swallows errors by default. You will need to extend Angular's
    <code>$exceptionHandler</code> to call <code>Countly.log_error()</code>.
    For more information,
    <a href="https://www.bennadel.com/blog/2542-logging-client-side-errors-with-angularjs-and-stacktrace-js.htm">see this blog post</a>.
  </p>
</div>
<div class="callout callout--info">
  <h3 class="callout__title">Generate custom SDK code snippets</h3>
  <p>
    <a href="http://code.count.ly/">Countly Code Generator</a> may be used to
    generate custom SDK code snippets simply and quickly. You may provide values
    for your custom event, or user profile or just start with basic integration,
    and this service will generate the necessary code for you to use in your
    favorite IDE.
  </p>
</div>
<h1>Setup properties</h1>
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
    <strong>debug</strong> - output debug info into console (default: false)
  </li>
  <li>
    <strong>ignore_bots</strong> - option to ignore traffic from bots (default:
    true)
  </li>
  <li>
    <strong>interval</strong> -&nbsp;<span style="font-weight:400">set an interval for how often inspections should be made to see if there is any data to report and then report it (default: 500 ms)</span>
  </li>
  <li>
    <strong>queue_size</strong> - maximum amount of queued requests to store
    (default: 1000)
  </li>
  <li>
    <strong>fail_timeout</strong> -
    <span style="font-weight:400">set the time to wait in seconds after a failed connection to the server (default: 60 seconds)</span>
  </li>
  <li>
    <strong>inactivity_time</strong> -&nbsp;<span style="font-weight:400">the time limit after which a user will be considered inactive if no actions have been made. No mouse movement, scrolling, or keys pressed. Expressed in minutes (default: 20 minutes)</span>
  </li>
  <li>
    <strong>session_update</strong> -
    <span style="font-weight:400">how often a session should be extended, expressed in seconds (default: 60 seconds)&nbsp;</span>
  </li>
  <li>
    <strong>max_events</strong> -&nbsp;maximum amount of events to send in one
    batch (default: 10)
  </li>
  <li>
    <strong>max_logs</strong> -&nbsp;<span style="font-weight:400">maximum amount of breadcrumbs to store for crash logs (default: 100)</span>
  </li>
  <li>
    <strong>ignore_referrers</strong> - array with referrers to ignore (default:
    none)
  </li>
  <li>
    <strong>ignore_prefetch</strong> -<span style="font-weight:400">&nbsp;ignore prefetching and pre-rendering from counting as real website visits (default: true)</span>
  </li>
  <li>
    <strong>force_post</strong> -
    <span style="font-weight:400">force using post method for all requests (default: false)</span>
  </li>
  <li>
    <strong>ignore_visitor</strong> -
    <span style="font-weight:400">ignore this current visitor (default: false)</span>
  </li>
  <li>
    <strong>require_consent</strong> - P<span style="font-weight:400">ass true if you are implementing GDPR compatible consent management. This would prevent running any functionality without proper consent (default: false)</span>
  </li>
  <li>
    <strong>utm</strong> - o<span style="font-weight:400">bject instructing which UTM parameters to track (default: {"source":true, "medium":true, "campaign":true, "term":true, "content":true})</span>
  </li>
  <li>
    <strong>use_session_cookie</strong> - use cookies to track sessions (default:
    true)
  </li>
  <li>
    <strong>session_cookie_timeout</strong> -
    <span style="font-weight:400">how long until a cookie session should expire, expressed in minutes (default: 30 minutes)</span>
  </li>
  <li>
    <strong>remote_config</strong> -
    <span style="font-weight:400">enable automatic remote config fetching, provide the callback function to be notified when fetching is complete (default: false)</span>
  </li>
  <li>
    <strong>namespace</strong> - h<span>ave a separate namespace for persistent data when using multiple trackers on the same domain</span>
  </li>
  <li>
    <span><strong>headers</strong> - object to override or add headers to all SDK requests</span>
  </li>
  <li>
    <span><strong>metrics</strong> -&nbsp;provide metrics for this user, otherwise, it will try to collect everything which is possible</span>
    <ul>
      <li>
        <span><strong>_os</strong> - the name of platform/operating system</span>
      </li>
      <li>
        <span><strong>_os_version</strong> - version of platform/operating system</span>
      </li>
      <li>
        <span><strong>_device</strong> - device model name</span>
      </li>
      <li>
        <span><strong>_resolution</strong> - screen resolution of the device</span>
      </li>
      <li>
        <span><strong>_carrier</strong> - carrier or operator used for connection</span>
      </li>
      <li>
        <span><strong>_density</strong> - screen density of the device</span>
      </li>
      <li>
        <span><strong>_locale</strong> - locale or language of the device in ISO format</span>
      </li>
      <li>
        <span><strong>_store</strong> - a source where the user came from</span>
      </li>
      <li>
        <span><strong>_browser</strong> - browser name</span>
      </li>
      <li>
        <span><strong>_browser_version</strong> - browser version</span>
      </li>
      <li>
        <span><strong>_ua</strong> - user agent string</span>
      </li>
    </ul>
  </li>
</ul>
<p>
  <span style="font-weight:400">Setting up properties on the Countly Web SDK is as follows (use your own server name if not using try.count.ly below):</span>
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
<p>
  <span style="font-weight:400">Note that the Countly web SDK automatically captures UTM tags and stores them as user properties together with the corresponding user. This will make users segmentable in all the places around the dashboard, where granular data is used and segmentation capabilities are provided.</span>
</p>
<h1>Helper methods</h1>
<p>
  <span style="font-weight:400">Helper methods were created to allow you to easily track the most common actions on your web.</span>
</p>
<div class="callout callout--warning">
  <h3 class="callout__title">Choose your helper methods carefully.</h3>
  <p>
    The helper methods we provide below are both for synchronous and asynchronous
    tracking code. Choose the right helper method depending on your implementation.
  </p>
</div>
<h2>Track Sessions</h2>
<p>
  <span style="font-weight:400">This method will automatically track user sessions by calling begin, extend, and end session methods.</span>
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
<h2>Track Pageviews</h2>
<p>
  <span style="font-weight:400">This method will track the current pageview by using location.path as the page name and then reporting it to the server.</span>
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
  <span style="font-weight:400">For Ajax updated contents and single page web applications, pass the page name as a parameter to record the new page view.</span>
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
  <span style="font-weight:400">Here is a good example if your single-page app uses URL hash.</span>
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
  <span style="font-weight:400">In some cases, you might like to ignore some URLs to exclude from tracking, such as dynamic URLs that include the user ID in the URL, internal URLs, or for any other reason. You may do so by providing another parameter with a list of strings of views to ignore or a list of regular expressions to ignore.</span>
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
<h2>Overriding view name and URL getters</h2>
<p>
  <span style="font-weight:400">There are cases when determining the view name requires more complex logic, and in some cases, you will need to separate the URL and the View naming. This is done so you may still have some business logic view names, yet you have the valid URL underneath them to view action maps, such as clicks and scrolls.</span>
</p>
<p>
  <span style="font-weight:400">To do so you may define the view name and URL getter functions. That way you won’t need to provide separate view names, rather the SDK will use this getter function to receive the proper view name and the URL you would like to use.</span>
</p>
<p>
  <span style="font-weight:400">Here is an example of how to create a getter for View and URL.</span>
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
<h2>Track Clicks / Heatmaps (Enterprise edition)</h2>
<p>
  <span style="font-weight:400">This method will automatically track clicks on the last reported view and display them on the heatmap.</span>
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
  <span style="font-weight:400">In the event you are facing issues with viewing heatmaps, kindly go through this&nbsp;<a href="https://resources.count.ly/docs/view-analytics#section-troubleshooting">Troubleshooting guide</a>.</span>
</p>
<div class="callout callout--info">
  <h3 class="callout__title">
    Important notification about viewing heatmaps with HTTP/HTTPS content:
  </h3>
  <p>
    Note that browsers do not allow loading HTTP iframe content on HTTPS websites.
    For this reason, if you are using HTTPS on your Countly instance, you will
    only be able to view HTTPS content and no HTTP page content will be visible.
  </p>
</div>
<p>
  <span style="font-weight:400">After you integrate the JS SDK and start sending click data, all generated heatmaps may be viewed under Analytics &gt; Page views, as shown below:</span>
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/b893929-11.png">
</div>
<h2>Track Scrolls / Scroll heatmaps (Enterprise edition)</h2>
<p>
  <span style="font-weight:400">This method will automatically track scrolls on the last reported view and display them on the heatmap.</span>
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
  <span style="font-weight:400">As with Click Heatmaps, collected data is viewable under Analytics &gt; Page views. You may change the heatmap type on the top bar once a view is open.</span>
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/5bc44bc-topbar.png">
</div>
<h2>Track link clicks</h2>
<p>
  <span style="font-weight:400">This method will track clicks to specific links and will report custom events with the&nbsp;</span><strong>linkClick</strong><span style="font-weight:400">&nbsp;key as well as the link's text, ID, and URLs as segments.</span>
</p>
<p>
  <span style="font-weight:400">All links will automatically be tracked by default for the entire page, but you may provide the parent node as a parameter for which to track link clicks.</span>
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
  <span style="font-weight:400">As soon as you include this one-liner coder, you will automatically be able to see the "linkClick" custom event in your dashboard as data flows in with the text, ID, and URLs as segments.</span>
</p>
<h2>Track form submissions</h2>
<p>
  <span style="font-weight:400">This method will automatically track form submissions and collect form data. It will then input values in the form and report them as a Custom Event with the&nbsp;<strong>formSubmit</strong>&nbsp;key.</span>
</p>
<p>
  <span style="font-weight:400">All forms will automatically be tracked by default for the entire page, but you may provide the parent node as a parameter for which to track forms.</span>
</p>
<p>
  <span style="font-weight:400">The second parameter controls whether to collect hidden inputs or not. Hidden inputs are not collected by default.</span>
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
<h2>Report conversion</h2>
<p>
  <span style="font-weight:400">When using Countly attribution analytics, you may also report conversions to the Countly server, e.g. when a visitor purchases an item or registers on your site.</span>
</p>
<p>
  <span style="font-weight:400">If a user visits your website through the Countly campaign link, the campaign information will be automatically stored by default for this user and used when reporting conversion.&nbsp;</span><span style="font-weight:400">If conversion has not yet been reported, the campaign information will be overwritten when that user visits through another campaign link. When you report the conversion, it would report the latest campaign user used to access your website.</span>
</p>
<p>
  <span style="font-weight:400">However, you may also overwrite that data and provide any specific campaign ID for which you would like to report conversion.</span>
</p>
<p>
  <span style="font-weight:400">Conversion will not be reported if there is no stored campaign data and you have yet to provide a campaign ID.</span>
</p>
<p>
  <span style="font-weight:400">Note: Conversion for each user may only be reported once, all other conversions will be ignored for that same user.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//user stored conversion data
Countly.q.push(['report_conversion']);

//or provide campaign id yourself
Countly.q.push(['report_conversion', "MyCampaignID"]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//user stored conversion data
Countly.report_conversion();

//or provide campaign id yourself
Countly.report_conversion("MyCampaignID");</code></pre>
  </div>
</div>
<h2>Report feedback</h2>
<p>
  In case you don't want to use Countly provided feedback and rating UI, you may
  use your own UI and simply report collected data to Countly.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//user feedback
Countly.q.push(['report_feedback', {
    widget_id:"1234567890",
    contactMe: true,
    rating: 5,
    email: "user@domain.com",
    comment: "Very good"
}]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//user feedback
Countly.report_feedback({
    widget_id:"1234567890",
    contactMe: true,
    rating: 5,
    email: "user@domain.com",
    comment: "Very good"
});</code></pre>
  </div>
</div>
<h2>Report NPS and Surveys</h2>
<p>
  There are two types of surveys available - NPS and Basic survey.
</p>
<p>
  Both NPS and Survey use the same API to fetch feedbacks from the server as well
  as to display them to the end user.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//Fetch user's NPS and Survey feedbacks from the server
Countly.q.push(['get_available_feedback_widgets', feedbackWidgetsCallback]);
<br>//Surveys feedback callback function
function feedbackWidgetsCallback(countlyPresentableFeedback, err) {
    if (err) {
        console.log(err);
        return;
    }
  
    //The available feedback types are nps and survey, decide which one to show
    var c<span>ountlyFeedbackWidget = countlyPresentableFeedback[0];
    
    //Display the feedback widget to the end user 
    Countly.present_feedback_widget(c<span>ountlyFeedbackWidget);
}
</span></span></code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//Fetch user's NPS and Survey feedbacks from the server
Countly.get_available_feedback_widgets(feedbackWidgetsCallback);
<br>//Surveys feedback callback function
function feedbackWidgetsCallback(countlyPresentableFeedback, err) {
    if (err) {
    	console.log(err);
        return;
    }
    
    //The available feedback types are nps and survey, decide which one to show
    var c<span>ountlyFeedbackWidget = countlyPresentableFeedback[0];
    
    //Display the </span><span>feedback widget to the end user 		
    Countly.present_feedback_widget(c<span>ountlyFeedbackWidget);
}
</span></span></code></pre>
  </div>
</div>
<p>
  Note: Feedback widget's show policies are handled internally by the web sdk.
</p>
<h2>Report device orientation</h2>
<p>
  By default, Countly reports the device orientation once a session starts, and
  at any time the orientation changes. In case you need to force reporting orientation,
  you may call the following method.
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
<h2>Opt in / Opt out</h2>
<p>
  <span style="font-weight:400">The Countly SDK will always be opt in by default, but you may easily disable all tracking by selecting&nbsp;the <strong>opt_out</strong>&nbsp;method. It will also persistently save settings and prevent tracking after page reloads. Select&nbsp;<strong>opt_in</strong> to resume tracking.</span>
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
  <span style="font-weight:400">Disabling tracking for specific users is more than sufficient for most cases. However, should you desire more granular feature controls, checkout the&nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037441932-Web-analytics-JavaScript-#section-gdpr-consent-management">GDPR section</a>.</span>
</p>
<div class="callout callout--info">
  <h3 class="callout__title">Opt out by default</h3>
  <p>
    If you would like to have opt out selected by default, combine these methods
    with the initial setting <strong>ignore_visitor</strong> on the Countly init
    object.
  </p>
</div>
<h1>Automatically fill user data</h1>
<p>
  <span style="font-weight:400">In most cases, you won’t know anything about your users, yet you will still want to try to collect any data possible. We provide 2 helper methods for this exact reason.</span>
</p>
<h2>Collect user data from filled forms</h2>
<p>
  <span style="font-weight:400">This method will look into the forms filled out by your users and will try to gather data, such as names, email addresses, usernames, etc.<br>All forms will automatically be checked, but you have the option to provide a form element if you would like to collect data only from a specific form, or select a method multiple times for different forms. Also, if you are already providing data for users, then you would not want to overwrite it. You may set the third parameter as true to indicate that data found should be stored in custom properties.</span>
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
  <span style="font-weight:400">Passwords and other sensitive data will be omitted, however, if you would explicitly like to exclude some form input from being processed, just add the css class&nbsp;<strong>cly_user_ignore</strong>&nbsp;to that element. Oppositely, you may need to specify data from this input to be collected as the provided key by adding the prefixed css class&nbsp;<strong>cly_user_key</strong>. Therefore, if you would like to store data as a name, you should specify the&nbsp;<strong>cly_user_name</strong>&nbsp;css class.</span>
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
<h2>Collect user data from Facebook</h2>
<p>&nbsp;</p>
<p>
  <span style="font-weight:400">If your website uses the Facebook JavaScript SDK, you may use this helper method to automatically collect user data from their Facebook accounts. Select the method right after Facebook SDK initialization and optionally set the object with custom properties and graph paths for values on where to receive them.</span>
</p>
<p>
  <span style="font-weight:400">Here is an example how to receive data from Facebook, including locations and time zones as custom properties.</span>
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
<h1>Custom Events</h1>
<h2>Adding an event</h2>
<p>
  <span style="font-weight:400">Custom events are a way to track any custom actions or other data you would like to track from your website. You may also set segments to be able to view a breakdown of the action by providing the segment values.</span>
</p>
<div class="callout callout--warning">
  <h3 class="callout__title">Data passed should be in UTF-8</h3>
  <p>
    All data passed to the Countly instance via the SDK or API should be in UTF-8.
  </p>
</div>
<p>A custom event consists of a JavaScript object with keys:</p>
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
  <span style="font-weight:400">Here is an example of adding a custom event with all possible properties:</span>
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
<h2>Timed Events</h2>
<p>
  <span style="font-weight:400">You may report time or duration with every event by providing the&nbsp;<strong>dur</strong>&nbsp;property of the event’s object. However, if you would like, you may also let the Web SDK track the duration of some specific events for you. You may use the&nbsp;<strong>start_event</strong>&nbsp;and&nbsp;<strong>end_event</strong>&nbsp;methods.</span>
</p>
<p>
  <span style="font-weight:400">Firstly, you may start tracking an event time by providing the name of the event (which later on will be used as the key for the event object).</span>
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
  <span style="font-weight:400">Countly will internally mark the start of the event and will wait until you end the event using the&nbsp;<strong>end_event</strong>&nbsp;method, setting up&nbsp;the <strong>dur</strong>&nbsp;property based on how much time has passed since&nbsp;the <strong>start_event</strong>&nbsp;for the same event name was selected.</span>
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
<h1>User Profiles and Custom data</h1>
<h2>User details</h2>
<p>
  <span style="font-weight:400">If you have any details about the user/visitor, you may provide Countly with that information. This will allow you to track every specific user on the "User Profiles" tab, which is available with <a href="http://count.ly/enterprise-edition">Countly Enterprise Edition</a>.</span>
</p>
<p>
  <span style="font-weight:400">The list of possible parameters you may pass:</span>
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
<h2>Modifying custom data</h2>
<p>
  <span style="font-weight:400">Additionally, you may perform different manipulations on custom data values, such as incrementing the current value on the server or storing an array of values under the same property.</span>
</p>
<p>
  <span style="font-weight:400">After using modifiers, don't forget to call&nbsp;<code class="javascript">userData.save</code>&nbsp;to send data to server.</span>
</p>
<p>
  <span style="font-weight:400">The list of available methods may be found below:</span>
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
<h1>Tracking Javascript error</h1>
<p>
  <span style="font-weight:400">Countly also provides a way for tracking JavaScript errors on your websites.</span>
</p>
<p>
  <span style="font-weight:400">Select the following function to automatically capture and report JavaScript errors on your website:</span>
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
  <span style="font-weight:400">Additionally, you may add more segments or properties/values to track with error reports by providing an object with a key/values to add to the error reports.</span>
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
  <span style="font-weight:400">Apart from automatically reporting unhandled errors, you may also report handled exceptions to the server, so you may figure out how to handle them later on (or if you even need to figure out how to handle them later on). Optionally, you may once again provide the custom segments to be used in the report (or use the ones provided with the&nbsp;<strong>track_error</strong>&nbsp;method as default ones).</span>
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
  <span style="font-weight:400">To better understand what your users did prior to receiving an error, you may leave breadcrumbs throughout the code on different user actions. These breadcrumbs will then be combined in a single log and reported to the server as well.</span>
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
<h1>Changing Device ID</h1>
<p>
  <span style="font-weight:400">In some cases, you may want to change the ID of the user/device that you provided or Countly automatically generated, e.g. when a user was changed.</span>
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
<p>
  <span style="font-weight:400">In some cases, you may also need to change a user's device ID in a way so that that server will merge the data of both user IDs (both the new and existing ID you provided) on the server, e.g. when a user used the website without authenticating and recorded some data and then authenticated, and you would like to change the ID to your internal ID of this user to keep tracking it across multiple devices.</span>
</p>
<p>
  <span style="font-weight:400">This call will merge any data recorded for the current ID and save it as a user with a newly provided ID.</span>
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
<h1>GDPR Consent management</h1>
<p>
  <span style="font-weight:400">In most cases, the </span><strong>opt_out</strong><span style="font-weight:400">&nbsp;and&nbsp;</span><strong>opt_in</strong><span style="font-weight:400">&nbsp;methods are enough to disable the tracking of specific users, such as testers. However, in some cases, you may require a more granular approach.</span>
</p>
<p>
  <span style="font-weight:400">This section will tell you how to set up GDPR compliant consent management with the Countly Web SDK.</span>
</p>
<h2>Disable tracking until given consent</h2>
<p>
  <span style="font-weight:400">To disable tracking until consent is given for a specific feature, all you need to do is pass true as the&nbsp;</span><strong>require_consent</strong><span style="font-weight:400">&nbsp;config before or during your selection of the Countly&nbsp;</span><strong>init</strong><span style="font-weight:400">&nbsp;method.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//before loading Countly script
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
<p>
  <span style="font-weight:400">Next, you may select all the&nbsp;<a href="https://support.count.ly/hc/en-us/articles/360037441932-Web-analytics-JavaScript-#helper-methods" target="_self">helper methods</a>&nbsp;you will be using. They won't be tracking or sending anything to the server until consent is given.</span>
</p>
<h2>Features for consent</h2>
<p>
  <span style="font-weight:400">The SDK provides different features for consent. You may check all the supported features for the current SDK by checking the&nbsp;</span><strong>Countly.features</strong><span style="font-weight:400">&nbsp;property. Here is a list containing all the properties with ex</span>planations:
</p>
<ul>
  <li>
    <span style="font-weight:400">sessions - tracks when, how often, and how long users use your website</span>
  </li>
  <li>
    <span style="font-weight:400">events - allows your custom events to be sent to the server</span>
  </li>
  <li>
    <span style="font-weight:400">views - allows for the views/pages accessed by a user to be tracked</span>
  </li>
  <li>
    <span style="font-weight:400">scrolls - allows a user’s scrolls to be tracked on the heatmap</span>
  </li>
  <li>
    <span style="font-weight:400">clicks - allows a user’s clicks and link clicks to be tracked on the heatmap</span>
  </li>
  <li>
    <span style="font-weight:400">forms - allows a user’s form submissions to be tracked</span>
  </li>
  <li>
    <span style="font-weight:400">crashes - allows JavaScript errors to be tracked</span>
  </li>
  <li>
    <span style="font-weight:400">attribution - allows the campaign from which a user came to be tracked</span>
  </li>
  <li>
    <span style="font-weight:400">users - allows user information, including custom properties, to be collected/provided</span>
  </li>
  <li>
    <span style="font-weight:400">star rating - allows users to rate the site and leave feedback</span>
  </li>
  <li>
    <span style="font-weight:400">feedback - allows users to take part in surveys and nps ratings and submit feedbacks</span>
  </li>
  <li>
    <span style="font-weight:400">apm - allows performance tracking of application by recording traces</span>
  </li>
  <li>
    <span style="font-weight:400">location - allows a user’s location (country, city area) to be recorded</span>
  </li>
</ul>
<p>
  <span style="font-weight:400">This is the most granular level with control features for which consent may be given. However, depending on your website and use case, you may also want to combine some of the features into one using the&nbsp;<strong>group_features</strong>&nbsp;method.</span>
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
<h2>Managing consent</h2>
<p>
  <span style="font-weight:400">Upon a visitor’s arrival to your website, you should check if you already have consent from this visitor. If not, you should present them with a popup explaining what will be tracked and allow them to consent to tracking. When a user selects the consent preferences, you should persistently store it, and on each Countly load, let Countly know for which features the user gave consent by calling the&nbsp;<strong>Countly.add_consent</strong>&nbsp;method and passing one or multiple features (as an array). For example, you should also allow the user to change their mind regarding separate settings screens and when changes are going to be made there.</span>
  <span style="font-weight:400">Respectively call the <strong>Countly.add_consent</strong> or <strong>Countly.remove_consent</strong>&nbsp;methods to allow Countly to track specific features or disable tracking for them.</span>
</p>
<p>
  <span style="font-weight:400">Here is a high-level example of how it could look:</span>
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
<h1>Remote configuration</h1>
<p>
  <span style="font-weight:400">Remote configuration functionality is disabled by default and needs to be explicitly enabled.</span>
</p>
<p>
  <span style="font-weight:400">When remote configuration is enabled, the SDK will only try to fetch it once upon SDK initialization and will receive the initially remote configuration and persistently store it.</span>
</p>
<p>
  <span style="font-weight:400">In the event of one of the following sessions, assuming it would not be possible to load the remote configuration from storage, you will receive an error object in the callback, but you will still have the stored values of the cached remote configuration object.</span>
</p>
<h2>Enabling Remote configuration</h2>
<p>
  <span style="font-weight:400">You may enable remote configuration by providing&nbsp;the </span><em><span style="font-weight:400">remote_config</span></em><span style="font-weight:400">&nbsp;setting when initializing the SDK.</span>
</p>
<p>
  <span style="font-weight:400">If you provide a callback, it will be called when remote configuration is initially loaded and reloaded if you change the device_id.</span>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//to enable remote configuration

//before loading Countly script
Countly.remote_config = true;

//or provide a callback to be notified when configs are loaded
Countly.remote_config = function(err, remoteConfigs){
    if (!err) {
        //we have our remoteConfigs here
        console.log(remoteConfigs);
    }
};</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//to enable remote configuration
Countly.init({
    debug:false,
    app_key:"YOUR_APP_KEY",
    device_id:"1234-1234-1234-1234",
    url: "https://try.count.ly",
    remote_config: true //this will enable loading remote configuration
});


//or provide a callback to be notified when configs are loaded
Countly.init({
    debug:false,
    app_key:"YOUR_APP_KEY",
    device_id:"1234-1234-1234-1234",
    url: "https://try.count.ly",
    remote_config: function(err, remoteConfigs){
        if (!err) {
            //we have our remoteConfigs here
            console.log(remoteConfigs);
        }
    }
});</code></pre>
  </div>
</div>
<h2>
  Receiving configuration values<span style="font-weight:400">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;</span>
</h2>
<p>
  <span style="font-weight:400">You receive the initially loaded remote configuration values in the provided callback, but if you&nbsp;need to get an updated version afterward, you can manually reload it.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>
</p>
<p>
  <span style="font-weight:400">You may call&nbsp;</span><em><span style="font-weight:400">get_remote_config</span></em><span style="font-weight:400"> each time you would like to receive the remote config object of a value for a specific key.</span>
</p>
<p>
  <span style="font-weight:400">This method should be called once the remote configurations have been successfully loaded, or it will simply return an empty object or undefined values.</span>
</p>
<pre><code class="javascript">//get whole remote config object
var remoteConfig = Countly.get_remote_config();

//or get value for specific key like 'test'
var test = Countly.get_remote_config("test");</code></pre>
<h2>Reloading configuration values</h2>
<p>
  <span style="font-weight:400">Should you need to reload the remote config in order to receive the latest value, call&nbsp;the </span><em><span style="font-weight:400">fetch_remote_config</span></em><span style="font-weight:400">&nbsp;method.</span>
</p>
<p>
  <span style="font-weight:400">By using this method, you may reload the entire object or simply reload some specific keys or omit some specific keys in order to decrease the amount of data transfer needed, assuming the values for some of the keys are large.</span>
</p>
<pre><code class="javascript">//reload whole configuration object
Countly.fetch_remote_config(function(err, remoteConfigs){
    if (!err) {
        console.log(remoteConfigs);
    }
});


//reload specific keys only, as `key1` and `key2`
Countly.fetch_remote_config(["key1","key2"], function(err, remoteConfigs){
    if (!err) {
        console.log(remoteConfigs);
    }
});

//reload all key values except specific keys, as `key1` and `key2
Countly.fetch_remote_config(null, ["key1","key2"], function(err, remoteConfigs){
    if (!err) {
        console.log(remoteConfigs);
    }
});</code></pre>
<h1>Performance monitoring</h1>
<p>
  There are 2 ways to report performance traces. One way is to construct and report
  them manually. The other is using a plugin that will use boomerang.js to collect
  data and report it as a performance trace.
</p>
<p>
  To manually report trace you need to construct the trace and call a method like
  this:
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
    stz: 1234567890123, //start timestamp in miliseconds
    etz: 1234567890123, //end timestamp in miliseconds
    app_metrics: {
        duration: 1000 //duration of trace
    }
}]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//report custom trace
Countly.report_trace({
    type: "device", //device or network
    name: "test call", //use name to identify trace and group them by
    stz: 1234567890123, //start timestamp in miliseconds
    etz: 1234567890123, //end timestamp in miliseconds
    app_metrics: {
        duration: 1000 //duration of trace
    }
});</code></pre>
  </div>
</div>
<p>
  To automatically report traces you will need to include 2 additional files in
  your project:
</p>
<pre>&lt;script type='text/javascript' src='../plugin/boomerang/countly_boomerang.js'&gt;&lt;/script&gt;<br>&lt;script type='text/javascript' src="../plugin/boomerang/boomerang.min.js"&gt;&lt;/script&gt;</pre>
<p>
  After that, you may call a method to start reporting loading and network traces
  automatically. This method accepts boomerang initialization config (<a href="http://akamai.github.io/boomerang/BOOMR.html" target="_blank" rel="noopener">more information on boomerang.js</a>)
  as a parameter, so if you are familiar with it, you can modify it on your own.
  In case you are not, you may follow this pattern:
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Asynchronous</span>
    <span class="tabs-link">Synchronous</span>
  </div>
  <div class="tab">
    <pre><code class="javascript">//automatically report traces
Countly.q.push(["track_performance", {
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
}]);</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="javascript">//automatically report traces
Countly.track_performance({
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
});</code></pre>
  </div>
</div>
<h1>Tracking a session manually</h1>
<h2>Beginning a session</h2>
<p>
  <span style="font-weight:400">This method would allow you to control sessions manually. Only use this method if you aren’t planning on calling the track_sessions method and set the&nbsp;</span><em><span style="font-weight:400">use_session_cookie</span></em><span style="font-weight:400">&nbsp;setting to false for more granular control of the session.</span>
</p>
<p>
  <span style="font-weight:400">If&nbsp;<strong>noHeartBeat</strong>&nbsp;is true, then the Countly Web SDK will not automatically extend the session, meaning you would be the one to do it automatically.</span>
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
<h2>Extending a session</h2>
<p>
  <span style="font-weight:400">The Countly SDK will extend the session itself by default (if&nbsp;<strong>noHeartBeat</strong>&nbsp;was provided in the&nbsp;<strong>begin_session</strong>), but if you have not selected this option, you may then extend it using this method and provide the seconds since the last <strong>begin_session</strong>&nbsp;or&nbsp;<strong>session_duration</strong>&nbsp;call.</span>
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
<h2>Ending a session</h2>
<p>
  <span style="font-weight:400">When a visitor is leaving your app or website, you should end their session with this method or by optionally providing the amount of seconds since the last&nbsp;<strong>begin session</strong>&nbsp;or&nbsp;<strong>session_duration</strong>&nbsp;calls, which ever came last.</span>
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
<h1>Offline mode</h1>
<p>
  <span style="font-weight:400">Some cases do exist when you would like the SDK to collect data but not send it to the server until a certain point. Additionally, this mode allows you to delay providing the device_id property until a later time.</span>
</p>
<p>
  <span style="font-weight:400">E.g. if you would like to track your users with a custom device_id, such as with your internal customer ID, and you may only receive that value as soon as the user logs in. Yet, you would also like to track what the user did before logging in.</span>
</p>
<p>
  <span style="font-weight:400">Using offline mode within this context allows you to omit the user merging and server overhead that comes with it, including any possibly skewed aggregation data.</span>
</p>
<p>
  <span style="font-weight:400">To launch the SDK in offline mode, simply provide the offline_mode config value as true. At this point you may omit providing the device_id value if you would like. </span>
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
  <span style="font-weight:400">Or you can enable offline mode at any point later in the SDK.</span>
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
  <span style="font-weight:400">If you would like to disable offline mode and optionally provide the device_id at a later time, you may do so by adhering to the following:</span>
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
<h1>Multiple trackers on the same domain</h1>
<p>
  <span style="font-weight:400">Sometimes you would like to track different parts of the same domain/website as separate applications.</span>
</p>
<p>
  <span style="font-weight:400">If you just instantiate the Countly SDK in both places, but with different app IDs, then both of their continuous storages will clash storing information for both apps. There are times when this is exactly what you would like to have happen. Generally, it’s function will share a device_id, and although they might be storing requests together, each will be sent to a different app on the same server.</span>
</p>
<p>
  <span style="font-weight:400">However, there are situations where you would like to keep them completely separate. To do so you will need to provide a namespace for the different trackers to keep their local storages from clashing.</span>
</p>
<p>
  <span style="font-weight:400">Simply providing a&nbsp;<strong>namespace&nbsp;</strong>as the init option will suffice.</span>
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
<h1>Cross website/domain tracking</h1>
<p>
  <span style="font-weight:400">You will need to use the same device_id value on the same user in both places to track the same user across different websites or domains.</span>
</p>
<p>
  <span style="font-weight:400">This may be achieved by passing the device ID as a URL parameter when transferring a user from one website/domain to the other.</span>
</p>
<p>
  <strong><span style="font-weight:400">Simply take the device ID value from <strong>Countly.device_id</strong>&nbsp;and pass it as a URL parameter named&nbsp;<strong>cly_device_id</strong>&nbsp;as follows:&nbsp;<a href="http://newdomain.com/?cly_device_id=your-user-device-id">http://newdomain.com/?cly_device_id=your-user-device-id.</a></span></strong>
</p>
<h1>Using the Web SDK in Webview</h1>
<p>
  <span style="font-weight:400">If you are going to use the Web SDK in the Webview of your app, there are prerequisites that must be checked to ensure it is fully functioning. There are no known iOS issues at this moment, but some specific settings need to be enabled for Android.</span>
</p>
<p>
  <span style="font-weight:400">Ensure JavaScript has been enabled for your Webview</span>
</p>
<pre><code class="java">myWebView.getSettings().setJavaScriptEnabled(true);<br></code></pre>
<p>
  <span style="font-weight:400">Ensure local storage has been enabled</span>
</p>
<pre><code class="java">//change the path to where you want to store local storage data
myWebView.getSettings().setDomStorageEnabled(true);
myWebView.getSettings().setDatabaseEnabled(true);
if (Build.VERSION.SDK_INT &lt; Build.VERSION_CODES.KITKAT) {
    myWebView.getSettings().setDatabasePath("/data/data/" + myWebView.getContext().getPackageName() + "/databases/");
}</code></pre>
<p>
  <span style="font-weight:400">If you would like to use Countly both in the native app and Webview, then you would maybe also like to match the device_id between them, so the transitions may be seamless and you may continue to track events and data from both for the same user.</span>
</p>
<p>
  <span style="font-weight:400">In this case, there are a couple things you should do: </span>
</p>
<ol>
  <li>
    <span style="font-weight:400">Defer initializing Countly by putting the initialization code in some function. </span>
  </li>
  <li>
    <span style="font-weight:400">Do not track sessions in Webview as they are already tracked by the native app. </span>
  </li>
  <li>
    <span style="font-weight:400">Pass the device_id to Webview and run the initialization function once Webview has loaded.</span>
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
  <span style="font-weight:400">Then, on the native app side, all you have to do is call the JavaScript functions in the Webview and pass on the device_id to complete this function.</span>
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

NSString *js = [NSString stringWithFormat: @"InitializeCountly('%@');", CountlyDeviceInfo.sharedInstance.deviceID];
[myWebView stringByEvaluatingJavaScriptFromString:js];</code></pre>
  </div>
</div>
<h1>Tracking users with Javascript disabled</h1>
<p>
  <span style="font-weight:400">In some cases, a user might have JavaScript disabled, meaning normal ways of tracking those users will prove ineffective. In such a case, you may use the transparent 1px x 1px image hosted on your Countly server as reporting the URL and report all the same&nbsp;<a href="https://api.count.ly/reference#i">parameters as all the SDKs have been described here</a>.</span>
</p>
<p>
  <span style="font-weight:400">Assuming your Countly is hosted at domain.com and the app_key is "12345", the default setup should look like this:</span>
</p>
<pre><code class="html">&lt;noscript&gt;&lt;img src='http://domain.com/pixel.png?app_key=12345&amp;begin_session=1'/&gt;&lt;/noscript&gt;</code></pre>
<p>
  <span style="font-weight:400">Simply place it anywhere in your HTML code and it should only work if JavaScript is disabled, which means SDK tracking won't work.</span>
</p>
<p>
  <span style="font-weight:400">This would then track how many total sessions there are in where users have JavaScript disabled. The server will attach the device_id as a no_js by default and add the user profile name as ‘No JS’, so you may easier identify how many users without JavaScript you have.</span>
</p>
<p>
  <span style="font-weight:400">However, as mentioned before, this accepts any parameters as a normal SDK endpoint does. Thus, if you dynamically generate data via the server, you may also dynamically generate this URL to provide information that you have about the user. That might be the device_id parameter (for identification), OS, OS version, and any other metrics or information you have, as for example</span>
</p>
<pre><code class="html">&lt;noscript&gt;&lt;img src='http://domain.com/pixel.png?app_key=12345&amp;device_id=test@test.com&amp;begin_session=1&amp;metrics={"_os":"Android", "_os_version":"4.1"}'/&gt;&lt;/noscript&gt;</code></pre>
<h1>Tracked cookie list and explanations</h1>
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
<h1>Symbolication</h1>
<div class="callout callout--warning">
  <h3 class="callout__title">Enterprise</h3>
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