#CoreMotion.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMDeviceMotion.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMDeviceMotion.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMDeviceMotion.h	2016-07-10 09:50:48.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMotion.framework/Headers/CMDeviceMotion.h	2016-07-25 07:27:41.000000000 +0200
@@ -23,12 +23,12 @@
  *        accuracy of a magnetic field estimate.
  *
  */
-typedef enum {
+typedef NS_ENUM(int, CMMagneticFieldCalibrationAccuracy) {
 	CMMagneticFieldCalibrationAccuracyUncalibrated = -1,
 	CMMagneticFieldCalibrationAccuracyLow,
 	CMMagneticFieldCalibrationAccuracyMedium,
 	CMMagneticFieldCalibrationAccuracyHigh
-} CMMagneticFieldCalibrationAccuracy;
+} ;
 
 /*
  *  CMCalibratedMagneticField

```