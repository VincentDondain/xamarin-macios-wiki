#IOSurface.framework

``` diff
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOSurface.framework/Headers/IOSurfaceAPI.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOSurface.framework/Headers/IOSurfaceAPI.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOSurface.framework/Headers/IOSurfaceAPI.h	2016-08-01 23:00:48.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/IOSurface.framework/Headers/IOSurfaceAPI.h	2016-09-26 18:46:58.000000000 -0400
@@ -115,7 +115,7 @@
 extern const CFStringRef kIOSurfacePixelFormat					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);
 
 /* kIOSurfacePixelSizeCastingAllowed - If false the creator promises that there will be no pixel size casting when used on the GPU.  Default is true.  */
-extern const CFStringRef kIOSurfacePixelSizeCastingAllowed					IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_9_0);
+extern const CFStringRef kIOSurfacePixelSizeCastingAllowed					IOSFC_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
 
 CFTypeID IOSurfaceGetTypeID(void)
 	IOSFC_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_0);

```