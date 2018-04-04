---
title: SQL Server 컴퓨터 학습 서비스에 대 한 Dmv | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b3643ea0-d9f3-463f-8ece-572127f32a24
caps.latest.revision: ''
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 2e51f5229eb085eb4b92a4f6f53cc7b28ebb7485
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="dmvs-for-sql-server-machine-learning-services"></a>SQL Server 컴퓨터 학습 서비스에 대 한 Dmv
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

시스템 카탈로그 뷰 및 Dmv는 기계 학습에서 SQL Server 관련 된 문서를 나열 합니다.

확장된 이벤트에 대 한 정보를 참조 하십시오. [기계 학습의 확장 이벤트](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md)합니다.

> [!TIP]
> 제품 팀 컴퓨터 학습 세션 및 패키지 사용률을 모니터링 하는 데 사용할 수 있는 사용자 지정 보고서를 제공 했습니다. 자세한 내용은 참조 [Management Studio에서 사용자 지정 보고서를 사용 하 여 기계 학습 모니터링](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)합니다.

## <a name="system-configuration-and-system-resources"></a>시스템 구성 및 시스템 리소스

모니터링 하 고 외부 스크립트를 사용 하 여 사용 하는 리소스를 분석할 수 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 시스템 카탈로그 뷰 및 Dmv 합니다.

+ [ sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)

  사용자 연결 및 시스템 세션 둘 다에 대한 정보를 반환합니다. *session_id* 열을 보고 시스템 세션을 식별할 수 있습니다. 값이 51보다 크거나 같으면 사용자 연결이고, 값이 51보다 작으면 시스템 프로세스입니다.

+ [sys.dm_os_performance_counters(Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)

  서버에서 사용 중인 각 시스템 성능 카운터에 대한 행을 반환합니다.  이 정보를 사용하여 실행된 스크립트 수, 각 인증 모드를 사용하여 실행된 스크립트 또는 전체 인스턴스에서 실행된 R 호출 수를 확인할 수 있습니다.

  이 예제에서는 R 스크립트와 관련된 카운터만 가져옵니다.

  ```SQL
  SELECT * from sys.dm_os_performance_counters WHERE object_name LIKE '%External Scripts%'
  ```

  인스턴스별로 이 DMV에서 외부 스크립트에 대해 보고되는 카운터는 다음과 같습니다.

  + **총 실행**: 로컬 또는 원격 호출에 의해 시작 되는 외부 프로세스의 수
  + **병렬 실행**: 스크립트를 포함 하는 _@parallel_ 사양과 하 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 을 생성 하는 병렬 쿼리 계획을 사용 하 여 수
  + **실행 될 때 스트리밍**: 스트리밍 기능은 호출 된 횟수
  + **SQL CC 실행**: 수가 외부 스크립트 실행 호출을 원격으로 인스턴스화한 하 고 SQL Server를 사용 하 여 계산 컨텍스트로 써 있는
  + **묵시적 인증. 로그인**: 묵시적 인증을 사용하여 ODBC 루프백 호출이 수행된 횟수, 즉 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 스크립트 요청을 보내는 사용자를 대신하여 호출을 실행한 횟수입니다.
  + **총 실행 시간 (밀리초)**: 호출과 호출이 완료까지 경과 시간
  + **실행 오류**: 스크립트에서 오류를 보고한 횟수입니다. 이 개수는 R 오류를 포함하지 않습니다.


+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)

  이 DMV는 현재 외부 스크립트를 실행 중인 각 작업자 계정에 대해 단일 행을 보고합니다. 이 작업자 계정은 스크립트를 보내는 사용자의 자격 증명과 다릅니다. Windows 사용자 한 명이 여러 스크립트 요청을 보내는 경우 해당 사용자의 모든 요청을 처리할 작업자 계정 하나가 할당됩니다. 다른 Windows 사용자가 외부 스크립트를 실행하기 위해 로그인하는 경우 별도 작업자 계정이 요청을 처리합니다.

  이 DMV는 현재 실행 중인 스크립트가 없는 경우 결과를 반환하지 않으므로 장기 실행 스크립트를 모니터링하는 데 유용합니다. 다음 값이 반환됩니다.

  + **external_script_request_id**: 스크립트 및 중간 결과 저장 하는 데 사용 하는 작업 디렉터리의 임시 이름으로도 사용 되는 A GUID
  + **언어**:와 같은 값 `R` 외부 스크립트의 언어를 표시 하는
  + **degree_of_parallelism**: 사용 된 하는 프로세스 병렬의 수를 나타내는 정수
  + **external_user_name**: A 실행 패드 작업자와 같은 계정 **SQLRUser01**

+ [sys.dm_external_script_execution_stats(Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)

  이 DMV는 내부 추적할 수 외부 스크립트 호출은 인스턴스에서 수행 됩니다 (원격 분석) 모니터링을 위해 제공 됩니다. 원격 분석 서비스를 시작 하는 경우 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 을 수행 하 고 특정 기계 학습 함수를 호출할 때마다 디스크 기반 카운터를 늘립니다.

  특정 추적된 함수 호출당 카운터가 증가 합니다. 예를 들어 `rxLinMod` 가 호출되어 병렬로 실행될 때 카운터는 1씩 증가합니다.
  
  일반적으로 생성된 프로세스가 활성 상태인 경우에만 성능 카운터가 유효합니다. 따라서 DMV에서 쿼리는 실행이 중지된 서비스의 데이터 세부 정보를 표시할 수 없습니다. 예를 들어 실행 패드에서 병렬 R 작업을 여러 개 만들지만 Windows 작업 개체에 의해 빠르게 실행된 후 정리되는 경우 DMV에 데이터가 표시되지 않을 수도 있습니다.
 
  그러나 이 DMV에서 추적하는 카운터는 계속 실행 중 상태로 인스턴스가 종료되더라도 디스크에 쓰기를 사용하여 dm_external_script _execution 카운터의 상태를 유지합니다.
 
 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 사용하는 시스템 성능 카운터에 대한 자세한 내용은 [SQL Server 개체 사용](../../relational-databases/performance-monitor/use-sql-server-objects.md)을 참조하세요.

## <a name="resource-governor-views"></a>리소스 관리자 뷰

버전을 지 원하는 리소스 관리자, Python 또는 R 작업에 대 한 외부 리소스 풀을 만드는 en 효과적으로 추적 하 고 리소스를 관리할 수 있습니다.

+ [sys.resource_governor_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-resource-pools-transact-sql.md)

  현재 리소스 풀 상태, 리소스 풀의 현재 구성 및 리소스 풀 통계에 대한 정보를 반환합니다.

  > [!IMPORTANT]
  > 
  > 다른 서버 서비스에 적용되는 리소스 풀을 먼저 수정해야 R Services에 추가 리소스를 할당할 수 있습니다.

+ [sys.resource_governor_external_resource_pools](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)

  외부 리소스 풀에 대한 현재 구성 값을 보여 주는 새 카탈로그 뷰입니다.
  Enterprise Edition에서 외부 리소스 풀을 추가로 구성할 수 있습니다. 예를 들어 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에서 실행되는 R 작업에 대한 리소스를 원격 클라이언트에서 시작되는 R 작업과 별도로 처리할 수 있습니다.

  > [!NOTE]
  > 
  > Standard Edition에서는 모든 외부 스크립트 작업 같은 외부 기본 리소스 풀 내에서 실행 합니다.

+ [sys.resource_governor_workload_groups](../../relational-databases/system-catalog-views/sys-resource-governor-workload-groups-transact-sql.md)

  작업 그룹 통계 및 작업 그룹의 현재 구성을 반환합니다. 이 뷰는 `sys.dm_resource_governor_resource_pools`와 조인하여 리소스 풀 이름을 가져올 수 있습니다.
  외부 스크립트의 경우 워크로드 그룹과 연결된 외부 풀의 ID를 표시하는 새 열이 추가되었습니다.

+ [sys.dm_resource_governor_external_resource_pool_affinity](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)

  특정 리소스 풀로 선호도가 설정된 프로세서 및 리소스를 확인할 수 있는 새 시스템 카탈로그 뷰입니다.

  각 스케줄러가 개별 프로세서에 매핑되는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]의 스케줄러당 하나의 행을 반환합니다. 이 뷰를 사용하여 스케줄러 상태를 모니터링하거나 런어웨이 태스크를 식별할 수 있습니다.

  기본 구성에서 워크로드 풀은 프로세서에 자동으로 할당되므로 반환할 선호도 값이 없습니다.

  선호도 일정은 리소스 풀을 지정된 ID로 식별된 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 일정에 매핑합니다. 이러한 Id의 값에 매핑하는 `scheduler_id` 열에 `sys.dm_os_schedulers`합니다.


> [!NOTE] 
> 
> 리소스 풀을 구성 및 사용자 지정하는 기능은 Enterprise 및 Developer Edition에서만 사용할 수 있지만 기본 풀과 DMV는 모든 버전에서 사용할 수 있습니다. 따라서 외부 스크립트 작업에 대 한 리소스 캡을 확인 하려면 이러한 Dmv Standard Edition에서 사용할 수 있습니다.

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스 모니터링에 대한 일반적인 내용은 [카탈로그 뷰](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md) 및 [리소스 관리자 관련 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)를 참조하세요.

## <a name="monitoring-script-execution"></a>모니터링 스크립트 실행

실행 되는 R 및 Python 스크립트 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 에 의해 시작 된 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 인터페이스입니다. 그러나 실행 패드는 리소스를 적절하게 관리하는, Microsoft에서 제공하는 안전한 서비스로 간주되므로 개별적으로 리소스가 관리되거나 모니터링되지 않습니다.

실행 패드 서비스에서 실행 되는 개별 스크립트를 사용 하 여 관리 되는 [Windows 작업 개체](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx)합니다. 작업 개체를 사용하면 프로세스 그룹을 하나의 단위로 관리할 수 있습니다. 각 작업 개체는 계층적이며 연결된 모든 프로세스의 특성을 제어합니다. 작업 개체에서 수행된 작업은 작업 개체와 연결된 모든 프로세스에 영향을 줍니다.

즉, 개체와 연결된 하나의 작업을 종료해야 하는 경우 관련된 모든 프로세스도 종료됨에 유의하세요. Windows 작업 개체에 할당된 R 스크립트를 실행 중이며 해당 스크립트가 실행하는 관련된 ODBC 작업을 종료해야 하는 경우 부모 R 스크립트 프로세스도 종료됩니다.

병렬 처리를 사용 하는 외부 스크립트를 시작 하는 경우 단일 Windows 작업 개체는 모든 병렬 자식 프로세스를 관리 합니다.

작업에서 프로세스가 실행되고 있는지 확인하려면 `IsProcessInJob` 함수를 사용합니다.

## <a name="next-steps"></a>다음 단계

[기계 학습 솔루션 관리 및 모니터링](../../advanced-analytics/r/managing-and-monitoring-r-solutions.md)
