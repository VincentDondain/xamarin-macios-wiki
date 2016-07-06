#NetFS.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/NetFS.framework/Headers/NetFS.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/NetFS.framework/Headers/NetFS.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/NetFS.framework/Headers/NetFS.h	2015-08-23 01:15:38.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/NetFS.framework/Headers/NetFS.h	2016-05-11 15:52:20.000000000 +0200
@@ -223,6 +223,8 @@
  *     and we've always supported NFS submounts, so we continue to do so)
  *     the kNetFSAllowSubMountsKey has no effect, as there's no notion of
  *     submounts
+ * 4)  kNetFSOpenURLMountKey is set to true to indicate that the mount is a
+ *     result of an "openURL" event, and as such may be subject to auto-quarantine.
  */
 //#define kNetFSNoUserPreferencesKey	CFSTR("NoUserPreferences")	/* defined for GetServerInfo above */
 #define kNetFSPasswordKey		CFSTR("Password")
@@ -231,6 +233,7 @@
 #define kNetFSMountFlagsKey		CFSTR("MountFlags")
 #define kNetFSAllowSubMountsKey		CFSTR("AllowSubMounts")
 #define kNetFSMountAtMountDirKey	CFSTR("MountAtMountDir")
+#define kNetFSOpenURLMountKey           CFSTR("OpenURLMount")
 
 /*
  * Dictionary keys for the mount information dictionary returned by

```