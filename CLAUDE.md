# Claude working notes — PamDx Data Analysis Guide

## Repo purpose

MkDocs documentation site published at:
**https://pamgene.github.io/PamGene_data_analysis_guide/**

Source is in `docs/`, built output is in `site/`, deployed via the `gh-pages` branch.

## Structure

```
docs/
├── index.md                                  # Homepage (contents to be added by user)
├── Tercen Data Analysis Guide/
│   ├── index.md                              # Preface / overview of Part 1
│   ├── Attachments/                          # All images for Part 1 chapters
│   ├── I. Experiment Design.md
│   ├── II. Image analysis.md
│   ├── III. Basic processing.md
│   ├── IV. Phosphosite analysis.md
│   ├── V. Kinase analysis.md
│   ├── VI. Further insights.md
│   └── Workflow Decisions in PamGene Data Analysis.md
└── PamDx methods/
    ├── index.md                              # Overview of Part 2
    ├── Attachments/                          # Images for Part 2 chapters
    ├── Limma.md
    └── UKA.md
```

## Commands

Use the miniconda Python — `mkdocs` is not on PATH:

```powershell
# Build site locally
C:\Users\dschuller\AppData\Local\miniconda3\python.exe -m mkdocs build --config-file mkdocs.yml

# Build with strict mode (turns warnings into errors — catches broken links)
C:\Users\dschuller\AppData\Local\miniconda3\python.exe -m mkdocs build --config-file mkdocs.yml --strict

# Deploy to GitHub Pages (publishes to gh-pages branch → live site)
C:\Users\dschuller\AppData\Local\miniconda3\python.exe -m mkdocs gh-deploy --config-file mkdocs.yml
```

## Before every commit

1. **Run a strict build** — catches broken internal links and missing nav files:
   ```powershell
   C:\Users\dschuller\AppData\Local\miniconda3\python.exe -m mkdocs build --config-file mkdocs.yml --strict
   ```
   Fix all warnings before committing. Common causes:
   - A file is listed in `nav` in `mkdocs.yml` but doesn't exist
   - A file exists in `docs/` but is missing from `nav` (shows as INFO, not an error)
   - An internal link uses a path relative to the wrong folder (e.g. a file inside a subfolder linking with the subfolder prefix again)

2. **Check image paths** — images are referenced relative to the `.md` file they're in. If a chapter file is inside `Tercen Data Analysis Guide/`, images should be `Attachments/da_xx.png`, not `../Attachments/...`.

3. **Check nav matches files** — every `.md` file in `docs/` should appear in `mkdocs.yml` nav, and every nav entry must point to a file that exists.

## After committing — deploy

Pushing to `main` does NOT update the live site. Always run `gh-deploy` after pushing:

```powershell
C:\Users\dschuller\AppData\Local\miniconda3\python.exe -m mkdocs gh-deploy --config-file mkdocs.yml
```

## Adding a new chapter

1. Create the `.md` file in the appropriate subfolder under `docs/`
2. Add it to `mkdocs.yml` nav in the correct position
3. If it needs images, add them to the `Attachments/` folder in the same subfolder
4. Run a strict build to verify no broken links
5. Commit, then `gh-deploy`
