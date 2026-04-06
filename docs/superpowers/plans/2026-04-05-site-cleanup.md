# Site Cleanup Implementation Plan

> **For agentic workers:** Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Strip all al-folio demo/template content and make paulroze.github.io a clean personal landing page with real data.

**Architecture:** Keep About (homepage), CV, and Repositories as the three visible nav pages. Delete all demo posts, projects, bibliography. Disable unused pages (teaching, publications, profiles, dropdown, blog, news). Apply Pavel's real CV/resume data from the old `claude/incomplete-description-*` branch. Fix all config values still pointing to al-folio defaults.

**Tech Stack:** Jekyll, al-folio theme, GitHub Pages

---

### Task 1: Create working branch

**Files:**

- None (git operation)

- [ ] **Step 1: Create and checkout branch**

```bash
git checkout -b cleanup/site-overhaul master
```

- [ ] **Step 2: Verify clean state**

```bash
git status
```

Expected: clean working tree on `cleanup/site-overhaul`

---

### Task 2: Delete all demo content files

**Files:**

- Delete: all 29 files in `_posts/`
- Delete: all 6 files in `_projects/`
- Delete: `_bibliography/papers.bib`
- Delete: `_pages/about_einstein.md`
- Delete: `_news/announcement_1.md`, `_news/announcement_2.md`, `_news/announcement_3.md`

- [ ] **Step 1: Remove demo blog posts**

```bash
rm _posts/*.md
```

- [ ] **Step 2: Remove demo projects**

```bash
rm _projects/*.md
```

- [ ] **Step 3: Remove Einstein bibliography**

```bash
rm _bibliography/papers.bib
```

- [ ] **Step 4: Remove Einstein about page**

```bash
rm _pages/about_einstein.md
```

- [ ] **Step 5: Remove placeholder news items**

```bash
rm _news/*.md
```

- [ ] **Step 6: Commit**

```bash
git add -A
git commit -m "Remove all demo/template content

Delete 29 demo blog posts, 6 placeholder projects, Einstein bibliography,
Einstein about page, and placeholder news announcements."
```

---

### Task 3: Fix \_config.yml

**Files:**

- Modify: `_config.yml`

Changes needed:

1. Add SEO keywords (line 15)
2. Enable `serve_og_meta: true` (line 61)
3. Enable `serve_schema_org: true` (line 62)
4. Set `og_image` to profile pic (line 63)
5. Fix `blog_name` from "al-folio" (line 129)
6. Fix `blog_description` (line 130)
7. Remove external_sources Medium feed (lines 163-165)
8. Fix scholar `last_name`/`first_name` (lines 293-294)
9. Clear `display_tags` and `display_categories` (lines 285-286)
10. Remove disqus_shortname (line 157)

- [ ] **Step 1: Apply all config fixes**

See exact edits in execution.

- [ ] **Step 2: Commit**

```bash
git add _config.yml
git commit -m "Fix _config.yml: SEO, blog name, remove al-folio defaults"
```

---

### Task 4: Apply real CV and resume data

**Files:**

- Modify: `_data/cv.yml` (full rewrite with Pavel's career data from old branch)
- Modify: `assets/json/resume.json` (full rewrite with Pavel's career data from old branch)

- [ ] **Step 1: Replace cv.yml with real data**

Use the CV data extracted from the old `claude/incomplete-description-*` branch.

- [ ] **Step 2: Replace resume.json with real data**

Use the resume JSON extracted from the old branch.

- [ ] **Step 3: Commit**

```bash
git add _data/cv.yml assets/json/resume.json
git commit -m "Replace Einstein demo data with Pavel's real CV and resume"
```

---

### Task 5: Update page files

**Files:**

- Modify: `_pages/about.md` — tighten the expanded bio (concise, not generic)
- Modify: `_pages/cv.md` — remove `cv_pdf: example_pdf.pdf`, fix description, set `nav: true`
- Modify: `_pages/repositories.md` — already `nav: true`, keep as-is
- Modify: `_pages/publications.md` — keep `nav: false` (no papers)
- Modify: `_pages/teaching.md` — keep `nav: false`
- Modify: `_pages/profiles.md` — keep `nav: false`
- Modify: `_pages/dropdown.md` — keep `nav: false`
- Modify: `_pages/blog.md` — keep `nav: false` (no posts)
- Modify: `_pages/projects.md` — keep `nav: false` (no projects)

- [ ] **Step 1: Update about.md** — add concise professional sections

- [ ] **Step 2: Fix cv.md** — remove example_pdf, update description, enable in nav

- [ ] **Step 3: Commit**

```bash
git add _pages/
git commit -m "Update about page, enable CV in nav, remove example PDF link"
```

---

### Task 6: Verify and push

- [ ] **Step 1: Review all changes**

```bash
git diff master --stat
git log --oneline master..HEAD
```

- [ ] **Step 2: Push branch**

```bash
git push -u origin cleanup/site-overhaul
```

- [ ] **Step 3: Create PR**
