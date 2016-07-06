#AVKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerView.h	2015-08-23 04:05:34.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVKit.framework/Headers/AVPlayerView.h	2016-06-02 03:13:50.000000000 +0200
@@ -100,7 +100,7 @@
 	@property	actionPopUpButtonMenu
 	@abstract	Clients can set this property in order to show an action pop up button. Default is nil.
  */
-@property (nullable) NSMenu *actionPopUpButtonMenu;
+@property (nullable) IBOutlet NSMenu *actionPopUpButtonMenu;
 
 /*!
 	@property	showsFullScreenToggleButton

```