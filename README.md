# adminsys-da2i-projet2
## Projet d'Administration Système (Licence DA2I)
### Edouard CATTEZ

---------------------

## Sommaire

- Introduction
  - Présentation
  - Installation
- Script de backup
  - Sauvegarde
  - Restauration

# Introduction

## Présentation

Backup est un système de sauvegarde incrémental de vos données. Vous pouvez également restaurer à tout moment la sauvegarde de votre choix.

Dans ce projet, nous allons utiliser une machine virtuelle préalablement créée avec Linux Debian tout en respectant le [**sujet du projet**](http://moodle.univ-lille1.fr/pluginfile.php/18443/mod_resource/content/4/sujet-2.txt).

## Installation

- Créer deux disques avec vmplayer de 1 Go (sdb, sdc)
- Lister les disques/partitions: `fdisk -l`

Ouvrez un terminal et suivez les étapes suivantes (assurez-vous d'avoir les droits d'exécution des commandes) :

```
apt-get install rsync

fdisk /dev/sdb (2 partitions de 500M)
fdisk /dev/sdc (1 partition de 1Go)

mkfs.ext3 /dev/sdc1
mkfs.ext3 /dev/sdb1

mount /dev/sdc1 /srv
mount /dev/sdb1 /home
```

Pour finir, éditez le fichier /etc/fstab et insérez les lignes ci-après :

```
/dev/sdc1	/srv	ext3	defaults	1 2
/dev/sdb1	/home	ext3	defaults	1 2
```

# Script de backup

Commande: `./backup [ start | stop ] [ -h ] [ -r <nb> ] [ -e <ssh> ]`

| Option | Argument | Description |
|:-------|:---------|:------------|
| start | - | Démarre le daemon |
| stop | - | Arrête le daemon |
| -h | - | Affiche l'aide |
| -r | `<nb>` | Mode restauration avec le numéro de la sauvegarde à restaurer |
| -e | `<ssh>` | Sauvegarde vers un dossier distant / Restaure depuis un dossier distant |

Le script s'appuie sur certaines commandes shell.

| Commande | Description |
|:---------|:------------|
| `rsync -azvu <source> <destination>` | Sauvegarde un dossier source vers un dossier de destination |
| `crontab -l` | Liste la table des planifications |
| `crontab -e` | Edite la table des planifications |

Une ligne de la crontab est définie comme suit :

```
* * * * * <absolute/path/to/command>
```

Chaque étoile correspond à une échelle de temps (minutes, heures...)

**Exemple**

| Ligne | Description |
|:---------|:------------|
| `*/2 * * * 1-5 /<backup_script>` | Exécute le script de backup toutes les 2 minutes du lundi au vendredi |

## Sauvegarde

TODO

## Restauration

TODO
