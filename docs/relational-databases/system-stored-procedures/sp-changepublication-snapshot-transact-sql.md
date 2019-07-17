---
title: sp_changepublication_snapshot (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changepublication_snapshot_TSQL
- sp_changepublication_snapshot
helpviewer_keywords:
- sp_changepublication_snapshot
ms.assetid: 518a4618-3592-4edc-8425-cbc33cdff891
author: stevestein
ms.author: sstein
ms.openlocfilehash: f17f8b8dc95d7f99a969572658ab80bb6c22c433
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124884"
---
# <a name="spchangepublicationsnapshot-transact-sql"></a>sp_changepublication_snapshot(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 게시에 대한 스냅샷 에이전트의 속성을 변경합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changepublication_snapshot [ @publication= ] 'publication'  
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
`[ @publication = ] 'publication'` 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @frequency_type = ] frequency_type` 에이전트를 예약 하는 빈도입니다. *frequency_type* 됩니다 **int**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|요청 시|  
|**4**|일별|  
|**8**|매주|  
|**16**|매월|  
|**32**|매월 상대적|  
|**64**|자동 시작|  
|**128**|되풀이|  
|NULL(기본값)||  
  
`[ @frequency_interval = ] frequency_interval` 에이전트가 실행 되는 날짜를 지정 합니다. *frequency_interval* 됩니다 **int**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|일요일|  
|**2**|월요일|  
|**3**|화요일|  
|**4**|수요일|  
|**5**|목요일|  
|**6**|금요일|  
|**7**|토요일|  
|**8**|Day|  
|**9**|평일|  
|**10**|주말|  
|NULL(기본값)||  
  
`[ @frequency_subday = ] frequency_subday` 단위입니다 *freq_subday_interval*합니다. *frequency_subday* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
|NULL(기본값)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 에 대 한 간격인 *frequency_subday*합니다. *frequency_subday_interval* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 스냅숏 에이전트가 실행 될 날짜가입니다. *frequency_relative_interval* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 사용 하는 되풀이 비율 *frequency_type*합니다. *frequency_recurrence_factor* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @active_start_date = ] active_start_date` 가 경우 스냅숏 에이전트 첫 번째 예약 된 날짜 이며 YYYYMMDD 형식으로 합니다. *active_start_date* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @active_end_date = ] active_end_date` 날짜에서 스냅숏 에이전트가 예약 된 형식은 YYYYMMDD입니다. *active_end_date* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 스냅숏 에이전트가 처음 하루 중 시간 예약 된 hhmmss입니다. *active_start_time_of_day* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 하루 중 스냅숏 에이전트에 예약 된 형식은 HHMMSS입니다. *active_end_time_of_day* 됩니다 **int**, 기본값은 NULL입니다.  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'` 기존 작업을 사용 하는 경우 기존 스냅숏 에이전트 작업의 이름이입니다. *snapshot_agent_name* 됩니다 **nvarchar(100)** 이며 기본값은 NULL입니다.  
  
`[ @publisher_security_mode = ] publisher_security_mode` 보안 모드는 에이전트에서 게시자에 연결할 때. *publisher_security_mode* 됩니다 **smallint**, 기본값은 NULL입니다. **0** 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 하 고 **1** Windows 인증을 지정 합니다. 값이 **0** 를 지정 해야 이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'` 로그인에 게시자에 연결할 때 사용 됩니다. *publisher_login* 됩니다 **sysname**, 기본값은 NULL입니다. *publisher_login* 시기를 지정 해야 합니다 *publisher_security_mode* 됩니다 **0**합니다. 하는 경우 *publisher_login* 가 NULL 및 *publisher_security_mode* 됩니다 **1**에 지정 된 Windows 계정이 *job_login* 될 때 사용 됩니다 게시자에 연결합니다.  
  
`[ @publisher_password = ] 'publisher_password'` 게시자에 연결할 때 암호가 사용 됩니다. *publisher_password* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요. 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
`[ @job_login = ] 'job_login'` 에이전트가 실행 되는 Windows 계정의 로그인이입니다. *job_login* 됩니다 **nvarchar(257)** , 기본값은 NULL입니다. 이 Windows 계정은 에이전트가 배포자에 연결할 때 항상 사용됩니다. 새 스냅샷 에이전트 작업을 만들 때는 이 매개 변수를 제공해야 합니다. 이외에 대 한 변경할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
`[ @job_password = ] 'job_password'` 에이전트가 실행 되는 Windows 계정의 암호가입니다. *job_password* 됩니다 **sysname**, 기본값은 NULL입니다. 새 스냅샷 에이전트 작업을 만들 때는 이 매개 변수를 제공해야 합니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
`[ @publisher = ] 'publisher'` 지정 된 비- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 해서는 안에서 스냅숏 에이전트를 만들 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changepublication_snapshot** 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_changepublication_snapshot**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
