---
title: 병합 복제 성능 향상 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- designing databases [SQL Server], replication performance
- Merge Agent, performance
- snapshots [SQL Server replication], performance considerations
- merge replication performance [SQL Server replication]
- subscriptions [SQL Server replication], performance considerations
- performance [SQL Server replication], merge replication
- agents [SQL Server replication], performance
ms.assetid: f929226f-b83d-4900-a07c-a62f64527c7f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 261f22847c8b397d57ff5f732ea4d97091895daa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939208"
---
# <a name="enhance-merge-replication-performance"></a>병합 복제 성능 향상
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [일반적인 복제 성능 향상](../../../relational-databases/replication/administration/enhance-general-replication-performance.md)에서 설명하는 일반적인 성능 팁을 고려한 후 병합 복제에 대한 다음 영역을 추가로 고려해 보십시오.  
  
## <a name="database-design"></a>데이터베이스 디자인  
  
-   행 필터 및 조인 필터에 사용된 열을 인덱싱합니다.  
  
     게시된 아티클에 행 필터를 사용하는 경우 필터의 WHERE 절에 사용되는 각 열에 인덱스를 만듭니다. 인덱스가 없으면 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 테이블의 각 행을 읽은 후 해당 행을 파티션에 포함할 것인지 여부를 결정합니다. 인덱스가 있다면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 어떤 행을 포함해야 하는지를 빨리 찾을 수 있습니다. 복제가 인덱스에서만 필터의 WHERE 절을 모두 확인하면 가장 빠른 처리가 이루어집니다.  
  
     조인 필터에 사용되는 모든 열에 인덱스를 만드는 것도 중요합니다. 병합 에이전트는 실행될 때마다 기본 테이블의 어떤 열과 관련 테이블의 어떤 열을 파티션에 포함할 것인지를 결정하기 위해 부모 테이블을 검색합니다. 조인된 열에 인덱스를 만들면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 병합 에이전트가 실행될 때마다 테이블의 각 행을 읽지 않아도 됩니다.  
  
     필터링에 대한 자세한 내용은 [병합 복제의 게시된 데이터 필터링](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)을 참조하세요.  
  
-   LOB(Large Object) 데이터 형식을 포함하는 테이블을 너무 많이 정규화한 경우를 고려해 보십시오.  
  
     동기화가 발생할 때 병합 에이전트는 게시자 또는 구독자에서 전체 데이터 행을 읽고 전송해야 합니다. 이 행에 LOB를 사용하는 열이 있다면 추가 메모리 할당이 필요하고 이러한 열이 업데이트되지 않았어도 성능에 부정적 영향을 미칠 수 있습니다. 이렇게 성능에 미칠 영향을 줄이려면 나머지 행 데이터에 대해 일 대 일 관계를 사용하여 LOB 열을 별개의 테이블에 두도록 합니다. **text**, **ntext**및 **image** 데이터 형식은 사용되지 않습니다. LOB를 포함시킬 경우 데이터 형식 **varchar(max)** , **nvarchar(max)** , **varbinary(max)** 를 각각 사용하는 것이 좋습니다.  
  
## <a name="publication-design"></a>게시 디자인  
  
-   90RTM([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전)의 게시 호환성 수준을 사용합니다.  
  
     하나 이상의 구독자가 동일한 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용하면 게시에서 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전만 지원하도록 지정합니다. 이렇게 하면 게시에서 새로운 기능과 성능 최적화를 사용할 수 있습니다.  
  
-   적절한 게시 보존 설정을 사용합니다.  
  
     구독이 동기화되기 전까지의 최대 시간을 나타내는 게시 보존 기간은 추적 메타데이터가 저장되는 기간을 결정합니다. 값이 높으면 스토리지 및 처리 성능에 영향을 줄 수 있습니다. 게시 보존 기간을 설정하는 방법은 [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)를 참조하십시오.  
  
-   게시자에서만 변경되는 테이블의 다운로드 전용 아티클을 사용합니다. 자세한 내용은 [다운로드 전용 아티클로 병합 복제 성능 최적화](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)를 참조하세요.  
  
### <a name="filter-design-and-use"></a>필터 디자인 및 사용  
  
-   행 필터 절의 복잡도를 제한합니다.  
  
     필터링 조건의 복잡도를 제한하면 병합 에이전트가 구독자로 보낼 행 변경 내용을 평가할 때 성능을 향상시킬 수 있습니다. 병합 행 필터 절에 하위 선택을 사용하지 않도록 합니다. 대신 다른 테이블의 행 필터 절을 기반으로 하는 한 테이블에서 데이터를 보다 효율적으로 분할할 수 있는 조인 필터의 사용을 고려합니다. 필터링에 대한 자세한 내용은 [병합 복제의 게시된 데이터 필터링](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)을 참조하세요.  
  
-   매개 변수가 있는 필터와 함께 사전 계산 파티션을 사용합니다. 이 기능은 기본적으로 사용됩니다. 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요.  
  
     사전 계산 파티션은 여러 가지 필터링 동작을 제한합니다. 애플리케이션이 이러한 제한 사항을 따를 수 없는 경우 **keep_partition_changes** 옵션을 **True**로 설정하면 성능상 이점이 있습니다. 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)를 참조하세요.  
  
-   데이터가 필터링되었지만 사용자 간에 공유되지 않으면 겹치지 않는 파티션을 사용합니다.  
  
     복제에서는 파티션 또는 구독 간에 공유되지 않는 데이터의 성능을 최적화할 수 있습니다. 자세한 내용은 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)를 참조하세요.  
  
-   복잡한 조인 필터 계층을 만들지 않습니다.  
  
     5개 이상의 테이블을 가진 조인 필터는 병합 처리 중 성능에 크게 영향을 줄 수 있습니다. 5개 이상의 테이블을 가진 조인 필터를 생성하는 경우 다른 해결책을 고려하는 것이 좋습니다.  
  
    -   주로 조회 테이블, 작은 테이블 및 변경이 필요하지 않은 테이블로 구성된 테이블은 필터링하지 않습니다. 이러한 테이블을 전체적으로 게시의 일부로 만듭니다. 구독자 간에 분할되어야 하는 테이블 사이에만 조인 필터를 사용하는 것이 좋습니다. 자세한 내용은 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)를 참조하세요.  
  
    -   조인에 테이블이 많은 경우 데이터베이스 디자인을 비정규화하거나 매핑 테이블을 사용할 것을 고려합니다. 예를 들어 영업 사원은 자신의 고객에 대한 데이터만 필요한 경우 고객을 영업 사원과 연결하기 위해 6개의 조인이 필요하다면 영업 사원을 식별하는 customer 테이블에 열을 추가할 것을 고려합니다. 영업 사원 데이터는 중복되지만 복제를 분할하는 것이 해당 테이블을 비정규화하는 것보다 성능상 이점이 있습니다.  
  
    -   일괄 처리에 많은 데이터 변경 사항이 있을 때 사전 계산 파티션의 성능을 향상시키기 위해 신중하게 애플리케이션을 디자인합니다. 조인 필터에서 부모 테이블의 데이터 변경은 자식 테이블의 해당 데이터 변경보다 먼저 수행되어야 합니다.  
  
-   논리에 맞는 경우 **join_unique_key** 옵션을 **1** 로 설정합니다.  
  
     이 매개 변수를 **1** 로 설정하면 조인 필터에서 자식 테이블과 부모 테이블 사이의 관계가 일 대 일 또는 일 대 다가 됩니다. 자식 테이블의 조인 열에 고유성을 보장하는 제약 조건이 있는 경우에만 이 매개 변수를 **1** 로 설정하십시오. 그렇지 않은 경우에 이 매개 변수를 **1** 로 설정하면 데이터가 일치하지 않을 수 있습니다. 자세한 내용은 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)를 참조하세요.  
  
-   사전 계산 파티션을 사용하는 경우 많은 변경 사항이 있는 일괄 처리를 실행하지 않도록 합니다.  
  
     많은 데이터 변경 사항이 있는 일괄 처리를 실행한 후 병합 에이전트를 실행하면 이 에이전트에서 큰 일괄 처리를 여러 개의 작은 일괄 처리로 나눕니다. 이 시간 동안 다른 병합 에이전트 프로세스는 차단될 수 있습니다. 일괄 처리의 변경 사항 수를 줄이고 일괄 처리 사이에 병합 에이전트를 실행하십시오. 이렇게 할 수 없으면 게시에 대한 **generation_leveling_threshold** 값을 늘립니다.  
  
## <a name="subscription-considerations"></a>구독 고려 사항  
  
-   구독 동기화 일정은 엇갈리게 설정합니다.  
  
     많은 구독자가 게시자와 동기화하는 경우 각각의 병합 에이전트가 서로 다른 시간에 실행되도록 일정을 엇갈리게 설정해 봅니다. 자세한 내용은 [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md)을 참조하세요.  
  
## <a name="merge-agent-parameters"></a>병합 에이전트 매개 변수  
 병합 에이전트와 해당 매개 변수에 대한 자세한 내용은 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)를 참조하십시오.  
  
-   끌어오기 구독에 대한 모든 구독자를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전으로 업그레이드합니다.  
  
     구독자를 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전으로 업그레이드하면 해당 구독자의 구독에서 사용한 병합 에이전트가 업그레이드됩니다. 여러 가지 새로운 기능과 성능 최적화를 사용하려면 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전의 병합 에이전트가 필요합니다.  
  
-   구독이 빠른 연결을 통해 동기화되고 게시자에서 구독자로 변경 내용이 전송되면 병합 에이전트에 대해 **–ParallelUploadDownload** 매개 변수를 사용합니다.  
  
     [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 에서는 새로운 병합 에이전트 매개 변수인 **–ParallelUploadDownload**가 도입되었습니다. 이 매개 변수를 설정하면 병합 에이전트가 게시자로 업로드되는 변경 내용과 구독자로 다운로드되는 변경 내용을 병렬로 처리할 수 있습니다. 이것은 네트워크 대역폭이 높은 대규모 환경에서 유용합니다. 에이전트 프로필 및 명령줄에서 에이전트 매개 변수를 지정할 수 있습니다. 참조 항목:  
  
    -   [복제 에이전트 프로필 작업](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [복제 에이전트의 명령 프롬프트 매개 변수 보기 및 수정&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
-   특히 동기화할 때 구독자로부터의 업로드와 구독자로의 다운로드가 더 많이 필요한 경우 **-MakeGenerationInterval** 매개 변수의 값을 늘릴 것을 고려합니다.  
  
-   LOB 열이 있는 행처럼 많은 양의 데이터가 있는 데이터 행을 동기화할 때는 웹 동기화에 추가 메모리 할당이 필요하고 성능이 저하될 수 있습니다. 병합 에이전트에서 대량의 데이터가 있는 데이터 행을 너무 많이 포함한 XML 메시지를 생성하는 경우 이러한 현상이 발생합니다. 병합 에이전트가 웹 동기화 중에 너무 많은 리소스를 소비하는 경우 다음 중 한 가지 방법으로 단일 메시지에 보내는 행 수를 줄이십시오.  
  
    -   병합 에이전트에 느린 연결 에이전트 프로필을 사용합니다. 자세한 내용은 [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)을 참조하세요.  
  
    -   병합 에이전트의 경우 **-DownloadGenerationsPerBatch** 및 **-UploadGenerationsPerBatch** 매개 변수를 10 이하의 값으로 줄입니다. 이들 매개 변수의 기본값은 50입니다.  
  
## <a name="snapshot-considerations"></a>스냅샷 고려 사항  
  
-   초기 스냅샷을 생성하기 전에 대형 테이블에 ROWGUIDCOL 열을 만듭니다.  
  
     병합 복제에서 게시된 각 테이블은 ROWGUIDCOL 열을 가져야 합니다. 스냅샷 에이전트가 초기 스냅샷 파일을 만들기 전에 ROWGUIDCOL 열이 테이블에 없다면 에이전트는 우선 ROWGUIDCOL 열을 추가하고 채워야 합니다. 병합 복제 중 스냅샷을 생성할 때 성능을 향상시키려면 게시하기 전 각 테이블에 ROWGUIDCOL 열을 만듭니다. 이 열은 어떤 이름도 가질 수 있지만(기본적으로 스냅샷 에이전트는**rowguid** 를 사용) 다음 데이터 형식 특징이 있어야 합니다.  
  
    -   UNIQUEIDENTIFIER 데이터 형식  
  
    -   NEWSEQUENTIALID() 또는 NEWID()의 기본값. NEWSEQUENTIALID()는 변경을 수행하고 추적할 때 성능을 향상시킬 수 있으므로 사용하는 것이 좋습니다.  
  
    -   ROWGUIDCOL 속성 집합  
  
    -   열에 있는 고유 인덱스  
  
-   스냅샷을 미리 생성하거나 구독자가 처음 동기화될 때 스냅샷의 생성과 적용을 요청하도록 합니다.  
  
     이러한 옵션 중 하나 또는 둘 모두를 사용하여 매개 변수가 있는 필터를 사용하는 게시에 대한 스냅샷을 제공할 수 있습니다. 이러한 옵션을 하나도 지정하지 않으면 **bcp** 유틸리티를 사용하지 않고 일련의 SELECT 및 INSERT 문을 사용하여 구독을 초기화하게 되는데 이 경우 프로세스의 속도가 훨씬 느립니다. 자세한 내용은 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을(를) 참조하세요.  
  
## <a name="maintenance-and-monitoring-considerations"></a>유지 관리 및 모니터링 고려 사항  
  
-   병합 복제 시스템 테이블의 인덱스를 가끔씩 다시 만듭니다.  
  
     병합 복제 유지 관리 목적으로, 병합 복제와 연결된 **MSmerge_contents**, **MSmerge_genhistory** 및 **MSmerge_tombstone**, **MSmerge_current_partition_mappings** 및 **MSmerge_past_partition_mappings** 시스템 테이블의 증가를 확인합니다. 이러한 테이블의 인덱스를 주기적으로 다시 만듭니다. 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조하세요.  
  
-   복제 모니터의 **동기화 기록** 탭을 사용하여 동기화 성능을 모니터링합니다.  
  
     병합 복제의 경우 복제 모니터는 각 처리 단계(변경 내용 업로드, 변경 내용 다운로드 등)에 소요된 시간을 포함하여 동기화 중에 처리된 각 아티클에 대한 자세한 통계를 **동기화 기록** 탭에 표시합니다. 이 통계는 속도 저하의 원인이 되고 병합 구독의 성능 문제를 해결하기에 가장 적합한 특정 테이블을 정확히 찾아내는 데 도움이 될 수 있습니다. 자세한 통계 보기에 대한 자세한 내용은 [복제 모니터를 사용하여 정보 보기 및 태스크 수행](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)을 참조하세요.  
  
  
