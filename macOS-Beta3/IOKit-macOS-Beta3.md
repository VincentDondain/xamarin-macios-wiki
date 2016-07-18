#IOKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDUsageTables.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDUsageTables.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDUsageTables.h	2016-06-29 01:11:16.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hid/IOHIDUsageTables.h	2016-07-10 08:58:23.000000000 +0200
@@ -94,7 +94,9 @@
     kHIDUsage_GD_Keyboard    = 0x06,    /* Application Collection */
     kHIDUsage_GD_Keypad    = 0x07,    /* Application Collection */
     kHIDUsage_GD_MultiAxisController    = 0x08,    /* Application Collection */
-    /* 0x09 - 0x2F Reserved */
+    kHIDUsage_GD_TabletPCSystemControls    = 0x09,    /* Application Collection */
+    kHIDUsage_GD_AssistiveControl    = 0x0A,    /* Application Collection */
+    /* 0x0B - 0x2F Reserved */
     kHIDUsage_GD_X    = 0x30,    /* Dynamic Value */
     kHIDUsage_GD_Y    = 0x31,    /* Dynamic Value */
     kHIDUsage_GD_Z    = 0x32,    /* Dynamic Value */
@@ -301,6 +303,7 @@
     kHIDUsage_Game_GunSafety    = 0x36,    /* On/Off Control */
     kHIDUsage_Game_GamepadFireOrJump    = 0x37,    /* Logical Collection */
     kHIDUsage_Game_GamepadTrigger    = 0x39,    /* Logical Collection */
+    kHIDUsage_Game_GamepadFormFitting    = 0x39,    /* Static Flag */
     /* 0x3A - 0xFFFF Reserved */
     kHIDUsage_Game_Reserved = 0xFFFF
 };
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h	2016-06-29 01:11:16.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOKit.framework/Headers/hidsystem/IOHIDParameter.h	2016-07-10 08:58:23.000000000 +0200
@@ -335,7 +335,6 @@
     kIOHIDNumLockState              = 0x00000002,
     kIOHIDActivityUserIdle          = 0x00000003,
     kIOHIDActivityDisplayOn         = 0x00000004,
-    kIOHIDModifierFlags             = 0x00000005
 };
 
 #endif /* !_DEV_EVSIO_H */

```