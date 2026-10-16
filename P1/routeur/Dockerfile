# Image routeur : FRRouting (zebra, bgpd, ospfd, isisd), base Alpine donc busybox inclus
FROM frrouting/frr:latest

# Active les demons demandes par le sujet
RUN sed -i 's/^bgpd=no/bgpd=yes/; s/^ospfd=no/ospfd=yes/; s/^isisd=no/isisd=yes/' /etc/frr/daemons

# Outils utiles pour les parties 2 et 3 (bridge, vxlan)
RUN apk add --no-cache bridge-utils iproute2 tcpdump

# Lance FRR en arriere-plan puis laisse un shell au premier plan pour la console GNS3
RUN printf '#!/bin/sh\n/usr/lib/frr/docker-start &\nexec /bin/sh\n' > /start.sh && chmod +x /start.sh
CMD ["/start.sh"]