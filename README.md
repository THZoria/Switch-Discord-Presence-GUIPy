# XGC's Mirror - 
As of now this is a 1:1 mirror of the upstream source. It has been forked and put in the XGC Orgs Github as a repository because we feel this is an interesting project and integrating it with our other projects is something we feel looking into will be beneficial, and we'll make any relevant information gleaned available to the community. 


# Switch Discord Presence GUIPy

> A **cross-platform** desktop app (Windows • macOS • Linux) built with **Python + PyQt6** that publishes **Discord Rich Presence** based on what’s running on your **Nintendo Switch** (and **Quest** via overrides).  
> Modern UI, **EN/FR**, **light/dark/auto themes**, auto-reconnect, and integrated logs.
  <a rel="VERSION" href="https://github.com/THZoria/Switch-Discord-Presence-GUIPy">
        <img src="https://img.shields.io/static/v1?label=version&message=1.0.3&labelColor=111111&color=06f&style=for-the-badge" alt="Version">
    </a>

---

<img width="1102" height="839" alt="image" src="https://github.com/user-attachments/assets/7cae28e9-3547-484c-babe-2725d31ef3e3" />

<img width="1102" height="839" alt="image" src="https://github.com/user-attachments/assets/569d04bb-df71-4873-9992-9835e839d389" />

---

## Features

- **Modern GUI (PyQt6)**  
  Clean layout, responsive, with dedicated network thread (smooth UI, no freezes).

- **Live “Now Playing” + Logs**  
  Shows the current title and a rolling log of connection/RPC events.

- **Language Switching (EN/FR)**  
  Toggle instantly without restarting; preferences are saved.

- **Themes: Light / Dark / Auto**  
  Auto follows the OS theme; change on the fly.

- **Auto-Reconnect**  
  Recovers from device or Discord client disconnects gracefully.

- **Home Menu Filter**  
  Optional “Ignore Home Screen (Home Menu)” to avoid posting presence when idle.

- **Overrides Support (Switch & Quest)**  
  Automatically fetches *Override* JSONs to map/rename titles and image keys.

- **Safe Shutdown**  
  Clears presence and closes sockets cleanly when you hit **Stop** or exit.

---

## Requirements

- **Python 3.10+**
- **Discord Desktop** running on the **same machine & user session**
- A **Discord Application ID (Client ID)** from the **Discord Developer Portal**  
  > Do **not** use your User ID. Create an application and use its **Application ID**.
- A Nintendo Switch on CFW with the [SwitchPresence-Rewritten sysmodule](https://github.com/SunResearchInstitute/SwitchPresence-Rewritten)

Optional (for custom images in Rich Presence):
- In your Discord app → **Rich Presence → Art Assets**, add images (keys like `switch` or game-specific keys from overrides).

---

## Installation

```bash
# Clone the repo
git clone https://github.com/<your-account>/<your-repo>.git
cd <your-repo>

# (Recommended) Create & activate a virtual environment
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
source .venv/bin/activate

# Install dependencies
pip install --upgrade pip
pip install PyQt6 pypresence requests
```

## Quick Start

1. **Create a Discord Application**
   - Open the **Discord Developer Portal** → **New Application**.
   - In *General Information*, copy the **Application ID** (aka **Client ID**).

2. **(Optional) Add Art Assets**
   - In your Discord app → **Rich Presence → Art Assets**, add images with keys you plan to use:
     - `switch` (for the Home Menu)
     - Any keys referenced by overrides (or generated as `0` + lowercase hex PID via `iconFromPid`).

3. **Run the app**
   ```bash
   python src/presence_app/main.py
   ```
- Enter Device IP and Discord Client ID (your app’s Application ID).
- Optionally check Ignore Home Screen (Home Menu).
- Click Connect and keep Discord Desktop open.
- Uses TCP port 0xCAFE (51966). Ensure your bridge/server is running and firewalls allow it.

- ## Building Executables

> PyInstaller must run **on each target OS** (no macOS cross-compile from Windows/Linux).

### Windows (x64)
```bash
pip install pyinstaller
pyinstaller --noconfirm --clean ^
  --name "Switch Discord Presence GUIPy" ^
  --windowed --onefile ^
  --icon assets/icons/app.ico ^
  src/presence_app/main.py
# Output: dist/Switch Discord Presence GUIPy.exe
```

### macOS (Intel & Apple Silicon)
```bash
pip install pyinstaller
pyinstaller --noconfirm --clean \
  --name "Switch Discord Presence GUIPy" \
  --windowed \
  --icon assets/icons/app.icns \
  src/presence_app/main.py
# Output: dist/Switch Discord Presence GUIPy.app
```

- Create a DMG (optional):

```bash
brew install create-dmg
create-dmg \
  --volname "Switch Discord Presence GUIPy" \
  --app-drop-link 400 120 \
  --window-size 500 300 \
  --icon-size 96 \
  --icon "Switch Discord Presence GUIPy.app" 120 120 \
  "dist/SwitchDiscordPresenceGUIPy-mac.dmg" "dist/"
```

### Linux (x64)
```bash
pip install pyinstaller
pyinstaller --noconfirm --clean \
  --name "Switch Discord Presence GUIPy" \
  --windowed --onefile \
  src/presence_app/main.py
# Output: dist/Switch Discord Presence GUIPy
# Optional: tar -C dist -czf SwitchDiscordPresenceGUIPy-linux-x64.tar.gz "Switch Discord Presence GUIPy"
```

--- 

## Tips

• Remove --onefile for faster startup (use onedir).
• If a Qt plugin is missing, add: --hidden-import PyQt6.sip
• On macOS, build on each arch (Intel & ARM). PyInstaller doesn’t cross-compile.

--- 

## Troubleshooting

- Client ID is Invalid (4000)
→ You used a User ID. Use the Application ID (Client ID) from your Discord Developer Portal app.
- Discord not detected
→ Ensure Discord Desktop runs in the same user session as this app (don’t mix Admin/non-Admin).
- No images in presence
→ Add Art Assets to your Discord app with correct keys: `switch`, any override `CustomKey`, or `0<pid-hex>`.
- Can’t connect to device
→ Verify IP, port 51966 (0xCAFE), firewall rules, and that your bridge/server is running.
- Unreadable UI (colors)
→ Switch theme under Settings → Theme (Light/Dark/Auto).

--- 

## Suggested Structure

## Suggested Structure

```text
project/
├─ src/presence_app/main.py
├─ assets/icons/app.ico
├─ assets/icons/app.icns
├─ requirements.txt
└─ .github/workflows/build.yml   # optional CI
```

--- 

## Credits

-  pypresence — Discord RPC
-  PyQt6 — UI framework
- SunResearchInstitute — SwitchPresence-Rewritten
- Poka228 - PresenceClient-Rewritten

--- 

## License


# MIT License

Distributed under the MIT License. See LICENSE.

```
Copyright (c) 2025 **THZoria**

Permission is hereby granted, free of charge, to any person obtaining a copy  
of this software and associated documentation files (the "Software"), to deal  
in the Software without restriction, including without limitation the rights  
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell  
copies of the Software, and to permit persons to whom the Software is  
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in  
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR  
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,  
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE  
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER  
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,  
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN  
THE SOFTWARE.
```
