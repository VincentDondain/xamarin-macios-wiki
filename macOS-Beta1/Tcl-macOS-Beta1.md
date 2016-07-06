#Tcl.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Tcl.framework/Headers/tcl-private/tclInt.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Tcl.framework/Headers/tcl-private/tclInt.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Tcl.framework/Headers/tcl-private/tclInt.h	2010-07-25 12:13:48.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Tcl.framework/Headers/tcl-private/tclInt.h	2016-04-19 04:43:06.000000000 +0200
@@ -843,7 +843,7 @@
 				 * is marked by a unique ClientData tag during
 				 * compilation, and that same tag is used to
 				 * find the variable at runtime. */
-    char name[4];		/* Name of the local variable starts here. If
+    char name[1];		/* Name of the local variable starts here. If
 				 * the name is NULL, this will just be '\0'.
 				 * The actual size of this field will be large
 				 * enough to hold the name. MUST BE THE LAST
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Tcl.framework/Headers/tcl.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Tcl.framework/Headers/tcl.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Tcl.framework/Headers/tcl.h	2010-08-04 19:02:39.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Tcl.framework/Headers/tcl.h	2016-04-19 04:43:06.000000000 +0200
@@ -1124,7 +1124,7 @@
 	int words[1];		/* Multiple integer words for key. The actual
 				 * size will be as large as necessary for this
 				 * table's keys. */
-	char string[4];		/* String for key. The actual size will be as
+	char string[1];		/* String for key. The actual size will be as
 				 * large as needed to hold the key. */
     } key;			/* MUST BE LAST FIELD IN RECORD!! */
 };

```