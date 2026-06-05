---
title: "Mon lab était une passoire"
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

J'ai vu passer il y a quelques temps un article sur [Data‑Shield IPv4 Blocklist Community](https://github.com/duggytuxy/Data-Shield_IPv4_Blocklist#). Un projet communautaire qui construit une liste d'une centaine d'IPs malveillantes. Cette liste peut alors être utilisée par tout le monde pour protéger ses serveurs en bloquant tout accès depuis les adresses qu'elle contient. La retention est de 15 jours, ce qui permet de garder le nombre d'IPs raisonnable et de ne pas surcharger le serveur.
Bien qu'ayant trouvé l'idée très intéressante, la mise en place me paraissait inutile sur mon lab car trop peu exposé. Mais lors d'un détour par l'administration Proxmox à la recherche de logs, je découvre qu'il subit en permanence des tentatives de connexions ssh. Je réalise alors 3 choses : 
 * Je n'ai pas installé fail2ban sur ce serveur
 * Je n'ai pas désactivé la connection par mot de passe en ssh 
 * Je subis des attaques malgré la faible visibilité de mon serveur

Au niveau des VMs tout passe par OPNsense que j’ai déjà installé, ajouter cette liste dynamique ne me coute finalement pas grand chose et permettra même de justifier de la présence du firewall.
Je ne vais pas tout détailler ici, de toute façon je n'invente rien et je vais absolument tout pomper de la procédure [indiquée par le projet](https://github.com/duggytuxy/Data-Shield_IPv4_Blocklist#community--vendor-tutorials) pour OPNsense.

OPNsense étant hébergé sur une VM, Proxmox n’en bénéficie pas. Je vais donc sécuriser ce point.
Proxmox intègre un pare-feu, somme toute très bien mais qui ne gère pas les liste d’ip dynamique via une url. Je vais donc rester sur des points basique mais nécessaire.
 * Refuser les connexions ssh avec password,
 * Installation de fail2ban avec jail ssh et jail interface web proxmox,
  *la jail ssh est rendu inutile par la connexion avec certificat obligatoire mais je la met par principe*
 * Mise en place de la MFA sur l’accès web Proxmox (TOTP et WebAuth)
 * Vérification de l’activation de unattended-upgrade pour bénéficier des mises à jour de sécurité automatiquement.

 