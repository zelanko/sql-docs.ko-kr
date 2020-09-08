---
description: sysdbmaintplan_jobs(Transact-SQL)
title: sysdbmaintplan_jobs (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplan_jobs
- sysdbmaintplan_jobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplan_jobs system table
ms.assetid: bc65cd70-6ef2-4c17-be11-877ecf4efe50
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7ab3398bdf0c258a5997ce64d48db781234059bf
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89517843"
---
# <a name="sysdbmaintplan_jobs-transact-sql"></a>sysdbmaintplan_jobs(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 테이블은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드된 인스턴스에 대한 기존 정보를 유지하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이 테이블의 내용을 변경하지 않습니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|데이터베이스 유지 관리 계획 ID입니다.|  
|**job_id**|**uniqueidentifier**|데이터베이스 유지 관리 계획과 연관된 작업의 ID입니다.|  
  
  
