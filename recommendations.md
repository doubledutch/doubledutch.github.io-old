# Mobile

## Images

### base-64 encoding workaround
DoubleDutch extensions are deployed as pure Javascript over the air, so directly bundling
images is not supported. A workaround is to base-64 encode smaller images and paste into
your Javascript.

[This site](https://www.base64-image.de/) is good for base-64 encoding images.

Copy the resulting base-64 encoded image into a file containing such encoded images, e.g.

```javascript
// images.js
export const myImage = {uri: 'data:image/png;base64,iVBORw...'}
```

Then, you can use such images in any React Native `Image` component, e.g.

```javascript
import {myImage} from './images'

// In JSX
<Image source={myImage} />
```

# Admin

## Big Screen

Some extensions, especially interactive activities and games in a large room
(e.g. [Trivia](https://github.com/doubledutch/trivia)), launch a "Big Screen"
for display. This is often used to display status, scores, or other information
that should be visible to everyone in the room.

Some recommendations for building such "Big Screens":

1. Make your big screen fill the whole window (`height: 100%; width: 100%;`). When
   displaying on a big screen, set the browser to full screen viewing, to hide the
   URL bar and other UI chrome.
2. Do not use pixels anywhere in any styling.  Prefer `vh` instead
   so that your UI will scale consistently to any screen size. Set a base `font-size`
   for your root element based on `vh` (e.g. `font-size: 4vh;`) and set other
   `font-size`s in children DOM elements relative to that (e.g. `h1 {font-size: 2em;}`).
   Use `vh` for all other dimensions as well, including `margin`, `padding`, `border`, etc.
