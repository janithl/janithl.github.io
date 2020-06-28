Title: Building Flagitect
Date: 2020-06-28 09:55
Category: General
Tags: code, design
Subtitle: just like a wavin flag

[Flagitect just hit version 1.2.0][1], and so this is a brief introduction
into the technical aspects of how the app is structured.

![Flagitect v1.2.0]({filename}/images/flagitect-1.2.0.jpg)

### Stack

The app is written in React Native (currently version 0.62). There is no navigation
library in use, as the app only needs some modals in the UI at the moment. The editor
uses [react-native-svg][2] to render the flags. [rn-fetch-blob][3] is used to save
the various output files (as a PNG raster or SVG vector inside an HTML) to device storage.

### State Management

State is managed using a [single `useReducer` hook][4] near the root of the component
tree. The store is currently divided into 3 parts with their own reducer functions:
flag, ui, and charges. I found this approach had most of the advantages of Redux (since
the component tree was shallow and I didn't need to use the Context API) when it came to
composing the state and reducers. I use two `useEffect` hooks to store the state in
device storage[^1] whenever it changes, and load it from storage at app start.

### Components

There is your standard `Header`, `Footer`, `Menu` etc. components, and a bunch
of `renderSomething` components that render either charges or divisions. SVG is a
fantastic language for laying out shapes and designs, and I used a bunch of features
including [patterns][5] and [transform][6] to enable various rendering needs.

### Finally

[Flagitect is completely free and open source (MIT licensed)][7], and I'd love for
people using it to submit issues and PRs, or even fork it and make things better. I
found that Google Play was lacking when it came to flag design apps, and so I created
Flagitect in the hope that amateur vexillologists like myself would find it useful. ☺️

[^1]: For this, I'm using [[React Native Async Storage][8] as this functionality has been spun off from the React Native core.

[1]: https://play.google.com/store/apps/details?id=com.flagitect
[2]: https://github.com/react-native-community/react-native-svg
[3]: https://github.com/joltup/rn-fetch-blob
[4]: https://reactjs.org/docs/hooks-reference.html#usereducer
[5]: https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Patterns
[6]: https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/transform
[7]: https://github.com/janithl/Flagitect
[8]: https://github.com/react-native-community/async-storage
