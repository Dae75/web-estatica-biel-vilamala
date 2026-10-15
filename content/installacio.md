---
title: "Guia d'instal·lació de Hugo"
intro: "De zero a una web funcionant al teu ordinador en uns 15 minuts. Són els mateixos passos que vam seguir en Biel i en Marc."
toc: true
---

## Requisits

- Un ordinador amb Windows, macOS o Linux.
- Un terminal. A Windows recomanem **Git Bash**, que s'instal·la amb Git.
- Un editor de codi, per exemple [VS Code](https://code.visualstudio.com).
- Un compte a [GitHub](https://github.com), necessari per a la pàgina de publicació.

## 1. Instal·lar Git

### Windows
```powershell
winget install Git.Git
```

### macOS
```bash
brew install git
```

### Linux (Debian/Ubuntu)
```bash
sudo apt install git
```

## 2. Instal·lar Hugo

Instal·la sempre l'edició **extended**, que inclou funcions extra (com processar SASS) i és la que fan servir la majoria de temes.

### Windows
```powershell
winget install Hugo.Hugo.Extended
```

### macOS
```bash
brew install hugo
```

### Linux
```bash
sudo snap install hugo
```

## 3. Comprovar la instal·lació

Tanca el terminal, obre'n un de nou i executa:

```bash
git --version
hugo version
```

Si Hugo respon amb un número de versió i la paraula `extended`, tot està bé. Si diu `command not found`, reinicia el terminal o l'ordinador.

## 4. Configurar Git (només el primer cop)

```bash
git config --global user.name "El teu nom"
git config --global user.email "el-teu-correu@exemple.com"
```

## 5. Crear el primer site

```bash
hugo new site el-meu-site
cd el-meu-site
git init -b main
```

Assegura't d'estar **dins la carpeta del projecte** abans de fer `git init`. Així el repositori és exclusiu d'aquesta web. Si ho fas des d'una carpeta que ja és un repositori, Git mostrarà el missatge `Reinitialized existing Git repository`, i aleshores estàs al lloc equivocat.

## 6. Estructura que s'ha creat

| Carpeta o fitxer | Per a què serveix |
|---|---|
| `content/` | Les pàgines, escrites en Markdown |
| `layouts/` | Les plantilles HTML |
| `static/` | Fitxers que es copien tal qual (CSS, imatges) |
| `assets/` | Fitxers que Hugo pot processar |
| `data/` | Dades en JSON, YAML o TOML |
| `archetypes/` | Models per a pàgines noves |
| `hugo.toml` | La configuració del site |

## 7. Crear les plantilles mínimes

Hugo no mostra res sense plantilles. Dins de `layouts/` calen tres fitxers:

| Fitxer | Funció |
|---|---|
| `baseof.html` | L'estructura comuna: capçalera, menú i peu |
| `home.html` | El disseny de la portada |
| `page.html` | El disseny de la resta de pàgines |

Si no existeixen, Hugo mostra l'avís `found no layout file`. El codi complet el pots veure al repositori d'aquesta web, o bé pots usar un [tema](../personalitzacio/#usar-un-tema).

## 8. Provar en local

Engega el servidor de desenvolupament:

```bash
hugo server
```

Obre l'adreça que mostra el terminal (normalment `http://localhost:1313`). Els canvis que facis als fitxers es veuen al navegador a l'instant. Atura el servidor amb `Ctrl+C`.

## Següent pas

Quan la web funcioni en local, passa a la guia de [publicació](../publicacio/).
