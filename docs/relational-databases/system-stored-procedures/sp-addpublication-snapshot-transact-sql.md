---
title: sp_addpublication_snapshot (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addpublication_snapshot_TSQL
- sp_addpublication_snapshot
helpviewer_keywords:
- sp_addpublication_snapshot
ms.assetid: 192b6214-df6e-44a3-bdd4-9d933a981619
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 659d0b54238795663f1daea81332004f3c5bf7f3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32993310"
---
# <a name="spaddpublicationsnapshot-transact-sql"></a>sp_addpublication_snapshot(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 게시에 대해 스냅숏 에이전트를 만듭니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addpublication_snapshot [ @publication= ] 'publication'  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @snapshot_job_name = ] 'snapshot_agent_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication=**] **'***publication***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@frequency_type=**] *frequency_type*  
 스냅숏 에이전트가 실행되는 빈도입니다. *frequency_type* 은 **int**, 다음 값 중 하나가 될 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**1**|한 번|  
|**4** (기본값)|매일|  
|**8**|매주|  
|**16**|매월|  
|**32**|매월(frequency_interval에 따라 달라짐)|  
|**64**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 시작될 때|  
|**128**|컴퓨터가 유휴 상태일 때 실행|  
  
 [  **@frequency_interval=**] *frequency_interval*  
 값 설정 된 빈도에 적용 하려면 *frequency_type*합니다. *frequency_interval* 은 **int**, 다음 값 중 하나가 될 수 있습니다.  
  
|frequency_type 값|frequency_interval에 미치는 영향|  
|------------------------------|-----------------------------------|  
|**1**|*frequency_interval* 는 사용 되지 않습니다.|  
|**4** (기본값)|모든 *frequency_interval* 기본값 매일 일입니다.|  
|**8**|*frequency_interval* 은 다음 중 하나 이상을 (함께 [ &#124; (비트 OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md) 논리 연산자).<br /><br /> **1** = 일요일&#124;<br /><br /> **2** = 월요일&#124;<br /><br /> **4** = 화요일&#124;<br /><br /> **8** = 수요일&#124;<br /><br /> **16** = 목요일&#124;<br /><br /> **32** = 금요일&#124;<br /><br /> **64** = 토요일|  
|**16**|에 *frequency_interval* 해당 월의 일 합니다.|  
|**32**|*frequency_interval* 다음 중 하나입니다.<br /><br /> **1** = 일요일&#124;<br /><br /> **2** = 월요일&#124;<br /><br /> **3** = 화요일&#124;<br /><br /> **4** = 수요일&#124;<br /><br /> **5** = 목요일&#124;<br /><br /> **6** = 금요일&#124;<br /><br /> **7** = 토요일&#124;<br /><br /> **8** = 일&#124;<br /><br /> **9** = 평일&#124;<br /><br /> **10** = 주말|  
|**64**|*frequency_interval* 는 사용 되지 않습니다.|  
|**128**|*frequency_interval* 는 사용 되지 않습니다.|  
  
 [  **@frequency_subday=**] *frequency_subday*  
 에 대 한 단위 *freq_subday_interval*합니다. *frequency_subday* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|둘째|  
|**4** (기본값)|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 에 대 한 간격인 *frequency_subday*합니다. *frequency_subday_interval* 은 **int**, 기본값 5 의미 하는 5 분 마다.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 스냅숏 에이전트가 실행되는 날짜입니다. *frequency_relative_interval* 은 **int**, 기본값은 1입니다.  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 사용 하는 되풀이 비율 *frequency_type*합니다. *frequency_recurrence_factor* 은 **int**, 기본값은 0입니다.  
  
 [  **@active_start_date=**] *active_start_date*  
 스냅숏 에이전트가 처음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_start_date* 은 **int**, 기본값은 0입니다.  
  
 [  **@active_end_date=**] *active_end_date*  
 스냅숏 에이전트가 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_end_date* 은 **int**, 99991231 기본값은 9999 의미 하는 12 월 31 일입니다.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 하루 중 스냅숏 에이전트가 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_start_time_of_day* 은 **int**, 기본값은 0입니다.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 하루 중 스냅숏 에이전트가 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_end_time_of_day* 은 **int**, 오후 11시 59분: 59 235959 기본값, 즉 235959입니다.  
  
 [  **@snapshot_job_name =** ] **'***snapshot_agent_name***'**  
 기존 작업이 사용되는 경우 기존 스냅숏 에이전트 작업의 이름입니다. *snapshot_agent_name* 은 **nvarchar (100)** 이며 기본값은 NULL입니다. 이 매개 변수는 내부용이고 새 게시를 만들 때 지정되지 않아야 합니다. 경우 *snapshot_agent_name* 을 지정할 경우 *job_login* 및 *job_password* NULL 이어야 합니다.  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 게시자에 연결할 때 에이전트가 사용하는 보안 모드입니다. *publisher_security_mode* 은 **smallint**, 기본값은 1입니다. **0** 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 하 고 **1** Windows 인증을 지정 합니다. 값이 **0** 지정 해야 이외[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [ **@publisher_login**=] **'***publisher_login***'**  
 게시자에 연결할 때 사용하는 로그인입니다. *publisher_login* 은 **sysname**, 기본값은 NULL입니다. *publisher_login* 지정 해야 *publisher_security_mode* 은 **0**합니다. 경우 *publisher_login* null 및 *publisher_security_mode* 은 **1**에 지정 된 Windows 계정이 *job_login* 사용 됩니다 게시자에 연결 합니다.  
  
 [ **@publisher_password**=] **'***publisher_password***'**  
 게시자에 연결할 때 사용하는 암호입니다. *publisher_password* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 보안 향상을 위해 런타임에 로그인 이름과 암호를 제공하는 것이 좋습니다.  
  
 [ **@job_login**=] **'***job_login***'**  
 에이전트 실행에 사용되는 Windows 계정의 로그인입니다. *job_login* 은 **nvarchar (257)**, 기본값은 NULL입니다. 이 Windows 계정은 에이전트가 배포자에 연결할 때 항상 사용됩니다. 새 스냅숏 에이전트 작업을 만들 때는 이 매개 변수를 제공해야 합니다.  
  
> [!NOTE]  
>  에 대 한 비-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자의 경우에 지정 된 동일한 로그인 이어야 합니다. [sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)합니다.  
  
 [ **@job_password**=] **'***job_password***'**  
 에이전트 실행에 사용되는 Windows 계정의 암호입니다. *job_password* 은 **sysname**, 기본값은 없습니다. 새 스냅숏 에이전트 작업을 만들 때는 이 매개 변수를 제공해야 합니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 보안 향상을 위해 런타임에 로그인 이름과 암호를 제공하는 것이 좋습니다.  
  
 [ **@publisher**=] **'***게시자***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외의 게시자를 지정합니다. *게시자* 은 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 에서 스냅숏 에이전트를 만들 때 사용할 수 해야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_addpublication_snapshot** 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-snapsh_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_addpublication_snapshot**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md)   
 [스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-snapshot.md)   
 [sp_addpublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_startpublication_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
