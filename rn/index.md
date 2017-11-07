## DoubleDutch Development Kit

The DoubleDutch development platform supports developing standalone extensions that can be hosted
within the DoubleDutch mobile app. Extensions are written in Javascript using the React Native framework.

## Examples

<table style="border:none;">
<tr>
  <td><img src="https://github.com/AdamLiechty/where-in-the-world/raw/master/samples/bay.jpg" width="250px" alt="Bay Area satellite view" /></td>
  <td><img src="https://github.com/doubledutch/personal-leads/raw/master/personal-leads.png" width="250px" alt="Bay Area satellite view" /></td>
</tr>
<tr>
  <td><a href="https://github.com/AdamLiechty/where-in-the-world">Where in the World?</a></td>
  <td><a href="https://github.com/doubledutch/personal-leads">Personal Leads</a></td>
</tr></table>

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
please submit a request [here](https://customersupport.doubledutch.me/hc/en-us/requests/new).

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

Upon publishing your extension, you will receive a URL to the extension bundle. This URL can be inserted
into a DoubleDutch mobile app as a new menu section in the [CMS](https://cms.doubledutch.me) or
[Studio](https://studio.doubledutch.me) by adding it as a Web View. Simply paste the mobile URL which will
be of the form:

```
https://firebasestorage.googleapis.com/v0/b/bazaar-179323.appspot.com/o/extensions%2F{extension_name}%2F{extension_version}%2Fmobile%2Findex.__platform__.0.46.4.manifest.bundle?module={extension_name}&alt=media#plugin
```

Finally, install your extension to that event using the event ID from the URL in the CMS or Studio:

```bash
doubledutch install [event_id]
```


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
