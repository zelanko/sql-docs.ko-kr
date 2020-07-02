---
title: sp_add_maintenance_plan_db (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_maintenance_plan_db_TSQL
- sp_add_maintenance_plan_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_maintenance_plan_db
ms.assetid: 76f4fefa-5b99-4deb-beed-e198987a45a9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8a3af8712870400d979a131dd26c4f6891b1b16a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85646640"
---
# <a name="sp_add_maintenance_plan_db-transact-sql"></a>sp_add_maintenance_plan_db(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  데이터베이스와 유지 관리 계획을 연결합니다.  
  
> [!NOTE]  
>  이 저장 프로시저는 데이터베이스 유지 관리 계획에 사용됩니다. 이 기능은 이러한 저장 프로시저를 사용하지 않는 유지 관리 계획으로 바뀌었습니다. 이 프로시저를 사용하여 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드된 설치에 대한 데이터베이스 유지 관리 계획을 유지할 수 있습니다.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_maintenance_plan_db [ @plan_id = ] 'plan_id' ,   
     [ @db_name = ] 'database_name'  
```  
  
## <a name="arguments"></a>인수  
`[ @plan_id = ] 'plan_id'`유지 관리 계획의 계획 ID를 지정 합니다. *plan_id* 은 **UNIQUEIDENTIFIER**이며 유효한 id 여야 합니다.  
  
`[ @db_name = ] 'database_name'`유지 관리 계획에 추가할 데이터베이스의 이름을 지정 합니다. 계획에 추가하기 전에 데이터베이스를 만들거나 데이터베이스가 이미 있어야 합니다. *database_name*은 **sysname**입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_add_maintenance_plan_db** 는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_add_maintenance_plan_db**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예제  
 이 예에서는 **sp_add_maintenance_plan**에서 만든 유지 관리 계획에 **AdventureWorks2012** 데이터베이스를 추가 합니다.  
  
```  
EXECUTE   sp_add_maintenance_plan_db N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC',N'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>참고 항목  
 [유지 관리 계획](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Transact-sql&#41;의 데이터베이스 유지 관리 계획 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
