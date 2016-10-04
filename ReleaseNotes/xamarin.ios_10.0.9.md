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
using the `xcode8.1` branch, and include some additional IDE integratin tools.

This release is based on our cycle 8 ([XI 10.0.x](https://developer.xamarin.com/releases/ios/xamarin.ios_10/xamarin.ios_10.0/) work, more details and bug fixes can be found on it's release notes.

### iOS 10.1

Minor API additions were made to:
* HomeKit (updated to beta 2)
* MediaPlayer (updated to beta 2)
* PassKit (updated to beta 2)
* StoreKit (not yet available)

### tvOS 10.0.0.2

No API changes were made to the beta release of the SDK shipping with Xcode 8.1 (beta 2).

### watchOS 3.1

Minor API additions were made to:
* HomeKit (updated to beta 2)
* PassKit (updated to beta 2)

### Known Issues

* None specific to Xcode 8.1 and it's SDK;
* Unsolved issues from [XI 10.0.x](https://developer.xamarin.com/releases/ios/xamarin.ios_10/xamarin.ios_10.0/) are listed in the linked release notes.

### API diff

This is a live document so there's no static list to link to. However our [Jenkins bots](https://jenkins.mono-project.com/job/xamarin-macios-pr-builder/) produce this information for every commit that is being built. Pick on based on `master` and look for the **API diff** link on the left column.
