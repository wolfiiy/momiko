+++
title = "Sous-domaine personnalisé avec Github Pages"
date = "2025-04-02T10:32:53+02:00"
author = "wolfiy"
authorTwitter = "" #do not include @
cover = ""
tags = ["réseau"]
keywords = ["réseau", "domaine", "Github"]
description = "Ce post décrit la marche à suivre pour mettre en place un sous-domaine personnalisé sur un site hébergé à l'aide du service Github Pages."
showFullContent = false
readingTime = true
hideComments = false
draft = false
+++

## Prérequis

Le code source du site doit être stocké dans un dépôt Git hébergé sur *Github*. A noter que ce dépôt doit être visible au public car l'utilisation de *Pages* avec un *repository* privé est limitée aux utilisateurs *Enterprise*.

### Déploiement du site

Pour ajouter un nom de domaine personnalisé, le site doit être publié sur *Github Pages*. Selon la méthode employée pour développer le site, les instructions diffèrent. Par exemple, le site sur lequel vous vous trouvez a été généré à l'aide de Hugo, et le *workflow Github* suivant est utilisé pour le déploiement.

{{< code language="yaml" open="false" title=".github/workflows/hugo.yaml" opts="lineNumbers=true" >}}
# Sample workflow for building and deploying a Hugo site to GitHub Pages
name: Deploy Hugo site to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches:
      - master

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

# Default to bash
defaults:
  run:
    shell: bash

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.145.0
      HUGO_ENVIRONMENT: production
      TZ: Europe/Zurich
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb
      - name: Install Dart Sass
        run: sudo snap install dart-sass
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5
      - name: Install Node.js dependencies
        run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
      - name: Cache Restore
        id: cache-restore
        uses: actions/cache/restore@v4
        with:
          path: |
            ${{ runner.temp }}/hugo_cache
          key: hugo-${{ github.run_id }}
          restore-keys:
            hugo-
      - name: Build with Hugo
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/" \
            --cacheDir "${{ runner.temp }}/hugo_cache"
      - name: Cache Save
        id: cache-save
        uses: actions/cache/save@v4
        with:
          path: |
            ${{ runner.temp }}/hugo_cache
          key: ${{ steps.cache-restore.outputs.cache-primary-key }}
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
{{< /code >}}

Cette configuration est tirée de la documentation de Hugo[^1].

[^1]: Hugo, *[Host on Github Pages](https://gohugo.io/host-and-deploy/host-on-github-pages/)*

## Configuration du DNS

Afin de permettre aux serveurs DNS de faire correspondre le nom de domaine personnel à celui généré automatiquement par Github, il faut créer un enregistrement `CNAME` faisant correspondre ceux-ci. Par exemple, dans mon cas, pour lier le sous-domaine `blog`:

{{< code language="dns" open="true" title="Enregistrement CNAME" opts="lineNumbers=true" >}}
blog 300 IN CNAME wolfiiy.github.io.
{{< /code >}}

ou, via l'interface web de mon *registrar*:

{{< figure src="/images/posts/custom-domain-github/cname-registrar.png" alt="Ajout d'un enregistrement CNAME pour le sous domaine blog" position="center" caption="Ajout d'un enregistrement CNAME pour le sous domaine blog." captionPosition="center">}}

### Vérification

Une fois le `CNAME` créé, son fonctionnement peut être vérifié à l'aide de la commande `dig <sous-domaine>.<domaine>.<tld>`. Celle-ci doit retourner le nom de domaine par défaut utilisé par les *Github Pages* ainsi que les 4 adresses IP suivantes[^2]:

- `185.199.108.153`
- `185.199.109.153`
- `185.199.110.153`
- `185.199.111.153`

[^2]: Github, *[Managing a Custom Domain for Your Github Pages Site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)*

Par exemple, après avoir exécuté `dig blog.wolfiy.ch`, la sortie suivante s'affiche:

{{< code language="txt" open="true" title="Output de la commande dig" opts="lineNumbers=true" >}}
; <<>> DiG 9.20.7 <<>> blog.wolfiy.ch
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 65404
;; flags: qr rd ra; QUERY: 1, ANSWER: 5, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;blog.wolfiy.ch.			IN	A

;; ANSWER SECTION:
blog.wolfiy.ch.		269	IN	CNAME	wolfiiy.github.io.
wolfiiy.github.io.	3569	IN	A	185.199.108.153
wolfiiy.github.io.	3569	IN	A	185.199.109.153
wolfiiy.github.io.	3569	IN	A	185.199.110.153
wolfiiy.github.io.	3569	IN	A	185.199.111.153

;; Query time: 3 msec
;; SERVER: 192.168.1.1#53(192.168.1.1) (UDP)
;; WHEN: Tue Apr 01 20:22:07 CEST 2025
;; MSG SIZE  rcvd: 138
{{< /code >}}

## Ajout du nom de domaine

Une fois la configuration du DNS validée, accéder au dépôt concerné sur *Github*. Sous *Settings* > *Pages* > *Custom domaine*, entrer le sous domaine à utiliser et cliquer sur *save*.

{{< figure src="/images/posts/custom-domain-github/dns-check-in-progress.png" alt="Vérification du DNS en cours" position="center" caption="Vérification du DNS en cours." captionPosition="center">}}

Ensuite, une vérification DNS s'effectue alors et, après quelques minutes, le message *DNS Check successful* apparait.

{{< figure src="/images/posts/custom-domain-github/dns-check-successful.png" alt="Vérification du DNS terminée" position="center" caption="Vérification du DNS terminée." captionPosition="center">}}

### HTTPS

Juste en dessous du champ permettant d'ajouter un domaine, une case à cocher permet de forcer le passage du trafic en HTTPS. Si cette option est grisée, attendre quelques minutes afin qu'un certificat soit généré.

{{< figure src="/images/posts/custom-domain-github/cert-01.png" alt="Première étape de la génération du certificat" position="center" caption="Première étape de la génération du certificat." captionPosition="center">}}

{{< figure src="/images/posts/custom-domain-github/cert-02.png" alt="Seconde étape de la génération du certificat" position="center" caption="Seconde étape de la génération du certificat." captionPosition="center">}}

{{< figure src="/images/posts/custom-domain-github/cert-03.png" alt="Dernière étape de la génération du certificat" position="center" caption="Dernière étape de la génération du certificat." captionPosition="center">}}

Ce processus peut théoriquement durer jusqu'à 24 heures, mais dans les faits, une dizaine de minutes suffit largement.

Enfin, la case *Enforce HTTPS* peut être cochée.

{{< figure src="/images/posts/custom-domain-github/enforce-https.png" alt="Forcer le trafic en HTTPS" position="center" caption="Forcer le trafic en HTTPS." captionPosition="center">}}

### Problèmes potentiels

Si, lors du chargement d'un site généré avec Hugo sur un navigateur basé sur *Chromium*, aucune feuille de style ou aucun script ne semble être chargé, et que la console affiche un message d'erreur du type "Cross request from HTTP to HTTPS", dépublier puis republier le site. Cela pourrait être simplement dû à un problème de cache. Aussi, ne pas oublier de changer la `baseUrl`[^3].

[^3]: Github, *[Securing Your Github Pages Site With HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)*