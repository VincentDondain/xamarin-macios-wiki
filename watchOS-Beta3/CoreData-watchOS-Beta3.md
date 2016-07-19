#CoreData.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentContainer.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentContainer.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentContainer.h	2016-06-27 06:09:43.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentContainer.h	2016-07-10 07:49:23.000000000 +0200
@@ -37,7 +37,7 @@
 @property (strong, readonly) NSPersistentStoreCoordinator *persistentStoreCoordinator;
 @property (copy) NSArray<NSPersistentStoreDescription *> *persistentStoreDescriptions;
 
-// Creates a container using the model named `name` in the main bundle, or the merged model (from the main bundle) if no match was found.
+// Creates a container using the model named `name` in the main bundle
 - (instancetype)initWithName:(NSString *)name;
 
 - (instancetype)initWithName:(NSString *)name managedObjectModel:(NSManagedObjectModel *)model NS_DESIGNATED_INITIALIZER;

```