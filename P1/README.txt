# Project P1 - BADASS

Created on: 2026-10-12

Author: calleaum

## Description

Partie 1 du projet BADASS : mise en place de GNS3 avec deux images Docker.

host-calleaum : image Alpine (busybox inclus) avec quelques outils réseau
 (iproute2, bridge-utils, tcpdump, iputils).

routeur-calleaum : image basée sur FRRouting avec zebra, bgpd, ospfd, isisd
  et busybox. Un script `/start.sh` lance FRR en arrière-plan puis laisse
  un shell au premier plan pour la console GNS3.

Aucune IP configurée par défaut sur le host et le routeur.

## Particularités de la VM

- "default-ulimits" (nofile 1024) dans `/etc/docker/daemon.json` : sans cela,
  FRR 8.4 (watchfrr) tente d'allouer 32 Gio et échoue avec "Out of memory".
- "busybox-static" installé sur la VM : GNS3 l'injecte dans les conteneurs.
- uBridge compilé à la main (absent des dépôts Debian 13) avec les capacités
  réseau via "setcap".