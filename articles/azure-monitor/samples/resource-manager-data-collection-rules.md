---
title: Exemples de modèles Resource Manager pour les règles de collecte de données
description: Exemples de modèles Azure Resource Manager pour créer des associations entre les règles de collecte de données et les machines virtuelles dans Azure Monitor.
ms.subservice: logs
ms.topic: sample
author: bwren
ms.author: bwren
ms.date: 11/17/2020
ms.openlocfilehash: 1c059edb1422a572011f167f7f1c02d5e87e5da2
ms.sourcegitcommit: 5ae2f32951474ae9e46c0d46f104eda95f7c5a06
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/23/2020
ms.locfileid: "95324822"
---
# <a name="resource-manager-template-samples-for-data-collection-rules-in-azure-monitor"></a>Exemples de modèles Resource Manager pour les règles de collecte de données dans Azure Monitor
Cet article contient des exemples de [modèle Azure Resource Manager](../../azure-resource-manager/templates/template-syntax.md) permettant de déployer et de configurer l’[agent Log Analytics](../platform/log-analytics-agent.md) et l’[extension de diagnostic](../platform/diagnostics-extension-overview.md) associé pour les machines virtuelles dans Azure Monitor. Chaque exemple comprend un fichier de modèle et un fichier de paramètres avec des exemples de valeurs à fournir au modèle.

[!INCLUDE [azure-monitor-samples](../../../includes/azure-monitor-resource-manager-samples.md)]


## <a name="create-association-between-azure-vm-and-rule"></a>Créer une association entre une machine virtuelle Azure et une règle

L’exemple suivant installe l’agent Azure Monitor sur une machine virtuelle Microsoft Azure. Une association est créée entre une machine virtuelle Azure et une règle de collecte de données.

### <a name="template-file"></a>Fichier de modèle

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "vmName": {
            "type": "string",
            "metadata": {
                "description": "Name of the virtual machine."
            }
        },
        "associationName": {
            "type": "string",
            "metadata": {
                "description": "Name of the association."
            }
        },
        "dataCollectionRuleId": {
            "type": "string",
            "metadata": {
                "description": "Resource ID of the data collection rule."
            }
        }
    },
    "resources": [
        {
            "type": "Microsoft.Compute/virtualMachines/providers/dataCollectionRuleAssociations",
            "name": "[concat(parameters('vmName'),'/microsoft.insights/', parameters('associationName'))]",
            "apiVersion": "2019-11-01-preview",
            "properties": {
                "description": "Association of data collection rule. Deleting this association will break the data collection for this virtual machine.",
                "dataCollectionRuleId": "[parameters('dataCollectionRuleId')]"
            }
        }
    ]
}
```

### <a name="parameter-file"></a>Fichier de paramètres

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "vmName": {
        "value": "my-windows-vm"
      },
      "location": {
        "value": "eastus"
      }
  }
}
```

## <a name="create-association-between-azure-arc-and-rule"></a>Créer une association entre Azure Arc et une règle

L’exemple suivant installe l’agent Azure Monitor sur une machine virtuelle Microsoft Azure. Une association est créée entre un ordinateur serveur avec Azure Arc et une règle de collecte de données.

### <a name="template-file"></a>Fichier de modèle

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "vmName": {
            "type": "string",
            "metadata": {
                "description": "Name of the virtual machine."
            }
        },
        "associationName": {
            "type": "string",
            "metadata": {
                "description": "Name of the association."
            }
        },
        "dataCollectionRuleId": {
            "type": "string",
            "metadata": {
                "description": "Resource ID of the data collection rule."
            }
        }
    },
    "resources": [
        {
            "type": "Microsoft.HybridCompute/machines/providers/dataCollectionRuleAssociations",
            "name": "[concat(parameters('machineName'),'/microsoft.insights/', parameters('associationName'))]",
            "apiVersion": "2019-11-01-preview",
            "properties": {
                "description": "Association of data collection rule. Deleting this association will break the data collection for this Arc server.",
                "dataCollectionRuleId": "[parameters('dataCollectionRuleId')]"
            }
        }
    ]
}
```

### <a name="parameter-file"></a>Fichier de paramètres

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "vmName": {
        "value": "my-windows-vm"
      },
      "location": {
        "value": "eastus"
      }
  }
}
```


## <a name="next-steps"></a>Étapes suivantes

* [Obtenir d’autres exemples de modèle pour Azure Monitor](resource-manager-samples.md).
* [En savoir plus sur l’agent Log Analytics](../platform/log-analytics-agent.md).
* [En savoir plus sur l’extension de diagnostic](../platform/diagnostics-extension-overview.md).
