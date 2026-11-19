# Installing VinylEV

VinylEV is a desktop widget that shows what Spotify is playing on a spinning vinyl record. It
runs on any Mac (Apple silicon or Intel) with macOS 14 Sonoma or newer, and needs the Spotify
desktop app.

## 1. Install
1. Open **VinylEV.dmg** (from the Download button on the releases page).
2. Drag **VinylEV** onto the **Applications** folder.
3. Eject the disk image.

## 2. Open it the first time
VinylEV isn't from the App Store and isn't notarized by Apple, so macOS can't check it
automatically. Expect a warning the first time. On macOS 15 (Sequoia) and later, right-click → Open
no longer gets around it.

1. Open **Applications** and double-click **VinylEV**.
2. macOS says it *cannot verify that VinylEV is free of malware*. Click **Done** (not "Move to Trash").
3. Open **System Settings → Privacy & Security** and scroll down to **Security**.
4. Next to "VinylEV was blocked to protect your Mac", click **Open Anyway**.
5. Click **Open Anyway** again and enter your Mac password.

On macOS 14, right-click the app → **Open** → **Open** also works. You only do this once.

**If the Open Anyway button doesn't appear**, or macOS says the app is "damaged", open
**Terminal** and run the following, then open VinylEV again:

```bash
xattr -dr com.apple.quarantine /Applications/VinylEV.app
```

This only removes the "downloaded from the internet" flag from VinylEV.

## 3. First run
A small welcome window opens. VinylEV then keeps running in the background: no Dock icon, no
menu bar item. It starts by itself when you log in (macOS shows a "Login Item Added" notice).

**Allow Spotify control.** With Spotify open, macOS asks *"VinylEV wants to control Spotify"*.
Click **Allow**. VinylEV uses this to read the current track, cover and position, and for the
widget's play / pause / skip buttons. If you clicked *Don't Allow*, the widget says "Allow
Automation for Spotify in VinylEV": open **System Settings → Privacy & Security → Automation →
VinylEV** and turn on **Spotify**. The welcome window has a button that opens this pane.

VinylEV never opens Spotify by itself. To see the welcome window again, open VinylEV from
Applications while it's running.

## 4. Add the widget
1. Right-click the desktop → **Edit Widgets…**
2. Search **VinylEV** and drag a size onto the desktop (or into Notification Center):
   Small (just the record), Medium, Large or Extra Large (with a progress bar).

**Keep the album colors:** macOS shows desktop widgets in a tinted, monochrome style when a
window is in front of them. To always see them in color: **System Settings → Desktop & Dock →
Widget style → Full-color**.

## If something doesn't work
- **VinylEV isn't in Edit Widgets:** open VinylEV from Applications once (the widget is
  registered when the app starts), and make sure only one copy of VinylEV.app exists. Then, in
  Terminal: `killall chronod NotificationCenter` and open Edit Widgets again. To check that macOS
  knows the widget: `pluginkit -m -v | grep -i vinylev`.
- **The widget shows gray bars or doesn't change:** restart VinylEV with
  `pkill -x VinylEV; open /Applications/VinylEV.app`.
- **"Not Playing" while music plays:** Spotify's desktop app has to be the player (the web
  player isn't supported), and VinylEV must be allowed to control Spotify (step 3).

## Good to know
- The record turns in small steps once a second, which macOS smooths into a spin. Widgets can't
  run a continuous animation, so expect the odd tiny hitch.
- Widgets update a moment after Spotify changes (about half a second to a few seconds), because
  macOS refreshes widgets on its own schedule.
- Spotify desktop app only.

## Updating
Download the new **VinylEV.dmg** from the releases page and drag the app into Applications again
to replace the old one. Your settings and the Spotify permission are kept.

## Removing it
1. Remove the VinylEV widgets from the desktop.
2. In Terminal, run the following. It removes the login item, VinylEV's settings and its cached
   album covers:
   ```bash
   /Applications/VinylEV.app/Contents/MacOS/VinylEV --uninstall
   ```
3. Drag VinylEV from Applications to the Bin.

VinylEV is not affiliated with, endorsed by, or sponsored by Spotify.
