#MessageUI.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MessageUI.framework/Headers/MFMessageComposeViewController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MessageUI.framework/Headers/MFMessageComposeViewController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MessageUI.framework/Headers/MFMessageComposeViewController.h	2016-06-29 07:05:23.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MessageUI.framework/Headers/MFMessageComposeViewController.h	2016-07-10 12:53:11.000000000 +0200
@@ -57,6 +57,7 @@
 */
 extern NSString *const MFMessageComposeViewControllerTextMessageAvailabilityKey __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_5_0);
 
+@class MSMessage;
 @protocol MFMessageComposeViewControllerDelegate;
 
 /*!
@@ -152,6 +153,15 @@
  */
 @property(nonatomic,copy,readonly,nullable) NSArray<NSDictionary *> *attachments /*__OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_7_0)*/;
 
+
+/*!
+ @property   message
+ @abstract   This property sets the initial interactive message.
+ */
+@property(nonatomic,copy,nullable) MSMessage *message __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_10_0);
+
+
+
 /*!
  @method     addAttachmentURL:withAlternateFilename:
  @abstract   Returns <tt>YES</tt>if the attachment at the specified URL was added to the composition successfully.

```