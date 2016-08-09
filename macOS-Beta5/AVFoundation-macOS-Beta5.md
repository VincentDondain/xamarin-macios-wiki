#AVFoundation.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetResourceLoader.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetResourceLoader.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetResourceLoader.h	2016-07-25 07:52:57.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetResourceLoader.h	2016-08-05 07:54:32.000000000 +0200
@@ -42,6 +42,10 @@
 				An object conforming to the AVAssetResourceLoaderDelegate protocol.
  @param			delegateQueue
 				A dispatch queue on which all delegate methods will be invoked.
+ @discussion
+  If you employ an AVAssetResourceLoader delegate that loads media data for playback, you should set the value of your AVPlayer’s automaticallyWaitsToMinimizeStalling property to NO. Allowing the value of automaticallyWaitsToMinimizeStalling to remain YES — its default value — when an AVAssetResourceLoader delegate is used for the loading of media data can result in poor start-up times for playback and poor recovery from stalls, because the behaviors provided by AVPlayer when automaticallyWaitsToMinimizeStalling has a value of YES depend on predictions of the future availability of media data that that do not function as expected when data is loaded via a client-controlled means, using the AVAssetResourceLoader delegate interface.
+
+  You can allow the value of automaticallyWaitsToMinimizeStalling to remain YES if you use an AVAssetResourceLoader delegate to manage content keys for FairPlay Streaming, to provide dynamically-generated master playlists for HTTP Live Streaming, or to respond to authentication challenges, but not to load media data for playback.
 */
 - (void)setDelegate:(nullable id <AVAssetResourceLoaderDelegate>)delegate queue:(nullable dispatch_queue_t)delegateQueue;
 
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayer.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayer.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayer.h	2016-07-27 05:35:54.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayer.h	2016-08-05 07:30:59.000000000 +0200
@@ -380,13 +380,18 @@
  
  When this property is YES, whenever 1) the rate is set from zero to non-zero or 2) the playback buffer becomes empty and playback stalls, the player will attempt to determine if, at the specified rate, its currentItem will play to the end without interruptions. Should it determine that such interruptions would occur and these interruptions can be avoided by delaying the start or resumption of playback, the value of timeControlStatus will become AVPlayerTimeControlStatusWaitingToPlayAtSpecifiedRate and playback will start automatically when the likelihood of stalling has been minimized.
  
- You may want to set this property to NO when you need precise control over playback start times, e.g., when synchronizing multiple instances of AVPlayer. If the value of this property is NO, reasonForWaitingToPlay cannot assume a value of AVPlayerWaitingToMinimizeStallsReason.
+ You may want to set this property to NO when you need precise control over playback start times, e.g., when synchronizing multiple instances of AVPlayer, and you should set it to NO if you use an AVAssetResourceLoader delegate to load media data (more on this below). If the value of this property is NO, reasonForWaitingToPlay cannot assume a value of AVPlayerWaitingToMinimizeStallsReason.
  This implies that setting rate to a non-zero value in AVPlayerTimeControlStatusPaused will cause playback to start immediately as long as the playback buffer is not empty. When the playback buffer becomes empty during AVPlayerTimeControlStatusPlaying and playback stalls, playback state will switch to AVPlayerTimeControlStatusPaused and the rate will become 0.0.
  
  Changing the value of this property to NO while the value of timeControlStatus is AVPlayerTimeControlStatusWaitingToPlayAtSpecifiedRate with a reasonForWaitingToPlay of AVPlayerWaitingToMinimizeStallsReason will cause the player to attempt playback at the specified rate immediately.
  
  For clients linked against iOS 10.0 and running on that version or later or linked against OS X 10.12 and running on that version or later, the default value of this property is YES.
- In versions of iOS prior to iOS 10.0 and versions of OS X prior to 10.12, this property is unavailable, and the behavior of the AVPlayer corresponds to the type of content being played. For streaming content, including HTTP Live Streaming, the AVPlayer acts as if automaticallyWaitsToMinimizeStalling is YES. For file-based content, including file-based content accessed via progressive http download, the AVPlayer acts as if automaticallyWaitsToMinimizeStalling is NO. */
+ In versions of iOS prior to iOS 10.0 and versions of OS X prior to 10.12, this property is unavailable, and the behavior of the AVPlayer corresponds to the type of content being played. For streaming content, including HTTP Live Streaming, the AVPlayer acts as if automaticallyWaitsToMinimizeStalling is YES. For file-based content, including file-based content accessed via progressive http download, the AVPlayer acts as if automaticallyWaitsToMinimizeStalling is NO.
+
+ If you employ an AVAssetResourceLoader delegate that loads media data for playback, you should set the value of your AVPlayer’s automaticallyWaitsToMinimizeStalling property to NO. Allowing the value of automaticallyWaitsToMinimizeStalling to remain YES when an AVAssetResourceLoader delegate is used for the loading of media data can result in poor start-up times for playback and poor recovery from stalls, because the behaviors provided by AVPlayer when automaticallyWaitsToMinimizeStalling has a value of YES depend on predictions of the future availability of media data that that do not function as expected when data is loaded via a client-controlled means, using the AVAssetResourceLoader delegate interface.
+
+ You can allow the value of automaticallyWaitsToMinimizeStalling to remain YES if you use an AVAssetResourceLoader delegate to manage content keys for FairPlay Streaming, to provide dynamically-generated master playlists for HTTP Live Streaming, or to respond to authentication challenges, but not to load media data for playback.
+*/
 
 @property (nonatomic) BOOL automaticallyWaitsToMinimizeStalling NS_AVAILABLE(10_12, 10_0);
 
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h	2016-07-25 07:40:26.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h	2016-08-05 07:31:00.000000000 +0200
@@ -165,9 +165,7 @@
 	 */
 	AVF_EXPORT NSString *const AVVideoAllowFrameReorderingKey /* NSNumber (BOOL) */							 NS_AVAILABLE(10_10, 7_0);
 
-	AVF_EXPORT NSString *const AVVideoProfileLevelKey /* NSString, profile/level constants are specific to a particular encoder, one of: */               NS_AVAILABLE(10_8, 4_0);
-
-
+	AVF_EXPORT NSString *const AVVideoProfileLevelKey /* NSString, H.264 only, one of: */                    NS_AVAILABLE(10_8, 4_0);
 		AVF_EXPORT NSString *const AVVideoProfileLevelH264Baseline30 /* Baseline Profile Level 3.0 */        NS_AVAILABLE(10_8, 4_0);
 		AVF_EXPORT NSString *const AVVideoProfileLevelH264Baseline31 /* Baseline Profile Level 3.1 */        NS_AVAILABLE(10_8, 4_0);
         AVF_EXPORT NSString *const AVVideoProfileLevelH264Baseline41 /* Baseline Profile Level 4.1 */        NS_AVAILABLE(10_8, 5_0);

```