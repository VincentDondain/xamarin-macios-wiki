#Messages.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessageError.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessageError.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessageError.h	2016-06-28 08:51:47.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessageError.h	2016-07-12 06:30:42.000000000 +0200
@@ -9,7 +9,7 @@
 #import <Messages/MessagesDefines.h>
 
 MESSAGES_EXTERN NSString * const MSStickersErrorDomain NS_AVAILABLE_IOS(10_0);
-MESSAGES_EXTERN NSString * const MSStickersErrorStickerInfoKey NS_AVAILABLE_IOS(10_0);
+
 MESSAGES_EXTERN NSString * const MSMessagesErrorDomain NS_AVAILABLE_IOS(10_0);
 
 typedef NS_ENUM(NSInteger, MSMessageErrorCode) {
@@ -17,7 +17,6 @@
     MSMessageErrorCodeFileUnreadable,
     MSMessageErrorCodeImproperFileType,
     MSMessageErrorCodeImproperFileURL,
-    MSMessageErrorCodeStickerFileImproperPath,
     MSMessageErrorCodeStickerFileImproperFileAttributes,
     MSMessageErrorCodeStickerFileImproperFileSize,
     MSMessageErrorCodeStickerFileImproperFileFormat,

```