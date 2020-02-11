---
title: sp_addpublication_snapshot (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_snapshot_TSQL
- sp_addpublication_snapshot
helpviewer_keywords:
- sp_addpublication_snapshot
ms.assetid: 192b6214-df6e-44a3-bdd4-9d933a981619
author: stevestein
ms.author: sstein
ms.openlocfilehash: c32ea67eef368a17b129989e3f05c29ab0533d72
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68769107"
---
# <a name="sp_addpublication_snapshot-transact-sql"></a>sp_addpublication_snapshot(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  지정된 게시에 대해 스냅샷 에이전트를 만듭니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용 &#40;SQL Server 구성 관리자&#41;을 ](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)참조 하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @frequency_type = ] frequency_type`스냅숏 에이전트 실행 되는 빈도입니다. *frequency_type* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**4** (기본값)|매일|  
|**20cm(8**|매주|  
|**x**|매월|  
|**32**|매월(frequency_interval에 따라 달라짐)|  
|**64**|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 시작될 때|  
|**128**|컴퓨터가 유휴 상태일 때 실행|  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*에 의해 설정 된 빈도에 적용 되는 값입니다. *frequency_interval* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|frequency_type 값|frequency_interval에 미치는 영향|  
|------------------------------|-----------------------------------|  
|**1**|*frequency_interval* 사용 되지 않습니다.|  
|**4** (기본값)|매일 *frequency_interval* 매일 (기본값)을 사용 합니다.|  
|**20cm(8**|*frequency_interval* 은 [&#124; (비트 or)](../../t-sql/language-elements/bitwise-or-transact-sql.md) 논리 연산자와 결합 된 다음 중 하나 이상입니다.<br /><br /> **1** = 일요일 &#124;<br /><br /> **2** = 월요일 &#124;<br /><br /> **4** = 화요일 &#124;<br /><br /> **8** = 수요일 &#124;<br /><br /> **16** = 목요일 &#124;<br /><br /> **32** = 금요일 &#124;<br /><br /> **64** = 토요일|  
|**x**|월의 *frequency_interval* 날짜|  
|**32**|*frequency_interval* 은 다음 중 하나입니다.<br /><br /> **1** = 일요일 &#124;<br /><br /> **2** = 월요일 &#124;<br /><br /> **3** = 화요일 &#124;<br /><br /> **4** = 수요일 &#124;<br /><br /> **5** = 목요일 &#124;<br /><br /> **6** = 금요일 &#124;<br /><br /> **7** = 토요일 &#124;<br /><br /> **8** = 일 &#124;<br /><br /> **9** = 평일 &#124;<br /><br /> **10** = 주말|  
|**64**|*frequency_interval* 사용 되지 않습니다.|  
|**128**|*frequency_interval* 사용 되지 않습니다.|  
  
`[ @frequency_subday = ] frequency_subday`는 *freq_subday_interval*단위입니다. *frequency_subday* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|Second|  
|**4** (기본값)|분|  
|**20cm(8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*에 대 한 간격입니다. *frequency_subday_interval* 은 **int**이며 기본값은 5 분 간격을 의미 하는 5입니다.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`스냅숏 에이전트 실행 되는 날짜입니다. *frequency_relative_interval* 은 **int**이며 기본값은 1입니다.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*에서 사용 하는 되풀이 비율입니다. *frequency_recurrence_factor* 은 **int**이며 기본값은 0입니다.  
  
`[ @active_start_date = ] active_start_date`스냅숏 에이전트 처음으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_start_date* 은 **int**이며 기본값은 0입니다.  
  
`[ @active_end_date = ] active_end_date`스냅숏 에이전트가 마지막으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_end_date* 는 **int**이며 기본값은 9999 년 12 월 31 일을 의미 하는 99991231입니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`하루 중 스냅숏 에이전트 처음으로 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_start_time_of_day* 은 **int**이며 기본값은 0입니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`하루 중 스냅숏 에이전트이 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_end_time_of_day* 은 **int**이며 기본값은 235959입니다 .이는 11:59:59 오후을 의미 합니다. 235959입니다.  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'`기존 작업을 사용 하는 경우 기존 스냅숏 에이전트 작업 이름의 이름입니다. *snapshot_agent_name* 은 **nvarchar (100)** 이며 기본값은 NULL입니다. 이 매개 변수는 내부용이고 새 게시를 만들 때 지정되지 않아야 합니다. *Snapshot_agent_name* 지정 된 경우 *job_login* 및 *job_password* 은 NULL 이어야 합니다.  
  
`[ @publisher_security_mode = ] publisher_security_mode`게시자에 연결할 때 에이전트가 사용 하는 보안 모드입니다. *publisher_security_mode* 은 **smallint**이며 기본값은 1입니다. **0** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 지정 하 고, **1** 은 Windows 인증을 지정 합니다. 비- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자에 대해 **0** 값을 지정 해야 합니다. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`게시자에 연결할 때 사용 되는 로그인입니다. *publisher_login* 는 **sysname**이며 기본값은 NULL입니다. *publisher_security_mode* **0**인 경우 *publisher_login* 를 지정 해야 합니다. *Publisher_login* 가 NULL이 고 *publisher_security_mode* 가 **1**이면 게시자에 연결할 때 *job_login* 에 지정 된 계정이 사용 됩니다.  
  
`[ @publisher_password = ] 'publisher_password'`게시자에 연결할 때 사용 되는 암호입니다. *publisher_password* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 보안 향상을 위해 런타임에 로그인 이름과 암호를 제공하는 것이 좋습니다.  
  
`[ @job_login = ] 'job_login'`에이전트를 실행 하는 계정에 대 한 로그인입니다. Azure SQL Database Managed Instance에서 SQL Server 계정을 사용 합니다. *job_login* 은 **nvarchar (257)** 이며 기본값은 NULL입니다. 이 계정은 항상 배포자에 대 한 에이전트 연결에 사용 됩니다. 새 스냅샷 에이전트 작업을 만들 때는 이 매개 변수를 제공해야 합니다.  
  
> [!NOTE]
>  이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자의 경우에는 [sp_adddistpublisher &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)에 지정 된 것과 동일한 로그인 이어야 합니다.  
  
`[ @job_password = ] 'job_password'`에이전트를 실행 하는 Windows 계정의 암호입니다. *job_password* 는 **sysname**이며 기본값은 없습니다. 새 스냅샷 에이전트 작업을 만들 때는 이 매개 변수를 제공해야 합니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 보안 향상을 위해 런타임에 로그인 이름과 암호를 제공하는 것이 좋습니다.  
  
`[ @publisher = ] 'publisher'`이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정 합니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  ** 게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스냅숏 에이전트를 만들 때 게시자를 사용 하면 안 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addpublication_snapshot** 는 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-snapsh_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_addpublication_snapshot**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Transact-sql&#41;sp_addpublication &#40;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [Transact-sql&#41;sp_changepublication_snapshot &#40;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [Transact-sql&#41;sp_startpublication_snapshot &#40;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
