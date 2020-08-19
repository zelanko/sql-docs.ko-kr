---
description: sp_changesubstatus(Transact-SQL)
title: sp_changesubstatus (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubstatus
- sp_changesubstatus_TSQL
helpviewer_keywords:
- sp_changesubstatus
ms.assetid: 9370e47a-d128-4f15-9224-1c3642770c39
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f08825d906705d87596347742c6481dda9c07d7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486238"
---
# <a name="sp_changesubstatus-transact-sql"></a>sp_changesubstatus(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  기존 구독자의 상태를 변경합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changesubstatus [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
        , [ @status = ] 'status'  
    [ , [ @previous_status = ] 'previous_status' ]  
    [ , [ @destination_db = ] 'destination_db' ]  
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
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
    [ , [ @distribution_jobid = ] distribution_jobid ]  
    [ , [ @from_auto_sync = ] from_auto_sync ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @offloadagent= ] remote_agent_activation ]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] dts_package_location ]  
    [ , [ @skipobjectactivation = ] skipobjectactivation  
  [ , [ @distribution_job_name= ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 **%** 입니다. *게시* 를 지정 하지 않으면 모든 게시에 영향을 줍니다.  
  
`[ @article = ] 'article'` 아티클의 이름입니다. 이 이름은 게시에 대해 고유해야 합니다. *article* 은 **sysname**이며 기본값은 **%** 입니다. *Article* 을 지정 하지 않으면 모든 아티클이 영향을 받습니다.  
  
`[ @subscriber = ] 'subscriber'` 상태를 변경할 구독자의 이름입니다. *구독자* 는 **sysname**이며 기본값은 **%** 입니다. *구독자* 를 지정 하지 않으면 지정 된 아티클에 대 한 모든 구독자의 상태가 변경 됩니다.  
  
`[ @status = ] 'status'`**Syssubscriptions** 테이블의 구독 상태입니다. *status* 는 **sysname**이며 기본값은 없으며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**active**|구독자가 동기화되어 데이터를 받습니다.|  
|**inactive**|구독이 없는 구독자 항목이 있습니다.|  
|**예약한**|구독자가 데이터를 요청하고 있으나 아직 동기화되지 않았습니다.|  
  
`[ @previous_status = ] 'previous_status'` 구독의 이전 상태입니다. *previous_status* 는 **sysname**이며 기본값은 NULL입니다. 이 매개 변수를 사용 하면 현재 해당 상태에 있는 모든 구독을 변경 하 여 특정 구독 집합에서 그룹 기능을 허용할 수 있습니다. 예를 들어 모든 활성 구독을 **구독**으로 다시 설정할 수 있습니다.  
  
`[ @destination_db = ] 'destination_db'` 대상 데이터베이스의 이름입니다. *destination_db* 는 **sysname**이며 기본값은 **%** 입니다.  
  
`[ @frequency_type = ] frequency_type` 배포 태스크를 예약 하는 빈도입니다. *frequency_type* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*에 의해 설정 된 빈도에 적용 되는 값입니다. *frequency_interval* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 배포 작업의 날짜입니다. 이 매개 변수는 *frequency_type* 이 32 (매월 상대적)로 설정 된 경우에 사용 됩니다. *frequency_relative_interval* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|처음|  
|**2**|초|  
|**4**|세 번째|  
|**8**|넷째|  
|**16**|마지막|  
|NULL(기본값)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*에서 사용 하는 되풀이 비율입니다. *frequency_recurrence_factor* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @frequency_subday = ] frequency_subday` 정의 된 기간 동안 다시 예약 하는 빈도 (분)입니다. *frequency_subday* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|초|  
|**4**|Minute|  
|**8**|시간|  
|NULL(기본값)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*에 대 한 간격입니다. *frequency_subday_interval* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 하루 중에서 배포 태스크가 처음으로 시작 되도록 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_start_time_of_day* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 하루 중에서 배포 태스크가 중지 되도록 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_end_time_of_day* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_start_date = ] active_start_date` 배포 태스크가 처음으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_start_date* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_end_date = ] active_end_date` 배포 태스크가 마지막으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_end_date* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @optional_command_line = ] 'optional_command_line'` 는 선택적 명령 프롬프트입니다. *optional_command_line* 은 **nvarchar (4000)** 이며 기본값은 NULL입니다.  
  
`[ @distribution_jobid = ] distribution_jobid` 구독 상태를 비활성에서 활성으로 변경 하는 경우 구독에 대 한 배포자의 배포 에이전트 작업 ID입니다. 기타 경우에는 정의되지 않습니다. 이 저장 프로시저에 대한 단일 호출에 둘 이상의 배포 에이전트가 연관된 경우 결과는 정의되지 않습니다. *distribution_jobid* 는 **binary (16)** 이며 기본값은 NULL입니다.  
  
`[ @from_auto_sync = ] from_auto_sync` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @offloadagent = ] remote_agent_activation`
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. *Remote_agent_activation* 를 **0** 이 아닌 값으로 설정 하면 오류가 발생 합니다.  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. *Remote_agent_server_name* 를 NULL이 아닌 값으로 설정 하면 오류가 발생 합니다.  
  
`[ @dts_package_name = ] 'dts_package_name'` DTS (데이터 변환 서비스) 패키지의 이름을 지정 합니다. *dts_package_name* 는 **sysname**이며 기본값은 NULL입니다. 예를 들어 **DTSPub_Package** 이라는 패키지의 경우를 지정 `@dts_package_name = N'DTSPub_Package'` 합니다.  
  
`[ @dts_package_password = ] 'dts_package_password'` 패키지에 대 한 암호를 지정 합니다. *dts_package_password* 는 **sysname** 이며 기본값은 암호 속성이 변경 되지 않은 상태로 유지 되도록 지정 하는 NULL입니다.  
  
> [!NOTE]  
>  DTS 패키지에는 암호가 있어야 합니다.  
  
`[ @dts_package_location = ] dts_package_location` 패키지 위치를 지정 합니다. *dts_package_location* 은 **int**이며 기본값은 **0**입니다. **0**인 경우 패키지 위치가 배포자에 있습니다. **1**인 경우 패키지 위치가 구독자에 있습니다. 패키지의 위치는 **배포자** 또는 **구독자**일 수 있습니다.  
  
`[ @skipobjectactivation = ] skipobjectactivation` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @distribution_job_name = ] 'distribution_job_name'` 배포 작업의 이름입니다. *distribution_job_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @publisher = ] 'publisher'` 이외 게시자를 지정 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher* 는 **sysname**이며 기본값은 NULL입니다.  
  
> [!NOTE]  
>  게시자에 대 한 아티클 속성을 변경할 때는 *게시자* 를 사용 하면 안 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changesubstatus** 는 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 **sp_changesubstatus** **Syssubscriptions** 테이블의 구독자 상태를 변경 된 상태로 변경 합니다. 필요한 경우 **sysarticles** 테이블의 문서 상태를 업데이트 하 여 활성 또는 비활성으로 표시 합니다. 필요한 경우 복제 된 테이블에 대해 **sysobjects** 테이블에서 복제 플래그를 설정 하거나 해제 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할, **db_owner** 고정 데이터베이스 역할의 멤버 또는 구독의 작성자만 **sp_changesubstatus**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Transact-sql&#41;sp_addsubscription &#40;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [Transact-sql&#41;sp_dropsubscription &#40;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpdistributor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Transact-sql&#41;sp_helpsubscription &#40;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
