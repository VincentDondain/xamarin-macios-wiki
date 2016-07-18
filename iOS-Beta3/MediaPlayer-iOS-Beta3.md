#MediaPlayer.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h	2016-07-11 14:34:21.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MediaPlayer.framework/Headers/MPMediaItem.h	2016-07-11 07:29:02.000000000 +0200
@@ -153,6 +153,9 @@
 MP_EXTERN NSString * const MPMediaItemPropertyBookmarkTime NS_AVAILABLE_IOS(6_0);
 @property (nonatomic, readonly) NSTimeInterval bookmarkTime NS_AVAILABLE_IOS(7_0);
 
+MP_EXTERN NSString * const MPMediaItemPropertyDateAdded NS_AVAILABLE_IOS(10_0);
+@property (nonatomic, readonly) NSDate *dateAdded NS_AVAILABLE_IOS(10_0);
+
 @end
 
 //-----------------------------------------------------

```