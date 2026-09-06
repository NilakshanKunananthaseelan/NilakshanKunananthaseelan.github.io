# Nilakshan Kunananthaseelan — research portfolio

A deliberately small Jekyll site for GitHub Pages. The site uses semantic HTML, one stylesheet, and no client-side JavaScript or third-party UI framework.

## Run locally

```bash
bundle install
bundle exec jekyll serve
```

Then visit `http://127.0.0.1:4000`.

## Add a publication

Edit `_data/publications.yml`. Each publication can contain a title, year, venue, authors, short description, internal paper-page URL, and any number of external links. Set `featured: true` to include it on the home page.

Create the matching paper page in `_papers` using an existing file as a template. The `paper_id` in its front matter must match the publication's `slug`. Jekyll publishes these pages at `/papers/<filename>/`.

## Write a post

Create a Markdown file in `_posts` using the filename format `YYYY-MM-DD-short-title.md`:

```yaml
---
layout: post
title: "A clear title"
date: 2026-08-17
description: "A one-sentence summary used on the writing index."
categories: writing
reading_time: 6
---
```

Everything after the front matter is ordinary Markdown. Only posts with the `writing` category appear in the public writing index, which keeps publication records and essays separate.

## Main content

- `index.html` — home page
- `research.md` — research programme and publications
- `writing.md` — essay index
- `about.md` — biography, experience, and service
- `_data/publications.yml` — publication data
- `style.scss` — complete visual system
