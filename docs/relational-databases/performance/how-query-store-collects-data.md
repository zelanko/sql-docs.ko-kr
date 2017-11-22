---
title: "쿼리 저장소에서 데이터를 수집하는 방법 | Microsoft Docs"
ms.custom: 
ms.date: 09/13/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Query Store, data collection
ms.assetid: 8d5eec36-0013-480a-9c11-183e162e4c8e
caps.latest.revision: "10"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 72e1970bf68219376f3f2a9d16d03e133ec0832b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="how-query-store-collects-data"></a>쿼리 저장소에서 데이터를 수집하는 방법
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  쿼리 저장소는 쿼리 및 계획과 관련된 컴파일 및 런타임 정보를 지속적으로 수집하는 **비행 데이터 레코더** 로 작동합니다. 데이터와 관련된 쿼리는 내부 테이블에 유지되고 뷰 집합을 통해 사용자에게 표시됩니다.  
  
## <a name="views"></a>뷰  
 다음 다이어그램은 파란색 엔터티로 표시된 컴파일 시간 정보와 함께 쿼리 저장소 뷰와 논리적 관계를 보여 줍니다.  
  
 ![query-store-process-2views](../../relational-databases/performance/media/query-store-process-2views.png "query-store-process-2views")  
  
 **보기 설명**  
  
|보기|설명|  
|----------|-----------------|  
|**sys.query_store_query_text**|데이터베이스에 대해 실행되는 고유 쿼리 텍스트를 표시합니다. 쿼리 텍스트 전후의 주석 및 공백은 무시됩니다. 텍스트 내의 주석 및 공백은 무시되지 않습니다. 배치의 모든 문은 별도 쿼리 텍스트 항목을 생성합니다.|  
|**sys.query_context_settings**|실행되는 쿼리의 설정에 영향을 주는 계획의 고유 조합을 표시합니다. `context_settings_id` 은(는) 쿼리 키의 일부이므로 설정에 영향을 주는 다른 계획으로 실행되는 동일한 쿼리 텍스트는 쿼리 저장소에 별도 쿼리 항목을 생성합니다.|  
|**sys.query_store_query**|쿼리 저장소에서 개별적으로 추적되고 강제로 적용되는 쿼리 항목입니다. 다른 컨텍스트 설정에서 실행되거나 다른 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모듈(프로시저, 트리거 등이 저장됨)의 외부 및 내부에서 실행되는 경우 단일 쿼리 텍스트는 여러 쿼리 항목을 생성할 수 있습니다.|  
|**sys.query_store_plan**|컴파일 시간 통계로 쿼리에 대한 예상 계획을 표시합니다. 저장된 계획은 `SET SHOWPLAN_XML ON`을(를) 사용하여 얻을 수 있는 것과 동일합니다.|  
|**sys.query_store_runtime_stats_interval**|쿼리 저장소는 시간을 자동으로 생성된 시간 창(간격)으로 분할하고 실행된 모든 계획에 대한 해당 간격에 집계 통계를 저장합니다. 간격의 크기는 통계 수집 간격 구성 옵션([!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서) 또는 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 사용하여 `INTERVAL_LENGTH_MINUTES`에 의해 제어됩니다.|  
|**sys.query_store_runtime_stats**|실행된 계획에 대한 집계된 런타임 통계입니다. 모든 캡처된 메트릭은 4개의 통계 함수 형태인 평균, 최소값, 최대값 및 표준 편차로 표현됩니다.|  
  
 쿼리 저장소 뷰에 대한 자세한 내용은 **쿼리 저장소를 사용하여 성능 모니터링** 의 [관련된 뷰, 함수 및 프로시저](monitoring-performance-by-using-the-query-store.md)섹션을 참조하세요.  
  
## <a name="query-processing"></a>쿼리 처리  
 쿼리 저장소는 다음 주요 지점에서 쿼리 처리 파이프라인과 상호 작용합니다.  
  
1.  쿼리가 처음으로 컴파일될 때 쿼리 텍스트 및 초기 계획이 쿼리 저장소로 전송됩니다.  
  
2.  쿼리가 다시 컴파일될 때 계획이 쿼리 저장소에서 업데이트됩니다. 새 계획을 만든 경우 쿼리 저장소는 해당 실행 통계와 함께 이전 것을 유지하는 쿼리에 대한 새 계획 항목을 추가합니다.  
  
3.  쿼리 실행 시 런타임 통계는 쿼리 저장소에 전송됩니다. 쿼리 저장소는 현재 활성 간격 내에서 실행된 모든 계획에 대한 정확한 집계 통계를 유지합니다.  
  
4.  컴파일 및 재컴파일 단계에 대한 확인을 하는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은(는) 현재 실행 중인 쿼리에 대해 적용해야 하는 계획이 쿼리 저장소에 있는지 여부를 확인합니다. 강제 계획이 있고 프로시저 캐시의 계획이 강제 계획과 다른 경우 쿼리는 계획 힌트가 해당 쿼리에 적용됐던 것과 동일한 방식으로 효과적으로 다시 컴파일됩니다. 이 프로세스는 사용자 응용 프로그램에 투명하게 수행합니다.  
  
 다음 다이어그램은 위에서 설명한 통합 지점을 보여 줍니다.  
  
 ![query-store-process-2processor](../../relational-databases/performance/media/query-store-process-2processor.png "query-store-process-2processor")  
  
 I/O 오버헤드를 최소화하기 위해 새 데이터가 메모리 내에 캡처됩니다. 쓰기 작업은 지연되고 나중에 디스크에 플러시됩니다. 쿼리 및 계획 정보(아래 다이어그램의 계획 저장소)가 최소 대기 시간으로 플러시됩니다. 런타임 통계(Runtime Stats)가 `DATA_FLUSH_INTERVAL_SECONDS` 문의 `SET QUERY_STORE` 옵션을 사용하여 정의된 기간 동안 메모리에서 유지됩니다. SSMS 쿼리 저장소 대화 상자를 사용하여 **데이터 플러시 간격(분)**을 입력할 수 있으며 초 단위로 변환됩니다.  
  
 ![query-store-process-3plan](../../relational-databases/performance/media/query-store-process-3.png "query-store-process-3plan")  
  
 시스템 충돌이 발생할 경우 쿼리 저장소는 `DATA_FLUSH_INTERVAL_SECONDS`(으)로 정의된 양까지 런타임 데이터를 손실할 수 있습니다. 900초(15분)의 기본값은 쿼리 캡처 성능과 데이터 가용성 사이의 최적의 균형입니다.  
메모리 부족 시 런타임 통계는 `DATA_FLUSH_INTERVAL_SECONDS`(으)로 정의된 것보다 먼저 디스크에 플러시될 수 있습니다.  
쿼리 저장소 데이터를 읽는 동안 메모리 내 및 디스크의 데이터는 투명하게 통합됩니다.
세션 종료 또는 클라이언트 응용 프로그램 다시 시작/크래시의 경우 쿼리 통계는 기록되지 않습니다.  
  
 ![query-store-process-4planinfo](../../relational-databases/performance/media/query-store-process-4planinfo.png "query-store-process-4planinfo")    

  
## <a name="see-also"></a>관련 항목:  
 [관련된 뷰, 함수 및 프로시저](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [쿼리 저장소에 대한 모범 사례](../../relational-databases/performance/best-practice-with-the-query-store.md)   
 [쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)  
  
  
