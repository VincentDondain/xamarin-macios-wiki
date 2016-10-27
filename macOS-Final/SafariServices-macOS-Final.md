#SafariServices.framework

``` diff
diff -ruN /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariPageProperties.h /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariPageProperties.h
--- /Applications/Xcode81-GM.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariPageProperties.h	2016-08-13 00:31:19.000000000 -0400
+++ /Applications/Xcode81-Final.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariPageProperties.h	2016-10-06 23:21:56.000000000 -0400
@@ -16,8 +16,8 @@
 SF_CLASS_AVAILABLE_MAC_SAFARI(10_0)
 @interface SFSafariPageProperties : NSObject
 
-@property (nonatomic, readonly) NSURL *url;
-@property (nonatomic, copy, readonly) NSString *title;
+@property (nonatomic, readonly, nullable) NSURL *url;
+@property (nonatomic, copy, readonly, nullable) NSString *title;
 @property (nonatomic, readonly) BOOL usesPrivateBrowsing;
 @property (nonatomic, readonly, getter=isActive) BOOL active;
 

```