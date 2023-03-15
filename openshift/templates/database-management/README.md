# Déployer l'outil de gestion de base de données OmniDB sur OpenShift

Ce dépôt contient les instructions nécessaires pour déployer l'outil de gestion de base de données OmniDB sur OpenShift.

| Gabarit  | Descripton |
| -------- | ---------- |
| [omnidb.yaml](https://github.com/CQEN-QDCE/aries-toolkit/blob/master/openshift/templates/database-management/omnidb.yaml) | Installation d'OmniDB. |
| [omnidb.params](https://github.com/CQEN-QDCE/aries-toolkit/blob/master/openshift/templates/database-management/omnidb.params) | Paramètres d'installation. |

## Paramètres du gabarit

Tous les paramètres du gabarit sont obligatoires. La plupart d'entre eux ont des valeurs par défaut, mais certains n'en ont pas. Ils doivent être fournis lors de l'instanciation avec 'oc process'.

Le fichier de paramètres permet la personnalisation de l'installation.

Commencer par créer un projet sur OpenShift:
```bash
oc new-project omnidb
```
Lancez l'installation sur OpenShift
```bash
oc process -f ./omnidb.yaml --param-file=./omni.params | oc apply -f -
```

Une fois que tous les pods sont démarrés, vous pouvez accéder à l'agent à l'adresse https://omnidb.<APP_DOMAIN>.

| Paramètre | Description | Défaut      |
| --------- | ----------- | ----------- |
| **APP_NAME** | Nom utilisé pour regrouper les composantes ensembles dans la console OpenShift. | omnidb |
| **APP_DOMAIN** | Le nom de domaine externe pour accéder à l'application. | |
| **OMNIDB_NAME** | Nom attribué à tous les objets OmniDB définis dans ce modèle. | omnidb |
| **OMNIDB_PORT** | Numéro de port sur lequel l'application écoute. | 8080 |
| **STORAGE_CLASS_NAME** | Nom de la classes de stockage utilisée par les volumes. | gp2 |
| **OMNIDB_VOLUME_SIZE** | Capacité du volume persistant de l'application. | 128Mi |
