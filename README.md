# Runway — Hand-Tracked Runner

> A browser-based three-lane endless runner controlled with real-time hand gestures.

Runway turns a webcam into a game controller. It uses MediaPipe Hands to detect hand landmarks in the browser and converts wrist movement and finger poses into gameplay actions.

## Demo

Add a short gameplay GIF or video here:

```text
![Runway demo](demo.gif)
```

## Features

- Three-lane endless runner
- Real-time webcam hand tracking
- Up to two hands tracked
- Swipe-based lane movement
- Three-finger pause/resume gesture
- Both-hands-raised hold gesture to quit
- Keyboard fallback controls
- Dynamic difficulty progression
- Collision detection and distance scoring
- Hand landmark visualization
- Live tracked-hand count and FPS indicator
- Responsive Canvas-based game UI

## Controls

| Input | Action |
|---|---|
| Swipe right | Move one lane right |
| Swipe left | Move one lane left |
| One hand + 3 extended fingers, held | Pause / resume |
| Both hands raised, held | Quit |
| `←` | Move left |
| `→` | Move right |
| `Space` | Pause / resume |
| `Esc` | Quit |
| `Enter` | Start/restart |

## Tech Stack

- HTML5
- CSS3
- JavaScript
- HTML5 Canvas API
- MediaPipe Hands
- Browser camera APIs
- jsDelivr CDN

## How It Works

```text
Webcam
   ↓
MediaPipe Hands
   ↓
21 hand landmarks
   ↓
Gesture detection
   ↓
Game input state
   ↓
Canvas game loop
   ↓
Player movement / pause / quit
```

The application keeps gesture detection separate from the rendering loop: MediaPipe writes gesture state, while the game loop consumes that state for gameplay.

## Run Locally

The project is intentionally dependency-light and currently consists of a single HTML file.

### Simple option

Open `gesture-runner.html` in a modern browser and allow camera access.

### Recommended option

Serve the project from a local web server:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000/gesture-runner.html
```

Allow camera access when prompted.

## Project Structure

```text
runway-hand-tracked-runner/
├── gesture-runner.html
├── README.md
├── LICENSE
├── .gitignore
├── docs/
│   ├── ARCHITECTURE.md
│   ├── PROJECT_REPORT.md
│   └── GESTURE_GUIDE.md
└── screenshots/
    ├── start-screen.png
    ├── gameplay.png
    └── hand-tracking.png
```

The screenshot files are placeholders for your own captures; add them before publishing if you want them displayed in the README.

## Gesture Detection

Swipe detection tracks wrist X movement over a short rolling time window. A threshold and cooldown reduce repeated triggers.

The three-finger gesture is detected by comparing finger-tip and PIP landmark positions.

The quit gesture requires two detected hands whose wrists are in the upper portion of the camera frame and held there for a short duration.

## Configuration

Useful values in the source include:

```javascript
const QUIT_HOLD_MS = 1100;
const PAUSE_HOLD_MS = 380;
const SWIPE_WINDOW_MS = 260;
const SWIPE_THRESHOLD = 0.16;
```

MediaPipe is configured for a maximum of two hands with detection and tracking confidence thresholds.

## Limitations

- The current project uses one webcam.
- Screen recording is not built into the application.
- Face-camera overlay and multi-camera support are not currently implemented.
- Gesture recognition is landmark/rule based rather than a trained gesture classifier.
- Lighting, camera position, occlusion, and rapid movement can affect recognition.
- MediaPipe assets are currently loaded from jsDelivr, so runtime network access is required.

## Privacy

The application requests camera permission for hand tracking. The current source does not contain a backend, database, account system, or server-side upload feature. Hand tracking runs in the browser.

## Future Ideas

Potential future work:

- Dedicated second camera for face + hand tracking
- Built-in screen recording
- More robust gesture classification
- Calibration screen
- High-score persistence
- Sound and music
- Power-ups and additional obstacle types
- Mobile support
- More game modes

## Credits

Hand tracking is provided by MediaPipe Hands. Browser libraries are loaded through jsDelivr.

## License

See `LICENSE`.
