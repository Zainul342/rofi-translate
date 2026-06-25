# rofi-translate

A simple Rofi popup to translate Indonesian prompts into English on the fly. 

I wrote this because prompting AI coding assistants (like Antigravity CLI or Claude Code) in Indonesian wastes a lot of context tokens. Translating within the active CLI session also clutters the transcript. This script runs outside the CLI, queries Google Translate directly, and pastes the English translation instantly.

## How it works
- **`Enter`**: Translates and pastes the English text directly into your active window/terminal.
- **`Shift + Enter`**: Translates and copies to your clipboard (without auto-pasting).

## Speed
Unlike `translate-shell` which takes ~1.5s because of wrapper bloat, this script curls the Google Translate API endpoint directly. It completes translations in **~150ms**, making the auto-paste feel instant.

## Dependencies
Make sure you have these installed:
- `rofi`
- `curl`
- `jq`
- `xclip`
- `xdotool`
- `notify-send` (optional, for notifications)

On Arch/EndeavourOS:
```bash
sudo pacman -S rofi curl jq xclip xdotool libnotify
```

You also need `translate-shell` as a fallback backend:
```bash
curl -Lo ~/.local/bin/trans https://git.io/trans && chmod +x ~/.local/bin/trans
```

## Installation
1. Move `rofi-translate` to your local bin path:
   ```bash
   cp rofi-translate ~/.local/bin/
   chmod +x ~/.local/bin/rofi-translate
   ```
2. Map it in your `~/.config/sxhkd/sxhkdrc`:
   ```sxhkd
   # Translate ID to EN and paste
   super + t
       rofi-translate
   ```
3. Reload sxhkd (`super + Escape`).
