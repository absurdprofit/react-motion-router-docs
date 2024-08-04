---
sidebar_position: 3
---

# Navigation

Moving between screens can be though of in terms of a normal anchor tag.
```html 
<a href="/posts" />
```
However due to the browser interpreting such a navigation as a cross-document transition, the `<Anchor />` component is implemented for your convenience.

## Push Navigating to a screen
```jsx
import React from 'react';
import { Anchor } from '@react-motion-router/core';

const screenStyle = {
  display: "flex",
  height: "100vh",
  width: "100vw",
  justifyContent: "center",
  alignItems: "center"
}

function Home() {
  return (
    <div style={screenStyle}>
      <div style={{ display: "flex", flexDirection: "column", textAlign: "center", gap: "15px" }}>
        <h1>Home</h1>
        <Anchor href="/posts">Go To Posts</Anchor>
      </div>
    </div>
  );
}
```

We could also use the imperative API via the navigation object that gets passed to your screen as a prop.
```diff
import React from 'react';
import { Anchor } from '@react-motion-router/core';

const screenStyle = {
  display: "flex",
  height: "100vh",
  width: "100vw",
  justifyContent: "center",
  alignItems: "center"
}

- function Home() {
+ function Home({ navigation }) {
   return (
     <div style={screenStyle}>
       <div style={{ display: "flex", flexDirection: "column", textAlign: "center", gap: "15px" }}>
         <h1>Home</h1>
-         <Anchor href="/posts">Go To Posts</Anchor>
+         <button onClick={() => navigation.navigate('/posts')}>Go To Posts</button>
       </div>
     </div>
   );
  } 
```
<u>_However note this pattern may reduce accessibility and can be a pain point for users. Use the `<Anchor />` component where possible._</u>
<!-- Copy and Paste Me -->
<div class="glitch-embed-wrap" style={{ height: '420px', width: '100%' }}>
  <iframe
    src="https://glitch.com/embed/#!/embed/oasis-luminous-pepperberry?path=src/app.jsx&previewSize=100"
    title="oasis-luminous-pepperberry on Glitch"
    allow="geolocation; microphone; camera; midi; encrypted-media; xr-spatial-tracking; fullscreen"
    allowFullScreen
    style={{ height: '100%', width: '100%', border: 0 }}>
  </iframe>
</div>

## Going back
Now you may be wondering how to navigate to a previous route. This is also pretty straightforward via the `<Anchor />` component. The benefit of using the anchor
component in this scenario is the underlying `<a />` will have its href prop set to the previous route's URL. Meaning users get the ability to open the route in a new tab for example.
```jsx
import { Anchor } from '@react-motion-router/core';

// present on every screen
function Nav() {
  return (
    <nav>
      <Anchor goBack>&lt; Go Back</Anchor>
    </nav>
  );
}

function Posts() {
  return (
    <div style={screenStyle}>
      <div style={{ display: "flex", flexDirection: "column", textAlign: "center", gap: "15px" }}>
        <Nav />
        <h1>Posts</h1>
      </div>
    </div>
  );
}
```
A bit of a gotcha here is that go back WILL try to navigate to a previous route even if this means leaving our app. We can conditionally render the anchor based on if we have any previous history entries.
```diff
-  import { Anchor, useNavigation } from '@react-motion-router/core';
+  import { Anchor, useNavigation } from '@react-motion-router/core';

function Nav() {
+  const navigation = useNavigation();
+  if (!navigation.canGoBack()) return <></>;
  return (
    <nav>
      <Anchor goBack>&lt; Go Back</Anchor>
    </nav>
  );
}
```
<!-- Copy and Paste Me -->
<div class="glitch-embed-wrap" style={{ height: '420px', width: '100%' }}>
  <iframe
    src="https://glitch.com/embed/#!/embed/energetic-rightful-amazonsaurus?path=src/app.jsx&previewSize=100"
    title="energetic-rightful-amazonsaurus on Glitch"
    allow="geolocation; microphone; camera; midi; encrypted-media; xr-spatial-tracking; fullscreen"
    allowFullScreen
    style={{ height: '100%', width: '100%', border: 0 }}>
  </iframe>
</div>

## The Navigation object
Note our use of the useNavigation hook in the previous example. This allows us to access the imperative API at any level in the DOM without prop drilling.