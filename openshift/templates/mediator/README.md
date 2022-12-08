# Déployer un agent médiateur Aries sur OpenShift

Ce dépôt contient les instructions nécessaires pour déployer un agent médiateur Aries sur OpenShift.

| Gabarit  | Descripton |
| -------- | ---------- |
| [aries-mediator.yaml](https://github.com/CQEN-QDCE/aries-toolkit/blob/master/openshift/templates/mediator/aries-mediator.yaml) | Installation de l'agent. |
| [aries-mediator.candy-dev.params](https://github.com/CQEN-QDCE/aries-toolkit/blob/master/openshift/templates/mediator/aries-mediator.candy-dev.params) | Paramètres pour un environnement de développement. |

## Paramètres du gabarit

Tous les paramètres du gabarit sont obligatoires. La plupart d'entre eux ont des valeurs par défaut, mais certains n'en ont pas. Ils doivent être fournis lors de l'instanciation avec 'oc process'.

Le fichier de paramètres permet la personnalisation de l'installation pour un environnement particulier (par exemple).

Commencer par créer un projet sur OpenShift:
```bash
oc new-project aries-mediator
```
Lancez l'installation sur OpenShift
```bash
oc process -f ./aries-mediator.yaml --param-file=./aries-mediator.candy-dev.params | oc apply -f -
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
| **POSTGRESQL_PORT** | Port sur lequel PostgreSQL écoute. | 5432 |
| **WALLET_STORAGE_TYPE** | Le type de stockage du portefeuille. Les valeurs possibles sont 'postgres_storage' ou 'sqlite_storage' pour le moment. | postgres_storage |
| **AGENT_ADMIN_PORT** | Numéro de port sur lequel l'agent écoute pour servir l'API d'administration. | 3000 |
| **WALLET_ENCRYPTION_KEY** | Clé de chiffrement è utiliser pour encrypter le portefeuille de l'agent. | {auto-généré} |
| **ACAPY_AUTO_ACCEPT_INVITES** | | |
| **WALLET_TYPE** | Le type de portfeuille. Les types internes pris en charge sont "basic", "indy" et "askar". | askar |
| **WALLET_STORAGE_CONFIG** | Configuration du stockage du portfeuille. |  |
| **WALLET_STORAGE_CREDS** | Les identifiants de stockage du portefeuille. |  |
| **ACAPY_NAME** | Nom attribué à tous les objets de l'agent ACA-Py définis dans ce modèle. | acapy |
| **ACAPY_LABEL** | Libellé de l'agent. | Aries issuer |
| **ACAPY_IMAGE_URL** | L'URL de l'image pour l'agent. |  |
| **AGENT_HTTP_PORT** | Port sur lequel l'agent écoute. |  |
| **LOG_LEVEL** | Le niveau de journalisation de l'agent émetteur. | DEBUG |
| **TAILS_SERVER_NAME** | Nom attribué à tous les objets du serveur de queues définis dans ce modèle. | tails-server |
| **TAILS_SERVER_PORT** | Port sur lequel le serveur de queues écoute. | 6543 |
| **AGENT_DID_SEED** | Valeur utilisée pour créer l'agent DID. |  |
| **AGENT_DID** | Le DID public associé à l'agent. |  |
| **GENESIS_FILE_URL** | L'URL à partir de laquelle le fichier genesis peut être téléchargé. |  |
| **STORAGE_CLASS_NAME** | Nom de la classes de stockage utilisée par les volumes. | gp2 |
| **TAILS_SERVER_VOLUME_SIZE** | Capacité du volume persistant pour le server de queues. | 1Gi |
| **POSTGRESQL_VOLUME_SIZE** | Capacité du volume persistant de la base de données PostgreSQL. | 1Gi |
| **ROUTE_TIMEOUT** | Le délai d'attente pour la route de l'application.  Lorsque ce délai est dépassé, la route de l'application répondra par une erreur 504 Gateway Timeout. | 120s |
| **CPU_REQUEST** | La demande de ressources CPU (en cœurs) pour ce build. | 100m |
| **CPU_LIMIT** | La limite de ressources CPU (en cœurs) pour cette construction. | 250m |
| **MEMORY_REQUEST** | Les ressources que la mémoire demande (en Mi, Gi, etc.) pour cette construction. | 128Mi |
| **MEMORY_LIMIT** | La limite de mémoire des ressources (en Mi, Gi, etc.) pour cette construction. | 256Mi |

# Déployer un agent médiateur Aries sur OpenShift

Ce dépôt contient les instructions nécessaires pour déployer un agent médiateur Aries sur OpenShift.

| Gabarit  | Descripton |
| -------- | ---------- |
| [aries-mediator.yaml](https://github.com/CQEN-QDCE/aries-toolkit/blob/master/openshift/templates/mediator/aries-mediator.yaml) | Installation de l'agent. |
| [aries-mediator.candy-dev.params](https://github.com/CQEN-QDCE/aries-toolkit/blob/master/openshift/templates/mediator/aries-mediator.candy-dev.params) | Paramètres pour un environnement de développement. |

## Paramètres du gabarit

Tous les paramètres du gabarit sont obligatoires. La plupart d'entre eux ont des valeurs par défaut, mais certains n'en ont pas. Ils doivent être fournis lors de l'instanciation avec 'oc process'.

Le fichier de paramètres permet la personnalisation de l'installation pour un environnement particulier (par exemple).

Commencer par créer un projet sur OpenShift:
```bash
oc new-project aries-mediator
```
Lancez l'installation sur OpenShift
```bash
oc process -f ./aries-mediator.yaml --param-file=./aries-mediator.candy-dev.params | oc apply -f -
```

Une fois que tous les pods sont démarrés, vous pouvez accéder à l'agent à l'adresse https://aries-mediator.<APP_DOMAIN>.

| Paramètre | Description | Défaut      |
| --------- | ----------- | ----------- |
| **ENV_NAME** | Nom de l'environnement (ex: development, staging, production). | development |
| **APP_NAME** | Nom utilisé pour regrouper les composantes ensembles dans la console OpenShift. | aries-issuer |
| **APP_GROUP** | Utilisé pour regrouper les composants. | aries-issuer |
| **SUFFIX** | Un suffixe appliqué à tous les objets de ce modèle. | |
| **APP_DOMAIN** | Le nom de domaine externe pour accéder à l'agent. | |
| **AGENT_SUBDOMAIN** | Le nom de sous domaine pour accéder à l'agent émetteur Aries. | aries-issuer |
| **POSTGRESQL_NAME** | Nom attribué à tous les objets PostgreSQL définis dans ce modèle. | postgres-database |
| **POSTGRESQL_ROLE** | Le rôle de PostgreSql au sein de l'application - utilisé pour les politiques de réseau. | database |
| **POSTGRESQL_PASSWORD** | Mot de passe de l'utilisateur PostgreSQL. | {auto-généré} |
| **POSTGRESQL_ADMIN_PASSWORD** | Mot de passe de l'utilisateur administrateur PostgreSQL. | {auto-généré} |
| **POSTGRESQL_DATABASE_NAME** | Nom de la base de données de l'agent. | wallet |
| **POSTGRESQL_PORT** | Port sur lequel PostgreSQL écoute. | 5432 |
| **POSTGRESQL_VOLUME_SIZE** | Capacité du volume persistant de la base de données PostgreSQL. | 1Gi |
| **ACAPY_NAME** | Nom attribué à tous les objets de l'agent ACA-Py définis dans ce modèle. | acapy |
| **ACAPY_ROLE** | Le rôle d'ACA-Py au sein de l'application - utilisé pour les politiques de réseau. | aries-mediator-agent |
| **ACAPY_LABEL** | Libellé de l'agent. | Aries mediator |
| **ACAPY_AUTO_ACCEPT_INVITES** | false |
| **ACAPY_IMAGE_URL** | L'URL de l'image pour l'agent. |  |
| **WALLET_STORAGE_TYPE** | Le type de stockage du portefeuille. Les valeurs possibles sont 'postgres_storage' ou 'sqlite_storage' pour le moment. | postgres_storage |
| **AGENT_ADMIN_PORT** | Numéro de port sur lequel l'agent écoute pour servir l'API d'administration. | 3000 |
| **WALLET_ENCRYPTION_KEY** | Clé de chiffrement è utiliser pour encrypter le portefeuille de l'agent. | {auto-généré} |
| **WALLET_TYPE** | Le type de portfeuille. Les types internes pris en charge sont "basic", "indy" et "askar". | askar |
| **WALLET_STORAGE_CONFIG** | Configuration du stockage du portfeuille. |  |
| **WALLET_STORAGE_CREDS** | Les identifiants de stockage du portefeuille. |  |
| **AGENT_HTTP_PORT** | Port sur lequel l'agent écoute. | 8000 |
| **AGENT_WS_PORT** | Port sur lequel l'agent écoute. | 8001 |
| **CADDY_NAME** | Nom attribué à tous les objets de l'agent ACA-Py définis dans ce modèle. | caddy-proxy |
| **CADDY_ROLE** | Le rôle de Caddy au sein de l'application - utilisé pour les politiques de réseau. | reverse-proxy |
| **CADDY_HTTP_PORT** | Port HTTP sur lequel Caddy écoute. | 80 |
| **CADDY_HTTPS_PORT** | Port HTTPS sur lequel Caddy écoute. | 443 |
| **CADDY_HTTP_DEFAULT_PORT** | Port HTTP par défaut sur lequel Caddy écoute. | 2015 |
| **LOG_LEVEL** | Le niveau de journalisation de l'agent émetteur. | DEBUG |
| **ROUTE_TIMEOUT** | Le délai d'attente pour la route de l'application.  Lorsque ce délai est dépassé, la route de l'application répondra par une erreur 504 Gateway Timeout. | 120s |
| **CPU_REQUEST** | La demande de ressources CPU (en cœurs) pour ce build. | 100m |
| **CPU_LIMIT** | La limite de ressources CPU (en cœurs) pour cette construction. | 250m |
| **MEMORY_REQUEST** | Les ressources que la mémoire demande (en Mi, Gi, etc.) pour cette construction. | 128Mi |
| **MEMORY_LIMIT** | La limite de mémoire des ressources (en Mi, Gi, etc.) pour cette construction. | 256Mi |
