# WhatsApp-Web-Pages

Static support pages for the **WhatsApp Web Customizer** browser extension.

This repository hosts the small standalone HTML pages the extension links to from
outside the browser — pages Chrome/Firefox can open even when no extension code is
running.

## Contents

- **`uninstall.html`** — the uninstall redirect page. Chrome runs no extension code
  at uninstall time; the only available hook is `chrome.runtime.setUninstallURL()`,
  which points here. When the user removes the extension this page:
  1. Reads the anonymous PostHog `distinct_id` and extension version from the URL.
  2. Fires an `extension_uninstalled` event to PostHog (via a `keepalive` fetch so it
     survives the navigation away).
  3. Forwards the user to a short Google Form, pre-filled so the survey can be
     answered in one click.

## Tech

- Plain HTML, CSS and JavaScript — no build step.
- [PostHog](https://posthog.com/) for anonymous product analytics (client-side
  project key only).
- A Google Form for uninstall feedback.

## Usage

These pages are meant to be hosted as static files and referenced by the extension
(for example as its `setUninstallURL` target). Open `uninstall.html` directly to
preview the redirect behaviour.
