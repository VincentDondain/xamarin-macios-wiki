#CoreImage.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIDetector.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIDetector.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIDetector.h	2016-07-10 10:00:07.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIDetector.h	2016-07-25 08:46:22.000000000 +0200
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
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilter.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilter.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilter.h	2016-07-10 07:43:13.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilter.h	2016-07-25 08:46:22.000000000 +0200
@@ -233,7 +233,7 @@
  kCIApplyOptionDefinition: the Domain of Definition of the produced image. Value is either a CIFilterShape object, or a four element NSArray defining a rectangle.
  @param  k         CIKernel of the filter
  @param  args      Array of arguments that are applied to the kernel
- @param  options   Array of additional options
+ @param  dict      Array of additional options
 */
 - (nullable CIImage *)apply:(CIKernel *)k
 				  arguments:(nullable NSArray *)args
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilterGenerator.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilterGenerator.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilterGenerator.h	2016-07-09 08:58:07.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreImage.framework/Headers/CIFilterGenerator.h	2016-07-25 08:46:22.000000000 +0200
@@ -76,7 +76,7 @@
  @param      targetKey The key that you assigned the source object to.
 */
 - (void)disconnectObject:(id)sourceObject
-                 withKey:(NSString *)key
+                 withKey:(NSString *)sourceKey
                 toObject:(id)targetObject
                  withKey:(NSString *)targetKey;
 

```