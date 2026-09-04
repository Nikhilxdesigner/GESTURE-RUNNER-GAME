# Project Report

## Project Title

**Runway — Hand-Tracked Runner**

## 1. Project Overview

Runway is a browser-based three-lane endless runner controlled primarily through hand gestures.

Instead of requiring a traditional keyboard or controller, the application uses a webcam and MediaPipe Hands to interpret hand movement and finger poses as game commands.

## 2. Objective

The objective was to explore how real-time computer vision can be used as an alternative human-computer interaction method for a simple game.

The project combines:

- Browser-based computer vision
- Gesture recognition
- Real-time rendering
- Game-state management
- Keyboard fallback interaction

## 3. Core Interaction

The current interaction model is:

```text
Swipe left/right
      ↓
Lane change

3 fingers held
      ↓
Pause/resume

Both hands raised and held
      ↓
Quit
```

Keyboard controls are retained as a fallback.

## 4. Technologies Used

### Frontend

- HTML
- CSS
- JavaScript

### Graphics

- HTML5 Canvas

### Computer Vision

- MediaPipe Hands

### Delivery

- jsDelivr CDN

## 5. Technical Challenges

### Real-time gesture detection

Raw hand landmarks are continuous coordinates rather than direct commands. The application therefore needs thresholds, timing windows, and cooldowns to turn movement into discrete actions.

### Avoiding accidental inputs

A swipe cooldown and short rolling wrist-history window are used to reduce repeated or accidental lane changes.

### Continuous gameplay

The game loop must update movement, obstacles, collision detection, score, particles, and rendering continuously while remaining responsive to gesture input.

### Camera conditions

Gesture detection depends on the camera being able to clearly see the user's hand. Lighting, distance, occlusion, and movement speed can affect recognition.

## 6. Game Mechanics

The player occupies one of three lanes.

Obstacles spawn randomly and move downward. The game becomes harder over time by increasing movement speed and reducing the obstacle spawn interval.

A collision ends the current run.

The score increases continuously based on elapsed gameplay and also receives an increment when an obstacle successfully passes the player.

## 7. Current Scope

The current version intentionally focuses on a small, self-contained prototype:

- One HTML file
- No backend
- No build process
- No database
- No user accounts
- No external game engine

## 8. Future Development

Possible next stages include:

1. Better gesture classification
2. Calibration and sensitivity settings
3. Persistent high scores
4. Audio
5. Power-ups
6. Additional obstacle types
7. Second-camera support
8. Face-camera overlay
9. Browser screen recording
10. Additional game modes

## 9. Learning Outcome

The project demonstrates the integration of a computer-vision input pipeline with an interactive browser game.

It also provides a practical example of converting continuous sensor data into stable, discrete user controls.
