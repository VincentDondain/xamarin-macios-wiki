#MapKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h	2016-06-26 18:23:58.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h	2016-07-09 11:36:07.000000000 +0200
@@ -9,17 +9,23 @@
 #import <MapKit/MKAnnotation.h>
 #import <CoreLocation/CLLocation.h>
 #import <CoreLocation/CLPlacemark.h>
+@class CNPostalAddress;
 
 NS_ASSUME_NONNULL_BEGIN
 
 NS_CLASS_AVAILABLE(10_9, 3_0) __TVOS_AVAILABLE(9_2)
 @interface MKPlacemark : CLPlacemark <MKAnnotation>
 
+- (instancetype)initWithCoordinate:(CLLocationCoordinate2D)coordinate NS_AVAILABLE(10_12, 10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+
 // An address dictionary is a dictionary in the same form as returned by 
 // ABRecordCopyValue(person, kABPersonAddressProperty).
 - (instancetype)initWithCoordinate:(CLLocationCoordinate2D)coordinate
                  addressDictionary:(nullable NSDictionary<NSString *, id> *)addressDictionary;
 
+- (instancetype)initWithCoordinate:(CLLocationCoordinate2D)coordinate
+                 postalAddress:(nonnull CNPostalAddress *)postalAddress NS_AVAILABLE(10_12, 10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_UNAVAILABLE;
+
 // To create an MKPlacemark from a CLPlacemark, call [MKPlacemark initWithPlacemark:] passing the CLPlacemark instance that is returned by CLGeocoder.
 // See CLGeocoder.h and CLPlacemark.h in CoreLocation for more information.
 

```