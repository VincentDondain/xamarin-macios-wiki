#CoreImage.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIDetector.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIDetector.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIDetector.h	2016-07-10 10:00:07.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIDetector.h	2016-07-25 08:46:22.000000000 +0200
@@ -107,6 +107,12 @@
  valid values range: 0.0 <= CIDetectorMinFeatureSize <= 1.0. The default value is 10/(height of input image). */
 CORE_IMAGE_EXPORT NSString* const CIDetectorMinFeatureSize NS_AVAILABLE(10_8, 6_0);
 
+/* For rectangle detector, the value for this key is an integer NSNumber
+ from 1 ... 256 that represents the maximum number of features to return. 
+ valid value range: 1 <= CIDetectorMaxFeatureCount <= 256. The default value is 1.
+ */
+CORE_IMAGE_EXPORT NSString* const CIDetectorMaxFeatureCount NS_AVAILABLE(10_12, 10_0);
+
 /* The key in the options dictionary used to specify number of angles, the value for this key is one of 1, 3, 5, 7, 9, 11.*/
 CORE_IMAGE_EXPORT NSString* const CIDetectorNumberOfAngles NS_AVAILABLE(10_11, 9_0);
 
```