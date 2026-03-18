# Claude Desktop Launcher Bookmark

A single HTML file that opens the Claude desktop app when loaded in a browser. Designed to live in your bookmarks bar as a quick-launch shortcut.

## How It Works

The page fires `claude://open` via JavaScript on load. macOS recognizes Claude Desktop's registered protocol handler and launches the app. The page then attempts to close itself.

Multiple trigger events are bound as fallbacks: page load, tab focus, visibility change, mouseover, mousemove, click, keydown, and touch. If the initial load fires, the rest are redundant. If it doesn't (some browsers defer JS on background tabs), any interaction with the page will catch it.

The file pulls a favicon from the web so it displays the Claude icon in your bookmarks bar.

## Setup

1. Save `index.html` somewhere stable (e.g., `~/Documents/bookmarks/`)
2. Open it in your browser once to confirm it works
3. Drag it to your bookmarks bar, or bookmark the `file:///` URL manually

## Limitations

- **First-run confirmation:** Browsers show a "This site wants to open Claude" dialog the first time. Check "Always allow" to suppress it going forward.
- **Self-close:** `window.close()` only works reliably on tabs opened by JavaScript. A bookmark-opened tab may refuse to close. Chrome is stricter about this than Safari.
- **No install detection:** If Claude Desktop isn't installed, the protocol silently fails. There's no reliable cross-browser way to detect whether the app exists.
- **Protocol path:** Claude Desktop registers `claude://` but the exact path may vary. If `claude://open` doesn't trigger it, try `claude://` or `claude://claude.ai/new` instead.

## Customization

If `claude://open` doesn't work, change the URL in both the `<script>` tag and the fallback `<a>` tag:

| Target | URL |
|---|---|
| Open app | `claude://open` |
| New conversation | `claude://claude.ai/new` |
| Just the protocol | `claude://` |

## License

Do whatever you want with this. It's a single HTML file.