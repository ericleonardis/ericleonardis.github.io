# Website Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Redesign ericleonardis.github.io from a single-page academic site into a multi-page gallery-minimal professional portfolio.

**Architecture:** Static HTML + CSS with no frameworks or build tools. One shared stylesheet (`css/main.css`), one HTML file per page. Nav and footer are duplicated per page (no JS templating). Responsive via CSS media queries.

**Tech Stack:** HTML5, CSS3, GitHub Pages

---

## File Structure

```
/
├── index.html          (Home — rewrite)
├── research.html       (Research — new)
├── film.html           (Film — new)
├── scicomm.html        (Sci Comm — new)
├── music.html          (Music — new)
├── css/
│   └── main.css        (Shared stylesheet — rewrite)
├── images/             (existing images, unchanged)
├── CV/                 (existing PDFs, unchanged)
└── _config.yml         (simplify for plain HTML)
```

---

### Task 1: Shared CSS (`css/main.css`)

**Files:**
- Rewrite: `css/main.css`

- [ ] **Step 1: Write the complete stylesheet**

Replace `css/main.css` with:

```css
/* === Reset === */
*, *::before, *::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* === Base === */
body {
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  background: #fcfcfc;
  color: #1a1a1a;
  -webkit-font-smoothing: antialiased;
}

a {
  color: inherit;
  text-decoration: none;
}

img {
  max-width: 100%;
  height: auto;
  display: block;
}

/* === Layout === */
.page-wrap {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 48px;
}

/* === Nav === */
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 24px 48px;
  border-bottom: 1px solid #e8e8e8;
  background: #fff;
}

nav .logo {
  font-size: 15px;
  font-weight: 300;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: #1a1a1a;
  text-decoration: none;
}

nav .nav-links {
  display: flex;
  gap: 24px;
  list-style: none;
}

nav .nav-links a {
  font-size: 11px;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: #999;
  font-weight: 400;
  transition: color 0.2s;
}

nav .nav-links a:hover,
nav .nav-links a.active {
  color: #1a1a1a;
}

/* Hamburger (hidden on desktop) */
.nav-toggle {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
}

.nav-toggle span {
  display: block;
  width: 20px;
  height: 2px;
  background: #1a1a1a;
  margin: 4px 0;
  transition: 0.2s;
}

/* === Sections === */
.section {
  padding: 36px 0;
}

.section-label {
  font-size: 10px;
  letter-spacing: 2.5px;
  text-transform: uppercase;
  color: #999;
  margin-bottom: 20px;
  font-weight: 500;
}

.divider {
  height: 1px;
  background: #eee;
}

/* === Hero === */
.hero {
  padding: 64px 0 48px;
}

.hero h1 {
  font-size: 38px;
  font-weight: 300;
  letter-spacing: -0.5px;
  line-height: 1.2;
  margin-bottom: 14px;
}

.hero h1 strong {
  font-weight: 600;
}

.hero .subtitle {
  font-size: 15px;
  color: #666;
  line-height: 1.7;
  max-width: 620px;
  font-weight: 300;
}

/* === Page Header (subpages) === */
.page-header {
  padding: 48px 0 36px;
}

.page-header h1 {
  font-size: 32px;
  font-weight: 300;
  letter-spacing: -0.3px;
  margin-bottom: 8px;
}

.page-header .subtitle {
  font-size: 14px;
  color: #666;
  font-weight: 300;
  line-height: 1.6;
  max-width: 560px;
}

/* === Tags === */
.tag {
  font-size: 9px;
  letter-spacing: 2px;
  text-transform: uppercase;
  font-weight: 600;
  margin-bottom: 8px;
  display: inline-block;
}

.tag-research { color: #2563eb; }
.tag-film { color: #7c3aed; }
.tag-scicomm { color: #059669; }
.tag-music { color: #d97706; }

/* === Cards === */
.card-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

.card {
  background: #fff;
  border: 1px solid #eee;
  border-radius: 4px;
  padding: 24px;
  transition: border-color 0.2s;
  text-decoration: none;
  color: inherit;
  display: block;
}

.card:hover {
  border-color: #ccc;
}

.card .card-img {
  border-radius: 3px;
  margin-bottom: 14px;
  overflow: hidden;
}

.card h3 {
  font-size: 15px;
  font-weight: 500;
  margin-bottom: 4px;
  line-height: 1.4;
}

.card .authors {
  font-size: 12px;
  color: #888;
  font-weight: 300;
  margin-bottom: 6px;
  line-height: 1.4;
}

.card p {
  font-size: 12px;
  color: #666;
  line-height: 1.6;
  font-weight: 300;
}

/* === Featured Card (horizontal) === */
.featured-card {
  background: #fff;
  border: 1px solid #eee;
  border-radius: 4px;
  padding: 32px;
  display: flex;
  gap: 28px;
  transition: border-color 0.2s;
  text-decoration: none;
  color: inherit;
  margin-bottom: 24px;
}

.featured-card:last-child {
  margin-bottom: 0;
}

.featured-card:hover {
  border-color: #ccc;
}

.featured-card .featured-img {
  width: 280px;
  flex-shrink: 0;
  border-radius: 3px;
  overflow: hidden;
}

.featured-card .featured-img img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.featured-card h3 {
  font-size: 18px;
  font-weight: 500;
  margin-bottom: 4px;
  line-height: 1.3;
}

.featured-card .authors {
  font-size: 13px;
  color: #888;
  font-weight: 300;
  margin-bottom: 8px;
  line-height: 1.4;
}

.featured-card p {
  font-size: 13px;
  color: #666;
  line-height: 1.6;
  font-weight: 300;
}

.featured-card .meta {
  font-size: 11px;
  color: #999;
  margin-top: 12px;
  letter-spacing: 0.5px;
}

/* === Document Cards (Resume/CV) === */
.doc-cards {
  display: flex;
  gap: 16px;
}

.doc-card {
  border: 1px solid #eee;
  border-radius: 4px;
  padding: 18px 32px;
  background: #fff;
  display: flex;
  align-items: center;
  gap: 12px;
  transition: border-color 0.2s;
  text-decoration: none;
  color: inherit;
}

.doc-card:hover {
  border-color: #ccc;
}

.doc-card .doc-icon {
  width: 32px;
  height: 40px;
  background: #f0f0f0;
  border-radius: 2px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 9px;
  color: #bbb;
  letter-spacing: 0.5px;
  font-weight: 500;
}

.doc-card .doc-title {
  font-size: 13px;
  font-weight: 500;
}

.doc-card .doc-sub {
  font-size: 11px;
  color: #999;
  margin-top: 2px;
}

/* === List Items (publications, events) === */
.pub-list {
  list-style: none;
}

.pub-item {
  padding: 16px 0;
  border-bottom: 1px solid #f0f0f0;
}

.pub-item:last-child {
  border-bottom: none;
}

.pub-item a {
  display: block;
  text-decoration: none;
  color: inherit;
  transition: color 0.2s;
}

.pub-item a:hover .pub-title {
  color: #2563eb;
}

.pub-item .pub-title {
  font-size: 14px;
  font-weight: 400;
  margin-bottom: 2px;
  transition: color 0.2s;
}

.pub-item .pub-authors {
  font-size: 12px;
  color: #888;
  font-weight: 300;
  margin-bottom: 2px;
}

.pub-item .pub-venue {
  font-size: 12px;
  color: #999;
}

/* === Flyer Grid (Music) === */
.flyer-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

.flyer-item img {
  border-radius: 3px;
  margin-bottom: 10px;
}

.flyer-item .flyer-title {
  font-size: 13px;
  font-weight: 500;
}

.flyer-item .flyer-sub {
  font-size: 11px;
  color: #999;
}

/* === Video Embed === */
.video-wrap {
  position: relative;
  padding-bottom: 56.25%;
  height: 0;
  overflow: hidden;
  border-radius: 4px;
  margin-top: 16px;
}

.video-wrap iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: 0;
}

/* === Footer === */
footer {
  padding: 32px 0;
  border-top: 1px solid #e8e8e8;
  margin-top: 40px;
  display: flex;
  justify-content: space-between;
  font-size: 11px;
  color: #999;
  letter-spacing: 0.5px;
}

footer a {
  color: #666;
  transition: color 0.2s;
}

footer a:hover {
  color: #1a1a1a;
}

/* === Responsive === */
@media (max-width: 768px) {
  nav {
    padding: 20px 24px;
  }

  nav .nav-links {
    display: none;
    flex-direction: column;
    position: absolute;
    top: 60px;
    left: 0;
    right: 0;
    background: #fff;
    border-bottom: 1px solid #e8e8e8;
    padding: 16px 24px;
    gap: 16px;
  }

  nav .nav-links.open {
    display: flex;
  }

  .nav-toggle {
    display: block;
  }

  .page-wrap {
    padding: 0 24px;
  }

  .hero {
    padding: 40px 0 32px;
  }

  .hero h1 {
    font-size: 28px;
  }

  .page-header h1 {
    font-size: 26px;
  }

  .card-grid {
    grid-template-columns: 1fr;
  }

  .featured-card {
    flex-direction: column;
  }

  .featured-card .featured-img {
    width: 100%;
    max-height: 200px;
  }

  .doc-cards {
    flex-direction: column;
  }

  .flyer-grid {
    grid-template-columns: 1fr 1fr;
  }

  footer {
    flex-direction: column;
    gap: 8px;
  }
}
```

- [ ] **Step 2: Verify the file renders**

Open `css/main.css` and confirm it's valid CSS with no syntax errors. Check file size is reasonable (~300 lines).

- [ ] **Step 3: Commit**

```bash
git add css/main.css
git commit -m "feat: rewrite main.css with gallery-minimal design system"
```

---

### Task 2: Home Page (`index.html`)

**Files:**
- Rewrite: `index.html`

- [ ] **Step 1: Write the complete homepage**

Replace `index.html` with:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Eric Leonardis, PhD</title>
  <link rel="stylesheet" href="/css/main.css">
</head>
<body>

  <nav>
    <a href="/" class="logo">Eric Leonardis</a>
    <button class="nav-toggle" aria-label="Toggle navigation" onclick="document.querySelector('.nav-links').classList.toggle('open')">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links">
      <li><a href="/" class="active">Home</a></li>
      <li><a href="/research.html">Research</a></li>
      <li><a href="/CV/ResumeEricLeonardis.pdf">Resume</a></li>
      <li><a href="/CV/EricLeonardisCV.pdf">CV</a></li>
      <li><a href="/scicomm.html">Sci Comm</a></li>
      <li><a href="/film.html">Film</a></li>
      <li><a href="/music.html">Music</a></li>
    </ul>
  </nav>

  <div class="page-wrap">

    <div class="hero">
      <h1><strong>Eric Leonardis</strong>, PhD</h1>
      <p class="subtitle">
        Postdoctoral fellow in systems neuroscience at the Salk Institute for Biological Studies.
        I build computational models of biological motor control, speak about AI and film,
        and serve as a scientific advisor for the National Academy of Sciences Science &amp; Entertainment Exchange.
      </p>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Research</div>
      <div class="card-grid">
        <a href="/research.html" class="card">
          <div class="tag tag-research">NeurIPS 2025</div>
          <div class="card-img">
            <img src="/mousearm.png" alt="Mouse Forelimb Imitation Learning">
          </div>
          <h3>Massively Parallel Imitation Learning of Mouse Forelimb Musculoskeletal Reaching Dynamics</h3>
          <div class="authors">Leonardis, E. J., Bhagat, S., Lobato-Rios, D., Pereira, T. D., Azim, E.</div>
          <p>1M+ steps/sec via JAX and MuJoCo-MJX. Data on the Brain &amp; Mind Workshop.</p>
        </a>
        <a href="/research.html" class="card">
          <div class="tag tag-research">Preprint</div>
          <div class="card-img">
            <img src="/mimic.jpg" alt="MIMIC-MJX Framework">
          </div>
          <h3>MIMIC-MJX: Neuromechanical Emulation of Animal Behavior</h3>
          <div class="authors">Lobato-Rios, D., Leonardis, E. J., et al.</div>
          <p>Data-driven biomechanical control framework integrating stac-mjx and track-mjx.</p>
        </a>
      </div>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Documents</div>
      <div class="doc-cards">
        <a href="/CV/ResumeEricLeonardis.pdf" class="doc-card" target="_blank">
          <div class="doc-icon">PDF</div>
          <div>
            <div class="doc-title">Resume</div>
            <div class="doc-sub">1 page overview</div>
          </div>
        </a>
        <a href="/CV/EricLeonardisCV.pdf" class="doc-card" target="_blank">
          <div class="doc-icon">PDF</div>
          <div>
            <div class="doc-title">Curriculum Vitae</div>
            <div class="doc-sub">Full academic record</div>
          </div>
        </a>
      </div>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Science Communication</div>
      <div class="card-grid">
        <a href="/scicomm.html" class="card">
          <div class="tag tag-scicomm">Talk</div>
          <h3>Body Horror and the Brain</h3>
          <p>Neurohumanities Network &amp; Harvard Medical School. Visceral responses, the insular cortex, and horror in media.</p>
        </a>
        <a href="https://www.wired.com/story/game-horror-sounds-psychology-dead-space-remake-scorn/" class="card" target="_blank" rel="noopener">
          <div class="tag tag-scicomm">Press</div>
          <h3>WIRED — What Creepy Video Game Sounds Do to Your Brain</h3>
          <p>Interview on body horror, the insular cortex, and embodied cognition in video games.</p>
        </a>
      </div>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Film</div>
      <a href="/film.html" class="featured-card">
        <div class="featured-img">
          <img src="/comicconpic.jpg" alt="Eric Leonardis at Comic-Con">
        </div>
        <div>
          <div class="tag tag-film">Comic-Con International</div>
          <h3>Evolution of AI in Film and In Reality</h3>
          <p>Panel on how modern AI influences storytelling, scientific communication, and ethics. Organized by Andrea Decker.</p>
        </div>
      </a>
    </div>

    <footer>
      <span><a href="mailto:leonardiseric@gmail.com">leonardiseric@gmail.com</a></span>
      <span><a href="https://github.com/ericleonardis" target="_blank" rel="noopener">GitHub</a></span>
    </footer>

  </div>

</body>
</html>
```

- [ ] **Step 2: Open in browser and verify layout**

Run: `open index.html` or view at localhost via GitHub Pages dev server. Verify:
- Nav displays all 7 links
- Hero section renders with bold name
- Research cards show with images, author lists, and descriptions
- Document cards link to PDFs
- Sci Comm and Film sections render
- Footer displays

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: rewrite homepage with gallery-minimal design"
```

---

### Task 3: Research Page (`research.html`)

**Files:**
- Create: `research.html`

- [ ] **Step 1: Write the complete research page**

Create `research.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Research — Eric Leonardis</title>
  <link rel="stylesheet" href="/css/main.css">
</head>
<body>

  <nav>
    <a href="/" class="logo">Eric Leonardis</a>
    <button class="nav-toggle" aria-label="Toggle navigation" onclick="document.querySelector('.nav-links').classList.toggle('open')">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links">
      <li><a href="/">Home</a></li>
      <li><a href="/research.html" class="active">Research</a></li>
      <li><a href="/CV/ResumeEricLeonardis.pdf">Resume</a></li>
      <li><a href="/CV/EricLeonardisCV.pdf">CV</a></li>
      <li><a href="/scicomm.html">Sci Comm</a></li>
      <li><a href="/film.html">Film</a></li>
      <li><a href="/music.html">Music</a></li>
    </ul>
  </nav>

  <div class="page-wrap">

    <div class="page-header">
      <h1>Research</h1>
      <p class="subtitle">
        Computational models of biological motor control, neurorobotics, and dynamical systems analysis.
      </p>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Featured</div>

      <a href="https://arxiv.org/pdf/2511.21848v1" class="featured-card" target="_blank" rel="noopener">
        <div class="featured-img">
          <img src="/mousearm.png" alt="Mouse Forelimb Imitation Learning">
        </div>
        <div>
          <div class="tag tag-research">NeurIPS 2025</div>
          <h3>Massively Parallel Imitation Learning of Mouse Forelimb Musculoskeletal Reaching Dynamics</h3>
          <div class="authors">Leonardis, E. J., Bhagat, S., Lobato-Rios, D., Pereira, T. D., Azim, E.</div>
          <p>
            Accepted to the NeurIPS 2025 — Data on the Brain &amp; Mind Workshop, December 7, San Diego, CA.
            Uses MIMIC-MJX with JAX and MuJoCo-MJX to achieve more than 1 million steps per second
            through the physics and RL environment.
          </p>
          <div class="meta">arXiv 2025 · San Diego, CA</div>
        </div>
      </a>

      <a href="https://arxiv.org/abs/2511.20532" class="featured-card" target="_blank" rel="noopener">
        <div class="featured-img">
          <img src="/mimic.jpg" alt="MIMIC-MJX Framework">
        </div>
        <div>
          <div class="tag tag-research">Preprint</div>
          <h3>MIMIC-MJX: Neuromechanical Emulation of Animal Behavior</h3>
          <div class="authors">Lobato-Rios, D., Leonardis, E. J., et al.</div>
          <p>
            Collaborative framework integrating stac-mjx and track-mjx for data-driven control
            of biomechanical bodies in physics simulation. High-speed imitation learning from motion capture data.
          </p>
          <div class="meta">arXiv 2025</div>
        </div>
      </a>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Publications</div>
      <ul class="pub-list">
        <li class="pub-item">
          <a href="https://www.frontiersin.org/articles/10.3389/fpsyg.2022.897603/full" target="_blank" rel="noopener">
            <div class="pub-title">Interactive Neurorobotics</div>
            <div class="pub-authors">Leonardis, E. J., Breston, L., Samad Rodriguez, T., Quinn, L. K., Bhatt, B., Chiba, A. A.</div>
            <div class="pub-venue">Frontiers in Psychology, 2022</div>
          </a>
        </li>
        <li class="pub-item">
          <a href="/ConvergentCrossSorting_BrestonLeonardisetal2021.pdf" target="_blank">
            <div class="pub-title">Convergent Cross Sorting for Estimating Dynamic Coupling</div>
            <div class="pub-authors">Breston, L., Leonardis, E. J., Quinn, L. K., Bhatt, B., Chiba, A. A.</div>
            <div class="pub-venue">Scientific Reports, 2021</div>
          </a>
        </li>
        <li class="pub-item">
          <a href="/PiRatHeathLeonardis2018.pdf" target="_blank">
            <div class="pub-title">PiRat: An Autonomous Framework for Studying Social Behavior in Rats and Robots</div>
            <div class="pub-authors">Heath, S., Wiles, J., Quinn, L. K., Leonardis, E. J., Chiba, A. A.</div>
            <div class="pub-venue">IROS 2018</div>
          </a>
        </li>
        <li class="pub-item">
          <a href="/AmygdalaLeonardis2017 (1).pdf" target="_blank">
            <div class="pub-title">Amygdala Study</div>
            <div class="pub-authors">Leonardis, E. J., et al.</div>
            <div class="pub-venue">2017</div>
          </a>
        </li>
        <li class="pub-item">
          <a href="/hippocampusleonardis2017.pdf" target="_blank">
            <div class="pub-title">Hippocampus Study</div>
            <div class="pub-authors">Leonardis, E. J., et al.</div>
            <div class="pub-venue">2017</div>
          </a>
        </li>
        <li class="pub-item">
          <a href="/ConceptualBlendinginAnimals_CogSciSymposia_7_27.pdf" target="_blank">
            <div class="pub-title">Conceptual Blending in Animals</div>
            <div class="pub-authors">Leonardis, E. J., et al.</div>
            <div class="pub-venue">CogSci Symposia</div>
          </a>
        </li>
      </ul>
    </div>

    <footer>
      <span><a href="mailto:leonardiseric@gmail.com">leonardiseric@gmail.com</a></span>
      <span><a href="https://github.com/ericleonardis" target="_blank" rel="noopener">GitHub</a></span>
    </footer>

  </div>

</body>
</html>
```

- [ ] **Step 2: Verify in browser**

Check featured cards show images and author lists. Check publication list items are clickable and link to correct PDFs/URLs.

- [ ] **Step 3: Commit**

```bash
git add research.html
git commit -m "feat: add research page with featured papers and publication list"
```

---

### Task 4: Film Page (`film.html`)

**Files:**
- Create: `film.html`

- [ ] **Step 1: Write the complete film page**

Create `film.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Film — Eric Leonardis</title>
  <link rel="stylesheet" href="/css/main.css">
</head>
<body>

  <nav>
    <a href="/" class="logo">Eric Leonardis</a>
    <button class="nav-toggle" aria-label="Toggle navigation" onclick="document.querySelector('.nav-links').classList.toggle('open')">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links">
      <li><a href="/">Home</a></li>
      <li><a href="/research.html">Research</a></li>
      <li><a href="/CV/ResumeEricLeonardis.pdf">Resume</a></li>
      <li><a href="/CV/EricLeonardisCV.pdf">CV</a></li>
      <li><a href="/scicomm.html">Sci Comm</a></li>
      <li><a href="/film.html" class="active">Film</a></li>
      <li><a href="/music.html">Music</a></li>
    </ul>
  </nav>

  <div class="page-wrap">

    <div class="page-header">
      <h1>Film</h1>
      <p class="subtitle">
        Exploring AI, neuroscience, and storytelling through panels, consulting, and media.
        Scientific advisor for the National Academy of Sciences Science &amp; Entertainment Exchange.
      </p>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Featured</div>

      <div class="featured-card">
        <div class="featured-img">
          <img src="/comicconpic.jpg" alt="Eric Leonardis at Comic-Con">
        </div>
        <div>
          <div class="tag tag-film">Comic-Con International</div>
          <h3>Evolution of AI in Film and In Reality</h3>
          <p>
            I spoke at Comic-Con International on the "Evolution of AI in Film and In Reality" panel,
            sharing my work at the intersection of AI, neuroscience, and media. I discussed how modern AI
            influences storytelling, scientific communication, and ethics. The room was packed, and I'm grateful
            to Andrea Decker for organizing the event.
          </p>
          <div class="meta">San Diego, CA</div>
        </div>
      </div>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Events &amp; Panels</div>
      <ul class="pub-list">
        <li class="pub-item">
          <div class="pub-title">Body Horror and the Brain</div>
          <div class="pub-venue">Neurohumanities Network / Harvard Medical School, 2024</div>
        </li>
        <li class="pub-item">
          <div class="pub-title">The Science Behind Science Fiction</div>
          <div class="pub-venue">Horrible Imaginings Film Festival</div>
        </li>
        <li class="pub-item">
          <div class="pub-title">Science and Entertainment Exchange — Film Script Advising</div>
          <div class="pub-venue">National Academy of Sciences</div>
        </li>
      </ul>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Media</div>
      <ul class="pub-list">
        <li class="pub-item">
          <a href="https://www.kpbs.org/" target="_blank" rel="noopener">
            <div class="pub-title">KPBS Cinema Junkie Podcast</div>
            <div class="pub-venue">Recurring Guest</div>
          </a>
        </li>
      </ul>
    </div>

    <footer>
      <span><a href="mailto:leonardiseric@gmail.com">leonardiseric@gmail.com</a></span>
      <span><a href="https://github.com/ericleonardis" target="_blank" rel="noopener">GitHub</a></span>
    </footer>

  </div>

</body>
</html>
```

- [ ] **Step 2: Verify in browser**

Check Comic-Con featured card renders with image. Check event list items display correctly.

- [ ] **Step 3: Commit**

```bash
git add film.html
git commit -m "feat: add film page with featured panel and events list"
```

---

### Task 5: Sci Comm Page (`scicomm.html`)

**Files:**
- Create: `scicomm.html`

- [ ] **Step 1: Write the complete sci comm page**

Create `scicomm.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Science Communication — Eric Leonardis</title>
  <link rel="stylesheet" href="/css/main.css">
</head>
<body>

  <nav>
    <a href="/" class="logo">Eric Leonardis</a>
    <button class="nav-toggle" aria-label="Toggle navigation" onclick="document.querySelector('.nav-links').classList.toggle('open')">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links">
      <li><a href="/">Home</a></li>
      <li><a href="/research.html">Research</a></li>
      <li><a href="/CV/ResumeEricLeonardis.pdf">Resume</a></li>
      <li><a href="/CV/EricLeonardisCV.pdf">CV</a></li>
      <li><a href="/scicomm.html" class="active">Sci Comm</a></li>
      <li><a href="/film.html">Film</a></li>
      <li><a href="/music.html">Music</a></li>
    </ul>
  </nav>

  <div class="page-wrap">

    <div class="page-header">
      <h1>Science Communication</h1>
      <p class="subtitle">
        Public talks, press, and outreach bridging neuroscience, AI, and culture.
      </p>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Featured</div>

      <div class="featured-card">
        <div class="featured-img">
          <img src="/images/ericnerdnitecomiccon3.jpg" alt="Eric Leonardis presenting">
        </div>
        <div>
          <div class="tag tag-scicomm">Talk</div>
          <h3>Body Horror and the Brain</h3>
          <p>
            Lecture with the Neurohumanities Network and Harvard Medical School on visceral responses,
            the insular cortex, and horror in media. Exploring how our brains process body horror
            and what that tells us about embodied cognition.
          </p>
          <div class="meta">2024 · Neurohumanities Network</div>
        </div>
      </div>

      <div class="video-wrap">
        <iframe
          src="https://www.youtube.com/embed/K9SOa6mo79Q?si=6b4XGmXhxNlMYpRr"
          title="Body Horror and the Brain — Eric Leonardis"
          allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
          allowfullscreen>
        </iframe>
      </div>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Press &amp; Interviews</div>
      <ul class="pub-list">
        <li class="pub-item">
          <a href="https://www.wired.com/story/game-horror-sounds-psychology-dead-space-remake-scorn/" target="_blank" rel="noopener">
            <div class="pub-title">What Creepy Video Game Sounds Do to Your Brain</div>
            <div class="pub-authors">Farokhmanesh, M. (2023)</div>
            <div class="pub-venue">WIRED</div>
          </a>
        </li>
      </ul>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Talks &amp; Lectures</div>
      <ul class="pub-list">
        <li class="pub-item">
          <a href="https://youtu.be/K9SOa6mo79Q?si=EUJoXRbPZSd_FCrT" target="_blank" rel="noopener">
            <div class="pub-title">Body Horror and the Brain</div>
            <div class="pub-venue">Neurohumanities Network / Harvard Medical School, 2024</div>
          </a>
        </li>
        <li class="pub-item">
          <div class="pub-title">The Science Behind Science Fiction</div>
          <div class="pub-venue">Horrible Imaginings Film Festival</div>
        </li>
        <li class="pub-item">
          <div class="pub-title">SD Natural History Museum Events</div>
          <div class="pub-venue">San Diego Natural History Museum</div>
        </li>
      </ul>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Video</div>
      <p style="font-size: 14px; color: #666; font-weight: 300; margin-bottom: 16px;">
        PiRat: rat-robot interaction project in collaboration with Janet Wiles' CIS Lab at UQ.
      </p>
      <div class="video-wrap">
        <iframe
          src="https://www.youtube.com/embed/uzqJsvfEnr4"
          title="PiRat Robot Interaction"
          allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
          allowfullscreen>
        </iframe>
      </div>
    </div>

    <footer>
      <span><a href="mailto:leonardiseric@gmail.com">leonardiseric@gmail.com</a></span>
      <span><a href="https://github.com/ericleonardis" target="_blank" rel="noopener">GitHub</a></span>
    </footer>

  </div>

</body>
</html>
```

- [ ] **Step 2: Verify in browser**

Check featured card, embedded YouTube video, press list, and talks list all render correctly.

- [ ] **Step 3: Commit**

```bash
git add scicomm.html
git commit -m "feat: add sci comm page with talks, press, and videos"
```

---

### Task 6: Music Page (`music.html`)

**Files:**
- Create: `music.html`

- [ ] **Step 1: Write the complete music page**

Create `music.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Music — Eric Leonardis</title>
  <link rel="stylesheet" href="/css/main.css">
</head>
<body>

  <nav>
    <a href="/" class="logo">Eric Leonardis</a>
    <button class="nav-toggle" aria-label="Toggle navigation" onclick="document.querySelector('.nav-links').classList.toggle('open')">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links">
      <li><a href="/">Home</a></li>
      <li><a href="/research.html">Research</a></li>
      <li><a href="/CV/ResumeEricLeonardis.pdf">Resume</a></li>
      <li><a href="/CV/EricLeonardisCV.pdf">CV</a></li>
      <li><a href="/scicomm.html">Sci Comm</a></li>
      <li><a href="/film.html">Film</a></li>
      <li><a href="/music.html" class="active">Music</a></li>
    </ul>
  </nav>

  <div class="page-wrap">

    <div class="page-header">
      <h1>Music</h1>
      <p class="subtitle">DJ sets, events, and mixes.</p>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Events</div>
      <div class="flyer-grid">
        <!-- Add flyer items as images become available -->
        <!-- Example format:
        <div class="flyer-item">
          <img src="/images/flyers/event-name.jpg" alt="Event Name">
          <div class="flyer-title">Event Name</div>
          <div class="flyer-sub">Venue · Date</div>
        </div>
        -->
      </div>
      <p style="font-size: 13px; color: #999; font-weight: 300; padding: 40px 0;">
        Flyer archive coming soon.
      </p>
    </div>

    <div class="divider"></div>

    <div class="section">
      <div class="section-label">Links</div>
      <p style="font-size: 14px; color: #666; font-weight: 300;">
        Find me on
        <a href="https://ra.co/dj/ericleonardis/biography" target="_blank" rel="noopener" style="color: #1a1a1a; font-weight: 500;">Resident Advisor</a>
      </p>
    </div>

    <footer>
      <span><a href="mailto:leonardiseric@gmail.com">leonardiseric@gmail.com</a></span>
      <span><a href="https://github.com/ericleonardis" target="_blank" rel="noopener">GitHub</a></span>
    </footer>

  </div>

</body>
</html>
```

- [ ] **Step 2: Verify in browser**

Check page renders with placeholder text for flyers and RA link works.

- [ ] **Step 3: Commit**

```bash
git add music.html
git commit -m "feat: add music page with flyer grid placeholder and RA link"
```

---

### Task 7: Update `_config.yml` and clean up

**Files:**
- Modify: `_config.yml`

- [ ] **Step 1: Simplify Jekyll config**

The site no longer needs the jekyll-theme-minimal since we have our own CSS. Update `_config.yml`:

```yaml
name: Eric Leonardis, PhD
markdown: kramdown
```

Remove the `theme: jekyll-theme-minimal` line so Jekyll doesn't inject theme styles that conflict with our CSS.

- [ ] **Step 2: Remove old CV index page**

The `CV/index.html` was a Jekyll stub for the old theme. It's no longer needed since Resume and CV are direct PDF links.

```bash
rm CV/index.html
```

- [ ] **Step 3: Commit**

```bash
git add _config.yml
git rm CV/index.html
git commit -m "chore: simplify Jekyll config and remove old CV index stub"
```

---

### Task 8: Final visual review

- [ ] **Step 1: Open each page in a browser and verify**

Open each page and check:
- `index.html` — Hero, research cards with author lists, document cards, sci comm cards, film card, footer
- `research.html` — Featured papers with images and authors, publication list with links
- `film.html` — Comic-Con featured card, events list
- `scicomm.html` — Body Horror featured card, YouTube embed, press list, talks list, PiRat video
- `music.html` — Placeholder flyer grid, RA link

- [ ] **Step 2: Test responsive layout**

Resize browser to mobile width (< 768px) and verify:
- Nav collapses to hamburger menu
- Hamburger toggle opens/closes nav links
- Card grids become single column
- Featured cards stack vertically
- Footer stacks vertically

- [ ] **Step 3: Verify all links work**

Click every link on every page:
- PDF links open correct documents
- arXiv links open correct papers
- YouTube videos play
- External links (WIRED, RA) open in new tabs
- Internal navigation between pages works
