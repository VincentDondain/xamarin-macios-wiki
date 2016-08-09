#Intents.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-07-25 07:30:57.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSearchForMessagesIntent.h	2016-08-03 04:13:04.000000000 +0200
@@ -136,9 +136,6 @@
 - (void)resolveDateTimeRangeForSearchForMessages:(INSearchForMessagesIntent *)intent
                                   withCompletion:(void (^)(INDateComponentsRangeResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveDateTimeRange(forSearchForMessages:with:));
 
-- (void)resolveIdentifiersForSearchForMessages:(INSearchForMessagesIntent *)intent
-                                withCompletion:(void (^)(NSArray<INStringResolutionResult *> *resolutionResults))completion NS_SWIFT_NAME(resolveIdentifiers(forSearchForMessages:with:));
-
 - (void)resolveGroupNamesForSearchForMessages:(INSearchForMessagesIntent *)intent
                                withCompletion:(void (^)(NSArray<INStringResolutionResult *> *resolutionResults))completion NS_SWIFT_NAME(resolveGroupNames(forSearchForMessages:with:));
 
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntent.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntent.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntent.h	2016-07-25 07:30:57.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Intents.framework/Headers/INSetMessageAttributeIntent.h	2016-08-03 04:27:22.000000000 +0200
@@ -84,9 +84,6 @@
 
  */
 
-- (void)resolveIdentifiersForSetMessageAttribute:(INSetMessageAttributeIntent *)intent
-                                  withCompletion:(void (^)(NSArray<INStringResolutionResult *> *resolutionResults))completion NS_SWIFT_NAME(resolveIdentifiers(forSetMessageAttribute:with:));
-
 - (void)resolveAttributeForSetMessageAttribute:(INSetMessageAttributeIntent *)intent
                                 withCompletion:(void (^)(INMessageAttributeResolutionResult *resolutionResult))completion NS_SWIFT_NAME(resolveAttribute(forSetMessageAttribute:with:));
 

```