---
title: sp_MSchange_snapshot_agent_properties (T-sql)
description: SQL Server 복제에 사용 되는 스냅숏 에이전트에 대 한 속성을 변경 하는 데 사용 되는 sp_MSchange_snapshot_agent_properties 저장 프로시저에 대해 설명 합니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_snapshot_agent_properties_TSQL
- sp_MSchange_snapshot_agent_properties
helpviewer_keywords:
- sp_MSchange_snapshot_agent_properties
ms.assetid: 7947a788-3fd7-469f-84db-b03ba89a153c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6c5c3c2573465072de0d1f0a7c08d47df5d387b6
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321807"
---
# <a name="sp_mschange_snapshot_agent_properties-transact-sql"></a>sp_MSchange_snapshot_agent_properties(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전의 배포자에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 실행 되는 스냅숏 에이전트 작업의 속성을 변경 합니다. 이 저장 프로시저는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 인스턴스에서 게시자가 실행될 때 속성을 변경하는 데 사용됩니다. 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![토픽 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-sql 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_MSchange_snapshot_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @frequency_type= ] frequency_type  
        , [ @frequency_interval= ] frequency_interval  
        , [ @frequency_subday= ] frequency_subday  
        , [ @frequency_subday_interval= ] frequency_subday_interval  
        , [ @frequency_relative_interval= ] frequency_relative_interval  
        , [ @frequency_recurrence_factor= ] frequency_recurrence_factor  
        , [ @active_start_date= ] active_start_date  
        , [ @active_end_date= ] active_end_date  
        , [ @active_start_time_of_day= ] active_start_time_of_day  
        , [ @active_end_time_of_day= ] active_end_time_of_day  
        , [ @snapshot_job_name = ] 'snapshot_agent_name'  
        , [ @publisher_security_mode = ] publisher_security_mode  
        , [ @publisher_login = ] 'publisher_login'  
        , [ @publisher_password = ] 'publisher_password'   
        , [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
        , [ @publisher_type = ] 'publisher_type'  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher_db = ] 'publisher_db'`게시 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @frequency_type = ] frequency_type`스냅숏 에이전트 실행 되는 빈도입니다. *frequency_type* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**1(sp1)**|한 번|  
|**sr-2**|주문형|  
|**3-4**|매일|  
|**20cm(8**|매주|  
|**5-10**|매월|  
|**20**|매월(frequency_interval에 상대적임)|  
|**40**|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 시작될 때|  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*에 의해 설정 된 빈도에 적용 되는 값입니다. *frequency_interval* 는 **int**이며 기본값은 없습니다.  
  
`[ @frequency_subday = ] frequency_subday`*Freq_subday_interval*단위입니다. *frequency_subday* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**1(sp1)**|한 번|  
|**sr-2**|Second|  
|**3-4**|분|  
|**20cm(8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*에 대 한 간격입니다. *frequency_subday_interval* 는 **int**이며 기본값은 없습니다.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`스냅숏 에이전트 실행 되는 날짜입니다. *frequency_relative_interval* 는 **int**이며 기본값은 없습니다.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*에서 사용 하는 되풀이 비율입니다. *frequency_recurrence_factor* 는 **int**이며 기본값은 없습니다.  
  
`[ @active_start_date = ] active_start_date`스냅숏 에이전트 처음으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_start_date* 는 **int**이며 기본값은 없습니다.  
  
`[ @active_end_date = ] active_end_date`스냅숏 에이전트가 마지막으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_end_date* 는 **int**이며 기본값은 없습니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`하루 중 스냅숏 에이전트 처음으로 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_start_time_of_day* 는 **int**이며 기본값은 없습니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`하루 중 스냅숏 에이전트이 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_end_time_of_day* 는 **int**이며 기본값은 없습니다.  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'`기존 작업을 사용 하는 경우 기존 스냅숏 에이전트 작업 이름의 이름입니다. *snapshot_agent_name* 은 **nvarchar (100)** 이며 기본값은 없습니다.  
  
`[ @publisher_security_mode = ] publisher_security_mode`게시자에 연결할 때 에이전트가 사용 하는 보안 모드입니다. *publisher_security_mode* 는 **int**이며 기본값은 없습니다. **0** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 지정 하 고, **1** 은 Windows 인증을 지정 합니다. 비- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자에 대해 **0** 값을 지정 해야 합니다. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`게시자에 연결할 때 사용 되는 로그인입니다. *publisher_login* 는 **sysname**이며 기본값은 없습니다. *publisher_security_mode* **0**인 경우 *publisher_login* 를 지정 해야 합니다. *Publisher_login* 가 NULL이 고 publisher *_ * * Security_mode* **1**이면 게시자에 연결할 때 *job_login* 에 지정 된 Windows 계정이 사용 됩니다.  
  
`[ @publisher_password = ] 'publisher_password'`게시자에 연결할 때 사용 되는 암호입니다. *publisher_password* 은 **nvarchar (524)** 이며 기본값은 없습니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 보안 향상을 위해 런타임에 로그인 이름과 암호를 제공하는 것이 좋습니다.  
  
`[ @job_login = ] 'job_login'`에이전트가 실행 되는 Windows 계정의 로그인입니다. *job_login* 은 **nvarchar (257)** 이며 기본값은 없습니다. 이 Windows 계정은 에이전트가 배포자에 연결할 때 항상 사용됩니다. 새 스냅샷 에이전트 작업을 만들 때는 이 매개 변수를 제공해야 합니다. *이외 게시자에 대해서는 변경할 수 없습니다* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *.*  
  
`[ @job_password = ] 'job_password'`에이전트를 실행 하는 Windows 계정의 암호입니다. *job_password* 는 **sysname**이며 기본값은 없습니다. 새 스냅샷 에이전트 작업을 만들 때는 이 매개 변수를 제공해야 합니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 보안 향상을 위해 런타임에 로그인 이름과 암호를 제공하는 것이 좋습니다.  
  
`[ @publisher_type = ] 'publisher_type'`인스턴스에서 게시자가 실행 되 고 있지 않을 때 게시자 유형을 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publisher_type* 는 **sysname**이며 다음 값 중 하나일 수 있습니다.  
  
|Value|설명|  
|-----------|-----------------|  
|**MSSQLSERVER**|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정합니다.|  
|**ORACLE**|표준 Oracle 게시자를 지정합니다.|  
|**ORACLE GATEWAY**|Oracle Gateway 게시자를 지정합니다.|  
  
 Oracle 게시자와 Oracle Gateway 게시자 간의 차이점에 대 한 자세한 내용은 [Oracle 게시 개요](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)를 참조 하세요.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_MSchange_snapshot_agent_properties** 는 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
 **Sp_MSchange_snapshot_agent_properties**를 실행 하는 경우 모든 매개 변수를 지정 해야 합니다. [Sp_helppublication_snapshot](../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md) 를 실행 하 여 스냅숏 에이전트 작업의 현재 속성을 반환 합니다.  
  
 게시자가 이상 버전의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스에서 실행 되는 경우 [sp_changepublication_snapshot](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md) 를 사용 하 여 스냅숏 에이전트 작업의 속성을 변경 해야 합니다.  
  
## <a name="permissions"></a>권한  
 배포자에서 **sysadmin** 고정 서버 역할의 멤버만 **sp_MSchange_snapshot_agent_properties**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addpublication_snapshot &#40;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
  
