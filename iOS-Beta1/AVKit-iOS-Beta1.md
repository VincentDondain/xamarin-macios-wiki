#AVKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h	2015-10-03 02:15:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerViewController.h	2016-06-02 06:27:41.000000000 +0200
@@ -69,6 +69,12 @@
 @property (nonatomic) BOOL allowsPictureInPicturePlayback NS_AVAILABLE_IOS(9_0);
 
 /*!
+	@property	updatesNowPlayingInfoCenter
+	@abstract	Whether or not the now playing info center should be updated. Default is YES.
+ */
+@property (nonatomic) BOOL updatesNowPlayingInfoCenter NS_AVAILABLE_IOS(10_0);
+
+/*!
 	@property	delegate
 	@abstract	The receiver's delegate.
  */

```