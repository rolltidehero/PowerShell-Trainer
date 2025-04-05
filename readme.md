# PowerShell Trainer [v0.1.0]

A web-based simulator for practicing PowerShell commands, designed for easy customization and learning.

**Live Demo:** [https://training.hackn.net/powershell](https://training.hackn.net/powershell)

## Features

* **Command Simulation:** Practice running PowerShell commands and see simulated output.
* **Command Library:** Browse commands categorized by module.
* **External Data:** Loads command examples from an external `commands.json` file for easy updates.
* **Favorites System:**
  * Mark commands as favorites (⭐/☆) directly from the list.
  * Add custom commands to your favorites list.
  * Filter the list to show only favorites.
  * Favorites are saved in your browser's `localStorage`.
* **Customization:**
  * Light/Dark theme toggle (☀️/🌙).
  * Adjust Font Family (Mono/Sans), Size (XS-LG), and Weight (Normal/Bold).
  * Toggle behavior options (Auto-clear input, Tooltips, Syntax Highlighting).
* **Data Management:**
  * Import/Export your favorites list via JSON (copy/paste).
  * Import/Export the entire command set via JSON (copy/paste).
* **Regeneration:** Suggests related commands from the same module.
* **Changelog:** View recent changes via the Log (📜) button in the header (opens Settings modal).

## Setup & Usage

**Requirement:** This application **must be hosted on a web server** (like Apache, Nginx, IIS, or a simple development server like Python's `http.server` or Node.js's `http-server`). It cannot be run by simply opening the HTML file directly from your local filesystem (`file://...`) because it needs to fetch the `commands.json` file.

1. **Place Files:** Copy the main HTML file (e.g., `index.html`) and the `commands.json` file into the same directory on your web server.
2. **Access:** Navigate to the HTML file's URL through your web browser (e.g., `http://your-server-address/path/to/index.html`).
3. **Start Practicing:** The application will load the commands from `commands.json` and you can start using the interface.

## Using the Interface

* **Command List (Left Panel):**
  * Use the dropdown to filter commands by **Module** or view your **Favorites**.
  * Click on a command title to copy the command into the input field below the terminal.
  * Click the star icon (⭐/☆) next to a command title to toggle its favorite status. Changes are saved automatically.
* **Terminal (Right Panel):**
  * The top area (`#output`) displays simulated command output. It always uses a dark theme.
  * The bottom area (`#input-area`) contains the input field and action buttons.
  * Type a command in the input field or select one from the list.
  * Click **Run** (▶️) or press `Enter` to simulate execution.
  * Click **Favorite** (⭐) to save the current text in the input field as a custom favorite.
  * Click **Regen** (🔄) to load a different command from the same module as the one currently in the input field.
  * Click **Clear** (🗑️) to clear the terminal output area.
* **Header Controls (Top Right):**
  * **Log (📜):** Opens the Settings modal to view the Changelog section.
  * **Settings (⚙️):** Opens the Settings modal to customize appearance, behavior, and manage data.
  * **Theme (☀️/🌙):** Toggles between light and dark mode for the application interface (excluding the terminal output).
* **Settings Modal (⚙️):**
  * Adjust appearance (Font, Size, Weight).
  * Toggle behaviors (Auto-clear, Tooltips, Syntax Highlighting).
  * Manage Data:
    * **Export Favs/Cmds (📋):** Displays your current favorites or the loaded command set as JSON in a text area for you to copy manually.
    * **Import Favs/Cmds (📤):** Allows you to select a local JSON file (using the structure described below) to import favorites or replace the current command set for the session.
  * **Reset (♻️):** Resets all settings (theme, fonts, options) and clears favorites stored in the browser. It also reloads the command set from the default internal fallback list.
  * **Changelog:** View recent application updates.

## `commands.json` File

This file allows you to easily customize the commands available in the trainer. It must be placed in the same directory as the main HTML file on your web server.

**Structure:**

The file should be a single JSON object where:

* Each **key** is the exact PowerShell command string (lowercase recommended for consistency).
* Each **value** is an object containing:
  * `module` (string): The category or module the command belongs to (e.g., "Defender", "Utility").
  * `title` (string): A user-friendly title for the command.
  * `output` (string): The simulated output to display when the command is "run". Use `\n` for newlines.

**Example Entry:**{

```json
  "get-mpcomputerstatus": {
    "module": "Defender",
    "title": "Check Defender Status",
    "output": "AntivirusEnabled                 : True\nAntispywareEnabled               : True\n..."
  },
  "get-date": {
    "module": "Utility",
    "title": "Get Current Date/Time",
    "output": "Friday, April 4, 2025 11:50:00 PM"
  }
  // Add more commands here following the same structure
}

```
