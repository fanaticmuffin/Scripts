# Scripts
Just random scripts to share
# arr_rename.py

Renames Sonarr series and Radarr movie folders (and their files) that don't match the arr's naming format, through the arr itself, then checks no files went missing. Any problem stops the run.

Python 3.9+ (standard library only) and the rest of this repo (`lib/`).

## Setup

Copy `.env.example` to `.env` and fill in `SONARR_URL` / `SONARR_API_KEY` and/or `RADARR_URL` / `RADARR_API_KEY`.

## Usage
```bash
./arr_rename.py sonarr            # dry run: shows what it would rename
./arr_rename.py sonarr -i         # asks about each rename
./arr_rename.py radarr --apply    # renames everything it safely can
```

Renames that would lose information (a year, an id tag, the title) are marked **IRREGULAR** and only done with `-i` or `--force`. Everything printed is also saved to `logs/arr_rename.log`.

## Options

| Option | Description |
| --- | --- |
| `sonarr` / `radarr` | Which arr to check (required, first) |
| `--url URL` | Arr address (default: `SONARR_URL` / `RADARR_URL`) |
| `--api-key KEY` | Arr API key (default: `SONARR_API_KEY` / `RADARR_API_KEY`) |
| `--apply` | Do every rename except irregular ones (default is a dry run) |
| `-i`, `--interactive` | Ask about each rename: yes / no / all / quit |
| `--force` | With `--apply`, also do irregular and `TBA?` renames |
| `--files` | Also rename files of items whose folder is fine |
| `--tba` | Sonarr only: like `--files`, but only files whose "TBA" episode title now has a real one |
| `--ignore-case` | Skip folders and files that only differ in capitals |
| `--ignore-punctuation` | Skip folders and files that only differ in special characters |
| `--ignore-tag TAG` | Leave items with this tag alone (default: `SONARR_IGNORE_TAG` / `RADARR_IGNORE_TAG`) |
| `--discord-webhook URL` | Post each run's report to Discord (default: `DISCORD_WEBHOOK_URL`) |
| `--discord-user ID` | Discord user id to ping when something needs `-i` or was forced (default: `DISCORD_USER_ID`) |

`--apply` and `-i` can't be combined, and neither can `--files` and `--tba`.