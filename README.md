# 🚀 Flowboard

[![CI](https://github.com/ayoub-sourrakh/flowboard/actions/workflows/ci.yml/badge.svg)](https://github.com/ayoub-sourrakh/flowboard/actions/workflows/ci.yml)
[![Deploy](https://github.com/ayoub-sourrakh/flowboard/actions/workflows/deploy.yml/badge.svg)](https://github.com/ayoub-sourrakh/flowboard/actions/workflows/deploy.yml)

Mini SaaS de gestion de projets et de tâches construit avec Rails 8.

## 📋 Stack Technique

- **Backend:** Ruby 3.3.4, Rails 8.0.3
- **Database:** PostgreSQL 16
- **Cache/Jobs:** Redis 7, Sidekiq 7
- **Frontend:** Hotwire (Turbo + Stimulus), TailwindCSS v3, esbuild
- **Containerisation:** Docker & Docker Compose
- **CI/CD:** GitHub Actions
- **Déploiement:** Render.com

## 🚀 Installation

### Prérequis

- Ruby 3.3.4
- Node.js 14+ (recommandé: 20+)
- Docker & Docker Compose
- Git

### Setup Rapide

```bash
# 1. Cloner le projet
git clone git@github.com:ayoub-sourrakh/flowboard.git
cd flowboard

# 2. Installer les dépendances
bundle install
npm install

# 3. Copier les variables d'environnement
cp .env.example .env

# 4. Démarrer PostgreSQL et Redis avec Docker
docker-compose up -d

# 5. Créer et migrer la base de données
rails db:create db:migrate

# 6. Démarrer l'application
bin/dev
```

**Accéder à l'application :** http://localhost:3000

### Services Disponibles

- **Application Rails** : http://localhost:3000
- **Sidekiq Dashboard** : http://localhost:3000/sidekiq
- **PostgreSQL** : localhost:5432
- **Redis** : localhost:6379

## 🔧 Commandes Utiles

### Développement

```bash
# Démarrer tous les services (Rails + Sidekiq + CSS + JS)
bin/dev

# Console Rails
rails console

# Sidekiq (background jobs)
bundle exec sidekiq
```

### Tests & Qualité

```bash
# Lancer tous les tests
rails test

# Tests système (avec navigateur)
rails test:system

# Linter Ruby
rubocop

# Scan de sécurité
brakeman

# Tout en une fois (comme le CI)
rubocop && brakeman && rails test
```

### Docker

```bash
# Démarrer tous les services
docker-compose up -d

# Voir les logs
docker-compose logs -f

# Arrêter les services
docker-compose down

# Reconstruire les images
docker-compose build
```

### Base de Données

```bash
# Créer la base de données
rails db:create

# Lancer les migrations
rails db:migrate

# Rollback
rails db:rollback

# Reset complet
rails db:drop db:create db:migrate db:seed
```

## 🌿 Workflow Git

### Branches

- `main` - Branche principale (production-ready)
- `develop` - Branche de développement
- `feature/*` - Nouvelles fonctionnalités
- `bugfix/*` - Corrections de bugs
- `hotfix/*` - Corrections urgentes

### Créer une feature

```bash
git checkout develop
git pull origin develop
git checkout -b feature/nom-de-la-feature
# ... travail ...
git add .
git commit -m "feat: description"
git push origin feature/nom-de-la-feature
# Créer une Pull Request vers develop
```

## 📝 Conventions de Commit

Format : `type: description`

Types :
- `feat:` - Nouvelle fonctionnalité
- `fix:` - Correction de bug
- `docs:` - Documentation
- `style:` - Formatage
- `refactor:` - Refactoring
- `test:` - Tests
- `chore:` - Maintenance

## 📦 Structure du Projet

```
flowboard/
├── app/
│   ├── controllers/      # Contrôleurs HTTP
│   ├── models/           # Modèles de données
│   ├── views/            # Templates HTML
│   ├── javascript/       # Code JavaScript (Stimulus)
│   ├── assets/           # Assets (CSS, images)
│   └── jobs/             # Background jobs (Sidekiq)
├── config/
│   ├── environments/     # Configs par environnement
│   ├── initializers/     # Initialisation (Sidekiq, etc.)
│   └── database.yml      # Configuration base de données
├── db/
│   ├── migrate/          # Migrations
│   └── schema.rb         # Schéma actuel
├── test/                 # Tests (Minitest)
├── docs/                 # Documentation
│   ├── DEPLOYMENT.md     # Guide de déploiement
│   └── ...
├── .github/
│   └── workflows/        # CI/CD (GitHub Actions)
├── docker-compose.yml    # Services Docker
└── render.yaml           # Configuration Render
```

## 🚀 Déploiement

Le projet est configuré pour un déploiement automatique sur Render.com.

**Guide complet :** [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md)

### Déploiement Rapide

1. Créer un compte sur [Render.com](https://render.com)
2. Connecter le repository GitHub
3. Render détectera automatiquement `render.yaml`
4. Configurer `RAILS_MASTER_KEY` dans les variables d'environnement
5. Déployer ! 🚀

Le déploiement se fait automatiquement à chaque push sur `main`.

## 🤝 Contribution

1. Fork le projet
2. Créer une branche feature (`git checkout -b feature/amazing-feature`)
3. Commit les changements (`git commit -m 'feat: add amazing feature'`)
4. Push vers la branche (`git push origin feature/amazing-feature`)
5. Ouvrir une Pull Request vers `develop`

Voir [CONTRIBUTING.md](CONTRIBUTING.md) pour plus de détails.

## 📚 Documentation

- [Guide d'installation](docs/SETUP.md)
- [Guide de déploiement](docs/DEPLOYMENT.md)
- [Architecture](docs/ARCHITECTURE.md)

## 📄 License

MIT

---

**Développé avec ❤️ par l'équipe Flowboard**
