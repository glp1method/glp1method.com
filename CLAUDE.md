# GLP-1 Method — Project Guide for Claude

## Site Overview
Static HTML site deployed on **GitHub Pages** at `glp1method.com`.
Repo: `https://github.com/glp1method/glp1method.com`

No build step, no framework — raw HTML/CSS files committed directly to `main`.

## File Structure
```
index.html                                      ← homepage / sales page
assessment.html                                 ← Food Noise Assessment landing page
blog/index.html                                 ← blog index
blog/what-semaglutide-does-to-your-brain.html   ← April 2026 (use as template for all future posts)
blog/emotional-eating-glp1.html                 ← May 2026
blog/glp1-mood-changes-emotional-flatness.html  ← June 2026
CNAME                                           ← glp1method.com
```

## Deployment
- Push to `main` → GitHub Pages auto-deploys (~60 seconds).
- GitHub Pages serves pretty URLs: `assessment.html` → `/assessment`, `blog/index.html` → `/blog/`.
- For local preview use `npx serve -p 4000 .` (no `-s` flag — SPA mode breaks routing).
- Locally, use `.html` extension for assessment: `localhost:4000/assessment.html`.

## Design System

### Fonts (Google Fonts)
- **Playfair Display** — headings, logo, display text
- **DM Sans** — body, nav, UI

### CSS Variables (defined in every file's `<style>` block)
```css
--forest:      #12302D   /* dark green — primary background, CTAs */
--forest-mid:  #1A4540
--forest-light:#235550
--gold:        #C9A84C   /* accent — logo, highlights, buttons */
--gold-light:  #E8C97A
--sage:        #4A9E98   /* secondary accent — labels, links */
--sage-light:  #7ABFBA
--cream:       #F2EDE6   /* page background */
--cream-dark:  #E8E0D5   /* newsletter section background */
--white:       #FFFFFF
--muted:       #8AADA9
--text-dark:   #1C2B2B
--text-mid:    #4A6060
```

## Nav Structure (identical across all pages)
```html
<nav>
  <a href="/" class="nav-logo">GLP-1 Method</a>
  <div class="nav-links">
    <a href="/blog/" class="nav-link">Blog</a>
    <a href="/assessment" class="nav-link">Free Assessment</a>
    <a href="https://glp1method.gumroad.com/l/tuajms" target="_blank" class="nav-cta">Get the Workbook</a>
  </div>
</nav>
```
Active page gets `class="nav-link active"` on its link.

### Mobile Nav (≤600px)
Nav wraps to two rows: logo on row 1, all three links on row 2. Each file's `<style>` block contains this rule — keep it consistent:
```css
@media (max-width: 600px) {
  nav { flex-wrap: wrap; padding: 12px 20px; gap: 0; }
  .nav-links { width: 100%; justify-content: flex-start; margin-top: 8px; padding-top: 8px; border-top: 1px solid rgba(201,168,76,0.15); gap: 16px; }
  .nav-link { font-size: 0.78rem; }
  .nav-cta { font-size: 0.75rem; padding: 8px 14px; }
}
```

## Newsletter Embed (Sender)
Form ID: `azp8Yy` — Sender account ID: `42891c26866884`

Embed markup (copy from any existing page when creating new blog posts):
```html
<div style="text-align: left" class="sender-form-field" data-sender-form-id="azp8Yy"></div>
```
Script tag goes before `</body>`:
```html
<script>
  (function (s, e, n, d, er) {
    s['Sender'] = er;
    s[er] = s[er] || function () { (s[er].q = s[er].q || []).push(arguments) }, s[er].l = 1 * new Date();
    s[er].on = function(event, callback) { s[er].listeners = s[er].listeners || {}; (s[er].listeners[event] = s[er].listeners[event] || []).push(callback); };
    var a = e.createElement(n), m = e.getElementsByTagName(n)[0];
    a.async = 1; a.src = d; m.parentNode.insertBefore(a, m)
  })(window, document, 'script', 'https://cdn.sender.net/accounts_resources/universal.js', 'sender');
  sender('42891c26866884');
</script>
```

Section wrapper uses `.newsletter-section` / `.newsletter-inner` classes (CSS in each file's style block):
- Background: `var(--cream-dark)`
- Padding: `72px 48px` desktop / `56px 24px` mobile

## Blog Post Template
Use `blog/what-semaglutide-does-to-your-brain.html` as the template for all future posts.

### Required `<head>` SEO tags (adapt per post)
```html
<title>[Post Title] | GLP-1 Method</title>
<meta name="description" content="[~155-char description]">
<meta property="og:title" content="[Post Title]">
<meta property="og:description" content="[Same as description]">
<meta property="og:url" content="https://glp1method.com/blog/[slug]">
<meta property="og:type" content="article">
<meta property="og:site_name" content="GLP-1 Method">
<meta property="article:published_time" content="[YYYY-MM-DD]">
<meta property="article:author" content="Zane Guilfoyle">
<meta name="author" content="Zane Guilfoyle, LPC">
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="[Post Title]">
<meta name="twitter:description" content="[Same as description]">
<link rel="canonical" href="https://glp1method.com/blog/[slug]">
```

### Blog index card order
Cards in `blog/index.html` must be ordered **newest first**. Add new post card at the top of the `.posts-grid`.

### Bottom-of-post order (top → bottom)
1. Article body (`.article-body`)
2. Newsletter section (`<!-- NEWSLETTER -->`)
3. Food Noise Assessment CTA (`<!-- BOTTOM CTA -->`, dark forest background)
4. Footer

## Key External Links
- Workbook (Gumroad): `https://glp1method.gumroad.com/l/tuajms`
- Assessment: `/assessment` (internal)
