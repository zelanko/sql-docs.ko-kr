---
title: rxExecBy를 사용하여 여러 모델 만들기
description: RevoScaleR 라이브러리의 rxExecBy 함수를 사용 하 여 SQL Server에 저장 된 컴퓨터 데이터에 대해 여러 개의 미니 모델을 빌드합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1b2e6e1d546b9bbd1b3b3196c37716acbbe0ae74
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715716"
---
# <a name="creating-multiple-models-using-rxexecby"></a>rxExecBy를 사용하여 여러 모델 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

RevoScaleR의 **Rxexecby** 함수는 여러 관련 모델의 병렬 처리를 지원 합니다. 여러 유사한 엔터티의 데이터를 기반으로 하는 하나의 커다란 모델을 학습 하는 대신, 데이터 과학자는 단일 엔터티와 관련 된 데이터를 사용 하 여 여러 개의 관련 모델을 신속 하 게 만들 수 있습니다. 

예를 들어 장치 오류를 모니터링 하 고 다양 한 유형의 장비에 대 한 데이터를 캡처하는 경우를 가정 합니다. RxExecBy를 사용 하 여 단일 대량 데이터 집합을 입력으로 제공 하 고, 데이터 집합을 층 화 기준 하는 열 (예: 장치 유형)을 지정한 다음 개별 장치에 대해 여러 모델을 만들 수 있습니다.

이 사용 사례는 동시 처리를 위해 구성 요소 부분으로 복잡 한 문제를 분리 하므로 ["pleasingly parallel"](https://en.wikipedia.org/wiki/Embarrassingly_parallel) 이라고 합니다.

이러한 접근 방식의 일반적인 응용 프로그램에는 개별 가계 스마트 미터에 대 한 예측, 개별 제품 라인에 대 한 수익 예측 만들기 또는 개별 은행 분기에 맞게 조정 된 대출 승인을 위한 모델 생성이 포함 됩니다.

## <a name="how-rxexec-works"></a>RxExec 작동 방법

RevoScaleR의 rxExecBy 함수는 많은 수의 작은 데이터 집합에 대 한 고용량 병렬 처리를 위해 설계 되었습니다.

1. R 코드의 일부로 rxExecBy 함수를 호출 하 고 정렬 되지 않은 데이터의 데이터 집합을 전달 합니다.
2. 데이터를 그룹화 하 고 정렬 하는 데 사용할 파티션을 지정 합니다.
3. 각 데이터 파티션에 적용 해야 하는 변환 또는 모델링 함수를 정의 합니다.
4. 함수가 실행 되 면 데이터 쿼리는 환경에서 지원 되는 경우 병렬로 처리 됩니다. 또한 모델링 또는 변환 태스크는 개별 코어 간에 분산 되 고 병렬로 실행 됩니다. 작업에 대해 지원 되는 계산 컨텍스트는 RxSpark 및 RxInSQLServer입니다.
5. 여러 결과가 반환 됩니다.

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy 구문 및 예제

**Rxexecby** 는 지정 된 **키** 열에서 분할 될 수 있는 데이터 집합 또는 데이터 원본 개체의 입력 중 하나인 4 개의 입력을 사용 합니다. 함수는 각 파티션에 대 한 출력을 반환 합니다. 출력 형식은 인수로 전달 되는 함수에 따라 달라 집니다. 예를 들어 rxLinMod와 같은 모델링 함수를 전달 하는 경우 데이터 집합의 각 파티션에 대해 별도의 학습 된 모델을 반환할 수 있습니다.

### <a name="supported-functions"></a>지원되는 함수

모델링: `rxLinMod` `rxLogit` ,,,`rxGlm``rxDtree`

점수 매기기 `rxPredict`:,

변환 또는 분석:`rxCovCor`

## <a name="example"></a>예제

다음 예에서는 [DayOfWeek] 열에서 분할 된 항공편 데이터 집합을 사용 하 여 여러 모델을 만드는 방법을 보여 줍니다. 사용자 정의 함수 `delayFunc`는 rxexecby를 호출 하 여 각 파티션에 적용 됩니다. 이 함수는 월요일, 화요일 등에 대 한 별도의 모델을 만듭니다.

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

오류가 발생 `varsToPartition is invalid`하면 키 열 이름을 올바르게 입력 했는지 확인 합니다. R 언어는 대/소문자를 구분 합니다.

이 특정 예제는 SQL Server에 대해 최적화 되지 않으므로 많은 경우에서 SQL을 사용 하 여 데이터를 그룹화 하 여 성능을 향상 시킬 수 있습니다. 그러나 rxExecBy를 사용 하 여 R에서 병렬 작업을 만들 수 있습니다.

다음 예에서는 SQL Server를 계산 컨텍스트로 사용 하 여 R의 프로세스를 보여 줍니다.

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


