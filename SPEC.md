# Car Avoidance Game - Specification Document

## 1. Project Overview

- **Project Name**: Car Avoidance (Penak回避)
- **Project Type**: Browser-based arcade game (HTML5 Canvas + CSS)
- **Core Functionality**: Endless runner-style car avoidance game where player dodges oncoming traffic
- **Target Users**: Casual gamers on mobile and desktop devices

---

## 2. UI/UX Specification

### Layout Structure

**Game Container**
- Max width: 400px (centered on desktop)
- Height: 70vh (min 500px, max 700px)
- Centered horizontally on all screen sizes

**Page Sections**
1. **Start Screen** - Title, high score, start button
2. **Game Screen** - Road, player car, obstacles, score display, speed indicator
3. **Game Over Screen** - Final score, high score, restart button

**Responsive Breakpoints**
- Mobile: < 480px (full width, touch controls visible)
- Desktop: >= 480px (max 400px width, keyboard controls)

### Visual Design

**Color Palette**
- Road gradient: #f0f8ff (top) → #e6f7ff (bottom) - light blue sky feel
- Road surface: #444444 (dark asphalt)
- Road lines: #ffffff (white dashed center line)
- Player car: #ff3333 (bright red) with #cc0000 darker shade
- Obstacle cars: 
  - Type 1: #ffcc00 (yellow)
  - Type 2: #009933 (green)
  - Type 3: #0066cc (blue)
  - Type 4: #9933cc (purple)
- UI Background: #1a1a2e (dark navy)
- UI Text: #ffffff (white)
- Accent: #00d4ff (cyan glow)
- Danger: #ff4444 (red)

**Dark Mode Colors**
- Road: #1a1a2e (dark navy)
- Road lines: #ffd700 (gold)
- Player car: #00ff88 (bright green)
- UI Background: #0d0d1a

**Typography**
- Primary Font: 'Orbitron', sans-serif (futuristic racing feel)
- Fallback: 'Segoe UI', Arial, sans-serif
- Title: 32px, bold, letter-spacing: 2px
- Score: 24px, bold
- Buttons: 18px, bold
- Speed indicator: 14px

**Spacing System**
- Container padding: 20px
- Button padding: 15px 40px
- Element gaps: 15px
- Road margins: 10px from edges

**Visual Effects**
- Road line animation: continuous downward scroll (CSS animation)
- Car shadow: 0 4px 8px rgba(0,0,0,0.3)
- Glow effect on player car: 0 0 15px rgba(255,51,51,0.5)
- Screen shake on collision (CSS keyframes)
- Smooth car movement transitions: 0.1s ease-out
- Speed increase flash: cyan glow pulse
- Button hover: scale(1.05) with glow

### Components

**Player Car**
- Width: 50px, Height: 80px
- Rounded corners (8px)
- Simple car shape with windshield detail
- Left/right movement within road bounds
- Visual states: normal, collision (shake + flash red)

**Obstacle Cars**
- Width: 45-55px (varied)
- Height: 70-90px (varied)
- Same car shape style, different colors
- Spawn from top, move downward

**Road**
- 3-lane appearance (visual only, no hard lanes)
- Animated dashed center lines
- Side barriers (darker strips)

**UI Elements**
- Score display: top-right corner, pill-shaped background
- Speed indicator: top-left corner, shows current speed level
- High score badge: star icon with number
- Mobile controls: left/right buttons (60x60px each)

**Buttons**
- Start Game: "MULAI" - cyan gradient
- Restart: "COBA LAGI" - green gradient
- Toggle Dark Mode: icon button

---

## 3. Functionality Specification

### Core Features

**Player Movement**
- Horizontal movement only (left/right)
- Movement speed: 8px per frame
- Boundary detection: cannot exit road area
- Controls: Arrow keys (desktop), Touch buttons (mobile), Swipe (mobile)

**Obstacle System**
- Spawn interval: starts at 1500ms, decreases with speed
- Spawn position: random X within road bounds
- Movement: downward at current game speed
- Speed increase: every 10 points scored
- Maximum obstacles on screen: 5
- Collision detection: bounding box overlap

**Scoring System**
- +1 point per frame survived (60 points per second base)
- +10 bonus when obstacle passes player
- High score saved to localStorage
- Score display updates in real-time

**Speed/Difficulty**
- Initial speed: 5 (pixels per frame)
- Speed increase: +0.5 every 10 points
- Maximum speed: 15
- Visual indicator shows current speed level

**Game States**
1. START - Show title, high score, start button
2. PLAYING - Active gameplay
3. GAME_OVER - Show final score, high score, restart

### User Interactions

**Desktop Controls**
- Left Arrow: Move car left
- Right Arrow: Move car right
- Space/Enter: Start game / Restart

**Mobile Controls**
- Left button: Move car left
- Right button: Move car right
- Touch swipe: Move car in swipe direction
- Tap buttons: Start game / Restart

### Data Handling

**localStorage**
- Key: 'carAvoidanceHighScore'
- Value: integer (highest score achieved)
- Load on game start
- Save on game over if new high score

### Edge Cases

- Window resize: recalculate road boundaries
- Tab hidden: pause game
- Touch and keyboard simultaneously: both work
- Rapid key presses: smooth handling, no stacking
- Obstacle overlap: prevent spawning too close vertically

---

## 4. Acceptance Criteria

### Visual Checkpoints
- [ ] Game container centered with max 400px width
- [ ] Road has animated moving lines
- [ ] Player car has red color with glow effect
- [ ] Obstacles have varied colors (not all same)
- [ ] Score displays in top-right with pill background
- [ ] Speed indicator visible in top-left
- [ ] Mobile buttons are at least 60x60px
- [ ] Start screen shows title, high score, start button
- [ ] Game over screen shows final score, high score, restart button
- [ ] Dark mode toggle works correctly

### Functional Checkpoints
- [ ] Player moves left/right with arrow keys
- [ ] Player moves left/right with touch buttons
- [ ] Player cannot move outside road boundaries
- [ ] Obstacles spawn from top and move down
- [ ] Speed increases every 10 points
- [ ] Score increments during gameplay
- [ ] Collision stops game and shows game over
- [ ] High score persists after page reload
- [ ] Restart button resets game properly
- [ ] No console errors during gameplay

### Performance Checkpoints
- [ ] Smooth 60fps animation
- [ ] No memory leaks from obstacle creation
- [ ] Touch response under 100ms
- [ ] Works on Chrome, Safari, Firefox mobile
