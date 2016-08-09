#Messages.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessage.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessage.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessage.h	2016-07-25 10:13:22.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Messages.framework/Headers/MSMessage.h	2016-08-07 08:19:44.000000000 +0200
@@ -35,7 +35,7 @@
 
 /*!
  @property   session
- @abstract   An NSUUID that identifies the session that message belongs to.
+ @abstract   An MSSession that identifies the session that message belongs to.
  */
 @property (nonatomic, readonly, nullable) MSSession *session;
 

```