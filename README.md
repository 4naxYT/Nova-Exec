# 🚀 Nova Executor

**Nova Executor** is a powerful, multi‑API Roblox executor built on the **Quorum API** framework. It provides a modern, feature‑rich interface with Monaco editor integration, script hub, client management, and seamless switching between multiple execution backends.

![Python](https://img.shields.io/badge/Python-3.11%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey)

---

## ✨ Features

- **Multi‑API Support** – Choose between Xeno, Velocity, LX63, and Valex APIs (more coming).
- **Monaco Editor** – Professional code editor with Lua syntax highlighting, auto‑completion, and multi‑tab support.
- **Script Hub** – Browse and execute scripts directly from ScriptBlox.com.
- **Client Manager** – View all running Roblox processes, attach to specific clients, and execute scripts per PID.
- **Auto‑Update** – One‑click update downloads the latest API DLLs from GitHub.
- **Debug Console** – Integrated console with coloured logs and pop‑out window.
- **Customizable UI** – Transparency, colour themes (Dark Contrast / Rose), always‑on‑top mode.
- **System Tray** – Minimise to tray with “Show” and “Exit” options.
- **Notification Sounds** – Optional audio feedback on injection / execution.

---

## 🧩 Supported APIs

| API      | Pattern     | UNC%  | sUNC% | Status               |
|----------|-------------|-------|-------|----------------------|
| **Xeno** | Static      | 90%   | 41%   | 🟡 Downgrade required |
| **Valex**| Instance    | 94%   | 95%   | ⚫ Discontinued       |
| **Bunni**| Instance    | 100%  | 100%  | 🟢 Working (Premium)  |
| **Velocity** | Instance | 99%  | 98%   | 🔴 Down / Patched     |
| **LX63** | Instance    | 96%   | 95%   | 🔴 Down / Patched     |

*Status updates are fetched live from the [API Distributor Info](https://raw.githubusercontent.com/4naxYT/Nova-Exec/refs/heads/main/API%20Distributor%20Info.md) page.*

---

## 📥 Installation

### Prerequisites
- **Windows 10 / 11** (64‑bit)
- **Python 3.11 or higher** (64‑bit) – [Download](https://python.org)
- **7‑Zip** or **UnRAR** (for auto‑updates) – [7‑Zip Download](https://7-zip.org)

### Steps
1. **Clone or download** this repository.
2. **Run the dependency installer** as Administrator:
   ```batch
   cd Main
   setup_dependencies.bat
   ```
3. **Launch Nova Executor**:
   ```batch
   python LaunchUi.py
   ```

> 💡 **First launch** – No APIs are initially present. Go to **Settings → Updates** and click **Check for Updates** to download the latest API DLLs.

---

## 🎮 Usage Guide

### 1. Select API
- Use the dropdown in the sidebar to choose your preferred backend (Xeno, Velocity, etc.).
- The debug console will confirm successful loading.

### 2. Inject
- Click **Inject** to attach to a running Roblox process.
- The status LED turns 🟢 **green** when attached, 🟡 **yellow** during attachment, 🔴 **red** if failed.

### 3. Write / Load Scripts
- Type Lua code directly in the Monaco editor.
- Use **Open Script** to load a `.lua` file from disk.
- Use **Save Script** to save the current editor content.
- The editor supports multiple tabs (native Monaco feature).

### 4. Execute
- Click **Execute** to run the current script.
- If multiple Roblox clients are running, select one in the **Client(s)** tab to execute on that specific PID.

### 5. Script Hub
- Search for scripts by name or browse trending scripts.
- Filters: Universal, Verified, Free/Paid.
- **Execute** – runs the script immediately.
- **Open** – loads the script into the editor without executing.

### 6. Client Management
- The **Client(s)** tab lists all Roblox processes with their PIDs and attach status.
- Select a client via radio button to target script execution.

### 7. Settings
- **Auto‑attach** – automatically inject when Roblox starts.
- **Always on top** – keeps the window above others.
- **UI Transparency** – slider to adjust opacity.
- **Theme** – switch between Dark Contrast and Rose.
- **Folder paths** – set custom workspace and auto‑execute folders.
- **Debug console** – enable / disable the integrated console.
- **Check for Updates** – downloads the latest API DLLs.

### 8. Debug Console
- Displays internal logs, injection status, script execution results, and errors.
- Coloured output: 🔵 INFO, 🟢 SUCCESS, 🔴 ERROR.
- **Pop out** button opens a separate window.
- **Clear** button empties the console.

---

## 🔄 Auto‑Update Mechanism

Nova Executor uses a simple version‑based updater:

1. When you click **Check for Updates**, it fetches `Fetch Commit.txt` from GitHub.
2. Compares the content with your local `Main/Version.txt`.
3. If different, it downloads the four API RAR files (LX3, Velocity, Xeno, Monaco).
4. Extracts them into `Main/Dependencies/` while preserving your `Workspace`, `Auto-Execute`, `Scripts`, and `Settings.json`.
5. Updates `Version.txt` to match the remote version.
6. Notifies you to restart the UI.

---

## 🗂️ Project Structure

```
Nova-Exec/
├── LaunchUi.py                  # Main application
├── requirements.txt             # Python dependencies
├── README.md                    # This file
├── web/
│   ├── index.html               # UI layout
│   ├── style.css                # Styling
│   └── script.js                # Frontend logic
└── Main/
    ├── setup_dependencies.bat   # Dependency installer
    ├── Settings.json            # User configuration
    ├── Version.txt              # Local version (auto‑generated)
    ├── Workspace/               # User scripts
    ├── Auto-Execute/            # Auto‑run scripts on attach
    ├── Scripts/                 # Example scripts
    └── Dependencies/
        ├── Quorum_API(Lx3)/
        ├── Quorum_API(Velocity)/
        ├── Quorum_API(Xeno)/
        └── Quorum_Monaco(Code_EditorAPI)/
```

---

## ❓ Troubleshooting

| Issue | Solution |
|-------|----------|
| **Monaco editor doesn’t load** | Check the iframe path in `web/index.html`. Ensure `Main/Dependencies/Quorum_Monaco(Code_EditorAPI)/Monaco/index.html` exists. |
| **`pythonnet` fails to load DLL** | Run 64‑bit Python. Verify with `python -c "import platform; print(platform.architecture())"`. |
| **Auto‑update fails to extract** | Install 7‑Zip and add it to PATH, or install `unrar`. Restart the app. |
| **Injection fails** | Make sure Roblox is running and the selected API is compatible with the current Roblox version. Check the debug console for error codes. |
| **System tray icon missing** | Install `pystray` correctly (included in `requirements.txt`). The app will still work, but tray functionality may be limited. |

---

## 🛠️ Building from Source (Optional)

If you want to create a standalone `.exe`, use **PyInstaller**:

```bash
pip install pyinstaller
pyinstaller --onefile --windowed --add-data "web;web" LaunchUi.py
```

> ⚠️ The resulting executable will be large (due to Python + dependencies). The recommended usage is running `LaunchUi.py` directly.

---

## 📜 Credits

- **Quorum API** – Provided by KïtKåt & the Quorum Hub team.
- **Monaco Editor** – Microsoft / Salad (discord.gg/YwwFwjetq2).
- **ScriptBlox** – Free script repository.
- **Icons & Design** – Nova Executor UI.

---

## 📄 License

This project is licensed under the **MIT License**. You are free to use, modify, and distribute it, provided you include the original copyright notice.

---

## ⚠️ Disclaimer

Nova Executor is intended for educational purposes only. Use at your own risk. The authors are not responsible for any consequences arising from the misuse of this software. Respect Roblox’s Terms of Service.

---

## 📬 Support & Community

- **GitHub Issues** – Report bugs or request features.
- **Discord** – [Join our server](https://discord.gg/YwwFwjetq2) for help and updates.

---

**Made with ❤️ for the Roblox scripting community.**
