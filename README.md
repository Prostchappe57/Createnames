# CreateNames.ch – Deployment Guide

## Projektstruktur

```
createnames/
├── public/
│   ├── index.html        ← Homepage (Hero, AdSense, Features, App-Embed)
│   ├── app.html          ← Die fertige MyLegacy-App (deine Datei)
│   ├── impressum.html    ← Impressum
│   └── datenschutz.html  ← Datenschutzerklärung
├── vercel.json           ← Routing-Konfiguration
└── README.md
```

---

## 🚀 Deployment auf Vercel (Schritt für Schritt)

### Option A – Vercel CLI (empfohlen)

```bash
# 1. Vercel CLI installieren
npm install -g vercel

# 2. Im Projektordner anmelden
vercel login

# 3. Deployen
cd createnames
vercel --prod
```

Beim ersten Mal fragt Vercel:
- **Set up and deploy?** → Yes
- **Which scope?** → Dein Account
- **Link to existing project?** → No
- **Project name?** → createnames
- **In which directory?** → `./` (Root)
- **Override settings?** → No

### Option B – GitHub + Vercel Dashboard

1. GitHub Repository erstellen: `createnames`
2. Diesen Ordnerinhalt pushen
3. Auf [vercel.com](https://vercel.com) → "New Project" → GitHub-Repo importieren
4. Root Directory: `/` (kein Framework, Static Site)
5. → Deploy

### Eigene Domain verbinden

1. Vercel Dashboard → Dein Projekt → Settings → Domains
2. `createnames.ch` hinzufügen
3. Bei deinem Domain-Registrar (Swisscom, Switch, etc.) DNS setzen:
   ```
   A-Record:   @   →   76.76.21.21
   CNAME:      www →   cname.vercel-dns.com
   ```
4. Vercel stellt automatisch ein SSL-Zertifikat aus ✅

---

## 📢 Google AdSense einrichten

1. Konto erstellen: [adsense.google.com](https://adsense.google.com)
2. Domain `createnames.ch` hinzufügen und verifizieren
3. Deinen **Publisher-ID** (Format: `ca-pub-XXXXXXXXXXXXXXXX`) kopieren
4. In `public/index.html` ersetzen:
   ```
   ca-pub-XXXXXXXXXXXXXXXX  →  deine echte Publisher-ID
   ```
5. Ad-Slot-IDs (`1234567890`, `0987654321`) durch deine echten Slot-IDs ersetzen
6. Warten bis AdSense die Website genehmigt (1–14 Tage)

---

## ✏️ Impressum ausfüllen

In `public/impressum.html` und `public/datenschutz.html`:
- `Vorname Nachname` → deinen echten Namen
- `Musterstrasse 1` → deine Adresse
- `1234 Musterstadt` → Postleitzahl und Ort

---

## 🔧 Lokales Testen

```bash
# Mit npx serve (kein Node-Server nötig)
cd createnames
npx serve public

# Dann öffnen: http://localhost:3000
```

---

## Checkliste vor Go-Live

- [ ] AdSense Publisher-ID eingetragen
- [ ] Impressum mit echten Daten ausgefüllt
- [ ] Datenschutz-E-Mail-Adresse eingetragen
- [ ] Domain-DNS gesetzt
- [ ] SSL-Zertifikat aktiv (automatisch durch Vercel)
- [ ] Cookie-Banner getestet (Accept / Decline)
- [ ] App.html korrekt eingebettet (iframe)
- [ ] Mobile-Ansicht getestet
