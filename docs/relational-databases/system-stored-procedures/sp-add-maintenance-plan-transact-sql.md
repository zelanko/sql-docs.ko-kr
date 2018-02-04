---
title: sp_add_maintenance_plan (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_maintenance_plan
- sp_add_maintenance_plan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_maintenance_plan
ms.assetid: 01ab1834-6260-47cb-a1b7-20722217b062
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 44a663e97610514204c6209c13be4d515197af33
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="spaddmaintenanceplan-transact-sql"></a>sp_add_maintenance_plan(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  유지 관리 계획을 추가하고 계획 ID를 반환합니다.  
  
> [!NOTE]  
>  이 저장 프로시저는 데이터베이스 유지 관리 계획에 사용됩니다. 이 기능은 이러한 저장 프로시저를 사용하지 않는 유지 관리 계획으로 바뀌었습니다. 이 프로시저를 사용하여 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드된 설치에 대한 데이터베이스 유지 관리 계획을 유지할 수 있습니다.  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_maintenance_plan [ @plan_name = ] 'plan_name' ,   
     @plan_id = 'plan_id' OUTPUT  
```  
  
## <a name="arguments"></a>인수  
 [ **@plan_name =**] **'***plan_name***'**  
 추가할 유지 관리 계획의 이름을 지정합니다. *plan_name* 은 **varchar (128)**합니다.  
  
 **@plan_id = '** *plan_id* **'**  
 유지 관리 계획의 ID를 지정합니다. *plan_id* 은 **uniqueidentifier**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 **sp_add_maintenance_plan** 에서 실행 되어야 합니다는 **msdb** 데이터베이스 하 고 새로 만들었거나, 하지만 비어 있는 경우 유지 관리 계획을 만듭니다. 하나 이상의 데이터베이스를 추가 하 고 작업 또는 작업 연결을 하려면 실행 **sp_add_maintenance_plan_db** 및 **sp_add_maintenance_plan_job**합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_add_maintenance_plan**합니다.  
  
## <a name="examples"></a>예  
 Myplan이라는 유지 관리 계획을 만듭니다.  
  
```  
DECLARE   @myplan_id UNIQUEIDENTIFIER;  
EXECUTE   sp_add_maintenance_plan N'Myplan',@plan_id=@myplan_id OUTPUT  
PRINT   'The id for the maintenance plan "Myplan" is:'+convert(varchar(256),@myplan_id);  
GO  
```  
  
 유지 관리 계획을 만드는 데 성공하면 계획 ID를 반환합니다.  
  
```  
'The id for the maintenance plan "Myplan" is:' FAD6F2AB-3571-11D3-9D4A-00C04FB925FC  
```  
  
## <a name="see-also"></a>관련 항목:  
 [유지 관리 계획](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [데이터베이스 유지 관리 계획 저장 프로시저 &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
