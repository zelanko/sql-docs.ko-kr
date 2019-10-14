---
title: 쿼리 저장소에서 데이터를 수집하는 방법 | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, data collection
ms.assetid: 8d5eec36-0013-480a-9c11-183e162e4c8e
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f60ded18e88d57c5a2975b567fa246923ece7ebe
ms.sourcegitcommit: f6bfe4a0647ce7efebaca11d95412d6a9a92cd98
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2019
ms.locfileid: "71974356"
---
# <a name="how-query-store-collects-data"></a>쿼리 저장소에서 데이터를 수집하는 방법
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SQL Server 쿼리 저장소는 플라이트 데이터 레코더처럼 작동하여, 쿼리 및 계획과 관련된 컴파일 및 런타임 정보를 지속적으로 수집합니다. 데이터와 관련된 쿼리는 내부 테이블에 유지되고 뷰 집합을 통해 사용자에게 표시됩니다.
  
## <a name="views"></a>뷰 
 다음 다이어그램은 파란색 엔터티로 표시된 컴파일 시간 정보와 함께 쿼리 저장소 뷰와 논리적 관계를 보여 줍니다.
  
 ![쿼리 저장소 프로세스 뷰](../../relational-databases/performance/media/query-store-process-2views.png "query-store-process-2views")  
**뷰 설명**  
  
|보기|설명|  
|----------|-----------------|  
|**sys.query_store_query_text**|데이터베이스에 대해 실행되는 고유 쿼리 텍스트를 표시합니다. 쿼리 텍스트 전후의 주석 및 공백은 무시됩니다. 텍스트 내의 주석 및 공백은 무시되지 않습니다. 배치의 모든 문은 별도 쿼리 텍스트 항목을 생성합니다.|  
|**sys.query_context_settings**|쿼리 실행에 사용되는 계획 관련 설정의 고유한 조합을 표시합니다. `context_settings_id`는 쿼리 키의 일부이므로, 다른 계획 관련 설정으로 동일한 쿼리 텍스트를 실행할 경우 쿼리 저장소에 별도의 쿼리 항목이 생성됩니다.|  
|**sys.query_store_query**|쿼리 저장소에서 개별적으로 추적되고 강제로 적용되는 쿼리 항목입니다. 다른 컨텍스트 설정에서 실행되거나 저장 프로시저, 트리거 등의 다른 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈 외부 및 내부에서 실행되는 경우 단일 쿼리 텍스트는 여러 쿼리 항목을 생성할 수 있습니다.|  
|**sys.query_store_plan**|컴파일 시간 통계로 쿼리에 대한 예상 계획을 표시합니다. 저장된 계획은 `SET SHOWPLAN_XML ON`을 사용하여 가져오는 계획과 동일합니다.|  
|**sys.query_store_runtime_stats_interval**|쿼리 저장소는 시간을 자동으로 생성된 시간 창(간격)으로 분할하고 실행된 모든 계획에 대한 해당 간격에 집계 통계를 저장합니다. 간격 크기는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 **통계 수집 간격** 구성 옵션 또는 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 사용하여 `INTERVAL_LENGTH_MINUTES`를 통해 제어됩니다.|  
|**sys.query_store_runtime_stats**|실행된 계획에 대한 집계된 런타임 통계입니다. 캡처된 모든 메트릭은 다음 4가지 통계 함수 형태로 표시됩니다. 평균, 최댓값, 최솟값 및 표준 편차.|  
  
 쿼리 저장소 뷰에 대한 자세한 내용은 [쿼리 저장소를 사용하여 성능 모니터링](monitoring-performance-by-using-the-query-store.md)의 “관련된 뷰, 함수 및 프로시저” 섹션을 참조하세요. 
  
## <a name="query-processing"></a>쿼리 처리
 쿼리 저장소는 다음 주요 지점에서 쿼리 처리 파이프라인과 상호 작용합니다.
  
1.  쿼리가 처음으로 컴파일될 때 쿼리 텍스트 및 초기 계획이 쿼리 저장소로 전송됩니다.
  
2.  쿼리가 다시 컴파일될 때 계획이 쿼리 저장소에서 업데이트됩니다. 새 계획이 생성되면, 쿼리 저장소는 쿼리에 대한 새 계획 항목을 추가하고 이전 계획을 해당 실행 통계와 함께 유지합니다.
  
3.  쿼리 실행 시 런타임 통계가 쿼리 저장소로 전송됩니다. 쿼리 저장소는 현재 활성 간격 내에서 실행된 모든 계획에 대한 정확한 집계 통계를 유지합니다. 
  
4.  컴파일 및 재컴파일 확인 단계에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 현재 실행 중인 쿼리에 대해 적용해야 하는 계획이 쿼리 저장소에 있는지 확인합니다. 강제 계획이 있고, 프로시저 캐시의 계획이 강제 계획과 다르면 쿼리가 다시 컴파일됩니다. PLAN HINT가 해당 쿼리에 적용된 것과 동일한 방식으로 작동합니다. 이 프로세스는 사용자 애플리케이션에 투명하게 수행합니다. 
  
 다음 다이어그램은 이전 단계에서 설명한 통합 지점을 보여 줍니다.
  
 ![쿼리 저장소 프로세스](../../relational-databases/performance/media/query-store-process-2processor.png "query-store-process-2processor") 

## <a name="remarks"></a>Remarks
 I/O 오버헤드를 최소화하기 위해 새 데이터가 메모리 내에 캡처됩니다. 쓰기 작업은 지연되고 나중에 디스크에 플러시됩니다. 다음 다이어그램에 계획 저장소로 표시된 쿼리 및 계획 정보는 최소 대기 시간으로 플러시됩니다. Runtime Stats로 표시된 런타임 통계가 `SET QUERY_STORE` 문의 `DATA_FLUSH_INTERVAL_SECONDS` 옵션을 사용하여 정의된 기간 동안 메모리에 유지됩니다. [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 쿼리 저장소 대화 상자를 사용하여 **데이터 플러시 간격(분)** 의 값을 입력할 수 있으며, 내부적으로 초 단위로 변환됩니다. 
  
 ![쿼리 저장소 프로세스 계획](../../relational-databases/performance/media/query-store-process-3.png "query-store-process-3plan") 
  
 [추적 플래그 7745](../../relational-databases/performance/best-practice-with-the-query-store.md#Recovery)를 사용하는 동안 시스템이 충돌하거나 종료되면 쿼리 저장소에서 수집되었지만 아직 유지되지 않은 런타임 데이터가 `DATA_FLUSH_INTERVAL_SECONDS`로 정의된 기간까지 손실될 수 있습니다. 쿼리 캡처 성능과 데이터 가용성 간의 균형을 위해 기본값 900초(15분)를 사용하는 것이 좋습니다.
 
 > [!IMPORTANT] 
 > **최대 크기(MB)** 한도는 엄격하게 적용되지 않습니다. 쿼리 저장소가 디스크에 데이터를 쓰는 경우에만 스토리지 크기가 확인됩니다. 이 간격은 **데이터 플러시 간격** 값으로 설정됩니다. 쿼리 저장소가 스토리지 크기 검사 간에 최대 크기 한도를 위반할 경우 읽기 전용 모드로 전환됩니다. **크기 기반 정리 모드**를 사용하도록 설정하면, 최대 크기 한도를 적용하는 정리 메커니즘도 트리거됩니다.
 
 > [!NOTE]
 > 메모리 부족 시 런타임 통계는 `DATA_FLUSH_INTERVAL_SECONDS`로 정의된 것보다 먼저 디스크에 플러시될 수 있습니다.
 
 쿼리 저장소 데이터를 읽는 동안 메모리 내 데이터와 디스크의 데이터는 투명하게 통합됩니다. 
 
 세션이 종료되거나 클라이언트 애플리케이션이 다시 시작 또는 충돌하면 쿼리 통계가 기록되지 않습니다. 
  
 ![쿼리 저장소 프로세스 계획 정보](../../relational-databases/performance/media/query-store-process-4planinfo.png "query-store-process-4planinfo")    

## <a name="see-also"></a>관련 항목:
 [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [쿼리 저장소에 대한 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md)  
 [쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md) 
  
  
