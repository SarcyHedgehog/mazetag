# MazeTag 3D

A browser-based multiplayer 3D maze game built with **Multisynq (Croquet)** and **Three.js**.

Players join the same room, load the same map, and compete in a shared real-time maze.

---

## Features

- Real-time multiplayer using Multisynq
- Deterministic shared game model
- 3D rendering with Three.js
- Lobby with:
  - map selection
  - create new game
  - join existing game
- Multiple map support
- Variable map sizes
- Excel-based map creation pipeline
- Static hosting / GitHub Pages deployment

---

## How it Works

### Lobby (`index.html`)

The lobby handles:

- selecting a map from `maps.js`
- creating a room
- joining a room by name

The selected map is included in the actual session room name so that different maps cannot accidentally join the same multiplayer session.

Example:

- room entered: `jim`
- selected map: `map2`
- actual session room: `jim_map2`

The lobby then opens:

```text
mazetag.html?room=jim_map2&map=map2
```

This avoids deterministic mismatch bugs where two players might otherwise join the same room while loading different maps.

---

### Game Shell (`mazetag.html`)

`mazetag.html` is now a thin shell.

It is responsible for:

- loading `config.js`
- loading the selected map file dynamically
- defining the import map for Three.js
- providing the HUD / control HTML
- loading the main game module

---

### Main Game Code (`game-main.js`)

The main game logic has been split out of `mazetag.html` into:

```text
game-main.js
```

This makes the project easier to debug and safer to edit.

`game-main.js` now contains:

- constants
- map interpretation
- model logic
- player movement logic
- input handling
- rendering
- session join logic

This was the first step in modularising the project and makes future refactors much easier.

---

## Maps

Maps are stored in files such as:

```text
map1.js
map2.js
map3.js
```

They now export a richer structure:

```js
window.MAP_DATA = {
  name: "Map Name",
  width: 16,
  height: 16,
  cells: [ ... ]
};
```

The game reads:

- `MAP_DATA.name`
- `MAP_DATA.width`
- `MAP_DATA.height`
- `MAP_DATA.cells`

This allows maps to have different sizes.

Older maps using `MAZE_DATA` were previously supported during transition, but current maps should use `MAP_DATA`.

---

## Map Registry (`maps.js`)

Available maps are listed in `maps.js`, for example:

```js
window.MAZE_MAPS = [
  { id: "map1", title: "Classic Maze", file: "map1.js" },
  { id: "map2", title: "Open Arena", file: "map2.js" },
  { id: "map3", title: "Compact 10x10", file: "map3.js" }
];
```

To add a new map:

1. Create the map in Excel
2. Export the JS file
3. Save it as `mapX.js`
4. Add it to `maps.js`

No other code changes should be needed unless the map introduces genuinely new mechanics.

---

## Excel Map Tool

Maps are created in Excel using cell borders.

Current workflow:

- maze starts at `B2`
- width is read from `A4`
- height is read from `A5`
- VBA exports JavaScript map data

The clean export macro writes:

```text
JS_Maze_Output_Clean
```

which you then copy from the formula bar into a `map?.js` file.

This makes it easy to create and iterate on maps without touching game code.

---

## Input Handling

The current movement system supports:

- buffered taps
- held direction input
- repeated turns while holding a direction
- prevention of map/session mismatch

This is still being tuned, but is already much more reliable than the original “exact timing only” approach.

---

## Project Structure

```text
index.html          # Lobby
mazetag.html        # Game shell
game-main.js        # Main game module
maps.js             # Map registry
map1.js             # Map data
map2.js             # Map data
map3.js             # Map data
config.js           # Generated at deploy from secrets
```

---

## Deployment

Deployment is handled via GitHub Actions.

The workflow:

- generates `config.js`
- copies game files into the website repo
- deploys map files
- publishes via the website repository

Because deployment is tied to `main`, feature branches can be used safely for testing and development before merge.

---

## Development Workflow

Recommended workflow:

- `main` = stable / live
- feature branches = work in progress

Typical flow:

1. branch from `main`
2. make and test changes locally
3. push branch
4. open PR
5. merge to `main`
6. deploy runs from `main`

---

## Future Improvements

- [x] Multi-map support
- [x] Map-aware session separation
- [x] Split main game code out of HTML into `game-main.js`
- [x] Variable-sized map data
- [ ] Further modularise game code (`game-model.js`, `game-view.js`, etc.)
- [ ] Wall / floor textures
- [ ] Transparent wall sections / windows
- [ ] Map metadata in lobby (size, style, notes)
- [ ] Better spawn point control
- [ ] Additional gameplay features such as portals

---

## Notes

- The project is intended to be open source and easy to fork
- The Excel map creator is part of that workflow
- Map-specific structure belongs in the map files
- Session options and gameplay toggles generally belong in the lobby rather than the map definition

---

## Credits

Built with:

- Multisynq / Croquet
- Three.js

Part of the SarcasticHedgehog experiments.
