#Messages.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSConversation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSConversation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSConversation.h	2016-06-05 05:35:26.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSConversation.h	2016-06-28 08:51:47.000000000 +0200
@@ -24,7 +24,7 @@
 @property (nonatomic, readonly) NSUUID *localParticipantIdentifier;
 
 /*!
- @property   recipientIdentityTokens
+ @property   remoteParticipantIdentifiers
  @abstract   A NSArray of NSUUID instances, each uniquely identifies a remote participant in the conversation.
  @discussion Each NSUUID identifies the a remote participant in the conversation scoped to
  this device. These values will be stable while the extension is enabled. If the extension
@@ -47,19 +47,14 @@
  @method     insertMessage:localizedChangeDescription:completionHandler:
  @abstract   Stages provided the MSMessage for sending.
  @discussion This method inserts a MSMessage object into the Messages input field,
- Subsequent calls to this method will replace any existing message on the input field.
- If the MSMessage was initialized with the session identifier of an existing message,
- the existing message will be updated and moved to the bottom of the conversation
- transcript. If a change description text is provided, Messages will use this to
- construct an entry in the conversation transcript to replace the updated message.
+ Subsequent calls to this method will replace any existing message on the input field. 
  If the message was successfully inserted on the input field, the completion handler
  will be called with a nil error parameter otherwise the error parameter will be
  populated with an NSError object describing the failure.
  @param      message            The MSMessage instance describing the message to be sent.
- @param      changeDescription  A succinct string describing changes made to the message instance.
  @param      completionHandler  A completion handler called when the message has been staged or if there was an error.
  */
-- (void)insertMessage:(MSMessage *)message localizedChangeDescription:(nullable NSString *)changeDescription completionHandler:(nullable void (^)(NSError * _Nullable))completionHandler;
+- (void)insertMessage:(MSMessage *)message completionHandler:(nullable void (^)(NSError * _Nullable))completionHandler;
 
 /*!
  @method     insertSticker:completionHandler:
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessage.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessage.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessage.h	2016-06-05 05:35:26.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessage.h	2016-06-28 08:51:47.000000000 +0200
@@ -81,6 +84,14 @@
 @property (nonatomic, copy, nullable) NSString *accessibilityLabel;
 
 /*!
+ @property   summaryText
+ @abstract   A localized string describing the message.
+ @discussion This string should provide a succinct description of the message. This
+ will be used to provide a summary of the message in the UI.
+ */
+@property (nonatomic, copy, nullable) NSString *summaryText;
+
+/*!
  @property   error
  @abstract   An error object that indicates why a message failed to send.
  @discussion This value is nil if the message is has not yet been sent, is still
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessageError.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessageError.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessageError.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessageError.h	2016-06-28 08:51:47.000000000 +0200
@@ -0,0 +1,25 @@
+//
+//  MSMessageError.h
+//  Messages
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <Messages/MessagesDefines.h>
+
+MESSAGES_EXTERN NSString * const MSStickersErrorDomain NS_AVAILABLE_IOS(10_0);
+MESSAGES_EXTERN NSString * const MSStickersErrorStickerInfoKey NS_AVAILABLE_IOS(10_0);
+MESSAGES_EXTERN NSString * const MSMessagesErrorDomain NS_AVAILABLE_IOS(10_0);
+
+typedef NS_ENUM(NSInteger, MSMessageErrorCode) {
+    MSMessageErrorCodeFileNotFound = 1,
+    MSMessageErrorCodeFileUnreadable,
+    MSMessageErrorCodeImproperFileType,
+    MSMessageErrorCodeImproperFileURL,
+    MSMessageErrorCodeStickerFileImproperPath,
+    MSMessageErrorCodeStickerFileImproperFileAttributes,
+    MSMessageErrorCodeStickerFileImproperFileSize,
+    MSMessageErrorCodeStickerFileImproperFileFormat,
+    MSMessageErrorCodeURLExceedsMaxSize,
+} NS_ENUM_AVAILABLE_IOS(10_0);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSStickerBrowserView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSStickerBrowserView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSStickerBrowserView.h	2016-06-05 05:35:26.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSStickerBrowserView.h	2016-06-28 08:51:47.000000000 +0200
@@ -61,6 +61,22 @@
 @property (nonatomic, weak, nullable) id <MSStickerBrowserViewDataSource> dataSource;
 
 /*!
+ @abstract The Sticker Browser View content offset.
+ */
+@property (nonatomic, assign, readwrite) CGPoint contentOffset;
+
+/*!
+ @abstract The Sticker Browser View content inset.
+ */
+@property (nonatomic, assign, readwrite) UIEdgeInsets contentInset;
+
+/*!
+ @abstract animate Sticker Browser View at constant velocity to new offset.
+ */
+- (void)setContentOffset:(CGPoint)contentOffset animated:(BOOL)animated;
+
+
+/*!
  @abstract Asks the Sticker Browser View to reload its data from its data source.
  */
 - (void)reloadData;

```