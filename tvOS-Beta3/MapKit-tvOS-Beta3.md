#MapKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h	2016-06-27 06:34:52.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h	2016-07-10 12:48:46.000000000 +0200
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