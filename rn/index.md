## DoubleDutch features with React Native

Currently, DoubleDutch developer tools for React Native features are only supported on Mac OS X.

### Prerequisites

- [NodeJS](https://nodejs.org)
- [Yarn](https://yarnpkg.com/en/docs/install)
- [XCode](https://developer.apple.com/xcode/) (to run in iOS simulator)

### Getting Started

1. Install the `doubledutch` command line tools

```
npm i -g doubledutch-cli
```

2. Initialize a new project. This will create a new folder in your current folder.

```
doubledutch feature init my-feature
```

3. Run the sample code in the simulator

```
cd my-feature/mobile
npm run ios
```

4. Make edits to the code in your favorite editor.
   <a href="https://code.visualstudio.com/"><img alt="Visual Studio Code" src="https://code.visualstudio.com/favicon.ico" height="20" width="20" /></a>
   <a href="https://atom.io/"><img alt="Atom" src="https://atom.io/favicon.ico" height="20" width="20" /></a>
   <a href="https://www.sublimetext.com/"><img alt="Sublime Text" src="https://www.sublimetext.com/favicon.ico" height="20" width="20" /></a>
   
5. Hit `⌘ R` in the simulator to refresh.  `⌘ D` for debugging.

### Reference

[Docs](./reference.md)
