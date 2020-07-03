---
title: dbo.sys알림 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysnotifications_TSQL
- sysnotifications
- sysnotifications_TSQL
- dbo.sysnotifications
dev_langs:
- TSQL
helpviewer_keywords:
- sysnotifications system table
ms.assetid: c5150d18-e8b7-48a7-ada7-77c583af6e41
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1b6ac4c1c037c186e1fe6fc20ad1b3ef0cfba976
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890419"
---
# <a name="dbosysnotifications-transact-sql"></a>dbo.sysnotifications(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  각 알림에 대해 한 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|경고의 ID입니다.|  
|**operator_id**|**int**|알림을 전달하는 대상이 되는 운영자의 ID입니다.|  
|**notification_method**|**tinyint**|알림 방법입니다.<br /><br /> **1** = 전자 메일<br /><br /> **2** = 호출기<br /><br /> **4**  =  **netsend**<br /><br /> **7** = 모두|  
  
  
