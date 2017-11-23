---
title: sp_help_operator (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_operator
- sp_help_operator_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_operator
ms.assetid: caedc43d-44b8-415a-897e-92923f6de3b8
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 392586d2f3ea34b6914cb7bf34757d0481e890a9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sphelpoperator-transact-sql"></a>sp_help_operator(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서버에서 정의된 운영자에 관한 정보를 보고합니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_help_operator  
     { [ @operator_name = ] 'operator_name'   
     | [ @operator_id = ] operator_id }  
```  
  
## <a name="arguments"></a>인수  
 [  **@operator_name=** ] **'***operator_name***'**  
 운영자 이름입니다. *operator_name* 은 **sysname**합니다. 경우 *operator_name* 은 지정 하지 않으면 모든 연산자에 대 한 정보가 반환 됩니다.  
  
 [  **@operator_id=** ] *operator_id*  
 정보를 요청한 운영자의 ID입니다. *operator_id*은 **int**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  어느 *operator_id* 또는 *operator_name* 지정 해야 하지만 둘 다 지정할 수 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**id**|**int**|운영자의 ID입니다.|  
|**name**|**sysname**|운영자의 이름입니다.|  
|**사용 하도록 설정**|**tinyint**|운영자가 모든 알림을 받을 수 있습니다.<br /><br /> **1** = 예<br /><br /> **0** = 아니요|  
|**email_address**|**nvarchar (100)**|운영자의 전자 메일 주소입니다.|  
|**last_email_date**|**int**|운영자가 마지막으로 전자 메일을 받은 날짜입니다.|  
|**last_email_time**|**int**|운영자가 마지막으로 전자 메일을 받은 시간입니다.|  
|**pager_address**|**nvarchar (100)**|운영자의 호출기 주소입니다.|  
|**last_pager_date**|**int**|운영자가 마지막으로 호출을 받은 날짜입니다.|  
|**last_pager_time**|**int**|운영자가 마지막으로 호출을 받은 시간입니다.|  
|**weekday_pager_start_time**|**int**|운영자가 평일에 호출기로 알림을 받을 수 있는 기간의 시작 시간입니다.|  
|**weekday_pager_end_time**|**int**|운영자가 평일에 호출기로 알림을 받을 수 있는 기간의 종료 시간입니다.|  
|**saturday_pager_start_time**|**int**|운영자가 토요일에 호출기로 알림을 받을 수 있는 기간의 시작 시간입니다.|  
|**saturday_pager_end_time**|**int**|운영자가 토요일에 호출기로 알림을 받을 수 있는 기간의 종료 시간입니다.|  
|**sunday_pager_start_time**|**int**|운영자가 일요일에 호출기로 알림을 받을 수 있는 기간의 시작 시간입니다.|  
|**sunday_pager_end_time**|**int**|운영자가 일요일에 호출기로 알림을 받을 수 있는 기간의 종료 시간입니다.|  
|**pager_days**|**tinyint**|비트 마스크 (**1** = 일요일, **64** = 토요일)의 일-요일을 나타내는 운영자가 호출기로 알림을 받을 수 있습니다.|  
|**netsend_address**|**nvarchar (100)**|네트워크 팝업 알림에 필요한 운영자 주소입니다.|  
|**last_netsend_date**|**int**|운영자가 마지막으로 네트워크 팝업으로 알림을 받은 날짜입니다.|  
|**last_netsend_time**|**int**|운영자가 마지막으로 네트워크 팝업으로 알림을 받은 시간입니다.|  
|**category_name**|**sysname**|해당 운영자가 속한 운영자 범주의 이름입니다.|  
  
## <a name="remarks"></a>주의  
 **sp_help_operator** 에서 실행 되어야 합니다는 **msdb** 데이터베이스입니다.  
  
## <a name="permissions"></a>Permissions  
 기본적으로 **sysadmin** 고정 서버 역할의 멤버는 이 저장 프로시저를 실행할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 `François Ajenstat`라는 운영자에 관한 정보를 보고합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_operator  
    @operator_name = N'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_add_operator &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_update_operator &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
