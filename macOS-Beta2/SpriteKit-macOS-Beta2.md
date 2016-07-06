#SpriteKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h	2016-05-27 03:54:53.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h	2016-06-26 09:10:58.000000000 +0200
@@ -1 +1 @@
-#define SK_VERSION 18064005
+#define SK_VERSION 18082000
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVideoNode.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVideoNode.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVideoNode.h	2016-05-27 03:54:53.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVideoNode.h	2016-06-26 09:10:58.000000000 +0200
@@ -11,7 +11,6 @@
 
 #if __has_include(<AVFoundation/AVPlayer.h>)
 @class AVPlayer;
-#endif
 
 
 #import <SpriteKit/SKSpriteNode.h>
@@ -24,9 +23,7 @@
 /**
  Create a video node from an AVPlayer. You can use the AVPlayer to control playback.
  */
-#if __has_include(<AVFoundation/AVPlayer.h>)
 + (SKVideoNode *)videoNodeWithAVPlayer:(AVPlayer*)player;
-#endif
 
 /**
  Create a video node from a file.
@@ -45,9 +42,7 @@
  
  Initialize a video node from an AVPlayer. You can use the AVPlayer to control playback.
  */
-#if __has_include(<AVFoundation/AVPlayer.h>)
 - (instancetype)initWithAVPlayer:(AVPlayer*)player NS_DESIGNATED_INITIALIZER;
-#endif
 
 /**
  Initialize a video node from a file.
@@ -79,3 +74,5 @@
 @end
 
 NS_ASSUME_NONNULL_END
+
+#endif

```