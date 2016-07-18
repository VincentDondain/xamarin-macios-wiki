#AVFoundation.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerLooper.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerLooper.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerLooper.h	2016-06-27 06:19:34.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerLooper.h	2016-07-10 10:02:26.000000000 +0200
@@ -47,11 +47,31 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+/*!
+ @enum AVPlayerLooperStatus
+ @abstract
+    These constants are returned by the AVPlayerLooper status property to indicate whether it can successfully accomplish looping playback.
+ @constant AVPlayerLooperStatusUnknown
+    Indicates that the status of the looper is not yet known.
+ @constant AVPlayerLooperStatusReady
+    Indicates that the looper is ready for looping playback.
+ @constant AVPlayerLooperStatusFailed
+    Indicates that the looper is not able to perform looping playback because of an error. The error is described by the value of the error property.
+ @constant AVPlayerLooperStatusCancelled
+    Indicates that the looper is no longer looping because -disableLooping was invoked.
+ */
+typedef NS_ENUM(NSInteger, AVPlayerLooperStatus) {
+    AVPlayerLooperStatusUnknown,
+    AVPlayerLooperStatusReady,
+    AVPlayerLooperStatusFailed,
+    AVPlayerLooperStatusCancelled
+};
+
 NS_CLASS_AVAILABLE(10_12, 10_0)
 @interface AVPlayerLooper : NSObject
 {
 @private
-	AVPlayerLooperInternal *_looper;
+    AVPlayerLooperInternal *_looper;
 }
 AV_INIT_UNAVAILABLE
 
@@ -100,27 +120,36 @@
  @result
     An initialized AVPlayerLooper.
  @discussion
-    The specified AVPlayerItem will be used as a template to generate at least 3 AVPlayerItem replicas and the replicas will be inserted into specified AVQueuePlayer's play queue to accomplish the looping playback. The specified AVPlayerItem should have its asset.duration property loaded beforehand so initialization would not be blocked until the duration value is known. The specified AVPlayerItem will not be used in the actual looping playback. Furthermore, AVPlayerItem replicas will be generated at initialization time so any changes made to the specified AVPlayerItem's property afterwards will not be reflected in the replicas used for looping playback. Specified CMTimeRange will limit each item loop iteration to playing within the specified time range. To play from beginning and the whole duration of the item, specify kCMTimeRangeInvalid for the range parameter. Time range will be accomplished by seeking to range start time and setting AVPlayerItem's forwardPlaybackEndTime property on the looping item replicas. Client should not modify AVQueuePlayer's play queue while AVPlayerLooper is performing the looping. AVPlayerLooper will insert the replica items before any existing items in the specified AVQueuePlayer's play queue and change the actionAtItemEnd to AVPlayerActionAtItemEndAdvance if required. AVQueuePlayer's play queue and actionAtItemEnd will be restored when -disableLooping method is called and then current looping item replicas completes playback or when AVPlayerLooper is destroyed. While AVPlayerLooper is being initialized, the specified AVQueuePlayer will be paused (rate of 0.0) if necessary and the original player rate will be restored after initialization completes. The client shall set the specified AVQueuePlayer's rate to 0 beforehand if additional set-up work needs to be performed after AVPlayerLooper initialization and before starting looping playback. An NSInvalidArgumentException will be raised if the player and template item are not specified or the template item has a 0 duration. An NSInvalidArgumentException will be raised if a valid time range has a duration of 0 or is not contained within time 0 and duration of the templateItem.
+    The specified AVPlayerItem will be used as a template to generate at least 3 AVPlayerItem replicas and the replicas will be inserted into specified AVQueuePlayer's play queue to accomplish the looping playback. The specified AVPlayerItem should have its asset's duration property loaded beforehand so looping setup work would not be blocked until the duration value is known. Otherwise, AVPlayerLooper's status property is  AVPlayerLooperStatusUnknown until the duration property is loaded. The specified AVPlayerItem will not be used in the actual looping playback. Furthermore, AVPlayerItem replicas will be generated at initialization time so any changes made to the specified AVPlayerItem's property afterwards will not be reflected in the replicas used for looping playback. Specified CMTimeRange will limit each item loop iteration to playing within the specified time range. To play from beginning and the whole duration of the item, specify kCMTimeRangeInvalid for the range parameter. Time range will be accomplished by seeking to range start time and setting AVPlayerItem's forwardPlaybackEndTime property on the looping item replicas. Client should not modify AVQueuePlayer's play queue while AVPlayerLooper is performing the looping. AVPlayerLooper will insert the replica items before any existing items in the specified AVQueuePlayer's play queue and change the actionAtItemEnd to AVPlayerActionAtItemEndAdvance if required. AVQueuePlayer's play queue and actionAtItemEnd will be restored when -disableLooping method is called and then current looping item replicas completes playback or when AVPlayerLooper is destroyed. While AVPlayerLooper is being initialized, the specified AVQueuePlayer will be paused (rate of 0.0) if necessary and the original player rate will be restored after initialization completes. The client shall set the specified AVQueuePlayer's rate to 0 beforehand if additional set-up work needs to be performed after AVPlayerLooper initialization and before starting looping playback. An NSInvalidArgumentException will be raised if the player and template item are not specified or the template item has a 0 duration. An NSInvalidArgumentException will be raised if a valid time range has a duration of 0 or is not contained within time 0 and duration of the templateItem.
  */
 - (instancetype)initWithPlayer:(AVQueuePlayer *)player templateItem:(AVPlayerItem *)itemToLoop timeRange:(CMTimeRange)loopRange NS_DESIGNATED_INITIALIZER;
 
 /*!
- @method disableLooping
+ @property status
  @abstract
-    Disables the item looping
+    The ability of the receiver to be used for looping playback.
  @discussion
-    AVPlayerLooper will stop performing player queue operations for looping and let the current looping item replica play to the end. The player's original actionAtItemEnd property will be restored afterwards.
+    The value of this property is an AVPlayerLooperStatus that indicates whether the receiver is ready for looping playback. When the value of this property is AVPlayerStatusFailed, the receiver can no longer be used for playback and a new instance needs to be created in its place. When this happens, clients can check the value of the error property to determine the nature of the failure. This property is key value observable.
  */
-- (void)disableLooping;
+@property (readonly) AVPlayerLooperStatus status;
 
 /*!
- @property loopingEnabled
+ @property error
  @abstract
-    Boolean specifying whether AVPlayerLooper is looping or not.
+    If the receiver's status is AVPlayerLooperStatusFailed, this describes the error that caused the failure.
  @discussion
-    loopingEnabled returns NO if disableLooping method is called or if an error is encountered that prevents looping playback, which can occur either when a looping item fails to become ready for playback or when a looping item fails to play to its end time. Errors arising in the former case can be discovered by observing the AVPlayer keypath @“currentItem.error”. Errors arising in the latter case can be discovered by handling the NSNotification AVPlayerItemFailedToPlayToEndTimeNotification. This property is key value observable.
+    The value of this property is a NSError that describes what caused the receiver to not be able to perform looping playback. If the receiver's status is not AVPlayerLooperStatusFailed, the value of this property is nil.
  */
-@property (nonatomic, readonly, getter=isLoopingEnabled) BOOL loopingEnabled;
+@property (readonly, nullable) NSError *error;
+
+/*!
+ @method disableLooping
+ @abstract
+    Disables the item looping
+ @discussion
+    AVPlayerLooper will stop performing player queue operations for looping and let the current looping item replica play to the end. The player's original actionAtItemEnd property will be restored afterwards. After this method is called, the value of the receiver's status property will be AVPlayerLooperStatusCancelled.
+ */
+- (void)disableLooping;
 
 /*!
  @property loopCount
@@ -129,14 +158,14 @@
  @discussion
     Starts at 0 and increments when the player starts playback of the AVPlayerItem again. This property is key value observable.
  */
-@property (nonatomic, readonly) NSInteger loopCount;
+@property (readonly) NSInteger loopCount;
 
```