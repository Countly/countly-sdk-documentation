# Working test scenarios

# Scenario test plan for views

**sE_X** - view start event for view name X

**eE_X** - view end event for view name X 

validation should check all segmentation values and meta data like: cvid, pvid, peid

duration is marked as "d=X"

all view event segmentation should have the "name" field with the view name and the "segment" field with the platform name (for example, "Android") these 2 will not be explicitly mentioned but should still be validated

if not explicitly mentioned, the duration is 0, the sum is 0, count is 1, ts, dow, hour are also "correct"

when recording views and events, a custom id generator should be used for ID's.
View ids should be returned in the form "idvX" where x is an incrementing number starting from 1
Event ids should be returned in the form "ideX" where x is an incrementing number starting from 1

## (1XX) Value sanitation, wrong usage, simple tests

### MV_100_badValues_null

recordView(x2),
startAutoStoppedView(x2),
startView(x2), 
pauseViewWithID, 
resumeViewWithID,
stopViewWithName(x2), 
stopViewWithID(x2), 
addSegmentationToViewWithID, 
addSegmentationToViewWithName,
setGlobalViewSegmentation,
updateGlobalViewSegmentation

called with "null" values.
versions with and without segmentation.

nothing should crash, no events should be recorded
EQ and RQ should be checked at the start and at the end

### MV_101_badValues_emptyString

recordView(x2),
startAutoStoppedView(x2),
startView(x2), 
pauseViewWithID, 
resumeViewWithID,
stopViewWithName(x2), 
stopViewWithID(x2), 
addSegmentationToViewWithID, 
addSegmentationToViewWithName

called with empty string values

versions with and without segmentation

nothing should crash, no events should be recorded
EQ and RQ should be checked at the start and at the end

### MV_102_badValues_nonExistingViews

pauseViewWithID, 
resumeViewWithID,
stopViewWithName(x2),
stopViewWithID(x2), 
addSegmentationToViewWithID,
addSegmentationToViewWithName

These should be called with view names and id's that are not started

nothing should crash, no events should be recorded
EQ and RQ should be checked at the start and at the end

## (2XX) Usage flows

### MV_200A_autoStoppedView_autoClose_legacy

This should not be implemented by SDK's where the legacy call behaves differently

Make sure auto closing views behave correctly
Includes the legacy method "recordView" in its flow and the new "startAutoStoppedView"
Double calling "recordView" or "startAutoStoppedView" should stop the view.
Calling "start view" should also stop them.

After every action, the EQ should be validated so make sure that the correct event is recorded

* recordView view A 
(sE_A id=idv1 pvid="" segm={visit="1" start="1"})
* wait 1 sec
* recordView view B 
(eE_A d=1 id=idv1 pvid="", segm={}) 
(sE_B id=idv2 pvid=idv1 segm={visit="1"})
* wait 1 sec
* start view C 
(eE_B d=1 id=idv2 pvid=idv1, segm={}) 
(sE_C id=idv3 pvid=idv2 segm={visit="1"})
* wait 1 sec
* startAutoStoppedView D
(sE_D id=idv4 pvid=idv3 segm={visit="1"})
* wait 1 sec
* startAutoStoppedView E 
(eE_D d=1 id=idv4 pvid=idv3, segm={}) 
(sE_E id=idv5 pvid=idv4 segm={visit="1"})
* wait 1 sec
* start view F 
(eE_E d=1 id=idv5 pvid=idv4, segm={}) 
(sE_F id=idv6 pvid=idv5 segm={visit="1"})
* wait 1 sec
* recordView view G
(sE_G id=idv7 pvid=idv6 segm={visit="1"})
* wait 1 sec
* startAutoStoppedView H 
(eE_G d=1 id=idv7 pvid=idv6, segm={}) 
(sE_H id=idv8 pvid=idv7 segm={visit="1"})
* wait 1 sec
* recordView view I 
(eE_H d=1 id=idv8 pvid=idv7, segm={}) 
(sE_I id=idv9 pvid=idv8 segm={visit="1"})
* stopAllViews
(eE_C d=6 id=idv3 pvid=idv8, segm={}) 
(eE_F d=3 id=idv6 pvid=idv8, segm={}) 
(eE_I d=0 id=idv9 pvid=idv8, segm={}) 

### MV_200B_autoStoppedView_autoClose

without the deprecated "recordViewCall"
After every action, the EQ should be validated so make sure that the correct event is recorded

* startAutoStoppedView view A 
(sE_A id=idv1 pvid="" segm={visit="1" start="1"})
* wait 1 sec
* startAutoStoppedView view B 
(eE_A d=1 id=idv1 pvid="", segm={}) 
(sE_B id=idv2 pvid=idv1 segm={visit="1"})
* wait 1 sec
* start view C 
(eE_B d=1 id=idv2 pvid=idv1, segm={}) 
(sE_C id=idv3 pvid=idv2 segm={visit="1"})
* stopAllViews
(eE_X d=0 id=idv3 pvid=idv2, segm={}) 


### MV_201A_autoStopped_pausedResumed_Legacy

* start view A
* startAutoStoppedView B
* wait 1 sec
* pause view B 
* wait 1 sec
* resume view B
* wait 1 sec
* RecordView C
* wait 1 sec
* pause view C 
* wait 1 sec
* resume view C
* stopAllViews 

should record 8 events

### MV_201B_autoStopped_pausedResumed

* start view A 
* start startAutoStoppedView B 
* wait 1 sec
* pause view B 
* wait 1 sec
* resume view B
* stopAllViews 

should record 5 events

### MV_202A_autoStopped_stopped_legacy

* startAutoStoppedView A 
* wait 1 sec
* stop by name
* startAutoStoppedView B 
* wait 1 sec
* stop by ID
* startAutoStoppedView C 
* wait 1 sec
* stopAllViews
* record view D 
* wait 1 sec
* stop by name
* record view E 
* wait 1 sec
* stop by ID
* record view F 
* wait 1 sec
* stopAllViews

should record 12 events

### MV_202B_autoStopped_stopped

* startAutoStoppedView view A 
* wait 1 sec
* stop by name
* startAutoStoppedView view B 
* wait 1 sec
* stop by ID
* startAutoStoppedView view c 
* wait 1 sec
* stopAllViews

should record 6 events

### MV_203_startView_PausedResumed

* start view A 
* wait 1 sec
* pause view A 
* wait 1 sec
* resume view A
* wait 1 sec
* stopAllViews 

3 events

### MV_203_startView_stopped

* start view A 
* wait 1 sec
* stop by name
* start view B 
* wait 1 sec
* stop by ID
* start view c 
* wait 1 sec
* stopAllViews

should record 6 events

## (3XX) Consent and other features

### MV_300A_callingWithNoConsent_legacy

recordView(x2),
startAutoStoppedView(x2), 
startView(x2), 
pauseViewWithID, 
resumeViewWithID,
stopViewWithName(x2),
stopViewWithID(x2), 

calling these with valid values should not record anything in EQ or RQ

### MV_300B_callingWithNoConsent

recordView(x2),
startAutoStoppedView(x2), 
startView(x2), 
pauseViewWithID, 
resumeViewWithID,
stopViewWithName(x2),
stopViewWithID(x2), 

calling these with valid values should not record anything in EQ or RQ

### MV_301_consentRemoved WIP

### MV_310_


A) 310_XXXXXX

B) MV_310


) test_MV_310_consentRemoved

) test_MV_310

=====


A) regularTest.java

   sc_MV_ManualView.java   
   sc_UT_Utils.java

B) scenarios/MV_ManualView.java
   scenarios/UT_Utils.java

   regularTest.java

C) someTests/regularTest.java

   MV_ManualView.java
   UT_Utils.java





SC-MA
SC-MB
SC-MV
SC-UA
SC-UB
SC-UC

session end clears first view


changing device ID stops views and resets first segm

## (4XX) segmentation

### MV_4XX_segmentationPrecedence WIP

make sure that the segmentation value precedence is taken into account 

### MV_401_globalSegmentation

We make sure that "setGlobalSegmentation" and "updateGlobalSegmentation" updates/sets global segmentation

After every action, the EQ should be validated so make sure that the correct event is recorded
For ease here is couple of parameters to be used with this test
MAX_DOUBLE_VALUE=179769313486231570814527423731704356798070567525844996598917476803157260780028538760589558632766878171540458953514382464234321326889464182768467546703537516986049910576551282076245490090389328944075868508455133942304583236903222948165808559332123348274797826204144723168738177180919299881250404026184124858368.0000000000000000
MIN_DOUBLE_VALUE=-179769313486231570814527423731704356798070567525844996598917476803157260780028538760589558632766878171540458953514382464234321326889464182768467546703537516986049910576551282076245490090389328944075868508455133942304583236903222948165808559332123348274797826204144723168738177180919299881250404026184124858368.0000000000000000

Tip: For all of the primitive types; integer, float, long, double usually platforms provide their MAX and MIN values as static parameters. If possible use them to increase readibility.

* initalize the SDK with global view segmentation (segm={int=2147483647 bool=true double=MAX_DOUBLE_VALUE float=-340282346638528859811704183484516925440.0000000000000000 long=9223372036854775807 string="STRING_OF_YOUR_CHOICE" arr=[1, 2, 3]})
* start view A with segm={double=1.1}
(sE_A id=idv1 pvid="" segm={visit="1" start="1" int=2147483647 bool=true double=1.1 float=-340282346638528859811704183484516925440.0000000000000000 long=9223372036854775807 string="STRING_OF_YOUR_CHOICE"})
* setGlobalViewSegmentation (segm={int=2147483647 bool=false double=MIN_DOUBLE_VALUE float=340282346638528859811704183484516925440.0000000000000000 long=9223372036854775807 string="STRING_OF_YOUR_CHOICE2" map=[(key, val), (key1, val1)]})
* wait 1 sec
* pause view A
(eE_A id=idv1 pvid="" d=1.0 segm={int=2147483647 bool=false double=MIN_DOUBLE_VALUE float=340282346638528859811704183484516925440.0000000000000000 long=9223372036854775807 string="STRING_OF_YOUR_CHOICE2"})
* updateGlobalViewSegmentation (segm={int=-2147483648 string="STRING_OF_YOUR_CHOICE3" map=[(key, val), (key1, val1)]})
* start view B with segm={float=1.1}
(sE_B id=idv2 pvid=idv1 segm={visit="1" int=-2147483647 bool=false double=MIN_DOUBLE_VALUE float=1.1 long=9223372036854775807 string="STRING_OF_YOUR_CHOICE3"})
* wait 1 sec
* stopAllViews with segm={bool=true arr=["1", "2", "3"] string1="STRING_OF_YOUR_CHOICE4"}
* validate 2 stop view event is recorded in order of A,B and correct segm values are existed
(eE_A id=idv1 pvid=idv1 d=0.0 segm={int=-2147483647 bool=true double=MIN_DOUBLE_VALUE float=340282346638528859811704183484516925440.0000000000000000 long=9223372036854775807 string="STRING_OF_YOUR_CHOICE3" string1="STRING_OF_YOUR_CHOICE4"})
(eE_B id=idv2 pvid=idv1 d=1.0 segm={int=-2147483647 bool=true double=MIN_DOUBLE_VALUE float=340282346638528859811704183484516925440.0000000000000000 long=9223372036854775807 string="STRING_OF_YOUR_CHOICE3" string1="STRING_OF_YOUR_CHOICE4"})

## (5XX) automatic views WIP

manual calls not working but the global segm calls do

################

start views with the same name


###########

automatic view tracking exceptions

###

## A mixed test flow #2

We also validate the deprecated "recordView". "RecordView" should behave the same as "startAutoStoppedView"

* startView A
* RecordView B
* startAutoStoppedView C

At this point there are 4 events, 3 starting and 1 closing

* stopAllViews

## Make sure we can use view actions with the auto stopped ones

* startAutoStoppedView A
* wait a moment
* pause view
* wait a moment
* resume view
* stop view with stopViewWithName/stopViewWithID

## Validate segmentation

Just make sure the values are used

* SetGlobalSegm at init (2 value)
* startView A

make sure the correct things are added

* update segmentation that updates one of the initial fields and adds another field
* startView B

make sure the correct things are added

* set segmentation

* Stop A with no segmentation

* Stop B with segmentation

again make sure that segmentation is correctly applied

## Validate segmentation 2

* startView A
* startView B
* stopAllViews with segmentation

make sure that the stop segmentation was added to all views

## Validate segmentation 3

Check for value precedence

* set global segm value for key X, value 1
* start view and provide segm with key X, value 2

make sure value 2 is recorded

* start view and provide segm with key X, value 3

make sure value 3 is recorded

# Validate segmentation does not override internal keys

Internal keys: "name", "start", "visit", "segment"

* Set global segm to use internal keys
* Start view and provide segm with internal keys
* Stop view and provide segm with internal keys

make sure that internal keys are not overridden at any point
