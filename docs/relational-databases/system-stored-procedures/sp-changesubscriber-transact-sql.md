---
title: sp_changesubscriber (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_changesubscriber
- sp_changesubscriber_TSQL
helpviewer_keywords: sp_changesubscriber
ms.assetid: d453c451-e957-490f-b968-5e03aeddaf10
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b52c51d2e516b8d4c4f787c8e5d56d95922b2d4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spchangesubscriber-transact-sql"></a>sp_changesubscriber(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  구독자에 대한 옵션을 변경합니다. 구독자에 대한 모든 배포 태스크가 이 게시자로 업데이트됩니다. 이 저장된 프로시저에 기록 된 **MSsubscriber_info** 배포 데이터베이스의 테이블입니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changesubscriber [ @subscriber= ] 'subscriber'  
    [ , [ @type= ] type ]  
    [ , [ @login= ] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @commit_batch_size= ] commit_batch_size ]  
    [ , [ @status_batch_size= ] status_batch_size ]  
    [ , [ @flush_frequency= ] flush_frequency ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @security_mode= ] security_mode ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@subscriber=**] **'***구독자***'**  
 옵션을 변경할 대상이 되는 구독자의 이름입니다. *구독자* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@type=**] *유형*  
 구독자 유형입니다. *형식* 은 **tinyint**, 기본값은 NULL입니다. **0** 나타냅니다는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다. **1** 지정 이외의[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 기타 ODBC 데이터 원본 서버 구독자입니다.  
  
 [  **@login=**] **'***로그인***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인 ID입니다. *로그인* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@password=**] **'***암호***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 암호입니다. *암호* 은 **sysname**, 기본값은  **%** 합니다. **%**password 속성에 변경 내용이 없는지를 나타냅니다.  
  
 [  **@commit_batch_size=**] *commit_batch_size*  
 이전 버전과의 호환성을 위해서만 지원됩니다.  
  
 [  **@status_batch_size=**] *status_batch_size*  
 이전 버전과의 호환성을 위해서만 지원됩니다.  
  
 [  **@flush_frequency=**] *flush_frequency*  
 이전 버전과의 호환성을 위해서만 지원됩니다.  
  
 [  **@frequency_type=**] *frequency_type*  
 배포 태스크를 예약하는 빈도입니다. *frequency_type* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|요청 시|  
|**4**|일별|  
|**8**|매주|  
|**16**|매월|  
|**32**|매월 상대적|  
|**64**|자동 시작|  
|**128**|되풀이|  
  
 [  **@frequency_interval=**] *frequency_interval*  
 에 대 한 간격인 *frequency_type*합니다. *frequency_interval* 은 **int**, 기본값은 NULL입니다.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 배포 태스크 날짜입니다. 이 매개 변수는 때 *frequency_type* 로 설정 된 **32** (매월 상대)입니다. *frequency_relative_interval* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1**|첫째|  
|**2**|둘째|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 배포 작업이 정의 된 기간 동안 되풀이 되는 얼마나 자주 *frequency_type*합니다. *frequency_recurrence_factor* 은 **int**, 기본값은 NULL입니다.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 정의된 기간 동안 다시 예약하는 빈도입니다. *frequency_subday* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|둘째|  
|**4**|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 에 대 한 간격인 *frequence_subday*합니다. *frequency_subday_interval* 은 **int**, 기본값은 NULL입니다.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 하루 중에서 배포 태스크가 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_start_time_of_day* 은 **int**, 기본값은 NULL입니다.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 하루 중에서 배포 태스크가 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_end_time_of_day*은 **int**, 기본값은 NULL입니다.  
  
 [  **@active_start_date=**] *active_start_date*  
 배포 태스크가 처음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_start_date* 은 **int**, 기본값은 NULL입니다.  
  
 [  **@active_end_date=**] *active_end_date*  
 배포 태스크가 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_end_date*은 **int**, 기본값은 NULL입니다.  
  
 [  **@description=**] **'***설명***'**  
 선택적인 텍스트 설명입니다. *설명* 은 **nvarchar (255)**, 기본값은 NULL입니다.  
  
 [  **@security_mode=**] *security_mode*  
 구현된 보안 모드입니다. *security_mode* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증|  
|**1**|Windows 인증|  
  
 [  **@publisher** =] **'***게시자***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외의 게시자를 지정합니다. *게시자* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 에서 아티클 속성을 변경 하는 경우 사용할 수 해야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_changesubscriber** 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_changesubscriber**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_addsubscriber&#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributiondb&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [sp_helpserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
