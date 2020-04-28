---
title: 버퍼 풀 확장 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 909ab7d2-2b29-46f5-aea1-280a5f8fedb4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9e435ab4cec86d439a7e2fba31f6099bf8668ec0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175438"
---
# <a name="buffer-pool-extension"></a>Buffer Pool Extension
  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 도입된 버퍼 풀 확장은 I/O 처리량을 크게 향상하기 위해 비휘발성 RAM(즉, 반도체 드라이브) 확장을 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 버퍼 풀에 원활하게 통합할 수 있는 기능을 제공합니다. 버퍼 풀 확장은 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서만 제공됩니다. 자세한 내용은 [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조하세요.

## <a name="benefits-of-the-buffer-pool-extension"></a>버퍼 풀 확장의 이점
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 주 목적은 데이터 저장 및 검색이므로 데이터베이스 엔진의 핵심 특성은 집중형 디스크 I/O입니다. 디스크 I/O 작업은 많은 리소스를 소비하며 완료하는 데 비교적 오랜 시간이 걸리므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 I/O의 효율성을 높이는 데 주안점을 둡니다. 버퍼 풀은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 주 메모리 할당 원본으로 사용됩니다. 버퍼 관리는 이러한 효율성을 얻기 위한 핵심 구성 요소입니다. 버퍼 관리 구성 요소는 데이터베이스 페이지에 액세스하고 업데이트하기 위한 버퍼 관리자와 데이터베이스 파일 I/O를 줄이기 위한 버퍼 풀의 두 가지 메커니즘으로 구성되어 있습니다.

 데이터 및 인덱스 페이지는 디스크에서 버퍼 풀로 읽히고 수정된 페이지(더티 페이지라고도 함)는 디스크에 다시 쓰여집니다. 서버 및 데이터베이스 검사점에서 메모리가 부족하면 버퍼 캐시에 있는 핫(활성) 더티 페이지가 캐시에서 제거되고 기계식 디스크에 쓰여진 다음 다시 캐시에서 읽힙니다. 일반적으로 이러한 I/O 작업은 4KB 데이터에서 16KB 데이터 정도의 작은 임의 읽기 및 쓰기입니다. 작은 임의 I/O 패턴은 잦은 검색을 유발하기 때문에 기계식 디스크 충돌 경합이 발생하고, I/O 대기 시간이 증가하며, 시스템의 총 I/O 처리량이 감소합니다.

 이러한 I/O 병목 상태를 해결하는 일반적인 방법은 DRAM이나 고성능 SAS 스핀들을 추가하는 것입니다. 이러한 방법은 도움이 되지만 중요한 단점이 있습니다. DRAM은 데이터 스토리지 드라이브보다 더 비싸며, 스핀들 추가는 하드웨어 구입 비용을 증가시킵니다. 또한 전력 소비가 많고 구성 요소의 오류 발생 가능성이 높아 운영 비용이 증가합니다.

 버퍼 풀 확장 기능은 비휘발성 스토리지(일반적으로 SSD)로 버퍼 풀 캐시를 확장합니다. 이 확장 덕분에 버퍼 풀은 더 큰 데이터베이스 작업 집합을 수용할 수 있고, 그에 따라 RAM과 SSD 간의 I/O 페이징이 강제로 수행됩니다. 따라서 작은 임의 I/O가 기계식 디스크에서 SSD로 효과적으로 오프로드됩니다. SSD의 더 낮은 대기 시간과 향상된 임의 I/O 성능 덕분에 버퍼 풀 확장은 I/O 처리량을 크게 향상합니다.

 다음 목록에서는 버퍼 풀 확장 기능의 이점에 대해 설명합니다.

-   임의 I/O 처리량의 증가

-   I/O 대기 시간의 감소

-   트랜잭션 처리량의 증가

-   더 큰 하이브리드 버퍼 풀로 읽기 성능 향상

-   현재와 미래의 저렴한 메모리 드라이브를 사용할 수 있는 캐싱 아키텍처

### <a name="concepts"></a>개념
 다음은 버퍼 풀 확장 기능에 적용되는 용어입니다.

 SSD (반도체 드라이브) 반도체 드라이브는 메모리 (RAM)에 데이터를 영구적으로 저장 합니다. 자세한 내용은 [이 정의](http://en.wikipedia.org/wiki/Solid-state_drive)를 참조하십시오.

 버퍼에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버퍼는 데이터 또는 인덱스 페이지와 크기가 같은 메모리의 8kb 페이지입니다. 따라서 버퍼 캐시는 8KB 페이지로 나누어집니다. 페이지는 버퍼 관리자에 더 많은 데이터를 읽어 올 버퍼 영역이 필요할 때까지 버퍼 캐시에 남아 있습니다. 데이터는 수정되는 경우에만 다시 디스크에 쓰여집니다. 이러한 메모리 내의 수정된 페이지를 더티 페이지라고 합니다. 디스크에 있는 해당 데이터베이스 이미지와 동일한 페이지를 클린 페이지라고 합니다. 버퍼 캐시의 데이터는 여러 번 수정한 후 디스크에 다시 쓸 수 있습니다.

 버퍼 풀은 버퍼 캐시 라고도 합니다. 버퍼 풀은 캐시된 데이터 페이지를 저장하기 위해 모든 데이터베이스에서 공유하는 전역 리소스입니다. 버퍼 풀 캐시의 최대 및 최소 크기는 시작하는 동안 결정되거나 SQL Server 인스턴스가 sp_configure를 사용하여 동적으로 다시 구성될 때 결정됩니다. 이 크기에 따라 실행 중인 인스턴스에서 언제든지 버퍼 풀에 캐시할 수 있는 최대 페이지 수가 결정됩니다.

 검사점 검사점은 예기치 않은 종료 또는 충돌 후 복구 하 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 는 동안에서 트랜잭션 로그에 포함 된 변경 내용을 적용 하기 시작할 수 있는 알려진 올바른 지점을 만듭니다. 검사점은 메모리 내의 더티 페이지와 트랜잭션 로그 정보를 디스크에 쓰고 트랜잭션 로그에 대한 정보도 기록합니다. 자세한 내용은 [데이터베이스 검사점&#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)을 참조하세요.

## <a name="buffer-pool-extension-details"></a>버퍼 풀 확장 세부 정보
 SSD 스토리지는 디스크 스토리지 하위 시스템보다는 메모리 하위 시스템에 대한 확장으로 사용됩니다. 즉, 버퍼 풀 확장 파일을 통해 버퍼 풀 관리자는 DRAM 및 NAND 플래시 메모리를 둘 다 사용하여 SSD에서 지원하는 비휘발성 RAM에서 비활성화된 페이지에 대해 훨씬 더 큰 버퍼 풀을 유지 관리할 수 있습니다. 그러면 SSD에서 L1(수준 1)이 DRAM이고 L2(수준)가 버퍼 풀 확장 파일인 여러 수준 캐싱 계층이 만들어집니다. L2 캐시에는 클린 페이지만 기록되므로 데이터 안전을 유지할 수 있습니다. 버퍼 관리자는 L1 캐시와 L2 캐시 간의 클린 페이지 이동을 처리합니다.

 다음 그림에서는 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소를 기준으로 버퍼 풀에 대한 대략적인 아키텍처 개요를 보여 줍니다.

 ![SSD 버퍼 풀 확장 아키텍처](../media/ssdbufferpoolextensionarchitecture.gif "SSD 버퍼 풀 확장 아키텍처")

 사용하도록 설정된 경우 버퍼 풀 확장은 SSD에 있는 버퍼 풀 캐싱 파일의 크기와 파일 경로를 지정합니다. 이 파일은 SSD에 있는 스토리지의 인접 익스텐트이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 시작하는 동안 정적으로 구성됩니다. 파일 구성 매개 변수의 변경은 버퍼 풀 확장 기능이 사용하지 않도록 설정된 경우에만 수행할 수 있습니다. 버퍼 풀 확장이 사용하지 않도록 설정된 경우 관련된 모든 구성 설정이 레지스트리에서 제거됩니다. 버퍼 풀 확장 파일은 SQL Server 인스턴스를 종료하면 즉시 삭제됩니다.

## <a name="best-practices"></a>모범 사례
 다음과 같은 최선의 구현 방법을 따르십시오.

-   처음으로 버퍼 풀 확장을 사용하도록 설정한 경우 최대 성능 이점을 얻으려면 SQL Server 인스턴스를 다시 시작하는 것이 좋습니다.

-   버퍼 풀 확장 크기는 Enterprise 버전에서 max_server_memory 값의 최대 32배이며 Standard 버전에서는 4배입니다.  실제 메모리(max_server_memory) 크기와 버퍼 풀 확장 크기의 비율을 1:16 이하로 유지하는 것이 좋습니다. 1:4에서 1:8 사이의 범위에서 더 낮은 비율이 최적일 수 있습니다. max_server_memory 옵션을 설정하는 방법은 [서버 메모리 서버 구성 옵션](server-memory-server-configuration-options.md)을 참조하세요.

-   프로덕션 환경에서 구현하기 전에 버퍼 풀 확장을 철저히 테스트합니다. 프로덕션 환경에서는 파일 구성을 변경하거나 기능을 사용하지 않도록 설정하지 마십시오. 기능을 사용하지 않도록 설정하면 버퍼 풀 크기가 크게 감소하기 때문에 이러한 활동은 서버 성능에 부정적인 영향을 미칠 수 있습니다. 사용하지 않도록 설정하면 SQL Server 인스턴스를 다시 시작할 때까지 기능을 지원하는 데 사용된 메모리가 회수되지 않습니다. 하지만 기능을 다시 사용하도록 설정하면 인스턴스를 다시 시작하지 않고도 메모리가 다시 사용됩니다.

## <a name="return-information-about-the-buffer-pool-extension"></a>버퍼 풀 확장에 대한 정보 반환
 다음과 같은 동적 관리 뷰를 사용하여 버퍼 풀 확장의 구성을 표시하고 확장에 있는 데이터 페이지에 대한 정보를 반환할 수 있습니다.

-   [sys.dm_os_buffer_pool_extension_configuration&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql)

-   [sys.dm_os_buffer_descriptors&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql)

 성능 카운터는 SQL Server, Buffer Manager 개체에서 버퍼 풀 확장 파일에 있는 데이터 페이지를 추적하기 위해 사용할 수 있습니다. 자세한 내용은 [버퍼 풀 확장 성능 카운터](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)를 참조하십시오.

 다음과 같은 Xevent를 사용할 수 있습니다.

|XEvent|설명|매개 변수|
|------------|-----------------|----------------|
|sqlserver.buffer_pool_extension_pages_written|페이지 또는 페이지 그룹을 버퍼 풀에서 제거하여 버퍼 풀 확장 파일에 쓸 때 발생합니다.|number_page<br /><br /> first_page_id<br /><br /> first_page_offset<br /><br /> initiator_numa_node_id|
|sqlserver.buffer_pool_extension_pages_read|페이지를 버퍼 풀 확장 파일에서 가져와서 버퍼 풀에 쓸 때 발생합니다.|number_page<br /><br /> first_page_id<br /><br /> first_page_offset<br /><br /> initiator_numa_node_id|
|sqlserver.buffer_pool_extension_pages_evicted|페이지를 버퍼 풀 확장 파일에서 제거할 때 발생합니다.|number_page<br /><br /> first_page_id<br /><br /> first_page_offset<br /><br /> initiator_numa_node_id|
|sqlserver.buffer_pool_eviction_thresholds_recalculated|제거 임계값을 계산할 때 발생합니다.|warm_threshold<br /><br /> cold_threshold<br /><br /> pages_bypassed_eviction<br /><br /> eviction_bypass_reason<br /><br /> eviction_bypass_reason_description|

## <a name="related-tasks"></a>관련 작업

|||
|-|-|
|**태스크 설명**|**항목**|
|버퍼 풀 확장을 사용하도록 설정하고 구성합니다.|[ALTER SERVER CONFIGURATION&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)|
|버퍼 풀 확장 구성을 수정합니다.|[ALTER SERVER CONFIGURATION&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)|
|버퍼 풀 확장 구성을 봅니다.|[sys.dm_os_buffer_pool_extension_configuration&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql)|
|버퍼 풀 확장을 모니터링합니다.|[sys.dm_os_buffer_descriptors&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql)<br /><br /> [성능 카운터](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)|


