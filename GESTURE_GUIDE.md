# Gesture Guide

## Current Gestures

### 1. Swipe Right

**Action:** Move one lane to the right.

The application tracks the primary hand's wrist X coordinate over a short time window. If horizontal movement exceeds the configured threshold, a right lane-change request is queued.

### 2. Swipe Left

**Action:** Move one lane to the left.

It uses the same wrist-history mechanism as the right swipe, with the opposite direction.

### 3. Three Fingers

**Action:** Pause or resume.

The current implementation requires exactly one detected hand and three extended fingers.

The gesture must be held briefly before it triggers.

### 4. Both Hands Raised

**Action:** Quit the current run.

Both hands must be detected and both must have their wrists in the upper region of the camera frame.

The gesture must be held for approximately 1.1 seconds.

A radial progress indicator shows the quit hold.

## Keyboard Fallback

| Key | Action |
|---|---|
| `←` | Lane left |
| `→` | Lane right |
| `Space` | Pause/resume |
| `Esc` | Quit |
| `Enter` | Start/restart |

## Tuning Values

```javascript
const QUIT_HOLD_MS = 1100;
const PAUSE_HOLD_MS = 380;
const SWIPE_WINDOW_MS = 260;
const SWIPE_THRESHOLD = 0.16;
```

Additional gesture state includes a swipe cooldown and a pause cooldown.

## Tips for Reliable Tracking

- Keep the hand clearly visible.
- Avoid very dark lighting.
- Avoid rapid movement directly toward or away from the camera.
- Keep enough distance for the full hand to remain in view.
- Make left/right swipes deliberate.
- Hold the three-finger and both-hands gestures steadily.

## Known Constraint

The current three-finger detection uses landmark geometry rather than a dedicated machine-learning gesture classifier. It is intentionally lightweight but can be affected by hand orientation and landmark accuracy.
