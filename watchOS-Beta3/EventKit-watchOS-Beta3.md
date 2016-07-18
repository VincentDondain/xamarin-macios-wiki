#EventKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKParticipant.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKParticipant.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKParticipant.h	2016-06-27 06:47:19.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKParticipant.h	2016-07-11 07:19:04.000000000 +0200
@@ -61,7 +61,7 @@
 @property(nonatomic, readonly) EKParticipantType participantType;
 
 /*!
-    @property   isCurrentUser
+    @property   currentUser
     @abstract   A boolean indicating whether this participant represents the
                 owner of this account.
  */

```