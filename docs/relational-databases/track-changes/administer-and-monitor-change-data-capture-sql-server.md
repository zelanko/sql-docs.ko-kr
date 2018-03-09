---
title: "변경 데이터 캡처 관리 및 모니터링(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: track-changes
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- change data capture [SQL Server], monitoring
- change data capture [SQL Server], administering
- change data capture [SQL Server], jobs
ms.assetid: 23bda497-67b2-4e7b-8e4d-f1f9a2236685
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ffe44a6f8b86c1c745ac583ddccac3d6998612e5
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="administer-and-monitor-change-data-capture-sql-server"></a>변경 데이터 캡처 관리 및 모니터링(SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
이 항목에서는 변경 데이터 캡처를 관리 및 모니터링하는 방법에 대해 설명합니다.  
  
##  <a name="Capture"></a> 캡처 작업  
 캡처 작업은 매개 변수가 없는 저장 프로시저인 **sp_MScdc_capture_job**을 실행하여 시작됩니다. 이 저장 프로시저는 먼저 msdb.dbo.cdc_jobs의 캡처 작업을 위해 *maxtrans*, *maxscans*, *continuous*및 *pollinginterval* 의 구성 값을 추출합니다. 그런 다음 이러한 구성 값은 **sp_cdc_scan**저장 프로시저에 매개 변수로 전달되고 로그 검색을 수행하기 위해 **sp_replcmds** 를 호출하는 데 사용됩니다.  
  
### <a name="capture-job-parameters"></a>캡처 작업 매개 변수  
 캡처 작업의 동작을 이해하려면 구성 가능한 매개 변수가 **sp_cdc_scan**에서 어떻게 사용되는지 알아야 합니다.  
  
#### <a name="maxtrans-parameter"></a>maxtrans 매개 변수  
 *maxtrans* 매개 변수는 단일 로그 검색 주기에서 처리할 수 있는 트랜잭션의 최대 수를 지정합니다. 검색 중에 처리할 트랜잭션 수가 이 한도에 도달하면 현재 검색에 추가 트랜잭션이 포함되지 않습니다. 검색 주기가 완료된 후에는 처리된 트랜잭션의 수가 항상 *maxtrans*보다 작거나 같습니다.  
  
#### <a name="maxscans-parameter"></a>maxscans 매개 변수  
 *maxscans* 매개 변수는 반환(continuous = 0) 또는 waitfor 실행(continuous = 1) 전에 로그를 비우기 위해 시도되는 검색 주기의 최대 수를 지정합니다.  
  
#### <a name="continous-parameter"></a>continuous 매개 변수  
 *continuous* 매개 변수는 로그를 비우거나 검색 주기의 최대 수를 실행한 후 **sp_cdc_scan** 이 제어를 포기할지를 지정합니다(단발 모드). 또한 명시적으로 중지될 때까지 **sp_cdc_scan** 을 계속 실행할지도 지정합니다(연속 모드).  
  
##### <a name="one-shot-mode"></a>단발 모드  
 단발 모드에서는 캡처 작업에서 **sp_cdc_scan** 이 *maxtrans* 의 최대 검색 횟수까지 수행하여 로그를 비우고 반환하도록 요청합니다. 로그에 있는 *maxtrans* 와 모든 트랜잭션은 이후 검색에서 처리됩니다.  
  
 단발 모드는 처리할 트랜잭션 양이 알려져 있고 작업이 종료된 후 자동으로 닫히면 이점을 얻을 수 있는 제어된 테스트 환경에서 사용됩니다. 프로덕션 환경에서는 단발 모드를 사용하지 않는 것이 좋습니다. 프로덕션 환경은 검색 주기의 실행 빈도를 관리하는 작업 일정에 의존하기 때문입니다.  
  
 단발 모드로 실행될 때는 다음과 같은 공식을 사용하여 초당 트랜잭션의 단위로 캡처 작업의 예상 처리량에 대한 상한 값을 계산할 수 있습니다.  
  
 `(maxtrans * maxscans) / number of seconds between scans`  
  
 로그 검색 및 변경 테이블 채우기를 위해 필요한 시간이 0과 크게 차이 나지 않더라도 평균 작업 처리량은 단일 검색에 대해 허용되는 최대 트랜잭션 수와 최대 허용 검색 수를 곱한 값을 로그 처리 분할 시간(초)으로 나눈 값을 초과할 수 없습니다.  
  
 로그 검색을 제어하는 데 단발 모드를 사용하는 경우에는 로그 처리 간격(초)이 작업 일정에 의해 제어됩니다. 이러한 유형의 동작이 필요한 경우 캡처 작업을 연속 모드에서 실행하여 로그 검색의 일정 조정을 관리하는 것이 좋습니다.  
  
##### <a name="continuous-mode-and-the-polling-interval"></a>연속 모드 및 폴링 간격  
 연속 모드에서 캡처 작업은 **sp_cdc_scan** 이 연속으로 실행되도록 요청합니다. 이렇게 하면 저장 프로시저에서 maxtrans 및 maxscans뿐만 아니라 로그 처리 간격(초)(폴링 간격)에 대한 값을 제공함으로써 고유한 대기 루프를 관리할 수 있습니다. 이 모드에서 실행될 때 캡처 작업은 활성 상태로 유지되고 로그 검색 사이에 **WAITFOR** 를 실행합니다.  
  
> [!NOTE]  
>  폴링 간격 값이 0보다 큰 경우 연속 모드에서 실행되는 작업에도 되풀이되는 단발 작업의 처리량과 동일한 상한 값이 적용됩니다. 따라서 (*maxtrans* \* *maxscans*)를 0이 아닌 폴링 간격으로 나누면 캡처 작업에서 처리할 수 있는 트랜잭션의 평균 수에 대한 상한 값이 나옵니다.  
  
### <a name="capture-job-customization"></a>캡처 작업 사용자 지정  
 캡처 작업에서 새 검색을 즉시 시작할지, 아니면 고정된 폴링 간격을 사용하지 않고 새 검색을 시작하기 전에 대기 시간을 사용할지를 결정하는 추가 논리를 적용할 수 있습니다. 이러한 옵션을 사용하면 단순히 하루 일과를 기준으로 업무량이 많을 때는 대기 시간을 매우 길게 적용하고, 주간 업무를 완료하고 야간 업무를 준비해야 하는 마감 시간에는 폴링 간격을 0으로 설정할 수도 있습니다. 캡처 프로세스 진행 상황을 모니터링하여 자정에 커밋된 모든 트랜잭션이 검색되고 변경 테이블에 보관된 시간을 확인할 수도 있습니다. 이렇게 하면 캡처 작업이 종료된 후 예약된 일일 재시작 시간에 다시 시작되도록 할 수 있습니다. **sp_cdc_scan** 을 호출하는 배달된 작업 단계를 사용자가 작성한 **sp_cdc_scan**용 래퍼 호출로 바꾸면 최소한의 노력으로도 고도로 사용자 지정된 동작을 얻을 수 있습니다.  
  
##  <a name="Cleanup"></a> 정리 작업  
 이 섹션에서는 변경 데이터 캡처 정리 작업의 작동 방식에 대한 정보를 제공합니다.  
  
### <a name="structure-of-the-cleanup-job"></a>정리 작업의 구조  
 변경 데이터 캡처는 보존 기반 정리 전략을 사용하여 변경 테이블 크기를 관리합니다. 정리 메커니즘은 첫 번째 데이터베이스 테이블이 설정될 때 생성되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업으로 구성됩니다. 단일 정리 작업은 모든 데이터베이스 변경 테이블의 정리를 처리하며 정의된 모든 캡처 인스턴스에 대해 동일한 보존 값을 적용합니다.  
  
 정리 작업은 매개 변수가 없는 저장 프로시저인 **sp_MScdc_cleanup_job**을 실행하여 시작됩니다. 이 저장 프로시저는 먼저 **msdb.dbo.cdc_jobs**에서 정리 작업에 대해 구성된 보존 값 및 임계값을 추출합니다. 보존 값은 변경 테이블의 새로운 하위 워터마크를 계산하는 데 사용됩니다. 저장 프로시저는 *cdc.lsn_time_mapping* 테이블의 최대 **tran_end_time** 값에서 지정된 시간 값(분)을 빼 datetime 값으로 표현된 새로운 하위 워터마크를 얻습니다. 그런 다음 CDC.lsn_time_mapping 테이블을 사용하여 이 datetime 값을 해당 **lsn** 값으로 변환합니다. 테이블의 여러 항목에서 동일한 커밋 시간을 공유하는 경우에는 최소 **lsn** 이 있는 항목에 해당하는 **lsn** 을 새로운 하위 워터마크로 선택합니다. 이 **lsn** 값을 **sp_cdc_cleanup_change_tables** 로 전달하여 데이터베이스 변경 테이블에서 변경 테이블 항목을 제거합니다.  
  
> [!NOTE]  
>  최근 트랜잭션의 커밋 시간을 기반으로 새로운 하위 워터마크를 계산하는 방법은 지정된 시간 동안 변경 테이블에 변경 내용을 보관할 수 있는 이점이 있습니다. 이는 캡처 프로세스가 실행 중인 경우에도 마찬가지입니다. 실제 하위 워터마크와 커밋 시간을 공유하는 최소 **lsn** 을 선택하면 현재 하위 워터마크와 커밋 시간이 동일한 모든 항목이 변경 테이블 내에 계속 표시됩니다.  
  
 정리 작업을 수행하면 모든 캡처 인스턴스의 하위 워터마크가 단일 트랜잭션 내에서 처음으로 업데이트됩니다. 그런 다음 변경 테이블과 cdc.lsn_time_mapping 테이블에서 오래된 항목을 제거하려고 시도합니다. 구성 가능한 임계값은 모든 단일 문에서 삭제할 수 있는 항목의 개수를 제한합니다. 모든 개별 테이블에서 삭제 작업을 수행하지 못한 경우에도 남은 테이블에서 작업을 계속 시도할 수 있습니다.  
  
### <a name="cleanup-job-customization"></a>정리 작업 사용자 지정  
 정리 작업에서 삭제할 변경 테이블 항목을 결정하는 데 사용되는 전략을 사용자 지정할 수 있습니다. 배달된 정리 작업에서 지원되는 유일한 전략은 시간 기반 전략입니다. 이 경우 마지막으로 처리된 트랜잭션의 커밋 시간에서 허용되는 보존 기간을 빼는 방식으로 새로운 하위 워터마크가 계산됩니다. 기본 정리 프로시저는 시간 대신 **lsn** 에 기반을 두므로 원하는 만큼의 전략을 사용하여 변경 테이블에 보관할 최소 **lsn** 을 결정할 수 있습니다. 이들 중 일부만 엄격히 시간에 기반을 둡니다. 예를 들어 변경 테이블에 액세스해야 하는 다운스트림 프로세스를 실행할 수 없는 경우 클라이언트에 대한 지식을 사용하여 장애 조치를 제공할 수 있습니다. 또한 기본 전략은 동일한 **lsn** 을 사용하여 데이터베이스의 모든 변경 테이블을 정리하지만 기본 정리 프로시저를 호출하여 캡처 인스턴스 수준에서 정리를 수행할 수도 있습니다.  
  
##  <a name="Monitor"></a> 변경 데이터 캡처 프로세스 모니터링  
 변경 데이터 캡처 프로세스 모니터링을 통해 변경 내용이 올바르게 기록되고 있고 변경 테이블에 대한 대기 시간이 적절한지 확인할 수 있습니다. 모니터링을 사용하면 발생할 수 있는 오류를 확인할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는 변경 데이터 캡처를 모니터링하는 데 도움이 되는 두 가지 동적 관리 뷰인 [sys.dm_cdc_log_scan_sessions](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md) 및 [sys.dm_cdc_errors](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md)가 포함되어 있습니다.  
  
### <a name="identify-sessions-with-empty-result-sets"></a>빈 결과 집합이 포함된 세션 확인  
 sys.dm_cdc_log_scan_sessions의 각 행은 로그 검색 세션을 나타냅니다(ID가 0인 행은 제외). 로그 검색 세션은 [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md)을 한 번 실행하는 것과 같습니다. 세션 중에 검색을 수행하면 변경 내용이나 빈 결과가 반환될 수 있습니다. 결과 집합이 비어 있으면 sys.dm_cdc_log_scan_sessions의 empty_scan_count 열이 1로 설정됩니다. 캡처 작업이 계속해서 실행될 때와 같이 연속된 빈 결과 집합이 반환되면 마지막 남은 행에 있는 empty_scan_count가 증가합니다. 예를 들어 sys.dm_cdc_log_scan_sessions에 검색 후 이미 변경 내용이 반환된 10개의 행이 있고 하나의 행에 5개의 빈 결과가 있는 경우 뷰에는 총 11개의 행이 포함됩니다. empty_scan_count 열에서 마지막 행의 값은 5입니다. 검색 결과가 비어 있는 세션을 확인하려면 다음과 같은 쿼리를 실행합니다.  
  
 `SELECT * from sys.dm_cdc_log_scan_sessions where empty_scan_count <> 0`  
  
### <a name="determine-latency"></a>대기 시간 확인  
 sys.dm_cdc_log_scan_sessions 관리 뷰에는 각 캡처 세션에 대한 대기 시간을 기록하는 열이 포함됩니다. 대기 시간이란 원본 테이블에서 커밋되고 있는 트랜잭션과 변경 테이블에서 커밋되고 있는 마지막으로 캡처된 트랜잭션 사이의 경과 시간입니다. 대기 시간 열은 활성 세션에 대해서만 채워집니다. empty_scan_count 열에서 값이 0보다 큰 세션의 경우 대기 시간 열은 0으로 설정됩니다. 다음 쿼리는 가장 최근의 세션에 대한 평균 대기 시간을 반환합니다.  
  
 `SELECT latency FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0`  
  
 대기 시간 데이터를 사용하여 캡처 프로세스에서 트랜잭션을 처리하는 속도가 빠르거나 느린지 확인할 수 있습니다. 이 데이터는 캡처 프로세스가 계속해서 실행되는 경우에 가장 유용합니다. 캡처 프로세스가 예약 일정에 따라 실행되는 경우 원본 테이블에서 커밋되고 있는 트랜잭션과 예약 시간에 실행되는 캡처 프로세스 사이의 시간 간격으로 인해 대기 시간이 길어질 수 있습니다.  
  
 캡처 프로세스 효율성에 대한 또 다른 중요한 측정값은 처리량입니다. 이 수치는 각 세션 중에 처리되는 초당 평균 명령 수를 나타냅니다. 세션의 처리량을 확인하려면 command_count 열에 있는 값을 duration 열에 있는 값으로 나눕니다. 다음 쿼리는 가장 최근의 세션에 대한 평균 처리량을 반환합니다.  
  
 `SELECT command_count/duration AS [Throughput] FROM sys.dm_cdc_log_scan_sessions WHERE session_id = 0`  
  
### <a name="use-data-collector-to-collect-sampling-data"></a>데이터 수집기를 사용하여 샘플링 데이터 수집  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 수집기를 사용하면 모든 테이블 또는 동적 관리 뷰에서 데이터에 대한 스냅숏을 수집하고 성능 데이터 웨어하우스를 구축할 수 있습니다. 데이터베이스에 변경 데이터 캡처가 설정된 경우 나중에 분석할 수 있도록 sys.dm_cdc_log_scan_sessions 뷰 및 sys.dm_cdc_errors 뷰의 스냅숏을 정기적으로 수집하는 것이 좋습니다. 다음 절차에서는 sys.dm_cdc_log_scan_sessions 관리 뷰에서 샘플 데이터를 수집하도록 데이터 수집기를 설정합니다.  
  
 **데이터 컬렉션 구성**  
  
1.  데이터 수집기를 설정하고 및 관리 데이터 웨어하우스를 구성합니다. 자세한 내용은 [데이터 컬렉션 관리](../../relational-databases/data-collection/manage-data-collection.md)를 참조하세요.  
  
2.  다음 코드를 실행하여 변경 데이터 캡처에 대한 사용자 지정 수집기를 만듭니다.  
  
    ```sql  
    USE msdb;  
  
    DECLARE @schedule_uid uniqueidentifier;  
  
    -- Collect and upload data every 5 minutes  
    SELECT @schedule_uid = (  
    SELECT schedule_uid from sysschedules_localserver_view   
    WHERE name = N'CollectorSchedule_Every_5min')  
  
    DECLARE @collection_set_id int;  
  
    EXEC dbo.sp_syscollector_create_collection_set  
    @name = N' CDC Performance Data Collector',  
    @schedule_uid = @schedule_uid,          
    @collection_mode = 0,                   
    @days_until_expiration = 30,                
    @description = N'This collection set collects CDC metadata',  
    @collection_set_id = @collection_set_id output;  
  
    -- Create a collection item using statistics from   
    -- the change data capture dynamic management view.  
    DECLARE @paramters xml;  
    DECLARE @collection_item_id int;  
  
    SELECT @paramters = CONVERT(xml,   
        N'<TSQLQueryCollector>  
            <Query>  
              <Value>SELECT * FROM sys.dm_cdc_log_scan_sessions</Value>  
              <OutputTable>cdc_log_scan_data</OutputTable>  
            </Query>  
          </TSQLQueryCollector>');  
  
    EXEC dbo.sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = N'302E93D1-3424-4BE7-AA8E-84813ECF2419',  
    @name = ' CDC Performance Data Collector',  
    @frequency = 5,   
    @parameters = @paramters,  
    @collection_item_id = @collection_item_id output;  
  
    GO  
    ```  
  
3.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **관리**, **데이터 컬렉션**을 차례로 확장합니다. **CDC Performance Data Collector**를 마우스 오른쪽 단추로 클릭한 다음 **데이터 컬렉션 집합을 시작합니다**를 클릭합니다.  
  
4.  1단계에서 구성한 데이터 웨어하우스에서 custom_snapshots.cdc_log_scan_data 테이블을 찾습니다. 이 테이블은 로그 검색 세션의 데이터 스냅숏 기록을 제공합니다. 이 데이터를 사용하여 시간에 따른 대기 시간, 처리량 및 기타 성능 측정값을 분석할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 변경 내용 추적&#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [변경 데이터 캡처 정보&#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [변경 데이터 캡처 설정 및 해제&#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [변경 데이터 작업&#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)  
  
  
