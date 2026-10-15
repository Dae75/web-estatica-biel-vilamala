---
title: "Personalitzar la teva web"
intro: "Tot el que cal saber per canviar l'aspecte i el contingut d'una web feta amb Hugo."
toc: true
---

## On es canvia cada cosa

| Què vols canviar | Fitxer |
|---|---|
| Nom del site i adreça | `hugo.toml` |
| Opcions del menú | `hugo.toml`, bloc `[menus]` |
| Logo i peu de pàgina | `layouts/baseof.html` |
| Disseny de la portada | `layouts/home.html` |
| Disseny de les pàgines | `layouts/page.html` |
| Textos de cada pàgina | `content/*.md` |
| Colors i tipografia | `static/css/style.css` |
| Imatges | `static/img/` |

## Canviar el nom de la web

Són tres llocs:

1. A `hugo.toml`, la línia `title = '...'`.
2. A `layouts/baseof.html`, el logo de la capçalera i el text del peu.
3. A `content/_index.md`, la secció "Qui som".

## Afegir una pàgina nova

Crea el fitxer, per exemple `content/sobre-nosaltres.md`:

```markdown
---
title: "Sobre nosaltres"
---

Aquí va el text de la pàgina.
```

Afegeix-la al menú, a `hugo.toml`:

```toml
[[menus.main]]
  name = 'Sobre nosaltres'
  pageRef = '/sobre-nosaltres'
  weight = 70
```

El número de `weight` marca l'ordre: com més baix, més a l'esquerra.

## Escriure en Markdown

```markdown
## Títol de secció
Text amb **negreta** i *cursiva*.

- Element de llista
- Un altre element

[Text de l'enllaç](https://exemple.com)
```

## Afegir imatges

Posa la imatge a `static/img/foto.jpg` i, al Markdown, fes-hi referència així:

```markdown
![Descripció de la imatge](/web-estatica-biel/img/foto.jpg)
```

Recorda posar el nom del teu repositori al camí, perquè la web no està a l'arrel del domini.

## Canviar colors i estils

Al fitxer `static/css/style.css` trobaràs els colors principals:

| Color | Ús |
|---|---|
| `#0f172a` | Fons del menú |
| `#38bdf8` | Detalls i botons |
| `#1e40af` | Degradat de la capçalera |

Canvia'ls pels teus i desa. Amb `hugo server` engegat, veuràs el resultat a l'instant.

## Les plantilles

Les plantilles són HTML amb petites instruccions de Hugo entre dobles claus. Per exemple, `.Title` mostra el títol de la pàgina i `.Content` el seu contingut. Amb `baseof.html` defineixes l'estructura comuna (capçalera i peu) i les altres plantilles hi encaixen.

## Usar un tema

Si no vols crear el disseny des de zero, pots instal·lar un tema de la [galeria oficial](https://themes.gohugo.io). Cada tema explica la seva instal·lació, però el procés habitual és:

```bash
git submodule add https://github.com/AUTOR/NOM-DEL-TEMA.git themes/nom-del-tema
echo "theme = 'nom-del-tema'" >> hugo.toml
```

Si uses un tema, hauràs d'esborrar o adaptar les teves plantilles de `layouts/`, perquè tenen prioritat sobre les del tema. Al workflow de GitHub, afegeix `submodules: recursive` dins de `with:` al pas `actions/checkout`.
