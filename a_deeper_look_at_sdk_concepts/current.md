<h1 id="h_01HABT18WSGG477SSMB4BGB04K">Sessions</h1>
<p>
  <span style="font-weight: 400;">Session, in its most basic definition, is a group of interactions a user engages in your application/website in a given timeframe. It can be used to keep track of user-specific states like user identity, views, and events. Again, it can be seen as hits to the server by a single user, grouped in a certain way. Countly has a specific internal logic to group these hits and calls them as sessions.</span>
</p>
<p>
  <span style="font-weight: 400;">In Countly, there are two main methods you can use to track sessions in your application or website. These are automatic session tracking and manual session tracking. They both obey the same session flow where a session starts with a “begin session” signal, a session is updated/extended with a “session duration” signal (which is configurable and by default is every 60 seconds), and a session end mark is given by “end session” signal. While the automatic session tracking follows this flow with a certain logic and triggers, as explained below, in the case of the manual tracking, the triggers are set by the developers who integrate the SDK into their application or website.</span>
</p>
<p>
  <span style="font-weight: 400;">In automatic session tracking, sessions always start with a “begins session” signal when a user connects to your website/app, session is updated/extended by “session update” signal as long as the user is active and the session ends with an “end session” request when the app or site is closed.</span>
</p>
<p>
  <span style="font-weight: 400;">However, for Web SDK, after the session has started, as long as the user is active (like clicking or scrolling through a page), the inactivity timer will be reset to its initial value (which is 20 minutes by default). This way, the inactivity timer will only start counting when a user is inactive for the last minute (this default value can be changed during the initialization.). And if the user stays inactive for the whole duration of the inactivity timer, only then, the session will come to an end.</span>
</p>
<p>
  <span style="font-weight: 400;">In case a user becomes active just at the end of the inactivity timer or just at the end of the session, Countly servers provide a grace period to extend the session instead of terminating it. This “session cooldown” value is 15 seconds by default and can be changed from the Countly dashboard under the settings section:</span>
</p>
<p>
  <img src="/guide-media/01GVBGKPGGWB79MAQ25JJBXCN9" alt="001.png">
</p>
<p align="justify">
  <font face="Arial, serif">
    So if a user becomes active from inactivity at the end of the inactivity
    timer or opens your site/app again after closing it, as long as it is within
    the session cooldown time, the user session will be extended instead of the
    creation of a new session.
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
    <img src="/guide-media/01GVCKHHAJASX64PZQ27KP9DD7" alt="002.png">
  </font>
</p>
<p align="justify">
  <font face="Arial, serif">
    This is a limit for your session update signals, where, if you were updating
    your session in a longer time frame than this value (which is 2 minutes by
    default), then Countly servers would cap them to this default value. To provide
    a better session flow logic, as a tandem to the session update signal, the
    SDK also sends recorded events until that time as a request to the server,
    and these events are tied to the begin session signal coming before them.
  </font>
</p>
<p align="justify">
  <font face="Arial, serif">
    Session information of a user can be observed from their user profile under
    the “session history” section with their corresponding events, duration,
    and starting time:
  </font>
</p>
<p align="justify">
  <font face="Arial, serif">
    <img src="/guide-media/01GV9ZW670RZWB810F4EGKE57T" alt="003.png">
  </font>
</p>
<p align="justify">&nbsp;</p>
<p align="justify">
  <font face="Arial, serif">
    So the total duration of a session will be calculated by summing up these
    session duration signals, and these signals would only be sent as long as
    the user is active or, if not, at least inactive while keeping the app/site
    open within the inactivity timer’s activity, for automatic session tracking.
  </font>
</p>
<p align="justify">
  <font face="Arial, serif">
    Manual session tracking works on the same principle as the automatic tracking.
    However, the developer has total control over when and where to send “begin
    session,” “session update,” and “end session” signals. Also, other inner
    logic that is ingrained into automatic session tracking must be handled by
    the developer in order to achieve a proper integration. Which are:
  </font>
</p>
<ul>
  <li>
    <p align="justify">
      <font face="Arial, serif">
        Sending metrics and location information with the begin session signal.
      </font>
    </p>
  </li>
  <li>
    <p align="justify">
      <font face="Arial, serif">Sending begin session only once per app use/ site visit.</font>
    </p>
  </li>
  <li>
    <p align="justify">
      <font face="Arial, serif">Handling inactivity timer logic (optional, for web SDK).</font>
    </p>
  </li>
  <li>
    <p align="justify">
      <font face="Arial, serif">
        Sending session update signals with time elapsed regularly (with
        an internal logic).
      </font>
    </p>
  </li>
  <li>
    <p align="justify">
      <font face="Arial, serif">
        Sending end session signal at a proper occasion like tab or app close.
      </font>
    </p>
  </li>
</ul>
<p align="justify">
  <font face="Arial, serif">
    User metrics and location information should also be sent with the begin
    session signal. Things like an inactivity timer and other time-related matters
    have to be handled by the developer to record accurate session information,
    considering the limitations of the platform that they are working with and
    keeping in mind the behavior and the expectations of the Countly server.
  </font>
</p>
<p align="justify">
  <font face="Arial, serif">
    It should also be kept in mind that, if consents are enabled and “session”
    consent was not provided, during the initialization, &nbsp;session tracking
    will not work.
  </font>
</p>
<h1 id="h_01HABT18WSV43CFW5YDA5G0BNP">Reporting "feature data" manually with events</h1>
<h2 id="h_01HABT18WSXVTMVFRN0SFX427D">Views</h2>
<p>
  <span data-preserver-spaces="true">Currently, SDK doesn't have any direct mechanism to record views. You may record views by using&nbsp;<code><span class="pl-c1">RecordEvent</span></code>&nbsp;method.&nbsp;</span>
</p>
<p>
  <span data-preserver-spaces="true">There are a couple of other values that can be set when recording a view.&nbsp;</span>
</p>
<ul>
  <li>
    <strong><span data-preserver-spaces="true">key-</span></strong><span>&nbsp;</span><code class="java">[CLY]_view</code><span>&nbsp;</span>is
    predefined by SDK, do not change it while recording a view.<span data-preserver-spaces="true"><br></span>
  </li>
  <li>
    <strong><span data-preserver-spaces="true">segmentation- </span></strong><span data-preserver-spaces="true">A map where you can provide the view's name and other information related to views. </span><span data-preserver-spaces="true">You may also provide&nbsp;</span><span data-preserver-spaces="true">custom data for your view to track additional information. It is a mandatory field, you may not set it to&nbsp;</span><strong><span data-preserver-spaces="true">null</span></strong><span data-preserver-spaces="true">.</span><span data-preserver-spaces="true"></span>
  </li>
  <li>
    <strong>count- </strong>It defines how many times this event<span>&nbsp;</span><span>occurred</span>.
    Set it to 1.
  </li>
</ul>
<p>Example:</p>
<pre><code class="java hljs">std::map&lt;std::string, std::string&gt; segmentation;<br>segmentation[<span class="hljs-string">"</span><span><span class="hljs-string">name</span></span><span class="hljs-string">"</span>] = <span class="hljs-string">"view-name"</span>;<br>segmentation[<span class="hljs-string">"</span><span><span class="hljs-string">visit</span></span><span class="hljs-string">"</span>] = <span class="hljs-string">"1"</span>;<br>segmentation[<span class="hljs-string">"</span><span><span class="hljs-string">segment</span></span><span class="hljs-string">"</span>] = <span class="hljs-string">"Windows"</span>;<br>segmentation[<span class="hljs-string">"</span><span><span class="hljs-string">start</span></span><span class="hljs-string">"</span>] = <span class="hljs-string">"1"</span>;<br></code><code class="java hljs"><br><span class="pl-c1">Countly::getInstance</span><span>()</span>.<span>RecordEvent</span>(<span class="hljs-string">"[CLY]_view"</span>, segmentation, <span class="hljs-number">1</span>);</code></pre>
<p>
  <strong>Note: </strong>'name,' 'visit,' 'start', and 'segment' are internal keys
  to record a view.
</p>
<h1 id="h_01HABT18WTFWFNKVPJJ6G6DEM4">Working with Feedback Widgets</h1>
<h2 id="h_01HABT18WTEHRZTAQ49GRGNBP1">Interpreting Retrieved Feedback Widget Lists</h2>
<p>
  When working with feedback widgets, at some point, the available feedback widget
  list has to be retrieved from the Countly server. The SDK will expose a method
  for that, and it will be named similar to
  <code>getAvailableFeedbackWidgets</code>. The return value will be a list of
  objects that describe the available widgets. The objects will have the following
  fields, the brackets contain their key in the retrieved JSON:
</p>
<ul>
  <li>
    widget id (_id)- This is the respective widget ID that you can also see in
    your dashboard.
  </li>
  <li>
    widget type (type)- This describes the widget type. It would be either 'nps,'
    'survey', or 'rating'.
  </li>
  <li>
    widget name (name)- This is the widget name from your dashboard.
  </li>
  <li>
    widget tags (tg)- This is an Array of String tag values from the widget creation
    (this would be an empty Array if no tags were assigned).
  </li>
  <li>
    appearance information (appearance)- (not exposed in all SDKs) This is some
    UI information about the widget (currently, only rating and survey widgets
    would have these values).
  </li>
</ul>
<p>
  In our Web SDK, you would not receive a parsed result. Instead, you would receive
  the JSON as it would be returned from the server. The returned array would look
  something like the following:
</p>
<div>
  <pre><span>[</span><br><span>  &nbsp;{</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"_id"</span><span>:</span><span>"614811419f030e44be07d82f"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"type"</span><span>:</span><span>"rating"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"appearance"</span><span>:{</span><br><span>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span><span>"position"</span><span>:</span><span>"mleft"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span><span>"bg_color"</span><span>:</span><span>"#fff"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span><span>"text_color"</span><span>:</span><span>"#ddd"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span><span>"text"</span><span>:</span><span>"Feedback"</span><br><span>  &nbsp; &nbsp; },</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"tg"</span><span>:[</span><span>"startPage"</span><span>],</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"name"</span><span>:</span><span>"Leave us a feedback"</span><br><span>  &nbsp;},</span><br><span>  &nbsp;{</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"_id"</span><span>:</span><span>"614811419f030e44be07d839"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"type"</span><span>:</span><span>"nps"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"name"</span><span>:</span><span>"One response for all"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"tg"</span><span>:[</span><span>]</span><br><span>  &nbsp;},</span><br><span>  &nbsp;{</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"_id"</span><span>:</span><span>"614811429f030e44be07d83d"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"type"</span><span>:</span><span>"survey"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"appearance"</span><span>:{</span><br><span>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span><span>"position"</span><span>:</span><span>"bLeft"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span><span>"show"</span><span>:</span><span>"uSubmit"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span><span>"color"</span><span>:</span><span>"#0166D6"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span><span>"logo"</span><span>:</span><span>null</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span><span>"submit"</span><span>:</span><span>"Submit"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span><span>"previous"</span><span>:</span><span>"Previous"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;</span><span>"next"</span><span>:</span><span>"Next"</span><br><span>  &nbsp; &nbsp; },</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"name"</span><span>:</span><span>"Product Feedback example"</span><span>,</span><br><span>&nbsp; &nbsp; &nbsp; </span><span>"tg"</span><span>:[</span><span>]</span><br><span>  &nbsp;}</span><br><span>]</span></pre>
</div>
<h2 id="h_01HABT18WT0D08H8DR2BAD77T2">Reporting a feedback widget manually</h2>
<p>
  This guide will go into the reporting of feedback widgets (<a href="https://support.count.ly/hc/en-us/articles/900003407386-NPS-Net-Promoter-Score-" target="_self">nps</a>,
  <a href="https://support.count.ly/hc/en-us/articles/900004337763-Surveys" target="_self" rel="undefined">surveys</a>,
  and
  <a href="https://support.count.ly/hc/en-us/articles/360037641291-Ratings" target="_blank" rel="noopener">ratings</a>)
  manually. It will give more context into how the widget data should be interpreted
  and how the response should be structured when reporting back to the SDK. Also,
  it must be noted that not all SDKs contain the functionality to do manual feedback
  widget reporting.&nbsp;
</p>
<p>The SDK should provide 3 calls to perform this process:</p>
<ol>
  <li>A call to fetch the widget list from the server.</li>
  <li>A call to fetch a single widget's data from the server.</li>
  <li>A call to report a single widget to the server.</li>
</ol>
<p>
  The widget list received would be a JSON array of objects corresponding to the
  widgets. By selecting one of these objects (widgets) and providing it in the
  second call developer can fetch its data from the server. When receiving the
  data, it would be packaged in a JSON type object. Their structure would slightly
  differ depending on the type of widget being reported.
</p>
<p>
  In case of a survey, widget data would look something like this:<br>
  <br>
</p>
<pre class="c-mrkdwn__pre" data-stringify-type="pre">{<br>   "_id":"601345cf5e313f747656c241",<br>   "app_id":"5e3356e07b96b63120334842",<br>   "name":"Survey name",<br>   "questions":[<br>      {<br>         "type":"multi",<br>         "question":"Multi answer question",<br>         "required":true,<br>         "choices":[<br>            {<br>               "key":"ch1611875792-0",<br>               "value":"Choice A"<br>            },<br>            {<br>               "key":"ch1611875792-1",<br>               "value":"Choice B"<br>            },<br>            {<br>               "key":"ch1611875792-2",<br>               "value":"Choice C"<br>            },<br>            {<br>               "key":"ch1611875792-3",<br>               "value":"Choice D"<br>            }<br>         ],<br>         "randomize":false,<br>         "id":"1611875792-0"<br>      },<br>      {<br>         "type":"radio",<br>         "question":"Radio button question",<br>         "required":false,<br>         "choices":[<br>            {<br>               "key":"ch1611875792-0",<br>               "value":"First"<br>            },<br>            {<br>               "key":"ch1611875792-1",<br>               "value":"Second"<br>            },<br>            {<br>               "key":"ch1611875792-2",<br>               "value":"Third"<br>            },<br>            {<br>               "key":"ch1611875792-3",<br>               "value":"Fourth"<br>            }<br>         ],<br>         "randomize":false,<br>         "id":"1611875792-1"<br>      },<br>      {<br>         "type":"text",<br>         "question":"Text input question",<br>         "required":true,<br>         "id":"1611875792-2"<br>      },<br>      {<br>         "type":"dropdown",<br>         "question":"Question with a dropdown",<br>         "required":false,<br>         "choices":[<br>            {<br>               "key":"ch1611875792-0",<br>               "value":"Value 1"<br>            },<br>            {<br>               "key":"ch1611875792-1",<br>               "value":"Value 2"<br>            },<br>            {<br>               "key":"ch1611875792-2",<br>               "value":"Value 3"<br>            }<br>         ],<br>         "randomize":false,<br>         "id":"1611875792-3"<br>      },<br>      {<br>         "type":"rating",<br>         "question":"Rating type question",<br>         "required":false,<br>         "id":"1611875792-4"<br>      }<br>   ],<br>   "msg":{<br>      "thanks":"Thanks for your feedback!"<br>   },<br>   "appearance":{<br>      "show":"uClose",<br>      "position":"bLeft",<br>      "color":"#2eb52b"<br>   },<br>   "type":"survey"<br>}</pre>
<p>&nbsp;</p>
<p>
  In case of an NPS widget, the JSON internally would look something like this:
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
  And in case of a rating widget, it would look something like this:
</p>
<pre>{<br> "_id":"62222d125852e20462481193",<br> "popup_header_text":"What&amp;#39;s your opinion about this page?",<br> "popup_comment_callout":"Add comment",<br> "popup_email_callout":"Contact me via e-mail",<br> "popup_button_callout":"Submit feedback",<br> "popup_thanks_message":"Thank you for your feedback",<br> "trigger_position":"mright",<br> "trigger_bg_color":"13B94D",<br> "trigger_font_color":"FFFFFF",<br> "trigger_button_text":"Feedback",<br> "target_devices":{<br> "phone":true,<br> "desktop":true,<br> "tablet":true<br> },<br> "target_page":"all",<br> "target_pages":["/"],<br> "is_active":"true",<br> "hide_sticker":false,<br> "app_id":"12345687af5c256b91a6345f",<br> "contact_enable":"true",<br> "comment_enable":"true",<br> "trigger_size":"m",<br> "type":"rating",<br> "ratings_texts":[<br> "Very dissatisfied",<br> "Somewhat dissatisfied",<br> "Neither satisfied Nor Dissatisfied",<br> "Somewhat Satisfied",<br> "Very Satisfied"<br> ],<br> "status":true,<br> "targeting":null,<br> "ratingsCount":116,<br> "ratingsSum":334<br>}</pre>
<p>
  These describe all server-side configured information that would be used to visualize
  a widget manually. Starting from some style and color-related fields and, finally
  all questions and their potential answers. In the case of surveys, it also shows
  the required id's to report survey results.
</p>
<p>&nbsp;</p>
<p>
  When reporting these widget's results manually, the filled-out response is reported
  through the segmentation field of the reporting event. So depending on the type
  of widget you are reporting, you have to construct a
  <strong>widgetResult </strong>object, specific to that widget, which would then
  be utilized in the third call that has been mentioned at the top of this section.
  In this third call, the developer is expected to provide the widget object obtained
  from the first call, the widget's data object that has been obtained from the
  second call, and a properly formed <strong>widgetResult&nbsp;</strong>object
  that has been created with respect to the type of widget that is being reported.
  More information on how to form this object is provided below.
</p>
<h3 id="h_01HABT18WVCY6BTEXM9TW7XJ0B">Reporting NPS widgets manually</h3>
<p>
  To report the results of an NPS widget manually, no information from the widget's
  data JSON is needed. These widgets can report only two pieces of information
  - an Integer <strong>rating,</strong> ranging from 0 to 10, and a String
  <strong>comment</strong>, representing the user's comment.
</p>
<p>
  Therefore when reporting these results, you need to set two segmentation values,
  one with the key of "rating" and an Integer value and the other with the "comment"
  key and a String value.
</p>
<h4 id="h_01HABT18WVKNM54RJC97S4KQ5T">Android sample code</h4>
<p>
  The following sample code would report the result of an NPS widget:
</p>
<pre><span>Countly</span>.<span>sharedInstance</span>().feedback().getFeedbackWidgetData(chosenWidget, <span>new </span><span>RetrieveFeedbackWidgetData</span>() {<br>    <span>@Override </span><span>public void </span><span>onFinished</span>(<span>JSONObject </span>retrievedWidgetData, <span>String </span>error) {<br>        <span>Map</span>&lt;<span>String</span>, <span>Object</span>&gt; <span>segm </span>= <span>new </span>HashMap&lt;&gt;();<br>        <span>segm</span>.put(<span>"rating"</span>, <span>3</span>);<span>//value from 0 to 10<br></span><span>        </span><span>segm</span>.put(<span>"comment"</span>, <span>"Filled out comment"</span>);<br><br>        <span>Countly</span>.<span>sharedInstance</span>().feedback().reportFeedbackWidgetManually(<span>widgetToReport</span>, retrievedWidgetData, <span>segm</span>);<br>    }<br>});</pre>
<h4 id="h_01HABT18WV01YQA39M5CJN18WP">Web sample code</h4>
<p>
  The following code shows what the expected widgetResult objects look like for
  the NPS widget:
</p>
<pre>var widgetResult = {<br>         rating: 3, // between 0 to 10<br>         comment: "any comment" // string<br>    };</pre>
<h3 id="h_01HABT18WVQRSQ4RQS28P4QN9R">Reporting Rating widgets manually</h3>
<p>
  To report the results of a Rating widget manually, again, no information from
  the obtained widget data is needed. These widgets have similar reporting capabilities
  to NPS widgets. Similarly there would be an Integer <strong>rating,</strong>
  ranging from 1 to 5, and a String <strong>comment</strong>, representing the
  user's comment. Then, in addition to these, there would be an
  <strong>email</strong> String for the user email and a
  <strong>contactMe</strong> Boolean (true or false) if the user gave consent to
  be contacted again or not.
</p>
<h4 id="h_01HABT18WV70HE6GXMF0X9V2AN">Web sample code</h4>
<p>
  The following code shows what the expected widgetResult objects look like for
  the Rating widget:
</p>
<pre>var widgetResult = {<br>         rating: 3, // between 1 to 5<br>         comment: "any comment", // string<br>         email: "email@any.mail", // string<br>         contactMe: true // boolean<br>    };</pre>
<h3 id="h_01HABT18WVWCX0W68RGB0FJ1KK">Reporting Survey widgets manually</h3>
<p>
  To report survey widgets manually, an investigation of the widget data received
  from the second call is needed. Each question has a question type, and depending
  on the question type, the answer needs to be reported in a different way. Each
  question also has it's own ID, which needs to be used as part of the segmentation
  key when reporting the result.
</p>
<p>
  The question id can be seen in the "id" field. For example, in the above posted
  survey JSON the first question has the ID of "1611875792-0". When trying to report
  the result for a question,
  <strong>you would append "answ-" to the start of an ID</strong> and then use
  that as a segmentation key. For example, for the first survey questions, you
  would have the result segmentation key of "answ-1611875792-0".
</p>
<p>
  At the end, your widgetResult would look something like this (Web example):
</p>
<pre>var widgetResult = {<br>       "answ-1602694029-0": "answer", // for text input fields<br>       "answ-1602694029-1": 7, // for rating picker<br>       "answ-1602694029-2": "ch1602694029-0", // there is a question with choices. It is a choice key<br>       "answ-1602694029-3": "ch1602694030-0,ch1602694030-1" // in case 2 choices selected<br>      };</pre>
<p>
  The specific value would depend on the question type. Here is a description of
  how to report results for different question types:
</p>
<p>
  <strong>Multiple answer question</strong>
</p>
<p>
  It has the type "multi". In the question description, there is a field "choices,"
  which describes all valid options and their keys.
</p>
<p>Users can select any combination of all answers.</p>
<p>
  You would prepare the segmentation value by concatenating the keys of the chosen
  options and using a comma as the delimiter.
</p>
<p>
  For example, the above survey has four options in its first question. If a user
  chooses the first, third, and fourth options as the result, the resulting value
  for the answer would be: "ch1611875792-0,ch1611875792-2,ch1611875792-3".
</p>
<p>
  <strong>Radio buttons</strong>
</p>
<p>
  It has the type "radio". In the question description, there is a field "choices,"
  which describes all valid options and their keys.
</p>
<p>Only one option can be selected.</p>
<p>
  You would use the chosen options key value as the value for your result segmentation.
</p>
<p>
  <strong>Dropdown value selector</strong>
</p>
<p>
  It has the type "dropdown". In the question description, there is a field "choices,"
  which describes all valid options and their keys.
</p>
<p>Only one option can be selected.</p>
<p>
  You would use the chosen options key value as the value for your result segmentation.
</p>
<p>
  <strong>Text input field</strong>
</p>
<p>It has the type "text".</p>
<p>You would provide any String you want as the answer.</p>
<p>
  <strong>Rating picker</strong>
</p>
<p>It has the type "rating"</p>
<p>
  You would provide any Integer value from 1 to 10 as the answer.
</p>
<h4 id="h_01HABT18WV5DA061HYZ3FYBCD3">Android sample code</h4>
<p>
  The following sample code would go through all of the received Survey widgets
  questions and choose a random answer to every question. It then reports the results:
</p>
<pre><span>Countly</span>.<span>sharedInstance</span>().feedback().getFeedbackWidgetData(chosenWidget, <span>new </span><span>RetrieveFeedbackWidgetData</span>() {<br>    <span>@Override </span><span>public void </span><span>onFinished</span>(<span>JSONObject </span>retrievedWidgetData, <span>String </span>error) {<br>        <span>JSONArray questions </span>= retrievedWidgetData.optJSONArray(<span>"questions"</span>);<br><br>        <span>Map</span>&lt;<span>String</span>, <span>Object</span>&gt; <span>segm </span>= <span>new </span>HashMap&lt;&gt;();<br>        <span>Random rnd </span>= <span>new </span>Random();<br><br>        <span>//iterate over all questions and set random answers<br></span><span>        </span><span>for </span>(<span>int </span>a = <span>0</span>; a &lt; <span>questions</span>.length(); a++) {<br>            <span>JSONObject </span>question = <span>null</span>;<br>            <span>try </span>{<br>                question = <span>questions</span>.getJSONObject(a);<br>            } <span>catch </span>(<span>JSONException </span>e) {<br>                e.printStackTrace();<br>            }<br>            <span>String wType </span>= question.optString(<span>"type"</span>);<br>            <span>String questionId </span>= question.optString(<span>"id"</span>);<br>            <span>String answerKey </span>= <span>"answ-" </span>+ <span>questionId</span>;<br>            <span>JSONArray choices </span>= question.optJSONArray(<span>"choices"</span>);<br><br>            <span>switch </span>(<span>wType</span>) {<br>                <span>//multiple answer question<br></span><span>                </span><span>case </span><span>"multi"</span>:<br>                    <span>StringBuilder sb </span>= <span>new </span>StringBuilder();<br><br>                    <span>for </span>(<span>int </span>b = <span>0</span>; b &lt; <span>choices</span>.length(); b++) {<br>                        <span>if </span>(b % <span>2 </span>== <span>0</span>) {//pick every other choice<br>                            <span>if </span>(b != <span>0</span>) {<br>                                <span>sb</span>.append(<span>","</span>);<br>                            }<br>                            <span>sb</span>.append(<span>choices</span>.optJSONObject(b).optString(<span>"key"</span>));<br>                        }<br>                    }<br>                    <span>segm</span>.put(<span>answerKey</span>, <span>sb</span>.toString());<br>                    <span>break</span>;<br>                <span>//radio buttons<br></span><span>                </span><span>case </span><span>"radio"</span>:<br>                <span>//dropdown value selector<br></span><span>                </span><span>case </span><span>"dropdown"</span>:<br>                    <span>int </span><span>pick </span>= <span>rnd</span>.nextInt(<span>choices</span>.length());<br>                    <span>segm</span>.put(<span>answerKey</span>, <span>choices</span>.optJSONObject(<span>pick</span>).optString(<span>"key"</span>));<span>//pick the key of random choice<br></span><span>                    </span><span>break</span>;<br>                <span>//text input field<br></span><span>                </span><span>case </span><span>"text"</span>:<br>                    <span>segm</span>.put(<span>answerKey</span>, <span>"Some random text"</span>);<br>                    <span>break</span>;<br>                <span>//rating picker<br></span><span>                </span><span>case </span><span>"rating"</span>:<br>                    <span>segm</span>.put(<span>answerKey</span>, <span>rnd</span>.nextInt(<span>11</span>));<span>//put a random rating<br></span><span>                    </span><span>break</span>;<br>            }<br>        }<br><br>        <span>Countly</span>.<span>sharedInstance</span>().feedback().reportFeedbackWidgetManually(<span>widgetToReport</span>, retrievedWidgetData, <span>segm</span>);<br>    }<br>});</pre>
<h1 id="h_01HABT18WV676C95X2768C5PN5">
  There Is No SDK That I Can Integrate for My Use Case. What are the options?
</h1>
<p>
  Countly SDKs provide you with many options to track your users with the least
  amount of code in a way that fits your use case. Behind the scene, the SDK would
  do various tasks to gather information, reshape this information in a way the
  Countly servers can understand, and prevent the possibility of data loss as much
  as possible. With the help of the SDKs, you only need to write a single line
  of code while the SDK does hundreds of lines of work behind the hood. However,
  the core principles behind these operations are simple even though they are tedious.
  So if you come across a situation where you can not integrate a Countly SDK into
  your project, you can still be able to track your users and inform that information
  to your Countly instance as long as you can send API calls following the core
  rules and structures that is shared among all Countly SDKs.
</p>
<p>
  To be able to track your users manually and to share this information you have
  gathered with your Countly instance you will need to know three things:
</p>
<ol>
  <li>What information is the server looking for?</li>
  <li>What API endpoint should you use?</li>
  <li>How should you structure your requests?</li>
</ol>
<p>
  As long as you have the answers to these questions, you can track your users
  and gather information in any way you want as long as you form and send correct
  requests to your Countly server. Documentations that would be useful to find
  the answers to these questions are the
  <a href="https://support.count.ly/hc/en-us/articles/900005345483-Countly-Terminology" target="_blank" rel="noopener">Countly glossary</a>
  to understand the Countly terminology, the
  <a href="https://api.count.ly/reference/i#modifying-custom-user-data" target="_blank" rel="noopener">API documentation</a>
  to see the endpoints and the data structure, the
  <a href="https://support.count.ly/hc/en-us/articles/360037753291-SDK-development-guide" target="_blank" rel="noopener">SDK Development Guide</a>
  to see the scope of the endpoints, and the specific documentation of the
  <a href="https://support.count.ly/hc/en-us/sections/360007310512-SDKs" target="_blank" rel="noopener">SDK</a>
  of your platform to see the capabilities and the features.
</p>
<h1 id="h_01HABT18WVPPB1PX9J7MG2ZSCT">Handling the Device ID in Your Integrations</h1>
<p>
  Countly tracks your users through an ID called the 'device ID.' This is attached
  to every request (which contains events and other data) that is sent to the Countly
  server. This ID consists of String characters.
</p>
<p>
  This ID is normally (by default) generated in the environment the Countly SDK
  has been integrated into (e.g., a smartphone, a web browser, or a desktop application).
  But how you handle this ID would depend on how you define a user in your platform
  specifically.
</p>
<p>
  What happens if there are several users and several devices that are used interchangeably?
  What happens if a user can log in and log out, hence transitioning between a
  known and an anonymous user? In such cases, you should experiment and decide
  on the correct user tracking strategy before going into production to minimize
  the negative effects. For an overview on how these different situations could
  be handled, look
  <a href="#h_01GG7QB1WJQR1G8NX3EHP1ADG7" target="_self">below</a>.
</p>
<h2 id="h_01HABT18WV7K7Z4RJB5B82AZTY">Available Mechanisms For Interacting With Device ID</h2>
<p>
  Countly SDKs try to be configurable and flexible, and handling device IDs is
  no exception.
</p>
<h3 id="h_01HABT18WVX6YTM8WK5145BPY1">Device ID During Init</h3>
<p>
  Countly SDKs behave differently in the first on a device compared to subsequent
  init's.
</p>
<p>
  On your first init, when integrating a Countly SDK, Countly will try to acquire
  a device ID. By default, Countly will generate a random value (for the
  <strong>device_id</strong>) to identify the user or use some platform-specific
  value; for example, IDFV for
  <a href="/hc/en-us/articles/360037753511" target="_self">iOS</a>, and then store
  it in the local storage.
</p>
<p>
  On subsequent inits, the SDK would fetch and use this same value as the device
  ID. It will not generate a new one. By default, the SDK would ignore any provided
  device ID values.
</p>
<p>
  There are some configuration options during initialization. During the first
  init, it is possible to do the following actions:
</p>
<ul>
  <li>
    Provide a custom device ID- SDK will use the provided ID and will not generate
    one.
  </li>
  <li>
    Tell the SDK which device ID generation method to use- in some SDKs, it is
    possible to influence the ID generator and pick a specific method.
  </li>
  <li>
    Enable temporary device ID mode- while in this mode, the SDK will not send
    anything to the Countly server until a device ID has been provided.
  </li>
  <li>
    Provide a device ID with a URL parameter- this exists only in the Web SDK.
    This provides a way to "inject" a device ID on a first run.
  </li>
</ul>
<p>
  Some SDKs might have a "clear stored device ID" flag that can be set during init.
  If this is done, then the SDK will clear it's stored value and will try to reacquire
  a device ID value. It would then behave like on the first init. It is generally
  not advised to use this flag as it can cause user count inflation issues.
</p>
<p>
  For a deeper overview of how the SDK would behave in different situations, have
  a look at
  <a href="https://support.count.ly/hc/en-us/articles/360037753291-SDK-development-guide#device-id-state-management-during-init" target="_blank" rel="noopener">this</a>
  table.
</p>
<h3 id="h_01GG7QEZ64EJEE01S5NHXGW1QR">Changing Device ID</h3>
<p>
  Countly SDKs provide two ways to change the device_id after the SDK initialization:
</p>
<p>
  1. Change device_id without merging. That will simply end the session of the
  old device_id, sync all the left data, and start a new session for the new device_id.
</p>
<p>
  This is handy, for example, when multiple users use the same device, and you
  want to track them without sharing their data individually.
</p>
<p>
  2. Change device_id with merging. This will create a new user with a new device_id,
  and start a new session. Then, merge the data of the anonymous user with the
  old device_id into this new ID. And afterward, delete the anonymous user with
  the old device_id from Countly and only keep this user's information under the
  new developer-given ID.
</p>
<p>
  This is handy when, for example, you are firstly tracking an anonymous user with
  a Countly generated device_id, but then the user authenticates, so you retrieve
  the ID for this user and change it in the SDK, allowing to merge both users on
  the server. This means that everything that the anonymous user had, all events
  and properties, will now be assigned to an identified user, and the old user
  will be deleted.
</p>
<p>
  You can implement different strategies that utilize these two options with the
  help of device ID type information. Most Countly SDKs provide calls to see the
  current device ID and the device ID type. The main types you would like to check
  for device ID management are to see if the ID was SDK-generated or developer-supplied.
</p>
<h3 id="h_01GG7QKAWDG3P7QC5G691MS9R8">Offline / Temporary ID mode</h3>
<p>
  It is possible to launch the Countly SDK in an <em>offline/temporary ID </em>mode
  during the first initialization. This mode can also enabled after initialization
  with the use of special calls exposed by the SDK.
</p>
<p>
  If this mode is enabled, no data will be sent to the server until a real device
  ID value is provided by the host app. After that is done, all stored requests
  will be marked as created by this device ID and then sent to the server and assigned
  to this user.
</p>
<h3 id="h_01GG7QHSKF855N2WREMQMW3ZPH">Device ID Type</h3>
<p>
  Most Countly SDKs provide calls to see the current device ID and the device ID
  type. The main types you would like to check for device ID management are to
  see if the ID was SDK-generated or developer-supplied.
</p>
<h2 id="h_01GG7QB1WJQR1G8NX3EHP1ADG7">Different user tracking strategies</h2>
<h3 id="h_01HABT18WWTB0FRGMQMW22JND2">Default User Tracking</h3>
<p>
  As mentioned in the "Device ID during init" section. With no additional configuration,
  the SDK will generate a random device ID on the first init and then use it.
</p>
<p>
  Generally speaking, this way assigns a unique ID to a particular user who is
  the owner of that device (phone, browser, PC, or tablet).
</p>
<p>
  <strong>Pros</strong>
</p>
<ul>
  <li>
    This is the easiest and fastest implementation, with no additional steps
    needed other than undertaking the default SDK implementation.
  </li>
</ul>
<p>
  <strong>Cons</strong>
</p>
<ul>
  <li>
    If multiple different users use the same device, they will be identified
    as a single user in the Countly dashboard and will have a single profile
    under
    <a href="https://count.ly/plugins/user-profiles" target="_blank" rel="noopener nofollow">User Profiles</a>.
  </li>
  <li>
    If the same user uses multiple devices, each device will be identified as
    a separate user in the Countly dashboard; hence the same user will have separate
    user profiles.
  </li>
  <li>
    Depending on the platform, if app storage is reset (erased) or the app is
    uninstalled and re-installed again, this user most likely will be identified
    as a new user, and a new user profile will be created. This highly depends
    on how the platform behaves. Check
    <a href="https://support.count.ly/hc/en-us/articles/360037501352-Countly-Implementation-and-Technical-FAQ#in-which-situations-does-a-device-id-reset" target="_self">here</a>
    to understand what happens in such cases.
  </li>
</ul>
<h3 id="h_01HABT18WW2EQPJV5HVB9PYDBJ">Tracking Known Users</h3>
<p>
  This method, as opposed to the first one, helps Countly identify and track users
  if they are <em>known</em> to you. It is used when tracking the same user across
  multiple devices <em>or</em> different users on the same device, as the default
  tracking method is not appropriate. In this case, you need to provide your
  <strong>user identifier</strong> as the device ID. This unique identifier can
  be a user email address or an internal customer ID — or simply anything
  <strong>unique</strong> to that user. The Countly SDK can then use this String
  as the <strong>device_id</strong>. From this point on, Countly will know precisely
  what user it is, and the same <strong>device_id</strong> will be used even across
  different devices.
</p>
<p>
  To accomplish that, you need to provide a String value as the
  <strong>device_id</strong> upon the SDK initialization inside the config object.
  The user authentication page is a good candidate for implementing this method.
  So this might fit applications that can identify their users right away during
  the SDK init, or have little or no actions before authenticating users.
</p>
<p>
  This would be the case when the user inside the Countly dashboard directly corresponds
  to your customer (e.g., 1 Countly user = 1 company customer, regardless of the
  device or platform they use).
</p>
<p>
  <strong>Pros</strong>
</p>
<ul>
  <li>
    Each of your customers will be exactly one single user inside Countly and
    have one user profile.
  </li>
</ul>
<p>
  <strong>Cons</strong>
</p>
<ul>
  <li>
    If you do not know your user ID right away and would know it only after the
    user authenticates, you will miss all the actions that were made before authentication.
  </li>
</ul>
<h3 id="h_01HABT18WW4680K69GS1P5NFN0">Known User With Pre-Tracking</h3>
<p>
  To tackle the problem of missing out on data before user authentication, it is
  possible to launch the Countly SDK in an <em>offline/temporary ID mode.</em>
  This mode is described in the
  <a href="#h_01GG7QKAWDG3P7QC5G691MS9R8" target="_self">Offline / Temporary ID mode</a>
  section.
</p>
<p>
  This way, you can track everything needed, before knowing the user's identity.
  When the user finally authenticates, you get your user’s identifier and use that
  to exit the Offline / Temporary ID mode
</p>
<p>
  For the definition of the user, nothing changes- it still directly corresponds
  to your customer.
</p>
<p>
  <strong>Pros</strong>
</p>
<ul>
  <li>
    Each of your customers will be exactly one single user inside Countly and
    have one user profile.
  </li>
  <li>
    You will have the opportunity to be able to collect and visualize data before
    the user authenticates, but only after authentication.
  </li>
</ul>
<p>
  <strong>Cons</strong>
</p>
<ul>
  <li>
    If your user does not authenticate (and so be <em>known</em>), you will never
    receive any data from this user.
  </li>
</ul>
<h3 id="h_01HABT18WW14G16YGGDEW9NAC5">Managing Anonymous and Known Users Together</h3>
<p>
  It is also possible to collect data of both user states (before login/known and
  after login/known) and manage the ID using the functionality discussed in the
  above,
  <a href="#h_01GG7QEZ64EJEE01S5NHXGW1QR" target="_self">changing device ID</a>
  section.
</p>
<p>
  You can implement different strategies that utilize these two options with the
  help of the device ID type information that has been discussed in the
  <a href="#h_01GG7QHSKF855N2WREMQMW3ZPH" target="_self">device ID type</a> section.
</p>
<p>
  So with this knowledge, for example, you can start tracking a user as anonymous
  with a Countly generated ID. Then, upon authentication, change the
  <strong>device_id</strong> to your own ID by merging. And then, when the user
  logs out, you can change it back to the anonymous generated ID without user merge.
  The problem is that when the user logs out, it will create a new user inside
  the Countly dashboard again, and there will be two different user profiles: one
  with your provided ID and the other with a random ID.
</p>
<p>
  So the user on the Countly dashboard represents both your customer and anonymous
  user before authentication. And in some cases, it could be the same user but
  with two different user profiles inside Countly. For applications like banking,
  where the user must log in and log out every time, that can double the user count,
  thus skewing the data.
</p>
<p>
  You can try to tweak this strategy to minimize double-user creation. For example,
  upon logout, let’s not change the <strong>device_id</strong> at all and keep
  using your provided one. Instead, upon authentication, we check if the
  <em>type</em> of <strong>device_id</strong> provided is yours, if it is, we switch
  the <strong>device_id</strong> <em>without</em> merging. But if the type of
  <strong>device_id</strong> is Countly generated, then we change the
  <strong>device_id</strong> <em>with</em> user merging.
</p>
<p>In such a case, the scenario would look like this:</p>
<ul class="">
  <li>
    The app starts for the first time, and a Countly-generated ID is created.
  </li>
  <li>
    Upon authentication, you confirm that the current <strong>device_id</strong>
    is Countly generated; it means we need to do merging when switching to your
    provided <strong>device_id</strong>.
  </li>
  <li>When the user logs out, we do not do anything.</li>
  <li>
    When the user logs in, we check the current <strong>device_id</strong>, and
    we see that it was provided by you. So we switch to the authenticated user’s
    <strong>device_id</strong> <em>without</em> merging. If it is the same user
    and the same ID the SDK currently has, nothing will happen. But if it is
    a different ID, then it is probable that another user logged in, and the
    SDK will stop the current session and start a new one for the new user.
  </li>
</ul>
<p>
  These are just a couple of examples of how you could manage tracking data for
  both known users and anonymous ones. The actual implementations may differ based
  on your application specifics. But an example integration of the mentioned method
  can be reached from
  <a href="https://support.count.ly/hc/en-us/articles/900000908046-Getting-started-with-SDKs#handling-loginlogout-in-your-app" target="_self">here</a>.
</p>
<p>
  <strong>Pros</strong>
</p>
<ul>
  <li>
    You get to track data for users both before and after authentication.
  </li>
</ul>
<p>
  <strong>Cons</strong>
</p>
<ul>
  <li>
    In some cases, aggregated data may be skewed and may over-report users and
    new users due to many anonymous users getting created.
  </li>
  <li>
    Merging can be quite a performance-intensive process, especially if the user
    that is merged has a lot of data or there are lots of users to merge.
  </li>
  <li>
    In some cases, the same user may have a user profile for both states: a known
    user and an anonymous one.
  </li>
  <li>
    It requires SDK integration and customization, which is slightly more difficult.
  </li>
</ul>
<h3 id="h_01HABT18WWEGJEHHSQPARRPB9F">Other Known Strategies</h3>
<p>
  We have seen our customers using their own different implementations, and one
  of them was quite effective, which is why we have included it here.&nbsp;This
  strategy involves dividing the onboarding (pre-authenticated users) and authenticated
  users into separate Countly apps.
</p>
<p>
  In this scenario, the customer had quite a long and complicated onboarding process
  with the registration form. But once that was done, there was nothing else to
  do before the login screen. So they wanted to utilize one user profile per one
  customer inside the Countly dashboard. But they also wanted to track how a user
  onboards, how long it takes, and where they would drop off if registration was
  not finished.
</p>
<p>
  That is why sending onboarding data to one app and then sending data of known
  users to the other app made perfect sense for them.
</p>
<p>
  Another strategy could be you also leaving a custom property with your user ID
  once registration is complete on the onboarding app, just to be able to tie both
  users together. This approach would require changing <strong>app_key</strong>
  in the running SDK, and currently, not all SDKs support that. You would need
  to consult Countly or make modifications yourself on certain SDKs.
</p>
<h3 id="h_01HABT18WWG9VJE5WPSSJWKNVD">Conclusion</h3>
<p>
  There are different user tracking strategies available. Each one has its own
  pros and cons. You need to understand what kind of data you want to collect and
  what you want the word <em>user</em> to mean exactly for you in the Countly dashboard.
  Make sure you know the options, and then you will be able to find the best way
  that fits you with all its trade-offs.
</p>
<h1 id="h_01HABT18WWYQ2QYPZY3GHZBA9B">Setting Custom User Metrics</h1>
<p>
  User metrics are sent when starting a session or requesting remote config. Some
  SDKs expose functionality to override the SDK set metric values or provide custom
  ones.
</p>
<p>
  Not all keys are used by all SDKs. Here is a list of metric keys used by Countly:
</p>
<ul>
  <li>
    <span><strong>_os</strong>- The name of the platform/operating system.</span>
  </li>
  <li>
    <span><strong>_os_version</strong>- Version of platform/operating system.</span>
  </li>
  <li>
    <span><strong>_app_version</strong>- sets the application version. For some platforms, this is retrieved from the app configuration.</span><span></span>
  </li>
  <li>
    <span><strong>_device</strong>- Device model name.</span>
  </li>
  <li>
    <span><strong>_device_type</strong>- sets what kind of device is using the app. The potential values are: "console," "mobile," "tablet," "smart tv," "wearable," "embedded," "desktop".</span>
  </li>
  <li>
    <span><strong>_resolution</strong>- The screen resolution of the device.</span>
  </li>
  <li>
    <span><strong>_density</strong>- Screen density of the device.</span>
  </li>
  <li>
    <span><strong>_locale</strong>- Locale or language of the device in ISO format.</span>
  </li>
  <li>
    <span><strong>_store</strong>- (Mobile SDK) A source where the user came from.&nbsp;</span>
  </li>
  <li>
    <span><strong>_carrier</strong>- (Mobile SDK) Carrier or operator used for connection.</span><span></span>
  </li>
  <li>
    <span><strong>_has_watch</strong>- (iOS SDK).&nbsp;</span>
  </li>
  <li>
    <div>
      <div>
        <span><strong>_installed_watch_app</strong>- (iOS SDK).&nbsp;</span>
      </div>
    </div>
  </li>
  <li>
    <span><strong>_browser</strong>- (Web SDK) Browser name.</span>
  </li>
  <li>
    <span><strong>_browser_version</strong>- (Web SDK) Browser version.</span>
  </li>
  <li>
    <span><strong>_ua</strong>- (Web SDK) User agent String.</span>
  </li>
</ul>
<h1 id="h_01HABT18WWS0TZ37FZX1FW3ECS">Preparing Your App for Symbolication</h1>
<p>
  <span style="font-weight: 400;">This section will guide you through the Android, iOS, and JavaScript symbolication processes.</span>
</p>
<h2 id="h_01HABT18WWB8BGBKK00RD3PA1W">Android</h2>
<p>
  <span style="font-weight: 400;">Android's official tool for code shrinking and obfuscation is called ProGuard. A detailed description of its usage can be found&nbsp;<a href="https://developer.android.com/studio/build/shrink-code.html" target="_blank" rel="noopener">here</a>. There is also a paid tool with additional features called&nbsp;<a href="https://www.guardsquare.com/en/dexguard" target="_blank" rel="noopener">DexGuard</a>. Both ProGuard and DexGuard can be used for Countly crash symbolication. Currently, we do not support any other Android obfuscation libraries.</span>
</p>
<p>
  <span style="font-weight: 400;">If you are using Android Studio for development, the mapping files will not be produced when you make instant runs. For them to appear, you will either need to generate a signed APK or choose the <strong>Build APK</strong>&nbsp;option.</span>
</p>
<div class="img-container wysiwyg-text-align-center">
  <img src="https://archive.count.ly/images/guide/e31d5d2-3.png">
</div>
<p>
  <span style="font-weight: 400;">After the build is complete, the symbol file called <code>mapping.txt</code></span><span style="font-weight: 400;">&nbsp;can be found under <code>&lt;module-name&gt;/build/outputs/mapping/release/</code></span><span style="font-weight: 400;">&nbsp;or <code>&lt;module-name&gt;/build/outputs/mapping/debug/</code></span><span style="font-weight: 400;">, depending on how you initiate the build process.</span>
</p>
<h3 id="h_01HABT18WW4ZW13QKAAV1GZSBB">ProGuard Rules</h3>
<p>
  <span style="font-weight: 400;">You have the option of adding some rules to ProGuard (or DexGuard) and modifying how it runs. These rules should be added to the <strong>proguard-rules.pro</strong>&nbsp;file.</span>
</p>
<p>
  <span style="font-weight: 400;">If you decide to use ProGuard, you have to keep in mind that it will rename the function and class names. Therefore, it will break the code that is using reflection if you don't take steps to stop this from happening. You may find more information in the ProGuard </span><a href="https://www.guardsquare.com/en/proguard/manual/introduction" target="_blank" rel="noopener">manual</a><span style="font-weight: 400;">.</span>
</p>
<p>
  <span style="font-weight: 400;">At the very least, you should include these lines in your ProGuard rule file:</span>
</p>
<pre><code class="text">-keep class org.openudid.** { *; }
-renamesourcefileattribute SourceFile
-keepattributes SourceFile,LineNumberTable</code></pre>
<p>
  <span style="font-weight: 400;">The first one is needed to prevent <code>openudid</code> from breaking, and Countly uses it for generating user IDs. The second and third rules are needed to add source file and line number information to your Android stack traces.</span>
</p>
<p>
  <span style="font-weight: 400;">The ProGuard rule file should be named <strong>proguard-rules.pro</strong>, and it is usually located at the root of your module. More information </span><a href="https://developer.android.com/studio/build/shrink-code.html#keep-code" target="_blank" rel="noopener">here</a><span style="font-weight: 400;">.</span>
</p>
<h2 id="h_01HABT18WWQ6R5BYSGCNXTKTGY">iOS</h2>
<p>
  <span class="wysiwyg-color-black" style="font-weight: 400;">The symbol file is a dSYM file for iOS.</span>
</p>
<ul>
  <li>
    <span style="font-weight: 400;">A dSYM file is Apple's standard Mach-O file which contains debug symbols for a given build.</span>
  </li>
  <li>
    <span style="font-weight: 400;">It includes debug symbols for all architectures used for the build (e.g. armv7, arm64).</span>
  </li>
  <li>
    <span style="font-weight: 400;">Its size may vary depending on the original source code and libraries used in the project.</span>
  </li>
  <li>
    <span style="font-weight: 400;">It is a file-like folder structure, and actual dSYM data is in the binary </span><span style="font-weight: 400;">file </span><code>AppName.app.dSYM/Contents/Resources/DWARF/AppName</code>.
  </li>
</ul>
<h3 id="h_01HABT18WW3S1CDQA8S8D7XWB1">dSYM Location</h3>
<p>
  <span style="font-weight: 400;">First of all, for each executable target (main app, extensions, and Cocoa Touch Frameworks) in the project, a separate dSYM file is generated when the project is built. The dSYM location depends on the build settings. By default, it is defined by <code>$DWARF_DSYM_FOLDER_PATH</code>&nbsp;Xcode Environment Variable.</span>
</p>
<p>
  An example location is:
  <code>~/Library/Developer/Xcode/DerivedData/AppName-abcdef0123456789/Build/Products/Release-iphoneos/AppName.app.dSYM</code>
</p>
<p>
  <span style="font-weight: 400;">In addition, if you use the <code>Product &gt; Archive</code></span><span style="font-weight: 400;"> option in Xcode to create the <code>.xcarchive</code></span><span style="font-weight: 400;"> of your app, you may find a dSYM already created inside the <code>.xcarchive</code></span><span style="font-weight: 400;">. By default, its location is: <code>~/Library/Developer/Xcode/Archives/YYYY-MM-DD/AppName DD-MM-YYYY, HH.mm.xcarchive/dSYMs</code></span>
</p>
<h3 id="h_01HABT18WWB2RYD1XCT9HESD1D">Automatic dSYM Upload</h3>
<p>
  For automatic dSYM, please see the Countly iOS SDK documentation
  <a href="https://support.count.ly/hc/en-us/articles/360037753511-iOS-watchOS-tvOS-macOS#symbolication" target="_self" rel="undefined">here</a>.
</p>
<h2 id="h_01HABT18WWMW9E0W66Z9QMN1P7">JavaScript</h2>
<p>
  In order to symbolicate errors, we need a source map file. We will try to lay
  out how you can produce a source map file for builds that use Webpack, you can
  also consult your build tool's documentation on how to generate one for your
  builds.
</p>
<p>
  So, for this demonstration, we will use the
  <a href="https://github.com/Countly/countly-sdk-web/tree/master/samples/symbolication" target="_self">sample frontend application</a>
  that is available in the Countly Web SDK repository. It is a simple project with
  just one source file <code>src/index.js</code> that imports a third-party dependency,
  the Countly SDK, and binds a couple of buttons to throw errors.
</p>
<pre>import Countly from "countly-sdk-web"<br><br>Countly.init({<br>  app_key: "YOUR_APP_KEY",<br>  app_version: "1.0",<br>  url: "https://try.count.ly",<br>  debug: true<br>});<br><br>//track sessions automatically<br>Countly.track_sessions();<br><br>//track pageviews automatically<br>Countly.track_pageview();<br><br>//track any clicks to webpages automatically<br>Countly.track_clicks();<br><br>//track link clicks automatically<br>Countly.track_links();<br><br>//track form submissions automatically<br>Countly.track_forms();<br><br>//track javascript errors<br>Countly.track_errors();<br><br>//let's cause some errors<br>function cause_error(){<br>  undefined_function();<br>}<br><br>window.onload = function() {<br>  document.getElementById("handled_error").onclick = function handled_error(){<br>    Countly.add_log('Pressed handled button'); <br>    try {<br>      cause_error();<br>    } catch(err){<br>      Countly.log_error(err)<br>    }<br>  };<br><br>  document.getElementById("unhandled_error").onclick = function unhandled_error(){<br>    Countly.add_log('Pressed unhandled button'); <br>    cause_error();<br>  };<br>}</pre>
<p>
  We also have a webpack configuration that takes this source file, resolves its
  import, and minifies the resulting file, creating a single minified file
  <strong>dist/main.js</strong>. Also, note that we've set the
  <a href="https://webpack.js.org/configuration/devtool/" target="_self">devtool</a>
  option to
  <span><code>hidden-source-map</code> which means webpack will generate a source map file but will not reference it in the <strong>main.js</strong> file. This is typically ideal for production environments where you don't need to inspect the underlying code in the browser. You might want to go with <code>source-map</code> in development environments, it <em>will</em> reference the source map file in <strong>main.js</strong>&nbsp;and ease debugging in the browser.<br></span>
</p>
<pre>const path = require('path');
const webpack = require('webpack');
const TerserPlugin = require('terser-webpack-plugin');

module.exports = {
  mode: 'development',
  plugins: [new webpack.ProgressPlugin()],
  devtool: "hidden-source-map",

  module: {
    rules: [{
      test: /\.(js|jsx)$/,
      include: [path.resolve(__dirname, 'src')],
      loader: 'babel-loader'
    }]
  },

  optimization: {
    minimize: true,
    minimizer: [new TerserPlugin()],
  },

  output: {
    devtoolModuleFilenameTemplate: '[resource-path]',
    devtoolFallbackModuleFilenameTemplate: '[absolute-resource-path]'
  }
};
</pre>
<p>
  Here is a screenshot of how you would run the webpack with npx and use the webpack
  package that would be installed along with your project.
</p>
<p>
  <img src="/guide-media/01GVBGJPE1FSBDCNJNEARRF63E" alt="1612759824.png">
</p>
<p>
  Then, you can see that webpack produced<strong> themain.js</strong>&nbsp;file
  along with its source map file <strong>main.js.map</strong>. Now, we just need
  to upload that source map file to our Countly instance.
</p>
<p>
  <img src="/guide-media/01GVCKG7Q5YKKS920QD1T2RG8Y" alt="1612759876.png">
</p>
<h1 id="h_01HDNHXZ2Y30VG0D1TKCYPHJXT">Acquiring public key or certificate for SSL pinning</h1>
<p>
  <span>You can use the "<a href="https://www.openssl.org/source/">openssl</a>" command line utility to get this information.</span>
</p>
<h2 id="h_01HEHTTDPAS4D3X2T8SWKVHMR8">
  <span>Acquiring the SSL public key from a server</span>
</h2>
<p>
  <span>To get the current public key from your server you can use the following snippet (replace xxx.server.ly with your server name):</span>
</p>
<pre><code lang="bash">#get the public key
openssl s_client -connect xxx.server.ly:443 | openssl x509 -pubkey -noout
</code></pre>
<p>That command would produce output similar to the following:</p>
<pre><code lang="bash">depth=2 C = CC, O = XXX Server Service, CN = X1 Z1
verify return:1
depth=1 C = CC, O = XXX Server Service, CN = Y2 Z34
verify return:1
depth=0 CN = *.xxx.server.ly
verify return:1
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAqBv1G1nbGTlZa5ARZYSy
x+ZfVZLaWJlHrIm8crPjj6X/LXfPj/K/bBeVwB2VrpEfLr/vJsv4AC3Dp+YZzchv
zOQUBIiJW0xZ3DXaV9arok9vUk1Srdphr6AO8gixS8Hv7Jnd6B+GszZxtE1tTxjg
5mzm67V1gg0dKSEKEvX49YdVsjj6HKSzqK8J1GS/gllgUuACZMMtxi3L9eBtOkZZ
ihgtHLuL5kf6i5sKb0nZUvCh5cxInNnDE3NohzHacC0p8Uah4WvnJ6nNLFD76xYG
fEn98nqOp9Lw+T4UWuH9A5D+uR4L/6rcHvNvqGlgKX0uZkKuyZnhVdjXeunQzwmX
UwIDAQAB
-----END PUBLIC KEY-----
</code></pre>
<p>
  <span>The public key for <code>xxx.server.ly</code> is returned in the pem format, its bytes are between the <code>-----BEGIN PUBLIC KEY-----</code> and</span><code style="font-size: 15px;">-----END PUBLIC KEY-----</code>
  tags. You would not copy the tags and just the characters between them when providing
  this information to the SDK. Remember to not add any newlines when providing
  this to the SDK.
</p>
<h2 id="h_01HEHTTDPAS4D3X2T8SWKVHMR8">
  <span>Acquiring the SSL certificate information from a server</span>
</h2>
<p>
  <span>To get the whole certificate from your server you can use the following snippets (replace xxx.server.ly with your server name):</span>
</p>
<pre><code lang="bash">#get the list of certificates
openssl s_client -connect xxx.server.ly:443 -showcerts
</code></pre>
<p>
  The command would produce output similar to the following (for improving readability,
  the certificate related bytes are cut short):
</p>
<pre><code lang="bash">CONNECTED(00000003)
depth=2 O = Digital Signature Trust Co., CN = DST Root CA X3
verify return:1
depth=1 C = US, O = Let's Encrypt, CN = Let's Encrypt Authority X3
verify return:1
depth=0 CN = xxx.server.ly
verify return:1
---
Certificate chain
 0 s:/CN=xxx.server.ly
   i:/C=US/O=Let's Encrypt/CN=Let's Encrypt Authority X3
-----BEGIN CERTIFICATE-----
MIIEKDCCAxCgAwIBAgISA+z3u2fRWjX3pN/gVx3hU69zMA0GCSqGSIb3DQEBCwUA
MEoxCzAJBgNVBAYTAlVTMRYwFAYDVQQKEw1MZXQncyBFbm...
-----END CERTIFICATE-----
 1 s:/C=US/O=Let's Encrypt/CN=Let's Encrypt Authority X3
   i:/O=Digital Signature Trust Co./CN=DST Root CA X3
-----BEGIN CERTIFICATE-----
MIIDdzCCAl+gAwIBAgIQAqxcJmoA5OoRVjRk4VSSbzAN...
-----END CERTIFICATE-----
---
Server certificate
subject=/CN=xxx.server.ly
issuer=/C=US/O=Let's Encrypt/CN=Let's Encrypt Authority X3
---
No client certificate CA names sent
Peer signing digest: SHA256
Server Temp Key: ECDH, P-256, 256 bits
---
SSL handshake has read 3072 bytes and written 460 bytes
---
New, TLSv1/SSLv3, Cipher is ECDHE-RSA-AES256-GCM-SHA384
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES256-GCM-SHA384
    Session-ID: B049D3E8126B5421704F7F793EBF78E2B595A7B4820341F169F5C394D177697A4
    Session-ID-ctx:
    Master-Key: 05F08C1C9B9E5EDC01A3A51DA3B656E715E1173186C3167EDC758BFBB7603A80
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    Start Time: 1642277969
    Timeout   : 7200 (sec)
    Verify return code: 0 (ok)
---
</code></pre>
<p>
  <span>The produced output would contain information about multiple certificates, it shows the certificate chain of trust to the respective root certificate authority. The specific certificate information for your server would be at the top and that is the one you would need to copy.</span>
</p>
<p>
  <span>You would copy the string/bytes between the first <code lang="bash">---BEGIN CERTIFICATE---</code> and <code lang="bash">-----END CERTIFICATE-----</code> tags and paste them to init block of the SDK that you are using. Remember to not add any newlines when providing this to the SDK.</span>
</p>
<h1 id="h_01HDNJK8PAE5GEQWRFDS4KD6S6">Common SSL certificate problems</h1>
<p>
  <span>Problems might be encountered related to SSL or certificate exceptions. <a href="https://developer.android.com/privacy-and-security/security-ssl">Here</a> is a list of common reasons for issues in Android.</span><span></span>
</p>
<p>
  Sometimes a good way of exploring the cause of the problem is the same openssl
  certificate command:
</p>
<pre><code lang="bash">openssl s_client -connect xxx.server.ly:443 -showcerts</code></pre>
<p>Example output might look like this:</p>
<pre><code lang="bash">0056931101000000:error:10080002:BIO routines:BIO_lookup_ex:system lib:crypto/bio/bio_addr.c:738:nodename nor servname provided, or not known
connect:errno=0</code></pre>
<p>Its error codes may lead to a solution.</p>
<p>
  A common issue, which can be encountered is that the server's certificate does
  not contain the full chain of trust in it and it shows only 1 entry. In such
  cases,
  <a href="https://serverfault.com/questions/875297/verify-return-code-21-unable-to-verify-the-first-certificate-lets-encrypt-apa" target="_blank" rel="noopener">this</a>&nbsp;may
  be helpful.
</p>
<h1 id="h_01HDZY2VYR54AX1CZKP46A98EJ">Tracking Events in a WebView</h1>
<p>
  Incase you are using a WebView in your application, you can establish communication
  between the WebView and the native application. This will allow you to send data
  from the WebView to the native application and vice versa.
</p>
<p>
  This can be used to track information that happens inside the WebView and send
  it to the native application. For example, if you have a WebView that is used
  to display a web page, you can track the page views inside the WebView and send
  them to the native application. The native application can then send this information
  to Countly.
</p>
<h2 id="h_01HE01VEM5PTGQFQBKG1WHE8KP">Tracking from Host or Child</h2>
<p>
  There are two scenarios which can shape the nature of this communication:
</p>
<p>
  The first is when you want to track everything from the SDK running in the native
  application. In this case, the WebView would be sending information(events) to
  the native application and the native application would be using this information
  to send events.
</p>
<p>
  The second scenario is when you want to track events happening inside the WebView
  from an SDK running inside the web app on that view. In this case, the native
  application would send the current device ID to the WebView and the WebView would
  use this device ID to send events directly to the server. In this scenario if
  session tracking is desired it should only be done in the native application.
</p>
<p>
  Here we will demonstrate two methods to establish communication between the WebView
  and the native application. Each for different platforms and scenarios mentioned
  above.
</p>
<h2 id="h_01HE01VEM5HHNMVD0P9VNHMNZD">Tracking Depending on the Native Platform</h2>
<h3 id="h_01HDZY2VYRXV4301CSARPRFPZP">Android</h3>
<h4 id="h_01HEA8VVYTFHXHE7K8VZ6CTVWT">Tracking Events from the WebView</h4>
<p>
  To track events happening inside the web app, that the user is interacting with
  through the WebView, with the SDK running on that web app (it is assumed to be
  Web SDK here) you would need to send device ID of the user to that SDK from the
  native app and you would need to modify the init configuration of the SDK running
  on that web app.&nbsp;
</p>
<p>
  Assuming you have already created a WebView in your native application, next
  you would need to enable the JavaScript and local storage access on that WebView:
</p>
<div>
  <pre><span>// for example<br>private WebView webView;<br>webView </span>= findViewById(<span>R</span>.<span>id</span>.<span>webview</span>)<span>;<br></span><span>WebSettings webSettings </span>= <span>webView</span>.getSettings()<span>;<br></span><span>webSettings</span>.setJavaScriptEnabled(<span>true</span>)<span>; // Enable JS<br>webSettings.setDomStorageEnabled(true); // Enable local storage access<br></span><span>webView</span>.setWebViewClient(<span>new </span>WebViewClient())<span>;</span></pre>
</div>
<p>
  Then you would need to load the URL of the web app by adding device ID to the
  search query:
</p>
<div>
  <pre><span>String deviceID </span>= <span>Countly</span>.<span>sharedInstance</span>().deviceId().getID()<span>; // get device ID<br></span><span>webView</span>.loadUrl(<span>"https://your.web.app.address?cly_device_id=" </span>+ <span>deviceID</span>)<span>;</span></pre>
</div>
<p>
  This way when the SDK is initialized inside the WebView it would use the device
  ID you provided. During the initialization of the SDK of your web app you would
  need to set 'clear_stored_id' to true or set the 'storage' to 'none':
</p>
<div>
  <pre><span>Countly</span><span>.</span><span>init</span><span>({</span><br><span> &nbsp; </span><span>app_key</span><span>: </span><span>"YOUR_APP_KEY"</span><span>,</span><br><span> &nbsp; </span><span>url</span><span>: </span><span>"https://xxx.count.ly"</span><span>,</span><br><span> &nbsp; </span><span>clear_stored_id</span><span>: </span><span>true</span><span>,<br></span>   // OR you can use:<br><span> &nbsp; </span><span>// storage: "none"</span><br><span>});</span></pre>
</div>
<p id="h_01HEA9PTY20MT5R1TE5XF0YVD2">
  From this point on all events you send with the web SDK on that web app would
  be registered for the same user that was using the native app. A key point here
  is to not track sessions with the Web SDK if you are already tracking it at the
  native app.
</p>
<h4 id="h_01HE01VEM5C8W6S7JDQ0EP2SB1">Tracking Events from the Native App</h4>
<p>
  There are three things that need to be done to establish communication between
  the WebView and the native application on Android:
</p>
<ul>
  <li>To enable JavaScript in the WebView</li>
  <li>
    Add a JavaScript Interface that expects a message (and sends an event with
    it)
  </li>
  <li>
    Use the method that sends a message to native side at the web app
  </li>
</ul>
<p>
  Here is an example of how to send events from WebView to the native application
  assuming you have set a WebView:
</p>
<pre><span>// for example you have set up a WebView like this<br>private WebView webView;<br></span>webView = findViewById(R.id.webview);<br>WebSettings webSettings = webView.getSettings();<br>webSettings.setJavaScriptEnabled(true); // Enable JS here<br>webSettings.setDomStorageEnabled(true);<br>webView.addJavascriptInterface(new JSBridge(), "JSBridge"); // Add JS Interface<br>webView.setWebViewClient(new WebViewClient());</pre>
<p>
  We will need a class where we define the method we will use to send a message
  from web app:
</p>
<div>
  <pre><span>// Define the class we will add with JS Interface<br>class </span><span>JSBridge </span>{<br>    <span>@JavascriptInterface<br></span><span>    </span><span>public void </span><span>communicate</span>(<span>String key</span>) { // method that will get message <br><span>        </span><span>Countly</span>.<span>sharedInstance</span>().events().recordEvent(<span>key</span>)<span>; // record an event with message<br></span><span>    </span>}<br>}</pre>
</div>
<p>
  Then on the WebView side, you can send messages to the native application using
  the method we created in our class at native side. Here is an example of how
  to do this:
</p>
<pre>// create a function that uses the JSBridge we have declared at native side<br>function sendMessage(message) {<br>  JSBridge.<span>communicate</span>(message);<br>}</pre>
<p>
  Calling this method with a message you provide would result in that message to
  be used as a key of an event and recorded at the native side by the SDK running
  there.
</p>
<h3 id="h_01HE01VEM6H1VRDJNDHJ0A2Z1K">iOS</h3>
<h4 id="01HEAAX5QBHWXE0ES9Y9NMH4GZ">Tracking Events from the WebView</h4>
<p>
  To track events inside the WebView the only thing you need to do at the native
  side is to pass the device ID of the user:
</p>
<pre><code>// Lets assume you have a WebView like this
import UIKit
import WebKit
class ViewController: UIViewController, WKUIDelegate, WKScriptMessageHandler {
  var webView: WKWebView!<br>
  override func loadView() {
    let webConfiguration = WKWebViewConfiguration()
    webView = WKWebView(frame: .zero, configuration: webConfiguration)
    webView.configuration.preferences.javaScriptEnabled = true
    webView.uiDelegate = self
    view = webView
  }
  override func viewDidLoad() {
    super.viewDidLoad()<br>    <br>    // get device ID
    let id = <span class="hljs-selector-tag">Countly</span><span class="hljs-selector-class">.sharedInstance</span><span>()</span><span class="hljs-selector-class">.deviceID</span><span>()</span><br>    <br>    // your web app url + device ID
    let myURL = URL(string:"https://your.app.url?cly_devide_id=" + id)
    let myRequest = URLRequest(url: myURL!)
    webView.load(myRequest)
  }
}</code></pre>
<p>At your web app initialize the SDK like this:</p>
<pre><code>// Making sure that SDK does not try to use the device ID from storage
<span>Countly</span><span>.</span><span>init</span><span>({</span><br><span> &nbsp; </span><span>app_key</span><span>: </span><span>"YOUR_APP_KEY"</span><span>,</span><br><span> &nbsp; </span><span>url</span><span>: </span><span>"https://xxx.count.ly"</span><span>,</span><br><span> &nbsp; </span><span>clear_stored_id</span><span>: </span><span>true</span><span>,<br></span>   // OR you can use:<br><span> &nbsp; </span><span>// storage: "none"</span><br><span>});</span>
</code></pre>
<p>
  Now you can use the SDK inside the web app as normal and all events would be
  registered under the user from the native app. Session tracking should not be
  enabled inside the web app if it was enabled at the native side.
</p>
<h4 id="01HEAAXF77XNR21YXRT9FF2FZ6">Tracking Events from the Native App</h4>
<p>
  To track events from your native app you can use a simple userContentController
  and pass a message from the WebView which then you can use for sending events
  or more:
</p>
<pre><code>// Lets assume you have a WebView like this
import UIKit
import WebKit
class ViewController: UIViewController, WKUIDelegate, WKScriptMessageHandler {
  <br>  // Controller logic here
  func userContentController(_ userContentController: WKUserContentController, didReceive message: WKScriptMessage) {
    // You can create an event with message from JS side here
    print(message.body)<br>    <span class="hljs-selector-tag">Countly</span><span class="hljs-selector-class">.sharedInstance</span><span>()</span><span class="hljs-selector-class">.recordEvent</span><span>(message.body</span><span>)</span>
  }<br>
  var webView: WKWebView!
  var webHandler: String = "jsHandler" // handler name. We will use this at WebView<br>
  override func loadView() {
    let webConfiguration = WKWebViewConfiguration()
    webView = WKWebView(frame: .zero, configuration: webConfiguration)
    webView.configuration.preferences.javaScriptEnabled = true
    
    // Assign controller here
    let contentController = WKUserContentController()
    webView.configuration.userContentController = contentController
    webView.configuration.userContentController.add(self, name: webHandler)
  
    webView.uiDelegate = self
    view = webView
  }
  override func viewDidLoad() {
    super.viewDidLoad()
    let myURL = URL(string:"https://your.app.url") // your web app url
    let myRequest = URLRequest(url: myURL!)
    webView.load(myRequest)
  }
}</code></pre>
<p>At your web app create a function like this:</p>
<pre><code>// You can call this function inside your web app to send a message to your native app
function sendMessage(param) {
  try {
    window.webkit.messageHandlers.jsHandler.postMessage(param); // we send message here
  } catch (error) {
    // log or sth else
  }
}
</code></pre>
<h1 id="h_01HEADFCRX3BVR8QZNKQZY3B0T">Using Web SDK inside a Flutter Web App</h1>
<p>
  One of the ways to execute JavaScript in Dart is to use Dart:js library (another
  way would be to use its superset, the 'js' library). Using this library you can
  use the Countly methods inside your Dart code. However it depends on you defining
  the functions you will use before hand. So an example strategy to use Web SDK
  inside a Flutter Web App would go through these steps:
</p>
<ul>
  <li>Add a new '.js' file in 'web' folder of your project</li>
  <li>Inside that file set some methods to call later:</li>
</ul>
<div>
  <pre><span>// lets say inside the my_methods.js file you have created<br>function</span><span> </span><span>sendEvent</span><span>(</span><span>key</span><span>) {</span><br><span>  &nbsp; </span><span>Countly</span><span>.</span><span>add_event</span><span>({key: key</span><span>});</span><br><span>}</span></pre>
</div>
<ul>
  <li>
    At the 'head' tag of index.html add this file and Countly script as a source:
  </li>
</ul>
<pre>&lt;script type='text/javascript' src='https://cdn.jsdelivr.net/npm/countly-sdk-web@latest/lib/countly.min.js' defer&gt;&lt;/script&gt;<br>&lt;script src="<span>my_methods.js</span>" defer&gt;&lt;/script&gt;<br>&lt;body&gt;<br>&lt;script&gt;<br>// ... Flutter related code here<br><br>// initialize Countly<br><span>Countly</span><span>.</span><span>init</span><span>({</span><br><span> &nbsp; </span><span>app_key</span><span>: </span><span>"YOUR_APP_KEY"</span><span>,</span><br><span> &nbsp; </span><span>url</span><span>: </span><span>"https://xxx.count.ly"</span><br><span>});</span><br>&lt;/script&gt;<br>&lt;/body&gt;</pre>
<ul>
  <li>Now in flutter import dart:js</li>
  <li>
    And use js.context.callMethod('method_name',['args']) to call those methods:
  </li>
</ul>
<pre>import 'dart:js' as js; // import the library<br><br>// ... your other code here<br><br>// lets say you have a button that triggers this function:<br>void webEvent() {<br>   js.context.callMethod('sendEvent',['some_key']); // call the method from <span>my_methods.js</span><br>}</pre>
<p>
  Now you should be able to send an event with a key you want in your code. You
  can change things according to your own project inspiring from these basic principles.
</p>
<h1 id="h_01HJ5MD0WB97PA9Z04NG2G0AKC">What Information Is Collected by the SDKs</h1>
<p>
  <span>The following description mentions data that is collected by SDK's to perform their functions and implement the required features. Before any of it is sent to the server, it is stored locally.</span>
</p>
<h2 id="h_01HJ5NDP00ATX2WXQAN1MJCCS1">
  <span>Parameters Sent With Every Request</span>
</h2>
<p>
  <span>When sending any network requests to the server, the following informations are sent in addition of the main data</span><span></span>
</p>
<table style="border-collapse: collapse; height: 220px; width: 100%; margin-right: auto; margin-left: auto;" border="1">
  <tbody>
    <tr style="height: 22px;">
      <th style="width: 25%; text-align: left; vertical-align: middle; height: 22px; border-right: solid 1px; padding-left: 10px;" scope="colGroup">Parameter Name</th>
      <th style="width: 75%; text-align: left; vertical-align: middle; height: 22px; padding-left: 10px;" scope="colGroup">Description</th>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">timestamp</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>timestamp that request is created at</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">hour</td>
      <td style="width: 25%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>hour that request is created at</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">tz</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>timezone of the request that is created on</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">dow</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>day of the week that request is created at (For Countly, the week commences on Sunday, designated as index 0)</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">sdk_version</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>version of the SDK that request is created from</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">sdk_name</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>name of the SDK that request is created from</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">app_key</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>key for the app that is sending the request</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">device_id</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>unique device identifier that request is created for</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">av</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>application version if it is provided</span>
      </td>
    </tr>
  </tbody>
</table>
<p>&nbsp;</p>
<p>
  <span>Here is an example of a base request. To visualize things better it is URL decoded. When sending, data has to be URL encoded</span>
</p>
<pre><span>https://xxx.server.ly/i?timestamp=1703164988058&amp;hour=14&amp;tz=180&amp;dow=4&amp;sdk_version=23.12.0&amp;sdk_name=CountlySDK&amp;app_key=APP_KEY&amp;device_id=DEVICE_ID&amp;av=1.0.0&amp;rr=0</span></pre>
<h2 id="01HJ678RSDEGG93FK2RS9RS0GW">
  <span>Parameters Specific to Certain Requests</span>
</h2>
<p>
  <span>Depending on the request prepared, some additional information might be added to make a deeper analysis. Those additional informations are specific informations related to device/sdk/platform that are reachable.</span>
</p>
<h3 id="h_01HJ5PA5GMQSE8ATC3FJ6VAGP3">Common Metrics</h3>
<p>
  Those additional informations are needed for Session, Crash Reporting and Remote
  Config requests. These are the common collected device metrics i<span>f they are available for the specific device/sdk/platform.</span>
</p>
<table style="border-collapse: collapse; height: 220px; width: 100%; margin-right: auto; margin-left: auto;" border="1">
  <tbody>
    <tr style="height: 22px;">
      <th style="width: 25%; text-align: left; padding-left: 10px; vertical-align: middle; height: 22px; border-right: solid 1px;" scope="colGroup">Parameter Name</th>
      <th style="width: 75%; text-align: left; padding-left: 10px; vertical-align: middle; height: 22px;" scope="colGroup">Description</th>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_device</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>name of the device</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_os</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>device OS</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_os_version</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>device OS version</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_resolution</td>
      <td style="width: 25%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>resolution of the device/application</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_app_version</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>application version</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_manufacturer</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">device manufacturer</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_carrier</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">device carrier if extractable by the SDK</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_orientation</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">device orientation if exists</td>
    </tr>
  </tbody>
</table>
<p>&nbsp;</p>
<h3 id="h_01HJ5QCQ99BYBMTZCSN5S3TSEV">Session Specific Metrics</h3>
<p>
  The following metrics are additional to the common metrics that sent with every
  begin session request.
</p>
<table style="border-collapse: collapse; height: 98px; width: 100%; margin-right: auto; margin-left: auto;" border="1">
  <tbody>
    <tr style="height: 22px;">
      <th style="width: 25%; text-align: left; padding-left: 10px; vertical-align: middle; height: 22px; border-right: solid 1px;" scope="colGroup">Parameter Name</th>
      <th style="width: 75%; text-align: left; padding-left: 10px; vertical-align: middle; height: 22px;" scope="colGroup">Description</th>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_locale</td>
      <td style="width: 75%; height: 10px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>locale of the device</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_density</td>
      <td style="width: 75%; height: 10px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">
        <span>density of the screen</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_device_type</td>
      <td style="width: 75%; height: 10px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">device type</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_store</td>
      <td style="width: 75%; height: 10px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">package name or store name if collected by the SDK</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_ua</td>
      <td style="width: 75%; height: 10px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">User agent (Only used by the Web SDK)</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_browser</td>
      <td style="width: 75%; height: 10px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">Browser name (Only used by the Web SDK)</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_browser_version</td>
      <td style="width: 75%; height: 10px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">Browser version (Only used by the Web SDK)</td>
    </tr>
  </tbody>
</table>
<p>&nbsp;</p>
<p>
  Here is an example of session begin request. This is URL decoded, when sending,
  data has to be URL encoded
</p>
<pre><span>https://xxx.server.ly/i?timestamp=1703164988058&amp;hour=14&amp;tz=180&amp;dow=4&amp;sdk_version=23.12.0&amp;sdk_name=CountlySDK&amp;app_key=APP_KEY&amp;device_id=DEVICE_ID&amp;av=1.0.0&amp;rr=0&amp;end_session=1&amp;session_duration=35&amp;metrics=<br>{"_device": "CountlyDevice",<br>"_os": "MacOS",<br>"_os_version": "1.0.0",<br>"_resolution": "1080x1080",<br>"_app_version": "1.0.0",<br>"_manufacturer": "Countly",<br>"_carrier": "Countly-Mobile",<br>"_density": "XXHDPI",<br>"_locale": "en_US",<br>"_device_type": "web",<br>"_store": "ly.count.sdk",<br>"_orientation": "Horizontal",<br>"_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X x.y; rv:42.0) Gecko/20100101 Firefox/42.0",<br>"_browser": "Firefox",<br>"_browser_version": "42.0"<br>}</span><span></span><span></span></pre>
<h3 id="h_01HJ5V4WX0XFP7FC8ETDC3B96M">Crash Specific Metrics</h3>
<p>
  These metrics are automatically collected when a crash is reported manually or
  automatically
</p>
<table style="border-collapse: collapse; height: 220px; width: 100%; margin-right: auto; margin-left: auto;" border="1">
  <tbody>
    <tr style="height: 22px;">
      <th style="width: 25%; text-align: left; padding-left: 10px; vertical-align: middle; height: 22px; border-right: solid 1px;" scope="colGroup">Parameter Name</th>
      <th style="width: 75%; text-align: left; padding-left: 10px; vertical-align: middle; height: 22px;" scope="colGroup">Description</th>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_cpu</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">CPU information of the device</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_opengl</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">OpenGL information if exists</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_root</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">Device root information if exists</td>
    </tr>
    <tr>
      <td style="width: 25%; vertical-align: middle; text-align: left; padding-left: 10px; border-right: solid 1px;">_ram_total</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">Total RAM of the device</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_ram_current</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">Current RAM of the device</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_disk_current</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">Current disk of the device</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_bat</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">Battery level of the device if exists</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_run</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">Running time of the SDK</td>
    </tr>
    <tr>
      <td style="width: 25%; vertical-align: middle; text-align: left; padding-left: 10px; border-right: solid 1px;">_architecture</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">CPU architecture if collected by the SDK</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_online</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">Device online status if collected by the SDK</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_muted</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">Device muted status if collected by the SDK</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_background</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">Application in background status if collected by the SDK</td>
    </tr>
    <tr>
      <td style="width: 25%; vertical-align: middle; text-align: left; padding-left: 10px; border-right: solid 1px;">_executable_name</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">Executable name (Only used by the iOS SDK)</td>
    </tr>
    <tr>
      <td style="width: 25%; vertical-align: middle; text-align: left; padding-left: 10px; border-right: solid 1px;">_build_uuid</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">Build UUID (Only used by the iOS SDK)</td>
    </tr>
    <tr>
      <td style="width: 25%; vertical-align: middle; text-align: left; padding-left: 10px; border-right: solid 1px;">_app_build</td>
      <td style="width: 75%; height: 22px; vertical-align: middle; text-align: left; padding-left: 10px;" scope="colGroup">App build version (Only used by the iOS SDK)</td>
    </tr>
  </tbody>
</table>
<p>&nbsp;</p>
<h3 id="h_01HJ5WD48B7TVTNP7TFY0646MK">Crash Data</h3>
<p>
  These parameters are automatically collected when a crash is reported manually
  or automatically
</p>
<table style="border-collapse: collapse; height: 174px; width: 100%; margin-right: auto; margin-left: auto;" border="1">
  <tbody>
    <tr style="height: 22px;">
      <th style="width: 25%; vertical-align: middle; height: 22px; border-right: solid 1px; padding-left: 10px; text-align: left;" scope="colGroup">Parameter Name</th>
      <th style="width: 75%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px;">Description</th>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_error</td>
      <td style="width: 75%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px;">
        <span>error description</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_nonfatal</td>
      <td style="width: 75%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px;">
        <span>whether crash is fatal or not</span>
      </td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_logs</td>
      <td style="width: 75%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px;">breadcrumbs if given</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_type</td>
      <td style="width: 75%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px;">type of the crash if given</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_name</td>
      <td style="width: 75%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px;">name of the crash if given</td>
    </tr>
    <tr style="height: 22px;">
      <td style="width: 25%; vertical-align: middle; height: 22px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_native_cpp</td>
      <td style="width: 75%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px;">true if it is a native crash (Only used by the Android SDK)</td>
    </tr>
    <tr style="height: 10px;">
      <td style="width: 25%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px; border-right: solid 1px;" scope="colGroup">_plcrash</td>
      <td style="width: 75%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px;">
        true if PL Crash Reporter enabled (Only used by the iOS SDK)
      </td>
    </tr>
    <tr style="height: 10px;">
      <td style="width: 25%; vertical-align: middle; text-align: left; padding-left: 10px; height: 10px; border-right: solid 1px;" scope="colGroup">_binary_images</td>
      <td style="width: 75%; vertical-align: middle; height: 10px; text-align: left; padding-left: 10px;">binary stack trace (iOS SDK)</td>
    </tr>
  </tbody>
</table>
<p>&nbsp;</p>
<p>Here is an example crash request:</p>
<pre><span>https://xxx.server.ly/i?timestamp=1703164988058&amp;hour=14&amp;tz=180&amp;dow=4&amp;sdk_version=23.12.0&amp;sdk_name=CountlySDK&amp;app_key=APP_KEY&amp;device_id=DEVICE_ID&amp;av=1.0.0&amp;rr=0&amp;crash={<br></span>"_device":"Android SDK built for x86",<br>"_os":"Android",<br>"_os_version":"10",<br>"_resolution":"1080x2088",<br>"_app_version":"1.0.0",<br>"_manufacturer":"Google",<br>"_orientation":"Portrait",<br>"_carrier": "C-Mobile",<br>"_cpu":"x86",<br>"_opengl":"2",<br>"_root":"false",<br>"_ram_total":"1994",<br>"_ram_current":"213",<br>"_disk_total":"2162",<br>"_disk_current":"32",<br>"_bat":"100.0",<br>"_run":"6",<br>"_architecture":"arch",<br>"_online":"true",<br>"_muted":"false",<br>"_background":"false",<br>"_executable_name":"name",<br>"_build_uuid":"uuid",<br>"_app_build":"1.0",<br>"_error":"java.lang.Exception: RangeError (index): Invalid value: Not in inclusive range 0..2: 10\n\tat ly.count.dart.countly_flutter.CountlyFlutterPlugin.onMethodCall(CountlyFlutterPlugin.java:340)\n\tat io.flutter.plugin.common.MethodChannel$IncomingMethodCallHandler.onMessage(MethodChannel.java:8)\n\tat io.flutter.embedding.engine.dart.DartMessenger.invokeHandler(DartMessenger.java:295)\n\tat io.flutter.embedding.engine.dart.DartMessenger.lambda$dispatchMessageToQueue$0$io-flutter-embedding-engine-dart-DartMessenger(DartMessenger.java:322)\n\tat io.flutter.embedding.engine.dart.DartMessenger$$ExternalSyntheticLambda0.run(Unknown Source:12)\n\tat android.os.Handler.handleCallback(Handler.java:883)\n\tat android.os.Handler.dispatchMessage(Handler.java:100)\n\tat android.os.Looper.loop(Looper.java:214)\n\tat android.app.ActivityThread.main(ActivityThread.java:7356)\n\tat java.lang.reflect.Method.invoke(Native Method)\n\tat com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:492)\n\tat com.android.internal.os.ZygoteInit.main(ZygoteInit.java:930)\n",<br>"_nonfatal":"false"<br>"_logs":"logs",<br>"_type":"crash",<br>"_name":"error",<br>"_native_cpp":"true",<br>"_plcrash":"plcrash",<br>"_binary_images":"110001101"<br>}</pre>
<h2 id="h_01HJ5XRSX13YGV6FBBXKVRGRZC">Device ID Sources</h2>
<p>
  By default all of the Countly SDKs uses their implementation of device id generation
  method if no developer supplied custom id is given during initialization. Here
  are the device id generation methods for each SDK:
</p>
<p>
  - The Android SDK uses Secure.ANDROID_ID as the default ID and advertising id
  as a fallback devices ID
</p>
<p>- The iOS SDK uses:</p>
<ul>
  <li>
    On iOS and tvOS, default device ID is Identifier For Vendor (IDFV).
  </li>
  <li>
    On watchOS and macOS, default device ID is a persistently stored random NSUUID
    string.
  </li>
</ul>
<p>- The Windows SDK uses:</p>
<ul>
  <li>
    <strong>cpuId</strong> - [net35, net45] (we recommend against using this)
    uses the OS-provided CPU id info to generate a hash that is used as an id.
    It should be possible to generate the same id on a reinstall if the CPU stays
    the same. On virtual machines and Windows 10 devices are not guaranteed to
    be unique and generate the same id and therefore device id conflicts.
  </li>
  <li>
    <strong>multipleWindowsFields</strong> - [net35, net45] uses multiple OS-provided
    fields (CPU id, disk serial number, windows serial number, windows username,
    mac address) to generate a hash that would be used as the device Id. This
    method should regenerate the same id on a reinstall, provided those source
    fields do not change.
  </li>
  <li>
    <strong>windowsGUID</strong> - [all platforms] generates a random GUID that
    will be used as a device id. Very high chance of being unique. Will generate
    a new id on a reinstall.
  </li>
</ul>
<p>- The Web SDK generates a random device id</p>
<p>
  - The Unity SDK uses <span>SystemInfo.deviceUniqueIdentifier</span><span></span>
</p>
<p>
  <span>- The Java SDK uses a random UUID</span>
</p>
