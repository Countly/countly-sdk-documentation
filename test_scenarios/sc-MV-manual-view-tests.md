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

### MV_102_badValues_nonExistingViews

pauseViewWithID, 
resumeViewWithID,
stopViewWithName(x2),
stopViewWithID(x2), 
addSegmentationToViewWithID,
addSegmentationToViewWithName

These should be called with view names and id's that are not started

nothing should crash, no events should be recorded

## (2XX) Usage flows

### MV_200A_autostartView_autoClose_legacy

Make sure auto closing views behave correctly
Includes the legacy method "recordView" in its flow

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
(eE_C d=6 id=idv2 pvid=idv8, segm={}) 
(eE_F d=3 id=idv6 pvid=idv8, segm={}) 
(eE_I d=0 id=idv9 pvid=idv8, segm={}) 

### MV_200B_autostartView_autoClose WIP

without the deprecated "recordViewCall"

### MV_201_simpleFlowMultipleViews

Make sure all the basic functions are working correctly and we are keeping time correctly

* start view A (sE_A)
* start view B (sE_B)
* wait 1 sec
* pause view A (eE_A_1)
* wait 1 sec
* resume view A
* stop view with stopViewWithName/stopViewWithID/stopAllViews (eE_1, eE_2)
* Stop view B if needed

make sure the summary time is correct
in total there should be 5 events. validate their values

### MV_202_mixedStartFlow (WIP)

Validate the interaction of "startView" and "startAutoStoppedView". "startAutoStoppedView" should be automatically stopped when calling "startView", but not the other way around

* startView A (sE_A)
* wait 1 sec
* startAutoStoppedView C (sE_C)
* wait 1 sec
* startView B (eE_C_1, sE_B)
* wait 1 sec
* stopViewWithName A (eE_A_3)
* stopViewWithID B (eE_B_1)

### MV_203_startAutoStoppedView (WIP)

We make sure that "startAutoStoppedView" closes other views started by it

* startAutoStoppedView A
* startAutoStoppedView B

make sure that at this point there are 3 events, 2 starting and 1 closing.

* stopAllViews

This should produce 1 more closing view

## (3XX) Consent and other features

### MV_300_callingWithNoConsent

recordView(x2),
startAutoStoppedView(x2),  startView(x2), pauseViewWithID, resumeViewWithID,
stopViewWithName(x2), stopViewWithID(x2), 
addSegmentationToViewWithID, addSegmentationToViewWithName,
setGlobalViewSegmentation,
updateGlobalViewSegmentation

calling these with valid values should not cord anything in EQ

### MV_301_consentRemoved WIP

### MV_310_

session end clears first view

## (4XX) segmentation

### MV_4XX_segmentationPrecedence WIP

make sure that the segmentation value precedence is taken into account 

## (5XX) automatic views WIP

manual calls not working but the global segm calls do

################

start views with the same name

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
