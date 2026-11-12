# NetSuite relay for yoraito-sync

NetSuite only sends a login back to an `https://` address. yoraito-sync runs on the user's own computer at `http://127.0.0.1:<port>`, so NetSuite can't redirect to it directly. This page closes the gap.

- **Address:** https://yoraitoai.github.io/netsuite-relay/ (GitHub Pages). Register it as the redirect URI on the NetSuite integration record; yoraito-sync uses it by default.
- **What it does:** it reads `code`, `state`, `company` and `error` from NetSuite's redirect and sends the browser to `http://127.0.0.1:<port>/oauth/netsuite/callback`. The port comes from the `state` that yoraito-sync created (`v1.<nonce>.<port>`), and must be 1024 to 65535. The host is always `127.0.0.1`, and any other `state` is refused, so the page can't be used to send people elsewhere.
- **What it doesn't do:** it holds no secrets, calls no server and loads nothing else. The login uses PKCE, so a code seen here is useless without the verifier, which never leaves the user's computer.

The source of truth is `spike/relay/netsuite.html` in yoraito-sync. Keep this `index.html` identical to it.
