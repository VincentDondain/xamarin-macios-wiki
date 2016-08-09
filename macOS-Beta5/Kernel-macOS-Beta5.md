#Kernel.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h	2016-07-23 01:08:55.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/Availability.h	2016-08-02 01:42:58.000000000 +0200
@@ -363,12 +363,12 @@
  * Use to specify the release that a particular API became available.
  *
  * Platform names:
- *   macosx, ios, tvos, watchos
+ *   macos, ios, tvos, watchos
  *
  * Examples:
- *    __API_AVAILABLE(macosx(10.10))
- *    __API_AVAILABLE(macosx(10.9), ios(10.0))
- *    __API_AVAILABLE(macosx(10.4), ios(8.0), watchos(2.0), tvos(10.0))
+ *    __API_AVAILABLE(macos(10.10))
+ *    __API_AVAILABLE(macos(10.9), ios(10.0))
+ *    __API_AVAILABLE(macos(10.4), ios(8.0), watchos(2.0), tvos(10.0))
  */
 #define __API_AVAILABLE(...) __API_AVAILABLE_GET_MACRO(__VA_ARGS__,__API_AVAILABLE4, __API_AVAILABLE3, __API_AVAILABLE2, __API_AVAILABLE1)(__VA_ARGS__)
 
@@ -379,15 +379,15 @@
  * Use to specify the release that a particular API became unavailable.
  *
  * Platform names:
- *   macosx, ios, tvos, watchos
+ *   macos, ios, tvos, watchos
  *
  * Examples:
  *
- *    __API_DEPRECATED("No longer supported", macosx(10.4, 10.8))
- *    __API_DEPRECATED("No longer supported", macosx(10.4, 10.8), ios(2.0, 3.0), watchos(2.0, 3.0), tvos(9.0, 10.0))
+ *    __API_DEPRECATED("No longer supported", macos(10.4, 10.8))
+ *    __API_DEPRECATED("No longer supported", macos(10.4, 10.8), ios(2.0, 3.0), watchos(2.0, 3.0), tvos(9.0, 10.0))
  *
  *    __API_DEPRECATED_WITH_REPLACEMENT("-setName:", tvos(10.0, 10.4), ios(9.0, 10.0))
- *    __API_DEPRECATED_WITH_REPLACEMENT("SomeClassName", macosx(10.4, 10.6), watchos(2.0, 3.0))
+ *    __API_DEPRECATED_WITH_REPLACEMENT("SomeClassName", macos(10.4, 10.6), watchos(2.0, 3.0))
  */
 #define __API_DEPRECATED(...) __API_DEPRECATED_MSG_GET_MACRO(__VA_ARGS__,__API_DEPRECATED_MSG5,__API_DEPRECATED_MSG4,__API_DEPRECATED_MSG3,__API_DEPRECATED_MSG2,__API_DEPRECATED_MSG1)(__VA_ARGS__)
 #define __API_DEPRECATED_WITH_REPLACEMENT(...) __API_DEPRECATED_REP_GET_MACRO(__VA_ARGS__,__API_DEPRECATED_REP5,__API_DEPRECATED_REP4,__API_DEPRECATED_REP3,__API_DEPRECATED_REP2,__API_DEPRECATED_REP1)(__VA_ARGS__)
@@ -397,7 +397,7 @@
  * Use to specify that an API is unavailable for a particular platform.
  *
  * Example:
- *    __API_UNAVAILABLE(macosx)
+ *    __API_UNAVAILABLE(macos)
  *    __API_UNAVAILABLE(watchos, tvos)
  */
 #define __API_UNAVAILABLE(...) __API_UNAVAILABLE_GET_MACRO(__VA_ARGS__,__API_UNAVAILABLE3,__API_UNAVAILABLE2,__API_UNAVAILABLE1)(__VA_ARGS__)
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h	2016-07-23 01:08:47.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/AvailabilityInternal.h	2016-08-02 01:42:50.000000000 +0200
@@ -17335,13 +17335,14 @@
  * Use to specify the release that a particular API became available.
  *
  * Platform names:
- *   macosx, ios, tvos, watchos
+ *   macos, ios, tvos, watchos
  *
  * Examples:
- *    __API_AVAILABLE(macosx(10.10))
- *    __API_AVAILABLE(macosx(10.9), ios(10.0))
- *    __API_AVAILABLE(macosx(10.4), ios(8.0), watchos(2.0), tvos(10.0))
+ *    __API_AVAILABLE(macos(10.10))
+ *    __API_AVAILABLE(macos(10.9), ios(10.0))
+ *    __API_AVAILABLE(macos(10.4), ios(8.0), watchos(2.0), tvos(10.0))
  */
+#define __API_AVAILABLE_PLATFORM_macos(x) macos,introduced=x
 #define __API_AVAILABLE_PLATFORM_macosx(x) macosx,introduced=x
 #define __API_AVAILABLE_PLATFORM_ios(x) ios,introduced=x
 #define __API_AVAILABLE_PLATFORM_watchos(x) watchos,introduced=x
@@ -17360,16 +17361,17 @@
  * Use to specify the release that a particular API became unavailable.
  *
  * Platform names:
- *   macosx, ios, tvos, watchos
+ *   macos, ios, tvos, watchos
  *
  * Examples:
  *
- *    __API_DEPRECATED("No longer supported", macosx(10.4, 10.8))
- *    __API_DEPRECATED("No longer supported", macosx(10.4, 10.8), ios(2.0, 3.0), watchos(2.0, 3.0), tvos(9.0, 10.0))
+ *    __API_DEPRECATED("No longer supported", macos(10.4, 10.8))
+ *    __API_DEPRECATED("No longer supported", macos(10.4, 10.8), ios(2.0, 3.0), watchos(2.0, 3.0), tvos(9.0, 10.0))
  *
  *    __API_DEPRECATED_WITH_REPLACEMENT("-setName:", tvos(10.0, 10.4), ios(9.0, 10.0))
- *    __API_DEPRECATED_WITH_REPLACEMENT("SomeClassName", macosx(10.4, 10.6), watchos(2.0, 3.0))
+ *    __API_DEPRECATED_WITH_REPLACEMENT("SomeClassName", macos(10.4, 10.6), watchos(2.0, 3.0))
  */
+#define __API_DEPRECATED_PLATFORM_macos(x,y) macos,introduced=x,deprecated=y
 #define __API_DEPRECATED_PLATFORM_macosx(x,y) macosx,introduced=x,deprecated=y
 #define __API_DEPRECATED_PLATFORM_ios(x,y) ios,introduced=x,deprecated=y
 #define __API_DEPRECATED_PLATFORM_watchos(x,y) watchos,introduced=x,deprecated=y
@@ -17394,9 +17396,10 @@
  * Use to specify that an API is unavailable for a particular platform.
  *
  * Example:
- *    __API_UNAVAILABLE(macosx)
+ *    __API_UNAVAILABLE(macos)
  *    __API_UNAVAILABLE(watchos, tvos)
  */
+#define __API_UNAVAILABLE_PLATFORM_macos macos,unavailable
 #define __API_UNAVAILABLE_PLATFORM_macosx macosx,unavailable
 #define __API_UNAVAILABLE_PLATFORM_ios ios,unavailable
 #define __API_UNAVAILABLE_PLATFORM_watchos watchos,unavailable
@@ -17408,5 +17411,24 @@
 #define __API_UNAVAILABLE3(x,y,z) __API_UNAVAILABLE2(x,y) __API_U(z)
 #define __API_UNAVAILABLE_GET_MACRO(_1,_2,_3,NAME,...) NAME
 
+/*
+ * Swift compiler version
+ * Allows for project-agnostic “epochs” for frameworks imported into Swift via the Clang importer, like #if _compiler_version for Swift
+ * Example:
+ *
+ *  #if __swift_compiler_version_at_least(800, 2, 20)
+ *  - (nonnull NSString *)description;
+ *  #else
+ *  - (NSString *)description;
+ *  #endif
+ */
+ 
+#ifdef __SWIFT_COMPILER_VERSION
+    #define __swift_compiler_version_at_least_impl(X, Y, Z, a, b, ...) \
+    __SWIFT_COMPILER_VERSION >= ((X * UINT64_C(1000) * 1000 * 1000) + (Z * 1000 * 1000) + (a * 1000) + b)
+    #define __swift_compiler_version_at_least(...) __swift_compiler_version_at_least_impl(__VA_ARGS__, 0, 0, 0, 0)
+#else
+    #define __swift_compiler_version_at_least(...) 1
+#endif
 
 #endif /* __AVAILABILITY_INTERNAL__ */
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h	2016-07-27 03:48:35.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/hidevent/IOHIDUtility.h	2016-08-06 04:55:18.000000000 +0200
@@ -43,9 +43,11 @@
 
 struct Key {
     uint64_t _value;
-    Key ():_value(0){}
-    Key (uint32_t usagePage, uint32_t usage):_value(((uint64_t)usagePage << 32) | usage) {}
-    Key (uint64_t usageAndUsagePage): _value (usageAndUsagePage) {}
+    bool _modified;
+    Key ():_value(0), _modified(false){}
+    Key (uint32_t usagePage, uint32_t usage):_value(((uint64_t)usagePage << 32) | usage), _modified(false) {}
+    Key (uint32_t usagePage, uint32_t usage, bool modified):_value(((uint64_t)usagePage << 32) | usage), _modified(modified) {}
+    Key (uint64_t usageAndUsagePage): _value (usageAndUsagePage), _modified(false) {}
     friend bool operator==(const Key &lhs, const Key &rhs) {
         return (lhs._value == rhs._value);
     }
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h	2016-07-27 03:59:05.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/IOKit/usb/IOUSBHostFamily.h	2016-08-06 05:01:56.000000000 +0200
@@ -435,6 +435,8 @@
 #define kUSBHostPortPropertyCompanionIndex                      "kUSBCompanionIndex"
 #define kUSBHostPortPropertyDisconnectInterval                  "kUSBDisconnectInterval"
 #define kUSBHostPortPropertyUsbCPortNumber                      "UsbCPortNumber"
+#define kUSBHostPortPropertyCompanionPresent                    "UsbCompanionPortPresent"               // OSNumber used to determine presence of companion properties
+#define kUSBHostPortPropertyCompanionPortNumber                 "UsbCompanionPortNumber"                // OSData  key to set/get the port number of the companion port
 
 #define kUSBHostHubPropertyPowerSupply                          "kUSBHubPowerSupply"                    // OSNumber mA available for downstream ports, 0 for bus-powered
 #define kUSBHostHubPropertyIdlePolicy                           "kUSBHubIdlePolicy"                     // OSNumber ms to be used as device idle policy
@@ -451,6 +453,8 @@
 #define kUSBHostControllerPropertyHighSpeedCompanion            "kUSBHighSpeedCompanion"                // OSBoolean false to disable high-speed companion controller
 #define kUSBHostControllerPropertySuperSpeedCompanion           "kUSBSuperSpeedCompanion"               // OSBoolean false to disable superspeed companion controller
 #define kUSBHostControllerPropertyRevision                      "Revision"                              // OSData    Major/minor revision number of controller
+#define kUSBHostControllerPropertyCompanionPresent              "UsbCompanionControllerPresent"         // OSNumber used to determine presence of companion properties
+#define kUSBHostControllerPropertyCompanionControllerName       "UsbCompanionControllerName"            // OSString  key to set/get the name of the service, i.e. companion controller dictionary.
 
 #define kUSBHostPortPropertyExternalDeviceResetController       "kUSBHostPortExternalDeviceResetController"
 #define kUSBHostPortPropertyExternalDevicePowerController       "kUSBHostPortExternalDevicePowerController"
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_framework.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_framework.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_framework.h	2016-07-27 03:31:05.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_framework.h	2016-08-06 04:23:16.000000000 +0200
@@ -82,6 +82,7 @@
 struct componentname;
 struct cs_blob;
 struct devnode;
+struct exception_action;
 struct flock;
 struct fdescnode;
 struct fileglob;
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_mach_internal.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_mach_internal.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_mach_internal.h	2016-07-27 03:31:06.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_mach_internal.h	2016-08-06 04:23:16.000000000 +0200
@@ -80,6 +80,18 @@
 /* threads */
 void	act_set_astmacf(struct thread *);
 void	mac_thread_userret(struct thread *);
+
+/* exception actions */
+void mac_exc_action_label_init(struct exception_action *action);
+void mac_exc_action_label_inherit(struct exception_action *parent, struct exception_action *child);
+void mac_exc_action_label_destroy(struct exception_action *action);
+int mac_exc_action_label_update(struct task *task, struct exception_action *action);
+void mac_exc_action_label_reset(struct exception_action *action);
+
+void mac_exc_action_label_task_update(struct task *task, struct proc *proc);
+void mac_exc_action_label_task_destroy(struct task *task);
+
+int mac_exc_action_check_exception_send(struct task *victim_task, struct exception_action *action);
 #endif /* MAC */
 
 #endif	/* !_SECURITY_MAC_MACH_INTERNAL_H_ */
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h	2016-07-27 03:31:06.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/security/mac_policy.h	2016-08-06 04:23:16.000000000 +0200
@@ -89,6 +89,7 @@
 struct bpf_d;
 struct cs_blob;
 struct devnode;
+struct exception_action;
 struct fileglob;
 struct ifnet;
 struct inpcb;
@@ -689,6 +690,78 @@
 	struct label *vnodelabel
 );
 /**
+  @brief Access control for sending an exception to an exception action
+  @param crashlabel The crashing process's label
+  @param action Exception action
+  @param exclabel Policy label for exception action
+
+  Determine whether the the exception message caused by the victim
+  process can be sent to the exception action.
+
+  @return Return 0 if the message can be sent, otherwise an
+  appropriate value for errno should be returned.
+*/
+typedef int mpo_exc_action_check_exception_send_t(
+	struct label *crashlabel,
+	struct exception_action *action,
+	struct label *exclabel
+);
+/**
+  @brief Create an exception action label
+  @param action Exception action to label
+  @param exclabel Policy label to be filled in for exception action
+
+  Set the label on an exception action.
+*/
+typedef void mpo_exc_action_label_associate_t(
+	struct exception_action *action,
+	struct label *exclabel
+);
+/**
+  @brief Copy an exception action label
+  @param src Source exception action label
+  @param dest Destination exception action label
+
+  Copy the label information from src to dest.
+  Exception actions are often inherited, e.g. from parent to child.
+  In that case, the labels are copied instead of created fresh.
+*/
+typedef void mpo_exc_action_label_copy_t(
+	struct label *src,
+	struct label *dest
+);
+/**
+ @brief Destroy exception action label
+ @param label The label to be destroyed
+
+ Destroy the label on an exception action.  In this entry point, a
+ policy module should free any internal storage associated with
+ label so that it may be destroyed.
+*/
+typedef void mpo_exc_action_label_destroy_t(
+	struct label *label
+);
+/**
+  @brief Initialize exception action label
+  @param label New label to initialize
+
+  Initialize a label for an exception action.
+*/
+typedef int mpo_exc_action_label_init_t(
+	struct label *label
+);
+/**
+  @brief Update the label on an exception action
+  @param p Process to update the label from
+  @param exclabel Policy label to be updated for exception action
+
+  Update the credentials of an exception action with the given task.
+*/
+typedef void mpo_exc_action_label_update_t(
+	struct proc *p,
+	struct label *exclabel
+);
+/**
   @brief Access control for changing the offset of a file descriptor
   @param cred Subject credential
   @param fg Fileglob structure
@@ -6063,7 +6136,7 @@
  * Please note that this should be kept in sync with the check assumptions
  * policy in bsd/kern/policy_check.c (policy_ops struct).
  */
-#define MAC_POLICY_OPS_VERSION 44 /* inc when new reserved slots are taken */
+#define MAC_POLICY_OPS_VERSION 45 /* inc when new reserved slots are taken */
 struct mac_policy_ops {
 	mpo_audit_check_postselect_t		*mpo_audit_check_postselect;
 	mpo_audit_check_preselect_t		*mpo_audit_check_preselect;
@@ -6208,12 +6281,13 @@
 	mpo_proc_check_expose_task_t		*mpo_proc_check_expose_task;
 	mpo_proc_check_set_host_special_port_t	*mpo_proc_check_set_host_special_port;
 	mpo_proc_check_set_host_exception_port_t *mpo_proc_check_set_host_exception_port;
-	mpo_reserved_hook_t			*mpo_reserved11;
-	mpo_reserved_hook_t			*mpo_reserved12;
-	mpo_reserved_hook_t			*mpo_reserved13;
-	mpo_reserved_hook_t			*mpo_reserved14;
-	mpo_reserved_hook_t			*mpo_reserved15;
-	mpo_reserved_hook_t			*mpo_reserved16;
+	mpo_exc_action_check_exception_send_t	*mpo_exc_action_check_exception_send;
+	mpo_exc_action_label_associate_t	*mpo_exc_action_label_associate;
+	mpo_exc_action_label_copy_t	*mpo_exc_action_label_copy;
+	mpo_exc_action_label_destroy_t	*mpo_exc_action_label_destroy;
+	mpo_exc_action_label_init_t	*mpo_exc_action_label_init;
+	mpo_exc_action_label_update_t	*mpo_exc_action_label_update;
+
 	mpo_reserved_hook_t			*mpo_reserved17;
 	mpo_reserved_hook_t			*mpo_reserved18;
 	mpo_reserved_hook_t			*mpo_reserved19;
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h	2016-07-27 03:31:59.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/kdebug.h	2016-08-06 04:24:13.000000000 +0200
@@ -182,6 +182,7 @@
 #define DBG_MACH_ENERGY_PERF	0xA3 /* Energy/performance resource stats */
 #define DBG_MACH_SYSDIAGNOSE	0xA4	/* sysdiagnose keychord */
 #define DBG_MACH_ZALLOC 	0xA5 	/* Zone allocator */
+#define DBG_MACH_KALLOC		0xA6
 
 /* Codes for Scheduler (DBG_MACH_SCHED) */
 #define MACH_SCHED              0x0     /* Scheduler */
@@ -562,6 +563,7 @@
 /* Kernel Debug Sub Classes for Applications (DBG_APPS) */
 #define DBG_APP_LOGINWINDOW     0x03
 #define DBG_APP_AUDIO           0x04
+#define DBG_APP_SYSTEMUI        0x05
 #define DBG_APP_SIGNPOST        0x0A
 #define DBG_APP_APPKIT          0x0C
 #define DBG_APP_DFR             0x0E
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h	2016-07-27 03:32:03.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/syscall.h	2016-08-06 04:24:18.000000000 +0200
@@ -29,7 +29,7 @@
  * System call switch table.
  *
  * DO NOT EDIT-- this file is automatically generated.
- * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.1.4.1.1/bsd/kern/syscalls.master
+ * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.1.24/bsd/kern/syscalls.master
  */
 
 #ifndef _SYS_SYSCALL_H_
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h	2016-07-27 03:32:04.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Kernel.framework/Headers/sys/sysproto.h	2016-08-06 04:24:18.000000000 +0200
@@ -29,7 +29,7 @@
  * System call switch table.
  *
  * DO NOT EDIT-- this file is automatically generated.
- * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.1.4.1.1/bsd/kern/syscalls.master
+ * created from /Library/Caches/com.apple.xbs/Sources/xnu/xnu-3789.1.24/bsd/kern/syscalls.master
  */
 
 #ifndef _SYS_SYSPROTO_H_

```