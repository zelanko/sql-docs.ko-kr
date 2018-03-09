---
title: "PREDICT 문을 모니터링의 확장 이벤트 | Microsoft Docs"
titleSuffix: SQL Server
ms.custom: 
ms.date: 03/01/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 0e2847690a8d63753c9246995211d0705128f7ab
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="extended-events-for-monitoring-predict-statements"></a>PREDICT 문 모니터링에 대 한 확장된 이벤트

이 문서에서는 SQL Server에서 사용 하는 작업 모니터링 및 분석 하는 데 사용할 수 있는 제공 된 확장된 이벤트를 설명 [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) 를 SQL Server에서 실시간 점수 매기기를 수행 합니다.

실시간 점수 매기기 기계 학습 SQL Server에 저장 된 모델에서에서 점수를 생성 합니다. PREDICT 함수는 외부 런타임 R, Python, 특정 이진 형식을 사용 하 여 작성 된 모델만 등 필요 하지 않습니다. 자세한 내용은 참조 [실시간 점수 매기기](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring)합니다.

## <a name="prerequisites"></a>필수 구성 요소

확장된 이벤트 (XEvents 라고도 함) 및 세션에서 이벤트를 추적 하는 방법에 대 한 일반적인 내용은 다음이 문서를 참조 합니다.

+ [확장 이벤트 개념 및 아키텍처](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [SSMS에서 이벤트 캡처 설정](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [개체 탐색기에서 이벤트 세션 관리](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>확장된 이벤트 테이블

지 원하는 모든 버전의 SQL Server에서 사용할 수 있는 다음 확장 이벤트는 [T-SQL 예측](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) Linux 및 Azure SQL 데이터베이스에서 SQL Server를 포함 하 여 문입니다. 

예측 하는 T-SQL 문은 SQL Server 2017에서 도입 되었습니다. 

|name |object_type|description| 
|----|----|----|
|predict_function_completed |이벤트  |기본 제공 실행 시간 분석|
|predict_model_cache_hit |이벤트|모델 PREDICT 함수 모델 캐시에서 검색 될 때 발생 합니다. PREDICT 함수 모델 캐시에서 발생 한 문제를 해결 하려면 다른 predict_model_cache_ * 이벤트와 함께이 이벤트를 사용 합니다.|
|predict_model_cache_insert |이벤트  |   모델에 예측 함수 모델 캐시에 삽입 될 때 발생 합니다. PREDICT 함수 모델 캐시에서 발생 한 문제를 해결 하려면 다른 predict_model_cache_ * 이벤트와 함께이 이벤트를 사용 합니다.    |
|predict_model_cache_miss   |이벤트|모델은 예측 함수 모델 캐시에서 찾을 수 없을 때 발생 합니다. 이 이벤트가 자주 발생 SQL Server에 더 많은 메모리가 필요 함을 나타낼 수 있습니다. PREDICT 함수 모델 캐시에서 발생 한 문제를 해결 하려면 다른 predict_model_cache_ * 이벤트와 함께이 이벤트를 사용 합니다.|
|predict_model_cache_remove |이벤트| 모델은 예측 함수에 대 한 모델 캐시에서 제거 될 때 발생 합니다. PREDICT 함수 모델 캐시에서 발생 한 문제를 해결 하려면 다른 predict_model_cache_ * 이벤트와 함께이 이벤트를 사용 합니다.|

## <a name="query-for-related-events"></a>관련된 이벤트에 대 한 쿼리

이러한 이벤트에 대해 반환 되는 모든 열의 목록을 보려면 SQL Server Management Studio에서 다음 쿼리를 실행 합니다.

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>예

예측을 사용 하 여 점수 매기기 세션 성능에 대 한 정보를 캡처하려면:

1. 확장 이벤트 세션을 지원 되는 다른 또는 Management Studio를 사용 하 여 새로 만들 [도구](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)합니다.
2. 이벤트 추가 `predict_function_completed` 및 `predict_model_cache_hit` 세션입니다.
3. 확장된 이벤트 세션을 시작 합니다.
4. 예측을 사용 하는 쿼리를 실행 합니다.

결과에서 이러한 열을 검토 합니다.

+ 에 대 한 값 `predict_function_completed` 표시 된 시간에 모델을 로드 및 평가 하는 데 걸린 쿼리 합니다.
+ 에 대 한 부울 값 `predict_model_cache_hit` 쿼리에 캐시 된 모델을 사용할지 여부를 나타냅니다. 

### <a name="native-scoring-model-cache"></a>기본 점수 매기기 모델 캐시

예측할 특정 이벤트 외에도 캐시 된 모델 및 캐시 사용에 대 한 자세한 정보를 보려면 다음 쿼리를 사용할 수 있습니다.

기본 점수 매기기 모델 캐시를 보려면:

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

모델 캐시에서 개체를 표시 합니다.

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

