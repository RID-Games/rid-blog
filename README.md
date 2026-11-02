# rid-blog — The Cardboard Supercomputer (field logs)

Static site, zero build step, zero dependencies. Plain HTML + one CSS block
per page, matching the RID homepage design system (JetBrains Mono / Hanken
Grotesk, void-navy + amber, HUD brackets).

## Structure

    index.html                              blog home (hero + log index)
    posts/27b-on-a-565-dollar-gpu/index.html  Field Log 001
    assets/                                  web-sized images (<=1600px)
    CNAME                                    blog.rebelintelligencedetachment.com

## Deploy (GitHub Pages, ~5 minutes)

1. Create a new public repo, e.g. `rid-blog`.
2. From this directory:

       git init && git add -A
       git commit -m "Field Log 001: 27B on a 565-dollar GPU"
       git branch -M main
       git remote add origin git@github.com:<you>/rid-blog.git
       git push -u origin main

3. Repo → Settings → Pages → Build and deployment: **Deploy from a branch**,
   branch `main` / `/ (root)`. GitHub reads the CNAME file automatically.
4. DNS (wherever rebelintelligencedetachment.com's DNS lives) — add:

       CNAME  blog  →  <you>.github.io

5. Wait for DNS, then enable **Enforce HTTPS** in Pages settings once the
   certificate is issued (a few minutes after DNS resolves).

## Adding a post

1. `mkdir posts/<slug>` and copy the structure of the existing post page
   (title, meta/OG tags, eyebrow with the next FIELD LOG number).
2. Resize any photo first: `ffmpeg -i in.jpg -vf "scale=1600:-2" -q:v 3 out.jpg`
3. Add a card to the log index in `index.html` (flip a STANDBY card to a live
   `<a class="log">` when it ships).
4. Commit + push. No build, no cache-busting needed (GitHub Pages invalidates).

## House rules

- **No `$` characters in prose** (renders as math in some MD viewers; write
  "dollars" / "USD"). Code blocks are exempt.
- Every number published must trace to a measurement artifact (probe JSON,
  samples.log, timing report). No vibes.
- Images: keep web-sized (<=1600px wide, q~82).
