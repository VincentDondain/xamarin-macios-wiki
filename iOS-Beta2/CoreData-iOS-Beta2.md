#CoreData.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequest.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequest.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequest.h	2016-05-26 06:17:02.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequest.h	2016-06-27 07:21:43.000000000 +0200
@@ -23,14 +23,17 @@
 typedef NS_OPTIONS(NSUInteger, NSFetchRequestResultType) {
     NSManagedObjectResultType		= 0x00,
     NSManagedObjectIDResultType		= 0x01,
-    NSDictionaryResultType          NS_ENUM_AVAILABLE(10_6,3_0) = 0x02,
-    NSCountResultType				NS_ENUM_AVAILABLE(10_6,3_0) = 0x04
+    NSDictionaryResultType          API_AVAILABLE(macosx(10.6), ios(3.0)) = 0x02,
+    NSCountResultType				API_AVAILABLE(macosx(10.6), ios(3.0)) = 0x04
 };
 
 /* Protocol conformance for possible result types a fetch request can return. */
 @protocol NSFetchRequestResult <NSObject>
 @end
 
+@interface NSNumber (NSFetchedResultSupport) <NSFetchRequestResult>
+@end
+
 @interface NSDictionary (NSFetchedResultSupport) <NSFetchRequestResult>
 @end
 
 ```