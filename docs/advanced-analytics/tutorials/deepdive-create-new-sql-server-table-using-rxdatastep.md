---
title: rxDataStep을 사용하여 테이블 만들기
description: SQL Server에서 R 언어를 사용하여 SQL Server 테이블을 만드는 방법에 대한 자습서 연습입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f4ac51fc1affb4128abab017eb00cba4b56960fa
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727250"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>rxDataStep을 사용하여 새 SQL Server 테이블 만들기(SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 단원은 SQL Server에서 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)를 사용하는 방법에 대한 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)의 일부입니다.

이 단원에서는 메모리 내 데이터 프레임, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컨텍스트 및 로컬 파일 간에 데이터를 이동하는 방법을 알아봅니다.

> [!NOTE]
> 이 단원에서는 다른 데이터 세트가 사용됩니다. 항공사 지연 데이터 세트는 Machine Learning 실험을 위해 널리 사용되는 공용 데이터 세트입니다. 이 예제에 사용되는 데이터 파일은 다른 제품 샘플들과 동일한 디렉터리에 있습니다.

## <a name="load-data-from-a-local-xdf-file"></a>로컬 XDF 파일에서 데이터 로드

이 자습서의 처음 절반 부분에서는 **RxTextData** 함수를 사용하여 데이터를 텍스트 파일에서 R로 가져온 후, **RxDataStep** 함수를 사용하여 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 이동했습니다.

이 단원에서는 다른 접근 방법에 따라 [XDF 형식](https://en.wikipedia.org/wiki/Extensible_Data_Format)으로 저장된 파일의 데이터를 사용합니다. XDF 파일을 사용하여 데이터에 대해 몇 가지 간단한 변환을 수행한 후 변환된 데이터를 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장합니다.

**XDF란?**

XDF 형식은 고차원 데이터를 위해 개발된 XML 표준이며, [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)에서 사용되는 네이티브 파일 형식입니다. 또한 행 및 열 처리와 분석을 최적화하는 R 인터페이스가 포함된 이진 파일 형식입니다.  XDF 형식을 사용하여 데이터를 이동하고 분석에 유용한 데이터의 하위 집합을 저장할 수 있습니다.

1. 컴퓨팅 컨텍스트를 로컬 워크스테이션으로 설정합니다. **이 단계를 수행하려면 DDL 권한이 필요합니다.**

    ```R
    rxSetComputeContext("local")
    ```
  
2. **RxXdfData** 함수를 사용하여 새 데이터 원본 개체를 정의합니다. XDF 데이터 원본을 정의하려면 데이터 파일의 경로를 지정합니다.  

    텍스트 변수를 사용하여 파일 경로를 지정할 수 있습니다. 하지만 이 경우에는 **rxGetOption** 함수를 사용하고 샘플 데이터 디렉터리에서 파일(AirlineDemoSmall.xdf)을 가져오는 간단한 방법이 있습니다.
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. 메모리 내 데이터에서 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf)를 호출하여 데이터 세트 요약을 확인합니다.
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**결과**

```R
Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)
Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)
Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday
```

> [!NOTE]
> 
> XDF 파일로 데이터를 로드하기 위해 다른 함수를 호출할 필요가 없으며 데이터에서 즉시 **rxGetVarInfo** 를 호출할 수 있다는 사실을 알아차리셨나요? 그 이유는 XDF가 **RevoScaleR**의 기본 임시 스토리지 방법이기 때문입니다. XDF 파일 외에도 **rxGetVarInfo** 함수는 이제 여러 원본 유형을 지원합니다.

## <a name="move-contents-to-sql-server"></a>SQL Server로 콘텐츠 이동

XDF 데이터 원본이 로컬 R 세션에 생성되었으면 이제 이 데이터를 데이터베이스 테이블로 이동하고 1~7까지의 정수 값으로 *DayOfWeek*를 저장할 수 있습니다.

1. SQL Server 데이터 원본 개체를 정의하고, 데이터를 포함할 테이블 및 원격 서버에 대한 연결을 지정합니다.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. 문제가 발생할 경우에 대비하여 이름이 같은 테이블이 이미 있는지 확인하고, 있을 경우 테이블을 삭제하는 단계를 포함합니다. 이름이 같은 기존 테이블이 있으면 새 테이블이 생성되지 않습니다.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. **rxDataStep**을 사용하여 데이터를 테이블에 로드합니다. 이 함수는 이미 정의된 데이터 원본 사이에 데이터를 이동하고 선택적으로 중간에 데이터를 변환할 수 있습니다.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    이 테이블은 상당히 크기 때문에 다음과 같은 최종 상태 메시지가 표시될 때까지 잠시 기다려야 합니다. *읽은 행: 200000, 총 처리된 행: 600000*.
     
## <a name="load-data-from-a-sql-table"></a>SQL 테이블에서 데이터 로드

테이블에 데이터가 있으면, 간단한 SQL 쿼리를 사용하여 이를 로드할 수 있습니다. 

1. 새 SQL Server 데이터 원본을 만듭니다. 입력은 바로 전에 만들고 데이터를 로드한 새 테이블에 대한 쿼리입니다. 이 정의는 **RxSqlServerData**에 대해 *colInfo* 인수를 사용하여 *DayOfWeek* 열에 대한 요소 수준을 추가합니다.
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. **rxSummary**를 한 번 더 호출하여 쿼리의 데이터 요약을 검토합니다.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [rxDataStep을 사용하여 청크 분석 수행](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)