# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository overview

This is the marketing website for Apex Advisory Services, LLC, served via GitHub Pages at the custom domain `apexadvisorysvcs.com` (configured via `CNAME`). The entire site is a single self-contained file, `index.html` — there is no build system, package manager, bundler, or JavaScript framework. All CSS is in a `<style>` block in the `<head>`, and all behavior is in a small vanilla-JS `<script>` block at the end of the body.

## Working with this repo

- Edit `index.html` directly; there is nothing to compile or bundle.
- To preview locally, open `index.html` in a browser directly, or serve the directory with any static file server (e.g. `python3 -m http.server`) if relative-path/CORS behavior needs to be tested.
- There are no tests, linters, or CI pipelines configured. Verify changes by visually checking the page in a browser (the site uses scroll-triggered fade-in animations via `IntersectionObserver`, so check both above- and below-the-fold sections).
- Deployment is implicit: pushing to the branch served by GitHub Pages publishes the site directly. There is no separate build/deploy step.

## Structure of index.html

The page is a single-page site with anchor-linked navigation (`#about`, `#services`, `#packages`, `#clients`, `#contact`) into these sections, in order: `#hero`, `#about`, `#services`, `#packages`, `#clients`, `#contact`, and a `<footer>`.

- Styling uses CSS custom properties defined on `:root` (`--navy`, `--gold`, `--cream`, etc.) — reuse these variables rather than hardcoding new colors.
- Fonts are loaded from Google Fonts: `Playfair Display` (serif, used for headings) and `Jost` (sans, used for body text).
- Section-level layout follows a repeated pattern: a `.section-label`, `.section-title`, `.gold-rule` divider, and `.section-subtitle`, followed by section-specific grid content (`.services-grid`, `.packages-grid`, `.clients-grid`, etc.).
- Scroll-in animations are driven by the `.fade-up` class combined with the `IntersectionObserver` in the trailing `<script>` block; sibling cards within `.services-grid`, `.packages-grid`, and `.clients-grid` get staggered transition delays. New elements that should animate in on scroll need the `fade-up` class added.
- The contact form has no backend — submission just triggers a client-side `alert()`. There is no form-processing endpoint wired up.
