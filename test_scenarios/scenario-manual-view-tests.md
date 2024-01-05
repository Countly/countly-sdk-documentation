# Scenario test plan for views

**sE_X** - view start event for view name X

**eE_X_Y** - view end event for view name X with duration Y

validation should also check cvid, pvid, peid

## (1XX) Value sanitation, wrong usage, simple tests

### 100_badValues_null

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

### 101_badValues_emptyString

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

### 102_badValues_nonExistingViews

recordView(x2),
startAutoStoppedView(x2),  
startView(x2), 
pauseViewWithID, 
resumeViewWithID,
stopViewWithName(x2),
stopViewWithID(x2), 
addSegmentationToViewWithID,
addSegmentationToViewWithName

These should be called with view names and id's that are not started

nothing should crash, no events should be recorded

## (2XX) Usage flows

### 200_autostartView_autoClose

Make sure auto closing views behave correctly

* recordView view A (sE_A)
* recordView view B (eE_A_0, sE_B)
* start view C (eE_B_0, sE_C)
* startAutoStoppedView D
* startAutoStoppedView E
* start view F
* recordView view G
* startAutoStoppedView H
* recordView view I

### 201_simpleFlowMultipleViews

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

### 202_mixedStartFlow (WIP)

Validate the interaction of "startView" and "startAutoStoppedView". "startAutoStoppedView" should be automatically stopped when calling "startView", but not the other way around

* startView A (sE_A)
* wait 1 sec
* startAutoStoppedView C (sE_C)
* wait 1 sec
* startView B (eE_C_1, sE_B)
* wait 1 sec
* stopViewWithName A (eE_A_3)
* stopViewWithID B (eE_B_1)

### 203_startAutoStoppedView (WIP)

We make sure that "startAutoStoppedView" closes other views started by it

* startAutoStoppedView A
* startAutoStoppedView B

make sure that at this point there are 3 events, 2 starting and 1 closing.

* stopAllViews

This should produce 1 more closing view

### 2XX_segmentationPrecedence

make sure that the segmentation value precedence is taken into account 

## (3XX) Consent

### 300_callingWithNoConsent

recordView(x2),
startAutoStoppedView(x2),  startView(x2), pauseViewWithID, resumeViewWithID,
stopViewWithName(x2), stopViewWithID(x2), 
addSegmentationToViewWithID, addSegmentationToViewWithName,
setGlobalViewSegmentation,
updateGlobalViewSegmentation

calling these with valid values should not cord anything in EQ

### 301_consentRemoved


################

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
