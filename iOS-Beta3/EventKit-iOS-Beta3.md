#EventKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKParticipant.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKParticipant.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKParticipant.h	2016-06-27 07:56:27.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKParticipant.h	2016-07-11 07:11:52.000000000 +0200
@@ -61,7 +61,7 @@
 @property(nonatomic, readonly) EKParticipantType participantType;
 
 /*!
-    @property   isCurrentUser
+    @property   currentUser
     @abstract   A boolean indicating whether this participant represents the
                 owner of this account.
  */

```