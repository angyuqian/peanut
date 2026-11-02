# Peanut 🥜

A private web app for two parents-to-be: the run-up to the birth, the confinement weeks and the baby. Open it on both phones and add it to the home screen.

- **Home**: weeks and "sleeps to go", a daily note from Peanut for Mum, a daily "Psst, Papa" nudge for Dad, hugs, a notes jar, a one-tap mood check, and what's next.
- **Mum**: daily check-in (mood, energy, body, sleep, symptoms), a 3-week trend, red-flag prompts, "what would help", a care log, and who to call.
- **Baby**: breastfeed timer (left/right, switch side), bottles, diapers, sleep, pumping, growth, temperature, a 7-day summary. A contraction timer appears at the top from 36 weeks.
- **Plan**: to-dos with owners and due dates (including "X days after birth"), appointments, key dates.
- **Gear**: registry, hospital and confinement bags, thank-yous.
- **More**: names (with hearts), notes jar, money, nannies and centres, books, links, settings.

## Deploy (GitHub Desktop, from this folder)

1. In GitHub Desktop: File → Add local repository → choose this `peanut` folder → "create a repository" → Publish. Untick "Keep this code private" if you're on a free plan (Pages needs a public repo on free accounts). The `.gitignore` keeps `peanut-seed.json` out.
2. On github.com, open the repo → Settings → Pages → Deploy from a branch → `main`, `/ (root)`.
3. Make a fine-grained token: GitHub → Settings → Developer settings → Fine-grained tokens → Generate.
   - Repository access: **only this repo**
   - Permissions: **Contents: Read and write** (nothing else)
   - Expiry: past the end of confinement (you can swap it later in Settings)
4. Open `https://<you>.github.io/peanut/` on your phone. Choose a passphrase, load `peanut-seed.json` as starter data, pick "Sync both phones via GitHub", paste the token.
5. Delete `peanut-seed.json` once it's loaded. It's your spreadsheet in plain text.
6. On the other phone, open the same link (give Pages a minute or two), enter the passphrase, then Share → Add to Home Screen.

## Daily reminders

A web page can't send notifications on its own without a server. Peanut uses your phone's calendar instead: tap **Remind me daily** on Home, pick a time, and it downloads a calendar file with one alert a day, each carrying that day's note.

- iPhone: in the Calendar app, add a calendar called "Peanut" first. Open the downloaded file, tap Add All, choose Peanut. Delete that calendar to remove them all.
- Android: open the file with Google Calendar.
- After the birth, make a fresh set so the notes switch to the after-birth ones. Peanut reminds you.

## Privacy

| What | Where | Readable by the public? |
|---|---|---|
| App code, icons | `main` branch | Yes, contains no personal data |
| `config.json` (repo name, salt, token) | `main` branch | Token is encrypted |
| `peanut.vault.json` (all your data) | `peanut-data` branch | Encrypted |

- Encryption: PBKDF2-SHA256 (600,000 iterations) from your passphrase, then AES-GCM 256. The passphrase never leaves the phone.
- Saves are commits to `peanut-data`, so Pages doesn't rebuild on every tap. Phones pull every 45 seconds while open.
- Both phones editing at once: records merge, newest edit wins. Offline edits are kept and pushed later.
- "Keep this phone unlocked" stores the key in the browser. Anyone holding that unlocked phone can open Peanut. More → Settings → Lock forgets it.
- The notes jar hides the other person's future notes in the app. It's not cryptographically secret from them.

## Limits

- **The passphrase is the whole security model.** The encrypted files are public; a weak passphrase can be brute-forced. Use four or more random words. Forget it and the data is gone.
- If the passphrase leaks: revoke the token on GitHub, download a backup, delete `config.json` and the `peanut-data` branch, set up again with a new passphrase, import the backup.
- Token expired: More → Settings → Replace token. The other phone picks it up.
- Health prompts are prompts, not medical advice. When unsure, call.
