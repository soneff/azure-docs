---
author: MikeRayMSFT
ms.author: mikeray
ms.service: azure-arc
ms.topic: include
ms.date: 12/13/2022
---


|**Service**|**Port**|**URL**|**Direction**|**Notes**|
|--|--|--|--|--|
| Helm chart (direct connected mode only) | 443 | `arcdataservicesrow1.azurecr.io` | Outbound |Provisions the Azure Arc data controller bootstrapper and cluster level objects, such as custom resource definitions, cluster roles, and cluster role bindings, is pulled from an Azure Container Registry. | 
| Azure monitor APIs <sup>*</sup> | 443 |`*.ods.opinsights.azure.com`<br/>`*.oms.opinsights.azure.com`<br/>`*.monitoring.azure.com` | Outbound | Azure Data Studio and Azure CLI connect to the Azure Resource Manager APIs to send and retrieve data to and from Azure for some features. See [Azure Monitor APIs](#azure-monitor-apis).
| Azure Arc data processing service <sup>*</sup>| 443 |`san-af-<region>-prod.azurewebsites.net` | Outbound<br/> Inbound |

<sup>*</sup> Requirement depends on deployment mode:

  - For direct mode, the controller pod on the Kubernetes cluster needs to have outbound connectivity to the endpoints to send the logs, metrics, inventory, and billing information to Azure Monitor/Data Processing Service. 
  - For indirect mode, the machine that runs `az arcdata dc upload` needs to have the outbound connectivity to Azure Monitor and Data Processing Service.

### Azure Monitor APIs

Connectivity from Azure Data Studio to the Kubernetes API server uses the Kubernetes authentication and encryption that you have established.  Each user that is using Azure Data Studio or CLI must have an authenticated connection to the Kubernetes API to perform many of the actions related to Azure Arc-enabled data services.
