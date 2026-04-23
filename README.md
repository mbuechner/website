# My website
My personal website.

## Voraussetzungen

- [Hugo Extended](https://gohugo.io/installation/) (getestet mit v0.160.1)
- [Node.js](https://nodejs.org/) (für Pagefind)
- Git

## Installation

1. Repository klonen:
```bash
git clone https://github.com/mbuechner/website.git
cd website
```

2. Git-Submodule initialisieren (lädt das Hugo-Theme):
```bash
git submodule update --init --recursive
```

## Webseite bauen

### Production Build

Erstelle die statische Webseite im `public/` Verzeichnis:

```bash
hugo
```

Erstelle anschließend den Suchindex mit Pagefind:

```bash
npx pagefind --site public
```

Die fertige Webseite befindet sich dann im `public/` Verzeichnis und kann auf einem Webserver bereitgestellt werden.

### Development Server

Starte den lokalen Development Server mit Live-Reload:

```bash
hugo server --buildDrafts --buildFuture
```

Die Webseite ist dann unter [http://localhost:1313/](http://localhost:1313/) erreichbar.

## Suche mit Pagefind

Diese Website verwendet [Pagefind](https://pagefind.app/) für die Volltextsuche. Nach jedem Build muss der Suchindex neu erstellt werden:

```bash
npx pagefind --site public
```

- **Voraussetzung:** Node.js muss installiert sein (siehe oben).
- Die Konfiguration erfolgt automatisch, Pagefind durchsucht alle HTML-Dateien im `public/`-Verzeichnis.
- Das Suchfeld ist nach dem Build sofort nutzbar.

**Tipp:** Mit `npx` wird immer die in `package.json` angegebene Version verwendet, falls vorhanden. Ohne `package.json` lädt `npx` die neueste Version aus dem Internet.