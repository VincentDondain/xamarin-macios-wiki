#MessageUI.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MessageUI.framework/Headers/MFMailComposeViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MessageUI.framework/Headers/MFMailComposeViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MessageUI.framework/Headers/MFMailComposeViewController.h	2015-10-03 02:17:37.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MessageUI.framework/Headers/MFMailComposeViewController.h	2016-05-25 05:38:54.000000000 +0200
@@ -24,13 +24,12 @@
     @constant   MFMailComposeResultSent        User successfully sent/queued the message.
     @constant   MFMailComposeResultFailed      User's attempt to save or send was unsuccessful.
 */
-enum MFMailComposeResult {
+typedef NS_ENUM(NSInteger, MFMailComposeResult) {
     MFMailComposeResultCancelled,
     MFMailComposeResultSaved,
     MFMailComposeResultSent,
     MFMailComposeResultFailed
-};
-typedef enum MFMailComposeResult MFMailComposeResult;   // available in iPhone 3.0
+} NS_ENUM_AVAILABLE_IOS(3_0);
 
 /*!
     @const      MFMailComposeErrorDomain
@@ -50,11 +49,10 @@
     @constant   MFMailComposeErrorCodeSaveFailed    Generic error indicating a save failed.
     @constant   MFMailComposeErrorCodeSendFailed    Generic error indicating a send failed.
 */
-enum MFMailComposeErrorCode {
+typedef NS_ENUM(NSInteger, MFMailComposeErrorCode) {
     MFMailComposeErrorCodeSaveFailed,
     MFMailComposeErrorCodeSendFailed
-};
-typedef enum MFMailComposeErrorCode MFMailComposeErrorCode;     // available in iPhone 3.0
+} NS_ENUM_AVAILABLE_IOS(3_0);
 
 
 @protocol MFMailComposeViewControllerDelegate;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MessageUI.framework/Headers/MFMessageComposeViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MessageUI.framework/Headers/MFMessageComposeViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MessageUI.framework/Headers/MFMessageComposeViewController.h	2015-10-03 02:17:37.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MessageUI.framework/Headers/MFMessageComposeViewController.h	2016-05-25 05:38:54.000000000 +0200
@@ -24,12 +24,11 @@
  @constant   MessageComposeResultFailed      User's attempt to save or send was unsuccessful.
  */
 
-enum MessageComposeResult {
+typedef NS_ENUM(NSInteger, MessageComposeResult) {
     MessageComposeResultCancelled,
     MessageComposeResultSent,
     MessageComposeResultFailed
-};
-typedef enum MessageComposeResult MessageComposeResult;   // available in iPhone 4.0
+} NS_ENUM_AVAILABLE_IOS(4_0);
 
 /*!
  @constant  MFMessageComposeViewControllerAttachmentURL   The url for the given attachment.

```