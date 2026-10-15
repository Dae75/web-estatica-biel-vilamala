---
title: "Preguntes habituals i recursos"
intro: "Els errors que ens han sortit a Biel i a Marc mentre fèiem aquesta web, i com es resolen."
toc: true
---

## Errors habituals

### La web no té estils a GitHub Pages
Revisa que el `baseURL` del `hugo.toml` coincideixi exactament amb l'adreça de la web, incloent el nom del repositori.

### Error 404 a GitHub Pages
Comprova que a **Settings → Pages** la font sigui **GitHub Actions** i que el workflow hagi acabat en verd a la pestanya **Actions**.

### `hugo: command not found`
Reinicia el terminal. Si continua fallant, torna a executar la instal·lació de Hugo.

### `found no layout file`
Hugo no troba les plantilles. Comprova que a `layouts/` hi ha `baseof.html`, `home.html` i `page.html`.

### Hugo mostra avisos de `deprecated`
Normalment són canvis de noms entre versions. L'avís indica quina opció has de substituir i per quina. Per exemple, `languageCode` ara es diu `locale`.

### `git init` diu "Reinitialized existing Git repository"
Estàs dins d'una carpeta que ja pertany a un altre repositori. Entra a la carpeta del projecte abans de fer `git init`.

## Preguntes freqüents

### Cal saber programar?
No gaire. Per escriure contingut només cal Markdown. Per a les plantilles et serviran nocions bàsiques d'HTML i CSS.

### Es pot fer un blog?
Sí, és un dels usos més habituals. Crea una carpeta `content/blog/` amb un fitxer per entrada.

### Es poden fer formularis de contacte?
La web és estàtica, així que cal un servei extern com Formspree o Netlify Forms.

### Es pot usar un domini propi?
Sí. GitHub Pages permet configurar un domini personalitzat a **Settings → Pages**.

## Recursos

- [Documentació oficial de Hugo](https://gohugo.io/documentation/)
- [Galeria de temes](https://themes.gohugo.io)
- [Fòrum de la comunitat](https://discourse.gohugo.io)
- [Documentació de GitHub Pages](https://docs.github.com/pages)
- [Guia de Markdown](https://www.markdownguide.org)
