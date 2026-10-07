# embed code live

Local web page that renders a pasted embed code (iframe, script widget, raw HTML) and serves it from this Mac. Mainly used to watch live-stream embeds from third-party sites.

## Files
- `embed-host.html`: the whole app, a single self-contained file (currently v3, version label in the `<h1>`)
- `README.md`: usage docs
- `embed.txt`: optional embed source the page can watch; gitignored, never commit it

## Run
`cd ~/embed-host && python3 -m http.server 8000`, then open http://localhost:8000/embed-host.html.
Must be served over http. Opening via file:// breaks YouTube and most stream embeds.

## How it works
- Embed is inserted directly into the page (`#frame` div), not a sandboxed srcdoc iframe. Stream sites detect sandboxes and show "Remove sandbox attributes on the iframe tag", so the sandbox was removed deliberately.
- On render, every iframe gets `referrerpolicy="strict-origin-when-cross-origin"` (YouTube error 153 without it), an expanded `allow` list (autoplay, fullscreen, encrypted-media, picture-in-picture), and any `sandbox` attribute is stripped. Scripts are re-created so they execute.
- Live view: `#live=<base64 embed>` in the URL hides the editor; a lone iframe fills the window.
- `?watch` polls `embed.txt` every 2s; `?live` forces live view.
- Last embed is saved in localStorage.

## History
- v1: sandboxed srcdoc iframe; stream refused to play.
- v2: direct rendering + referrer/allow attributes.
- v3: fixed placeholder overlay (`.empty[hidden]` needed because `display: grid` overrode `hidden`), added version label.

## Repo
GitHub: Prezbo8/embed-code-live (public). Hosted on GitHub Pages from `main`: https://prezbo8.github.io/embed-code-live/embed-host.html. Push updates with `git add -A && git commit -m "..." && git push`.

## Notes
- Unsandboxed embeds can open pop-ups and redirects; keep that trade-off in mind with any change.
- Bump the version label in the `<h1>` whenever embed-host.html changes, so a stale cached copy is easy to spot.
