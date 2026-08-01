---
theme: ./theme
title: learn-dev — Présentation
info: |
  Diaporama de soutenance — Titre professionnel Développeur Web et Web Mobile (DWWM),
  RNCP37674 — Eric Bouchut — session août 2026.
author: Eric Bouchut
lang: fr
aspectRatio: 16/9
transition: slide-left
mdc: true
download: false
colorSchema: auto
layout: intro
---

# learn-dev

## Plateforme Web d'apprentissage de la programmation

**Eric Bouchut** — Titre professionnel Développeur Web et Web Mobile (DWWM)

Soutenance — RNCP 37674 — session août 2026

<!--
(~0,5 min) 


- Saluer le jury.
- Se présenter brièvement.
-->

---
layout: section
---

# Introduction

---

# Le besoin

- **Contexte**: Apprendre à programmer suppose un **parcours structuré** : 
    - du contenu organisé, 
    - une progression lisible, 
    - un espace où un formateur publie et fait évoluer ses cours.
- **Problème** : offrir un environnement multi-rôles simple, **sûr** et **accessible**.
- **Solution** :
  > *`learn-dev` est une plateforme Web où des formateurs publient des cours composés de leçons
  > en Markdown, et où des étudiants s'inscrivent et les suivent.*

<!--
(~1 min) 

Me présenter. 

- Poser le besoin : structurer l'apprentissage du code. 
- Annoncer la solution en une phrase. 
- Enchaîner sur ce qu'est concrètement l'application.
-->


---

# Vue d'ensemble de learn-dev 

<div class="grid grid-cols-2 gap-6 items-center">

<div>

- **Trois rôles** : 
    - étudiant (`STUDENT`), 
    - formateur (`INSTRUCTOR`), 
    - administrateur (`ADMIN`).  

- **Étudiant** : catalogue, inscription à des cours, lecture des leçons.
- **Formateur** : création de cours/leçons, cycle de vie de publication, gestion des inscriptions.
- **Administrateur** : gestion des comptes, modération des contenus.

</div>

<img src="/images/mockup-home.png" class="rounded shadow" />

</div>

<!--
(~1 min)

- Décrire les 3 rôles et le parcours nominal. 
- Préciser : application Web rendue côté
serveur (Spring Boot + Thymeleaf), responsive et accessible.
-->

---
layout: image
image: /images/learn-dev-home.png
backgroundSize: contain
---

# Démo

---
layout: section
---

# Conception

<!--
Cette section aborde:

- **l'organisation du travail** (aujourd'hui en solo, donc pas encore de SCRUM)
- le cahier des charges
- la modélisation des données et la base qui les stockent
- le maquettage et l'expérience utilisateur (UX)
- l'environnement de travail
-->

---

# Gestion de projet

- GitHub **Project**, 
- **Issues**,
- **ADR**s (*Architecture Decision Records*),
- **Plans** de développement,
- Développement **incrémental** : (authentification, domaine cours, création de contenu, administration),
- Git: **Branche par fonctionnalité**,
- **Conventional Commits**,
- **Pull-Requests**,
- **YAGNI**.

<!--
(~2 min)

Insister sur la démarche d'ingénierie :
- **[Project](https://github.com/users/ebouchut/projects/7/views/2)** pour **orchestrer** ce qui suit 
- **[Issues](https://github.com/ebouchut/learn-dev/issues)**: pour décrire les besoins fonctionnels et les bug
- **[ADR](https://github.com/ebouchut/learn-dev/blob/dev/docs/adr/README.md)** C'est l'**enregistrement des décisions d'architecture**s pour aider les nouveaux arrivants sur le projet (ou moi-même dans 6 mois :-).
  >  Chaque *ADR* répond à cette question: pourquoi a-t-on fait ce choix ?  
    - **Problème** à résoudre et les **contraintes**.
    - **Critères de décision**: ce qui a guidé le choix.
    - **Options** envisagées
    - **Option retenue**: pourquoi, bénéfices et compromis.
    - **Avantages/inconvénients** de chaque option.
- **[Plans](https://github.com/ebouchut/learn-dev/tree/dev/docs/plans)** de dev versionnés: Ils décrivent quoi faire et comment.
- [Branche Git par fonctionnalité](https://github.com/ebouchut/learn-dev/tree/dev?tab=contributing-ov-file#git-branching-strategy) pour que chaque développement n'impacte pas la branche commune (`dev`).
- [Pull-Requests](https://github.com/ebouchut/learn-dev/pulls?q=is:pr+is:closed)
- **`YAGNI`** : *You aren't gonna need it*  
  > Ne construire que ce qui est nécessaire pour la v1.

C'est de la communication écrite (compétence transversale).
-->

---

# Cahier des charges

## Objectifs fonctionnels

- s'inscrire et suivre des cours, 
- gérer et publier des cours,
- administrer.

## Objectifs non fonctionnel

- sécurité, 
- accessibilité (*RGAA*),
- responsive, 
- tests, 
- Intégration Continue (CI).

---

# Personas

- **Léa** (étudiante)
    - s'inscrit et suit des cours, sur mobile comme sur ordinateur.
- **Marc** (formateur)
    - rédige les leçons de cours qu'il conçoit en Markdown, 
    - gère la publication de ses cours,
- **Awa** (admin):
    - gère les comptes,
    - modère en toute sécurité.

<!--
(~2 min) 
Dérouler les besoins par persona. 
Relier aux besoins non fonctionnels.
-->

---
layout: section
---

# Base de données  <small>(CP5)</small>

---
layout: two-cols
---

::left::

# Base de données — MCD

Modèle Conceptuel de Données


- Vue **client** de ses **donnés métier** :
    - **entités**
        - identifiants (soulignés)
    - **relations**
        - cardinalités

- Aucune syntaxe technique (base de données)

::right::

  <img src="/images/mcd.png" class="max-h-[85%] max-w-[85%]" alt="MCD" />



<!--
(~1,5 min)

- Présenter la modélisation Merise (MCD). 
- 9 entités : utilisateurs, rôles, cours, leçons, inscriptions, jetons, audit. 
- Montrer les associations et cardinalités.
-->


---
layout: two-cols
---


::left::

# Base de données — MLD

Modèle Logique de Données


- **Structure relationnelle**
    - **tables**
    - **tables de jointure** 
        - modélisent la cardinalité `N,N`
    - **clé étrangères** (Foreign Keys)
        - précédées par `#`
        - modélisent les cardinalités `1,1` et `1,N`
- **Indépendant de la base de données**


::right::

<Transform :scale="1.2" origin="top">
  <img src="/images/mld.svg" class="h-100 mx-auto rounded" />
</Transform>

<!--
(~1,5 min)

9 entités : utilisateurs, rôles, cours, leçons, inscriptions, jetons, audit. 
- Relationnel mais pas spécifique à une base de données.
- PAS encore les **types** de colonnes, contraintes... 
-->


---

# Base de données — MPD

Modèle Physique de Données

- Syntaxe spécifique à la base de données relationelle **PostgreSQL**,
- **Clé primaire**
    - **`UUID`** pour la table `users` (anti-IDOR) 
    - **`BIGINT`** pour toute les autres
    - **Clé primaire composite** pour les 2 tables de jonction 


<!--
(~1,5 min) 

- Pourquoi PostgreSQL ? ([ADR-0007]()), 
- Liquibase ([ADR-0005]()), 
- UUID ([ADR-0003]()).
- Contrôle anti-dérive de schéma fait par la CI et au démarrage de l'application.
-->

---
layout: full
---

# Modèle Physique de Données

<img src="/images/mpd.svg" class="max-h-[100%] max-w-[100%]" alt="MPD" />

---

# Maquettage et accessibilité <small>(CP2)</small>

<div class="grid grid-cols-[1fr_auto] gap-6 items-center">

<div>

- **Maquettes Figma** + prototypes HTML ; charte, deux thèmes (Catppuccin / Soft Paper).
- **Responsive** : versions Web (bureau) **et Web mobile** (points de rupture en `rem`).
- **Accessibilité RGAA / WCAG AA** : structure sémantique, *skip link*, contrastes
  calculés (min. 4,73:1), police **Atkinson Hyperlegible**.

</div>

<img src="/images/mockup-mobile.png" class="h-90 rounded shadow" />

</div>

<!--
(~2 min) Montrer la version mobile. Insister sur l'accessibilité « par construction » et les
contrastes mesurés. C'est CP2 (maquetter) : Web ET Web mobile.
-->

---

# Environnement technique <small>(CP1)</small>

- **Java 21**
- **Maven** (dépendances, cycle de vie logiciel)
- **Spring Boot 3.5** (Web MVC, Data JPA, Validation, Mail)
- **Spring Security** (*RBAC*), 
- **Thymeleaf** (templates/vues), 
- **commonmark-java**: conversion du *Markdown* en *HTML*
- **jsoup**: assainissement des tags et attributs HTML 
- **PostgreSQL 17** + **Liquibase**.
- **Docker** et **Docker Compose** (Postgres, Mongo, Mailpit)
- **Git**: Gestion de l'historique du code source
- **CI**:  GitHub Actions.


<!--
(~2 min) 

Balayer la stack:
- **Java** langage de **Programmation Orientée Objet** (*POO*)
- **Maven**: outil qui:
    - gére les dépéndances (installation, mise à jour, résoluition de conflits, dépendances transitives)
- **Spring Boot** contient une galaxie de frameworks j'ai utilisés pour:
  - le MVC
- **Spring Security**: framework de sécurité qui gère :
    - l'**authentification** via le **formulaire de connexion** 
    - le **controle d'accès** basé sur les **roles** 
- **Thymeleaf**: moteur templates utilisé pour le rendu coté serveur
-->

---
layout: section
---

# Développement

---

# Architecture en couches

MVC (Controller Model View)

- **`Controller`**  reçoit les requêtes HTTP entrantes et dispatche leur traitement et renvoie la réponse
    - **`Service`** applique les règles métier d'une entité. 
        - **`Repository`** fait les interactions avec la base de données pour une entité.

```mermaid { scale: 0.6 }
flowchart LR
    browser@{shape: curv-trap, label: "Navigateur Web"}
    controller[Contrôleur]
    service["Service<br/>règles métier"]
    repository["Repository<br/>(Spring Data JPA)"]
    db["Base de données
        (PostgreSQL)"]
    thymeleaf[Thymeleaf]
    views@{ shape: docs, label: "Templates de Vue" }
    view@{  shape: doc,  label: "'Template de Vue" }

    browser     -->|HTTP| controller
    controller  --> service
    service     --> repository
    repository  --> db
    db          -.-> repository
    repository  -.-> service
    service     -.-> controller
    controller  -->|nom de template de vue| thymeleaf
    thymeleaf   -->|cherche| views
    views       -.-> view
    view        -.->|template de vue| thymeleaf
    thymeleaf   -->|Renseigne la vue| thymeleaf
    thymeleaf   -.-> |"HTML (vue remplie)"| browser
```

---

# Deux fonctionnalités CRUD

- **Fonctionnalités**:
  1. **Inscription d'un utilisateur**
      - validation, 
      - sécurité, 
      - jeu d'essai.
  2. **Gestion des cours et leçons**
      - cycle de vie, 
      - autorisations.
- **Erreurs HTTP** explicites :
    - `403`: Pas authentifié ou authorisation insuffisante
    - `404`: On ne le présente plus
    - `409`: conflit dans les paramètres de la requête

<!--
(~1 min)

- Voici **2 features** que je vais détailler par la suite.
- **Erreur `403`**: Si le login échoue ne **jamais** préciser **la cause** (login n'existe pas ou mot de passe est incorrect) mais renvoyer `403`.
-->

---

# Feature 1 — Inscription <small>(CP4, CP7)</small>

<div class="grid grid-cols-2 gap-4 items-center">

<div>

- Formulaire **validé** (Bean Validation), **erreurs accessibles**.
- **Unicité** username/e-mail ; motif **Post-Redirect-Get**.

```java
public User register(RegisterForm form) {
    if (users.existsByUsername(form.username())) {
        throw new DuplicateUsernameException();
    }
    if (users.existsByEmail(form.email())) {
        throw new DuplicateEmailException();
    }
    // hachage BCrypt, jamais de mot de passe en clair
    user.setPassword(encoder.encode(form.password()));
    return users.saveAndFlush(user);
}
```

</div>

<img src="/images/mockup-register.png" class="h-80 rounded shadow" />

</div>

<!--
(~2 min) Démo/écran de l'inscription. Montrer la validation et les messages d'erreur reliés
au champ (aria). Le code : unicité + hachage BCrypt, jamais de mot de passe en clair.
CP4 (dynamique) + CP7 (composant métier).
-->

---

# Jeu d'essai — Inscription

| Scénario | Attendu | Obtenu |
|---|---|---|
| [Cas nominal](https://github.com/ebouchut/learn-dev/blob/2e892c853b7e04881a388faf3a663a83e9d93f28/src/test/java/com/ericbouchut/learndev/auth/RegistrationServiceTest.java#L30-L42) | Compte créé, mot de passe **haché**, rôle `STUDENT` | Conforme |
| [E-mail déjà utilisé](https://github.com/ebouchut/learn-dev/blob/2e892c853b7e04881a388faf3a663a83e9d93f28/src/test/java/com/ericbouchut/learndev/auth/RegistrationServiceTest.java#L44-L52) | Erreur de champ, **aucune** création | Conforme |
| Mot de passe trop court (< 8) | Rejet par la validation | Conforme |
| [E-mail invalide]() | Rejet par la validation | Conforme |

<!--
(~1,5 min)

 - Dérouler le jeu d'essai : entrées, attendu, obtenu, écarts (aucun). 
 - Couvert pardes tests automatisés.
-->

---

# Feature 2 — Cours et leçons <small>(CP7)</small>

- **Autorisations** : le cours d'un autre formateur → **403** ; contenu invisible → **404** ;
  transition invalide → **409**.
- Réordonnancement des leçons, gestion des inscrits, **journal d'audit**.

```mermaid { scale: 0.9 }
stateDiagram-v2
    direction LR
    [*] --> DRAFT
    DRAFT --> PUBLISHED : publier
    DRAFT --> ARCHIVED : archiver
    PUBLISHED --> ARCHIVED : archiver
    ARCHIVED --> DRAFT : restaurer
```

<!--
(~2,5 min) Montrer l'espace formateur : création, publication, réordonnancement. Insister
sur les règles métier (cycle de vie ci-dessus, appliqué aux cours ET aux leçons) et la
gestion fine des erreurs HTTP. CP7.
-->

---

# Front-end : interfaces et responsive <small>(CP3, CP4)</small>

<div class="grid grid-cols-2 gap-6 items-center">

<div>

- **21 gabarits Thymeleaf**, HTML5 sémantique, CSS responsive, fragment de mise en page
  partagé.
- Rendu **dynamique** du Markdown des leçons (converti puis **assaini** contre les XSS).
- Navigation précédent/suivant, affichage conditionnel selon le rôle.

</div>

<img src="/images/mockup-catalog.png" class="rounded shadow" />

</div>

<!--
(~2 min) Montrer le catalogue. Rappeler responsive + RGAA (CP3) et la partie dynamique
serveur (CP4).
-->

---

# Accès aux données <small>(CP6)</small>

- **Spring Data JPA** : *repositories* = interfaces, requêtes **dérivées** et
  **paramétrées** (anti-injection SQL) ; `@Transactional`.
- **NoSQL** : MongoDB **provisionné** en vue d'un stockage de contenu (non encore branché).

```java
public interface UserRepository extends JpaRepository<User, UUID> {

    @EntityGraph(attributePaths = "roles")   // l'utilisateur ET ses rôles en 1 requête
    Optional<User> findByUsername(String username);

    boolean existsByUsername(String username);
    boolean existsByEmail(String email);
}
```

<!--
(~1,5 min) Montrer le repository : une interface, Spring génère l'implémentation ; requêtes
paramétrées donc pas d'injection SQL. Assumer honnêtement l'écart NoSQL : SQL au cœur,
MongoDB prêt mais pas branché. CP6.
-->

---

# Sécurité

<div class="grid grid-cols-2 gap-4 items-start">

<div>

- **BCrypt**, **CSRF** activé, **anti-XSS** (jsoup).
- **Anti-IDOR** (UUID), **anti-énumération**, **verrouillage de compte**, **rate-limiting**.
- Jetons **hachés SHA-256**, **journal d'audit**, matrice d'autorisations **testée**.
- Référence **OWASP Top 10** ; veille **Semgrep**.

</div>

```mermaid { scale: 0.55 }
sequenceDiagram
    actor U as Navigateur
    participant S as Spring Security
    participant DB as PostgreSQL
    U->>S: POST /auth/login (+ jeton CSRF)
    S->>DB: charge utilisateur + rôles
    S->>S: vérifie le hash BCrypt
    alt échec
        S-->>U: 302 /auth/login?error
    else succès
        S-->>U: 302 /dashboard + Set-Cookie JSESSIONID<br/>(HttpOnly, SameSite=Lax)
    end
```

</div>

<!--
(~2 min) Balayer les défenses, 
dérouler la séquence de connexion : 
- CSRF, 
- BCrypt,
- session HttpOnly. 

Relier à OWASP. C'est un point fort : sécurité dès la conception.
-->

---

# Tests

- **64 tests** (pyramide) : unitaires (Mockito), tranche JPA, intégration (MockMvc).
- **PostgreSQL réel** en test via **Testcontainers** (schéma fidèle : UUID, contraintes).
- **Couverture** du code par les tests :
    -  mesurée par **JaCoCo**, 
    - publiée sur **[Codecov](https://app.codecov.io/gh/ebouchut/learn-dev)**.


<!--
(~1,5 min) 
Montrer:
- la stratégie de tests 
- la matrice de sécurité. 
La CI verrouille la qualité à chaque push.
-->

---
layout: section
---

# Déploiement

---

# Conteneurisation et CI <small>(CP8)</small>

- **Image Docker multi-étapes** : build Maven puis exécution **non-root**.
- **Docker Compose** (Postgres / Mongo / Mailpit)
- **Profils** `dev`/ `prod`
- **Secrets** via `.env`.
- **Procédure documentée**
  ```bash
  docker compose up -d        # 1. services (base de données, SMTP local)
  ./mvnw spring-boot:run      # 2. application => http://localhost:8080
  ```
- **CI GitHub Actions** (4 workflows): 
    - build, 
    - tests, 
    - lint, 
    - contrôle anti-dérive du schéma.


<!--
(~4 min) 
Rappeler : le déploiement en prod n'est pas exigé, 
c'est la QUALITÉ de la procédure documentée qui compte. 

Montrer : 
- le Dockerfile
- un workflow CI. 

CP8.
-->

---
layout: section
---

# Conclusion


---

# Challenges et évolutions

- **Challenges** : 
    - concurrence à l'inscription (contrainte d'unicité captée),
    - sécurité du rendu Markdown (assinissement des entrées pour éviter XSS),
    - un seul `h1` par page (accessibilité).
- **Évolutions** : 
    - brancher **MongoDB** (NoSQL),
    - suivre la progression leçon par leçon,
    - API REST pour utiliser de React.

<!--
(~1 min)

Ouvrir sur les évolutions,
notamment le volet NoSQL.
-->

---
layout: end
---

# Merci de votre attention.


Projet : **[github.com/ebouchut/learn-dev](https://github.com/ebouchut/learn-dev)**
- Dossier : https://github.com/users/ebouchut/projects/7/views/2

Des questions ?

<!--
(~0,5 min)

Remercier le jury et l'équipe pédagogique. 
Inviter aux questions.
-->
