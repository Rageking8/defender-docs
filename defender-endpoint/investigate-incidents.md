---
title: Investigate incidents in Microsoft Defender for Endpoint
description: See associated alerts, manage the incident, and see alert metadata to help you investigate an incident
search.appverid: met150
ms.service: defender-endpoint
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier1
- mde-edr
ms.topic: conceptual
ms.subservice: edr
ms.date: 06/05/2024
---

# Investigate incidents in Microsoft Defender for Endpoint

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)


Investigate incidents that affect your network, understand what they mean, and collate evidence to resolve them.

When you investigate an incident, you'll see:

- Incident details
- Incident comments and actions
- Tabs (alerts, devices, investigations, evidence, graph)

> [!VIDEO https://learn-video.azurefd.net/vod/player?id=46fe6a58-ea33-4f79-a1ec-26ae86d68033]

## Analyze incident details

Click an incident to see the **Incident pane**. Select **Open incident page** to see the incident details and related information (alerts, devices, investigations, evidence, graph).

:::image type="content" source="media/atp-incident-details.png" alt-text="The details of an incident" lightbox="media/atp-incident-details.png":::

### Alerts

You can investigate the alerts and see how they were linked together in an incident. Alerts are grouped into incidents based on the following reasons:

- Automated investigation - The automated investigation triggered the linked alert while investigating the original alert
- File characteristics - The files associated with the alert have similar characteristics
- Manual association - A user manually linked the alerts
- Proximate time - The alerts were triggered on the same device within a certain timeframe
- Same file - The files associated with the alert are exactly the same
- Same URL - The URL that triggered the alert is exactly the same

:::image type="content" source="media/atp-incidents-alerts-reason.png" alt-text="The Alerts tab with incident details page showing the reasons the alerts were linked together in that incident" lightbox="media/atp-incidents-alerts-reason.png":::

You can also manage an alert and see alert metadata along with other information. For more information, see [Investigate alerts](investigate-alerts.md).

### Devices

You can also investigate the devices that are part of, or related to, a given incident. For more information, see [Investigate devices](investigate-machines.md).

:::image type="content" source="media/atp-incident-device-tab.png" alt-text="The Devices tab in incident details page" lightbox="media/atp-incident-device-tab.png":::

### Investigations

Select **Investigations** to see all the automatic investigations launched by the system in response to the incident alerts.

:::image type="content" source="media/atp-incident-investigations-tab.png" alt-text="The investigations tab in the incident details page" lightbox="media/atp-incident-investigations-tab.png":::

## Going through the evidence

Microsoft Defender for Endpoint automatically investigates all the incidents' supported events and suspicious entities in the alerts, providing you with autoresponse and information about the important files, processes, services, and more.

Each of the analyzed entities will be marked as infected, remediated, or suspicious.

:::image type="content" source="media/atp-incident-evidence-tab.png" alt-text="The Evidence tab in incident details page" lightbox="media/atp-incident-evidence-tab.png":::

## Visualizing associated cybersecurity threats

Microsoft Defender for Endpoint aggregates the threat information into an incident so you can see the patterns and correlations coming in from various data points. You can view such correlation through the incident graph.

### Incident graph

The **Graph** tells the story of the cybersecurity attack. For example, it shows you what was the entry point, which indicator of compromise or activity was observed on which device. etc.

:::image type="content" source="media/atp-incident-graph-tab.png" alt-text="The incident graph" lightbox="media/atp-incident-graph-tab.png":::

You can click the circles on the incident graph to view the details of the malicious files, associated file detections, how many instances have there been worldwide, whether it's been observed in your organization, if so, how many instances.

:::image type="content" source="media/atp-incident-graph-details.png" alt-text="The incident details page" lightbox="media/atp-incident-graph-details.png":::

## Related topics

- [Incidents queue](view-incidents-queue.md)
- [Investigate incidents in Microsoft Defender for Endpoint](investigate-incidents.md)
- [Manage Microsoft Defender for Endpoint incidents](manage-incidents.md)
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
