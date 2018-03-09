---
title: sp_MSchange_snapshot_agent_properties (Transact SQL) | Microsoft Docs
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
- sp_MSchange_snapshot_agent_properties_TSQL
- sp_MSchange_snapshot_agent_properties
helpviewer_keywords: sp_MSchange_snapshot_agent_properties
ms.assetid: 7947a788-3fd7-469f-84db-b03ba89a153c
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c503aafed87719edd03996142ad6a47e34a68106
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spmschangesnapshotagentproperties-transact-sql"></a>sp_MSchange_snapshot_agent_properties(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  실행 되는 스냅숏 에이전트 작업의 속성을 변경는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 또는 이상 버전의 배포자입니다. 이 저장된 프로시저는 게시자 인스턴스에서 실행 될 때 속성을 변경 하는 데 사용 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]합니다. 이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publisher**  =] **'***게시자***'**  
 게시자의 이름입니다. *게시자* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 게시 데이터베이스의 이름입니다. *publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@publication =** ] **'***게시***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@frequency_type =** ] *frequency_type*  
 스냅숏 에이전트가 실행되는 빈도입니다. *frequency_type* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|요청 시|  
|**4**|일별|  
|**8**|매주|  
|**10**|매월|  
|**20**|매월(frequency_interval에 상대적임)|  
|**40**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 시작될 때|  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 값 설정 된 빈도에 적용 하려면 *frequency_type*합니다. *frequency_interval* 은 **int**, 기본값은 없습니다.  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 에 대 한 단위 *freq_subday_interval*합니다. *frequency_subday* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|둘째|  
|**4**|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 에 대 한 간격인 *frequency_subday*합니다. *frequency_subday_interval* 은 **int**, 기본값은 없습니다.  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 스냅숏 에이전트가 실행되는 날짜입니다. *frequency_relative_interval* 은 **int**, 기본값은 없습니다.  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 사용 하는 되풀이 비율 *frequency_type*합니다. *frequency_recurrence_factor* 은 **int**, 기본값은 없습니다.  
  
 [  **@active_start_date =** ] *active_start_date*  
 스냅숏 에이전트가 처음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_start_date* 은 **int**, 기본값은 없습니다.  
  
 [  **@active_end_date =** ] *active_end_date*  
 스냅숏 에이전트가 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_end_date* 은 **int**, 기본값은 없습니다.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 하루 중 스냅숏 에이전트가 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_start_time_of_day* 은 **int**, 기본값은 없습니다.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 하루 중 스냅숏 에이전트가 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_end_time_of_day* 은 **int**, 기본값은 없습니다.  
  
 [  **@snapshot_job_name =** ] **'***snapshot_agent_name***'**  
 기존 작업이 사용되는 경우 기존 스냅숏 에이전트 작업의 이름입니다. *snapshot_agent_name* 은 **nvarchar (100)**, 기본값은 없습니다.  
  
 [  **@publisher_security_mode** =] *publisher_security_mode*  
 게시자에 연결할 때 에이전트가 사용하는 보안 모드입니다. *publisher_security_mode* 은 **int**, 기본값은 없습니다. **0** 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 하 고 **1** Windows 인증을 지정 합니다. 값이 **0** 지정 해야 이외[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@publisher_login** =] **'***publisher_login***'**  
 게시자에 연결할 때 사용하는 로그인입니다. *publisher_login* 은 **sysname**, 기본값은 없습니다. *publisher_login* 지정 해야 *publisher_security_mode* 은 **0**합니다. 경우 *publisher_login* 이 NULL이 고 게시자*_**security_mode* 은 **1**에 지정 된 Windows 계정이 다음  *job_login* 게시자에 연결할 때 사용할 수 있습니다.  
  
 [  **@publisher_password** =] **'***publisher_password***'**  
 게시자에 연결할 때 사용하는 암호입니다. *publisher_password* 은 **nvarchar (524)**, 기본값은 없습니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 보안 향상을 위해 런타임에 로그인 이름과 암호를 제공하는 것이 좋습니다.  
  
 [  **@job_login** =] **'***job_login***'**  
 에이전트 실행에 사용되는 Windows 계정의 로그인입니다. *job_login* 은 **nvarchar (257)**, 기본값은 없습니다. 이 Windows 계정은 에이전트가 배포자에 연결할 때 항상 사용됩니다. 새 스냅숏 에이전트 작업을 만들 때는 이 매개 변수를 제공해야 합니다. *이 이외에 대 한 변경할 수 없습니다* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *게시자입니다.*  
  
 [  **@job_password** =] **'***job_password***'**  
 에이전트 실행에 사용되는 Windows 계정의 암호입니다. *job_password* 은 **sysname**, 기본값은 없습니다. 새 스냅숏 에이전트 작업을 만들 때는 이 매개 변수를 제공해야 합니다.  
  
> [!IMPORTANT]  
>  스크립트 파일에 인증 정보를 저장하지 않도록 합니다. 보안 향상을 위해 런타임에 로그인 이름과 암호를 제공하는 것이 좋습니다.  
  
 [  **@publisher_type** =] **'***publisher_type***'**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 게시자가 실행되고 있지 않을 때 게시자 유형을 지정합니다. *publisher_type* 은 **sysname**, 다음 값 중 하나가 될 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정합니다.|  
|**ORACLE**|표준 Oracle 게시자를 지정합니다.|  
|**ORACLE GATEWAY**|Oracle Gateway 게시자를 지정합니다.|  
  
 Oracle 게시자와 Oracle Gateway 게시자의 차이점에 대 한 자세한 내용은 참조 [Publishing](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_MSchange_snapshot_agent_properties** 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
 실행할 때는 모든 매개 변수를 지정 해야 **sp_MSchange_snapshot_agent_properties**합니다. 실행 [sp_helppublication_snapshot](../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md) 스냅숏 에이전트 작업의 현재 속성을 반환 합니다.  
  
 게시자의 인스턴스에서 실행 하는 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전을 사용할지 또는 [sp_changepublication_snapshot](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md) 스냅숏 에이전트 작업의 속성을 변경 합니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할이 배포자에서 실행할 수 있는 **sp_MSchange_snapshot_agent_properties**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_addpublication_snapshot&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
  
