---
title: Configure identity - Azure Event Grid IoT Edge | Microsoft Docs 
description: Configure Event Grid module's identity
author: VidyaKukke
manager: rajarv
ms.author: vkukke
ms.reviewer: spelluru
ms.subservice: iot-edge
ms.date: 02/15/2022
ms.topic: article
---

# Configure identity for the Event Grid module

This article gives shows how to configure identity for Grid on Edge. By default, the Event Grid module presents its identity certificate as configured by the IoT security daemon. Event Grid on Edge presents its identity certificate with its outgoing calls when it delivers events. A subscriber  can then validate it's the Event Grid module that sent the event before accepting.

See [Security and authentication](security-authentication.md) guide for all the possible configurations.

> [!IMPORTANT]
> On March 31, 2023, Event Grid on Azure IoT Edge support will be retired, so make sure to transition to IoT Edge native capabilities prior to that date. For more information, see [Transition from Event Grid on Azure IoT Edge to Azure IoT Edge ](transition.md). 



## Always present identity certificate
Here's an example configuration for always presenting an identity certificate on outgoing calls. 

```json
 {
  "Env": [
    "outbound__clientAuth__clientCert__enabled=true",
    "outbound__clientAuth__clientCert__source=IoTEdge"
  ]
}
 ```

## Don't present identity certificate
Here's an example configuration for not presenting an identity certificate on outgoing calls. 

```json
 {
  "Env": [
    "outbound__clientAuth__clientCert__enabled=false"
  ]
}
 ```
