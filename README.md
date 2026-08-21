# team-moeller.de — statische Website

Statischer Export der Website https://team-moeller.de/ (vorher CMSimple 5.20), migriert am 21.08.2026.
Reines HTML/CSS — kein PHP, kein Build-Schritt, direkt über GitHub Pages auslieferbar.

## Struktur

```
index.html                  Startseite („Willkommen") — die einzige index.html
add-ins.html                Add-Ins-Übersicht
add-ins/                    …ihre Unterseiten (z. B. add-ins/tm-vba-inspector.html)
downloads.html              Downloads-Seite
downloads/                  später die Download-Dateien selbst (zip/pdf)
tipps-und-tricks.html + tipps-und-tricks/   inkl. wizhook-objekt.html + wizhook-objekt/…
links.html + links/
donations.html, service.html, impressum.html, datenschutzerklaerung.html
historie.html + historie/   Jahresarchive (historie/2000.html …)
willkommen/access.html      versteckte Unterseite der Startseite
inhaltsverzeichnis.html     statische Sitemap (ersetzt CMSimple ?&sitemap)
en.html + en/               englische Version (Sitemap: en/sitemap.html)
assets/css/                 core.css + template.css (ehem. CMSimple-Template msninsp2)
assets/images/              alle Bilder (userfiles + Template-Grafiken unter template/)
404.html                    Fehlerseite für GitHub Pages
```

Schema: jede Seite ist eine `<name>.html`; hat sie Unterseiten, liegen die in einem
gleichnamigen Ordner daneben. Alle Links/Assets sind **relativ** — die Seite läuft auch
lokal per `python3 -m http.server` oder unter einem Repo-Unterpfad.

## Gegenüber dem CMS entfernt/ersetzt

- Suchfunktion (PHP) — entfernt; Empfehlung für später: [Pagefind](https://pagefind.app/)
- Kontakt-Formular → `mailto:webmaster@team-moeller.de`
- Besucherzähler (CountVisits) — ersatzlos entfernt
- Druckansicht-Link (`?&print`) — entfernt (später per Print-CSS lösbar)
- Google-Analytics-Snippet (ga.js) und toter Google+-Footerlink — entfernt
- `Datenschutzerkaerung` (Tippfehler im CMS) → Ordner heißt jetzt `datenschutzerklaerung/`

Inhalte sind ansonsten 1:1 identisch übernommen (Layout, Texte, Bilder).

## Noch offen

- **Download-Dateien**: bewusst nicht mitkopiert. Alle Seiten verlinken bereits auf
  `downloads/<datei>` — Liste der 58 Dateien in [downloads-manifest.md](downloads-manifest.md).
  Quelle: `https://team-moeller.de/userfiles/downloads/<datei>`.
- **Tote Links**: siehe [link-report.md](link-report.md) — u. a. zwei interne Links auf der
  Links-Seite, deren Zielseiten schon im CMS fehlten.
- `downloads-manifest.md` und `link-report.md` vor dem Livegang löschen oder behalten — Geschmackssache.

## GitHub Pages einrichten

1. Repo anlegen, diesen Ordner pushen.
2. Settings → Pages → „Deploy from a branch", Branch `main`, Ordner `/ (root)`.
3. Custom Domain `team-moeller.de` eintragen (legt die `CNAME`-Datei an) und beim
   DNS-Provider A/AAAA-Records auf GitHub Pages zeigen lassen bzw. `www` per CNAME.
4. „Enforce HTTPS" aktivieren, sobald das Zertifikat ausgestellt ist.

Die Datei `.nojekyll` verhindert, dass GitHub Pages den Jekyll-Prozessor über die Dateien laufen lässt.
