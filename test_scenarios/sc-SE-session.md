## Init options
    M:Manual Sessions enabled
    A:Automatic sessions enabled
    H:Hybrid Sessions enabled
    CR:Consent Required
    CNR:Consent not Required
    CG:Session Consent given
    CNG:Session Consent not given

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

## Manual Sessions

## 200_CR_CG_M
    init();
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
    In the request queue there should be:
    0- consent information
    1- orientation
    2- begin_session
    3- update_session
    4- update_session
    5- end_session

## 201_CNR_M
    Same as 200_CR_CG_M except:
    In the request queue there should be:
    0- begin_session
    1- update_session
    2- update_session
    3- orientation
    4- end_session

## 202_CR_CNG_M
    Same as 200_CR_CG_M except:
    In the request queue there should be:
    0- consent information
    1- empty location

## 203_CR_CG_M_id_change
    init();
    endSession();
    updateSession();
    updateSession();
      wait (seconds: 2);
    changeIDwithMerge('newID');
    beginSession();
      wait (seconds:2);
    endSession();
      wait (seconds:2);
    changeIDwithoutMerge('newID_2');
      wait (seconds:1);
    beginSession();
      wait (seconds:1);
    endSession();
      wait (seconds:1);
    giveAllConsent();
      wait (seconds:1);
    beginSession();
      wait (seconds:2);
    changeIDwithoutMerge('newID_3');
    In the request queue there should be:
    0- consent information, true
    1- orientation (iOS only)
    2- device ID change
    3- begin session
    4- end session
    5- location
    6- consent information, true
    7- begin session
    8- end session
    9- location

## 207_CNR_M_id_change
    init();
    endSession();
    updateSession();
    updateSession();
      wait (seconds: 2);
    changeIDwithMerge('newID');
    beginSession();
      wait (seconds:2);
    endSession();
    changeIDwithoutMerge('newID_2');
    endSession();
    beginSession();
      wait (seconds:2);
    changeIDwithoutMerge('newID_3');
    In the request queue there should be:
    0- device ID change
    1- begin session
    2- orientation
    3- end session
    4- begin session
    5- orientation (android only)

### Automatic Sessions

## 204_CNR_A_id_change
    init();
      wait (seconds: 1);
    changeIDwithMerge('newID');
    beginSession();
    updateSession();
    endSession();
      wait (seconds: 2);
    changeIDwithoutMerge('newID_2');
    beginSession();
    updateSession();
    endSession();
    *go to background*
      wait(seconds: 3);
    *back to foreground*
      wait (seconds: 3);
    changeIDwithMerge('newID');
    Currently in the request queue there should be:
    0- begin_session
    1- change ID
    2- end session
    3- begin_session
    4- end session
    5- begin_session (auto fg in ios not working)
    6- change ID
    EQ: orientation (android only)

## 205_CR_CG_A_id_change
    init();
      wait (seconds: 1);
    changeIDwithMerge('newID');
    beginSession();
    updateSession();
    endSession();
    *go to background*
      wait (seconds: 1);
    *back to foreground*
      wait (seconds: 1);
    changeIDwithoutMerge('newID_2');
    beginSession();
    updateSession();
    endSession();
      wait (seconds: 1);
    changeIDwithMerge('newID');
      wait (seconds: 1);
    changeIDwithoutMerge('newID_2');
      wait (seconds: 1);
    changeIDwithMerge('newID');
    Currently in the request queue there should be:
    0- consents (begin ses in ios)ß
    1- begin_session (consent in ios)
    2- change ID
    3- orientation (android only)
    4- end session (orientation in ios)
    5- begin_session (end session in ios)
    6- orientation (begin session in ios)
    7- end session
    8- location
    9- change ID
    10- change ID

## 206_CR_CNG_A_id_change
    Same as 205_CR_CG_A
    Currently in the request queue there should be:
    0- consents
    1- location
    2- change ID
    3- change ID
    4- change ID
