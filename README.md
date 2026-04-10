# Intranet New Deal Technologique

Site web statique pour le programme New Deal Technologique du Ministère de la Communication du Sénégal.

## Description

Ce projet est un intranet gouvernemental moderne basé sur le template HTML5Up "Forty". Il a été développé dans le cadre de l'examen DevOps pour démontrer la mise en place d'un pipeline CI/CD complet.

## Technologies

- HTML5
- CSS3
- JavaScript
- Nginx (serveur web)
- Docker
- GitHub Actions (CI/CD)

## Structure du projet

```
├── .github/workflows/          # Pipelines GitHub Actions
│   ├── ci.yml                 # CI Pipeline - Dev branch
│   ├── cd.yml                 # CD Pipeline - Prod branch
│   ├── ci-evolved.yml         # CI Pipeline évoluée
│   └── cd-evolved.yml         # CD Pipeline évoluée
├── assets/                    # Ressources CSS, JS, images
├── images/                    # Images du site
├── index.html                 # Page d'accueil
├── landing.html               # Page projets
├── generic.html               # Page ressources
├── elements.html              # Page services
├── Dockerfile                 # Configuration Docker
├── .gitignore                 # Fichiers à ignorer
└── README.md                  # Ce fichier
```

## Pipelines CI/CD

### CI Pipeline (branche dev)

1. **Build**: Construction de l'image Docker avec nginx:alpine3.23
2. **Security Scan**: Analyse de sécurité (vulnérabilités + secrets)
3. **Push**: Envoi vers Docker Hub

### CD Pipeline (branche prod)

1. **Security Scan**: Analyse de sécurité
2. **Deploy**: Déploiement sur runner_prod
3. **Expose**: Service exposé sur le port 80

### Pipelines évoluées

- Changement de l'image de base vers nginx:alpine3.23-slim
- Blocage du déploiement en cas de vulnérabilités CRITICAL
- Notifications par email (succès/échec)

## Configuration requise

- Docker
- Accès GitHub
- Secrets Docker Hub configurés
- Runner GitHub Actions nommé "runner_prod"

## Variables d'environnement (GitHub Secrets)

- `DOCKER_HUB_USERNAME`: Nom d'utilisateur Docker Hub
- `DOCKER_HUB_TOKEN`: Token Docker Hub
- `EMAIL_USERNAME`: Compte email pour notifications
- `EMAIL_PASSWORD`: Mot de passe email
- `NOTIFICATION_EMAIL`: Email de destination pour les notifications

## Déploiement local

```bash
# Construire l'image
docker build -t intranet-newdeal .

# Lancer le conteneur
docker run -d -p 80:80 --name intranet intranet-newdeal

# Accéder au site
http://localhost
```

## Branches

- `dev`: Développement et tests
- `prod`: Production

## Contact

Ministère de la Communication du Sénégal
New Deal Technologique