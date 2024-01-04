<p>
  This documentation shows how you can use the Countly GTM SDK in Google Tag Manager
  platform.
</p>
<p>
  You can reach the source code of the SDK from its Git repo
  <a href="https://github.com/Countly/countly-sdk-gtm" target="_blank" rel="noopener noreferrer">here</a>.
</p>
<h1 id="h_01HABTQ436ACJV96Q5P2MMNGWZ" class="anchor-heading">Adding the SDK to the Project</h1>
<p>
  You can reach the Countly SDK template in your Google Tag Manager container through:
</p>
<pre>Workspace &gt; Tags &gt; New &gt; Tag Configuration &gt; Community Template Gallery &gt; Countly Analytics
</pre>
<p>
  Another method to get the SDK template is to add it manually after downloading
  it from the Git repo
  <a href="https://github.com/Countly/countly-sdk-gtm" target="_blank" rel="noopener noreferrer">here</a>.
  You can either download it as a zip file and extract its content:
</p>
<pre>Code &gt; Download ZIP&nbsp;</pre>
<p>or you can clone the repo and reach files directly:</p>
<pre>git clone https://github.com/Countly/countly-sdk-gtm.git</pre>
<p>
  After you should import the <code>template.tpl</code> file you have downloaded
  to your container through:
</p>
<pre>Workspace &gt; Templates &gt; New &gt; Import
</pre>
<p>Now it should be available at:</p>
<pre>Workspace &gt; Tags &gt; New &gt; Tag Configuration &gt; Countly Analytics
</pre>
<h1 id="h_01HABTQ436KQ0HD0G5NXFBZQR7" class="anchor-heading">SDK Integration</h1>
<h2 id="h_01HHNRWS0NC1ETRH4WG2YDD878">Minimal Setup</h2>
<p>
  The first thing you should be doing with the SDK template is to initialize the
  SDK as soon as possible on your web page by selecting a proper trigger.
  <code>Initialization</code> trigger is a good candidate for this. For SDK initialization
  the template offers the action <code>Initialize the SDK</code> in the drop down
  menu:
</p>
<p>
  <img src="/guide-media/01HHNRG4J4WHCA00Z4V9C795D0" width="500" height="500" alt="001.png">
</p>
<p>
  Here the Server URL and the App Key are mandatory values.
  <span>Please check&nbsp;</span><a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#acquiring-your-application-key-and-server-url">here</a><span>&nbsp;for more information on how to acquire your application key (APP_KEY) and server URL.</span>
</p>
<h2 id="h_01HHNRWK1D3WCXZW2H3WQKGX42">Enabling Features</h2>
<p>
  After setting up you App Key and Server URL you will see checkboxes below. These
  are optional features of the SDK that you can enable during initialization:
</p>
<ul>
  <li>
    <strong>Enable SDK Logs:</strong> Enables the SDK to print logs in browser
    console for debugging&nbsp;
  </li>
  <li>
    <strong>Track Sessions</strong>: Enables automatic session tracking
  </li>
  <li>
    <strong>Track Page Views</strong>: Enables automatic view tracking
  </li>
  <li>
    <strong>Track Clicks</strong>: Enables automatic tracking of user click actions
  </li>
  <li>
    <strong>Track Scrolls</strong>: Enables automatic tracking of user scroll
    actions
  </li>
  <li>
    <strong>Track Errors</strong>: Enables the tracking of JavaScript errors
    happening on your website
  </li>
</ul>
<h1 id="h_01HHNS9CX3XMFQ7BQNDNZZV6DM">Events</h1>
<p>
  Another action the SDK template provides is the ability to record events. Events
  are a way to track any custom actions or other data you would like to track from
  your website. You may also set segments to be able to view a breakdown of the
  action by providing the segment values.
</p>
<p>
  To record an event you would need to use the <code>Record Event</code> action
  in the template's drop down menu:
</p>
<p>
  <img src="/guide-media/01HHNSFHWTSA9HFT191WTTJ01R" width="600" height="600" alt="002.png">
</p>
<p>
  Here the Event Key is a mandatory value. It represents the name of the event
  that you will see in you Countly server. However, segmentation is optional key/value
  pairs you can send with the event if extra information would be needed.
</p>
<p>&nbsp;</p>