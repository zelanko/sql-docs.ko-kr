---
title: dbo.sysnotifications (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysnotifications_TSQL
- sysnotifications
- sysnotifications_TSQL
- dbo.sysnotifications
dev_langs: TSQL
helpviewer_keywords: sysnotifications system table
ms.assetid: c5150d18-e8b7-48a7-ada7-77c583af6e41
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 61f9e69444b8df91a7c92f38ecc4b9b577b7b405
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysnotifications-transact-sql"></a>dbo.sysnotifications(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 알림에 대해 한 행을 포함합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|경고의 ID입니다.|  
|**operator_id**|**int**|알림을 전달하는 대상이 되는 운영자의 ID입니다.|  
|**notification_method**|**tinyint**|알림 방법입니다.<br /><br /> **1** = 전자 메일<br /><br /> **2** = 호출기<br /><br /> **4** = **netsend**<br /><br /> **7** = all|  
  
  
