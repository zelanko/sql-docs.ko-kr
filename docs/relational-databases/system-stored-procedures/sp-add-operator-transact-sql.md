---
title: sp_add_operator (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_operator
- sp_add_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_operator
ms.assetid: 817cd98a-4dff-4ed8-a546-f336c144d1e0
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cfb553006c52cad2595bc75666988fab93e2b165
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spaddoperator-transact-sql"></a>sp_add_operator(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  경고 및 작업과 함께 사용할 운영자(알림 수신자)를 만듭니다.  
  
 
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@name=** ] **'***name***'**  
 운영자(알림 수신자)의 이름입니다. 이 이름은 고유 해야 하며 퍼센트를 포함할 수 없습니다 (**%**) 문자. *이름* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@enabled=** ] *enabled*  
 운영자의 현재 상태를 나타냅니다. *활성화* 은 **tinyint**, 기본값은 **1** (사용). 경우 **0**, 연산자는 사용 되지 않으며 알림을 받지 않습니다.  
  
 [ **@email_address=** ] **'***email_address***'**  
 운영자의 전자 메일 주소입니다. 이 문자열은 전자 메일 시스템으로 직접 전달됩니다. *email_address* 은 **nvarchar (100)**, 기본값은 NULL입니다.  
  
 실제 전자 메일 주소 또는 별칭을 지정할 수 있습니다 *email_address*합니다. 예를 들어:  
  
 '**jdoe**'또는'**jdoe@xyz.com**'  
  
> [!NOTE]  
>  데이터베이스 메일에서는 전자 메일 주소를 사용해야 합니다.  
  
 [ **@pager_address=** ] **'***pager_address***'**  
 운영자의 호출기 주소입니다. 이 문자열은 전자 메일 시스템으로 직접 전달됩니다. *pager_address* 은 **narchar(100)**, 기본값은 NULL입니다.  
  
 [ **@weekday_pager_start_time=** ] *weekday_pager_start_time*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 월요일부터 금요일까지의 평일에 지정된 운영자에게 호출기 알림을 보내는 시간입니다. *weekday_pager_start_time*은 **int**, 기본값은 **090000**, 오전 9 시를 나타내는 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
 [ **@weekday_pager_end_time=** ] *weekday_pager_end_time*  
 시간 **SQLServerAgent** 서비스에 더 이상 보내는 호출기 알림 전달을 시작할 지정 된 운영자에 게 평일에 월요일부터 금요일까지 합니다. *weekday_pager_end_time*은 **int**, 오후 6 시를 나타내는 180000 기본적으로 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
 [ **@saturday_pager_start_time =**] *saturday_pager_start_time*  
 시간 **SQLServerAgent** 서비스가 토요일에 지정한 운영자 호출기 알림을 보냅니다. *saturday_pager_start_time* 은 **int**, 오전 9 시를 나타내는 090000의 기본값 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
 [ **@saturday_pager_end_time=** ] *saturday_pager_end_time*  
 시간 **SQLServerAgent** 서비스 호출기 알림이 지정된 된 운영자 토요일에 더 이상 보내는 합니다. *saturday_pager_end_time*은 **int**, 기본값은 **180000**, 오후 6 시를 나타내는 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
 [ **@sunday_pager_start_time=** ] *sunday_pager_start_time*  
 시간 **SQLServerAgent** 서비스가 일요일에 지정한 운영자 호출기 알림을 보냅니다. *sunday_pager_start_time*은 **int**, 기본값은 **090000**, 오전 9 시를 나타내는 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
 [ **@sunday_pager_end_time =**] *sunday_pager_end_time*  
 시간 **SQLServerAgent** 서비스 호출기 알림이 지정된 된 운영자 일요일에 더 이상 보내는 합니다. *sunday_pager_end_time*은 **int**, 기본값은 **180000**, 오후 6 시를 나타내는 이때 시간은 HHMMSS 형식으로 입력해야 합니다.  
  
 [ **@pager_days=** ] *pager_days*  
 운영자가 지정된 시작/종료 시간에 따라 호출할 수 있는 요일을 나타내는 숫자입니다. *pager_days*은 **tinyint**, 기본값은 **0** 연산자가 없음을 나타내는 페이지를 받을 수 있습니다. 유효한 값은 **0** 통해 **127**합니다. *pager_days*는 필요한 요일에 대 한 개별 값을 더하여 계산 합니다. 예를 들어 월요일부터 금요일까지 **2**+**4**+**8**+**16** + **32** = **62**합니다. 다음 표에서는 각 요일에 대한 값을 나열합니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**1**|일요일|  
|**2**|월요일|  
|**4**|화요일|  
|**8**|수요일|  
|**16**|목요일|  
|**32**|금요일|  
|**64**|토요일|  
  
 [ **@netsend_address=** ] **'***netsend_address***'**  
 네트워크 메시지가 전송되는 운영자의 네트워크 주소입니다. *netsend_address*은 **nvarchar (100)**, 기본값은 NULL입니다.  
  
 [  **@category_name=** ] **'***범주***'**  
 이 운영자에 대한 범주 이름입니다. *범주* 은 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 **sp_add_operator** 에서 실행 되어야 합니다는 **msdb** 데이터베이스입니다.  
  
 호출은 전자 메일 시스템에 의해 지원되므로 호출 기능을 사용하려면 전자 메일에서 호출기로 전달되는 시스템이 있어야 합니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 작업 구조를 만들고 관리할 수 있는 바람직한 방법을 제공하는데 이는 그래픽을 사용하여 쉽게 작업을 관리할 수 있는 방법입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_add_operator**합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [sp_delete_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_update_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
