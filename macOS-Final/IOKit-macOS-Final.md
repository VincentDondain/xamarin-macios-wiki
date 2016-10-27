#IOKit.framework

``` diff
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDKeys.h	2016-10-05 23:59:49.000000000 -0400
@@ -397,7 +397,8 @@
  */
 enum {
     kIOHIDValueOptionsFlagRelativeSimple    = (1<<0),
-    kIOHIDValueOptionsFlagPrevious          = (1<<1)
+    kIOHIDValueOptionsFlagPrevious          = (1<<1),
+    kIOHIDValueOptionsUpdateElementValues   = (1<<2)
 };
 typedef uint32_t IOHIDValueOptions;
 
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDProperties.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDProperties.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDProperties.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDProperties.h	2016-10-05 23:59:49.000000000 -0400
@@ -88,7 +88,7 @@
  *
  * @abstract    CFArray of dictionaries that contain user defined key mappings.
  */
-#define kIOHIDUserUsageMapKey                       "UserKeyMapping"
+#define kIOHIDUserKeyUsageMapKey                     "UserKeyMapping"
 
 /*!
  * @define      kIOHIDKeyboardCapsLockDelayOverride
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDUsageTables.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDUsageTables.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDUsageTables.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDUsageTables.h	2016-10-05 23:59:49.000000000 -0400
@@ -1549,6 +1549,7 @@
     kHIDUsage_Snsr_Property_PowerState_D3_Sleep                 = 0x0854,
     kHIDUsage_Snsr_Property_PowerState_D4_PowerOff              = 0x0855,
     /* 0x0855 - 0x085F Reserved */
+    kHIDUsage_Snsr_Light_Illuminance                            = 0x04D1,
     
     /* Specific Sensor Type Data Fields */
     /*** TODO ***/
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h	2016-08-16 20:29:00.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h	2016-10-05 23:59:49.000000000 -0400
@@ -139,7 +139,7 @@
 
 //
 //
-#define kIOHIDMouseClickNotification    "HIDClickNotification"
+#define kIOHIDResetStickyKeyNotification    "HIDResetStickyKeyNotification"
 
 // if kIOHIDMouseKeysOptionTogglesKey is 1, then a sequence of five
 // option keys in sequence will toggle mouse keys on or off
@@ -162,6 +162,7 @@
 
 // Parametric Acceleration Keys
 #define kHIDAccelParametricCurvesKey            "HIDAccelCurves"
+#define kHIDPointerReportRateKey                "HIDPointerReportRate"
 #define kHIDTrackingAccelParametricCurvesKey    "HIDTrackingAccelCurves"
 #define kHIDScrollAccelParametricCurvesKey      "HIDScrollAccelCurves"
 #define kHIDAccelParametricCurvesDebugKey       "HIDAccelCurvesDebug"

```