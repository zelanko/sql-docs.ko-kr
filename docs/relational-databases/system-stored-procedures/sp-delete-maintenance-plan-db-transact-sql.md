---
title: sp_delete_maintenance_plan_db (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_maintenance_plan_db_TSQL
- sp_delete_maintenance_plan_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_maintenance_plan_db
- maintenance plans [SQL Server], deleting
- removing maintenance plan
- disassociating maintenance plan
ms.assetid: d1e8afb5-12ee-492b-a770-ba708ed7c8a4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4843eb9de8badced7e446f20a997a530478c2756
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68056525"
---
# <a name="sp_delete_maintenance_plan_db-transact-sql"></a>sp_delete_maintenance_plan_db(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 데이터베이스에서 지정된 유지 관리 계획을 분리합니다.  
  
> [!NOTE]  
>  이 저장 프로시저는 데이터베이스 유지 관리 계획에 사용됩니다. 이 기능은 이러한 저장 프로시저를 사용하지 않는 유지 관리 계획으로 바뀌었습니다. 이 프로시저를 사용하여 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드된 설치에 대한 데이터베이스 유지 관리 계획을 유지할 수 있습니다.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_delete_maintenance_plan_db [ @plan_id = ] 'plan_id' ,   
     [ @db_name = ] 'database_name'   
```  
  
## <a name="arguments"></a>인수  
`[ @plan_id = ] 'plan\_id'`유지 관리 계획 ID를 지정 합니다. **uniqueidentifier** *plan_id* 입니다.  
  
`[ @db_name = ] 'database\_name'`유지 관리 계획에서 삭제할 데이터베이스 이름을 지정 합니다. *database_name* 는 **sysname**입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_delete_maintenance_plan_db** 는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
 **Sp_delete_maintenance_plan_db** 저장 프로시저는 유지 관리 계획과 지정한 데이터베이스 간의 연결을 제거 합니다. 데이터베이스를 삭제 하거나 삭제 하지 않습니다.  
  
 유지 관리 계획에서 마지막 데이터베이스를 **sp_delete_maintenance_plan_db** 제거 하는 경우에도 저장 프로시저는 유지 관리 계획을 삭제 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_delete_maintenance_plan_db**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 **Sp_add_maintenance_plan_db**를 사용 하 여 이전에 추가한 **AdventureWorks2012** 데이터베이스에서 유지 관리 계획을 삭제 합니다.  
  
```  
EXECUTE   sp_delete_maintenance_plan_db N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC', N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>참고 항목  
 [유지 관리 계획](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Transact-sql&#41;의 데이터베이스 유지 관리 계획 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
