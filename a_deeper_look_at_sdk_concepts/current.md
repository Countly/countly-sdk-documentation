<h1>
Sessions
</h1>
<p>
  <span style="font-weight: 400;">Session in its most basic definition is a group of interactions a user engages in your application/website in a given timeframe. It can be used to keep track of user specific state like user identity, views and events. Again, it can be seen as hits to the server by a single user, grouped in a certain way. Countly has a specific internal logic to group these hits and calls them as sessions.</span>
</p>
<p>
  <span style="font-weight: 400;">In Countly, there are two main methods you can use to track sessions in your application or website. These are namely&nbsp; automatic session tracking and manual session tracking. They both obey the same session flow where a session starts with a “begin session” signal, a session is updated/extended with a “session duration” signal (which is configurable and by default it is every 60 seconds) and where a session end mark is given by “end session” signal. While the automatic session tracking follows this flow with a certain logic and triggers, as explained below, in the case of the manual tracking the triggers are set by the developers who integrate the SDK to their application or website.</span>
</p>
<p>
  <span style="font-weight: 400;">In automatic session tracking, sessions always start with a “begins session” signal when a user connects to your website/app, session is updated/extended by “session update” signal as long as the user is active and the session ends with an “end session” request when the app or site is closed.</span>
</p>
<p>
  <span style="font-weight: 400;">However for Web SDK, after the session has started, as long as the user is active (like clicking or scrolling through a page), the inactivity timer will be reset to its initial value (which is 20 minutes by default). This way the inactivity timer will only start counting when a user is inactive for the last minute (this default value can be changed during the initialization.). And if the user stays inactive for the whole duration of the inactivity timer, only then, the session will come to an end.</span>
</p>
<p>
  <span style="font-weight: 400;">In case a user becomes active just at the end of the inactivity timer or just at the end of the session, Countly servers provide a grace period to extend the session instead of terminating it. This “session cooldown” value is 15 seconds by default and can be changed from the Countly dashboard under the settings section:</span>
</p>
<p>
  <img src="/hc/article_attachments/9291005248537/001.png" alt="001.png">
</p>
<p align="justify">
  <font face="Arial, serif">
    So if a user becomes active from inactivity at the end of inactivity timer
    or opens your site/app again after closing it, as long as it is within the
    session cooldown time, the user session will be extended instead of the creation
    of a new session.
  </font>
</p>
<p align="justify">
  <font face="Arial, serif">
    Another option you can change from your dashboard’s settings section is the
    “maximal session duration”:
  </font>
</p>
<p align="justify">
  <font face="Arial, serif">
    <img src="/hc/article_attachments/9291007294617/002.png" alt="002.png">
  </font>
</p>
<p align="justify">
  <font face="Arial, serif">
    This is a limit for your session update signals, where, if you were updating
    your session in a longer time frame than this value (which is 2 minutes by
    default) Countly servers would cap them to this default value instead to
    provide a better session flow logic, as tandem to the session update signal,
    the SDK also sends recorded events until that time as a request to the server
    and these events are tied to the begin session signal coming before them.
  </font>
</p>
<p align="justify">
  <font face="Arial, serif">
    Session information of a user can be observed from their user profile under
    the “session history” section with their corresponding events, duration and
    starting time:
  </font>
</p>
<p align="justify">
  <font face="Arial, serif">
    <img src="/hc/article_attachments/9291008662425/003.png" alt="003.png">
  </font>
</p>
<p align="justify">&nbsp;</p>
<p align="justify">
  <font face="Arial, serif">
    So the total duration of a session will be calculated by summing up these
    session duration signals and these signals would only be sent as long as
    the user is active or if not, at least inactive while keeping the app/site
    open within the inactivity timer’s activity, for automatic session tracking.
  </font>
</p>
<p align="justify">
  <font face="Arial, serif">
    Manual session tracking works on the same principle as the automatic tracking
    however the developer has the total control over when and where to send “begin
    session”, “session update” and “end session” signals. Also other inner logic
    that is ingrained into automatic session tracking must be handled by the
    developer in order to achieve a proper integration. Which are:
  </font>
</p>
<ul>
  <li>
    <p align="justify">
      <font face="Arial, serif">
        Sending metrics and location information with the begins session
        signal
      </font>
    </p>
  </li>
  <li>
    <p align="justify">
      <font face="Arial, serif">Sending begin session only once per app use/ site visit</font>
    </p>
  </li>
  <li>
    <p align="justify">
      <font face="Arial, serif">Handling inactivity timer logic (optional, for web sdk)</font>
    </p>
  </li>
  <li>
    <p align="justify">
      <font face="Arial, serif">
        Sending session update signals with time elapsed regularly (with
        an internal logic)
      </font>
    </p>
  </li>
  <li>
    <p align="justify">
      <font face="Arial, serif">
        Sending end session signal at proper occasion like tab or app close
      </font>
    </p>
  </li>
</ul>
<p align="justify">
  <font face="Arial, serif">
    User metrics and location information should also be sent with the begin
    session signal. Things like inactivity timer and other time related matters
    have to be handled by the developer to record accurate session information,
    considering the limitations of the platform that they are working with and
    keeping in mind the behavior and the expectations of the Countly server.
  </font>
</p>
<p align="justify">
  <font face="Arial, serif">
    It should also be kept in mind that, if consents are enabled during the initialization,
    if “session” consent was not provided, session tracking would not be working.
  </font>
</p>
<h1>
Reporting "feature data" manually with events
</h1>
<h2>
Views
</h2>
<p>
  <span data-preserver-spaces="true">Currently, SDK doesn't have any direct mechanism to record views. You may record views by using&nbsp;<code><span class="pl-c1">RecordEvent</span></code>&nbsp;method.&nbsp;</span>
</p>
<p>
  <span data-preserver-spaces="true">There are a couple of other values that can be set when recording a view.&nbsp;</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">key-</span></strong><span>&nbsp;</span><code class="java">[CLY]_view</code><span>&nbsp;</span>is
    a predefined by SDK, do not change it while recoding a view.<span data-preserver-spaces="true"><br></span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">segmentation -&nbsp;</span></strong><span data-preserver-spaces="true">A map where you can provide view's name other information related to views.</span><span data-preserver-spaces="true">&nbsp; You may also provide&nbsp;</span><span data-preserver-spaces="true">custom data for your view to track additional information. It is a mandatory field, you may not set it to&nbsp;</span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true">.</span><span data-preserver-spaces="true"></span>
  </li>
  <li>
    <strong>count -&nbsp;</strong>It defines how many time this event<span>&nbsp;</span><span>occurred</span>.
    Set it to 1.
  </li>
</ul>
<p>Example:</p>
<pre><code class="java hljs">std::map&lt;std::string, std::string&gt; segmentation;<br>segmentation[<span class="hljs-string">"</span><span><span class="hljs-string">name</span></span><span class="hljs-string">"</span>] = <span class="hljs-string">"view-name"</span>;<br>segmentation[<span class="hljs-string">"</span><span><span class="hljs-string">visit</span></span><span class="hljs-string">"</span>] = <span class="hljs-string">"1"</span>;<br>segmentation[<span class="hljs-string">"</span><span><span class="hljs-string">segment</span></span><span class="hljs-string">"</span>] = <span class="hljs-string">"Windows"</span>;<br>segmentation[<span class="hljs-string">"</span><span><span class="hljs-string">start</span></span><span class="hljs-string">"</span>] = <span class="hljs-string">"1"</span>;<br></code><code class="java hljs"><br><span class="pl-c1">Countly::getInstance</span><span>()</span>.<span>RecordEvent</span>(<span class="hljs-string">"[CLY]_view"</span>, segmentation, <span class="hljs-number">1</span>);</code></pre>
<p>
  <strong>Note: '</strong>name', 'visit', 'start' and 'segment' are internal keys
  to record a view.
</p>
<h1>Reporting a feedback widget manually</h1>
<p>
  This guide will go into the reporting of feedback widgets (<a href="https://support.count.ly/hc/en-us/articles/900003407386-NPS-Net-Promoter-Score-" target="_self">nps</a>
  and
  <a href="https://support.count.ly/hc/en-us/articles/900004337763-Surveys" target="_self" rel="undefined">surveys</a>)
  manually. It will give more context into how the widget data should be intepreted
  and how the response should be structured when reporting back to the SDK. Not
  all SDK's contain the functionality to do manual feedback widget reporting.&nbsp;
</p>
<p>
  The SDK should provide 2 calls to perform this. One to retrieve the widget data
  describing the widget and another to report the result.
</p>
<p>
  When receiving the data, it would be packaged in a JSON type object. Their structure
  would slightly differ depending for which type of widget it is reported.
</p>
<p>
  In case of a survey, it would looks something like this:<br>
  <br>
</p>
<pre class="c-mrkdwn__pre" data-stringify-type="pre">{<br>   "_id":"601345cf5e313f747656c241",<br>   "app_id":"5e3356e07b96b63120334842",<br>   "name":"Survey name",<br>   "questions":[<br>      {<br>         "type":"multi",<br>         "question":"Multi answer question",<br>         "required":true,<br>         "choices":[<br>            {<br>               "key":"ch1611875792-0",<br>               "value":"Choice A"<br>            },<br>            {<br>               "key":"ch1611875792-1",<br>               "value":"Choice B"<br>            },<br>            {<br>               "key":"ch1611875792-2",<br>               "value":"Choice C"<br>            },<br>            {<br>               "key":"ch1611875792-3",<br>               "value":"Choice D"<br>            }<br>         ],<br>         "randomize":false,<br>         "id":"1611875792-0"<br>      },<br>      {<br>         "type":"radio",<br>         "question":"Radio button question",<br>         "required":false,<br>         "choices":[<br>            {<br>               "key":"ch1611875792-0",<br>               "value":"First"<br>            },<br>            {<br>               "key":"ch1611875792-1",<br>               "value":"Second"<br>            },<br>            {<br>               "key":"ch1611875792-2",<br>               "value":"Third"<br>            },<br>            {<br>               "key":"ch1611875792-3",<br>               "value":"Fourth"<br>            }<br>         ],<br>         "randomize":false,<br>         "id":"1611875792-1"<br>      },<br>      {<br>         "type":"text",<br>         "question":"Text input question",<br>         "required":true,<br>         "id":"1611875792-2"<br>      },<br>      {<br>         "type":"dropdown",<br>         "question":"Question with a dropdown",<br>         "required":false,<br>         "choices":[<br>            {<br>               "key":"ch1611875792-0",<br>               "value":"Value 1"<br>            },<br>            {<br>               "key":"ch1611875792-1",<br>               "value":"Value 2"<br>            },<br>            {<br>               "key":"ch1611875792-2",<br>               "value":"Value 3"<br>            }<br>         ],<br>         "randomize":false,<br>         "id":"1611875792-3"<br>      },<br>      {<br>         "type":"rating",<br>         "question":"Rating type question",<br>         "required":false,<br>         "id":"1611875792-4"<br>      }<br>   ],<br>   "msg":{<br>      "thanks":"Thanks for your feedback!"<br>   },<br>   "appearance":{<br>      "show":"uClose",<br>      "position":"bLeft",<br>      "color":"#2eb52b"<br>   },<br>   "type":"survey"<br>}</pre>
<p>&nbsp;</p>
<p>
  In case of a NPS widget, the JSON internally would look something like this:
</p>
<pre>{
   "_id":"60186d8b3687037dbb058d80",
   "app_id":"5e3356e07b96b63120334842",
   "name":"test3",
   "msg":{
      "mainQuestion":"How likely are you to recommend this product to a friend?",
      "followUpAll":"",
      "followUpPromoter":"We're glad you like us. What do you like the most about our product?",
      "followUpPassive":"Thank you for your feedback. How can we improve your experience?",
      "followUpDetractor":"We're sorry to hear it. What would you like us to improve on?",
      "thanks":"Thanks for your feedback!"
   },
   "followUpType":"score",
   "appearance":{
      "show":"uSubmit",
      "color":"#027aff",
      "style":"full"
   },
   "type":"nps"
}</pre>
<p>
  Both of these describe all server side configured information that would be used
  to visualize a widget manually. Starting from some style and color related fields
  and finally all questions and their potential answers. In the case of surveys,
  it also shows the required id's to report survey results.
</p>
<p>&nbsp;</p>
<p>
  When reporting the widgets results manually, the filled out response is reported
  through the segmentation field.
</p>
<h2>Reporting NPS widgets manually</h2>
<p>
  To report the results of a NPS widget manually, no information from the widgets
  data JSON is needed. These widgets can report only two pieces of information
  - an integer rating from 1 to 10 and a String comment.
</p>
<p>
  Therefore when reporting these results, you need to set two segmentation values,
  one with the key of "rating" and an int value and the other with the "comment"
  key and a String value.
</p>
<h3>Android sample code</h3>
<p>
  The following sample code would report the result of a NPS widget:
</p>
<pre><span>Countly</span>.<span>sharedInstance</span>().feedback().getFeedbackWidgetData(chosenWidget, <span>new </span><span>RetrieveFeedbackWidgetData</span>() {<br>    <span>@Override </span><span>public void </span><span>onFinished</span>(<span>JSONObject </span>retrievedWidgetData, <span>String </span>error) {<br>        <span>Map</span>&lt;<span>String</span>, <span>Object</span>&gt; <span>segm </span>= <span>new </span>HashMap&lt;&gt;();<br>        <span>segm</span>.put(<span>"rating"</span>, <span>3</span>);<span>//value from 1 to 10<br></span><span>        </span><span>segm</span>.put(<span>"comment"</span>, <span>"Filled out comment"</span>);<br><br>        <span>Countly</span>.<span>sharedInstance</span>().feedback().reportFeedbackWidgetManually(<span>widgetToReport</span>, retrievedWidgetData, <span>segm</span>);<br>    }<br>});</pre>
<h2>Reporting Survey widgets manually</h2>
<p>
  To report survey widgets manually, investigation of the data JSON is needed.
  Each question has a question type and depending on the question type, the answer
  needs to be reported in a different way. Each questions also has it's own ID
  which needs to be used as part of the segmentation key when reporting the result.
</p>
<p>
  The questions id can be seen in the "id" field. For example, in the above posted
  survey JSON the first question has the ID of "1611875792-0". When trying to report
  the result for a question, you would append "answ-" to the start of an ID and
  then use that as segmentation key. For example, for the first survey questions
  you would have the result segmentation key of "answ-1611875792-0".
</p>
<p>
  The specific value would depend on the question type. Here is a description of
  how to report results for different question types:
</p>
<p>
  <strong>Multiple answer question</strong>
</p>
<p>
  It has the type "multi". In the question description there is a field "choices"
  which describes all valid options and their keys.
</p>
<p>Users can select any combination of all answers.</p>
<p>
  You would prepare the segmentation value by concatinating the keys of the chosen
  options and using a comma as the delimiter.
</p>
<p>
  For example, the above survey has 4 options in it's first question. If a user
  would choose the first, third and fourth option as the result, the resulting
  value for the answer would be: "ch1611875792-0,ch1611875792-2,ch1611875792-3".
</p>
<p>
  <strong>Radio buttons</strong>
</p>
<p>
  It has the type "radio". In the question description there is a field "choices"
  which describes all valid options and their keys.
</p>
<p>Only one option can be selected.</p>
<p>
  You would use the chosen options key value as the value for your result segementation.
</p>
<p>
  <strong>Dropdown value selector</strong>
</p>
<p>
  It has the type "dropdown". In the question description there is a field "choices"
  which describes all valid options and their keys.
</p>
<p>Only one option can be selected.</p>
<p>
  You would use the chosen options key value as the value for your result segementation.
</p>
<p>
  <strong>Text input field</strong>
</p>
<p>It has the type "text".</p>
<p>You would provide any string you want as the answer.</p>
<p>
  <strong>Rating picker</strong>
</p>
<p>It has the type "rating"</p>
<p>You would provide any int value from 1 to 10 as the answer.</p>
<h3>Android sample code</h3>
<p>
  The following sample code would go through all of the received Survey widgets
  questions and choose a random answer to every question. It the reports the results:
</p>
<pre><span>Countly</span>.<span>sharedInstance</span>().feedback().getFeedbackWidgetData(chosenWidget, <span>new </span><span>RetrieveFeedbackWidgetData</span>() {<br>    <span>@Override </span><span>public void </span><span>onFinished</span>(<span>JSONObject </span>retrievedWidgetData, <span>String </span>error) {<br>        <span>JSONArray questions </span>= retrievedWidgetData.optJSONArray(<span>"questions"</span>);<br><br>        <span>Map</span>&lt;<span>String</span>, <span>Object</span>&gt; <span>segm </span>= <span>new </span>HashMap&lt;&gt;();<br>        <span>Random rnd </span>= <span>new </span>Random();<br><br>        <span>//iterate over all questions and set random answers<br></span><span>        </span><span>for </span>(<span>int </span>a = <span>0</span>; a &lt; <span>questions</span>.length(); a++) {<br>            <span>JSONObject </span>question = <span>null</span>;<br>            <span>try </span>{<br>                question = <span>questions</span>.getJSONObject(a);<br>            } <span>catch </span>(<span>JSONException </span>e) {<br>                e.printStackTrace();<br>            }<br>            <span>String wType </span>= question.optString(<span>"type"</span>);<br>            <span>String questionId </span>= question.optString(<span>"id"</span>);<br>            <span>String answerKey </span>= <span>"answ-" </span>+ <span>questionId</span>;<br>            <span>JSONArray choices </span>= question.optJSONArray(<span>"choices"</span>);<br><br>            <span>switch </span>(<span>wType</span>) {<br>                <span>//multiple answer question<br></span><span>                </span><span>case </span><span>"multi"</span>:<br>                    <span>StringBuilder sb </span>= <span>new </span>StringBuilder();<br><br>                    <span>for </span>(<span>int </span>b = <span>0</span>; b &lt; <span>choices</span>.length(); b++) {<br>                        <span>if </span>(b % <span>2 </span>== <span>0</span>) {//pick every other choice<br>                            <span>if </span>(b != <span>0</span>) {<br>                                <span>sb</span>.append(<span>","</span>);<br>                            }<br>                            <span>sb</span>.append(<span>choices</span>.optJSONObject(b).optString(<span>"key"</span>));<br>                        }<br>                    }<br>                    <span>segm</span>.put(<span>answerKey</span>, <span>sb</span>.toString());<br>                    <span>break</span>;<br>                <span>//radio buttons<br></span><span>                </span><span>case </span><span>"radio"</span>:<br>                <span>//dropdown value selector<br></span><span>                </span><span>case </span><span>"dropdown"</span>:<br>                    <span>int </span><span>pick </span>= <span>rnd</span>.nextInt(<span>choices</span>.length());<br>                    <span>segm</span>.put(<span>answerKey</span>, <span>choices</span>.optJSONObject(<span>pick</span>).optString(<span>"key"</span>));<span>//pick the key of random choice<br></span><span>                    </span><span>break</span>;<br>                <span>//text input field<br></span><span>                </span><span>case </span><span>"text"</span>:<br>                    <span>segm</span>.put(<span>answerKey</span>, <span>"Some random text"</span>);<br>                    <span>break</span>;<br>                <span>//rating picker<br></span><span>                </span><span>case </span><span>"rating"</span>:<br>                    <span>segm</span>.put(<span>answerKey</span>, <span>rnd</span>.nextInt(<span>11</span>));<span>//put a random rating<br></span><span>                    </span><span>break</span>;<br>            }<br>        }<br><br>        <span>Countly</span>.<span>sharedInstance</span>().feedback().reportFeedbackWidgetManually(<span>widgetToReport</span>, retrievedWidgetData, <span>segm</span>);<br>    }<br>});</pre>
<p>&nbsp;</p>
<h1>Handling the Device ID in Your Integrations</h1>
<p>
  Countly tracks your users through an ID called the 'device ID'. This ID is normally
  (by default) generated in the environment the Countly SDK has been integrated
  into (e.g. a smartphone, a web browser, or a desktop application). But how you
  handle this ID would depend on how you define a user in your platform specifically.
</p>
<p>
  What happens if there are several users and several devices that are used interchangeably?
  What happens if a user can log in and log out, hence transitioning between a
  known and an anonymous user? In such cases, you should experiment and decide
  on the correct user tracking strategy before going into production to minimize
  the negative effects.
</p>
<h2>Default User Tracking</h2>
<p>
  By default, Countly defines each device that connects to/uses your app or website
  as a user. Here, the device can be a phone, browser, PC, or tablet.
</p>
<p>
  On your first init, when implementing a Countly SDK, Countly will generate a
  random value (called <strong>device_id</strong>) to identify the user or use
  some platform-specific value; for example, IDFV for
  <a href="/hc/en-us/articles/360037753511" target="_self">iOS</a> and Advertising
  ID for <a href="/hc/en-us/articles/360037754031" target="_self">Android</a>,
  and then store it in the local storage. On consequent inits, the SDK would fetch
  and use this same value as the device ID and would not generate a new one.
</p>
<p>
  Generally speaking, this way assigns a unique ID to a particular user who is
  the owner of that device.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Pros</span>
    <span class="tabs-link">Cons</span>
  </div>
  <div class="tab">
    <ul>
      <li>
        This is the easiest and fastest implementation, with no additional
        steps needed other than undertaking the default SDK implementation.
      </li>
    </ul>
  </div>
  <div class="tab is-hidden">
    <ul>
      <li>
        If multiple different users use the same device, they will be identified
        as a single user in the Countly dashboard and will have a single
        profile under
        <a href="https://count.ly/plugins/user-profiles" target="_blank" rel="noopener nofollow">User Profiles</a>.
      </li>
      <li>
        If the same user uses multiple devices, each device will be identified
        as a separate user in the Countly dashboard; hence the same user
        will have separate user profiles.
      </li>
      <li>
        Depending on the platform, if app storage is reset (erased) or the
        app is uninstalled and re-installed again, this user may be identified
        as a new user and a new user profile is created. This highly depends
        on how the platform behaves. Check
        <a href="https://support.count.ly/hc/en-us/articles/360037501352-Countly-Implementation-and-Technical-FAQ#in-which-situations-does-a-device-id-reset" target="_self">here</a>
        to understand what happens in such cases.
      </li>
    </ul>
  </div>
</div>
<h2>Tracking Known Users</h2>
<p>
  This method, as opposed to the first one, helps Countly identify and track users
  if they are <em>known</em> to you. It is used when tracking the same user across
  multiple devices <em>or</em> different users on the same device, as the default
  tracking method is not appropriate. In this case, you need to provide your
  <strong>user identifier</strong> as the device ID. This unique identifier can
  be a user email address or an internal customer ID — or simply anything
  <strong>unique</strong> to that user. The Countly SDK can then use this string
  as the <strong>device_id</strong>. From this point on, Countly will know precisely
  what user it is and the same <strong>device_id</strong> will be used even across
  different devices.
</p>
<p>
  To accomplish that, you need to provide a string value as the
  <strong>device_id</strong> upon the SDK initialization inside the config object.
  The user authentication page is a good candidate for implementing this method.
  So this might fit applications that can identify their users right away during
  the SDK init, or have little or no actions before authenticating users.
</p>
<p>
  This would be the case when the user inside the Countly dashboard directly corresponds
  to your customer (e.g. 1 Countly user = 1 company customer, regardless of the
  device or platform they use).
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Pros</span>
    <span class="tabs-link">Cons</span>
  </div>
  <div class="tab">
    <ul>
      <li>
        Each of your customers will be exactly 1 single user inside Countly
        and have 1 user profile.
      </li>
    </ul>
  </div>
  <div class="tab is-hidden">
    <ul>
      <li>
        If you do not know your user ID right away and would know it only
        after the user authenticates, you would miss all the actions that
        were made before authentication.
      </li>
    </ul>
  </div>
</div>
<h2>Known User With Pre-Tracking</h2>
<p>
  To tackle the problem of missing out on data before user authentication, it is
  possible to launch the Countly SDK in an <em>offline mode.</em> In this case,
  it will track data but will not send it until you provide your user ID and enable
  the <em>online mode</em>.
</p>
<p>
  This way, you can initialize the SDK in offline mode right when the app starts/user
  connects and track everything needed; when the user finally authenticates, and
  you get your user’s identifier, you can set it as <strong>device_id</strong>
  and enable the online mode so the Countly SDK will start sending data. All previously
  collected data in the offline mode will also be assigned to that user.
</p>
<p>
  For the definition of the user, nothing changes - it still directly corresponds
  to your customer.
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Pros</span>
    <span class="tabs-link">Cons</span>
  </div>
  <div class="tab">
    <ul>
      <li>
        Each of your customers will be exactly 1 single user inside Countly
        and have 1 user profile.
      </li>
      <li>
        You will have the opportunity to be able to collect and visualize
        data before the user authenticates, but only after authentication.
      </li>
    </ul>
  </div>
  <div class="tab is-hidden">
    <ul>
      <li>
        If your user does not authenticate (and so be <em>known</em>), you
        will never receive any data from this user.
      </li>
    </ul>
  </div>
</div>
<h2>Managing Anonymous and Known Users Together</h2>
<p>
  It is also possible to collect data of both user states (before login/known and
  after login/known) and the SDK provides two ways to manage that by allowing to
  change <strong>device_id</strong> <em>after</em> the SDK initialization:
</p>
<p>
  <strong>1. </strong>Change <strong>device_id </strong>without merging. That will
  simply end the session of the old <strong>device_id</strong>, sync all the left
  data, and start a new session for the new <strong>device_id</strong>.
</p>
<p>
  This is handy, for example, when multiple users use the same device and you want
  to track them without sharing their data individually.
</p>
<p>
  <strong>2.</strong> Change <strong>device_id</strong> with merging. This will
  create a new user with a new <strong>device_id</strong>, and start a new session.
  Then, merge the data of the anonymous user with the old
  <strong>device_id</strong> into this new ID. And afterward, delete the anonymous
  user with the old <strong>device_id</strong> from Countly and only keep this
  user's information under the new, developer given ID.
</p>
<p>
  This is handy when, for example, you are firstly tracking an anonymous user with
  a Countly generated <strong>device_id</strong>, but then the user authenticates
  so you retrieve the ID for this user and change it in the SDK, allowing to merge
  both users on the server. This means that everything that the anonymous user
  had, all events and properties, will now be assigned to an identified user and
  the old user will be deleted.
</p>
<p>
  You can implement different strategies that utilize these two options with the
  help of device ID type information. Most Countly SDKs provide calls to see the
  current device ID and the device ID type. The main types you would like to check
  for device ID management are to see if the ID was SDK generated or developer
  supplied.
</p>
<p>
  So with this knowledge, for example, you can start tracking a user as anonymous
  with a Countly generated ID. Then, upon authentication, change the
  <strong>device_id</strong> to your own ID by merging. And then, when the user
  logs out, you can change it back to the anonymous generated ID without user merge.
  The problem is that when the user logs out, it will create a new user inside
  the Countly dashboard again, and there will be 2 different user profiles: one
  with your provided ID and the other with a random ID.
</p>
<p>
  So the user on the Countly dashboard represents both your customer and anonymous
  user before authentication. And in some cases, it could be the same user but
  with 2 different user profiles inside Countly. For applications like banking,
  where the user must log in and log out every time, that can double the user count,
  thus skewing the data.
</p>
<p>
  You can try to tweak this strategy to minimize double-user creation. For example,
  upon logout, let’s not change the <strong>device_id</strong> at all and keep
  using your provided one. Instead, upon authentication, we check if the
  <em>type</em> of <strong>device_id</strong> provided is yours, if it is we switch
  the <strong>device_id</strong> <em>without</em> merging. But if the type of
  <strong>device_id</strong> is Countly generated, then we change the
  <strong>device_id</strong> <em>with</em> user merging.
</p>
<p>In such a case, the scenario would look like this:</p>
<ul class="">
  <li>
    The app starts for the first time and a Countly-generated ID is created.
  </li>
  <li>
    Upon authentication, you confirm that the current <strong>device_id</strong>
    is Countly generated; it means we need to do merging when switching to your
    provided <strong>device_id</strong>.
  </li>
  <li>When the user logs out, we do not do anything.</li>
  <li>
    When the user logs in, we check the current <strong>device_id</strong> and
    we see that it was provided by you. So we switch to the authenticated user’s
    <strong>device_id</strong> <em>without</em> merging. If it is the same user
    and the same ID the SDK currently has, nothing will happen. But if it is
    a different ID, then it is probable that another user logged in and the SDK
    will stop the current session and start a new one for the new user.
  </li>
</ul>
<p>
  These are just a couple of examples of how you could manage tracking data for
  both known users and anonymous ones. The actual implementations may differ based
  on your application specifics. But an example integration of the mentioned method
  can be reached from
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#handling-loginlogout-in-your-app" target="_self">here</a>
</p>
<div class="tabs">
  <div class="tabs-menu">
    <span class="tabs-link is-active">Pros</span>
    <span class="tabs-link">Cons</span>
  </div>
  <div class="tab">
    <ul>
      <li>
        You get to track data for users both before and after authentication.
      </li>
    </ul>
  </div>
  <div class="tab is-hidden">
    <ul>
      <li>
        In some cases, aggregated data may be skewed and may over-report
        users and new users due to many anonymous users getting created.
      </li>
      <li>
        Merging can be quite a performance-intensive process, especially
        if the user that is merged has a lot of data or there are lots of
        users to merge.
      </li>
      <li>
        In some cases, the same user may have a user profile for both states:
        a known user and an anonymous one.
      </li>
      <li>
        It requires SDK integration and customization which is slightly more
        difficult.
      </li>
    </ul>
  </div>
</div>
<h2>Other Known Strategies</h2>
<p>
  We have seen our customers using their own different implementations, and one
  of them was quite effective, which is why we have included it here.&nbsp;This
  strategy involves dividing the onboarding (pre-authenticated users) and authenticated
  users into separate Countly apps.
</p>
<p>
  In this scenario, the customer had quite a long and complicated onboarding process
  with the registration form. But once that was done, there was nothing else to
  do before the login screen. So they wanted to utilize 1 user profile per 1 customer
  inside the Countly dashboard. But they also wanted to track how a user onboards,
  how long it takes, and where they would drop off if registration was not finished.
</p>
<p>
  That is why sending onboarding data to one app and then sending data of known
  users to the other app made perfect sense for them.
</p>
<p>
  Another strategy could be you also leaving a custom property with your user ID
  once registration is complete on the onboarding app, just to be able to tie both
  users together. But note, this approach would require changing
  <strong>app_key</strong> in the running SDK, and currently not all SDKs support
  that. You would need to consult Countly or make modifications yourself on certain
  SDKs.
</p>
<h2>Conclusion</h2>
<p>
  There are different user tracking strategies available. Each one has its own
  pros and cons. You need to understand what kind of data you want to collect and
  what you want the word <em>user</em> to mean exactly for you in the Countly dashboard.
  Make sure you know the options and then you would be able to find the best way
  that fits you with all its trade-offs.
</p>