#EventKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKCalendarItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKCalendarItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKCalendarItem.h	2015-08-14 08:31:10.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKCalendarItem.h	2016-05-20 09:07:14.000000000 +0200
@@ -64,7 +64,7 @@
 @property(nonatomic, copy, nullable) NSURL *URL NS_AVAILABLE(10_8, 5_0);
 
 @property(nonatomic, readonly, nullable) NSDate *lastModifiedDate;
-@property(nonatomic, readonly, nullable) NSDate *creationDate NS_AVAILABLE(10_8, 5_0);
+@property(nonatomic, readonly, nullable, strong) NSDate *creationDate NS_AVAILABLE(10_8, 5_0);
 @property(nonatomic, copy, nullable) NSTimeZone *timeZone  NS_AVAILABLE(10_8, 5_0);
 
 // These exist to do simple checks for the presence of data without
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKEvent.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKEvent.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKEvent.h	2015-08-14 08:31:10.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKEvent.h	2016-05-20 09:07:14.000000000 +0200
@@ -182,7 +182,7 @@
 /*!
     @property   birthdayPersonUniqueID
     @abstract   Specifies the address book unique ID of the person this event was created for.
-    @disussion  This property is only valid for events in the built-in Birthdays calendar. It specifies
+    @discussion This property is only valid for events in the built-in Birthdays calendar. It specifies
                 the Address Book unique ID of the person this event was created for. For any other type of event,
                 this property returns nil.
  */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKEventStore.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKEventStore.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKEventStore.h	2015-08-14 08:31:10.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKEventStore.h	2016-05-28 06:17:18.000000000 +0200
@@ -324,7 +324,7 @@
     @discussion Creates a simple query predicate to search for events within a certain date range. At present,
                 this will return events in the default time zone ([NSTimeZone defaultTimeZone]).
 
-                OS X Only: For performance reasons, this method will only return events within a four year timespan.
+                For performance reasons, this method will only return events within a four year timespan.
                 If the date range between the startDate and endDate is greater than four years, then it will be shortened 
                 to the first four years.
  
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKRecurrenceRule.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKRecurrenceRule.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKRecurrenceRule.h	2015-08-14 08:31:10.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EKRecurrenceRule.h	2016-05-20 09:07:14.000000000 +0200
@@ -79,7 +79,7 @@
 
 /*!
     @property       calendarIdentifier;
-    @description    Calendar used by this recurrence rule.
+    @discussion     Calendar used by this recurrence rule.
 */
 @property(nonatomic, readonly) NSString *calendarIdentifier;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EventKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EventKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EventKit.h	2015-08-14 08:31:10.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/EventKit.framework/Headers/EventKit.h	2016-05-21 08:32:47.000000000 +0200
@@ -6,6 +6,9 @@
  *
  */
 
+#import <TargetConditionals.h>
+#import <Availability.h>
+
 #if __IPHONE_4_0 <= __IPHONE_OS_VERSION_MAX_ALLOWED || !TARGET_OS_IPHONE
 
 #import <EventKit/EventKitDefines.h>

```