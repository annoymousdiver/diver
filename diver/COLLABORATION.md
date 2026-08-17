# Anonymous repo collaboration — onboarding for `annoymousdiver/diver`

- Repo:      https://github.com/annoymousdiver/diver
- Live site: https://annoymousdiver.github.io/diver/
- Identity:  everyone commits as `annoymousdiver <317812257+annoymousdiver@users.noreply.github.com>`

## One-time setup (per collaborator, per machine)

```bash
# 1. Clone with the shared PAT (Personal Access Token)
#    Replace <PAT> with the token shared out-of-band — never commit it.
git clone https://annoymousdiver:<PAT>@github.com/annoymousdiver/diver.git
cd diver

# 2. CRITICAL — pin local identity in this clone (does not touch global config)
git config user.name  "annoymousdiver"
git config user.email "317812257+annoymousdiver@users.noreply.github.com"
git config commit.gpgsign false
git config tag.gpgsign    false

# 3. Activate the pre-commit hook (blocks accidental commits with a wrong identity)
git config core.hooksPath .githooks

# 4. Verify
git config user.email     # must print the noreply address — NOT your real email
```

## Every time you commit

```bash
# Before staging new media, strip metadata from any new figures/videos
./scripts/strip-metadata.sh

# Commit normally — the pre-commit hook double-checks identity
git add <files>
git commit -m "..."

# Last sanity check before push (Author: AND Commit: must show the noreply email)
git log -1 --pretty=fuller

git push
```

## Anonymity gotchas

- **Branch names** — generic (`feature/teaser-update`), never `feature/<yourname>-...`.
- **Commit messages** — no real names, advisor/lab names, university jargon, or "for tomorrow's meeting with X".
- **Issues / PRs** — public on a public repo. Use the shared account for any in-thread comments.
- **File paths in code** — grep for `/home/`, `/Users/`, `~/`, hostnames before committing.
- **PDFs** — convert to PNG/SVG; the strip script does not handle PDF metadata.
- **OS metadata files** — `.gitignore` already excludes `.DS_Store`, `._*`, `Thumbs.db`, etc.
- **Timezone** — commit timestamps include your TZ offset. Low practical risk, but if it
  worries you: `TZ=UTC git commit ...`.

## Checklist

1. Browse https://github.com/annoymousdiver/diver/commits/main — every author/avatar must be `annoymousdiver`.
2. Check https://github.com/annoymousdiver profile — bio/location/pinned/socials must be empty or generic.
3. Open the live site in an incognito browser — view-source for leftover author info.
4. `find static -type f \( -name '._*' -o -name '.DS_Store' \)` should return nothing.
