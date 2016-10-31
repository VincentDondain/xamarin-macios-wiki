#IntentsUI.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/IntentsUI.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/IntentsUI.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/IntentsUI.h	2016-09-28 09:42:47.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/IntentsUI.h	2016-10-22 03:52:55.000000000 +0200
@@ -13,7 +13,6 @@
 //! Project version string for IntentsUI.
 FOUNDATION_EXPORT const unsigned char IntentsUIVersionString[];
 
-// In this header, you should import all the public headers of your framework using statements like #import <IntentsUI/PublicHeader.h>
 #import <IntentsUI/INImage+IntentsUI.h>
 #import <IntentsUI/INUIHostedViewControlling.h>
 #import <IntentsUI/INUIHostedViewSiriProviding.h>

```