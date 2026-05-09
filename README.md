# FMHY.net Search Skill for Hermes Agent

A simple skill for searching the [FMHY.net](https://fmhy.net) free media wiki via their single-page API.

## What it does

FMHY maintains a massive wiki of free tools, streaming sites, software alternatives, and resources. This skill downloads the entire site as a single markdown dump (~1.8 MB) and searches it with `grep`/`rg`.

## Install

Copy or symlink into your Hermes skills directory:

```bash
cp -r fmhy-net ~/.hermes/skills/research/
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

MIT
