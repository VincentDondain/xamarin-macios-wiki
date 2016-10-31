#CoreData.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h	2016-09-13 04:40:40.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h	2016-10-22 02:11:03.000000000 +0200
@@ -216,7 +216,7 @@
  */
 - (BOOL)setQueryGenerationFromToken:(nullable NSQueryGenerationToken *)generation error:(NSError **)error API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
-/* Whether the context automatically merges changes saved to its parent. Setting this property to YES when the context is pinned to a non-current query generation is not supported.
+/* Whether the context automatically merges changes saved to its coordinator or parent context. Setting this property to YES when the context is pinned to a non-current query generation is not supported.
 */
 @property (nonatomic) BOOL automaticallyMergesChangesFromParent API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 

```