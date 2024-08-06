## Init options
    M:Manual Sessions enabled
    A:Automatic sessions enabled
    H:Hybrid Sessions enabled
    CR:Consent Required
    CNR:Consent not Required
    CG:Session Consent given
    CNG:Session Consent not given

## Notes
  ## Anomalies

    Android:
      * Device id change without merge do not start a new session (CNR_A) : fix added but requires checking
      * Has scrolls, clicks, star-rating consent (ios dont)
      * Orientation doc should state it is on by default
    
    iOS:
      * no location req (203) : iOS should send an empty location request, when consent revoked and also we init with no consent.
      * no orientation req (205)
      * 206: no consent given request while CR_CNG
      * check if app to fg starts session (204) : fix is being added

## Manuals

## 200_CR_CG_M
    endSession();
    endSession();
    updateSession();
    updateSession();
      wait (seconds: 2);
    beginSession();
      wait (seconds: 2);
    beginSession();
    updateSession();
      wait(seconds: 2);
    updateSession();
      wait(seconds: 2);
    endSession();
      wait(seconds: 2);
    endSession();
    updateSession();
    updateSession();
    Check request queue and verify in this order:
    1. 5 reqs only
    2. 1 consent status req
    3. 1 begin session req
    4. 2 session update reqs with duration 2 seconds
    5. 1 end session req with duration 2 secs

## 201_CNR_M
    Same as 200_CR_CG_M except:
    1. 4 reqs instead of 5 (no consent status req)

## 202_CR_CNG_M
    Same as 200_CR_CG_M except:
    1. No requests generated

## 203_CR_CG_M_id_change
    endSession();
    updateSession();
    updateSession();
      wait (seconds: 2);
    changeIDwithMerge('newID');
    beginSession();
      wait (seconds:2);
    endSession();
    changeIDwithoutMerge('newID_2');
    beginSession();
    endSession();
    Check request queue and verify:
    1. There is 1 begin session req only
    2. There is 1 end session req only with duration 2

### Automatic

## 204_CNR_A_id_change
      wait (seconds: 1);
    changeIDwithMerge('newID');
      wait (seconds: 1);
    changeIDwithoutMerge('newID_2');
      wait (seconds: 1);
    changeIDwithMerge('newID');
      wait (seconds: 1);
    changeIDwithoutMerge('newID_2');
      wait (seconds: 1);
    *go to background*
      wait (seconds: 1);
    *back to foreground*
    changeIDwithMerge('newID');
    *go to background*
      wait (seconds: 1);
    *back to foreground*
    Check request queue and verify:
    1. too lazy to calculate just let us know and lets verify together

## 205_CR_CG_A_id_change
    same as 204_CNR_A_id_change

## 206_CR_CNG_A_id_change
    same as 204_CNR_A_id_change