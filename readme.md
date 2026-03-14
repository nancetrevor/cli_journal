# cli_obsidian

A small Go CLI for quick daily-note capture and retrieval in an Obsidian-style vault.

<img src="assets/journal.gif" alt="Project Demo" width="700">

## What it does
- Appends timestamped entries to daily markdown files (`YYYY-MM-DD.md`).
- Supports optional tags on entries.
- Searches notes by date range, tags, and query terms.
- Opens matching files in `nvim` or Obsidian.

## Build
```bash
go build -o odn .
```

## Configuration
Set your default editor:

```bash
./odn config --editor nvim
# or
./odn config --editor obsidian
```

Reset to defaults:

```bash
./odn config default
```

Config file location:
- `~/.config/cli_obsidian/config.json`

## Usage

### Add note entries
Add a single-line entry:

```bash
./odn add --tag work,idea "Ship first draft of CLI docs"
```

Add multi-line input from stdin (finish with `Ctrl-D`):

```bash
./odn add --tag journal
```

Output format written to the daily file:

```text
- [15:04] Ship first draft of CLI docs #work #idea
```

### Search notes
Search specific date:

```bash
./odn search --date 2026-02-10
```

Search by range:

```bash
./odn search --from 2026-02-01 --to 2026-02-10
```

Search by year/month:

```bash
./odn search --year 2026 --month 02
```

Search by tags and query terms:

```bash
./odn search --tags work,idea --query deploy,rollback
```

Notes:
- `--tags` and `--query` are comma-separated.
- Search uses AND logic within each list (all tags and all query terms must match).
- After results are listed, enter a number to open a file or `q` to quit.

### Open note files
Open today's note:

```bash
./odn open today
```

Open a specific note:

```bash
./odn open 2026-02-10
```

`.md` is optional; it will be appended automatically.

## Command reference
```text
odn add [--tag tag1,tag2] [entry text]
odn search [--date YYYY-MM-DD] [--year YYYY] [--month MM] [--from YYYY-MM-DD] [--to YYYY-MM-DD] [--tags a,b] [--query x,y]
odn open <today|YYYY-MM-DD|filename>
odn config --editor <nvim|obsidian>
odn config default
```
