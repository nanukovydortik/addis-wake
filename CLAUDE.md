# addis-wake: turning Adam's desktop (ADDIS) on and off

This repo is **public**. It holds one status flag, `wake.json`, which the mini PC (hue-os)
reads every minute. Never write task details, names, links or anything private here.

When Adam asks in this session (Czech or English):

- **"zapni PC" / "turn on the PC" / "probuď PC"**: overwrite `wake.json` with
  `{"id": "manual-<YYYYMMDD-HHMM>", "requested_utc": "<now ISO, UTC>", "status": "requested"}`,
  then commit and push to `main`. Tell him: "Odesláno. Mini PC ho do minuty začne budit; do pár
  minut by měl být online." (Wake signal at 0, 3 and 6 min. If the PC isn't up after 10 min,
  hue-os power-cycles the Tapo plug when it's configured, otherwise it notifies him in hue-os.)
- **"vypni PC" / "turn off the PC"**: overwrite `wake.json` with
  `{"id": "manual-<YYYYMMDD-HHMM>", "requested_utc": "<now ISO, UTC>", "status": "shutdown"}`,
  commit and push. ADDIS's PC-queue task (every 15 min) sees it and shuts down with a 5-minute
  warning. Tell him it takes up to ~20 minutes.
- **"stav PC" / "PC status"**: `git pull` and report what `wake.json` says, in plain words
  ("requested at 9:12, waiting", "done", "shutdown requested at …").

Use the current time from `date -u`. Each id must be new (the mini PC ignores ids it has
already handled). Don't do anything else in this repo.
