# Examen DevOps - Intranet New Deal Technologique

## État du projet

Ce projet contient tous les éléments demandés pour l'examen DevOps.

## Contenu du projet

### 1. Site web personnalisé ✅

Le template HTML5Up "Forty" a été entièrement personnalisé pour le Ministère de la Communication du Sénégal :

- **index.html** : Page d'accueil avec présentation du New Deal Technologique
- **landing.html** : Page des projets (administration électronique, formations, infrastructures)
- **generic.html** : Page des ressources documentaires
- **elements.html** : Page des services (support technique, cybersécurité, hébergement)

Toutes les pages ont été adaptées avec :
- Titres et contenus en français
- Informations du Ministère de la Communication
- Coordonnées sénégalaises (+221 33 800 00 00)
- Email : contact@newdealtechnologique.sn
- Adresse : Ministère de la Communication, Dakar, Sénégal

### 2. Dockerfile ✅

Configuration Docker avec :
- Image de base : `nginx:alpine3.23`
- Copie de tous les fichiers HTML, CSS, JS et images
- Exposition du port 80
- Démarrage de Nginx

### 3. Pipelines CI/CD ✅

#### CI Pipeline (.github/workflows/ci.yml)
Déclenchée sur la branche `dev` :
1. **Job Build** : Construction de l'image Docker
2. **Job Security Scan** : Analyse Trivy (vulnérabilités) + TruffleHog (secrets)
3. **Job Push** : Envoi vers Docker Hub

#### CD Pipeline (.github/workflows/cd.yml)
Déclenchée sur la branche `prod` :
1. **Job Security Scan** : Analyse de sécurité
2. **Job Deploy** : Déploiement sur runner `runner_prod` avec exposition port 80

#### Pipelines Évoluées (.github/workflows/ci-evolved.yml et cd-evolved.yml)
Version améliorée avec :
- Changement vers `nginx:alpine3.23-slim`
- Blocage en cas de vulnérabilités CRITICAL
- Notifications par email (succès/échec)

### 4. Documentation ✅

- **README.md** : Documentation complète du projet
- **.gitignore** : Fichiers à ne pas committer

## Instructions pour l'étudiant

### Étape 1 : Créer le repository GitHub

1. Connectez-vous à votre compte GitHub
2. Créez un nouveau repository nommé `intranet-newdeal`
3. Initialisez-le avec un README
4. Copiez l'URL du repository

### Étape 2 : Initialiser le dépôt local

```bash
# Dans le dossier du projet
git init
git remote add origin https://github.com/VOTRE_COMPTE/intranet-newdeal.git
git add .
git commit -m "Initial commit - Intranet New Deal Technologique"
git branch -M main
```

### Étape 3 : Créer les branches

```bash
# Créer et pousser la branche dev
git checkout -b dev
git push -u origin dev

# Créer et pousser la branche prod
git checkout -b prod
git push -u origin prod

# Revenir à main
git checkout main
git push -u origin main
```

### Étape 4 : Inviter le collaborateur

1. Allez dans les paramètres du repository GitHub
2. Cliquez sur "Collaborators" dans le menu de gauche
3. Cliquez sur "Add people"
4. Entrez l'email : `moisawade@gmail.com`
5. Choisissez les permissions appropriées

### Étape 5 : Configurer les secrets GitHub

Dans les paramètres du repository → Secrets and variables → Actions :

Ajoutez les secrets suivants :
- `DOCKER_HUB_USERNAME` : Votre nom d'utilisateur Docker Hub
- `DOCKER_HUB_TOKEN` : Votre token Docker Hub (créer sur hub.docker.com)
- `EMAIL_USERNAME` : Votre email pour les notifications
- `EMAIL_PASSWORD` : Mot de passe ou app password
- `NOTIFICATION_EMAIL` : Email de destination des notifications

### Étape 6 : Configurer le runner de production

1. Allez dans Settings → Actions → Runners
2. Téléchargez et configurez un runner nommé `runner_prod`
3. Suivez les instructions pour l'installer sur votre machine de production

### Étape 7 : Tester les pipelines

1. Poussez des modifications sur la branche `dev` pour tester la CI
2. Poussez des modifications sur la branche `prod` pour tester la CD

### Étape 8 : Captures d'écran

Prenez des captures d'écran :
- De l'exécution de la CI sur dev
- De l'exécution de la CD sur prod
- Des jobs qui réussissent
- Des scans de sécurité

### Étape 9 : Soumission

1. Créez un document Word nommé `NOM_PRENOM.docx`
2. Insérez les captures d'écran
3. Envoyez à `moussawade@groupeisi.com`
4. Objet : `examen_devops_l3iage_2026`

## Points importants

- Les workflows sont configurés pour utiliser `ubuntu-latest` comme spécifié
- Les jobs utilisent `needs` pour assurer l'ordre d'exécution
- Les scans de sécurité incluent Trivy (vulnérabilités) et TruffleHog (secrets)
- Le déploiement en production utilise un runner dédié nommé `runner_prod`
- Le service est exposé sur le port 80

## Bon courage pour votre examen ! 🚀