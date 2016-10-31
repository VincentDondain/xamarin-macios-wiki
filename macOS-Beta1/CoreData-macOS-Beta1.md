#CoreData.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObject.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObject.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObject.h	2016-08-18 03:39:53.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObject.h	2016-10-18 01:42:16.000000000 +0200
@@ -39,7 +39,7 @@
     NSManagedObjectID*  _cd_objectID;
     uintptr_t           _cd_extraFlags;
     id                  _cd_observationInfo;
-    id*                 _cd_snapshots;
+    void*               _cd_extras;
     uintptr_t           _cd_lockingInfo;
     id                  _cd_queueReference;
 #endif
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h	2016-08-18 03:39:53.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h	2016-10-18 01:42:17.000000000 +0200
@@ -276,7 +276,7 @@
  */
 - (BOOL)setQueryGenerationFromToken:(nullable NSQueryGenerationToken *)generation error:(NSError **)error API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
-/* Whether the context automatically merges changes saved to its parent. Setting this property to YES when the context is pinned to a non-current query generation is not supported.
+/* Whether the context automatically merges changes saved to its coordinator or parent context. Setting this property to YES when the context is pinned to a non-current query generation is not supported.
  */
 @property (nonatomic) BOOL automaticallyMergesChangesFromParent API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyDescription.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyDescription.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyDescription.h	2016-08-18 03:39:53.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyDescription.h	2016-10-18 01:42:17.000000000 +0200
@@ -20,12 +20,14 @@
 #if (!__OBJC2__)
 @private
 	NSString *_versionHashModifier;
-	id _underlyingProperty;
+	id _underlyingProperty2;
 	NSData *_versionHash;
     NSEntityDescription *_entity;
     NSString *_name;
     NSArray *_validationPredicates;
     NSArray *_validationWarnings;
+    __strong void *_extraIvars;
+    NSMutableDictionary *_userInfo;
     struct __propertyDescriptionFlags {
         unsigned int _isReadOnly:1;
         unsigned int _isTransient:1;
@@ -36,10 +38,14 @@
         unsigned int _isStoredInExternalRecord:1;
 		unsigned int _extraIvarsAreInDataBlob:1;
         unsigned int _isOrdered:1;
-        unsigned int _reservedPropertyDescription:23;
+        
+        unsigned int _hasMaxValueInExtraIvars:1;
+        unsigned int _hasMinValueInExtraIvars:1;
+        unsigned int _storeBinaryDataExternally:1;
+        unsigned int _reservedAttributeFlagOne:1;
+
+        unsigned int _reservedPropertyDescription:19;
     } _propertyDescriptionFlags;    
-    __strong void *_extraIvars;
-    NSMutableDictionary *_userInfo;
 	long _entitysReferenceIDForProperty;
 #endif
 }

```