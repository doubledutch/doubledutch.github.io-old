# Mobile

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
