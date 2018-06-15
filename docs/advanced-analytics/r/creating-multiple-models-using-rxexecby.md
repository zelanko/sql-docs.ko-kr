---
title: RxExecBy (SQL Server 기계 학습)를 사용 하 여 여러 모델을 만드는 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 752ab5fc883f8fd99309496abb771931a05afc6a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31204585"
---
# <a name="creating-multiple-models-using-rxexecby"></a>RxExecBy를 사용 하 여 여러 모델 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

새 함수를 포함 하는 SQL Server 2017 CTP 2.0 **rxExecBy**를 지 원하는 여러 관련된 모델의 병렬 처리 합니다. 매우 큰 모델 데이터를에서 기반으로 여러 비슷한 엔터티 하나는 기차를 하는 대신 데이터 과학자 매우 빠르게 만들 수 여러 관련된 모델 엔터티 하나에 고유한 데이터를 사용 하 여 각 합니다.

예를 들어 장치 실패를 모니터링 하 고 다양 한 유형의 장비에 대 한 데이터를 캡처하는 가정 합니다. RxExecBy를 사용 하 여 입력으로 단일 큰 데이터 집합을 제공 장치 유형이 같은 데이터 집합을 층 화하여 할 열을 지정 고 그런 다음 개별 장치에 대 한 여러 모델 모델을 만들 수 있습니다.

이 프로세스 되었습니다 소개 "pleasingly 병렬" 처리, 데이터 과학자에 대 한 다소 성가실 또는 아무리 잘 번거로운 였으며 신속 하 고 간단한 작업을 사용 하면 작업을 사용 하기 때문에 있습니다.

이 방법의 일반적인 응용 프로그램의 개별 가구 스마트 미터에 대 한 예측, 별도 제품 라인에 대 한 수익 예측 또는 범주 예측자 변수 개별 은행 분기에 맞는 대출 승인에 대 한 포함 됩니다.

## <a name="how-rxexec-works"></a>RxExec의 작동 원리

RevoScaleR의 rxExecBy 함수 대규모 병렬 많은 수의 작은 데이터 집합을 통해 처리를 위해 설계 되었습니다.

1. R 코드의 일부로 rxExecBy 함수를 호출 하 고 순서가 지정 되지 않은 데이터의 데이터 집합을 전달 합니다.
2. 파티션에 있는 데이터를 그룹화 하거나 정렬할를 지정 합니다.
3. 변환 또는 모델링 각 데이터 파티션에 적용 해야 하는 함수를 정의 합니다.
4. 실행 되는 함수, 사용자 환경에서 지원 가능한 경우 병렬로 데이터 쿼리 처리 됩니다. 또한, 모델링 또는 변환 작업은 개별 코어 간에 분산 않으며 병렬로 실행 합니다. 지원 되는 계산 컨텍스트 소 작업 RxSpark 및 RxInSQLServer을 포함 합니다.
5. 여러 결과가 반환 됩니다.

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy 구문 및 예제

**rxExecBy** 는 4 개의 입력 인 분할할 수 있는 데이터 집합 또는 데이터 원본 개체가 입력 중 하나에 지정 된 **키** 열입니다. 각 파티션에 대 한 출력을 반환합니다. 출력의 형식을 인수로 전달 되는 함수에 따라 달라 집니다. 그리고 예를 들어 rxLinMod 등의 모델링 기능을 전달 하는 경우 데이터 집합의 각 파티션에 대 한 별도 학습 된 모델 반환할 수 있습니다.

### <a name="supported-functions"></a>지원되는 함수

모델링: `rxLinMod`, `rxLogit`, `rxGlm`, `rxDtree`

점수 매기기: `rxPredict`,

변환 또는 분석: `rxCovCor`

## <a name="example"></a>예제

다음 예제에서는 [DayOfWeek] 열에서 분할 되는 항공사 데이터 집합을 사용 하 여 여러 모델을 만드는 방법을 보여 줍니다. 사용자 정의 함수 `delayFunc`, 호출 rxExecBy로 각 파티션에 적용 됩니다. 월요일, 화요일에 대 한 별도 모델을 만듭니다. 함수 등입니다.

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

오류가 발생 하는 경우 `varsToPartition is invalid`, 키 열 또는 열 이름을 올바르게 입력 되었는지 여부를 확인 합니다. R 언어는 대/소문자 구분입니다.

이 예제에서는 SQL Server에 대 한 최적화 되지 않은 하며 대부분의 경우에서 수 데이터를 그룹화 할 SQL을 사용 하 여 성능을 향상 시킬 합니다. 그러나 rxExecBy를 사용 하 여 만들 수 있습니다 동시 작업이 오른쪽에서

다음 예제에서는 SQL Server를 사용 하 여 계산 컨텍스트로 써 R에서 프로세스를 보여 줍니다.

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


