# FMHY.net Search Skill

A simple skill for searching the [FMHY.net](https://fmhy.net) free media wiki via their single-page API.

## What it does

FMHY maintains a massive wiki of free tools, streaming sites, software alternatives, and resources. This skill downloads the entire site as a single markdown dump (~1.8 MB) and searches it with standard shell tools (`grep`, `sed`, optionally `rg`).

## Install

Clone or copy this repo into a subdirectory of your agent's skills directory. The main thing each platform needs to find is the `SKILL.md` file.

```bash
git clone https://github.com/Dthen/fmhy-skill.git
```

## Quick usage

```bash
# Download fresh, search, clean up
TMPFILE=$(mktemp)
curl -s "https://api.fmhy.net/single-page" > "$TMPFILE"

# Search
grep -i "vpn" "$TMPFILE"
rg -i "self.hosted.*audiobook" "$TMPFILE" -C 2
sed -n '/# ► Gaming/,/# ► /p' "$TMPFILE" | rg -i "emulator"

# Clean up
rm -f "$TMPFILE"
```

## Browse mode

When you know the area but not the keyword:
```bash
grep "^# ►" "$TMPFILE"           # list all categories
sed -n '/# ► Audio/,/# ► /p' "$TMPFILE" | head -n 50   # dump a section
```

## Markdown cheatsheet

| Symbol | Meaning |
|--------|---------|
| `# ►` | Top-level category |
| `## ▷` | Subcategory |
| `⭐` | Curated pick |
| `↪️` | Cross-link to another section |

## Requirements

- Unix-like shell (Linux, macOS, WSL, Git Bash)
- `curl`, `grep`
- `rg` (ripgrep) — optional but recommended

## License

BSD Zero Clause (0BSD)

Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE.
