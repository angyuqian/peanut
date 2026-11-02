# Peanut 🥜

A private web app for two parents-to-be: the run-up to the birth, the confinement weeks and the baby.

Open **https://angyuqian.github.io/peanut/**, enter the passcode, and add it to your home screen.

- **Home**: weeks to go, a daily note from Peanut for Mum, a daily "Psst, Papa" nudge for Dad, hugs, a notes jar, a one-tap mood check, and what's next.
- **Mum**: daily check-in, a 3-week trend, red-flag prompts, "what would help", a care log, who to call.
- **Baby**: feed timer, bottles, diapers, sleep, pumping, growth, temperature, a 7-day summary. Contraction timer from 36 weeks.
- **Plan**, **Gear**, **More**: to-dos, appointments, registry, bags, names, notes, money, nannies, settings.

## Syncing (once)

Both phones share one copy of the data once a GitHub token is added. Do it once on any device:

1. [Make a fine-grained token](https://github.com/settings/personal-access-tokens/new): Repository access → Only select repositories → `peanut`. Permissions → Contents → Read and write.
2. Paste it into the blue card on the Home page.

The other devices pick it up on their own. Until then, edits stay on the device they were made on.

## Privacy

Everything personal is encrypted in the browser with the passcode (PBKDF2-SHA256, 600,000 rounds, then AES-GCM). The repo holds the app code, `config.json` (salt and the encrypted token) and the encrypted data on the `peanut-data` branch. Without the passcode it's unreadable.

## Daily reminders

Tap **Remind me daily** on Home to download a calendar file with one alert a day, each with that day's note. On iPhone, add a calendar called "Peanut" first and import into it, so you can delete them all at once later.
