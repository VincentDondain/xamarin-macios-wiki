#SecurityInterface.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SecurityInterface.framework/Headers/SFCertificateTrustPanel.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SecurityInterface.framework/Headers/SFCertificateTrustPanel.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SecurityInterface.framework/Headers/SFCertificateTrustPanel.h	2016-06-26 09:32:06.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SecurityInterface.framework/Headers/SFCertificateTrustPanel.h	2016-07-10 09:01:07.000000000 +0200
@@ -29,10 +29,11 @@
 #if defined (__LP64__)
 	id _reserved_SFCertificateTrustPanel;
 #else
-	IBOutlet NSSplitView *_splitView;		
-	IBOutlet NSTextField *_messageView;		
+    IBOutlet NSStackView *_stackView;
+	IBOutlet NSSplitView *_splitView;
 	IBOutlet NSButton *_saveChangesButton;
-	IBOutlet NSButton *_cancelButton;	
+	IBOutlet NSButton *_cancelButton;
+    IBOutlet NSLayoutConstraint *_discloseContentHeightConstraint;
 	NSString *_defaultMessage;
 	BOOL _saveChanges;
 	id _reserved_SFCertificateTrustPanel;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SecurityInterface.framework/Headers/SFChooseIdentityPanel.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SecurityInterface.framework/Headers/SFChooseIdentityPanel.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SecurityInterface.framework/Headers/SFChooseIdentityPanel.h	2016-05-04 00:21:23.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SecurityInterface.framework/Headers/SFChooseIdentityPanel.h	2016-07-10 09:01:07.000000000 +0200
@@ -30,6 +30,7 @@
 	IBOutlet SFCertificateView *_certificateView;
 	IBOutlet NSButton *_cancelButton;	
 	IBOutlet NSButton *_okButton;	
+    IBOutlet NSLayoutConstraint *_aboveContentHeightConstraint;
 	int _indexOfChosenIdentity;
 	SecCertificateRef _currCertRefDisplayed;
 	NSArray *_identities;

```