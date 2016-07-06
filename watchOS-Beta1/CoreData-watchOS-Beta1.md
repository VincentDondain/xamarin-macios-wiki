#CoreData.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreData.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreData.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreData.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreData.h	2016-05-21 07:41:59.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	CoreData.h
 	Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
 	All rights reserved.
 */
 
@@ -47,4 +47,7 @@
 #import <CoreData/NSMergePolicy.h>
 
 #import <CoreData/NSFetchedResultsController.h>
+#import <CoreData/NSQueryGenerationToken.h>
+#import <CoreData/NSPersistentStoreDescription.h>
+#import <CoreData/NSPersistentContainer.h>
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataDefines.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataDefines.h	2016-05-21 07:41:58.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	CoreDataDefines.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
 	All rights reserved.
 */
 #ifndef _COREDATADEFINES_H
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataErrors.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataErrors.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataErrors.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataErrors.h	2016-05-26 06:17:02.000000000 +0200
@@ -1,7 +1,7 @@
 /*
 	CoreDataErrors.h
 	Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
 	All rights reserved.
  */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStore.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStore.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStore.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStore.h	2016-05-21 07:41:58.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSAtomicStore.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -23,6 +23,7 @@
 
 NS_CLASS_AVAILABLE(10_5,3_0)
 @interface NSAtomicStore : NSPersistentStore {
+#if (!__OBJC2__)
 	@private
     NSMutableDictionary *_nodeCache;
     NSMutableDictionary *_entityCache;
@@ -30,6 +31,7 @@
     NSInteger _nextReference;
 	void *_reserved4;
 	void *_reserved5;
+#endif
 }
 
 // API method that may be overriden by subclasses for custom initialization
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStoreCacheNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStoreCacheNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStoreCacheNode.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStoreCacheNode.h	2016-05-21 07:41:58.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSAtomicStoreCacheNode.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -20,11 +20,13 @@
 
 NS_CLASS_AVAILABLE(10_5,3_0)
 @interface NSAtomicStoreCacheNode : NSObject {
+#if (!__OBJC2__)
     @private
     NSManagedObjectID *_objectID;
     uintptr_t __versionNumber;
 	NSMutableDictionary *_propertyCache;
 	void *_reserved1;
+#endif
 }
 
 /* The designated initializer for the cache node. */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAttributeDescription.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAttributeDescription.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAttributeDescription.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAttributeDescription.h	2016-05-21 07:41:59.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSAttributeDescription.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -34,18 +34,6 @@
 // Attributes represent individual values like strings, numbers, dates, etc.
 NS_CLASS_AVAILABLE(10_4,3_0)
 @interface NSAttributeDescription : NSPropertyDescription {
-@private
-	Class _attributeValueClass;
-	NSString *_valueTransformerName;
-    NSAttributeType _type;
-    NSString *_attributeValueClassName;
-    struct __attributeDescriptionFlags {
-		unsigned int _hasMaxValueInExtraIvars:1;
-		unsigned int _hasMinValueInExtraIvars:1;
-		unsigned int _storeBinaryDataExternally:1;
-        unsigned int _reservedAttributeDescription:29;
-    } _attributeDescriptionFlags;
-    id _defaultValue;
 }
 
 // NSUndefinedAttributeType is valid for transient properties - Core Data will still track the property as an id value and register undo/redo actions, etc. NSUndefinedAttributeType is illegal for non-transient properties.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchDeleteRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchDeleteRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchDeleteRequest.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchDeleteRequest.h	2016-05-21 07:41:58.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSBatchDeleteRequest.h
     Core Data
-    Copyright (c) 2015-2015, Apple Inc.
+    Copyright (c) 2015-2016, Apple Inc.
     All rights reserved.
  */
 
@@ -25,10 +25,12 @@
 //  delete rules (for example, minimum relationship counts).
 NS_CLASS_AVAILABLE(10_11,9_0)
 @interface NSBatchDeleteRequest : NSPersistentStoreRequest {
+#if (!__OBJC2__)
     @private
     NSBatchDeleteRequestResultType _resultType;
     NSFetchRequest *_deleteTarget;
     void *_reserved;
+#endif
 }
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchUpdateRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchUpdateRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchUpdateRequest.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchUpdateRequest.h	2016-05-21 07:41:58.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  NSBatchUpdateRequest.h
  Core Data
- Copyright (c) 2004-2015, Apple Inc.
+ Copyright (c) 2004-2016, Apple Inc.
  All rights reserved.
  */
 
@@ -22,6 +22,7 @@
 //  the underlying store do not violate any validation rules specified in the model.
 NS_CLASS_AVAILABLE(10_10,8_0)
 @interface NSBatchUpdateRequest : NSPersistentStoreRequest {
+#if (!__OBJC2__)
     @private
     id _entity;
     NSPredicate *_predicate;
@@ -32,12 +33,13 @@
         unsigned int _RESERVED:28;
     } _flags;
     NSDictionary *_columnsToUpdate;
+#endif
 }
 
 + (instancetype)batchUpdateRequestWithEntityName:(NSString*)entityName;
 
-- (instancetype)initWithEntityName:(NSString *)entityName;
-- (instancetype)initWithEntity:(NSEntityDescription *)entity;
+- (instancetype)initWithEntityName:(NSString *)entityName NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithEntity:(NSEntityDescription *)entity NS_DESIGNATED_INITIALIZER;
 
 @property (copy, readonly) NSString* entityName;
 @property (strong, readonly) NSEntityDescription *entity;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityDescription.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityDescription.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityDescription.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityDescription.h	2016-05-21 07:49:58.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSEntityDescription.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -22,41 +22,6 @@
 // Entities describe the "types" of objects available.
 NS_CLASS_AVAILABLE(10_4,3_0)
 @interface NSEntityDescription : NSObject <NSCoding, NSCopying, NSFastEnumeration> {
-@private
-	int32_t  _cd_rc;
-	id _snapshotClass;
-	NSString *_versionHashModifier;
-	NSData *_versionHash;
-    __weak NSManagedObjectModel *_model;
-    NSString *_classNameForEntity;
-    Class _instanceClass;
-    NSString *_name;
-    __weak NSEntityDescription *_rootentity;
-    __weak NSEntityDescription *_superentity;
-    NSMutableDictionary *_subentities;
-    NSMutableDictionary *_properties;
-    id _propertyMapping;
-    __strong NSRange *_propertyRanges;
-    struct __entityDescriptionFlags {
-        unsigned int _isAbstract:1;
-        unsigned int _shouldValidateOnSave:1;
-        unsigned int _isImmutable:1;
-        unsigned int _isFlattened:1;
-        unsigned int _skipValidation:1;
-        unsigned int _hasPropertiesIndexedBySpotlight:1;
-        unsigned int _hasPropertiesStoredInTruthFile:1;
-        unsigned int _rangesAreInDataBlob:1; 
-		unsigned int _hasAttributesWithExternalDataReferences:1;
-        unsigned int _hasNonstandardPrimitiveProperties:2;
-        unsigned int _hasUniqueProperties:1;
-        unsigned int _validationUniqueProperties:1;
-        unsigned int _reservedEntityDescription:19;
-    } _entityDescriptionFlags;
-    __strong void *_extraIvars;
-    NSMutableDictionary *_userInfo;
-    id _flattenedSubentities;
-    id** _kvcPropertyAccessors;
-    long _modelsReferenceIDForEntity;
 }
 
 + (nullable NSEntityDescription *)entityForName:(NSString *)entityName inManagedObjectContext:(NSManagedObjectContext *)context;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMapping.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMapping.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMapping.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMapping.h	2016-05-26 06:23:57.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSEntityMapping.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -28,7 +28,7 @@
 
 NS_CLASS_AVAILABLE(10_5,3_0)
 @interface NSEntityMapping : NSObject {
-
+#if (!__OBJC2__)
 @private
     void *_reserved;
     void *_reserved1;
@@ -49,7 +49,7 @@
         unsigned int _isInUse:1;
         unsigned int _reservedEntityMapping:31;
     } _entityMappingFlags;
-
+#endif
 }
 
 /* Returns/sets the name of the mapping. The name is used only as a means of distinguishing mappings in a model.  If not specified, defaults to the string composed by the source entity name followed by the destination entity name (ex. SourceName->DestinationName)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMigrationPolicy.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMigrationPolicy.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMigrationPolicy.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMigrationPolicy.h	2016-05-26 06:17:02.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSEntityMigrationPolicy.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSExpressionDescription.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSExpressionDescription.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSExpressionDescription.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSExpressionDescription.h	2016-05-21 07:41:58.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  NSExpressionDescription.h
  Core Data
- Copyright (c) 2004-2015, Apple Inc.
+ Copyright (c) 2004-2016, Apple Inc.
  All rights reserved.
  */
 
@@ -19,6 +19,7 @@
    max(attribute). NSExpressionDescriptions cannot be set as properties on NSEntityDescription. */
 NS_CLASS_AVAILABLE(10_6,3_0)
 @interface NSExpressionDescription : NSPropertyDescription {
+#if (!__OBJC2__)
 	@private
 	id _reservedtype1_1;
 	id _reservedtype1_2;
@@ -31,6 +32,7 @@
 	void *_reservedtype2_3;
 	NSExpression *_expression;
 	NSAttributeType _expressionResultType;
+#endif
 }
 
 @property (nullable, strong) NSExpression *expression;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequest.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequest.h	2016-05-26 06:17:02.000000000 +0200
@@ -1,12 +1,14 @@
 /*
     NSFetchRequest.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
 #import <Foundation/NSArray.h>
 #import <CoreData/NSPersistentStoreRequest.h>
+#import <CoreData/NSManagedObject.h>
+#import <CoreData/NSManagedObjectID.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -22,45 +24,33 @@
     NSManagedObjectResultType		= 0x00,
     NSManagedObjectIDResultType		= 0x01,
     NSDictionaryResultType          NS_ENUM_AVAILABLE(10_6,3_0) = 0x02,
-	NSCountResultType				NS_ENUM_AVAILABLE(10_6,3_0) = 0x04
+    NSCountResultType				NS_ENUM_AVAILABLE(10_6,3_0) = 0x04
 };
 
+/* Protocol conformance for possible result types a fetch request can return. */
+@protocol NSFetchRequestResult <NSObject>
+@end
+
+@interface NSDictionary (NSFetchedResultSupport) <NSFetchRequestResult>
+@end
+
+@interface NSManagedObject (NSFetchedResultSupport) <NSFetchRequestResult>
+@end
 
+@interface NSManagedObjectID (NSFetchedResultSupport) <NSFetchRequestResult>
+@end
 
 NS_CLASS_AVAILABLE(10_4, 3_0)
-@interface NSFetchRequest : NSPersistentStoreRequest <NSCoding> {
-@private
-	NSArray *_groupByProperties;
-	NSPredicate *_havingPredicate;
-	id* _additionalPrivateIvars;
-	NSArray *_valuesToFetch;
-    NSEntityDescription *_entity;
-    NSPredicate *_predicate;
-    NSArray *_sortDescriptors;
-    NSUInteger _batchSize;
-    unsigned long _fetchLimit;
-    NSArray *_relationshipKeyPathsForPrefetching;
-    struct _fetchRequestFlags {
-        unsigned int distinctValuesOnly:1;
-        unsigned int includesSubentities:1;
-        unsigned int includesPropertyValues:1;
-        unsigned int resultType:3;
-        unsigned int returnsObjectsAsFaults:1;
-        unsigned int excludePendingChanges:1;
-        unsigned int isInUse:1;
-        unsigned int entityIsName:1;
-        unsigned int refreshesRefetched:1;
-        unsigned int propertiesValidated:1;
-        unsigned int disableCaching:1;
-        unsigned int _RESERVED:19;
-    } _flags;
-}
+@interface NSFetchRequest<__covariant ResultType:id<NSFetchRequestResult>> : NSPersistentStoreRequest <NSCoding>
 
 + (instancetype)fetchRequestWithEntityName:(NSString*)entityName NS_AVAILABLE(10_7, 4_0);
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithEntityName:(NSString*)entityName NS_AVAILABLE(10_7, 4_0);
 
+// Executes the fetch request using the current managed object context. This method must be called from within a block submitted to a managed object context.
+- (nullable NSArray<ResultType> *)execute:(NSError **)error  NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+
 @property (nullable, nonatomic, strong) NSEntityDescription *entity;
 @property (nullable, nonatomic, readonly, strong) NSString *entityName NS_AVAILABLE(10_7, 4_0);
 
@@ -128,4 +118,20 @@
 
 @end
 
+
+@class NSAsynchronousFetchResult<ResultType:id<NSFetchRequestResult>>;
+
+typedef void (^NSPersistentStoreAsynchronousFetchResultCompletionBlock)(NSAsynchronousFetchResult *result);
+
+NS_CLASS_AVAILABLE(10_10,8_0)
+@interface NSAsynchronousFetchRequest<ResultType:id<NSFetchRequestResult>> : NSPersistentStoreRequest
+
+@property (strong, readonly) NSFetchRequest<ResultType> * fetchRequest;
+@property (nullable, strong, readonly) NSPersistentStoreAsynchronousFetchResultCompletionBlock completionBlock;
+@property (nonatomic) NSInteger estimatedResultCount;
+
+- (instancetype)initWithFetchRequest:(NSFetchRequest<ResultType> *)request completionBlock:(nullable void(^)(NSAsynchronousFetchResult<ResultType> *))blk;
+
+@end
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequestExpression.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequestExpression.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequestExpression.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequestExpression.h	2016-05-21 07:41:58.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSFetchRequestExpression.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -15,6 +15,7 @@
 
 NS_CLASS_AVAILABLE(10_5,3_0)
 @interface NSFetchRequestExpression : NSExpression {
+#if (!__OBJC2__)
 @private
     void* _reserved1;
     void* _reserved2;
@@ -26,6 +27,7 @@
         unsigned int isCountOnly:1;
         unsigned int _RESERVED:31;
     } _flags;
+#endif
 }
 
 /* Returns an expression which will evaluate to the result of executing a fetch request on a context.  The first argument must be an expression which evaluates to an NSFetchRequest *, and the second must be an expression which evaluates to an NSManagedObjectContext *.  If the desired result is simply the count for the request, the "countOnly" argument should be YES.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedPropertyDescription.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedPropertyDescription.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedPropertyDescription.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedPropertyDescription.h	2016-05-21 07:41:58.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSFetchedPropertyDescription.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -15,11 +15,13 @@
 // Fetched properties allow to specify related objects through a "weakly" resolved property, so there is no actual join necessary.
 NS_CLASS_AVAILABLE(10_4,3_0)
 @interface NSFetchedPropertyDescription : NSPropertyDescription {
+#if (!__OBJC2__)
 @private
 	void *_reserved5;
 	void *_reserved6;
     NSFetchRequest *_fetchRequest;
     NSString *_lazyFetchRequestEntityName;
+#endif
 }
 
 // As part of the predicate for a fetched property, you can use the two variables $FETCH_SOURCE (which is the managed object fetching the property) and $FETCHED_PROPERTY (which is the NSFetchedPropertyDescription instance).
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedResultsController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedResultsController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedResultsController.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedResultsController.h	2016-05-26 06:23:57.000000000 +0200
@@ -1,44 +1,38 @@
 /*
-    NSFetchedResultsController.h
-    Core Data
-    Copyright (c) 2009-2015, Apple Inc.
-    All rights reserved.
-
-Class Overview
-==============
-
-This class is intended to efficiently manage the results returned from a Core Data fetch request.
-
-You configure an instance of this class using a fetch request that specifies the entity, optionally a filter predicate, and an array containing at least one sort ordering. When you execute the fetch, the instance efficiently collects information about the results without the need to bring all the result objects into memory at the same time. As you access the results, objects are automatically faulted into memory in batches to match likely access patterns, and objects from previous accessed disposed of. This behavior further serves to keep memory requirements low, so even if you traverse a collection containing tens of thousands of objects, you should never have more than tens of them in memory at the same time.
-
-This class is tailored to work in conjunction with UITableView, however you are free to use it with your own views. UITableView expects its data source to present the results as an array of sections made up of rows. NSFetchedResultsController can efficiently analyze the result of the fetch request and pre-compute all the information about sections in the result set. Moreover, the controller can cache the results of this computation so that if the same data is subsequently re-displayed, the work does not have to be repeated. In addition:
-* The controller monitors changes to objects in its associated managed object context, and updates the results accordingly. It reports changes in the results set to its delegate.
-* The controller automatically purges unneeded objects if it receives an application low memory notification.
-* The controller maintains a persistent cache of the section information across application launches if the cacheName is not nil.  If caching is enabled, you must not mutate the fetch request, its predicate, or its sort descriptor without first calling +deleteCacheWithName:
-
-Typical use
-===========
-
+ NSFetchedResultsController.h
+ Core Data
+ Copyright (c) 2009-2016, Apple Inc.
+ All rights reserved.
+ 
+ Class Overview
+ ==============
+ 
+ This class is intended to efficiently manage the results returned from a Core Data fetch request.
+ 
+ You configure an instance of this class using a fetch request that specifies the entity, optionally a filter predicate, and an array containing at least one sort ordering. When you execute the fetch, the instance efficiently collects information about the results without the need to bring all the result objects into memory at the same time. As you access the results, objects are automatically faulted into memory in batches to match likely access patterns, and objects from previous accessed disposed of. This behavior further serves to keep memory requirements low, so even if you traverse a collection containing tens of thousands of objects, you should never have more than tens of them in memory at the same time.
+ 
+ This class is tailored to work in conjunction with views that present collections of objects. These views typically expect their data source to present results as a list of sections made up of rows. NSFetchedResultsController can efficiently analyze the result of the fetch request and pre-compute all the information about sections in the result set. Moreover, the controller can cache the results of this computation so that if the same data is subsequently re-displayed, the work does not have to be repeated. In addition:
+ * The controller monitors changes to objects in its associated managed object context, and updates the results accordingly. It reports changes in the results set to its delegate.
+ * The controller automatically purges unneeded objects if it receives an application low memory notification.
+ * The controller maintains a persistent cache of the section information across application launches if the cacheName is not nil.  If caching is enabled, you must not mutate the fetch request, its predicate, or its sort descriptor without first calling +deleteCacheWithName:
+ 
+ Typical use
+ ===========
+ 
 	Developers create an instance of NSFetchedResultsController and configure it with a fetchRequest.  It is expected that the sort descriptor used in the request groups the results into sections. This allows for section information to be pre-computed.
-	After creating an instance, the performFetch: method should be called to actually perform the fetching. 
-	Once configured, this class can be a helper class when implementing the following methods from the UITableViewDataSource protocol
-
-- (NSInteger)tableView:(UITableView *)table numberOfRowsInSection:(NSInteger)section;
-- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView; 
-- (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section; 
-- (NSArray *)sectionIndexTitlesForTableView:(UITableView *)tableView;   
-- (NSInteger)tableView:(UITableView *)tableView sectionForSectionIndexTitle:(NSString *)title atIndex:(NSInteger)index; 
-
-	The instance of NSFetchedResultsController also registers to receive change notifications on the managed object context that holds the fetched objects. Any change in the context that affects the result set or section information is properly processed. A delegate can be set on the class so that it's also notified when the result objects have changed. This would typically be used to update the display of the table view.  
+	After creating an instance, the performFetch: method should be called to actually perform the fetching.
+	Once started, convenience methods on the instance can be used for configuring the initial state of the view.
+ 
+	The instance of NSFetchedResultsController also registers to receive change notifications on the managed object context that holds the fetched objects. Any change in the context that affects the result set or section information is properly processed. A delegate can be set on the class so that it's also notified when the result objects have changed. This would typically be used to update the display of the view.
 	WARNING: The controller only performs change tracking if a delegate is set and responds to any of the change tracking notification methods.  See the NSFetchedResultsControllerDelegate protocol for which delegate methods are change tracking.
-
-Handling of Invalidated Objects
-===============================
+ 
+ Handling of Invalidated Objects
+ ===============================
 	
-		When a managed object context notifies the NSFetchedResultsController of individual objects being invalidated (NSInvalidatedObjectsKey), the controller treats these as deleted objects and sends the proper delegate calls.
-		It's possible for all the objects in a managed object context to be invalidated simultaneously. This can happen as a result of calling -reset on NSManagedObjectContext, or if a store is removed from the the NSPersistentStoreCoordinator. When this happens, NSFetchedResultsController currently does not invalidate all objects, nor does it send individual notifications for object deletions. Instead, developers must call performFetch: again to reset the state of the controller if all the objects in a context have been invalidated. They should also reload all their data in the UITableView.
-		
-*/
+ When a managed object context notifies the NSFetchedResultsController of individual objects being invalidated (NSInvalidatedObjectsKey), the controller treats these as deleted objects and sends the proper delegate calls.
+ It's possible for all the objects in a managed object context to be invalidated simultaneously. This can happen as a result of calling -reset on NSManagedObjectContext, or if a store is removed from the the NSPersistentStoreCoordinator. When this happens, NSFetchedResultsController currently does not invalidate all objects, nor does it send individual notifications for object deletions. Instead, developers must call performFetch: again to reset the state of the controller if all the objects in a context have been invalidated. They should also reset the state of their view.
+ 
+ */
 
 #import <Foundation/NSArray.h>
 #import <Foundation/NSDictionary.h>
@@ -54,38 +48,8 @@
 @protocol NSFetchedResultsControllerDelegate;
 @protocol NSFetchedResultsSectionInfo;
 
-NS_CLASS_AVAILABLE(NA,3_0)
-@interface NSFetchedResultsController : NSObject {
-@private
-	NSFetchRequest *_fetchRequest;
-	NSManagedObjectContext *_managedObjectContext;
-	NSString *_sectionNameKeyPath;
-	NSString *_sectionNameKey;
-	NSString *_cacheName;
-	void	  *_cache;
-	struct _fetchResultsControllerFlags {
-	  unsigned int _sendObjectChangeNotifications:1;
-	  unsigned int _sendSectionChangeNotifications:1;
-	  unsigned int _sendDidChangeContentNotifications:1;
-	  unsigned int _sendWillChangeContentNotifications:1;
-	  unsigned int _sendSectionIndexTitleForSectionName:1;
-	  unsigned int _changedResultsSinceLastSave:1;
-	  unsigned int _hasMutableFetchedResults:1;
-	  unsigned int _hasBatchedArrayResults:1;
-	  unsigned int _hasSections:1;
-	  unsigned int _usesNonpersistedProperties:1;
-	  unsigned int _includesSubentities:1;
-	  unsigned int _reservedFlags:21;
-	} _flags;
-	id _delegate;
-	id _sortKeys;
-	id _fetchedObjects;
-	id _sections;
-	id _sectionsByName;
-	id _sectionIndexTitles;
-	id _sectionIndexTitlesSections;
-	
-}
+NS_CLASS_AVAILABLE(10_12,3_0)
+@interface NSFetchedResultsController<ResultType:id<NSFetchRequestResult>> : NSObject
 
 /* ========================================================*/
 /* ========================= INITIALIZERS ====================*/
@@ -96,43 +60,43 @@
 	context - the context that will hold the fetched objects
 	sectionNameKeyPath - keypath on resulting objects that returns the section name. This will be used to pre-compute the section information.
 	cacheName - Section info is cached persistently to a private file under this name. Cached sections are checked to see if the time stamp matches the store, but not if you have illegally mutated the readonly fetch request, predicate, or sort descriptor.
-*/
-- (instancetype)initWithFetchRequest:(NSFetchRequest *)fetchRequest managedObjectContext: (NSManagedObjectContext *)context sectionNameKeyPath:(nullable NSString *)sectionNameKeyPath cacheName:(nullable NSString *)name;
+ */
+- (instancetype)initWithFetchRequest:(NSFetchRequest<ResultType> *)fetchRequest managedObjectContext: (NSManagedObjectContext *)context sectionNameKeyPath:(nullable NSString *)sectionNameKeyPath cacheName:(nullable NSString *)name;
 
 /* Executes the fetch request on the store to get objects.
-    Returns YES if successful or NO (and an error) if a problem occurred. 
-    An error is returned if the fetch request specified doesn't include a sort descriptor that uses sectionNameKeyPath.
-    After executing this method, the fetched objects can be accessed with the property 'fetchedObjects'
-*/
+ Returns YES if successful or NO (and an error) if a problem occurred.
+ An error is returned if the fetch request specified doesn't include a sort descriptor that uses sectionNameKeyPath.
+ After executing this method, the fetched objects can be accessed with the property 'fetchedObjects'
+ */
 - (BOOL)performFetch:(NSError **)error;
 
 /* ========================================================*/
 /* ====================== CONFIGURATION ===================*/
 /* ========================================================*/
 
-/* NSFetchRequest instance used to do the fetching. You must not change it, its predicate, or its sort descriptor after initialization without disabling caching or calling +deleteCacheWithName.  The sort descriptor used in the request groups objects into sections. 
-*/
-@property (nonatomic, readonly) NSFetchRequest *fetchRequest;
+/* NSFetchRequest instance used to do the fetching. You must not change it, its predicate, or its sort descriptor after initialization without disabling caching or calling +deleteCacheWithName.  The sort descriptor used in the request groups objects into sections.
+ */
+@property (nonatomic, readonly) NSFetchRequest<ResultType> *fetchRequest;
 
-/* Managed Object Context used to fetch objects. The controller registers to listen to change notifications on this context and properly update its result set and section information. 
-*/
+/* Managed Object Context used to fetch objects. The controller registers to listen to change notifications on this context and properly update its result set and section information.
+ */
 @property (nonatomic, readonly) NSManagedObjectContext *managedObjectContext;
 
-/* The keyPath on the fetched objects used to determine the section they belong to. 
-*/
+/* The keyPath on the fetched objects used to determine the section they belong to.
+ */
 @property (nullable, nonatomic, readonly) NSString *sectionNameKeyPath;
 
 /* Name of the persistent cached section information. Use nil to disable persistent caching, or +deleteCacheWithName to clear a cache.
-*/
+ */
 @property (nullable, nonatomic, readonly) NSString *cacheName;
 
 /* Delegate that is notified when the result set changes.
-*/
+ */
 @property(nullable, nonatomic, assign) id< NSFetchedResultsControllerDelegate > delegate;
 
 /* Deletes the cached section information with the given name.
-    If name is nil, then all caches are deleted.
-*/
+ If name is nil, then all caches are deleted.
+ */
 + (void)deleteCacheWithName:(nullable NSString *)name;
 
 /* ========================================================*/
@@ -140,39 +104,36 @@
 /* ========================================================*/
 
 /* Returns the results of the fetch.
-    Returns nil if the performFetch: hasn't been called.
-*/
-@property  (nullable, nonatomic, readonly) NSArray *fetchedObjects;
+ Returns nil if the performFetch: hasn't been called.
+ */
+@property  (nullable, nonatomic, readonly) NSArray<ResultType> *fetchedObjects;
 
 /* Returns the fetched object at a given indexPath.
-*/
-- (id)objectAtIndexPath:(NSIndexPath *)indexPath;
+ */
+- (ResultType)objectAtIndexPath:(NSIndexPath *)indexPath;
 
 /* Returns the indexPath of a given object.
-*/
--(nullable NSIndexPath *)indexPathForObject:(id)object;
+ */
+-(nullable NSIndexPath *)indexPathForObject:(ResultType)object;
 
 /* ========================================================*/
 /* =========== CONFIGURING SECTION INFORMATION ============*/
 /* ========================================================*/
 /*	These are meant to be optionally overridden by developers.
-*/
+ */
 
-/* Returns the corresponding section index entry for a given section name.	
-    Default implementation returns the capitalized first letter of the section name.
-    Developers that need different behavior can implement the delegate method -(NSString*)controller:(NSFetchedResultsController *)controller sectionIndexTitleForSectionName
-    Only needed if a section index is used.
-*/
+/* Returns the corresponding section index entry for a given section name.
+ Default implementation returns the capitalized first letter of the section name.
+ Developers that need different behavior can implement the delegate method -(NSString*)controller:(NSFetchedResultsController *)controller sectionIndexTitleForSectionName
+ Only needed if a section index is used.
+ */
 - (nullable NSString *)sectionIndexTitleForSectionName:(NSString *)sectionName;
 
 /* Returns the array of section index titles.
-    It's expected that developers call this method when implementing UITableViewDataSource's
-	- (NSArray *)sectionIndexTitlesForTableView:(UITableView *)tableView
-	
-    The default implementation returns the array created by calling sectionIndexTitleForSectionName: on all the known sections.
-    Developers should override this method if they wish to return a different array for the section index.
-    Only needed if a section index is used.
-*/
+ Default implementation returns the array created by calling sectionIndexTitleForSectionName: on all the known sections.
+ Developers should override this method if they wish to return a different array for the section index.
+ Only needed if a section index is used.
+ */
 @property (nonatomic, readonly) NSArray<NSString *> *sectionIndexTitles;
 
 /* ========================================================*/
@@ -180,19 +141,12 @@
 /* ========================================================*/
 
 /* Returns an array of objects that implement the NSFetchedResultsSectionInfo protocol.
-   It's expected that developers use the returned array when implementing the following methods of the UITableViewDataSource protocol
-
-- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView; 
-- (NSInteger)tableView:(UITableView *)table numberOfRowsInSection:(NSInteger)section;
-- (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section; 
-
-*/
+ This provide a convenience interface for determining the number of sections, the names and titles of the sections, and access to the model objects that belong to each section.
+ */
 @property (nullable, nonatomic, readonly) NSArray<id<NSFetchedResultsSectionInfo>> *sections;
 
 /* Returns the section number for a given section title and index in the section index.
-    It's expected that developers call this method when executing UITableViewDataSource's
-	- (NSInteger)tableView:(UITableView *)tableView sectionForSectionIndexTitle:(NSString *)title atIndex:(NSInteger)index;
-*/
+ */
 - (NSInteger)sectionForSectionIndexTitle:(NSString *)title atIndex:(NSInteger)sectionIndex;
 
 @end
@@ -202,19 +156,19 @@
 @protocol NSFetchedResultsSectionInfo
 
 /* Name of the section
-*/
+ */
 @property (nonatomic, readonly) NSString *name;
 
 /* Title of the section (used when displaying the index)
-*/
+ */
 @property (nullable, nonatomic, readonly) NSString *indexTitle;
 
 /* Number of objects in section
-*/
+ */
 @property (nonatomic, readonly) NSUInteger numberOfObjects;
 
 /* Returns the array of objects in the section.
-*/
+ */
 @property (nullable, nonatomic, readonly) NSArray *objects;
 
 @end // NSFetchedResultsSectionInfo
@@ -224,58 +178,59 @@
 @protocol NSFetchedResultsControllerDelegate <NSObject>
 
 typedef NS_ENUM(NSUInteger, NSFetchedResultsChangeType) {
-	NSFetchedResultsChangeInsert = 1,
-	NSFetchedResultsChangeDelete = 2,
-	NSFetchedResultsChangeMove = 3,
-	NSFetchedResultsChangeUpdate = 4
-} NS_ENUM_AVAILABLE(NA,  3_0);
+    NSFetchedResultsChangeInsert = 1,
+    NSFetchedResultsChangeDelete = 2,
+    NSFetchedResultsChangeMove = 3,
+    NSFetchedResultsChangeUpdate = 4
+} NS_ENUM_AVAILABLE(10_12,  3_0);
 
 /* Notifies the delegate that a fetched object has been changed due to an add, remove, move, or update. Enables NSFetchedResultsController change tracking.
 	controller - controller instance that noticed the change on its fetched objects
 	anObject - changed object
 	indexPath - indexPath of changed object (nil for inserts)
 	type - indicates if the change was an insert, delete, move, or update
-	newIndexPath - the destination path for inserted or moved objects, nil otherwise
+	newIndexPath - the destination path of changed object (nil for deletes)
 	
 	Changes are reported with the following heuristics:
-
-	On Adds and Removes, only the Added/Removed object is reported. It's assumed that all objects that come after the affected object are also moved, but these moves are not reported. 
-	The Move object is reported when the changed attribute on the object is one of the sort descriptors used in the fetch request.  An update of the object is assumed in this case, but no separate update message is sent to the delegate.
-	The Update object is reported when an object's state changes, and the changed attributes aren't part of the sort keys. 
-*/
+ 
+	Inserts and Deletes are reported when an object is created, destroyed, or changed in such a way that changes whether it matches the fetch request's predicate. Only the Inserted/Deleted object is reported; like inserting/deleting from an array, it's assumed that all objects that come after the affected object shift appropriately.
+	Move is reported when an object changes in a manner that affects its position in the results.  An update of the object is assumed in this case, no separate update message is sent to the delegate.
+	Update is reported when an object's state changes, and the changes do not affect the object's position in the results.
+ */
 @optional
 - (void)controller:(NSFetchedResultsController *)controller didChangeObject:(id)anObject atIndexPath:(nullable NSIndexPath *)indexPath forChangeType:(NSFetchedResultsChangeType)type newIndexPath:(nullable NSIndexPath *)newIndexPath;
 
 /* Notifies the delegate of added or removed sections.  Enables NSFetchedResultsController change tracking.
-
+ 
 	controller - controller instance that noticed the change on its sections
 	sectionInfo - changed section
 	index - index of changed section
 	type - indicates if the change was an insert or delete
-
-	Changes on section info are reported before changes on fetchedObjects. 
-*/
+ 
+	Changes on section info are reported before changes on fetchedObjects.
+ */
 @optional
 - (void)controller:(NSFetchedResultsController *)controller didChangeSection:(id <NSFetchedResultsSectionInfo>)sectionInfo atIndex:(NSUInteger)sectionIndex forChangeType:(NSFetchedResultsChangeType)type;
 
 /* Notifies the delegate that section and object changes are about to be processed and notifications will be sent.  Enables NSFetchedResultsController change tracking.
-   Clients utilizing a UITableView may prepare for a batch of updates by responding to this method with -beginUpdates
-*/
+ Clients may prepare for a batch of updates by using this method to begin an update block for their view.
+ */
 @optional
 - (void)controllerWillChangeContent:(NSFetchedResultsController *)controller;
 
 /* Notifies the delegate that all section and object changes have been sent. Enables NSFetchedResultsController change tracking.
-   Providing an empty implementation will enable change tracking if you do not care about the individual callbacks.
-*/
+ Clients may prepare for a batch of updates by using this method to begin an update block for their view.
+ Providing an empty implementation will enable change tracking if you do not care about the individual callbacks.
+ */
 @optional
 - (void)controllerDidChangeContent:(NSFetchedResultsController *)controller;
 
 /* Asks the delegate to return the corresponding section index entry for a given section name.	Does not enable NSFetchedResultsController change tracking.
-    If this method isn't implemented by the delegate, the default implementation returns the capitalized first letter of the section name (seee NSFetchedResultsController sectionIndexTitleForSectionName:)
-    Only needed if a section index is used.
-*/
+ If this method isn't implemented by the delegate, the default implementation returns the capitalized first letter of the section name (seee NSFetchedResultsController sectionIndexTitleForSectionName:)
+ Only needed if a section index is used.
+ */
 @optional
-- (nullable NSString *)controller:(NSFetchedResultsController *)controller sectionIndexTitleForSectionName:(NSString *)sectionName __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_0);
+- (nullable NSString *)controller:(NSFetchedResultsController *)controller sectionIndexTitleForSectionName:(NSString *)sectionName NS_AVAILABLE(10_12,4_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStore.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStore.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStore.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStore.h	2016-05-26 06:17:01.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  NSIncrementalStore.h
  Core Data
- Copyright (c) 2004-2015, Apple Inc.
+ Copyright (c) 2004-2016, Apple Inc.
  All rights reserved.
  */
 
@@ -23,11 +23,6 @@
 // data incrementally, allowing for the management of large and/or shared datasets.
 NS_CLASS_AVAILABLE(10_7,5_0)
 @interface NSIncrementalStore : NSPersistentStore {
-	@private
-	NSDictionary *_storeMetadata;
-	uint64_t _lastIdentifier;
-	void* _reserveda;
-	void* _reservedb;
 }
 
 // CoreData expects loadMetadata: to validate that the URL used to create the store is usable
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStoreNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStoreNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStoreNode.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStoreNode.h	2016-05-21 07:41:59.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  NSIncrementalStoreNode.h
  Core Data
- Copyright (c) 2004-2015, Apple Inc.
+ Copyright (c) 2004-2016, Apple Inc.
  All rights reserved.
  */
 
@@ -15,11 +15,6 @@
 // Provides the basic unit of external data that the Core Data stack interacts with.
 NS_CLASS_AVAILABLE(10_7,5_0)
 @interface NSIncrementalStoreNode : NSObject {
-@private
-    NSManagedObjectID *_objectID;
-    uint64_t _versionNumber;
-	id _propertyCache;
-	void *_reserved1;
 }
 
 // Returns an object initialized with the following values
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObject.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObject.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObject.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObject.h	2016-05-21 07:49:58.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSManagedObject.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -16,7 +16,7 @@
 @class NSError;
 @class NSManagedObjectContext;
 @class NSManagedObjectID;
-
+@class NSFetchRequest;
 
 typedef NS_OPTIONS(NSUInteger, NSSnapshotEventType) {
 	NSSnapshotEventUndoInsertion = 1 << 1,
@@ -29,27 +29,27 @@
 
 NS_CLASS_AVAILABLE(10_4,3_0) NS_REQUIRES_PROPERTY_DEFINITIONS
 @interface NSManagedObject : NSObject {
-@private
-    int32_t             _cd_rc;
-    uintptr_t           _cd_stateFlags;
-    id                  _cd_rawData;
-    id                  _cd_entity;
-    NSManagedObjectContext* _cd_managedObjectContext;
-    NSManagedObjectID*  _cd_objectID;
-    uintptr_t           _cd_extraFlags;
-    id                  _cd_observationInfo;
-    id*                 _cd_snapshots;
-    uintptr_t           _cd_lockingInfo;
-    id                  _cd_queueReference;
 }
 
 /*  Distinguish between changes that should and should not dirty the object for any key unknown to Core Data.  10.5 & earlier default to NO.  10.6 and later default to YES. */
 /*    Similarly, transient attributes may be individually flagged as not dirtying the object by adding +(BOOL)contextShouldIgnoreChangesFor<key> where <key> is the property name. */
-+ (BOOL)contextShouldIgnoreUnmodeledPropertyChanges NS_AVAILABLE(10_6,3_0);
+@property(class, readonly) BOOL contextShouldIgnoreUnmodeledPropertyChanges NS_AVAILABLE(10_6,3_0);
+
+/* The Entity represented by this subclass. This method is only legal to call on subclasses of NSManagedObject that represent a single entity in the model.
+ */
++ (NSEntityDescription*)entity NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+
+/* A new fetch request initialized with the Entity represented by this subclass. This property's getter is only legal to call on subclasses of NSManagedObject that represent a single entity in the model.
+ */
++ (NSFetchRequest*)fetchRequest NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
 
 // The designated initializer.
 - (__kindof NSManagedObject*)initWithEntity:(NSEntityDescription *)entity insertIntoManagedObjectContext:(nullable NSManagedObjectContext *)context NS_DESIGNATED_INITIALIZER;
 
+/* Returns a new object, inserted into managedObjectContext. This method is only legal to call on subclasses of NSManagedObject that represent a single entity in the model.
+ */
+-(instancetype)initWithContext:(NSManagedObjectContext*)moc NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+
 // identity
 @property (nullable, nonatomic, readonly, assign) NSManagedObjectContext *managedObjectContext;
 @property (nonatomic, readonly, strong) NSEntityDescription *entity;
@@ -132,7 +132,7 @@
 - (NSDictionary<NSString *, id> *)changedValuesForCurrentEvent NS_AVAILABLE(10_7, 5_0);
 
 // validation - in addition to KVC validation managed objects have hooks to validate their lifecycle state; validation is a critical piece of functionality and the following methods are likely the most commonly overridden methods in custom subclasses
-- (BOOL)validateValue:(id __nullable * __nonnull)value forKey:(NSString *)key error:(NSError **)error;    // KVC
+- (BOOL)validateValue:(id _Nullable * _Nonnull)value forKey:(NSString *)key error:(NSError **)error;    // KVC
 - (BOOL)validateForDelete:(NSError **)error;
 - (BOOL)validateForInsert:(NSError **)error;
 - (BOOL)validateForUpdate:(NSError **)error;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h	2016-05-26 06:23:56.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSManagedObjectContext.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -23,6 +23,7 @@
 @class NSPersistentStore;
 @class NSPersistentStoreCoordinator;
 @class NSPropertyDescription;
+@class NSQueryGenerationToken;
 @class NSUndoManager;
 @class NSNotification;
 
@@ -41,6 +42,8 @@
 COREDATA_EXTERN NSString * const NSRefreshedObjectsKey NS_AVAILABLE(10_5, 3_0);
 COREDATA_EXTERN NSString * const NSInvalidatedObjectsKey NS_AVAILABLE(10_5, 3_0);
 
+COREDATA_EXTERN NSString * const NSManagedObjectContextQueryGenerationKey NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+
 // User info keys for NSManagedObjectContextObjectsDidChangeNotification:  the values for these keys are arrays of objectIDs
 COREDATA_EXTERN NSString * const NSInvalidatedAllObjectsKey NS_AVAILABLE(10_5, 3_0); // All objects in the context have been invalidated
 
@@ -67,62 +70,6 @@
 
 NS_CLASS_AVAILABLE(10_4,3_0)
 @interface NSManagedObjectContext : NSObject <NSCoding> {
-@private
-  volatile id _queueOwner;
-  void *_dispatchQueue;
-  void* _reserved1;
-  int32_t _spinLock;
-  id _parentObjectStore;
-  struct _managedObjectContextFlags {
-      unsigned int _registeredForCallback:1;
-      unsigned int _propagatesDeletesAtEndOfEvent:1;
-      unsigned int _exhaustiveValidation:1;
-      unsigned int _processingChanges:1;
-      unsigned int _useCommittedSnapshot:1;
-      unsigned int _registeredUndoTransactionID:1;
-      unsigned int _retainsAllRegisteredObjects:1;
-      unsigned int _savingInProgress:1;
-      unsigned int _wasDisposed:1;
-      unsigned int _unprocessedChangesPending:1;
-      unsigned int _isDirty:1;
-      unsigned int _ignoreUndoCheckpoints:1;
-	  unsigned int _propagatingDeletes:1;
-	  unsigned int _isNSEditorEditing:1;
-      unsigned int _isMainThreadBlessed:1;
-      unsigned int _isImportContext:1;
-      unsigned int _preflightSaveInProgress:1;
-      unsigned int _disableDiscardEditing:1;
-      unsigned int _isParentStoreContext:1;
-      unsigned int _postSaveNotifications:1;
-      unsigned int _isMerging:1;
-      unsigned int _concurrencyType:1;
-      unsigned int _deleteInaccessible:1;
-      unsigned int _reservedFlags:9;
-  } _flags;
-  NSMutableSet *_unprocessedChanges;
-  NSMutableSet *_unprocessedDeletes;
-  NSMutableSet *_unprocessedInserts;
-  NSMutableSet *_insertedObjects;
-  NSMutableSet *_deletedObjects;
-  NSMutableSet *_changedObjects;
-  NSMutableSet *_lockedObjects;
-  NSMutableSet *_refreshedObjects;
-  id _infoByGID;
-  id *_cachedObsInfoByEntity;
-  short _undoTransactionID;
-  id _lock;
-  long _lockCount;
-  long _objectStoreLockCount;
-  NSTimeInterval _fetchTimestamp;
-  intptr_t _referenceCallbackRegistration;
-  id _referenceQueue;
-  id _reserved3;
-  id _reserved4;
-  int32_t _cd_rc;
-  int32_t _ignoreChangeNotification;
-  id _reserved6;
-  NSString* _contextLabel;
-  id* _additionalPrivateIvars;
 }
 
 + (instancetype)new NS_DEPRECATED(10_4,10_11,3_0,9_0, "Use -initWithConcurrencyType: instead");
@@ -162,7 +109,7 @@
 - (nullable NSArray *)executeFetchRequest:(NSFetchRequest *)request error:(NSError **)error;
 
 // returns the number of objects a fetch request would have returned if it had been passed to -executeFetchRequest:error:.   If an error occurred during the processing of the request, this method will return NSNotFound. 
-- (NSUInteger) countForFetchRequest: (NSFetchRequest *)request error: (NSError **)error NS_AVAILABLE(10_5, 3_0);    
+- (NSUInteger) countForFetchRequest: (NSFetchRequest *)request error: (NSError **)error NS_AVAILABLE(10_5, 3_0) __attribute__((swift_error(nonnull_error)));
 
 // Method to pass a request to the store without affecting the contents of the managed object context.
 // Will return an NSPersistentStoreResult which may contain additional information about the result of the action
@@ -231,12 +178,48 @@
 - (void)mergeChangesFromContextDidSaveNotification:(NSNotification *)notification NS_AVAILABLE(10_5, 3_0);
 
 /* Similar to mergeChangesFromContextDidSaveNotification, this method handles changes from potentially other processes or serialized state.  It more efficiently
-     * merges changes into multiple contexts, as well as nested context. The keys in the dictionary should be one those from an
-     *  NSManagedObjectContextObjectsDidChangeNotification: NSInsertedObjectsKey, NSUpdatedObjectsKey, etc.
-     *  the values should be an NSArray of either NSManagedObjectID or NSURL objects conforming to valid results from -URIRepresentation
-     */
+ * merges changes into multiple contexts, as well as nested context. The keys in the dictionary should be one those from an
+ *  NSManagedObjectContextObjectsDidChangeNotification: NSInsertedObjectsKey, NSUpdatedObjectsKey, etc.
+ *  the values should be an NSArray of either NSManagedObjectID or NSURL objects conforming to valid results from -URIRepresentation
+ */
 + (void)mergeChangesFromRemoteContextSave:(NSDictionary*)changeNotificationData intoContexts:(NSArray<NSManagedObjectContext*> *)contexts NS_AVAILABLE(10_11,9_0);
 
+/* Return the query generation currently in use by this context. Will be one of the following:
+ * - nil, default value
+ * - this context is not using generational querying
+ * - an opaque token
+ * - specifies the generation of data this context is vending
+ *
+ * All child contexts will return nil.
+ */
+@property (nullable, nonatomic, strong, readonly) NSQueryGenerationToken *queryGenerationToken NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+
+/* Set the query generation this context should use. Must be one of the following values:
+ * - nil
+ * - this context will not use generational querying
+ * - the value returned by +[NSQueryGenerationToken currentQueryGenerationToken]
+ * - this context will pin itself to the generation of the database when it first loads data
+ * - the result of calling -[NSManagedObjectContext queryGenerationToken] on another managed object context
+ * - this context will be set to whatever query generation the original context is currently using;
+ *
+ * Query generations are for fetched data only; they are not used during saving. If a pinned context saves,
+ * its query generation will be updated after the save.
+ *
+ * All nested contexts will defer to their parent context’s data. It is a programmer error to try to set
+ * the queryGenerationToken on a child context.
+ *
+ * Query generations are tracked across the union of stores. Additions to the persistent store coordinator's
+ * persistent stores will be ignored until the context's query generation is updated to include them.
+ *
+ * May partially fail if one or more stores being tracked by the token are removed from the persistent
+ * store coordinator.
+ */
+- (BOOL)setQueryGenerationFromToken:(nullable NSQueryGenerationToken *)generation error:(NSError **)error NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+
+/* Whether the context automatically merges changes saved to its parent. Setting this property to YES when the context is pinned to a non-current query generation is not supported.
+*/
+@property (nonatomic) BOOL automaticallyMergesChangesFromParent NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectID.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectID.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectID.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectID.h	2016-05-21 07:41:58.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSManagedObjectID.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectModel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectModel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectModel.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectModel.h	2016-05-26 06:17:01.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSManagedObjectModel.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -19,21 +19,6 @@
 // Models describe object graphs to be managed. Models (and their entities/properties/fetch request templates) are editable until they are used by a persistent store coordinator, allowing developers to create/modify them dynamically. However, once a model is being used, it MUST NOT be changed. When the persistent store coordinator first fetches data using a model, it will become uneditable. Any attempt to mutate a model or any of its subobjects after that point will cause an exception to be thrown. If you need to modify a model that is in use, create a copy, modify the copy, and then discard the objects with the old model.
 NS_CLASS_AVAILABLE(10_4,3_0)
 @interface NSManagedObjectModel : NSObject <NSCoding, NSCopying, NSFastEnumeration> {
-@private
-	id _dataForOptimization;
-	id *_optimizationHints; 
-    id _localizationPolicy;
-    NSMutableDictionary *_entities;
-    NSMutableDictionary *_configurations;
-    NSMutableDictionary *_fetchRequestTemplates;
-	NSSet *_versionIdentifiers;
-    struct __managedObjectModelFlags {
-        unsigned int _isInUse:1;
-        unsigned int _isImmutable:1;
-		unsigned int _isOptimizedForEncoding:1;
-        unsigned int _hasEntityWithConstraints:1;
-        unsigned int _reservedEntityDescription:28;
-    } _managedObjectModelFlags;
 }
 
 + (nullable NSManagedObjectModel *)mergedModelFromBundles:(nullable NSArray<NSBundle *> *)bundles;    // looks up all models in the specified bundles and merges them; if nil is specified as argument, uses the main bundle
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMappingModel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMappingModel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMappingModel.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMappingModel.h	2016-05-21 07:41:58.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSMappingModel.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -17,6 +17,7 @@
 
 NS_CLASS_AVAILABLE(10_5,3_0)
 @interface NSMappingModel: NSObject {
+#if (!__OBJC2__)
     @private
     void *_reserved;
     void *_reserved1;
@@ -27,7 +28,7 @@
         unsigned int _isInUse:1;
         unsigned int _reservedModelMapping:31;
     } _modelMappingFlags;
-
+#endif
 }
 
 /* Returns the mapping model to translate data from the source to the destination model.  This method is a companion to the mergedModelFromBundles: methods;  in this case, the framework uses the version information from the models to locate the appropriate mapping model in the available bundles.  If the mapping model for the models cannot be found, this method returns nil. 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMergePolicy.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMergePolicy.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMergePolicy.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMergePolicy.h	2016-05-26 06:23:56.000000000 +0200
@@ -1,7 +1,7 @@
 //
 //  NSMergePolicy.h
 //  Core Data
-//  Copyright (c) 2004-2015, Apple Inc. All rights reserved.
+//  Copyright (c) 2004-2016, Apple Inc. All rights reserved.
 //
 
 #import <Foundation/NSArray.h>
@@ -40,13 +40,6 @@
 
 NS_CLASS_AVAILABLE(10_7, 5_0)
 @interface NSMergeConflict : NSObject {
-@private
-    id _source;
-    id _snapshot1;
-    id _snapshot2;
-    id _snapshot3;
-    NSUInteger _newVersion;
-    NSUInteger _oldVersion;
 }
 
 @property (readonly, retain) NSManagedObject* sourceObject;
@@ -83,13 +76,6 @@
  */
 NS_CLASS_AVAILABLE(10_11, 9_0)
 @interface NSConstraintConflict : NSObject {
-@private
-    NSArray *_constraint;
-    NSManagedObject *_databaseObject;
-    NSDictionary *_databaseSnapshot;
-    NSDictionary *_conflictedValues;
-    NSArray *_conflictingObjects;
-    NSArray *_conflictingSnapshots;
 }
 
 @property (readonly, retain) NSArray<NSString*> *constraint; // The constraint which has been violated.
@@ -119,12 +105,14 @@
 
 NS_CLASS_AVAILABLE(10_7, 5_0)
 @interface NSMergePolicy : NSObject {
-@private
-    NSUInteger _type;
-    void* _reserved2;
-    void* _reserved3;
 }
 
+@property (class, readonly, strong) NSMergePolicy *errorMergePolicy NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+@property (class, readonly, strong) NSMergePolicy *rollbackMergePolicy NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+@property (class, readonly, strong) NSMergePolicy *overwriteMergePolicy NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+@property (class, readonly, strong) NSMergePolicy *mergeByPropertyObjectTrumpMergePolicy NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+@property (class, readonly, strong) NSMergePolicy *mergeByPropertyStoreTrumpMergePolicy NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+
 @property (readonly) NSMergePolicyType mergeType;
 
 /*
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMigrationManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMigrationManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMigrationManager.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMigrationManager.h	2016-05-26 06:23:57.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSMigrationManager.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -21,26 +21,6 @@
 
 NS_CLASS_AVAILABLE(10_5, 3_0)
 @interface NSMigrationManager : NSObject {
-    @private
-    NSManagedObjectModel *_sourceModel;
-    NSDictionary *_sourceEntitiesByVersionHash;
-    NSManagedObjectModel *_destinationModel;
-    NSDictionary *_destinationEntitiesByVersionHash;
-    NSMappingModel *_mappingModel;
-    NSManagedObjectContext *_sourceManagedObjectContext;
-    NSManagedObjectContext *_destinationManagedObjectContext;
-    NSMigrationContext *_migrationContext;
-    NSDictionary *_userInfo;
-    struct _migrationManagerFlags {
-        unsigned int _migrationWasCancelled:1;
-        unsigned int _usesStoreSpecificMigrationManager:1;
-        unsigned int _reservedMigrationManager:30;
-    } _migrationManagerFlags;
-	NSError *_migrationCancellationError;
-	id _reserved1;
-	id _reserved2;
-	id _reserved3;
-	id _reserved4;
 }
 
 /* Creates a migration manager instance with the corresponding source and destination models.  (All validation of the arguments is performed during migrateStoreFromURL:toURL:)  As with the NSPersistentStoreCoordinator, once models are added to the migration manager they are immutable and cannot be altered.*/
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentContainer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentContainer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentContainer.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentContainer.h	2016-05-21 07:41:59.000000000 +0200
@@ -0,0 +1,53 @@
+/*
+ NSPersistentContainer.h
+ Core Data
+ Copyright (c) 2016, Apple Inc.
+ All rights reserved.
+ */
+
+#import <Foundation/NSArray.h>
+#import <Foundation/NSURL.h>
+#import <CoreData/NSManagedObjectContext.h>
+#import <CoreData/NSPersistentStoreCoordinator.h>
+#import <CoreData/NSManagedObjectModel.h>
+#import <CoreData/NSPersistentStoreDescription.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+// An instance of NSPersistentContainer includes all objects needed to represent a functioning Core Data stack, and provides convenience methods and properties for common patterns.
+NS_CLASS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0)
+@interface NSPersistentContainer : NSObject {
+#if (!__OBJC2__)
+@private
+    id _name;
+    NSManagedObjectContext *_viewContext;
+    id _storeCoordinator;
+    id _storeDescriptions;
+#endif
+}
+
++ (instancetype)persistentContainerWithName:(NSString *)name;
++ (instancetype)persistentContainerWithName:(NSString *)name managedObjectModel:(NSManagedObjectModel *)model;
+
++ (NSURL *)defaultDirectoryURL;
+
+@property (copy, readonly) NSString *name;
+@property (strong, readonly) NSManagedObjectContext *viewContext;
+@property (strong, readonly) NSManagedObjectModel *managedObjectModel;
+@property (strong, readonly) NSPersistentStoreCoordinator *persistentStoreCoordinator;
+@property (copy) NSArray<NSPersistentStoreDescription *> *persistentStoreDescriptions;
+
+// Creates a container using the model named `name` in the main bundle, or the merged model (from the main bundle) if no match was found.
+- (instancetype)initWithName:(NSString *)name;
+
+- (instancetype)initWithName:(NSString *)name managedObjectModel:(NSManagedObjectModel *)model NS_DESIGNATED_INITIALIZER;
+
+// Load stores from the storeDescriptions property that have not already been successfully added to the container. The completion handler is called once for each store that succeeds or fails.
+- (void)loadPersistentStoresWithCompletionHandler:(void (^)(NSPersistentStoreDescription *, NSError * _Nullable))block;
+
+- (NSManagedObjectContext *)newBackgroundContext NS_RETURNS_RETAINED;
+- (void)performBackgroundTask:(void (^)(NSManagedObjectContext *))block;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStore.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStore.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStore.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStore.h	2016-05-21 07:41:59.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSPersistentStore.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -23,22 +23,6 @@
 
 NS_CLASS_AVAILABLE(10_5, 3_0)
 @interface NSPersistentStore : NSObject {
-    @private
-    __weak NSPersistentStoreCoordinator *_coordinator;
-    NSString *_configurationName;
-    NSURL *_url;
-    NSDictionary *_options;
-    id* _oidFactories;
-    id _defaultFaultHandler;
-    struct _objectStoreFlags {
-        unsigned int isReadOnly:1;
-        unsigned int cleanOnRemove:1;
-        unsigned int isMDDirty:1;
-        unsigned int _RESERVED:29;
-    } _flags;
-	void *_temporaryIDClass;
-	id _externalRecordsMonitor;
-	void *_reserved3;
 }
 
 /* Get metadata from the persistent store at url. Must be overriden by subclasses.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreCoordinator.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreCoordinator.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreCoordinator.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreCoordinator.h	2016-05-21 07:49:57.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSPersistentStoreCoordinator.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -21,6 +21,7 @@
 @class NSManagedObjectContext;
 @class NSPersistentStore;
 @class NSPersistentStoreRequest;
+@class NSPersistentStoreDescription;
 
 // Persistent store types supported by Core Data:
 COREDATA_EXTERN NSString * const NSSQLiteStoreType NS_AVAILABLE(10_4, 3_0);
@@ -28,7 +29,6 @@
 COREDATA_EXTERN NSString * const NSBinaryStoreType NS_AVAILABLE(10_4, 3_0);
 COREDATA_EXTERN NSString * const NSInMemoryStoreType NS_AVAILABLE(10_4, 3_0);
 
-
 // Persistent store metadata dictionary keys:
 
 // key in the metadata dictionary to identify the store type
@@ -105,6 +105,9 @@
 */
 COREDATA_EXTERN NSString * const NSPersistentStoreOSCompatibility NS_AVAILABLE(10_5, 3_0);
 
+/* User info key specifying the maximum connection pool size that should be used on a store that supports concurrent request handling, the value should be an NSNumber. The connection pool size determines the number of requests a store can handle concurrently, and should be a function of how many contexts are attempting to access store data at any time. Generally, application developers should not set this, and should use the default value. The default connection pool size is implementation dependent and may vary by store type and/or platform.
+ */
+COREDATA_EXTERN NSString * const NSPersistentStoreConnectionPoolMaxSizeKey NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
 
 /* store option for the destroy... and replace... to indicate that the store file should be destroyed even if the operation might be unsafe (overriding locks
  */
@@ -115,20 +118,6 @@
 
 NS_CLASS_AVAILABLE(10_4,3_0)
 @interface NSPersistentStoreCoordinator : NSObject {
-@private
-    volatile id _queueOwner;
-    void *_dispatchQueue;
-    struct _persistentStoreCoordinatorFlags {
-        unsigned int _isRegistered:1;
-        unsigned int _reservedFlags:31;
-    } _flags;
-#ifdef __LP64__
-	uint32_t _reserved32;
-#endif
-    long _miniLock;
-    id *_additionalPrivateIvars;
-    NSManagedObjectModel *_managedObjectModel;
-    NSArray *_persistentStores;
 }
 
 - (instancetype)initWithManagedObjectModel:(NSManagedObjectModel *)model NS_DESIGNATED_INITIALIZER;
@@ -151,6 +140,8 @@
  */
 - (nullable __kindof NSPersistentStore *)addPersistentStoreWithType:(NSString *)storeType configuration:(nullable NSString *)configuration URL:(nullable NSURL *)storeURL options:(nullable NSDictionary *)options error:(NSError **)error;
 
+- (void)addPersistentStoreWithDescription:(NSPersistentStoreDescription *)storeDescription completionHandler:(void (^)(NSPersistentStoreDescription *, NSError * _Nullable))block NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+
 - (BOOL)removePersistentStore:(NSPersistentStore *)store error:(NSError **)error;
 
 /* Sets the metadata stored in the persistent store during the next save operation executed on it; the store type and UUID (NSStoreTypeKey and NSStoreUUIDKey) are always added automatically (but NSStoreUUIDKey is only added if it is not set manually as part of the dictionary argument)
@@ -174,8 +165,7 @@
 
 /* Returns a dictionary of the registered store types:  the keys are the store type strings and the values are the NSPersistentStore subclasses wrapped in NSValues.
 */
-
-+ (NSDictionary<NSString *, NSValue*> *)registeredStoreTypes NS_AVAILABLE(10_5, 3_0);
+@property(class, readonly, strong) NSDictionary<NSString *, NSValue *> *registeredStoreTypes NS_AVAILABLE(10_5, 3_0);
 
 /* Registers the specified NSPersistentStore subclass for the specified store type string.  This method must be invoked before a custom subclass of NSPersistentStore can be loaded into a persistent store coordinator.  Passing nil for the store class argument will unregister the specified store type.
 */
@@ -186,11 +176,6 @@
 + (nullable NSDictionary<NSString *, id> *)metadataForPersistentStoreOfType:(NSString*)storeType URL:(NSURL *)url options:(nullable NSDictionary *)options error:(NSError **)error NS_AVAILABLE(10_9,7_0);
 + (BOOL)setMetadata:(nullable NSDictionary<NSString *, id> *)metadata forPersistentStoreOfType:(NSString*)storeType URL:(NSURL*)url options:(nullable NSDictionary*)options error:(NSError**)error NS_AVAILABLE(10_9,7_0);
     
-+ (nullable NSDictionary<NSString *, id> *)metadataForPersistentStoreOfType:(nullable NSString *)storeType URL:(NSURL *)url error:(NSError **)error NS_DEPRECATED(10_5,10_11,3_0,9_0, "Use a -metadataForPersistentStoreOfType:URL:options:error: and pass in an options dictionary matching addPersistentStoreWithType");
-+ (BOOL)setMetadata:(nullable NSDictionary<NSString *, id> *)metadata forPersistentStoreOfType:(nullable NSString *)storeType URL:(NSURL*)url error:(NSError **)error NS_DEPRECATED(10_5, 10_11,3_0,9_0,"Use a -setMetadata:forPersistentStoreOfType:URL:options:error: and pass in an options dictionary matching addPersistentStoreWithType");
-    
-
-
 /* Used for save as - performance may vary depending on the type of old and new store; the old store is usually removed from the coordinator by the migration operation, and therefore is no longer a useful reference after invoking this method
 */
 - (nullable NSPersistentStore *)migratePersistentStore:(NSPersistentStore *)store toURL:(NSURL *)URL options:(nullable NSDictionary *)options withType:(NSString *)storeType error:(NSError **)error;
@@ -210,6 +195,14 @@
 - (void)performBlockAndWait:(void (^)())block  NS_AVAILABLE(10_10, 8_0);
 
 
++ (nullable NSDictionary<NSString *, id> *)metadataForPersistentStoreOfType:(nullable NSString *)storeType URL:(NSURL *)url error:(NSError **)error NS_DEPRECATED(10_5,10_11,3_0,9_0, "Use a -metadataForPersistentStoreOfType:URL:options:error: and pass in an options dictionary matching addPersistentStoreWithType");
+    
++ (BOOL)setMetadata:(nullable NSDictionary<NSString *, id> *)metadata forPersistentStoreOfType:(nullable NSString *)storeType URL:(NSURL*)url error:(NSError **)error NS_DEPRECATED(10_5, 10_11,3_0,9_0,"Use a -setMetadata:forPersistentStoreOfType:URL:options:error: and pass in an options dictionary matching addPersistentStoreWithType");
+    
+
 @end
 
+
+    
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreDescription.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreDescription.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreDescription.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreDescription.h	2016-05-21 07:41:58.000000000 +0200
@@ -0,0 +1,53 @@
+/*
+ NSPersistentStoreDescription.h
+ Core Data
+ Copyright (c) 2016, Apple Inc.
+ All rights reserved.
+ */
+
+#import <Foundation/NSArray.h>
+#import <Foundation/NSDictionary.h>
+#import <Foundation/NSURL.h>
+
+
+NS_ASSUME_NONNULL_BEGIN
+
+// An instance of NSPersistentStoreDescription encapsulates all information needed to describe a persistent store.
+NS_CLASS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0)
+@interface NSPersistentStoreDescription : NSObject <NSCopying> {
+#if (!__OBJC2__)
+@private
+    id _type;
+    id _configuration;
+    id _url;
+    id _options;
+#endif
+}
+
++ (instancetype)persistentStoreDescriptionWithURL:(NSURL *)URL;
+
+@property (copy) NSString *type;
+@property (copy, nullable) NSString *configuration;
+@property (copy, nullable) NSURL *URL;
+@property (nonatomic, copy, readonly) NSDictionary<NSString *, NSObject *> *options;
+
+- (void)setOption:(nullable NSObject *)option forKey:(NSString *)key;
+
+// Store options
+@property (getter = isReadOnly) BOOL readOnly;
+@property NSTimeInterval timeout;
+@property (nonatomic, copy, readonly) NSDictionary<NSString *, NSObject *> *sqlitePragmas;
+
+- (void)setValue:(nullable NSObject *)value forPragmaNamed:(NSString *)name;
+
+// addPersistentStore-time behaviours
+@property BOOL shouldAddStoreAsynchronously;
+@property BOOL shouldMigrateStoreAutomatically;
+@property BOOL shouldInferMappingModelAutomatically;
+
+// Returns a store description instance with default values for the store located at `URL` that can be used immediately with `addPersistentStoreWithDescription:completionHandler:`.
+- (instancetype)initWithURL:(NSURL *)url NS_DESIGNATED_INITIALIZER;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreRequest.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreRequest.h	2016-05-21 07:41:59.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  NSPersistentStoreRequest.h
  Core Data
- Copyright (c) 2004-2015, Apple Inc.
+ Copyright (c) 2004-2016, Apple Inc.
  All rights reserved.
  */
 
@@ -9,8 +9,6 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class NSFetchRequest;
-@class NSAsynchronousFetchResult;
 @class NSPersistentStore;
 
 typedef NS_ENUM(NSUInteger, NSPersistentStoreRequestType) {
@@ -22,8 +20,6 @@
 
 NS_CLASS_AVAILABLE(10_7, 5_0)
 @interface NSPersistentStoreRequest : NSObject <NSCopying> {
-	@private
-	NSArray *_affectedStores;
 }
 
 // Stores this request should be sent to.
@@ -34,22 +30,4 @@
 
 @end
 
-typedef void (^NSPersistentStoreAsynchronousFetchResultCompletionBlock)(NSAsynchronousFetchResult *result);
-
-
-NS_CLASS_AVAILABLE(10_10,8_0)
-@interface NSAsynchronousFetchRequest : NSPersistentStoreRequest {
-@private
-    NSFetchRequest* _fetchRequest;
-    id _requestCompletionBlock;
-    NSInteger _estimatedResultCount;
-}
-@property (strong, readonly) NSFetchRequest* fetchRequest;
-@property (nullable, strong, readonly) NSPersistentStoreAsynchronousFetchResultCompletionBlock completionBlock;
-@property (nonatomic) NSInteger estimatedResultCount;
-
-- (instancetype)initWithFetchRequest:(NSFetchRequest*)request completionBlock:(nullable NSPersistentStoreAsynchronousFetchResultCompletionBlock)blk;
-
-@end
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreResult.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreResult.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreResult.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreResult.h	2016-05-21 07:41:58.000000000 +0200
@@ -1,11 +1,11 @@
 /*
  NSPersistentStoreResult.h
  Core Data
- Copyright (c) 2004-2015, Apple Inc.
+ Copyright (c) 2004-2016, Apple Inc.
  All rights reserved.
  */
 #import <Foundation/NSArray.h>
-#import <CoreData/NSPersistentStoreRequest.h>
+#import <CoreData/NSFetchRequest.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -38,12 +38,14 @@
 
 NS_CLASS_AVAILABLE(10_10, 8_0)
 @interface NSPersistentStoreAsynchronousResult : NSPersistentStoreResult {
+#if (!__OBJC2__)
 @private
     NSProgress* _requestProgress;
     NSError* _requestError;
     NSManagedObjectContext* _requestContext;
     id _requestCompletionBlock;
     int32_t _flags;
+#endif
 }
 
 @property (strong, readonly) NSManagedObjectContext* managedObjectContext;
@@ -55,25 +57,28 @@
 @end
 
 NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface NSAsynchronousFetchResult : NSPersistentStoreAsynchronousResult {
+@interface NSAsynchronousFetchResult<ResultType:id<NSFetchRequestResult>> : NSPersistentStoreAsynchronousResult {
+#if (!__OBJC2__)
 @private
     NSAsynchronousFetchRequest* _fetchRequest;
     NSArray* _finalResult;
     id _intermediateResultCallback;
+#endif
 }
 
-@property (strong, readonly) NSAsynchronousFetchRequest* fetchRequest;
-@property (nullable, strong, readonly) NSArray * finalResult;
+@property (strong, readonly) NSAsynchronousFetchRequest<ResultType> * fetchRequest;
+@property (nullable, strong, readonly) NSArray<ResultType> * finalResult;
 
 @end
 
 // The result returned when executing an NSBatchUpdateRequest
 NS_CLASS_AVAILABLE(10_10,8_0)
 @interface NSBatchUpdateResult : NSPersistentStoreResult {
+#if (!__OBJC2__)
 @private
     id _aggregatedResult;
     NSBatchUpdateRequestResultType _resultType;
- 
+#endif
 }
 
 // Return the result. See NSBatchUpdateRequestResultType for options
@@ -86,10 +91,11 @@
 // The result returned when executing an NSBatchDeleteRequest
 NS_CLASS_AVAILABLE(10_11,9_0)
 @interface NSBatchDeleteResult : NSPersistentStoreResult {
+#if (!__OBJC2__)
 @private
     id _aggregatedResult;
     NSBatchDeleteRequestResultType _resultType;
-    
+#endif
 }
 
 // Return the result. See NSBatchDeleteRequestResultType for options
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyDescription.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyDescription.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyDescription.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyDescription.h	2016-05-21 07:41:59.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSPropertyDescription.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -17,29 +17,6 @@
 // Properties describe values within a managed object. There are different types of properties, each of them represented by a subclass which encapsulates the specific property behavior.
 NS_CLASS_AVAILABLE(10_4,3_0)
 @interface NSPropertyDescription : NSObject <NSCoding, NSCopying> {
-@private
-	NSString *_versionHashModifier;
-	id _underlyingProperty;
-	NSData *_versionHash;
-    __weak NSEntityDescription *_entity;
-    NSString *_name;
-    NSArray *_validationPredicates;
-    NSArray *_validationWarnings;
-    struct __propertyDescriptionFlags {
-        unsigned int _isReadOnly:1;
-        unsigned int _isTransient:1;
-        unsigned int _isOptional:1;
-        unsigned int _isIndexed:1;
-        unsigned int _skipValidation:1;
-        unsigned int _isIndexedBySpotlight:1;
-        unsigned int _isStoredInExternalRecord:1;
-		unsigned int _extraIvarsAreInDataBlob:1;
-        unsigned int _isOrdered:1;
-        unsigned int _reservedPropertyDescription:23;
-    } _propertyDescriptionFlags;    
-    __strong void *_extraIvars;
-    NSMutableDictionary *_userInfo;
-	long _entitysReferenceIDForProperty;
 }
 
 @property (nonatomic, readonly, assign) NSEntityDescription *entity;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyMapping.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyMapping.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyMapping.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyMapping.h	2016-05-21 07:41:58.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSPropertyMapping.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -15,6 +15,7 @@
 
 NS_CLASS_AVAILABLE(10_5,3_0)
 @interface NSPropertyMapping : NSObject {
+#if (!__OBJC2__)
     @private
     void *_reserved;
     NSArray *_transformValidations;
@@ -26,6 +27,7 @@
         unsigned int _isInUse:1;
         unsigned int _reservedPropertyMapping:31;
     } _propertyMappingFlags;
+#endif
 }
 
 /* Returns/sets the name of the property in the destination entity for the mapping.  
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSQueryGenerationToken.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSQueryGenerationToken.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSQueryGenerationToken.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSQueryGenerationToken.h	2016-05-21 07:41:58.000000000 +0200
@@ -0,0 +1,21 @@
+//
+//  NSQueryGenerationToken.h
+//  Core Data
+//  Copyright (c) 2016, Apple Inc. All rights reserved.
+//
+
+#import <Foundation/NSArray.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0)
+// Class used to track database generations for generational querying.
+// See NSManagedObjectContext for details on how it is used.
+@interface NSQueryGenerationToken : NSObject <NSCopying> 
+
+@property (class, readonly, strong) NSQueryGenerationToken *currentQueryGenerationToken; // Used to inform a context that it should use the current generation
+
+@end
+
+NS_ASSUME_NONNULL_END
+
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSRelationshipDescription.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSRelationshipDescription.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSRelationshipDescription.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSRelationshipDescription.h	2016-05-21 07:41:59.000000000 +0200
@@ -1,7 +1,7 @@
 /*
     NSRelationshipDescription.h
     Core Data
-    Copyright (c) 2004-2015, Apple Inc.
+    Copyright (c) 2004-2016, Apple Inc.
     All rights reserved.
 */
 
@@ -22,16 +22,6 @@
 // Relationships represent references to other objects. They usually come in pairs, where the reference back is called the "inverse".
 NS_CLASS_AVAILABLE(10_4,3_0)
 @interface NSRelationshipDescription : NSPropertyDescription {
-@private
-	void *_reserved5;
-	void *_reserved6;
-    __weak NSEntityDescription *_destinationEntity;
-    NSString *_lazyDestinationEntityName;
-    NSRelationshipDescription *_inverseRelationship;
-    NSString *_lazyInverseRelationshipName;
-    unsigned long _maxCount;
-    unsigned long _minCount;
-    NSDeleteRule _deleteRule;
 }
 
 @property (nullable, nonatomic, assign) NSEntityDescription *destinationEntity;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSSaveChangesRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSSaveChangesRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSSaveChangesRequest.h	2015-08-07 22:19:59.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSSaveChangesRequest.h	2016-05-21 07:41:59.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  NSSaveChangesRequest.h
  Core Data
- Copyright (c) 2004-2015, Apple Inc.
+ Copyright (c) 2004-2016, Apple Inc.
  All rights reserved.
  */
 
@@ -16,13 +16,6 @@
 
 NS_CLASS_AVAILABLE(10_7,5_0)
 @interface NSSaveChangesRequest : NSPersistentStoreRequest {
-@private
-    NSSet *_insertedObjects;
-    NSSet *_updatedObjects;
-    NSSet *_deletedObjects;
-    NSSet* _optimisticallyLockedObjects;
-    uintptr_t _flags;
-    void* _reserved1;
 }
 
 // Default initializer.

```