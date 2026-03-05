# Cahier des Charges — Application de Gestion de Budget Personnel

**Projet scolaire de groupe**
**Technologie : .NET MAUI**
**Date :** Mars 2026

---

## 1. Présentation du Projet

### 1.1 Contexte

Dans le cadre d'un projet scolaire de groupe, nous développons une application mobile de gestion de budget personnel destinée aux étudiants et jeunes adultes. Beaucoup de personnes dans cette tranche d'âge n'ont pas de vue claire sur leurs dépenses mensuelles, ce qui peut mener à des difficultés financières. L'application vise à rendre la gestion financière simple, visuelle et accessible.

### 1.2 Objectifs

- Permettre aux utilisateurs de suivre leurs dépenses au quotidien
- Catégoriser les dépenses pour identifier les habitudes financières
- Visualiser les données sous forme de graphiques compréhensibles
- Définir et suivre des objectifs d'épargne mensuels
- Démontrer les compétences de l'équipe en développement .NET MAUI

### 1.3 Public Cible

- Étudiants universitaires et collégiaux
- Jeunes adultes (18–30 ans) débutant dans la gestion financière personnelle

---

## 2. Périmètre du Projet

### 2.1 Ce qui est inclus (In Scope)

- Création et gestion d'un compte utilisateur local
- Ajout, modification et suppression de dépenses
- Catégorisation des dépenses (alimentation, transport, loisirs, etc.)
- Tableau de bord avec résumé mensuel
- Graphiques de visualisation des dépenses
- Définition d'objectifs d'épargne mensuels
- Interface utilisateur simple et intuitive

### 2.2 Ce qui est exclu (Out of Scope)

- Connexion bancaire ou import automatique de transactions
- Fonctionnalités multi-utilisateurs ou partage de budget
- Notifications push avancées
- Synchronisation cloud entre appareils

---

## 3. Fonctionnalités

### 3.1 Gestion du Compte Utilisateur

| ID | Fonctionnalité | Priorité |
|----|---------------|----------|
| F01 | Créer un compte (nom, email, mot de passe) | Haute |
| F02 | Se connecter / se déconnecter | Haute |
| F03 | Modifier les informations du profil | Moyenne |

### 3.2 Gestion des Dépenses

| ID | Fonctionnalité | Priorité |
|----|---------------|----------|
| F04 | Ajouter une dépense (montant, date, catégorie, description) | Haute |
| F05 | Modifier une dépense existante | Haute |
| F06 | Supprimer une dépense | Haute |
| F07 | Consulter la liste des dépenses (filtrable par mois) | Haute |

### 3.3 Catégories

| ID | Fonctionnalité | Priorité |
|----|---------------|----------|
| F08 | Catégories prédéfinies (alimentation, logement, transport, loisirs, santé, autre) | Haute |
| F09 | Ajouter une catégorie personnalisée | Basse |

### 3.4 Tableau de Bord

| ID | Fonctionnalité | Priorité |
|----|---------------|----------|
| F10 | Afficher le total des dépenses du mois en cours | Haute |
| F11 | Afficher le solde restant par rapport au budget défini | Haute |
| F12 | Graphique en camembert des dépenses par catégorie | Moyenne |
| F13 | Graphique en barres des dépenses par semaine ou par mois | Moyenne |

### 3.5 Objectifs d'Épargne

| ID | Fonctionnalité | Priorité |
|----|---------------|----------|
| F14 | Définir un budget mensuel total | Haute |
| F15 | Définir un objectif d'épargne mensuel | Moyenne |
| F16 | Afficher la progression vers l'objectif d'épargne | Moyenne |

---

## 4. Architecture Technique

### 4.1 Technologie

- **Framework :** .NET MAUI (Multi-platform App UI)
- **Langage :** C#
- **Stockage local :** SQLite (via SQLite-net-pcl)
- **Graphiques :** LiveCharts2 ou Microcharts (bibliothèque MAUI compatible)
- **Pattern :** MVVM (Model-View-ViewModel)

### 4.2 Structure du Projet

```
BudgetApp/
├── Models/
│   ├── User.cs
│   ├── Expense.cs
│   ├── Category.cs
│   └── SavingsGoal.cs
├── ViewModels/
│   ├── LoginViewModel.cs
│   ├── DashboardViewModel.cs
│   ├── ExpenseViewModel.cs
│   └── GoalViewModel.cs
├── Views/
│   ├── LoginPage.xaml
│   ├── DashboardPage.xaml
│   ├── ExpenseListPage.xaml
│   ├── AddExpensePage.xaml
│   └── GoalsPage.xaml
├── Services/
│   ├── DatabaseService.cs
│   └── AuthService.cs
└── Resources/
    └── Styles/
```

### 4.3 Modèle de Données Simplifié

**User**
- Id, Nom, Email, MotDePasse (hashé), BudgetMensuel

**Expense**
- Id, UserId, Montant, Date, Description, CategoryId

**Category**
- Id, Nom, Icone, Couleur

**SavingsGoal**
- Id, UserId, Mois, Annee, MontantCible, MontantEpargne

---

## 5. Interface Utilisateur

### 5.1 Navigation Principale

L'application comportera 4 écrans principaux accessibles via une barre de navigation :

1. **Tableau de bord** — vue d'ensemble du mois
2. **Dépenses** — liste et ajout de dépenses
3. **Graphiques** — visualisation des données
4. **Objectifs** — suivi de l'épargne

### 5.2 Critères d'ergonomie

- Interface claire et minimaliste adaptée aux mobiles
- Thème visuel cohérent (couleurs, typographie)
- Formulaires simples avec validation des saisies
- Messages d'erreur compréhensibles

---

## 6. Contraintes

### 6.1 Contraintes Techniques

- L'application doit fonctionner sur Android (iOS en bonus si le temps le permet)
- Les données sont stockées localement sur l'appareil (pas de serveur requis)
- Compatibilité avec .NET 8 / MAUI

### 6.2 Contraintes de Projet

- Projet réalisé en groupe dans le cadre scolaire
- Délais à respecter selon le calendrier du cours
- Code versionné sur un dépôt Git partagé (GitHub/GitLab)

---

## 7. Répartition des Tâches (Exemple)

| Membre | Responsabilités |
|--------|----------------|
| Membre 1 | Modèles de données, base de données SQLite |
| Membre 2 | Écrans Login, Profil et navigation |
| Membre 3 | Tableau de bord et graphiques |
| Membre 4 | Écran dépenses (ajout, liste, modification) |
| Membre 5 | Objectifs d'épargne et tests |

---

## 8. Livrables

- Code source complet sur dépôt Git
- Application fonctionnelle sur Android
- Ce cahier des charges
- Présentation du projet (diaporama ou démo)

---

*Document rédigé dans le cadre d'un projet scolaire — Version 1.0*
