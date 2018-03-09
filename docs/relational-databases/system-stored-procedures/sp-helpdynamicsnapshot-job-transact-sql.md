---
title: sp_helpdynamicsnapshot_job (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdynamicsnapshot_TSQL
- sp_helpdynamicsnapshot_job_TSQL
- job_TSQL
- helpdynamicsnapshot
- job
- sp_helpdynamicsnapshot
- sp_helpdynamicsnapshot_job
- helpdynamicsnapshot_TSQL
helpviewer_keywords:
- sp_helpdynamicsnapshot_job
ms.assetid: d6dfdf26-f874-495f-a8a6-8780699646d7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f9accc8ae7ffb64d82fa10c3b60a2f8fec44b8a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdynamicsnapshotjob-transact-sql"></a>sp_helpdynamicsnapshot_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  필터링된 데이터 스냅숏을 생성하는 에이전트 작업에 대한 정보를 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpdynamicsnapshot_job [ [ @publication = ] 'publication' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@publication =** ] **'***게시***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은  **%** , 지정 된 일치 하는 모든 필터링 된 데이터 스냅숏 작업에 정보를 반환 하는 *dynamic_ snapshot_jobid*및 *dynamic_snapshot_jobname*모든 게시에 대 한 합니다.  
  
 [  **@dynamic_snapshot_jobname =** ] **'***dynamic_snapshot_jobname***'**  
 필터링된 데이터 스냅숏 작업의 이름입니다. *dynamic_snapshot_jobname*은 **sysname**, 기본값은  **%** ', 지정 된 게시에 대 한 모든 동적 작업을 반환 하는 *dynamic_ snapshot_jobid*합니다. 작업을 만들 때 작업 이름을 명시적으로 지정하지 않은 경우에는 작업 이름이 다음 형식으로 지정됩니다.  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
 [  **@dynamic_snapshot_jobid =** ] **'***dynamic_snapshot_jobid***'**  
 필터링된 데이터 스냅숏 작업의 식별자입니다. *dynamic_snapshot_jobid*은 **uniqueidentifier**, 기본값은 NULL로 반환 하는 지정 된 일치 하는 모든 스냅숏 작업 *dynamic_snapshot_jobname*합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**id**|**int**|필터링된 데이터 스냅숏 작업을 식별합니다.|  
|**job_name**|**sysname**|필터링된 데이터 스냅숏 작업의 이름입니다.|  
|**job_id**|**uniqueidentifier**|식별 된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자에서 에이전트 작업입니다.|  
|**dynamic_filter_login**|**sysname**|평가에 사용 되는 값은 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 게시용으로 정의 된 매개 변수가 있는 행 필터에는 함수입니다.|  
|**dynamic_filter_hostname**|**sysname**|평가에 사용 되는 값은 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 게시용으로 정의 된 매개 변수가 있는 행 필터에는 함수입니다.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|매개 변수가 있는 행 필터를 사용하는 경우 스냅숏 파일을 읽을 폴더의 경로입니다.|  
|**frequency_type**|**int**|에이전트 실행이 예약되는 빈도로 다음 값 중 하나가 될 수 있습니다.<br /><br /> **1** = 한 번<br /><br /> **2** = 요청 시<br /><br /> **4** = 매일<br /><br /> **8** = 매주<br /><br /> **16** = 매월<br /><br /> **32** = 매월 상대적<br /><br /> **64** = 자동 시작<br /><br /> **128** = 되풀이|  
|**frequency_interval**|**int**|에이전트가 실행되는 요일로 다음 값 중 하나가 될 수 있습니다.<br /><br /> **1** = 일요일<br /><br /> **2** = 월요일<br /><br /> **3** = 화요일<br /><br /> **4** = 수요일<br /><br /> **5** = 목요일<br /><br /> **6** = 금요일<br /><br /> **7** = 토요일<br /><br /> **8** = 일<br /><br /> **9** = 평일<br /><br /> **10** = 주말|  
|**frequency_subday_type**|**int**|얼마나 자주 에이전트가 실행 되는 경우 정의 하는 형식이 *frequency_type* 은 **4** (매일), 다음이 값 중 하나일 수 있습니다.<br /><br /> **1** = 지정 된 시간<br /><br /> **2** = 초<br /><br /> **4** = 분<br /><br /> **8** = 시간|  
|**frequency_subday_interval**|**int**|간격의 수 *frequency_subday_type* 에이전트 예약된 실행 간에 발생 하는 합니다.|  
|**frequency_relative_interval**|**int**|지정된 된 월에서 에이전트가 실행 되는 주로 때 *frequency_type* 은 **32** (매월 상대적) 이며 다음이 값 중 하나일 수 있습니다.<br /><br /> **1** = 첫 번째<br /><br /> **2** = 초<br /><br /> **4** = 세 번째<br /><br /> **8** = 네 번째<br /><br /> **16** = 마지막|  
|**frequency_recurrence_factor**|**int**|에이전트 예약 실행 간의 주 수 또는 월 수입니다.|  
|**active_start_date**|**int**|에이전트의 실행이 음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다.|  
|**active_end_date**|**int**|에이전트의 실행이 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다.|  
|**active_start_time**|**int**|에이전트의 실행이 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다.|  
|**active_end_time**|**int**|에이전트의 실행이 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_helpdynamicsnapshot_job** 병합 복제에 사용 됩니다.  
  
 모든 기본 매개 변수 값이 사용되는 경우에는 전체 게시 데이터베이스에 대한 모든 분할 데이터 스냅숏 작업의 정보가 반환됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정 서버 역할의 **db_owner** 실행할 수 있는 게시에 대 한 고정 데이터베이스 역할 및 게시 액세스 목록 **sp_helpdynamicsnapshot_job**.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
