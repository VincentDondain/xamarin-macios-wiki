#SafariServices.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariApplication.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariApplication.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariApplication.h	2016-06-27 01:42:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariApplication.h	2016-07-11 08:32:22.000000000 +0200
@@ -30,6 +30,9 @@
 /// This will cause -validateToolbarItemInWindow:completionHandler: to be called on all windows, to let the extension update enabled states or badges of its toolbar items.
 + (void)setToolbarItemsNeedUpdate;
 
+/// Opens Safari Extensions preferences and selects extension with the identifier.
++ (void)showPreferencesForExtensionWithIdentifier:(NSString *)identifier completionHandler:(void (^ _Nullable)(NSError * _Nullable error))completionHandler NS_EXTENSION_UNAVAILABLE("Not available to extensions");
+
 @end
 
 NS_ASSUME_NONNULL_END

```