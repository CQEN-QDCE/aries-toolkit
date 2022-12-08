# Déployer un agent vérificateur Aries sur OpenShift

Ce dépôt contient les instructions nécessaires pour déployer un agent vérificateur Aries sur OpenShift.

| Gabarit  | Descripton |
| -------- | ---------- |
| [aries-verifier.yaml](https://github.com/CQEN-QDCE/aries-toolkit/blob/master/openshift/templates/verifier/aries-verifier.yaml) | Installation de l'agent. |
| [aries-verifier.candy-dev.params](https://github.com/CQEN-QDCE/aries-toolkit/blob/master/openshift/templates/verifier/aries-verifier.candy-dev.params) | Paramètres pour un environnement de développement. |

## Paramètres du gabarit

La majorité des paramètres du modèle sont obligatoires. La plupart d'entre eux ont des valeurs par défaut, mais certains n'en ont pas. Ils doivent être fournis lors de l'instanciation avec 'oc process'.

```
APP_DOMAIN=
ACAPY_LABEL=
WALLET_ENCRYPTION_KEY=
GENESIS_FILE_URL=
POSTGRESQL_PASSWORD=
```

Le fichier de paramètres permet la personnalisation de l'installation pour un environnement particulier (par exemple).

Commencer par créer un projet sur OpenShift:
```bash
oc new-project aries-toolkit
```
Lancez l'installation sur OpenShift
```bash
oc process -f ./aries-verifier.yaml --param-file=./aries-verifier.candy-dev.params | oc apply -f -
```

Une fois que tous les pods sont démarrés, vous pouvez accéder à l'agent à l'adresse https://aries-verifier.<APP_DOMAIN>.

| Paramètre | Description | Défaut      |
| --------- | ----------- | ----------- |
| **ENV_NAME** | Nom de l'environnement (ex: development, staging, production). | development |
| **APP_NAME** | Nom utilisé pour regrouper les composantes ensembles dans la console OpenShift. | aries-verifier |
| **APP_GROUP** | Utilisé pour regrouper les composants. | aries-verifier |
| **SUFFIX** | Un suffixe appliqué à tous les objets de ce modèle. | |
| **ROLE** | Le rôle de ce service dans l'application - utilisé pour les politiques de réseau. | agent |
| **API_ROLE** | Le rôle du service api au sein de l'application - utilisé pour les politiques de réseau. | api |
| **APP_DOMAIN** | Le nom de domaine externe pour accéder à l'application. | |
| **AGENT_SUBDOMAIN** | Le nom de sous domaine pour accéder à l'agent émetteur Aries. | aries-verifier |
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
| **ACAPY_LABEL** | Libellé de l'agent. | Aries Verifier |
| **ACAPY_IMAGE_URL** | L'URL de l'image pour l'agent. |  |
| **AGENT_HTTP_PORT** | Port sur lequel l'agent écoute. |  |
| **LOG_LEVEL** | Le niveau de journalisation de l'agent émetteur. | DEBUG |
| **GENESIS_FILE_URL** | L'URL à partir de laquelle le fichier genesis peut être téléchargé. |  |
| **STORAGE_CLASS_NAME** | Nom de la classes de stockage utilisée par les volumes. | gp2 |
| **POSTGRESQL_VOLUME_SIZE** | Capacité du volume persistant de la base de données PostgreSQL. | 1Gi |
| **ROUTE_TIMEOUT** | Le délai d'attente pour la route de l'application.  Lorsque ce délai est dépassé, la route de l'application répondra par une erreur 504 Gateway Timeout. | 120s |
| **CPU_REQUEST** | La demande de ressources CPU (en cœurs) pour ce build. | 100m |
| **CPU_LIMIT** | La limite de ressources CPU (en cœurs) pour cette construction. | 250m |
| **MEMORY_REQUEST** | Les ressources que la mémoire demande (en Mi, Gi, etc.) pour cette construction. | 128Mi |
| **MEMORY_LIMIT** | La limite de mémoire des ressources (en Mi, Gi, etc.) pour cette construction. | 256Mi |

