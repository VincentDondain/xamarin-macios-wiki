id:23e82b9c-09e5-428f-9aab-196687fb6ebd
title:Xamarin.iOS
version:10.5.0
releasedate:2016-11-01

<div class="note">
	<b>Master / Cycle 10 Daily Builds</b>
	This version of Xamarin.iOS will ship as part of Xamarin **cycle 10** releases.
	Some fixes might be backported into `cycle9` and released long before other parts of `master` becomes public.
</div>

<div class="note">
	<b>Mono TLS Removal:</b>
	This version of Xamarin.iOS (C10) does <b>not</b> ship with the old Mono (managed) SSL/TLS provider, which
	only supported the SSLv3 and TLSv1 standards. TLS support (up to version 1.2) is provided by the 
	newer AppleTLS provider (already the default since XI 9.8 / C7).
</div>

Requirements
============

- The latest features and API requires Xcode 8 and the bundled iOS, tvOS and watchOS SDKs;
- Apple Xcode 8 requires a Mac running OSX 10.11.5 (El Capitan) or newer;

What's New
==========

This release is built upon our [open sourced SDK](https://github.com/xamarin/xamarin-macios),
using the `master` branch, and include some additional IDE integratin tools.

### Memory usage and executable size improvements

We've <a href="https://github.com/xamarin/xamarin-macios/commit/7728c4cd196e605e036ecf531a8bd81072094412">reworked how managed types are registered</a> with the Objective-C runtime, improving executable size and memory usage significantly (for a sample app the executable size decreased by ~200 kb and the memory usage decreased by ~400 kb).

### API diff

This is a live document so there's no static list to link to. However our [Jenkins bots](https://jenkins.mono-project.com/job/xamarin-macios-pr-builder/) produce this information for every commit that is being built. Pick on based on `master` and look for the **API diff** link on the left column.