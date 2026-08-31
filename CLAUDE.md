# KiRoulOu — Landing page — Contexte projet

## Le projet, en bref

KiRoulOu est une plateforme web (puis mobile) qui centralise les randonnées **VTT** organisées par les clubs et associations en France : carte interactive, fiches événements avec traces GPX, infos pratiques, préinscription en ligne avec paiement.

- **Deux publics cibles** : les clubs/associations organisateurs (publication gratuite, option Premium à venir) et les pratiquants (recherche, inscription, téléchargement des parcours).
- **Portée volontairement restreinte au VTT uniquement** pour le lancement — pas de marche ni de trail pour l'instant. C'est un choix stratégique assumé (focus produit, ressources limitées, porteur de projet solo). Ne pas réintroduire de multi-sport dans les textes ou visuels sans validation explicite.
- **Lancement pilote en Bretagne**, extension nationale envisagée seulement après validation locale.
- **Phase actuelle : pré-lancement.** L'application elle-même n'est pas encore développée (calendrier estimé à 1 an – 1 an et demi de développement solo, avec l'appui de l'IA, avant un lancement pilote complet). La landing page sert à constituer une liste d'attente pendant cette phase de développement, pas à présenter un produit déjà fonctionnel.
- Porteur de projet : Christophe Salou, micro-entreprise déjà immatriculée, développement solo assisté par IA, budget d'exploitation très contraint (< 100 €/mois).

## Marque

- **Nom : KiRoulOu** (jeu de mots sur "qui roule où"). Toujours écrit avec cette casse exacte (K, R, O majuscules).
- Logo : badge circulaire façon pignon de vélo, illustration d'un cycliste VTT en cabré, 2 couleurs seulement.
- **Palette de marque (extraite directement du logo, à ne pas modifier sans raison) :**
  - `--ink` (prune très foncé, quasi noir) : `#2B1F2B`
  - `--sage` (vert du badge) : `#A7CE9D`
  - `--sage-light` (fond clair dérivé) : `#EDF5EA`
  - `--sage-dark` (vert plus soutenu, accents) : `#6E9C63`
  - `--clay` (accent chaud pour CTA) : `#C9822B` — réutilisé depuis le pitch deck du projet pour rester cohérent entre tous les supports
  - `--paper` (fond clair général) : `#FAF9F5`
- Typographies : **Archivo** (900, display/titres) + **Karla** (texte courant), chargées via Google Fonts.
- Slogan/accroche validée : _« Toutes les randos VTT de Bretagne, bientôt au même endroit. »_

## Ce qui existe déjà (autres livrables du projet, pour contexte, pas à modifier ici)

Une étude de marché, un business plan avec prévisionnel financier 3 ans, un document personas/user stories, et un pitch deck ont déjà été produits (formats .docx/.pptx, hors périmètre de ce repo). Ils servent de référence pour rester cohérent sur : le positionnement VTT-only, le modèle freemium (gratuit clubs + abonnement Premium à 150 €/an via Stripe Billing), et le calendrier réaliste de développement (1 à 1,5 an). Si la landing page doit un jour refléter des chiffres ou des délais, se référer à ces documents plutôt que d'inventer de nouveaux chiffres.

## La landing page — état actuel

`index.html` + `style.css`, HTML/CSS/JS sans dépendance externe hébergée par nous à part Google Fonts et le script Tally (les deux images de marque — badge et silhouette — restent encodées en base64 directement dans `index.html`, mais le CSS a été extrait dans son propre fichier pour la maintenabilité). S'y ajoutent des fichiers d'assets séparés (nécessaires pour être de vraies URLs, pas du base64) : `favicon.ico`, `favicon-32x32.png`, `favicon-16x16.png`, `apple-touch-icon.png`, `og-image.png` (1200×630, généré à partir du badge pour l'aperçu de partage social), `robots.txt`, `sitemap.xml`. Neuf fichiers au total, tous à la racine, à déposer ensemble sur l'hébergement — plus un seul fichier unique. Domaine cible : `beta-kiroulou.bezedache.com` (sous-domaine de `bezedache.com`, choisi pour ne pas écraser une version précédente déjà en ligne sur `kiroulou.bezedache.com`) — c'est cette URL qui est codée en dur dans le `canonical`, les balises Open Graph/Twitter, `sitemap.xml` et `robots.txt` ; à corriger partout si le sous-domaine change un jour.

### Structure de la page (dans l'ordre)

1. **Hero** — fond vert clair avec lignes topographiques SVG discrètes en arrière-plan, badge logo, titre, sous-texte, bouton qui scroll vers le formulaire.
2. **Le problème** — 3 points courts (dispersion, temps perdu pour les clubs bénévoles, info éclatée), présentés en liste façon panneau de signalisation (bordure gauche colorée), pas en cartes avec ombre.
3. **Comment ça marchera** — un **profil altimétrique SVG** (ligne + 3 points d'étape : Découvrir / S'inscrire / Rouler) sert de fil conducteur visuel. C'est un choix délibéré qui fait écho au produit lui-même (les fiches événements afficheront un vrai profil altimétrique) — ne pas remplacer par une grille de cartes générique.
4. **Inscription (`#signup`)** — fond sombre (`--ink`), formulaire **Tally encastré en iframe** dans une carte blanche flottante, plus silhouette du cycliste en filigrane très discret en arrière-plan (asset `kiroulou-silhouette.png`, fond détouré en transparent).
5. **Footer** — wordmark, email de contact.

### Intégration Tally

- Formulaire encastré (pas de popup — testé puis explicitement écarté par le porteur de projet, qui préfère le formulaire visible directement sur la page).
- Script chargé en tête de page : `<script async src="https://tally.so/widgets/embed.js"></script>` — c'est ce script qui détecte automatiquement les balises `data-tally-src` et charge l'iframe, aucun JS custom nécessaire.
- URL actuelle de l'iframe : `https://tally.so/embed/Mexzk0?hideTitle=1&transparentBackground=1&dynamicHeight=1`
- **⚠️ Point non résolu à vérifier avant toute mise en prod** : deux IDs de formulaire Tally différents sont apparus au fil des échanges (`1Aa7QQ` puis `Mexzk0`). Le porteur de projet doit confirmer que `Mexzk0` est bien le bon formulaire (avec la logique de branchement club/pratiquant) et pas un brouillon. Ne pas modifier cet ID sans confirmation explicite.
- Il existe un **second formulaire Google Forms**, plus détaillé (10 questions), qui sert au démarchage direct de clubs ciblés — celui-là n'a pas vocation à apparaître sur la landing page publique.

### Photo / imagerie

- Aucune photo n'est utilisée sur la page actuellement : le hero repose sur un dégradé + motif topographique SVG plutôt qu'une photo, précisément parce qu'une image iStock non licenciée avait été proposée au départ et écartée pour raison de droits d'auteur. **Si une photo est ajoutée un jour, vérifier qu'elle est bien libre de droits** (Unsplash/Pexels ou achat réel), jamais une capture d'aperçu basse résolution d'une banque payante.

## Principes de design à respecter si la page évolue

- Éviter les clichés de design généré par IA : pas de fond crème + accent terracotta générique, pas d'eyebrow en petites majuscules espacées au-dessus de chaque titre, pas de grille de cartes identiques à coins arrondis avec ombre uniforme, pas de flèche `→` systématique en fin de bouton.
- Le motif du profil altimétrique (ligne brisée façon dénivelé) est la signature visuelle de la page — le réutiliser plutôt que d'introduire un nouveau motif si on ajoute une section.
- Rester sobre sur les animations : pas d'animation d'apparition systématique sur chaque section au scroll.
- Mobile-first vérifié : la page est responsive (colonnes qui passent en une seule colonne sous 760px), à retester après toute modification de mise en page.

## Prochaines étapes probables

- Confirmation de l'ID Tally définitif.
- Mise en ligne sur `beta-kiroulou.bezedache.com` et test réel du chargement du formulaire (non testable en local, l'iframe dépend d'un accès internet vers tally.so) — déposer les 9 fichiers ensemble, pas seulement `index.html`.

Fait : favicon (dérivé du badge, plusieurs tailles) et image Open Graph pour le partage sur les réseaux sociaux.
