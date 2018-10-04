---
title: sp_addpushsubscription_agent (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addpushsubscription_agent_TSQL
- sp_addpushsubscription_agent
helpviewer_keywords:
- sp_addpushsubscription_agent
ms.assetid: 1fdd2052-50d8-4318-8aa7-fc635d5cad18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f037d88ed536cf3fecc0b658dcba3f62d1e1bd47
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832321"
---
# <a name="spaddpushsubscriptionagent-transact-sql"></a>sp_addpushsubscription_agent(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

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
 [  **@publication =**] **'***게시***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
 [  **@subscriber =**] **'***구독자***'**  
 구독자의 이름입니다. *구독자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@subscriber_db =**] **'***subscriber_db***'**  
 구독 데이터베이스의 이름입니다. *subscriber_db* 됩니다 **sysname**, 기본값은 NULL입니다. 에 SQL Server 이외 구독자의 값을 지정 **(기본 대상)** 에 대 한 *subscriber_db*합니다.  
  
 [  **@subscriber_security_mode =**] *subscriber_security_mode*  
 동기화 시 구독자에 연결하는 데 사용할 보안 모드입니다. *subscriber_security_mode* 됩니다 **int**, 기본값은 1입니다. **0** 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다. **1** Windows 인증을 지정 합니다.  
  
> [!IMPORTANT]  
>  지연 업데이트 구독의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 구독자에 연결하고 각 구독자로의 연결에는 다른 계정을 지정합니다. 다른 모든 구독에는 Windows 인증을 사용합니다.  
  
 [  **@subscriber_login =**] **'***subscriber_login***'**  
 동기화 시 구독자에 연결하는 데 사용할 구독자 로그인입니다. *subscriber_login* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@subscriber_password =**] **'***subscriber_password***'**  
 구독자 암호입니다. *subscriber_password* 필요한 경우 *subscriber_security_mode* 로 설정 되어 **0**합니다. *subscriber_password* 됩니다 **sysname**, 기본값은 NULL입니다. 구독자 암호가 사용되는 경우에는 자동으로 암호화됩니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요. 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
 [  **@job_login =** ] **'***job_login***'**  
 에이전트가 실행 되는 계정에 대 한 로그인이입니다. Azure SQL Database 관리 되는 인스턴스에서 SQL Server 계정을 사용 합니다. *job_login* 됩니다 **nvarchar(257)**, 기본값은 NULL입니다. Windows 통합 인증을 사용할 때 배포자에 대한 에이전트 연결과 구독자에 대한 연결에 항상 이 Windows 계정을 사용합니다.  
  
 [  **@job_password =** ] **'***job_password***'**  
 에이전트가 실행 되는 계정의 암호가입니다. *job_password* 됩니다 **sysname**, 기본값은 없습니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
 [ **@job_name =** ] **'***job_name***'**  
 기존 에이전트 작업의 이름입니다. *job_name* 됩니다 **sysname**, 기본값은 NULL입니다. 이 매개 변수는 새로 만든 작업(기본값) 대신 기존 작업을 사용하여 구독이 동기화될 경우에만 지정됩니다. 구성원이 아닌 경우는 **sysadmin** 고정 서버 역할을 지정 해야 *job_login* 하 고 *job_password* 지정 하는 경우 *job_name*.  
  
 [  **@frequency_type =** ] *frequency_type*  
 배포 에이전트를 예약하는 빈도입니다. *frequency_type* 됩니다 **int**, 이며 다음 값 중 하나일 수 있습니다.  
  
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
>  값을 지정 **64** 하면 배포 에이전트가 연속 모드로 실행 합니다. 이 설정에 해당 하는 **-연속** 에이전트에 대 한 매개 변수입니다. 자세한 내용은 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)을 참조하세요.  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 설정 된 빈도에 적용 하려면 값인 *frequency_type*합니다. *frequency_interval* 됩니다 **int**, 기본값은 1입니다.  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 배포 에이전트의 날짜입니다. 이 매개 변수를 사용 하면 *frequency_type* 로 설정 된 **32** (매월 상대적)입니다. *frequency_relative_interval* 됩니다 **int**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1** (기본값)|첫째|  
|**2**|둘째|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 사용 하는 되풀이 비율 *frequency_type*합니다. *frequency_recurrence_factor* 됩니다 **int**, 기본값은 0입니다.  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 정의된 기간 동안 다시 예약하는 빈도입니다. *frequency_subday* 됩니다 **int**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|둘째|  
|**4** (기본값)|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 에 대 한 간격인 *frequency_subday*합니다. *frequency_subday_interval* 됩니다 **int**, 기본값은 5입니다.  
  
 [  **@active_start_time_of_day =** ] *active_start_time_of_day*  
 하루 중에서 배포 에이전트가 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_start_time_of_day* 됩니다 **int**, 기본값은 0입니다.  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 하루 중에서 배포 에이전트가 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_end_time_of_day* 됩니다 **int**, 기본값은 235959입니다.  
  
 [ **@active_start_date =** ] *active_start_date*  
 배포 에이전트가 처음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_start_date* 됩니다 **int**, 기본값은 0입니다.  
  
 [ **@active_end_date =** ] *active_end_date*  
 배포 에이전트가 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_end_date* 됩니다 **int**, 기본값은 99991231입니다.  
  
 [  **@dts_package_name =** ] **'***dts_package_name***'**  
 DTS(데이터 변환 서비스) 패키지의 이름을 지정합니다. *dts_package_name* 되는 **sysname** 이며 기본값은 NULL입니다. 예를 들어 `DTSPub_Package`의 패키지 이름을 지정하려면 매개 변수가 `@dts_package_name = N'DTSPub_Package'`여야 합니다.  
  
 [  **@dts_package_password =** ] **'***dts_package_password***'**  
 패키지를 실행하는 데 필요한 암호를 지정합니다. *dts_package_password* 됩니다 **sysname** 이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  경우에 암호를 지정 해야 합니다 *dts_package_name* 지정 됩니다.  
  
 [  **@dts_package_location =** ] **'***dts_package_location***'**  
 패키지 위치를 지정합니다. *dts_package_location* 되는 **nvarchar(12)**, 배포자의 기본값을 사용 하 여 합니다. 패키지의 위치 일 수 있습니다 **배포자** 하거나 **구독자**합니다.  
  
 [  **@enabled_for_syncmgr =** ] **'***enabled_for_syncmgr***'**  
 구독을 통해 동기화 할 수 있는지 여부는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Synchronization Manager. *enabled_for_syncmgr* 됩니다 **nvarchar(5)**, 기본값은 FALSE입니다. 하는 경우 **false**의 구독이 동기화 관리자에 등록 되지 않았습니다. 하는 경우 **true**, 구독이 동기화 관리자에 등록 및 시작 하지 않고 동기화 할 수 있습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다.  
  
 [  **@distribution_job_name =** ] **'***distribution_job_name***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@publisher =** ] **'***게시자***'**  
 게시자의 이름입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [  **@subscriber_provider=** ] **'***subscriber_provider***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 데이터 원본용 OLE DB 공급자를 등록할 때 사용하는 고유 PROGID(프로그래밍 식별자)입니다. *subscriber_provider* 됩니다 **sysname**, 기본값은 NULL입니다. *subscriber_provider* 배포자에 설치 된 OLE DB 공급자에 대해 고유 해야 합니다. *subscriber_provider* 에서만 지원 됩니다 이외[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다.  
  
 [  **@subscriber_datasrc=** ] **'***subscriber_datasrc***'**  
 OLE DB 공급자가 이해하는 데이터 원본의 이름입니다. *subscriber_datasrc* 됩니다 **nvarchar(4000)**, 기본값은 NULL입니다. *subscriber_datasrc* OLE DB 공급자를 초기화 하는 DBPROP_INIT_DATASOURCE 속성으로 전달 됩니다. *subscriber_datasrc* 에서만 지원 됩니다 이외[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다.  
  
 [  **@subscriber_location=** ] **'***subscriber_location***'**  
 OLE DB 공급자가 이해하는 데이터베이스의 위치입니다. *subscriber_location* 됩니다 **nvarchar(4000)**, 기본값은 NULL입니다. *subscriber_location* OLE DB 공급자를 초기화 DBPROP_INIT_LOCATION 속성으로 전달 됩니다. *subscriber_location* 에서만 지원 됩니다 이외[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다.  
  
 [  **@subscriber_provider_string=** ] **'***subscriber_provider_string***'**  
 데이터 원본을 식별하는 OLE DB 공급자별 연결 문자열입니다. *subscriber_provider_string* 됩니다 **nvarchar(4000)**, 기본값은 NULL입니다. *subscriber_provider_string* IDataInitialize 전달 되거나 DBPROP_INIT_PROVIDERSTRING 속성으로 설정 되어 OLE DB 공급자를 초기화 됩니다. *subscriber_provider_string* 에서만 지원 됩니다 이외[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다.  
  
 [  **@subscriber_catalog=** ] **'***subscriber_catalog***'**  
 OLE DB 공급자에 연결할 때 사용할 카탈로그입니다. *subscriber_catalog* 됩니다 **sysname**, 기본값은 NULL입니다. *subscriber_catalog* OLE DB 공급자를 초기화 DBPROP_INIT_CATALOG 속성으로 전달 됩니다. *subscriber_catalog* 에서만 지원 됩니다 이외[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_addpushsubscription_agent** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addpushsubscription-a_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_addpushsubscription_agent**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [SQL Server 이외 구독자에 대한 구독 만들기](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_addsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)   
 [sp_dropsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
