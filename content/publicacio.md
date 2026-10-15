---
title: "Publicar la web a GitHub Pages"
intro: "Posa la teva web en línia gratis i fes que s'actualitzi sola cada cop que pugis canvis."
toc: true
---

## Com funciona

GitHub Pages serveix fitxers estàtics, així que és ideal per a Hugo. Amb **GitHub Actions** configurem un procés automàtic: cada vegada que fas `git push`, GitHub construeix la web amb Hugo i la publica.

## 1. Configurar el `baseURL`

Al fitxer `hugo.toml`, posa l'adreça final de la web:

```toml
baseURL = 'https://EL-TEU-USUARI.github.io/NOM-DEL-REPOSITORI/'
```

L'usuari va **en minúscules** a l'adreça, encara que el teu usuari tingui majúscules. Per exemple, l'usuari `Dae75` es converteix en `dae75.github.io`.

## 2. Crear el `.gitignore`

A l'arrel del projecte, crea un fitxer `.gitignore` amb:

```
public/
resources/_gen/
.hugo_build.lock
```

Així no pugem a GitHub els fitxers que Hugo genera sol.

## 3. Crear el workflow

Crea el fitxer `.github/workflows/hugo.yml`:

```yaml
name: Desplega Hugo a GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.168.0
    steps:
      - name: Instal·lar Hugo
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb
          sudo dpkg -i ${{ runner.temp }}/hugo.deb
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v5
        id: pages
      - name: Construir
        run: hugo --minify --baseURL "${{ steps.pages.outputs.base_url }}/"
      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - id: deployment
        uses: actions/deploy-pages@v4
```

Posa a `HUGO_VERSION` la mateixa versió que tens instal·lada (`hugo version`), així la web es construeix igual a GitHub que al teu ordinador.

## 4. Crear el repositori a GitHub

1. Ves a [github.com/new](https://github.com/new).
2. Posa-li un nom, marca **Public** i **no** afegeixis README, .gitignore ni llicència.
3. Clica **Create repository**.

## 5. Pujar el codi

```bash
git add .
git commit -m "Primera versió de la web"
git remote add origin https://github.com/EL-TEU-USUARI/NOM-DEL-REPOSITORI.git
git push -u origin main
```

## 6. Activar GitHub Pages

1. Al repositori, ves a **Settings → Pages**.
2. A **Build and deployment → Source**, tria **GitHub Actions**.
3. Ves a la pestanya **Actions** i espera que el desplegament acabi en verd (1-2 minuts).
4. La web serà a `https://EL-TEU-USUARI.github.io/NOM-DEL-REPOSITORI/`.

## 7. Publicar canvis nous

Cada cop que modifiquis alguna cosa:

```bash
git add .
git commit -m "Descripció del canvi"
git push
```

En un parell de minuts la web publicada s'actualitza.

## Alternatives

Hugo també es pot publicar a Netlify, Cloudflare Pages o a qualsevol hostatge que serveixi fitxers estàtics: només cal pujar el contingut de la carpeta `public/` després d'executar `hugo`.
