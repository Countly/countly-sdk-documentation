## Init options
    M:Manual Sessions enabled
    A:Automatic sessions enabled
    H:Hybrid Sessions enabled
    CR:Consent Required
    CNR:Consent not Required
    CG:Session Consent given
    CNG:Session Consent not given
    
    sendUserProperty:
        Map<String, Object> userProperties = {
            'name': 'Nicola Tesla',
            'username': 'nicola',
            'email': 'info@nicola.tesla',
            'organization': 'Trust Electric Ltd',
            'phone': '+90 822 140 2546',
            'picture': 'http://images2.fanpop.com/images/photos/3300000/Nikola-Tesla-nikola-tesla-3365940-600-738.jpg',
            'picturePath': '',
            'gender': 'M',
            'byear': 1919,
            'special_value': 'something special',
            'not_special_value': 'something special cooking'
        };
        Countly.instance.userProfile.setUserProperties(userProperties);
        
    sendUserData:
        Countly.instance.userProfile.setProperty('a12345', 'My Property');
        Countly.instance.userProfile.increment('b12345');
        Countly.instance.userProfile.incrementBy('c12345', 10);
        Countly.instance.userProfile.multiply('d12345', 20);
        Countly.instance.userProfile.saveMax('e12345', 100);
        Countly.instance.userProfile.saveMin('f12345', 50);
        Countly.instance.userProfile.setOnce('g12345', '200');
        Countly.instance.userProfile.pushUnique('h12345', 'morning');
        Countly.instance.userProfile.push('i12345', 'morning');
        Countly.instance.userProfile.pull('k12345', 'morning');
        
    sendSameData:
        Countly.instance.userProfile.setProperty('a12345', '1');
        Countly.instance.userProfile.setProperty('a12345', '2');
        Countly.instance.userProfile.setProperty('a12345', '3');
        Countly.instance.userProfile.setProperty('a12345', '4');

## 200_CNR_A
    Init SDK
    sendUserProperty
    sendUserData
    Check request queue:
    - There can be begin session request

## 201_CR_CG_A
    same as 200

## 202_CR_CNG_A
    same as 200 but there should be no request

## 203_CNR_A_events
    Init SDK
    RecordBasicEvent A
    RecordBasicEvent B
    sendSameData
    RecordBasicEvent C
    sendSameData
    RecordBasicEvent D
    sendSameData
    RecordBasicEvent E
    Check requests queue:
        - Begin session
        - Event A and B
        - User Property a12345 = 4
        - Event C
        - User Property a12345 = 4
        - Event D
        - User Property a12345 = 4
    Check event queue:
        - Event E

## 204_XX_XX_X
    Will be added in the future.

## 205_CR_CG_A
    same as 203

## 206_CR_CNG_A
    same as 203 but there should be no request

## 207_CNR_M
    Init SDK
    Begin Session
    RecordBasicEvent A
    RecordBasicEvent B
    sendSameData
    End Session
    RecordBasicEvent C
    sendUserData
    EndSession
    Change device ID Merge ('merge_id')
    sendSameData
    Change device ID Non Merge ('non_merge_id')
    sendSameData
    RecordBasicEvent D
    Check requests queue:
        - Begin session
        - Event A and B
        - User Property a12345 = 4
        - End Session
        - Event C
        - User Data
        - Merge ID
        - User Property a12345 = 4
        - User Property a12345 = 4
    Check event queue:
        - Event D

## 208_CR_CG_M
    same as 207
    Check requests queue:
        - Begin session
        - Event A and B
        - User Property a12345 = 4
        - End Session
        - Event C
        - User Data
        - Merge ID
    Check event queue:
        -

## 209_CR_CNG_M 
    same as 207 but no there should be no request

## 210_CNR_M_duration
    Init SDK with session update 5 secs
    sendUserData
    wait 6 secs
    Check request queue:
        - User property req with all data
