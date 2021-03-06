# react-native-gesture-handler

This is an experimental implementation of a new declarative API for gesture handling in react-native. The project is **Android only** at the moment and works by completely replacing current react native touch system, which means that all `Touchable` and `PanResponder` components you may use in your app will not function as expected.

## Installation

I. First install the library from npm repository:
```bash
  npm install --save react-native-gesture-handler
```

II. Update your main activity (or wherever you create an instance of `ReactActivityDelegate`), so that it overrides the method responsible for creating a `ReactRootView` instance. Then use a root view wrapper provided by this library:
```java
// Don't forget imports
import com.facebook.react.ReactActivityDelegate;
import com.facebook.react.ReactRootView;
import com.swmansion.gesturehandler.react.RNGestureHandlerEnabledRootView;

class MainActivity extends ReactActivity {

  // Add the following method to your main activity class
  @Override
  protected ReactActivityDelegate createReactActivityDelegate() {
    return new ReactActivityDelegate(this, getMainComponentName()) {
      @Override
      protected ReactRootView createRootView() {
        return new RNGestureHandlerEnabledRootView(MainActivity.this);
      }
    };
  }
}
```

III. Run:
```bash
  react-native link react-native-gesture-handler
```

IV. You're all set, just run your app with `react-native run-android`

## Examples

If you don't feel like trying it on a real app, but just want to play with the API you can run the example project. Clone the repo, go to the `Example/` folder and run:
```bash
  npm install && react-native run-android
```

You will need to have an android device or emulator connected as well as `react-native-cli` package installed globally.

## API

Here are a gesture recognizers currently available in the package:
 - `TapGestureHandler`
 - `LongPressGestureHandler`
 - `PanGestureHandler`

Whenever you use a native component that should handle touch events you can either wrap it with `NativeViewGestureHandler` or import wrapper component exported by the library instead iporting it from `react-native` package. Here is the list of available components:
 - `Slider`
 - `Switch`
 - `TextInput`
 - `ToolbarAndroid`
 - `ViewPagerAndroid`
 - `WebView`
 - `NativeViewGestureHandler`

Last available element exported by the library is a dictionary of constants used to express the state of the recognizer. Here are the available options:
 - `State.UNDETERMINED`
 - `State.FAILED`
 - `State.BEGAN`
 - `State.CANCELLED`
 - `State.ACTIVE`

#### Common `GestureHandler` properties

 - `shouldCancelWhenOutside`
 - `shouldCancelOthersWhenActivated`
 - `canStartHandlingWithDownEventOnly`
 - `onGestureEvent`
 - `onHandlerStateChange`

#### `LongPressGestureHandler` extra properties

 - `minDurationMs`

#### `PanGestureHandler` extra properties

 - `minDeltaX`
 - `minDeltaY`
 - `minDist`
 - `maxVelocity`


## Roadmap

 - Build two more gesture recognizers: `DoubleTapGestuerHandler`, `FlingGestureHandler`
 - Send out necessary updates to RN core for native animated event support
 - Support for multi-touch events (build `PinchGestureHandler`)
 - iOS port

## Troubleshooting

This project is very experimental so it is not suprising you're seeking help. Try searching over the issues on GitHub [here](https://github.com/kmagiera/react-native-gesture-handler/issues). If you don't find anything that would help feel free to open a new issue!

## Contributing

If you are interested in the project and want to contribute or support it in other ways don't hesitate to contact me! Also all PRs are always welcome!
