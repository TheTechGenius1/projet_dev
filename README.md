# VoteNow — Application de vote en ligne sécurisée

## 📋 Objectif
Une application web complète pour organiser des élections en ligne avec gestion des candidats, vote sécurisé, annulation de vote et résultats en temps réel. Application **100% statique** (HTML/CSS/JS) avec stockage local.

---

## ✨ Fonctionnalités principales

### 🗳️ Espace Votant
- **Inscription sécurisée** : Saisie du prénom, nom et INE (numéro d'identification)
- **Identifiant de vote unique** : Généré automatiquement au format `VOT-XXXXXXXXX-XXXXXX`
- **Vote sécurisé** : Sélection d'un candidat avec photo, nom et slogan
- **Annulation du vote** : Possibilité d'annuler dans les **2 minutes** après le vote
- **Visualisation des candidats** : Affichage des photos, slogans et projets PDF
- **Consultation des résultats** : Graphiques en temps réel avec pourcentages

### 👨‍💼 Espace Administration
- **Connexion sécurisée** : Authentification avec identifiant + code
- **Gestion des candidats** :
  - ➕ Ajouter un candidat (nom, slogan, photo, projet PDF)
  - ✏️ **Modifier les informations** (photo, PDF, nom, slogan)
  - 🗑️ Supprimer un candidat
- **Contrôle des votes en direct** :
  - 📊 Compteurs : Total votes, électeurs inscrits, taux de participation
  - 📈 Graphiques actualisés chaque 2 secondes
  - Votes par candidat avec barres proportionnelles
- **Gestion des votes** :
  - 🔐 Ouvrir/Fermer les votes
  - 🗑️ Réinitialiser tous les votes
  - ⬇️ **Exporter les résultats en CSV**
- **Session persistante** : Admin reste connecté jusqu'à déconnexion

### 📄 Section Candidats
- Affichage complet de tous les candidats
- Consultation des projets PDF
- Téléchargement des projets

### 📊 Section Résultats
- Tableau des voix par candidat avec pourcentages
- Graphique en barres proportionnelles
- Annonce du gagnant 🏆
- Actualisation en temps réel

---

## 🔒 Sécurité

### Front-end
- **Stockage local** : Données conservées dans `localStorage` du navigateur
- **INE unique** : Chaque électeur ne peut voter qu'une fois (vérification INE)
- **Identifiants de vote** : Générés aléatoirement pour chaque votant
- **Annulation limitée** : 2 minutes pour changer d'avis
- **Sessions admin** : Identifiant + code (max 3 admins par défaut)

### ⚠️ Limitations (à savoir)
- **Pas de backend** : Les données restent dans le navigateur
- **Pas de chiffrement** : Ne pas utiliser pour élection réelle sans backend
- **Pas de base de données** : Les données disparaissent après effacement du cache
- **Admin côté client** : Les mots de passe sont visibles dans le code (démo uniquement)

### 🔐 Recommandations pour production
1. Implémenter un **backend** (Node.js, Python, PHP, etc.)
2. Utiliser une **base de données sécurisée** (PostgreSQL, MongoDB)
3. Implémenter un **système d'authentification robuste** (JWT, OAuth2)
4. Utiliser **HTTPS** pour les connexions
5. Ajouter **audit logging** de tous les votes
6. Implémenter la **vérification des électeurs** (API externe)

---

## 📦 Installation

### Prérequis
- Navigateur moderne (Chrome, Firefox, Safari, Edge)
- Éditeur de texte (VS Code, Sublime Text, etc.)

### Étapes
1. **Cloner le projet**
   ```bash
   git clone https://github.com/votre-repo/votenow.git
   cd votenow
   ```

2. **Ouvrir dans un navigateur**
   ```
   Ouvrir le fichier : /html/index.html
   ```

3. **(Optionnel) Serveur local**
   ```bash
   # Avec Python 3
   python -m http.server 8000
   
   # Avec Python 2
   python -m SimpleHTTPServer 8000
   
   # Avec Node.js (http-server)
   npx http-server
   ```
   Puis accéder à : `http://localhost:8000`

---

## 🎮 Utilisation

### Pour les votants
1. Aller à l'onglet **🗳️ Vote**
2. Cliquer sur **"S'inscrire pour voter"**
3. Remplir le formulaire (prénom, nom, INE)
4. L'identifiant de vote est généré automatiquement
5. Sélectionner un candidat et voter
6. **Optionnel** : Annuler le vote dans les 2 minutes suivantes
7. Consulter les résultats dans l'onglet **📊 Résultats**

### Pour l'administrateur
1. Aller à l'onglet **👨‍💼 Administration**
2. Se connecter avec identifiant + code (voir configuration)
3. **Gérer les candidats** :
   - Ajouter : Remplir le formulaire en haut
   - Modifier : Cliquer sur ✏️
   - Supprimer : Cliquer sur 🗑️
4. **Contrôler les votes** :
   - Voir les statistiques en direct
   - Ouvrir/Fermer les votes
   - Exporter les résultats
   - Réinitialiser si nécessaire

---

## ⚙️ Configuration

### Modifier les comptes admin
Dans le fichier `/jss/ap.js`, ligne ~18 :

```javascript
const ADMINS = [
  { id: "admin01", code: "code123" },
  { id: "admin02", code: "code456" },
  { id: "admin03", code: "code789" }
];
```

**Ajouter/Modifier les admins :**
```javascript
const ADMINS = [
  { id: "madiop", code: "madiop2024" },
  { id: "directeur", code: "directeur123" },
  { id: "observateur", code: "obs456" }
];
```

### Modifier le délai d'annulation de vote
Dans `/jss/ap.js`, ligne ~520 :

```javascript
const CANCEL_WINDOW = 2 * 60 * 1000; // 2 minutes en millisecondes
```

Pour 5 minutes :
```javascript
const CANCEL_WINDOW = 5 * 60 * 1000;
```

### Modifier les candidats par défaut
Dans `/jss/ap.js`, ligne ~680 :

```javascript
setCandidates([
  { id: cryptoRandomId(), name: 'Awa Diop', slogan: 'Ensemble, on avance!' },
  { id: cryptoRandomId(), name: 'Moussa Ndiaye', slogan: 'Transparence et action' },
  { id: cryptoRandomId(), name: 'Sokhna Fall', slogan: 'Proximité et efficacité' }
]);
```

---

## 📁 Structure du projet

```
votenow/
├── html/
│   ├── index.html              # Page principale (onglets)
│   ├── home.html               # (Optionnel) Accueil avec tutoriel
│   ├── tutorial.html           # (Optionnel) Tutoriel vidéo
│   └── terms.html              # (Optionnel) Conditions d'utilisation
├── css/
│   ├── style.css               # Styles globaux
│   ├── responsive.css          # Media queries (responsive design)
│   └── components.css          # Composants réutilisables
├── jss/
│   ├── ap.js                   # Logique principale (850+ lignes)
│   ├── tutorial.js             # (Optionnel) Gestion tutoriel
│   └── terms.js                # (Optionnel) Conditions d'utilisation
├── assets/
│   ├── icons/                  # Icônes
│   ├── images/                 # Images
│   └── avatar.png              # Photo par défaut
├── videos/
│   └── tutorial.mp4            # Vidéo de tutoriel
├── README.md                   # Ce fichier
└── package.json                # (Optionnel) Métadonnées du projet
```

---

## 🌐 Responsive Design

L'application s'adapte à tous les écrans :

| Écran | Résolution | Adaptation |
|-------|-----------|-----------|
| 📱 Mobile | 320px - 480px | Layout empilé, texte ajusté |
| 📱 Petit mobile | 481px - 640px | Grille 1 colonne |
| 📱 Tablette | 641px - 1024px | Grille 2 colonnes |
| 💻 Desktop | 1025px+ | Grille 3 colonnes |
| 🖥️ Ultra-large | 1600px+ | Layout optimisé |

**Testez sur** :
- Chrome DevTools (F12)
- iPhone/Android simulateurs
- Navigateurs réels

---

## 🎨 Customisation

### Couleurs
Modifier les variables CSS dans `style.css` :

```css
:root {
  --primary: #2563eb;        /* Bleu principal */
  --primary-dark: #1e40af;   /* Bleu foncé */
  --primary-light: #dbeafe;  /* Bleu clair */
  --danger: #dc2626;         /* Rouge (danger) */
  --success: #16a34a;        /* Vert (succès) */
  --warning: #f59e0b;        /* Orange (alerte) */
  --text: #1f2937;           /* Texte noir */
  --text-light: #6b7280;     /* Texte gris */
  --border: #e5e7eb;         /* Bordures */
  --bg: #f9fafb;             /* Fond */
}
```

### Police de caractères
```css
body {
  font-family: 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
}
```

### Thème sombre
Ajouter un commutateur et utiliser :
```css
@media (prefers-color-scheme: dark) {
  :root {
    --bg: #111827;
    --text: #f3f4f6;
  }
}
```

---

## 📊 Export des données

### Format CSV exporté
```
Candidat,Votes,Pourcentage
"Awa Diop",45,60.00%
"Moussa Ndiaye",20,26.67%
"Sokhna Fall",10,13.33%

Résumé
Total des votes,75
Total des électeurs inscrits,100
Taux de participation,75.00%
Date d'export,"6 décembre 2025 14:30:00"
```

### Utiliser les données
1. Cliquer sur **⬇️ Exporter les résultats (CSV)**
2. Ouvrir dans Excel/LibreOffice/Google Sheets
3. Analyser, imprimer, archiver

---

## 🐛 Dépannage

### Les données disparaissent après fermeture
**Cause** : Cache/LocalStorage supprimé
**Solution** : Les données sont dans le navigateur, pas dans le cloud

### Impossible de voter deux fois
**Cause** : Vérification par INE
**Solution** : Utiliser un INE différent pour une autre inscription

### Le bouton "Annuler" n'apparaît pas
**Cause** : Plus de 2 minutes écoulées
**Solution** : C'est voulu ! Attendre le prochain vote ou contacter l'admin

### Admin ne peut pas se connecter
**Cause** : Identifiant/code incorrect
**Solution** : Vérifier la configuration dans `ap.js`

### Les modifications de candidat ne s'affichent pas
**Cause** : Rafraîchissement de page manquant
**Solution** : Actualiser la page (F5 ou Ctrl+R)

---

## 📱 Compatibilité navigateurs

| Navigateur | Version | Support |
|-----------|---------|---------|
| Chrome | 90+ | ✅ Complet |
| Firefox | 88+ | ✅ Complet |
| Safari | 14+ | ✅ Complet |
| Edge | 90+ | ✅ Complet |
| IE 11 | - | ❌ Non supporté |

---

## 📝 Conditions d'utilisation (Résumé)

- ✅ Utilisation gratuite et non commerciale
- ✅ Modification du code autorisée
- ✅ Redistribution avec attribution
- ❌ Pas de garantie (as-is)
- ❌ Pas de responsabilité en cas de perte de données
- ⚠️ Usage légal uniquement

**Pour les conditions complètes** : Consulter `terms.html`

---

## 🤝 Contribution

Les contributions sont bienvenues !

1. **Fork** le projet
2. **Créer une branche** : `git checkout -b feature/nouvelle-fonction`
3. **Commit** : `git commit -m "Ajout nouvelle fonction"`
4. **Push** : `git push origin feature/nouvelle-fonction`
5. **Pull Request** : Créer une PR

---

## 📧 Support

- **Issues** : Signaler un bug
- **Discussions** : Proposer des améliorations
- **Email** : contact@votenow.local

---

## 📄 Licence

MIT License - Voir `LICENSE.md`

---

## 🎓 Crédits

- **Développeur** : Madiop Guèye
- **Framework** : HTML5 / CSS3 / Vanilla JavaScript
- **Icônes** : Unicode Emojis
- **Inspiré par** : Démocratie numérique

---

## 🚀 Feuille de route

### ✅ V1.0 (Actuelle)
- [x] Vote sécurisé avec INE
- [x] Annulation de vote (2 minutes)
- [x] Gestion des candidats
- [x] Résultats en temps réel
- [x] Interface admin
- [x] Export CSV
- [x] Responsive design

### 🔄 V1.1 (Prochaine)
- [ ] Page d'accueil avec tutoriel
- [ ] Vidéo de démonstration
- [ ] Conditions d'utilisation interactive
- [ ] Thème sombre automatique
- [ ] Statistiques avancées

### 🔮 V2.0 (Futur)
- [ ] Backend Node.js + PostgreSQL
- [ ] Authentification OAuth2
- [ ] Système de cache
- [ ] API REST
- [ ] Analytics avancées
- [ ] Support multilingue

---

## ⭐ Merci !

Si ce projet vous a été utile, mettez une ⭐ sur GitHub !

---

**Dernière mise à jour** : 6 décembre 2025  
**Version** : 1.0.0  
**Auteur** : Madiop Guèye# projet_dev
