# Linux Image Ansible

[![CI](https://github.com/lacrif/docker-debian-systemd/actions/workflows/ci.yml/badge.svg)](https://github.com/lacrif/docker-debian-systemd/actions/workflows/ci.yml) 
[![Docker pulls](https://img.shields.io/docker/pulls/lacrif/debian-systemd)](https://hub.docker.com/r/lacrif/debian-systemd/)

## Description

Ce repository fournit des conteneurs Docker spécialement conçus pour tester des playbooks et rôles Ansible dans un environnement isolé et contrôlé. Ces images sont particulièrement utiles pour l'intégration continue (CI) et les tests automatisés avec des outils comme Jenkins et Travis CI.

## Prérequis

Docker installé sur votre système
Connaissances de base d'Ansible et Docker

## Installation

### Depuis Docker Hub

``` bash
docker pull lacrif/debian-systemd:<version>
```

Remplacez <version> par la version souhaitée : 'bookworm','trixie'

## Utilisation

### Molecule

Ajoutez le code suivant à votre fichier de scénario Molecule, par exemple dans molecule/default/molecule.yml.

```yaml
platforms:
  - name: instance
    image: lacrif/debian-systemd:bookworm
    tmpfs:
      - /run
      - /tmp
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:rw
    cgroupns_mode: host
    privileged: true
    pre_build_image: true
```

### Démarrage du conteneur

Exécuter un conteneur à partir de l'image :

```bash
docker run -d -it --name debian-bookworm-systemd --privileged --cgroupns=host --tmpfs=/run --tmpfs=/tmp --volume=/sys/fs/cgroup:/sys/fs/cgroup:rw lacrif/debian-systemd:bookworm
```

Utilisez-le, exemple :

```bash
docker exec -it debian-bookworm-systemd /bin/bash
```

## Auteur

[![Static Badge](https://img.shields.io/badge/Lacrif-0000?style=flat&logo=github&logoColor=white&color=black&link=https%3A%2F%2Fgithub.com%2Flacrif)](https://github.com/lacrif)

