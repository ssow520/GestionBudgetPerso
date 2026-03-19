# Cahier des Charges — BudgetMaster
## Application de Gestion de Budget Personnel

**Projet :** Scolaire de groupe — Techniques de l'informatique  
**Technologie :** .NET MAUI (C#)  
**Équipe :** Souleymane Sow, Ines Rbah 
**Établissement :** Collège LaSalle, Montréal  
**Date :** Mars 2026 | **Version :** 2.0 | **Deadline :** 19 avril 2026

---

## Table des matières

1. [Présentation du Projet](#1-présentation-du-projet)
2. [Périmètre du Projet](#2-périmètre-du-projet)
3. [Fonctionnalités](#3-fonctionnalités)
4. [Principes de Conception](#4-principes-de-conception)
5. [Patrons de Conception](#5-patrons-de-conception)
6. [Architecture Technique](#6-architecture-technique)
7. [Interface Utilisateur](#7-interface-utilisateur)
8. [Contraintes](#8-contraintes)
9. [Livrables](#9-livrables)
10. [Gestion de Projet](#10-gestion-de-projet)

---

## 1. Présentation du Projet

### 1.1 Contexte

Dans le cadre d'un projet scolaire de groupe, nous développons **BudgetMaster**, une application mobile de gestion de budget personnel destinée aux étudiants et jeunes adultes. Beaucoup de personnes dans cette tranche d'âge n'ont pas de vue claire sur leurs dépenses mensuelles, ce qui peut mener à des difficultés financières. L'application vise à rendre la gestion financière simple, visuelle et accessible.

### 1.2 Objectifs

- Permettre aux utilisateurs de suivre leurs dépenses au quotidien
- Catégoriser les dépenses pour identifier les habitudes financières
- Visualiser les données sous forme de graphiques compréhensibles
- Définir et suivre des objectifs d'épargne mensuels
- Démontrer les compétences de l'équipe en développement .NET MAUI
- Appliquer les principes de conception logicielle et les patrons de conception

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
- Graphiques de visualisation des dépenses (camembert, barres)
- Définition d'objectifs d'épargne mensuels avec suivi de progression
- Interface utilisateur simple, intuitive et accessible
- Application des patrons de conception MVVM, Repository, Observer, Singleton, Factory, Command, Strategy

### 2.2 Ce qui est exclu (Out of Scope)

- Connexion bancaire ou import automatique de transactions
- Fonctionnalités multi-utilisateurs ou partage de budget
- Notifications push avancées
- Synchronisation cloud entre appareils

---

## 3. Fonctionnalités

### 3.1 Gestion du Compte Utilisateur

| ID  | Fonctionnalité                                          | Priorité |
|-----|---------------------------------------------------------|----------|
| F01 | Créer un compte (nom, email, mot de passe)              | Haute    |
| F02 | Se connecter / se déconnecter                           | Haute    |
| F03 | Modifier les informations du profil                     | Moyenne  |
| F04 | Validation des saisies avec messages d'erreur clairs    | Haute    |

### 3.2 Gestion des Dépenses

| ID  | Fonctionnalité                                                      | Priorité |
|-----|---------------------------------------------------------------------|----------|
| F05 | Ajouter une dépense (montant, date, catégorie, description)         | Haute    |
| F06 | Modifier une dépense existante                                      | Haute    |
| F07 | Supprimer une dépense (confirmation requise)                        | Haute    |
| F08 | Consulter la liste des dépenses (filtrable par mois)                | Haute    |
| F09 | Recherche de dépenses par mot-clé                                   | Basse    |

### 3.3 Catégories

| ID  | Fonctionnalité                                                                          | Priorité |
|-----|-----------------------------------------------------------------------------------------|----------|
| F10 | Catégories prédéfinies (alimentation, logement, transport, loisirs, santé, autre)       | Haute    |
| F11 | Ajouter une catégorie personnalisée (nom, icône, couleur)                               | Basse    |
| F12 | Supprimer une catégorie personnalisée                                                   | Basse    |

### 3.4 Tableau de Bord

| ID  | Fonctionnalité                                                      | Priorité |
|-----|---------------------------------------------------------------------|----------|
| F13 | Afficher le total des dépenses du mois en cours                     | Haute    |
| F14 | Afficher le solde restant par rapport au budget défini              | Haute    |
| F15 | Graphique en camembert des dépenses par catégorie                   | Moyenne  |
| F16 | Graphique en barres des dépenses par semaine ou par mois            | Moyenne  |
| F17 | Résumé comparatif mois précédent vs mois actuel                     | Basse    |

### 3.5 Objectifs d'Épargne

| ID  | Fonctionnalité                                                          | Priorité |
|-----|-------------------------------------------------------------------------|----------|
| F18 | Définir un budget mensuel total                                         | Haute    |
| F19 | Définir un objectif d'épargne mensuel                                   | Moyenne  |
| F20 | Afficher la progression vers l'objectif d'épargne (barre de progression)| Moyenne  |
| F21 | Alerte visuelle si le budget est dépassé (> 90%)                        | Moyenne  |

---

## 4. Principes de Conception

L'application respecte les principes fondamentaux du génie logiciel afin de garantir un code maintenable, évolutif et robuste.

### 4.1 Principes SOLID

#### S — Single Responsibility Principle (SRP)
Chaque classe a une seule responsabilité bien définie :
- `DatabaseService` → uniquement la gestion de la connexion SQLite
- `AuthService` → uniquement l'authentification et la session
- `ExpenseViewModel` → uniquement la logique de présentation des dépenses
- `ExpenseRepository` → uniquement l'accès aux données des dépenses

#### O — Open/Closed Principle (OCP)
Les classes sont ouvertes à l'extension mais fermées à la modification. L'utilisation d'interfaces (`IRepository<T>`, `IAuthService`) permet d'ajouter de nouveaux comportements sans toucher au code existant. Par exemple, on peut ajouter un `CloudRepository` sans modifier `ExpenseViewModel`.

#### L — Liskov Substitution Principle (LSP)
Toutes les implémentations d'une interface sont interchangeables. `SqliteExpenseRepository` et un futur `CloudExpenseRepository` implémentent tous deux `IExpenseRepository` et peuvent être utilisés de façon transparente.

#### I — Interface Segregation Principle (ISP)
Les interfaces sont petites et spécifiques. On distingue `IExpenseRepository`, `ICategoryRepository` et `ISavingsGoalRepository` plutôt qu'une seule grande interface avec toutes les méthodes.

#### D — Dependency Inversion Principle (DIP)
Les modules de haut niveau (ViewModels) dépendent d'abstractions (interfaces), pas d'implémentations concrètes. L'injection de dépendances est configurée dans `MauiProgram.cs` via le conteneur DI de .NET MAUI.

### 4.2 Autres Principes Appliqués

#### DRY — Don't Repeat Yourself
Aucune logique dupliquée. Les opérations CRUD communes sont factorisées dans une classe générique `BaseRepository<T>`. Les styles XAML sont définis une seule fois dans `ResourceDictionary`.

#### KISS — Keep It Simple, Stupid
Interface minimaliste et directe. Chaque écran a un rôle clair. Les formulaires sont simples avec un minimum de champs requis.

#### YAGNI — You Aren't Gonna Need It
Seules les fonctionnalités définies dans ce cahier des charges sont implémentées. Pas de suringénierie ni de fonctionnalités hypothétiques futures.

#### Séparation des préoccupations (SoC)
L'architecture MVVM assure une séparation stricte entre :
- La couche de données (Models + Repositories)
- La couche de présentation logique (ViewModels)
- La couche visuelle (Views XAML)

---

## 5. Patrons de Conception

Les patrons de conception suivants sont appliqués pour résoudre des problèmes récurrents de façon éprouvée.

### 5.1 Patrons Architecturaux

#### MVVM — Model-View-ViewModel *(patron principal)*
Patron central de l'application, recommandé par Microsoft pour .NET MAUI.

| Couche    | Rôle                                                                 |
|-----------|----------------------------------------------------------------------|
| Model     | Classes de données pures (User, Expense, Category, SavingsGoal)      |
| ViewModel | Logique de présentation, commandes `ICommand`, `ObservableProperty`  |
| View      | Fichiers XAML liés aux ViewModels via DataBinding                    |

**Avantage :** les ViewModels sont testables indépendamment de l'UI.

#### Repository Pattern *(accès aux données)*
Abstraction de la couche d'accès aux données SQLite derrière des interfaces.

| Interface               | Implémentation               |
|-------------------------|------------------------------|
| `IExpenseRepository`    | `SqliteExpenseRepository`    |
| `ICategoryRepository`   | `SqliteCategoryRepository`   |
| `ISavingsGoalRepository`| `SqliteSavingsGoalRepository`|
| `IUserRepository`       | `SqliteUserRepository`       |

**Avantage :** isoler les ViewModels de la technologie de persistance (SQLite aujourd'hui, API REST demain).

### 5.2 Patrons de Création

#### Singleton
Utilisé pour `DatabaseService` afin de garantir une seule connexion SQLite partagée dans toute l'application.

```csharp
// MauiProgram.cs
builder.Services.AddSingleton<DatabaseService>();
```

- Évite les conflits d'accès concurrentiel à la base de données
- Garantit que toutes les opérations partagent la même `SQLiteAsyncConnection`

#### Factory Method
Utilisé pour la création des catégories prédéfinies via `CategoryFactory`.

```csharp
public static class CategoryFactory
{
    public static List<Category> CreateDefaultCategories() { ... }
}
```

- Centralise la logique de création des catégories système
- Respecte OCP : ajouter une catégorie ne modifie pas les consommateurs

### 5.3 Patrons Comportementaux

#### Observer — `INotifyPropertyChanged`
Implémenté via **CommunityToolkit.Mvvm** avec `[ObservableProperty]` et `[RelayCommand]`.

```csharp
[ObservableProperty]
private decimal totalDepenses;
```

- Les Views (XAML) s'abonnent automatiquement aux changements des ViewModels via le DataBinding
- Élimine le couplage direct entre View et ViewModel

#### Command Pattern — `ICommand`
Toutes les actions utilisateur (boutons, swipes) sont encapsulées dans des commandes.

```csharp
[RelayCommand]
private async Task AddExpenseAsync() { ... }

[RelayCommand]
private async Task DeleteExpenseAsync(int id) { ... }
```

**Avantage :** les commandes peuvent être désactivées (`CanExecute`) selon l'état de l'application.

#### Strategy
Utilisé pour les algorithmes de filtrage et de tri des dépenses.

```csharp
public interface IExpenseFilter
{
    IEnumerable<Expense> Apply(IEnumerable<Expense> expenses);
}

public class MonthFilter : IExpenseFilter { ... }
public class CategoryFilter : IExpenseFilter { ... }
public class DateRangeFilter : IExpenseFilter { ... }
```

`ExpenseListViewModel` utilise un `IExpenseFilter` actif sans connaître l'implémentation concrète.

### 5.4 Récapitulatif des Patrons

| Patron        | Catégorie      | Classe(s) concernée(s)   | Rôle                          |
|---------------|----------------|--------------------------|-------------------------------|
| MVVM          | Architectural  | Toute l'application      | Séparation UI / logique       |
| Repository    | Architectural  | `*Repository`            | Abstraction accès données     |
| Singleton     | Création       | `DatabaseService`        | Instance unique SQLite        |
| Factory Method| Création       | `CategoryFactory`        | Création catégories défaut    |
| Observer      | Comportemental | Tous les ViewModels      | Binding UI automatique        |
| Command       | Comportemental | Tous les ViewModels      | Actions utilisateur           |
| Strategy      | Comportemental | `ExpenseListViewModel`   | Filtres interchangeables      |

---

## 6. Architecture Technique

### 6.1 Technologie

| Composant       | Détail                          |
|-----------------|---------------------------------|
| Framework       | .NET MAUI (.NET 8)              |
| Langage         | C# 12                           |
| Stockage local  | SQLite via `SQLite-net-pcl`     |
| Graphiques      | LiveCharts2 (MAUI compatible)   |
| MVVM Toolkit    | CommunityToolkit.Mvvm           |
| Hachage         | BCrypt.Net-Next (mots de passe) |
| Pattern         | MVVM + Repository + DI          |
| Versionnement   | Git / GitHub                    |

### 6.2 Structure du Projet

```
BudgetMaster/
├── Models/
│   ├── User.cs
│   ├── Expense.cs
│   ├── Category.cs
│   └── SavingsGoal.cs
├── Repositories/
│   ├── Interfaces/
│   │   ├── IUserRepository.cs
│   │   ├── IExpenseRepository.cs
│   │   ├── ICategoryRepository.cs
│   │   └── ISavingsGoalRepository.cs
│   ├── BaseRepository.cs
│   ├── UserRepository.cs
│   ├── ExpenseRepository.cs
│   ├── CategoryRepository.cs
│   └── SavingsGoalRepository.cs
├── ViewModels/
│   ├── LoginViewModel.cs
│   ├── RegisterViewModel.cs
│   ├── DashboardViewModel.cs
│   ├── ExpenseListViewModel.cs
│   ├── AddEditExpenseViewModel.cs
│   ├── ChartsViewModel.cs
│   ├── GoalsViewModel.cs
│   └── ProfileViewModel.cs
├── Views/
│   ├── LoginPage.xaml
│   ├── RegisterPage.xaml
│   ├── DashboardPage.xaml
│   ├── ExpenseListPage.xaml
│   ├── AddEditExpensePage.xaml
│   ├── ChartsPage.xaml
│   ├── GoalsPage.xaml
│   └── ProfilePage.xaml
├── Services/
│   ├── DatabaseService.cs       ← Singleton
│   └── AuthService.cs
├── Factories/
│   └── CategoryFactory.cs       ← Factory Method
├── Filters/
│   ├── IExpenseFilter.cs        ← Strategy (interface)
│   ├── MonthFilter.cs
│   ├── CategoryFilter.cs
│   └── DateRangeFilter.cs
├── Resources/
│   └── Styles/
│       ├── Colors.xaml
│       └── Styles.xaml
└── MauiProgram.cs               ← Configuration DI
```

### 6.3 Modèle de Données

#### User

| Champ           | Type              | Description                             |
|-----------------|-------------------|-----------------------------------------|
| Id              | int (PK)          | Clé primaire auto-incrémentée           |
| Nom             | string            | Nom complet de l'utilisateur            |
| Email           | string (unique)   | Adresse email — identifiant de connexion|
| MotDePasseHash  | string            | Mot de passe haché BCrypt               |
| BudgetMensuel   | decimal           | Budget total mensuel défini             |
| DateCreation    | DateTime          | Date de création du compte              |

#### Expense

| Champ       | Type      | Description                          |
|-------------|-----------|--------------------------------------|
| Id          | int (PK)  | Clé primaire auto-incrémentée        |
| UserId      | int (FK)  | Référence vers User                  |
| CategoryId  | int (FK)  | Référence vers Category              |
| Montant     | decimal   | Montant de la dépense (positif)      |
| Date        | DateTime  | Date de la dépense                   |
| Description | string    | Note ou description libre            |
| DateCreation| DateTime  | Date d'enregistrement                |

#### Category

| Champ       | Type             | Description                                       |
|-------------|------------------|---------------------------------------------------|
| Id          | int (PK)         | Clé primaire auto-incrémentée                     |
| Nom         | string           | Nom de la catégorie                               |
| Icone       | string           | Nom de l'icône (ex: `food_icon`)                  |
| Couleur     | string           | Code couleur hex (ex: `#4CAF50`)                  |
| EstSysteme  | bool             | `true` si catégorie prédéfinie (non supprimable)  |
| UserId      | int? (FK nullable)| `null` si système, sinon référence vers User      |

#### SavingsGoal

| Champ          | Type      | Description                              |
|----------------|-----------|------------------------------------------|
| Id             | int (PK)  | Clé primaire auto-incrémentée            |
| UserId         | int (FK)  | Référence vers User                      |
| Mois           | int       | Mois concerné (1–12)                     |
| Annee          | int       | Année concernée                          |
| MontantCible   | decimal   | Montant d'épargne visé                   |
| MontantEpargne | decimal   | Montant épargné calculé automatiquement  |

---

## 7. Interface Utilisateur

### 7.1 Navigation Principale

L'application comporte 5 écrans principaux accessibles via une barre de navigation Shell :

1. **Connexion / Inscription** — écran d'accueil avant authentification
2. **Tableau de bord** — vue d'ensemble du mois en cours
3. **Dépenses** — liste, ajout et modification des dépenses
4. **Graphiques** — visualisation des données financières
5. **Objectifs** — suivi et définition des objectifs d'épargne

### 7.2 Critères d'Ergonomie et d'Accessibilité

- Interface claire et minimaliste adaptée aux mobiles (Material Design guidelines)
- Thème visuel cohérent : couleurs, typographie, espacements constants
- Formulaires simples avec validation en temps réel et messages d'erreur compréhensibles
- Confirmation requise avant toute action destructrice (suppression d'une dépense)
- Support du mode sombre et clair (`AppThemeBinding` dans XAML)
- Taille de police minimum 14sp pour la lisibilité sur mobile
- Contrastes respectant les normes WCAG AA (ratio >= 4.5:1)

### 7.3 Écrans Détaillés

| Écran               | Contenu principal                                                  |
|---------------------|--------------------------------------------------------------------|
| `LoginPage`         | Formulaire email / mot de passe + lien inscription                 |
| `RegisterPage`      | Formulaire création de compte avec validation                      |
| `DashboardPage`     | Résumé du mois, total dépenses, solde, alerte budget               |
| `ExpenseListPage`   | Liste filtrée + bouton ajout + swipe suppression                   |
| `AddEditExpensePage`| Formulaire ajout/modification (réutilisable pour les deux cas)     |
| `ChartsPage`        | Camembert par catégorie + barres par période                       |
| `GoalsPage`         | Budget mensuel + objectif épargne + barre de progression           |
| `ProfilePage`       | Modification des informations personnelles                         |

---

## 8. Contraintes

### 8.1 Contraintes Techniques

- L'application doit fonctionner sur Android (API 21+) — iOS en bonus si le temps le permet
- Les données sont stockées localement sur l'appareil — aucun serveur requis
- Compatibilité avec .NET 8 / MAUI
- Les mots de passe doivent être hachés (BCrypt) — jamais stockés en clair
- Validation côté ViewModel avant toute écriture en base de données

### 8.2 Contraintes de Projet

- Projet réalisé en groupe de 3 dans le cadre scolaire
- Deadline : **19 avril 2026**
- Code versionné sur dépôt Git partagé (GitHub) avec branches par feature
- Sprints planifiés dans Notion (3 sprints couvrant 8 Epics)
- Revues de code entre équipiers avant merge sur la branche principale

---

## 9. Livrables

| Livrable                    | Description                                    |
|-----------------------------|------------------------------------------------|
| Code source complet         | Dépôt GitHub avec historique Git propre        |
| Application Android (.apk)  | APK fonctionnel et testé                       |
| Cahier des charges          | Ce document (version 2.0)                      |
| Diagrammes UML              | Classes, séquence, cas d'utilisation           |
| Présentation (diaporama)    | Démo et explication de l'architecture          |
| Manuel d'utilisation        | Guide utilisateur simplifié                    |

---

## 10. Gestion de Projet

### 10.1 Équipe

| Membre           | Responsabilités principales                          |
|------------------|------------------------------------------------------|
| Souleymane Sow   | Architecture, ViewModels, Repository layer, DI       |
| Moses Kasindi    | UI/UX XAML, graphiques (LiveCharts2), tests          |
| Ruth Kegmo       | Models, Services, authentification, base de données  |

### 10.2 Sprints

| Sprint   | Période       | Objectifs principaux                                      |
|----------|---------------|-----------------------------------------------------------|
| Sprint 1 | Semaines 1–2  | Architecture, setup projet, Models, DB, Auth              |
| Sprint 2 | Semaines 3–4  | CRUD dépenses, catégories, tableau de bord                |
| Sprint 3 | Semaines 5–6  | Graphiques, objectifs, polish UI, tests, démo             |

---

*Document rédigé dans le cadre d'un projet scolaire — Version 2.0 — Mars 2026*
