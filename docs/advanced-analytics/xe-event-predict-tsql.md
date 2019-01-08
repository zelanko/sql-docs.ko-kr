---
title: PREDICT 문-SQL Server Machine Learning Services를 모니터링 하는 것에 대 한 확장된 이벤트
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e680da7485069e6838edff260a505461a22c472b
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432246"
---
# <a name="extended-events-for-monitoring-predict-statements"></a>PREDICT 문 모니터링에 대한 확장 이벤트

이 문서에서는 SQL Server에서 사용 하는 작업 모니터링 및 분석에 사용할 수 있는 제공 된 확장된 이벤트를 설명 [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) 에 SQL Server의 실시간 점수 매기기를 수행 합니다.

실시간 점수 매기기 기계 학습 모델을 SQL Server에 저장 된에서 점수를 생성 합니다. PREDICT 함수는 특정 이진 형식을 사용 하 여 작성 된 모델을 Python 또는 R 등의 외부 실행 시간이 필요 하지 않습니다. 자세한 내용은 [실시간 점수 매기기](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring)합니다.

## <a name="prerequisites"></a>사전 요구 사항

확장된 이벤트 (XEvents 라고도 함) 및 세션에서 이벤트를 추적 하는 방법에 대 한 일반적인 내용은 다음이 문서를 참조 합니다.

+ [확장 이벤트 개념 및 아키텍처](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [SSMS에서 이벤트 캡처 설정](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [개체 탐색기에서 이벤트 세션 관리](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>확장된 이벤트 테이블

지 원하는 모든 버전의 SQL Server에서 사용할 수 있는 다음 확장 이벤트는 [T-SQL 예측](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) Linux 및 Azure SQL Database에서 SQL Server를 포함 하 여 문을 합니다. 

예측 하는 T-SQL 문은 SQL Server 2017에서 도입 되었습니다. 

|NAME |object_type|description| 
|----|----|----|
|predict_function_completed |이벤트  |기본 제공 실행 시간 중단점|
|predict_model_cache_hit |이벤트|모델을 PREDICT 함수 모델 캐시에서 검색 될 때 발생 합니다. PREDICT 함수 모델 캐시에서 발생 하는 문제를 해결 하려면 다른 predict_model_cache_ * 이벤트와 함께이 이벤트를 사용 합니다.|
|predict_model_cache_insert |이벤트  |   모델이 PREDICT 함수 모델 캐시에 삽입 될 때 발생 합니다. PREDICT 함수 모델 캐시에서 발생 하는 문제를 해결 하려면 다른 predict_model_cache_ * 이벤트와 함께이 이벤트를 사용 합니다.    |
|predict_model_cache_miss   |이벤트|모델을 PREDICT 함수 모델 캐시에서 찾을 수 없으면 발생 합니다. 이 이벤트가 자주 발생 SQL Server 메모리가 부족을 나타낼 수 있습니다. PREDICT 함수 모델 캐시에서 발생 하는 문제를 해결 하려면 다른 predict_model_cache_ * 이벤트와 함께이 이벤트를 사용 합니다.|
|predict_model_cache_remove |이벤트| PREDICT 함수 모델 캐시에서 모델이 제거 될 때 발생 합니다. PREDICT 함수 모델 캐시에서 발생 하는 문제를 해결 하려면 다른 predict_model_cache_ * 이벤트와 함께이 이벤트를 사용 합니다.|

## <a name="query-for-related-events"></a>관련된 이벤트에 대 한 쿼리

이러한 이벤트에 대 한 반환 된 모든 열의 목록을 보려면 SQL Server Management Studio에서 다음 쿼리를 실행 합니다.

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>예

예측을 사용 하 여 점수 매기기 세션의 성능에 대 한 정보를 캡처하려면:

1. 확장 이벤트 세션을 지원 되는 다른 또는 Management Studio를 사용 하 여 새로 만듭니다 [도구](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)합니다.
2. 이벤트를 추가 `predict_function_completed` 고 `predict_model_cache_hit` 세션입니다.
3. 확장된 이벤트 세션을 시작 합니다.
4. 예측을 사용 하는 쿼리를 실행 합니다.

결과에서 이러한 열을 검토 합니다.

+ 값 `predict_function_completed` 에서는 모델을 로드 하 고 점수 매기기에 소요 되는 쿼리를 얼마나 시간입니다.
+ 부울 값을 `predict_model_cache_hit` 쿼리 캐시 된 모델을 사용할지 여부를 나타냅니다. 

### <a name="native-scoring-model-cache"></a>네이티브 점수 매기기 모델 캐시

예측할 특정 이벤트 외에도 캐시 된 모델 및 캐시 사용에 대 한 자세한 정보를 보려면 다음 쿼리를 사용할 수 있습니다.

네이티브 점수 매기기 모델 캐시를 보려면:

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

모델 캐시에서 개체를 보려면:

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

