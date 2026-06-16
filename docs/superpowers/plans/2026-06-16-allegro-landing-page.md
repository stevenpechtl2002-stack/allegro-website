# Allegro Landing Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a stunning Rustico Italiano landing page for Allegro Pizzeria Pforzheim as a static GitHub project deployable on Vercel.

**Architecture:** Single-page static site (HTML + CSS + JS) with 6 sections: Hero, Mittagstisch, Über uns, Speisekarte, Galerie, Kontakt. No build tools, no frameworks — pure browser-native code that Vercel serves as-is.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, flexbox, animations), vanilla JS (IntersectionObserver, smooth scroll), Google Fonts (Playfair Display + Inter), Unsplash images via URL.

---

## File Map

| File | Responsibility |
|------|---------------|
| `index.html` | Page structure, all sections, semantic markup |
| `css/style.css` | All styles: CSS variables, layout, animations, responsive |
| `js/main.js` | Sticky nav, scroll animations, mobile menu, parallax |
| `vercel.json` | Static site config for Vercel |
| `.gitignore` | Exclude .DS_Store, .vercel |

---

### Task 1: Git-Projekt initialisieren und GitHub-Repo erstellen

**Files:**
- Create: `.gitignore`
- Create: `vercel.json`
- Create: `index.html` (Grundstruktur)
- Create: `css/style.css` (leer)
- Create: `js/main.js` (leer)

- [ ] **Step 1: Verzeichnis initialisieren**

```bash
cd /Users/andreaspechtl/allegro
git init
mkdir -p css js
```

- [ ] **Step 2: .gitignore erstellen**

```
.DS_Store
.vercel
node_modules/
*.log
```

Speichere als `.gitignore`.

- [ ] **Step 3: vercel.json erstellen**

```json
{
  "rewrites": [
    { "source": "/(.*)", "destination": "/index.html" }
  ]
}
```

- [ ] **Step 4: Leere CSS- und JS-Dateien anlegen**

`css/style.css` — leere Datei erstellen.
`js/main.js` — leere Datei erstellen.

- [ ] **Step 5: index.html Grundstruktur erstellen**

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Allegro Pizzeria & Restaurant — Pforzheim</title>
  <meta name="description" content="Authentische italienische Küche im Herzen von Pforzheim. Pizza, Pasta, Salate — täglich frisch. Mittagstisch Mo–Fr 11:30–13:30 Uhr." />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400;1,700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet" />
  <link rel="stylesheet" href="css/style.css" />
</head>
<body>
  <nav id="navbar"><!-- Task 2 --></nav>
  <main>
    <section id="hero"><!-- Task 3 --></section>
    <section id="mittagstisch"><!-- Task 4 --></section>
    <section id="ueber-uns"><!-- Task 5 --></section>
    <section id="speisekarte"><!-- Task 6 --></section>
    <section id="galerie"><!-- Task 7 --></section>
    <section id="kontakt"><!-- Task 8 --></section>
  </main>
  <footer id="footer"><!-- Task 8 --></footer>
  <script src="js/main.js"></script>
</body>
</html>
```

- [ ] **Step 6: GitHub-Repo erstellen und pushen**

```bash
gh repo create allegro-website --public --source=. --remote=origin --push
```

Falls `gh` nicht verfügbar:
```bash
# Manuell auf github.com ein neues Repo "allegro-website" erstellen, dann:
git remote add origin https://github.com/DEIN-USERNAME/allegro-website.git
git branch -M main
git add -A
git commit -m "feat: initial project structure"
git push -u origin main
```

- [ ] **Step 7: Erstes Commit**

```bash
git add -A
git commit -m "feat: init project structure for Allegro landing page"
git push
```

---

### Task 2: CSS Grundvariablen und Navigation

**Files:**
- Modify: `css/style.css`
- Modify: `index.html` (nav Bereich)

- [ ] **Step 1: CSS-Variablen und Reset in style.css schreiben**

```css
/* ===== CSS VARIABLES ===== */
:root {
  --bg-darkest: #0A0603;
  --bg-dark: #0F0805;
  --bg-medium: #1A0F07;
  --bg-card: #2C1A0E;
  --bg-card-hover: #3D2010;
  --brown-mid: #5C3317;
  --brown-light: #8B4513;
  --gold: #D4A853;
  --gold-dark: #B8922E;
  --gold-light: #E8C47A;
  --cream: #F5DEB3;
  --cream-mid: #C8A97A;
  --cream-dark: #8B6642;
  --text-muted: #6B4C2A;
  --font-serif: 'Playfair Display', Georgia, serif;
  --font-sans: 'Inter', system-ui, sans-serif;
  --transition: 0.3s ease;
  --border-gold: 1px solid rgba(212, 168, 83, 0.3);
  --shadow-gold: 0 4px 30px rgba(212, 168, 83, 0.15);
}

/* ===== RESET ===== */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

html { scroll-behavior: smooth; font-size: 16px; }

body {
  background: var(--bg-dark);
  color: var(--cream);
  font-family: var(--font-sans);
  line-height: 1.6;
  overflow-x: hidden;
}

img { display: block; width: 100%; height: 100%; object-fit: cover; }

a { color: inherit; text-decoration: none; }

/* ===== UTILITY ===== */
.container { max-width: 1100px; margin: 0 auto; padding: 0 24px; }
.section-label { font-family: var(--font-sans); font-size: 11px; font-weight: 600; letter-spacing: 4px; text-transform: uppercase; color: var(--gold); margin-bottom: 12px; }
.section-title { font-family: var(--font-serif); font-size: clamp(32px, 5vw, 52px); font-weight: 700; color: var(--cream); line-height: 1.15; margin-bottom: 20px; }
.gold-divider { width: 60px; height: 2px; background: var(--gold); margin: 20px 0; }
.btn-primary { display: inline-block; background: var(--gold); color: var(--bg-darkest); font-family: var(--font-sans); font-size: 12px; font-weight: 700; letter-spacing: 2px; text-transform: uppercase; padding: 14px 28px; border-radius: 2px; transition: background var(--transition), transform var(--transition); cursor: pointer; border: none; }
.btn-primary:hover { background: var(--gold-light); transform: translateY(-2px); }
.btn-outline { display: inline-block; border: 1.5px solid var(--gold); color: var(--gold); font-family: var(--font-sans); font-size: 12px; font-weight: 600; letter-spacing: 2px; text-transform: uppercase; padding: 13px 28px; border-radius: 2px; transition: background var(--transition), color var(--transition), transform var(--transition); }
.btn-outline:hover { background: var(--gold); color: var(--bg-darkest); transform: translateY(-2px); }

/* ===== FADE-IN ANIMATION ===== */
.fade-up { opacity: 0; transform: translateY(40px); transition: opacity 0.7s ease, transform 0.7s ease; }
.fade-up.visible { opacity: 1; transform: translateY(0); }
.fade-up.delay-1 { transition-delay: 0.15s; }
.fade-up.delay-2 { transition-delay: 0.3s; }
.fade-up.delay-3 { transition-delay: 0.45s; }
```

- [ ] **Step 2: Navigation HTML schreiben**

Ersetze `<nav id="navbar"><!-- Task 2 --></nav>` mit:

```html
<nav id="navbar">
  <div class="nav-inner container">
    <a href="#hero" class="nav-logo">
      <span class="logo-text">Allegro</span>
      <span class="logo-sub">Pforzheim</span>
    </a>
    <button class="nav-toggle" id="navToggle" aria-label="Menü öffnen">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links" id="navLinks">
      <li><a href="#mittagstisch" class="nav-link">Mittagstisch</a></li>
      <li><a href="#speisekarte" class="nav-link">Karte</a></li>
      <li><a href="#ueber-uns" class="nav-link">Über uns</a></li>
      <li><a href="#galerie" class="nav-link">Galerie</a></li>
      <li><a href="#kontakt" class="nav-link nav-cta">Kontakt</a></li>
    </ul>
  </div>
</nav>
```

- [ ] **Step 3: Navigation CSS schreiben** (ans Ende von style.css anfügen)

```css
/* ===== NAVIGATION ===== */
#navbar {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 1000;
  padding: 20px 0;
  transition: background var(--transition), padding var(--transition), backdrop-filter var(--transition);
}
#navbar.scrolled {
  background: rgba(15, 8, 5, 0.95);
  backdrop-filter: blur(12px);
  padding: 12px 0;
  border-bottom: var(--border-gold);
}
.nav-inner { display: flex; align-items: center; justify-content: space-between; }
.nav-logo { display: flex; flex-direction: column; line-height: 1; }
.logo-text { font-family: var(--font-serif); font-size: 24px; font-style: italic; color: var(--cream); letter-spacing: 1px; }
.logo-sub { font-size: 9px; letter-spacing: 4px; text-transform: uppercase; color: var(--gold); margin-top: 2px; }
.nav-links { display: flex; list-style: none; gap: 36px; align-items: center; }
.nav-link { font-size: 12px; font-weight: 500; letter-spacing: 2px; text-transform: uppercase; color: var(--cream-mid); transition: color var(--transition); position: relative; }
.nav-link::after { content: ''; position: absolute; bottom: -4px; left: 0; width: 0; height: 1px; background: var(--gold); transition: width var(--transition); }
.nav-link:hover { color: var(--gold); }
.nav-link:hover::after { width: 100%; }
.nav-cta { color: var(--gold) !important; border: 1px solid rgba(212,168,83,0.4); padding: 8px 16px; border-radius: 2px; }
.nav-cta:hover { background: var(--gold); color: var(--bg-darkest) !important; }
.nav-cta::after { display: none; }
.nav-toggle { display: none; flex-direction: column; gap: 5px; background: none; border: none; cursor: pointer; padding: 4px; }
.nav-toggle span { display: block; width: 24px; height: 1.5px; background: var(--cream); transition: var(--transition); }
```

- [ ] **Step 4: Navigation JS in main.js schreiben**

```javascript
// ===== STICKY NAV =====
const navbar = document.getElementById('navbar');
window.addEventListener('scroll', () => {
  navbar.classList.toggle('scrolled', window.scrollY > 60);
});

// ===== MOBILE MENU =====
const navToggle = document.getElementById('navToggle');
const navLinks = document.getElementById('navLinks');
navToggle.addEventListener('click', () => {
  navLinks.classList.toggle('open');
  navToggle.classList.toggle('active');
});
document.querySelectorAll('.nav-link').forEach(link => {
  link.addEventListener('click', () => {
    navLinks.classList.remove('open');
    navToggle.classList.remove('active');
  });
});

// ===== FADE-IN ON SCROLL =====
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
      observer.unobserve(entry.target);
    }
  });
}, { threshold: 0.15 });
document.querySelectorAll('.fade-up').forEach(el => observer.observe(el));
```

- [ ] **Step 5: Visuell prüfen** — Öffne `index.html` im Browser. Nav sollte beim Scrollen dunkler werden. Mobile-Breakpoint noch nicht, das kommt in Task 9.

- [ ] **Step 6: Commit**

```bash
git add -A
git commit -m "feat: add sticky navigation with scroll effect"
git push
```

---

### Task 3: Hero Section

**Files:**
- Modify: `index.html` (hero section)
- Modify: `css/style.css` (hero styles)
- Modify: `js/main.js` (parallax)

- [ ] **Step 1: Hero HTML**

Ersetze `<section id="hero"><!-- Task 3 --></section>` mit:

```html
<section id="hero">
  <div class="hero-bg" id="heroBg"></div>
  <div class="hero-overlay"></div>
  <div class="hero-content container">
    <div class="hero-inner">
      <p class="hero-label fade-up">Ristorante · Pizzeria · Pforzheim</p>
      <h1 class="hero-title fade-up delay-1">
        <span class="hero-title-main">Cucina</span>
        <span class="hero-title-accent">Autentica</span>
      </h1>
      <p class="hero-subtitle fade-up delay-2">
        Handgemachte Pizza &amp; Pasta —<br />täglich frisch, mit Leidenschaft.
      </p>
      <div class="hero-ctas fade-up delay-3">
        <a href="tel:072311016 29" class="btn-primary">Tisch reservieren</a>
        <a href="#mittagstisch" class="btn-outline">Zum Mittagstisch</a>
      </div>
      <div class="hero-scroll-hint fade-up delay-3">
        <span>Scroll</span>
        <div class="scroll-line"></div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Hero CSS**

```css
/* ===== HERO ===== */
#hero {
  position: relative;
  height: 100vh;
  min-height: 600px;
  display: flex;
  align-items: center;
  overflow: hidden;
}
.hero-bg {
  position: absolute;
  inset: -10%;
  background-image: url('https://images.unsplash.com/photo-1513104890138-7c749659a591?w=1920&q=80&auto=format&fit=crop');
  background-size: cover;
  background-position: center;
  will-change: transform;
}
.hero-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    135deg,
    rgba(10, 6, 3, 0.85) 0%,
    rgba(44, 26, 14, 0.75) 50%,
    rgba(10, 6, 3, 0.70) 100%
  );
}
.hero-content { position: relative; z-index: 1; padding-top: 80px; }
.hero-inner { max-width: 620px; }
.hero-label { font-size: 11px; font-weight: 600; letter-spacing: 5px; text-transform: uppercase; color: var(--gold); margin-bottom: 24px; }
.hero-title { font-family: var(--font-serif); line-height: 1.0; margin-bottom: 24px; }
.hero-title-main { display: block; font-size: clamp(56px, 10vw, 96px); font-weight: 400; font-style: italic; color: var(--cream); }
.hero-title-accent { display: block; font-size: clamp(56px, 10vw, 96px); font-weight: 900; color: var(--gold); letter-spacing: -2px; }
.hero-subtitle { font-size: clamp(15px, 2vw, 18px); font-weight: 300; color: var(--cream-mid); line-height: 1.7; margin-bottom: 40px; }
.hero-ctas { display: flex; gap: 16px; flex-wrap: wrap; margin-bottom: 60px; }
.hero-scroll-hint { display: flex; align-items: center; gap: 16px; }
.hero-scroll-hint span { font-size: 10px; letter-spacing: 3px; text-transform: uppercase; color: var(--text-muted); }
.scroll-line { width: 60px; height: 1px; background: var(--gold); position: relative; overflow: hidden; }
.scroll-line::after { content: ''; position: absolute; top: 0; left: -100%; width: 100%; height: 100%; background: var(--cream); animation: scrollLine 2s infinite; }
@keyframes scrollLine { to { left: 100%; } }
```

- [ ] **Step 3: Parallax JS**

Füge ans Ende von `js/main.js` hinzu:

```javascript
// ===== PARALLAX HERO =====
const heroBg = document.getElementById('heroBg');
if (heroBg) {
  window.addEventListener('scroll', () => {
    const scrolled = window.scrollY;
    heroBg.style.transform = `translateY(${scrolled * 0.4}px)`;
  }, { passive: true });
}
```

- [ ] **Step 4: Visuell prüfen** — Öffne im Browser. Hero sollte Vollbild-Pizza-Foto mit dunklem Overlay, goldenem Titel und zwei Buttons zeigen. Beim Scrollen Parallax-Effekt.

- [ ] **Step 5: Commit**

```bash
git add -A
git commit -m "feat: add hero section with parallax background"
git push
```

---

### Task 4: Mittagstisch Section

**Files:**
- Modify: `index.html`
- Modify: `css/style.css`

- [ ] **Step 1: Mittagstisch HTML**

Ersetze `<section id="mittagstisch"><!-- Task 4 --></section>` mit:

```html
<section id="mittagstisch">
  <div class="container">
    <div class="mt-header fade-up">
      <p class="section-label">Täglich frisch</p>
      <h2 class="section-title">Mittagstisch</h2>
      <div class="gold-divider"></div>
      <p class="mt-info">
        <strong>Montag bis Freitag</strong> · 11:30 – 13:30 Uhr · Ausgenommen an Feiertagen
        <span class="mt-surcharge">+1,00 € bei Bestellung auf zwei Tellern</span>
      </p>
    </div>

    <div class="mt-grid">
      <div class="mt-card fade-up delay-1">
        <div class="mt-card-type">Salat</div>
        <div class="mt-card-body">
          <h3 class="mt-card-name">Kleiner gemischter Salat</h3>
        </div>
        <div class="mt-card-price">5,50 €</div>
      </div>
      <div class="mt-card fade-up delay-1">
        <div class="mt-card-type">Salat</div>
        <div class="mt-card-body">
          <h3 class="mt-card-name">Insalata Romana</h3>
          <p class="mt-card-desc">Feta, Paprika, Oliven</p>
        </div>
        <div class="mt-card-price">10,50 €</div>
      </div>
      <div class="mt-card fade-up delay-2">
        <div class="mt-card-type">Pasta</div>
        <div class="mt-card-body">
          <h3 class="mt-card-name">Penne</h3>
          <p class="mt-card-desc">Schinken, Paprika, Sahnesauce</p>
        </div>
        <div class="mt-card-price">9,90 €</div>
      </div>
      <div class="mt-card fade-up delay-2">
        <div class="mt-card-type">Pasta</div>
        <div class="mt-card-body">
          <h3 class="mt-card-name">Spaghetti</h3>
          <p class="mt-card-desc">Mozzarella, Basilikum, Tomatensauce</p>
        </div>
        <div class="mt-card-price">9,90 €</div>
      </div>
      <div class="mt-card mt-card-featured fade-up delay-3">
        <div class="mt-card-type">Pizza</div>
        <div class="mt-card-body">
          <h3 class="mt-card-name">Pizza Prosciutto</h3>
          <p class="mt-card-desc">Schinken, Käse</p>
        </div>
        <div class="mt-card-price">9,90 €</div>
      </div>
      <div class="mt-card fade-up delay-3">
        <div class="mt-card-type">Pizza</div>
        <div class="mt-card-body">
          <h3 class="mt-card-name">Pizza Melanzane</h3>
          <p class="mt-card-desc">Aubergine, Zucchini, Käse</p>
        </div>
        <div class="mt-card-price">9,90 €</div>
      </div>
      <div class="mt-card mt-card-full fade-up">
        <div class="mt-card-type">Fitness</div>
        <div class="mt-card-body">
          <h3 class="mt-card-name">Fitness-Teller</h3>
          <p class="mt-card-desc">Gegrillte Hähnchenbrust, gemischter Salat</p>
        </div>
        <div class="mt-card-price">13,50 €</div>
      </div>
    </div>

    <div class="mt-abo fade-up">
      <div class="mt-abo-inner">
        <div>
          <p class="mt-abo-title">Wochenkarte per E-Mail</p>
          <p class="mt-abo-desc">Verpasse keine Spezialitäten — erhalte die aktuelle Mittagskarte direkt in dein Postfach.</p>
        </div>
        <a href="mailto:info@allegro-pf.de?subject=Mittagskarte%20Abo" class="btn-primary">Jetzt anmelden</a>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Mittagstisch CSS**

```css
/* ===== MITTAGSTISCH ===== */
#mittagstisch {
  padding: 120px 0 100px;
  background: var(--bg-darkest);
  position: relative;
}
#mittagstisch::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--gold), transparent);
}
.mt-header { max-width: 600px; margin-bottom: 60px; }
.mt-info { color: var(--cream-mid); font-size: 14px; margin-top: 16px; line-height: 1.8; }
.mt-surcharge { display: block; color: var(--text-muted); font-size: 12px; margin-top: 4px; font-style: italic; }
.mt-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 2px; margin-bottom: 40px; }
.mt-card { background: var(--bg-card); padding: 24px 20px; display: flex; flex-direction: column; gap: 8px; transition: background var(--transition); border-left: 2px solid transparent; }
.mt-card:hover { background: var(--bg-card-hover); border-left-color: var(--gold); }
.mt-card-featured { border-left-color: rgba(212,168,83,0.4); }
.mt-card-full { grid-column: 1 / -1; flex-direction: row; justify-content: space-between; align-items: center; background: rgba(212,168,83,0.08); }
.mt-card-type { font-size: 10px; font-weight: 700; letter-spacing: 3px; text-transform: uppercase; color: var(--gold); }
.mt-card-name { font-family: var(--font-serif); font-size: 17px; color: var(--cream); font-weight: 600; }
.mt-card-desc { font-size: 13px; color: var(--cream-dark); margin-top: 2px; }
.mt-card-price { font-family: var(--font-serif); font-size: 22px; color: var(--gold); font-weight: 700; margin-top: auto; }
.mt-card-full .mt-card-price { margin-top: 0; }
.mt-abo { margin-top: 60px; border: var(--border-gold); border-radius: 4px; padding: 32px; background: rgba(212,168,83,0.04); }
.mt-abo-inner { display: flex; justify-content: space-between; align-items: center; gap: 24px; flex-wrap: wrap; }
.mt-abo-title { font-family: var(--font-serif); font-size: 20px; color: var(--cream); margin-bottom: 6px; }
.mt-abo-desc { color: var(--cream-dark); font-size: 14px; }
```

- [ ] **Step 3: Visuell prüfen** — Alle 7 Menüeinträge als elegante Karten mit goldenen Typen-Labels und Preisen.

- [ ] **Step 4: Commit**

```bash
git add -A
git commit -m "feat: add Mittagstisch section with menu cards"
git push
```

---

### Task 5: Über uns Section

**Files:**
- Modify: `index.html`
- Modify: `css/style.css`

- [ ] **Step 1: Über uns HTML**

Ersetze `<section id="ueber-uns"><!-- Task 5 --></section>` mit:

```html
<section id="ueber-uns">
  <div class="container">
    <div class="about-grid">
      <div class="about-content fade-up">
        <p class="section-label">Unsere Geschichte</p>
        <h2 class="section-title">Mit Leidenschaft<br />in Pforzheim</h2>
        <div class="gold-divider"></div>
        <p class="about-text">
          Willkommen im Allegro — einem Ort, wo italienische Küchentradition und herzliche Gastfreundschaft aufeinandertreffen. Inhaber <strong>Artur Grießhaber</strong> hat es sich zur Aufgabe gemacht, authentische Geschmackserlebnisse direkt nach Pforzheim zu bringen.
        </p>
        <p class="about-text">
          Jedes Gericht wird mit frischen Zutaten und echter Handwerkskunst zubereitet — von der knusprigen Pizza aus dem Steinofen bis zur cremigen Pasta al dente. Kein Halbfertigprodukt, kein Kompromiss.
        </p>
        <blockquote class="about-quote">
          „Bei uns kommt die Leidenschaft direkt auf den Teller."
        </blockquote>
        <a href="#kontakt" class="btn-outline" style="margin-top: 32px;">Besucht uns</a>
      </div>
      <div class="about-image-wrap fade-up delay-2">
        <div class="about-image">
          <img src="https://images.unsplash.com/photo-1414235077428-338989a2e8c0?w=800&q=80&auto=format&fit=crop" alt="Restaurant Atmosphäre" loading="lazy" />
        </div>
        <div class="about-badge">
          <span class="about-badge-icon">🍕</span>
          <span class="about-badge-text">Frisch<br />jeden Tag</span>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Über uns CSS**

```css
/* ===== ÜBER UNS ===== */
#ueber-uns {
  padding: 120px 0;
  background: var(--bg-dark);
  position: relative;
  overflow: hidden;
}
#ueber-uns::before {
  content: 'Allegro';
  position: absolute;
  right: -60px;
  top: 50%;
  transform: translateY(-50%);
  font-family: var(--font-serif);
  font-size: 200px;
  font-style: italic;
  color: rgba(212,168,83,0.04);
  white-space: nowrap;
  pointer-events: none;
}
.about-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: center; }
.about-text { color: var(--cream-mid); font-size: 15px; line-height: 1.85; margin-bottom: 20px; }
.about-text strong { color: var(--cream); }
.about-quote { border-left: 3px solid var(--gold); padding: 16px 24px; margin: 32px 0 0; font-family: var(--font-serif); font-size: 18px; font-style: italic; color: var(--gold); background: rgba(212,168,83,0.06); border-radius: 0 4px 4px 0; }
.about-image-wrap { position: relative; }
.about-image { height: 520px; border-radius: 4px; overflow: hidden; box-shadow: 0 20px 60px rgba(0,0,0,0.5); }
.about-badge { position: absolute; bottom: -24px; left: -24px; background: var(--gold); color: var(--bg-darkest); border-radius: 4px; padding: 20px; display: flex; align-items: center; gap: 12px; box-shadow: 0 8px 30px rgba(212,168,83,0.3); }
.about-badge-icon { font-size: 32px; }
.about-badge-text { font-size: 13px; font-weight: 700; line-height: 1.3; text-transform: uppercase; letter-spacing: 1px; }
```

- [ ] **Step 3: Commit**

```bash
git add -A
git commit -m "feat: add Über uns section"
git push
```

---

### Task 6: Speisekarte Highlights

**Files:**
- Modify: `index.html`
- Modify: `css/style.css`

- [ ] **Step 1: Speisekarte HTML**

Ersetze `<section id="speisekarte"><!-- Task 6 --></section>` mit:

```html
<section id="speisekarte">
  <div class="container">
    <div class="menu-header fade-up">
      <p class="section-label">Was wir lieben</p>
      <h2 class="section-title">Unsere Karte</h2>
      <div class="gold-divider"></div>
    </div>
    <div class="menu-grid">
      <div class="menu-card fade-up">
        <div class="menu-card-img">
          <img src="https://images.unsplash.com/photo-1574071318508-1cdbab80d002?w=600&q=80&auto=format&fit=crop" alt="Pizza" loading="lazy" />
          <div class="menu-card-overlay"></div>
          <span class="menu-card-emoji">🍕</span>
        </div>
        <div class="menu-card-body">
          <h3 class="menu-card-title">Pizza</h3>
          <ul class="menu-card-items">
            <li>Margherita</li>
            <li>Prosciutto</li>
            <li>Melanzane</li>
            <li>& mehr</li>
          </ul>
          <div class="menu-card-price">ab 9,90 €</div>
        </div>
      </div>
      <div class="menu-card fade-up delay-1">
        <div class="menu-card-img">
          <img src="https://images.unsplash.com/photo-1621996346565-e3dbc646d9a9?w=600&q=80&auto=format&fit=crop" alt="Pasta" loading="lazy" />
          <div class="menu-card-overlay"></div>
          <span class="menu-card-emoji">🍝</span>
        </div>
        <div class="menu-card-body">
          <h3 class="menu-card-title">Pasta</h3>
          <ul class="menu-card-items">
            <li>Penne al Prosciutto</li>
            <li>Spaghetti Pomodoro</li>
            <li>& mehr</li>
          </ul>
          <div class="menu-card-price">ab 9,90 €</div>
        </div>
      </div>
      <div class="menu-card fade-up delay-2">
        <div class="menu-card-img">
          <img src="https://images.unsplash.com/photo-1512621776951-a57141f2eefd?w=600&q=80&auto=format&fit=crop" alt="Salate" loading="lazy" />
          <div class="menu-card-overlay"></div>
          <span class="menu-card-emoji">🥗</span>
        </div>
        <div class="menu-card-body">
          <h3 class="menu-card-title">Salate</h3>
          <ul class="menu-card-items">
            <li>Insalata Romana</li>
            <li>Fitness-Teller</li>
            <li>& mehr</li>
          </ul>
          <div class="menu-card-price">ab 5,50 €</div>
        </div>
      </div>
    </div>
    <div class="menu-cta fade-up">
      <p class="menu-cta-text">Vollständige Karte? Ruf uns an oder schreib uns.</p>
      <div style="display:flex;gap:16px;flex-wrap:wrap;">
        <a href="tel:0723110 1629" class="btn-primary">📞 07231 – 10 16 29</a>
        <a href="mailto:info@allegro-pf.de" class="btn-outline">E-Mail schreiben</a>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Speisekarte CSS**

```css
/* ===== SPEISEKARTE ===== */
#speisekarte {
  padding: 120px 0;
  background: var(--bg-medium);
}
.menu-header { max-width: 500px; margin-bottom: 60px; }
.menu-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; margin-bottom: 60px; }
.menu-card { background: var(--bg-card); border-radius: 4px; overflow: hidden; transition: transform var(--transition), box-shadow var(--transition); }
.menu-card:hover { transform: translateY(-8px); box-shadow: 0 20px 50px rgba(0,0,0,0.4), 0 0 0 1px rgba(212,168,83,0.2); }
.menu-card-img { position: relative; height: 220px; overflow: hidden; }
.menu-card-img img { transition: transform 0.6s ease; }
.menu-card:hover .menu-card-img img { transform: scale(1.08); }
.menu-card-overlay { position: absolute; inset: 0; background: linear-gradient(to top, rgba(10,6,3,0.8) 0%, transparent 60%); }
.menu-card-emoji { position: absolute; bottom: 16px; left: 16px; font-size: 36px; }
.menu-card-body { padding: 24px; }
.menu-card-title { font-family: var(--font-serif); font-size: 24px; color: var(--cream); margin-bottom: 12px; }
.menu-card-items { list-style: none; color: var(--cream-dark); font-size: 13px; line-height: 2; }
.menu-card-items li::before { content: '— '; color: var(--gold); }
.menu-card-price { margin-top: 16px; font-family: var(--font-serif); font-size: 20px; color: var(--gold); font-weight: 700; }
.menu-cta { text-align: center; border-top: var(--border-gold); padding-top: 48px; }
.menu-cta-text { color: var(--cream-mid); margin-bottom: 24px; font-size: 15px; }
```

- [ ] **Step 3: Commit**

```bash
git add -A
git commit -m "feat: add Speisekarte section with food images"
git push
```

---

### Task 7: Galerie Section

**Files:**
- Modify: `index.html`
- Modify: `css/style.css`
- Modify: `js/main.js` (Lightbox)

- [ ] **Step 1: Galerie HTML**

Ersetze `<section id="galerie"><!-- Task 7 --></section>` mit:

```html
<section id="galerie">
  <div class="container">
    <div class="gallery-header fade-up">
      <p class="section-label">Einblicke</p>
      <h2 class="section-title">Atmosphäre</h2>
      <div class="gold-divider"></div>
    </div>
  </div>
  <div class="gallery-grid">
    <div class="gallery-item fade-up" data-src="https://images.unsplash.com/photo-1555396273-367ea4eb4db5?w=1200&q=80">
      <img src="https://images.unsplash.com/photo-1555396273-367ea4eb4db5?w=800&q=80&auto=format&fit=crop" alt="Restaurant" loading="lazy" />
      <div class="gallery-overlay"><span class="gallery-zoom">＋</span></div>
    </div>
    <div class="gallery-item fade-up delay-1" data-src="https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?w=1200&q=80">
      <img src="https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?w=800&q=80&auto=format&fit=crop" alt="Pizza" loading="lazy" />
      <div class="gallery-overlay"><span class="gallery-zoom">＋</span></div>
    </div>
    <div class="gallery-item gallery-item-tall fade-up delay-2" data-src="https://images.unsplash.com/photo-1481931098730-318b6f776db0?w=1200&q=80">
      <img src="https://images.unsplash.com/photo-1481931098730-318b6f776db0?w=800&q=80&auto=format&fit=crop" alt="Pasta" loading="lazy" />
      <div class="gallery-overlay"><span class="gallery-zoom">＋</span></div>
    </div>
    <div class="gallery-item gallery-item-wide fade-up" data-src="https://images.unsplash.com/photo-1414235077428-338989a2e8c0?w=1200&q=80">
      <img src="https://images.unsplash.com/photo-1414235077428-338989a2e8c0?w=800&q=80&auto=format&fit=crop" alt="Restaurant Innen" loading="lazy" />
      <div class="gallery-overlay"><span class="gallery-zoom">＋</span></div>
    </div>
    <div class="gallery-item fade-up delay-1" data-src="https://images.unsplash.com/photo-1546069901-ba9599a7e63c?w=1200&q=80">
      <img src="https://images.unsplash.com/photo-1546069901-ba9599a7e63c?w=800&q=80&auto=format&fit=crop" alt="Salat" loading="lazy" />
      <div class="gallery-overlay"><span class="gallery-zoom">＋</span></div>
    </div>
  </div>

  <!-- Lightbox -->
  <div class="lightbox" id="lightbox">
    <button class="lightbox-close" id="lightboxClose">✕</button>
    <img class="lightbox-img" id="lightboxImg" src="" alt="" />
  </div>
</section>
```

- [ ] **Step 2: Galerie CSS**

```css
/* ===== GALERIE ===== */
#galerie { padding: 120px 0; background: var(--bg-darkest); }
.gallery-header { max-width: 500px; margin-bottom: 60px; }
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 280px 280px;
  gap: 4px;
}
.gallery-item { position: relative; overflow: hidden; cursor: pointer; }
.gallery-item-tall { grid-row: span 2; }
.gallery-item-wide { grid-column: span 2; }
.gallery-item img { width: 100%; height: 100%; object-fit: cover; transition: transform 0.6s ease; }
.gallery-item:hover img { transform: scale(1.08); }
.gallery-overlay { position: absolute; inset: 0; background: rgba(44,26,14,0); transition: background var(--transition); display: flex; align-items: center; justify-content: center; }
.gallery-item:hover .gallery-overlay { background: rgba(44,26,14,0.6); }
.gallery-zoom { font-size: 48px; color: var(--gold); opacity: 0; transform: scale(0.5); transition: opacity var(--transition), transform var(--transition); }
.gallery-item:hover .gallery-zoom { opacity: 1; transform: scale(1); }

/* Lightbox */
.lightbox { position: fixed; inset: 0; background: rgba(0,0,0,0.95); z-index: 9999; display: none; align-items: center; justify-content: center; }
.lightbox.open { display: flex; }
.lightbox-img { max-width: 90vw; max-height: 90vh; object-fit: contain; border-radius: 2px; }
.lightbox-close { position: absolute; top: 24px; right: 32px; background: none; border: none; color: var(--cream); font-size: 32px; cursor: pointer; opacity: 0.7; transition: opacity var(--transition); }
.lightbox-close:hover { opacity: 1; }
```

- [ ] **Step 3: Lightbox JS**

Füge ans Ende von `js/main.js` hinzu:

```javascript
// ===== LIGHTBOX =====
const lightbox = document.getElementById('lightbox');
const lightboxImg = document.getElementById('lightboxImg');
const lightboxClose = document.getElementById('lightboxClose');

document.querySelectorAll('.gallery-item').forEach(item => {
  item.addEventListener('click', () => {
    lightboxImg.src = item.dataset.src;
    lightbox.classList.add('open');
    document.body.style.overflow = 'hidden';
  });
});
lightboxClose.addEventListener('click', closeLightbox);
lightbox.addEventListener('click', e => { if (e.target === lightbox) closeLightbox(); });
document.addEventListener('keydown', e => { if (e.key === 'Escape') closeLightbox(); });
function closeLightbox() {
  lightbox.classList.remove('open');
  document.body.style.overflow = '';
}
```

- [ ] **Step 4: Commit**

```bash
git add -A
git commit -m "feat: add gallery section with lightbox"
git push
```

---

### Task 8: Kontakt Section und Footer

**Files:**
- Modify: `index.html`
- Modify: `css/style.css`

- [ ] **Step 1: Kontakt HTML**

Ersetze `<section id="kontakt"><!-- Task 8 --></section>` mit:

```html
<section id="kontakt">
  <div class="container">
    <div class="kontakt-header fade-up">
      <p class="section-label">Wir freuen uns auf euch</p>
      <h2 class="section-title">Besuch uns</h2>
      <div class="gold-divider"></div>
    </div>
    <div class="kontakt-grid">
      <div class="kontakt-info fade-up">
        <div class="kontakt-block">
          <p class="kontakt-label">Adresse</p>
          <p class="kontakt-value">Stuttgarter Straße 55<br />75179 Pforzheim</p>
        </div>
        <div class="kontakt-block">
          <p class="kontakt-label">Telefon</p>
          <a href="tel:0723110 1629" class="kontakt-value kontakt-link">07231 – 10 16 29</a>
        </div>
        <div class="kontakt-block">
          <p class="kontakt-label">E-Mail</p>
          <a href="mailto:info@allegro-pf.de" class="kontakt-value kontakt-link">info@allegro-pf.de</a>
        </div>
        <div class="kontakt-block">
          <p class="kontakt-label">Mittagstisch</p>
          <p class="kontakt-value">Mo – Fr · 11:30 – 13:30 Uhr<br /><span style="color:var(--text-muted);font-size:13px;">Ausgenommen an Feiertagen</span></p>
        </div>
        <a href="tel:0723110 1629" class="btn-primary" style="margin-top:16px;">Jetzt anrufen &amp; reservieren</a>
      </div>
      <div class="kontakt-map fade-up delay-2">
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2611.3!2d8.7057!3d48.8904!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x4797462c5b5e2e4b%3A0x1234!2sStuttgarter+Stra%C3%9Fe+55%2C+75179+Pforzheim!5e0!3m2!1sde!2sde!4v1234567890"
          allowfullscreen=""
          loading="lazy"
          referrerpolicy="no-referrer-when-downgrade"
          title="Allegro Restaurant Pforzheim">
        </iframe>
      </div>
    </div>
  </div>
</section>
```

Ersetze `<footer id="footer"><!-- Task 8 --></footer>` mit:

```html
<footer id="footer">
  <div class="container">
    <div class="footer-inner">
      <div class="footer-logo">
        <span class="logo-text">Allegro</span>
        <span class="logo-sub">Pforzheim</span>
      </div>
      <p class="footer-tagline">Cucina Autentica · Pforzheim seit Jahren</p>
      <nav class="footer-links">
        <a href="https://allegro-pf.de/impressum" target="_blank" rel="noopener">Impressum</a>
        <a href="https://allegro-pf.de/datenschutz" target="_blank" rel="noopener">Datenschutz</a>
        <a href="https://allegro-pf.de/cookie-richtlinie" target="_blank" rel="noopener">Cookie-Richtlinie</a>
      </nav>
      <p class="footer-copy">&copy; 2026 Allegro Pizzeria &amp; Restaurant · Artur Grießhaber</p>
    </div>
  </div>
</footer>
```

- [ ] **Step 2: Kontakt + Footer CSS**

```css
/* ===== KONTAKT ===== */
#kontakt { padding: 120px 0; background: var(--bg-dark); }
.kontakt-header { max-width: 500px; margin-bottom: 60px; }
.kontakt-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 60px; align-items: start; }
.kontakt-block { margin-bottom: 32px; }
.kontakt-label { font-size: 10px; font-weight: 700; letter-spacing: 3px; text-transform: uppercase; color: var(--gold); margin-bottom: 8px; }
.kontakt-value { font-size: 16px; color: var(--cream); line-height: 1.6; }
.kontakt-link { color: var(--cream-mid); transition: color var(--transition); }
.kontakt-link:hover { color: var(--gold); }
.kontakt-map { border-radius: 4px; overflow: hidden; height: 400px; border: var(--border-gold); }
.kontakt-map iframe { width: 100%; height: 100%; border: none; filter: grayscale(60%) sepia(20%); }

/* ===== FOOTER ===== */
#footer {
  background: var(--bg-darkest);
  border-top: var(--border-gold);
  padding: 48px 0;
}
.footer-inner { display: flex; flex-direction: column; align-items: center; gap: 16px; text-align: center; }
.footer-logo { display: flex; flex-direction: column; align-items: center; line-height: 1; margin-bottom: 4px; }
.footer-tagline { color: var(--text-muted); font-size: 13px; letter-spacing: 1px; }
.footer-links { display: flex; gap: 32px; }
.footer-links a { color: var(--cream-dark); font-size: 12px; letter-spacing: 1px; transition: color var(--transition); }
.footer-links a:hover { color: var(--gold); }
.footer-copy { color: var(--text-muted); font-size: 12px; }
```

- [ ] **Step 3: Commit**

```bash
git add -A
git commit -m "feat: add Kontakt section and footer"
git push
```

---

### Task 9: Mobile Responsiveness

**Files:**
- Modify: `css/style.css` (media queries)
- Modify: `css/style.css` (mobile nav)

- [ ] **Step 1: Mobile CSS ans Ende von style.css anfügen**

```css
/* ===== MOBILE NAV ===== */
.nav-links.open { display: flex; }
.nav-toggle.active span:nth-child(1) { transform: translateY(6.5px) rotate(45deg); }
.nav-toggle.active span:nth-child(2) { opacity: 0; }
.nav-toggle.active span:nth-child(3) { transform: translateY(-6.5px) rotate(-45deg); }

/* ===== RESPONSIVE ===== */
@media (max-width: 900px) {
  .about-grid { grid-template-columns: 1fr; gap: 48px; }
  .about-image { height: 360px; }
  .about-badge { bottom: -16px; left: 16px; }
  .menu-grid { grid-template-columns: 1fr; }
  .menu-card-img { height: 200px; }
  .gallery-grid { grid-template-columns: 1fr 1fr; grid-template-rows: auto; }
  .gallery-item-tall { grid-row: span 1; }
  .gallery-item-wide { grid-column: span 2; }
  .kontakt-grid { grid-template-columns: 1fr; }
  .kontakt-map { height: 300px; }
  .mt-grid { grid-template-columns: 1fr 1fr; }
}

@media (max-width: 640px) {
  .nav-toggle { display: flex; }
  .nav-links {
    display: none;
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background: rgba(10,6,3,0.98);
    backdrop-filter: blur(16px);
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 32px;
    z-index: 999;
  }
  .nav-link { font-size: 14px; letter-spacing: 3px; }
  .hero-ctas { flex-direction: column; }
  .mt-grid { grid-template-columns: 1fr; }
  .mt-card-full { flex-direction: column; align-items: flex-start; }
  .mt-abo-inner { flex-direction: column; }
  .gallery-grid { grid-template-columns: 1fr; }
  .gallery-item-wide { grid-column: span 1; }
  .footer-links { flex-direction: column; gap: 12px; }
}
```

- [ ] **Step 2: Auf Mobile prüfen** — Im Browser DevTools auf 375px (iPhone) und 768px (iPad) testen. Nav-Hamburger sollte funktionieren, alle Sektionen gestapelt.

- [ ] **Step 3: Commit**

```bash
git add -A
git commit -m "feat: add responsive mobile layout"
git push
```

---

### Task 10: Vercel Deployment

**Files:**
- Prüfen: `vercel.json`

- [ ] **Step 1: Vercel-Konto verknüpfen (falls nicht geschehen)**

Gehe auf [vercel.com](https://vercel.com) → "Add New Project" → GitHub-Repo `allegro-website` importieren.

Einstellungen:
- Framework Preset: **Other** (kein Framework)
- Build Command: *(leer lassen)*
- Output Directory: *(leer lassen / `.`)*
- Root Directory: *(leer lassen)*

→ "Deploy" klicken.

- [ ] **Step 2: Deployment verifizieren**

Vercel gibt eine URL wie `allegro-website-xxx.vercel.app` — diese im Browser aufrufen und alle 6 Sektionen prüfen:
- ✅ Hero mit Parallax
- ✅ Nav sticky beim Scrollen
- ✅ Mittagstisch-Karten
- ✅ Über uns mit Bild
- ✅ Speisekarte mit 3 Karten
- ✅ Galerie mit Lightbox
- ✅ Kontakt mit Karte
- ✅ Footer mit Links
- ✅ Mobile Nav funktioniert

- [ ] **Step 3: (Optional) Custom Domain**

Falls `allegro-pf.de` auf Vercel zeigen soll: Vercel Dashboard → Domains → `allegro-pf.de` hinzufügen → DNS beim Domain-Provider auf Vercel-Nameserver oder CNAME zeigen lassen.

- [ ] **Step 4: Final commit**

```bash
git add -A
git commit -m "feat: complete Allegro landing page ready for Vercel"
git push
```

---

## Checkliste Spec-Coverage

| Spec-Anforderung | Task |
|---|---|
| Navigation sticky | Task 2 |
| Hero mit Parallax + CTAs | Task 3 |
| Mittagstisch + Wochenkarte + E-Mail-Abo | Task 4 |
| Über uns + Inhaber-Zitat | Task 5 |
| Speisekarte Highlights | Task 6 |
| Galerie Masonry + Lightbox | Task 7 |
| Kontakt + Google Maps + Footer | Task 8 |
| Mobile Responsiveness | Task 9 |
| GitHub + Vercel Deployment | Task 1 + 10 |
| Rustico Farben + Playfair Display | Task 2 (CSS Vars) |
| Unsplash Bilder | Tasks 3, 5, 6, 7 |
| Fade-in Animationen | Task 2 (JS Observer) |
