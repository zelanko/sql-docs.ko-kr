---
title: sp_changesubstatus (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aa9452d7dc2e611b1b581c12cf33e88950eacc2a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53212342"
---
# <a name="spchangesubstatus-transact-sql"></a>sp_changesubstatus(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 구독자의 상태를 변경합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ **@publication=**] **'***publication***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 **%** 합니다. 하는 경우 *게시* 지정 하지 않으면 모든 게시에 영향을 받습니다.  
  
 [  **@article=**] **'***문서***'**  
 아티클의 이름입니다. 이 이름은 게시에 대해 고유해야 합니다. *문서* 됩니다 **sysname**, 기본값은 **%** 합니다. 하는 경우 *문서* 지정 하지 않으면 모든 아티클에 적용 됩니다.  
  
 [  **@subscriber=**] **'***구독자***'**  
 상태를 변경할 구독자의 이름입니다. *구독자* 됩니다 **sysname**, 기본값은 **%** 합니다. 하는 경우 *구독자* 지정 하지 않으면 지정 된 아티클에 모든 구독자에 대 한 상태가 변경 됩니다.  
  
 [  **@status =**] **'***상태***'**  
 구독 상태를 **syssubscriptions** 테이블입니다. *상태* 됩니다 **sysname**이며 기본값은 없고 수 이러한 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**Active**|구독자가 동기화되어 데이터를 받습니다.|  
|**비활성**|구독이 없는 구독자 항목이 있습니다.|  
|**구독**|구독자가 데이터를 요청하고 있으나 아직 동기화되지 않았습니다.|  
  
 [  **@previous_status=**] **'***previous_status***'**  
 구독의 이전 상태입니다. *previous_status* 됩니다 **sysname**, 기본값은 NULL입니다. 이 매개 변수를 사용 하면 현재 구독의 특정 집합에 그룹 함수를 허용 하므로, 해당 상태를 포함 하는 모든 구독을 변경할 수 있습니다 (예를 들어 모든 활성 프로세스 설정 구독을 다시 **구독**).  
  
 [  **@destination_db=**] **'***destination_db***'**  
 대상 데이터베이스의 이름입니다. *destination_db* 됩니다 **sysname**, 기본값은 **%** 합니다.  
  
 [  **@frequency_type=**] *frequency_type*  
 배포 태스크를 예약하는 빈도입니다. *frequency_type* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@frequency_interval=**] *frequency_interval*  
 설정 된 빈도에 적용 하려면 값인 *frequency_type*합니다. *frequency_interval* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 배포 태스크 날짜입니다. 이 매개 변수를 사용 하면 *frequency_type* 32 (매월 상대)로 설정 됩니다. *frequency_relative_interval* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|첫째|  
|**2**|Second|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
|NULL(기본값)||  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 사용 하는 되풀이 비율 *frequency_type*합니다. *frequency_recurrence_factor* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 정의된 기간 동안 다시 예약하는 빈도(분)입니다. *frequency_subday* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
|NULL(기본값)||  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 에 대 한 간격인 *frequency_subday*합니다. *frequency_subday_interval* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 하루 중에서 배포 태스크가 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_start_time_of_day* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 하루 중에서 배포 태스크가 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_end_time_of_day* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@active_start_date=**] *active_start_date*  
 배포 태스크가 처음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_start_date* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@active_end_date=**] *active_end_date*  
 배포 태스크가 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_end_date* 됩니다 **int**, 기본값은 NULL입니다.  
  
 [  **@optional_command_line=**] **'***optional_command_line***'**  
 선택적 명령 프롬프트입니다. *optional_command_line* 됩니다 **nvarchar(4000)**, 기본값은 NULL입니다.  
  
 [  **@distribution_jobid=**] *distribution_jobid*  
 구독 상태를 비활성에서 활성으로 변경할 때 구독에 대한 배포자에 있는 배포 에이전트의 작업 ID입니다. 기타 경우에는 정의되지 않습니다. 이 저장 프로시저에 대한 단일 호출에 둘 이상의 배포 에이전트가 연관된 경우 결과는 정의되지 않습니다. *distribution_jobid* 됩니다 **binary(16)**, 기본값은 NULL입니다.  
  
 [  **@from_auto_sync=**] *from_auto_sync*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@offloadagent=** ] *remote_agent_activation*  
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. 설정 *remote_agent_activation* 이외의 값으로 **0** 오류를 생성 합니다.  
  
 [  **@offloadserver=** ] **'***remote_agent_server_name***'**  
 > [!NOTE]  
>  원격 에이전트 활성화는 더 이상 사용되지 않으며 지원되지 않습니다. 이 매개 변수는 이전 버전 스크립트와의 호환성을 유지하기 위한 목적으로만 지원됩니다. 설정 *remote_agent_server_name* NULL이 아닌 값으로 오류를 생성 합니다.  
  
 [ **@dts_package_name**=] **'***dts_package_name***'**  
 DTS(데이터 변환 서비스) 패키지의 이름을 지정합니다. *dts_package_name* 되는 **sysname**, 기본값은 NULL 사용 하 여 합니다. 명명 된 예 패키지용 **DTSPub_Package** 지정 하는 경우 `@dts_package_name = N'DTSPub_Package'`합니다.  
  
 [ **@dts_package_password**=] **'***dts_package_password***'**  
 패키지 암호를 지정합니다. *dts_package_password* 됩니다 **sysname** 기본값은 NULL 사용 하 여 변경 되지 않은 상태로 남아 있을 암호 속성이 지정 합니다.  
  
> [!NOTE]  
>  DTS 패키지에는 암호가 있어야 합니다.  
  
 [ **@dts_package_location**=] *dts_package_location*  
 패키지 위치를 지정합니다. *dts_package_location* 되는 **int**, 기본값은 **0**합니다. 하는 경우 **0**, 패키지 위치는 배포자입니다. 하는 경우 **1**, 패키지 위치는 구독자의 합니다. 패키지의 위치 일 수 있습니다 **배포자** 하거나 **구독자**합니다.  
  
 [ **@skipobjectactivation**=] *skipobjectactivation*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@distribution_job_name=** ] **'***distribution_job_name***'**  
 배포 작업의 이름입니다. *distribution_job_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [ **@publisher**=] **'***게시자***'**  
 이외 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
> [!NOTE]  
>  *게시자* 해서는 안에서 아티클 속성을 변경 하는 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_changesubstatus** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
 **sp_changesubstatus** 구독자의 상태를 변경 합니다 **syssubscriptions** 변경 된 상태를 사용 하 여 테이블입니다. 필요한 경우에서 문서 상태를 업데이트 합니다 **sysarticles** 활성 또는 비활성 테이블입니다. 필요한 경우 해당 복제 플래그 설정 또는 해제는 **sysobjects** 복제 된 테이블에 대 한 테이블입니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정 서버 역할 **db_owner** 고정된 데이터베이스 역할 또는 구독의 작성자 실행할 수 있습니다 **sp_changesubstatus**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_addsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpdistributor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
