#NetworkExtension.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWTCPConnection.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWTCPConnection.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWTCPConnection.h	2016-09-24 00:47:08.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWTCPConnection.h	2016-10-20 10:00:28.000000000 +0200
@@ -162,7 +162,7 @@
  * @param length The exact number of bytes the caller wants to read
  * @param completion The completion handler to be invoked when there is data to read or an error occurred
  */
-- (void)readLength:(NSUInteger)length completionHandler:(void (^)(NSData *data, NSError * __nullable error))completion NS_AVAILABLE(10_11, 9_0);
+- (void)readLength:(NSUInteger)length completionHandler:(void (^)(NSData * __nullable data, NSError * __nullable error))completion NS_AVAILABLE(10_11, 9_0);
 
 /*!
  * @method readMinimumLength:maximumLength:completionHandler:
@@ -189,7 +189,7 @@
  * @param maximum The maximum number of bytes the caller wants to read
  * @param completion The completion handler to be invoked when there is data to read or an error occurred
  */
-- (void)readMinimumLength:(NSUInteger)minimum maximumLength:(NSUInteger)maximum completionHandler:(void (^)(NSData *data, NSError * __nullable error))completion NS_AVAILABLE(10_11, 9_0);
+- (void)readMinimumLength:(NSUInteger)minimum maximumLength:(NSUInteger)maximum completionHandler:(void (^)(NSData * __nullable data, NSError * __nullable error))completion NS_AVAILABLE(10_11, 9_0);
 
 /*!
  * @method write:completionHandler:
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWUDPSession.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWUDPSession.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWUDPSession.h	2016-09-25 15:44:24.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/NetworkExtension.framework/Headers/NWUDPSession.h	2016-10-20 10:00:28.000000000 +0200
@@ -131,7 +131,7 @@
  * @param handler A handler called when datagrams have been read, or when an error has occurred.
  * @param minDatagrams The maximum number of datagrams to send to the handler.
  */
-- (void)setReadHandler:(void (^)(NSArray<NSData *> *datagrams, NSError * __nullable error))handler
+- (void)setReadHandler:(void (^)(NSArray<NSData *> * __nullable datagrams, NSError * __nullable error))handler
 		  maxDatagrams:(NSUInteger)maxDatagrams NS_AVAILABLE(10_11, 9_0);
 
 /*!

```