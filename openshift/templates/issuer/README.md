# Déployer un agent émetteur Aries sur OpenShift

Ce dépôt contient les instructions nécessaires pour déployer un agent émetteur Aries sur OpenShift. L'agent supporte la révocation.

| Gabarit  | Descripton |
| -------- | ---------- |
| [aries-issuer.yaml](https://github.com/CQEN-QDCE/aries-toolkit/blob/master/openshift/templates/issuer/aries-issuer.yaml) | Installation de l'application. |
| [aries-issuer.candy-dev.params](https://github.com/CQEN-QDCE/aries-toolkit/blob/master/openshift/templates/issuer/aries-issuer.candy-dev.params) | Paramètres pour un environnement de développement. |

## Paramètres du gabarit

Tous les paramètres du gabarit sont obligatoires. La plupart d'entre eux ont des valeurs par défaut, mais certains n'en ont pas. Ils doivent être fournis lors de l'instanciation avec 'oc process'.

Le fichier de paramètres permet la personnalisation de l'installation pour un environnement particulier (par exemple).

Commencer par créer un projet sur OpenShift:
```bash
oc new-project aries-toolkit
```
Lancez l'installation sur OpenShift
```bash
oc process -f ./aries-issuer.yaml --param-file=./aries-issuer.candy-dev.params | oc apply -f -
```

Une fois que tous les pods sont démarrés, vous pouvez accéder à l'agent à l'adresse https://aries-issuer.<APP_DOMAIN>.

| Paramètre | Description | Défaut      |
| --------- | ----------- | ----------- |
| **ENV_NAME** | Nom de l'environnement (ex: development, staging, production). | development |
| **APP_NAME** | Nom utilisé pour regrouper les composantes ensembles dans la console OpenShift. | aries-issuer |
| **APP_GROUP** | Utilisé pour regrouper les composants. | aries-issuer |
| **SUFFIX** | Un suffixe appliqué à tous les objets de ce modèle. | |
| **ROLE** | Le rôle de ce service dans l'application - utilisé pour les politiques de réseau. | agent |
| **API_ROLE** | Le rôle du service api au sein de l'application - utilisé pour les politiques de réseau. | api |
| **APP_DOMAIN** | Le nom de domaine externe pour accéder à l'application. | |
| **AGENT_SUBDOMAIN** | Le nom de sous domaine pour accéder à l'agent émetteur Aries. | aries-issuer |
| **TAILS_SERVER_SUBDOMAIN** | Le nom de sous domaine pour accéder au serveur de queues. | aries-issuer-tails |
| **POSTGRESQL_NAME** | Nom attribué à tous les objets PostgreSQL définis dans ce modèle. | postgres-database |
| **POSTGRESQL_PASSWORD** | Mot de passe de l'utilisateur PostgreSQL. | {auto-généré} |
| **POSTGRESQL_ADMIN_PASSWORD** | Mot de passe de l'utilisateur administrateur PostgreSQL. | {auto-généré} |
| **POSTGRESQL_DATABASE_NAME** | Nom de la base de données de l'agent. | wallet |
| **POSTGRESQL_PORT** | Numéro de port sur lequel PostgreSQL écoute. | 5432 |
| **WALLET_STORAGE_TYPE** | Le type de stockage du portefeuille. Les valeurs possibles sont 'postgres_storage' ou 'sqlite_storage' pour le moment. | postgres_storage |
| **AGENT_ADMIN_PORT** | Numéro de port sur lequel l'agent écoute pour servir l'API d'administration. | 3000 |
| **WALLET_ENCRYPTION_KEY** | Clé de chiffrement è utiliser pour encrypter le portefeuille de l'agent. | {auto-généré} |
| **ACAPY_AUTO_ACCEPT_INVITES** | | |
| **WALLET_TYPE** | Le type de portfeuille. Les types internes pris en charge sont "basic", "indy" et "askar". | askar |
| **WALLET_STORAGE_CONFIG** | Configuration du stockage du portfeuille. |  |
| **WALLET_STORAGE_CREDS** | Les identifiants de stockage du portefeuille. |  |


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


