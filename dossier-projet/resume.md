# Résumé du projet — *learn-dev*

**Eric Bouchut** — Titre professionnel Développeur Web et Web Mobile (DWWM), RNCP37674
(niveau 5) — Centre La Plateforme\_ — Session août 2026.

## Problématique et solution

Apprendre à programmer suppose un parcours structuré : du contenu pédagogique organisé et un
environnement où un formateur publie et fait évoluer ses cours pendant que les étudiants s'y
inscrivent et progressent. **learn-dev** est une **plateforme web d'apprentissage de la
programmation** : des **formateurs** y publient des **cours** composés de **leçons** rédigées
en Markdown, et des **étudiants** parcourent le catalogue, s'inscrivent et suivent les leçons.
Un rôle **administrateur** gère les comptes et modère les contenus.

## Périmètre fonctionnel

L'application (v1) couvre l'**authentification** complète (inscription, connexion,
vérification d'e-mail, réinitialisation de mot de passe, verrouillage de compte), la
**gestion des cours et leçons** côté formateur (création, cycle de vie
brouillon → publié → archivé, réordonnancement, gestion des inscrits), le parcours
**étudiant** (catalogue, inscription, lecture des leçons) et l'**administration** (comptes,
modération). L'ensemble est **responsive** (web et web mobile) et conçu pour l'**accessibilité**
(RGAA 4 / WCAG 2.1 AA).

## Environnement technique

Application web **rendue côté serveur** : **Java 21**, **Spring Boot 3.5** (Web MVC, Security,
Data JPA, Validation, Mail), **Thymeleaf**, **PostgreSQL 17** avec migrations **Liquibase**,
rendu Markdown (**commonmark-java** + assainissement **jsoup**). Outillage : **Maven**,
**Podman / Docker Compose** (PostgreSQL, MongoDB, Mailpit), tests **JUnit 5 / Mockito /
Testcontainers** (64 tests, couverture **JaCoCo/Codecov**), intégration continue **GitHub
Actions**, modélisation **Merise** (MCD/MLD/MPD) et 14 décisions d'architecture (ADR).

## Sécurité

Mots de passe hachés en **BCrypt**, protection **CSRF**, défense **anti-XSS** (assainissement
du HTML des leçons), **anti-injection SQL** (requêtes paramétrées JPA), **anti-IDOR**
(identifiants **UUID**), réponses **anti-énumération**, **verrouillage de compte**, jetons
stockés en **SHA-256**, **limitation de débit** et **journal d'audit**.

## Compétences couvertes

Le projet met en œuvre les compétences du titre : maquettage accessible (**CP2**), interfaces
statiques et dynamiques (**CP3, CP4**), création de base de données (**CP5**), composants
d'accès aux données (**CP6**) et composants métier côté serveur (**CP7**), ainsi que la
configuration de l'environnement (**CP1**) et la documentation du déploiement (**CP8**).

*Dépôt du projet : <https://github.com/ebouchut/learn-dev>*
