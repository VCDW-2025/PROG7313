Why choose BlueStacks? 🚀
Big-screen experience 🖥️
See your app on a full monitor, perfect for UI polishing and live demos.

Speedy & smooth ⚡
Hardware-accelerated x86 images make it boot faster and run heavier graphics better than the stock emulator.

Cable-free “device” 🔌➡️📱
Shows up to adb like real hardware, so you can install, debug, and logcat without plugging in a phone.

Touch & sensor tricks 🎯
Built-in tools let you map multi-touch, fake GPS, or flip the “device” without extra scripts.

Google Play out of the box 🛍️
Test in-app purchases, Play licensing, or simple consumer flows without side-loading services.

Cross-platform consistency 🌐
Works on Windows and macOS (Intel & Apple Silicon), so every student can follow the same setup.

Bonus gamer perks 🎮
FPS counter, macro recorder, and key-mapping help when profiling performance-heavy apps.

A quick, flexible desktop Android environment—no phone, no fuss, plenty of power.

---

## 1. Prepare the pieces you need

| What | Why it matters | Quick check |
|------|----------------|-------------|
| **Android Studio installed** | Provides the SDK, `adb`, and IDE | _Help → About_ shows a recent version |
| **BlueStacks 5 (or later)** | Earlier versions expose the ADB bridge differently | _Settings → About_ shows “5.x” or higher |
| **Platform-tools on your PATH** | Lets you run `adb` in any terminal | `.\adb --version` returns a version number |

If `.\adb --version` fails, add the platform-tools directory to your system PATH (e.g., `C:\Users\<you>\AppData\Local\Android\Sdk\platform-tools` on Windows or `$HOME/Android/Sdk/platform-tools` on macOS/Linux).

---

## 2. Enable ADB inside BlueStacks (one-time)

1. **Launch BlueStacks** and wait until the home screen has fully loaded.  
2. Click the **gear icon (Settings)** on the side toolbar.  
3. Choose **Preferences** (left menu).  
4. Under *Developer Mode*, toggle **“Enable Android Debug Bridge (ADB)”** **ON**.  
5. A **port number** appears in the help text—usually `5555`, but note the exact value (e.g., `5557`, `5558`, etc.).  
6. Close the Settings panel; BlueStacks is now listening on `127.0.0.1:<port>`.

> **Tip:** If you later disable and re-enable ADB, the port may change—always re-check.

---

## 3. Connect from your desktop to BlueStacks

Open **Command Prompt (Windows)** or **Terminal (macOS/Linux)**.

```bash
# Replace 5555 with the port you saw in step 2-5
.\adb connect 127.0.0.1:5555
```

A successful response looks like:

```
connected to 127.0.0.1:5555
```

If you see `cannot connect to 127.0.0.1:5555`, verify:

* BlueStacks is still running.  
* The port matches the one shown in BlueStacks.  
* No firewall or VPN is blocking local (loopback) traffic.

---

## 4. Confirm the link

```bash
.\adb devices
```

Expected output:

```
List of devices attached
127.0.0.1:5555      device
```

**“device”** status means everything is ready. If it shows **“offline”** or **“unauthorized”**, disconnect and reconnect:

```bash
.\adb disconnect 127.0.0.1:5555
.\adb connect     127.0.0.1:5555
```

---

## 5. Make Android Studio recognise BlueStacks

1. **Open Android Studio** → your project.  
2. In the **device drop-down** of the toolbar (usually says *Pixel 3a API 34* or similar), BlueStacks appears under **“Connected Devices”** with the same loopback address:  

   ```
   127.0.0.1:5555 (Android X, API 33)   • Google Play
   ```

3. Select it and click **Run** (green triangle). Your app installs and launches inside BlueStacks just as on a physical phone.

---

## 6. Common problems & fixes

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| `adb` not recognised | PATH doesn’t include platform-tools | Add it or use full path to `adb.exe` |
| Device never shows in Android Studio | Connected to wrong port | Re-check BlueStacks Preferences |
| Device status **“offline”** | Bridge hung after BlueStacks restart | `adb kill-server && adb start-server && adb connect …` |
| App installs, but screen is blank | ABI mismatch (x86 vs arm) | Ensure your build includes an x86/x86_64 variant, or enable *Run with Rosetta* on ARM Macs |

