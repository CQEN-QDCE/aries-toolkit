# Déploiement Aries Issuer sur OpenShift

Ce dépôt contient les instructions nécessaires pour déployer un agent émetteur Aries sur OpenShift.

| Gabarit  | Descripton |
| -------- | ---------- |
| [ssi-studio.yaml](https://github.com/CQEN-QDCE/ssi-studio/blob/master/openshift/templates/ssi-studio.yaml) | Installation de l'application. |
| [ssi-studio.dev.params](https://github.com/CQEN-QDCE/ssi-studio/blob/master/openshift/templates/ssi-studio.dev.params) | Paramètres pour un environnement de développement. |

## Paramètres du gabarit

Tous les paramètres du gabarit sont obligatoires. La plupart d'entre eux ont des valeurs par défaut, mais certains n'en ont pas. Ils doivent être fournis lors de l'instanciation avec 'oc process'.

Le fichier de paramètres permet la personnalisation de l'installation pour un environnement particulier (par exemple).

Commencer par créer un projet sur OpenShift:
```bash
oc new-project ssi-studio
```
Lancez l'installation sur OpenShift
```bash
oc process -f ./ssi-studio.yaml --param-file=./ssi-studio.dev.params | oc apply -f -
```

Une fois que tous les pods sont démarrés, vous pouvez accéder à l'application à l'adresse https://ssi-studio.<APP_DOMAIN>.

| Paramètre | Description | Défaut      |
| --------- | ----------- | ----------- |
| **APP_NAME** | Nom utilisé pourregrouper les composantes ensembles dans la console OpenShift. | ssi-studio |
| **APP_DOMAIN** | Le nom de domaine externe pour accéder à l'application. | |
| **APP_SUBDOMAIN** | Le nom de sous domaine pour accéder à l'application. | ssi-studio |
| **POSTGRESQL_USERNAME** | Nom d'utilisateur PostgreSQL. | dbuser |
| **POSTGRESQL_PASSWORD** | Mot de passe de l'utilisateur PostgreSQL. | {auto-généré} |
| **POSTGRESQL_ADMIN_USERNAME** | Nom d'utilisateur de l'administrateur PostgreSQL. | postgres |
| **POSTGRESQL_ADMIN_PASSWORD** | Mot de passe de l'utilisateur administrateur PostgreSQL. | {auto-généré} |
| **POSTGRESQL_DATABASE_NAME** | Nom de la base de données de l'application. | ssi-studio |
| **POSTGRESQL_PORT** | Numéro de port sur lequel PostgreSQL écoute. | 5432 |
| **POSTGRESQL_NAME** | Nom assigné à tous les objets PostgreSQL déployés par le gabarit. | postgres-database |
| **POSTGRESQL_VOLUME_SIZE** | Capacité du volume persistant PostgreSQL. | 1Gi |
| **NESTJS_NAME** |  Nom assigné à tous les objets NestJs déployés par le gabarit. | nestjs-backend |
| **ANGULAR_NAME** |  Nom assigné à tous les objets Angular déployés par le gabarit. | angular-frontend |
| **KEYCLOAK_SUBDOMAIN** | Le nom de sous domaine pour accéder à Keycloak. | ssi-studio-keycloak |
| **KEYCLOAK_ADMIN_USER** | Nom d'utilisateur de l'administrateur Keycloak. | admin |
| **KEYCLOAK_ADMIN_PASSWORD** | Mot de passe de l'utilisateur administrateur Keycloak. | {auto-généré} |
| **KEYCLOAK_REALM** | Nom du domain keycloak de l'application | SSI-Studio |
| **KEYCLOAK_CLIENT_ID** |  Nom assigné à tous les objets NestJs déployés par le gabarit. | angular-app |
| **KEYCLOAK_DATABASE_NAME** | Nom de la base de données de Keycloak. | keycloak |
| **GITHUB_REPOSITORY_URI** | Uri du dépôt de code de l'application. | https://github.com/CQEN-QDCE/ssi-studio.git |
| **STORAGE_CLASS_NAME** | Nom de la classes de stockage utilisée par les volumes. | gp2 |
| **NGINX_PORT** | Numéro de port sur lequel NGINX écoute. | 8080 |


