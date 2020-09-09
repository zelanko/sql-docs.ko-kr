---
description: dbo.systaskids(Transact-SQL)
title: dbo.systaskids (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3a3e639fcc99f3b78d499e76062cd7f6d32f516c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551083"
---
# <a name="dbosystaskids-transact-sql"></a>dbo.systaskids(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업에 대해 이전 버전의 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 생성된 태스크 매핑을 포함합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**task_id**|**int**|태스크의 ID입니다.|  
|**job_id**|**uniqueidentifier**|태스크에 매핑되는 작업의 ID입니다.|  
  
  
