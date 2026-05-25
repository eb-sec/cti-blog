# THREAT//THREAD – Deployment Guide

## Was du bekommst

- `index.html`  – Startseite mit Postliste
- `post.html`   – Vorlage für jeden Blogpost
- `about.html`  – Über-mich-Seite (noch zu erstellen, Vorlage unten)

Keine Dependencies, kein Build-Step, kein Node.js.
Reines HTML/CSS – du kannst es überall hosten.

---

## Option 1 – GitHub Pages (empfohlen, kostenlos)

### Schritt 1: Repository erstellen

```bash
# Neues Repository auf github.com erstellen
# Name: deinbenutzername.github.io  (für Root-Domain)
# oder: cti-blog  (für deinbenutzername.github.io/cti-blog)

git clone https://github.com/DEIN_USERNAME/cti-blog
cd cti-blog
```

### Schritt 2: Dateien hinzufügen

```bash
cp index.html post.html about.html ./
git add .
git commit -m "initial blog setup"
git push origin main
```

### Schritt 3: GitHub Pages aktivieren

1. Repository → Settings → Pages
2. Source: "Deploy from a branch"
3. Branch: main / root
4. Save

Blog ist live unter: `https://DEIN_USERNAME.github.io/cti-blog`

---

## Option 2 – Eigene Domain + Netlify (empfohlen für professionellen Auftritt)

### Schritt 1: Domain kaufen

Empfohlene Anbieter:
- **Namecheap** – günstig, ~10€/Jahr für .com
- **Porkbun** – oft günstiger als Namecheap
- **INWX** – deutsch, DSGVO-konform

Gute Domain-Ideen für CTI-Blogs:
- `vorname-security.com`
- `vorname-cti.io`
- `threatthread.io`
- `deinname.security`

### Schritt 2: Netlify einrichten

1. netlify.com → Sign up (kostenlos)
2. "Add new site" → "Deploy manually"
3. Blog-Ordner reinziehen (drag & drop)
4. Netlify gibt dir eine URL: `random-name.netlify.app`

### Schritt 3: Eigene Domain verbinden

1. Netlify → Site settings → Domain management
2. "Add custom domain" → deine Domain eingeben
3. Bei deinem Domain-Anbieter die Netlify-Nameserver eintragen:
   ```
   dns1.p01.nsone.net
   dns2.p01.nsone.net
   dns3.p01.nsone.net
   dns4.p01.nsone.net
   ```
4. 15–30 Minuten warten bis DNS propagiert
5. Netlify aktiviert HTTPS automatisch (Let's Encrypt)

---

## Neuen Post erstellen

1. `post.html` kopieren:
   ```bash
   cp post.html posts/misp-cti-pipeline.html
   ```

2. Im neuen File anpassen:
   - `<title>` im Head
   - Post-Metadaten (Datum, Tags, Lesezeit)
   - `<h1 class="post-title">` – Titel
   - `<p class="post-subtitle">` – Untertitel/Lead
   - Inhalt der `<article class="article-body">` ersetzen
   - Related Posts am Ende anpassen

3. In `index.html` einen neuen Card-Eintrag hinzufügen:
   ```html
   <a href="posts/dein-post.html" class="post-card">
     <div class="card-meta">
       <span class="tag tag-red">Dein Tag</span>
       <span class="post-date">Jun 01, 2026</span>
     </div>
     <h3 class="card-title">Dein Titel</h3>
     <p class="card-excerpt">Kurze Beschreibung...</p>
     <div class="card-footer">
       <span class="read-time">X min read</span>
       <span class="card-arrow">→</span>
     </div>
   </a>
   ```

---

## Was du noch anpassen musst

Suche in allen HTML-Dateien nach diesen Platzhaltern und ersetze sie:

| Platzhalter | Ersetzen mit |
|---|---|
| `THREAT//THREAD` | Dein Blog-Name (oder behalten) |
| `CTI Research` | Dein Tagline |
| `contact@yoursite.com` | Deine E-Mail |
| `https://github.com` | Dein GitHub-Profil |
| `junior_cti_analyst` | Dein Username |
| `12` (Post-Anzahl) | Aktuelle Zahl |

---

## About-Seite erstellen

Kopiere `index.html`, entferne Hero/Posts/About-Strip und füge folgendes ein:

```html
<div class="about-page" style="max-width:720px;margin:120px auto 80px;padding:0 40px">
  <h1 style="font-family:var(--display);font-size:42px;font-weight:800;
             color:var(--white);margin-bottom:24px">About</h1>
  <p style="font-size:18px;color:var(--text2);line-height:1.8;margin-bottom:20px">
    Dein Text hier.
  </p>
</div>
```

---

## DSGVO-Hinweis (Deutschland)

Da du in Deutschland wohnst:

- Google Fonts werden aktuell direkt von Google geladen → DSGVO-Problem
- Lösung: Fonts selbst hosten

```bash
# Fonts herunterladen (google-webfonts-helper.herokuapp.com)
# Dann in CSS ersetzen:
@font-face {
  font-family: 'Syne';
  src: url('/fonts/syne-800.woff2') format('woff2');
  font-weight: 800;
}
```

- Kein Analytics ohne Cookie-Banner
- Impressum + Datenschutzerklärung nötig wenn öffentlich erreichbar
  (easygenerator.de für kostenlose Datenschutzerklärung)

---

## Fertig

Dein Blog ist live. Erster Post: MISP-CTI-Bridge Write-up.
