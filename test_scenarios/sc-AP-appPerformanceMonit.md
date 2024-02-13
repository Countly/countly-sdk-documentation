

## AP_200_notEnabledNothingWorking
features not enabled 
'setAppStartTimestampOverride' is set
init the SDK and no requests are recorded

## AP_201_automaticAppStart
app start enabled but not manual trigger
init SDK and request is created. duration bellow 1 sec

automatic trigger should create request after the screen loads
call manual trigger
no additional requests


## AP_202_manualAppStartTrigger_notUsed
app start enabled and manual trigger
init SDK and request is not created

## AP_203_manualAppStartTrigger_correct
app start enabled and manual trigger
init SDK
wait 2 seconds
call trigger and request is created and duration is 2-3 sec

call trigger again, nothing is created


## AP_204_FBTrackingEnabled_working
F/B enabled

init SDK

no requests created
go background
proper request created
go foreground
proper  request created

## AP_205_AppStatOverride_automatic
app start enabled (automatic)
override set (an hour in the past)
init SDK
observe duration

## AP_206_AppStartOverride_manual
app start enabled (manual)
override set (an hour in the past)
init SDK
trigger manual call
observe duration

## AP_207A_enableFBAndStartTimeTracking_manual
app start enabled and manual trigger
foreground, background tracking enabled
init SDK
do manual trigger 
go background, go foreground
validate that all 3 apm requests have been recorded


## AP_207B_enableFBAndStartTimeTracking_manual
This should be done for SDK's that have the legacy method

set the config option that would enable "all" apm features (app start and foreground/background)
init SDK
do manual trigger 
go background, go foreground
validate that all 3 apm requests have been recorded