---
title: sp_help_maintenance_plan (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_maintenance_plan_TSQL
- sp_help_maintenance_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_maintenance_plan
ms.assetid: e972a510-960e-41d6-93c5-c71cd581a585
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42a98fe7af16c4e8aab22d6ace02f359dfe02c54
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096201"
---
# <a name="sp_help_maintenance_plan-transact-sql"></a>sp_help_maintenance_plan(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 유지 관리 계획에 관한 정보를 반환합니다. 계획을 지정하지 않은 경우에는 저장 프로시저가 모든 유지 관리 계획에 관한 정보를 반환합니다.  
  
> **참고:** 이 저장 프로시저는 데이터베이스 유지 관리 계획에 사용 됩니다. 이 기능은 이러한 저장 프로시저를 사용하지 않는 유지 관리 계획으로 바뀌었습니다. 이 프로시저를 사용하여 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드된 설치에 대한 데이터베이스 유지 관리 계획을 유지할 수 있습니다.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_maintenance_plan [ [ @plan_id = ] 'plan_id' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @plan_id = ] 'plan\_id'`유지 관리 계획의 계획 ID를 지정 합니다. **UNIQUEIDENTIFIER** *plan_id* 입니다. 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 None  
  
## <a name="result-sets"></a>결과 집합  
 *Plan_id* 지정 하면 **sp_help_maintenance_plan** 는 계획, 데이터베이스 및 작업의 세 가지 테이블을 반환 합니다.  
  
### <a name="plan-table"></a>계획 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|유지 관리 계획 ID입니다.|  
|**plan_name**|**sysname**|유지 관리 계획 이름입니다.|  
|**date_created**|**datetime**|유지 관리 계획을 만든 날짜입니다.|  
|**소유자도**|**sysname**|유지 관리 계획의 소유자입니다.|  
|**max_history_rows**|**int**|시스템 테이블에 있는 유지 관리 계획을 기록하는 데 사용하도록 지정된 최대 행 수입니다.|  
|**remote_history_server**|**int**|기록 보고서를 작성할 원격 서버의 이름입니다.|  
|**max_remote_history_rows**|**int**|기록 보고서를 작성할 수 있는 원격 서버의 시스템 테이블에서 지정된 최대 행 수입니다.|  
|**user_defined_1**|**int**|기본값은 NULL입니다.|  
|**user_defined_2**|**nvarchar (100)**|기본값은 NULL입니다.|  
|**user_defined_3**|**datetime**|기본값은 NULL입니다.|  
|**user_defined_4**|**uniqueidentifier**|기본값은 NULL입니다.|  
  
### <a name="database-table"></a>데이터베이스 테이블  
  
|열 이름|Description|  
|-----------------|-----------------|  
|**database_name**|유지 관리 계획과 연관된 모든 데이터베이스의 이름입니다. *database_name* 는 **sysname**입니다.|  
  
### <a name="job-table"></a>작업 테이블  
  
|열 이름|Description|  
|-----------------|-----------------|  
|**job_id**|유지 관리 계획과 연관된 모든 작업의 ID입니다. **uniqueidentifier** *job_id* 입니다.|  
  
## <a name="remarks"></a>설명  
 **sp_help_maintenance_plan** **msdb** 데이터베이스에 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_help_maintenance_plan**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 유지 관리 계획 FAD6F2AB-3571-11D3-9D4A-00C04FB925FC에 대한 정보를 보여 줍니다.  
  
```  
EXECUTE   sp_help_maintenance_plan   
   N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## <a name="see-also"></a>참고 항목  
 [유지 관리 계획](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Transact-sql&#41;의 데이터베이스 유지 관리 계획 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
