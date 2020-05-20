---
title: sp_delete_maintenance_plan_job (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_maintenance_plan_job
- sp_delete_maintenance_plan_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_maintenance_plan_job
ms.assetid: 1c2148c3-2928-4d9b-b1c8-3512cfbd6a63
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7e408132edbfc042335fd1e0297f0e8a4b07223b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833374"
---
# <a name="sp_delete_maintenance_plan_job-transact-sql"></a>sp_delete_maintenance_plan_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 작업에서 지정된 유지 관리 계획을 분리합니다.  
  
> [!NOTE]  
>  이 저장 프로시저는 데이터베이스 유지 관리 계획에 사용됩니다. 이 기능은 이러한 저장 프로시저를 사용하지 않는 유지 관리 계획으로 바뀌었습니다. 이 프로시저를 사용하여 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드된 설치에 대한 데이터베이스 유지 관리 계획을 유지할 수 있습니다.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_maintenance_plan_job [ @plan_id = ] 'plan_id' ,   
   [ @job_id = ] 'job_id'   
```  
  
## <a name="arguments"></a>인수  
`[ @plan_id = ] 'plan\_id'`유지 관리 계획의 ID를 지정 합니다. *plan_id* 은 **UNIQUEIDENTIFIER**이며 유효한 id 여야 합니다.  
  
`[ @job_id = ] 'job\_id'`유지 관리 계획과 관련 된 작업의 ID를 지정 합니다. *job_id* 은 **UNIQUEIDENTIFIER**이며 유효한 id 여야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_delete_maintenance_plan_job** 는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
 모든 작업이 유지 관리 계획에서 제거 되 면 사용자가 **sp_delete_maintenance_plan_db** 를 실행 하 여 계획에서 나머지 데이터베이스를 제거 하는 것이 좋습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_delete_maintenance_plan_job**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 유지 관리 계획에서 작업 "B8FCECB1-E22C-11D2-AA64-00C04F688EAE"를 삭제합니다.  
  
```  
EXECUTE   sp_delete_maintenance_plan_job N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC', N'B8FCECB1-E22C-11D2-AA64-00C04F688EAE';  
```  
  
## <a name="see-also"></a>참고 항목  
 [유지 관리 계획](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Transact-sql&#41;의 데이터베이스 유지 관리 계획 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
