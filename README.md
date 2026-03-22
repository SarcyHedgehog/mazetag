# MazeTag 3D

A browser-based multiplayer 3D maze game built using **Multisynq (Croquet)** and **Three.js**.

Players join the same room and compete in a shared, real-time maze environment.

--- 

## 🚀 Features

- Real-time multiplayer (Multisynq)
- Deterministic game model (no server required)
- 3D rendering with Three.js
- Multiple maps (generated via Excel)
- Simple lobby system with room creation/join
- Static hosting (GitHub Pages)

---

## 🧭 How It Works

### Lobby (`index.html`)

The lobby handles:
- Map selection
- Creating a new game
- Joining an existing game

When a game starts, the lobby:

1. Combines the room name and selected map:
   ```
   FridayGame_map1
   ```

2. Redirects to:
   ```
   mazetag.html?room=FridayGame_map1&map=map1
   ```

👉 This ensures:
- Each map has its own session
- No risk of players joining the same room with different maps

---

### Game (`mazetag.html`)

The game page:
- Reads `room` and `map` from the URL
- Dynamically loads the correct `mapX.js` file
- Starts the Multisynq session
- Runs the game model and rendering

If a map fails to load, it safely falls back to `map1`.

---

## 🗺️ Maps

Maps are stored as:

```
map1.js
map2.js
...
```

Each file defines:

```js
const MAZE_DATA = [ ... ];
```

Maps are generated from an Excel tool using VBA, which converts cell borders into wall data.

---

### Map List (`maps.js`)

Available maps are defined in:

```js
window.MAZE_MAPS = [
  { id: "map1", title: "Classic Maze", file: "map1.js" },
  { id: "map2", title: "Tighter Maze", file: "map2.js" }
];
```

To add a new map:
1. Generate `mapX.js`
2. Add it to `maps.js`
3. Deploy (no other code changes needed)

---

## 🧠 Architecture

- **Model (Multisynq)** → deterministic game state
- **View (Three.js)** → rendering and controls
- **Session identity** → based on room name (including map)

No central server is required.

---

## 🔧 Deployment

Deployment is handled via GitHub Actions:

- Copies game files to `sarcastichedgehog.com`
- Generates `config.js` from secrets
- Deploys all `map*.js` automatically

---

## 📁 Project Structure

```
index.html         # Lobby (create/join + map select)
mazetag.html       # Game
maps.js            # Map registry
map1.js            # Generated map data
map2.js            # Additional maps
config.js          # Generated at deploy (API key)
```

---

## 🛠️ Future Improvements

- [x] Multiple map support
- [x] Map-aware session separation
- [ ] Extract game logic into separate JS modules
- [ ] Add textures (walls, floors, transparency)
- [ ] Improve mobile controls
- [ ] Add scoring / game modes
- [ ] Map preview in lobby

---

## 🧪 Development

Run locally with VS Code Live Server or similar.

Example:
```
http://localhost:5500/index.html
```

---

## 📜 Notes

- This project is designed to be easily forked and modified
- Maps are intentionally simple to generate and extend
- Multisynq ensures all players remain in sync without a server

---

## 🎮 Credits

Built using:
- Multisynq / Croquet
- Three.js

---

## 🦔

Part of the SarcasticHedgehog experiments.
