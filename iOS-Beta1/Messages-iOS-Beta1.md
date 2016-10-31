#Messages.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSConversation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSConversation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSConversation.h	2016-09-24 05:09:30.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSConversation.h	2016-10-25 05:35:23.000000000 +0200
@@ -44,7 +44,7 @@
 @property (nonatomic, readonly, nullable) MSMessage *selectedMessage;
 
 /*!
- @method     insertMessage:localizedChangeDescription:completionHandler:
+ @method     insertMessage:completionHandler:
  @abstract   Stages provided the MSMessage for sending.
  @discussion This method inserts a MSMessage object into the Messages input field,
  Subsequent calls to this method will replace any existing message on the input field. 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessage.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessage.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessage.h	2016-09-24 05:09:30.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessage.h	2016-10-25 05:35:23.000000000 +0200
@@ -25,7 +25,7 @@
 /*!
  @method     initWithSession:
  @abstract   Initializes a message with a session.
- @see insertMessage:localizedChangeDescription:completionHandler:
+ @see        insertMessage:completionHandler:
  @param      session  The session that new message will join.
  @discussion A message initialized with a session will be updated 
  and moved to the bottom of the conversation transcript when another message created
@@ -50,7 +50,7 @@
 
 /*!
  @property   layout
- @abstract   A subclass of to MSMessageLayout.
+ @abstract   A subclass of MSMessageLayout.
  @discussion The MSMessageLayout subclass will be used to construct UI
  representing the message in the conversation transcript.
  */
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSSession.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSSession.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSSession.h	2016-09-24 05:09:30.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSSession.h	2016-10-25 05:35:23.000000000 +0200
@@ -14,7 +14,7 @@
  entry in the conversation transcript.
  */
 NS_CLASS_AVAILABLE_IOS(10_0)
-@interface MSSession : NSObject
+@interface MSSession : NSObject <NSSecureCoding>
 @end
 
 NS_ASSUME_NONNULL_END

```