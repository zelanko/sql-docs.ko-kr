---
title: sp_helpdynamicsnapshot_job (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a155e7031a78cac6dcea4ca380f7b496d59170f0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85733220"
---
# <a name="sp_helpdynamicsnapshot_job-transact-sql"></a>sp_helpdynamicsnapshot_job(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  필터링된 데이터 스냅샷을 생성하는 에이전트 작업에 대한 정보를 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpdynamicsnapshot_job [ [ @publication = ] 'publication' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 **%** 모든 게시에 대해 지정 된 *dynamic_snapshot_jobid*및 *dynamic_snapshot_jobname*일치 하는 모든 필터링 된 데이터 스냅숏 작업에 대 한 정보를 반환 하는입니다.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`필터링 된 데이터 스냅숏 작업의 이름입니다. *dynamic_snapshot_jobname*는 **sysname**이며 기본값은 **%** 지정 된 *dynamic_snapshot_jobid*를 사용 하 여 게시에 대 한 모든 동적 작업을 반환 하는 '입니다. 작업을 만들 때 작업 이름을 명시적으로 지정하지 않은 경우에는 작업 이름이 다음 형식으로 지정됩니다.  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`필터링 된 데이터 스냅숏 작업의 식별자입니다. *dynamic_snapshot_jobid*은 **uniqueidentifier**이며 기본값은 지정 된 *dynamic_snapshot_jobname*와 일치 하는 모든 스냅숏 작업을 반환 하는 NULL입니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|필터링된 데이터 스냅샷 작업을 식별합니다.|  
|**job_name**|**sysname**|필터링된 데이터 스냅샷 작업의 이름입니다.|  
|**job_id**|**uniqueidentifier**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자에서 에이전트 작업을 식별 합니다.|  
|**dynamic_filter_login**|**sysname**|게시에 대해 정의 된 매개 변수가 있는 행 필터에서 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 함수를 계산 하는 데 사용 되는 값입니다.|  
|**dynamic_filter_hostname**|**sysname**|게시에 대해 정의 된 매개 변수가 있는 행 필터에서 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 함수를 계산 하는 데 사용 되는 값입니다.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|매개 변수가 있는 행 필터를 사용하는 경우 스냅샷 파일을 읽을 폴더의 경로입니다.|  
|**frequency_type**|**int**|에이전트 실행이 예약되는 빈도로 다음 값 중 하나가 될 수 있습니다.<br /><br /> **1** = 한 번<br /><br /> **2** = 요청 시<br /><br /> **4** = 매일<br /><br /> **8** = 매주<br /><br /> **16** = 매월<br /><br /> **32** = 매월 상대적<br /><br /> **64** = 자동 시작<br /><br /> **128** = 되풀이|  
|**frequency_interval**|**int**|에이전트가 실행되는 요일로 다음 값 중 하나가 될 수 있습니다.<br /><br /> **1** = 일요일<br /><br /> **2** = 월요일<br /><br /> **3** = 화요일<br /><br /> **4** = 수요일<br /><br /> **5** = 목요일<br /><br /> **6** = 금요일<br /><br /> **7** = 토요일<br /><br /> **8** = 일<br /><br /> **9** = 평일<br /><br /> **10** = 주말|  
|**frequency_subday_type**|**int**|는 *frequency_type* 가 **4** 일 때 에이전트가 실행 되는 빈도를 정의 하는 유형이 며 다음 값 중 하나일 수 있습니다.<br /><br /> **1** = 지정 된 시간<br /><br /> **2** = 초<br /><br /> **4** = 분<br /><br /> **8** = 시간|  
|**frequency_subday_interval**|**int**|에이전트의 예약 된 실행 간에 발생 하는 *frequency_subday_type* 간격의 수입니다.|  
|**frequency_relative_interval**|**int**|*Frequency_type* 가 **32** (매월 상대적)이 고 다음 값 중 하나일 수 있는 경우 에이전트가 지정 된 월에 실행 되는 주입니다.<br /><br /> **1** = 첫 번째<br /><br /> **2** = 초<br /><br /> **4** = 세 번째<br /><br /> **8** = 네 번째<br /><br /> **16** = 마지막|  
|**frequency_recurrence_factor**|**int**|에이전트 예약 실행 간의 주 수 또는 월 수입니다.|  
|**active_start_date**|**int**|에이전트의 실행이 음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다.|  
|**active_end_date**|**int**|에이전트의 실행이 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다.|  
|**active_start_time**|**int**|에이전트의 실행이 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다.|  
|**active_end_time**|**int**|에이전트의 실행이 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpdynamicsnapshot_job** 는 병합 복제에 사용 됩니다.  
  
 모든 기본 매개 변수 값이 사용되는 경우에는 전체 게시 데이터베이스에 대한 모든 분할 데이터 스냅샷 작업의 정보가 반환됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버, **db_owner** 고정 데이터베이스 역할 및 게시에 대 한 게시 액세스 목록의 멤버만 **sp_helpdynamicsnapshot_job**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
