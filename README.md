# embed code live

A single local web page that renders a pasted embed code (iframe, script widget, raw HTML). Built for watching live-stream embeds from third-party sites.

## Run

```sh
cd ~/embed-host && python3 -m http.server 8000
```

Open http://localhost:8000/embed-host.html.

Serve it over http. Opening it via `file://` breaks YouTube and most stream embeds.

## Use

- Paste an embed code and press **Render** (or ⌘ + Enter).
- **Open live view** / **Copy live link**: opens the embed alone, full window (`#live=<base64 embed>`).
- **Watch embed.txt**: put an `embed.txt` next to the page and it reloads every 2s when the file changes. `?watch` turns this on at load, and `?live` forces live view.
- Your last embed is saved in localStorage.
- **Shield** (top-right of the embed, on by default): an invisible layer over the embed catches your clicks, so the embed never gets the click it needs to open a pop-up. Turn it off to press play or unmute, then turn it back on. Use the page's **Fullscreen** button, since the embed's own one is behind the shield.

## Note

Embeds are rendered unsandboxed, because stream sites refuse to play inside a sandboxed iframe. So an embed can open pop-ups and redirects. Only paste embed codes from sources you're fine with.
