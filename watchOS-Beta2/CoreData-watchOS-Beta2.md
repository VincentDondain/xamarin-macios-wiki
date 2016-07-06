#CoreData.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataErrors.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataErrors.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataErrors.h	2016-05-26 06:17:02.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataErrors.h	2016-06-27 06:09:43.000000000 +0200
@@ -15,19 +15,19 @@
 NS_ASSUME_NONNULL_BEGIN
 
 // User info keys for errors created by Core Data:
-COREDATA_EXTERN NSString * const NSDetailedErrorsKey NS_AVAILABLE(10_4,3_0);           // if multiple validation errors occur in one operation, they are collected in an array and added with this key to the "top-level error" of the operation
+COREDATA_EXTERN NSString * const NSDetailedErrorsKey API_AVAILABLE(macosx(10.4),ios(3.0));           // if multiple validation errors occur in one operation, they are collected in an array and added with this key to the "top-level error" of the operation
 
-COREDATA_EXTERN NSString * const NSValidationObjectErrorKey NS_AVAILABLE(10_4,3_0);    // object that failed to validate for a validation error
-COREDATA_EXTERN NSString * const NSValidationKeyErrorKey NS_AVAILABLE(10_4,3_0);       // key that failed to validate for a validation error
-COREDATA_EXTERN NSString * const NSValidationPredicateErrorKey NS_AVAILABLE(10_4,3_0); // for predicate-based validation, the predicate for the condition that failed to validate
-COREDATA_EXTERN NSString * const NSValidationValueErrorKey NS_AVAILABLE(10_4,3_0);     // if non-nil, the value for the key that failed to validate for a validation error
+COREDATA_EXTERN NSString * const NSValidationObjectErrorKey API_AVAILABLE(macosx(10.4),ios(3.0));    // object that failed to validate for a validation error
+COREDATA_EXTERN NSString * const NSValidationKeyErrorKey API_AVAILABLE(macosx(10.4),ios(3.0));       // key that failed to validate for a validation error
+COREDATA_EXTERN NSString * const NSValidationPredicateErrorKey API_AVAILABLE(macosx(10.4),ios(3.0)); // for predicate-based validation, the predicate for the condition that failed to validate
+COREDATA_EXTERN NSString * const NSValidationValueErrorKey API_AVAILABLE(macosx(10.4),ios(3.0));     // if non-nil, the value for the key that failed to validate for a validation error
 
-COREDATA_EXTERN NSString * const NSAffectedStoresErrorKey NS_AVAILABLE(10_4,3_0);      // stores prompting an error
-COREDATA_EXTERN NSString * const NSAffectedObjectsErrorKey NS_AVAILABLE(10_4,3_0);     // objects prompting an error
+COREDATA_EXTERN NSString * const NSAffectedStoresErrorKey API_AVAILABLE(macosx(10.4),ios(3.0));      // stores prompting an error
+COREDATA_EXTERN NSString * const NSAffectedObjectsErrorKey API_AVAILABLE(macosx(10.4),ios(3.0));     // objects prompting an error
 
-COREDATA_EXTERN NSString * const NSPersistentStoreSaveConflictsErrorKey NS_AVAILABLE(10_7, 5_0);     // key in NSError's userInfo specifying the NSArray of NSMergeConflict
+COREDATA_EXTERN NSString * const NSPersistentStoreSaveConflictsErrorKey API_AVAILABLE(macosx(10.7),ios(5.0));     // key in NSError's userInfo specifying the NSArray of NSMergeConflict
 
-COREDATA_EXTERN NSString * const NSSQLiteErrorDomain NS_AVAILABLE(10_5,3_0);           // Predefined domain for SQLite errors, value of "code" will correspond to preexisting values in SQLite.
+COREDATA_EXTERN NSString * const NSSQLiteErrorDomain API_AVAILABLE(macosx(10.5),ios(3.0));           // Predefined domain for SQLite errors, value of "code" will correspond to preexisting values in SQLite.
 
 enum : NSInteger {
     NSManagedObjectValidationError                   = 1550,   // generic validation error
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStore.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStore.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStore.h	2016-05-21 07:41:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStore.h	2016-06-27 06:09:43.000000000 +0200
@@ -21,7 +21,7 @@
 @class NSEntityDescription;
 @class NSManagedObjectID;
 
-NS_CLASS_AVAILABLE(10_5,3_0)
+API_AVAILABLE(macosx(10.5),ios(3.0))
 @interface NSAtomicStore : NSPersistentStore {
 #if (!__OBJC2__)
 	@private
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStoreCacheNode.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStoreCacheNode.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStoreCacheNode.h	2016-05-21 07:41:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAtomicStoreCacheNode.h	2016-06-27 06:09:43.000000000 +0200
@@ -18,7 +18,7 @@
 
 @class NSEntityDescription;
 
-NS_CLASS_AVAILABLE(10_5,3_0)
+API_AVAILABLE(macosx(10.5),ios(3.0))
 @interface NSAtomicStoreCacheNode : NSObject {
 #if (!__OBJC2__)
     @private
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAttributeDescription.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAttributeDescription.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAttributeDescription.h	2016-05-21 07:41:59.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSAttributeDescription.h	2016-06-27 06:09:43.000000000 +0200
@@ -27,12 +27,12 @@
     NSBooleanAttributeType = 800,
     NSDateAttributeType = 900,
     NSBinaryDataAttributeType = 1000,
-    NSTransformableAttributeType NS_ENUM_AVAILABLE(10_5,3_0) = 1800, // If your attribute is of NSTransformableAttributeType, the attributeValueClassName must be set or attribute value class must implement NSCopying.
-    NSObjectIDAttributeType NS_ENUM_AVAILABLE(10_6,3_0) = 2000
+    NSTransformableAttributeType API_AVAILABLE(macosx(10.5), ios(3.0)) = 1800, // If your attribute is of NSTransformableAttributeType, the attributeValueClassName must be set or attribute value class must implement NSCopying.
+    NSObjectIDAttributeType API_AVAILABLE(macosx(10.6), ios(3.0)) = 2000
  };
 
 // Attributes represent individual values like strings, numbers, dates, etc.
-NS_CLASS_AVAILABLE(10_4,3_0)
+API_AVAILABLE(macosx(10.4),ios(3.0))
 @interface NSAttributeDescription : NSPropertyDescription {
 }
 
@@ -44,12 +44,12 @@
 @property (nullable, retain) id defaultValue;   // value is retained and not copied
 
 /* Returns the version hash for the attribute.  This value includes the versionHash information from the NSPropertyDescription superclass, and the attribute type.*/
-@property (readonly, copy) NSData *versionHash NS_AVAILABLE(10_5,3_0);
+@property (readonly, copy) NSData *versionHash API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* The name of the transformer used to convert a NSTransformedAttributeType.  The transformer must output NSData from transformValue and allow reverse transformation.  If this value is not set, or set to nil, Core Data will default to using a transformer which uses NSCoding to archive/unarchive the attribute value.*/
-@property (nullable, copy) NSString *valueTransformerName NS_AVAILABLE(10_5,3_0);
+@property (nullable, copy) NSString *valueTransformerName API_AVAILABLE(macosx(10.5),ios(3.0));
 
-@property () BOOL allowsExternalBinaryDataStorage NS_AVAILABLE(10_7, 5_0);
+@property () BOOL allowsExternalBinaryDataStorage API_AVAILABLE(macosx(10.7),ios(5.0));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchDeleteRequest.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchDeleteRequest.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchDeleteRequest.h	2016-05-21 07:41:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchDeleteRequest.h	2016-06-27 06:09:43.000000000 +0200
@@ -23,7 +23,7 @@
 //  It is up to the developer creating the request to ensure that changes made by the request to
 //  the underlying store do not violate any validation rules specified in the model beyond basic
 //  delete rules (for example, minimum relationship counts).
-NS_CLASS_AVAILABLE(10_11,9_0)
+API_AVAILABLE(macosx(10.11),ios(9.0))
 @interface NSBatchDeleteRequest : NSPersistentStoreRequest {
 #if (!__OBJC2__)
     @private
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchUpdateRequest.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchUpdateRequest.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchUpdateRequest.h	2016-05-21 07:41:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSBatchUpdateRequest.h	2016-06-27 06:09:43.000000000 +0200
@@ -20,7 +20,7 @@
 //  WARNING:
 //  It is up to the developer creating the request to ensure that changes made by the request to
 //  the underlying store do not violate any validation rules specified in the model.
-NS_CLASS_AVAILABLE(10_10,8_0)
+API_AVAILABLE(macosx(10.10),ios(8.0))
 @interface NSBatchUpdateRequest : NSPersistentStoreRequest {
 #if (!__OBJC2__)
     @private
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityDescription.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityDescription.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityDescription.h	2016-05-21 07:49:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityDescription.h	2016-06-27 06:09:43.000000000 +0200
@@ -20,7 +20,7 @@
 @class NSAttributeDescription;
 
 // Entities describe the "types" of objects available.
-NS_CLASS_AVAILABLE(10_4,3_0)
+API_AVAILABLE(macosx(10.4),ios(3.0))
 @interface NSEntityDescription : NSObject <NSCoding, NSCopying, NSFastEnumeration> {
 }
 
@@ -49,23 +49,23 @@
 
 /* Returns a boolean indicating if the receiver is a subentity of the specified entity.  (This method is the Core Data entity inheritance equivalent of -isKindOfClass:)
 */
-- (BOOL)isKindOfEntity:(NSEntityDescription *)entity NS_AVAILABLE(10_5,3_0);
+- (BOOL)isKindOfEntity:(NSEntityDescription *)entity API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Returns the version hash for the entity.  The version hash is used to uniquely identify an entity based on the collection and configuration of properties for the entity.  The version hash uses only values which affect the persistence of data and the user-defined versionHashModifier value.  (The values which affect persistence are the name of the entity, the version hash of the superentity (if present), if the entity is abstract, and all of the version hashes for the properties.)  This value is stored as part of the version information in the metadata for stores which use this entity, as well as a definition of an entity involved in an NSEntityMapping.
 */
-@property (readonly, copy) NSData *versionHash NS_AVAILABLE(10_5,3_0);
+@property (readonly, copy) NSData *versionHash API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Returns/sets the version hash modifier for the entity.  This value is included in the version hash for the entity, allowing developers to mark/denote an entity as being a different "version" than another, even if all of the values which affect persistence are equal.  (Such a difference is important in cases where the structure of an entity is unchanged, but the format or content of data has changed.)
 */
-@property (nullable, copy) NSString *versionHashModifier NS_AVAILABLE(10_5,3_0);
+@property (nullable, copy) NSString *versionHashModifier API_AVAILABLE(macosx(10.5),ios(3.0));
 
-@property (nullable, copy) NSString *renamingIdentifier NS_AVAILABLE(10_6,3_0);
+@property (nullable, copy) NSString *renamingIdentifier API_AVAILABLE(macosx(10.6),ios(3.0));
 
 /* Returns/sets the set of compound indices for the entity. Returns/takes an array of arrays, each of which contains one or more NSPropertyDescription or NSString instances (strings must be the names of properties of the entity on which the index is created).
     This value does not form part of the entity's version hash, and may be ignored by stores which do not natively support compound
     indexes.
  */
-@property (strong) NSArray<NSArray<id> *> *compoundIndexes NS_AVAILABLE(10_7,5_0);
+@property (strong) NSArray<NSArray<id> *> *compoundIndexes API_AVAILABLE(macosx(10.7),ios(5.0));
 
 /* Returns/sets uniqueness constraints for the entity. A uniqueness constraint is a set of one or more attributes whose value must be unique over the set of instances of that entity.
     Returns/sets an array of arrays, each of which contains one or more NSAttributeDescription or NSString instances (strings must be the names of attributes on the entity) on which the constraint is registered. 
@@ -74,7 +74,7 @@
     although subentites may extend a sueprentity's constraint.
 */
                                                                                                                                                                       
-@property (strong)NSArray<NSArray<id> *> *uniquenessConstraints NS_AVAILABLE(10_11,9_0);
+@property (strong)NSArray<NSArray<id> *> *uniquenessConstraints API_AVAILABLE(macosx(10.11),ios(9.0));
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMapping.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMapping.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMapping.h	2016-05-26 06:23:57.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMapping.h	2016-06-27 07:21:43.000000000 +0200
@@ -26,7 +26,7 @@
     NSTransformEntityMappingType    = 0x05,         /* entity exists in source and destination and is mapped */
 };
 
-NS_CLASS_AVAILABLE(10_5,3_0)
+API_AVAILABLE(macosx(10.5),ios(3.0))
 @interface NSEntityMapping : NSObject {
 #if (!__OBJC2__)
 @private
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMigrationPolicy.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMigrationPolicy.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMigrationPolicy.h	2016-05-26 06:17:02.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSEntityMigrationPolicy.h	2016-06-27 06:09:43.000000000 +0200
@@ -20,19 +20,19 @@
  NSMigrationPropertyMappingKey   $propertyMapping
  NSMigrationEntityPolicyKey      $entityPolicy
 */
-COREDATA_EXTERN NSString * const NSMigrationManagerKey NS_AVAILABLE(10_5,3_0);
-COREDATA_EXTERN NSString * const NSMigrationSourceObjectKey NS_AVAILABLE(10_5,3_0);
-COREDATA_EXTERN NSString * const NSMigrationDestinationObjectKey NS_AVAILABLE(10_5,3_0);
-COREDATA_EXTERN NSString * const NSMigrationEntityMappingKey NS_AVAILABLE(10_5,3_0);
-COREDATA_EXTERN NSString * const NSMigrationPropertyMappingKey NS_AVAILABLE(10_5,3_0);
-COREDATA_EXTERN NSString * const NSMigrationEntityPolicyKey NS_AVAILABLE(10_5,3_0);
+COREDATA_EXTERN NSString * const NSMigrationManagerKey API_AVAILABLE(macosx(10.5),ios(3.0));
+COREDATA_EXTERN NSString * const NSMigrationSourceObjectKey API_AVAILABLE(macosx(10.5),ios(3.0));
+COREDATA_EXTERN NSString * const NSMigrationDestinationObjectKey API_AVAILABLE(macosx(10.5),ios(3.0));
+COREDATA_EXTERN NSString * const NSMigrationEntityMappingKey API_AVAILABLE(macosx(10.5),ios(3.0));
+COREDATA_EXTERN NSString * const NSMigrationPropertyMappingKey API_AVAILABLE(macosx(10.5),ios(3.0));
+COREDATA_EXTERN NSString * const NSMigrationEntityPolicyKey API_AVAILABLE(macosx(10.5),ios(3.0));
 
 @class NSManagedObject;
 @class NSEntityMapping;
 @class NSMigrationManager;
 @class NSError;
 
-NS_CLASS_AVAILABLE(10_5,3_0)
+API_AVAILABLE(macosx(10.5),ios(3.0))
 @interface NSEntityMigrationPolicy : NSObject
 
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSExpressionDescription.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSExpressionDescription.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSExpressionDescription.h	2016-05-21 07:41:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSExpressionDescription.h	2016-06-27 06:09:43.000000000 +0200
@@ -17,7 +17,7 @@
    An NSExpressionDescription describes a column to be returned from a fetch that may not appear 
    directly as an attribute or relationship on an entity. Examples would be: upper(attribute) or
    max(attribute). NSExpressionDescriptions cannot be set as properties on NSEntityDescription. */
-NS_CLASS_AVAILABLE(10_6,3_0)
+API_AVAILABLE(macosx(10.6),ios(3.0))
 @interface NSExpressionDescription : NSPropertyDescription {
 #if (!__OBJC2__)
 	@private
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequest.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequest.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequest.h	2016-05-26 06:17:02.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequest.h	2016-06-27 07:21:43.000000000 +0200
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
 
@@ -40,19 +43,19 @@
 @interface NSManagedObjectID (NSFetchedResultSupport) <NSFetchRequestResult>
 @end
 
-NS_CLASS_AVAILABLE(10_4, 3_0)
+API_AVAILABLE(macosx(10.4),ios(3.0))
 @interface NSFetchRequest<__covariant ResultType:id<NSFetchRequestResult>> : NSPersistentStoreRequest <NSCoding>
 
-+ (instancetype)fetchRequestWithEntityName:(NSString*)entityName NS_AVAILABLE(10_7, 4_0);
++ (instancetype)fetchRequestWithEntityName:(NSString*)entityName API_AVAILABLE(macosx(10.7),ios(4.0));
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
-- (instancetype)initWithEntityName:(NSString*)entityName NS_AVAILABLE(10_7, 4_0);
+- (instancetype)initWithEntityName:(NSString*)entityName API_AVAILABLE(macosx(10.7),ios(4.0));
 
 // Executes the fetch request using the current managed object context. This method must be called from within a block submitted to a managed object context.
-- (nullable NSArray<ResultType> *)execute:(NSError **)error  NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+- (nullable NSArray<ResultType> *)execute:(NSError **)error  API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
 @property (nullable, nonatomic, strong) NSEntityDescription *entity;
-@property (nullable, nonatomic, readonly, strong) NSString *entityName NS_AVAILABLE(10_7, 4_0);
+@property (nullable, nonatomic, readonly, strong) NSString *entityName API_AVAILABLE(macosx(10.7),ios(4.0));
 
 @property (nullable, nonatomic, strong) NSPredicate *predicate;
 
@@ -64,57 +67,57 @@
 
 /* Returns/sets the result type of the fetch request (the instance type of objects returned from executing the request.)  Setting the value to NSManagedObjectIDResultType will demote any sort orderings to "best effort" hints if property values are not included in the request.  Defaults to NSManagedObjectResultType.   
 */
-@property (nonatomic) NSFetchRequestResultType resultType NS_AVAILABLE(10_5,3_0);
+@property (nonatomic) NSFetchRequestResultType resultType API_AVAILABLE(macosx(10.5),ios(3.0));
 
 
 /* Returns/sets if the fetch request includes subentities.  If set to NO, the request will fetch objects of exactly the entity type of the request;  if set to YES, the request will include all subentities of the entity for the request.  Defaults to YES. 
 */
-@property (nonatomic) BOOL includesSubentities NS_AVAILABLE(10_5,3_0);
+@property (nonatomic) BOOL includesSubentities API_AVAILABLE(macosx(10.5),ios(3.0));
 
 
 /* Returns/sets if, when the fetch is executed, property data is obtained from the persistent store.  If the value is set to NO, the request will not obtain property information, but only information to identify each object (used to create NSManagedObjectIDs.)  If managed objects for these IDs are later faulted (as a result attempting to access property values), they will incur subsequent access to the persistent store to obtain their property values.  Defaults to YES. 
 */
-@property (nonatomic) BOOL includesPropertyValues NS_AVAILABLE(10_5,3_0);
+@property (nonatomic) BOOL includesPropertyValues API_AVAILABLE(macosx(10.5),ios(3.0));
 
 
 /* Returns/sets if the objects resulting from a fetch request are faults.  If the value is set to NO, the returned objects are pre-populated with their property values (making them fully-faulted objects, which will immediately return NO if sent the -isFault message.)  If the value is set to YES, the returned objects are not pre-populated (and will receive a -didFireFault message when the properties are accessed the first time.)  This setting is not utilized if the result type of the request is NSManagedObjectIDResultType, as object IDs do not have property values.  Defaults to YES. 
 */
-@property (nonatomic) BOOL returnsObjectsAsFaults NS_AVAILABLE(10_5,3_0);
+@property (nonatomic) BOOL returnsObjectsAsFaults API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Returns/sets an array of relationship keypaths to prefetch along with the entity for the request.  The array contains keypath strings in NSKeyValueCoding notation, as you would normally use with valueForKeyPath.  (Prefetching allows Core Data to obtain developer-specified related objects in a single fetch (per entity), rather than incurring subsequent access to the store for each individual record as their faults are tripped.)  Defaults to an empty array (no prefetching.) 
 */
-@property (nullable, nonatomic, copy) NSArray<NSString *> *relationshipKeyPathsForPrefetching NS_AVAILABLE(10_5,3_0);
+@property (nullable, nonatomic, copy) NSArray<NSString *> *relationshipKeyPathsForPrefetching API_AVAILABLE(macosx(10.5),ios(3.0));
 
 
 /* Results accommodate the currently unsaved changes in the NSManagedObjectContext.  When disabled, the fetch request skips checking unsaved changes and only returns objects that matched the predicate in the persistent store.  Defaults to YES.
 */
-@property (nonatomic) BOOL includesPendingChanges NS_AVAILABLE(10_6, 3_0);
+@property (nonatomic) BOOL includesPendingChanges API_AVAILABLE(macosx(10.6),ios(3.0));
 
 /* Returns/sets if the fetch request returns only distinct values for the fields specified by propertiesToFetch. This value is only used for NSDictionaryResultType. Defaults to NO. */
-@property (nonatomic) BOOL returnsDistinctResults NS_AVAILABLE(10_6, 3_0);
+@property (nonatomic) BOOL returnsDistinctResults API_AVAILABLE(macosx(10.6),ios(3.0));
 
 /* Specifies a collection of either NSPropertyDescriptions or NSString property names that should be fetched. The collection may represent attributes, to-one relationships, or NSExpressionDescription.  If NSDictionaryResultType is set, the results of the fetch will be dictionaries containing key/value pairs where the key is the name of the specified property description.  If NSManagedObjectResultType is set, then NSExpressionDescription cannot be used, and the results are managed object faults partially pre-populated with the named properties */
-@property (nullable, nonatomic, copy) NSArray *propertiesToFetch NS_AVAILABLE(10_6, 3_0);
+@property (nullable, nonatomic, copy) NSArray *propertiesToFetch API_AVAILABLE(macosx(10.6),ios(3.0));
 
 /* Allows you to specify an offset at which rows will begin being returned.  Effectively, the request will skip over 'offset' number of matching entries.  For example, given a fetch which would normally return a, b, c, and d, specifying an offset of 1 will return b, c, and d and an offset of 4  will return an empty array. Offsets are ignored in nested requests such as subqueries.  Default value is 0.  */
-@property (nonatomic) NSUInteger fetchOffset NS_AVAILABLE(10_6, 3_0);
+@property (nonatomic) NSUInteger fetchOffset API_AVAILABLE(macosx(10.6),ios(3.0));
 
 /* This breaks the result set into batches.  The entire request will be evaluated, and the identities of all matching objects will be recorded, but no more than batchSize objects' data will be fetched from the persistent store at a time.  The array returned from executing the request will be a subclass that transparently faults batches on demand.  For purposes of thread safety, the returned array proxy is owned by the NSManagedObjectContext the request is executed against, and should be treated as if it were a managed object registered with that context.  A batch size of 0 is treated as infinite, which disables the batch faulting behavior.  The default is 0. */
 
-@property (nonatomic) NSUInteger fetchBatchSize NS_AVAILABLE(10_6, 3_0);
+@property (nonatomic) NSUInteger fetchBatchSize API_AVAILABLE(macosx(10.6),ios(3.0));
 
-@property (nonatomic) BOOL shouldRefreshRefetchedObjects NS_AVAILABLE(10_7,  5_0);
+@property (nonatomic) BOOL shouldRefreshRefetchedObjects API_AVAILABLE(macosx(10.7),ios(5.0));
 
 /* Specifies the way in which data should be grouped before a select statement is run in an SQL database.
  Values passed to propertiesToGroupBy must be NSPropertyDescriptions, NSExpressionDescriptions, or keypath strings; keypaths can not contain 
  any to-many steps. 
  If GROUP BY is used, then you must set the resultsType to NSDictionaryResultsType, and the SELECT values must be literals, aggregates, 
  or columns specified in the GROUP BY. Aggregates will operate on the groups specified in the GROUP BY rather than the whole table. */
-@property (nullable, nonatomic, copy) NSArray *propertiesToGroupBy NS_AVAILABLE(10_7,  5_0);
+@property (nullable, nonatomic, copy) NSArray *propertiesToGroupBy API_AVAILABLE(macosx(10.7),ios(5.0));
 
 /* Specifies a predicate that will be used to filter rows being returned by a query containing a GROUP BY. If a having predicate is
  supplied, it will be run after the GROUP BY.  Specifying a HAVING predicate requires that a GROUP BY also be specified. */
-@property (nullable, nonatomic, strong) NSPredicate *havingPredicate NS_AVAILABLE(10_7,  5_0);
+@property (nullable, nonatomic, strong) NSPredicate *havingPredicate API_AVAILABLE(macosx(10.7),ios(5.0));
 
 @end
 
@@ -123,7 +126,7 @@
 
 typedef void (^NSPersistentStoreAsynchronousFetchResultCompletionBlock)(NSAsynchronousFetchResult *result);
 
-NS_CLASS_AVAILABLE(10_10,8_0)
+API_AVAILABLE(macosx(10.10),ios(8.0))
 @interface NSAsynchronousFetchRequest<ResultType:id<NSFetchRequestResult>> : NSPersistentStoreRequest
 
 @property (strong, readonly) NSFetchRequest<ResultType> * fetchRequest;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequestExpression.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequestExpression.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequestExpression.h	2016-05-21 07:41:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchRequestExpression.h	2016-06-27 06:09:43.000000000 +0200
@@ -13,7 +13,7 @@
 
 static const NSExpressionType NSFetchRequestExpressionType = (NSExpressionType)50;
 
-NS_CLASS_AVAILABLE(10_5,3_0)
+API_AVAILABLE(macosx(10.5),ios(3.0))
 @interface NSFetchRequestExpression : NSExpression {
 #if (!__OBJC2__)
 @private
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedPropertyDescription.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedPropertyDescription.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedPropertyDescription.h	2016-05-21 07:41:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedPropertyDescription.h	2016-06-27 06:09:43.000000000 +0200
@@ -13,7 +13,7 @@
 @class NSFetchRequest;
 
 // Fetched properties allow to specify related objects through a "weakly" resolved property, so there is no actual join necessary.
-NS_CLASS_AVAILABLE(10_4,3_0)
+API_AVAILABLE(macosx(10.4),ios(3.0))
 @interface NSFetchedPropertyDescription : NSPropertyDescription {
 #if (!__OBJC2__)
 @private
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedResultsController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedResultsController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedResultsController.h	2016-05-26 06:23:57.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSFetchedResultsController.h	2016-06-27 05:48:03.000000000 +0200
@@ -48,7 +48,7 @@
 @protocol NSFetchedResultsControllerDelegate;
 @protocol NSFetchedResultsSectionInfo;
 
-NS_CLASS_AVAILABLE(10_12,3_0)
+API_AVAILABLE(macosx(10.12),ios(3.0))
 @interface NSFetchedResultsController<ResultType:id<NSFetchRequestResult>> : NSObject
 
 /* ========================================================*/
@@ -182,7 +182,7 @@
     NSFetchedResultsChangeDelete = 2,
     NSFetchedResultsChangeMove = 3,
     NSFetchedResultsChangeUpdate = 4
-} NS_ENUM_AVAILABLE(10_12,  3_0);
+} API_AVAILABLE(macosx(10.12), ios(3.0));
 
 /* Notifies the delegate that a fetched object has been changed due to an add, remove, move, or update. Enables NSFetchedResultsController change tracking.
 	controller - controller instance that noticed the change on its fetched objects
@@ -230,7 +230,7 @@
  Only needed if a section index is used.
  */
 @optional
-- (nullable NSString *)controller:(NSFetchedResultsController *)controller sectionIndexTitleForSectionName:(NSString *)sectionName NS_AVAILABLE(10_12,4_0);
+- (nullable NSString *)controller:(NSFetchedResultsController *)controller sectionIndexTitleForSectionName:(NSString *)sectionName API_AVAILABLE(macosx(10.12),ios(4.0));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStore.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStore.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStore.h	2016-05-26 06:17:01.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStore.h	2016-06-27 07:21:43.000000000 +0200
@@ -21,7 +21,7 @@
 // Abstract class defining the API through which Core Data communicates with a store. 
 // This API is designed to allow users to create persistent stores which load and save 
 // data incrementally, allowing for the management of large and/or shared datasets.
-NS_CLASS_AVAILABLE(10_7,5_0)
+API_AVAILABLE(macosx(10.7),ios(5.0))
 @interface NSIncrementalStore : NSPersistentStore {
 }
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStoreNode.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStoreNode.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStoreNode.h	2016-05-21 07:41:59.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSIncrementalStoreNode.h	2016-06-27 06:09:43.000000000 +0200
@@ -13,7 +13,7 @@
 @class NSPropertyDescription;
 
 // Provides the basic unit of external data that the Core Data stack interacts with.
-NS_CLASS_AVAILABLE(10_7,5_0)
+API_AVAILABLE(macosx(10.7),ios(5.0))
 @interface NSIncrementalStoreNode : NSObject {
 }
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObject.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObject.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObject.h	2016-05-21 07:49:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObject.h	2016-06-27 05:48:01.000000000 +0200
@@ -27,28 +27,28 @@
 	NSSnapshotEventMergePolicy = 1 << 6
 };
 
-NS_CLASS_AVAILABLE(10_4,3_0) NS_REQUIRES_PROPERTY_DEFINITIONS
+API_AVAILABLE(macosx(10.4),ios(3.0)) NS_REQUIRES_PROPERTY_DEFINITIONS
 @interface NSManagedObject : NSObject {
 }
 
 /*  Distinguish between changes that should and should not dirty the object for any key unknown to Core Data.  10.5 & earlier default to NO.  10.6 and later default to YES. */
 /*    Similarly, transient attributes may be individually flagged as not dirtying the object by adding +(BOOL)contextShouldIgnoreChangesFor<key> where <key> is the property name. */
-@property(class, readonly) BOOL contextShouldIgnoreUnmodeledPropertyChanges NS_AVAILABLE(10_6,3_0);
+@property(class, readonly) BOOL contextShouldIgnoreUnmodeledPropertyChanges API_AVAILABLE(macosx(10.6),ios(3.0));
 
 /* The Entity represented by this subclass. This method is only legal to call on subclasses of NSManagedObject that represent a single entity in the model.
  */
-+ (NSEntityDescription*)entity NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
++ (NSEntityDescription*)entity API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
 /* A new fetch request initialized with the Entity represented by this subclass. This property's getter is only legal to call on subclasses of NSManagedObject that represent a single entity in the model.
  */
-+ (NSFetchRequest*)fetchRequest NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
++ (NSFetchRequest*)fetchRequest API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
 // The designated initializer.
 - (__kindof NSManagedObject*)initWithEntity:(NSEntityDescription *)entity insertIntoManagedObjectContext:(nullable NSManagedObjectContext *)context NS_DESIGNATED_INITIALIZER;
 
 /* Returns a new object, inserted into managedObjectContext. This method is only legal to call on subclasses of NSManagedObject that represent a single entity in the model.
  */
--(instancetype)initWithContext:(NSManagedObjectContext*)moc NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+-(instancetype)initWithContext:(NSManagedObjectContext*)moc API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
 // identity
 @property (nullable, nonatomic, readonly, assign) NSManagedObjectContext *managedObjectContext;
@@ -60,22 +60,22 @@
 @property (nonatomic, getter=isUpdated, readonly) BOOL updated;
 @property (nonatomic, getter=isDeleted, readonly) BOOL deleted;
 
-@property (nonatomic, readonly) BOOL hasChanges NS_AVAILABLE(10_7, 5_0);
+@property (nonatomic, readonly) BOOL hasChanges API_AVAILABLE(macosx(10.7),ios(5.0));
 
 /* returns YES if any persistent properties do not compare isEqual to their last saved state.  Relationship faults will not be unnecessarily fired.  This differs from the existing -hasChanges method which is a simple dirty flag and also includes transient properties */
-@property (nonatomic, readonly) BOOL hasPersistentChangedValues NS_AVAILABLE(10_9,7_0);
+@property (nonatomic, readonly) BOOL hasPersistentChangedValues API_AVAILABLE(macosx(10.9),ios(7.0));
 
 // this information is useful in many situations when computations are optional - this can be used to avoid growing the object graph unnecessarily (which allows to control performance as it can avoid time consuming fetches from databases)
 @property (nonatomic, getter=isFault, readonly) BOOL fault;    
 
 // returns a Boolean indicating if the relationship for the specified key is a fault.  If a value of NO is returned, the resulting relationship is a realized object;  otherwise the relationship is a fault.  If the specified relationship is a fault, calling this method does not result in the fault firing.
-- (BOOL)hasFaultForRelationshipNamed:(NSString *)key NS_AVAILABLE(10_5,3_0); 
+- (BOOL)hasFaultForRelationshipNamed:(NSString *)key API_AVAILABLE(macosx(10.5),ios(3.0)); 
 
 /* returns an array of objectIDs for the contents of a relationship.  to-one relationships will return an NSArray with a single NSManagedObjectID.  Optional relationships may return an empty NSArray.  The objectIDs will be returned in an NSArray regardless of the type of the relationship.  */
-- (NSArray<NSManagedObjectID *> *)objectIDsForRelationshipNamed:(NSString *)key NS_AVAILABLE(10_11,8_3);
+- (NSArray<NSManagedObjectID *> *)objectIDsForRelationshipNamed:(NSString *)key API_AVAILABLE(macosx(10.11),ios(8.3));
 
 /* Allow developers to determine if an object is in a transitional phase when receiving a KVO notification.  Returns 0 if the object is fully initialized as a managed object and not transitioning to or from another state */
-@property (nonatomic, readonly) NSUInteger faultingState NS_AVAILABLE(10_5,3_0);
+@property (nonatomic, readonly) NSUInteger faultingState API_AVAILABLE(macosx(10.5),ios(3.0));
 
 // lifecycle/change management (includes key-value observing methods)
 - (void)willAccessValueForKey:(nullable NSString *)key; // read notification
@@ -94,10 +94,10 @@
 - (void)awakeFromInsert;
 
 /* Callback for undo, redo, and other multi-property state resets */
-- (void)awakeFromSnapshotEvents:(NSSnapshotEventType)flags NS_AVAILABLE(10_6,3_0);
+- (void)awakeFromSnapshotEvents:(NSSnapshotEventType)flags API_AVAILABLE(macosx(10.6),ios(3.0));
 
 /* Callback before delete propagation while the object is still alive.  Useful to perform custom propagation before the relationships are torn down or reconfigure KVO observers. */
-- (void)prepareForDeletion NS_AVAILABLE(10_6,3_0);
+- (void)prepareForDeletion API_AVAILABLE(macosx(10.6),ios(3.0));
 
 // commonly used to compute persisted values from other transient/scratchpad values, to set timestamps, etc. - this method can have "side effects" on the persisted values
 - (void)willSave;    
@@ -106,7 +106,7 @@
 - (void)didSave;    
 
 // invoked automatically by the Core Data framework before receiver is converted (back) to a fault.  This method is the companion of the -didTurnIntoFault method, and may be used to (re)set state which requires access to property values (for example, observers across keypaths.)  The default implementation does nothing.  
-- (void)willTurnIntoFault NS_AVAILABLE(10_5,3_0);
+- (void)willTurnIntoFault API_AVAILABLE(macosx(10.5),ios(3.0));
 
 // commonly used to clear out additional transient values or caches
 - (void)didTurnIntoFault;    
@@ -129,7 +129,7 @@
 // returns a dictionary with the keys and (new) values that have been changed since last fetching or saving the object (this is implemented efficiently without firing relationship faults)
 - (NSDictionary<NSString *, id> *)changedValues;
 
-- (NSDictionary<NSString *, id> *)changedValuesForCurrentEvent NS_AVAILABLE(10_7, 5_0);
+- (NSDictionary<NSString *, id> *)changedValuesForCurrentEvent API_AVAILABLE(macosx(10.7),ios(5.0));
 
 // validation - in addition to KVC validation managed objects have hooks to validate their lifecycle state; validation is a critical piece of functionality and the following methods are likely the most commonly overridden methods in custom subclasses
 - (BOOL)validateValue:(id _Nullable * _Nonnull)value forKey:(NSString *)key error:(NSError **)error;    // KVC
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h	2016-05-26 06:23:56.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectContext.h	2016-06-27 05:48:04.000000000 +0200
@@ -28,73 +28,73 @@
 @class NSNotification;
 
 // Notifications immediately before and immediately after the context saves.  The user info dictionary contains information about the objects that changed and what changed
-COREDATA_EXTERN NSString * const NSManagedObjectContextWillSaveNotification NS_AVAILABLE(10_5, 3_0);
-COREDATA_EXTERN NSString * const NSManagedObjectContextDidSaveNotification NS_AVAILABLE(10_4, 3_0);
+COREDATA_EXTERN NSString * const NSManagedObjectContextWillSaveNotification API_AVAILABLE(macosx(10.5),ios(3.0));
+COREDATA_EXTERN NSString * const NSManagedObjectContextDidSaveNotification API_AVAILABLE(macosx(10.4),ios(3.0));
 
 // Notification when objects in a context changed:  the user info dictionary contains information about the objects that changed and what changed
-COREDATA_EXTERN NSString * const NSManagedObjectContextObjectsDidChangeNotification NS_AVAILABLE(10_4, 3_0);    
+COREDATA_EXTERN NSString * const NSManagedObjectContextObjectsDidChangeNotification API_AVAILABLE(macosx(10.4),ios(3.0));    
 
 // User info keys for NSManagedObjectContextObjectsDidChangeNotification:  the values for these keys are sets of managed objects
-COREDATA_EXTERN NSString * const NSInsertedObjectsKey NS_AVAILABLE(10_4, 3_0);
-COREDATA_EXTERN NSString * const NSUpdatedObjectsKey NS_AVAILABLE(10_4, 3_0);
-COREDATA_EXTERN NSString * const NSDeletedObjectsKey NS_AVAILABLE(10_4, 3_0);
+COREDATA_EXTERN NSString * const NSInsertedObjectsKey API_AVAILABLE(macosx(10.4),ios(3.0));
+COREDATA_EXTERN NSString * const NSUpdatedObjectsKey API_AVAILABLE(macosx(10.4),ios(3.0));
+COREDATA_EXTERN NSString * const NSDeletedObjectsKey API_AVAILABLE(macosx(10.4),ios(3.0));
 
-COREDATA_EXTERN NSString * const NSRefreshedObjectsKey NS_AVAILABLE(10_5, 3_0);
-COREDATA_EXTERN NSString * const NSInvalidatedObjectsKey NS_AVAILABLE(10_5, 3_0);
+COREDATA_EXTERN NSString * const NSRefreshedObjectsKey API_AVAILABLE(macosx(10.5),ios(3.0));
+COREDATA_EXTERN NSString * const NSInvalidatedObjectsKey API_AVAILABLE(macosx(10.5),ios(3.0));
 
-COREDATA_EXTERN NSString * const NSManagedObjectContextQueryGenerationKey NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+COREDATA_EXTERN NSString * const NSManagedObjectContextQueryGenerationKey API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
 // User info keys for NSManagedObjectContextObjectsDidChangeNotification:  the values for these keys are arrays of objectIDs
-COREDATA_EXTERN NSString * const NSInvalidatedAllObjectsKey NS_AVAILABLE(10_5, 3_0); // All objects in the context have been invalidated
+COREDATA_EXTERN NSString * const NSInvalidatedAllObjectsKey API_AVAILABLE(macosx(10.5),ios(3.0)); // All objects in the context have been invalidated
 
 // Default policy for all managed object contexts - save returns with an error that contains the object IDs of the objects that had conflicts(NSInsertedObjectsKey, NSUpdatedObjectsKey).
-COREDATA_EXTERN id NSErrorMergePolicy NS_AVAILABLE(10_4, 3_0);
+COREDATA_EXTERN id NSErrorMergePolicy API_AVAILABLE(macosx(10.4),ios(3.0));
 
 // This singleton policy merges conflicts between the persistent store's version of the object and the current in memory version. The merge occurs by individual property. For properties which have been changed in both the external source and in memory, the external changes trump the in memory ones.
-COREDATA_EXTERN id NSMergeByPropertyStoreTrumpMergePolicy NS_AVAILABLE(10_4, 3_0);    
+COREDATA_EXTERN id NSMergeByPropertyStoreTrumpMergePolicy API_AVAILABLE(macosx(10.4),ios(3.0));    
 
 // This singleton policy merges conflicts between the persistent store's version of the object and the current in memory version. The merge occurs by individual property. For properties which have been changed in both the external source and in memory, the in memory changes trump the external ones.
-COREDATA_EXTERN id NSMergeByPropertyObjectTrumpMergePolicy NS_AVAILABLE(10_4, 3_0);    
+COREDATA_EXTERN id NSMergeByPropertyObjectTrumpMergePolicy API_AVAILABLE(macosx(10.4),ios(3.0));    
 
 // This singleton policy overwrites all state for the changed objects in conflict The current object's state is pushed upon the persistent store.
-COREDATA_EXTERN id NSOverwriteMergePolicy NS_AVAILABLE(10_4, 3_0);    
+COREDATA_EXTERN id NSOverwriteMergePolicy API_AVAILABLE(macosx(10.4),ios(3.0));    
 
 // This singleton policy discards all state for the changed objects in conflict. The persistent store's version of the object is used.
-COREDATA_EXTERN id NSRollbackMergePolicy NS_AVAILABLE(10_4, 3_0);    
+COREDATA_EXTERN id NSRollbackMergePolicy API_AVAILABLE(macosx(10.4),ios(3.0));    
 
 typedef NS_ENUM(NSUInteger, NSManagedObjectContextConcurrencyType) {
-    NSConfinementConcurrencyType  NS_ENUM_DEPRECATED(10_4,10_11,3_0,9_0, "Use another NSManagedObjectContextConcurrencyType") = 0x00,
+    NSConfinementConcurrencyType  API_DEPRECATED( "Use another NSManagedObjectContextConcurrencyType", macosx(10.4,10.11), ios(3.0,9.0)) = 0x00,
     NSPrivateQueueConcurrencyType		= 0x01,
     NSMainQueueConcurrencyType			= 0x02
-} NS_ENUM_AVAILABLE(10_7,  5_0);
+} API_AVAILABLE(macosx(10.7), ios(5.0));
 
-NS_CLASS_AVAILABLE(10_4,3_0)
+API_AVAILABLE(macosx(10.4),ios(3.0))
 @interface NSManagedObjectContext : NSObject <NSCoding> {
 }
 
-+ (instancetype)new NS_DEPRECATED(10_4,10_11,3_0,9_0, "Use -initWithConcurrencyType: instead");
-- (instancetype)init NS_DEPRECATED(10_4,10_11,3_0,9_0, "Use -initWithConcurrencyType: instead");
-- (instancetype)initWithConcurrencyType:(NSManagedObjectContextConcurrencyType)ct NS_DESIGNATED_INITIALIZER  NS_AVAILABLE(10_7,  5_0);
++ (instancetype)new API_DEPRECATED( "Use -initWithConcurrencyType: instead", macosx(10.4,10.11), ios(3.0,9.0));
+- (instancetype)init API_DEPRECATED( "Use -initWithConcurrencyType: instead", macosx(10.4,10.11), ios(3.0,9.0));
+- (instancetype)initWithConcurrencyType:(NSManagedObjectContextConcurrencyType)ct NS_DESIGNATED_INITIALIZER  API_AVAILABLE(macosx(10.7),ios(5.0));
 
 /* asynchronously performs the block on the context's queue.  Encapsulates an autorelease pool and a call to processPendingChanges */
-- (void)performBlock:(void (^)())block NS_AVAILABLE(10_7,  5_0);
+- (void)performBlock:(void (^)())block API_AVAILABLE(macosx(10.7),ios(5.0));
 
 /* synchronously performs the block on the context's queue.  May safely be called reentrantly.  */
-- (void)performBlockAndWait:(void (^)())block NS_AVAILABLE(10_7,  5_0);
+- (void)performBlockAndWait:(void (^)())block API_AVAILABLE(macosx(10.7),ios(5.0));
 
 /* coordinator which provides model and handles persistency (multiple contexts can share a coordinator) */
 @property (nullable, strong) NSPersistentStoreCoordinator *persistentStoreCoordinator;
 
-@property (nullable, strong) NSManagedObjectContext *parentContext NS_AVAILABLE(10_7,  5_0);
+@property (nullable, strong) NSManagedObjectContext *parentContext API_AVAILABLE(macosx(10.7),ios(5.0));
 
 /* custom label for a context.  NSPrivateQueueConcurrencyType contexts will set the label on their queue */
-@property (nullable, copy) NSString *name NS_AVAILABLE(10_10, 8_0);
+@property (nullable, copy) NSString *name API_AVAILABLE(macosx(10.10),ios(8.0));
 
 @property (nullable, nonatomic, strong) NSUndoManager *undoManager;
 
 @property (nonatomic, readonly) BOOL hasChanges;
-@property (nonatomic, readonly, strong) NSMutableDictionary *userInfo NS_AVAILABLE(10_7,  5_0);
-@property (readonly) NSManagedObjectContextConcurrencyType concurrencyType NS_AVAILABLE(10_7,  5_0);
+@property (nonatomic, readonly, strong) NSMutableDictionary *userInfo API_AVAILABLE(macosx(10.7),ios(5.0));
+@property (readonly) NSManagedObjectContextConcurrencyType concurrencyType API_AVAILABLE(macosx(10.7),ios(5.0));
 
 /* returns the object for the specified ID if it is registered in the context already or nil. It never performs I/O. */
 - (nullable __kindof NSManagedObject *)objectRegisteredForID:(NSManagedObjectID *)objectID;
@@ -103,13 +103,13 @@
 - (__kindof NSManagedObject *)objectWithID:(NSManagedObjectID *)objectID;
 
 /* returns the object for the specified ID if it is already registered in the context, or faults the object into the context.  It might perform I/O if the data is uncached.  If the object cannot be fetched, or does not exist, or cannot be faulted, it returns nil.  Unlike -objectWithID: it never returns a fault.  */
-- (nullable __kindof NSManagedObject *)existingObjectWithID:(NSManagedObjectID*)objectID error:(NSError**)error NS_AVAILABLE(10_6, 3_0);
+- (nullable __kindof NSManagedObject *)existingObjectWithID:(NSManagedObjectID*)objectID error:(NSError**)error API_AVAILABLE(macosx(10.6),ios(3.0));
 
 // method to fetch objects from the persistent stores into the context (fetch request defines the entity and predicate as well as a sort order for the objects); context will match the results from persistent stores with current changes in the context (so inserted objects are returned even if they are not persisted yet); to fetch a single object with an ID if it is not guaranteed to exist and thus -objectWithObjectID: cannot be used, one would create a predicate like [NSComparisonPredicate predicateWithLeftExpression:[NSExpression expressionForKeyPath:@"objectID"] rightExpression:[NSExpression expressionForConstantValue:<object id>] modifier:NSPredicateModifierDirect type:NSEqualToPredicateOperatorType options:0]
 - (nullable NSArray *)executeFetchRequest:(NSFetchRequest *)request error:(NSError **)error;
 
 // returns the number of objects a fetch request would have returned if it had been passed to -executeFetchRequest:error:.   If an error occurred during the processing of the request, this method will return NSNotFound. 
-- (NSUInteger) countForFetchRequest: (NSFetchRequest *)request error: (NSError **)error NS_AVAILABLE(10_5, 3_0) __attribute__((swift_error(nonnull_error)));
+- (NSUInteger) countForFetchRequest: (NSFetchRequest *)request error: (NSError **)error API_AVAILABLE(macosx(10.5),ios(3.0)) __attribute__((swift_error(nonnull_error)));
 
 // Method to pass a request to the store without affecting the contents of the managed object context.
 // Will return an NSPersistentStoreResult which may contain additional information about the result of the action
@@ -117,7 +117,7 @@
 // A request may succeed in some stores and fail in others. In this case, the error will contain information
 // about each individual store failure.
 // Will always reject NSSaveChangesRequests.
-- (nullable __kindof NSPersistentStoreResult *)executeRequest:(NSPersistentStoreRequest*)request error:(NSError **)error NS_AVAILABLE(10_10, 8_0);
+- (nullable __kindof NSPersistentStoreResult *)executeRequest:(NSPersistentStoreRequest*)request error:(NSError **)error API_AVAILABLE(macosx(10.10),ios(8.0));
 
 - (void)insertObject:(NSManagedObject *)object;
 - (void)deleteObject:(NSManagedObject *)object;
@@ -149,7 +149,7 @@
 - (BOOL)save:(NSError **)error;
 
 /* calls -refreshObject:mergeChanges: on all currently registered objects with this context.  It handles dirtied objects and clearing the context reference queue */
-- (void)refreshAllObjects NS_AVAILABLE(10_11,8_3);
+- (void)refreshAllObjects API_AVAILABLE(macosx(10.11),ios(8.3));
 
     
 // whether or not the context propagates deletes to related objects at the end of the event, or only at save time
@@ -159,10 +159,10 @@
 @property (nonatomic) BOOL retainsRegisteredObjects;   // The default is NO.
 
 /*  set the rule to handle inaccessible faults.  If YES, then the managed object is marked deleted and all its properties, including scalars, nonnullable, and mandatory properties, will be nil or zero’d out.  If NO, the context will throw an exception. Managed objects that are inaccessible because their context is nil due to memory management issues will throw an exception regardless. */
-@property BOOL shouldDeleteInaccessibleFaults NS_AVAILABLE(10_11,9_0);
+@property BOOL shouldDeleteInaccessibleFaults API_AVAILABLE(macosx(10.11),ios(9.0));
 
 /*  this method will not be called from APIs which return an NSError like -existingObjectWithID:error: nor for managed objects with a nil context (e.g. the fault is inaccessible because the object or its context have been released) this method will not be called if Core Data determines there is an unambiguously correct action to recover.  This might happen if a fault was tripped during delete propagation.  In that case, the fault will simply be deleted.  triggeringProperty may be nil when either all properties are involved, or Core Data is unable to determine the reason for firing the fault. the default implementation logs and then returns the value of -shouldDeleteInaccessibleFaults. */
-- (BOOL)shouldHandleInaccessibleFault:(NSManagedObject*)fault forObjectID:(NSManagedObjectID*)oid triggeredByProperty:(nullable NSPropertyDescription*)property NS_AVAILABLE(10_11,9_0);
+- (BOOL)shouldHandleInaccessibleFault:(NSManagedObject*)fault forObjectID:(NSManagedObjectID*)oid triggeredByProperty:(nullable NSPropertyDescription*)property API_AVAILABLE(macosx(10.11),ios(9.0));
 
 // Staleness interval is the relative time until cached data should be considered stale. The value is applied on a per object basis. For example, a value of 300.0 informs the context to utilize cached information for no more than 5 minutes after that object was originally fetched. This does not affect objects currently in use. Principly, this controls whether fulfilling a fault uses data previously fetched by the application, or issues a new fetch.  It is a hint which may not be supported by all persistent store types.
 @property () NSTimeInterval stalenessInterval; // a negative value is considered infinite.  The default is infinite staleness.
@@ -171,18 +171,18 @@
 
 /* Converts the object IDs of the specified objects to permanent IDs.  This implementation will convert the object ID of each managed object in the specified array to a permanent ID.  Any object in the target array with a permanent ID will be ignored;  additionally, any managed object in the array not already assigned to a store will be assigned, based on the same rules Core Data uses for assignment during a save operation (first writable store supporting the entity, and appropriate for the instance and its related items.)  Although the object will have a permanent ID, it will still respond positively to -isInserted until it is saved.  If an error is encountered obtaining an identifier, the return value will be NO.
 */
-- (BOOL)obtainPermanentIDsForObjects:(NSArray<NSManagedObject *> *)objects error:(NSError **)error NS_AVAILABLE(10_5, 3_0);
+- (BOOL)obtainPermanentIDsForObjects:(NSArray<NSManagedObject *> *)objects error:(NSError **)error API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Merges the changes specified in notification object received from another context's NSManagedObjectContextDidSaveNotification into the receiver.  This method will refresh any objects which have been updated in the other context, fault in any newly inserted objects, and invoke deleteObject: on those which have been deleted.  The developer is only responsible for the thread safety of the receiver.
 */
-- (void)mergeChangesFromContextDidSaveNotification:(NSNotification *)notification NS_AVAILABLE(10_5, 3_0);
+- (void)mergeChangesFromContextDidSaveNotification:(NSNotification *)notification API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Similar to mergeChangesFromContextDidSaveNotification, this method handles changes from potentially other processes or serialized state.  It more efficiently
  * merges changes into multiple contexts, as well as nested context. The keys in the dictionary should be one those from an
  *  NSManagedObjectContextObjectsDidChangeNotification: NSInsertedObjectsKey, NSUpdatedObjectsKey, etc.
  *  the values should be an NSArray of either NSManagedObjectID or NSURL objects conforming to valid results from -URIRepresentation
  */
-+ (void)mergeChangesFromRemoteContextSave:(NSDictionary*)changeNotificationData intoContexts:(NSArray<NSManagedObjectContext*> *)contexts NS_AVAILABLE(10_11,9_0);
++ (void)mergeChangesFromRemoteContextSave:(NSDictionary*)changeNotificationData intoContexts:(NSArray<NSManagedObjectContext*> *)contexts API_AVAILABLE(macosx(10.11),ios(9.0));
 
 /* Return the query generation currently in use by this context. Will be one of the following:
  * - nil, default value
@@ -192,7 +192,7 @@
  *
  * All child contexts will return nil.
  */
-@property (nullable, nonatomic, strong, readonly) NSQueryGenerationToken *queryGenerationToken NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+@property (nullable, nonatomic, strong, readonly) NSQueryGenerationToken *queryGenerationToken API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
 /* Set the query generation this context should use. Must be one of the following values:
  * - nil
@@ -214,11 +214,11 @@
  * May partially fail if one or more stores being tracked by the token are removed from the persistent
  * store coordinator.
  */
-- (BOOL)setQueryGenerationFromToken:(nullable NSQueryGenerationToken *)generation error:(NSError **)error NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+- (BOOL)setQueryGenerationFromToken:(nullable NSQueryGenerationToken *)generation error:(NSError **)error API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
 /* Whether the context automatically merges changes saved to its parent. Setting this property to YES when the context is pinned to a non-current query generation is not supported.
 */
-@property (nonatomic) BOOL automaticallyMergesChangesFromParent NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+@property (nonatomic) BOOL automaticallyMergesChangesFromParent API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectID.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectID.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectID.h	2016-05-21 07:41:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectID.h	2016-06-27 06:09:43.000000000 +0200
@@ -14,7 +14,7 @@
 @class NSURL;
 
 // Managed object IDs are opaque identifiers for managed objects.
-NS_CLASS_AVAILABLE(10_4,3_0)
+API_AVAILABLE(macosx(10.4),ios(3.0))
 @interface NSManagedObjectID : NSObject <NSCopying> {
 }
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectModel.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectModel.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectModel.h	2016-05-26 06:17:01.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSManagedObjectModel.h	2016-06-27 07:21:43.000000000 +0200
@@ -17,7 +17,7 @@
 @class NSBundle;
 
 // Models describe object graphs to be managed. Models (and their entities/properties/fetch request templates) are editable until they are used by a persistent store coordinator, allowing developers to create/modify them dynamically. However, once a model is being used, it MUST NOT be changed. When the persistent store coordinator first fetches data using a model, it will become uneditable. Any attempt to mutate a model or any of its subobjects after that point will cause an exception to be thrown. If you need to modify a model that is in use, create a copy, modify the copy, and then discard the objects with the old model.
-NS_CLASS_AVAILABLE(10_4,3_0)
+API_AVAILABLE(macosx(10.4),ios(3.0))
 @interface NSManagedObjectModel : NSObject <NSCoding, NSCopying, NSFastEnumeration> {
 }
 
@@ -59,31 +59,31 @@
 
 /* Returns the managed object model used to create the store for the specified metadata.  This method is a companion to the mergedModelFromBundles: method;  in this case, the framework uses the version information stored in the metadata for a store to locate the models/entities used to create the store in the available bundles, and return the model.  If the model for the store cannot be found, this method will return nil.
 */
-+ (nullable NSManagedObjectModel *)mergedModelFromBundles:(nullable NSArray<NSBundle *> *)bundles forStoreMetadata:(NSDictionary<NSString *, id> *)metadata NS_AVAILABLE(10_5,3_0);
++ (nullable NSManagedObjectModel *)mergedModelFromBundles:(nullable NSArray<NSBundle *> *)bundles forStoreMetadata:(NSDictionary<NSString *, id> *)metadata API_AVAILABLE(macosx(10.5),ios(3.0));
 
 
 /* Returns a merged model from the specified array for the version information in the provided metadata.  (This is the companion method to mergedModelFromBundles:forStoreMetadata:)  If a model cannot be created to match the version information in the specified metadata, this method will return nil.  
 */
-+ (nullable NSManagedObjectModel *)modelByMergingModels:(NSArray<NSManagedObjectModel *> *)models forStoreMetadata:(NSDictionary<NSString *, id> *)metadata NS_AVAILABLE(10_5,3_0);
++ (nullable NSManagedObjectModel *)modelByMergingModels:(NSArray<NSManagedObjectModel *> *)models forStoreMetadata:(NSDictionary<NSString *, id> *)metadata API_AVAILABLE(macosx(10.5),ios(3.0));
 
 
 /* Returns the dictionary of fetch request templates, keyed by name, for the model.  If the template contains a predicate with substitution variables, you should instead use fetchRequestFromTemplateWithName:substitutionVariables: to create a new fetch request.
 */
-@property (readonly, copy) NSDictionary<NSString *, NSFetchRequest *> *fetchRequestTemplatesByName NS_AVAILABLE(10_5,3_0);
+@property (readonly, copy) NSDictionary<NSString *, NSFetchRequest *> *fetchRequestTemplatesByName API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Returns the collection of developer-defined version identifiers for the model.  For models created in Xcode, this value is set by the developer in the model inspector. Merged models return the combined  collection of identifiers. This value is meant to be used as a debugging hint to help developers determine the models that were combined to create a merged model. The framework does not give models a default identifier, nor does it depend this value at runtime.
 */
-@property (copy) NSSet *versionIdentifiers NS_AVAILABLE(10_5,3_0);
+@property (copy) NSSet *versionIdentifiers API_AVAILABLE(macosx(10.5),ios(3.0));
 
 
 /* Compares the version information in the store metadata with the entity version of a given configuration. Returns NO if there are differences between the version information.  (For information on specific differences, developers should utilize the entityVersionHashesByName method, and perform a comparison.)
 */
-- (BOOL)isConfiguration:(nullable NSString *)configuration compatibleWithStoreMetadata:(NSDictionary<NSString *, id> *)metadata NS_AVAILABLE(10_5,3_0);
+- (BOOL)isConfiguration:(nullable NSString *)configuration compatibleWithStoreMetadata:(NSDictionary<NSString *, id> *)metadata API_AVAILABLE(macosx(10.5),ios(3.0));
 
 
 /* Returns a dictionary of the version hashes for the entities in the model, keyed by entity name.  (The dictionary of version hash information is used by Core Data to determine schema compatibility.)
 */
-@property (readonly, copy) NSDictionary<NSString *, NSData *> *entityVersionHashesByName NS_AVAILABLE(10_5,3_0);
+@property (readonly, copy) NSDictionary<NSString *, NSData *> *entityVersionHashesByName API_AVAILABLE(macosx(10.5),ios(3.0));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMappingModel.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMappingModel.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMappingModel.h	2016-05-21 07:41:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMappingModel.h	2016-06-27 06:09:43.000000000 +0200
@@ -15,7 +15,7 @@
 @class NSManagedObjectModel;
 @class NSEntityMapping;
 
-NS_CLASS_AVAILABLE(10_5,3_0)
+API_AVAILABLE(macosx(10.5),ios(3.0))
 @interface NSMappingModel: NSObject {
 #if (!__OBJC2__)
     @private
@@ -37,7 +37,7 @@
 
 /* Returns a newly created mapping model to translate data from the source to the destination model, if possible.  The differences between the source and destination model are compared and if all changes are simple enough to be able to reasonably infer a data migration mapping model, such a model is created and returned.  If the mapping model can not be created, nil is returned and an error code is returned to indicate why inferring a mapping model automatically failed.
  */
-+ (nullable NSMappingModel *)inferredMappingModelForSourceModel:(NSManagedObjectModel *)sourceModel destinationModel:(NSManagedObjectModel *)destinationModel error:(NSError **)error NS_AVAILABLE(10_6,3_0);
++ (nullable NSMappingModel *)inferredMappingModelForSourceModel:(NSManagedObjectModel *)sourceModel destinationModel:(NSManagedObjectModel *)destinationModel error:(NSError **)error API_AVAILABLE(macosx(10.6),ios(3.0));
 
 /* Loads the mapping model from the specified URL.
 */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMergePolicy.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMergePolicy.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMergePolicy.h	2016-05-26 06:23:56.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMergePolicy.h	2016-06-27 07:21:43.000000000 +0200
@@ -15,19 +15,19 @@
 @class NSManagedObject;
 
 // Default policy for all managed object contexts - save returns with an error that contains the object IDs of the objects that had conflicts(NSInsertedObjectsKey, NSUpdatedObjectsKey).
-COREDATA_EXTERN id NSErrorMergePolicy NS_AVAILABLE(10_4, 3_0);
+COREDATA_EXTERN id NSErrorMergePolicy API_AVAILABLE(macosx(10.4),ios(3.0));
 
 // This singleton policy merges conflicts between the persistent store's version of the object and the current in memory version. The merge occurs by individual property. For properties which have been changed in both the external source and in memory, the external changes trump the in memory ones.
-COREDATA_EXTERN id NSMergeByPropertyStoreTrumpMergePolicy NS_AVAILABLE(10_4, 3_0);    
+COREDATA_EXTERN id NSMergeByPropertyStoreTrumpMergePolicy API_AVAILABLE(macosx(10.4),ios(3.0));    
 
 // This singleton policy merges conflicts between the persistent store's version of the object and the current in memory version. The merge occurs by individual property. For properties which have been changed in both the external source and in memory, the in memory changes trump the external ones.
-COREDATA_EXTERN id NSMergeByPropertyObjectTrumpMergePolicy NS_AVAILABLE(10_4, 3_0);    
+COREDATA_EXTERN id NSMergeByPropertyObjectTrumpMergePolicy API_AVAILABLE(macosx(10.4),ios(3.0));    
 
 // This singleton policy overwrites all state for the changed objects in conflict The current object's state is pushed upon the persistent store.
-COREDATA_EXTERN id NSOverwriteMergePolicy NS_AVAILABLE(10_4, 3_0);    
+COREDATA_EXTERN id NSOverwriteMergePolicy API_AVAILABLE(macosx(10.4),ios(3.0));    
 
 // This singleton policy discards all state for the changed objects in conflict. The persistent store's version of the object is used.
-COREDATA_EXTERN id NSRollbackMergePolicy NS_AVAILABLE(10_4, 3_0);    
+COREDATA_EXTERN id NSRollbackMergePolicy API_AVAILABLE(macosx(10.4),ios(3.0));    
 
 
 typedef NS_ENUM(NSUInteger, NSMergePolicyType) {
@@ -38,7 +38,7 @@
     NSRollbackMergePolicyType                   = 0x04
 };
 
-NS_CLASS_AVAILABLE(10_7, 5_0)
+API_AVAILABLE(macosx(10.7),ios(5.0))
 @interface NSMergeConflict : NSObject {
 }
 
@@ -74,7 +74,7 @@
  although if an entity hierarchy has a constraint which is extended in subentities, all constraint violations for that constraint
  will be collapsed into a single report.
  */
-NS_CLASS_AVAILABLE(10_11, 9_0)
+API_AVAILABLE(macosx(10.11),ios(9.0))
 @interface NSConstraintConflict : NSObject {
 }
 
@@ -103,15 +103,15 @@
 
 @end
 
-NS_CLASS_AVAILABLE(10_7, 5_0)
+API_AVAILABLE(macosx(10.7),ios(5.0))
 @interface NSMergePolicy : NSObject {
 }
 
-@property (class, readonly, strong) NSMergePolicy *errorMergePolicy NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
-@property (class, readonly, strong) NSMergePolicy *rollbackMergePolicy NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
-@property (class, readonly, strong) NSMergePolicy *overwriteMergePolicy NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
-@property (class, readonly, strong) NSMergePolicy *mergeByPropertyObjectTrumpMergePolicy NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
-@property (class, readonly, strong) NSMergePolicy *mergeByPropertyStoreTrumpMergePolicy NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+@property (class, readonly, strong) NSMergePolicy *errorMergePolicy API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
+@property (class, readonly, strong) NSMergePolicy *rollbackMergePolicy API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
+@property (class, readonly, strong) NSMergePolicy *overwriteMergePolicy API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
+@property (class, readonly, strong) NSMergePolicy *mergeByPropertyObjectTrumpMergePolicy API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
+@property (class, readonly, strong) NSMergePolicy *mergeByPropertyStoreTrumpMergePolicy API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
 @property (readonly) NSMergePolicyType mergeType;
 
@@ -135,12 +135,12 @@
  *  any mistakes will cause permanent data corruption in the form of dangling foreign keys.
  * Will be called before -resolveConstraintConflicts:error:
  */
-- (BOOL)resolveOptimisticLockingVersionConflicts:(NSArray<NSMergeConflict *> *)list error:(NSError **)error NS_AVAILABLE(10_11, 9_0);
+- (BOOL)resolveOptimisticLockingVersionConflicts:(NSArray<NSMergeConflict *> *)list error:(NSError **)error API_AVAILABLE(macosx(10.11),ios(9.0));
 
 /* Resolve uniqueness constraint violations for the list of failures.
  *  Will be called after -resolveOptimisticLockingVersionConflicts:error:
  */
-- (BOOL)resolveConstraintConflicts:(NSArray<NSConstraintConflict *> *)list error:(NSError **)error NS_AVAILABLE(10_11, 9_0);
+- (BOOL)resolveConstraintConflicts:(NSArray<NSConstraintConflict *> *)list error:(NSError **)error API_AVAILABLE(macosx(10.11),ios(9.0));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMigrationManager.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMigrationManager.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMigrationManager.h	2016-05-26 06:23:57.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSMigrationManager.h	2016-06-27 07:23:57.000000000 +0200
@@ -19,7 +19,7 @@
 @class NSMappingModel;
 @class NSMigrationContext;
 
-NS_CLASS_AVAILABLE(10_5, 3_0)
+API_AVAILABLE(macosx(10.5),ios(3.0))
 @interface NSMigrationManager : NSObject {
 }
 
@@ -32,7 +32,7 @@
 
 /* Tries to use a store specific migration manager to perform the store migration, note that a store specific migration manager class is not guaranteed to perform any of the migration manager delegate callbacks or update values for the observable properties.  
  Defaults to YES */
-@property () BOOL usesStoreSpecificMigrationManager NS_AVAILABLE(10_7,  5_0);
+@property () BOOL usesStoreSpecificMigrationManager API_AVAILABLE(macosx(10.7),ios(5.0));
 
 /* Resets the association tables for the migration.  (Note this does NOT reset the source or destination contexts).*/
 - (void)reset;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentContainer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentContainer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentContainer.h	2016-05-21 07:41:59.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentContainer.h	2016-06-27 06:09:43.000000000 +0200
@@ -15,7 +15,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 // An instance of NSPersistentContainer includes all objects needed to represent a functioning Core Data stack, and provides convenience methods and properties for common patterns.
-NS_CLASS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0)
+API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0))
 @interface NSPersistentContainer : NSObject {
 #if (!__OBJC2__)
 @private
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStore.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStore.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStore.h	2016-05-21 07:41:59.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStore.h	2016-06-27 06:09:43.000000000 +0200
@@ -21,7 +21,7 @@
 @class NSPersistentStoreRequest;
 @class NSPersistentStoreCoordinator;
 
-NS_CLASS_AVAILABLE(10_5, 3_0)
+API_AVAILABLE(macosx(10.5),ios(3.0))
 @interface NSPersistentStore : NSObject {
 }
 
@@ -36,7 +36,7 @@
 
 /* Returns the NSMigrationManager class optimized for this store class.  Subclasses of NSPersistentStore can override this to provide a custom migration manager subclass (eg to take advantage of store-specific functionality to improve migration performance).
  */
-+ (Class)migrationManagerClass NS_AVAILABLE(10_6, 3_0);
++ (Class)migrationManagerClass API_AVAILABLE(macosx(10.6),ios(3.0));
 
 /* the designated initializer for object stores. */
 - (instancetype)initWithPersistentStoreCoordinator:(nullable NSPersistentStoreCoordinator *)root configurationName:(nullable NSString *)name URL:(NSURL *)url options:(nullable NSDictionary *)options NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreCoordinator.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreCoordinator.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreCoordinator.h	2016-05-21 07:49:57.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreCoordinator.h	2016-06-27 06:09:43.000000000 +0200
@@ -24,99 +24,99 @@
 @class NSPersistentStoreDescription;
 
 // Persistent store types supported by Core Data:
-COREDATA_EXTERN NSString * const NSSQLiteStoreType NS_AVAILABLE(10_4, 3_0);
-COREDATA_EXTERN NSString * const NSXMLStoreType NS_AVAILABLE(10_4, NA);
-COREDATA_EXTERN NSString * const NSBinaryStoreType NS_AVAILABLE(10_4, 3_0);
-COREDATA_EXTERN NSString * const NSInMemoryStoreType NS_AVAILABLE(10_4, 3_0);
+COREDATA_EXTERN NSString * const NSSQLiteStoreType API_AVAILABLE(macosx(10.4),ios(3.0));
+COREDATA_EXTERN NSString * const NSXMLStoreType API_AVAILABLE(macosx(10.4)) API_UNAVAILABLE(ios);
+COREDATA_EXTERN NSString * const NSBinaryStoreType API_AVAILABLE(macosx(10.4),ios(3.0));
+COREDATA_EXTERN NSString * const NSInMemoryStoreType API_AVAILABLE(macosx(10.4),ios(3.0));
 
 // Persistent store metadata dictionary keys:
 
 // key in the metadata dictionary to identify the store type
-COREDATA_EXTERN NSString * const NSStoreTypeKey NS_AVAILABLE(10_4, 3_0);    
+COREDATA_EXTERN NSString * const NSStoreTypeKey API_AVAILABLE(macosx(10.4),ios(3.0));    
 
 // key in the metadata dictionary to identify the store UUID - the store UUID is useful to identify stores through URI representations, but it is NOT guaranteed to be unique (while the UUID generated for new stores is unique, users can freely copy files and thus the UUID stored inside, so developers that track/reference stores explicitly do need to be aware of duplicate UUIDs and potentially override the UUID when a new store is added to the list of known stores in their application)
-COREDATA_EXTERN NSString * const NSStoreUUIDKey NS_AVAILABLE(10_4, 3_0);    
+COREDATA_EXTERN NSString * const NSStoreUUIDKey API_AVAILABLE(macosx(10.4),ios(3.0));    
 
 /* A notification posted before the list of open persistent stores changes, similar to NSPersistentStoreCoordinatorStoresDidChangeNotification.  If the application is running, Core Data will post this before responding to iCloud account changes or "Delete All" from Documents & Data.
  */
-COREDATA_EXTERN NSString * const NSPersistentStoreCoordinatorStoresWillChangeNotification NS_AVAILABLE(10_9, 7_0);
+COREDATA_EXTERN NSString * const NSPersistentStoreCoordinatorStoresWillChangeNotification API_AVAILABLE(macosx(10.9),ios(7.0));
 
 // user info dictionary contains information about the stores that were added or removed
-COREDATA_EXTERN NSString * const NSPersistentStoreCoordinatorStoresDidChangeNotification NS_AVAILABLE(10_4, 3_0);    
+COREDATA_EXTERN NSString * const NSPersistentStoreCoordinatorStoresDidChangeNotification API_AVAILABLE(macosx(10.4),ios(3.0));    
 
 // sent during the invocation of NSPersistentStore's willRemoveFromPersistentStoreCoordinator during store deallocation or removal
-COREDATA_EXTERN NSString * const NSPersistentStoreCoordinatorWillRemoveStoreNotification NS_AVAILABLE(10_5, 3_0);    
+COREDATA_EXTERN NSString * const NSPersistentStoreCoordinatorWillRemoveStoreNotification API_AVAILABLE(macosx(10.5),ios(3.0));    
 
 // User info keys for NSPersistentStoreCoordinatorStoresDidChangeNotification:
 
 // The object values for NSAddedPersistentStoresKey and NSRemovedPersistentStoresKey will be arrays containing added/removed stores
-COREDATA_EXTERN NSString * const NSAddedPersistentStoresKey NS_AVAILABLE(10_4, 3_0);
-COREDATA_EXTERN NSString * const NSRemovedPersistentStoresKey NS_AVAILABLE(10_4, 3_0);
+COREDATA_EXTERN NSString * const NSAddedPersistentStoresKey API_AVAILABLE(macosx(10.4),ios(3.0));
+COREDATA_EXTERN NSString * const NSRemovedPersistentStoresKey API_AVAILABLE(macosx(10.4),ios(3.0));
 
 // The object value for NSUUIDChangedPersistentStoresKey will be an array where the object at index 0 will be the old store instance, and the object at index 1 the new
-COREDATA_EXTERN NSString * const NSUUIDChangedPersistentStoresKey NS_AVAILABLE(10_4, 3_0);
+COREDATA_EXTERN NSString * const NSUUIDChangedPersistentStoresKey API_AVAILABLE(macosx(10.4),ios(3.0));
 
 // Persistent store option keys:
 
 // flag indicating whether a store is treated as read-only or not - default is NO
-COREDATA_EXTERN NSString * const NSReadOnlyPersistentStoreOption NS_AVAILABLE(10_4, 3_0);    
+COREDATA_EXTERN NSString * const NSReadOnlyPersistentStoreOption API_AVAILABLE(macosx(10.4),ios(3.0));    
 
 // flag indicating whether an XML file should be validated with the DTD while opening - default is NO
-COREDATA_EXTERN NSString * const NSValidateXMLStoreOption NS_AVAILABLE(10_4, NA);    
+COREDATA_EXTERN NSString * const NSValidateXMLStoreOption API_AVAILABLE(macosx(10.4)) API_UNAVAILABLE(ios);    
 
 // Migration keys:
 
 /* Options key specifying the connection timeout for Core Data stores.  This value (an NSNumber) represents the duration, in seconds, Core Data will wait while attempting to create a connection to a persistent store.  If a connection is unable to be made within that timeframe, the operation is aborted and an error is returned.  
 */
-COREDATA_EXTERN NSString * const NSPersistentStoreTimeoutOption NS_AVAILABLE(10_5, 3_0);
+COREDATA_EXTERN NSString * const NSPersistentStoreTimeoutOption API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Options key for a dictionary of sqlite pragma settings with pragma values indexed by pragma names as keys.  All pragma values must be specified as strings.  The fullfsync and synchronous pragmas control the tradeoff between write performance (write to disk speed & cache utilization) and durability (data loss/corruption sensitivity to power interruption).  For more information on pragma settings visit <http://sqlite.org/pragma.html>
 */
-COREDATA_EXTERN NSString * const NSSQLitePragmasOption NS_AVAILABLE(10_5, 3_0);
+COREDATA_EXTERN NSString * const NSSQLitePragmasOption API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Option key to run an analysis of the store data to optimize indices based on statistical information when the store is added to the coordinator.  This invokes SQLite's ANALYZE command.  Ignored by other stores.
 */
-COREDATA_EXTERN NSString * const NSSQLiteAnalyzeOption NS_AVAILABLE(10_5, 3_0);
+COREDATA_EXTERN NSString * const NSSQLiteAnalyzeOption API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Option key to rebuild the store file, forcing a database wide defragmentation when the store is added to the coordinator.  This invokes SQLite's VACUUM command.  Ignored by other stores.
  */
-COREDATA_EXTERN NSString * const NSSQLiteManualVacuumOption NS_AVAILABLE(10_6, 3_0);
+COREDATA_EXTERN NSString * const NSSQLiteManualVacuumOption API_AVAILABLE(macosx(10.6),ios(3.0));
 
 /* Options key to ignore the built-in versioning provided by Core Data.  If the value for this key (an NSNumber) evaluates to YES (using boolValue), Core Data will not compare the version hashes between the managed object model in the coordinator and the metadata for the loaded store.  (It will, however, continue to update the version hash information in the metadata.)  This key is specified by default for all applications linked on or before Mac OS X 10.4.
 */
-COREDATA_EXTERN NSString * const NSIgnorePersistentStoreVersioningOption NS_AVAILABLE(10_5, 3_0);
+COREDATA_EXTERN NSString * const NSIgnorePersistentStoreVersioningOption API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Options key to automatically attempt to migrate versioned stores.  If the value for this key (an NSNumber) evaluates to YES (using boolValue) Core Data will, if the version hash information for added store is determined to be incompatible with the model for the coordinator, attempt to locate the source and mapping models in the application bundles, and perform a migration.  
 */
-COREDATA_EXTERN NSString * const NSMigratePersistentStoresAutomaticallyOption NS_AVAILABLE(10_5, 3_0);
+COREDATA_EXTERN NSString * const NSMigratePersistentStoresAutomaticallyOption API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* When combined with NSMigratePersistentStoresAutomaticallyOption, coordinator will attempt to infer a mapping model if none can be found */
-COREDATA_EXTERN NSString * const NSInferMappingModelAutomaticallyOption NS_AVAILABLE(10_6, 3_0);
+COREDATA_EXTERN NSString * const NSInferMappingModelAutomaticallyOption API_AVAILABLE(macosx(10.6),ios(3.0));
 
 /* Key to represent the version hash information (dictionary) for the model used to create a persistent store.  This key is used in the metadata for a persistent store.
 */
-COREDATA_EXTERN NSString * const NSStoreModelVersionHashesKey NS_AVAILABLE(10_5, 3_0);    
+COREDATA_EXTERN NSString * const NSStoreModelVersionHashesKey API_AVAILABLE(macosx(10.5),ios(3.0));    
 
 /* Key to represent the version identifier for the model used to create the store. This key is used in the metadata for a persistent store.
 */
-COREDATA_EXTERN NSString * const NSStoreModelVersionIdentifiersKey NS_AVAILABLE(10_5, 3_0);    
+COREDATA_EXTERN NSString * const NSStoreModelVersionIdentifiersKey API_AVAILABLE(macosx(10.5),ios(3.0));    
 
 /* Key to represent the earliest version of MacOS X the persistent store should support.  Backward compatibility may preclude some features.  The numeric values are defined in AvailabilityMacros.h
 */
-COREDATA_EXTERN NSString * const NSPersistentStoreOSCompatibility NS_AVAILABLE(10_5, 3_0);
+COREDATA_EXTERN NSString * const NSPersistentStoreOSCompatibility API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* User info key specifying the maximum connection pool size that should be used on a store that supports concurrent request handling, the value should be an NSNumber. The connection pool size determines the number of requests a store can handle concurrently, and should be a function of how many contexts are attempting to access store data at any time. Generally, application developers should not set this, and should use the default value. The default connection pool size is implementation dependent and may vary by store type and/or platform.
  */
-COREDATA_EXTERN NSString * const NSPersistentStoreConnectionPoolMaxSizeKey NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+COREDATA_EXTERN NSString * const NSPersistentStoreConnectionPoolMaxSizeKey API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
 /* store option for the destroy... and replace... to indicate that the store file should be destroyed even if the operation might be unsafe (overriding locks
  */
-COREDATA_EXTERN NSString * const NSPersistentStoreForceDestroyOption NS_AVAILABLE(10_8, 6_0);
+COREDATA_EXTERN NSString * const NSPersistentStoreForceDestroyOption API_AVAILABLE(macosx(10.8),ios(6.0));
 
 /* Key to represent the protection class for the persistent store.  Backward compatibility may preclude some features.  The acceptable values are those defined in Foundation for the NSFileProtectionKey.  The default value of NSPersistentStoreFileProtectionKey is NSFileProtectionCompleteUntilFirstUserAuthentication for all applications built on or after iOS5.  The default value for all older applications is NSFileProtectionNone. */
-COREDATA_EXTERN NSString * const NSPersistentStoreFileProtectionKey NS_AVAILABLE(NA, 5_0);
+COREDATA_EXTERN NSString * const NSPersistentStoreFileProtectionKey API_AVAILABLE(ios(5.0)) API_UNAVAILABLE(macosx);
 
-NS_CLASS_AVAILABLE(10_4,3_0)
+API_AVAILABLE(macosx(10.4),ios(3.0))
 @interface NSPersistentStoreCoordinator : NSObject {
 }
 
@@ -127,20 +127,20 @@
 @property (readonly, strong) NSArray<__kindof NSPersistentStore *> *persistentStores;
 
 /* custom name for a coordinator.  Coordinators will set the label on their queue */
-@property (nullable, copy) NSString *name  NS_AVAILABLE(10_10, 8_0);
+@property (nullable, copy) NSString *name  API_AVAILABLE(macosx(10.10),ios(8.0));
 
 - (nullable __kindof NSPersistentStore *)persistentStoreForURL:(NSURL *)URL;
 - (NSURL *)URLForPersistentStore:(NSPersistentStore *)store;
 
 /* Sets the URL for the specified store in the coordinator.  For atomic stores, this will alter the location to which the next save operation will persist the file;  for non-atomic stores, invoking this method will release the existing connection and create a new one at the specified URL.  (For non-atomic stores, a store must pre-exist at the destination URL; a new store will not be created.)
  */
-- (BOOL)setURL:(NSURL*)url forPersistentStore:(NSPersistentStore *)store NS_AVAILABLE(10_5, 3_0);
+- (BOOL)setURL:(NSURL*)url forPersistentStore:(NSPersistentStore *)store API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Adds the store at the specified URL (of the specified type) to the coordinator with the model configuration and options.  The configuration can be nil -- then it's the complete model; storeURL is usually the file location of the database
  */
 - (nullable __kindof NSPersistentStore *)addPersistentStoreWithType:(NSString *)storeType configuration:(nullable NSString *)configuration URL:(nullable NSURL *)storeURL options:(nullable NSDictionary *)options error:(NSError **)error;
 
-- (void)addPersistentStoreWithDescription:(NSPersistentStoreDescription *)storeDescription completionHandler:(void (^)(NSPersistentStoreDescription *, NSError * _Nullable))block NS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0);
+- (void)addPersistentStoreWithDescription:(NSPersistentStoreDescription *)storeDescription completionHandler:(void (^)(NSPersistentStoreDescription *, NSError * _Nullable))block API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0));
 
 - (BOOL)removePersistentStore:(NSPersistentStore *)store error:(NSError **)error;
 
@@ -161,20 +161,20 @@
  The contents of the array will vary depending on the request type: NSFetchRequest results will be an array of managed objects, managed object IDs, or NSDictionaries;
  NSSaveChangesRequests will an empty array. User defined requests will return arrays of arrays, where the nested array is the result returned form a single store.
  */
-- (nullable id)executeRequest:(NSPersistentStoreRequest *)request withContext:(NSManagedObjectContext *)context error:(NSError**)error NS_AVAILABLE(10_7,  5_0);
+- (nullable id)executeRequest:(NSPersistentStoreRequest *)request withContext:(NSManagedObjectContext *)context error:(NSError**)error API_AVAILABLE(macosx(10.7),ios(5.0));
 
 /* Returns a dictionary of the registered store types:  the keys are the store type strings and the values are the NSPersistentStore subclasses wrapped in NSValues.
 */
-@property(class, readonly, strong) NSDictionary<NSString *, NSValue *> *registeredStoreTypes NS_AVAILABLE(10_5, 3_0);
+@property(class, readonly, strong) NSDictionary<NSString *, NSValue *> *registeredStoreTypes API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Registers the specified NSPersistentStore subclass for the specified store type string.  This method must be invoked before a custom subclass of NSPersistentStore can be loaded into a persistent store coordinator.  Passing nil for the store class argument will unregister the specified store type.
 */
-+ (void)registerStoreClass:(Class)storeClass forStoreType:(NSString *)storeType NS_AVAILABLE(10_5, 3_0);
++ (void)registerStoreClass:(Class)storeClass forStoreType:(NSString *)storeType API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Allows to access the metadata stored in a persistent store without warming up a CoreData stack; the guaranteed keys in this dictionary are NSStoreTypeKey and NSStoreUUIDKey. If storeType is nil, Core Data will guess which store class should be used to get/set the store file's metadata. 
  */
-+ (nullable NSDictionary<NSString *, id> *)metadataForPersistentStoreOfType:(NSString*)storeType URL:(NSURL *)url options:(nullable NSDictionary *)options error:(NSError **)error NS_AVAILABLE(10_9,7_0);
-+ (BOOL)setMetadata:(nullable NSDictionary<NSString *, id> *)metadata forPersistentStoreOfType:(NSString*)storeType URL:(NSURL*)url options:(nullable NSDictionary*)options error:(NSError**)error NS_AVAILABLE(10_9,7_0);
++ (nullable NSDictionary<NSString *, id> *)metadataForPersistentStoreOfType:(NSString*)storeType URL:(NSURL *)url options:(nullable NSDictionary *)options error:(NSError **)error API_AVAILABLE(macosx(10.9),ios(7.0));
++ (BOOL)setMetadata:(nullable NSDictionary<NSString *, id> *)metadata forPersistentStoreOfType:(NSString*)storeType URL:(NSURL*)url options:(nullable NSDictionary*)options error:(NSError**)error API_AVAILABLE(macosx(10.9),ios(7.0));
     
 /* Used for save as - performance may vary depending on the type of old and new store; the old store is usually removed from the coordinator by the migration operation, and therefore is no longer a useful reference after invoking this method
 */
@@ -182,22 +182,22 @@
 
 /* delete or truncate the target persistent store in accordance with the store class's requirements.  It is important to pass similar options as addPersistentStoreWithType: ... SQLite stores will honor file locks, journal files, journaling modes, and other intricacies.  It is not possible to unlink a database file safely out from underneath another thread or process, so this API performs a truncation.  Other stores will default to using NSFileManager.
  */
-- (BOOL)destroyPersistentStoreAtURL:(NSURL *)url withType:(NSString *)storeType options:(nullable NSDictionary *)options error:(NSError**)error NS_AVAILABLE(10_11, 9_0);
+- (BOOL)destroyPersistentStoreAtURL:(NSURL *)url withType:(NSString *)storeType options:(nullable NSDictionary *)options error:(NSError**)error API_AVAILABLE(macosx(10.11),ios(9.0));
     
 /* copy or overwrite the target persistent store in accordance with the store class's requirements.  It is important to pass similar options as addPersistentStoreWithType: ... SQLite stores will honor file locks, journal files, journaling modes, and other intricacies.  Other stores will default to using NSFileManager.
  */
-- (BOOL)replacePersistentStoreAtURL:(NSURL *)destinationURL destinationOptions:(nullable NSDictionary *)destinationOptions withPersistentStoreFromURL:(NSURL *)sourceURL sourceOptions:(nullable NSDictionary *)sourceOptions storeType:(NSString *)storeType error:(NSError**)error NS_AVAILABLE(10_11, 9_0);
+- (BOOL)replacePersistentStoreAtURL:(NSURL *)destinationURL destinationOptions:(nullable NSDictionary *)destinationOptions withPersistentStoreFromURL:(NSURL *)sourceURL sourceOptions:(nullable NSDictionary *)sourceOptions storeType:(NSString *)storeType error:(NSError**)error API_AVAILABLE(macosx(10.11),ios(9.0));
 
 /* asynchronously performs the block on the coordinator's queue.  Encapsulates an autorelease pool. */
-- (void)performBlock:(void (^)())block  NS_AVAILABLE(10_10, 8_0);
+- (void)performBlock:(void (^)())block  API_AVAILABLE(macosx(10.10),ios(8.0));
 
 /* synchronously performs the block on the coordinator's queue.  May safely be called reentrantly. Encapsulates an autorelease pool. */
-- (void)performBlockAndWait:(void (^)())block  NS_AVAILABLE(10_10, 8_0);
+- (void)performBlockAndWait:(void (^)())block  API_AVAILABLE(macosx(10.10),ios(8.0));
 
 
-+ (nullable NSDictionary<NSString *, id> *)metadataForPersistentStoreOfType:(nullable NSString *)storeType URL:(NSURL *)url error:(NSError **)error NS_DEPRECATED(10_5,10_11,3_0,9_0, "Use a -metadataForPersistentStoreOfType:URL:options:error: and pass in an options dictionary matching addPersistentStoreWithType");
++ (nullable NSDictionary<NSString *, id> *)metadataForPersistentStoreOfType:(nullable NSString *)storeType URL:(NSURL *)url error:(NSError **)error API_DEPRECATED("Use -metadataForPersistentStoreOfType:URL:options:error: and pass in an options dictionary matching addPersistentStoreWithType", macosx(10.5,10.11), ios(3.0,9.0));
     
-+ (BOOL)setMetadata:(nullable NSDictionary<NSString *, id> *)metadata forPersistentStoreOfType:(nullable NSString *)storeType URL:(NSURL*)url error:(NSError **)error NS_DEPRECATED(10_5, 10_11,3_0,9_0,"Use a -setMetadata:forPersistentStoreOfType:URL:options:error: and pass in an options dictionary matching addPersistentStoreWithType");
++ (BOOL)setMetadata:(nullable NSDictionary<NSString *, id> *)metadata forPersistentStoreOfType:(nullable NSString *)storeType URL:(NSURL*)url error:(NSError **)error API_DEPRECATED("Use  -setMetadata:forPersistentStoreOfType:URL:options:error: and pass in an options dictionary matching addPersistentStoreWithType", macosx(10.5,10.11), ios(3.0,9.0));
     
 
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreDescription.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreDescription.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreDescription.h	2016-05-21 07:41:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreDescription.h	2016-06-27 06:09:43.000000000 +0200
@@ -13,7 +13,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 // An instance of NSPersistentStoreDescription encapsulates all information needed to describe a persistent store.
-NS_CLASS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0)
+API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0))
 @interface NSPersistentStoreDescription : NSObject <NSCopying> {
 #if (!__OBJC2__)
 @private
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreRequest.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreRequest.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreRequest.h	2016-05-21 07:41:59.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreRequest.h	2016-06-27 06:09:43.000000000 +0200
@@ -14,11 +14,11 @@
 typedef NS_ENUM(NSUInteger, NSPersistentStoreRequestType) {
     NSFetchRequestType = 1,
     NSSaveRequestType,
-    NSBatchUpdateRequestType NS_ENUM_AVAILABLE(10_10, 8_0) = 6,
-    NSBatchDeleteRequestType NS_ENUM_AVAILABLE(10_11, 9_0) = 7
+    NSBatchUpdateRequestType API_AVAILABLE(macosx(10.10), ios(8.0)) = 6,
+    NSBatchDeleteRequestType API_AVAILABLE(macosx(10.11), ios(9.0)) = 7
 };
 
-NS_CLASS_AVAILABLE(10_7, 5_0)
+API_AVAILABLE(macosx(10.7),ios(5.0))
 @interface NSPersistentStoreRequest : NSObject <NSCopying> {
 }
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreResult.h	2016-05-21 07:41:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPersistentStoreResult.h	2016-06-27 06:09:43.000000000 +0200
@@ -18,25 +18,25 @@
 @class NSAsynchronousFetchRequest;
 
 typedef NS_ENUM(NSUInteger, NSBatchUpdateRequestResultType) {
-    NSStatusOnlyResultType = 0x0,                 // Don't return anything
-    NSUpdatedObjectIDsResultType = 0x1,   // Return the object IDs of the rows that were updated
+    NSStatusOnlyResultType = 0x0,            // Return a status boolean
+    NSUpdatedObjectIDsResultType = 0x1,      // Return the object IDs of the rows that were updated
     NSUpdatedObjectsCountResultType = 0x2    // Return the number of rows that were updated
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10), ios(8.0));
 
 typedef NS_ENUM(NSUInteger, NSBatchDeleteRequestResultType) {
-    NSBatchDeleteResultTypeStatusOnly = 0x0,                 // Don't return anything
-    NSBatchDeleteResultTypeObjectIDs = 0x1,   // Return the object IDs of the rows that were deleted
-    NSBatchDeleteResultTypeCount = 0x2,   // Return the object IDs of the rows that were deleted
-} NS_ENUM_AVAILABLE(10_11, 9_0);
+    NSBatchDeleteResultTypeStatusOnly = 0x0, // Return a status boolean
+    NSBatchDeleteResultTypeObjectIDs = 0x1,  // Return the object IDs of the rows that were deleted
+    NSBatchDeleteResultTypeCount = 0x2,      // Return the number of rows that were deleted
+} API_AVAILABLE(macosx(10.11), ios(9.0));
 
 // Used to wrap the result of whatever is returned by the persistent store coordinator when
 // -[NSManagedObjectContext executeRequest:error:] is called
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10),ios(8.0))
 @interface NSPersistentStoreResult : NSObject
 
 @end
 
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10),ios(8.0))
 @interface NSPersistentStoreAsynchronousResult : NSPersistentStoreResult {
 #if (!__OBJC2__)
 @private
@@ -56,7 +56,7 @@
 
 @end
 
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10),ios(8.0))
 @interface NSAsynchronousFetchResult<ResultType:id<NSFetchRequestResult>> : NSPersistentStoreAsynchronousResult {
 #if (!__OBJC2__)
 @private
@@ -72,7 +72,7 @@
 @end
 
 // The result returned when executing an NSBatchUpdateRequest
-NS_CLASS_AVAILABLE(10_10,8_0)
+API_AVAILABLE(macosx(10.10),ios(8.0))
 @interface NSBatchUpdateResult : NSPersistentStoreResult {
 #if (!__OBJC2__)
 @private
@@ -89,7 +89,7 @@
 
 
 // The result returned when executing an NSBatchDeleteRequest
-NS_CLASS_AVAILABLE(10_11,9_0)
+API_AVAILABLE(macosx(10.11),ios(9.0))
 @interface NSBatchDeleteResult : NSPersistentStoreResult {
 #if (!__OBJC2__)
 @private
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyDescription.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyDescription.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyDescription.h	2016-05-21 07:41:59.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyDescription.h	2016-06-27 06:09:43.000000000 +0200
@@ -15,7 +15,7 @@
 @class NSPredicate;
 
 // Properties describe values within a managed object. There are different types of properties, each of them represented by a subclass which encapsulates the specific property behavior.
-NS_CLASS_AVAILABLE(10_4,3_0)
+API_AVAILABLE(macosx(10.4),ios(3.0))
 @interface NSPropertyDescription : NSObject <NSCoding, NSCopying> {
 }
 
@@ -38,25 +38,25 @@
 
 /* Returns a boolean value indicating if the property is important for searching.  NSPersistentStores can optionally utilize this information upon store creation for operations like defining indexes.
 */
-@property (getter=isIndexed) BOOL indexed NS_AVAILABLE(10_5,3_0);
+@property (getter=isIndexed) BOOL indexed API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Returns the version hash for the property.  The version hash is used to uniquely identify a property based on its configuration.  The version hash uses only values which affect the persistence of data and the user-defined versionHashModifier value.  (The values which affect persistence are the name of the property, the flags for isOptional, isTransient, and isReadOnly).  This value is stored as part of the version information in the metadata for stores, as well as a definition of a property involved in an NSPropertyMapping.
 */
-@property (readonly, copy) NSData *versionHash NS_AVAILABLE(10_5,3_0);
+@property (readonly, copy) NSData *versionHash API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Returns/sets the version hash modifier for the property.  This value is included in the version hash for the property, allowing developers to mark/denote a property as being a different "version" than another, even if all of the values which affects persistence are equal.  (Such a difference is important in cases where the design of a property is unchanged, but the format or content of data has changed.)
 */
-@property (nullable, copy) NSString *versionHashModifier NS_AVAILABLE(10_5,3_0);
+@property (nullable, copy) NSString *versionHashModifier API_AVAILABLE(macosx(10.5),ios(3.0));
 
 /* Returns a boolean value indicating if the property should be indexed by Spotlight.
 */
-@property (getter=isIndexedBySpotlight) BOOL indexedBySpotlight NS_AVAILABLE(10_6,3_0);
+@property (getter=isIndexedBySpotlight) BOOL indexedBySpotlight API_AVAILABLE(macosx(10.6),ios(3.0));
 
 /* Returns a boolean value indicating if the property data should be written out to the external record file.
 */
-@property (getter=isStoredInExternalRecord) BOOL storedInExternalRecord NS_AVAILABLE(10_6,3_0);
+@property (getter=isStoredInExternalRecord) BOOL storedInExternalRecord API_AVAILABLE(macosx(10.6),ios(3.0));
 
-@property (nullable, copy) NSString *renamingIdentifier NS_AVAILABLE(10_6,3_0);
+@property (nullable, copy) NSString *renamingIdentifier API_AVAILABLE(macosx(10.6),ios(3.0));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyMapping.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyMapping.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyMapping.h	2016-05-21 07:41:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSPropertyMapping.h	2016-06-27 06:09:43.000000000 +0200
@@ -13,7 +13,7 @@
 
 @class NSExpression;
 
-NS_CLASS_AVAILABLE(10_5,3_0)
+API_AVAILABLE(macosx(10.5),ios(3.0))
 @interface NSPropertyMapping : NSObject {
 #if (!__OBJC2__)
     @private
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSQueryGenerationToken.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSQueryGenerationToken.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSQueryGenerationToken.h	2016-05-21 07:41:58.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSQueryGenerationToken.h	2016-06-27 06:09:43.000000000 +0200
@@ -8,7 +8,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_12,10_0) __TVOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0)
+API_AVAILABLE(macosx(10.12),ios(10.0),tvos(10.0),watchos(3.0))
 // Class used to track database generations for generational querying.
 // See NSManagedObjectContext for details on how it is used.
 @interface NSQueryGenerationToken : NSObject <NSCopying> 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSRelationshipDescription.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSRelationshipDescription.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSRelationshipDescription.h	2016-05-21 07:41:59.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSRelationshipDescription.h	2016-06-27 06:09:43.000000000 +0200
@@ -20,7 +20,7 @@
 } ;
 
 // Relationships represent references to other objects. They usually come in pairs, where the reference back is called the "inverse".
-NS_CLASS_AVAILABLE(10_4,3_0)
+API_AVAILABLE(macosx(10.4),ios(3.0))
 @interface NSRelationshipDescription : NSPropertyDescription {
 }
 
@@ -36,9 +36,9 @@
 @property (getter=isToMany, readonly) BOOL toMany;    // convenience method to test whether the relationship is to-one or to-many
 
 // Returns the version hash for the relationship.  This value includes the versionHash information from the NSPropertyDescription superclass, the name of the destination entity and the inverse relationship, and the min and max count.
-@property (readonly, copy) NSData *versionHash NS_AVAILABLE(10_5,3_0);
+@property (readonly, copy) NSData *versionHash API_AVAILABLE(macosx(10.5),ios(3.0));
 
-@property (getter=isOrdered) BOOL ordered NS_AVAILABLE(10_7,  5_0);
+@property (getter=isOrdered) BOOL ordered API_AVAILABLE(macosx(10.7),ios(5.0));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSSaveChangesRequest.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSSaveChangesRequest.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSSaveChangesRequest.h	2016-05-21 07:41:59.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/NSSaveChangesRequest.h	2016-06-27 06:09:43.000000000 +0200
@@ -14,7 +14,7 @@
 @class NSPersistentStoreRequest;
 @class NSManagedObject;
 
-NS_CLASS_AVAILABLE(10_7,5_0)
+API_AVAILABLE(macosx(10.7),ios(5.0))
 @interface NSSaveChangesRequest : NSPersistentStoreRequest {
 }
 

```