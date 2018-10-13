---
title: RxExecBy (SQL Server Machine Learning)를 사용 하 여 여러 모델 만들기 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b83abad65689e3e12310251d09199f5aa0e7c3cb
ms.sourcegitcommit: 0d6e4cafbb5d746e7d00fdacf8f3ce16f3023306
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49085129"
---
# <a name="creating-multiple-models-using-rxexecby"></a>rxExecBy를 사용하여 여러 모델 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

새 함수를 포함 하는 SQL Server 2017 CTP 2.0 **rxExecBy**를 지 원하는 여러 관련된 모델의 병렬 처리 합니다. 매우 큰 모델 데이터를에서 기반으로 여러 비슷한 엔터티 하나는 학습, 대신 데이터 과학자가 매우 신속 하 게 만들면 여러 관련된 모델을 단일 엔터티에 관련 된 데이터를 사용 하 여 각 합니다.

예를 들어, 장치 오류를 모니터링 하 고 다양 한 유형의 장비에 대 한 데이터 캡처를 가정 합니다. RxExecBy를 사용 하 여 입력으로 단일 큰 데이터 집합을 제공 장치 유형과 같은 데이터 집합을 층 화 하는 열을 지정 한 후 개별 장치에 대해 여러 모델을 만들 수 있습니다.

이 프로세스 되었습니다 소개 "pleasingly 병렬" 처리, 데이터 과학자에 대 한 다소 번거롭습니다 되었거나 가장 좋은 것은 지루하고 신속 하 고 간단한 작업을 사용 하면 작업 걸리기 때문에 있습니다.

이 방법의 일반적인 응용 프로그램에는 개별 가구 스마트 측정기에 대 한 예측, 별도 제품 라인에 대 한 수익 예측 만들기 또는 개별 은행 분기에 맞게 조정 되는 대출 승인에 대 한 모델을 만드는 포함 됩니다.

## <a name="how-rxexec-works"></a>RxExec의 작동 원리

RevoScaleR의 rxExecBy 함수는 대규모 병렬 많은 수의 작은 데이터 집합을 통해 처리를 위해 설계 되었습니다.

1. R 코드의 일부로 rxExecBy 함수를 호출 하 고 순서가 지정 되지 않은 데이터의 데이터 집합을 전달 합니다.
2. 사용 되는 데이터는 그룹화 하거나 정렬할 파티션을 지정 합니다.
3. 변환 또는 모델링 각 데이터 파티션에 적용 해야 하는 함수를 정의 합니다.
4. 함수를 실행할 때 환경을 지 원하는 경우 데이터 쿼리를 병렬로 처리 됩니다. 또한 모델링 또는 변환 작업을 개별 코어 간에 분산 되며 병렬로 실행 됩니다. 지원 되는 계산 컨텍스트 다음에 대 한 작업 RxSpark 및 RxInSQLServer을 포함 합니다.
5. 여러 결과가 반환 됩니다.

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy 구문 및 예제

**rxExecBy** 는 4 개의 입력, 분할 될 수 있는 데이터 집합 또는 데이터 원본 개체를 중인 입력 중에 지정 된 **키** 열입니다. 함수는 각 파티션에 대 한 출력을 반환 합니다. 출력의 형식을 인수로 전달 되는 함수에 따라 달라 집니다,, 그리고 예를 들어 rxLinMod 같은 모델링 함수에 전달 하면 데이터 집합의 각 파티션에 대 한 별도 학습 된 모델을 반환할 수 있습니다.

### <a name="supported-functions"></a>지원되는 함수

모델링: `rxLinMod`하십시오 `rxLogit`, `rxGlm`, `rxDtree`

점수 매기기: `rxPredict`,

변환 또는 분석: `rxCovCor`

## <a name="example"></a>예제

다음 예제에서는 [DayOfWeek] 열에서 분할 되는 항공사 데이터 집합을 사용 하 여 여러 모델을 만드는 방법을 보여 줍니다. 사용자 정의 함수를 `delayFunc`, rxExecBy를 호출 하 여 파티션의 각에 적용 됩니다. 이 함수는 월요일, 화요일에 대 한 별도 모델을 만듭니다 등입니다.

```SQL
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

오류를 받게 되 면 `varsToPartition is invalid`, 키 열 또는 열 이름을 올바르게 입력 되었는지 여부를 확인 합니다. R 언어는 대/소문자 구분 합니다.

SQL 데이터를 그룹화 하 여 더 나은 성능을 달성 하는이 예제에서는 SQL Server에 최적화 되지 않는 및 대부분의 수는 있습니다. 그러나 rxExecBy를 사용 하 여 만들 수 있습니다 병렬 작업 R.에서

다음 예제에서는 r에서 SQL Server 계산 컨텍스트로 사용 하 여 프로세스를 보여 줍니다.

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


