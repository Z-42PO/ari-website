Site web de l'association d'airsoft "Airsoft Rhône Immersion"

# Comment mettre à jour le site ?

⚠️ **NE PAS** modifier le dossier `themes` ⚠️

## Prérequis

Installer les éléments suivants sur votre PC : 

- Git
- Hugo extended
- Node
- Go

👉 [Voir la page dédiée](https://github.com/zeon-studio/hugoplate?tab=readme-ov-file#-prerequisites) pour plus de détails.

## Récupération du code

```bash
git clone [...]
```

Avant toute modification, dans le dossier du site, vérifiez que vous avez la dernière version du code : 

```bash
git pull
```

Installer ensuite les dépendances

```bash
npm install
```

## Lancer le site localement

A taper dans le dossier du site :

```bash
npm run dev
```

Le site est alors accessible à l'adresse `http://localhost:1313/` dans votre navigateur. Vos modifications sont visibles en temps réel.

## Création / modification d'une page

### Le menu

Il menu est modifiable depuis le fichier `config/_default/menus.toml`

### Images et style

Si besoin de rajouter des images ou du style CSS, c'est dans le dossier `assets`. Le dossier `public` ne doit pas être modifié, il est généré lors du `run` et `build`.

⚠️ Bien utiliser des fichiers `.jpg` compressés à 75%. Côté max de 2000px. Eviter les `.png` autant que possible. Pour les images à fond transparent, essayer le `.svg` d'abord, plus léger, sinon utiliser le `.png` (pas le choix).

⚠️ NE PAS mettre d'espace dans les noms de fichiers (image ou autre).

### Pages

Les nouvelles pages sont à ajouter dans le dossier `content/pages` au format Markdown

### Shortcodes

Les shortcodes sont des blocs pré-concus pour afficher du contenu. La syntaxe est la suivante : `{{< nom-du-shortcode param1="" param2="" >}}Contenu au format Markdown et HTML{{< /nom-du-shortcode >}}`.

Tous les shortcodes n'acceptent pas du contenu riche donc la balise fermante n'est pas toujours nécessaire.

La structure HTML des shortcodes est dans `layouts/shortcodes`

#### Shortcode "features"

Permet d'afficher un contenu d'un côté et une image de l'autre.

```md
{{< features image="" video="" position="" title="" >}}
Contenu Markdown
{{< /features >}}
```

- `image` : chemin de l'image (relatif au site, par expl `/images/...`)
- `video` : id de la vidéo youtube (dans l'url `watch?v=VavncV32F0A` l'id est `VavncV32F0A`)
- `position` : position de l'image/vidéo (peut être `left` ou `right`)
- `title` : titre du bloc texte

#### Shortcode "columns"

Permet d'afficher du contenu en colonne. Le nombre d'utilisation du shortcode `column` détermine le nombre de colonne.

```md
{{< columns >}}
{{< column image="" title="" >}}
Contenu Markdown
{{< /column >}}

{{< column image="" title="" >}}
Contenu Markdown
{{< /column >}}
{{< /columns >}}
```

- `image` : chemin de l'image (relatif au site, par expl `/images/...`)
- `title` : titre du bloc texte

#### Shortcode "gslides"

Permet d'afficher un google slide.

```md
{{< gslides src="" title="" >}}
```

- `src` : url du google slide au format `https://docs.google.com/presentation/d/.../embed`
- `title` : titre du google slide

#### Autres shortcodes

Voir la page `content/pages/elements.md`

## Sauvegarde des modifications

Une fois les modifications effectuées, il faut les sauvegarder sur le dépôt distant :

```bash
git add .
git commit -m "feat: Update content"
git push --force-with-lease
```

## Mise à jour du site

Il faut builder le site pour avoir la version de production du code :

```bash
npm run build
```

Puis uploader le dossier `public` sur l'espace d'hébergement.

# Liens

[Documentation de Hugoplate](https://github.com/zeon-studio/hugoplate)

[Documentation des modules Hugo](https://github.com/gethugothemes/hugo-modules)

[Documentation de Tailwind](https://tailwindcss.com/docs/styling-with-utility-classes)