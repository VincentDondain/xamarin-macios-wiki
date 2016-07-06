#ReplayKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h	2016-05-25 05:35:09.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h	2016-06-27 06:49:16.000000000 +0200
@@ -30,11 +30,11 @@
 @interface RPBroadcastActivityViewController : UIViewController
 
 /*  @abstract Loads a RPBroadcastActivityViewController instance and returns it in the handler block.
- 
+
  The view controller will present the user with a list of broadcast services available on the device and allow the user to set up a broadcast with the service through the service's UI.
- 
+
  The RPBroadcastActivityViewController can be presented using [UIViewController presentViewController:animated:completion:] and should be dismissed when the delegate's broadcastActivityViewController:didFinishWithBroadcastController:error: method is called.
- 
+
  @param broadcastActivityViewController The RPBroadcastActivityViewController which can be presented.
  @param error Optional error in the RPRecordingErrorCode domain which is supplied in the event the view controller could not be loaded.
  */
@@ -61,11 +61,16 @@
 @interface RPBroadcastController : NSObject
 /*  @abstract Indicates whether the controller is currently broadcasting. */
 @property (nonatomic, readonly, getter=isBroadcasting) BOOL broadcasting;
+/*  @abstract Indicates whether the controller is currently paused. */
+@property (nonatomic, readonly, getter=isPaused) BOOL paused;
 /*  @abstract URL that can be used to redirect the user to the on-going or completed broadcast. */
 @property (nonatomic, readonly) NSURL *broadcastURL;
+/*  @abstract Dictionary updated by the service during a broadcast. The keys and values of this dictionary are defined by the broadcast service. KVO observable. */
+@property (nonatomic, readonly, nullable) NSDictionary <NSString *, NSObject <NSCoding> *> *serviceInfo;
 /*  @abstract Delegate which will be notified when an error occurs during broadcast. */
-@property (nonatomic, weak) id<RPBroadcastControllerDelegate> broadcastControllerDelegate;
-
+@property (nonatomic, weak) id<RPBroadcastControllerDelegate> delegate;
+/*  @abstract bundleID of the broadcast extension which was selected by the user. */
+@property (nonatomic, readonly) NSString *broadcastExtensionBundleID;
 /*  @abstract Start the broadcast.
  @param error Optional error in the RPRecordingErrorCode domain. A nil error signifies that broadcasting has started successfully.
  */
@@ -89,6 +94,7 @@
  */
 @protocol RPBroadcastControllerDelegate <NSObject>
 - (void)broadcastController:(RPBroadcastController *)broadcastController didFinishWithError:(NSError * __nullable)error;
+- (void)broadcastController:(RPBroadcastController *)broadcastController didUpdateServiceInfo:(NSDictionary <NSString *, NSObject <NSCoding> *> *)serviceInfo;
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastConfiguration.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastConfiguration.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastConfiguration.h	2016-05-23 08:15:43.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastConfiguration.h	2016-06-27 06:50:02.000000000 +0200
@@ -8,7 +8,15 @@
 #import <Foundation/Foundation.h>
 
 NS_CLASS_AVAILABLE_IOS(10_0)
+
+NS_ASSUME_NONNULL_BEGIN
 @interface RPBroadcastConfiguration : NSObject <NSCoding, NSSecureCoding>
+
+/* @abstract Specify the duration of a movie clip before it is delivered to the movie clip handler extension. Default is 5 seconds. */
 @property (nonatomic, assign) NSTimeInterval clipDuration;
-@property (nonatomic, strong, nullable) NSDictionary <NSNumber *, NSObject <NSCoding, NSSecureCoding> *> *videoCompressionProperties;
+
+/* @abstract Override the video compression properties used to encode movie clips. See AVVideoCompressionPropertiesKey in <AVFoundation/AVVideoSettings.h> for available properties. */
+@property (nonatomic, strong, nullable) NSDictionary <NSString *, NSObject <NSCoding, NSSecureCoding> *> *videoCompressionProperties;
+
 @end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastExtension.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastExtension.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastExtension.h	2016-05-23 08:15:43.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastExtension.h	2016-06-27 06:50:02.000000000 +0200
@@ -7,6 +7,7 @@
 
 #import "RPBroadcastConfiguration.h"
 #import <Foundation/Foundation.h>
+#import <AVFoundation/AVFoundation.h>
 #import <UIKit/UIKit.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -17,38 +18,84 @@
 @interface NSExtensionContext (RPBroadcastExtension)
 
 /*! @abstract Load information about the broadcasting app.
- @param bundleID Bundle identifier of the broadcasting application.
- @param displayName Display name of the broadcasting application.
- @param appIcon Optional app icon of the broadcasting application.
+    @param handler block which will be supplied a bundleID, displayName and an optional appIcon.
  */
 - (void)loadBroadcastingApplicationInfoWithCompletion:(void(^)(NSString *bundleID, NSString *displayName, UIImage * __nullable appIcon))handler;
 
 /*! @abstract Method to be called when the extension should finish.
     @param broadcastURL URL that can be used to redirect the user to the ongoing or completed broadcast. This URL is made available to the running application via a property in RPBroadcastController.
     @param broadcastConfiguration Configuration to use for generating movie clips
-    @param serviceInfo Dictionary that can be used to communicate any setup info required by the RPBroadcastProcessExtension extension process to process movie clips (typically to upload to a service). The values and keys in this dictionary are to be defined by the extension developer.
+    @param setupInfo Dictionary that can be used to share any setup information required by the upload extension. The values and keys in this dictionary are to be defined by the extension developer.
  */
-- (void)completeRequestWithBroadcastURL:(NSURL *)broadcastURL broadcastConfiguration:(RPBroadcastConfiguration *)broadcastConfiguration serviceInfo:(nullable NSDictionary <NSString *, NSObject <NSCoding> *> *)serviceInfo;
+- (void)completeRequestWithBroadcastURL:(NSURL *)broadcastURL broadcastConfiguration:(RPBroadcastConfiguration *)broadcastConfiguration setupInfo:(nullable NSDictionary <NSString *, NSObject <NSCoding> *> *)setupInfo;
+@end
 
+/*!
+ @class RPBroadcastProcessExtension
+ @abstract Base class for extensions that are responsible for handling video and audio data.
+ */
+NS_CLASS_AVAILABLE_IOS(10_0)
+@interface RPBroadcastHandler : NSObject <NSExtensionRequestHandling>
+/*! @abstract Call this method, supplying it with a dictionary defined by the service, to populate the serviceInfo property on RPBroadcastController. This can be used to communicate viewing stats or messages back to the broadcasting app.
+ @param serviceInfo Dictionary that can be passed back to the broadcasting app that may contain information about the ongoing broadcast.
+ */
+- (void)updateServiceInfo:(NSDictionary<NSString *, NSObject <NSCoding> *> *)serviceInfo;
 @end
 
 /*! 
-    @class RPBroadcastProcessExtension
-    @abstract Base class for extensions that are responsible for handling movie clips as they are recorded by ReplayKit during the broadcast flow. ReplayKit will call processMovieClipWithURL when a movie clip is available for processing.
+    @class RPBroadcastMP4ClipHandler
+    @abstract Subclass this class to handle movie clips as they are recorded by ReplayKit during the broadcast flow. ReplayKit will call processMP4ClipWithURL when a movie clip is available for processing.
  */
 NS_CLASS_AVAILABLE_IOS(10_0)
-@interface RPBroadcastMovieClipHandler : NSObject <NSExtensionRequestHandling>
-/*! @abstract Method which ReplayKit will call when a movie clip is ready for processing.
- @param movieClipURL URL that points to the location of the movie clip recorded by ReplayKit. Note that the URL may be nil in certain cases such as an error.
- @param serviceInfo Dictionary supplied by the UI extension that may contain setup information required for processing. The values in this dictionary are to be defined by the extension developer.
+@interface RPBroadcastMP4ClipHandler : RPBroadcastHandler
+/*! @abstract Method which ReplayKit will call when an MP4 movie clip is ready for processing.
+ @param mp4ClipURL URL that points to the location of the movie clip recorded by ReplayKit. Note that the URL may be nil in certain cases such as an error.
+ @param setupInfo Dictionary supplied by the UI extension that may contain setup information required for processing. The values in this dictionary are to be defined by the extension developer.
  @param finished Boolean indicating that application requested the broadcast to end.
  */
-- (void)processMovieClipWithURL:(nullable NSURL *)movieClipURL serviceInfo:(nullable NSDictionary <NSString *, NSObject *> *)serviceInfo finished:(BOOL)finished;
+- (void)processMP4ClipWithURL:(nullable NSURL *)mp4ClipURL setupInfo:(nullable NSDictionary <NSString *, NSObject *> *)setupInfo finished:(BOOL)finished;
 
 /*! @abstract Method that should be called when processing is complete.
-    @param error Optional error to communicate to ReplayKit and the host application that there was an issue with the broadcast and to stop broadcasting. Note that once this is called, regardles of the existence of an error, the current movie clip will no longer be available.
+    @param broadcastConfiguration Optional updated configuration that will be applied to the next MP4 clip.
+    @param error Optional error to communicate to ReplayKit and the host application that there was an issue with the broadcast and to stop broadcasting. Note that once this is called, regardles of the existence of an error, the current MP4 clip will no longer be available.
+ */
+- (void)finishedProcessingMP4ClipWithUpdatedBroadcastConfiguration:(nullable RPBroadcastConfiguration *)broadcastConfiguration error:(nullable NSError *)error;
+@end
+
+NS_ENUM_AVAILABLE_IOS(10_0)
+typedef NS_ENUM(NSInteger, RPSampleBufferType) {
+    RPSampleBufferTypeVideo = 1,
+    RPSampleBufferTypeAudioApp,
+    RPSampleBufferTypeAudioMic,
+};
+
+/*!
+ @class RPBroadcastSampleHandler
+ @abstract Subclass this class to handle CMSampleBuffer objects as they are captured by ReplayKit. To enable this mode of handling, set the RPBroadcastProcessMode in the extension's info.plist to RPBroadcastProcessModeSampleBuffer.
+ */
+NS_CLASS_AVAILABLE_IOS(10_0)
+@interface RPBroadcastSampleHandler : RPBroadcastHandler
+
+/*! @abstract Method is called when the RPBroadcastController startBroadcast method is called from the broadcasting application.
+    @param serviceInfo Dictionary that can be supplied by the UI extension to the sample handler.
+ */
+- (void)broadcastStartedWithSetupInfo:(nullable NSDictionary <NSString *, NSObject *> *)setupInfo;
+
+/*! @abstract Method is called when the RPBroadcastController pauseBroadcast method is called from the broadcasting application. */
+- (void)broadcastPaused;
+
+/*! @abstract Method is called when the RPBroadcastController resumeBroadcast method is called from the broadcasting application. */
+- (void)broadcastResumed;
+
+/*! @abstract Method is called when the RPBroadcastController finishBroadcast method is called from the broadcasting application. */
+- (void)broadcastFinished;
+
+/*! @abstract Method is called as video and audio data become available during a broadcast session and is delivered as CMSampleBuffer objects.
+    @param sampleBuffer CMSampleBuffer object which contains either video or audio data.
+    @param sampleBufferType Determine's the type of the sample buffer defined by the RPSampleBufferType enum.
  */
-- (void)finishedProcessingMovieClipWithUpdatedBroadcastConfiguration:(nullable RPBroadcastConfiguration *)broadcastConfiguration error:(nullable NSError *)error;
+- (void)processSampleBuffer:(CMSampleBufferRef)sampleBuffer withType:(RPSampleBufferType)sampleBufferType;
 
 @end
 NS_ASSUME_NONNULL_END
+
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPScreenRecorder.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPScreenRecorder.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPScreenRecorder.h	2016-05-23 08:15:43.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPScreenRecorder.h	2016-06-27 08:18:10.000000000 +0200
@@ -81,7 +81,7 @@
 /*! @abstract Called when recording has stopped for any reason.
  @param screenRecorder The instance of the screen recorder.
  @param error An NSError describing why recording has stopped in the RPRecordingErrorDomain.
- @param previewController If a partial movie is available before it was stopped, an instance of RPPreviewViewController will be returned.
+ @param previewViewController If a partial movie is available before it was stopped, an instance of RPPreviewViewController will be returned.
  */
 - (void)screenRecorder:(RPScreenRecorder *)screenRecorder didStopRecordingWithError:(NSError *)error previewViewController:(nullable RPPreviewViewController *)previewViewController;
 

```