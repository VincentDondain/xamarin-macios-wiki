#MapKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygon.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygon.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygon.h	2016-05-23 00:32:38.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolygon.h	2016-06-26 18:23:58.000000000 +0200
@@ -14,11 +14,11 @@
 NS_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKPolygon : MKMultiPoint <MKOverlay>
 
-+ (instancetype)polygonWithPoints:(MKMapPoint *)points count:(NSUInteger)count;
-+ (instancetype)polygonWithPoints:(MKMapPoint *)points count:(NSUInteger)count interiorPolygons:(nullable NSArray<MKPolygon *> *)interiorPolygons;
++ (instancetype)polygonWithPoints:(const MKMapPoint *)points count:(NSUInteger)count;
++ (instancetype)polygonWithPoints:(const MKMapPoint *)points count:(NSUInteger)count interiorPolygons:(nullable NSArray<MKPolygon *> *)interiorPolygons;
 
-+ (instancetype)polygonWithCoordinates:(CLLocationCoordinate2D *)coords count:(NSUInteger)count;
-+ (instancetype)polygonWithCoordinates:(CLLocationCoordinate2D *)coords count:(NSUInteger)count interiorPolygons:(nullable NSArray<MKPolygon *> *)interiorPolygons;
++ (instancetype)polygonWithCoordinates:(const CLLocationCoordinate2D *)coords count:(NSUInteger)count;
++ (instancetype)polygonWithCoordinates:(const CLLocationCoordinate2D *)coords count:(NSUInteger)count interiorPolygons:(nullable NSArray<MKPolygon *> *)interiorPolygons;
 
 @property (readonly, nullable) NSArray<MKPolygon *> *interiorPolygons;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolyline.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolyline.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolyline.h	2016-05-23 00:32:38.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPolyline.h	2016-06-26 18:23:58.000000000 +0200
@@ -14,8 +14,8 @@
 NS_CLASS_AVAILABLE(10_9, 4_0) __TVOS_AVAILABLE(9_2) __WATCHOS_PROHIBITED
 @interface MKPolyline : MKMultiPoint <MKOverlay>
 
-+ (instancetype)polylineWithPoints:(MKMapPoint *)points count:(NSUInteger)count;
-+ (instancetype)polylineWithCoordinates:(CLLocationCoordinate2D *)coords count:(NSUInteger)count;
++ (instancetype)polylineWithPoints:(const MKMapPoint *)points count:(NSUInteger)count;
++ (instancetype)polylineWithCoordinates:(const CLLocationCoordinate2D *)coords count:(NSUInteger)count;
 
 @end
 

```