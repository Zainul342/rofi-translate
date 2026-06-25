# rofi-translate

An ultra-fast, lightweight, and offline-like Indonesian to English translator popup for Linux window managers (bspwm, i3, sway, etc.) using **Rofi** and a direct Google Translate API endpoint.

It features two distinct modes of execution:
- **`Enter`**: Translates and automatically pastes the text directly into your currently focused window/terminal.
- **`Shift + Enter`**: Translates and copies the English text to your clipboard without pasting, showing a desktop notification.

## Features
- **Super Fast**: Direct curl query to Google Translate's single API endpoint, completing translations in **~150-250ms** (up to 10x faster than traditional wrapper tools).
- **RAM Efficient**: Consumes practically 0MB RAM (no running background daemons, local LLMs, or heavy Python dependencies).
- **Zero Configuration**: Uses system-installed utilities (`curl`, `jq`, `xclip`, `xdotool`).
- **DBus-Safe**: Asynchronous notifications running in the background to ensure it never hangs even if the notification server is slow or disconnected.

## Dependencies
Make sure you have the following packages installed on your Linux system:
- `rofi`
- `curl`
- `jq`
- `xclip`
- `xdotool`
- `notify-send` (libnotify)

On Arch Linux / EndeavourOS:
```bash
sudo pacman -S rofi curl jq xclip xdotool libnotify
```

Additionally, you need the standalone executable of **`translate-shell`** (as a fallback backend):
```bash
curl -Lo ~/.local/bin/trans https://git.io/trans && chmod +x ~/.local/bin/trans
```

## Installation
1. Clone this repository or download the script:
   ```bash
   git clone https://github.com/your-username/rofi-translate.git
   cd rofi-translate
   ```
2. Move the script to your local bin directory (ensure it is in your `PATH`):
   ```bash
   mkdir -p ~/.local/bin
   cp rofi-translate ~/.local/bin/
   chmod +x ~/.local/bin/rofi-translate
   ```

## Keyboard Shortcut Setup (`sxhkd`)
Add the following lines to your `~/.config/sxhkd/sxhkdrc`:

```sxhkd
# Translate Indonesian to English clipboard & auto-paste
super + t
    rofi-translate
```
Then, reload `sxhkd` by pressing `super + Escape` or running `pkill -USR1 -x sxhkd`.

## Usage
Press `super + t`:
1. Type your prompt in Indonesian (e.g., `tolong buatkan skrip backup`).
2. **Press `Enter`**: Auto-pastes the translated English (`please make a backup script`) into your active terminal.
3. **Press `Shift + Enter`**: Copies the English translation to your clipboard and notifies you.
