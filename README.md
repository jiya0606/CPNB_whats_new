# Copilot Notebooks — "What's new" panel prototype

Interactive static prototype. Open `index.html` directly in a browser, or deploy to GitHub Pages: **Settings → Pages → Build and deployment → Source: "Deploy from a branch" → Branch: `main` / `/ (root)`**.

No build step, no dependencies, no network calls — a single self-contained `index.html`.

## What it does
Click the **megaphone** (with the unread dot) in the top command bar. A **What's new** panel slides in over a dimmed mock of the CPNB homepage with 10 feature cards, each with an animated mini-mock that plays when scrolled into view (hover a card to replay it).

- Close with the **X**, the **scrim**, or **Escape**.
- The unread dot clears on first open and stays cleared across reloads (`localStorage`).
- "Try it" buttons are inert by design — they don't navigate.

A "New" pill and a "Read more here" link appear on four cards: **connectors**, **in-line suggestions**, **Verify Sources Faster**, and **Use the Best Fit Model**.

To see the unread dot again, clear the `cpnb_wn_seen_v1` key (DevTools → Application → Local Storage).
