FROM debian:bookworm

# Metadata
LABEL maintainer="Lacrif"

# Variables d'environnement
ENV container=docker
ENV DEBIAN_FRONTEND=noninteractive

# Installation et nettoyage en une seule couche pour minimiser la taille
RUN apt-get update \
    # Installation des dépendances minimales
    && apt-get install -y --no-install-recommends \
        python3 \
        systemd \
        systemd-sysv \
    # Nettoyage complet des caches et fichiers temporaires
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /usr/share/doc \
    && rm -rf /usr/share/man \
    && rm -rf /usr/share/info \
    && rm -rf /usr/share/lintian \
    && rm -rf /var/cache/debconf \
    && rm -rf /tmp/* \
    && rm -rf /var/tmp/*

# selectively remove systemd targets -- See https://hub.docker.com/_/centos/
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
    systemd-tmpfiles-setup.service ] || rm -f $i; done); \
    rm -f /lib/systemd/system/multi-user.target.wants/*;\
    rm -f /etc/systemd/system/*.wants/*;\
    rm -f /lib/systemd/system/local-fs.target.wants/*; \
    rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
    rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
    rm -f /lib/systemd/system/basic.target.wants/*;\
    rm -f /lib/systemd/system/anaconda.target.wants/*;

# VOLUME & CMD
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]
