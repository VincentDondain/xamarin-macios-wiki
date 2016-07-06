#AddressBook.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AddressBook.framework/Headers/ABAddressBook.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AddressBook.framework/Headers/ABAddressBook.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AddressBook.framework/Headers/ABAddressBook.h	2015-08-27 06:12:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AddressBook.framework/Headers/ABAddressBook.h	2016-06-03 02:58:17.000000000 +0200
@@ -52,8 +52,8 @@
 @private
     id                   _reserved8;
     
-    void                *_reserved2 __unused;
-    void                *_reserved3 __unused;
+    void                *_reserved2;
+    void                *_reserved3;
     id                   _reserved4;
     NSMutableDictionary *_tableSchemas;
     NSMutableDictionary *_reserved5 __unused;
@@ -63,7 +63,7 @@
 
     id                   _reserved1;
 	
-    void                *_reserved6 __unused;
+    void                *_reserved6;
     void                *_reserved7 __unused;
 
     struct __ABBookflags {
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AddressBook.framework/Headers/ABGlobals.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AddressBook.framework/Headers/ABGlobals.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/AddressBook.framework/Headers/ABGlobals.h	2015-08-27 06:12:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AddressBook.framework/Headers/ABGlobals.h	2016-06-03 02:58:17.000000000 +0200
@@ -37,6 +37,8 @@
 extern NSString * const kABAlternateBirthdayComponentsProperty; //Alternate non-Gregorian birth date - kABDateComponentsProperty
 
 extern NSString * const kABOrganizationProperty;          // Company name - kABStringProperty
+extern NSString * const kABOrganizationPhoneticProperty;   // Company name phonetic - kABStringProperty
+
 
 extern NSString * const kABJobTitleProperty;              // Job Title - kABStringProperty
 

```