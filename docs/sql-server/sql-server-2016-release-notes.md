---
title: SQL Server 2016 릴리스 정보 | Microsoft 문서
ms.date: 04/25/2018
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- build notes
- release issues
ms.assetid: c64077a2-bec8-4c87-9def-3dbfb1ea1fb6
author: craigg-msft
ms.author: craigg
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7db6dbdbe45102c2a1bc2533d156e55060869b58
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "76909853"
---
# <a name="sql-server-2016-release-notes"></a>SQL Server 2016 릴리스 정보
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
  이 문서는 서비스 팩을 포함하여 SQL Server 2016 릴리스 관련 제한 사항 및 문제를 설명합니다. 새로운 기능에 대한 자세한 내용은 [SQL Server 2016의 새로운 기능](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2016)을 참조하세요.

- [![평가 센터에서 다운로드](../includes/media/download2.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) **[평가 센터](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)** 에서 SQL Server 2016 다운로드
- [![Azure 가상 컴퓨터 소형](../includes/media/azure-vm.png)](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2016sp1-ws2016) Azure 계정이 있습니까?  계정이 있는 경우 **[여기](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2016sp1-ws2016)** 로 이동하여 SQL Server 2016 SP1이 이미 설치된 가상 머신을 실행해 보세요.
- [![SSMS 다운로드](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) SQL Server Management Studio의 최신 버전을 얻으려면 **[SSMS(SQL Server Management Studio) 다운로드](../ssms/download-sql-server-management-studio-ssms.md)** 를 참조하세요.

## <a name="bkmk_2016sp2"></a>SQL Server 2016 서비스 팩 2(SP2)

![info_tip](../sql-server/media/info-tip.png) SQL Server 2016 SP2에는 2016 SP1 이후부터 CU8까지 모든 누적 업데이트가 포함되어 있습니다.

- [![Microsoft 다운로드 센터](../includes/media/download2.png)](https://www.microsoft.com/download/details.aspx?id=56836) [SQL Server 2016 서비스 팩 2(SP2) 다운로드](https://www.microsoft.com/download/details.aspx?id=56836)
- 업데이트의 전체 목록은 [SQL Server 2016 서비스 팩 2 릴리스 정보](https://support.microsoft.com/help/4052908/sql-server-2016-service-pack-2-release-information)를 참조하세요.

SQL Server 2016 SP2를 설치하면 설치 후 다시 부팅이 필요할 수 있습니다. SQL Server 2016 SP2 설치 후 다시 부팅을 계획하고 설치를 수행하는 것이 가장 좋습니다.

SQL Server 2016 SP2에 포함된 성능 및 확장성 관련 개선 사항.

|기능|Description|자세한 정보|
|---|---|---|
|향상된 배포 DB 정리 프로시저 |   대형 배포 데이터베이스 테이블로 인해 차단 및 교착 상태가 발생했었습니다. 향상된 정리 프로시저는 이러한 일부 차단 또는 교착 상태 시나리오를 제거하려고 합니다. |   [KB4040276](https://support.microsoft.com/help/4040276/fix-indirect-checkpoints-on-the-tempdb-database-cause-non-yielding)  |
|변경 내용 추적 정리    |   변경 내용 추적 정리 성능 및 변경 내용 추적 측면 테이블에 대한 효율성이 개선되었습니다.    |   [KB4052129](https://support.microsoft.com//help/4052129/update-for-manual-change-tracking-cleanup-procedure-in-sql-server-2016) |
|CPU 시간 초과를 사용하여 Resource Governor 요청 취소   |   요청에 대한 CPU 임계값에 도달하면 요청을 실제로 취소하여 쿼리 요청 처리가 향상되었습니다. 이 동작은 추적 플래그 2422에서 활성화됩니다. |   [KB4038419](https://support.microsoft.com/help/4038419/add-cpu-timeout-to-resource-governor-request-max-cpu-time-sec)   |
|파일 그룹에 대상 테이블을 만드는 SELECT INTO    |   SQL Server 2016 SP2부터, SELECT INTO T-SQL 구문은 T-SQL 구문에서 ON <Filegroup name> 키워드를 사용하여 사용자의 기본 파일 그룹이 아닌 파일 그룹에 테이블을 로드하도록 지원합니다. |       |
|TempDB에 대한 간접 검사점 향상    |   DPLists에 대한 Spinlock 경합을 최소화하도록 TempDB에 대한 간접 검사점이 향상되었습니다. 향상된 기능으로 인해 TempDB에 대한 간접 검사점이 ON이면 SQL Server 2016의 TempDB 워크로드 규모를 즉시 확장할 수 있습니다.    |   [KB4040276](https://support.microsoft.com/help/4040276) |
|대형 메모리 시스템의 데이터베이스 백업 성능 향상  |   SQL Server 2016 SP2는 백업 중에 진행되는 I/O 드레이닝 방식을 최적화하여 중소 규모 데이터베이스의 백업 성능이 크게 향상되었습니다. 2TB 시스템에서 시스템 데이터베이스 백업을 수행할 때 성능이 100배 이상 향상되었습니다. 백업 및 백업 I/O에 대한 페이지가 버퍼 풀 반복에 비해 더 많은 시간이 소모되므로 데이터베이스 크기가 증가할수록 성능이 저하됩니다. 이러한 변경 사항은 대용량 메모리의 고급 서버에서 여러 개의 작은 데이터베이스를 호스팅하는 고객을 위해 백업 성능을 향상시키는 데 도움이 됩니다.    |       |
|TDE 가능 데이터베이스에 대한 VDI 백업 압축 지원   |   SQL Server 2016 SP2에 VDI 지원이 추가되어 VDI 백업 솔루션으로 TDE 지원 데이터베이스에 압축을 활용할 수 있습니다. 더불어, TDE 지원 데이터베이스의 백업 압축을 지원하기 위해 새로운 백업 형식이 도입되었습니다. SQL Server 엔진은 신규 및 기존 백업 형식을 투명하게 처리하여 백업을 복원합니다.   |       |
|복제 에이전트 프로필 매개 변수를 동적으로 로드    |   새롭게 향상된 기능으로 인해 에이전트를 다시 시작하지 않고도 복제 에이전트 매개 변수를 동적으로 로드할 수 있습니다. 이러한 변화는 가장 일반적으로 사용되는 에이전트 프로필 매개 변수에만 적용됩니다. |       |
|통계 생성/업데이트를 위한 MAXDOP 옵션 지원 |    CREATE/UPDATE statistics 문에 대해 MAXDOP 옵션을 지정할 수 있을 뿐만 아니라, 모든 유형의 인덱스에 대한 작성 또는 재작성 과정에서 통계가 업데이트될 때 올바른 MAXDOP 설정이 사용되도록(MAXDOP 옵션이 있는 경우) 할 수 있습니다.   |   [KB4041809](https://support.microsoft.com/help/4041809) |
|증분 통계를 위한 자동 통계 업데이트 향상 |    특정 시나리오 즉, 테이블의 여러 파티션에서 증분된 통계에 대한 총 수정 카운터가 자동 업데이트 임계값을 초과할 만큼 데이터 변경이 많이 발생했지만 자동 업데이트 임계값을 초과하는 개별 파티션이 없는 경우, 테이블에서 훨씬 더 많은 수정이 발생할 때까지 통계 업데이트가 지연될 수 있습니다. 이 동작은 추적 플래그 11024에서 수정되었습니다.   |       |

SQL Server 2016 SP2에는 지원 가능성 및 진단 관련 개선 사항이 포함되어 있습니다.

|기능|Description|자세한 정보|
|---|---|---|
|가용성 그룹의 데이터베이스에 완벽한 DTC 지원    |   가용성 그룹의 일부인 데이터베이스에 대한 데이터베이스 간 트랜잭션은 현재 SQL Server 2016에서 지원되지 않습니다. SQL Server 2016 SP2에서는 가용성 그룹 데이터베이스를 사용한 분산 트랜잭션을 완벽하게 지원합니다.   |       |
|TempDB의 암호화 상태를 정확하게 반영하도록 sys.databases is_encrypted 열 업데이트 |   sys.databases의 is_encryptedcolumn 열 값은 모든 사용자 데이터베이스의 암호화를 해제하고 SQL Server를 다시 시작한 후에도 TempDB의 경우 1입니다. 예상되는 동작은 TempDB가 이 상황에서 더 이상 암호화되지 않으므로 이 값은 0입니다. SQL Server 2016 SP2부터 sys.databases.is_encrypted는 TempDB의 암호화 상태를 정확하게 반영합니다.  |       |
|검증된 클론 및 백업 생성을 위한 새 DBCC CLONEDATABASE 옵션   |   SQL Server 2016 SP2의 DBCC CLONEDATABASE에는 검증된 클론을 생성하거나 백업 복제본을 생성하는 두 가지 옵션이 제공됩니다. WITH VERIFY_CLONEDB 옵션을 사용하여 클론 데이터베이스를 만들면 일관된 데이터베이스 클론이 만들어지고 확인됩니다. 이 기능은 Microsoft에서 프로덕션용으로 지원됩니다. 클론이 SELECT DATABASEPROPERTYEX(‘clone_database_name’, ‘IsVerifiedClone’)에서 확인되었는지 검증하기 위한 새로운 속성이 도입되었습니다. BACKUP_CLONEDB 옵션을 사용하여 클론을 만들면 고객이 복제본을 다른 서버로 옮기거나 문제 해결을 위해 Microsoft CSS(Customer Support)에 쉽게 보낼 수 있도록 데이터 파일과 동일한 폴더에 백업이 생성됩니다.  |       |
|DBCC CLONEDATABASE에 대한 SSB(Service Broker) 지원    |   DBCC CLONEDATABASE 명령이 SSB 개체의 스크립팅을 허용하도록 향상되었습니다.  |   [KB4092075](https://support.microsoft.com/help/4092075) |
|TempDB 버전 저장소 공간 사용량을 모니터링하는 새로운 DMV    |   SQL Server 2016 SP2에 sys.dm_tran_version_store_space_usage DMV가 새롭게 도입되어 TempDB에서 버전 저장소 사용량을 모니터링 할 수 있습니다. 이제 DBA를 프로덕션 서버에서 실행할 때 성능 오버 헤드가 발생하지 않으면서, 데이터베이스당 버전 저장소 사용 요구 사항을 기반으로 TempDB 크기를 사전에 계획할 수 있습니다. |       |
|복제 에이전트에 대한 완벽한 덤프 지원 | 현재 복제 에이전트에서 처리되지 않은 예외가 발생하는 경우 기본적으로 예외 증상의 미니 덤프가 만들어집니다. 이렇게 하면 처리되지 않은 예외 문제를 해결하는 것이 매우 어렵습니다. 이번 변경을 통해 복제 에이전트에 대한 전체 덤프를 생성할 수 있는 새로운 레지스트리 키가 도입되었습니다.  |       |
|가용성 그룹의 라우팅 실패 읽기에 대한 확장 이벤트 향상 |   전에는 라우팅 목록이 있으면 read_only_rout_fail xEvent가 발생했지만 라우팅 목록에 있는 모든 서버에 연결할 수 없었습니다. SQL Server 2016 SP2에는 문제 해결에 도움이 되는 추가 정보가 포함되며 xEvent가 실행되는 코드 포인트가 확장됩니다.  |       |
|트랜잭션 로그를 모니터링하는 새로운 DMV |   요약 수준 특성 및 데이터베이스의 트랜잭션 로그 파일에 대한 정보를 반환하는 새로운 DMV sys.dm_db_log_stats를 추가했습니다. |       |
|VLF 정보를 모니터링하는 새로운 DMV |   SQL Server 2016 SP2에 DMV sys.dm_db_log_info가 새로 도입되어 DBCC LOGINFO와 유사한 VLF 정보를 노출하여 고객이 겪을 수 있는 잠재적인 T-Log 문제를 모니터링, 경고 및 방지할 수 있습니다.    |       |
|sys.dm_os_sys_info의 프로세서 정보|   sys.dm_os_sys_info DMV에 socket_count 및 cores_per_numa와 같은 프로세서 관련 정보를 노출하도록 새 열이 추가되었습니다.  |       |
|sys.dm_db_file_space_usage의 익스텐트 수정 정보| 마지막 전체 백업 이후에 수정된 익스텐트의 수를 추적하는 새 열이 sys.dm_db_file_space_usage에 추가되었습니다.  |       |
|sys.dm_exec_query_stats의 세그먼트 정보 |   total_columnstore_segment_reads 및 total_columnstore_segment_skips와 같이, 건너뛴 columnstore 세그먼트와 읽은 columnstore 세그먼트의 수를 추적하는 새 열이 sys.dm_exec_query_stats에 추가되었습니다.   |   [KB4051358](https://support.microsoft.com/help/4051358) |
|배포 데이터베이스에 맞는 호환성 수준 설정  |   서비스 팩을 설치하면 배포 데이터베이스 호환성 수준이 90으로 변경됩니다. 이것은 sp_vupgrade_replication 저장 프로시저의 코드 경로 때문입니다. 이제 배포 데이터베이스에 올바른 호환성 수준을 설정하도록 SP가 변경되었습니다.   |       |
|마지막으로 알려진 양호한 DBCC CHECKDB 정보 노출    |   마지막으로 성공한 DBCC CHECKDB 실행 날짜를 프로그래밍 방식으로 반환하는 새 데이터베이스 옵션이 추가되었습니다. 사용자는 이제 DATABASEPROPERTYEX([database], ‘lastgoodcheckdbtime’)를 쿼리하여 지정된 데이터베이스에서 마지막으로 DBCC CHECKDB의 실행에 성공한 날짜/시간을 나타내는 단일 값을 얻을 수 있습니다.  |       |
|실행 계획 XML 향상| 통계 이름, 수정 카운터, 샘플링 비율 및 통계가 마지막으로 업데이트된 시간을 포함하는 [쿼리 계획을 컴파일하는데 사용되는 통계에 대한 정보](https://blogs.msdn.microsoft.com/sql_server_team/sql-server-2017-showplan-enhancements/)입니다. 이 기능은 CE 모델 120 이상에만 추가됩니다. 예를 들어 CE 70에서는 지원되지 않습니다.| |
| |쿼리 최적화 프로그램에서 "행 목표" 논리를 사용하는 경우 새로운 특성인 [EstimateRowsWithoutRowgoal](https://blogs.msdn.microsoft.com/sql_server_team/more-showplan-enhancements-row-goal/)이 실행 계획 XML에 추가됩니다.| |
| |스칼라 UDF(사용자 정의 함수)에 소요된 시간을 추적하는 새 런타임 속성 [UdfCpuTime and UdfElapsedTime](https://blogs.msdn.microsoft.com/sql_server_team/more-showplan-enhancements-udfs/)이 실제 실행 계획 XML에 있습니다.| |
| |실제 실행 계획 XML에서 [상위 10개의 가능한 대기 목록](https://blogs.msdn.microsoft.com/sql_server_team/new-showplan-enhancements/)에 CXPACKET 대기 유형을 추가합니다. 병렬 쿼리 실행에는 CXPACKET 대기가 자주 포함되지만 이런 유형의 대기는 실제 실행 계획 XML에서 보고되지 않았습니다. |       |
| |병렬 처리 연산자 유출 중 TempDB에 기록된 페이지 수를 보고하는 런타임 유출 경고가 확장되었습니다.| |
|보조 문자 데이터 정렬이 사용되는 데이터베이스에 대한 복제 지원  |   보조 문자 데이터 정렬을 사용하는 데이터베이스에서 복제가 지원됩니다. |       |
|가용성 그룹 장애 조치(failover)를 사용하여 적절한 Service Broker 처리 |   가용성 그룹 데이터베이스에서 Service Broker를 사용할 수 있는 현재 구현에서는 AG 장애 조치(failover) 중 주 복제본에서 시작된 모든 Service Broker 연결이 열린 상태로 유지됩니다. 향상된 버전에서는 AG 장애 조치(failover) 중 열려있는 모든 연결을 닫는 것이 목표입니다. |       |
|문제 해결에 대기하도록 병렬 처리 기능 향상 |   새로운 [CXCONSUMER](https://blogs.msdn.microsoft.com/sql_server_team/making-parallelism-waits-actionable/) 대기가 추가되었습니다.   |       |
|동일한 정보에 대한 DMV 간의 일관성 향상 |   sys.dm_exec_session_wait_stats DMV가 CXPACKET 및 CXCONSUMER 대기를 sys.dm_os_wait_stats DMV와 일관되게 추적합니다. |       |
|쿼리 내 병렬 처리 교착 상태 문제 해결 향상 | xEvent 필드 이름 worktable_physical_writes에 병렬 처리 연산자 유출 중 TempDB에 기록되는 페이지 수를 보고하는 새 exchange_spill 확장 이벤트가 있습니다.| |
| |sys.dm_exec_query_stats, sys.dm_exec_procedure_stats 및 sys.dm_exec_trigger_stats DMV의 spills 열(예: total_spills)에 병렬 처리 연산자에 의해 유출되는 데이터도 포함됩니다.| |
| |exchangeEvent 리소스에 더 많은 속성이 추가되어 병렬 처리 교착 상태 시나리오에 대한 XML Deadlock Graph가 향상되었습니다.| |
| |SyncPoint 리소스에 더 많은 특성이 추가되어 배치 모드 연산자와 관련된 교착 상태에 대한 XML Deadlock Graph가 향상되었습니다.| |
|일부 복제 에이전트 프로필 매개 변수를 동적으로 다시 로드 |   현재 복제 에이전트 구현에서 에이전트 프로필 매개 변수를 변경하려면 에이전트를 중지했다가 다시 시작해야 합니다. 향상된 버전에서는 복제 에이전트를 다시 시작하지 않고 매개 변수를 동적으로 다시 로드할 수 있습니다.   |       |

![horizontal-bar.png](media/horizontal-bar.png)

## <a name="bkmk_2016sp1"></a>SQL Server 2016 서비스 팩 1(SP1)
![info_tip](../sql-server/media/info-tip.png) SQL Server 2016 SP1은 보안 업데이트 MS16-136을 포함하여 SQL Server 2016 RTM CU3에 대한 모든 누적 업데이트를 포함합니다. SQL Server 2016 최신 누적 업데이트에서 제공하는 솔루션의 롤업을 포함하며 최신 누적 업데이트(CU3 및 2016년 11월 8일에 릴리스된 보안 업데이트 MS16-136)를 포함합니다.

다음 기능은 SQL Server SP1의 Standard, Web, Express 및 Local DB 버전에서 사용할 수 있습니다(언급한 것과 같이).
- 상시 암호화
- 변경된 데이터 캡처(Express에서 사용할 수 없음)
- columnstore
- 압축
- 동적 데이터 마스킹
- 미세 감사
- 메모리 내 OLTP(로컬 DB에서 사용할 수 없음)
- 여러 파일 스트림 컨테이너(Local DB에서 사용할 수 없음)
- 분할
- PolyBase
- 행 수준 보안

다음 표에는 SQL Server 2016 SP1에서 제공하는 주요 향상 기능이 요약되어 있습니다.

|기능|Description|자세한 정보|
|---|---|---|
|TF 715에서 자동 TABLOCK을 사용하여 힙으로 대량 삽입| 추적 플래그 715는 대량 로드 작업에 대한 테이블 잠금을 비클러스터형 인덱스가 없는 힙에 사용하도록 설정합니다.|[2.5x배 더 빠르게 SQL Server로 SAP 워크로드 마이그레이션](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|CREATE OR ALTER|저장 프로시저, 트리거, 사용자 정의 함수 및 뷰와 같은 개체를 배포합니다.|[SQL Server 데이터베이스 엔진 블로그](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/11/17/create-or-alter-another-great-language-enhancement-in-sql-server-2016-sp1/)|
|복제에 대한 DROP TABLE 지원|복제 아티클을 삭제하도록 복제에 대한 DROP TABLE DDL 지원|[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactiona)|
|파일 스트림 RsFx 드라이버 서명|파일 스트림 RsFx 드라이버는 SQL Server 2016 SP1 파일 스트림 RsFx 드라이버를 문제 없이 Windows Server 2016/Windows 10에 설치하도록 하는 Windows 하드웨어 개발자 센터 대시보드 포털(개발자 포털)을 사용하여 서명 및 인증됩니다.|[2.5x배 더 빠르게 SQL Server로 SAP 워크로드 마이그레이션](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|LPIM에서 SQL 서비스 계정 - 프로그래밍 방식으로 식별|LPIM(메모리의 페이지 잠금) 권한이 서비스 시작 시간에 적용되는 경우 DBA에서 프로그래밍 방식으로 식별하도록 허용합니다.|[개발자 선택 사항: SQL Server에서 LPIM 및 IFI 권한을 프로그래밍 방식으로 식별](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-programmatically-identify-lpim-and-ifi-privileges-in-sql-server)|
|수동 변경 내용 추적 정리|새 저장 프로시저는 요청 시 변경 내용 추적 내부 테이블을 정리합니다.| [KB 3173157](https://support.microsoft.com/help/3173157/adds-a-stored-procedure-for-the-manual-cleanup-of-the-change-tracking)|
|로컬 임시 테이블에 대한 병렬 INSERT..SELECT 변경 내용|INSERT..SELECT 작업에서 새 병렬 INSERT|[SQL Server 고객 자문 팀](https://blogs.msdn.microsoft.com/sqlcat/2016/07/21/real-world-parallel-insert-what-else-you-need-to-know/)|
|Showplan XML|권한 부여 경고 최대 메모리를 포함하는 확장된 진단은 쿼리, 활성화된 추적 플래그에 대해 활성화되었으며 다른 진단 정보를 제공합니다. | [KB 3190761](https://support.microsoft.com/help/3190761/update-to-improve-diagnostics-by-expose-data-type-of-the-parameters-fo)|
|스토리지 클래스 메모리|크기 순서대로 트랜잭션 커밋 시간을 가속화하는 기능을 발생시키는 Windows Server 2016에서 스토리지 클래스 메모리를 사용하여 트랜잭션 처리를 증가시킵니다.|[SQL Server 데이터베이스 엔진 블로그](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/12/02/transaction-commit-latency-acceleration-using-storage-class-memory-in-windows-server-2016sql-server-2016-sp1/)|
|USE HINT|쿼리 옵션, `OPTION(USE HINT('<option>'))`을 사용하여 지원되는 쿼리 수준 힌트를 통해 쿼리 최적화 프로그램 동작을 변경합니다. QUERYTRACEON과 달리 USE HINT 옵션은 sysadmin 권한이 필요하지 않습니다.|[개발자 선택 사항: USE HINT 쿼리 힌트](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-use-hint-query-hints/)|
|XEvent 추가|새로운 Xevent 및 Perfmon 진단 기능은 대기 시간 문제 해결을 개선합니다.|[확장 이벤트](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)|

또한 다음 수정 사항을 참조하세요.
- DBA와 SQL 커뮤니티의 피드백에 따라 SQL 2016 SP1부터 Hekaton 로깅 메시지가 최소로 줄어듭니다.
- 새 [추적 플래그](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)를 검토합니다.
- 전체 버전의 WideWorldImporters 샘플 데이터베이스는 이제 SQL Server 2016 SP1부터 Standard Edition 및 Express Edition을 사용하며 [Github]( https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0)에서 사용 가능합니다. 샘플에서 변경이 필요하지 않습니다. Enterprise 버전에 대한 RTM에서 만든 데이터베이스 백업은 SP1에서 Standard 및 Express를 사용합니다.

SQL Server 2016 SP1 설치는 설치 후에 다시 부팅해야 합니다. 모범 사례로, SQL Server 2016 SP1의 설치를 따라 다시 부팅을 계획 및 수행하는 것이 좋습니다.

### <a name="download-pages-and-more-information"></a>다운로드 페이지 및 추가 정보

- [Microsoft SQL Server 2016용 서비스 팩 1 다운로드](https://www.microsoft.com/download/details.aspx?id=54276)
- [SQL Server 2016 서비스 팩 1(SP1) 출시](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/)
- [SQL Server 2016 서비스 팩 1 릴리스 정보](https://support.microsoft.com/kb/3182545)
- ![info_tip](../sql-server/media/info-tip.png) [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]의 서비스 팩을 포함하여 지원되는 모든 버전에 대한 링크 및 자세한 내용은 [SQL Server 업데이트 센터](https://msdn.microsoft.com/library/ff803383.aspx)를 참조하세요.

![horizontal-bar.png](media/horizontal-bar.png)

##  <a name="bkmk_2016_ga"></a> SQL Server 2016 릴리스 - GA (일반 공급)
-   [데이터베이스 엔진(GA)](#bkmk_ga_instalpatch)
-   [Stretch Database(GA)](#bkmk_ga_stretch)
-   [쿼리 저장소(GA)](#bkmk_ga_query_store)
-   [제품 설명서(GA)](#bkmk_ga_docs)

### ![repl_icon_warn](../database-engine/availability-groups/windows/media/repl-icon-warn.gif) <a name="bkmk_ga_instalpatch"></a> 패치 설치 요구 사항(GA)
**문제 및 고객에게 미치는 영향:** Microsoft는 SQL Server 2016에서 필수 구성 요소로 설치되는 Microsoft VC++ 2013 런타임 이진 파일에 영향을 주는 문제를 확인했습니다. 업데이트로 이 문제를 해결할 수 있습니다. VC 런타임 이진 파일에 대한 이 업데이트가 없으면 SQL Server 2016의 특정 시나리오에서 안정성 문제를 발생할 수 있습니다. SQL Server 2016을 설치하기 전에 컴퓨터에 [KB 3164398](https://support.microsoft.com/kb/3164398)에서 설명한 패치가 필요한지 확인합니다. 패치는 [SQL Server 2016 RTM용 누적 업데이트 패키지 1(CU1)](https://www.microsoft.com/download/details.aspx?id=53338)에도 포함되어 있습니다.

**해결 방법:** 다음 솔루션 중 하나를 사용하세요.

- [KB 3138367 - Visual C++ 2013 및 Visual C++ 재배포 가능 패키지 업데이트](https://support.microsoft.com/kb/3138367)를 설치합니다. KB는 기본적으로 사용되는 해결 방법입니다. SQL Server 2016 설치 전 또는 설치 후에 이 업데이트를 설치할 수 있습니다.

    SQL Server 2016이 이미 설치되어 있는 경우 다음 단계를 순서대로 수행합니다.

    1.  적절한 *vcredist_\*exe*를 다운로드합니다.
    1.  데이터베이스 엔진의 모든 인스턴스에 대한 SQL Server 서비스를 중지합니다.
    1.  **KB 3138367**을 설치합니다.
    1.  컴퓨터를 다시 부팅합니다.


 - [KB 3164398 - SQL Server 2016 MSVCRT 필수 조건에 대한 중요 업데이트](https://support.microsoft.com/kb/3164398)를 설치합니다.

    **KB 3164398**을 사용하는 경우 Microsoft 업데이트를 통해 또는 Microsoft 다운로드 센터에서 SQL Server 설치 중에 설치할 수 있습니다.

    - **SQL Server 2016 설치 중:** SQL Server 설치 프로그램을 실행하는 컴퓨터가 인터넷에 액세스하는 경우 SQL Server 설치 프로그램이 전체 SQL Server 설치의 일부로 업데이트를 검사합니다. 업데이트를 수락하면 설치 프로그램이 다운로드되고 설치하는 동안 이진 파일을 업데이트합니다.

    - **Microsoft 업데이트:** 업데이트는 중요한 비보안 SQL Server 2016 업데이트로 Microsoft 업데이트에서 제공합니다. Microsoft 업데이트를 통해 SQL Server 2016을 설치하면 업데이트를 수행하기 위해 서버를 다시 시작해야 합니다.

    - **다운로드 센터:** 마지막으로, 업데이트는 Microsoft 다운로드 센터에서 제공합니다. SQL Server 2016을 설치한 후 업데이트 소프트웨어를 다운로드하고 서버에 설치할 수 있습니다.


### <a name="bkmk_ga_stretch"></a>Stretch Database

#### <a name="problem-with-a-specific-character-in-a-database-or-table-name"></a>데이터베이스 또는 테이블 이름의 특정 문자 문제

**문제 및 고객에게 미치는 영향:** 데이터베이스 또는 테이블에서 Stretch Database를 사용하도록 설정하는 작업이 오류로 인해 실패했습니다. 이 문제는 개체의 이름에 소문자에서 대문자로 변환할 때 다른 문자로 취급되는 문자가 포함되는 경우 발생합니다. 이 문제를 일으키는 문자의 예는 "ƒ" 문자입니다(ALT+159를 입력하여 생성).

**해결 방법:** 데이터베이스 또는 테이블에서 Stretch Database를 사용하도록 설정하려면 개체 이름을 바꾸고 문제 문자를 제거하는 것이 유일한 옵션입니다.

#### <a name="problem-with-an-index-that-uses-the-include-keyword"></a>INCLUDE 키워드를 사용하는 인덱스 문제

**문제 및 고객에게 미치는 영향:** 인덱스에서 추가 열을 포함하기 위해 INCLUDE 키워드를 사용하는 인덱스가 있는 테이블에서 Stretch Database를 사용하도록 설정하는 작업이 오류로 인해 실패했습니다.

**해결 방법:** INCLUDE 키워드를 사용하는 인덱스를 삭제하고, 테이블에서 Stretch Database를 사용하도록 설정한 다음, 인덱스를 다시 만듭니다. 이 작업을 수행하는 경우 영향을 받는 테이블의 사용자에게 영향을 주지 않거나 최소화하기 위해 조직의 유지 관리 방법 및 정책을 따라야 합니다.

### <a name="bkmk_ga_query_store"></a>Query Store

#### <a name="problem-with-automatic-data-cleanup-on-editions-other-than-enterprise-and-developer"></a>Enterprise 및 Developer 이외 버전의 자동 데이터 정리 문제

 **문제 및 고객에게 미치는 영향:** Enterprise 및 Developer 이외의 버전에서 자동 데이터 정리에 실패했습니다.
따라서 데이터를 수동으로 제거하지 않으면 쿼리 저장소 사용 공간이 시간이 갈수록 증가하여 한계에 도달합니다. 이 문제가 완화되지 않으면 정리를 실행하려고 할 때마다 덤프 파일을 생성하므로 할당된 디스크 공간이 오류 로그로 채워지게 됩니다. 정리 활성화 기간은 워크로드 빈도에 따라 다르지만 15분 이하입니다.

 **해결 방법:** Enterprise 및 Developer 이외의 버전에서 쿼리 저장소를 사용하려면 정리 정책을 명시적으로 해제해야 합니다. 이 작업은 SQL Server Management Studio(데이터베이스 속성 페이지)에서 또는 Transact-SQL 스크립트를 통해 수행할 수 있습니다.

```ALTER DATABASE <database name> SET QUERY_STORE (OPERATION_MODE = READ_WRITE, CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 0), SIZE_BASED_CLEANUP_MODE = OFF)```

또한 쿼리 저장소가 읽기 전용 모드로 전환되지 않도록 하려면 수동 정리 옵션을 사용하는 것이 좋습니다. 예를 들어 다음 쿼리를 실행하여 전체 데이터 공간을 정기적으로 정리합니다.

```ALTER DATABASE <database name> SET QUERY_STORE CLEAR```

또한 다음 쿼리 저장소 저장 프로시저를 실행하여 런타임 통계, 특정 쿼리 또는 계획을 정기적으로 정리합니다.

- `sp_query_store_reset_exec_stats`

- `sp_query_store_remove_plan`

- `sp_query_store_remove_query`


###  <a name="bkmk_ga_docs"></a> 제품 설명서(GA)
 **문제 및 고객에게 미치는 영향:** SQL Server 2016 설명서의 다운로드 가능한 버전은 아직 제공되지 않습니다. 도움말 라이브러리 관리자를 사용하여 **온라인에서 콘텐츠를 설치**하려고 하면 SQL Server 2012 및 SQL Sever 2014 설명서가 표시되지만 SQL Server 2016 설명서에 대한 옵션은 없습니다.

 **해결 방법:** 다음 해결 방법 중 하나를 사용하세요.

 ![SQL Server에 대한 도움말 설정 관리](../sql-server/media/docs-sql2016-managehelpsettings.png "SQL Server에 대한 도움말 설정 관리")

-   **온라인 또는 로컬 도움말 선택** 옵션을 사용하고 "온라인 도움말 사용"을 적용하도록 도움말을 구성합니다.

-   **온라인에서 콘텐츠 설치** 옵션을 사용하고 SQL Server 2014 콘텐츠를 다운로드합니다.

 **F1 도움말:** 기본적으로 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 F1 키를 누르면 F1 도움말 문서의 온라인 버전이 브라우저에 표시됩니다. 문제는 로컬 도움말을 구성하고 설치한 경우에도 브라우저 기반 도움말입니다.

**콘텐츠 업데이트:** SQL Server Management Studio 및 Visual Studio에서 설명서를 추가하는 프로세스 중에 도움말 뷰어 애플리케이션이 응답을 중지할 수 있습니다. 이 문제를 해결하려면 다음 단계를 완료하세요. 이 문제에 대한 자세한 내용은 [Visual Studio 도움말 뷰어가 중단됨](https://msdn.microsoft.com/library/mt654096.aspx)을 참조하세요.

* 메모장에서 %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio14_en US.settings 파일을 열고 다음 코드의 날짜를 미래의 날짜로 변경합니다.

```
     Cache LastRefreshed="12/31/2017 00:00:00"
```

## <a name="additional-information"></a>추가 정보
+ [SQL Server 2016 설치](../database-engine/install-windows/installation-for-sql-server-2016.md)
+ [SQL Server 업데이트 센터 - 지원되는 모든 버전에 대한 링크 및 정보](https://msdn.microsoft.com/library/ff803383.aspx)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png "MS_Logo_X-Small")
