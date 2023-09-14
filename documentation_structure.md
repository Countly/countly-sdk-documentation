# Documentation Structure

This file gives information about the documentation structure that each SDK should strive to adhere.

* It outlines the major titles and subtitles
* It shows the order in which the content should be presented
* It clarifies the header tags for titles

## General Rules

All feature sections (h1s in the document) should have:

* an introduction about that feature
* a link to it's relevant 'User Guides' article

### Nomenclature

All bold titles are h1 header tags. Ex: **H1 Title**

Some information about a title or a text that should be added to the documentation but it is not a title is provided inside parentheses. Ex: (information) or (Other things)

All subtitles presented in an orderly fashion. Ex:

**Main Title**

* First Subtitle

  * Second Subtitle

***

This represents:

h1: Main Title

h2: First Subtitle

h3: Second Subtitle

## The Structure

Each SDK document starts with an introductory text that includes:

* the current SDK version and the SDK name
* link to the archived doc page
* minimum platform, langauge requirements, supported platform versions
* SDK repo location
* example app location

***

**Adding the SDK to the Project** 

* (How should that be done, where can the library be found, how is the dependency added to their project)
* other things to note (like what is they should know prior to implementation)

***

**SDK Integration**

This should contain the core integration information about the SDK, including a short MVP setup

* Minimal Setup (mandatory fields and other useful information)
* SDK Logging / Debug Mode (this should mention also where the SDK logs can be found)
* Required App Permissions (if needed)
* Required Callbacks (if needed)
* (Other things if needed)
* Countly Code Generator

***

**Crash Reporting**

* (Intro)
* Automatic Crash Handling (how do we enable it, what needs to be done)
* Handled Exceptions
* Crash Breadcrumbs
* Automatic Crash Report Segmentation
* Crash Filtering
* Consent
* Native C++ Crash Reporting
* (platform specific information regarding crashes)
* Symbolication
  * (Overview)
  * (Symbol extraction)
  * (Automatic upload script)

***

**Events**

* (Intro with event field overview (sum, count, duration, segmentation). Mention allowed data types for segmentation)
* Recording Events
* Timed Events
* Past Events
* Consent

***

**Sessions**

* (Intro)
* Automatic Session Tracking
* Manual Sessions
  * Hybrid Mode
* Consent

***

**View Tracking**

* (Intro)
* Automatic Views (if applicable)(Including info of how the automatic view name is acquired)
  * Automatic View Segmentation
  * Automatic View Exceptions
* Manual View Recording (should include information about manual view segmentation)
  * Auto Stopped Views
  * Regular Views
  * Stopping Views
  * Simultaneous View Tracking
* Global View Segmentation
* Consent

***

**Device ID Management**

* (Intro)
* Retrieving Current Device ID (should include also a way to retrieve the current ID type)
* Changing Device ID  (should describe ways to do it with and without merge)
* Temporary Device ID
* Device ID Generation (should describe all the ways the ID is generated (when no custom id is provided by the dev) and what platform information is used to do that)
* Consent

***

**Push Notifications**

* (Intro)
* Integration (steps required to integrate and setup push for the project)
* Enabling Push (describes how to enable and configure push in the SDK)
* Removing Push and It’s Dependencies
* Customizing Push Messages
* Deep Links
* Rich Media
* Receiving Data Only Notifications
* Handling Push Callbacks
  * Handling ‘onClick’ Events
  * Handling ‘onReceive’ Events
* Consent

***

**User Location**

* (intro of used location values and location tracking)
* Setting Location (during init and after init)
* Disabling Location (during init and after init)
* Consent

***

**Heatmaps**

* (Intro)
* Tracking Clicks
* Tracking Scrolls
* Consent

***

**Remote Config**

* (Intro (slightly note AB testing), small overview of the flow)
* Downloading values
  * Automatic Remote Config Triggers (what they are and how to disable them)
  * Manual Calls
    * (Update “all”)
    * (Update “except keys”)
    * (Update “for keys only”)
* Accessing values (We don't mention the 'GetAndEnroll' call)
* Clearing Stored Values
* Global Download Callbacks (how to register and unregister)
* A/B Testing
  * Enrollment on Download
  * Enrollment on Access (we mention the 'GetAndEnroll' call)
  * Enrollment on Action (the explicit call)
* Consent


* Updating Remote Config
  * Automatic Remote Config Triggers
  * Manual Remote Config
    * (Update “all”)
    * (Update “except keys”)
    * (Update “for keys only”)
* Accessing Remote Config Values
* A/B Testing
* Clearing Stored Values
* Consent

***

**User Feedback**

* Ratings
  * Star Rating Dialog
  * Rating Widget
  * Manual Rating Reporting
* Feedback Widget
  * (NPS)
  * (Surveys)
  * Manual Reporting
* Consent

***

**User Profiles**

* Setting Predefined Values
* Setting Custom Values
* Setting User Picture
  * (picture upload)
  * (setting picture url)
* Modifying Data
* Orientation Tracking
* Consent

***

**Application Performance Monitoring**

* (setup / enabling)
* Custom Traces
* Network Traces
  * (Automatic network traces)
  * (Manual network traces)
* Automatic Device Traces
* App Time in Background / Foreground
* Consent

***

**User Consent**

* (Intro about consent in general)
* Setup During Init
* Changing Consent
* Feature Groups

***

**Security and Privacy**

* Parameter Tamper Protection
* SSL Certificate Pinning
* Using a Self-Signed Server Certificate
* (Tamper protection tools)

***

**Other Features and Notes**

* (Other features, configuration options)
* SDK Config Parameters Explained (should explain all init time SDK parameters)
* SDK Internal Limits
* Setting Event Queue Threshold
* Setting Maximum Request Queue Size
* Checking If the SDK Has Been Initialized
* Attribution
  * Direct Attribution
  * Indirect Attribution
* Forcing HTTP POST
* Custom HTTP Header Values
* Custom Metrics
* Log Listener
* Testing

***

**FAQ**
* What Information is Collected by the SDK
* Where Does the SDK Store the Data (where is it stored and what mechanism is it using)

* What Information Is Collected by the SDK (should mention every user and device related information that is collected by the SDK during its operation. Data should be described at a high granularity so that it can be used for GDPR reports.)
