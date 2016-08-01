#AVFoundation.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h	2016-07-10 10:02:26.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoSettings.h	2016-07-25 07:40:26.000000000 +0200
@@ -165,7 +165,9 @@
 	 */
 	AVF_EXPORT NSString *const AVVideoAllowFrameReorderingKey /* NSNumber (BOOL) */							 NS_AVAILABLE(10_10, 7_0);
 
-	AVF_EXPORT NSString *const AVVideoProfileLevelKey /* NSString, H.264 only, one of: */                    NS_AVAILABLE(10_8, 4_0);
+	AVF_EXPORT NSString *const AVVideoProfileLevelKey /* NSString, profile/level constants are specific to a particular encoder, one of: */               NS_AVAILABLE(10_8, 4_0);
+
+
 		AVF_EXPORT NSString *const AVVideoProfileLevelH264Baseline30 /* Baseline Profile Level 3.0 */        NS_AVAILABLE(10_8, 4_0);
 		AVF_EXPORT NSString *const AVVideoProfileLevelH264Baseline31 /* Baseline Profile Level 3.1 */        NS_AVAILABLE(10_8, 4_0);
         AVF_EXPORT NSString *const AVVideoProfileLevelH264Baseline41 /* Baseline Profile Level 4.1 */        NS_AVAILABLE(10_8, 5_0);

```