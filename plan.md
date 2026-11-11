# Project Title: Spin Cycle (Single-File Decision Wheel)

## 1. Overview
A single-file, highly interactive web application featuring a physics-based spinning pie wheel and an editable list of options. The app allows users to input custom text for the slices or use predefined sets via a preset system. It features a responsive layout (side-by-side on desktop, stacked on mobile), persistent storage via `localStorage`, and smooth rotation animations using the Canvas API. Includes a theme toggle for Light and Dark modes.

## 2. Tech Stack
* **Markup:** HTML5 (Semantic elements, `<dialog>` for preset naming).
* **Styling:** CSS3 (Custom Properties for theming, Flexbox for responsive layout).
* **Logic:** Vanilla JavaScript (ES6+).
* **Rendering:** HTML5 Canvas API (for the spinning wheel and slice drawing).

## 3. Requirements List
* **Core Functionality:**
    * A visual pie-chart spinner that rotates with physics-based deceleration.
    * A large overlay text that appears over the wheel to announce the winner upon spin completion.
    * The winning overlay is dismissed by any user interaction (click, touch, or keypress).
    * A "Spin" button positioned centrally below the wheel.
    * An editable list of options on the right side of the screen.
* **UI/UX & Layout:**
    * **Desktop Layout:** Two-pane split screen (Wheel on the left, Editing Panel on the right).
    * **Mobile Layout:** Stacked layout (Wheel on top, Editing Panel on bottom).
    * **Wheel Scaling & Geometry:** 
        * The canvas must dynamically resize to fit the available width and height of its container.
        * **Constraint:** The wheel must remain perfectly circular (1:1 aspect ratio) regardless of the container's aspect ratio to prevent oval distortion.
    * **Theme Management:** A visible toggle to switch between Light and Dark modes.
    * **Editing Panel Structure (Top to Bottom):**
        * Text input + "Add" button (supports 'Enter' key and maintains focus for rapid entry).
        * List of current options with a "Delete (X)" button per item.
        * Preset dropdown menu (Lists default presets first in alphabetical order, followed by user presets in alphabetical order).
        * "Clear All" button (removes current list after user confirmation).
        * "Save Preset" button (opens a dialog/popup to enter a preset name).
        * "Delete Preset" button (removes selected preset after confirmation).
        * "Import" button (imports presets from a JSON file).
        * "Export" button (exports user presets to a JSON file).
* **Data & Preset Management:**
    * **Default Presets:** 
        1. "Magic 8-Ball" (The 20-option list).
        2. "Yes/No" (Two-option list).
    * **User Presets:** Stored in `localStorage` with millisecond-based IDs.
    * **Deduplication:** During Import, presets are merged. If a preset ID already exists, it is not duplicated; only new IDs are added.
    * **Export Schema:** JSON containing `id`, `name`, and `options` array.
    * **Persistence:** `localStorage` handles all user-generated lists and presets.
* **Visual Logic:**
    * Dynamic slice coloring using a high-contrast palette.
    * Color distribution logic to prevent adjacent slices from sharing the same color.

## 4. Implementation Steps

### Step 1: Project Initialization and Theme Setup
* Create a single `index.html` file.
* Implement CSS Custom Properties (Variables) in `:root` for all colors (background, text, accents, etc.).
* Set up a `[data-theme="dark"]` class for theme switching.
* Implement a UI toggle button that switches the `[data-theme]` attribute on the `<html>` element.

### Step 2: Responsive Layout Implementation
* Build the HTML structure with two main containers: `.wheel-container` and `.controls-container`.
* Use CSS Flexbox on the main wrapper to handle layout.
* Implement a Media Query (`@media (max-width: 768px)`) to switch `flex-direction` from `row` to `column`.
* Style the "Spin" button to be centered directly below the canvas.

### Step 3: Core State and Storage Logic
* Implement a `state` object to track `options[]`, `presets[]`, `isSpinning`, and `currentTheme`.
* Implement `storageManager`:
    * `loadState()`: Fetches from `localStorage`.
    * `saveState()`: Saves to `localStorage`.
    * `getPresets()`: Returns a merged list of hardcoded defaults and user-stored presets.
    * `mergeImportedPresets(json)`: Handles logic for adding new presets by ID.
* Define the default "Magic 8-Ball" and "Yes/No" arrays.

### Step 4: Canvas Wheel Rendering Engine
* Initialize the `<canvas>` element.
* Implement a `resizeCanvas()` function that listens to the `window.resize` event.
    * It must calculate the maximum possible diameter (the minimum of `containerWidth` and `containerHeight`) and center the drawing area to ensure the wheel remains a **perfect circle** regardless of the container's aspect ratio.
* Implement a `drawWheel()` function that iterates through `state.options` to draw slices.
* Implement color distribution logic using a predefined high-contrast palette to ensure no two adjacent slices match.

### Step 5: Spin Physics and Winning Overlay
* Implement the `spin()` function using `requestAnimationFrame`.
* Use an exponential decay/easing function to simulate friction/deceleration.
* Implement the Winning Overlay: A `div` with high `z-index` that displays the selected option text.
* Add a global event listener to dismiss the overlay upon any user interaction.

### Step 6: List Management Implementation
* Implement the option input logic:
    * `Add` button functionality.
    * `Enter` key listener on the input field.
    * Logic to clear input and refocus immediately after adding an option.
* Implement "Delete (X)" for individual options.
* Implement "Clear All" with a `window.confirm()` prompt.

### Step 7: Preset Management Implementation
* Implement the Preset Dropdown:
    * Logic to sort defaults first (alphabetical), then user presets (alphabetical).
* Implement the "Save Preset" feature:
    * Use the `<dialog>` element for the name input.
    * Assign a millisecond-based timestamp as the `id`.
* Implement "Delete Preset" with a confirmation prompt.
* Implement "Import" (File API to read JSON) and "Export" (Blob/URL creation to download JSON).

### Step 8: Final Integration and Polish
* Connect the "Spin" button to the physics engine.
* Ensure all UI elements react to the `isSpinning` state (e.g., disabling the spin button).
* Verify that the theme toggle correctly updates all CSS variables and the canvas redraws if necessary.
