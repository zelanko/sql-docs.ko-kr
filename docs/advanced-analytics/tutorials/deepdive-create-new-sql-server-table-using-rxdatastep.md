---
title: RxDataStep (SQL과 R 심층 분석)를 사용 하 여 새 SQL Server 테이블 만들기 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2fe521908e34afc1ae3ec23d56cb9d5cea801f1b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202325"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-and-r-deep-dive"></a>RxDataStep (SQL과 R 심층 분석)를 사용 하 여 새 SQL Server 테이블 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 데이터 과학 심층 분석 자습서를 사용 하는 방법에 대 한 일부 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server와 함께 합니다.

이 단원에서는 메모리 내 데이터 프레임 간에 데이터를 이동 하는 방법을 배웁니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컨텍스트와 로컬 파일입니다.

> [!NOTE]
> 이 단원에서는 다른 데이터 집합을 사용 합니다. 항공편 지연 데이터 집합은 기계 학습 실험에 널리 사용 되는 공용 데이터 집합입니다. 이 예에서 사용 된 데이터 파일은 다른 제품 예제와 동일한 디렉터리에서 사용할 수 있습니다.

## <a name="create-sql-server-table-from-local-data"></a>로컬 데이터에서 SQL Server 테이블 만들기

이 자습서의 앞부분에서 사용한는 **RxTextData** 텍스트 파일에서 R로 데이터를 가져오려면 작동 하 고 다음 사용는 **RxDataStep** 함수에 데이터를 이동 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.

이 단원에는 다른 방법을 사용 하 고 파일에서 사용 하 여 데이터에 저장 된 [XDF 형식](https://en.wikipedia.org/wiki/Extensible_Data_Format)합니다. 변환 된 데이터 형식의 새 파일에 저장 하면 XDF 파일을 사용 하 여 데이터에 대 한 몇 가지 간단한 변형 작업을 수행한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블입니다.

**XDF 소식**

XDF 형식이 고 차원 데이터에 대 한 개발 하는 XML 표준 및에서 사용 하는 네이티브 파일 형식 [컴퓨터 학습 서버](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)합니다. 또한 행 및 열 처리와 분석을 최적화하는 R 인터페이스가 포함된 이진 파일 형식입니다.  XDF 형식을 사용하여 데이터를 이동하고 분석에 유용한 데이터의 하위 집합을 저장할 수 있습니다.

1. 계산 컨텍스트를 로컬 워크스테이션으로 설정합니다. **이 단계에 대 한 DDL 권한이 필요 합니다.**

  
    ```R
    rxSetComputeContext("local")
    ```
  
2. **RxXdfData** 함수를 사용하여 새 데이터 원본 개체를 정의합니다. XDF 데이터 소스를 정의 하려면 데이터 파일의 경로를 지정 합니다.  

    텍스트 변수를 사용 하 여 파일의 경로를 지정할 수 있습니다. 그러나,이 경우에 사용 하는 편리한 바로 가기는 **rxGetOption** 작동 하 고 샘플 데이터 디렉터리에서 파일 (AirlineDemoSmall.xdf)을 가져옵니다.
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. 메모리 내 데이터에서 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf)를 호출하여 데이터 세트 요약을 확인합니다.
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**결과**

*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*

*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*

*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*

> [!NOTE]
> 
> XDF 파일로 데이터를 로드하기 위해 다른 함수를 호출할 필요가 없으며 데이터에서 즉시 **rxGetVarInfo** 를 호출할 수 있다는 사실을 알아차리셨나요? XDF가 RevoScaleR에 대한 기본 임시 저장 방법이기 때문입니다. XDF 파일 외에 **rxGetVarInfo** 함수에는 이제 다양 한 원본 형식을 지원 합니다.
  
4. 이 데이터를 넣기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블, 저장 _DayOfWeek_ 으로 정수 1 ~ 7 사이의 값입니다.
  
    이렇게 하려면 먼저 SQL Server 데이터 원본을 정의합니다.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
5. 이름이 같은 테이블이 이미 있는지 확인하고, 있을 경우 테이블을 삭제합니다.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
6. 테이블을 만들고 **rxDataStep**에 대한 다양한 제품 샘플에서 사용되므로 테스트를 위해 보관해 두면 유용합니다. 이 함수는 두 데이터에서 이미 데이터 원본을 정의 하 고 전달 되는 도중 데이터를 선택적으로 변환할 수를 이동 합니다.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
            transforms = list( DayOfWeek = as.integer(DayOfWeek),
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
            overwrite = TRUE )
    ```
  
    이 테이블은 매우 크기 때문에 테이블, 하므로이 이와 같은 최종 상태 메시지가 표시 될 때까지 기다렸다가: *Rows Read: 200000, 총 행이 처리: 600000*합니다.
     
7. 계산 컨텍스트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터로 다시 설정합니다.

    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
8. 새 테이블에서 간단한 SQL 쿼리를 사용하여 새 SQL Server 데이터 원본을 만듭니다. 이 정의 대 한 계수 수준을 추가 *DayOfWeek* 열을 사용 하는 *colInfo* 인수를 **RxSqlServerData**합니다.
  
    ```R
    SqlServerAirDemo <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
9. 호출 **rxSummary** 쿼리에서 데이터의 요약을 검토 하는 한 번 더 합니다.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo)
    ```

## <a name="next-step"></a>다음 단계

[rxDataStep을 사용하여 청크 분석 수행](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)

## <a name="previous-step"></a>이전 단계

[rxImport를 사용하여 메모리에 데이터 로드](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
