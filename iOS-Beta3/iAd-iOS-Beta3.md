#iAd.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/MPMoviePlayerController_iAdPreroll.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/MPMoviePlayerController_iAdPreroll.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/MPMoviePlayerController_iAdPreroll.h	2016-06-29 07:12:19.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/iAd.framework/Headers/MPMoviePlayerController_iAdPreroll.h	2016-07-11 07:45:45.000000000 +0200
@@ -7,7 +7,7 @@
 
 #import <TargetConditionals.h>
 
-#if TARGET_OS_IOS
+#if TARGET_OS_IOS && TARGET_OS_EMBEDDED
 #import <MediaPlayer/MediaPlayer.h>
 
 /*!

```