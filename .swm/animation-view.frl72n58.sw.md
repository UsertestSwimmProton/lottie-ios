---
id: frl72n58
title: Animation View
file_version: 1.1.3
app_version: 1.12.1
---

`AnimationView` is a UIView (NSView on macOS) subclass that displays animation content. `AnimationView` offers a number of ways to load, play, and even change animations.

### **Creating Animation Views**

Animation views can be allocated with or without animation data. There are a handful of convenience initializers for initializing with animations.

### **Supplying Images**

`AnimationView` uses `AnimationImageProvider` to retrieve the images for its animation. An image provider can be supplied when the Animation View is initialized, or after by setting its `imageProvider` property. To force an AnimationView to reload its images call `reloadImages()` on the AnimationView.

<br/>

### **Playing Animations**

#### **Time**

There are several methods for playing animations, and portions of animations. Lottie describes Time in three ways:

*   Frame Time - Describes time in a frames per second format. `(Seconds * Framerate)` _eg: 0.5 second is FrameTime 12 when framerate is 24_.

*   Progress Time - Describes time in progress from 0 (the beginning of the animation timeline) to 1 (the end of the animation timeline).

*   Time - Describes time in seconds.

All three can be used to play and set time on an `AnimationView` #

#### **Basic Playing**

```
AnimationView.play(completion: LottieCompletionBlock?)
```

Plays the animation from its current state to the end of its timeline. Calls the completion block when the animation is stopped.

Parameters: : **completion**: A completion block that is called when the animation completes. The block will be passed `true` if the animation completes and `false` if the animation was interrupted. Optional.

Example:

```
starAnimationView.play { (finished) in
/// Animation stopped
}
```

#### **Play with Progress Time**

```
AnimationView.play(fromProgress: AnimationProgressTime?, toProgress: AnimationProgressTime, loopMode: LottieLoopMode?, completion: LottieCompletionBlock?)
```

Plays the animation from a `Progress Time` to a `Progress Time` with options.

Parameters: : **fromProgress**: The start progress of the animation. If `nil` the animation will start at the current progress. (Optional) : **toProgress**: The end progress of the animation. : **loopMode**: The loop behavior of the animation. If `nil` the view's `loopMode` property will be used. (Optional) : **completion**: An optional completion closure to be called when the animation stops. (Optional)

Example:

```
/// Play only the last half of an animation.
animationView.play(fromProgress: 0.5, toProgress: 1)
```

#### **Play with Frame Time**

```
AnimationView.play(fromFrame: AnimationProgressTime?, toFrame: AnimationFrameTime, loopMode: LottieLoopMode?, completion: LottieCompletionBlock?)
```

Plays the animation from a `Frame Time` to a `Frame Time` with options.

Parameters: : **fromFrame**: The start frame of the animation. If `nil` the animation will start at the current frame. (Optional) : **toFrame**: The end frame of the animation. : **loopMode**: The loop behavior of the animation. If `nil` the view's `loopMode` property will be used. (Optional) : **completion**: An optional completion closure to be called when the animation stops. (Optional)

Example:

```
/// Play from frame 24 to 48 of an animation.
animationView.play(fromFrame: 24, toFrame: 48)
```

#### **Play with Marker Names**

```
AnimationView.play(fromMarker: String?, toMarker: String, loopMode: LottieLoopMode?, completion: LottieCompletionBlock?)
```

Plays the animation from a named marker to another marker. Markers are point in time that are encoded into the Animation data and assigned a name. Read more on Markers [stronghere](https://airbnb.io/lottie/#/ios?id=using-markers) ==NOTE==: If markers are not found the play command will exit.

Parameters: : **fromMarker**: The start marker for the animation playback. If `nil` the animation will start at the current progress. (Optional) : **toMarker**: The end marker for the animation playback. : **loopMode**: The loop behavior of the animation. If `nil` the view's `loopMode` property will be used. (Optional) : **completion**: An optional completion closure to be called when the animation stops. (Optional)

Example:

```
/// Play from frame 24 to 48 of an animation.
animationView.play(fromMarker: "ftue1_begin", toMarker: "ftue1_end")
```

#### **Stop**

```
AnimationView.stop()
```

Stops the currently playing animation, if any. The animation view is reset to its start frame. The previous animation's completion block will be closed with `false` Example:

```
animationView.stop()
```

#### **Pause**

```
AnimationView.pause()
```

Pauses the animation in its current state. The previous animation's completion block will be closed with `false` Example:

```
animationView.pause()
```

### **Animation Settings**

`AnimationView` has a variety of settings for controlling playback, and visual state. #

#### **Content Mode**

```
/// iOS
var AnimationView.contentMode: UIViewContentMode { get set }
/// MacOS
var AnimationView.contentMode: LottieContentMode { get set }
```

Describes how the AnimationView should resize and scale its contents.

Options: : **scaleToFill**: Animation scaled to fill the bounds of AnimationView. The animation will be stretched if the aspect of the AnimationView is different than the Animation. : **scaleAspectFit**: Animation will be scaled to fit the AnimationView while preserving its aspect ratio. : **scaleAspectFill**: Animation will be scaled to fill the AnimationView while preserving its aspect ratio. : **topLeft**: Animation will not be scaled. #

#### **Background Behavior**

```
var AnimationView.backgroundBehavior: LottieBackgroundBehavior { get set }
```

Describes the behavior of an AnimationView when the app is moved to the background. (iOS only)

The default is `.pause`

Options: : **stop**: Stop the animation and reset it to the beginning of its current play time. The completion block is called. : **pause**: Pause the animation in its current state. The completion block is called. : **pauseAndRestore**: Pause the animation and restart it when the application moves back to the foreground. The completion block is stored and called when the animation completes. #

#### **Loop Mode**

```
var AnimationView.loopMode: LottieLoopMode { get set }
```

Sets the loop behavior for `play` calls. Defaults to `playOnce` Options: : **playOnce**: Animation is played once then stops. : **loop**: Animation will loop from end to beginning until stopped. : **autoReverse**: Animation will play forward, then backwards and loop until stopped. : **repeat(amount)**: Animation will loop from end to beginning up to _amount_ of times. : **repeatBackwards(amount)**: Animation will play forward, then backwards a _amount_ of times. #

#### **Is Animation Playing**

```
var AnimationView.isAnimationPlaying: Bool { get set }
```

Returns `true` if the animation is currently playing, `false` if it is not. #

#### **Should Rasterize When Idle**

```
var AnimationView.shouldRasterizeWhenIdle: Bool { get set }
```

When `true` the animation view will rasterize its contents when not animating. Rasterizing will improve performance of static animations. ==Note:== this will not produce crisp results at resolutions above the animation's natural resolution.

Defaults to `false` #

#### **Respect Animation Frame Rate**

```
var AnimationView.respectAnimationFrameRate: Bool { get set }
```

When `true` the animation will play back at the framerate encoded in the `Animation` model. When `false` the animation will play at the framerate of the device.

Defaults to `false` #

#### **Animation Speed**

```
var AnimationView.animationSpeed: CGFloat { get set }
```

Sets the speed of the animation playback. Higher speed equals faster time. Defaults to `1` #

#### **Current Progress**

```
var AnimationView.currentProgress: AnimationProgressTime { get set }
```

Sets the current animation time with a Progress Time. Returns the current Progress Time, or the final Progress Time if an animation is in progress. ==Note==: Setting this will stop the current animation, if any. #

#### **Current Time**

```
var AnimationView.currentTime: TimeInterval { get set }
```

Sets the current animation time with a TimeInterval. Returns the current TimeInterval, or the final TimeInterval if an animation is in progress. ==Note==: Setting this will stop the current animation, if any. #

#### **Current Frame**

```
var AnimationView.currentFrame: AnimationFrameTime { get set }
```

Sets the current animation time with a Frame Time. Returns the current Frame Time, or the final Frame Time if an animation is in progress. ==Note==: Setting this will stop the current animation, if any. #

#### **Realtime Frame**

```
var AnimationView.realtimeAnimationFrame: AnimationFrameTime { get }
```

Returns the realtime Frame Time of an AnimationView while an animation is in flight. #

#### **Realtime Progress**

```
var AnimationView.realtimeAnimationProgress: AnimationProgressTime { get }
```

Returns the realtime Progress Time of an AnimationView while an animation is in flight. #

#### **Force Display Update**

```
func AnimationView.forceDisplayUpdate()
```

Forces the AnimationView to redraw its contents.

### **Using Markers**

Markers are a way to describe a point in time by a key name. Markers are encoded into animation JSON. By using markers a designer can mark playback points for a developer to use without having to worry about keeping track of animation frames. If the animation file is updated, the developer does not need to update playback code.

Markers can be used to [strongplayback sections of animation](https://airbnb.io/lottie/#/ios?id=play-with-marker-names), or can be read directly for more advanced use. Both `Animation` and `AnimationView` have methods for reading Marker Times.

#### **Reading Marker Time**

```
/// Animation View Methods
AnimationView.progressTime(forMarker named: String) -> AnimationProgressTime?
AnimationView.frameTime(forMarker named: String) -> AnimationFrameTime?
/// Animation Model Methods
Animation.progressTime(forMarker named: String) -> AnimationProgressTime?
Animation.frameTime(forMarker named: String) -> AnimationFrameTime?
```

Each method returns the time for the marker specified by name. Returns nil if the marker is not found. #

### **Dynamic Animation Properties**

Nearly all properties of a Lottie animation can be changed at runtime using a combination of [strongAnimation Keypaths](https://airbnb.io/lottie/#/ios?id=animation-keypaths) and [strongValue Providers](https://airbnb.io/lottie/#/ios?id=value-providers). Setting a ValueProvider on a keypath will cause the animation to update its contents and read the new Value Provider. In addition, animation properties can be read using `Animation Keypaths`.

#### [strongSetting Dynamic Properties](https://airbnb.io/lottie/#/ios?id=setting-dynamic-properties)

```
AnimationView.setValueProvider(_ valueProvider: AnyValueProvider, keypath: AnimationKeypath)
```

Sets a ValueProvider for the specified keypath. The value provider will be set on all properties that match the keypath.

Parameters : **valueProvider**: The new value provider for the property. : **keypath**: The keypath used to search for properties.

Example:

```
/// A keypath that finds the color value for all `Fill 1` nodes.
let fillKeypath = AnimationKeypath(keypath: "**.Fill 1.Color")
/// A Color Value provider that returns a reddish color.
let redValueProvider = ColorValueProvider(Color(r: 1, g: 0.2, b: 0.3, a: 1))
/// Set the provider on the animationView.
animationView.setValueProvider(redValueProvider, keypath: fillKeypath)
```

#### [strongReading Animation Properties](https://airbnb.io/lottie/#/ios?id=reading-animation-properties)

```
AnimationView.getValue(for keypath: AnimationKeypath, atFrame: AnimationFrameTime?) -> Any?
```

Reads the value of a property specified by the Keypath. Returns nil if no property is found.

Parameters : **for**: The keypath used to search for the property. : **atFrame**: The Frame Time of the value to query. If nil then the current frame is used.

Example:

```
/// A keypath that finds the Position of `Group 1` in `Layer 1`
let fillKeypath = AnimationKeypath(keypath: "Layer 1.Group 1.Transform.Position")
let position = animationView.getValue(for: fillKeypath, atFrame: nil)
/// Returns Vector(10, 10, 0) for currentFrame. 
```

#### [strongLogging Keypaths](https://airbnb.io/lottie/#/ios?id=logging-keypaths)

```
AnimationView.logHierarchyKeypaths()
```

Logs all child keypaths of the animation into the console.

#### [strongAdding Views to Animations](https://airbnb.io/lottie/#/ios?id=adding-views-to-animations)

Custom views can be added to AnimationViews. These views will animate alongside the animation.

#### [strongEnabling and Disabling Animation Nodes](https://airbnb.io/lottie/#/ios?id=enabling-and-disabling-animation-nodes)

`public func setNodeIsEnabled(isEnabled: Bool, keypath: AnimationKeypath)`

Sets the enabled state of all animator nodes found with the keypath search. This can be used to interactively enable / disable parts of the animation. An enabled node affects the render tree, a disabled node will be removed from the render tree.

*   Parameter isEnabled: When true the animator nodes affect the rendering tree. When false the node is removed from the tree.

*   Parameter keypath: The keypath used to find the node(s).

Example

```
// Create an animation view.
let animation = Animation.named("LottieLogo1", subdirectory: "TestAnimations")
// Some time later. Create a keypath to find any node named "Stroke 1"
let keypath1 = AnimationKeypath(keypath: "**.Stroke 1")
// Disable all nodes named Stroke 1, removing them from the current render tree.
animationView.setNodeIsEnabled(isEnabled: false, keypath: keypath1)
// Re-enable all nodes named Stroke 1.
animationView.setNodeIsEnabled(isEnabled: true, keypath: keypath1)
```

#### [strongAdding Subviews](https://airbnb.io/lottie/#/ios?id=adding-subviews)

```
AnimationView.addSubview(_ subview: AnimationSubview, forLayerAt keypath: AnimationKeypath)
```

Searches for the nearest child layer to the first Keypath and adds the subview to that layer. The subview will move and animate with the child layer. Furthermore the subview will be in the child layers coordinate space. ==Note==: if no layer is found for the keypath, then nothing happens.

Parameters : **subview**: The subview to add to the found animation layer. : **keypath**: The keypath used to find the animation layer.

Example:

```
/// A keypath that finds `Layer 1`
let layerKeypath = AnimationKeypath(keypath: "Layer 1")

/// Wrap the custom view in an `AnimationSubview`
let subview = AnimationSubview()
subview.addSubview(customView)

/// Set the provider on the animationView.
animationView.addSubview(subview, forLayerAt: layerKeypath)
```

#### [strongConverting CGRect and CGPoint to Layers](https://airbnb.io/lottie/#/ios?id=converting-cgrect-and-cgpoint-to-layers)

```
/// Converts a rect
AnimationView.convert(_ rect: CGRect, toLayerAt keypath: AnimationKeypath) -> CGRect?
/// Converts a point
AnimationView.convert(_ point: CGPoint, toLayerAt keypath: AnimationKeypath) -> CGPoint?
```

These two methods are used to convert geometry from the AnimationView's coordinate space into the coordinate space of the layer found at Keypath.

If no layer is found, nil is returned

Parameters : **point or rect**: The CGPoint or CGRect in the AnimationView's coordinate space to convert. : **keypath**: The keypath used to find the layer.

<br/>

This file was generated by Swimm. [Click here to view it in the app](https://swimm-web-app.web.app/repos/Z2l0aHViJTNBJTNBbG90dGllLWlvcyUzQSUzQXVzZXJ0ZXN0aW5nLXN3aW1t/docs/frl72n58).
