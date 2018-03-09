---
title: sp_adddynamicsnapshot_job (Transact SQL) | Microsoft Docs
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
- sp_adddynamicsnapshot_job
- sp_adddynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_adddynamicsnapshot_job
ms.assetid: ef50ccf6-e360-4e4b-91b9-6706b8fabefa
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a3b2201611c5b58b795063dd06ecc7c0918c57f4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spadddynamicsnapshotjob-transact-sql"></a>sp_adddynamicsnapshot_job(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  매개 변수가 있는 행 필터로 게시에 대한 필터링된 데이터 스냅숏을 생성하는 에이전트 작업을 만듭니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다. 관리자가 이 저장 프로시저를 사용하여 구독자에 대한 필터링된 데이터 스냅숏 작업을 수동으로 만들 수 있습니다.  
  
> [!NOTE]  
>  필터링된 데이터 스냅숏 작업을 만들려면 게시에 대한 표준 스냅숏 작업이 있어야 합니다.  
  
 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)을 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication=**] **'***게시***'**  
 필터링된 데이터 스냅숏 작업이 추가될 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@suser_sname** =] **'***suser_sname***'**  
 값으로 필터링 되는 구독에 대 한 필터링 된 데이터 스냅숏을 만들 때 사용 되는 값은는 [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) 구독자에는 함수입니다. *suser_sname* 은 **sysname**, 기본값은 없습니다. *suser_sname* 게시를 동적으로 필터링 하려면이 함수를 사용 하지 않는 경우 NULL 이어야 합니다.  
  
 [  **@host_name** =] **'***host_name***'**  
 값으로 필터링 되는 구독에 대 한 필터링 된 데이터 스냅숏을 만들 때 사용 되는 값은는 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 구독자에는 함수입니다. *host_name* 은 **sysname**, 기본값은 없습니다. *host_name* 게시를 동적으로 필터링 하려면이 함수를 사용 하지 않는 경우 NULL 이어야 합니다.  
  
 [  **@dynamic_snapshot_jobname** =] **'***dynamic_snapshot_jobname***'**  
 만들어진 필터링된 데이터 스냅숏 작업의 이름입니다. *dynamic_snapshot_jobname* 은 **sysname**, 기본값은 null 이며 선택적 출력 매개 변수입니다. 를 지정 하는 경우 *dynamic_snapshot_jobname* 배포자에서 고유한 작업을 확인 해야 합니다. 지정하지 않은 경우 작업 이름이 자동으로 생성되고 결과 집합에 반환됩니다. 생성되는 이름은 다음과 같습니다.  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
> [!NOTE]  
>  동적 스냅숏 작업 이름을 생성할 때 표준 스냅숏 작업 이름을 잘라낼 수 있습니다.  
  
 [  **@dynamic_snapshot_jobid** =] **'***dynamic_snapshot_jobid***'**  
 만들어진 필터링된 데이터 스냅숏 작업에 대한 식별자입니다. *dynamic_snapshot_jobid* 은 **uniqueidentifier**, 기본값은 null 이며 선택적 출력 매개 변수입니다.  
  
 [  **@frequency_type=**] *frequency_type*  
 필터링된 데이터 스냅숏 작업을 예약하는 빈도입니다. *frequency_type* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|요청 시|  
|**4** (기본값)|일별|  
|**8**|매주|  
|**16**|매월|  
|**32**|매월 상대적|  
|**64**|자동 시작|  
|**128**|되풀이|  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 필터링된 데이터 스냅숏 작업을 실행할 기간(일)입니다. *frequency_interval* 은 **int**, 기본값은 1의 값에 따라 달라 집니다 *frequency_type*합니다.  
  
|값 *frequency_type*|에 미치는 영향 *frequency_interval*|  
|--------------------------------|-------------------------------------|  
|**1**|*frequency_interval* 는 사용 되지 않습니다.|  
|**4** (기본값)|모든 *frequency_interval* 기본값 매일 일입니다.|  
|**8**|*frequency_interval* 은 다음 중 하나 이상을 (함께 [&#124; &#40; 비트 OR &#41; &#40; Transact SQL &#41; ](../../t-sql/language-elements/bitwise-or-transact-sql.md) 논리 연산자).<br /><br /> **1** = 일요일 &#124; **2** = 월요일 &#124; **4** = 화요일 &#124; **8** = 수요일 &#124; **16** = 목요일 &#124; **32** = 금요일 &#124; **64** = 토요일|  
|**16**|에 *frequency_interval* 해당 월의 일 합니다.|  
|**32**|*frequency_interval* 다음 중 하나입니다.<br /><br /> **1** = 일요일 &#124; **2** = 월요일 &#124; **3** = 화요일 &#124; **4** = 수요일 &#124; **5** = 목요일 &#124; **6** = 금요일 &#124; **7** = 토요일 &#124; **8** = 하루 &#124; **9** = 평일 &#124; **10** = 주말|  
|**64**|*frequency_interval* 는 사용 되지 않습니다.|  
|**128**|*frequency_interval* 는 사용 되지 않습니다.|  
  
 [  **@frequency_subday=**] *frequency_subday*  
 단위를 지정 *frequency_subday_interval*합니다. *frequency_subday* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**1**|한 번|  
|**2**|둘째|  
|**4** (기본값)|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 개수 *frequency_subday* 각 작업 실행 간에 발생 하는 기간. *frequency_subday_interval* 은 **int**, 기본값은 5입니다.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 각 월에 필터링된 데이터 스냅숏 작업이 발생하는 빈도입니다. 이 매개 변수는 때 *frequency_type* 로 설정 된 **32** (매월 상대)입니다. *frequency_relative_interval* 은 **int**, 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**1** (기본값)|첫째|  
|**2**|둘째|  
|**4**|셋째|  
|**8**|넷째|  
|**16**|마지막|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 사용 하는 되풀이 비율 *frequency_type*합니다. *frequency_recurrence_factor* 은 **int**, 기본값은 0입니다.  
  
 [  **@active_start_date=**] *active_start_date*  
 필터링된 데이터 스냅숏 작업이 처음으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_start_date* 은 **int**, 기본값은 NULL입니다.  
  
 [  **@active_end_date=**] *active_end_date*  
 필터링된 데이터 스냅숏 작업이 마지막으로 실행되도록 예약된 날짜이며 YYYYMMDD 형식으로 표시됩니다. *active_end_date* 은 **int**, 기본값은 NULL입니다.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 하루 중에서 필터링된 데이터 스냅숏 작업이 처음으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_start_time_of_day* 은 **int**, 기본값은 NULL입니다.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 하루 중에서 필터링된 데이터 스냅숏 작업이 마지막으로 실행되도록 예약된 시간이며 HHMMSS 형식으로 표시됩니다. *active_end_time_of_day* 은 **int**, 기본값은 NULL입니다.  
  
## <a name="result-set"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**id**|**int**|필터링 된 데이터 스냅숏 작업에서 식별 된 [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) 시스템 테이블입니다.|  
|**dynamic_snapshot_jobname**|**sysname**|필터링된 데이터 스냅숏 작업의 이름입니다.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|고유 하 게 식별 하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자에서 에이전트 작업입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 **sp_adddynamicsnapshot_job** 매개 변수가 있는 필터를 사용 하는 게시에 대 한 병합 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-adddynamicsnapshot-jo_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_adddynamicsnapshot_job**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [매개 변수가 있는 필터로 병합 게시에 대 한 스냅숏 만들기](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [sp_dropdynamicsnapshot_job &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)   
 [sp_helpdynamicsnapshot_job &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)  
  
  
