# Get Started with Expo

To start creating a mobile app you need to install react-native by using expo framework.


```sh
npx create-expo-app@latest
```

## NativeWind

I am using tailwindcss for styling in the web, and we will use nativewind for react-native.

### Install nativewind:

```sh
npm install nativewind@preview react-native-css react-native-reanimated react-native-safe-area-context
```

### Setup Tailwind CSS

```sh
npm install --dev tailwindcss @tailwindcss/postcss postcss
```

Add tailwind to your postcss configuration by creating a file `postcss.config.mjs`:

```js
export default {
  plugins: {
    "@tailwindcss/postcss": {},
  },
};
```

Then, create a `global.css` inside the app folder on your project:

```css
@import "tailwindcss/theme.css" layer(theme);
@import "tailwindcss/preflight.css" layer(base);
@import "tailwindcss/utilities.css";

@import "nativewind/theme";
```

After that, you will create or modify your metro.config.js file, by doing that you must run `npx expo customize metro.config.js` to create a `metro.config.js` file:

```js
const { getDefaultConfig } = require("expo/metro-config");
const { withNativewind } = require("nativewind/metro");

/** @type {import('expo/metro-config').MetroConfig} */
const config = getDefaultConfig(__dirname);

module.exports = withNativewind(config);
```

Then, import global.css file to your root layout file:

```js
import './global.css'
```

Lastly, override the lightningcss version by forcing `lightningcss` to a specific version in your `package.json`:

```json
{
  "overrides": {
    "lightningcss": "1.30.1"
  }
}
```
