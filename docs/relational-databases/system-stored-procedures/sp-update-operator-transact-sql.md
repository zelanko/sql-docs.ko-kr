---
title: sp_update_operator (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_update_operator_TSQL
- sp_update_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_operator
ms.assetid: 231750a6-4828-4d03-afe6-b91d38c42ed3
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f0cdd4e69655ac469e875b37f3e299b89b1be2f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spupdateoperator-transact-sql"></a>sp_update_operator(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  경고 및 작업에 사용하기 위해 운영자(알림 수신자)에 관한 정보를 업데이트합니다.  
  
   ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_update_operator   
     [ @name =] 'name'   
     [ , [ @new_name = ] 'new_name' ]   
     [ , [ @enabled = ] enabled]   
     [ , [ @email_address = ] 'email_address' ]  
     [ , [ @pager_address = ] 'pager_number']   
     [ , [ @weekday_pager_start_time = ] weekday_pager_start_time ]  
     [ , [ @weekday_pager_end_time = ] weekday_pager_end_time ]   
     [ , [ @saturday_pager_start_time = ] saturday_pager_start_time ]  
     [ , [ @saturday_pager_end_time = ] saturday_pager_end_time ]   
     [ , [ @sunday_pager_start_time = ] sunday_pager_start_time ]  
     [ , [ @sunday_pager_end_time = ] sunday_pager_end_time ]   
     [ , [ @pager_days = ] pager_days ]   
     [ , [ @netsend_address = ] 'netsend_address' ]   
     [ , [ @category_name = ] 'category' ]  
```  
  
## <a name="arguments"></a>인수  
 [ @name=] '*이름*'  
 수정할 운영자의 이름입니다. *이름* 은 **sysname**, 기본값은 없습니다.  
  
 [ @new_name=] '*new_name*'  
 운영자의 새 이름입니다. 이 이름은 고유해야 합니다. *new_name* 은 **sysname**, 기본값은 NULL입니다.  
  
 [ @enabled=] *사용 하도록 설정*  
 운영자의 현재 상태를 나타내는 숫자 (**1** 현재 설정 되어 있으면 **0** 하지 않은 경우). *활성화* 은 **tinyint**, 기본값은 NULL입니다. 설정되어 있지 않으면 운영자는 경고 알림을 받을 수 없습니다.  
  
 [ @email_address=] '*email_address*'  
 운영자의 전자 메일 주소입니다. 이 문자열은 전자 메일 시스템으로 직접 전달됩니다. *email_address* 은 **nvarchar (100)**, 기본값은 NULL입니다.  
  
 [ @pager_address=] '*pager_number*'  
 운영자의 호출기 주소입니다. 이 문자열은 전자 메일 시스템으로 직접 전달됩니다. *pager_number* 은 **nvarchar (100)**, 기본값은 NULL입니다.  
  
 [ @weekday_pager_start_time=] *weekday_pager_start_time*  
 월요일부터 금요일까지 이 운영자에게 호출기 알림 전달을 시작할 수 있는 시간을 지정합니다. *weekday_pager_start_time*은 **int**, NULL, 기본값은 24 시간 시계와 사용 하기 위해 HHMMSS 형식으로 입력 해야 합니다.  
  
 [ @weekday_pager_end_time=] *weekday_pager_end_time*  
 월요일부터 금요일까지 지정한 운영자에게 호출기 알림 전달을 마쳐야 하는 시간을 지정합니다. *weekday_pager_end_time*은 **int**, NULL, 기본값은 24 시간 시계와 사용 하기 위해 HHMMSS 형식으로 입력 해야 합니다.  
  
 [ @saturday_pager_start_time=] *saturday_pager_start_time*  
 토요일에 지정한 운영자에게 호출기 알림 전달을 시작할 수 있는 시간을 지정합니다. *saturday_pager_start_time*은 **int**, NULL, 기본값은 24 시간 시계와 사용 하기 위해 HHMMSS 형식으로 입력 해야 합니다.  
  
 [ @saturday_pager_end_time=] *saturday_pager_end_time*  
 토요일에 지정한 운영자에게 호출기 알림 전달을 마쳐야 하는 시간을 지정합니다. *saturday_pager_end_time*은 **int**, NULL, 기본값은 24 시간 시계와 사용 하기 위해 HHMMSS 형식으로 입력 해야 합니다.  
  
 [ @sunday_pager_start_time=] *sunday_pager_start_time*  
 일요일에 지정한 운영자에게 호출기 알림 전달을 시작할 수 있는 시간을 지정합니다. *sunday_pager_start_time*은 **int**, NULL, 기본값은 24 시간 시계와 사용 하기 위해 HHMMSS 형식으로 입력 해야 합니다.  
  
 [ @sunday_pager_end_time=] *sunday_pager_end_time*  
 일요일에 지정한 운영자에게 호출기 알림 전달을 마쳐야 하는 시간을 지정합니다. *sunday_pager_end_time*은 **int**, NULL, 기본값은 24 시간 시계와 사용 하기 위해 HHMMSS 형식으로 입력 해야 합니다.  
  
 [ @pager_days=] *pager_days*  
 지정한 시작/종료 시간에 따라 운영자가 호출을 받을 수 있는 날을 지정합니다. *pager_days*은 **tinyint**, 기본값은 NULL이 고 사이의 값 이어야 하 고 **0** 통해 **127**합니다. *pager_days* 는 필요한 요일에 대 한 개별 값을 더하여 계산 합니다. 예를 들어 월요일부터 금요일까지 **2**+**4**+**8**+**16** + **32** = **64**합니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**1**|일요일|  
|**2**|월요일|  
|**4**|화요일|  
|**8**|수요일|  
|**16**|목요일|  
|**32**|금요일|  
|**64**|토요일|  
  
 [ @netsend_address=] '*netsend_address*'  
 네트워크 메시지가 전송되는 운영자의 네트워크 주소입니다. *netsend_address*은 **nvarchar (100)**, 기본값은 NULL입니다.  
  
 [ @category_name=] '*범주*'  
 이 경고에 대한 범주 이름입니다. *범주* 은 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 sp_update_operator는 msdb 데이터베이스에서 실행되어야 합니다.  
  
## <a name="permissions"></a>Permissions  
 이 프로시저를 실행할 수 있는 권한은 기본적으로 sysadmin 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 운영자의 상태를 설정으로 업데이트하고 호출 가능한 날을 월요일부터 금요일, 오전 8시부터 오후 5시까지로 설정합니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_operator   
    @name = N'François Ajenstat',  
    @enabled = 1,  
    @email_address = N'françoisa',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 64 ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_add_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
