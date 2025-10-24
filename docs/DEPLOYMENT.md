# 🚀 Guide de Déploiement - Render.com

## Prérequis

- Compte Render.com (gratuit)
- Repository GitHub connecté
- `RAILS_MASTER_KEY` (dans `config/master.key`)

## 📋 Étapes de Déploiement

### 1. Créer les Services sur Render

#### Option A : Déploiement Automatique (Recommandé)

1. Allez sur [Render Dashboard](https://dashboard.render.com)
2. Cliquez sur **"New +"** → **"Blueprint"**
3. Connectez votre repository GitHub `flowboard`
4. Render détectera automatiquement le `render.yaml`
5. Configurez les variables d'environnement

#### Option B : Déploiement Manuel

**1. PostgreSQL Database**
- New + → PostgreSQL
- Name: `flowboard-db`
- Database: `flowboard_production`
- User: `flowboard`
- Plan: Free

**2. Redis**
- New + → Redis
- Name: `flowboard-redis`
- Plan: Free

**3. Web Service**
- New + → Web Service
- Repository: `flowboard`
- Name: `flowboard`
- Runtime: Ruby
- Build Command:
  ```bash
  bundle install && npm install && npm run build && npm run build:css && bundle exec rails assets:precompile && bundle exec rails db:migrate
  ```
- Start Command:
  ```bash
  bundle exec puma -C config/puma.rb
  ```

**4. Sidekiq Worker**
- New + → Background Worker
- Repository: `flowboard`
- Name: `flowboard-sidekiq`
- Build Command: `bundle install`
- Start Command: `bundle exec sidekiq`

### 2. Configurer les Variables d'Environnement

Pour chaque service (Web + Worker), ajoutez :

```
RAILS_ENV=production
RAILS_MASTER_KEY=<votre_master_key>
DATABASE_URL=<auto_configuré_par_render>
REDIS_URL=<auto_configuré_par_render>
```

**Obtenir RAILS_MASTER_KEY :**
```bash
cat config/master.key
```

### 3. Configurer le Déploiement Automatique

#### A. Obtenir le Deploy Hook

1. Allez dans votre Web Service sur Render
2. Settings → Deploy Hook
3. Copiez l'URL (ex: `https://api.render.com/deploy/srv-xxx?key=yyy`)

#### B. Ajouter le Secret GitHub

1. Allez sur GitHub → Repository → Settings → Secrets and variables → Actions
2. Cliquez "New repository secret"
3. Name: `RENDER_DEPLOY_HOOK_URL`
4. Value: Collez l'URL du Deploy Hook
5. Cliquez "Add secret"

### 4. Tester le Déploiement

```bash
# Push sur main déclenche automatiquement le déploiement
git checkout main
git push origin main
```

Le workflow GitHub Actions va :
1. ✅ Lancer les tests (CI)
2. ✅ Déclencher le déploiement sur Render
3. ✅ Render va build et déployer l'application

## 🔍 Vérification

### Logs Render

```
Dashboard → Service → Logs
```

### Tester l'Application

```bash
# Votre URL Render
https://flowboard.onrender.com
```

### Vérifier la Base de Données

```bash
# Dans le Shell Render
bundle exec rails console

# Vérifier les migrations
ActiveRecord::Base.connection.tables
```

## 🐛 Dépannage

### Erreur : Missing RAILS_MASTER_KEY

```bash
# Générer une nouvelle master key
rails credentials:edit

# Copier la clé dans Render
cat config/master.key
```

### Erreur : Database Connection

- Vérifiez que `DATABASE_URL` est bien configuré
- Vérifiez que la database est liée au service

### Erreur : Assets Not Found

```bash
# Vérifier que le build command inclut
bundle exec rails assets:precompile
```

### Sidekiq ne démarre pas

- Vérifiez que `REDIS_URL` est configuré
- Vérifiez les logs du worker

## 📊 Monitoring

### Health Check

Render vérifie automatiquement `/up` (configuré dans routes.rb)

### Logs

```bash
# Voir les logs en temps réel
render logs -f flowboard
```

### Métriques

Dashboard Render → Service → Metrics

## 🔄 Rollback

En cas de problème :

1. Dashboard → Service → Events
2. Cliquez sur un déploiement précédent
3. "Redeploy"

## 🎯 Checklist Avant Production

- [ ] `RAILS_MASTER_KEY` configuré
- [ ] Database créée et migrée
- [ ] Redis configuré
- [ ] Sidekiq worker actif
- [ ] Variables d'environnement correctes
- [ ] SSL/TLS activé (automatique sur Render)
- [ ] Custom domain configuré (optionnel)
- [ ] Monitoring configuré

## 📞 Support

- [Render Documentation](https://render.com/docs)
- [Render Community](https://community.render.com)
- [GitHub Issues](https://github.com/ayoub-sourrakh/flowboard/issues)

---

**Bon déploiement ! 🚀**
