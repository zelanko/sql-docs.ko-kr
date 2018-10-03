---
title: sp_addsubscriber (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscriber
- sp_addsubscriber_TSQL
helpviewer_keywords:
- sp_addsubscriber
ms.assetid: b8a584ea-2a26-4936-965b-b84f026e39c0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ec23f8c6fd28ba20522c6a2962d8af0c9f809a9c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825141"
---
# <a name="spaddsubscriber-transact-sql"></a>sp_addsubscriber(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  새 구독자를 게시자에 추가하여 게시한 내용을 받을 수 있도록 합니다. 이 저장 프로시저는 스냅숏 및 트랜잭션 게시를 위한 게시 데이터베이스의 게시자에서 실행됩니다. 원격 배포자를 사용하는 병합 게시의 경우에는 이 저장 프로시저가 배포자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  이 저장 프로시저는 더 이상 사용되지 않습니다. 더 이상 게시자에서 구독자를 명시적으로 등록할 필요가 없습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addsubscriber [ @subscriber = ] 'subscriber'  
    [ , [ @type = ] type ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @commit_batch_size = ] commit_batch_size ]  
    [ , [ @status_batch_size = ] status_batch_size ]  
    [ , [ @flush_frequency = ] flush_frequency ]  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @description = ] 'description' ]  
    [ , [ @security_mode = ] security_mode ]  
    [ , [ @encrypted_password = ] encrypted_password ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@subscriber=**] **'***구독자***'**  
 이 서버의 게시에 유효한 구독자로 추가되는 서버의 이름입니다. *구독자* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@type=**] *형식*  
 구독자의 유형입니다. *형식* 됩니다 **tinyint**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0** (기본값)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자|  
|**1**|ODBC 데이터 원본 서버|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet 데이터베이스|  
|**3**|OLE DB 공급자|  
  
 [  **@login=**] **'***로그인***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 대한 로그인 ID입니다. *login*은 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제에 지정 된 구독 단위로 실행할 때 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@password=**] **'***암호***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 위한 암호입니다. *암호* 됩니다 **nvarchar(524)**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제에 지정 된 구독 단위로 실행할 때 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@commit_batch_size=**] *commit_batch_size*  
 이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다.  
  
> [!NOTE]  
>  값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@status_batch_size=**] *status_batch_size*  
 이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다.  
  
> [!NOTE]  
>  값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@flush_frequency=**] *flush_frequency*  
 이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다.  
  
> [!NOTE]  
>  값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@frequency_type=**] *frequency_type*  
 복제 에이전트를 예약하는 빈도입니다. *frequency_type* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|요청 시|  
|**4**|일별|  
|**8**|매주|  
|**16**|매월|  
|**32**|매월 상대적|  
|**64** (기본값)|자동 시작|  
|**128**|되풀이|  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제에 지정 된 구독 단위로 실행할 때 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [**@frequency_interval=** ] *frequency_interval*  
 설정 된 빈도에 적용 된 값인 *frequency_type*합니다. *frequency_interval* 됩니다 **int**, 기본값은 1입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제에 지정 된 구독 단위로 실행할 때 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 복제 에이전트의 날짜입니다. 이 매개 변수를 사용 하면 *frequency_type* 로 설정 된 **32** (매월 상대적)입니다. *frequency_relative_interval* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1** (기본값)|첫째|  
|**2**|둘째|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제에 지정 된 구독 단위로 실행할 때 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 사용 하는 되풀이 비율 *frequency_type*합니다. *frequency_recurrence_factor* 됩니다 **int**, 기본값은 **0**합니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제에 지정 된 구독 단위로 실행할 때 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 정의된 기간 동안 다시 예약하는 빈도입니다. *frequency_subday* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|둘째|  
|**4** (기본값)|Minute|  
|**8**|Hour|  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제에 지정 된 구독 단위로 실행할 때 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 에 대 한 간격인 *frequency_subday*합니다. *frequency_subday_interval* 됩니다 **int**, 기본값은 **5**합니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제에 지정 된 구독 단위로 실행할 때 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 하루 중에서 복제 에이전트가 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_start_time_of_day* 됩니다 **int**, 기본값은 **0**합니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제에 지정 된 구독 단위로 실행할 때 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 하루 중에서 복제 에이전트가 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_end_time_of_day*됩니다 **int**, 이며 기본값은 235959 의미 하는 오후 11시 59분: 59 235959입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제에 지정 된 구독 단위로 실행할 때 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@active_start_date=**] *active_start_date*  
 복제 에이전트가 처음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_start_date* 됩니다 **int**, 기본값은 0입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제에 지정 된 구독 단위로 실행할 때 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@active_end_date=**] *active_end_date*  
 복제 에이전트가 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_end_date* 됩니다 **int**, 이며 기본값은 99991231 의미 하는 12 월 31 일에서 9999입니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제에 지정 된 구독 단위로 실행할 때 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@description=**] **'***설명***'**  
 구독자에 관한 텍스트 설명입니다. *설명* 됩니다 **nvarchar(255)**, 기본값은 NULL입니다.  
  
 [  **@security_mode=**] *security_mode*  
 구현된 보안 모드입니다. *security_mode* 됩니다 **int**, 기본값은 1입니다. **0** 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다. **1** Windows 인증을 지정 합니다.  
  
> [!NOTE]  
>  이 매개 변수는 더 이상 사용되지 않으며 이전 버전 스크립트와의 호환성을 위해 유지 관리됩니다. 속성은 이제에 지정 된 구독 단위로 실행할 때 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)합니다. 값을 지정하면 해당 값은 이 구독자에서 구독을 만들 때 기본값으로 사용되며 경고 메시지가 반환됩니다.  
  
 [  **@encrypted_password=**] *encrypted_password*  
 이 매개 변수 사용 되지 않으며 설정에 이전 버전과 호환성을 위해 제공 됩니다 *encrypted_password* 값으로 있지만 **0** 오류가 발생 합니다.  
  
 [ **@publisher**=] **'***게시자***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외의 게시자를 지정합니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 해서는 안에서 게시 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_addsubscriber** 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
 **sp_addsubscriber** 구독자는 병합 게시에 대 한 익명 구독만 있으면 때는 필요 하지 않습니다.  
  
 **sp_addsubscriber** 쓸 합니다 [MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md) 테이블에 **배포** 데이터베이스입니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_addsubscriber**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [sp_changesubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)  
  
  
