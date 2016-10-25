The **xamarin-macios** wiki is where we keep our documents (release notes, Xcode diff, etc) about **Xamarin.iOS & Xamarin.Mac**.

### Contributing

You already reached our wiki! So you might already know that Xamarin's SDK are open sourced and that you can contribute to them. Some useful resources to help you are:

* our **mailing list**: you can [subscribe](http://lists.dot.net/mailman/listinfo/macios-devel) or read the [archives](http://lists.dot.net/pipermail/macios-devel/);
* our [gitter channel](https://gitter.im/xamarin/xamarin-macios)

Those resources are exclusively available to help you contributing to the Xamarin.iOS/Mac SDKs.


### Release Notes

Here we keep the initial drafts for release notes based on our main work (on master) or in special branches, e.g. `xcode8` tracks the API and tooling changes to support iOS 10, tvOS 10, watchOS 3 and macOS 10.12.

* [Xamarin.iOS 10.3 (master / C9)](https://github.com/xamarin/xamarin-macios/wiki/xamarin.ios_10.3)

Found a typo, an undocumented new feature or a missing bug fix reference ? just create a PR and we'll merge it after review.

Release notes for versions available on our updater channels (alpha / beta or stable) can be found on our web site:

* [Xamarin.iOS Release Notes](https://developer.xamarin.com/releases/ios/)
* [Xamarin.Mac Release Notes](https://developer.xamarin.com/releases/mac/)


### Continuous Builds

You can now download Xamarin.iOS and Xamarin.Mac packages directly from our build bots. They are provided **as-is** and **no** QA or other validations were done on those builds (e.g. builds that failed internal tests are also published)

* [master](https://jenkins.mono-project.com/view/Xamarin.MaciOS/job/xamarin-macios-builds-master/) : our latest bits (that will eventually become C9);
* [cycle8](https://jenkins.mono-project.com/view/Xamarin.MaciOS/job/xamarin-macios-builds-cycle8/) : our current cycle, used to ship Xamarin.Mac 2.10.x (until Sierra support is ready);
* [xcode8.1](https://jenkins.mono-project.com/view/Xamarin.MaciOS/job/xamarin-macios-builds-xcode8.1/) : our support for Xcode 8.1 and the latest SDK (based on xcode8 branch), used to ship Xamarin.iOS 10.2.x;


### Bindings

iOS, tvOS and watchOS are complete for Xcode 8.1, for macOS
please take a look at the [Bindings](https://github.com/xamarin/xamarin-macios/wiki/Bindings) document.