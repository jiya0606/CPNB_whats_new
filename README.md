# Copilot Notebooks — "What's new" panel prototype

Interactive static prototype. Open `index.html` directly in a browser, or deploy to GitHub Pages: **Settings → Pages → Build and deployment → Source: "Deploy from a branch" → Branch: `main` / `/ (root)`**.

No build step, no dependencies, no network calls — a single self-contained `index.html`.

## What it does
Click the **megaphone** (with the unread dot) in the top command bar. A **What's new** panel slides in over a dimmed mock of the CPNB homepage with 10 feature cards, each with an animated mini-mock that plays when scrolled into view (hover a card to replay it).

- Close with the **X**, the **scrim**, or **Escape**.
- The unread dot clears on first open and stays cleared across reloads (`localStorage`).
- "Try it" buttons are inert by design — they don't navigate.

## The two versions
A **Prototype view** switcher sits at the bottom-left of the mock (it is not part of the product UI — remove it before any real user test). It swaps between the two audiences, and each has its own shareable link:

| Audience | Ordering | Link |
| --- | --- | --- |
| Returning user | The four **New** (June 2026) cards lead | `index.html?user=returning` (default) |
| New user | The New cards sit at the **bottom** — everything is new to them anyway | `index.html?user=new` |

## The "New" cards
Four cards are tagged as new: **connectors**, **in-line suggestions**, **Verify Sources Faster**, and **Use the Best Fit Model**. Each gets a navy **NEW** badge above the title, a tinted blue card background, and a "Read more here" link to the June 2026 Copilot blog post.

To see the unread dot again, clear the `cpnb_wn_seen_v1` key (DevTools → Application → Local Storage).
