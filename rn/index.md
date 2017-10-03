## DoubleDutch features with React Native

Currently, DoubleDutch developer tools for React Native features are only supported on Mac OS X.

### Prerequisites

- [NodeJS](https://nodejs.org)
- [Yarn](https://yarnpkg.com/en/docs/install)
- [XCode](https://developer.apple.com/xcode/) (to run in iOS simulator)

### Getting Started

1. Install the `doubledutch` command line tools

```
npm i -g @doubledutch/cli
```

2. Create an empty folder for your project and initialize it.

<!--doubledutch feature init my-feature-->
```
cd ~/code/project
doubledutch init
```

3. Run the sample code in the simulator

```
cd ~/code/project/mobile
npm run ios
```

4. Make edits to the code in your favorite editor.
   <a href="https://code.visualstudio.com/"><img alt="Visual Studio Code" src="https://code.visualstudio.com/favicon.ico" height="20" width="20" /></a>
   <a href="https://atom.io/"><img alt="Atom" src="https://atom.io/favicon.ico" height="20" width="20" /></a>
   <a href="https://www.sublimetext.com/"><img alt="Sublime Text" src="https://www.sublimetext.com/favicon.ico" height="20" width="20" /></a>
   
5. Hit `⌘ R` in the simulator to refresh.  `⌘ D` for debugging.

### Reference

See documentation for various DoubleDutch platform components:

- [@doubledutch/rn-client - DoubleDutch React Native client](https://www.npmjs.com/package/@doubledutch/rn-client)
- [@doubledutch/firebase-connector](https://www.npmjs.com/package/@doubledutch/firebase-connector) - Easy realtime backend for your feature
- [@doubledutch/cli - DoubleDutch developer command line interface](https://www.npmjs.com/package/@doubledutch/cli)

