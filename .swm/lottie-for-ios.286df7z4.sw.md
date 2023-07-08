---
id: 286df7z4
title: Lottie for iOS
file_version: 1.1.3
app_version: 1.12.1
---

**View documentation, FAQ, help, examples, and more at** [strongairbnb.io/lottie](http://airbnb.io/lottie)

Lottie is a cross-platform library for iOS, macOS, tvOS, [Android](https://github.com/airbnb/lottie-android), and [Web](https://github.com/airbnb/lottie-web) that natively renders vector-based animations and art in realtime with minimal code.

Lottie loads and renders animations and vectors exported in the bodymovin JSON format. Bodymovin JSON can be created and exported from After Effects with [bodymovin](https://github.com/bodymovin/bodymovin), Sketch with [Lottie Sketch Export](https://github.com/buba447/Lottie-Sketch-Export), and from [Haiku](https://www.haiku.ai/).

Designers can create **and ship** beautiful animations without an engineer painstakingly recreating them by hand. Since the animations are backed by JSON, they are extremely small in size but can be large in complexity! Animations can be played, resized, looped, sped up, slowed down, reversed, and even interactively scrubbed. Lottie can play or loop just a portion of the animation as well, the possibilities are endless! Animations can even be **_changed at runtime_** in various ways! Change the color, position, or any keyframable value!

Here is just a small sampling of the power of Lottie

<br/>

<div align="center"><img src="https://firebasestorage.googleapis.com/v0/b/swimm-dev-content/o/repositories%2FZ2l0aHViJTNBJTNBbG90dGllLWlvcyUzQSUzQXVzZXJ0ZXN0aW5nLXN3aW1t%2Fbe865275-fc9b-4b0c-a384-49011e1617f7.gif?alt=media&token=e079049a-8c2c-47a1-8500-0074dfb301ee" style="width:'50%'"/></div>

<br/>

<div align="center"><img src="https://firebasestorage.googleapis.com/v0/b/swimm-dev-content/o/repositories%2FZ2l0aHViJTNBJTNBbG90dGllLWlvcyUzQSUzQXVzZXJ0ZXN0aW5nLXN3aW1t%2F3f56aab8-7ca2-42dd-babc-91c852bcdbd2.gif?alt=media&token=3dcb37c9-29c0-4ece-9077-c4545504f3b1" style="width:'50%'"/></div>

<br/>

<div align="center"><img src="https://firebasestorage.googleapis.com/v0/b/swimm-dev-content/o/repositories%2FZ2l0aHViJTNBJTNBbG90dGllLWlvcyUzQSUzQXVzZXJ0ZXN0aW5nLXN3aW1t%2Fe970b657-4ee6-4729-8ef8-a0ac7f1cdd7e.gif?alt=media&token=94a11f6d-f110-4451-8304-1682f18d29a2" style="width:'50%'"/></div>

<br/>

<div align="center"><img src="https://firebasestorage.googleapis.com/v0/b/swimm-dev-content/o/repositories%2FZ2l0aHViJTNBJTNBbG90dGllLWlvcyUzQSUzQXVzZXJ0ZXN0aW5nLXN3aW1t%2F76be82bd-c292-4824-922a-84a48a368cda.gif?alt=media&token=c22adc0d-e897-44b1-96d0-ae5bbf0b00e9" style="width:'50%'"/></div>

<br/>

<div align="center"><img src="https://firebasestorage.googleapis.com/v0/b/swimm-dev-content/o/repositories%2FZ2l0aHViJTNBJTNBbG90dGllLWlvcyUzQSUzQXVzZXJ0ZXN0aW5nLXN3aW1t%2F4f3c84ae-0ad0-47ed-b44e-4013aa0b0a36.gif?alt=media&token=3be267ec-93d1-4db6-84cf-c9f1280e3c28" style="width:'50%'"/></div>

<br/>

<br/>

<br/>

## Installing Lottie

Lottie supports [Swift Package Manager](https://www.swift.org/package-manager/), [CocoaPods](https://cocoapods.org/), and [Carthage](https://github.com/Carthage/Carthage) (Both dynamic and static).

### Github Repo

You can pull the [Lottie Github Repo](https://github.com/airbnb/lottie-ios/) and include the `Lottie.xcodeproj` to build a dynamic or static library.

### Swift Package Manager

To install Lottie using [Swift Package Manager](https://github.com/apple/swift-package-manager) you can follow the [tutorial published by Apple](https://developer.apple.com/documentation/xcode/adding_package_dependencies_to_your_app) using the URL for the Lottie repo with the current version:

1.  In Xcode, select “File” → “Add Packages...”

2.  Enter [https://github.com/airbnb/lottie-spm.git](https://github.com/airbnb/lottie-spm.git)

or you can add the following dependency to your `Package.swift`:

```
.package(url: "https://github.com/airbnb/lottie-spm.git", from: "4.2.0")
```

When using Swift Package Manager we recommend using the [lottie-spm](https://github.com/airbnb/lottie-spm) repo instead of the main lottie-ios repo. The main git repository for [lottie-ios](https://github.com/airbnb/lottie-ios) is somewhat large (300+ MB), and Swift Package Manager always downloads the full repository with all git history. The [lottie-spm](https://github.com/airbnb/lottie-spm) repo is much smaller (less than 500kb), so can be downloaded much more quickly.

Instead of downloading the full git history of Lottie and building it from source, the lottie-spm repo just contains a pointer to the precompiled XCFramework included in the [latest lottie-ios release](https://github.com/airbnb/lottie-ios/releases/latest) (typically ~8MB). If you prefer to include Lottie source directly your project, you can directly depend on the main lottie-ios repo by referencing `https://github.com/airbnb/lottie-ios.git` instead.

### CocoaPods

Add the pod to your Podfile:

```
pod 'lottie-ios'
```

And then run:

```
pod install
```

After installing the cocoapod into your project import Lottie with

```
import Lottie
```

### Carthage

Add Lottie to your Cartfile:

```
github "airbnb/lottie-ios" "master"
```

And then run:

```
carthage update
```

In your application targets “General” tab under the “Linked Frameworks and Libraries” section, drag and drop lottie-ios.framework from the Carthage/Build/iOS directory that `carthage update` produced.

### Data collection

The Lottie SDK does not collect any data. We provide this notice to help you fill out [App Privacy Details](https://developer.apple.com/app-store/app-privacy-details/).

## Contributing

We always appreciate contributions from the community. To make changes to the project, you can clone the repo and open `Lottie.xcworkspace`. This workspace includes:

*   the Lottie framework (for iOS, macOS, and tvOS)

*   unit tests and snapshot tests (for iOS, must be run on an iPhone 8 simulator)

*   an Example iOS app that lets you browse and test over 100 sample animations included in the repo

All pull requests with new features or bug fixes that affect how animations render should include snapshot test cases that validate the included changes.

*   To add a new sample animation to the snapshot testing suite, you can add the `.json` file to `Tests/Samples`. Re-run the snapshot tests to generate the new snapshot image files.

*   To update existing snapshots after making changes, you can set `isRecording = true` in `SnapshotTests.swift` `setUp()` method and then re-run the snapshot tests.

The project also includes several helpful commands defined in our [Rakefile](https://github.com/airbnb/lottie-ios/blob/master/Rakefile). To use these, you need to install [Bundler](https://bundler.io/):

```
$ sudo gem install bundle
$ bundle install
```

For example, all Swift code should be formatted according to the [Airbnb Swift Style Guide](https://github.com/airbnb/swift). After making changes, you can reformat the code automatically using [SwiftFormat](https://github.com/nicklockwood/SwiftFormat) and [SwiftLint](https://github.com/realm/SwiftLint) by running `bundle exec rake format:swift`. Other helpful commands include:

```
$ bundle exec rake build:all # builds all targets for all platforms
$ bundle exec rake build:package:iOS # builds the Lottie package for iOS
$ bundle exec rake test:package # tests the Lottie package
$ bundle exec rake format:swift # reformat Swift code based on the Airbnb Swift Style Guide
```

<br/>

This file was generated by Swimm. [Click here to view it in the app](https://swimm-web-app.web.app/repos/Z2l0aHViJTNBJTNBbG90dGllLWlvcyUzQSUzQXVzZXJ0ZXN0aW5nLXN3aW1t/docs/286df7z4).
