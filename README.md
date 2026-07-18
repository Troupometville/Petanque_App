# Planificateur Pétanque — Application Android

Ce dossier contient un projet **Capacitor** qui empaquette l'outil web existant
(`www/index.html`) dans une vraie application Android installable.

Il y a deux façons d'obtenir le fichier `.apk` à installer sur votre téléphone.
La première (GitHub) ne nécessite rien à installer sur votre ordinateur.
La seconde nécessite Android Studio en local.

---

## Option A — Compiler dans le cloud avec GitHub (recommandé, rien à installer)

1. Créez un compte gratuit sur [github.com](https://github.com) si vous n'en avez pas.
2. Créez un nouveau dépôt (bouton vert "New").
3. Mettez-y tout le contenu de ce dossier `petanque-app` (glisser-déposer les
   fichiers dans l'interface web de GitHub fonctionne très bien, pas besoin de
   ligne de commande).
4. Une fois les fichiers en ligne, allez dans l'onglet **Actions** du dépôt.
   Un workflow nommé "Build APK" se lance automatiquement (il est aussi
   déclenchable manuellement via "Run workflow").
5. Attendez la fin (2-5 minutes). Cliquez sur le run terminé, puis en bas de
   la page sur **planificateur-petanque-apk** dans "Artifacts" pour le
   télécharger — c'est un fichier `.zip` qui contient `app-debug.apk`.
6. Passez à la section **"Installer l'APK sur votre téléphone"** ci-dessous.

---

## Option B — Compiler en local avec Android Studio

Prérequis : [Node.js](https://nodejs.org) et
[Android Studio](https://developer.android.com/studio) installés sur votre
ordinateur (Android Studio installe automatiquement le SDK nécessaire).

Dans un terminal, à l'intérieur de ce dossier :

```bash
npm install
npx cap add android
npx cap sync android
npx cap open android
```

La dernière commande ouvre le projet dans Android Studio. Une fois qu'il a
fini d'indexer :

1. Menu **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
2. Une notification apparaît en bas à droite une fois terminé, avec un lien
   **"locate"** qui ouvre le dossier contenant `app-debug.apk`
   (chemin habituel : `android/app/build/outputs/apk/debug/app-debug.apk`).

---

## Installer l'APK sur votre téléphone

1. Transférez le fichier `app-debug.apk` sur votre téléphone Android (par
   e-mail à vous-même, via Google Drive, câble USB, Bluetooth... au choix).
2. Sur le téléphone, ouvrez le fichier depuis votre gestionnaire de fichiers
   ou l'application utilisée pour le transfert.
3. Android va vous avertir qu'il s'agit d'une source inconnue : acceptez et
   suivez le lien pour **autoriser l'installation depuis cette source**
   (le libellé exact dépend de la version d'Android, quelque chose comme
   "Autoriser depuis cette source" ou "Installer des applis inconnues").
4. Revenez à l'écran d'installation et appuyez sur **Installer**.
5. L'application "Planificateur Pétanque" apparaît alors dans votre tiroir
   d'applications avec sa propre icône, utilisable hors ligne.

> Ceci est un APK **debug**, suffisant pour un usage personnel. Il n'a pas
> besoin d'être publié sur le Play Store pour être installé de cette façon.

---

## Bon à savoir

- L'application est basée sur le fichier `www/index.html` : c'est exactement
  l'outil que vous utilisez déjà. Toute modification de cet outil peut être
  reportée ici en remplaçant `www/index.html`, puis en relançant
  `npx cap sync android` (ou en repoussant sur GitHub pour l'option A).
- Les sauvegardes (export/import) fonctionnent normalement : l'app tourne
  dans un vrai navigateur intégré (WebView), sans les restrictions du
  bac à sable de Claude.
- `appId` dans `capacitor.config.json` (`com.petanqueplanner.app`) identifie
  l'application de façon unique — ne le changez pas une fois l'app installée
  sur votre téléphone, sinon une réinstallation sera nécessaire.
