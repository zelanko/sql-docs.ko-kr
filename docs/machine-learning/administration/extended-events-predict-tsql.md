---
title: 확장 이벤트를 사용하여 T-SQL 모니터링
description: 확장 이벤트를 사용하여 SQL Server Machine Learning Services에서 PREDICT T-SQL 문을 모니터링하고 문제를 해결하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/24/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 79053a7dcf91b220bdb288fc7efc711c80684aa0
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88171872"
---
# <a name="monitor-predict-t-sql-statements-with-extended-events-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에서 확장 이벤트를 사용하여 PREDICT T-SQL 문 모니터링
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

확장 이벤트를 사용하여 SQL Server Machine Learning Services에서 [PREDICT](../../t-sql/queries/predict-transact-sql.md) T-SQL 문을 모니터링하고 문제를 해결하는 방법에 대해 알아봅니다.

## <a name="table-of-extended-events"></a>확장 이벤트 테이블

[PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) T-SQL 문을 지원하는 모든 버전의 SQL Server에서 다음 확장 이벤트를 사용할 수 있습니다. 

|name |object_type|description| 
|----|----|----|
|predict_function_completed |이벤트  |기본 제공 실행 시간 중단점|
|predict_model_cache_hit |이벤트|PREDICT 함수 모델 캐시에서 모델을 검색할 때 발생합니다. 다른 predict_model_cache_* 이벤트와 함께 이 이벤트를 사용하여 PREDICT 함수 모델 캐시에서 발생한 문제를 해결하세요.|
|predict_model_cache_insert |이벤트  |   모델이 PREDICT 함수 모델 캐시에 삽입될 때 발생합니다. 다른 predict_model_cache_* 이벤트와 함께 이 이벤트를 사용하여 PREDICT 함수 모델 캐시에서 발생한 문제를 해결하세요.    |
|predict_model_cache_miss   |이벤트|PREDICT 함수 모델 캐시에서 모델을 찾을 수 없을 때 발생합니다. 이 이벤트가 자주 발생하면 SQL Server에 더 많은 메모리가 필요함을 나타낼 수 있습니다. 다른 predict_model_cache_* 이벤트와 함께 이 이벤트를 사용하여 PREDICT 함수 모델 캐시에서 발생한 문제를 해결하세요.|
|predict_model_cache_remove |이벤트| PREDICT 함수를 위해 모델 캐시에서 모델을 제거할 때 발생합니다. 다른 predict_model_cache_* 이벤트와 함께 이 이벤트를 사용하여 PREDICT 함수 모델 캐시에서 발생한 문제를 해결하세요.|

## <a name="query-for-related-events"></a>관련 이벤트 쿼리

이러한 이벤트에 대해 반환된 모든 열의 목록을 보려면 SQL Server Management Studio에서 다음 쿼리를 실행합니다.

```sql
SELECT * 
FROM sys.dm_xe_object_columns 
WHERE object_name LIKE `predict%'
```

## <a name="examples"></a>예

PREDICT를 사용하여 점수 매기기 세션의 성능에 대한 정보를 캡처하려면 다음을 수행합니다.

1. Management Studio 또는 지원되는 다른 [도구](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)를 사용하여 새 확장 이벤트 세션을 만듭니다.
2. `predict_function_completed` 및 `predict_model_cache_hit` 이벤트를 세션에 추가합니다.
3. 확장 이벤트 세션을 시작합니다.
4. PREDICT를 사용하는 쿼리를 실행합니다.

결과에서 다음 열을 검토합니다.

+ `predict_function_completed`의 값은 쿼리가 모델을 로드하고 점수를 매기는 데 소요된 시간을 보여줍니다.
+ `predict_model_cache_hit`의 부울 값은 쿼리가 캐시된 모델을 사용했는지 여부를 나타냅니다. 

### <a name="native-scoring-model-cache"></a>네이티브 점수 매기기 모델 캐시

PREDICT와 관련된 이벤트 외에도 다음 쿼리를 사용하여 캐시된 모델 및 캐시 사용량에 대한 자세한 정보를 가져올 수 있습니다.

네이티브 점수 매기기 모델 캐시를 봅니다.

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

확장 이벤트(XEvents라고도 함) 및 세션에서 이벤트를 추적하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

+ [SQL Server Machine Learning Services에서 확장 이벤트를 사용하여 Python 및 R 스크립트 모니터링](extended-events.md)
+ [확장 이벤트 개념 및 아키텍처](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)
+ [SSMS에서 이벤트 캡처 설정](https://docs.microsoft.com/sql/relational-databases/extended-events/quick-start-extended-events-in-sql-server)
+ [개체 탐색기에서 이벤트 세션 관리](https://docs.microsoft.com/sql/relational-databases/extended-events/manage-event-sessions-in-the-object-explorer)
