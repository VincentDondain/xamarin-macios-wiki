#Contacts.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContact.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContact.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContact.h	2016-05-21 08:07:36.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNContact.h	2016-06-27 01:48:49.000000000 +0200
@@ -67,14 +67,15 @@
 @property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *nameSuffix;
 @property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *nickname;
 
-@property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *phoneticGivenName;
-@property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *phoneticMiddleName;
-@property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *phoneticFamilyName;
-
 @property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *organizationName;
 @property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *departmentName;
 @property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *jobTitle;
 
+@property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *phoneticGivenName;
+@property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *phoneticMiddleName;
+@property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *phoneticFamilyName;
+@property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *phoneticOrganizationName NS_AVAILABLE(10_12, 10_0);
+
 @property (readonly, copy, NS_NONATOMIC_IOSONLY) NSString *note;
 
 @property (readonly, copy, nullable, NS_NONATOMIC_IOSONLY) NSData *imageData;
@@ -142,12 +143,13 @@
 CONTACTS_EXTERN NSString * const CNContactPreviousFamilyNameKey              NS_AVAILABLE(10_11, 9_0);
 CONTACTS_EXTERN NSString * const CNContactNameSuffixKey                      NS_AVAILABLE(10_11, 9_0);
 CONTACTS_EXTERN NSString * const CNContactNicknameKey                        NS_AVAILABLE(10_11, 9_0);
-CONTACTS_EXTERN NSString * const CNContactPhoneticGivenNameKey               NS_AVAILABLE(10_11, 9_0);
-CONTACTS_EXTERN NSString * const CNContactPhoneticMiddleNameKey              NS_AVAILABLE(10_11, 9_0);
-CONTACTS_EXTERN NSString * const CNContactPhoneticFamilyNameKey              NS_AVAILABLE(10_11, 9_0);
 CONTACTS_EXTERN NSString * const CNContactOrganizationNameKey                NS_AVAILABLE(10_11, 9_0);
 CONTACTS_EXTERN NSString * const CNContactDepartmentNameKey                  NS_AVAILABLE(10_11, 9_0);
 CONTACTS_EXTERN NSString * const CNContactJobTitleKey                        NS_AVAILABLE(10_11, 9_0);
+CONTACTS_EXTERN NSString * const CNContactPhoneticGivenNameKey               NS_AVAILABLE(10_11, 9_0);
+CONTACTS_EXTERN NSString * const CNContactPhoneticMiddleNameKey              NS_AVAILABLE(10_11, 9_0);
+CONTACTS_EXTERN NSString * const CNContactPhoneticFamilyNameKey              NS_AVAILABLE(10_11, 9_0);
+CONTACTS_EXTERN NSString * const CNContactPhoneticOrganizationNameKey        NS_AVAILABLE(10_12, 10_0);
 CONTACTS_EXTERN NSString * const CNContactBirthdayKey                        NS_AVAILABLE(10_11, 9_0);
 CONTACTS_EXTERN NSString * const CNContactNonGregorianBirthdayKey            NS_AVAILABLE(10_11, 9_0);
 CONTACTS_EXTERN NSString * const CNContactNoteKey                            NS_AVAILABLE(10_11, 9_0);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNMutableContact.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNMutableContact.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNMutableContact.h	2016-05-23 02:05:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Contacts.framework/Headers/CNMutableContact.h	2016-06-27 01:48:49.000000000 +0200
@@ -30,14 +30,15 @@
 @property (copy, NS_NONATOMIC_IOSONLY) NSString *nameSuffix;
 @property (copy, NS_NONATOMIC_IOSONLY) NSString *nickname;
 
-@property (copy, NS_NONATOMIC_IOSONLY) NSString *phoneticGivenName;
-@property (copy, NS_NONATOMIC_IOSONLY) NSString *phoneticMiddleName;
-@property (copy, NS_NONATOMIC_IOSONLY) NSString *phoneticFamilyName;
-
 @property (copy, NS_NONATOMIC_IOSONLY) NSString *organizationName;
 @property (copy, NS_NONATOMIC_IOSONLY) NSString *departmentName;
 @property (copy, NS_NONATOMIC_IOSONLY) NSString *jobTitle;
 
+@property (copy, NS_NONATOMIC_IOSONLY) NSString *phoneticGivenName;
+@property (copy, NS_NONATOMIC_IOSONLY) NSString *phoneticMiddleName;
+@property (copy, NS_NONATOMIC_IOSONLY) NSString *phoneticFamilyName;
+@property (copy, NS_NONATOMIC_IOSONLY) NSString *phoneticOrganizationName;
+
 @property (copy, NS_NONATOMIC_IOSONLY) NSString *note;
 
 @property (copy, nullable, NS_NONATOMIC_IOSONLY) NSData *imageData;

```