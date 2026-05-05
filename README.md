# Japan Trip 2026 — Private Guide

Password-gated single-page travel guide. Hosted on GitHub Pages.

## Files

- `source.html` — plaintext editable source. **Never committed.** (`.gitignore`d.)
- `build.html` — browser-based encryption tool. Open it locally to rebuild `index.html`.
- `index.html` — encrypted gate. **This is the only content file in git.**
- `.gitignore` — keeps `source.html` out of git.

## Workflow

### First time

1. Open `build.html` in any browser.
2. Drop in `source.html`. Pick a strong passphrase (4+ random words). Click Encrypt.
3. The browser downloads `index.html`. Replace any existing `index.html` with this one.
4. Commit and push **only** `index.html`, `build.html`, `.gitignore`, and this `README.md`.
5. Enable GitHub Pages on the repo. Visit the URL → enter passphrase.

### Editing content later

1. Edit `source.html` locally.
2. Reopen `build.html` → drop `source.html` → enter the passphrase (same or new) → download new `index.html`.
3. Commit and push the new `index.html`.

### Rotating the passphrase

Same as editing content — just type a new passphrase in step 2. The old `index.html` in git history is still there, so if a strong attacker grabbed the old ciphertext, rotation alone won't stop them. Rotation protects future visitors only.

## Security model

- AES-256-GCM, key derived via PBKDF2-SHA256 with 200,000 iterations.
- Per-build random salt + IV.
- Passphrase is never stored. Derived key is cached in `sessionStorage` after a successful unlock and clears when the tab closes.
- The encrypted blob is permanently public on GitHub. Strong passphrase is the only real defense — see Security Notes inside `build.html`.

## Local previews

- Open `source.html` directly to preview content without password.
- Open the encrypted `index.html` to test the unlock flow.
