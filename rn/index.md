## DoubleDutch Developer Platform

See this [FAQ](../faq) for non-engineers.

The DoubleDutch development platform supports developing standalone extensions that can be hosted
within the DoubleDutch mobile app. Extensions are written in Javascript using the React Native framework.

## Developer Videos

<table>
  <tr>
    <td width="50%"><a href="https://www.youtube.com/watch?v=tz0Fx0YQvS0">1. Getting started<img src="https://img.youtube.com/vi/tz0Fx0YQvS0/hqdefault.jpg" width="400" /></a></td>
    <td width="50%"><a href="https://www.youtube.com/watch?v=LrdQl9G8jYo">2. Using the rn-client library<img src="https://img.youtube.com/vi/LrdQl9G8jYo/hqdefault.jpg" width="400" /></a></td>
  </tr>
</table>


## Examples

<table style="border:none;">
<tr>
  <td><img src="https://dd-bazaar.s3.amazonaws.com/discover_more/personal-leads-1.png" width="250px" alt="Personal Leads" /></td>
  <td><img src="https://dd-bazaar.s3.amazonaws.com/discover_more/question-answer-1.png" width="250px" alt="Question & Answer" /></td>
  <td><img src="https://dd-bazaar.s3.amazonaws.com/discover_more/ice-breaker-espionage-1.png" width="250px" alt="Ice Breaker Espionage" /></td>

</tr>
<tr>
  <td><a href="https://github.com/doubledutch/personal-leads">Personal Leads</a></td>
  <td><a href="https://github.com/doubledutch/question-and-answer">Question & Answer</a></td>
  <td><a href="https://github.com/doubledutch/assassins">Ice Breaker Espionage</a></td>
</tr>
<tr>
    <td><img src="https://github.com/AdamLiechty/where-in-the-world/raw/master/samples/bay.jpg" width="250px" alt="Bay Area satellite view" /></td>
</tr>
<tr>
  <td><a href="https://github.com/AdamLiechty/where-in-the-world">Where in the World?</a></td>
</tr>
</table>

## Developer Environment

The developer environment is currently limited to run on a Mac, though you can perform React Native
development on other platforms that can easily be moved into a DoubleDutch extension at a later point.

You do not need to have a DoubleDutch developer account in order to start developing a new extension.
DoubleDutch extensions can be written and tested locally in the iOS or Android simulator without any
prior contact with DoubleDutch Engineering.

### Prerequisites

- [NodeJS]
- [Yarn] (`brew install yarn`)
- [Watchman] (`brew install watchman`)
- [XCode] (to run in iOS simulator). If you have not used XCode before, be sure to open it once to
  accept the EULA and allow it to install the command line developer tools, or simply run `sudo xcodebuild -license accept`
  from the command line.

### Getting Started

1. Install the `doubledutch` [command line tools][@doubledutch/cli]

```
npm i -g @doubledutch/cli
```

2. Create an empty folder for your project and initialize it.

```
cd ~/code/project
doubledutch init
```

This will populate that folder with a functioning React Native project setup to run as an extension
within the DoubleDutch mobile app. By default the name of the extension will match the current folder
name. In the example above, you can find the Javascript files for your project in
`~/code/project/mobile/src/`. The file `home-view.js` is the root of your extension and has been
initialized with a simple "To do" style sample extension. This sample extension provides examples of
using useful DoubleDutch libraries such as [@doubledutch/rn-client] (used by all DoubleDutch extensions
built with React Native) and [@doubledutch/firebase-connector] (optional integration with Google Cloud
Platform's Firebase suite for easy backend development).

3. Run the sample code in the simulator

```
cd ~/code/project/mobile
npm run ios
```

The Javascript packager will take a couple minutes to initialize the first time. After that, `⌘ R` in the
simulator will quickly hot reload your changes.

4. Make edits to the code in your favorite editor.
   <a href="https://code.visualstudio.com/"><img alt="Visual Studio Code" src="https://code.visualstudio.com/favicon.ico" height="20" width="20" /></a>
   <a href="https://atom.io/"><img alt="Atom" src="https://atom.io/favicon.ico" height="20" width="20" /></a>
   <a href="https://www.sublimetext.com/"><img alt="Sublime Text" src="https://www.sublimetext.com/favicon.ico" height="20" width="20" /></a>
   
5. Hit `⌘ R` in the simulator to refresh.  `⌘ D` for debugging with Chrome developer tools.

### Interacting with the DoubleDutch mobile app

The sample extension that is created for you when you run `doubledutch init` uses the [@doubledutch/rn-client]
library, which serves as a bridge between your extension and the mobile app it is hosted within.

```javascript
import client, { Avatar, TitleBar } from '@doubledutch/rn-client'
```

This bridge allows you to access key information about the current event in the mobile app as well as the
attendee that is logged in:

```javascript
console.log(client.currentUser)
console.log(client.currentEvent)
```

In the simulator, mock data is provided for local development.

### Need a backend for your extension?

[@doubledutch/firebase-connector] provides optional integration with Google Cloud Platform's Firebase suite
for easy backend development. The default configuration provides access to realtime database references
in an environment managed by DoubleDutch. Each event's data is sandboxed, and [@doubledutch/firebase-connector]
provides database references that have various combinations of access control for attendees and event managers.
See [@doubledutch/firebase-connector] for more details.

### Publishing your DoubleDutch extension

Once you have finished development, you will need to be provisioned for a DoubleDutch developer account
before you can publish and install the extension in an event app. To request your developer credentials,
please submit a request [here](https://developer.doubledutch.me/hc/en-us/requests/new).

Next, use your developer credentials to authenticate via the `doubledutch` command line tools:

```bash
doubledutch login
```

You may now publish your extension to DoubleDutch

```bash
doubledutch publish
```

To update an extension you have already published, first update the version number in the `package.json`
file at the root folder of your project. Then, updating an extension is as simple as publishing again.

### Installing your extension to an event in a DoubleDutch event app

An Event Manager in the DoubleDutch CMS can install published extensions via the "Discover More" page in the CMS.
Many extensions are public and appear for all CMS users. Any non-public extension can be installed with the exact
published name of the extension (case-sensitive):

1. Visit the "Discover More" page in the DoubleDutch CMS
2. Click the "Custom DDDP extension" tile at the bottom of the page and click the "Add Custom" button.
3. Enter the exact published extension name.
4. The extension will be installed to the current event in the DoubleDutch CMS and saved as a tile in your personal
   "Discover More" page for later access.

### Reference

See documentation for various DoubleDutch platform components:

- [@doubledutch/rn-client].  DoubleDutch React Native client
- [@doubledutch/firebase-connector].  Easy realtime backend for your extension
- [@doubledutch/cli].  DoubleDutch developer command line interface

[@doubledutch/rn-client]: https://www.npmjs.com/package/@doubledutch/rn-client
[@doubledutch/firebase-connector]: https://www.npmjs.com/package/@doubledutch/firebase-connector
[@doubledutch/cli]: https://www.npmjs.com/package/@doubledutch/cli
[NodeJS]: https://nodejs.org
[Watchman]: http://brewformulas.org/Watchman
[Yarn]: https://yarnpkg.com/en/docs/install
[XCode]: https://developer.apple.com/xcode/
