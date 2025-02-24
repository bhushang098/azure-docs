---
title: Configure webhook subscriber authentication - Azure Event Grid IoT Edge | Microsoft Docs 
description: Configure webhook subscriber authentication 
author: VidyaKukke
manager: rajarv
ms.author: vkukke
ms.reviewer: spelluru
ms.subservice: iot-edge
ms.date: 02/15/2022
ms.topic: article
---

# Configure webhook subscriber authentication

This guide gives examples of the possible webhook subscriber configurations for an Event Grid module. By default, only HTTPS endpoints are accepted for webhook subscribers. The Event Grid module will reject if the subscriber presents a self-signed certificate.

> [!IMPORTANT]
> On March 31, 2023, Event Grid on Azure IoT Edge support will be retired, so make sure to transition to IoT Edge native capabilities prior to that date. For more information, see [Transition from Event Grid on Azure IoT Edge to Azure IoT Edge ](transition.md). 



## Allow only HTTPS subscriber

```json
 {
  "Env": [
    "outbound__webhook__httpsOnly=true",
    "outbound__webhook__skipServerCertValidation=false",
    "outbound__webhook__allowUnknownCA=false"
  ]
}
 ```

## Allow HTTPS subscriber with self-signed certificate

```json
 {
  "Env": [
    "outbound__webhook__httpsOnly=true",
    "outbound__webhook__skipServerCertValidation=false",
    "outbound__webhook__allowUnknownCA=true"
  ]
}
 ```

>[!NOTE]
>Set the property `outbound__webhook__allowUnknownCA` to `true` only in test environments as you might typically use self-signed certificates. For production workloads we recommend them to be set to **false**.

## Allow HTTPS subscriber but skip certificate validation

```json
 {
  "Env": [
    "outbound__webhook__httpsOnly=true",
    "outbound__webhook__skipServerCertValidation=true",
    "outbound__webhook__allowUnknownCA=false"
  ]
}
 ```

>[!NOTE]
>Set the property `outbound__webhook__skipServerCertValidation` to `true` only in test environments as you might not be presenting a certificate that needs to be authenticated. For production workloads we recommend them to be set to **false**

## Allow both HTTP and HTTPS with self-signed certificates

```json
 {
  "Env": [
    "outbound__webhook__httpsOnly=false",
    "outbound__webhook__skipServerCertValidation=false",
    "outbound__webhook__allowUnknownCA=true"
  ]
}
 ```

>[!NOTE]
>Set the property `outbound__webhook__httpsOnly` to `false` only in test environments as you might want to bring up a HTTP subscriber first. For production workloads we recommend them to be set to **true**
