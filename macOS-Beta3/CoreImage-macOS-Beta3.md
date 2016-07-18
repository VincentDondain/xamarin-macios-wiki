#CoreImage.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIRAWFilter.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIRAWFilter.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIRAWFilter.h	2016-06-26 17:49:40.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIRAWFilter.h	2016-07-09 08:58:07.000000000 +0200
@@ -47,9 +47,11 @@
 /** @const      kCIInputEVKey
  NSNumber (float) : Exposure adjustment, default = 0.0. Declared in CIFilter.h */
 
+/** NSNumber (float) : A value controlling the amount of baseline exposure applied to the image.
+ A value of 0 indicates no baseline exposure, i.e. linear response. Default varies from with camera settings. */
+CORE_IMAGE_EXPORT NSString *const kCIInputBaselineExposureKey NS_AVAILABLE(12_0, 10_0);
 
-
-/** NSNumber (float) : A value in the range of 0...1, controling the amount of boost applied to the image. 
+/** NSNumber (float) : A value in the range of 0...1, controlling the amount of boost applied to the image.
     A value of 0 indicates no boost, i.e. linear response. Default is 1, full boost. */
 CORE_IMAGE_EXPORT NSString *const kCIInputBoostKey NS_AVAILABLE(10_5, 10_0);
 
@@ -57,7 +59,9 @@
     Has no effect if the image used for initialization was not RAW. */
 CORE_IMAGE_EXPORT NSString *const kCIInputBoostShadowAmountKey NS_AVAILABLE(10_5, 10_0);
 
-
+/** NSNumber (BOOL) : Setting DisableGamutMap to YES disables gamut mapping.
+    The default value is NO. */
+CORE_IMAGE_EXPORT NSString *const kCIInputDisableGamutMapKey NS_AVAILABLE(12_0, 10_0);
 
 /** NSNumber (float): The X value of the chromaticity. You can always query this value and you'll get the current X value for neutral X,Y. */
 CORE_IMAGE_EXPORT NSString *const kCIInputNeutralChromaticityXKey NS_AVAILABLE(10_5, 10_0);

```