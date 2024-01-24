

## AP_200
features not enabled 
init the SDK and no requests are recorded

## AP_201
app start enabled but not manual trigger
init SDK and request is created. duration bellow 1 sec

call manual trigger
no additional requests

## AP_202
app start enabled and manual trigger
init SDK and request is not created

## AP_203
app start enabled and manual trigger
init SDK
wait 2 seconds
call trigger and request is created and duration is 2-3 sec

call trigger again, nothing is created


## AP_204
F/B enabled

init SDK

no requests created
go background
proper request created
go foreground
proper  request created