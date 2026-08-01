# Setup Guide — Retro Terminal GitHub Profile

This turns `github.com/JavaTypedScript` into a "special" self-updating
profile page. GitHub only renders a profile README when it lives in a
repo that has **the exact same name as your username**.

## 1. Create the special repository

1. Go to https://github.com/new
2. Repository name: **`JavaTypedScript`** (must match your username exactly)
3. Visibility: **Public**
4. Check "Add a README file" (you'll overwrite it)
5. Click **Create repository**

GitHub will show a banner on your profile confirming this repo powers
your profile page.

## 2. Add the files from this package

Clone it locally, or use the "Add file → Upload files" button on GitHub:

```
JavaTypedScript/
├── README.md
├── SETUP.md
└── .github/
    └── workflows/
        ├── snake.yml
        └── 3d-contrib.yml
```

```bash
git clone https://github.com/JavaTypedScript/JavaTypedScript.git
cd JavaTypedScript
# copy README.md, SETUP.md, and .github/ into this folder
git add .
git commit -m "feat: retro terminal profile"
git push origin main
```

## 3. Enable Actions permissions (required for both workflows)

The workflows commit back to your repo and push a new `output` branch,
so the default `GITHUB_TOKEN` needs write access:

1. Repo → **Settings → Actions → General**
2. Scroll to **Workflow permissions**
3. Select **Read and write permissions**
4. Save

## 4. Run the workflows once manually

1. Repo → **Actions** tab
2. Click **"3D Contribution Graph"** → **Run workflow** → Run workflow
3. Click **"Contribution Snake"** → **Run workflow** → Run workflow

Wait 1–2 minutes for each to finish (green checkmark).

- The 3D workflow commits SVGs into a `profile-3d-contrib/` folder on `main`.
- The snake workflow pushes SVGs to a new branch called `output`
  (created automatically — don't create it yourself).

After both have run once, refresh `https://github.com/JavaTypedScript`
and you should see the animated 3D graph and the snake eating your
contribution squares.

## 5. (Optional) Swap in your own color theme

- **Typing header**: edit the `readme-typing-svg.demolab.com` URL params
  (`color`, `font`, `lines`) at the top of `README.md`.
- **Stats cards**: `github-readme-stats` supports many themes — swap
  `theme=chartreuse-dark` for `dracula`, `synthwave`, `radical`, etc. at
  https://github.com/anuraghazra/github-readme-stats#themes
- **Streak stats**: same idea via the `?background=&stroke=&ring=&fire=`
  query params.
- **Snake palette**: change `?palette=github-dark` in `snake.yml` to any
  palette listed at https://github.com/Platane/snk#custom-palette

## 6. Keep it fresh

Both workflows are scheduled (`cron`) to re-run daily, so the 3D graph
and snake automatically reflect your latest contributions — no manual
maintenance needed once it's set up.

## Troubleshooting

| Symptom | Fix |
|---|---|
| Workflow fails with a 403 / permission error | Redo step 3 (Read and write permissions) |
| 3D graph / snake image shows "broken image" | Make sure you ran each workflow at least once (step 4) — the SVG paths in `README.md` don't exist until the first run |
| Stats card shows "user not found" | Double check the `username=` param matches `JavaTypedScript` exactly |
| Snake image never appears | Confirm an `output` branch was created; GitHub → branches dropdown |
