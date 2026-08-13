# Contributing

Thanks for helping out. This is a small, dependency-free extension, so contributing is easy.

## Run it locally

```bash
git clone https://github.com/ZonaHu/paste-typer.git
```

Open `chrome://extensions/`, enable Developer mode, click **Load unpacked**, select the folder. After editing, click the reload icon on the extension card and refresh the target page.

No build step, no dependencies.

## The most useful contribution: a new site adapter

Most "it doesn't work on site X" reports come down to the site using a custom editor that ignores standard key events. The fix is a new adapter.

Adapters live in `content/` and implement the interface in `inputAdapter.js`:

| Method | Does |
|---|---|
| `canHandle(element)` | Return true if this adapter should own the current page/element |
| `focus(element)` | Put the caret where typing should start |
| `typeCharacter(element, char)` | Send one character |
| `clear(element)` | Empty the field |

Look at `standardInputAdapter.js` for the simple case and `googleDocsAdapter.js` for a canvas-based editor. Register your adapter in `adapterManager.js`.

## Reporting a site that doesn't work

Open an issue with the URL (or a description if it's behind a login) and what happened: nothing typed, partial text, wrong order, page rejected the input. That's enough to start.

## Pull requests

Keep them focused. One fix or one adapter per PR. Describe what you tested it against.

## Code style

Plain JavaScript, no build tooling, no dependencies. Match the surrounding style.
