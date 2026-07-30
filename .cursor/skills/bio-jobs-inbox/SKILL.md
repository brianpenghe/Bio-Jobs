---
name: bio-jobs-inbox
description: >-
  Process Nature Careers / Science Careers email dumps from Bio-Jobs-Inbox into
  README.md job listings (dedupe, categorize, format), then clear the inbox.
  Use when the user asks to update jobs from the jobs folder, Bio-Jobs-Inbox,
  inbox emails, or job alerts.
---

# Bio-Jobs inbox → README

## Paths

| Role | Path |
|------|------|
| Repo / README | `/Users/phe/Library/CloudStorage/OneDrive-UCSF/Documents/Bio-Jobs/README.md` |
| Inbox | `/Users/phe/Library/CloudStorage/OneDrive-UCSF/Documents/Bio-Jobs-Inbox/` |

Inbox holds `.txt` email dumps (often Outlook/"AQMk…" filenames). User may say "jobs folder" or "job folder" — that means this inbox.

## Workflow

Copy and track:

```
- [ ] 1. List inbox `*.txt`
- [ ] 2. Extract unique Nature / Science Careers job IDs + clean URLs
- [ ] 3. Drop IDs already in README.md
- [ ] 4. Skip near-duplicates (same role mirrored on the other board, or newer SC/Nature ID for a role already listed)
- [ ] 5. Fetch title / org / location / country for remaining jobs
- [ ] 6. Categorize → section + region; insert at **top** of each regional list
- [ ] 7. Delete processed inbox `*.txt`
- [ ] 8. Commit/push only if the user asked
```

### Extract IDs

From each inbox file, unwrap `urldefense` links and collect:

- `https://www.nature.com/naturecareers/job/{id}/{slug}/`
- `https://jobs.sciencecareers.org/job/{id}/{slug}/`

Ignore logos, search, unsubscribe, beacons. Prefer clean URLs without TrackID query params.

### Dedup / skip

**Skip if** the job ID is already in `README.md`.

**Also skip near-duplicates**, e.g.:

- Same role on Nature and Science Careers (keep whichever is already listed, or pick one Nature/SC URL)
- Newer board ID for an identical title already listed (e.g. Ohio Eminent Scholar Nature + SC mirror)
- Off-scope alerts (non-bio: aerosol modelling, pure organic chemistry, pure math/info unless clearly life-science)

**Do add** newer EIT / Greenhouse-style IDs when the list historically keeps distinct posting IDs for the same lab/role family (e.g. new GBI postdoc ID).

### Categorize

| Section | Examples |
|---------|----------|
| Team Leader/PI | Faculty, PI, group leader, open-rank professor, chairs |
| Staff Scientist | Scientist, bioinformatician, engineer, lab manager, directors (non-PI ops) |
| Postdoc | Postdoc / research fellow |
| PhD | PhD studentship / graduate roles |
| RA/Internship | Research assistant, technician, SRA |
| Others | Teaching-only lecturers, pure ops/HR/finance, edge cases |

**Regions** (flag emoji in the bullet):

- 🌎 North America — US 🇺🇸, Canada 🇨🇦; Latin America may use regional flag under NA if no LatAm section (existing precedent)
- 🌍 Europe — UK 🏴󠁧󠁢󠁥󠁮󠁧󠁿 / 🇬🇧 / country flags; Switzerland 🇨🇭, etc.
- 🌏 Asia & Oceania — China 🇨🇳, HK 🇭🇰, Japan 🇯🇵, Qatar 🇶🇦, Singapore 🇸🇬, Australia 🇦🇺, …

If PhD has no North America `<details>` block yet and a NA/CA PhD appears, **add** that regional block.

### Bullet format

Newest first within each regional list:

```markdown
- 🇺🇸 [Short title — key focus, Org, City, ST](https://clean-url/)  
```

Optional suffix when known: ` · closes YYYY-MM-DD`

Prefer employer portals when available; Nature Careers / Science Careers URLs from the alert are fine. Match existing README style (em dash, trailing two spaces).

### Insert

Insert new bullets immediately after each relevant:

```html
<summary>🌎 North America</summary>
```

(or Europe / Asia), **before** the previous first listing.

### Cleanup

After a successful README update, delete all processed `*.txt` in `Bio-Jobs-Inbox`.

### Git

Do **not** commit or push unless the user explicitly asks. Typical messages:

- `Add Bio-Jobs-Inbox faculty, postdoc, and PhD openings.`
- `Add faculty, staff, postdoc, and RA listings from Bio-Jobs-Inbox.`

## Trigger phrases (examples)

- "update job listing based on my jobs folder"
- "include the jobs in the job folder"
- "check Bio-Jobs-Inbox"
- "process the inbox emails"
