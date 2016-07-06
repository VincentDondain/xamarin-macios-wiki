#PreferencePanes.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PreferencePanes.framework/Headers/NSPreferencePane.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PreferencePanes.framework/Headers/NSPreferencePane.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PreferencePanes.framework/Headers/NSPreferencePane.h	2016-05-12 09:56:35.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PreferencePanes.framework/Headers/NSPreferencePane.h	2016-06-26 09:37:12.000000000 +0200
@@ -39,7 +39,7 @@
 
 #define	kNSPrefPaneHelpMenuInfoPListKey		@"NSPrefPaneHelpAnchors"
 #define	kNSPrefPaneHelpMenuTitleKey			@"title"		
-#define	kNSPrefPaneHelpMenuAnchorKey		@"anchor"
+#define	kNSPrefPaneHelpMenuAnchorKey			@"anchor"
 
 #endif
 
@@ -54,12 +54,12 @@
 	
 		//  Connect these outlets to the initial, first and last keyboard
 		//  focus chain views.  These views MUST be subviews of the main view.
-		IBOutlet NSView * __nullable	_initialKeyView;
-		IBOutlet NSView * __nullable	_firstKeyView;
-		IBOutlet NSView * __nullable	_lastKeyView;
+		IBOutlet NSView * __nullable		_initialKeyView;
+		IBOutlet NSView * __nullable		_firstKeyView;
+		IBOutlet NSView * __nullable		_lastKeyView;
 	
 		NSView * __nonnull		_mainView;
-		NSBundle * __nonnull	_bundle;
+		NSBundle * __nonnull		_bundle;
 	
 		__nullable id _reserved1;
 		__nullable id _reserved2;

```