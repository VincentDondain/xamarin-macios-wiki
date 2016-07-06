#MapKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKAnnotationView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKAnnotationView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKAnnotationView.h	2016-02-26 17:20:10.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKAnnotationView.h	2016-05-23 00:32:38.000000000 +0200
@@ -28,14 +28,15 @@
 @protocol MKAnnotation;
 
 #if TARGET_OS_IPHONE
-MK_CLASS_AVAILABLE(NA, 3_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(NA, 3_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKAnnotationView : UIView
 #else
-MK_CLASS_AVAILABLE(10_9, NA)
+NS_CLASS_AVAILABLE(10_9, NA)
 @interface MKAnnotationView : NSView
 #endif
 
-- (instancetype)initWithAnnotation:(nullable id <MKAnnotation>)annotation reuseIdentifier:(nullable NSString *)reuseIdentifier;
+- (instancetype)initWithAnnotation:(nullable id <MKAnnotation>)annotation reuseIdentifier:(nullable NSString *)reuseIdentifier NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
 
 @property (nonatomic, readonly, nullable) NSString *reuseIdentifier;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKCircle.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKCircle.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKCircle.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKCircle.h	2016-06-01 05:05:44.000000000 +0200
@@ -12,7 +12,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKCircle : MKShape <MKOverlay>
 
 + (instancetype)circleWithCenterCoordinate:(CLLocationCoordinate2D)coord
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKCircleRenderer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKCircleRenderer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKCircleRenderer.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKCircleRenderer.h	2016-06-01 05:05:44.000000000 +0200
@@ -10,7 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKCircleRenderer : MKOverlayPathRenderer
 
 - (instancetype)initWithCircle:(MKCircle *)circle;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKCircleView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKCircleView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKCircleView.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKCircleView.h	2016-06-01 05:05:44.000000000 +0200
@@ -11,7 +11,7 @@
 #import <MapKit/MKOverlayPathView.h>
 
 // Prefer MKCircleRenderer
-MK_CLASS_AVAILABLE(NA, 4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(NA, 4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface MKCircleView : MKOverlayPathView
 
 - (instancetype)initWithCircle:(MKCircle *)circle NS_DEPRECATED_IOS(4_0, 7_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDirections.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDirections.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDirections.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDirections.h	2016-06-01 05:05:44.000000000 +0200
@@ -16,7 +16,7 @@
 typedef void (^MKDirectionsHandler)(MKDirectionsResponse * __nullable response, NSError * __nullable error);
 typedef void (^MKETAHandler)(MKETAResponse * __nullable response, NSError * __nullable error);
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKDirections : NSObject
 
 // The request will be copied during initialization, so any changes made to the request
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDirectionsRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDirectionsRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDirectionsRequest.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDirectionsRequest.h	2016-06-01 05:05:44.000000000 +0200
@@ -11,7 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 6_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 6_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKDirectionsRequest : NSObject
 
 @property (nonatomic, strong, nullable) MKMapItem *source;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDirectionsResponse.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDirectionsResponse.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDirectionsResponse.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDirectionsResponse.h	2016-06-01 05:05:44.000000000 +0200
@@ -16,7 +16,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKDirectionsResponse : NSObject
 
 // Source and destination may be filled with additional details compared to the request object.
@@ -27,7 +27,7 @@
 
 @end
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKRoute : NSObject
 
 @property (nonatomic, readonly) NSString *name; // localized description of the route's significant feature, e.g. "US-101"
@@ -45,7 +45,7 @@
 
 @end
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKRouteStep : NSObject
 
 @property (nonatomic, readonly) NSString *instructions; // localized written instructions
@@ -59,7 +59,7 @@
 
 @end
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKETAResponse : NSObject
 
 // Source and destination may be filled with additional details compared to the request object.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDistanceFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDistanceFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDistanceFormatter.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDistanceFormatter.h	2016-06-01 05:05:44.000000000 +0200
@@ -10,7 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2)
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2)
 @interface MKDistanceFormatter : NSFormatter
 
 // Convenience methods. MKDistanceFormatter also responds to the usual NSFormatter methods.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKFoundation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKFoundation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKFoundation.h	2015-10-03 02:09:04.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKFoundation.h	2016-06-01 05:05:44.000000000 +0200
@@ -15,4 +15,3 @@
 #endif
 
 #define MK_CLASS_AVAILABLE(_macIntro, _iphoneIntro) __attribute__((visibility("default"))) NS_CLASS_AVAILABLE(_macIntro, _iphoneIntro)
-#define MK_CLASS_DEPRECATED(_macIntro, _macDep, _iphoneIntro, _iphoneDep) __attribute__((visibility("default"))) NS_DEPRECATED(_macIntro, macDep, _iphoneIntro,_iphoneDep)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKGeodesicPolyline.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKGeodesicPolyline.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKGeodesicPolyline.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKGeodesicPolyline.h	2016-06-01 05:05:44.000000000 +0200
@@ -13,7 +13,7 @@
  An MKGeodesicPolyline follows the shortest path along the surface of the earth,
  which may appear as a curved line when drawn on the projected MKMapView.
  */
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKGeodesicPolyline : MKPolyline
 
 + (instancetype)polylineWithPoints:(MKMapPoint *)points count:(NSUInteger)count;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKLocalSearch.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKLocalSearch.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKLocalSearch.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKLocalSearch.h	2016-06-01 05:05:44.000000000 +0200
@@ -14,7 +14,7 @@
 
 typedef void (^MKLocalSearchCompletionHandler)(MKLocalSearchResponse * __nullable response, NSError * __nullable error);
 
-MK_CLASS_AVAILABLE(10_9, 6_1) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 6_1) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKLocalSearch : NSObject
 
 // The request will be copied during initialization, so any changes made to the request
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKLocalSearchRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKLocalSearchRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKLocalSearchRequest.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKLocalSearchRequest.h	2016-06-01 05:05:44.000000000 +0200
@@ -10,7 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 6_1) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 6_1) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKLocalSearchRequest : NSObject <NSCopying>
 
 @property (nonatomic, copy, nullable) NSString *naturalLanguageQuery;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKLocalSearchResponse.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKLocalSearchResponse.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKLocalSearchResponse.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKLocalSearchResponse.h	2016-06-01 05:05:44.000000000 +0200
@@ -12,7 +12,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 6_1) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 6_1) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKLocalSearchResponse : NSObject
 
 // An array of MKMapItems sorted by relevance in descending order
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapCamera.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapCamera.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapCamera.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapCamera.h	2016-06-01 05:05:44.000000000 +0200
@@ -12,7 +12,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKMapCamera : NSObject <NSSecureCoding, NSCopying>
 
 @property (nonatomic) CLLocationCoordinate2D centerCoordinate;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapItem.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapItem.h	2016-06-01 05:05:44.000000000 +0200
@@ -10,7 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 6_0) __TVOS_AVAILABLE(9_2)
+NS_CLASS_AVAILABLE(10_9, 6_0) __TVOS_AVAILABLE(9_2)
 @interface MKMapItem : NSObject
 
 // If this MKMapItem represents your current location (isCurrentLocation == YES), then placemark will be nil.
@@ -37,6 +37,7 @@
 MK_EXTERN NSString * const MKLaunchOptionsShowsTrafficKey       NS_AVAILABLE(10_9, 6_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED; // Key to a boolean NSNumber
 
 // Directions modes
+MK_EXTERN NSString * const MKLaunchOptionsDirectionsModeDefault NS_AVAILABLE(10_12, 10_0) __TVOS_PROHIBITED __WATCHOS_AVAILABLE(3_0); // Will pick the best directions mode, given the user's preferences
 MK_EXTERN NSString * const MKLaunchOptionsDirectionsModeDriving NS_AVAILABLE(10_9, 6_0) __TVOS_PROHIBITED;
 MK_EXTERN NSString * const MKLaunchOptionsDirectionsModeWalking NS_AVAILABLE(10_9, 6_0) __TVOS_PROHIBITED;
 MK_EXTERN NSString * const MKLaunchOptionsDirectionsModeTransit NS_AVAILABLE(10_11, 9_0) __TVOS_PROHIBITED;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapSnapshot.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapSnapshot.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapSnapshot.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapSnapshot.h	2016-06-01 05:05:44.000000000 +0200
@@ -16,7 +16,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKMapSnapshot : NSObject
 
 #if TARGET_OS_IPHONE
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapSnapshotOptions.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapSnapshotOptions.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapSnapshotOptions.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapSnapshotOptions.h	2016-06-01 05:05:44.000000000 +0200
@@ -12,7 +12,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKMapSnapshotOptions : NSObject <NSCopying>
 
 @property (nonatomic, copy) MKMapCamera *camera;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapSnapshotter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapSnapshotter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapSnapshotter.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapSnapshotter.h	2016-06-01 05:05:44.000000000 +0200
@@ -14,7 +14,7 @@
 
 typedef void (^MKMapSnapshotCompletionHandler)(MKMapSnapshot * __nullable snapshot, NSError * __nullable error);
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKMapSnapshotter : NSObject
 
 - (instancetype)initWithOptions:(MKMapSnapshotOptions *)options NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapView.h	2016-02-25 00:12:08.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapView.h	2016-06-01 05:05:13.000000000 +0200
@@ -29,10 +29,10 @@
 } NS_ENUM_AVAILABLE(NA, 5_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED;
 
 #if TARGET_OS_IPHONE
-MK_CLASS_AVAILABLE(NA, 3_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(NA, 3_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKMapView : UIView <NSCoding>
 #else
-MK_CLASS_AVAILABLE(10_9, NA)
+NS_CLASS_AVAILABLE(10_9, NA)
 @interface MKMapView : NSView <NSCoding>
 #endif
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMultiPoint.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMultiPoint.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMultiPoint.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMultiPoint.h	2016-06-01 05:05:44.000000000 +0200
@@ -12,7 +12,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKMultiPoint : MKShape
 
 - (MKMapPoint *)points NS_RETURNS_INNER_POINTER;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayPathRenderer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayPathRenderer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayPathRenderer.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayPathRenderer.h	2016-06-01 05:05:44.000000000 +0200
@@ -15,7 +15,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKOverlayPathRenderer : MKOverlayRenderer
 
 #if TARGET_OS_IPHONE
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayPathView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayPathView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayPathView.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayPathView.h	2016-06-01 05:05:44.000000000 +0200
@@ -11,7 +11,7 @@
 #import <MapKit/MKFoundation.h>
 
 // Prefer MKOverlayPathRenderer
-MK_CLASS_AVAILABLE(NA, 4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(NA, 4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface MKOverlayPathView : MKOverlayView
 
 @property (strong) UIColor *fillColor NS_DEPRECATED_IOS(4_0, 7_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayRenderer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayRenderer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayRenderer.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayRenderer.h	2016-06-01 05:05:44.000000000 +0200
@@ -11,7 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKOverlayRenderer : NSObject
 
 - (instancetype)initWithOverlay:(id <MKOverlay>)overlay NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayView.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKOverlayView.h	2016-06-01 05:05:44.000000000 +0200
@@ -12,7 +12,7 @@
 
 
 // Prefer MKOverlayRenderer
-MK_CLASS_AVAILABLE(NA, 4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(NA, 4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface MKOverlayView : UIView
 
 - (instancetype)initWithOverlay:(id <MKOverlay>)overlay NS_DESIGNATED_INITIALIZER NS_DEPRECATED_IOS(4_0, 7_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPinAnnotationView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPinAnnotationView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPinAnnotationView.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPinAnnotationView.h	2016-06-01 05:05:44.000000000 +0200
@@ -16,7 +16,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 3_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 3_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKPinAnnotationView : MKAnnotationView
 
 #if TARGET_OS_IPHONE
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h	2016-06-01 05:05:44.000000000 +0200
@@ -12,7 +12,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 3_0) __TVOS_AVAILABLE(9_2)
+NS_CLASS_AVAILABLE(10_9, 3_0) __TVOS_AVAILABLE(9_2)
 @interface MKPlacemark : CLPlacemark <MKAnnotation>
 
 // An address dictionary is a dictionary in the same form as returned by 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPointAnnotation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPointAnnotation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPointAnnotation.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPointAnnotation.h	2016-06-01 05:05:44.000000000 +0200
@@ -12,7 +12,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKPointAnnotation : MKShape
 
 @property (nonatomic, assign) CLLocationCoordinate2D coordinate;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygon.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygon.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygon.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygon.h	2016-06-01 05:05:44.000000000 +0200
@@ -11,7 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKPolygon : MKMultiPoint <MKOverlay>
 
 + (instancetype)polygonWithPoints:(MKMapPoint *)points count:(NSUInteger)count;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygonRenderer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygonRenderer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygonRenderer.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygonRenderer.h	2016-06-01 05:05:44.000000000 +0200
@@ -10,7 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKPolygonRenderer : MKOverlayPathRenderer
 
 - (instancetype)initWithPolygon:(MKPolygon *)polygon;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygonView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygonView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygonView.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygonView.h	2016-06-01 05:05:44.000000000 +0200
@@ -10,7 +10,7 @@
 #import <MapKit/MKFoundation.h>
 
 // Prefer MKPolygonRenderer
-MK_CLASS_AVAILABLE(NA, 4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(NA, 4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface MKPolygonView : MKOverlayPathView
 
 - (instancetype)initWithPolygon:(MKPolygon *)polygon NS_DEPRECATED_IOS(4_0, 7_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolyline.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolyline.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolyline.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolyline.h	2016-06-01 05:05:44.000000000 +0200
@@ -11,7 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKPolyline : MKMultiPoint <MKOverlay>
 
 + (instancetype)polylineWithPoints:(MKMapPoint *)points count:(NSUInteger)count;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolylineRenderer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolylineRenderer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolylineRenderer.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolylineRenderer.h	2016-06-01 05:05:44.000000000 +0200
@@ -11,7 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKPolylineRenderer : MKOverlayPathRenderer
 
 - (instancetype)initWithPolyline:(MKPolyline *)polyline;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolylineView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolylineView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolylineView.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolylineView.h	2016-06-01 05:05:44.000000000 +0200
@@ -12,7 +12,7 @@
 #import <MapKit/MKFoundation.h>
 
 // Prefer MKPolylineRenderer
-MK_CLASS_AVAILABLE(NA, 4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(NA, 4_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface MKPolylineView : MKOverlayPathView
 
 - (instancetype)initWithPolyline:(MKPolyline *)polyline NS_DEPRECATED_IOS(4_0, 7_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKReverseGeocoder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKReverseGeocoder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKReverseGeocoder.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKReverseGeocoder.h	2016-06-01 05:05:44.000000000 +0200
@@ -15,7 +15,7 @@
 
 // MKReverseGeocoder is now deprecated.
 // Use CLGeocoder in CoreLocation instead.
-MK_CLASS_DEPRECATED(NA, NA, 3_0, 5_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+NS_CLASS_DEPRECATED(NA, NA, 3_0, 5_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface MKReverseGeocoder : NSObject
 
 - (instancetype)initWithCoordinate:(CLLocationCoordinate2D)coordinate NS_DEPRECATED_IOS(3_0,5_0);
@@ -32,7 +32,7 @@
 
 @end
 
-MK_CLASS_DEPRECATED(NA, NA, 3_0, 5_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+NS_CLASS_DEPRECATED(NA, NA, 3_0, 5_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @protocol MKReverseGeocoderDelegate <NSObject>
 @required
 - (void)reverseGeocoder:(MKReverseGeocoder *)geocoder didFindPlacemark:(MKPlacemark *)placemark NS_DEPRECATED_IOS(3_0,5_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKShape.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKShape.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKShape.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKShape.h	2016-06-01 05:05:44.000000000 +0200
@@ -10,7 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKShape : NSObject <MKAnnotation>
 
 @property (nonatomic, copy, nullable) NSString *title;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKTileOverlay.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKTileOverlay.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKTileOverlay.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKTileOverlay.h	2016-06-01 05:05:44.000000000 +0200
@@ -11,7 +11,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 // MKTileOverlay represents a data source for raster image tiles in the spherical mercator projection (EPSG:3857).
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKTileOverlay : NSObject <MKOverlay>
 
 - (instancetype)initWithURLTemplate:(nullable NSString *)URLTemplate NS_DESIGNATED_INITIALIZER; // URL template is a string where the substrings "{x}", "{y}", "{z}", and "{scale}" are replaced with values from a tile path to create a URL to load. For example: http://server/path?x={x}&y={y}&z={z}&scale={scale}.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKTileOverlayRenderer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKTileOverlayRenderer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKTileOverlayRenderer.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKTileOverlayRenderer.h	2016-06-01 05:05:44.000000000 +0200
@@ -11,7 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKTileOverlayRenderer : MKOverlayRenderer
 
 - (instancetype)initWithTileOverlay:(MKTileOverlay *)overlay;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKUserLocation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKUserLocation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKUserLocation.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKUserLocation.h	2016-06-01 05:05:44.000000000 +0200
@@ -13,7 +13,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 3_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(10_9, 3_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKUserLocation : NSObject <MKAnnotation>
 
 // Returns YES if the user's location is being updated.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKUserTrackingBarButtonItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKUserTrackingBarButtonItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKUserTrackingBarButtonItem.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKUserTrackingBarButtonItem.h	2016-06-01 05:05:44.000000000 +0200
@@ -12,7 +12,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(NA, 5_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
+NS_CLASS_AVAILABLE(NA, 5_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @interface MKUserTrackingBarButtonItem : UIBarButtonItem
 
 - (instancetype)initWithMapView:(nullable MKMapView *)mapView NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MapKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MapKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MapKit.h	2016-02-26 05:41:36.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MapKit.h	2016-06-01 05:05:44.000000000 +0200
@@ -12,6 +12,7 @@
 #import <MapKit/MKGeometry.h>
 #import <MapKit/MKMapItem.h>
 #import <MapKit/MKPlacemark.h>
+#import <MapKit/NSUserActivity+MKMapItem.h>
 
 #if __has_include(<MapKit/MKMapView.h>)
 #import <MapKit/MKAnnotationView.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/NSUserActivity+MKMapItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/NSUserActivity+MKMapItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/NSUserActivity+MKMapItem.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/NSUserActivity+MKMapItem.h	2016-06-01 05:05:44.000000000 +0200
@@ -0,0 +1,16 @@
+//
+//  NSUserActivity+MKMapItem.h
+//  MapKit
+//
+//  Copyright (c) 2009-2016, Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+@class MKMapItem;
+
+@interface NSUserActivity (MKMapItem)
+
+@property (nonatomic, strong) MKMapItem *mapItem NS_AVAILABLE(10_12, 10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+
+@end

```