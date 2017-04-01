---
title: "SQL Server R 서비스에 대 한 Dmv | Microsoft Docs"
ms.custom: ""
ms.date: "11/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b3643ea0-d9f3-463f-8ece-572127f32a24
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# SQL Server R 서비스에 대 한 Dmv

시스템 카탈로그 뷰 및 Dmv 관련 된 항목 나열 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]합니다. 


확장된 이벤트에 대 한 정보를 참조 하십시오. [SQL Server R 서비스에 대 한 확장 이벤트](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)합니다.

> [!TIP]
> 제품 팀에서는 R 서비스 세션 및 패키지를 모니터링 하는 데 사용할 수 있는 사용자 지정 보고서를 제공 합니다. 자세한 내용은 참조 [Management Studio에서 사용자 지정 보고서를 사용 하 여 R 서비스를 모니터링](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)합니다.
> 

## <a name="system-configuration-and-system-resources"></a>시스템 구성 및 시스템 리소스

모니터링 하 고 R 스크립트를 사용 하 여 사용 하는 리소스를 분석할 수 있습니다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 시스템 카탈로그 뷰 및 Dmv 합니다.


**일반**
+ [ sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)

  사용자 연결 및 시스템 세션 모두에 대 한 정보를 반환합니다. 확인 하 여 시스템 세션을 식별할 수는 *session_id* 열; 보다 큰 값 이나 51 같음은 사용자 연결 하 고 값 보다 51 시스템 프로세스를 줄이려면. 



+ [sys.dm_os_performance_counters (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)

  서버에서 사용 되 고 각 시스템 성능 카운터에 대 한 행을 반환 합니다.  이 정보를 사용 하 여 실행 하는 얼마나 많은 스크립트를 볼 수 있는 인증 모드 또는 전체 인스턴스에 R 호출 수를 발행 했습니다를 사용 하는 스크립트 실행 합니다.

  이 예제에서는 R 스크립트와 관련 된 카운터를 가져옵니다.

  ```SQL
  SELECT * from sys.dm_os_performance_counters WHERE object_name LIKE '%Extended Scripts%'
  ```

  다음 카운터는 각 인스턴스에 대해 외부 스크립트에 대 한이 DMV에서 보고 됩니다.

  + **총 실행**: 로컬 또는 원격 호출에 의해 시작 된 R 프로세스의 수
  + **병렬 실행**: 스크립트를 포함 하는 횟수는 @parallel 사양과 있는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 를 생성 하 여 병렬 쿼리 계획을 사용할 수
  + **실행 될 때 스트리밍**: 스트리밍 기능은 호출 된 횟수입니다. 
  + **SQL CC 실행**: 호출 원격으로 인스턴스화 했 고 계산 컨텍스트로 사용 하는 SQL Server를 실행 하는 수의 R 스크립트 
  + **암시 된 인증 로그인**:는 ODBC 루프백 호출에 사용 하 여 작성 된 횟수 만큼 사용 권한에 포함 된 인증, 즉, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 스크립트 요청을 보내는 사용자를 대신 하 여 호출 실행
  + **총 실행 시간 (ms)**: 호출과 호출이 완료 간에 경과 된 시간입니다.
  + **실행 오류**: 횟수 스크립트 오류를 보고 했습니다. 이 개수는 R 오류를 포함 하지 않습니다.


+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)

  이 DMV는 외부 스크립트를 현재 실행 중인 각 작업자 계정에 대 한 단일 행을 보고 합니다. 이 작업자 계정 스크립트를 전송 하는 사용자의 자격 증명과 다를 않음을 유의 하십시오. Windows 사용자 한 명이 여러 스크립트 요청을 보내는 경우 해당 사용자의 모든 요청을 처리할 하나의 작업자 계정이 할당 합니다. 외부 스크립트를 실행 하는 다른 Windows 사용자 로그인 하는 경우 요청은 별도 작업자 계정에서 처리 됩니다. 
  이 DMV는 결과 반환 하지 않는 경우 스크립트가 현재 실행 되는; 따라서 가장 유용 장기 실행 스크립트를 모니터링 합니다. 이러한 값을 반환 합니다.
  + **external_script_request_id**: 스크립트 및 중간 결과 저장 하는 데 사용 하는 작업 디렉터리의 임시 이름으로도 사용 되는 GUID입니다.  
  + **언어**:과 같은 값 `R` 외부 스크립트의 언어를 나타냅니다.
  + **degree_of_parallelism**: 사용 된 병렬 수가 되는 프로세스를 나타내는 정수입니다. 
  + **external_user_name**: SQLRUser01 같은 실행 패드 작업자 계정에 있습니다. 
  

+ [sys.dm_external_script_execution_stats (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)

  이 DMV는 내부 인스턴스에서 수행할는 R 호출 수를 추적 하 (원격 분석) 모니터링을 위해 제공 됩니다. 원격 분석 서비스를 시작 하는 경우 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 않으며 특정 R 함수를 호출할 때마다 디스크 기반 카운터를 증가 시킵니다.

  이 카운터는 함수 호출당 증가 됩니다. 예를 들어 `rxLinMod` 가 호출되어 병렬로 실행될 때 카운터는 1씩 증가합니다.
  
  일반적으로 생성된 프로세스가 활성 상태인 경우에만 성능 카운터가 유효합니다. 따라서 DMV에서 쿼리는 실행이 중지된 서비스의 데이터 세부 정보를 표시할 수 없습니다. 예를 들어, 실행 패드 병렬 R 작업을 여러 개 만들고 아직 매우 신속 하 게 실행 되며 다음 Windows 작업 개체에 의해 정리, DMV 데이터 표시 되지 않습니다.
 
  이 DMV에서 추적 하는 카운터 유지 되는 반면 dm_external_script _execution 카운터는 유지 하는 인스턴스를 종료 하는 경우에 디스크에 쓰기를 사용 하 여에 대 한 상태이 고 실행 합니다.
 
 사용 하는 시스템 성능 카운터에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 참조 [사용 하 여 SQL Server 개체](../../relational-databases/performance-monitor/use-sql-server-objects.md)합니다.

**리소스 관리자 뷰**

+ [sys.resource_governor_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)

  현재 리소스 풀 상태, 리소스 풀의 현재 구성 및 리소스 풀 통계에 대한 정보를 반환합니다.

  > [!IMPORTANT]
  > 
  > R 서비스에 추가 리소스를 할당할 수 있습니다 전에 다른 서버 서비스에 적용 되는 리소스 풀을 수정 해야 합니다.


+ [sys.resource_governor_external_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)

  새 카탈로그 뷰를 외부 리소스 풀에 대 한 현재 구성 값을 보여 줍니다.
  Enterprise Edition에서 외부 리소스 풀을 구성할 수 있습니다: 예를 들어 R 작업 실행에 대 한 리소스를 처리 하도록 결정할 수 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 원격 클라이언트에서 시작 된 별도로 합니다. 

  > [!NOTE]
  > 
  > Standard Edition에서는 모든 R 작업은 동일한 외부 기본 리소스 풀에서 실행 됩니다.

+ [sys.resource_governor_workload_groups](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)

  작업 그룹 통계 및 작업 그룹의 현재 구성을 반환합니다. 이 뷰는 sys.dm_resource_governor_resource_pools와 조인하여 리소스 풀 이름을 가져올 수 있습니다.
  외부 스크립트는 새 열 작업 그룹에 연결 된 외부 풀의 id를 표시 하는 추가 되었습니다. 


+ [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)

  프로세서를 볼 수 있는 새 시스템 카탈로그 뷰 및 특정 리소스 풀 선호도 설정 되는 리소스입니다.

  각 스케줄러가 개별 프로세서에 매핑되는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]의 스케줄러당 하나의 행을 반환합니다. 이 뷰를 사용하여 스케줄러 상태를 모니터링하거나 런어웨이 태스크를 식별할 수 있습니다.

  기본 구성에서 작업 풀 프로세서에 자동으로 할당 됩니다 되며 따라서 반환할 선호도 값이 없습니다.

  선호도 일정은 리소스 풀을 매핑하는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 지정된 된 Id로 식별 되는 일정입니다. 이러한 Id sys.dm_os_schedulers (TRANSACT-SQL)의 scheduler_id 열에 있는 값에 매핑합니다.


> [!NOTE] 
> 
> 구성 및 리소스 풀을 사용자 지정 하는 기능 Enterprise 에서만에서 사용할 수는 같지만 Dmv 뿐만 아니라 개발자 버전, 기본 풀은 모든 버전에서 사용할 수 있습니다. 따라서 R 작업에 대 한 리소스 한도 확인 하려면 이러한 Dmv Standard Edition에서 사용할 수 있습니다. 

모니터링에 대 한 일반적인 내용은 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스 참조 [카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) 및 [리소스 관리자 관련 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)합니다.

## <a name="r-script-execution-and-monitoring"></a>R 스크립트 실행 및 모니터링

R 스크립트에서 실행 하는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 에 의해 시작 되는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 인터페이스입니다. 그러나, 실행 패드 리소스 적용 또는 중인 것으로 간주 된 리소스를 적절 하 게 관리 하는 Microsoft에서 제공 하는 안전한 서비스를 개별적으로 모니터링 하지 않습니다.

실행 패드 서비스에서 실행 되는 개별 R 스크립트를 사용 하 여 관리 되는 [Windows 작업 개체](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx)합니다. 작업 개체 그룹을 하나의 단위로 관리할 수에 대 한 프로세스를 사용 합니다. 각 작업 개체는 계층적 하 고 연결 된 모든 프로세스의 특성을 제어 합니다. 작업 개체에서 수행 된 작업 작업 개체와 연결 된 모든 프로세스를 영향을 줍니다. 

즉, 개체와 연결 하는 하나의 작업을 종료 해야 할 경우 모든 관련된 프로세스가 종료 됩니다도 인식 됩니다. Windows 작업 개체에 할당 된 R 스크립트를 실행 하는 경우 종료 해야 하는 관련된 ODBC 작업을 실행 하는 스크립트는 R 스크립트 프로세스 부모도 종료 됩니다. 

병렬 처리를 사용 하는 R 스크립트를 시작 하는 경우 단일 Windows 작업 개체는 모든 병렬 자식 프로세스를 관리 합니다.

프로세스 작업에서 실행 되 고 있는지를 확인 하려면 사용은 `IsProcessInJob` 함수입니다.

## <a name="see-also"></a>관련 항목:
[관리 및 모니터링](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)

