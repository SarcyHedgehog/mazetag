# Maze Tag 3D

Maze Tag 3D is a multiplayer game built with Three.js for 3D rendering and Multisynq for real-time collaborative gameplay. Players navigate a 3D maze, collect points, and try to avoid being 'It'!

**Playable (with configuration) directly from the `mazetag.html` file.**

**Live Demo:** [https://www.sarcastichedgehog.com]

**Repository:** [https://github.com/SarcyHedgehog/mazetag](https://github.com/SarcyHedgehog/mazetag)

## Gameplay

*   **Objective:** Score points by collecting blue cubes. If you are 'It', tag another player to make them 'It' and steal half their points! The player(s) with the highest score at the end of the round wins.
*   **Controls:**
    *   **Arrow Keys:** Use Left and Right arrow keys to turn your player ball.
    *   **On-Screen Buttons:** Tap the on-screen arrow buttons to turn (for touch devices).
*   **'It' Mechanic:** One player is randomly chosen to be 'It'. 'It' players move slightly faster and have an emissive glow.
*   **Immunity:** After being tagged (and no longer 'It'), or after tagging someone, you become briefly immune to being tagged again (shown by transparency).
*   **Rounds:** Games last for a fixed duration, followed by a short countdown to the next round.

## Running Locally

To run Maze Tag 3D on your local machine:

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/SarcyHedgehog/mazetag.git
    cd mazetag
    ```

2.  **Configure Multisynq Credentials:**
    *   The game requires API credentials to connect to the Multisynq backend. These are stored in a `config.js` file, which is **not** included in the repository (and is listed in `.gitignore`) for security.
    *   You'll find a `config_example.js` file in the repository. **Copy this file to `config.js`:**
        ```bash
        cp config_example.js config.js
        ```
    *   **Edit `config.js`** and replace the placeholder values with your actual Multisynq API Key and App ID.
        ```javascript
        // config.js
        window.APP_CONFIG = {
            API_KEY: "YOUR_MULTISYNQ_API_KEY_HERE", // Replace with your API Key
            APP_ID: "YOUR_MULTISYNQ_APP_ID_HERE"    // Replace with your App ID
        };
        ```
    *   You can obtain an API Key and App ID from https://www.multisynq.io/coder If you don't have one, you might need to register on the Multisynq platform.

3.  **Serve the Game:**
    *   You need to serve `mazetag.html` through a local web server. You **cannot** simply open the HTML file directly in your browser using a `file:///` path due to browser security restrictions (CORS) for JavaScript modules and other requests.
    *   **Using Python (if installed):**
        Navigate to the `mazetag` directory in your terminal and run:
        *   Python 3: `python -m http.server`
        *   Python 2: `python -m SimpleHTTPServer`
        Then open your browser to `http://localhost:8000/mazetag.html`.
    *   **Using VS Code Live Server extension:**
        If you use Visual Studio Code, you can install the "Live Server" extension. Right-click on `mazetag.html` in the explorer and choose "Open with Live Server".
    *   **Other HTTP servers:** Any simple HTTP server will work.

4.  **Play:**
    Open the game in multiple browser tabs or on multiple devices connected to your local network (if your server is accessible) to test the multiplayer functionality.

## Future Improvements

This project is actively being developed. Potential future enhancements include:

*   Adding more detailed textures to the maze and players.
*   Incorporating sound effects for movement, tagging, and cube collection.
*   Further investigation and resolution of any remaining "not turning" issues with player controls.
*   Importing maze layout data from an external file (e.g., `map1.js`) instead of having it hardcoded in `mazetag.html`.
*   Developing a game lobby system to allow players to see and join open game sessions or create new private/public ones.

## Release Notes

### Version 0.70 - (Current Date - e.g., June 18, 2024)

**✨ New Features & Enhancements:**

*   **Mobile Experience - Landscape Mode Enforcement:**
    *   Implemented screen orientation detection for mobile devices.
    *   The game now actively attempts to lock the screen to landscape mode on mobile.
    *   A user-friendly overlay is displayed prompting the user to rotate their device if it's detected in portrait mode, improving playability on phones and tablets.
    *   Initial attempt to enter fullscreen mode on mobile after the first user interaction to provide a more immersive experience (further refinements to fullscreen reliability planned).
*   **QR Code Display Fix:**
    *   Resolved an issue where the Multisynq Widget Dock (containing the QR code for joining sessions) was appearing as an empty white square. The initialization timing of the widget dock has been corrected, and it should now display the QR code reliably.
*   **Improved Input Handling for Turning (from v0.6x series):**
    *   Previous iterations included significant work to make keyboard and on-screen button turning controls more reliable and less prone to losing the player's turning intent.

**🐛 Bug Fixes:**

*   Corrected the initialization of the Multisynq Widget Dock to ensure QR code and stats are displayed.

**🔧 Behind the Scenes:**

*   Adopted a Git branching strategy for development, separating new features and fixes from the main deployable code.
*   Set up an automated deployment pipeline using GitHub Actions to publish changes from the `main` branch to the live GitHub Pages site.
*   Updated `.gitignore` to properly exclude local configuration files and temporary test scripts.

**📝 Known Issues / Next Steps:**

*   Fullscreen mode on mobile devices is not yet consistently hiding all browser UI elements; further investigation and refinement are planned.
*   Continue investigation into any remaining intermittent player turning issues.
*   Begin work on textures, sound effects, and importing maze data from external files.

## Contributing

This is a public repository, and contributions are welcome! If you have ideas for fixes, features, or improvements, please feel free to:

*   Open an issue to discuss your ideas.
*   Fork the repository and submit a pull request with your changes.

## Contact

For any questions or feedback, you can reach out to [jpoole@sarcastichedgehog.com](mailto:jpoole@sarcastichedgehog.com).

---