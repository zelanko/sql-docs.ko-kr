---
title: RevoScaleR rxDataStep을 사용 하 여 새 SQL Server 테이블 만들기
description: SQL Server에서 R 언어를 사용 하 여 SQL Server 테이블을 만드는 방법에 대 한 자습서 연습입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b18f2bd42070746551d21ff7508e7fce58b49037
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714910"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>RxDataStep을 사용 하 여 새 SQL Server 테이블 만들기 (SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 단원에서는 SQL Server [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 를 사용 하는 방법에 대 한 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 의 일부입니다.

이 단원에서는 메모리 내 데이터 프레임, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컨텍스트 및 로컬 파일 간에 데이터를 이동 하는 방법에 대해 알아봅니다.

> [!NOTE]
> 이 단원에서는 다른 데이터 집합을 사용 합니다. 항공편 지연 데이터 집합은 기계 학습 실험에 널리 사용 되는 공용 데이터 집합입니다. 이 예제에 사용 된 데이터 파일은 다른 제품 샘플과 동일한 디렉터리에서 사용할 수 있습니다.

## <a name="load-data-from-a-local-xdf-file"></a>로컬 XDF 파일에서 데이터 로드

이 자습서의 첫 번째 부분에서는 **RxTextData** 함수를 사용 하 여 텍스트 파일에서 R로 데이터를 가져온 다음 **Rxdatastep** 함수를 사용 하 여 데이터를로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이동 했습니다.

이 단원에서는 다른 방법을 사용 하 고 [Xdf 형식](https://en.wikipedia.org/wiki/Extensible_Data_Format)으로 저장 된 파일의 데이터를 사용 합니다. Xdf 파일을 사용 하 여 데이터에 대 한 간단한 변환을 수행한 후에는 변환 된 데이터를 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장 합니다.

**XDF 란?**

XDF 형식은 상위 차원 데이터를 위해 개발 된 XML 표준 이며 [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)에서 사용 하는 네이티브 파일 형식입니다. 또한 행 및 열 처리와 분석을 최적화하는 R 인터페이스가 포함된 이진 파일 형식입니다.  XDF 형식을 사용하여 데이터를 이동하고 분석에 유용한 데이터의 하위 집합을 저장할 수 있습니다.

1. 컴퓨팅 컨텍스트를 로컬 워크스테이션으로 설정합니다. **이 단계에서는 DDL 권한이 필요 합니다.**

    ```R
    rxSetComputeContext("local")
    ```
  
2. **RxXdfData** 함수를 사용하여 새 데이터 원본 개체를 정의합니다. XDF 데이터 원본을 정의 하려면 데이터 파일의 경로를 지정 합니다.  

    텍스트 변수를 사용 하 여 파일 경로를 지정할 수 있습니다. 그러나이 경우에는 **Rxgetoption** 함수를 사용 하 고 샘플 데이터 디렉터리에서 파일 (Rto Linedemosmall. xdf)을 가져오는 편리한 바로 가기가 있습니다.
  
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
> XDF 파일로 데이터를 로드하기 위해 다른 함수를 호출할 필요가 없으며 데이터에서 즉시 **rxGetVarInfo** 를 호출할 수 있다는 사실을 알아차리셨나요? 이는 XDF가 **RevoScaleR**에 대 한 기본 중간 저장소 방법 이기 때문입니다. XDF 파일 외에도 **Rxgetvarinfo** 함수는 이제 여러 소스 형식을 지원 합니다.

## <a name="move-contents-to-sql-server"></a>SQL Server로 콘텐츠 이동

로컬 R 세션에서 XDF 데이터 원본을 만든 후에는이 데이터를 데이터베이스 테이블로 이동 하 여 *DayOfWeek* 를 1 ~ 7 값의 정수로 저장할 수 있습니다.

1. SQL Server 데이터 원본 개체를 정의 하 고, 데이터를 포함할 테이블 및 원격 서버에 대 한 연결을 지정 합니다.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. 예방 조치로 이름이 같은 테이블이 이미 있는지 여부를 확인 하는 단계를 포함 하 고 있는 경우 해당 테이블을 삭제 합니다. 이름이 같은 기존 테이블은 새 테이블을 만드는 것을 방지 합니다.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. **Rxdatastep**을 사용 하 여 테이블에 데이터를 로드 합니다. 이 함수는 이미 정의 된 두 데이터 원본 간에 데이터를 이동 하 고 필요에 따라 경로 데이터를 변환할 수 있습니다.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    매우 큼 테이블 이므로 다음과 같은 최종 상태 메시지가 표시 될 때까지 기다립니다. *읽은 행: 20만, 총 처리 된 행: 60만*.
     
## <a name="load-data-from-a-sql-table"></a>SQL 테이블에서 데이터 로드

테이블에 데이터가 있으면 간단한 SQL 쿼리를 사용 하 여 로드할 수 있습니다. 

1. 새 SQL Server 데이터 원본을 만듭니다. 입력은 방금 만들고 데이터와 함께 로드 한 새 테이블에 대 한 쿼리입니다. 이 정의는 **RxSqlServerData**에 *colInfo* 인수를 사용 하 여 *DayOfWeek* 열의 요소 수준을 추가 합니다.
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. **Rxsummary** 를 한 번 더 호출 하 여 쿼리의 데이터 요약을 검토 합니다.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [rxDataStep을 사용하여 청크 분석 수행](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)