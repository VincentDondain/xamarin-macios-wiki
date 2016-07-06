#FinderSync.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/FinderSync.framework/Headers/FinderSync.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/FinderSync.framework/Headers/FinderSync.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/FinderSync.framework/Headers/FinderSync.h	2016-06-03 02:52:17.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/FinderSync.framework/Headers/FinderSync.h	2016-06-26 17:40:40.000000000 +0200
@@ -47,7 +47,7 @@
 
 /* The extension should build a list of menu items to be displayed in the specified kind of menu. See FIFinderSyncController's -targetedURL and -selectedItemURLs. This will be called for any of the menu kinds when the target or selection is inside the directoryURLs. For FIToolbarItemMenu it will always be called, even if the target and selection are not related to the extension. The extension's principal object provides a method for each menu item's assigned action.
 
-    Specific menu item properties are used: title, action, image, and enabled. Starting in OS X 10.11: tag, state, and indentationLevel also work, and submenus are allowed.
+    Specific menu item properties are used: title, action, image, and enabled. Starting in 10.11: tag, state, and indentationLevel also work, and submenus are allowed.
  */
 - (nullable NSMenu*)menuForMenuKind:(FIMenuKind)menu;
 

```