#ReplayKit.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h	2016-08-03 08:32:23.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h	2016-10-22 03:50:30.000000000 +0200
@@ -33,12 +33,12 @@
 
  The view controller will present the user with a list of broadcast services available on the device and allow the user to set up a broadcast with the service through the service's UI.
 
- The RPBroadcastActivityViewController can be presented using [UIViewController presentViewController:animated:completion:] and should be dismissed when the delegate's broadcastActivityViewController:didFinishWithBroadcastController:error: method is called.
+ The RPBroadcastActivityViewController can be presented using [UIViewController presentViewController:animated:completion:] and should be dismissed when the delegate's broadcastActivityViewController:didFinishWithBroadcastController:error: method is called. Note that on large screen devices such as iPad, the default presentation style for view controllers is a popover. For an instance of RPBroadcastActivityViewController to present properly on iPad, it needs to have its popoverPresentationController's sourceRect and sourceView configured.
 
  @param broadcastActivityViewController The RPBroadcastActivityViewController which can be presented.
  @param error Optional error in the RPRecordingErrorCode domain which is supplied in the event the view controller could not be loaded.
  */
-+ (void)loadBroadcastActivityViewControllerWithHandler:(void(^)(RPBroadcastActivityViewController * __nullable broadcastActivityViewController, NSError * __nullable error))handler;
++ (void)loadBroadcastActivityViewControllerWithHandler:(nonnull void(^)(RPBroadcastActivityViewController * __nullable broadcastActivityViewController, NSError * __nullable error))handler;
 
 /*  @abstract Delegate that is notified when the activity view controller is complete. */
 @property (nonatomic, weak, nullable) id<RPBroadcastActivityViewControllerDelegate> delegate;
@@ -88,13 +88,19 @@
 - (void)finishBroadcastWithHandler:(void(^)(NSError * __nullable error))handler;
 @end
 
+@protocol RPBroadcastControllerDelegate <NSObject>
+@optional
+
 /*  @abstract Called when broadcasting finishes due to an error.
  @param broadcastController The controller instance.
  @param error Required error in the RPRecordingErrorCode domain.
  */
-@protocol RPBroadcastControllerDelegate <NSObject>
-@optional
+
 - (void)broadcastController:(RPBroadcastController *)broadcastController didFinishWithError:(NSError * __nullable)error;
+/*  @abstract Called when the broadcast service has data to pass back to broadcasting app.
+ @param broadcastController The controller instance.
+ @param serviceInfo NSDictionary instance with keys and values defined by the broadcasting service.
+ */
 - (void)broadcastController:(RPBroadcastController *)broadcastController didUpdateServiceInfo:(NSDictionary <NSString *, NSObject <NSCoding> *> *)serviceInfo;
 @end
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastExtension.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastExtension.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastExtension.h	2016-08-03 08:54:24.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastExtension.h	2016-10-22 04:46:16.000000000 +0200
@@ -96,6 +96,11 @@
  */
 - (void)processSampleBuffer:(CMSampleBufferRef)sampleBuffer withType:(RPSampleBufferType)sampleBufferType;
 
+/*! @abstract Method that should be called when broadcasting can not proceed due to an error. Calling this method will stop the broadcast and deliver the error back to the broadcasting app through RPBroadcastController's delegate.
+    @param error NSError object that will be passed back to the broadcasting app through RPBroadcastControllerDelegate's broadcastController:didFinishWithError: method.
+ */
+- (void)finishBroadcastWithError:(NSError *)error;
+
 @end
 NS_ASSUME_NONNULL_END
 

```