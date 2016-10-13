id:23e82b9c-09e5-428f-9aab-196687fb6ebd
title:Xamarin.iOS
version:10.0.9
releasedate:2016-10-04

<div class="note">
	<b>Xcode 8.1 beta based builds</b>
	This version of Xamarin.iOS will ship when Xcode 8.1 is released publicly. This might happen before or after our cycle9.
</div>

Requirements
============

- The latest features and API requires Xcode 8.1 and the bundled iOS, tvOS and watchOS SDKs;
- Apple Xcode 8.1 requires a Mac running OSX 10.11.5 (El Capitan) or newer;

What's New
==========

This release is built upon our [open sourced SDK](https://github.com/xamarin/xamarin-macios),
using the `xcode8.1` branch, and include some additional IDE integration tools.

This release is based on our cycle 8 ([XI 10.0.x](https://developer.xamarin.com/releases/ios/xamarin.ios_10/xamarin.ios_10.0/) work, more details and bug fixes can be found on it's release notes.

### iOS 10.1

Minor API additions were made to:
* HomeKit (updated to beta 3)
* MediaPlayer (updated to beta 3)
* PassKit (updated to beta 3)
* StoreKit (updated to beta 3)

### tvOS 10.0.0.2

No API changes were made to the beta release of the SDK shipping with Xcode 8.1 (beta 3).

### watchOS 3.1

Minor API additions were made to:
* HomeKit (updated to beta 3)
* PassKit (updated to beta 3)

### Known Issues

* None specific to Xcode 8.1 and it's SDK;
* Unsolved issues from [XI 10.0.x](https://developer.xamarin.com/releases/ios/xamarin.ios_10/xamarin.ios_10.0/) are listed in the linked release notes.

### Upstream Issues (in Xcode)

* Issue: **"App" May Slow Down Your iPhone**: This happens when a 32bit-only application executes on a 64 bits capable platform, e.g. a i386 build running on a iPhone6 simulator (capable of 64bit). The warning simply means you're not using the optimal build for the platform. This can be normal when testing and, by default, simulator builds are only 32 or 64 bits (to make them faster).

	* Workaround: You can change your project settings to remove the warning. Application submitted to the app store should, in most cases, have both 32 and 64 bits slices or, at your choice, 64 bits only (but 32 bits only applications cannot be submitted anymore).

	* Note: this is a newer version of the **App not optimized for iOS10** warning shown during the iOS 10.0 betas.


### API diff

This is a live document so there's no static list to link to. However our [Jenkins bots](https://jenkins.mono-project.com/job/xamarin-macios-pr-builder/) produce this information for every commit that is being built. Pick on based on `master` and look for the **API diff** link on the left column.
