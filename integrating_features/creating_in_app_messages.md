<h1 id="h_01JP9QWQBZHAJQ1T4X9EDVFTWJ">What Are In-App Messages in Countly?</h1>
<div>
  <div>
    <div>
      <div>
        <p>
          In-app messages in Countly allow you to engage users with personalized
          notifications, promotions, or updates directly within your app.
        </p>
        <p>
          You can create and show in-app messages using two features we
          have:
        </p>
        <ul>
          <li>
            <strong>With Content Builder</strong>, you create and design
            in-app messages, defining the content, layout, and style
            of your messages.
          </li>
          <li>
            <strong>With Journeys</strong>, in-app messages are triggered
            by defining conditions and events, which determine when and
            how the messages will appear to users.
          </li>
        </ul>
      </div>
    </div>
  </div>
</div>
<div tabindex="0">
  <div></div>
</div>
<h1 id="h_01JP9QWQBZC3NHMTNWFQFFYS99">Setting Up In-App Messages on the Server</h1>
<p>
  To distribute in-app messages within your app, follow these steps:
</p>
<ol>
  <li>
    <p>
      <strong>Create a content block</strong>: Begin by creating a content
      block in the Content Builder. This content block defines the message's
      structure, such as the text, images, and buttons that will be displayed
      to the users. For detailed instructions, refer to the
      <a href="/hc/en-us/articles/17072500159388" target="_new" rel="noopener">Content Builder documentation</a>.
    </p>
  </li>
  <li>
    <p>
      <strong>Set up a journey</strong>: After creating the content block,
      configure a journey to define when and how the in-app message will be
      presented to your users. A journey specifies the user actions or conditions
      that trigger the message. For more information on creating a journey,
      refer to the
      <a href="/hc/en-us/articles/17072475592988" target="_new" rel="noopener">Journeys documentation</a>.
    </p>
  </li>
</ol>
<p>
  By following these steps, you'll be able to distribute personalized in-app messages
  to your users at the right time and in the right context.
</p>
<h1 id="h_01JP9QWQBZ0N2Q140V3E97G7R3">Integrating In-App Messages in SDKs</h1>
<p>
  Integrating in-app messages with the SDKs is straightforward and requires just
  a single line of code for all supported SDKs. Please note that all functions
  must be called after initializing the SDK; otherwise, the call will not be executed
  successfully.
</p>
<p>
  This call will retrieve and display the most up-to-date in-app message available
  for the user. By making this request, the system ensures that the user receives
  the latest content.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Android</span>
    <span class="tabs-link">iOS</span> <span class="tabs-link">Web</span>
    <span class="tabs-link">Flutter</span>
    <span class="tabs-link">React Native</span>
  </div>
  <div class="tab">
    <pre><code class="java">Countly.sharedInstance().contents().enterContentZone();</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="objectivec">[Countly.sharedInstance.content enterContentZone];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="js">Countly.content.enterContentZone();</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="dart">Countly.instance.content.enterContentZone()
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="js">Countly.content.enterContentZone();
</code></pre>
  </div>
</div>
<h3 id="h_01JP9XB7X6SXZ4RE7QV6B52QW2">Current Limitations</h3>
<p>
  In-app messages may not appear immediately, as content is fetched periodically
  from the server. This means that there could be a slight delay in displaying
  the latest messages to users, depending on the fetch interval set for the content.
</p>
<div class="callout callout--warning">
  <p>
    Frequent manual fetching can increase server load and lead to performance
    issues.
  </p>
</div>
<p>
  If you need to achieve an instant fetch, you can manually trigger a content refresh
  by using the "refreshContentZone" function, which will force the SDK to fetch
  the content immediately, bypassing the timer interval.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Android</span>
    <span class="tabs-link">iOS</span> <span class="tabs-link">Web</span>
    <span class="tabs-link">Flutter</span>
    <span class="tabs-link">React Native</span>
  </div>
  <div class="tab">
    <pre><code class="java">Countly.sharedInstance().contents().refreshContentZone();</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="objectivec">[Countly.sharedInstance.content refreshContentZone];</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="js">Countly.content.refreshContentZone();</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="dart">Countly.instance.content.refreshContentZone()
</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="js">Countly.content.refreshContentZone();
</code></pre>
  </div>
</div>
<p>
  For detailed information on content-related methods, you can refer to the Content
  Zone section in the
  <a href="/hc/en-us/sections/360007310512">SDKs documentation</a> of your respective
  platform
</p>