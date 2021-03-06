---
title: Configurer le comportement de session – Azure Active Directory B2C | Microsoft Docs
description: Découvrez comment configurer le comportement de session dans Azure Active Directory B2C.
services: active-directory-b2c
author: msmimart
manager: celestedg
ms.service: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 10/12/2020
ms.author: mimart
ms.subservice: B2C
ms.openlocfilehash: 091704fabb7b50a0c83625c6ae46d9a807f01ffc
ms.sourcegitcommit: d103a93e7ef2dde1298f04e307920378a87e982a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91961032"
---
# <a name="configure-session-behavior-in-azure-active-directory-b2c"></a>Configurer le comportement de session dans Azure Active Directory B2C

La gestion de [session d’authentification unique (SSO)](session-overview.md) dans Azure Active Directory B2C (Azure AD B2C) permet à un administrateur de contrôler l’interaction avec un utilisateur une fois celui-ci authentifié. Par exemple, l’administrateur peut contrôler si la sélection des fournisseurs d’identité s’affiche ou si des détails de compte doivent être entrés à nouveau. Cet article décrit comment configurer les paramètres d’authentification unique pour Azure AD B2C.

## <a name="session-behavior-properties"></a>Propriétés de comportement de session

Vous pouvez utiliser les propriétés suivantes pour gérer les sessions d’application web :

- **Durée de vie de session d’application web (minutes)** : la durée de vie du cookie de session Azure AD B2C stocké dans le navigateur de l’utilisateur après une authentification réussie.
    - Par défaut : 1 440 minutes.
    - Valeur minimale (inclusive) : 15 minutes.
    - Valeur maximale (inclusive) : 1 440 minutes.
- **Délai d’expiration de session d’application web** : le [type d’expiration de session](session-overview.md#session-expiry-type), *Rolling* (Propagé) ou *Absolute* (Absolu). 
- **Configuration de l’authentification unique** : l’[étendue de session](session-overview.md#session-scope) du comportement de l’authentification unique (SSO) sur plusieurs applications et flux d’utilisateurs dans votre client Azure AD B2C.


## <a name="configure-the-properties"></a>Configurer les propriétés

1. Connectez-vous au [portail Azure](https://portal.azure.com).
2. Veillez à utiliser l’annuaire qui contient votre locataire Azure AD B2C en sélectionnant le filtre **Annuaire et abonnement** dans le menu supérieur et en choisissant l’annuaire qui contient votre locataire Azure AD B2C.
3. Choisissez **Tous les services** dans le coin supérieur gauche du portail Azure, puis recherchez et sélectionnez **Azure AD B2C**.
4. Sélectionnez **Flux d’utilisateurs**.
5. Ouvrez le flux utilisateur que vous avez créé précédemment.
6. Sélectionner **Propriétés**.
7. Configurez **Durée de vie de la session de l’application web (minutes)** , **Délai d’expiration de la session de l’application web** , **Configuration de l’authentification unique** et **Exiger un jeton d’ID dans les demandes de déconnexion**, selon les besoins.

    ![Paramètres de propriété du comportement de la session sur le Portail Azure](./media/session-behavior/session-behavior.png)

8. Cliquez sur **Enregistrer**.

## <a name="configure-sign-out-behavior"></a>Configurer le comportement de déconnexion

### <a name="secure-your-logout-redirect"></a>Sécuriser la redirection de déconnexion

Après la déconnexion, l’utilisateur est redirigé vers l’URI spécifié dans le paramètre `post_logout_redirect_uri`, quelles que soient les URL de réponse qui ont été spécifiées pour l’application. Cependant, si un `id_token_hint` valide est transmis et que l’option **Exiger un jeton d’ID dans les demandes de déconnexion** est activée, Azure AD B2C vérifie que la valeur de `post_logout_redirect_uri` correspond à l’un des URI de redirection configurés de l’application avant d’effectuer la redirection. Si aucune URL de réponse correspondante n’a été configurée pour l’application, un message d’erreur s’affiche et l’utilisateur n’est pas redirigé. Pour exiger un jeton d’ID dans les demandes de déconnexion :

1. Connectez-vous au [portail Azure](https://portal.azure.com).
1. Veillez à utiliser l’annuaire qui contient votre locataire Azure AD B2C en sélectionnant le filtre **Annuaire et abonnement** dans le menu supérieur et en choisissant l’annuaire qui contient votre locataire Azure AD B2C.
1. Choisissez **Tous les services** dans le coin supérieur gauche du portail Azure, puis recherchez et sélectionnez **Azure AD B2C**.
1. Sélectionnez **Flux d’utilisateurs**.
1. Ouvrez le flux utilisateur que vous avez créé précédemment.
1. Sélectionner **Propriétés**.
1. Activez l’option **Exiger un jeton d’ID dans les demandes de déconnexion**.
1. Revenez à **Azure AD B2C**.
1. Sélectionnez **Inscriptions d’applications**, puis sélectionnez votre application.
1. Sélectionnez **Authentification**.
1. Dans la zone de texte **URL de déconnexion**, saisissez votre URI de redirection après déconnexion, puis sélectionnez **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur une [session Azure AD B2C](session-overview.md).
