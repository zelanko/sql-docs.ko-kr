---
title: RevoScaleR rxDataStep-SQL Server Machine Learning을 사용 하 여 새 SQL Server 테이블 만들기
description: SQL Server에서 R 언어를 사용 하 여 SQL Server 테이블을 만드는 방법에 대 한 연습 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1fb3f83cd3bbd39e3af4936ce8dfb8f16bad82d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641466"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>RxDataStep (RevoScaleR 및 SQL Server 자습서)를 사용 하 여 새 SQL Server 테이블 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는의 일부인를 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 사용 하는 방법에 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server를 사용 하 여 합니다.

이 단원에서는 메모리 내 데이터 프레임 간에 데이터를 이동 하는 방법을 알아봅니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컨텍스트 및 로컬 파일입니다.

> [!NOTE]
> 이 단원에서는 다른 데이터 집합을 사용합니다. 항공사 지연 데이터 집합은 기계 학습 실험에 널리 사용 되는 공용 데이터 집합입니다. 이 예제에 사용 되는 데이터 파일은 다른 제품 샘플과 동일한 디렉터리에 제공 됩니다.

## <a name="load-data-from-a-local-xdf-file"></a>로컬 XDF 파일에서 데이터 로드

이 자습서의 앞부분에서 사용한를 **RxTextData** 텍스트 파일에서 R로 데이터를 가져오려면 함수를 사용 합니다 **RxDataStep** 데이터를 이동 하는 함수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

이 단원에서는 다른 방법을 사용 하 고 파일에서 사용 하 여 데이터에 저장 합니다 [XDF 형식](https://en.wikipedia.org/wiki/Extensible_Data_Format)합니다. 변환된 된 데이터를 새로운 저장 하면 XDF 파일을 사용 하 여 데이터에 몇 가지 간단한 변환을 수행한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.

**XDF 란?**

XDF 형식은 고 차원 데이터에 대 한 개발 하는 XML 표준 및에서 사용 되는 네이티브 파일 형식 [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)합니다. 또한 행 및 열 처리와 분석을 최적화하는 R 인터페이스가 포함된 이진 파일 형식입니다.  XDF 형식을 사용하여 데이터를 이동하고 분석에 유용한 데이터의 하위 집합을 저장할 수 있습니다.

1. 컴퓨팅 컨텍스트를 로컬 워크스테이션으로 설정합니다. **이 단계에 대 한 DDL 권한이 필요 합니다.**

    ```R
    rxSetComputeContext("local")
    ```
  
2. **RxXdfData** 함수를 사용하여 새 데이터 원본 개체를 정의합니다. XDF 데이터 원본의 정의 하려면 데이터 파일의 경로를 지정 합니다.  

    텍스트 변수를 사용 하 여 파일의 경로를 지정할 수 있습니다. 그러나이 경우에 유용한 바로 가기는, 사용 하는 합니다 **rxGetOption** 함수 및 샘플 데이터 디렉터리에서 파일 (AirlineDemoSmall.xdf)를 가져옵니다.
  
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
> XDF 파일로 데이터를 로드하기 위해 다른 함수를 호출할 필요가 없으며 데이터에서 즉시 **rxGetVarInfo** 를 호출할 수 있다는 사실을 알아차리셨나요? XDF에 대 한 기본 임시 저장 방법 이므로 이것이 **RevoScaleR**합니다. XDF 파일 외에 **rxGetVarInfo** 함수에는 이제 여러 원본 유형을 지원 합니다.

## <a name="move-contents-to-sql-server"></a>SQL server 콘텐츠를 이동

로컬 R 세션에서 만든 XDF 데이터 원본과 함께 이동할 수 있습니다 이제이 데이터를 데이터베이스 테이블에 저장 *DayOfWeek* 값 1에서 7 사이인 정수로 합니다.

1. 원격 서버 연결을 확인 하 고 데이터를 포함 하도록 테이블을 지정 하는 SQL Server 데이터 원본 개체를 정의 합니다.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. 예방 조치로 여부를 확인 같은 이름의 테이블이 이미 있으면 존재 하는 경우 테이블을 삭제 하는 단계를 포함 합니다. 같은 이름의 기존 테이블을 새로 만들지 못하도록 방지 합니다.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. 사용 하 여 테이블에 데이터 로드 **rxDataStep**합니다. 이 함수는 두 데이터에서 이미 데이터 원본을 정의 하 고 데이터를 이동 하는 과정을 선택적으로 변환할 수를 이동 합니다.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    매우 큰 테이블이 이와 같은 최종 상태 메시지가 표시 될 때까지 기다렸다가: *Rows Read: 처리 된 200000, total 행: 600000*.
     
## <a name="load-data-from-a-sql-table"></a>SQL 테이블에서 데이터를 로드 합니다.

테이블에 데이터가 있으면 간단한 SQL 쿼리를 사용 하 여 로드할 수 있습니다. 

1. 새 SQL Server 데이터 원본을 만듭니다. 입력은 바로 전에 만들고 데이터를 사용 하 여 로드 된 새 테이블에 대 한 쿼리. 이 정의 대 한 요소 수준을 추가 합니다 *DayOfWeek* 열을 사용 하 여는 *colInfo* 인수를 **RxSqlServerData**합니다.
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. 호출 **rxSummary** 쿼리의 데이터 요약을 검토 하는 한 번 더 합니다.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [rxDataStep을 사용하여 청크 분석 수행](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)