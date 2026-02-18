<p>
  SDK Behavior Settings is a remote control mechanism for Countly SDKs that allows
  managing core behavior and features without requiring any code changes or app
  releases. This means you can control how your SDK behaves directly from your
  Countly server dashboard.
</p>
<p>
  To access it, navigate through the Countly dashboard:
  <strong>Utilities -&gt; SDK Manager -&gt; SDK Behavior Settings</strong>
</p>
<p>
  <img src="/guide-media/01K1Z767X1Y0Y6GY1VF23SS3BN">
</p>
<p>
  For more information about the SDK Behavior Settings, you can have a look
  <a href="/hc/en-us/articles/30459276723353#h_01HZ7RDSRQ1B93E997YXZMNN9Q">here</a>.
</p>
<h1 id="h_01JRSYQTVZ140AFKRASA1WZYFG">Integrating SDK Behavior Settings in SDKs</h1>
<p>
  On the SDK side, If you're using the latest version of the Android, iOS, Web,
  Flutter and React Native SDKs, SDK Behavior Settings is already supported out
  of the box. No code changes are required to support SDK Behavior Settings.
</p>
<p>
  To reduce network traffic or control the number of requests, you can disable
  automatic SDK Behavior Settings updates from the server.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Android</span>
    <span class="tabs-link">iOS</span> <span class="tabs-link">Web</span>
    <span class="tabs-link">Flutter</span>
    <span class="tabs-link">React Native</span>
  </div>
  <div class="tab">
    <pre><code class="java">countlyConfig.disableSDKBehaviorSettingsUpdates();</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="objectivec">countlyConfig.disableSDKBehaviorSettingsUpdates = YES;</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="js">config["disable_sdk_behavior_settings_updates"] = true</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="dart">countlyConfig.disableSDKBehaviorSettingsUpdates()</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="js">countlyConfig.disableSDKBehaviorSettingsUpdates()</code></pre>
  </div>
</div>
<p>
  In all cases, the settings may not be applied during the app’s first run. If
  this is a security sensitive case for the situations, you can manually download
  the settings using the <strong>"Download Config"</strong> button at the top right
  and provide it to the SDK during initialization.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Android</span>
    <span class="tabs-link">iOS</span> <span class="tabs-link">Web</span>
    <span class="tabs-link">Flutter</span>
    <span class="tabs-link">React Native</span>
  </div>
  <div class="tab">
    <pre><code class="java">countlyConfig.setSDKBehaviorSettings(String sdkBehaviorSettings)</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="objectivec">countlyConfig.sdkBehaviorSettings = NSString</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="js">config["behavior_settings"] = String</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="dart">countlyConfig.setSDKBehaviorSettings(String sdkBehaviorSettings)</code></pre>
  </div>
  <div class="tab is-hidden">
    <pre><code class="js">countlyConfig.setSDKBehaviorSettings(object sdkBehaviorSettings)</code></pre>
  </div>
</div>
<p>
  During SDK initialization, settings are determined based on the following priority
  (from highest to lowest):
</p>
<ol>
  <li>
    <p>
      The latest configuration fetched from the server (applied after initialization).
    </p>
  </li>
  <li>
    <p>
      A previously stored SDK Behavior Settings from past sessions.
    </p>
  </li>
  <li>
    <p>
      An SDK Behavior Settings explicitly provided during initialization.
    </p>
  </li>
  <li>
    <p>Other user-provided settings in the initialization config.</p>
  </li>
  <li>
    <p>The SDK's built-in default values.</p>
  </li>
</ol>
<p>
  This ensures that the SDK always starts with the best available configuration
  while allowing updates from the server after initialization.
</p>
<p>
  As a result of this order, some features might not use the latest SDK Behavior
  Settings immediately. Therefore, providing the SDK Behavior Settings during initialization
  might be necessary in certain cases.
</p>
<p>
  For more details on how SDKs handle Behavior Settings during initialization and
  runtime, see
  <a href="https://support.countly.com/hc/en-us/articles/21551709869980-How-SDKs-Work#h_01K01WEVMX2JA8N8SW0QKE7X8C">here.</a>
</p>