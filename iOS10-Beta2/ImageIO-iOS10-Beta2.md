#ImageIO.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageDestination.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageDestination.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageDestination.h	2016-05-28 06:38:30.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageDestination.h	2016-06-27 06:12:22.000000000 +0200
@@ -51,6 +51,13 @@
 
 IMAGEIO_EXTERN const CFStringRef kCGImageDestinationEmbedThumbnail  IMAGEIO_AVAILABLE_STARTING(__MAC_10_10, __IPHONE_8_0);
 
+
+/* Create an image using a colorspace, that has is compatible with older devices
+ * The value should be kCFBooleanTrue or kCFBooleanFalse
+ * Defaults to kCFBooleanFalse = don't do any color conversion
+ */
+IMAGEIO_EXTERN const CFStringRef kCGImageDestinationOptimizeColorForSharing  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_9_3);
+
 CF_ASSUME_NONNULL_END
 
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageProperties.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageProperties.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageProperties.h	2016-05-28 06:17:12.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ImageIO.framework/Headers/CGImageProperties.h	2016-06-27 05:51:50.000000000 +0200
@@ -379,6 +379,26 @@
 IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGLocalizedCameraModel  IMAGEIO_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_4_0);
 IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGCameraSerialNumber  IMAGEIO_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_4_0);
 IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGLensInfo  IMAGEIO_AVAILABLE_STARTING(__MAC_10_5, __IPHONE_4_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGBlackLevel  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGWhiteLevel  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGCalibrationIlluminant1  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGCalibrationIlluminant2  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGColorMatrix1  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGColorMatrix2  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGCameraCalibration1  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGCameraCalibration2  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGAsShotNeutral  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGAsShotWhiteXY  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGBaselineExposure  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGBaselineNoise  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGBaselineSharpness  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGPrivateData  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGCameraCalibrationSignature  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGProfileCalibrationSignature  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGNoiseProfile  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGWarpRectilinear  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGWarpFisheye  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
+IMAGEIO_EXTERN const CFStringRef  kCGImagePropertyDNGFixVignetteRadial  IMAGEIO_AVAILABLE_STARTING(__MAC_10_12, __IPHONE_10_0);
 
 
 /* Possible keys for kCGImagePropertyCIFFDictionary */

```