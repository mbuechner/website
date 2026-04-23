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