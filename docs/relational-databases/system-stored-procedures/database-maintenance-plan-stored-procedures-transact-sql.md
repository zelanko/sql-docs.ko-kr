---
title: 데이터베이스 유지 관리 계획 저장 프로시저 (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database maintenance plans [SQL Server]
- system stored procedures [SQL Server], database maintenance plans
- maintenance plans [SQL Server], stored procedures
ms.assetid: f5f658e3-417e-4286-9213-5738266f3b28
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43ba326369983800065b6ae23cfa83e35ad034f3
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38023841"
---
# <a name="database-maintenance-plan-stored-procedures-transact-sql"></a>데이터베이스 유지 관리 계획 저장 프로시저(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 다음과 같은 시스템 유지 관리 작업을 설정 하는 데 사용 되는 프로시저를 저장 합니다. 이 저장 프로시저는 데이터베이스 유지 관리 계획에 사용됩니다. 이 기능은 이러한 저장 프로시저를 사용하지 않는 유지 관리 계획으로 바뀌었습니다. 이 프로시저를 사용하여 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드된 설치에 대한 데이터베이스 유지 관리 계획을 유지할 수 있습니다.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
|||  
|-|-|  
|[sp_add_maintenance_plan](../../relational-databases/system-stored-procedures/sp-add-maintenance-plan-transact-sql.md)|[sp_delete_maintenance_plan_db](../../relational-databases/system-stored-procedures/sp-delete-maintenance-plan-db-transact-sql.md)|  
|[sp_add_maintenance_plan_db](../../relational-databases/system-stored-procedures/sp-add-maintenance-plan-db-transact-sql.md)|[sp_delete_maintenance_plan_job](../../relational-databases/system-stored-procedures/sp-delete-maintenance-plan-job-transact-sql.md)|  
|[sp_add_maintenance_plan_job](../../relational-databases/system-stored-procedures/sp-add-maintenance-plan-job-transact-sql.md)|[sp_help_maintenance_plan](../../relational-databases/system-stored-procedures/sp-help-maintenance-plan-transact-sql.md)|  
|[sp_delete_maintenance_plan](../../relational-databases/system-stored-procedures/sp-delete-maintenance-plan-transact-sql.md)||  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [유지 관리 계획](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
  
