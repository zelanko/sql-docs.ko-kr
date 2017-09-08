---
title: "RxDataStep를 사용 하 여 새 SQL Server 테이블 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4a5a8aaa8df1df4d34216f9d55806ccf5594292a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-new-sql-server-table-using-rxdatastep"></a>RxDataStep을 사용하여 새 SQL Server 테이블 만들기

이 단원에서는 메모리 내 데이터 프레임, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컨텍스트 및 로컬 파일 간에 데이터를 이동하는 방법을 알아봅니다.

> [!NOTE]
> 이 단원에서는 다른 데이터 집합을 사용합니다. 항공편 지연 데이터 집합은 기계 학습 실험에 널리 사용 되는 공용 데이터 집합입니다. 방금 R을 시작한 경우, 이 데이터 집합은 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 으로 게시된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 대한 다양한 제품 샘플에서 사용되므로 테스트를 위해 보관해 두면 유용합니다. 이 예제에 필요한 데이터 파일은 다른 제품 샘플과 같은 디렉터리에 있습니다.

## <a name="create-sql-server-table-from-local-data"></a>로컬 데이터에서 SQL Server 테이블 만들기

이 자습서의 첫 부분에 사용 되는 **RxTextData** 텍스트 파일에서 R로 데이터를 가져오려면 작동 하 고 다음 사용는 **RxDataStep** 함수에 데이터를 이동 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.

이 단원에서는 다른 접근 방식을 사용하고 [XDF 형식](https://en.wikipedia.org/wiki/Extensible_Data_Format)으로 저장된 파일에서 데이터를 가져옵니다. XDF 형식은 고차원 데이터용으로 개발된 XML 표준입니다. 또한 행 및 열 처리와 분석을 최적화하는 R 인터페이스가 포함된 이진 파일 형식입니다.  XDF 형식을 사용하여 데이터를 이동하고 분석에 유용한 데이터의 하위 집합을 저장할 수 있습니다.

XDF 파일을 사용하여 데이터에 대해 몇 가지 간단한 변환을 수행한 후 변환된 데이터를 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장합니다.

> [!NOTE]
> 이 단계를 수행하려면 DDL 권한이 필요합니다.

1. 계산 컨텍스트를 로컬 워크스테이션으로 설정합니다.
  
    ```R
    rxSetComputeContext("local")
    ```
  
2. **RxXdfData** 함수를 사용하여 새 데이터 원본 개체를 정의합니다. XDF 데이터 원본의 경우 데이터 파일의 경로만 지정하면 됩니다.  텍스트 변수를 사용 하 여 파일의 경로를 지정할 수 있습니다 이지만 경우에 간편한 바로 가기입니다 하므로 rxGetOption 함수에서 반환 된 디렉터리에는 예제 데이터 파일 (AirlineDemoSmall.xdf).
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. 데이터 집합의 요약 정보를 보려면 메모리 내 데이터에 rxGetVarInfo를 호출 합니다.
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**결과**

*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*

*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*

*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*

> [!NOTE]
> 
> XDF 파일로 데이터를 로드 하도록 다른 함수를 호출 하는 필요 하지 않은 데이터에 대해 rxGetVarInfo 즉시 호출할 수 있었습니다 하 알림? XDF가 RevoScaleR에 대한 기본 임시 저장 방법이기 때문입니다. XDF 파일에 대 한 자세한 내용은 참조 [는 XDF 만들](https://msdn.microsoft.com/microsoft-r/scaler-data-xdf)합니다.
  
4. 이제 이 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 넣고 _DayOfWeek_ 값이 1에서 7 사이인 정수로 저장합니다.
  
    이렇게 하려면 먼저 SQL Server 데이터 원본을 정의합니다.
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
5. 이름이 같은 테이블이 이미 있는지 확인하고, 있을 경우 테이블을 삭제합니다.
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
6. 테이블을 만들고 **rxDataStep**에 대한 다양한 제품 샘플에서 사용되므로 테스트를 위해 보관해 두면 유용합니다. 이 함수는 두 데이터에서 이미 데이터 원본을 정의 하 고 전달 되는 도중 데이터를 변형할 수를 이동 합니다.
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
            transforms = list( DayOfWeek = as.integer(DayOfWeek),
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
            overwrite = TRUE )
    ```
  
    이 테이블은 꽤 크기 때문에 잠시 기다려야 최종 상태 메시지가 표시됩니다. *Rows Read: 200000, Total Rows Processed: 600000*.
     
7. 계산 컨텍스트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터로 다시 설정합니다.

    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
8. 새 테이블에서 간단한 SQL 쿼리를 사용하여 새 SQL Server 데이터 원본을 만듭니다. 이 정의는 *colInfo* 인수를 사용하여 *DayOfWeek* 열에 대한 요소 수준을 RxSqlServerData에 추가합니다.
  
    ```R
    SqlServerAirDemo <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
9. RxSummary 쿼리에서 데이터의 요약을 검토 하는 한 번 더 호출 합니다.
  
    ```R
    rxSummary(~., data = sqlServerAirDemo)
    ```

## <a name="next-step"></a>다음 단계

[RxDataStep를 사용 하 여 청크 분석 수행](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)

## <a name="previous-step"></a>이전 단계

[데이터 rxImport를 사용 하 여 메모리에 로드](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)



