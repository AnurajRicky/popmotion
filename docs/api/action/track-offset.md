---
title: Track Offset
description: Track the offset of another Action.
category: action
---

# Track Offset

Tracks the offset of another action. Especially useful for tracking pointer input.

For instance, if a `tween` is halfway through a `0` -> `100` transition, and we begin tracking its offset at `50`, `trackOffset` will change from `0` to `50`.

`trackOffset(action, <Action>, props <Object>)`

```javascript
import { trackOffset } from 'popmotion';
```

## Props

- `from <Number>`: Will apply the action offset to this number. (default: `0`)

[...Action](/api/action)

## Methods

[...Action](/api/action)

## Playground

Press "start" and then try dragging the ball around:

```marksy
<Example template="Ball">{`
const ball = document.querySelector('.ball');
const ballRenderer = css(ball);
let pointerTracker;
let pointerOffset;

function startTracking(e) {
  pointerTracker = pointer(e).start();
  pointerOffset = composite({
    x: trackOffset(pointerTracker.x, {
      from: ballRenderer.get('x')
    }),
    y: trackOffset(pointerTracker.y, {
      from: ballRenderer.get('y')
    })
  }, {
    onUpdate: (props) => ballRenderer.set(props)
  }).start();
}

function stopTracking() {
  if (pointerTracker) pointerTracker.stop();
  if (pointerOffset) pointerOffset.stop();
}

ball.addEventListener('mousedown', startTracking);
ball.addEventListener('touchstart', startTracking);
document.addEventListener('mouseup', stopTracking);
document.addEventListener('touchend', stopTracking);
`}</Example>
```
