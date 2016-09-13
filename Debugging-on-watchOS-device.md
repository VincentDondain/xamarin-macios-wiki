Notes
-----

* Make sure the phone is connected to wifi (same network as the mac).
* Make sure "Debug over WiFi" is enabled for both the watch app project and the watch extension project
* Debugging is _slow_. In my tests it takes ~60 seconds + upload time (depends on the size of the app; calculate approx 60 seconds per 10mb for the watch app (myapp.app/Watch)) to hit a breakpoint at launch.
* It's flaky. If it doesn't work, try again a couple of times.
* Always use the watch charger. Without the charger it's much flakier.

Known issues
------------

* Symptom: the app doesn't launch on the watch (just a spinning wheel)

    This is printed to the device log (the signifant string is **other version in use**):

    Aug 30 13:37:44 WatchA gizmoappd[93] <Notice>: (Error) WatchKit: \<SPGizmoPlugInManager.m __72-[SPGizmoPlugInManager beginUsingExtension:serverIdentifier:completion:]_block_invoke:1120\> could not activate plugin com.xamarin.testapp.watchkitapp.watchkitextension (error:Error Domain=PlugInKit Code=16 "**other version in use**: \<PKPlugin: 0x15da4f80 com.xamarin.testapp.watchkitapp.watchkitextension(${BundleShortVersion}) (guid) 0(0) /private/var/containers/Bundle/Application/(guid)/unified-test-appsrtfh.app/PlugIns/testapp.appex\>" UserInfo={NSLocalizedDescription=**other version in use**: \<PKPlugin: 0x15da4f80 com.xamarin.testapp.watchkitapp.watchkitextension(${BundleShortVersion}) (guid) 0(0) /private/var/containers/Bundle/Application/(guid)/testapp.app/PlugIns/testapp.appex\>})

    Workaround: reboot the watch

When something doesn't work
---------------------------

* Make sure you have the latest versions of everything (Xcode, Xamarin Studio, Xamarin.iOS) installed.
* Reboot everything (watch + phone + mac).
* <a href="https://bugzilla.xamarin.com/enter_bug.cgi?product=iOS">File a bug</a> (see below for information to include in the bug report).

Logs to fetch when filing a bug
-------------------------------

* Execute the following in a terminal:

        echo 123456789 > ~/.mlaunch-verbosity

* Make sure to capture the device log

   * If using watchOS 3, the device log has to be enabled by installing the `sysdiagnose` profile that can be downloaded here: https://developer.apple.com/bug-reporting/profiles-and-logs/?platform=watchos. Follow Apple's Instructions to install it (except that you can just open that page on the phone and download the profile there, no need to email it to yourself).

   * If using watchOS 3, you might also want to capture the device log by invoking mlaunch directly and redirecting to a file (because there will be *a lot* of output once the sysdiagnose profile is installed):

            "/Applications/Xamarin Studio.app/Contents/Resources/lib/monodevelop/AddIns/MonoDevelop.IPhone/mlaunch.app/Contents/MacOS/mlaunch" --logdev --devname "Name of device (UUID works as well)" > mylog.txt

   * You can get the name of the device by executing:

            "/Applications/Xamarin Studio.app/Contents/Resources/lib/monodevelop/AddIns/MonoDevelop.IPhone/mlaunch.app/Contents/MacOS/mlaunch" --listdev

* Reproduce again (you'll get *a lot* of output in the Application Output if things are working correctly).

* Lower the verbosity again:

        rm -f ~/.mlaunch-verbosity
        
* Attach both the device log and the Application Output to the bug (as attachments / gists).