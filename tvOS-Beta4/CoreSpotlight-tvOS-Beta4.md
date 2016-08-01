#CoreSpotlight.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_Events.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_Events.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_Events.h	2016-07-09 03:08:29.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_Events.h	2016-07-22 23:27:50.000000000 +0200
@@ -25,6 +25,6 @@
 @property(nullable, copy) NSArray<NSDate *> *importantDates;
 
 //Whether this event covers complete days
-@property(nullable, copy) NSNumber *allDay;
+@property(nullable, strong) NSNumber *allDay;
 
 @end
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_General.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_General.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_General.h	2016-07-09 03:08:29.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_General.h	2016-07-22 23:27:50.000000000 +0200
@@ -65,17 +65,17 @@
 
 @interface CSSearchableItemAttributeSet (CSActionExtras)
 // If supportsPhoneCall is 1 and the item has the phoneNumbers property, then the phone number may be used to initiate phone calls. This should be used to indicate that using the phone number is appropriate, and a primary action for the user. For example, supportsPhoneCall would be set on a business, but not an academic paper that happens to have phone numbers for the authors or the institution.
-@property (nullable, copy) NSNumber *supportsPhoneCall;
+@property(nullable, strong) NSNumber *supportsPhoneCall;
 
 // If supportsNavigation is set to 1, and the item has the latitude and longitude properties set, then the latitude and longitude may be used for navigation. For example, supportsNavigation would be set on a restaurant review, but not on a photo.
-@property (nullable, copy) NSNumber *supportsNavigation;
+@property(nullable, strong) NSNumber *supportsNavigation;
 @end
 
 @interface CSSearchableItemAttributeSet(CSContainment)
 @property(nullable, copy) NSString *containerTitle;
 @property(nullable, copy) NSString *containerDisplayName;
 @property(nullable, copy) NSString *containerIdentifier;
-@property(nullable, copy) NSNumber *containerOrder;
+@property(nullable, strong) NSNumber *containerOrder;
 @end
 
 

```