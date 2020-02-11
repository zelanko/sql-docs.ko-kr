---
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: f780199361d9e5741187dd4e5346abb2df98b9cb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68130440"
---
# <a name="sysdbmaintplan_jobs-transact-sql"></a>sysdbmaintplan_jobs(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 테이블은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드된 인스턴스에 대한 기존 정보를 유지하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함됩니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이 테이블의 내용을 변경하지 않습니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|데이터베이스 유지 관리 계획 ID입니다.|  
|**job_id**|**uniqueidentifier**|데이터베이스 유지 관리 계획과 연관된 작업의 ID입니다.|  
  
  
