---
title: "데이터 흐름 성능 기능 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Integration Services packages, performance
- performance [Integration Services]
- data flow [Integration Services], troubleshooting
- SQL Server Integration Services packages, performance
- loading data
- control flow [Integration Services], troubleshooting
- SSIS packages, performance
- packages [Integration Services], performance
- queries [Integration Services], troubleshooting
- sorting data [Integration Services]
- aggregations [Integration Services]
ms.assetid: c4bbefa6-172b-4547-99a1-a0b38e3e2b05
caps.latest.revision: "69"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1598f40bb947a98b8fccc8ae47ba1dd7b9447b0a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="data-flow-performance-features"></a>데이터 흐름 성능 기능
  이 항목에서는 일반적인 성능 문제를 방지할 수 있도록 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 디자인하는 방법에 대한 제안 사항을 제공합니다. 또한 이 항목에서는 패키지의 성능 문제를 해결하기 위해 사용할 수 있는 기능 및 도구에 대한 정보를 제공합니다.  
  
## <a name="configuring-the-data-flow"></a>데이터 흐름 구성  
 성능 향상을 위해 데이터 흐름 태스크를 구성하려면 태스크의 속성을 구성하고 버퍼 크기를 조정하며 패키지에 대해 병렬 실행을 구성합니다.  
  
### <a name="configure-the-properties-of-the-data-flow-task"></a>데이터 흐름 태스크의 속성 구성  
  
> [!NOTE]  
>  이 섹션에 설명된 속성은 패키지의 각 데이터 흐름 태스크에 대해 개별적으로 설정해야 합니다.  
  
 성능에 영향을 주는 다음 데이터 흐름 태스크 속성을 구성할 수 있습니다.  
  
-   버퍼 데이터의 임시 저장소 위치(BufferTempStoragePath 속성)와 BLOB(Binary Large Object) 데이터가 들어 있는 열의 임시 저장소 위치(BLOBTempStoragePath 속성)를 지정합니다. 기본적으로 이러한 속성에는 TEMP 및 TMP 환경 변수의 값이 포함됩니다. 다른 폴더를 지정하여 임시 파일을 다른 하드 디스크 드라이브 또는 보다 빠른 하드 디스크 드라이브에 넣거나 해당 파일을 여러 드라이브로 분산할 수 있습니다. 디렉터리 이름을 세미콜론으로 구분하여 여러 디렉터리를 지정할 수 있습니다.  
  
-   DefaultBufferSize 속성을 설정하여 태스크에서 사용되는 버퍼의 기본 크기를 정의하고, DefaultBufferMaxRows 속성을 설정하여 각 버퍼의 최대 행 개수를 정의합니다. 버퍼의 기본 크기를 DefaultBufferMaxRows 속성 값에서 자동으로 계산할지 여부를 나타내는 AutoAdjustBufferSize 속성을 설정합니다. 기본 버퍼 크기는 10MB이고 최대 버퍼 크기는 2^31-1바이트입니다. 기본 최대 행 개수는 10,000개입니다.  
  
-   EngineThreads 속성을 설정하여 실행 중에 태스크에서 사용할 수 있는 스레드 수를 설정합니다. 이 속성은 데이터 흐름 엔진에 사용할 스레드 수에 대한 제안 사항을 제공합니다. 기본값은 10이고 최소값은 3입니다. 그러나 데이터 흐름 엔진은 이 속성 값에 관계없이 필요한 만큼의 스레드만 사용합니다. 동시성 문제를 방지하기 위해 필요한 경우에는 엔진에서 이 속성에 지정된 것보다 많은 수의 스레드를 사용할 수도 있습니다.  
  
-   데이터 흐름 태스크가 최적 모드에서 실행되는지 여부(RunInOptimizedMode 속성)를 나타냅니다. 최적화된 모드는 데이터 흐름에서 사용되지 않은 열, 출력 및 구성 요소를 제거하여 성능을 향상합니다.  
  
    > [!NOTE]  
    >  같은 이름의 속성인 RunInOptimizedMode를 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 프로젝트 수준에서 설정하여 데이터 흐름 태스크가 디버깅 중에 최적화된 모드에서 실행되도록 나타낼 수 있습니다. 이 프로젝트 속성은 디자인 타임에 데이터 흐름 태스크의 RunInOptimizedMode 속성보다 우선합니다.  
  
### <a name="adjust-the-sizing-of-buffers"></a>버퍼 크기 조정  
 데이터 흐름 엔진은 단일 데이터 행의 예상 크기를 계산하여 버퍼 크기 조정 태스크를 시작합니다. 그런 다음 예상 행 크기를 DefaultBufferMaxRows 값으로 곱하여 버퍼 크기의 예비 작업 값을 구합니다.  
  
-   AutoAdjustBufferSize를 true로 설정하면 데이터 흐름 엔진은 계산된 값을 버퍼 크기로 사용하고 DefaultBufferSize의 값은 무시됩니다.  
  
-   AutoAdjustBufferSize를 false로 설정하면 데이터 흐름 엔진은 버퍼 크기를 결정하기 위해 다음 규칙을 사용합니다.  
  
    -   결과가 DefaultBufferSize 값보다 크면 엔진은 행 개수를 줄입니다.  
  
    -   결과가 내부적으로 계산된 최소 버퍼 크기보다 작으면 엔진은 행 개수를 늘립니다.  
  
    -   결과가 최소 버퍼 크기와 DefaultBufferSize 값 사이에 있으면 엔진은 예상 행 크기에 DefaultBufferMaxRows 값을 곱한 값에 가능한 한 근접하게 버퍼 크기를 조정합니다.  
  
 데이터 흐름 태스크의 성능 테스트를 시작할 때는 DefaultBufferSize 및 DefaultBufferMaxRows의 기본값을 사용합니다. 데이터 흐름 태스크에 대한 로깅을 설정하고 BufferSizeTuning 이벤트를 선택하여 각 버퍼에 포함된 행 개수를 확인합니다.  
  
 버퍼의 크기를 조정하기 전에 불필요한 열을 제거하고 데이터 형식을 적절하게 구성하여 각 데이터 행의 크기를 줄이는 방식으로 성능을 향상시켜 보는 것이 좋습니다.  
  
 최적의 버퍼 수와 버퍼 크기를 확인하려면 DefaultBufferSize 및 DefaultBufferMaxRows 값으로 시험하면서 BufferSizeTuning 이벤트에서 보고된 정보와 성능을 모니터링합니다.  
  
 디스크에 대한 페이징이 발생하는 수준까지 버퍼 크기를 늘리지 마십시오. 디스크에 대한 페이징은 최적화되지 않은 버퍼 크기 이상으로 성능을 저하시킵니다. 페이징의 발생 여부를 확인하려면 MMC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console)의 성능 스냅인에서 "Buffers spooled" 성능 카운터를 모니터링합니다.  
  
### <a name="configure-the-package-for-parallel-execution"></a>패키지에 대해 병렬 실행 구성  
 병렬 실행은 실제 프로세서나 논리적 프로세서가 여러 개 있는 컴퓨터에서 성능을 향상시킵니다. 패키지에 있는 다른 태스크의 병렬 실행을 지원하기 위해 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서는 **MaxConcurrentExecutables** 와 **EngineThreads**라는 두 속성을 사용합니다.  
  
#### <a name="the-maxconcurrentexcecutables-property"></a>MaxConcurrentExcecutables 속성  
 **MaxConcurrentExecutables** 속성은 패키지 자체의 속성입니다. 이 속성은 동시에 실행할 수 있는 태스크 수를 정의합니다. 기본값인 -1은 논리적 프로세서나 실제 프로세서 수에서 2를 더한 수를 의미합니다.  
  
 이 속성이 작동하는 방식을 이해하기 위해 세 개의 데이터 흐름 태스크가 있는 샘플 패키지를 살펴 봅니다. **MaxConcurrentExecutables** 를 3으로 설정하면 세 개의 데이터 흐름 태스크가 모두 동시에 실행될 수 있습니다. 그러나 각 데이터 흐름 태스크에 원본에서 대상으로의 실행 트리가 10개 있다고 가정할 때 **MaxConcurrentExecutables** 를 3으로 설정하면 각 데이터 흐름 태스크 내에서 실행 트리가 병렬로 실행되지 않을 수 있습니다.  
  
#### <a name="the-enginethreads-property"></a>EngineThreads 속성  
 **EngineThreads** 속성은 각 데이터 흐름 태스크의 속성입니다. 이 속성은 데이터 흐름 엔진에서 만들어 병렬로 실행할 수 있는 스레드 수를 정의합니다. **EngineThreads** 속성은 데이터 흐름 엔진에서 원본에 대해 만드는 원본 스레드와 해당 엔진에서 변환 및 대상에 대해 만드는 작업자 스레드 모두에 동일하게 적용됩니다. 따라서 **EngineThreads** 를 10으로 설정하면 엔진에서 원본 스레드와 작업자 스레드를 각각 10개까지 만들 수 있습니다.  
  
 이 속성이 작동하는 방식을 이해하기 위해 세 개의 데이터 흐름 태스크가 있는 샘플 패키지를 살펴 봅니다. 각 데이터 흐름 태스크에 10개의 원본에서 대상으로의 실행 트리가 포함되어 있을 때 각 데이터 흐름 태스크에서 EngineThreads를 10으로 설정하면 30개의 실행 트리가 모두 동시에 실행될 수 있습니다.  
  
> [!NOTE]  
>  스레딩에 대한 설명은 이 항목의 범위를 벗어납니다. 그러나 사용 가능한 프로세서 수보다 많은 스레드를 병렬로 실행하지 않는 것이 일반적인 규칙입니다. 사용 가능한 프로세서 수보다 많은 스레드를 실행하면 스레드 간 컨텍스트 전환이 빈번하게 발생하므로 성능이 저하될 수 있습니다.  
  
## <a name="configuring-individual-data-flow-components"></a>개별 데이터 흐름 구성 요소 구성  
 성능 향상을 위해 개별 데이터 흐름 구성 요소를 구성하려면 몇 가지 일반적인 지침을 따라야 합니다. 데이터 흐름 구성 요소의 각 유형(원본, 변환 및 대상)과 관련된 지침도 있습니다.  
  
### <a name="general-guidelines"></a>일반적인 지침  
 데이터 흐름 구성 요소와 상관없이 성능 향상을 위해서는 쿼리를 최적화하고 불필요한 정렬을 사용하지 않는다는 두 가지 일반적인 지침을 따라야 합니다.  
  
#### <a name="optimize-queries"></a>쿼리 최적화  
 많은 데이터 흐름 구성 요소가 원본에서 데이터를 추출할 때나 참조 테이블을 만들기 위해 조회 작업에서 쿼리를 사용합니다. 기본 쿼리는 SELECT * FROM \<tableName> 구문을 사용합니다. 이 유형의 쿼리는 원본 테이블의 모든 열을 반환합니다. 디자인 타임에 모든 열을 사용할 수 있도록 만들면 모든 열을 조회, 통과 또는 원본 열로 선택할 수 있습니다. 그러나 사용할 열을 선택한 후에는 선택한 열만 포함되도록 쿼리를 수정해야 합니다. 열 수가 적을수록 더 작은 행이 만들어지므로 여분의 열을 제거하면 패키지의 데이터 흐름이 보다 효율적으로 개선됩니다. 행이 작을수록 하나의 버퍼에 더 많은 행을 넣을 수 있으며 데이터 집합의 모든 행을 보다 적은 작업으로 처리할 수 있습니다.  
  
 쿼리를 생성하려면 쿼리를 직접 입력하거나 쿼리 작성기를 사용합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 실행하면 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 진행률 탭에 경고가 나열됩니다. 이러한 경고에는 원본에서 데이터 흐름에 제공되지만 나중에 다운스트림 데이터 흐름 구성 요소에 사용되지 않는 데이터 열이 식별되어 포함됩니다. **RunInOptimizedMode** 속성을 사용하여 이러한 열을 자동으로 제거할 수 있습니다.  
  
#### <a name="avoid-unnecessary-sorting"></a>불필요한 정렬 방지  
 정렬은 근본적으로 느린 작업이므로 불필요한 정렬을 방지하면 패키지 데이터 흐름의 성능을 향상시킬 수 있습니다.  
  
 원본 데이터가 다운스트림 구성 요소에 의해 사용되기 전에 이미 정렬되어 있는 경우가 있습니다. SELECT 쿼리에 ORDER BY 절이 사용되거나 데이터가 원본에 정렬된 순서대로 삽입되면 이러한 사전 정렬이 발생할 수 있습니다. 이렇게 사전 정렬된 원본 데이터의 경우 데이터가 정렬되어 있음을 나타내는 힌트를 제공하여 특정 다운스트림 변환의 정렬 요구 사항을 만족시키기 위해 정렬 변환을 사용하는 것을 방지할 수 있습니다. 예를 들어 병합 및 병합 조인 변환에는 정렬된 입력이 필요합니다. 데이터가 정렬되어 있음을 나타내는 힌트를 제공하려면 다음 태스크를 수행해야 합니다.  
  
-   업스트림 데이터 흐름 구성 요소의 출력에 있는 **IsSorted** 속성을 **True**로 설정합니다.  
  
-   데이터가 정렬되는 정렬 키 열을 지정합니다.  
  
 자세한 내용은 [병합 및 병합 조인 변환을 위한 데이터 정렬](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)을 참조하세요.  
  
 데이터 흐름에서 데이터를 정렬해야 하는 경우 정렬 연산을 가능한 한 적게 사용하도록 데이터 흐름을 디자인하여 성능을 향상시킬 수 있습니다. 예를 들어 데이터 흐름에서 멀티캐스트 변환을 사용하여 데이터 집합을 복사합니다. 변환 후 여러 출력을 정렬하는 대신 멀티캐스트 변환을 실행하기 전에 데이터 집합을 한 번 정렬합니다.  
  
 자세한 내용은 [Sort Transformation](../../integration-services/data-flow/transformations/sort-transformation.md), [Merge Transformation](../../integration-services/data-flow/transformations/merge-transformation.md), [Merge Join Transformation](../../integration-services/data-flow/transformations/merge-join-transformation.md)및 [Multicast Transformation](../../integration-services/data-flow/transformations/multicast-transformation.md)를 참조하세요.  
  
### <a name="sources"></a>원본  
  
#### <a name="ole-db-source"></a>OLE DB 원본  
 OLE DB 원본을 사용하여 뷰에서 데이터를 검색할 때는 "SQL 명령"을 데이터 액세스 모드로 선택하고 SELECT 문을 입력합니다. SELECT 문을 사용하여 데이터에 액세스하면 "테이블 또는 뷰"를 데이터 액세스 모드로 선택하는 것보다 성능이 향상됩니다.  
  
### <a name="transformations"></a>변환  
 집계, 유사 항목 조회, 유사 항목 그룹화, 조회, 병합 조인 및 느린 변경 차원 변환의 성능을 향상시키려면 이 섹션의 제안 사항을 사용합니다.  
  
#### <a name="aggregate-transformation"></a>집계 변환  
 집계 변환에는 **Keys**, **KeysScale**, **CountDistinctKeys**및 **CountDistinctScale** 속성이 포함됩니다. 이 속성은 변환이 캐시하는 데이터에 필요한 메모리 양을 미리 할당할 수 있도록 하여 성능을 향상시킵니다. **Group by** 연산의 결과로 반환될 그룹의 정확한 수 또는 대략적인 수를 아는 경우 각각 **Keys** 및 **KeysScale** 속성을 설정합니다. **고유 카운트** 연산의 결과로 반환될 고유 값의 정확한 수 또는 대략적인 수를 아는 경우 각각 **CountDistinctKeys** 및 **CountDistinctScale** 속성을 설정합니다.  
  
 한 데이터 흐름에 여러 집계를 만들어야 하는 경우 여러 변환을 만드는 대신 하나의 집계 변환을 사용하는 여러 집계를 만드십시오. 이 방법을 사용하면 한 집계가 다른 집계의 하위 집합인 경우 성능이 향상됩니다. 이는 변환이 한 번만 들어오는 데이터를 검색하고 내부 저장소를 최적화할 수 있기 때문입니다. 예를 들어 집계에서 GROUP BY 절 및 AVG 집계를 사용하는 경우 이를 하나의 변환으로 조합하면 성능을 향상시킬 수 있습니다. 그러나 하나의 집계 변환 내에서 여러 집계를 수행하면 집계 작업이 직렬화되므로 여러 집계가 독립적으로 계산되어야 하는 경우 성능이 향상되지 않을 수 있습니다.  
  
#### <a name="fuzzy-lookup-and-fuzzy-grouping-transformations"></a>유사 항목 조회 및 유사 항목 그룹화 변환  
 유사 항목 조회 및 유사 항목 그룹화 변환의 성능 최적화에 대한 자세한 내용은 백서 [SQL Server 2005 데이터 변환 서비스의 퍼지 조회 및 퍼지 그룹화](http://go.microsoft.com/fwlink/?LinkId=96604)를 참조하십시오.  
  
#### <a name="lookup-transformation"></a>조회 변환  
 필요한 열만 조회하는 SELECT 문을 입력하여 메모리에서 참조 데이터의 크기를 최소화합니다. 이 옵션은 불필요한 데이터를 대량 반환하는 전체 테이블 또는 뷰 선택 작업보다 성능을 향상시킵니다.  
  
#### <a name="merge-join-transformation"></a>Merge Join Transformation  
 병합 조인 변환에서 과도한 메모리를 사용할 위험을 줄이기 위해 Microsoft에서 필요한 변경을 수행했기 때문에 더 이상 **MaxBuffersPerInput** 속성 값을 구성할 필요가 없습니다. 과도한 메모리가 사용되는 문제는 여러 병합 조인 입력에서 균일하지 않은 속도로 데이터를 생성하는 경우에 발생합니다.  
  
#### <a name="slowly-changing-dimension-transformation"></a>느린 변경 차원 변환  
 느린 변경 차원 마법사 및 느린 변경 차원 변형은 사용자 대부분의 요구를 충족하는 일반적인 용도의 도구입니다. 그러나 마법사에서 생성하는 데이터 흐름은 성능을 위해 최적화되지 않습니다.  
  
 일반적으로 느린 변경 차원 변환에서 가장 느린 구성 요소는 한 번에 하나의 행에 대해 UPDATE를 수행하는 OLE DB 명령 변환입니다. 따라서 느린 변경 차원 변환의 성능을 향상시키는 가장 효과적인 방법은 OLE DB 명령 변환을 바꾸는 것입니다. 업데이트할 모든 행을 준비 테이블에 저장하는 대상 구성 요소로 이러한 변환을 바꿀 수 있습니다. 그런 다음 모든 행에 대해 동시에 단일 집합 기반 Transact-SQL UPDATE를 수행하는 SQL 실행 태스크를 추가할 수 있습니다.  
  
 고급 사용자는 느린 변경 차원 처리를 위해 대규모 차원에 대해 최적화된 사용자 지정 데이터 흐름을 디자인할 수 있습니다. 이 방법에 대한 설명 및 예는 백서 [Project REAL: 비즈니스 인텔리전스 ETL 디자인 방법](http://go.microsoft.com/fwlink/?LinkId=96602)의 "고유 차원 시나리오" 섹션을 참조하십시오.  
  
### <a name="destinations"></a>대상  
 대상에서 성능을 향상시키려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상을 사용하고 대상의 성능을 테스트하십시오.  
  
#### <a name="sql-server-destination"></a>SQL Server 대상  
 패키지가 같은 컴퓨터에 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 데이터를 로드하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대상을 사용합니다. 이 대상은 고속 대량 로드를 위해 최적화되어 있습니다.  
  
#### <a name="testing-the-performance-of-destinations"></a>대상 성능 테스트  
 대상에 데이터를 저장하는 데는 예상보다 많은 시간이 소모됩니다. 대상의 낮은 데이터 처리 능력으로 인해 속도 저하가 일어났는지 여부를 식별하려면 임시로 대상을 행 개수 변환으로 대체하십시오. 처리량이 크게 향상되면 데이터를 로드하는 대상에서 속도 저하가 일어난 것입니다.  
  
### <a name="review-the-information-on-the-progress-tab"></a>진행률 탭의 정보 검토  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 실행할 때 제어 흐름과 데이터 흐름 모두에 대한 정보를 제공합니다. **진행률** 탭에는 태스크와 컨테이너가 실행 순서대로 나열되며 패키지 자체를 포함하여 각 태스크 및 컨테이너에 대한 시작 및 종료 시간, 경고 및 오류 메시지가 표시됩니다. 또한 데이터 흐름 구성 요소가 실행 순서대로 표시되고, 진행률(완료율로 표시)과 처리된 행 개수에 대한 정보가 포함됩니다.  
  
 **진행률** 탭에 메시지를 표시할지 여부는 **SSIS** 메뉴의 **디버그 진행률 보고** 옵션을 선택 또는 선택 취소하여 설정합니다. 진행률 보고를 사용하지 않으면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 복잡한 패키지를 실행하는 동안 성능을 높일 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [병합 및 병합 조인 변환을 위한 데이터 정렬](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>관련 내용  
 **기사와 블로그 게시물**  
  
-   technet.microsoft.com의 기술 문서 [SQL Server 2005 Integration Services: 성능에 대한 전략](http://go.microsoft.com/fwlink/?LinkId=98899)  
  
-   technet.microsoft.com의 기술 문서 [Integration Services: 성능 튜닝 기술](http://go.microsoft.com/fwlink/?LinkId=98900)  
  
-   sqlcat.com의 기술 문서 - [동기 변환을 여러 태스크로 분할하여 파이프라인의 처리량 증가](http://sqlcat.com/technicalnotes/archive/2010/08/18/increasing-throughput-of-pipelines-by-splitting-synchronous-transformations-into-multiple-tasks.aspx)  
  
-   msdn.microsoft.com의 기술 문서 - [데이터 로드 성능 가이드](http://go.microsoft.com/fwlink/?LinkId=220816)  
  
-   msdn.microsoft.com의 기술 문서 - [SSIS를 사용하여 30분 이내에 1TB 로드](http://go.microsoft.com/fwlink/?LinkId=220817)  
  
-   sqlcat.com의 기술 문서 - [SQL Server Integration Services의 상위 10가지 모범 사례](http://go.microsoft.com/fwlink/?LinkId=220818)  
  
-   sqlcat.com의 기술 문서 및 예제 - [SSIS용 "Balanced Data Distributor"](http://go.microsoft.com/fwlink/?LinkId=220822)  
  
-   blogs.msdn.com의 블로그 게시물 - [SSIS 패키지 성능 문제 해결](http://go.microsoft.com/fwlink/?LinkId=238156)  
  
 **비디오**  
  
-   비디오 시리즈, [엔터프라이즈에서 SSIS 패키지의 성능 설계 및 조정(SQL 비디오 시리즈)](http://go.microsoft.com/fwlink/?LinkId=400878)  
  
-   technet.microsoft.com의 비디오, [엔터프라이즈에서 SSIS 패키지 데이터 흐름 튜닝(SQL Server 비디오)](http://technet.microsoft.com/sqlserver/ff686901.aspx)  
  
-   technet.microsoft.com의 비디오, [SSIS 데이터 흐름 버퍼 이해(SQL Server 비디오)](http://technet.microsoft.com/sqlserver/ff686905.aspx)  
  
-   channel9.msdn.com의 비디오 - [Microsoft SQL Server Integration Services 성능 디자인 패턴](http://go.microsoft.com/fwlink/?LinkID=233698&clcid=0x409)  
  
-   sqlcat.com의 프레젠테이션 - [Microsoft IT의 SQL Server 2008 SSIS 데이터 흐름 엔진 향상 기능 활용 방법](http://go.microsoft.com/fwlink/?LinkId=217660)  
  
-   technet.microsoft.com의 비디오 - [Balanced Data Distributor](http://go.microsoft.com/fwlink/?LinkID=226278&clcid=0x409)  
  
## <a name="see-also"></a>관련 항목:  
 [패키지 배포 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)   
 [패키지 실행 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
