# Architecture

## Overview

Runway is a client-side web application. There is no application backend in the current implementation.

The architecture can be viewed as five layers:

```text
┌──────────────────────┐
│       Webcam         │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│    MediaPipe Hands   │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│  Gesture Processing  │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│     Game State        │
│ IDLE/RUNNING/PAUSED/ │
│ OVER                  │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│   Canvas Game Loop   │
└──────────────────────┘
```

## 1. Camera Layer

The browser camera feeds a video element at approximately 480×360.

MediaPipe receives the video frames through its camera callback.

## 2. Hand Tracking Layer

MediaPipe Hands is configured to detect up to two hands.

The application receives hand landmarks and uses them for:

- Finger extension detection
- Wrist movement
- Raised-hand detection
- Hand count
- Preview visualization

## 3. Gesture Layer

The callback converts raw landmarks into higher-level input state.

### Swipe

The primary hand wrist X coordinate is stored for a short rolling window. If movement exceeds the configured threshold, a lane-change request is queued.

### Pause

Exactly one detected hand with three extended fingers must be held briefly.

### Quit

Two hands must be raised and held for approximately 1.1 seconds. A radial progress indicator communicates the hold progress.

## 4. Game State Layer

The game uses four states:

```text
IDLE
 ↓
RUNNING ↔ PAUSED
 ↓
OVER
```

`requestAnimationFrame()` drives the game while it is running.

## 5. Game Loop

The game loop:

1. Calculates frame delta time.
2. Consumes pending gesture input.
3. Updates the player's target lane.
4. Moves the player smoothly.
5. Increases game speed over time.
6. Spawns obstacles.
7. Moves obstacles.
8. Checks collisions.
9. Updates score.
10. Updates particles.
11. Renders the frame.
12. Requests the next animation frame.

## 6. Rendering

The game uses an HTML5 Canvas.

Rendering includes:

- Three lane road
- Dashed lane dividers
- Obstacles
- Player
- Collision particles
- HUD overlays

The UI around the canvas is implemented with HTML/CSS.

## Design Principle

Gesture processing is decoupled from rendering. The MediaPipe callback updates shared gesture state, while the game loop consumes that state.

This prevents the game logic from being directly tied to the exact rendering frame rate.
