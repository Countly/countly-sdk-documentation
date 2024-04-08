# SDK Internal Limits Test Scenarios

These test scenarios tries to validate if SDK internal limits are implemented correctly.
There are two types of limits:
- Limits to the length of a string
- Limits to the count(size) of a thing

All limits should only apply to user provided values. Deviations from this rule are:
1.User provided but exempt things (meaning it has a different limit):
    - user image url (in user profiles)
2.Non user provided but included things:
    - crash stack trace lines per thread
    - crash stack trace line length

These tests should validate the general things we expect like:
- These methods should not break with bad values (more important for dynamically typed languages)
- These limits should not truncate SDK's internal keys/values

## Base conditions
Each test should have a bunch of events/settings (if applicable). These should be things effected by internal limits and should be bundled under a method called 'createInternalLimitsTestingEvents'.

Segmentations and names to use:
  gloabalSegmentation = {'gs1_123456': 123456, 'gs2_123456': '123456'}
  segmentation = {'s1_123456': 123456, 's2_123456': '123456'}
  eventWithSegmentation = {'key': 'ews_123456', 'count': 123456, 'sum': '1.23456', ...segmentation}
  userProperties = {
    'name': '123456',
    'username': '123456',
    'email': '123456',
    'organization': '123456',
    'phone': '123456',
    'picture': '123456',
    'picturePath': '123456',
    'gender': '123456',
    'byear': '123456',
    'cv1_123456': 123456,
    'cv2_123456': '123456'
  };

  setGlobalViewSegmentation(gloabalSegmentation)
  recordEvent(eventWithSegmentation)
  recordLegacyView('lvn_123456', segmentation)
  startAutoStoppedView('asvn_123456', segmentation)
  startView('svn_123456')
  endView('svn_123456', segmentation)
  startTrace('cmn_123456')
  endTrace('cmn_123456', segmentation)
  recordNetworkTrace('ntn_123456')
  addCrashLog('b1_123456')
  logException('e1_123456', true, segmentation)
  addCrashLog('b2_123456')
  logException('e2_123456', false, segmentation)
  setUserProperties(userProperties)
  setProperty('p1_123456', '123456')
  setProperty('p2_123456', 123456)
  increment('i_123456')
  incrementBy('ib_123456', 2)
  multiply('m_123456', 2)
  saveMax('smi_123456', 2)
  saveMin('sma_123456', 2)
  setOnce('so_123456', '123456')
  pushUnique('pu1_123456', '123456')
  pushUnique('pu2_123456', 123456)
  push('ps_123456', '123456')
  pull('pl_123456', '123456')

  TODO: add manual widget reporting calls
  TODO: add global crash segmentation call

## 100: bad and/or wrong values 
- IL_100_null: give all six limits null at init => createInternalLimitsTestingEvents => nothing truncated
- IL_101_zero: give all six limits 0 at init => createInternalLimitsTestingEvents => nothing truncated
- IL_100_negative: give all six limits -1 at init => createInternalLimitsTestingEvents => nothing truncated

## 200: check normal working of each limit
Set each limit to 5 and init => createInternalLimitsTestingEvents => check truncated/limited values
TODO: more detail
-IL_201_setMaxKeyLength
-IL_202_setMaxKeyLength
-IL_203_setMaxKeyLength
-IL_204_setMaxKeyLength
-IL_205_setMaxKeyLength
-IL_206_setMaxKeyLength

