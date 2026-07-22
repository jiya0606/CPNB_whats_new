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

---

# `v2.html` — the notebook-list flow

A second, self-contained prototype (`index.html` is untouched and still works on its own). Open `v2.html` directly, or at `.../v2.html` once deployed. One audience only — no view switcher, no `?user=` param.

## The three screens
1. **Home** — a notebook list. "Your notebooks" holds the one notebook the user has (*Customer Feedback Themes and Next Steps*), with the greyed-out **New notebook** create tile to its left. **Recommended for you** sits below with two suggestions: *1:1 Meeting Notes* and *Feature Spec Brainstorming* (both inert).
2. **New notebook** (the create tile) — a title field and a dashed drop zone reading **"Better references make better outputs"** over *"Drag and drop files here to add them as references"*, with **Add work content** (dark) and **Upload** (light). A left rail lists the **6 existing** feature cards. The drop zone highlights on dragover but accepts nothing.
3. **The notebook** (the notebook tile) — the same CPNB mock as `index.html`, with two differences: the megaphone panel shows **only the 4 June 2026 cards**, and a **connectors card** sits in the chat rail under "Let's connect the dots". Clicking it opens the full-size card — animation, title, description, and "Try it".

### The chat-rail banner
A compact 300×79 banner: icon on the left, a navy **NEW** pill over the title on the right, and an underlined **Dismiss** in the top-right corner. What draws the eye is the ripple — a halo pulsing outward from the banner edge every 3s (`.ft-wrap::before`) — plus a lift-and-tilt on hover. Both are disabled under `prefers-reduced-motion`.

Dismiss hides the banner for the session only; a reload brings it back, so each run-through of the prototype starts from the same place.

Back out of any screen with the chevron at the top left.

## "Try it" — guided tours
Most **"Try it"** buttons now teach *where* a feature lives instead of jumping to a canned page. Clicking one drops the user into the notebook and drives a **coach-mark tour**: a spotlight ring pulses over the exact control, a caption explains the step, and clicking the highlight walks forward — through multi-step paths — until the real feature surface opens (Select References, Share, the connector Sources flyout, the citations panel, the model picker, audio Customize, a mind map, or a suggested-edits page). **Skip** in the caption (or **Escape**) exits and resets.

The tour a card launches is matched by its title in `TOURS` / `TOUR_BY_TITLE` (JS). Two cards are exceptions: **card 2 (Send chat responses to a page)** stays a type-2 *action* demo and still navigates to `card02-example.html`; every other card runs a tour. Onboarding cards jump into the *Customer Feedback Themes and Next Steps* notebook; the four "New" cards run their tour in the notebook already on screen. For the two features with no in-notebook home yet — **in-line suggestions** and **best-fit model** — the tour first opens a small example source (an example page / a seeded chat answer, both with fabricated generic content) and runs the flow there.

## How the cards are shared
All ten cards are authored once inside `<template id="wn-cards">` and cloned into whichever screen needs them — the four `data-new="1"` cards to the panel, the other six to the new-notebook rail, and the connectors card again for the banner modal. Edit a card once and every screen follows. The blown-up card scales its mock (`.wn-card.lg`) rather than reflowing it, since each mini-mock is built at fixed pixel sizes.
