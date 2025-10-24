# 🚀 Flowboard

Mini SaaS de gestion de projets et de tâches construit avec Rails 8.

## 📋 Stack Technique

- **Backend:** Ruby 3.3.4, Rails 8.0.3
- **Database:** PostgreSQL 16
- **Frontend:** Hotwire (Turbo + Stimulus), TailwindCSS, esbuild
- **Containerisation:** Docker & Docker Compose

## 🚀 Installation

### Prérequis

- Ruby 3.3.4
- Node.js 20+
- Docker & Docker Compose
- Git

### Setup

```bash
# Cloner le projet
git clone git@github.com:ayoub-sourrakh/flowboard.git
cd flowboard

# Installer les dépendances
bundle install
yarn install

# Copier les variables d'environnement
cp .env.example .env

# Démarrer PostgreSQL avec Docker
docker-compose up -d postgres

# Créer la base de données
rails db:create db:migrate

# Démarrer l'application
bin/dev
```

Accéder à l'application : http://localhost:3000

## 🔧 Commandes Utiles

```bash
# Démarrer tous les services
bin/dev

# Console Rails
rails console

# Tests
rails test

# Linter
rubocop
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
├── app/              # Code de l'application
├── config/           # Configuration
├── db/               # Base de données
├── test/             # Tests
└── docker-compose.yml # Services Docker
```

## 🤝 Contribution

1. Fork le projet
2. Créer une branche feature (`git checkout -b feature/amazing-feature`)
3. Commit les changements (`git commit -m 'feat: add amazing feature'`)
4. Push vers la branche (`git push origin feature/amazing-feature`)
5. Ouvrir une Pull Request

## 📄 License

MIT
