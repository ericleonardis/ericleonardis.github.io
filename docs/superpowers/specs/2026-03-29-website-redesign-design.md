# Website Redesign — Design Spec

## Overview

Redesign of ericleonardis.github.io from a single-page academic site into a multi-page professional portfolio. Gallery-minimal aesthetic with thin typography, generous whitespace, and grid layouts. Static HTML + CSS, no frameworks or build tools.

## Design System

### Typography
- **Font family**: Helvetica Neue, Helvetica, Arial, sans-serif (system stack)
- **Headings**: Weight 300 (thin) for page titles, 500-600 for card titles
- **Body**: Weight 300-400, 13-15px, color #666
- **Labels/Nav**: Uppercase, letter-spacing 1.5-2.5px, 10-12px, color #999
- **Line height**: 1.6-1.7 for body text

### Colors
- **Background**: #fcfcfc (near-white)
- **Text**: #1a1a1a (near-black headings), #666 (body), #999 (secondary/labels)
- **Borders**: #e8e8e8 (nav/footer), #eee (cards/dividers)
- **Category accents**:
  - Research: #2563eb (blue)
  - Film: #7c3aed (purple)
  - Sci Comm: #059669 (green)
  - Music: #d97706 (amber)

### Spacing
- **Page horizontal padding**: 48px
- **Section vertical padding**: 36-48px
- **Grid gaps**: 20-24px
- **Hero top padding**: 64px

### Components
- **Cards**: White background, 1px solid #eee border, 4px border-radius, 24px padding. Subtle hover (border darkens to #ccc).
- **Featured cards**: Horizontal layout — image left (280px), text right. Larger padding (32px).
- **List items**: Title left, venue/year right, separated by 1px #f0f0f0 bottom border.
- **Section labels**: 10px uppercase with 2.5px letter-spacing, color #999.
- **Dividers**: 1px solid #eee, full width within padding.
- **Category tags**: 9px uppercase, 2px letter-spacing, category accent color.

## Navigation

**Order**: Home | Research | Resume | CV | Sci Comm | Film | Music

- Horizontal bar, logo left ("ERIC LEONARDIS" — thin uppercase, letter-spaced), links right
- 1px bottom border
- Active page indicated by darker text color (#1a1a1a vs #999)
- Resume and CV links open PDFs directly (no dedicated page)
- Same nav on every page
- Responsive: collapses to hamburger menu on mobile

## Pages

### Home (index.html)

**Purpose**: Curated landing page — professional first impression, highlights from each area.

**Sections in order**:
1. **Hero** — "**Eric Leonardis**, PhD" (h1, thin weight with bold name). One-liner subtitle describing role and interests. Max-width ~620px.
2. **Research** — Section label "Research". 2-column grid of cards for NeurIPS paper and MIMIC-MJX. Each card has: category tag, image/visual, title, author list, short description.
3. **Documents** — Section label "Documents". Two compact inline cards linking to Resume PDF and CV PDF. Each shows a small PDF icon, title, and subtitle.
4. **Science Communication** — Section label "Science Communication". 2-column grid: Body Horror talk card, WIRED interview card. Each has category tag, title, description.
5. **Film** — Section label "Film". Single horizontal featured card for Comic-Con panel (image left, text right).
6. **Footer** — Email left, GitHub right. 1px top border.

All highlight cards link to their respective full pages or external resources.

### Research (research.html)

**Purpose**: Most important page. Full research portfolio.

**Sections**:
1. **Page header** — "Research" (h2, thin weight). Subtitle describing research focus.
2. **Featured** — Section label "Featured". Two horizontal featured cards:
   - NeurIPS 2025 paper: image, tag ("NeurIPS 2025"), title, **full author list**, description, venue/date metadata, arXiv link.
   - MIMIC-MJX: image, tag ("Preprint"), title, **full author list**, description, arXiv link.
3. **Publications** — Section label "Publications". Clean list format: title | authors | venue/year. Each entry is a row with title and authors on the left, venue on the right. Links to PDFs or external sources. Includes:
   - Interactive Neurorobotics (Frontiers in Psychology)
   - Convergent Cross Sorting (Scientific Reports)
   - PiRat Robot Interaction (IROS 2018)
   - Amygdala study (2017)
   - Hippocampus study (2017)
   - Conceptual Blending paper

### Film (film.html)

**Purpose**: Film and media panel work.

**Sections**:
1. **Page header** — "Film" (h2). Subtitle about AI, neuroscience, and storytelling in media.
2. **Featured** — Comic-Con panel as horizontal featured card with photo, description, credits.
3. **Events** — List format for other film events and panels. Title | venue/organization.

### Sci Comm (scicomm.html)

**Purpose**: Public-facing science communication — talks, press, outreach.

**Sections**:
1. **Page header** — "Science Communication" (h2). Subtitle about bridging neuroscience and public.
2. **Featured** — Body Horror and the Brain talk as horizontal featured card. Embedded YouTube video or link.
3. **Press & Interviews** — List section. WIRED interview and other press items.
4. **Talks & Lectures** — List section. Public talks with venue and year.

Some overlap with Film page is expected and fine (e.g., Body Horror talk appears on both).

### Music (music.html)

**Purpose**: Bonus page — DJ events and music profile. Not linked from homepage.

**Sections**:
1. **Page header** — "Music" (h2). Brief subtitle.
2. **Events** — 3-column flyer grid. Each cell: flyer image, event name below, venue and date below that.
3. **Links** — Resident Advisor profile, SoundCloud, or other music platform links.

### Resume & CV

No dedicated HTML pages. Nav links point directly to PDF files:
- Resume: `/CV/EricLeonardisResume.pdf` (or current filename)
- CV: `/CV/EricLeonardisCV.pdf`

## Technical Approach

- **Static HTML + CSS**: One `.html` file per page, one shared `css/main.css`
- **No JavaScript required** for core functionality. Optional: small script for mobile hamburger menu toggle.
- **No frameworks**: No Bootstrap, no React, no build tools. Hand-coded.
- **Images**: Existing images from current site (SalkImage, comicconpic, mimic.jpg, mousearm.png). Optimized with max-width: 100% for responsiveness.
- **PDFs**: Existing PDFs stay in current locations.
- **Responsive**: CSS media queries for mobile (< 768px). Single column layout on mobile, nav collapses to hamburger.
- **GitHub Pages**: Continues to use Jekyll minimal theme config or switches to plain HTML (no Jekyll needed if not using templates).

## File Structure

```
/
├── index.html          (Home)
├── research.html       (Research)
├── film.html           (Film)
├── scicomm.html        (Sci Comm)
├── music.html          (Music)
├── css/
│   └── main.css        (Shared stylesheet)
├── images/
│   ├── SalkImage_Leonardis.jpg
│   ├── comicconpic.jpg
│   ├── mimic.jpg
│   ├── mousearm.png
│   └── (flyer images TBD)
├── CV/
│   ├── EricLeonardisCV.pdf
│   └── (resume PDF)
└── _config.yml         (Jekyll config — may simplify or remove)
```

## Responsive Behavior

- **Desktop (> 1024px)**: Full layout as designed. Max content width ~1100px.
- **Tablet (768-1024px)**: 2-column grids become 1-column. Featured cards stack vertically. Padding reduces to 32px.
- **Mobile (< 768px)**: Single column throughout. Nav collapses to hamburger menu. Hero text smaller. Flyer grid becomes 2 columns.

## Content Notes

- All research entries must include **full author lists** (e.g., "Leonardis, E., Smith, J., ...").
- Author lists appear on both featured cards and publication list items.
- Category tags use accent colors consistently across all pages.
- External links (arXiv, YouTube, WIRED) open in new tabs.
- Embedded YouTube videos on Sci Comm page for Body Horror talk and PiRat video.
