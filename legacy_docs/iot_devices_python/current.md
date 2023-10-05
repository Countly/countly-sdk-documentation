<p>
  <span style="font-weight:400">This d</span><span style="font-weight:400">ocumentation shows how to download and use different IoT device SDKs.</span>
</p>
<h1>Installing and Using Countly IoT Raspberry Pi SDK</h1>
<div class="img-container">
  <img src="https://count.ly/images/guide/D3BqDdmmTlORDHzQwXLn_Ekran%20Resmi%202016-02-28%2012.01.20.png" width="471" height="249">
</div>
<p>
  <span style="font-weight:400">The Countly Raspberry Pi SDK is one of the Countly iOT SDK families which sends data to the Countly server. After this SDK sends data to Countly, you may visualize it on the dashboard. The server takes care of both storing data and visualizing it for you, so you can get more insights from your devices.</span>
</p>
<p>
  <span style="font-weight:400">If a device </span><span style="font-weight:400">doesn’t have an internet connection and cannot send data, the SDK stores this data and then sends it to the queue. Items in this queue are then sent one-by-one after an internet connection has been established.</span>
</p>
<p>
  <span style="font-weight:400">You may add your Raspberry Pi Python SDK to your project in two different ways.</span>
</p>
<p>
  <strong>1st method: Getting the code from Github</strong>
</p>
<p>
  <span style="font-weight:400">The command below copies the SDK from Github directly to your computer. It needs the git command to be available on your operating system.</span>
</p>
<pre><code class="shell">git clone https://github.com/Countly/countly-sdk-iot.git .</code></pre>
<p>
  <span style="font-weight:400">Now, you may copy the Countly.py command to your project folder:</span>
</p>
<pre><code class="text">cp raspberry_pi/Raspberry_SDK/Countly.py   your_project_folder
</code></pre>
<p>
  <span style="font-weight:400">In order to import Countly in Python, use this line in your example py file:</span>
</p>
<pre><code class="python">from yourpackage.Countly import Countly
</code></pre>
<p>
  <strong>2nd method: Download using pip, easy Python installer</strong>
</p>
<p>
  <span style="font-weight:400">If you have&nbsp;</span><strong>pip</strong><span style="font-weight:400">&nbsp;command installed on your system, you may run the following command. This easily installs the Countly SDK into your system, so you may directly call it inside your app.</span>
</p>
<pre><code class="shell">pip install Raspberry_SDK
</code></pre>
<p>
  <span style="font-weight:400">In order to use the Countly SDK in your Python app, you may add it as follows:</span>
</p>
<pre><code class="python">from Raspberry_SDK.Countly import Countly
</code></pre>
<h2>Using the Countly IoT Raspberry Pi SDK</h2>
<p>To initiate the SDK without a timer,</p>
<pre><code class="python">countly = Countly("SERVER_URL", "APP_KEY", 0)
</code></pre>
<p>
  <span style="font-weight:400">where server_URL is the IP or name of the server, and APP_KEY is the application key that you retrieved from the dashboard once you create the application.</span>
</p>
<p>
  <span style="font-weight:400">To initiate the timer with a frequency, use the following:</span>
</p>
<pre><code class="python">countly = Countly("SERVER_URL", "APP_KEY", TIMER_SECOND)
</code></pre>
<p>
  <span style="font-weight:400">In order to send a specific event, use this command:</span>
</p>
<pre><code class="text">countly.event(‘EVENT_NAME’, EVENT_VALUE)
</code></pre>
<h2>Example scenario</h2>
<p>
  <span style="font-weight:400">The best method for retrieving data from the Raspberry Pi GPIO is to use the Grove interface. Grove is basically a ready-to-use toolset meant to ease the use of SPI, I2C, UART in analog and digital circuits. Prepared by&nbsp;</span><a href="http://seeedstudio.com/"><span style="font-weight:400">Seeed Studio</span></a><span style="font-weight:400">, it includes several sensors, I/O units, switches, lights, and joysticks.</span>
</p>
<p>
  <span style="font-weight:400">Not only does Grove work with Raspberry Pi, it also works with several industrial, well-known development boards, such as Arduino, Intel Edison, and Beagle Bone Green.&nbsp;</span><span style="font-weight:400">For more information about Grove,&nbsp;</span><a href="http://www.seeedstudio.com/wiki/Grove_System"><span style="font-weight:400">follow this link</span></a><span style="font-weight:400">. To use Grove in Raspberry Pi, a shield-like card called Grove Pi is used.</span>
</p>
<div class="img-container">
  <img src="https://count.ly/images/guide/65KEdFFpTWeZlP34EElC_Ekran%20Resmi%202016-02-28%2012.05.31.png" width="551" height="384">
</div>
<p>
  <span style="font-weight:400">In order to use Grove sensors and the Grove Pi shield, create an account on Countly. An App Key will automatically be created for you. We’ll use this key inside the SDK in places where it is relevant.</span>
</p>
<h3>Raspberry Pi configuration</h3>
<p>
  <span style="font-weight:400">You may find the necessary configuration regarding how to use Python and Grove with Raspberry Pi. We will need this configuration, so start reading and&nbsp;</span><a href="http://www.dexterindustries.com/GrovePi/get-started-with-the-grovepi/"><span style="font-weight:400">implementing what is written here</span></a><span style="font-weight:400">.</span>
</p>
<p>
  <span style="font-weight:400">After installing Grove, you may install the Countly SDK:</span>
</p>
<pre><code class="shell">pip install Raspberry_SDK</code></pre>
<p>
  <span style="font-weight:400">In our example scenario, we have a light sensor. This sensor is connected to the Grove input Analog 0. After configuring the Grove Pi and Grove light sensors, the following code may be used to send light sensor data to the Countly servers:</span>
</p>
<pre><code class="python">import threading
import grovepi 
from raspberry_pi.Raspberry_SDK.Countly import Countly
 
light_sensor = 0
 
countly = Countly("SERVER_URL", "APP_KEY", 0)
 
def grove():
      threading.Timer(30,grove).start()
       countly.event("Light", int(grovepi.analogRead(light_sensor)/10.24))
 
grove()</code></pre>
<p>
  <span style="font-weight:400">You have now finished sending data from Raspberry Pi to your server.</span>
</p>