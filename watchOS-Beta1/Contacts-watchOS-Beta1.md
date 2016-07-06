#Contacts.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContact.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContact.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContact.h	2015-08-08 01:27:04.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContact.h	2016-05-21 08:07:36.000000000 +0200
@@ -79,7 +79,7 @@
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSData *imageData;
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSData *thumbnailImageData;
-@property (readonly, NS_NONATOMIC_IOSONLY) BOOL imageDataAvailable NS_AVAILABLE(NA, 9_0);
+@property (readonly, NS_NONATOMIC_IOSONLY) BOOL imageDataAvailable NS_AVAILABLE(10_12, 9_0);
 
 @property (readonly, copy, NS_NONATOMIC_IOSONLY) NSArray<CNLabeledValue<CNPhoneNumber*>*>             *phoneNumbers;
 @property (readonly, copy, NS_NONATOMIC_IOSONLY) NSArray<CNLabeledValue<NSString*>*>                  *emailAddresses;
@@ -153,7 +153,7 @@
 CONTACTS_EXTERN NSString * const CNContactNoteKey                            NS_AVAILABLE(10_11, 9_0);
 CONTACTS_EXTERN NSString * const CNContactImageDataKey                       NS_AVAILABLE(10_11, 9_0);
 CONTACTS_EXTERN NSString * const CNContactThumbnailImageDataKey              NS_AVAILABLE(10_11, 9_0);
-CONTACTS_EXTERN NSString * const CNContactImageDataAvailableKey              NS_AVAILABLE(NA, 9_0);
+CONTACTS_EXTERN NSString * const CNContactImageDataAvailableKey              NS_AVAILABLE(10_12, 9_0);
 CONTACTS_EXTERN NSString * const CNContactTypeKey                            NS_AVAILABLE(10_11, 9_0);
 CONTACTS_EXTERN NSString * const CNContactPhoneNumbersKey                    NS_AVAILABLE(10_11, 9_0);
 CONTACTS_EXTERN NSString * const CNContactEmailAddressesKey                  NS_AVAILABLE(10_11, 9_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContactFetchRequest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContactFetchRequest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContactFetchRequest.h	2015-08-08 01:27:04.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContactFetchRequest.h	2016-05-21 08:31:25.000000000 +0200
@@ -16,7 +16,7 @@
  * @discussion Used with [CNContactStore enumerateContactsWithFetchRequest:error:usingBlock:]. Can combine any of these options to create a contact fetch request.
  */
 NS_CLASS_AVAILABLE(10_11, 9_0)
-@interface CNContactFetchRequest : NSObject
+@interface CNContactFetchRequest : NSObject <NSSecureCoding>
 
 
 /*!
@@ -45,7 +45,7 @@
  *
  * @discussion If YES returns CNMutableContact objects, otherwise returns CNContact objects. Default is NO.
  */
-@property (NS_NONATOMIC_IOSONLY) BOOL mutableObjects;
+@property (NS_NONATOMIC_IOSONLY) BOOL mutableObjects NS_AVAILABLE(10_12, 10_0);
 
 /*!
  * @abstract To return linked contacts as unified contacts.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContactVCardSerialization.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContactVCardSerialization.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContactVCardSerialization.h	2015-08-08 01:27:04.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContactVCardSerialization.h	2016-05-21 08:31:25.000000000 +0200
@@ -10,6 +10,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 @protocol CNKeyDescriptor;
+@class CNContact;
 
 /*!
  * @abstract Contact vCard support.
@@ -27,8 +28,8 @@
  */
 + (id<CNKeyDescriptor>)descriptorForRequiredKeys;
 
-+ (nullable NSData *)dataWithContacts:(NSArray *)contacts error:(NSError *__nullable *__nullable)error;
-+ (nullable NSArray *)contactsWithData:(NSData *)data error:(NSError *__nullable *__nullable)error;
++ (nullable NSData *)dataWithContacts:(NSArray<CNContact *>*)contacts error:(NSError *__nullable *__nullable)error;
++ (nullable NSArray<CNContact *>*)contactsWithData:(NSData *)data error:(NSError *__nullable *__nullable)error;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContactsUserDefaults.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContactsUserDefaults.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContactsUserDefaults.h	2015-08-08 01:27:04.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContactsUserDefaults.h	2016-05-21 08:31:25.000000000 +0200
@@ -12,6 +12,8 @@
 
 /*!
  * @abstract The user defaults for contacts.
+ *
+ * @note This class is not thread safe.
  */
 NS_CLASS_AVAILABLE(10_11, 9_0)
 @interface CNContactsUserDefaults : NSObject
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNLabeledValue.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNLabeledValue.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNLabeledValue.h	2015-08-08 01:27:04.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNLabeledValue.h	2016-05-21 08:31:25.000000000 +0200
@@ -20,7 +20,7 @@
 /*! The identifier is unique among contacts on the device. It can be saved and used for finding labeled values next application launch. */
 @property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *identifier;
 
-@property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *label;
+@property (readonly, nullable, copy, NS_NONATOMIC_IOSONLY) NSString *label;
 @property (readonly, copy, NS_NONATOMIC_IOSONLY) ValueType value;
 
 /*! Returns a new CNLabeledValue with a new identifier. */

```