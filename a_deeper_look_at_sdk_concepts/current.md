<h1>
  <span style="font-weight: 400;">Sessions</span>
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
<h1 align="justify">
  <font face="Arial, serif">Reporting "feature data" manually with events</font>
</h1>
<h2>
  <font face="Arial, serif">Views</font>
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
<h1>
  <font face="Arial, serif">Reporting a feedback widget manually</font>
</h1>
<p>
  This guide will go into the reporting of feedback widgets (<a href="https://support.count.ly/hc/en-us/articles/900003407386-NPS-Net-Promoter-Score-" target="_self">nps</a>,
  <a href="https://support.count.ly/hc/en-us/articles/900004337763-Surveys" target="_self" rel="undefined">surveys</a>
  and
  <a href="https://support.count.ly/hc/en-us/articles/360037641291-Ratings" target="_blank" rel="noopener">ratings</a>)
  manually. It will give more context into how the widget data should be interpreted
  and how the response should be structured when reporting back to the SDK. Also
  it must be noted that not all SDKs contain the functionality to do manual feedback
  widget reporting.&nbsp;
</p>
<p>The SDK should provide 3 calls to perform this process:</p>
<ol>
  <li>A call to fetch the widget list from the server</li>
  <li>A call to fetch a single widget's data from the server</li>
  <li>A call to report a single widget to the server</li>
</ol>
<p>
  Widget list received would be a JSON array of objects corresponding to the widgets.
  By selecting one of these objects (widgets) and providing it in the second call
  developer can fetch its data from the server. When receiving the data, it would
  be packaged in a JSON type object. Their structure would slightly differ depending
  on the type of widget being reported.
</p>
<p>
  In case of a survey, widget data would look something like this:<br>
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
  And incase of a rating widget it would look something like this:
</p>
<pre>{<br>    "_id":"62222d125852e20462481193",<br>    "popup_header_text":"What&amp;#39;s your opinion about this page?",<br>    "popup_comment_callout":"Add comment",<br>    "popup_email_callout":"Contact me via e-mail",<br>    "popup_button_callout":"Submit feedback",<br>    "popup_thanks_message":"Thank you for your feedback",<br>    "trigger_position":"mright",<br>    "trigger_bg_color":"13B94D",<br>    "trigger_font_color":"FFFFFF",<br>    "trigger_button_text":"Feedback",<br>    "target_devices":{<br>        "phone":true,<br>        "desktop":true,<br>        "tablet":true<br>       },<br>    "target_page":"all",<br>    "target_pages":["/"],<br>    "is_active":"true",<br>    "hide_sticker":false,<br>    "app_id":"12345687af5c256b91a6345f",<br>    "contact_enable":"true",<br>    "comment_enable":"true",<br>    "trigger_size":"m",<br>    "type":"rating",<br>    "ratings_texts":[<br>        "Very dissatisfied",<br>        "Somewhat dissatisfied",<br>        "Neither satisfied Nor Dissatisfied",<br>        "Somewhat Satisfied",<br>        "Very Satisfied"<br>       ],<br>    "status":true,<br>    "targeting":null,<br>    "ratingsCount":116,<br>    "ratingsSum":334<br>}</pre>
<p>
  These describe all server side configured information that would be used to visualize
  a widget manually. Starting from some style and color related fields and finally
  all questions and their potential answers. In the case of surveys, it also shows
  the required id's to report survey results.
</p>
<p>&nbsp;</p>
<p>
  When reporting these widget's results manually, the filled out response is reported
  through the segmentation field of the reporting event. So depending on the type
  of widget you are reporting, you have to construct a
  <strong>widgetResult </strong>object, specific to that widget, which would
  then be utilized in the third call that has been mentioned at the top of this
  section. In this third call the developer is expected to provide the widget object
  obtained from the first call, the widget's data object that has been obtained
  from the second call, and a properly formed
  <strong>widgetResult&nbsp;</strong>object that has been created with respect
  to the type of widget that is being reported. More information on how to form
  this object is provided below.
</p>
<h2>Reporting NPS widgets manually</h2>
<p>
  To report the results of an NPS widget manually, no information from the widget's
  data JSON is needed. These widgets can report only two pieces of information
  - an integer <strong>rating,</strong> ranging from 0 to 10, and a String
  <strong>comment</strong>, representing the user's comment.
</p>
<p>
  Therefore when reporting these results, you need to set two segmentation values,
  one with the key of "rating" and an int value and the other with the "comment"
  key and a String value.
</p>
<h3>Android sample code</h3>
<p>
  The following sample code would report the result of an NPS widget:
</p>
<pre><span>Countly</span>.<span>sharedInstance</span>().feedback().getFeedbackWidgetData(chosenWidget, <span>new </span><span>RetrieveFeedbackWidgetData</span>() {<br>    <span>@Override </span><span>public void </span><span>onFinished</span>(<span>JSONObject </span>retrievedWidgetData, <span>String </span>error) {<br>        <span>Map</span>&lt;<span>String</span>, <span>Object</span>&gt; <span>segm </span>= <span>new </span>HashMap&lt;&gt;();<br>        <span>segm</span>.put(<span>"rating"</span>, <span>3</span>);<span>//value from 0 to 10<br></span><span>        </span><span>segm</span>.put(<span>"comment"</span>, <span>"Filled out comment"</span>);<br><br>        <span>Countly</span>.<span>sharedInstance</span>().feedback().reportFeedbackWidgetManually(<span>widgetToReport</span>, retrievedWidgetData, <span>segm</span>);<br>    }<br>});</pre>
<h3>Web sample code</h3>
<p>
  The following code shows what is the expected widgetResult objects looks like
  for NPS widget:
</p>
<pre>var widgetResult = {<br>         rating: 3, // between 0 to 10<br>         comment: "any comment" // string<br>    };</pre>
<h2>Reporting Rating widgets manually</h2>
<p>
  To report the results of a Rating widget manually, again no information from
  the obtained widget data is needed. These widgets has similar reporting capabilities
  to NPS widgets. So similarly there would be an integer
  <strong>rating,</strong> ranging from 1 to 5, and a String
  <strong>comment</strong>, representing the user's comment. Then in addition to
  these there would be an <strong>email</strong> String for user email and a
  <strong>contactMe</strong> Boolean (true or false) if the user gave consent to
  be contacted again or not.
</p>
<h3>Web sample code</h3>
<p>
  The following code shows what is the expected widgetResult objects looks like
  for Rating widget:
</p>
<pre>var widgetResult = {<br>         rating: 3, // between 1 to 5<br>         comment: "any comment", // string<br>         email: "email@any.mail", // string<br>         contactMe: true // boolean<br>    };</pre>
<h2>Reporting Survey widgets manually</h2>
<p>
  To report survey widgets manually, investigation of the widget data received
  from the second call is needed. Each question has a question type and depending
  on the question type, the answer needs to be reported in a different way. Each
  questions also has it's own ID which needs to be used as part of the segmentation
  key when reporting the result.
</p>
<p>
  The questions id can be seen in the "id" field. For example, in the above posted
  survey JSON the first question has the ID of "1611875792-0". When trying to report
  the result for a question,
  <strong>you would append "answ-" to the start of an ID</strong> and then use
  that as segmentation key. For example, for the first survey questions you would
  have the result segmentation key of "answ-1611875792-0".
</p>
<p>
  At the end your widgetResult would look something like this (Web example):
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
  It has the type "multi". In the question description there is a field "choices"
  which describes all valid options and their keys.
</p>
<p>Users can select any combination of all answers.</p>
<p>
  You would prepare the segmentation value by concatenating the keys of the chosen
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
  You would use the chosen options key value as the value for your result segmentation.
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
  You would use the chosen options key value as the value for your result segmentation.
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