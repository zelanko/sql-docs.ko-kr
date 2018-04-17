---
title: dbo.systaskids (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- systaskids_TSQL
- dbo.systaskids
- systaskids
- dbo.systaskids_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- systaskids system table
ms.assetid: 45c56d89-4160-4d84-80bf-a7a05488792d
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a5411592013cf83af4f327df5f463c59b4f7760
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="dbosystaskids-transact-sql"></a>dbo.systaskids(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  현재 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업에 대해 이전 버전의 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 생성된 태스크 매핑을 포함합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**task_id**|**int**|태스크의 ID입니다.|  
|**job_id**|**uniqueidentifier**|태스크에 매핑되는 작업의 ID입니다.|  
  
  
