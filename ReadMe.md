# React Native Responsive Dimensions

Responsive height, width and responsive fontSize for your react native components!

The dimensions auto adjust based on the window size (view port) or the screen size of the device 🙌🏽

Support for responsive dimension hooks to help auto-adjust dimensions for devices whose display or screen sizes may change such as foldable phones or browser windows! 😎

---

### Compatible with Expo & React Native Web 🚀

### PRs Welcome 👍✨


- 📦 [Installation](#installation)
- ℹ️ [Usage](#usage)
- 🎣 [Responsive Hooks](#responsive-hooks)
- 💡 [Examples](#examples)
- ✨ [Why Responsive Dimensions?](#why-responsive-dimensions)

## Installation

#npm
```sh
npm install keYa-react-native-responsive-dimensions
```
#yarn
```sh
yarn add keYa-react-native-responsive-dimensions
```

## Usage

While working with mobile devices, there are two kinds of dimensions you will have to focus on

- Window Dimensions ﹣ which is the size of the window / view port on which your app is being displayed
- Screen Dimensions ﹣ this is the total screen dimensions of your device (your app may occupy the entire screen or only a portion of the screen)

### Working with Window Dimensions

```ts
import { StyleSheet } from "react-native";
import {
  responsiveHeight,
  responsiveWidth,
  responsiveFontSize
} from "keYa-react-native-responsive-dimensions";

const styles = StyleSheet.create({
  container: {
    justifyContent: "center",
    height: responsiveHeight(50), // 50% of window height
    width: responsiveWidth(50), // 50% of window width
    alignItems: "center"
  },
  sampleText: {
    fontSize: responsiveFontSize(2) // 2% of total window size
  }
});
```

### Working with Screen Dimensions

```ts
import { StyleSheet } from "react-native";
import {
  responsiveScreenHeight,
  responsiveScreenWidth,
  responsiveScreenFontSize
} from "keYa-react-native-responsive-dimensions";

const styles = StyleSheet.create({
  container: {
    justifyContent: "center",
    height: responsiveScreenHeight(50), // 50% of Screen height
    width: responsiveScreenWidth(50), // 50% of Screen width
    alignItems: "center"
  },
  sampleText: {
    fontSize: responsiveScreenFontSize(2) // 2% of total screen size
  }
});
```

## Responsive hooks

The above responsive dimension methods do not auto update once the value is set. They are suitable for using within `StyleSheet.create` method as the values don't change once set. However, you might want your views to respond to dimension changes such as screen rotation, device folding (in foldable devices) & browser window resizing (react-native-web).

The values set by these hooks auto respond to changes. The following hooks are available for use ﹣

- `useResponsiveHeight`
- `useResponsiveWidth`
- `useResponsiveFontSize`
- `useResponsiveScreenHeight`
- `useResponsiveScreenWidth`
- `useResponsiveScreenFontSize`
- `useDimensionsChange`

### Sample Usage

```tsx
import React from "react";
import { View } from "react-native";
import {
  useResponsiveHeight,
  useResponsiveWidth
} from "keYa-react-native-responsive-dimensions";

const App = () => {
  const height = useResponsiveHeight(25);
  const width = useResponsiveWidth(25);

  return <View style={{ height, width }} />;
};
```

### Reacting to dimension changes with `useDimensionsChange`

`useDimensionsChange` basically calls a function whenever the dimensions update with new window & screen dimensions as arguments. This is a good place to include your layout animations if your UI layout reacts to dimension updates and you want to make the transitions smooth.

```tsx
import React, { useCallback } from "react";
import { View, LayoutAnimation } from "react-native";
import {
  useResponsiveHeight,
  useResponsiveWidth,
  useDimensionsChange
} from "keYa-react-native-responsive-dimensions";

const App = () => {
  const height = useResponsiveHeight(25);
  const width = useResponsiveWidth(25);

  useDimensionsChange(
    useCallback(({ window, screen }) => {
      LayoutAnimation.configureNext(LayoutAnimation.Presets.easeInEaseOut);
    }, [])
  );

  return <View style={{ height, width }} />;
};
```

## Examples

- [Using Responsive Height & Width (snack)][responsive-example]
- [Using the Responsive Hooks (react-native-web)][responsive-hooks-example]

## Why Responsive Dimensions

I built responsive dimensions as a personal tool to tackle some of my problems I face during my everyday app development. You might want to use it if your usecase comes under one of the following scenarios.

- While working with React Native UI (especially animations) there are lots of scenarios that require calculating a certain percentage of the display area.

- If your app supports tablets then you might want to scale some of your fonts & UI Components based on the display size.

- If you are using react-native-web or targetting foldable devices your UI needs to react to the changes in the window dimensions.