---
title: PREDICT 문 모니터링에 대한 확장 이벤트
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1c534681200abf056c8bc7dd3745d8098d59c146
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345659"
---
# <a name="extended-events-for-monitoring-predict-statements"></a>PREDICT 문 모니터링에 대한 확장 이벤트

이 문서에서는 [예측](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) 을 사용 하 여 SQL Server에서 실시간 점수 매기기를 수행 하는 작업을 모니터링 및 분석 하는 데 사용할 수 있는 SQL Server에서 제공 하는 확장 이벤트에 대해 설명 합니다.

실시간 점수 매기기는 SQL Server에 저장 된 기계 학습 모델의 점수를 생성 합니다. PREDICT 함수에는 R 또는 Python과 같은 외부 실행 시간이 필요 하지 않으며 특정 이진 형식을 사용 하 여 만든 모델만 필요 합니다. 자세한 내용은 [실시간 점수 매기기](https://docs.microsoft.com/sql/advanced-analytics/real-time-scoring)를 참조 하세요.

## <a name="prerequisites"></a>사전 요구 사항

확장 이벤트 (Xevent 라고도 함) 및 세션에서 이벤트를 추적 하는 방법에 대 한 일반적인 정보는 다음 문서를 참조 하세요.

+ [확장 이벤트 개념 및 아키텍처](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [SSMS에서 이벤트 캡처 설정](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [개체 탐색기에서 이벤트 세션 관리](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)

## <a name="table-of-extended-events"></a>확장 이벤트 표

다음 확장 이벤트는 SQL Server on Linux 및 Azure SQL Database를 포함 하 여 [T-SQL PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) 문을 지 원하는 모든 버전의 SQL Server에서 사용할 수 있습니다. 

T-sql PREDICT 문은 SQL Server 2017에서 도입 되었습니다. 

|name |object_type|description| 
|----|----|----|
|predict_function_completed |이벤트  |기본 제공 실행 시간 분석|
|predict_model_cache_hit |이벤트|PREDICT 함수 모델 캐시에서 모델을 검색할 때 발생 합니다. 다른 predict_model_cache_ * 이벤트와 함께이 이벤트를 사용 하 여 PREDICT 함수 모델 캐시로 인 한 문제를 해결 합니다.|
|predict_model_cache_insert |이벤트  |   모델을 PREDICT 함수 모델 캐시에 삽입할 때 발생 합니다. 다른 predict_model_cache_ * 이벤트와 함께이 이벤트를 사용 하 여 PREDICT 함수 모델 캐시로 인 한 문제를 해결 합니다.    |
|predict_model_cache_miss   |이벤트|PREDICT 함수 모델 캐시에서 모델을 찾을 수 없을 때 발생 합니다. 이 이벤트가 자주 발생 하면 SQL Server에 더 많은 메모리가 필요 함을 나타낼 수 있습니다. 다른 predict_model_cache_ * 이벤트와 함께이 이벤트를 사용 하 여 PREDICT 함수 모델 캐시로 인 한 문제를 해결 합니다.|
|predict_model_cache_remove |이벤트| 예측 함수에 대해 모델 캐시에서 모델이 제거 될 때 발생 합니다. 다른 predict_model_cache_ * 이벤트와 함께이 이벤트를 사용 하 여 PREDICT 함수 모델 캐시로 인 한 문제를 해결 합니다.|

## <a name="query-for-related-events"></a>관련 이벤트에 대 한 쿼리

이러한 이벤트에 대해 반환 된 모든 열의 목록을 보려면 SQL Server Management Studio에서 다음 쿼리를 실행 합니다.

```sql
SELECT * FROM sys.dm_xe_object_columns WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>예

PREDICT를 사용 하 여 점수 매기기 세션의 성능에 대 한 정보를 캡처하려면 다음을 수행 합니다.

1. Management Studio 또는 지원 되는 다른 [도구](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)를 사용 하 여 새 확장 이벤트 세션을 만듭니다.
2. 이벤트 `predict_function_completed` 와`predict_model_cache_hit` 를 세션에 추가 합니다.
3. 확장 이벤트 세션을 시작 합니다.
4. PREDICT를 사용 하는 쿼리를 실행 합니다.

결과에서 다음 열을 검토 합니다.

+ 에 대 한 `predict_function_completed` 값은 쿼리가 모델 및 점수 매기기를 로드 하는 데 걸린 시간을 보여 줍니다.
+ 의 `predict_model_cache_hit` 부울 값은 쿼리에서 캐시 된 모델을 사용 했는지 여부를 나타냅니다. 

### <a name="native-scoring-model-cache"></a>네이티브 점수 매기기 모델 캐시

다음 쿼리를 사용 하 여 예측 관련 이벤트 외에 캐시 된 모델 및 캐시 사용에 대 한 자세한 정보를 얻을 수 있습니다.

네이티브 점수 매기기 모델 캐시 보기:

```sql
SELECT *
FROM sys.dm_os_memory_clerks
WHERE type = 'CACHESTORE_NATIVESCORING';
```

모델 캐시에서 개체를 봅니다.

```sql
SELECT *
FROM sys.dm_os_memory_objects
WHERE TYPE = 'MEMOBJ_NATIVESCORING';
```

