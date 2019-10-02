---
title: 확장 이벤트를 사용 하 여 예측 T-sql 모니터링
description: 확장 이벤트를 사용 하 여 SQL Server Machine Learning Services에서 예측 T-sql 문을 모니터링 하 고 문제를 해결 하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 958ac3e24a9deec231e7fd4d5da14477d693f4de
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714307"
---
# <a name="monitor-predict-t-sql-statements-with-extended-events-in-sql-server-machine-learning-services"></a>SQL Server에서 확장 이벤트를 사용 하 여 예측 T-sql 문을 모니터링 Machine Learning Services

확장 이벤트를 사용 하 여 SQL Server Machine Learning Services에서 [예측](../../t-sql/queries/predict-transact-sql.md) t-sql 문을 모니터링 하 고 문제를 해결 하는 방법에 대해 알아봅니다.

## <a name="table-of-extended-events"></a>확장 이벤트 표

다음 확장 이벤트는 [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) t-sql 문을 지 원하는 모든 버전의 SQL Server에서 사용할 수 있습니다. 

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
SELECT * 
FROM sys.dm_xe_object_columns 
WHERE object_name LIKE `predict%'
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

## <a name="next-steps"></a>다음 단계

확장 이벤트 (Xevent 라고도 함) 및 세션에서 이벤트를 추적 하는 방법에 대 한 자세한 내용은 다음 문서를 참조 하세요.

+ [SQL Server Machine Learning Services에서 확장 이벤트를 사용 하 여 Python 및 R 스크립트 모니터링](extended-events.md)
+ [확장 이벤트 개념 및 아키텍처](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [SSMS에서 이벤트 캡처 설정](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [개체 탐색기에서 이벤트 세션 관리](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)
