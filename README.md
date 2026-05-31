# French Quiz App

Une application web de quiz de français, **100 % statique** (sans serveur), hébergée gratuitement sur **GitHub Pages**. Le contenu des quiz est créé et publié depuis une application de bureau, l'**Admin Tool**, sans jamais toucher au code.

Ce dépôt est un **modèle (template)** : créez votre propre copie en quelques minutes et obtenez un site comme celui-ci :

> **`https://<votre-utilisateur>.github.io/french-quiz-app/`**

<!-- screenshot: page d'accueil de l'application étudiante -->

---

## Mise en route (de zéro à un site en ligne)

### Étape 1 — Créer votre dépôt depuis ce modèle

1. En haut de cette page, cliquez sur **« Use this template »** → **« Create a new repository »**.
2. Donnez-lui un nom (par ex. `french-quiz-app`).
3. Réglez la visibilité sur **Public** (requis pour GitHub Pages gratuit).
4. Cliquez sur **« Create repository »**.

<!-- screenshot: bouton "Use this template" -->

### Étape 2 — Activer GitHub Pages

Le workflow `.github/workflows/pages.yml` inclus déploie le site automatiquement. Il suffit de pointer Pages dessus une seule fois :

1. Dans votre nouveau dépôt : **Settings → Pages**.
2. Sous **Build and deployment → Source**, choisissez **« GitHub Actions »**.

C'est tout : à chaque publication de quiz, le site se redéploie tout seul.

### Étape 3 — Générer un jeton d'accès GitHub (PAT)

L'Admin Tool publie vos quiz en poussant sur votre dépôt ; il lui faut un jeton.

1. GitHub → **Settings → Developer settings → Personal access tokens → Tokens (classic)**.
2. **Generate new token (classic)**.
3. Cochez la portée **`repo`**.
4. Générez et **copiez le jeton** (il ne sera plus affiché ensuite).

> Conservez ce jeton en lieu sûr. Vous le collerez dans l'Admin Tool à l'étape 6.

### Étape 4 — Cloner le dépôt en local (GitHub Desktop)

L'Admin Tool lit et écrit les fichiers dans une copie locale de votre dépôt.

1. Installez **[GitHub Desktop](https://desktop.github.com/)** si nécessaire.
2. Sur la page de votre dépôt : **Code → Open with GitHub Desktop**.
3. Choisissez un dossier local (par ex. `~/Documents/French Quiz App`).

### Étape 5 — Installer l'Admin Tool

1. Téléchargez la dernière version depuis les **[Releases de l'Admin Tool](https://github.com/alakin66/french-quiz-app-admin/releases)** :
   - `Quiz.Admin_x.y.z_aarch64.dmg` (macOS Apple Silicon — M1/M2/M3).
2. Ouvrez le `.dmg` et glissez **Quiz Admin** dans **Applications**.
3. Au premier lancement, macOS peut afficher « impossible d'ouvrir car développeur non identifié ». L'app est signée en ad-hoc : faites un **clic droit → Ouvrir**, puis confirmez **Ouvrir**. (À faire une seule fois.)

### Étape 6 — Configurer l'Admin Tool

Au premier lancement, l'écran **Paramètres** s'affiche.

| Champ | Valeur |
|---|---|
| **Dossier du dépôt local** | le dossier cloné à l'étape 4 (bouton **Parcourir…**) |
| **Utilisateur GitHub** | votre nom d'utilisateur GitHub |
| **Dépôt GitHub** | `votre-utilisateur/french-quiz-app` |
| **Jeton GitHub** | le jeton de l'étape 3 |
| (optionnel) **Fournisseur / Clé API LLM** | pour la génération de quiz par IA |

Enregistrez. Le dossier est initialisé automatiquement (`data/quizzes.json` et `data/quizzes.js`) s'il est vide.

<!-- screenshot: écran Paramètres -->

### Étape 7 — Créer et publier votre premier quiz

1. Sur la page **Modules**, créez un module (ou importez un fichier Excel `.xlsx`).
2. Ajoutez des quiz et des questions ; rédigez l'introduction du module.
3. Cliquez sur **🚀 Publier**, saisissez un message, puis confirmez.
4. L'Admin Tool pousse `data/quizzes.js` sur GitHub ; le workflow déploie le site (~1 min).
5. Ouvrez **`https://<votre-utilisateur>.github.io/french-quiz-app/`** : votre quiz est en ligne.

---

## Dépannage

| Problème | Cause probable / solution |
|---|---|
| **« git introuvable » à la publication** | git n'est pas installé. Installez **[GitHub Desktop](https://desktop.github.com/)** (il fournit git), puis relancez l'Admin Tool. |
| **« repoPath non configuré » ou modules absents** | Le **Dossier du dépôt local** pointe au mauvais endroit. Il doit viser la **racine** du dépôt cloné (celui qui contient le dossier `data/`), pas le dossier `data/` lui-même. |
| **La publication échoue (401 / 403)** | Jeton expiré ou sans la portée `repo`. Regénérez-en un (étape 3) et collez-le dans les Paramètres. |
| **Le site ne se met pas à jour** | Vérifiez l'onglet **Actions** du dépôt : le workflow « Deploy to GitHub Pages » doit réussir. Source Pages bien réglée sur **GitHub Actions** (étape 2). |
| **macOS refuse d'ouvrir l'app** | **Clic droit → Ouvrir** (et non double-clic) la première fois (voir étape 5). |

---

## Comment ça marche

```
Admin Tool (bureau)  →  data/quizzes.js  →  GitHub Pages  →  index.html (quiz interactif)
```

- `index.html`, `js/student.js`, `css/student.css` — l'application étudiante (statique).
- `data/quizzes.js` — données des quiz, générées et poussées par l'Admin Tool ; **ne pas modifier à la main**.
- `data/quizzes.json` — source au format admin (lue par l'Admin Tool).
- `.github/workflows/pages.yml` — déploiement automatique sur GitHub Pages.

L'Admin Tool et son code source vivent dans un dépôt séparé : **[french-quiz-app-admin](https://github.com/alakin66/french-quiz-app-admin)**.
