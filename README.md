You can try this on my [Project Test Drive](https://rmdrake.github.io/ryanmdrake/testdrive.html).

# Spin Cycle

A highly interactive, single-file, physics-based decision wheel web application. Perfect for making quick decisions, playing games, or adding a bit of fun to your workflow.

## 🚀 Features

- **Physics-Based Spinning:** Enjoy smooth, realistic rotation with physics-based deceleration.
- **Interactive Wheel:** A dynamic Canvas-driven wheel that scales beautifully to any screen size.
- **Dynamic Text Scaling:** Text inside slices automatically scales its font size to prevent overlap and ensure readability, even with long options or many slices.
- **Responsive Design:**
    - **Desktop:** Side-by-side view (Wheel on the left, Controls on the right).
    - **Mobile:** Stacked layout (Wheel on top, Controls below).
- **Preset System:**
    - **Default Presets:** Comes with "Magic 8-Ball" and "Yes/No" sets.
    - **Custom Presets:** Save your custom lists as named presets.
    - **Import/Export:** Easily share your presets by exporting them as JSON files or importing others' presets.
- **Theme Management:** Switch seamlessly between **Light** and **Dark** modes.
- **Zero Installation:** It's a single HTML file. No dependencies, no installation.

## 🛠 Tech Stack

- **Markup:** HTML5 (Semantic elements, `<dialog>`)
- **Styling:** CSS3 (Custom Properties for theming, Flexbox)
- **Logic:** Vanilla JavaScript (ES6+)
- **Rendering:** HTML5 Canvas API

## 📖 How to Use

### Getting Started
1. Download or save the `spincycle.html` file to your computer.
2. Open the file in any modern web browser (Chrome, Firefox, Safari, Edge).

### Adding Options
- Type your option in the input field in the control panel.
- Press **Enter** or click **Add**.
- To remove an option, click the **X** button next to it.

### Spinning the Wheel
- Click the large **SPIN!** button.
- When the wheel stops, a large overlay will announce the winner.
- Click anywhere on the screen to dismiss the winner overlay.

### Managing Presets
- **To save a custom list:** Type your options, then click **Save Preset** and enter a name in the popup.
- **To use a preset:** Select a preset from the dropdown menu in the "Presets" section.
- **To export presets:** Click **Export** to download a `.json` file containing all your user-created presets.
- **To import presets:** Click **Import**, select a `.json` file, and they will be merged into your list.

### Switching Themes
- Click the **🌓 Mode** button in the top right corner to toggle between Light and Dark themes.

## 🛠 Technical Implementation Details

- **Rendering:** The wheel is rendered using the HTML5 Canvas API to ensure smooth 60fps animations.
- **Physics:** The spin uses a velocity-based approach with an exponential decay (friction) factor to simulate physical deceleration.
- **Persistence:** User settings, custom lists, and presets are stored locally in your browser via `localStorage`.
- **Collision Detection (Winner Logic):** The winning index is calculated by finding which slice's angular range encompasses the 12 o'clock (top) position after accounting for the total rotation.

---
*Made with ❤️ for quick decisions.*
