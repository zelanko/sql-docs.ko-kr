---
title: rxExecBy를 사용하여 여러 모델 만들기
description: RevoScaleR 라이브러리의 rxExecBy 함수를 사용하여 SQL Server에 저장된 컴퓨터 데이터에 대해 여러 개의 미니 모델을 빌드합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: dbba63ae69997c9c5dbdccf49ec590b3f4eba652
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727487"
---
# <a name="creating-multiple-models-using-rxexecby"></a>rxExecBy를 사용하여 여러 모델 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

RevoScaleR의 **rxExecBy** 함수는 여러 관련 모델의 병렬 처리를 지원합니다. 데이터 과학자는 여러 비슷한 엔터티 데이터를 기준으로 하나의 대형 모델을 학습하는 대신 각각 단일 엔터티와 관련된 데이터를 사용하여 여러 개의 관련 모델을 빠르게 만들 수 있습니다. 

예를 들어 디바이스 오류를 모니터링하고, 여러 유형의 장비에 대해 데이터를 캡처한다고 가정해보세요. rxExecBy를 사용하면 하나의 큰 데이터 세트를 입력으로 제공하고, 디바이스 유형과 같이 데이터 세트를 계층화할 열을 지정한 후, 개별 디바이스에 대해 여러 모델을 만들 수 있습니다.

이러한 사용 사례는 동시 처리를 위해 하나의 크고 복잡한 문제를 구성 요소 부분들로 세분화하기 때문에 ["기분 좋은 병렬화(pleasingly parallel)"](https://en.wikipedia.org/wiki/Embarrassingly_parallel)라고 부릅니다.

이러한 접근 방식이 적용되는 일반적인 사례에는 개별적인 가정용 스마트 측정기를 위한 예측, 개별 제품 라인을 위한 수익 예상 생성, 개별 은행 지점에 맞게 맞춤화된 대출 승인을 위한 모델 생성 등이 포함됩니다.

## <a name="how-rxexec-works"></a>rxExec 작동 방법

RevoScaleR의 rxExecBy 함수는 대량의 소규모 데이터 세트에 대한 대량 병렬 처리를 위해 디자인되었습니다.

1. rxExecBy 함수를 R 코드의 일부로 호출하고 정렬되지 않은 데이터의 데이터 세트를 전달합니다.
2. 데이터를 그룹화하고 정렬해야 하는 파티션을 지정합니다.
3. 각 데이터 파티션에 적용되어야 하는 변환 또는 모델링 함수를 정의합니다.
4. 함수가 실행되면 데이터 쿼리가 병렬로 처리됩니다(해당 환경에서 지원되는 경우). 또한 모델링 또는 변환 작업이 개별 코어 사이에 분포되고 병렬로 실행됩니다. 이러한 작업에 대해 지원되는 계산 컨텍스트에는 RxSpark 및 RxInSQLServer가 포함됩니다.
5. 여러 결과가 반환됩니다.

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy 구문 및 예

**rxExecBy**에는 4개의 입력이 사용됩니다. 입력 중 하나는 데이터 세트 또는 데이터 원본 개체로 사용되며, 지정된 **키** 열로 분할될 수 있습니다. 이 함수는 각 파티션에 대해 출력을 반환합니다. 출력 형식은 인수로 전달된 함수에 따라 달라집니다. 예를 들어 rxLinMod와 같은 모델링 함수를 전달하는 경우, 데이터 세트의 각 파티션에 대해 개별적인 학습 모델을 반환할 수 있습니다.

### <a name="supported-functions"></a>지원되는 함수

모델링: `rxLinMod`, `rxLogit`, `rxGlm`, `rxDtree`

채점: `rxPredict`,

변환 또는 분석: `rxCovCor`

## <a name="example"></a>예제

다음 예제는 [DayOfWeek] 열로 분할된 항공사 데이터 세트를 사용하여 여러 모델을 생성하는 방법을 보여줍니다. 사용자 정의 함수 `delayFunc`는 rxExecBy를 호출하여 각 파티션에 적용됩니다. 이 함수는 월요일, 화요일 등에 대해 개별적으로 모델을 만듭니다.

```sql
EXEC sp_execute_external_script
@language = N'R'
, @script = N'
delayFunc <- function(key, data, params) { 
    df <- rxImport(inData = airlineData) 
    rxLinMod(ArrDelay ~ CRSDepTime, data = df) 
} 
OutputDataSet <- rxExecBy(airlineData, c("DayOfWeek"), delayFunc)
'
, @input_data_1 = N'select ArrDelay, DayOfWeek, CRSDepTime from AirlineDemoSmall]'
, @input_data_1_name = N'airlineData'

```

`varsToPartition is invalid` 오류가 발생하면 키 열의 이름이 올바르게 입력되었는지 확인합니다. R 언어는 대/소문자를 구분합니다.

이 특정 예제는 SQL Server용으로 최적화되지 않았으며, 많은 경우에 데이터를 그룹화하는 SQL을 사용하여 더 나은 성능을 얻을 수 있습니다. 하지만 rxExecBy를 사용하면 R에서 병렬 작업을 만들 수 있습니다.

다음 예제는 SQL Server를 계산 컨텍스트로 사용하는 R에서의 프로세스를 보여줍니다.

```R
sqlServerConnString <- "SERVER=hostname;DATABASE=TestDB;UID=DBUser;PWD=Password;"
inTable <- paste("airlinedemosmall")
sqlServerDataDS <- RxSqlServerData(table = inTable, connectionString = sqlServerConnString)

# user function
".Count" <- function(keys, data, params)
{
  myDF <- rxImport(inData = data)
  return (nrow(myDF))
}

# Set SQL Server compute context with level of parallelism = 2
sqlServerCC <- RxInSqlServer(connectionString = sqlServerConnString, numTasks = 4)
rxSetComputeContext(sqlServerCC)

# Execute rxExecBy in SQL Server compute context
sqlServerCCResults <- rxExecBy(inData = sqlServerDataDS, keys = c("DayOfWeek"), func = .Count)
```


