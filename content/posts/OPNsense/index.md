---
title: "Booster OPNsense avec une liste d'IPs"
date: 2026-05-27
draft: true
image: image.jpg
tags:
  - project
  - security
  - story
  - homelab
  - firewall
---

J'ai vu passer il y a quelques temps un article sur [Data‑Shield IPv4 Blocklist Community](https://github.com/duggytuxy/Data-Shield_IPv4_Blocklist#). Un projet communautaire qui construit une liste d'une centaine d'IPs malveillantes. Cette liste peut alors être utilisée par tout le monde pour protéger ses serveurs en blocant tout accès depuis les adresses qu'elle contient. La retention est de 15 jours, ce qui permet de garder le nombre d'IPs raisonable et de ne pas surcharger le serveur.
Bien qu'ayant trouvé l'idée très intéressante, la mise en place me parraissait inutile sur mon lab car trop peu exposé. Mais lors d'un détour par l'administration Proxmox à la recherche de logs, je découvre qu'il subit en permanence des tentative de connexions ssh. Je réalise alors 3 choses : 
 * Je n'ai pas installé fail2ban sur ce serveur
 * Je n'ai pas désactivé la connection par mot de passe en ssh 
 * Je subis des attaques malgré la faible visibilité de mon serveur

Ayant déjà OPNsense installé, ajouter cette liste dynamique ne me coute finalement pas grand chose et permettra même de justifier de sa présence.
Je ne vais pas tout détailler ici, de toute façon je n'invente rien et je vais absolument tout pomper de la procédure [indiquée par le projet](https://github.com/duggytuxy/Data-Shield_IPv4_Blocklist#community--vendor-tutorials) pour OPNsense.

Je ne verrais sûrement aucune différence sur mon serveur mais au moins les VMs auront une protection supplémentaire.
Proxmox maintenant, il héberge Opnsense et ne peut donc pas bénéficier de cette liste.