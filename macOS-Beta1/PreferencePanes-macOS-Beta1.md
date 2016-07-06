#PreferencePanes.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/PreferencePanes.framework/Headers/NSPreferencePane.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PreferencePanes.framework/Headers/NSPreferencePane.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/PreferencePanes.framework/Headers/NSPreferencePane.h	2015-08-23 04:16:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/PreferencePanes.framework/Headers/NSPreferencePane.h	2016-05-12 09:56:35.000000000 +0200
@@ -19,6 +19,10 @@
 extern NSString * __nonnull const 	NSPreferencePaneDoUnselectNotification;
 extern NSString * __nonnull const 	NSPreferencePaneCancelUnselectNotification;
 
+extern NSString * __nonnull const	NSPreferencePaneSwitchToPaneNotification;
+extern NSString * __nonnull const	NSPreferencePrefPaneIsAvailableNotification;
+extern NSString * __nonnull const	NSPreferencePaneUpdateHelpMenuNotification;
+
 // Help Menu support
 APPKIT_EXTERN NSString * __nonnull const				NSPrefPaneHelpMenuInfoPListKey;
 APPKIT_EXTERN NSString * __nonnull const				NSPrefPaneHelpMenuTitleKey;

```