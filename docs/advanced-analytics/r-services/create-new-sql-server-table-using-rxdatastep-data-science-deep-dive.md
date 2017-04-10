---
title: "RxDataStep을 사용하여 새 SQL Server 테이블 만들기(데이터 과학 심층 분석) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# RxDataStep을 사용하여 새 SQL Server 테이블 만들기(데이터 과학 심층 분석)
이 단원에서는 메모리 내 데이터 프레임, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컨텍스트 및 로컬 파일 간에 데이터를 이동하는 방법을 알아봅니다.  
  
> [!NOTE]  
> 이 단원에서는 다른 데이터 집합을 사용합니다. 항공사 지연 데이터 집합은 기계 학습 실험에 널리 사용되는 공용 데이터 집합입니다. 방금 R을 시작한 경우, 이 데이터 집합은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]으로 게시된 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에 대한 다양한 제품 샘플에서 사용되므로 테스트를 위해 보관해 두면 유용합니다. 이 예제에 필요한 데이터 파일은 다른 제품 샘플과 같은 디렉터리에 있습니다.  
  
## 로컬 데이터에서 SQL Server 테이블 만들기  
이 자습서의 첫 번째 단원에서는 *RxTextData* 함수를 사용하여 텍스트 파일에서 R로 데이터를 가져온 다음 *RxDataStep* 함수를 사용하여 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 이동했습니다.  
  
이 단원에서는 다른 접근 방식을 사용하고 [XDF 형식](https://en.wikipedia.org/wiki/Extensible_Data_Format)으로 저장된 파일에서 데이터를 가져옵니다. XDF 형식은 고차원 데이터용으로 개발된 XML 표준입니다. 또한 행 및 열 처리와 분석을 최적화하는 R 인터페이스가 포함된 이진 파일 형식입니다.  XDF 형식을 사용하여 데이터를 이동하고 분석에 유용한 데이터의 하위 집합을 저장할 수 있습니다.
  
XDF 파일을 사용하여 데이터에 대해 몇 가지 간단한 변환을 수행한 후 변환된 데이터를 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 저장합니다.  
  
> [!NOTE]  
> 이 단계를 수행하려면 DDL 권한이 필요합니다.  
  
1.  계산 컨텍스트를 로컬 워크스테이션으로 설정합니다.  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
2.  *RxXdfData* 함수를 사용하여 새 데이터 원본 개체를 정의합니다. XDF 데이터 원본의 경우 데이터 파일의 경로만 지정하면 됩니다.  텍스트 변수를 사용하여 파일 경로를 지정할 수 있지만, 이 경우 샘플 데이터 파일(AirlineDemoSmall.xdf)이 *rxGetOption* 함수에서 반환된 디렉터리에 있으므로 유용한 바로 가기가 있습니다.
  
    ```R  
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))   
    ```  
  
  
3.  메모리 내 데이터에서 *rxGetVarInfo*를 호출하여 데이터 집합 요약을 확인합니다.  
  
    ```R  
    rxGetVarInfo(xdfAirDemo)    
    ```  
  
**결과**  
  
*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*   
*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*   
*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*  

> [!NOTE]
> 
> XDF 파일로 데이터를 로드하기 위해 다른 함수를 호출할 필요가 없으며 데이터에서 즉시 *rxGetVarInfo*를 호출할 수 있다는 사실을 알아차리셨나요? XDF가 RevoScaleR에 대한 기본 임시 저장 방법이기 때문입니다. XDF 파일에 대한 자세한 내용은 [ScaleR Getting Started Guide](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-transform#using-the-data-step-to-create-an-xdf-file-from-a-data-frame)(ScaleR 시작 가이드)를 참조하세요. 
  
4.  이제 이 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 넣고 _DayOfWeek_ 값이 1에서 7 사이인 정수로 저장합니다.  
  
    이렇게 하려면 먼저 SQL Server 데이터 원본을 정의합니다.  
  
    ```R  
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)   
    ```  
  
5.  이름이 같은 테이블이 있는지 확인하고, 있을 경우 테이블을 삭제합니다.  
  
    ```R  
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)    
    ```  
  
6.  테이블을 만들고 `rxDataStep`을 사용하여 데이터를 로드합니다.  
  
    ```R  
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,    
            transforms = list( DayOfWeek = as.integer(DayOfWeek),   
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),   
            overwrite = TRUE )    
    ```  
  
7.  계산 컨텍스트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터로 다시 설정합니다.  
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
  
8.  간단한 SQL 문을 사용하여 데이터 하위 집합을 정의합니다.  
  
    ```R    
    SqlServerAirDemo <- RxSqlServerData(  
        sqlQuery = "SELECT * FROM AirDemoSmallTest",      
        connectionString = sqlConnString,   
        rowsPerRead = 50000,      
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))    
    ```  
  
9. *rxSummary*를 호출하여 쿼리의 데이터 요약을 검토합니다.  
  
    ```R  
    rxSummary(~., data = sqlServerAirDemo)   
    ```  
  
## 다음 단계  
[RxDataStep을 사용하여 청크 분석 수행&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/perform-chunking-analysis-using-rxdatastep-data-science-deep-dive.md)  
  
## 이전 단계  
[rxImport를 사용하여 메모리에 데이터 로드&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/load-data-into-memory-using-rximport-data-science-deep-dive.md)  
  
## 관련 항목:  
[데이터 과학 심층 분석: RevoScaleR 패키지 사용](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
