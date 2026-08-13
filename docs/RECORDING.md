# How to record the demo GIF

The GIF is the single highest-leverage thing in the README. Target: **under 10 seconds, under 3 MB, 640px wide, loops cleanly.**

The one job of this GIF: a stranger scrolling GitHub sees "site blocks paste → extension types it in anyway" without reading a word.

## Setup (5 minutes)

1. Open `docs/demo-page.html` in Chrome (drag the file into a tab). It blocks paste exactly like a real portal, so you never have to record against a real bank.
2. Zoom the page to ~125% (`Cmd/Ctrl` + `+`) so text is readable when scaled down to 640px.
3. Copy a realistic value to your clipboard, e.g. `4029-8817-3341-9052`.
4. Hide anything personal: bookmarks bar (`Cmd/Ctrl+Shift+B`), other tabs, notifications (macOS: Focus mode).
5. Turn typing speed **up** in the extension. Real-time typing is too slow for a GIF. Aim for the whole string landing in ~3 seconds.

## The shot list

Record a region tight around the form, not the whole screen. Roughly 1000x600.

| Time | What happens |
|---|---|
| 0.0-0.8s | Static on the empty "Account number" field. Cursor visible. |
| 0.8-1.6s | Press `Cmd/Ctrl+V`. The red "Pasting is disabled" toast appears. **This is the hook, hold it long enough to read.** |
| 1.6-2.4s | Click the Paste Typer icon, click "Load from Clipboard", click Start. Move the mouse deliberately, not fast. |
| 2.4-5.5s | The number types itself into the field, character by character. |
| 5.5-7.0s | Full value sits in the field. Hold still. |
| 7.0s | Stop. |

Two rules that matter more than the rest: **hold the "paste blocked" moment** (that's the problem statement), and **end on a full, still field** (that's the payoff, and it makes the loop read cleanly).

## Tools

| Platform | Tool | Notes |
|---|---|---|
| macOS | [Kap](https://getkap.co) | Free, exports GIF directly, best option |
| macOS | CleanShot X | Paid, nicer cursor rendering |
| Windows | [ScreenToGif](https://www.screentogif.com) | Free, frame-level editing |
| Linux | [Peek](https://github.com/phw/peek) | Free, simple |
| Any | Record MP4, convert with ffmpeg | See below |

## Export settings

- **Width 640px**, 15 fps, loop forever
- Under 3 MB (GitHub renders larger files, but they load slowly and mobile users bail)
- Show the cursor, so viewers can follow the clicks

## MP4 to GIF with ffmpeg

```bash
# High-quality two-pass conversion
ffmpeg -i demo.mp4 -vf "fps=15,scale=640:-1:flags=lanczos,palettegen" -y palette.png
ffmpeg -i demo.mp4 -i palette.png -lavfi "fps=15,scale=640:-1:flags=lanczos [x]; [x][1:v] paletteuse" -y docs/demo.gif

# If it's over 3 MB, drop to 12 fps or trim the ends
```

Save as `docs/demo.gif`. The README already points there.

## Also worth capturing

While you're set up, grab these. They cost 2 extra minutes and get reused everywhere:

- **A still PNG** of the extension popup (`docs/popup.png`) for the Chrome Web Store listing
- **A short MP4** of the same demo. Twitter, Reddit, and LinkedIn all handle MP4 better than GIF, and it stays sharp.
