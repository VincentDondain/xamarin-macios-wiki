#UIKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSFileProviderExtension.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSFileProviderExtension.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSFileProviderExtension.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSFileProviderExtension.h	2016-06-29 06:52:45.000000000 +0200
@@ -20,10 +20,18 @@
 // When modifying the files stored in the directory returned by documentStorageURL, you should pass this identifier
 // to your file coordinator's setPurposeIdentifier: method.
 // By default, this returns the bundle identifier of the application containing your extension. You need to make sure to use the same identifier in your containing app.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) NSString *providerIdentifier;
+#else
 - (NSString *)providerIdentifier;
+#endif
 
 // The root URL for provided documents. This URL must be writable from your app extension, and must only be used for the extension's files or their placeholders.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) NSURL *documentStorageURL;
+#else
 - (NSURL *)documentStorageURL;
+#endif
 
 // You may want to override these.
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutManager.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutManager.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutManager.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSLayoutManager.h	2016-06-27 06:29:56.000000000 +0200
@@ -192,8 +192,14 @@
 
 // Returns (by reference for the "get" method) the character index or glyph index or both of the first unlaid character/glyph in the layout manager at this time.
 - (void)getFirstUnlaidCharacterIndex:(nullable NSUInteger *)charIndex glyphIndex:(nullable NSUInteger *)glyphIndex;
+
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) NSUInteger firstUnlaidCharacterIndex;
+@property(nonatomic, readonly) NSUInteger firstUnlaidGlyphIndex;
+#else
 - (NSUInteger)firstUnlaidCharacterIndex;
 - (NSUInteger)firstUnlaidGlyphIndex;
+#endif
 
 // Returns the container in which the given glyph is laid and (optionally) by reference the whole range of glyphs that are in that container.  This will cause glyph generation and layout for the line fragment containing the specified glyph, or if non-contiguous layout is not enabled, up to and including that line fragment; if non-contiguous layout is not enabled and effectiveGlyphRange is non-NULL, this will additionally cause glyph generation and layout for the entire text container containing the specified glyph.
 - (nullable NSTextContainer *)textContainerForGlyphAtIndex:(NSUInteger)glyphIndex effectiveRange:(nullable NSRangePointer)effectiveGlyphRange;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h	2016-06-03 06:16:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSParagraphStyle.h	2016-06-27 07:03:36.000000000 +0200
@@ -43,7 +43,11 @@
 
 NS_CLASS_AVAILABLE(10_0, 6_0) @interface NSParagraphStyle : NSObject <NSCopying, NSMutableCopying, NSSecureCoding>
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) NSParagraphStyle *defaultParagraphStyle; // This class method returns a shared and cached NSParagraphStyle instance with the default style settings, with same value as the result of [[NSParagraphStyle alloc] init].
+#else
 + (NSParagraphStyle *)defaultParagraphStyle; // This class method returns a shared and cached NSParagraphStyle instance with the default style settings, with same value as the result of [[NSParagraphStyle alloc] init].
+#endif
 
 + (NSWritingDirection)defaultWritingDirectionForLanguage:(nullable NSString *)languageName;  // languageName is in ISO lang region format
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h	2016-05-23 08:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIAccessibility.h	2016-06-27 06:29:57.000000000 +0200
@@ -409,7 +409,8 @@
 UIKIT_EXTERN BOOL UIAccessibilityIsShakeToUndoEnabled(void) NS_AVAILABLE_IOS(9_0);
 UIKIT_EXTERN NSString *const UIAccessibilityShakeToUndoDidChangeNotification NS_AVAILABLE_IOS(9_0);
 
-// Returns whether the system preference for AssistiveTouch is enabled
+// Returns whether the system preference for AssistiveTouch is enabled.
+// This always returns false if Guided Access is not enabled.
 UIKIT_EXTERN BOOL UIAccessibilityIsAssistiveTouchRunning(void) NS_AVAILABLE_IOS(10_0);
 UIKIT_EXTERN NSString *const UIAccessibilityAssistiveTouchStatusDidChangeNotification NS_AVAILABLE_IOS(10_0);
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivity.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivity.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivity.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivity.h	2016-06-29 06:52:46.000000000 +0200
@@ -36,17 +36,30 @@
 NS_CLASS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED @interface UIActivity : NSObject
 
 // override methods
-
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) UIActivityCategory activityCategory NS_AVAILABLE_IOS(7_0); // default is UIActivityCategoryAction.
+#else
 + (UIActivityCategory)activityCategory NS_AVAILABLE_IOS(7_0); // default is UIActivityCategoryAction.
+#endif
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, nullable) NSString *activityType;       // default returns nil. subclass may override to return custom activity type that is reported to completion handler
+@property(nonatomic, readonly, nullable) NSString *activityTitle;      // default returns nil. subclass must override and must return non-nil value
+@property(nonatomic, readonly, nullable) UIImage *activityImage;       // default returns nil. subclass must override and must return non-nil value
+#else
 - (nullable NSString *)activityType;       // default returns nil. subclass may override to return custom activity type that is reported to completion handler
 - (nullable NSString *)activityTitle;      // default returns nil. subclass must override and must return non-nil value
 - (nullable UIImage *)activityImage;       // default returns nil. subclass must override and must return non-nil value
+#endif
 
 - (BOOL)canPerformWithActivityItems:(NSArray *)activityItems;   // override this to return availability of activity based on items. default returns NO
 - (void)prepareWithActivityItems:(NSArray *)activityItems;      // override to extract items and set up your HI. default does nothing
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, nullable) UIViewController *activityViewController;   // return non-nil to have view controller presented modally. call activityDidFinish at end. default returns nil
+#else
 - (nullable UIViewController *)activityViewController;   // return non-nil to have view controller presented modally. call activityDidFinish at end. default returns nil
+#endif
 - (void)performActivity;                        // if no view controller, this method is called. call activityDidFinish when done. default calls [self activityDidFinish:NO]
 
 // state method
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityIndicatorView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityIndicatorView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityIndicatorView.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityIndicatorView.h	2016-06-29 06:52:45.000000000 +0200
@@ -29,7 +29,11 @@
 
 - (void)startAnimating;
 - (void)stopAnimating;
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, getter=isAnimating) BOOL animating;
+#else
 - (BOOL)isAnimating;
+#endif
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityItemProvider.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityItemProvider.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityItemProvider.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityItemProvider.h	2016-06-29 06:52:46.000000000 +0200
@@ -35,7 +35,11 @@
 @property(nullable,nonatomic,strong,readonly) id        placeholderItem;
 @property(nullable,nonatomic,copy,readonly)   NSString *activityType;     // activity type available when -item is called. nil at other times. use this in your -item method to customize the data to return
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonnull, nonatomic, readonly) id item;   // called on secondary thread when user selects an activity. you must subclass and return a non-nil value. The item can use the UIActivityItemSource protocol to return extra information
+#else
 - (nonnull id)item;   // called on secondary thread when user selects an activity. you must subclass and return a non-nil value. The item can use the UIActivityItemSource protocol to return extra information
+#endif
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h	2016-06-27 06:32:24.000000000 +0200
@@ -103,13 +103,21 @@
 
 NS_CLASS_AVAILABLE_IOS(2_0) @interface UIApplication : UIResponder
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) UIApplication *sharedApplication NS_EXTENSION_UNAVAILABLE_IOS("Use view controller based solutions where appropriate instead.");
+#else
 + (UIApplication *)sharedApplication NS_EXTENSION_UNAVAILABLE_IOS("Use view controller based solutions where appropriate instead.");
+#endif
 
 @property(nullable, nonatomic, assign) id<UIApplicationDelegate> delegate;
 
 - (void)beginIgnoringInteractionEvents NS_EXTENSION_UNAVAILABLE_IOS("");               // nested. set should be set during animations & transitions to ignore touch and other events
 - (void)endIgnoringInteractionEvents NS_EXTENSION_UNAVAILABLE_IOS("");
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, getter=isIgnoringInteractionEvents) BOOL ignoringInteractionEvents;                  // returns YES if we are at least one deep in ignoring events
+#else
 - (BOOL)isIgnoringInteractionEvents;                  // returns YES if we are at least one deep in ignoring events
+#endif
 
 @property(nonatomic,getter=isIdleTimerDisabled)       BOOL idleTimerDisabled;	  // default is NO
 
@@ -192,7 +200,11 @@
 - (void)unregisterForRemoteNotifications NS_AVAILABLE_IOS(3_0);
 
 // Returns YES if the application is currently registered for remote notifications, taking into account any systemwide settings; doesn't relate to connectivity.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, getter=isRegisteredForRemoteNotifications) BOOL registeredForRemoteNotifications NS_AVAILABLE_IOS(8_0);
+#else
 - (BOOL)isRegisteredForRemoteNotifications NS_AVAILABLE_IOS(8_0);
+#endif
 
 - (void)registerForRemoteNotificationTypes:(UIRemoteNotificationType)types NS_DEPRECATED_IOS(3_0, 8_0, "Use -[UIApplication registerForRemoteNotifications] and UserNotifications Framework's -[UNUserNotificationCenter requestAuthorizationWithOptions:completionHandler:]") __TVOS_PROHIBITED;
 
@@ -221,7 +233,11 @@
 - (void)registerUserNotificationSettings:(UIUserNotificationSettings *)notificationSettings NS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED;
 
 // Returns the enabled user notification settings, also taking into account any systemwide settings.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, nullable) UIUserNotificationSettings *currentUserNotificationSettings NS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED;
+#else
 - (nullable UIUserNotificationSettings *)currentUserNotificationSettings NS_AVAILABLE_IOS(8_0) __TVOS_PROHIBITED;
+#endif
 
 @end
 
@@ -482,6 +498,6 @@
 
 // Option for openURL:options:CompletionHandler: only open URL if it is a valid universal link with an application configured to open it
 // If there is no application configured, or the user disabled using it to open the link, completion handler called with NO
-UIKIT_EXTERN NSString *const UIApplicationOpenURLOptionUniversalLinksOnly;
+UIKIT_EXTERN NSString *const UIApplicationOpenURLOptionUniversalLinksOnly NS_AVAILABLE_IOS(10_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIButton.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIButton.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIButton.h	2016-05-04 00:21:25.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIButton.h	2016-06-27 06:29:57.000000000 +0200
@@ -31,7 +31,7 @@
 
 + (instancetype)buttonWithType:(UIButtonType)buttonType;
 
-@property(nonatomic)          UIEdgeInsets contentEdgeInsets UI_APPEARANCE_SELECTOR; // default is UIEdgeInsetsZero
+@property(nonatomic)          UIEdgeInsets contentEdgeInsets UI_APPEARANCE_SELECTOR; // default is UIEdgeInsetsZero. On tvOS, detault is nonzero except for custom buttons on tvOS 10 or later.
 @property(nonatomic)          UIEdgeInsets titleEdgeInsets;                // default is UIEdgeInsetsZero
 @property(nonatomic)          BOOL         reversesTitleShadowWhenHighlighted; // default is NO. if YES, shadow reverses to shift between engrave and emboss appearance
 @property(nonatomic)          UIEdgeInsets imageEdgeInsets;                // default is UIEdgeInsetsZero
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionView.h	2016-06-03 05:02:20.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionView.h	2016-06-29 06:52:46.000000000 +0200
@@ -155,7 +155,11 @@
 @property (nonatomic) BOOL allowsSelection; // default is YES
 @property (nonatomic) BOOL allowsMultipleSelection; // default is NO
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property (nonatomic, readonly, nullable) NSArray<NSIndexPath *> *indexPathsForSelectedItems; // returns nil or an array of selected index paths
+#else
 - (nullable NSArray<NSIndexPath *> *)indexPathsForSelectedItems; // returns nil or an array of selected index paths
+#endif
 - (void)selectItemAtIndexPath:(nullable NSIndexPath *)indexPath animated:(BOOL)animated scrollPosition:(UICollectionViewScrollPosition)scrollPosition;
 - (void)deselectItemAtIndexPath:(NSIndexPath *)indexPath animated:(BOOL)animated;
 
@@ -170,7 +174,11 @@
 
 // Information about the current state of the collection view.
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property (nonatomic, readonly) NSInteger numberOfSections;
+#else
 - (NSInteger)numberOfSections;
+#endif
 - (NSInteger)numberOfItemsInSection:(NSInteger)section;
 
 - (nullable UICollectionViewLayoutAttributes *)layoutAttributesForItemAtIndexPath:(NSIndexPath *)indexPath;
@@ -180,8 +188,13 @@
 - (nullable NSIndexPath *)indexPathForCell:(UICollectionViewCell *)cell;
 
 - (nullable UICollectionViewCell *)cellForItemAtIndexPath:(NSIndexPath *)indexPath;
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property (nonatomic, readonly) NSArray<__kindof UICollectionViewCell *> *visibleCells;
+@property (nonatomic, readonly) NSArray<NSIndexPath *> *indexPathsForVisibleItems;
+#else
 - (NSArray<__kindof UICollectionViewCell *> *)visibleCells;
 - (NSArray<NSIndexPath *> *)indexPathsForVisibleItems;
+#endif
 
 - (nullable UICollectionReusableView *)supplementaryViewForElementKind:(NSString *)elementKind atIndexPath:(NSIndexPath *)indexPath NS_AVAILABLE_IOS(9_0);
 - (NSArray<UICollectionReusableView *> *)visibleSupplementaryViewsOfKind:(NSString *)elementKind NS_AVAILABLE_IOS(9_0);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewLayout.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewLayout.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewLayout.h	2016-05-04 00:21:21.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICollectionViewLayout.h	2016-06-29 06:52:46.000000000 +0200
@@ -108,8 +108,13 @@
 
 @interface UICollectionViewLayout (UISubclassingHooks)
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) Class layoutAttributesClass; // override this method to provide a custom class to be used when instantiating instances of UICollectionViewLayoutAttributes
+@property(class, nonatomic, readonly) Class invalidationContextClass NS_AVAILABLE_IOS(7_0); // override this method to provide a custom class to be used for invalidation contexts
+#else
 + (Class)layoutAttributesClass; // override this method to provide a custom class to be used when instantiating instances of UICollectionViewLayoutAttributes
 + (Class)invalidationContextClass NS_AVAILABLE_IOS(7_0); // override this method to provide a custom class to be used for invalidation contexts
+#endif
 
 // The collection view calls -prepareLayout once at its first layout as the first message to the layout instance.
 // The collection view calls -prepareLayout again after layout is invalidated and before requerying the layout information.
@@ -134,7 +139,11 @@
 - (CGPoint)targetContentOffsetForProposedContentOffset:(CGPoint)proposedContentOffset withScrollingVelocity:(CGPoint)velocity; // return a point at which to rest after scrolling - for layouts that want snap-to-point scrolling behavior
 - (CGPoint)targetContentOffsetForProposedContentOffset:(CGPoint)proposedContentOffset NS_AVAILABLE_IOS(7_0); // a layout can return the content offset to be applied during transition or update animations
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) CGSize collectionViewContentSize; // Subclasses must override this method and use it to return the width and height of the collection view’s content. These values represent the width and height of all the content, not just the content that is currently visible. The collection view uses this information to configure its own content size to facilitate scrolling.
+#else
 - (CGSize)collectionViewContentSize; // Subclasses must override this method and use it to return the width and height of the collection view’s content. These values represent the width and height of all the content, not just the content that is currently visible. The collection view uses this information to configure its own content size to facilitate scrolling.
+#endif
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h	2016-05-23 08:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIColor.h	2016-06-29 06:37:32.000000000 +0200
@@ -42,7 +42,24 @@
 
 // Some convenience methods to create colors.  These colors will be as calibrated as possible.
 // These colors are cached.
-+ (UIColor *)blackColor;      // 0.0 white 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) UIColor *blackColor;      // 0.0 white
+@property(class, nonatomic, readonly) UIColor *darkGrayColor;   // 0.333 white
+@property(class, nonatomic, readonly) UIColor *lightGrayColor;  // 0.667 white
+@property(class, nonatomic, readonly) UIColor *whiteColor;      // 1.0 white
+@property(class, nonatomic, readonly) UIColor *grayColor;       // 0.5 white
+@property(class, nonatomic, readonly) UIColor *redColor;        // 1.0, 0.0, 0.0 RGB
+@property(class, nonatomic, readonly) UIColor *greenColor;      // 0.0, 1.0, 0.0 RGB
+@property(class, nonatomic, readonly) UIColor *blueColor;       // 0.0, 0.0, 1.0 RGB
+@property(class, nonatomic, readonly) UIColor *cyanColor;       // 0.0, 1.0, 1.0 RGB
+@property(class, nonatomic, readonly) UIColor *yellowColor;     // 1.0, 1.0, 0.0 RGB
+@property(class, nonatomic, readonly) UIColor *magentaColor;    // 1.0, 0.0, 1.0 RGB
+@property(class, nonatomic, readonly) UIColor *orangeColor;     // 1.0, 0.5, 0.0 RGB
+@property(class, nonatomic, readonly) UIColor *purpleColor;     // 0.5, 0.0, 0.5 RGB
+@property(class, nonatomic, readonly) UIColor *brownColor;      // 0.6, 0.4, 0.2 RGB
+@property(class, nonatomic, readonly) UIColor *clearColor;      // 0.0 white, 0.0 alpha
+#else
++ (UIColor *)blackColor;      // 0.0 white
 + (UIColor *)darkGrayColor;   // 0.333 white 
 + (UIColor *)lightGrayColor;  // 0.667 white 
 + (UIColor *)whiteColor;      // 1.0 white 
@@ -57,6 +74,7 @@
 + (UIColor *)purpleColor;     // 0.5, 0.0, 0.5 RGB 
 + (UIColor *)brownColor;      // 0.6, 0.4, 0.2 RGB 
 + (UIColor *)clearColor;      // 0.0 white, 0.0 alpha 
+#endif
 
 // Set the color: Sets the fill and stroke colors in the current drawing context. Should be implemented by subclassers.
 - (void)set;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIControl.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIControl.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIControl.h	2016-05-04 00:21:21.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIControl.h	2016-06-27 06:32:24.000000000 +0200
@@ -93,8 +93,14 @@
 - (void)removeTarget:(nullable id)target action:(nullable SEL)action forControlEvents:(UIControlEvents)controlEvents;
 
 // get info about target & actions. this makes it possible to enumerate all target/actions by checking for each event kind
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic,readonly) NSSet *allTargets;
+@property(nonatomic,readonly) UIControlEvents allControlEvents;                            // list of all events that have at least one action
+#else
 - (NSSet *)allTargets;                                                                     // set may include NSNull to indicate at least one nil target
 - (UIControlEvents)allControlEvents;                                                       // list of all events that have at least one action
+#endif
+
 - (nullable NSArray<NSString *> *)actionsForTarget:(nullable id)target forControlEvent:(UIControlEvents)controlEvent;    // single event. returns NSArray of NSString selector names. returns nil if none
 
 // send the action. the first method is called for the event and is a point at which you can observe or override behavior. it is called repeately by the second.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDevice.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDevice.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDevice.h	2016-05-04 00:21:25.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDevice.h	2016-06-27 06:29:56.000000000 +0200
@@ -45,7 +45,11 @@
 
 NS_CLASS_AVAILABLE_IOS(2_0) @interface UIDevice : NSObject 
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) UIDevice *currentDevice;
+#else
 + (UIDevice *)currentDevice;
+#endif
 
 @property(nonatomic,readonly,strong) NSString    *name;              // e.g. "My iPhone"
 @property(nonatomic,readonly,strong) NSString    *model;             // e.g. @"iPhone", @"iPod touch"
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h	2016-06-03 05:02:20.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h	2016-06-29 06:37:33.000000000 +0200
@@ -92,7 +92,11 @@
 
 // Subclasses should generally not need to override this. Instead they should use the undoManager or call -updateChangeCount: every time they get a change and UIKit will calculate -hasUnsavedChanges automatically.
 // The default implementation of -autosaveWithCompletionHandler: initiates a save if [self hasUnsavedChanges] is YES.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) BOOL hasUnsavedChanges __TVOS_PROHIBITED;
+#else
 - (BOOL)hasUnsavedChanges __TVOS_PROHIBITED;
+#endif
 
 // Record the fact that a change affecting the value returned by -hasUnsavedChanges has occurred. Subclasses should not need to call this if they set the undoManager.
 - (void)updateChangeCount:(UIDocumentChangeKind)change __TVOS_PROHIBITED;
@@ -115,7 +119,11 @@
 // The default implementation of this method invokes [self hasUnsavedChanges] and, if that returns YES, invokes [self saveToURL:[self fileURL] forSaveOperation:UIDocumentSaveForOverwriting completionHandler:completionHandler].
 - (void)autosaveWithCompletionHandler:(void (^ __nullable)(BOOL success))completionHandler __TVOS_PROHIBITED;
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, nullable) NSString *savingFileType __TVOS_PROHIBITED; // The default implementation returns the current file type. saveToURL: will save to an extension based on this type so subclasses can override this to allow moving the document to a new type.
+#else
 - (nullable NSString *)savingFileType __TVOS_PROHIBITED; // The default implementation returns the current file type. saveToURL: will save to an extension based on this type so subclasses can override this to allow moving the document to a new type.
+#endif
 - (NSString *)fileNameExtensionForType:(nullable NSString *)typeName saveOperation:(UIDocumentSaveOperation)saveOperation __TVOS_PROHIBITED; // For a specified type, and a particular kind of save operation, return a file name extension that can be appended to a base file name.
 
 // This method is responsible for doing document writing in a way that minimizes the danger of leaving the disk to which writing is being done in an inconsistent state in the event of an application crash, system crash, hardware failure, power outage, etc.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDynamicAnimator.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDynamicAnimator.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDynamicAnimator.h	2016-06-03 05:02:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDynamicAnimator.h	2016-06-29 06:52:46.000000000 +0200
@@ -41,7 +41,11 @@
 - (void)updateItemUsingCurrentState:(id <UIDynamicItem>)item;
 
 @property (nonatomic, readonly, getter = isRunning) BOOL running;
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property (nonatomic, readonly) NSTimeInterval elapsedTime;
+#else
 - (NSTimeInterval)elapsedTime;
+#endif
 
 @property (nullable, nonatomic, weak) id <UIDynamicAnimatorDelegate> delegate;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIEvent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIEvent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIEvent.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIEvent.h	2016-06-29 06:52:45.000000000 +0200
@@ -48,7 +48,11 @@
 
 @property(nonatomic,readonly) NSTimeInterval  timestamp;
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, nullable) NSSet <UITouch *> *allTouches;
+#else
 - (nullable NSSet <UITouch *> *)allTouches;
+#endif
 - (nullable NSSet <UITouch *> *)touchesForWindow:(UIWindow *)window;
 - (nullable NSSet <UITouch *> *)touchesForView:(UIView *)view;
 - (nullable NSSet <UITouch *> *)touchesForGestureRecognizer:(UIGestureRecognizer *)gesture NS_AVAILABLE_IOS(3_2);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocus.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocus.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocus.h	2016-06-03 06:16:42.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFocus.h	2016-06-27 06:32:25.000000000 +0200
@@ -57,7 +57,11 @@
 
 /// Indicates whether or not this item is currently allowed to become focused.
 /// Returning NO restricts the item from being focusable, even if it is visible in the user interface. For example, UIControls return NO if they are disabled.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) BOOL canBecomeFocused;
+#else
 - (BOOL)canBecomeFocused;
+#endif
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2016-06-29 06:52:45.000000000 +0200
@@ -25,7 +25,11 @@
 + (nullable UIFont *)fontWithName:(NSString *)fontName size:(CGFloat)fontSize;
 
 // Returns an array of font family names for all installed fonts
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) NSArray<NSString *> *familyNames;
+#else
 + (NSArray<NSString *> *)familyNames;
+#endif
 
 // Returns an array of font names for the specified family name
 + (NSArray<NSString *> *)fontNamesForFamilyName:(NSString *)familyName;
@@ -63,7 +67,11 @@
 + (UIFont *)fontWithDescriptor:(UIFontDescriptor *)descriptor size:(CGFloat)pointSize NS_AVAILABLE_IOS(7_0);
 
 // Returns a font descriptor which describes the font.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) UIFontDescriptor *fontDescriptor NS_AVAILABLE_IOS(7_0);
+#else
 - (UIFontDescriptor *)fontDescriptor NS_AVAILABLE_IOS(7_0);
+#endif
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2016-06-03 06:16:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2016-06-27 06:29:56.000000000 +0200
@@ -62,7 +62,11 @@
 
 - (nullable id)objectForKey:(NSString *)anAttribute;
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) NSDictionary<NSString *, id> *fontAttributes;
+#else
 - (NSDictionary<NSString *, id> *)fontAttributes;
+#endif
 
 // Instance conversion
 // Returns "normalized" font descriptors matching the receiver. mandatoryKeys is an NSSet instance containing keys that are required to be identical in order to be matched. mandatoryKeys can be nil.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGeometry.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGeometry.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGeometry.h	2016-05-23 07:49:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGeometry.h	2016-06-27 07:06:58.000000000 +0200
@@ -55,8 +55,13 @@
     return offset1.horizontal == offset2.horizontal && offset1.vertical == offset2.vertical;
 }
 
+#if UIKIT_REMOVE_ZERO_FROM_SWIFT
+UIKIT_EXTERN const UIEdgeInsets UIEdgeInsetsZero NS_SWIFT_UNAVAILABLE("Use UIEdgeInsets.zero instead");
+UIKIT_EXTERN const UIOffset UIOffsetZero NS_SWIFT_UNAVAILABLE("Use UIOffset.zero instead");
+#else
 UIKIT_EXTERN const UIEdgeInsets UIEdgeInsetsZero;
 UIKIT_EXTERN const UIOffset UIOffsetZero;
+#endif
 
 UIKIT_EXTERN NSString *NSStringFromCGPoint(CGPoint point);
 UIKIT_EXTERN NSString *NSStringFromCGVector(CGVector vector);
@@ -84,6 +89,15 @@
 + (NSValue *)valueWithUIEdgeInsets:(UIEdgeInsets)insets;
 + (NSValue *)valueWithUIOffset:(UIOffset)insets NS_AVAILABLE_IOS(5_0);
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) CGPoint CGPointValue;
+@property(nonatomic, readonly) CGVector CGVectorValue;
+@property(nonatomic, readonly) CGSize CGSizeValue;
+@property(nonatomic, readonly) CGRect CGRectValue;
+@property(nonatomic, readonly) CGAffineTransform CGAffineTransformValue;
+@property(nonatomic, readonly) UIEdgeInsets UIEdgeInsetsValue;
+@property(nonatomic, readonly) UIOffset UIOffsetValue NS_AVAILABLE_IOS(5_0);
+#else
 - (CGPoint)CGPointValue;
 - (CGVector)CGVectorValue;
 - (CGSize)CGSizeValue;
@@ -91,6 +105,7 @@
 - (CGAffineTransform)CGAffineTransformValue;
 - (UIEdgeInsets)UIEdgeInsetsValue;
 - (UIOffset)UIOffsetValue NS_AVAILABLE_IOS(5_0);
+#endif
 
 @end
     
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h	2016-06-29 06:52:45.000000000 +0200
@@ -67,7 +67,11 @@
 // individual UIGestureRecognizer subclasses may provide subclass-specific location information. see individual subclasses for details
 - (CGPoint)locationInView:(nullable UIView*)view;                                // a generic single-point location for the gesture. usually the centroid of the touches involved
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) NSUInteger numberOfTouches;                                          // number of touches involved for which locations can be queried
+#else
 - (NSUInteger)numberOfTouches;                                          // number of touches involved for which locations can be queried
+#endif
 - (CGPoint)locationOfTouch:(NSUInteger)touchIndex inView:(nullable UIView*)view; // the location of a particular touch
 
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGuidedAccessRestrictions.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGuidedAccessRestrictions.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGuidedAccessRestrictions.h	2016-06-03 05:02:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGuidedAccessRestrictions.h	2016-06-29 06:52:46.000000000 +0200
@@ -45,7 +45,11 @@
  Each restriction identifier must be unique string.
  For example: com.MyCompany.MyApp.SomeRestrictionIdentifier
  */
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, nullable) NSArray<NSString *> *guidedAccessRestrictionIdentifiers;
+#else
 - (nullable NSArray<NSString *> *)guidedAccessRestrictionIdentifiers;
+#endif
 
 // Called each time the restriction associated with the identifier changes state.
 - (void)guidedAccessRestrictionWithIdentifier:(NSString *)restrictionIdentifier didChangeState:(UIGuidedAccessRestrictionState)newRestrictionState;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h	2016-05-23 08:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImage.h	2016-06-27 07:06:58.000000000 +0200
@@ -137,9 +137,14 @@
 @property (nullable, nonatomic, readonly) UIImageAsset *imageAsset NS_AVAILABLE_IOS(8_0); // The asset is not encoded along with the image. Returns nil if the image is not CGImage based.
 #endif
 
+// Creates a version of this image that, when assigned to a UIImageView’s image property, draws its underlying image contents horizontally mirrored when running under a right-to-left language. Affects the flipsForRightToLeftLayoutDirection property; does not affect the imageOrientation property.
+// This method cannot be used to create a left-to-right version of a right-to-left source image, and will be deprecated in a future release. New code should instead use -imageWithHorizontallyFlippedOrientation to construct a UIImageAsset.
 - (UIImage *)imageFlippedForRightToLeftLayoutDirection NS_AVAILABLE_IOS(9_0);
 @property (nonatomic, readonly) BOOL flipsForRightToLeftLayoutDirection NS_AVAILABLE_IOS(9_0);
 
+// Creates a version of this image with an imageOrientation property that is horizontally mirrored from this image’s. Does not affect the flipsForRightToLeftLayoutDirection property.
+- (UIImage *)imageWithHorizontallyFlippedOrientation NS_AVAILABLE_IOS(10_0);
+
 @end
 
 @interface UIImage(UIImageDeprecated)
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageView.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIImageView.h	2016-06-29 06:52:45.000000000 +0200
@@ -38,7 +38,11 @@
 
 - (void)startAnimating;
 - (void)stopAnimating;
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, getter=isAnimating) BOOL animating;
+#else
 - (BOOL)isAnimating;
+#endif
 
 // if YES, the UIImageView will display a focused appearance when any of its immediate or distant superviews become focused
 @property (nonatomic) BOOL adjustsImageWhenAncestorFocused UIKIT_AVAILABLE_TVOS_ONLY(9_0);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInterface.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInterface.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInterface.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIInterface.h	2016-06-29 06:52:45.000000000 +0200
@@ -56,6 +56,16 @@
 // System colors
 
 @interface UIColor (UIColorSystemColors)
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) UIColor *lightTextColor __TVOS_PROHIBITED;                // for a dark background
+@property(class, nonatomic, readonly) UIColor *darkTextColor __TVOS_PROHIBITED;                 // for a light background
+
+@property(class, nonatomic, readonly) UIColor *groupTableViewBackgroundColor __TVOS_PROHIBITED;
+
+@property(class, nonatomic, readonly) UIColor *viewFlipsideBackgroundColor NS_DEPRECATED_IOS(2_0, 7_0) __TVOS_PROHIBITED;
+@property(class, nonatomic, readonly) UIColor *scrollViewTexturedBackgroundColor NS_DEPRECATED_IOS(3_2, 7_0) __TVOS_PROHIBITED;
+@property(class, nonatomic, readonly) UIColor *underPageBackgroundColor NS_DEPRECATED_IOS(5_0, 7_0) __TVOS_PROHIBITED;
+#else
 + (UIColor *)lightTextColor __TVOS_PROHIBITED;                // for a dark background
 + (UIColor *)darkTextColor __TVOS_PROHIBITED;                 // for a light background
 
@@ -64,15 +74,23 @@
 + (UIColor *)viewFlipsideBackgroundColor NS_DEPRECATED_IOS(2_0, 7_0) __TVOS_PROHIBITED;
 + (UIColor *)scrollViewTexturedBackgroundColor NS_DEPRECATED_IOS(3_2, 7_0) __TVOS_PROHIBITED;
 + (UIColor *)underPageBackgroundColor NS_DEPRECATED_IOS(5_0, 7_0) __TVOS_PROHIBITED;
+#endif
 @end
 
 // System fonts
 
 @interface UIFont (UIFontSystemFonts)
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) CGFloat labelFontSize __TVOS_PROHIBITED;
+@property(class, nonatomic, readonly) CGFloat buttonFontSize __TVOS_PROHIBITED;
+@property(class, nonatomic, readonly) CGFloat smallSystemFontSize __TVOS_PROHIBITED;
+@property(class, nonatomic, readonly) CGFloat systemFontSize __TVOS_PROHIBITED;
+#else
 + (CGFloat)labelFontSize __TVOS_PROHIBITED;
 + (CGFloat)buttonFontSize __TVOS_PROHIBITED;
 + (CGFloat)smallSystemFontSize __TVOS_PROHIBITED;
 + (CGFloat)systemFontSize __TVOS_PROHIBITED;
+#endif
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-06-03 05:02:19.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-06-27 07:06:58.000000000 +0200
@@ -130,7 +130,6 @@
 #import <UIKit/UIProgressView.h>
 #import <UIKit/UIReferenceLibraryViewController.h>
 #import <UIKit/UIRefreshControl.h>
-#import <UIKit/UIRefreshControlHosting.h>
 #import <UIKit/UIResponder.h>
 #import <UIKit/UIRotationGestureRecognizer.h>
 #import <UIKit/UIScreen.h>
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2016-06-29 06:52:45.000000000 +0200
@@ -26,3 +26,6 @@
 #define UIKIT_CLASS_AVAILABLE_TVOS_ONLY(vers) UIKIT_EXTERN __IOS_UNAVAILABLE __WATCHOS_UNAVAILABLE __TVOS_AVAILABLE(vers)
 #define UIKIT_CLASS_AVAILABLE_IOS_TVOS(_ios, _tvos) UIKIT_EXTERN __IOS_AVAILABLE(_ios) __WATCHOS_UNAVAILABLE __TVOS_AVAILABLE(_tvos)
 #define UIKIT_CLASS_AVAILABLE_IOS_WATCHOS_TVOS(_ios, _watchos, _tvos) UIKIT_EXTERN __IOS_AVAILABLE(_ios) __WATCHOS_AVAILABLE(_watchos) __TVOS_AVAILABLE(_tvos)
+
+#define UIKIT_DEFINE_AS_PROPERTIES (!defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_UIKIT_EPOCH) && SWIFT_SDK_OVERLAY_UIKIT_EPOCH >= 1))
+#define UIKIT_REMOVE_ZERO_FROM_SWIFT (!defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_UIKIT_EPOCH) && SWIFT_SDK_OVERLAY_UIKIT_EPOCH >= 1))
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIManagedDocument.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIManagedDocument.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIManagedDocument.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIManagedDocument.h	2016-06-29 06:52:45.000000000 +0200
@@ -18,7 +18,11 @@
 
 /* The name for the persistent store file inside the document's file wrapper.  When working with the Core Data APIs, this path component is appended to the document URL provided by the UIDocument APIs.  The default name is @"documentpersistentstore.db"
  */
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) NSString *persistentStoreName;
+#else
 + (NSString *)persistentStoreName;
+#endif
 
 /* Persistent documents always have a managed object context and a persistent store coordinator through that context.  The managed object context is required to be initialized with the concurrency type NSMainQueueConcurrencyType and it must have a parent context initialized with the concurrency type NSPrivateQueueConcurrencyType.
  */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIMenuController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIMenuController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIMenuController.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIMenuController.h	2016-06-29 06:52:45.000000000 +0200
@@ -23,7 +23,11 @@
 
 NS_CLASS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED @interface UIMenuController : NSObject
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) UIMenuController *sharedMenuController;
+#else
 + (UIMenuController *)sharedMenuController;
+#endif
 
 @property(nonatomic,getter=isMenuVisible) BOOL menuVisible;	    // default is NO
 - (void)setMenuVisible:(BOOL)menuVisible animated:(BOOL)animated;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h	2016-06-29 06:37:32.000000000 +0200
@@ -17,7 +17,12 @@
 
 NS_CLASS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED @interface UIPasteboard : NSObject
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) UIPasteboard *generalPasteboard;
+#else
 + (UIPasteboard *)generalPasteboard;
+#endif
+
 + (nullable UIPasteboard *)pasteboardWithName:(NSString *)pasteboardName create:(BOOL)create;
 + (UIPasteboard *)pasteboardWithUniqueName;
 
@@ -31,7 +36,11 @@
 
 // First item
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) NSArray<NSString *> * pasteboardTypes;
+#else
 - (NSArray<NSString *> *)pasteboardTypes;
+#endif
 - (BOOL)containsPasteboardTypes:(NSArray<NSString *> *)pasteboardTypes;
 - (nullable NSData *)dataForPasteboardType:(NSString *)pasteboardType;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverBackgroundView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverBackgroundView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverBackgroundView.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPopoverBackgroundView.h	2016-06-29 06:52:46.000000000 +0200
@@ -40,6 +40,10 @@
 
 /* This method may be overridden to prevent the drawing of the content inset and drop shadow inside the popover. The default implementation of this method returns YES.
  */
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) BOOL wantsDefaultContentAppearance NS_AVAILABLE_IOS(6_0);
+#else
 + (BOOL)wantsDefaultContentAppearance NS_AVAILABLE_IOS(6_0);
+#endif
 
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPresentationController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPresentationController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPresentationController.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPresentationController.h	2016-06-27 06:29:56.000000000 +0200
@@ -57,7 +57,11 @@
 // By default this implementation defers to the delegate, if one exists, or returns the current presentation style. UIFormSheetPresentationController, and
 // UIPopoverPresentationController override this implementation to return UIModalPresentationStyleFullscreen if the delegate does not provide an
 // implementation for adaptivePresentationStyleForPresentationController:
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) UIModalPresentationStyle adaptivePresentationStyle;
+#else
 - (UIModalPresentationStyle)adaptivePresentationStyle;
+#endif
 - (UIModalPresentationStyle)adaptivePresentationStyleForTraitCollection:(UITraitCollection *)traitCollection NS_AVAILABLE_IOS(8_3);
 
 - (void)containerViewWillLayoutSubviews;
@@ -66,6 +70,23 @@
 // A view that's going to be animated during the presentation. Must be an ancestor of a presented view controller's view
 // or a presented view controller's view itself.
 // (Default: presented view controller's view)
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, nullable) UIView *presentedView;
+
+// Position of the presented view in the container view by the end of the presentation transition.
+// (Default: container view bounds)
+@property(nonatomic, readonly) CGRect frameOfPresentedViewInContainerView;
+
+// By default each new presentation is full screen.
+// This behavior can be overriden with the following method to force a current context presentation.
+// (Default: YES)
+@property(nonatomic, readonly) BOOL shouldPresentInFullscreen;
+
+// Indicate whether the view controller's view we are transitioning from will be removed from the window in the end of the
+// presentation transition
+// (Default: NO)
+@property(nonatomic, readonly) BOOL shouldRemovePresentersView;
+#else
 - (nullable UIView *)presentedView;
 
 // Position of the presented view in the container view by the end of the presentation transition.
@@ -81,6 +102,7 @@
 // presentation transition
 // (Default: NO)
 - (BOOL)shouldRemovePresentersView;
+#endif
 
 - (void)presentationTransitionWillBegin;
 - (void)presentationTransitionDidEnd:(BOOL)completed;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPressesEvent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPressesEvent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPressesEvent.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPressesEvent.h	2016-06-29 06:52:46.000000000 +0200
@@ -13,7 +13,11 @@
 
 NS_CLASS_AVAILABLE_IOS(9_0) @interface UIPressesEvent : UIEvent
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) NSSet <UIPress *> *allPresses;
+#else
 - (NSSet <UIPress *> *)allPresses;
+#endif
 - (NSSet <UIPress *> *)pressesForGestureRecognizer:(UIGestureRecognizer *)gesture;
 
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintInteractionController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintInteractionController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintInteractionController.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintInteractionController.h	2016-06-27 06:32:24.000000000 +0200
@@ -30,13 +30,25 @@
 
 NS_CLASS_AVAILABLE_IOS(4_2) __TVOS_PROHIBITED @interface UIPrintInteractionController : NSObject
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly, getter=isPrintingAvailable) BOOL printingAvailable;                    // return YES if system supports printing. use this to hide HI for unsupported devices.
+#else
 + (BOOL)isPrintingAvailable;                    // return YES if system supports printing. use this to hide HI for unsupported devices.
+#endif
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) NSSet<NSString *> *printableUTIs;                       // return set of all document UTI types we can print
+#else
 + (NSSet<NSString *> *)printableUTIs;                       // return set of all document UTI types we can print
+#endif
 + (BOOL)canPrintURL:(NSURL *)url;
 + (BOOL)canPrintData:(NSData *)data;
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) UIPrintInteractionController *sharedPrintController;
+#else
 + (UIPrintInteractionController *)sharedPrintController;
+#endif
 
 @property(nullable,nonatomic,strong) UIPrintInfo                             *printInfo;      // changes to printInfo ignored while printing. default is nil
 @property(nullable,nonatomic,weak)   id<UIPrintInteractionControllerDelegate> delegate;       // not retained. default is nil
@@ -69,7 +81,7 @@
 __TVOS_PROHIBITED @protocol UIPrintInteractionControllerDelegate <NSObject>
 @optional
 
-- (UIViewController *)printInteractionControllerParentViewController:(UIPrintInteractionController *)printInteractionController;
+- ( UIViewController * _Nullable )printInteractionControllerParentViewController:(UIPrintInteractionController *)printInteractionController;
 
 - (UIPrintPaper *)printInteractionController:(UIPrintInteractionController *)printInteractionController choosePaper:(NSArray<UIPrintPaper *> *)paperList;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRefreshControlHosting.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRefreshControlHosting.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRefreshControlHosting.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRefreshControlHosting.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,17 +0,0 @@
-//
-//  UIRefreshControlHosting.h
-//  UIKit
-//
-//  Copyright 2016 Apple Inc. All rights reserved.
-//
-
-#import <Foundation/Foundation.h>
-
-@class UIRefreshControl;
-
-NS_CLASS_AVAILABLE_IOS(10_0) @protocol UIRefreshControlHosting <NSObject>
-
-@property (nonatomic, strong, nullable) UIRefreshControl *refreshControl __TVOS_PROHIBITED;
-
-@end
-
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRegion.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRegion.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRegion.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIRegion.h	2016-06-29 06:52:45.000000000 +0200
@@ -14,7 +14,11 @@
 
 /*! A shared infinite region
  */
-+ (instancetype)infiniteRegion;
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) UIRegion *infiniteRegion;
+#else
++ (UIRegion *)infiniteRegion;
+#endif
 
 /*! Create a circular region with radius
  */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h	2016-06-03 06:16:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIResponder.h	2016-06-27 06:29:56.000000000 +0200
@@ -16,15 +16,31 @@
 
 NS_CLASS_AVAILABLE_IOS(2_0) @interface UIResponder : NSObject
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, nullable) UIResponder *nextResponder;
+#else
 - (nullable UIResponder*)nextResponder;
+#endif
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) BOOL canBecomeFirstResponder;    // default is NO
+#else
 - (BOOL)canBecomeFirstResponder;    // default is NO
+#endif
 - (BOOL)becomeFirstResponder;
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) BOOL canResignFirstResponder;    // default is YES
+#else
 - (BOOL)canResignFirstResponder;    // default is YES
+#endif
 - (BOOL)resignFirstResponder;
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) BOOL isFirstResponder;
+#else
 - (BOOL)isFirstResponder;
+#endif
 
 // Generally, all responders which do custom touch handling should override all four of these methods.
 // Your responder will receive either touchesEnded:withEvent: or touchesCancelled:withEvent: for each
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h	2016-06-03 06:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h	2016-06-27 06:29:57.000000000 +0200
@@ -34,8 +34,13 @@
 
 NS_CLASS_AVAILABLE_IOS(2_0) @interface UIScreen : NSObject <UITraitEnvironment>
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) NSArray<UIScreen *> *screens NS_AVAILABLE_IOS(3_2);          // all screens currently attached to the device
+@property(class, nonatomic, readonly) UIScreen *mainScreen;      // the device's internal screen
+#else
 + (NSArray<UIScreen *> *)screens NS_AVAILABLE_IOS(3_2);          // all screens currently attached to the device
 + (UIScreen *)mainScreen;      // the device's internal screen
+#endif
 
 @property(nonatomic,readonly) CGRect  bounds;                // Bounds of entire screen in points
 @property(nonatomic,readonly) CGFloat scale NS_AVAILABLE_IOS(4_0);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScrollView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScrollView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScrollView.h	2016-06-03 05:02:19.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScrollView.h	2016-06-27 06:32:24.000000000 +0200
@@ -9,8 +9,8 @@
 #import <CoreGraphics/CoreGraphics.h>
 #import <UIKit/UIView.h>
 #import <UIKit/UIGeometry.h>
-#import <UIKit/UIRefreshControlHosting.h>
 #import <UIKit/UIKitDefines.h>
+#import <UIKit/UIRefreshControl.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -32,7 +32,7 @@
 @class UIEvent, UIImageView, UIPanGestureRecognizer, UIPinchGestureRecognizer;
 @protocol UIScrollViewDelegate;
 
-NS_CLASS_AVAILABLE_IOS(2_0) @interface UIScrollView : UIView <NSCoding, UIRefreshControlHosting>
+NS_CLASS_AVAILABLE_IOS(2_0) @interface UIScrollView : UIView <NSCoding>
 
 @property(nonatomic)         CGPoint                      contentOffset;                  // default CGPointZero
 @property(nonatomic)         CGSize                       contentSize;                    // default CGSizeZero
@@ -115,6 +115,8 @@
 
 @property(nonatomic) UIScrollViewKeyboardDismissMode keyboardDismissMode NS_AVAILABLE_IOS(7_0); // default is UIScrollViewKeyboardDismissModeNone
 
+@property (nonatomic, strong, nullable) UIRefreshControl *refreshControl NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED;
+
 @end
 
 @protocol UIScrollViewDelegate<NSObject>
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISplitViewController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISplitViewController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISplitViewController.h	2016-06-03 06:16:42.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UISplitViewController.h	2016-06-27 06:29:57.000000000 +0200
@@ -39,7 +39,11 @@
 @property (nonatomic, readonly) UISplitViewControllerDisplayMode displayMode NS_AVAILABLE_IOS(8_0);
 
 // A system bar button item whose action will change the displayMode property depending on the result of targetDisplayModeForActionInSplitViewController:. When inserted into the navigation bar of the secondary view controller it will change its appearance to match its target display mode. When the target displayMode is PrimaryHidden, this will appear as a fullscreen button, for AllVisible or PrimaryOverlay it will appear as a Back button, and when it won't cause any action it will become hidden.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property (nonatomic, readonly) UIBarButtonItem *displayModeButtonItem NS_AVAILABLE_IOS(8_0);
+#else
 - (UIBarButtonItem *)displayModeButtonItem NS_AVAILABLE_IOS(8_0);
+#endif
 
 // An animatable property that can be used to adjust the relative width of the primary view controller in the split view controller. This preferred width will be limited by the maximum and minimum properties (and potentially other system heuristics).
 @property(nonatomic, assign) CGFloat preferredPrimaryColumnWidthFraction NS_AVAILABLE_IOS(8_0); // default: UISplitViewControllerAutomaticDimension
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIStackView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIStackView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIStackView.h	2016-06-03 06:16:43.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIStackView.h	2016-06-27 06:32:25.000000000 +0200
@@ -104,12 +104,17 @@
 NS_CLASS_AVAILABLE_IOS(9_0)
 @interface UIStackView : UIView
 
+- (instancetype)initWithFrame:(CGRect)frame NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+
 /* UIStackView enforces that all views in the arrangedSubviews list
  must be subviews of the UIStackView.
     Thus, when a view is added to the arrangedSubviews, UIStackView
  adds it as a subview if it isn't already. And when a view in a
  UIStackView's arrangedSubviews list receives -removeFromSuperview
  it is also removed from the arrangedSubviews.
+ 
+ Please note that this is a convenience initializer and cannot be overridden in Swift.
  */
 - (instancetype)initWithArrangedSubviews:(NSArray<__kindof UIView *> *)views; // Adds views as subviews of the receiver.
 @property(nonatomic,readonly,copy) NSArray<__kindof UIView *> *arrangedSubviews;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBar.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBar.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBar.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITabBar.h	2016-06-27 06:29:57.000000000 +0200
@@ -33,7 +33,11 @@
 
 - (void)beginCustomizingItems:(NSArray<UITabBarItem *> *)items __TVOS_PROHIBITED;   // list all items that can be reordered. always animates a sheet up. visible items not listed are fixed in place
 - (BOOL)endCustomizingAnimated:(BOOL)animated __TVOS_PROHIBITED;    // hide customization sheet. normally you should let the user do it. check list of items to see new layout. returns YES if layout changed
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, getter=isCustomizing) BOOL customizing __TVOS_PROHIBITED;
+#else
 - (BOOL)isCustomizing __TVOS_PROHIBITED;
+#endif
 
 /*
  The behavior of tintColor for bars has changed on iOS 7.0. It no longer affects the bar's background
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableViewController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableViewController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableViewController.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableViewController.h	2016-06-29 06:52:45.000000000 +0200
@@ -7,7 +7,6 @@
 #import <Foundation/Foundation.h>
 #import <UIKit/UIViewController.h>
 #import <UIKit/UITableView.h>
-#import <UIKit/UIRefreshControlHosting.h>
 #import <UIKit/UIKitDefines.h>
 
 // Creates a table view with the correct dimensions and autoresizing, setting the datasource and delegate to self.
@@ -17,7 +16,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE_IOS(2_0) @interface UITableViewController : UIViewController <UITableViewDelegate, UITableViewDataSource, UIRefreshControlHosting>
+NS_CLASS_AVAILABLE_IOS(2_0) @interface UITableViewController : UIViewController <UITableViewDelegate, UITableViewDataSource>
 
 - (instancetype)initWithStyle:(UITableViewStyle)style NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithNibName:(nullable NSString *)nibNameOrNil bundle:(nullable NSBundle *)nibBundleOrNil NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextChecker.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextChecker.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextChecker.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextChecker.h	2016-06-29 06:52:45.000000000 +0200
@@ -26,8 +26,12 @@
 
 /* Methods for dealing with ignored words. */
 - (void)ignoreWord:(NSString *)wordToIgnore;
-- (nullable NSArray<NSString *> *)ignoredWords;
-- (void)setIgnoredWords:(nullable NSArray<NSString *> *)words;
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, strong, nullable) NSArray<NSString *> *ignoredWords;
+#else
+- (nullable NSArray *)ignoredWords;
+- (void)setIgnoredWords:(nullable NSArray *)words;
+#endif
 
 /* These allow clients to programmatically instruct the checker to learn and unlearn words, and to determine whether a word has been learned (and hence can potentially be unlearned). */
 + (void)learnWord:(NSString *)word;
@@ -35,7 +39,11 @@
 + (void)unlearnWord:(NSString *)word;
 
 /* Entries in the availableLanguages list are all available spellchecking languages in user preference order, usually language abbreviations such as en_US. */
-+ (NSArray<NSString *> *)availableLanguages;
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) NSArray<NSString *> *availableLanguages;
+#else
++ (NSArray *)availableLanguages;
+#endif
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h	2016-06-27 06:32:24.000000000 +0200
@@ -18,7 +18,11 @@
 
 @protocol UIKeyInput <UITextInputTraits>
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) BOOL hasText;
+#else
 - (BOOL)hasText;
+#endif
 - (void)insertText:(NSString *)text;
 - (void)deleteBackward;
 
@@ -188,7 +192,11 @@
  * pending dictation results. -insertDictationPlaceholder must return a reference to the 
  * placeholder. This reference will be used to identify the placeholder by the other methods
  * (there may be more than one placeholder). */
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) id insertDictationResultPlaceholder;
+#else
 - (id)insertDictationResultPlaceholder;
+#endif
 - (CGRect)frameForDictationResultPlaceholder:(id)placeholder;
 /* willInsertResult will be NO if the recognition failed. */
 - (void)removeDictationResultPlaceholder:(id)placeholder willInsertResult:(BOOL)willInsertResult;
@@ -279,7 +287,11 @@
 
 // To query the UITextInputMode, refer to the UIResponder method -textInputMode.
 + (nullable UITextInputMode *)currentInputMode NS_DEPRECATED_IOS(4_2, 7_0)  __TVOS_PROHIBITED; // The current input mode.  Nil if unset.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) NSArray<UITextInputMode *> *activeInputModes; // The active input modes.
+#else
 + (NSArray<UITextInputMode *> *)activeInputModes; // The active input modes.
+#endif
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITraitCollection.h	2016-06-29 06:52:45.000000000 +0200
@@ -33,8 +33,8 @@
 + (UITraitCollection *)traitCollectionWithUserInterfaceStyle:(UIUserInterfaceStyle)userInterfaceStyle __TVOS_AVAILABLE(10_0) __WATCHOS_PROHIBITED __IOS_PROHIBITED;
 @property (nonatomic, readonly) UIUserInterfaceStyle userInterfaceStyle __TVOS_AVAILABLE(10_0) __WATCHOS_PROHIBITED __IOS_PROHIBITED; // unspecified: UIUserInterfaceStyleUnspecified
 
-+ (UITraitCollection *)traitCollectionWithLayoutDirection:(UITraitEnvironmentLayoutDirection)layoutDirection;
-@property (nonatomic, readonly) UITraitEnvironmentLayoutDirection layoutDirection; // unspecified: UITraitEnvironmentLayoutDirectionUnspecified
++ (UITraitCollection *)traitCollectionWithLayoutDirection:(UITraitEnvironmentLayoutDirection)layoutDirection NS_AVAILABLE_IOS(10_0);
+@property (nonatomic, readonly) UITraitEnvironmentLayoutDirection layoutDirection NS_AVAILABLE_IOS(10_0); // unspecified: UITraitEnvironmentLayoutDirectionUnspecified
 
 + (UITraitCollection *)traitCollectionWithDisplayScale:(CGFloat)scale;
 @property (nonatomic, readonly) CGFloat displayScale; // unspecified: 0.0
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIView.h	2016-06-03 05:02:19.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIView.h	2016-06-29 06:52:45.000000000 +0200
@@ -136,7 +136,11 @@
 
 NS_CLASS_AVAILABLE_IOS(2_0) @interface UIView : UIResponder <NSCoding, UIAppearance, UIAppearanceContainer, UIDynamicItem, UITraitEnvironment, UICoordinateSpace, UIFocusItem, CALayerDelegate>
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) Class layerClass;                        // default is [CALayer class]. Used when creating the underlying layer for the view.
+#else
 + (Class)layerClass;                        // default is [CALayer class]. Used when creating the underlying layer for the view.
+#endif
 
 - (instancetype)initWithFrame:(CGRect)frame NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
@@ -145,7 +149,11 @@
 @property(nonatomic)                                 NSInteger tag;                // default is 0
 @property(nonatomic,readonly,strong)                 CALayer  *layer;              // returns view's layer. Will always return a non-nil value. view is layer's delegate
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic,readonly) BOOL canBecomeFocused NS_AVAILABLE_IOS(9_0); // NO by default
+#else
 - (BOOL)canBecomeFocused NS_AVAILABLE_IOS(9_0); // NO by default
+#endif
 @property (readonly, nonatomic, getter=isFocused) BOOL focused NS_AVAILABLE_IOS(9_0);
 
 @property (nonatomic) UISemanticContentAttribute semanticContentAttribute NS_AVAILABLE_IOS(9_0);
@@ -303,10 +311,18 @@
 + (void)setAnimationTransition:(UIViewAnimationTransition)transition forView:(UIView *)view cache:(BOOL)cache;  // current limitation - only one per begin/commit block
 
 + (void)setAnimationsEnabled:(BOOL)enabled;                         // ignore any attribute changes while set.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) BOOL areAnimationsEnabled;
+#else
 + (BOOL)areAnimationsEnabled;
+#endif
 + (void)performWithoutAnimation:(void (NS_NOESCAPE ^)(void))actionsWithoutAnimation NS_AVAILABLE_IOS(7_0);
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) NSTimeInterval inheritedAnimationDuration NS_AVAILABLE_IOS(9_0);
+#else
 + (NSTimeInterval)inheritedAnimationDuration NS_AVAILABLE_IOS(9_0);
+#endif
 
 @end
 
@@ -426,7 +442,11 @@
 
 /* constraint-based layout engages lazily when someone tries to use it (e.g., adds a constraint to a view).  If you do all of your constraint set up in -updateConstraints, you might never even receive updateConstraints if no one makes a constraint.  To fix this chicken and egg problem, override this method to return YES if your view needs the window to use constraint-based layout.  
  */
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(class, nonatomic, readonly) BOOL requiresConstraintBasedLayout NS_AVAILABLE_IOS(6_0);
+#else
 + (BOOL)requiresConstraintBasedLayout NS_AVAILABLE_IOS(6_0);
+#endif
 
 @end
 
@@ -448,7 +468,11 @@
 
 /* override this if the alignment rect is obtained from the frame by insetting each edge by a fixed amount.  This is only called by alignmentRectForFrame: and frameForAlignmentRect:.
  */
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) UIEdgeInsets alignmentRectInsets NS_AVAILABLE_IOS(6_0);
+#else
 - (UIEdgeInsets)alignmentRectInsets NS_AVAILABLE_IOS(6_0);
+#endif
 
 - (UIView *)viewForBaselineLayout NS_DEPRECATED_IOS(6_0, 9_0, "Override -viewForFirstBaselineLayout or -viewForLastBaselineLayout as appropriate, instead") __TVOS_PROHIBITED;
 
@@ -488,7 +512,11 @@
  Note that not all views have an intrinsicContentSize.  UIView's default implementation is to return (UIViewNoIntrinsicMetric, UIViewNoIntrinsicMetric).  The _intrinsic_ content size is concerned only with data that is in the view itself, not in other views. Remember that you can also set constant width or height constraints on any view, and you don't need to override instrinsicContentSize if these dimensions won't be changing with changing view content.
  */
 UIKIT_EXTERN const CGFloat UIViewNoIntrinsicMetric NS_AVAILABLE_IOS(6_0); // -1
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) CGSize intrinsicContentSize NS_AVAILABLE_IOS(6_0);
+#else
 - (CGSize)intrinsicContentSize NS_AVAILABLE_IOS(6_0);
+#endif
 - (void)invalidateIntrinsicContentSize NS_AVAILABLE_IOS(6_0); // call this when something changes that affects the intrinsicContentSize.  Otherwise UIKit won't notice that it changed.  
 
 - (UILayoutPriority)contentHuggingPriorityForAxis:(UILayoutConstraintAxis)axis NS_AVAILABLE_IOS(6_0);
@@ -561,7 +589,12 @@
  -hasAmbiguousLayout runs a check for whether there is another center and bounds the receiver could have that could also satisfy the constraints.
  -exerciseAmbiguousLayout does more.  It randomly changes the view layout to a different valid layout.  Making the UI jump back and forth can be helpful for figuring out where you're missing a constraint.  
  */
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) BOOL hasAmbiguousLayout NS_AVAILABLE_IOS(6_0);
+#else
 - (BOOL)hasAmbiguousLayout NS_AVAILABLE_IOS(6_0);
+#endif
+
 - (void)exerciseAmbiguityInLayout NS_AVAILABLE_IOS(6_0); 
 @end
 
@@ -578,7 +611,11 @@
  The symptom of ambiguity is that views sometimes jump from place to place, or possibly are just in the wrong place.
  -hasAmbiguousLayout runs a check for whether there is another center and bounds the receiver could have that could also satisfy the constraints.
  */
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) BOOL hasAmbiguousLayout NS_AVAILABLE_IOS(10_0);
+#else
 - (BOOL)hasAmbiguousLayout NS_AVAILABLE_IOS(10_0);
+#endif
 @end
 
 @interface UIView (UIStateRestoration)
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewAnimating.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewAnimating.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewAnimating.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewAnimating.h	2016-06-29 06:52:45.000000000 +0200
@@ -47,6 +47,9 @@
 // Starts the animation either from an inactive state, or if the animation has been paused.
 - (void)startAnimation;
 
+// Starts the animation after the given delay.
+- (void)startAnimationAfterDelay:(NSTimeInterval)delay;
+
 // Pauses an active, running animation, or start the animation as paused. This is different
 // than stopping an animation.
 - (void)pauseAnimation;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h	2016-06-03 05:02:19.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h	2016-06-29 06:37:32.000000000 +0200
@@ -113,7 +113,11 @@
 - (void)viewDidUnload NS_DEPRECATED_IOS(3_0,6_0) __TVOS_PROHIBITED; // Called after the view controller's view is released and set to nil. For example, a memory warning which causes the view to be purged. Not invoked as a result of -dealloc.
 
 - (void)viewDidLoad; // Called after the view has been loaded. For view controllers created in code, this is after -loadView. For view controllers unarchived from a nib, this is after the view is set.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, getter=isViewLoaded) BOOL viewLoaded NS_AVAILABLE_IOS(3_0);
+#else
 - (BOOL)isViewLoaded NS_AVAILABLE_IOS(3_0);
+#endif
 
 @property(nullable, nonatomic, readonly, copy) NSString *nibName;     // The name of the nib to be loaded to instantiate the view.
 @property(nullable, nonatomic, readonly, strong) NSBundle *nibBundle; // The bundle from which to load the nib.
@@ -196,11 +200,19 @@
   method by checking the expression ([self isBeingDismissed] || [self isMovingFromParentViewController]).
 */
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, getter=isBeingPresented) BOOL beingPresented NS_AVAILABLE_IOS(5_0);
+@property(nonatomic, readonly, getter=isBeingDismissed) BOOL beingDismissed NS_AVAILABLE_IOS(5_0);
+
+@property(nonatomic, readonly, getter=isMovingToParentViewController) BOOL movingToParentViewController NS_AVAILABLE_IOS(5_0);
+@property(nonatomic, readonly, getter=isMovingFromParentViewController) BOOL movingFromParentViewController NS_AVAILABLE_IOS(5_0);
+#else
 - (BOOL)isBeingPresented NS_AVAILABLE_IOS(5_0);
 - (BOOL)isBeingDismissed NS_AVAILABLE_IOS(5_0);
 
 - (BOOL)isMovingToParentViewController NS_AVAILABLE_IOS(5_0);
 - (BOOL)isMovingFromParentViewController NS_AVAILABLE_IOS(5_0);
+#endif
 
 /*
   The next two methods are replacements for presentModalViewController:animated and
@@ -228,7 +240,11 @@
 @property(nonatomic,assign) BOOL modalPresentationCapturesStatusBarAppearance NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
 
 // Presentation modes may keep the keyboard visible when not required. Default implementation affects UIModalPresentationFormSheet visibility.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic,assign) BOOL disablesAutomaticKeyboardDismissal NS_AVAILABLE_IOS(4_3);
+#else
 - (BOOL)disablesAutomaticKeyboardDismissal NS_AVAILABLE_IOS(4_3);
+#endif
 
 @property(nonatomic,assign) BOOL wantsFullScreenLayout NS_DEPRECATED_IOS(3_0, 7_0) __TVOS_PROHIBITED; // Deprecated in 7_0, Replaced by the following:
 
@@ -241,10 +257,17 @@
 @property (nonatomic) CGSize preferredContentSize NS_AVAILABLE_IOS(7_0);
 
 // These methods control the attributes of the status bar when this view controller is shown. They can be overridden in view controller subclasses to return the desired status bar attributes.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) UIStatusBarStyle preferredStatusBarStyle NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED; // Defaults to UIStatusBarStyleDefault
+@property(nonatomic, readonly) BOOL prefersStatusBarHidden NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED; // Defaults to NO
+// Override to return the type of animation that should be used for status bar changes for this view controller. This currently only affects changes to prefersStatusBarHidden.
+@property(nonatomic, readonly) UIStatusBarAnimation preferredStatusBarUpdateAnimation NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED; // Defaults to UIStatusBarAnimationFade
+#else
 - (UIStatusBarStyle)preferredStatusBarStyle NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED; // Defaults to UIStatusBarStyleDefault
 - (BOOL)prefersStatusBarHidden NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED; // Defaults to NO
 // Override to return the type of animation that should be used for status bar changes for this view controller. This currently only affects changes to prefersStatusBarHidden.
 - (UIStatusBarAnimation)preferredStatusBarUpdateAnimation NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED; // Defaults to UIStatusBarAnimationFade
+#endif
 
 // This should be called whenever the return values for the view controller's status bar attributes have changed. If it is called from within an animation block, the changes will be animated along with the rest of the animation block.
 - (void)setNeedsStatusBarAppearanceUpdate NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
@@ -272,10 +295,17 @@
 - (BOOL)shouldAutorotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation NS_DEPRECATED_IOS(2_0, 6_0) __TVOS_PROHIBITED;
 
 // New Autorotation support.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) BOOL shouldAutorotate NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
+@property(nonatomic, readonly) UIInterfaceOrientationMask supportedInterfaceOrientations NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
+// Returns interface orientation masks.
+@property(nonatomic, readonly) UIInterfaceOrientation preferredInterfaceOrientationForPresentation NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
+#else
 - (BOOL)shouldAutorotate NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
 - (UIInterfaceOrientationMask)supportedInterfaceOrientations NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
 // Returns interface orientation masks.
 - (UIInterfaceOrientation)preferredInterfaceOrientationForPresentation NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
+#endif
 
 // The rotating header and footer views will slide out during the rotation and back in once it has completed.
 - (nullable UIView *)rotatingHeaderView NS_DEPRECATED_IOS(2_0,8_0, "Header views are animated along with the rest of the view hierarchy") __TVOS_PROHIBITED;     // Must be in the view hierarchy. Default returns nil.
@@ -302,7 +332,11 @@
 @property(nonatomic,getter=isEditing) BOOL editing;
 - (void)setEditing:(BOOL)editing animated:(BOOL)animated; // Updates the appearance of the Edit|Done button item as necessary. Clients who override it must call super first.
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) UIBarButtonItem *editButtonItem; // Return an Edit|Done button that can be used as a navigation item's custom view. Default action toggles the editing state with animation.
+#else
 - (UIBarButtonItem *)editButtonItem; // Return an Edit|Done button that can be used as a navigation item's custom view. Default action toggles the editing state with animation.
+#endif
 
 @end
 
@@ -367,8 +401,13 @@
 - (void)endAppearanceTransition __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_5_0);
 
 // Override to return a child view controller or nil. If non-nil, that view controller's status bar appearance attributes will be used. If nil, self is used. Whenever the return values from these methods change, -setNeedsUpdatedStatusBarAttributes should be called.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, nullable) UIViewController *childViewControllerForStatusBarStyle NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
+@property(nonatomic, readonly, nullable) UIViewController *childViewControllerForStatusBarHidden NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
+#else
 - (nullable UIViewController *)childViewControllerForStatusBarStyle NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
 - (nullable UIViewController *)childViewControllerForStatusBarHidden NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
+#endif
 
 // Call to modify the trait collection for child view controllers.
 - (void)setOverrideTraitCollection:(nullable UITraitCollection *)collection forChildViewController:(UIViewController *)childViewController NS_AVAILABLE_IOS(8_0);
@@ -390,7 +429,11 @@
 - (BOOL)automaticallyForwardAppearanceAndRotationMethodsToChildViewControllers NS_DEPRECATED_IOS(5_0,6_0) __TVOS_PROHIBITED;
 - (BOOL)shouldAutomaticallyForwardRotationMethods NS_DEPRECATED_IOS(6_0,8_0, "Manually forward viewWillTransitionToSize:withTransitionCoordinator: if necessary") __TVOS_PROHIBITED;
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) BOOL shouldAutomaticallyForwardAppearanceMethods NS_AVAILABLE_IOS(6_0);
+#else
 - (BOOL)shouldAutomaticallyForwardAppearanceMethods NS_AVAILABLE_IOS(6_0);
+#endif
 
 
 /*
@@ -511,7 +554,11 @@
 
 @interface UIViewController ()
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) NSArray <id <UIPreviewActionItem>> *previewActionItems NS_AVAILABLE_IOS(9_0);
+#else
 - (NSArray <id <UIPreviewActionItem>> *)previewActionItems NS_AVAILABLE_IOS(9_0);
+#endif
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h	2016-06-29 06:52:46.000000000 +0200
@@ -18,35 +18,65 @@
 // new UIModalPresentationCustom presentation type we invoke the
 // animateTransition: even though the transition is not animated. (This allows
 // the custom transition to add or remove subviews to the container view.)
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, getter=isAnimated) BOOL animated;
+#else
 - (BOOL)isAnimated;
+#endif
 
 // A modal presentation style whose transition is being customized or UIModaPresentationNone if this is not a modal presentation
 // or dismissal.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) UIModalPresentationStyle presentationStyle;
+#else
 - (UIModalPresentationStyle)presentationStyle;
+#endif
 
 /// initiallyInteractive indicates whether the transition was initiated as an interactive transition.
 /// It never changes during the course of a transition.
 /// It can only be YES if isAnimated is YES.
 ///If it is NO, then isInteractive can only be YES if isInterruptible is YES
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) BOOL initiallyInteractive;
+#else
 - (BOOL)initiallyInteractive;
+#endif
 @property(nonatomic,readonly) BOOL isInterruptible NS_AVAILABLE_IOS(10_0);
 
 // Interactive transitions have non-interactive segments. For example, they all complete non-interactively. Some interactive transitions may have
 // intermediate segments that are not interactive.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, getter=isInteractive) BOOL interactive;
+#else
 - (BOOL)isInteractive;
+#endif
 
 // isCancelled is usually NO. It is only set to YES for an interactive transition that was cancelled.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, getter=isCancelled) BOOL cancelled;
+#else
 - (BOOL)isCancelled;
+#endif
 
 // The full expected duration of the transition if it is run non-interactively. 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) NSTimeInterval transitionDuration;
+#else
 - (NSTimeInterval)transitionDuration;
+#endif
 
 // These three methods are potentially meaningful for interactive transitions that are
 // completing. It reports the percent complete of the transition when it moves
 // to the non-interactive completion phase of the transition.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) CGFloat percentComplete;
+@property(nonatomic, readonly) CGFloat completionVelocity;
+@property(nonatomic, readonly) UIViewAnimationCurve completionCurve;
+#else
 - (CGFloat)percentComplete;
 - (CGFloat)completionVelocity;
 - (UIViewAnimationCurve)completionCurve;
+#endif
 
 // Currently only two keys are defined by the system:
 //   UITransitionContextToViewControllerKey
@@ -59,10 +89,18 @@
 - (nullable __kindof UIView *)viewForKey:(NSString *)key NS_AVAILABLE_IOS(8_0);
 
 // The view in which the animated transition is taking place.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) UIView *containerView;
+#else
 - (UIView *)containerView;
+#endif
 
 // This is either CGAffineTransformIdentity (indicating no rotation), or a rotation transform of +90, -90, or 180.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) CGAffineTransform targetTransform NS_AVAILABLE_IOS(8_0);
+#else
 - (CGAffineTransform)targetTransform NS_AVAILABLE_IOS(8_0);
+#endif
 
 @end
 
@@ -122,7 +160,11 @@
 // appropriate transition coordinator to return, otherwise it should call
 // super. Only custom container view controllers should ever need to override
 // this method.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, nullable) id <UIViewControllerTransitionCoordinator> transitionCoordinator NS_AVAILABLE_IOS(7_0);
+#else
 - (nullable id <UIViewControllerTransitionCoordinator>)transitionCoordinator NS_AVAILABLE_IOS(7_0);
+#endif
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h	2016-06-03 06:16:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h	2016-06-29 06:37:32.000000000 +0200
@@ -64,11 +64,24 @@
 @protocol UIViewControllerContextTransitioning <NSObject>
 
 // The view in which the animated transition should take place.
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) UIView *containerView;
+#else
 - (UIView *)containerView;
+#endif
 
 // Most of the time this is YES. For custom transitions that use the new UIModalPresentationCustom
 // presentation type we will invoke the animateTransition: even though the transition should not be
 // animated. This allows the custom transition to add or remove subviews to the container view. 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly, getter=isAnimated) BOOL animated;
+
+@property(nonatomic, readonly, getter=isInteractive) BOOL interactive; // This indicates whether the transition is currently interactive.
+
+@property(nonatomic, readonly) BOOL transitionWasCancelled;
+
+@property(nonatomic, readonly) UIModalPresentationStyle presentationStyle;
+#else
 - (BOOL)isAnimated;
 
 // The next two values can change if the animating transition is interruptible.
@@ -76,6 +89,7 @@
 - (BOOL)transitionWasCancelled;
 
 - (UIModalPresentationStyle)presentationStyle;
+#endif
 
 // An interaction controller that conforms to the
 // UIViewControllerInteractiveTransitioning protocol (which is vended by a
@@ -116,7 +130,11 @@
 // manipulate the associated view controller's view.
 - (nullable __kindof UIView *)viewForKey:(NSString *)key NS_AVAILABLE_IOS(8_0);
 
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) CGAffineTransform targetTransform NS_AVAILABLE_IOS(8_0);
+#else
 - (CGAffineTransform)targetTransform NS_AVAILABLE_IOS(8_0);
+#endif
 
 // The frame's are set to CGRectZero when they are not known or
 // otherwise undefined.  For example the finalFrame of the
@@ -142,12 +160,8 @@
 /// A conforming object implements this method if the transition it creates can
 /// be interrupted. For example, it could return an instance of a
 /// UIViewPropertyAnimator. It is expected that this method will return the same
-/// instance for the life of a transition. An interruptibleAnimator should only
-/// be created if the transitionContext is not nil. If the transitionContext is
-/// nil, then this method should return the previously created
-/// interruptibleAnimator if the transition is still in flight, or nil if it is
-/// not.
-- (nullable id <UIViewImplicitlyAnimating>) interruptibleAnimatorForTransition:(nullable id <UIViewControllerContextTransitioning>)transitionContext NS_AVAILABLE_IOS(10_0);
+/// instance for the life of a transition.
+- (id <UIViewImplicitlyAnimating>) interruptibleAnimatorForTransition:(id <UIViewControllerContextTransitioning>)transitionContext NS_AVAILABLE_IOS(10_0);
 
 // This is a convenience and if implemented will be invoked by the system when the transition context's completeTransition: method is invoked.
 - (void)animationEnded:(BOOL) transitionCompleted;
@@ -159,8 +173,13 @@
 - (void)startInteractiveTransition:(id <UIViewControllerContextTransitioning>)transitionContext;
 
 @optional
+#if UIKIT_DEFINE_AS_PROPERTIES
+@property(nonatomic, readonly) CGFloat completionSpeed;
+@property(nonatomic, readonly) UIViewAnimationCurve completionCurve;
+#else
 - (CGFloat)completionSpeed;
 - (UIViewAnimationCurve)completionCurve;
+#endif
 
 /// In 10.0, if an object conforming to UIViewControllerAnimatedTransitioning is
 /// known to be interruptible, it is possible to start it as if it was not
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewPropertyAnimator.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewPropertyAnimator.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewPropertyAnimator.h	2016-06-03 05:02:46.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewPropertyAnimator.h	2016-06-27 06:29:56.000000000 +0200
@@ -17,9 +17,15 @@
 
 @property(nonatomic, readonly) NSTimeInterval duration;
 
+// Defaults to 0. This property is set when calling -[UIView startAnimationAfterDelay:].
+@property(nonatomic, readonly) NSTimeInterval delay;
+
 /// Defaults to YES. Raises if set on an active animator.
 @property(nonatomic, getter=isUserInteractionEnabled) BOOL userInteractionEnabled;
 
+// Defaults to NO. Set if you need to manage the the hittesting of animating view hierarchies
+@property(nonatomic, getter=isManualHitTestingEnabled) BOOL manualHitTestingEnabled;
+
 /// Defaults to YES. Raises if set on an active animator.
 @property(nonatomic, getter=isInterruptible) BOOL interruptible;
 
@@ -27,7 +33,7 @@
 
 // All convenience initializers return an animator which is not running.
 - (instancetype)initWithDuration:(NSTimeInterval)duration curve:(UIViewAnimationCurve)curve animations:(void (^ __nullable)(void))animations;
-- (instancetype)initWithDuration:(NSTimeInterval)duration controlPoint1: (CGPoint)point1 controlPoint2:(CGPoint)point2  animations:(void (^)(void))animations;
+- (instancetype)initWithDuration:(NSTimeInterval)duration controlPoint1:(CGPoint)point1 controlPoint2:(CGPoint)point2 animations:(void (^ __nullable)(void))animations;
 - (instancetype)initWithDuration:(NSTimeInterval)duration dampingRatio:(CGFloat)ratio animations:(void (^ __nullable)(void))animations;
 
 /// @abstract This method provides compatibility with the old style [UIView

```