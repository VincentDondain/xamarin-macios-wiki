#MapKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDistanceFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDistanceFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDistanceFormatter.h	2016-03-03 03:45:54.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKDistanceFormatter.h	2016-06-01 05:57:29.000000000 +0200
@@ -10,7 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2)
+NS_CLASS_AVAILABLE(10_9, 7_0) __TVOS_AVAILABLE(9_2)
 @interface MKDistanceFormatter : NSFormatter
 
 // Convenience methods. MKDistanceFormatter also responds to the usual NSFormatter methods.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKFoundation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKFoundation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKFoundation.h	2015-08-15 08:37:02.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKFoundation.h	2016-06-01 05:57:29.000000000 +0200
@@ -15,4 +15,3 @@
 #endif
 
 #define MK_CLASS_AVAILABLE(_macIntro, _iphoneIntro) __attribute__((visibility("default"))) NS_CLASS_AVAILABLE(_macIntro, _iphoneIntro)
-#define MK_CLASS_DEPRECATED(_macIntro, _macDep, _iphoneIntro, _iphoneDep) __attribute__((visibility("default"))) NS_DEPRECATED(_macIntro, macDep, _iphoneIntro,_iphoneDep)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapItem.h	2016-03-03 03:45:54.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKMapItem.h	2016-06-01 05:57:29.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h	2016-03-03 03:45:54.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MKPlacemark.h	2016-06-01 05:57:29.000000000 +0200
@@ -12,7 +12,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-MK_CLASS_AVAILABLE(10_9, 3_0) __TVOS_AVAILABLE(9_2)
+NS_CLASS_AVAILABLE(10_9, 3_0) __TVOS_AVAILABLE(9_2)
 @interface MKPlacemark : CLPlacemark <MKAnnotation>
 
 // An address dictionary is a dictionary in the same form as returned by 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MapKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MapKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MapKit.h	2016-03-03 03:45:54.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/MapKit.h	2016-06-01 05:57:29.000000000 +0200
@@ -12,6 +12,7 @@
 #import <MapKit/MKGeometry.h>
 #import <MapKit/MKMapItem.h>
 #import <MapKit/MKPlacemark.h>
+#import <MapKit/NSUserActivity+MKMapItem.h>
 
 #if __has_include(<MapKit/MKMapView.h>)
 #import <MapKit/MKAnnotationView.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/NSUserActivity+MKMapItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/NSUserActivity+MKMapItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/NSUserActivity+MKMapItem.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/MapKit.framework/Headers/NSUserActivity+MKMapItem.h	2016-06-01 05:57:29.000000000 +0200
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