# A Multi-Platform UI Architecture

## What is a "Platform"?

### Web Platform

Who works on the web platform?
Who works on the web platforms?
Who is confused about me asking these 2 questions?

"The Web Platform" is usually defined as websites or web "apps" that are accessed via a unique HTTP URL.

But what is this?
`old webkit and IE specific CSS`

And what is this?
`responsive web breakpoints`
`touch vs click css`

What is this?
`latest ECMA stuff we use, but doesn't work in a browser when I enter it in the console`

What are these?
`different JS engines and DOM differences`

What is this?
`Web Components written in Rust`

What is this?
`The Tower of Babel` mythical story


Our code, our work, already proves that we have to:

1. write multi-platform code (different browsers, different human-interfaces, etc.)
2. have build tooling that supports our multi-platform targets (Babel saves us all.)

But do we do it intentionally or reactively?
`Important customer reported the site is broken in IE, so let's patch it just for IE users` -- Boomer War Stories

## Desktop

"Web apps, but on desktop"
- Electron, PWAs, etc.
- nativfier & my old blog post from forever ago...and funny side story that I made it to show how ridiculously easy it was to make a "desktop" app from any website...but people just started asking me for updates and fixing issues and is the first moment I actually got paid for OSS because someone wanted a flatpak of it for a linux distro and I made that for them and they subscribed to my Patreon for $1/month...and canceled a few months later. It was the most valuable few dollars I've ever received.

"Mobile apps, but on desktop"
- Android on Windows
- iOS app on Mac

"Desktop apps, but on desktop"
- One-off native platform apps
- React native windows and react native mac

## Mobile

"Web apps, but on mobile"
- HTML5, PhoneGap, the jank of the century

"Mobile apps, but on mobile"
- One-off native platform apps (iOS - Obj-c or Swift, Android - Java or Kotlin)
- (react native)

## Rendering Philosophy

Pause here for a very important distinction and traditional fork in the road.

Do you want to focus on every pixel or do you want to focus on interacting with databases?

Another way to put it -- are you building something highly visual like a 3d game or are you building a UI that basically renders JSON in a great way?

We are going to focus on the latter, because it's what most of us are likely building for a living when we're building applications.

The former is dominated by tools like Unity for building multi-platform games, for example.

Note on Flutter and note on Skia.

## What is "Native"?

Ask the audience

Usually we think of:

- Experience
  - Fast / Performant
  - Feels "at home" and familiar to the user
- Takes advantages of platform features/frameworks
  - Hardware (Interactions, Connectivity modules, other I/O like cameras and haptics)
  - Hardware Acceleration
  - Uses a specific high-level programmings language(s), like Swift for iOS or  
- It's not jank

What is *not* "native"?
- All the exampels we talked about above
- Shove another UI/UX paradigm, from another platform, into a foreign platform
  - HTML5 apps on Mobile; pressing command+r in Slack because it's a web app and watch it take forever to render
- React Native. (lol, just kidding. "The Native in React Native stands for Native.")

OH NO WE GOT TRICKED INTO A REACT NATIVE TALK...AHHHHHH.......
Don't worry, Knut is going to take us all home with his talk on RSC in a few minutes, but bare with me, I want to show you something cool and open your minds to something amazing.

High Level Philosophy of React Native

- Write abstract code that doesn't work ANYWHERE
  - `<View><Text>Hello no world.</Text></View>`
- Bind those abstractions to native elements...
  - `<View>` => `UIView` (iOS) || `android.view.View` (android)
  - `<Text>` => `UILabel` (iOS) || `android.widget.TextView` (android)
- ...and respect the platform specifics while doing that...
  - e.g. [lines 25-102 in `ViewNativeComponent.js`](https://www.meetup.com/reactjs-san-francisco/events/301598787/) are just handling how to abstract and respect the android platform side for a react native <View>
- ...and expose a single UI logic interface to the UI developer

**Switch Component Example**

Very quickly illustrate "respecting the platform" with something as simple as a switch.

Toggle vs. Checkmark

[React Native Switch](https://reactnative.dev/docs/switch)
[React Native Switch -- CODE](https://github.com/facebook/react-native/blob/main/packages/react-native/Libraries/Components/Switch/Switch.js)

## Yeah, But React Native isn't New. This is like intro level stuff, Erik.

Hold my matcha...

So, you might be thinking now...If react native's architecture is already a fully abstracted UI library that simply supplies a couple build targets out-of-the-box already, couldn't I just add more platform targets by defining the platform specific bindings to the common component library interface?

Yes. You pretty much can. And that's what's been going on in the ecosystem the last 5 years.

React native for web -- Twitter
React native for windows -- Do you use office or the start menu?
React native for macOS -- maintained by microsoft lol
React native for AR/VR -- Quest
React native for embedded -- Playstation store, KindleOS...

DEMO
