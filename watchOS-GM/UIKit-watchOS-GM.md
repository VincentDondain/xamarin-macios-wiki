#UIKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h
--- /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-08-06 03:20:59.000000000 -0500
+++ /Applications/Xcode8-GM.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-08-17 01:00:09.000000000 -0500
@@ -219,3 +219,9 @@
 #import <UIKit/UIViewPropertyAnimator.h>
 #endif
 
+#if __has_include(<UIKit/UIFeedbackGenerator.h>)
+#import <UIKit/UIFeedbackGenerator.h>
+#import <UIKit/UISelectionFeedbackGenerator.h>
+#import <UIKit/UIImpactFeedbackGenerator.h>
+#import <UIKit/UINotificationFeedbackGenerator.h>
+#endif

```