---
description: sysdbmaintplan_databases(Transact-SQL)
title: sysdbmaintplan_databases (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplan_databases
- sysdbmaintplan_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplan_databases system table
ms.assetid: f8413a44-8fcc-4899-84f2-b4afe0f8ec08
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5f2f6d15d1a1d1d7780472627c32cf4b978fb0d9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427615"
---
# <a name="sysdbmaintplan_databases-transact-sql"></a>sysdbmaintplan_databases(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 테이블은 이전 버전의에서 업그레이드 된 인스턴스에 대 한 기존 정보를 유지 하기 위해 포함 되었습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이후 버전에서는 이 테이블의 내용을 변경하지 마십시오. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**없으면**|유지 관리 계획 ID입니다.|  
|**database_name**|**sysname**|데이터베이스 유지 관리 계획과 연관된 데이터베이스의 이름입니다.|  
  
  
