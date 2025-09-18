# Edumapper - Estimation de Chances d'Accès

Bienvenue sur le projet Edumapper, développé dans le cadre d'un test technique. L'objectif est de recréer une interface utilisateur inspirée des maquettes Figma fournies, en utilisant Nuxt 4, TypeScript et Tailwind CSS.

---

## ✨ Fonctionnalités implémentées

- **Interface Utilisateur Responsive** : Intégration des maquettes Figma pour mobile, tablette et desktop.
- **Sélection de Lycée Dynamique** : Champ d'autocomplete pour choisir un lycée parmi une liste d'établissements.
- **Formulaire Interactif "Classe"** :
    - Accordion "Classe" pour masquer/afficher les options.
    - Groupes de boutons (chips) pour la sélection de la classe et du type de bac.
    - Gestion des états de sélection (simple, désélection possible).
    - Bouton "Confirmer" intégré à l'accordion pour valider les choix.
    - Réinitialisation des sélections temporaires si l'accordion est fermé sans confirmation.
- **API Locale Simulée** :
    - Endpoint `/api/form` qui fournit des données de lycée, classe et type de bac aléatoires à chaque chargement de page.
    - Endpoint `/api/lycees` qui fournit la liste complète des lycées pour l'autocomplete.
- **Validation du Formulaire** : Bouton de confirmation global désactivé tant que les choix requis ne sont pas faits, avec un placement adapté à la responsivité (desktop vs mobile/tablette).

---

## 🛠️ Stack Technique

- **Framework Frontend** : [Nuxt 4](https://nuxt.com/) (Vue 3, Typescript, Vite/Nitro)
- **Styling** : [Tailwind CSS v4](https://tailwindcss.com/) (via `@tailwindcss/vite` plugin)
- **Langage** : [TypeScript](https://www.typescriptlang.org/)
- **Icones** : [@nuxt/icon](https://icon.nuxtjs.org/)
- **Qualité de Code** : [@nuxt/eslint](https://eslint.nuxtjs.org/)
- **Outil de Breakpoints** : [@vueuse/core](https://vueuse.org/)
- **Gestionnaire de Paquets** : `npm`

---

## 📦 Conventions de Projet

- **Composants préfixés `EM`** : Tous les composants personnalisés sont préfixés par `EM` (ex: `EMButton`, `EMAccordion`) pour éviter les conflits et identifier les éléments du "design system" Edumapper.
- **Conventional Commits** : L'historique Git suit la spécification [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) (`feat:`, `fix:`, `chore:`, `style:`, `docs:`).
- **Structure des Fichiers** : Organisation modulaire des composants sous `app/components` et des routes API sous `server/api`.

---

## 🚀 Installation & Lancement

1.  **Cloner le dépôt :**
    ```bash
    git clone https://github.com/LeoBourret/Edumapper-test.git
    cd Edumapper-test
    ```
2.  **Installer les dépendances :**
    ```bash
    npm install
    ```
3.  **Lancer le serveur de développement :**
    ```bash
    npm run dev
    ```
    L'application sera accessible sur `http://localhost:3000`.

---

## 💡 Remarque

- **Intégration de la Police "DM Sans"** : Malgré l'utilisation du module `@nuxt/fonts`, l'intégration de la police "DM Sans" via la configuration de Tailwind CSS v4 n'a pas pu être finalisée dans le temps imparti. Ayant principalement travaillé avec Tailwind CSS v3, l'adaptation à la nouvelle méthode de configuration des fonts en v4 a présenté des difficultés, et ce point a été mis de côté pour privilégier la livraison des fonctionnalités.

---

J'espère que ce rendu répond aux attentes et démontre ma capacité à travailler sur un projet moderne et structuré.
