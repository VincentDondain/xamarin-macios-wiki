#NotificationCenter.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetController.h	2015-08-23 00:27:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetController.h	2016-06-06 05:45:38.000000000 +0200
@@ -1,11 +1,13 @@
 /*
  * NCWidgetController.h
  * NotificationCenter.framework
- * Copyright (c) 2014 Apple Inc. All rights reserved.
+ * Copyright (c) 2014-2015 Apple Inc. All rights reserved.
  */
 
 #import <Foundation/Foundation.h>
 
+NS_ASSUME_NONNULL_BEGIN
+
 /* The NCWidgetController provides an interface available to both the widget
    and the providing app can coordinate whether there is widget content
    available for display.
@@ -30,3 +32,5 @@
 - (void)setHasContent:(BOOL)flag forWidgetWithBundleIdentifier:(NSString *)bundleID;
 
 @end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetListViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetListViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetListViewController.h	2015-08-23 00:27:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetListViewController.h	2016-06-06 05:45:38.000000000 +0200
@@ -8,11 +8,12 @@
 
 @protocol NCWidgetListViewDelegate;
 
+NS_ASSUME_NONNULL_BEGIN
 
 NS_CLASS_AVAILABLE_MAC(10_10)
 @interface NCWidgetListViewController : NSViewController
 
-@property (weak) IBOutlet id<NCWidgetListViewDelegate> delegate;
+@property (nullable, weak) IBOutlet id<NCWidgetListViewDelegate> delegate;
 
 /* Set the contents array in order to provide contents for display in the list
    view. The list view controller will request a new content view controller
@@ -21,7 +22,7 @@
  
    As an optimization, when resetting contents, the list view controller may
    re-use content view controllers for identical objects already in contents. */
-@property (copy) NSArray *contents;
+@property (copy) NSArray<id> *contents;
 
 /* The minimum number of visible rows to display. When this property is set and
    the count of contetns is greater than this number, the list view controller
@@ -86,3 +87,5 @@
 - (void)widgetList:(NCWidgetListViewController *)list didRemoveRow:(NSUInteger)row;
 
 @end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetProviding.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetProviding.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetProviding.h	2015-08-23 00:27:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetProviding.h	2016-06-06 05:45:38.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  * NCWidgetProviding.h
  * NotificationCenter.framework
- * Copyright (c) 2014 Apple Inc. All rights reserved.
+ * Copyright (c) 2014-2015 Apple Inc. All rights reserved.
  */
 
 #import <AppKit/AppKit.h>
@@ -26,6 +26,9 @@
 } NS_ENUM_AVAILABLE_MAC(10_10);
 
 
+NS_ASSUME_NONNULL_BEGIN
+
+
 /* NCWidgetProviding is an optional protocol for further customizing aspects
    of the widget's behavior. */
 @protocol NCWidgetProviding <NSExtensionRequestHandling>
@@ -63,3 +66,5 @@
 - (void)presentViewControllerInWidget:(NSViewController *)viewController NS_AVAILABLE_MAC(10_10);
 
 @end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetSearchViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetSearchViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetSearchViewController.h	2015-08-23 00:27:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NCWidgetSearchViewController.h	2016-06-06 05:45:38.000000000 +0200
@@ -1,11 +1,12 @@
 /*
  * NCWidgetSearchViewController.h
  * NotificationCenter.framework
- * Copyright (c) 2014 Apple Inc. All rights reserved.
+ * Copyright (c) 2014-2015 Apple Inc. All rights reserved.
  */
 
 #import <AppKit/AppKit.h>
 
+NS_ASSUME_NONNULL_BEGIN
 
 @protocol NCWidgetSearchViewDelegate;
 
@@ -14,23 +15,23 @@
 
 /* The delegate is responsible for performing the search based on the
    searchTerm provided to it and setting the searchResults array accordingly. */
-@property (weak) IBOutlet id<NCWidgetSearchViewDelegate> delegate;
+@property (nullable, weak) IBOutlet id<NCWidgetSearchViewDelegate> delegate;
 
 /* A textual representation of the objects in searchResults will be displayed
    using the description property of each object. A different property may be
    specified for display using the searchResultKeyPath property. */
-@property (copy) NSArray *searchResults;
+@property (nullable, copy) NSArray<id> *searchResults;
 
 /* Specify localized header text for the search view. Defaults to "Search" */
-@property (copy) NSString *searchDescription;
+@property (nullable, copy) NSString *searchDescription;
 
 /* Specify a localized placeholder string to display in the list view when no
    results are available. */
-@property (copy) NSString *searchResultsPlaceholderString;
+@property (nullable, copy) NSString *searchResultsPlaceholderString;
 
 /* Specify a key path for the string property to display for each object in
    searchResults. By default "description" will be used. */
-@property (copy) NSString *searchResultKeyPath;
+@property (nullable, copy) NSString *searchResultKeyPath;
 
 @end
 
@@ -51,3 +52,5 @@
 - (void)widgetSearch:(NCWidgetSearchViewController *)controller resultSelected:(id)object;
 
 @end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NotificationCenter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NotificationCenter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NotificationCenter.h	2015-08-23 00:27:12.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/NotificationCenter.framework/Headers/NotificationCenter.h	2016-06-06 05:45:38.000000000 +0200
@@ -1,7 +1,7 @@
 /*
  * NotificationCenter.h
  * NotificationCenter.framework
- * Copyright (c) 2013, 2014 Apple Inc. All rights reserved.
+ * Copyright (c) 2013-2015 Apple Inc. All rights reserved.
  */
 
 #import <NotificationCenter/NCWidgetProviding.h>

```