# scaling-waffle


** Application web permettant aux utilisateurs de créer un profil

## Architecture technique

### Stack applicative
- **Backend** : FastAPI + PostgreSQL
- **Frontend** : Next.js
- **Auth** : JWT avec hashage bcrypt/argon2

![alt text]()

### Fonctionnalités core - A voir?! ...
1. Création de compte / Login / Logout
2. Gestion de profil (nom, email, bio, modification)
3. **Suivi d'activité utilisateur** (connexions, mises à jour profil)
4. Page "Mon Pulse" : profil + activité + statut service


### Modèle de données
à venir


## Infrastructure & DevOps

### Environnements
- **Dev** : Docker Compose => local
- **Préprod** : 1 seul VPS OVH : frontend, backend, Postgresql, Redis
- **Prod** : OVH 2-3 VPS : Frontend, Backend+DB, REDIS Monitoring ?!

### Provisionnement (Terraform)
- Stockage de l'état dans terraform cloud
- Séparation par environnement
- Règles firewall/réseau

### Configuration (Ansible)
- Installation Docker
- Installation Nomad => orchestration
- Durcissement système (hardening)
- HTTPS via certbot ? Caddy ou Traefik? 
- Déploiement applicatif
- Utilisation de rôles Galaxy => geerlingguy, cloudalchemy

### Orchestration (Nomad)
- Déploiement déclaratif des services
- Gestion multi-environnements (preprod/prod)
- Pas de surcharge Kubernetes pour un projet simple


### CI/CD (GitHub Actions) => Section validée passage rncp sept 2026
- Build
- Push images Docker
- Déploiement automatisé via Nomad job files


# Principe de Sécurité (Defense in depth)

### Niveau Infrastructure (Terraform)
- Ports strictement nécessaires (22, 80, 443)
- Segmentation réseau
- DB non accessible depuis internet

### Niveau Système (Ansible)
- SSH par clé uniquement, root désactivé
- Firewall local (UFW)
- Fail2ban contre brute force
- Mises à jour automatiques

### Niveau Applicatif
- Secrets externalisés (variables d'env)
- Validation des entrées
- HTTPS obligatoire
- Base de données : utilisateur non-superuser, accès IP limité


## Monitoring & Observabilité

### Infrastructure (Prometheus + Grafana)
- Métriques système (CPU, RAM, disque)
- Disponibilité des services
- Alertes si service down

### Application
- Nombre de connexions par jour
- Erreurs API / latence
- Endpoint /metrics pour Prometheus

### Logs (Loki + Promtail)
- Centralisation des logs
- Analyse des erreurs


## Questions pour validation ...

- Base de données sur même VPS que backend => justifié par coût/simplicité) ???
- Monitoring peut être sur VPS frontend (coût) ou VPS dédié ??
- Fonctionnalités applicatives volontairement SIMPLE mais peut être insuffisantes?



