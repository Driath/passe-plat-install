# Installer Passe-plat sur une machine

Un seul fichier `.sh` à télécharger puis à exécuter sur **macOS ou Linux**.
Aucun clone Git, compte GitHub ou Homebrew n'est nécessaire.

## Installation

1. [Télécharger passe-plat-install.sh](https://github.com/Driath/passe-plat-install/releases/latest/download/passe-plat-install.sh) sur la machine où tourneront vos apps.
2. Ouvrir son terminal et lancer :

   ```sh
   sh ~/Downloads/passe-plat-install.sh
   ```

   Si le fichier est ailleurs, taper `sh` suivi d'une espace, puis glisser le fichier dans le terminal.
3. Suivre les indications du script, puis scanner son QR depuis **Ajouter une machine** dans l'app Passe-plat.

Depuis un terminal disposant de `curl`, le téléchargement peut aussi se faire ainsi :

```sh
curl -fL --proto '=https' https://github.com/Driath/passe-plat-install/releases/latest/download/passe-plat-install.sh -o passe-plat-install.sh &&
sh passe-plat-install.sh
```

Le téléchargement se termine avant l'exécution. L'entrée du terminal reste disponible pour les questions interactives.

## Ce que fait le script

Le fichier contient la distribution machine complète. Il vérifie l'intégrité de son
archive, l'extrait temporairement, dépose la commande dans `~/.passe-plat/bin`, puis
lance la préparation interactive. Il conserve les appairages et paramètres existants.
Les réglages personnels des agents restent inchangés ; leurs hooks sont chargés au
lancement de l'app concernée.

Tailscale connecté, tmux et un serveur SSH sont des prérequis. Leur absence est détectée
avec une erreur codée en anglais et un lien ou une indication de préparation. Cette
version ne les installe pas automatiquement et n'exécute jamais `brew`.
Une installation existante de ces outils reste utilisable, quelle que soit son origine.

Le script cible macOS et Linux avec un shell POSIX et les utilitaires système usuels
(`tar`, `gzip`, `base64`, `mktemp`, `awk`, `shasum` ou `sha256sum`). Un fichier `.sh`
ne rend pas les systèmes sans shell POSIX compatibles.

## Vérifier ou lire avant installation

Chaque release contient le fichier et son empreinte SHA-256. L'empreinte intégrée détecte
une archive endommagée ; elle ne remplace pas la confiance dans la provenance du fichier.

```sh
sh passe-plat-install.sh --help
sh passe-plat-install.sh --extract-to ./passe-plat-sources
```

La seconde commande extrait les sources machine dans un **nouveau** répertoire sans
installer Passe-plat. La distribution ne contient aucune configuration ou clé d'utilisateur.

## Relancer

```sh
sh passe-plat-install.sh               # actualise les fichiers, conserve les appairages
passe-plat init --show                # affiche explicitement un nouveau QR
passe-plat doctor --json              # diagnostic
passe-plat uninstall                  # désinstallation
```

Après la première installation, ouvrir un nouveau terminal pour utiliser `passe-plat`,
ou appeler `~/.passe-plat/bin/passe-plat` depuis le terminal courant.
