---
title: Azure Security Center and Azure Container Registry
description: "Learn about scanning your container registries with Azure Security Center"
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2020
ms.author: memildin

---

# Azure Container Registry image scanning by Security Center

Azure Container Registry (ACR) is a managed, private Docker registry service that stores and manages your container images for Azure deployments in a central registry. It's based on the open-source Docker Registry 2.0.

Enable **Azure Defender for container registries** for deeper visibility into the vulnerabilities of the images in your Azure Resource Manager based registries. Enable or disable the plan at the subscription level to cover all registries in a subscription. This feature is charged per image, as shown on the [pricing page](security-center-pricing.md). Enabling Azure Defender, ensures that Security Center is ready to scan images that get pushed to the registry. 


## When are images scanned?

Whenever an image is pushed to your registry, Security Center automatically scans that image. To trigger the scan of an image, push it to your repository.

When the scan completes (typically after approximately 2 minutes, but can be up to 15 minutes), findings are available as Security Center recommendations like this:

[![Sample Azure Security Center recommendation about vulnerabilities discovered in an Azure Container Registry (ACR) hosted image](media/azure-container-registry-integration/container-security-acr-page.png)](media/azure-container-registry-integration/container-security-acr-page.png#lightbox)

## Benefits of integration

Security Center identifies Azure Resource Manager based ACR registries in your subscription and seamlessly provides:

* **Azure-native vulnerability scanning** for all pushed Linux images. Security Center scans the image using a scanner from the industry-leading vulnerability scanning vendor, Qualys. This native solution is seamlessly integrated by default.

* **Security recommendations** for Linux images with known vulnerabilities. Security Center provides details of each reported vulnerability and a  severity classification. Additionally, it gives guidance for how to  remediate the specific vulnerabilities found on each image pushed to registry.

![Azure Security Center and Azure Container Registry (ACR) high-level overview](./media/azure-container-registry-integration/aks-acr-integration-detailed.png)




## FAQ for Azure Container Registry image scanning

### How does Security Center scan an image?
The image is pulled from the registry. It's then run in an isolated sandbox with the Qualys scanner that extracts a list of known vulnerabilities.

Security Center filters and classifies findings from the scanner. When an image is healthy, Security Center marks it as such. Security Center generates security recommendations only for images that have issues to be resolved. By only notifying when there are problems, Security Center reduces the potential for unwanted informational alerts.

### How often does Security Center scan my images?
Image scans are triggered on every push.

### Can I get the scan results via REST API?
Yes. The results are under [Sub-Assessments Rest API](/rest/api/securitycenter/subassessments/list/). Also, you can use Azure Resource Graph (ARG), the Kusto-like API for all of your resources: a query can fetch a specific scan.
 
### What registry types are scanned? What types are billed?
The availability section lists the types of container registries supported by the Azure Defender for container registries. 

If registries that aren't supported are connected to your Azure subscription, they won't be scanned and you will not be billed for them.


## Next steps

To learn more about Security Center's container security features, see:

* [Azure Security Center and container security](container-security.md)

* [Integration with Azure Kubernetes Service](azure-kubernetes-service-integration.md)


