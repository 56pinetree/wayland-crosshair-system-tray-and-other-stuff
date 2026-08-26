# wayland-crosshair
(fork of: https://github.com/Divvv/wayland-crosshair)

A minimal crosshair overlay for Wayland compositors (Hyprland, Sway, etc.).

Displays a dot at the center of your screen (or anywhere else) as a fullscreen transparent overlay. Designed for gaming — it is completely invisible to the input system: no focus, no keyboard grabs, no mouse interception. Clicks and cursor movement pass straight through to the game underneath.

## Features

- Zero input interference — uses an empty Wayland input region so the overlay cannot be focused or clicked
- `wlr-layer-shell` overlay layer — renders above fullscreen games on Wayland
- True screen center — anchors to all four edges so the dot is always at exact pixel center regardless of resolution
- Negligible resource usage — static surface, redrawn once at startup
- System tray entry to close the program (via https://github.com/nschmidtdev/c_tray)

## Dependencies

- `gtk3`
- `gtk-layer-shell`
- `libappindicator3`

Install on Arch Linux:

```bash
sudo pacman -S gtk3 gtk-layer-shell (whatever libappindicator3 is on arch)
```

Install on Fedora:

```bash
sudo dnf install gtk3 gtk-layer-shell libappindicator-gtk3
```

```bash
# For compiling
sudo dnf install gtk3-devel gtk-layer-shell-devel libappindicator-gtk3-devel
```

## Build

Clone repo with submodules:
```bash
git clone https://github.com/56pinetree/wayland-crosshair-system-tray-and-other-stuff.git --recursive
```
If you've already cloned it:
```bash
git submodule update --init --recursive
```
Build the program:
```bash
make
```

## Usage

```bash
# Crosshair only
./crosshair

# Help
./crosshair -h/-help

# Crosshair with custom position, radius, and color
# (All values must be between 0.0 and 1.0)
./crosshair [height], [width], [radius], [red], [green], [blue]
./crosshair 0.5, 0.5, 2.0, 0.0, 0.6, 0.9

# Currently every argument needs to be passed in order,
# But you can put an 'x' in place of a value to keep default.
# To just change the color:
./crosshair x, x, x, 0.0, 0.6, 0.9
```

Close it by clicking the icon in the system tray.

Or kill it with:

```bash
pkill crosshair
```
## Setting the system tray icon
Make an icon named "crosshair-icon.png" and place it next to the binary

## Why not a Python/Electron/etc. script?

Most simple overlay examples steal input focus because they don't set `keyboard_interactivity = NONE` on the layer shell surface, and don't set an empty `wl_input_region`. This tool sets both, making it safe to run during gameplay.

## License

MIT
