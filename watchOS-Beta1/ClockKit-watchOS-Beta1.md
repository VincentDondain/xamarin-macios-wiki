#ClockKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKComplicationDataSource.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKComplicationDataSource.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKComplicationDataSource.h	2015-08-18 08:44:15.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKComplicationDataSource.h	2016-06-01 05:52:25.000000000 +0200
@@ -11,6 +11,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 @class CLKComplication;
+@class CLKTextProvider;
 @class CLKComplicationTemplate;
 @class CLKComplicationTimelineEntry;
 
@@ -56,6 +57,9 @@
 
 #pragma mark Update Scheduling
 
+/// These methods will no longer be called for clients adopting the WKRefreshBackgroundTask APIs, which are the recommended means of scheduling updates.
+/// In a future release these methods will no longer be called.
+
 /// Return the date when you would next like to be given the opportunity to update your complication content.
 /// We will make an effort to launch you at or around that date, subject to power and budget limitations.
 @optional
@@ -72,13 +76,22 @@
 @optional
 - (void)requestedUpdateBudgetExhausted;
 
-#pragma mark - Placeholder Templates
 
-/// When your extension is installed, this method will be called once per supported complication, and the results will be cached.
+#pragma mark - Descriptions and Sample Templates
+
+/// These methods will be called once per supported complication when your extension is installed, and the results cached.
+
+/// Provide a localizable template (that is, a template populated with localizable text providers) showing sample data for this complication. The template
+/// should as much as possible reflect what your complication would normally look like, but the data should be fake.
 /// If you pass back nil, we will use the default placeholder template (which is a combination of your icon and app name).
-@required
+@optional
+- (void)getLocalizableSampleTemplateForComplication:(CLKComplication *)complication withHandler:(void(^)(CLKComplicationTemplate * __nullable complicationTemplate))handler;
+
+/// Deprecated.
+@optional
 - (void)getPlaceholderTemplateForComplication:(CLKComplication *)complication withHandler:(void(^)(CLKComplicationTemplate * __nullable complicationTemplate))handler;
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKComplicationTemplate.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKComplicationTemplate.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKComplicationTemplate.h	2015-08-18 08:44:15.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKComplicationTemplate.h	2016-06-01 05:52:09.000000000 +0200
@@ -98,12 +98,8 @@
 @property (nonatomic) CLKComplicationColumnAlignment column2Alignment;
 @end
 
-#pragma mark - Utilitarian Small
 
-@interface CLKComplicationTemplateUtilitarianSmallFlat : CLKComplicationTemplate
-@property (nonatomic, copy) CLKTextProvider *textProvider;
-@property (nonatomic, copy, nullable) CLKImageProvider *imageProvider;
-@end
+#pragma mark - Utilitarian Small
 
 @interface CLKComplicationTemplateUtilitarianSmallSquare : CLKComplicationTemplate
 @property (nonatomic, copy) CLKImageProvider *imageProvider;
@@ -122,6 +118,14 @@
 @end
 
 
+#pragma mark - Utilitarian Small  &  Utilitarian Small Flat
+
+@interface CLKComplicationTemplateUtilitarianSmallFlat : CLKComplicationTemplate
+@property (nonatomic, copy) CLKTextProvider *textProvider;
+@property (nonatomic, copy, nullable) CLKImageProvider *imageProvider;
+@end
+
+
 #pragma mark - Utilitarian Large
 
 @interface CLKComplicationTemplateUtilitarianLargeFlat : CLKComplicationTemplate
@@ -129,6 +133,7 @@
 @property (nonatomic, copy, nullable) CLKImageProvider *imageProvider;
 @end
 
+
 #pragma mark - Circular Small
 
 @interface CLKComplicationTemplateCircularSmallSimpleText : CLKComplicationTemplate
@@ -161,5 +166,48 @@
 @property (nonatomic, copy) CLKTextProvider  *line2TextProvider;
 @end
 
+#pragma mark - Extra Large
+
+@interface CLKComplicationTemplateExtraLargeSimpleText : CLKComplicationTemplate
+@property (nonatomic, copy) CLKTextProvider *textProvider;
+@end
+
+@interface CLKComplicationTemplateExtraLargeSimpleImage : CLKComplicationTemplate
+@property (nonatomic, copy) CLKImageProvider *imageProvider;
+@end
+
+@interface CLKComplicationTemplateExtraLargeRingText : CLKComplicationTemplate
+@property (nonatomic, copy) CLKTextProvider *textProvider;
+@property (nonatomic) float fillFraction;
+@property (nonatomic) CLKComplicationRingStyle ringStyle;
+@end
+
+@interface CLKComplicationTemplateExtraLargeRingImage : CLKComplicationTemplate
+@property (nonatomic, copy) CLKImageProvider *imageProvider;
+@property (nonatomic) float fillFraction;
+@property (nonatomic) CLKComplicationRingStyle ringStyle;
+@end
+
+@interface CLKComplicationTemplateExtraLargeStackText : CLKComplicationTemplate
+@property (nonatomic, copy) CLKTextProvider *line1TextProvider;
+@property (nonatomic, copy) CLKTextProvider *line2TextProvider;
+@property (nonatomic) BOOL highlightLine2;
+@end
+
+@interface CLKComplicationTemplateExtraLargeStackImage : CLKComplicationTemplate
+@property (nonatomic, copy) CLKImageProvider *line1ImageProvider;
+@property (nonatomic, copy) CLKTextProvider  *line2TextProvider;
+@property (nonatomic) BOOL highlightLine2;
+@end
+
+@interface CLKComplicationTemplateExtraLargeColumnsText : CLKComplicationTemplate
+@property (nonatomic, copy) CLKTextProvider *row1Column1TextProvider;
+@property (nonatomic, copy) CLKTextProvider *row1Column2TextProvider;
+@property (nonatomic, copy) CLKTextProvider *row2Column1TextProvider;
+@property (nonatomic, copy) CLKTextProvider *row2Column2TextProvider;
+@property (nonatomic) CLKComplicationColumnAlignment column2Alignment;
+@property (nonatomic) BOOL highlightColumn2;
+@end
+
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKDefines.h	2015-11-02 04:44:11.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKDefines.h	2016-06-01 05:52:25.000000000 +0200
@@ -11,11 +11,13 @@
 #define CLK_DEPRECATED_WATCHOS(_watchOSIntro, _watchOSDep, ...) __WATCHOS_DEPRECATED(_watchOSIntro, _watchOSDep, __VA_ARGS__)
 
 typedef NS_ENUM(NSInteger, CLKComplicationFamily) {
-    CLKComplicationFamilyModularSmall,
-    CLKComplicationFamilyModularLarge,
-    CLKComplicationFamilyUtilitarianSmall,
-    CLKComplicationFamilyUtilitarianLarge,
-    CLKComplicationFamilyCircularSmall,
+    CLKComplicationFamilyModularSmall                                                         = 0,
+    CLKComplicationFamilyModularLarge                                                         = 1,
+    CLKComplicationFamilyUtilitarianSmall                                                     = 2,
+    CLKComplicationFamilyUtilitarianSmallFlat   /* subset of UtilitarianSmall */              = 6,
+    CLKComplicationFamilyUtilitarianLarge                                                     = 3,
+    CLKComplicationFamilyCircularSmall                                                        = 4,
+    CLKComplicationFamilyExtraLarge                                                           = 7,
 };
 
 typedef NS_OPTIONS(NSUInteger, CLKComplicationTimeTravelDirections) {
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKTextProvider.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKTextProvider.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKTextProvider.h	2016-02-24 05:26:21.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/ClockKit.framework/Headers/CLKTextProvider.h	2016-06-01 05:52:25.000000000 +0200
@@ -163,4 +163,20 @@
 
 @end
 
+
+#pragma mark - Localizable
+
+@interface CLKTextProvider (Localizable)
+
+// Creates a localizable simple text provider with a strings file key for the text and (optionally) a strings file key for shorter fallback text.
++ (instancetype)localizableTextProviderWithStringsFileTextKey:(NSString *)textKey;
++ (instancetype)localizableTextProviderWithStringsFileTextKey:(NSString *)textKey shortTextKey:(NSString * __nullable)shortTextKey;
+
+// Creates a localizable text provider with a strings file key that resolves to a format, and text provider replacement arguments.
+// Since the replacement arguments must all be text providers, the only allowable format specifiers are %@ and variants. (Reordering specifiers like %1@ are supported.)
++ (instancetype)localizableTextProviderWithStringsFileFormatKey:(NSString *)formatKey textProviders:(NSArray<CLKTextProvider *> *)textProviders;
+
+@end
+
 NS_ASSUME_NONNULL_END
+

```