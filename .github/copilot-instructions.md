# Copilot instructions

## Project overview

This repository is a personal CV / resume site for Silvano Coriani, served via **GitHub Pages**. There is no build tooling, package manager, or test suite — pushing to `main` triggers Jekyll on GitHub Pages and publishes the site at `https://scoriani.github.io/resume/cv.html`.

## Architecture

The site is intentionally tiny and flat at the repo root:

- `cv.html` — the actual resume page (entry point). Hand-written HTML with semantic class names (`resume`, `profile`, `skills-prog`, `skills-soft`, `experience`, etc.) used both for layout and as hooks for JS animations.
- `styles.css` — all styling for `cv.html`. Pure CSS, no preprocessor.
- `page.js` — jQuery-based animations for the skill bars (`.skills-prog .bar`) and circular skill indicators (`.skills-soft svg .cbar`). The bottom of the file contains an inline source map for the original CoffeeScript — **edit the JavaScript directly**, the CoffeeScript source is not part of the build.
- `_config.yml` — single line: `theme: jekyll-theme-minimal`. This theme applies to `README.md` / Markdown pages rendered by Jekyll, **not** to `cv.html`, which is served as-is.
- `docs/assets/images/` — images referenced from `cv.html` (e.g. `docs/assets/images/Silvano.jpg`, `cv.jpg`). Note the paths in `cv.html` are `docs/assets/images/...` even though the HTML lives at the repo root — keep this prefix when adding images.
- `README.md` — default GitHub Pages placeholder content, unrelated to the CV.

## Conventions

- **No build step.** Edit HTML/CSS/JS directly and commit; GitHub Pages rebuilds automatically. Preview locally by opening `cv.html` in a browser (it loads jQuery, Font Awesome, and Google Fonts from CDNs, so an internet connection is required).
- **Skill percentages are data-driven.** `page.js` reads `data-percent` from the parent of each `.skills-bar` / `.skills-soft li` to animate bars and circular meters. When adding a skill, set `data-percent="NN"` on the `<li>` rather than hard-coding widths in CSS.
- **Class names drive both layout and JS.** Don't rename `.skills-prog`, `.skills-bar`, `.bar`, `.skills-soft`, or `.cbar` without updating `page.js`.
- **jQuery is assumed to be globally available** in `page.js`. If you ever add new scripts, make sure jQuery is loaded first in `cv.html`.
- Content is in English; contact details and external links (Twitter, LinkedIn, GitHub, Amazon book link, Microsoft Docs articles) are intentional and should be preserved when restructuring sections.
