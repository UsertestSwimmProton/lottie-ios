---
id: r55jzbia
title: Image Provider
file_version: 1.1.3
app_version: 1.12.1
---

Image provider is a protocol that is used to supply images to `AnimationView`.

Some animations require a reference to an image. The image provider loads and provides those images to the `AnimationView`. Lottie includes a couple of prebuilt Image Providers that supply images from a Bundle, or from a FilePath.

Additionally custom Image Providers can be made to load images from a URL, or to Cache images.

### [strongBundleImageProvider](https://airbnb.io/lottie/#/ios?id=bundleimageprovider)

```
public class BundleImageProvider: AnimationImageProvider
```

An `AnimationImageProvider` that provides images by name from a specific bundle. The `BundleImageProvider` is initialized with a bundle and an optional searchPath.

```
/// Create a bundle that loads images from the Main bundle in the subdirectory "AnimationImages"
let imageProvider = BundleImageProvider(bundle: Bundle.main, searchPath: "AnimationImages")
/// Set the provider on an animation.
animationView.imageProvider = imageProvider
```

### [strongFilepathImageProvider](https://airbnb.io/lottie/#/ios?id=filepathimageprovider)

```
public class FilepathImageProvider: AnimationImageProvider
```

An `AnimationImageProvider` that provides images by name from a specific local filepath.

```
/// Create a bundle that loads images from a local URL filepath.
let imageProvider = AnimationImageProvider(filepath: url)
/// Set the provider on an animation.
animationView.imageProvider = imageProvider
```

<br/>

<br/>

This file was generated by Swimm. [Click here to view it in the app](https://swimm-web-app.web.app/repos/Z2l0aHViJTNBJTNBbG90dGllLWlvcyUzQSUzQXVzZXJ0ZXN0aW5nLXN3aW1t/docs/r55jzbia).
