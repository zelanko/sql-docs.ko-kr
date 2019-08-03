---
title: sp_addpushsubscription_agent (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpushsubscription_agent_TSQL
- sp_addpushsubscription_agent
helpviewer_keywords:
- sp_addpushsubscription_agent
ms.assetid: 1fdd2052-50d8-4318-8aa7-fc635d5cad18
author: stevestein
ms.author: sstein
ms.openlocfilehash: 754180cfa1ff907e9590b70ba074cd28eaaa804e
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769087"
---
# <a name="spaddpushsubscriptionagent-transact-sql"></a>sp_addpushsubscription_agent(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  밀어넣기 구독을 동기화하기 위한 새로 예약된 에이전트 작업을 트랜잭션 게시에 추가합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  게시자를 원격 배포자로 구성할 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 전송됩니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_addpushsubscription_agent [ @publication= ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @job_name = ] 'job_name' ]   
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
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @distribution_job_name = ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @subscriber_provider = ] 'subscriber_provider' ]   
    [ , [ @subscriber_datasrc = ] 'subscriber_datasrc' ]   
    [ , [ @subscriber_location = ] 'subscriber_location' ]  
    [ , [ @subscriber_provider_string = ] 'subscriber_provider_string' ]   
    [ , [ @subscriber_catalog = ] 'subscriber_catalog' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @subscriber = ] 'subscriber'`구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscriber_db = ] 'subscriber_db'`구독 데이터베이스의 이름입니다. *subscriber_db* 는 **sysname**이며 기본값은 NULL입니다. SQL Server 이외 구독자의 경우 *subscriber_db*에 대 한 **(기본 대상)** 값을 지정 합니다.  
  
`[ @subscriber_security_mode = ] subscriber_security_mode`동기화 시 구독자에 연결할 때 사용 하는 보안 모드입니다. *subscriber_security_mode* 은 **int**이며 기본값은 1입니다. **0** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 지정 합니다. **1** 은 Windows 인증을 지정 합니다.  
  
> [!IMPORTANT]  
>  지연 업데이트 구독의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 구독자에 연결하고 각 구독자로의 연결에는 다른 계정을 지정합니다. 다른 모든 구독에는 Windows 인증을 사용합니다.  
  
`[ @subscriber_login = ] 'subscriber_login'`동기화 할 때 구독자에 연결 하는 데 사용할 구독자 로그인입니다. *subscriber_login* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscriber_password = ] 'subscriber_password'`구독자 암호입니다. *subscriber_security_mode* 가 **0**으로 설정 된 경우 *subscriber_password* 가 필요 합니다. *subscriber_password* 는 **sysname**이며 기본값은 NULL입니다. 구독자 암호가 사용되는 경우에는 자동으로 암호화됩니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요. 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
`[ @job_login = ] 'job_login'`에이전트를 실행 하는 계정에 대 한 로그인입니다. Azure SQL Database Managed Instance에서 SQL Server 계정을 사용 합니다. *job_login* 은 **nvarchar (257)** 이며 기본값은 NULL입니다. Windows 통합 인증을 사용할 때 배포자에 대한 에이전트 연결과 구독자에 대한 연결에 항상 이 Windows 계정을 사용합니다.  
  
`[ @job_password = ] 'job_password'`에이전트를 실행 하는 계정의 암호입니다. *job_password* 는 **sysname**이며 기본값은 없습니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
`[ @job_name = ] 'job_name'`기존 에이전트 작업의 이름입니다. *job_name* 는 **sysname**이며 기본값은 NULL입니다. 이 매개 변수는 새로 만든 작업(기본값) 대신 기존 작업을 사용하여 구독이 동기화될 경우에만 지정됩니다. **Sysadmin** 고정 서버 역할의 멤버가 아닌 경우 *job_name*을 지정할 때 *job_login* 및 *job_password* 를 지정 해야 합니다.  
  
`[ @frequency_type = ] frequency_type`배포 에이전트 일정을 예약 하는 빈도입니다. *frequency_type* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
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
>  **64** 값을 지정 하면 배포 에이전트 연속 모드로 실행 됩니다. 이는 에이전트에 대 한 **-연속** 매개 변수 설정에 해당 합니다. 자세한 내용은 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)을 참조하세요.  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*에 의해 설정 된 빈도에 적용 되는 값입니다. *frequency_interval* 은 **int**이며 기본값은 1입니다.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`배포 에이전트 날짜입니다. 이 매개 변수는 *frequency_type* 이 **32** (매월 상대적)로 설정 된 경우에 사용 됩니다. *frequency_relative_interval* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1** (기본값)|첫째|  
|**2**|Second|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*에서 사용 하는 되풀이 비율입니다. *frequency_recurrence_factor* 은 **int**이며 기본값은 0입니다.  
  
`[ @frequency_subday = ] frequency_subday`정의 된 기간 동안 다시 예약 하는 빈도입니다. *frequency_subday* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|Second|  
|**4** (기본값)|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*에 대 한 간격입니다. *frequency_subday_interval* 는 **int**이며 기본값은 5입니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`하루 중 배포 에이전트 처음으로 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_start_time_of_day* 은 **int**이며 기본값은 0입니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`하루 중 배포 에이전트이 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_end_time_of_day* 는 **int**이며 기본값은 235959입니다.  
  
`[ @active_start_date = ] active_start_date`배포 에이전트 처음으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_start_date* 은 **int**이며 기본값은 0입니다.  
  
`[ @active_end_date = ] active_end_date`배포 에이전트가 마지막으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_end_date* 는 **int**이며 기본값은 99991231입니다.  
  
`[ @dts_package_name = ] 'dts_package_name'`DTS (데이터 변환 서비스) 패키지의 이름을 지정 합니다. *dts_package_name* 는 **sysname** 이며 기본값은 NULL입니다. 예를 들어 `DTSPub_Package`의 패키지 이름을 지정하려면 매개 변수가 `@dts_package_name = N'DTSPub_Package'`여야 합니다.  
  
`[ @dts_package_password = ] 'dts_package_password'`패키지를 실행 하는 데 필요한 암호를 지정 합니다. *dts_package_password* 는 **sysname** 이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *Dts_package_name* 가 지정 된 경우 암호를 지정 해야 합니다.  
  
`[ @dts_package_location = ] 'dts_package_location'`패키지 위치를 지정 합니다. *dts_package_location* 은 **nvarchar (12)** 이며 기본값은 배포자입니다. 패키지의 위치는 **배포자** 또는 **구독자**일 수 있습니다.  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'`동기화 관리자를 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 구독을 동기화 할 수 있는지 여부입니다. *enabled_for_syncmgr* 은 **nvarchar (5)** 이며 기본값은 FALSE입니다. **False**이면 구독이 동기화 관리자에 등록 되지 않습니다. **True**이면 구독이 동기화 관리자에 등록 되며를 시작 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]하지 않고 동기화 할 수 있습니다.  
  
`[ @distribution_job_name = ] 'distribution_job_name'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @subscriber_provider = ] 'subscriber_provider'`비 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본에 대 한 OLE DB 공급자가 등록 되는 고유한 PROGID (프로그래밍 식별자)입니다. *subscriber_provider* 는 **sysname**이며 기본값은 NULL입니다. *subscriber_provider* 는 배포자에 설치 된 OLE DB 공급자에 대해 고유 해야 합니다. *subscriber_provider* 은 이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자에 대해서만 지원 됩니다.  
  
`[ @subscriber_datasrc = ] 'subscriber_datasrc'`OLE DB 공급자가 인식 하는 데이터 원본의 이름입니다. *subscriber_datasrc* 는 **nvarchar (4000)** 이며 기본값은 NULL입니다. *subscriber_datasrc* 는 OLE DB 공급자를 초기화 하는 DBPROP_INIT_DATASOURCE 속성으로 전달 됩니다. *subscriber_datasrc* 은 이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자에 대해서만 지원 됩니다.  
  
`[ @subscriber_location = ] 'subscriber_location'`는 OLE DB 공급자가 이해 하는 데이터베이스의 위치입니다. *subscriber_location* 는 **nvarchar (4000)** 이며 기본값은 NULL입니다. *subscriber_location* 는 OLE DB 공급자를 초기화 하는 DBPROP_INIT_LOCATION 속성으로 전달 됩니다. *subscriber_location* 은 이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자에 대해서만 지원 됩니다.  
  
`[ @subscriber_provider_string = ] 'subscriber_provider_string'`데이터 원본을 식별 하는 OLE DB 공급자별 연결 문자열입니다. *subscriber_provider_string* 는 **nvarchar (4000)** 이며 기본값은 NULL입니다. *subscriber_provider_string* 을 IDataInitialize에 전달 하거나 DBPROP_INIT_PROVIDERSTRING 속성으로 설정 하 여 OLE DB 공급자를 초기화 합니다. *subscriber_provider_string* 은 이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자에 대해서만 지원 됩니다.  
  
`[ @subscriber_catalog = ] 'subscriber_catalog'`OLE DB 공급자에 연결할 때 사용 되는 카탈로그입니다. *subscriber_catalog* 는 **sysname**이며 기본값은 NULL입니다. *subscriber_catalog* 는 OLE DB 공급자를 초기화 하는 DBPROP_INIT_CATALOG 속성으로 전달 됩니다. *subscriber_catalog* 은 이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자에 대해서만 지원 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_addpushsubscription_agent** 는 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addpushsubscription-a_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만이 **sp_addpushsubscription_agent**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [SQL Server 이외 구독자에 대한 구독 만들기](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_addsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)   
 [sp_dropsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
