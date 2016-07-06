#AddressBook.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AddressBook.framework/Headers/ABAddressBook.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AddressBook.framework/Headers/ABAddressBook.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AddressBook.framework/Headers/ABAddressBook.h	2015-10-03 00:29:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AddressBook.framework/Headers/ABAddressBook.h	2016-05-14 16:53:32.000000000 +0200
@@ -10,9 +10,11 @@
 #define __ABAddressBook__
 
 #include <AddressBook/AddressBookDefines.h>
-#include <CoreFoundation/CoreFoundation.h>
 #include <AddressBook/ABRecord.h>
 
+#include <CoreFoundation/CoreFoundation.h>
+
+
 AB_EXTERN const CFStringRef ABAddressBookErrorDomain AB_DEPRECATED("use CNErrorDomain");
 
 enum {
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AddressBook.framework/Headers/AddressBook.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AddressBook.framework/Headers/AddressBook.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AddressBook.framework/Headers/AddressBook.h	2015-10-03 00:29:01.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/AddressBook.framework/Headers/AddressBook.h	2016-05-14 16:53:32.000000000 +0200
@@ -43,6 +43,7 @@
 #define __AddressBook__
 
 #include <AddressBook/ABAddressBook.h>
+#include <AddressBook/ABAddressBook.h>
 #include <AddressBook/ABRecord.h>
 #include <AddressBook/ABPerson.h>
 #include <AddressBook/ABGroup.h>

```