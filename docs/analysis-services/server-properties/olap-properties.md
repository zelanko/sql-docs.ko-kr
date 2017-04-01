---
title: "OLAP 속성 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "AggregationPerfLog 속성"
  - "DefaultPageSizeForProp 속성"
  - "UseSinglePassForDimSecurityAutoExist 속성"
  - "DeepCompressValue 속성"
  - "CacheRowsetRows 속성"
  - "Income 속성"
  - "AggregationNewAlgo 속성"
  - "MemoryAdjustFactor 속성"
  - "DimensionLatencyAccuracy 속성"
  - "InitialBonus 속성"
  - "DefaultPageSizeForDataHeader 속성"
  - "MaxCPUUsage 속성"
  - "DistinctBuffer 속성"
  - "PartitionLatencyAccuracy 속성"
  - "MaxRetries 속성"
  - "UseDataCacheRegistryMultiplyKey 속성"
  - "ConvertDeletedToUnknown 속성"
  - "DatabaseConnectionPoolMax 속성"
  - "DataFileInitEnabled 속성"
  - "DefaultPageSizeForHash 속성"
  - "MaxRolapOrConditions 속성"
  - "UseDataCacheFreeLastPageMemory 속성"
  - "OLAP [Analysis Services], 속성"
  - "MapHandleAlgorithm 속성"
  - "IndexBuildEnabled 속성"
  - "MaxObjectsInParallel 속성"
  - "IgnoreNullRolapRows 속성"
  - "DimensionPropertyCacheSize 속성"
  - "DefaultRefreshInterval 속성"
  - "CheckDistinctRecordSortOrder 속성"
  - "BufferMemoryLimit 속성"
  - "EnableTableGrouping 속성"
  - "ExpressNonEmptyUseEnabled 속성"
  - "CopyLinkedDataCacheAndRegistry 속성"
  - "UseDataSlice 속성"
  - "MemoryLimitErrorEnabled 속성"
  - "Enabled 속성"
  - "EnableRolapOptimization 속성"
  - "DatabaseConnectionPoolTimeout 속성"
  - "UseDataCacheRegistryHashTable 속성"
  - "AggregationsBuildEnabled 속성"
  - "Tax 속성"
  - "DatabaseConnectionPoolGeneralTimeout 속성"
  - "DefaultPageSizeForString 속성"
  - "DatabaseConnectionPoolConnectTimeout 속성"
  - "MinimumBalance 속성"
  - "OptimizeSchema 속성"
  - "UseCalculationCacheRegistry 속성"
  - "MaxTableDepth 속성"
  - "DataSliceInitEnabled 속성"
  - "PrefetchLowerGranularities 속성"
  - "UseVBANet 속성"
  - "BufferRecordLimit 속성"
  - "DefaultPageSizeForIndexHeader 속성"
  - "MaximumBalance 속성"
  - "CalculationCacheRegistryMaxIterations 속성"
  - "DefaultDrillthroughMaxRows 속성"
  - "IndexBuildThreshold 속성"
  - "UseDataCacheRegistry 속성"
  - "MemoryAdjustConst 속성"
  - "ApplyIntersect 속성"
  - "IndexFileInitEnabled 속성"
  - "CacheRowsetToDisk 속성"
  - "DataCacheRegistryMaxIterations 속성"
  - "AllowSEFiltering 속성"
  - "ForceMultiPass 속성"
  - "ApplySubtract 속성"
  - "IndexUseEnabled 속성"
  - "AggregationsUseEnabled 속성"
  - "DataPlacementOptimization 속성"
  - "UseMaterializedIterators 속성"
  - "CacheRecordLimit 속성"
  - "ROLAPDimensionProcessingEffort 속성"
  - "DefaultPageSizeForIndex 속성"
  - "EnableRolapDimQueryTableGrouping 속성"
  - "DimensionPropertyKeyCache 속성"
  - "SleepIntervalSecs 속성"
  - "DefaultPageSizeForData 속성"
  - "MapFormatMask 속성"
  - "CalculationEvaluationPolicy 속성"
  - "AggregationMemoryLimitMin 속성"
  - "RecordsReportGranularity 속성"
  - "MemoryLimit 속성"
  - "AggregationMemoryLimitMax 속성"
ms.assetid: 06eb0d78-96c0-42ff-b759-f4c794597c8d
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 18
---
# OLAP 속성
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 다음 표에 나열된 OLAP 서버 속성을 지원합니다. 추가 서버 속성 및 해당 속성 설정 방법에 대한 자세한 내용은 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)을 참조하세요.  
  
 **적용 대상:** 다차원 서버 모드에만  
  
## 메모리  
 **DefaultPageSizeForData**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DefaultPageSizeForDataHeader**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DefaultPageSizeForIndex**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DefaultPageSizeForIndexHeader**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DefaultPageSizeForString**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DefaultPageSizeForHash**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DefaultPageSizeForProp**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## LazyProcessing  
 **설정**  
 지연 집계 처리가 설정되어 있는지 여부를 지정하는 부울 속성입니다.  
  
 **SleepIntervalSecs**  
 보류 중인 지연 처리 작업이 있는지 여부를 서버에서 검사하는 간격(초)을 정의하는 부호 있는 32비트 정수 속성입니다.  
  
 **MaxCPUUsage**  
 백분율로 표시된 지연 처리에 대한 최대 CPU 사용량을 정의하는 부호 있는 64비트 배정밀도 부동 소수점 수 속성입니다. 서버는 스냅숏에 따라 평균 CPU 사용을 모니터링합니다. CPU 사용이 이 임계값 이상으로 가끔 치솟는 것은 정상적인 동작입니다.  
  
 이 속성의 기본값은 0.5로 CPU의 최대 50%가 지연 처리에 할당되어 있음을 나타냅니다.  
  
 **MaxObjectsInParallel**  
 병렬 방식으로 지연 처리될 수 있는 최대 파티션 수를 지정하는 부호 있는 32비트 정수 속성입니다.  
  
 **MaxRetries**  
 오류 발생 전에 지연 처리가 실패하는 경우의 재시도 횟수를 정의하는 부호 있는 32비트 정수 속성입니다.  
  
## ProcessPlan  
 **CacheRowsetRows**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **CacheRowsetToDisk**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DistinctBuffer**  
 고유 카운트에 사용되는 내부 버퍼 크기를 정의하는 부호 있는 32비트 정수 속성입니다. 메모리를 사용하는 대신 고유 카운트 처리 속도를 높이려면 이 값을 늘리십시오.  
  
 **EnableRolapDimQueryTableGrouping**  
 테이블 그룹화가 ROLAP 차원에 대해 설정되어 있는지 여부를 지정하는 부울 속성입니다. True인 경우 런타임 시 ROLAP 차원을 쿼리할 때 각 특성에 대한 별개의 쿼리와는 반대로 전체 ROLAP 차원 테이블이 한 번에 쿼리됩니다.  
  
 **EnableTableGrouping**  
 테이블 그룹화가 설정되어 있는지 여부를 지정하는 부울 속성입니다. True인 경우 차원을 처리할 때 각 특성에 대한 별개의 쿼리와는 반대로 전체 차원 테이블이 한 번에 쿼리됩니다.  
  
 **ForceMultiPass**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MaxTableDepth**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MemoryAdjustConst**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MemoryAdjustFactor**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MemoryLimit**  
 실제 메모리의 백분율로 표시된 처리 전용으로 할당된 최대 메모리 양을 정의하는 부호 있는 64비트 배정밀도 부동 소수점 수 속성입니다.  
  
 이 속성에 대한 기본값은 65로 실제 메모리의 65%가 큐브 및 차원 처리 전용으로 지정됩니다.  
  
 **MemoryLimitErrorEnabled**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **OptimizeSchema**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## ProactiveCaching  
 **DefaultRefreshInterval**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DimensionLatencyAccuracy**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **PartitionLatencyAccuracy**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
##  처리   
 **AggregationMemoryLimitMax**  
 실제 메모리의 백분율로 표시된 집계 처리 전용으로 할당된 최대 메모리 양을 정의하는 부호 있는 64비트 배정밀도 부동 소수점 수 속성입니다.  
  
 이 속성에 대한 기본값은 80으로 실제 메모리의 80%가 집계 처리 전용으로 지정됩니다.  
  
 **AggregationMemoryLimitMin**  
 실제 메모리의 백분율로 표시된 집계 처리 전용으로 할당된 최소 메모리 양을 정의하는 부호 있는 64비트 배정밀도 부동 소수점 수 속성입니다. 값이 크면 메모리 사용이 높은 대신 집계 처리 속도가 향상됩니다.  
  
 이 속성에 대한 기본값은 10으로 실제 메모리의 최소 10%가 집계 처리 전용으로 지정됩니다.  
  
 **AggregationNewAlgo**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **AggregationPerfLog2**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **AggregationsBuildEnabled**  
 집계 구축이 설정되어 있는지 여부를 지정하는 부울 속성입니다. 이 속성은 집계 디자인을 변경하지 않고 집계 구축을 벤치마크하기 위한 메커니즘입니다.  
  
 **BufferMemoryLimit**  
 실제 메모리의 백분율로 표시된 처리 버퍼 메모리 한도를 정의하는 부호 있는 64비트 배정밀도 부동 소수점 수 속성입니다.  
  
 이 속성의 기본값은 60으로 실제 메모리의 최대 60%까지 버퍼 메모리에 사용할 수 있음을 나타냅니다.  
  
 **BufferRecordLimit**  
 처리 중에 버퍼될 수 있는 레코드 수를 정의하는 부호 있는 32비트 정수 속성입니다.  
  
 이 속성의 기본값은 1048576(레코드)입니다.  
  
 **CacheRecordLimit**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **CheckDistinctRecordSortOrder**  
 파티션을 처리할 때 고유 카운트 쿼리의 결과에 대한 정렬 순서가 중요한지 여부를 정의하는 부울 속성입니다. True는 정렬 순서가 중요하지 않고 서버에서 "검사"되어야 함을 나타냅니다. 고유 카운트 측정값이 있는 파티션을 처리할 때 ORDER BY가 포함된 쿼리가 SQL에 전송되었습니다. 처리 속도를 높이려면 False로 설정합니다.  
  
 이 속성의 기본값은 True로 정렬 순서가 중요하지 않고 검사되어야 함을 나타냅니다.  
  
 **DatabaseConnectionPoolConnectTimeout**  
 새 연결을 열 때의 제한 시간(초)을 지정하는 부호 있는 32비트 정수 속성입니다.  
  
 **DatabaseConnectionPoolGeneralTimeout**  
 외부 OLEDB 연결에 사용할 데이터베이스 연결 제한 시간(초)을 지정하는 부호 있는 32비트 정수 속성입니다.  
  
 **DatabaseConnectionPoolMax**  
 풀에 있는 최대 데이터베이스 연결 수를 지정하는 부호 있는 32비트 정수 속성입니다.  
  
 이 속성의 기본값은 50(연결)입니다.  
  
 **DatabaseConnectionPoolTimeout**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataFileInitEnabled**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataPlacementOptimization**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataSliceInitEnabled**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DeepCompressValue**  
 숫자가 압축되어 수치 정확도가 손실될 수 있는지 여부를 지정하는 Double 데이터 형식의 측정값에 적용되는 부울 속성입니다. False 값은 압축되지 않고 정확도가 손실되지 않음을 나타냅니다.  
  
 이 속성의 기본값은 True로 압축이 설정되어 있고 정확도가 손실될 수 있음을 나타냅니다.  
  
 **DimensionPropertyKeyCache**  
 차원 속성 키가 캐시되어 있는지 여부를 지정하는 부울 속성입니다. 키가 고유 키가 아닌 경우 True로 설정되어야 합니다.  
  
 **IndexBuildEnabled**  
 인덱스가 처리 중에 작성되는지 여부를 지정하는 부울 속성입니다. 이 속성은 벤치마킹 및 정보 제공 용도로 제공됩니다.  
  
 **IndexBuildThreshold**  
 파티션에 대해 인덱스가 작성되지 않는 행 개수 임계값을 지정하는 부호 있는 32비트 정수 속성입니다.  
  
 이 속성의 기본값은 4096(행)입니다.  
  
 **IndexFileInitEnabled**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MapFormatMask**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **RecordsReportGranularity**  
 서버에서 처리 중에 Trace 이벤트를 기록하는 간격(행)을 지정하는 부호 있는 32비트 정수 속성입니다.  
  
 이 속성의 기본값은 1000으로 Trace 이벤트가 1000행마다 기록됨을 나타냅니다.  
  
 **ROLAPDimensionProcessingEffort**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## Query  
 **AggregationsUseEnabled**  
 런타임에 저장 집계가 사용되는지 여부를 정의하는 부울 속성입니다. 이 속성을 사용하면 정보 제공 및 벤치마크 목적으로 집계 디자인을 변경하거나 다시 처리하지 않고 집계를 해제할 수 있습니다.  
  
 이 속성의 기본값은 True로 집계가 설정되어 있음을 나타냅니다.  
  
 **AllowSEFiltering**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **CalculationCacheRegistryMaxIterations**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **CalculationEvaluationPolicy**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ConvertDeletedToUnknown**  
 삭제된 차원 멤버가 Unknown 멤버로 변환되는지 여부를 지정하는 부울 속성입니다.  
  
 **CopyLinkedDataCacheAndRegistry**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCacheRegistryMaxIterations**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DefaultDrillthroughMaxRows**  
 드릴스루 쿼리로부터 반환할 최대 행 개수를 지정하는 부호 있는 32비트 정수 속성입니다.  
  
 이 속성의 기본값은 10000(행)입니다.  
  
 **DimensionPropertyCacheSize**  
 쿼리에서 사용된 차원 멤버를 캐시하는 데 사용되는 메모리 크기(바이트)를 지정하는 부호 있는 32비트 정수 속성입니다.  
  
 기본값은 활성 쿼리당, 특성 계층당 4,000,000바이트(4MB)입니다. 기본값은 일반 계층이 있는 솔루션을 위해 균형 잡힌 캐시 크기를 제공합니다. 그러나 이 값을 늘리면 멤버가 아주 많거나 계층 구조의 중첩이 많은 차원의 경우 성능이 더 낫습니다.  
  
 캐시 크기를 늘릴 경우 미치는 영향:  
  
-   차원 캐시에 추가 메모리가 사용되도록 허용하는 경우 메모리 사용 비용이 늘어납니다. 실제 사용량은 쿼리 실행에 따라 달라집니다. 일부 쿼리의 경우 최대 허용 크기를 사용하지 않습니다.  
  
     이러한 캐시에 사용되는 메모리는 축소 불가능한 것으로 간주되며 **TotalMemoryLimit**을 기준으로 고려할 때 포함됩니다.  
  
-   서버의 모든 데이터베이스에 영향을 줍니다. **DimensionPropertyCachesize**는 서버 차원의 속성입니다. 이 속성을 변경하면 현재 인스턴스에서 실행되는 모든 데이터베이스에 영향을 줍니다.  
  
 차원 캐시 요구 사항을 예측하는 방법:  
  
1.  차원 캐시 크기를 많이 늘리기 시작하여 이 크기를 늘릴 경우 얻을 수 있는 이점이 있는지 여부를 확인합니다. 예를 들어 초기 단계로 기본값을 두 배로 만들 수 있습니다.  
  
2.  성능 향상이 확실할 경우 성능과 메모리 사용률 간 균형 지점에 도달할 때까지 값을 증분 감소시키십시오.  
  
 **ExpressNonEmptyUseEnabled**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **IgnoreNullRolapRows**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **IndexUseEnabled**  
 런타임에 인덱스가 사용되는지 여부를 정의하는 부울 속성입니다. 이 속성은 정보 제공 및 벤치마킹 용도로 제공됩니다.  
  
 **MapHandleAlgorithm**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **MaxRolapOrConditions**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **UseCalculationCacheRegistry**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **UseDataCacheFreeLastPageMemory**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **UseDataCacheRegistry**  
 쿼리 결과가 캐시되는(계산 결과를 사용하지 않음) 데이터 캐시 레지스트리를 설정할지 여부를 지정하는 부울 속성입니다.  
  
 **UseDataCacheRegistryHashTable**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **UseDataCacheRegistryMultiplyKey**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **UseDataSlice**  
 쿼리 최적화를 위해 런타임 시 파티션 데이터 조각을 사용할지 여부를 정의하는 부울 속성입니다. 이 속성은 벤치마킹 및 정보 제공 용도로 제공됩니다.  
  
 **UseMaterializedIterators**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **UseSinglePassForDimSecurityAutoExist**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **UseVBANet**  
 사용자 정의 함수에 대해 VBA .NET 어셈블리를 사용할지 여부를 정의하는 부울 속성입니다.  
  
 **CalculationPrefetchLocality\ ApplyIntersect**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **CalculationPrefetchLocality\ ApplySubtract**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **CalculationPrefetchLocality\ PrefetchLowerGranularities**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\  CachedPageAlloc\ Income**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\  CachedPageAlloc\ InitialBonus**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\  CachedPageAlloc\ MaximumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\  CachedPageAlloc\ MinimumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\  CachedPageAlloc\ Tax**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\CellStore\ Income**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\CellStore\ InitialBonus**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\CellStore\ MaximumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\CellStore\ MinimumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\CellStore\ Tax**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\ MemoryModel \ Income**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\ MemoryModel \ InitialBonus**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\ MemoryModel \ MaximumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\ MemoryModel \ MinimumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **DataCache\ MemoryModel\ Tax**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## 작업  
 **ProcessAggregation\ MemoryModel\ Income**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ MemoryModel\ InitialBonus**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ MemoryModel\ MaximumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ MemoryModel\ MinimumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ MemoryModel\ Tax**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ ProcessPartition\ Income**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ ProcessPartition \ InitialBonus**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ ProcessPartition \ MaximumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ ProcessPartition \ MinimumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ ProcessPartition \ Tax**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ ProcessProperty\ Income**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ ProcessProperty\ InitialBonus**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ ProcessProperty\ MaximumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ ProcessProperty\ MinimumBalance**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
 **ProcessAggregation\ ProcessProperty\ Tax**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 지원 지침에 따라 변경하는 경우를 제외하고 고급 속성을 변경하면 안 됩니다.  
  
## 관련 항목:  
 [Analysis Services의 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Analysis Services 인스턴스의 서버 모드 확인](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  