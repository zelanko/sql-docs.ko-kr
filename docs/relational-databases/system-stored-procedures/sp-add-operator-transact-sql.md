---
title: sp_add_operator (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_operator
- sp_add_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_operator
ms.assetid: 817cd98a-4dff-4ed8-a546-f336c144d1e0
author: stevestein
ms.author: sstein
ms.openlocfilehash: f410024e1458d20e436df72cc2978ce41b5d60df
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "74095507"
---
# <a name="sp_add_operator-transact-sql"></a>sp_add_operator(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  경고 및 작업과 함께 사용할 운영자(알림 수신자)를 만듭니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_add_operator [ @name = ] 'name'   
     [ , [ @enabled = ] enabled ]   
     [ , [ @email_address = ] 'email_address' ]   
     [ , [ @pager_address = ] 'pager_address' ]   
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
`[ @name = ] 'name'`운영자 이름 (알림 받는 사람)입니다. 이 이름은 고유 해야 하며 백분율 (**%**) 문자를 포함할 수 없습니다. *name* 은 **sysname**이며 기본값은 없습니다.  
  
`[ @enabled = ] enabled`운영자의 현재 상태를 나타냅니다. *enabled* 는 **tinyint**이며 기본값은 **1** (사용)입니다. **0**인 경우에는 연산자를 사용할 수 없으며 알림이 수신 되지 않습니다.  
  
`[ @email_address = ] 'email_address'`운영자의 전자 메일 주소입니다. 이 문자열은 전자 메일 시스템으로 직접 전달됩니다. *email_address* 은 **nvarchar (100)** 이며 기본값은 NULL입니다.  
  
 *Email_address*에 대 한 실제 전자 메일 주소나 별칭을 지정할 수 있습니다. 예를 들어:  
  
 '**jdoe**' 또는 '**jdoe\@xyz.com**'  
  
> [!NOTE]  
>  데이터베이스 메일에서는 전자 메일 주소를 사용해야 합니다.  
  
`[ @pager_address = ] 'pager_address'`운영자의 호출기 주소입니다. 이 문자열은 전자 메일 시스템으로 직접 전달됩니다. *pager_address* 은 **nvarchar (100)** 이며 기본값은 NULL입니다.  
  
`[ @weekday_pager_start_time = ] weekday_pager_start_time`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 월요일부터 금요일 까지의 평일에 지정 된 운영자에 게 호출기 알림을 보내는 시간입니다. *weekday_pager_start_time*는 **int**이며 기본값은 **090000**입니다 .이는 9:00 A.M.를 나타냅니다. 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
`[ @weekday_pager_end_time = ] weekday_pager_end_time`**SQLServerAgent** 서비스가 월요일부터 금요일 까지의 평일에 지정 된 운영자에 게 호출기 알림을 더 이상 보내지 않는 시간입니다. *weekday_pager_end_time*는 **int**이며 기본값은 18만입니다 .이는 6:00 P.M.를 나타냅니다. 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
`[ @saturday_pager_start_time = ] saturday_pager_start_time`**SQLServerAgent** 서비스가 토요일에 지정 된 운영자에 게 호출기 알림을 보내는 시간입니다. *saturday_pager_start_time* 는 **int**이며 기본값은 090000입니다 .이는 9:00 A.M.를 나타냅니다. 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
`[ @saturday_pager_end_time = ] saturday_pager_end_time`**SQLServerAgent** 서비스가 토요일에 지정 된 운영자에 게 호출기 알림을 더 이상 보내지 않는 시간입니다. *saturday_pager_end_time*는 **int**이며 기본값은 **18만**입니다 .이는 6:00 P.M.를 나타냅니다. 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
`[ @sunday_pager_start_time = ] sunday_pager_start_time`**SQLServerAgent** 서비스가 일요일에 지정 된 운영자에 게 호출기 알림을 보내는 시간입니다. *sunday_pager_start_time*는 **int**이며 기본값은 **090000**입니다 .이는 9:00 A.M.를 나타냅니다. 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
`[ @sunday_pager_end_time = ] sunday_pager_end_time`**SQLServerAgent** 서비스가 일요일에 지정 된 운영자에 게 호출기 알림을 더 이상 보내지 않는 시간입니다. *sunday_pager_end_time*는 **int**이며 기본값은 **18만**입니다 .이는 6:00 P.M.를 나타냅니다. 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
`[ @pager_days = ] pager_days`지정 된 시작/종료 시간에 따라 운영자를 페이지에 사용할 수 있는 요일을 나타내는 숫자입니다. *pager_days*은 **tinyint**이며 기본값은 운영자가 페이지를 받을 수 없음을 나타내는 **0** 입니다. 유효한 값은 **0** 부터 **127**까지입니다. *pager_days*는 필요한 요일에 대 한 개별 값을 더하여 계산 됩니다. 예를 들어 월요일부터 금요일까지 **2**+**4**+**8**+**16**+**32** = **62**입니다. 다음 표에서는 각 요일에 대한 값을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|일요일|  
|**2**|월요일|  
|**4**|화요일|  
|**20cm(8**|수요일|  
|**x**|목요일|  
|**32**|금요일|  
|**64**|토요일|  
  
`[ @netsend_address = ] 'netsend_address'`네트워크 메시지가 전송 되는 운영자의 네트워크 주소입니다. *netsend_address*은 **nvarchar (100)** 이며 기본값은 NULL입니다.  
  
`[ @category_name = ] 'category'`이 연산자에 대 한 범주 이름입니다. *category* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>설명  
 **sp_add_operator** 는 **msdb** 데이터베이스에서 실행 해야 합니다.  
  
 호출은 전자 메일 시스템에 의해 지원되므로 호출 기능을 사용하려면 전자 메일에서 호출기로 전달되는 시스템이 있어야 합니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 작업 구조를 만들고 관리할 수 있는 바람직한 방법을 제공하는데 이는 그래픽을 사용하여 쉽게 작업을 관리할 수 있는 방법입니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_add_operator**를 실행할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `danwi`에 대한 운영자 정보를 설정합니다. 운영자가 설정되어 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 월요일부터 금요일, 오전 8시부터 오후 5시까지 호출기 알림을 보냅니다.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_operator  
    @name = N'Dan Wilson',  
    @enabled = 1,  
    @email_address = N'danwi',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 62 ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_delete_operator &#40;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [Transact-sql&#41;sp_help_operator &#40;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [Transact-sql&#41;sp_update_operator &#40;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
