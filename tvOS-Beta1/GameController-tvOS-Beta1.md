#GameController.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCGamepad.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCGamepad.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCGamepad.h	2015-09-30 23:50:53.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameController.framework/Headers/GCGamepad.h	2016-05-27 07:08:34.000000000 +0200
@@ -20,6 +20,7 @@
  A profile maps the hardware notion of a controller into a logical controller. One that a developer can design for
  and depend on, no matter the underlying hardware.
  */
+NS_CLASS_DEPRECATED(10_9, 10_12, 7_0, 10_0)
 GAMECONTROLLER_EXPORT
 @interface GCGamepad : NSObject
 

```