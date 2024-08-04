---
sidebar_position: 2
---

# Start Simple

In React Motion Router screens are specified as components and passed to a router specific screen component.

## Creating a Stack Router
Assuming you've already installed the stack router via
```bash
npm install @react-motion-router/stack@^1.0.0
```
We then need to instantiate our stack router passing it a screen to start with.
```jsx
// In App.jsx
import React from 'react';
import { Router, Stack } from '@react-motion-router/stack';

function Home() {
  return (
    <div style={{ flex: 1, display: 'flex', justifyContent: 'center', alignItems: 'center' }}>
      <h1>Home</h1>
    </div>
  );
}

function App() {
  return (
    <Router>
      <Stack.Screen path="/" component={Home} />
    </Router>
  );
}

export default App;
```
<!-- Copy and Paste Me -->
<div class="glitch-embed-wrap" style={{ height: '420px', width: '100%' }}>
  <iframe
    src="https://glitch.com/embed/#!/embed/reminiscent-toothsome-toothbrush?path=src/app.jsx&previewSize=100"
    title="reminiscent-toothsome-toothbrush on Glitch"
    allow="geolocation; microphone; camera; midi; encrypted-media; xr-spatial-tracking; fullscreen"
    allowFullScreen
    style={{ height: '100%', width: '100%', border: 0 }}>
  </iframe>
</div>