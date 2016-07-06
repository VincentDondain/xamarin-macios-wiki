#ReplayKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h	2016-05-25 05:35:09.000000000 +0200
@@ -0,0 +1,94 @@
+//
+//  RPBroadcast.h
+//  ReplayKit
+//
+//  The following guidelines can be followed to add broadcasting capabilities to an application:
+//
+//  Use the RPScreenRecorder singleton to enable the microphone and front-facing camera recording.
+//
+//  Load an instance of RPBroadcastActivityViewController and present it when the user intends to start 	broadcasting. This will present a view controller thats allows the user to select from the broadcast servies available on the device. Selecting a broadcast service presents the service’s UI to the user and allows the user to sign-in and setup their broadcast.
+//
+//  Once setup with the service is complete, an RPBroadcastController instance will be provided via the RPBroadcastActivityViewControllerDelegate protocol. This controller can be used to start, pause and finish the broadcast.
+//
+//  RPBroadcastController will have an NSDictionary instance in its serviceInfo property which will contain a URL  to their broadcast (which can be provided to the user to share prior to starting a broadcast), as well as other optional meta data the service may wish to provide.
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <UIKit/UIKit.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@protocol RPBroadcastActivityViewControllerDelegate;
+@protocol RPBroadcastControllerDelegate;
+@class RPBroadcastController;
+
+/*! @class RPBroadcastActivityViewController
+ @abstract View controller that presents the user with a list of broadcast services installed on the device.
+ */
+NS_CLASS_AVAILABLE_IOS(10_0)
+@interface RPBroadcastActivityViewController : UIViewController
+
+/*  @abstract Loads a RPBroadcastActivityViewController instance and returns it in the handler block.
+ 
+ The view controller will present the user with a list of broadcast services available on the device and allow the user to set up a broadcast with the service through the service's UI.
+ 
+ The RPBroadcastActivityViewController can be presented using [UIViewController presentViewController:animated:completion:] and should be dismissed when the delegate's broadcastActivityViewController:didFinishWithBroadcastController:error: method is called.
+ 
+ @param broadcastActivityViewController The RPBroadcastActivityViewController which can be presented.
+ @param error Optional error in the RPRecordingErrorCode domain which is supplied in the event the view controller could not be loaded.
+ */
++ (void)loadBroadcastActivityViewControllerWithHandler:(void(^)(RPBroadcastActivityViewController * __nullable broadcastActivityViewController, NSError * __nullable error))handler;
+
+/*  @abstract Delegate that is notified when the activity view controller is complete. */
+@property (nonatomic, weak, nullable) id<RPBroadcastActivityViewControllerDelegate> delegate;
+@end
+
+@protocol RPBroadcastActivityViewControllerDelegate <NSObject>
+
+/*  @abstract Called when the view controller is finished.
+ @param broadcastActivityViewController The view controller instance.
+ @param broadcastController An RPBroadcastController instance that can be used to start and stop broadcasts to a user selected service.
+ @param error Optional error in the RPRecordingErrorCode domain. A nil error signifies that the user has successfully set up the broadcast with a broadcast service and is ready to start broadcasting.
+ */
+- (void)broadcastActivityViewController:(RPBroadcastActivityViewController *)broadcastActivityViewController didFinishWithBroadcastController:(nullable RPBroadcastController *)broadcastController error:(nullable NSError *)error;
+@end
+
+/*! @class RPBroadcastController
+ @abstract Available once a user has successfully initiated a broadcast using an RPBroadcastActivityViewController. Can be used to start, pause and stop a broadcast.
+ */
+NS_CLASS_AVAILABLE_IOS(10_0)
+@interface RPBroadcastController : NSObject
+/*  @abstract Indicates whether the controller is currently broadcasting. */
+@property (nonatomic, readonly, getter=isBroadcasting) BOOL broadcasting;
+/*  @abstract URL that can be used to redirect the user to the on-going or completed broadcast. */
+@property (nonatomic, readonly) NSURL *broadcastURL;
+/*  @abstract Delegate which will be notified when an error occurs during broadcast. */
+@property (nonatomic, weak) id<RPBroadcastControllerDelegate> broadcastControllerDelegate;
+
+/*  @abstract Start the broadcast.
+ @param error Optional error in the RPRecordingErrorCode domain. A nil error signifies that broadcasting has started successfully.
+ */
+- (void)startBroadcastWithHandler:(void(^)(NSError * __nullable error))handler;
+
+/*  @abstract Pause the broadcast. The broadcast will pause immediately. */
+- (void)pauseBroadcast;
+
+/*  @abstract Resumes the broadcast. The broadcast will resume immediately. */
+- (void)resumeBroadcast;
+
+/*  @abstract Finish the broadcast.
+ @param error Optional error in the RPRecordingErrorCode domain. A nil error signifies that broadcasting has finished successfully.
+ */
+- (void)finishBroadcastWithHandler:(void(^)(NSError * __nullable error))handler;
+@end
+
+/*  @abstract Called when broadcasting finishes due to an error.
+ @param broadcastController The controller instance.
+ @param error Required error in the RPRecordingErrorCode domain.
+ */
+@protocol RPBroadcastControllerDelegate <NSObject>
+- (void)broadcastController:(RPBroadcastController *)broadcastController didFinishWithError:(NSError * __nullable)error;
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastConfiguration.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastConfiguration.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastConfiguration.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastConfiguration.h	2016-05-25 05:50:39.000000000 +0200
@@ -0,0 +1,14 @@
+//
+//  RPBroadcastConfiguration.h
+//  ReplayKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+NS_CLASS_AVAILABLE_IOS(10_0)
+@interface RPBroadcastConfiguration : NSObject <NSCoding, NSSecureCoding>
+@property (nonatomic, assign) NSTimeInterval clipDuration;
+@property (nonatomic, strong, nullable) NSDictionary <NSNumber *, NSObject <NSCoding, NSSecureCoding> *> *videoCompressionProperties;
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastExtension.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastExtension.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastExtension.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcastExtension.h	2016-05-25 05:50:39.000000000 +0200
@@ -0,0 +1,54 @@
+//
+//  RPBroadcastExtension.h
+//  ReplayKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import "RPBroadcastConfiguration.h"
+#import <Foundation/Foundation.h>
+#import <UIKit/UIKit.h>
+
+NS_ASSUME_NONNULL_BEGIN
+/*! 
+    @category NSExtensionContext (RPBroadcastExtension)
+    @abstract Category which defines the method to call from on an extension context object when user interaction is complete during the broadcast setup flow.
+ */
+@interface NSExtensionContext (RPBroadcastExtension)
+
+/*! @abstract Load information about the broadcasting app.
+ @param bundleID Bundle identifier of the broadcasting application.
+ @param displayName Display name of the broadcasting application.
+ @param appIcon Optional app icon of the broadcasting application.
+ */
+- (void)loadBroadcastingApplicationInfoWithCompletion:(void(^)(NSString *bundleID, NSString *displayName, UIImage * __nullable appIcon))handler;
+
+/*! @abstract Method to be called when the extension should finish.
+    @param broadcastURL URL that can be used to redirect the user to the ongoing or completed broadcast. This URL is made available to the running application via a property in RPBroadcastController.
+    @param broadcastConfiguration Configuration to use for generating movie clips
+    @param serviceInfo Dictionary that can be used to communicate any setup info required by the RPBroadcastProcessExtension extension process to process movie clips (typically to upload to a service). The values and keys in this dictionary are to be defined by the extension developer.
+ */
+- (void)completeRequestWithBroadcastURL:(NSURL *)broadcastURL broadcastConfiguration:(RPBroadcastConfiguration *)broadcastConfiguration serviceInfo:(nullable NSDictionary <NSString *, NSObject <NSCoding> *> *)serviceInfo;
+
+@end
+
+/*! 
+    @class RPBroadcastProcessExtension
+    @abstract Base class for extensions that are responsible for handling movie clips as they are recorded by ReplayKit during the broadcast flow. ReplayKit will call processMovieClipWithURL when a movie clip is available for processing.
+ */
+NS_CLASS_AVAILABLE_IOS(10_0)
+@interface RPBroadcastMovieClipHandler : NSObject <NSExtensionRequestHandling>
+/*! @abstract Method which ReplayKit will call when a movie clip is ready for processing.
+ @param movieClipURL URL that points to the location of the movie clip recorded by ReplayKit. Note that the URL may be nil in certain cases such as an error.
+ @param serviceInfo Dictionary supplied by the UI extension that may contain setup information required for processing. The values in this dictionary are to be defined by the extension developer.
+ @param finished Boolean indicating that application requested the broadcast to end.
+ */
+- (void)processMovieClipWithURL:(nullable NSURL *)movieClipURL serviceInfo:(nullable NSDictionary <NSString *, NSObject *> *)serviceInfo finished:(BOOL)finished;
+
+/*! @abstract Method that should be called when processing is complete.
+    @param error Optional error to communicate to ReplayKit and the host application that there was an issue with the broadcast and to stop broadcasting. Note that once this is called, regardles of the existence of an error, the current movie clip will no longer be available.
+ */
+- (void)finishedProcessingMovieClipWithUpdatedBroadcastConfiguration:(nullable RPBroadcastConfiguration *)broadcastConfiguration error:(nullable NSError *)error;
+
+@end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPError.h	2015-10-03 02:28:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPError.h	2016-05-25 05:50:39.000000000 +0200
@@ -17,5 +17,7 @@
     RPRecordingErrorFailed = -5804, // Failed during recording
     RPRecordingErrorInsufficientStorage = -5805, // Insufficient storage for recording.
     RPRecordingErrorInterrupted = -5806, // Recording interrupted by other app
-    RPRecordingErrorContentResize = -5807 // Recording interrupted by multitasking and Content Resizing
+    RPRecordingErrorContentResize = -5807, // Recording interrupted by multitasking and Content Resizing
+    RPRecordingErrorBroadcastInvalidSession = -5808, // Attempted to start a broadcast without a prior session
+    RPRecordingErrorSystemDormancy = -5809 // Recording was forced to end when user pressed the power button
 };
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPPreviewViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPPreviewViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPPreviewViewController.h	2015-10-03 02:28:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPPreviewViewController.h	2016-05-25 05:50:39.000000000 +0200
@@ -7,6 +7,13 @@
 
 #import <UIKit/UIKit.h>
 
+NS_ENUM_AVAILABLE_IOS(10_0)
+typedef NS_ENUM(NSInteger, RPPreviewViewControllerMode) {
+    RPPreviewViewControllerModePreview,
+    RPPreviewViewControllerModeShare
+}; __IOS_PROHIBITED
+
+
 NS_CLASS_AVAILABLE_IOS(9_0)
 NS_ASSUME_NONNULL_BEGIN
 /*! @class RPPreviewViewController
@@ -16,6 +23,7 @@
 
 @interface RPPreviewViewController : UIViewController
 @property (nonatomic, weak, nullable) id<RPPreviewViewControllerDelegate>previewControllerDelegate;
+@property (nonatomic, assign) RPPreviewViewControllerMode mode __IOS_PROHIBITED __TVOS_AVAILABLE(10_0);  // Set
 @end
 
 @protocol RPPreviewViewControllerDelegate <NSObject>
@@ -24,6 +32,6 @@
 - (void)previewControllerDidFinish:(RPPreviewViewController *)previewController;
 
 /* @abstract Called when the view controller is finished and returns a set of activity types that the user has completed on the recording. The built in activity types are listed in UIActivity.h. */
-- (void)previewController:(RPPreviewViewController *)previewController didFinishWithActivityTypes:(NSSet <NSString *> *)activityTypes;
+- (void)previewController:(RPPreviewViewController *)previewController didFinishWithActivityTypes:(NSSet <NSString *> *)activityTypes __TVOS_PROHIBITED;
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPScreenRecorder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPScreenRecorder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPScreenRecorder.h	2015-10-03 02:28:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPScreenRecorder.h	2016-05-23 08:15:43.000000000 +0200
@@ -2,9 +2,15 @@
 //  RPScreenRecorder.h
 //  ReplayKit
 //
-//  ReplayKit is a high level framework that can be used to add video and audio recording capabilities to an application. An application supplied user interface can use the RPScreenRecorder singleton to start and stop recording. Once recording is finished, the framework will vend an instance of RPPreviewViewController that can be presented using [UIViewController presentViewController:animated:completion:]. The view controller allows the user to preview, trim and share the movie.
+//  ReplayKit is a high level framework that can be used to add video and audio recording and broadcast capabilities to an application. An application supplied user interface can use the RPScreenRecorder singleton to start and stop recording or broadcasting.
 //
-//  Copyright © 2015 Apple Inc. All rights reserved.
+//  Optionally the framework allows the user to also record microphone content as well as content from the front facing camera.
+//
+//  When local recording stops, the framework will vend an instance of RPPreviewViewController that can be presented using [UIViewController presentViewController:animated:completion:]. The view controller allows the user to preview, trim and share the movie.
+//
+//  When broadcasting stops, the framework will return a url that can be used to view a broadcast.
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -14,6 +20,7 @@
 
 NS_CLASS_AVAILABLE_IOS(9_0)
 @protocol RPScreenRecorderDelegate;
+@class RPBroadcastActivityViewController;
 
 /*! @class RPScreenRecorder
  @abstract Singleton class used to control app recording.
@@ -23,17 +30,24 @@
 /* @abstract Shared instance of the screen recorder. */
 + (RPScreenRecorder *)sharedRecorder;
 
-- (nullable instancetype) init __attribute__((unavailable("use sharedRecorder instead")));
-+ (nullable instancetype) new __attribute__((unavailable("use sharedRecorder instead")));
+- (instancetype)init NS_UNAVAILABLE; // Use sharedRecorder instead
 
-/*! @abstract Starts app recording with a completion handler. Note that before recording actually starts, the user may be prompted with UI to confirm recording.
+/*! 
+ Deprecated. Use startRecordingWithHandler: instead.
+ 
+ @abstract Starts app recording with a completion handler. Note that before recording actually starts, the user may be prompted with UI to confirm recording.
  @param microphoneEnabled Determines whether the microphone input should be included in the recorded movie audio.
  @result handler Called after user interactions are complete. Will be passed an optional NSError in the RPRecordingErrorDomain domain if there was an issue starting the recording.
  */
-- (void)startRecordingWithMicrophoneEnabled:(BOOL)microphoneEnabled handler:(nullable void(^)(NSError * __nullable error))handler;
+- (void)startRecordingWithMicrophoneEnabled:(BOOL)microphoneEnabled handler:(nullable void(^)(NSError * __nullable error))handler NS_DEPRECATED_IOS(9_0, 10_0);
+
+/*! @abstract Starts app recording with a completion handler. Note that before recording actually starts, the user may be prompted with UI to confirm recording.
+ @result handler Called after user interactions are complete. Will be passed an optional NSError in the RPRecordingErrorDomain domain if there was an issue starting the recording.
+ */
+- (void)startRecordingWithHandler:(nullable void(^)(NSError * __nullable error))handler NS_AVAILABLE_IOS(10_0);
 
 /*! @abstract Stops app recording with a completion handler.
- @result handler Called when the movie is ready. Will return an instance of RPPreviewViewController on success which should be presested using [UIViewController presentViewController:animated:completion:]. Will be passed an optional NSError in the RPRecordingErrorDomain domain if there was an issue stopping the recording.
+ @result handler Called when the movie is ready. Will return an instance of RPPreviewViewController on success which should be presented using [UIViewController presentViewController:animated:completion:]. Will be passed an optional NSError in the RPRecordingErrorDomain domain if there was an issue stopping the recording.
  */
 - (void)stopRecordingWithHandler:(nullable void(^)(RPPreviewViewController * __nullable previewViewController, NSError * __nullable error))handler;
 
@@ -44,14 +58,20 @@
 /* @abstract Delegate instance for RPScreenRecorder. */
 @property (nonatomic, weak, nullable) id<RPScreenRecorderDelegate> delegate;
 
+/* @abstract Check if ReplayKit is available on the device. Implement the screenRecorderDidChangeAvailability: on the delegate to listen for changes to this property. Can be used for key value observing. */
+@property (nonatomic, readonly, getter=isAvailable) BOOL available;
+
 /* @abstract Check if a recording session is in progress. Can be used for key value observing. */
 @property (nonatomic, readonly, getter=isRecording) BOOL recording;
 
-/* @abstract Check if microphone is enabled during recording. This can not be used to enable the microphone during a recording session - use startRecordingWithMicrophoneEnabled:withHandler: for that scenario. Can be used for key value observing. */
-@property (nonatomic, readonly, getter=isMicrophoneEnabled) BOOL microphoneEnabled;
+/* @abstract Specify or query whether the microphone should be enabled during recording. Can be used for key value observing. Default is NO. */
+@property (nonatomic, getter=isMicrophoneEnabled) BOOL microphoneEnabled __TVOS_PROHIBITED;
 
-/* @abstract Check if screen recording is available. Implement the screenRecorderDidChangeAvailability: on the delegate to listen for changes to this property. Can be used for key value observing. */
-@property (nonatomic, readonly, getter=isAvailable) BOOL available;
+/* @abstract Specify or query whether the camera should be enabled during recording. Can be used for key value observing. Default is NO. */
+@property (nonatomic, getter=isCameraEnabled) BOOL cameraEnabled NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
+
+/* @abstract A UIView instance that renders the front facing camera contents. This will be nil if the camera has not been enabled */
+@property (nonatomic, readonly, nullable) UIView *cameraPreviewView NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/ReplayKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/ReplayKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/ReplayKit.h	2015-10-03 02:28:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/ReplayKit.h	2016-05-25 05:50:39.000000000 +0200
@@ -7,8 +7,10 @@
 
 #import <UIKit/UIKit.h>
 
-#import <ReplayKit/RPPreviewViewController.h>
 #import <ReplayKit/RPScreenRecorder.h>
+#import <ReplayKit/RPPreviewViewController.h>
+#import <ReplayKit/RPBroadcast.h>
+#import <ReplayKit/RPBroadcastExtension.h>
 #import <ReplayKit/RPError.h>
 
 

```