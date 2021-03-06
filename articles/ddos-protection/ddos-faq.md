---
title: Questions fréquemment posées sur le service Azure DDoS Protection standard
description: Forum aux questions sur Azure DDoS Protection Standard, qui contribue à assurer la défense contre les attaques DDoS.
services: virtual-network
documentationcenter: na
author: yitoh
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/28/2020
ms.author: yitoh
ms.openlocfilehash: 6c475971f604c951280d0351d593cd5d96879d31
ms.sourcegitcommit: 9889a3983b88222c30275fd0cfe60807976fd65b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/20/2020
ms.locfileid: "94992401"
---
# <a name="azure-ddos-protection-standard-frequent-asked-questions"></a>Questions fréquemment posées sur le service Azure DDoS Protection standard

Cet article répond aux questions courantes sur le service Azure DDoS Protection standard. 

## <a name="what-is-a-distributed-denial-of-service-ddos-attack"></a>Qu’est-ce qu’une attaque par déni de service distribué (Distributed Denial of Service, DDoS) ?
Le déni de service distribué, ou DDoS, est un type d’attaque dans lequel une personne malveillante envoie plus de demandes à une application que l’application ne peut en gérer. Cela aboutit à un épuisement des ressources qui affecte la disponibilité et la capacité de l’application à servir ses clients. Ces dernières années, le secteur a constaté une forte augmentation des attaques, celles-ci gagnant en sophistication et en ampleur. Les attaques DDoS peuvent être ciblées sur n’importe quel point de terminaison qui est publiquement accessible via Internet.

## <a name="what-is-azure-ddos-protection-standard-service"></a>Qu’est-ce que le service Azure DDoS Protection standard ?
Azure DDoS Protection Standard, combiné aux meilleures pratiques de conception d’application, offre des fonctions d’atténuation DDoS améliorée contre les attaques DDoS. Cette solution s’adapte automatiquement pour protéger vos ressources Azure spécifiques dans un réseau virtuel. La protection est simple à activer sur n’importe quel réseau virtuel, nouveau ou existant, et ne nécessite aucun changement au niveau de l’application ou des ressources. Elle offre plusieurs avantages par rapport au service de base, notamment la journalisation, la création d’alertes et la télémétrie. Consultez [Vue d’ensemble d’Azure DDoS Protection Standard](ddos-protection-overview.md) pour plus de détails. 

## <a name="what-about-protection-at-the-service-layer-layer-7"></a>Qu’en est-il de la protection au niveau de la couche de service (couche 7) ?
Les clients peuvent utiliser le service Azure DDoS Protection conjointement avec la [référence SKU WAF Application Gateway](../web-application-firewall/ag/ag-overview.md) pour la protection tant au niveau de la couche réseau (couches 3 et 4, assurée par le service Azure DDoS Protection) qu’au niveau de la couche Application (couche 7, assurée par la référence SKU WAF Application Gateway).

## <a name="are-services-unsafe-in-azure-without-the-service"></a>Les services ne sont-ils pas sûrs dans Azure sans le service ?
Les services qui s’exécutent sur Azure sont protégés intrinsèquement par le service Azure DDoS Protection de base en place pour protéger l’infrastructure d’Azure. Toutefois, la protection qui préserve l’infrastructure a un seuil sensiblement supérieur à celui que la plupart des applications sont capables de gérer, et ne fournit pas de télémétrie ou d’alertes. Ainsi, si un volume de trafic peut être considéré comme inoffensif par la plateforme, il peut s’avérer dévastateur pour l’application qui le reçoit. 

Grâce à l’intégration au service Azure DDoS Protection standard, l’application bénéficie d’une surveillance dédiée pour détecter les attaques et les seuils spécifiques des applications. Un service est protégé à l’aide d’un profil réglé sur le volume de trafic attendu, ce qui offre une protection plus rigoureuse contre les attaques DDoS.

## <a name="what-are-the-supported-protected-resource-types"></a>Quels sont les types de ressources protégées pris en charge ?
Les adresses IP publiques dans les réseaux virtuels ARM sont actuellement le seul type de ressource protégée. Les services PaaS (mutualisés) ne sont pas pris en charge actuellement. Consultez [Architectures de référence du service Azure DDoS Protection standard](ddos-protection-reference-architectures.md) pour plus de détails.

## <a name="are-classicrdfe-protected-resources-supported"></a>Les ressources protégées classiques/RDFE sont-elles prises en charge ?
Seules les ressources protégées basées sur ARM sont prises en charge dans la préversion. Les machines virtuelles dans les déploiements classiques/RDFE ne sont pas prises en charge. La prise en charge n’est pas actuellement planifiée pour les ressources classiques/RDFE. Consultez [Architectures de référence du service Azure DDoS Protection standard](ddos-protection-reference-architectures.md) pour plus de détails.

## <a name="can-i-protect-my-on-premise-resources-using-ddos-protection"></a>Puis-je protéger mes ressources locales à l’aide de la protection DDoS ?
Les points de terminaison publics de votre service associés à un réseau virtuel dans Azure doivent être activés pour la protection DDoS. Voici quelques exemples de conceptions :
- Sites Web (IaaS) dans Azure et les bases de données backend dans le centre de données local. 
- Application Gateway dans Azure (protection DDoS activée sur App Gateway/WAF) et sites web dans les centres de données locaux.

Consultez [Architectures de référence du service Azure DDoS Protection standard](ddos-protection-reference-architectures.md) pour plus de détails.

## <a name="can-i-register-a-domain-outside-of-azure-and-associate-that-to-a-protected-resource-like-vm-or-elb"></a>Puis-je inscrire un domaine extérieur à Azure et l’associer à une ressource protégée telle qu’une machine virtuelle ou un ELB ?
Pour les scénarios d’adresse IP publique, le service de protection DDoS prend en charge toutes les applications, quel que soit l’emplacement où le domaine associé est inscrit ou hébergé, à condition que l’adresse IP publique associée soit hébergée sur Azure. 

## <a name="can-i-manually-configure-the-ddos-policy-applied-to-the-vnetspublic-ips"></a>Puis-je configurer manuellement la stratégie DDoS appliquée aux adresses IP publiques/de réseaux virtuels ?
Non, malheureusement, la personnalisation de stratégie n’est pas disponible pour le moment.

## <a name="can-i-allowlistblocklist-specific-ip-addresses"></a>Puis-je mettre en liste verte ou rouge des adresses IP spécifiques ?
Non, malheureusement, la configuration manuelle n’est pas disponible pour le moment.

## <a name="how-can-i-test-ddos-protection"></a>Comment puis-je tester la protection DDoS ?
Consultez [Test à l’aide de simulations](test-through-simulations.md).

## <a name="how-long-does-it-take-for-the-metrics-to-load-on-portal"></a>Combien de temps faut-il pour charger les métriques sur le portail ?
Les métriques doivent être visibles sur le portail dans un délai de 5 minutes. Si votre ressource subit une attaque, d’autres métriques s’affichent sur le portail dans les 5 à 7 minutes. 
    