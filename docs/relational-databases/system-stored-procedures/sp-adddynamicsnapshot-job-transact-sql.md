---
title: sp_adddynamicsnapshot_job (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddynamicsnapshot_job
- sp_adddynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_adddynamicsnapshot_job
ms.assetid: ef50ccf6-e360-4e4b-91b9-6706b8fabefa
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 48f94f7fcf823a9ed9acc519e393369e44b45302
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68771338"
---
# <a name="sp_adddynamicsnapshot_job-transact-sql"></a>sp_adddynamicsnapshot_job(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  매개 변수가 있는 행 필터로 게시에 대한 필터링된 데이터 스냅샷을 생성하는 에이전트 작업을 만듭니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다. 관리자가 이 저장 프로시저를 사용하여 구독자에 대한 필터링된 데이터 스냅샷 작업을 수동으로 만들 수 있습니다.  
  
> [!NOTE]  
>  필터링된 데이터 스냅샷 작업을 만들려면 게시에 대한 표준 스냅샷 작업이 있어야 합니다.  
  
 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을(를) 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_adddynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]   
    [ , [ @host_name = ] 'host_name' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' OUTPUT ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' OUTPUT ]   
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
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`필터링 된 데이터 스냅숏 작업이 추가 될 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @suser_sname = ] 'suser_sname'`구독자에서 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 함수의 값으로 필터링 되는 구독에 대 한 필터링 된 데이터 스냅숏을 만들 때 사용 되는 값입니다. *suser_sname* 는 **sysname**이며 기본값은 없습니다. 이 함수를 사용 하 여 게시를 동적으로 필터링 하지 않는 경우 *suser_sname* 은 NULL 이어야 합니다.  
  
`[ @host_name = ] 'host_name'`구독자에서 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 함수의 값으로 필터링 되는 구독에 대 한 필터링 된 데이터 스냅숏을 만들 때 사용 되는 값입니다. *host_name* 는 **sysname**이며 기본값은 없습니다. 이 함수를 사용 하 여 게시를 동적으로 필터링 하지 않는 경우 *host_name* 은 NULL 이어야 합니다.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`만들어진 필터링 된 데이터 스냅숏 작업의 이름입니다. *dynamic_snapshot_jobname* 는 **sysname**이며 기본값은 NULL이 고은 선택적 출력 매개 변수입니다. 지정 하는 경우 *Dynamic_snapshot_jobname* 배포자에서 고유한 작업으로 확인 해야 합니다. 지정하지 않은 경우 작업 이름이 자동으로 생성되고 결과 집합에 반환됩니다. 생성되는 이름은 다음과 같습니다.  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
> [!NOTE]  
>  동적 스냅샷 작업 이름을 생성할 때 표준 스냅샷 작업 이름을 잘라낼 수 있습니다.  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`만들어진 필터링 된 데이터 스냅숏 작업의 식별자입니다. *dynamic_snapshot_jobid* 은 **uniqueidentifier**이며 기본값은 NULL이 고 선택적 출력 매개 변수입니다.  
  
`[ @frequency_type = ] frequency_type`필터링 된 데이터 스냅숏 작업을 예약 하는 빈도입니다. *frequency_type* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|주문형|  
|**4** (기본값)|매일|  
|**20cm(8**|매주|  
|**x**|매월|  
|**32**|매월 상대적|  
|**64**|자동 시작|  
|**128**|되풀이|  
  
`[ @frequency_interval = ] frequency_interval`필터링 된 데이터 스냅숏 작업이 실행 되는 기간 (일 단위로 측정)입니다. *frequency_interval* 은 **int**이며 기본값은 1이 고 *frequency_type*의 값에 따라 달라 집니다.  
  
|*Frequency_type* 의 값|*Frequency_interval* 에 대 한 영향|  
|--------------------------------|-------------------------------------|  
|**1**|*frequency_interval* 사용 되지 않습니다.|  
|**4** (기본값)|매일 *frequency_interval* 매일 (기본값)을 사용 합니다.|  
|**20cm(8**|*frequency_interval* 은 [&#124; &#40;비트 or&#41; &#40;transact-sql&#41;](../../t-sql/language-elements/bitwise-or-transact-sql.md) 논리 연산자)와 결합 된 다음 중 하나 이상입니다.<br /><br /> **1** = 일요일 &#124; **2** = 월요일 &#124; **4** = 화요일 &#124; **8** = 수요일 &#124; **16** = 목요일 &#124; **32** = 금요일 &#124; **64** = 토요일|  
|**x**|월의 *frequency_interval* 날짜|  
|**32**|*frequency_interval* 은 다음 중 하나입니다.<br /><br /> **1** = 일요일 &#124; **2** = 월요일 &#124; **3** = 화요일 &#124; **4** = 수요일 &#124; **5** = 목요일 &#124; **6** = 금요일 &#124; **7** = 토요일 &#124; **8** = 일 &#124; **9** = 평일 &#124; **10** = 주말|  
|**64**|*frequency_interval* 사용 되지 않습니다.|  
|**128**|*frequency_interval* 사용 되지 않습니다.|  
  
`[ @frequency_subday = ] frequency_subday`*Frequency_subday_interval*단위를 지정 합니다. *frequency_subday* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|초|  
|**4** (기본값)|Minute|  
|**20cm(8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`각 작업 실행 사이에 발생 하는 *frequency_subday* 기간의 수입니다. *frequency_subday_interval* 은 **int**이며 기본값은 5입니다.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`매월 필터링 된 데이터 스냅숏 작업의 발생입니다. 이 매개 변수는 *frequency_type* 이 **32** (매월 상대적)로 설정 된 경우에 사용 됩니다. *frequency_relative_interval* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1** (기본값)|처음|  
|**2**|초|  
|**4**|셋째|  
|**20cm(8**|넷째|  
|**x**|마지막|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*에서 사용 하는 되풀이 비율입니다. *frequency_recurrence_factor* 은 **int**이며 기본값은 0입니다.  
  
`[ @active_start_date = ] active_start_date`필터링 된 데이터 스냅숏 작업이 처음으로 예약 된 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_start_date* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_end_date = ] active_end_date`필터링 된 데이터 스냅숏 작업이 중지 되는 날짜 이며 YYYYMMDD 형식으로 표시 됩니다. *active_end_date* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`하루 중에서 필터링 된 데이터 스냅숏 작업이 처음으로 시작 되도록 예약 된 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_start_time_of_day* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`하루 중에서 필터링 된 데이터 스냅숏 작업이 중지 되는 시간이 며 HHMMSS 형식으로 표시 됩니다. *active_end_time_of_day* 은 **int**이며 기본값은 NULL입니다.  
  
## <a name="result-set"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|[MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) 시스템 테이블에서 필터링 된 데이터 스냅숏 작업을 식별 합니다.|  
|**dynamic_snapshot_jobname**|**sysname**|필터링된 데이터 스냅샷 작업의 이름입니다.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|배포자에서 에이전트 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업을 고유 하 게 식별 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_adddynamicsnapshot_job** 은 매개 변수가 있는 필터를 사용 하는 게시에 대 한 병합 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-adddynamicsnapshot-jo_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_adddynamicsnapshot_job**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [매개 변수가 있는 필터를 사용 하 여 병합 게시에 대 한 스냅숏 만들기](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [매개 변수가 있는 행 필터](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Transact-sql&#41;sp_dropdynamicsnapshot_job &#40;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)   
 [Transact-sql&#41;sp_helpdynamicsnapshot_job &#40;](../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)  
  
  
