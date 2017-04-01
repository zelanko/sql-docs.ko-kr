---
title: "RxSqlServerData를 사용하여 SQL Server 데이터 개체 만들기 | Microsoft Docs"
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
ms.assetid: bcf5f7ff-795b-4815-b163-bcddd496efce
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# RxSqlServerData를 사용하여 SQL Server 데이터 개체 만들기
이제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 만들었으며 데이터 작업에 필요한 권한이 있으므로 서버 및 워크스테이션에서 데이터로 작업할 수 있도록 하는 개체를 R에서 만듭니다.  
  
## SQL Server 데이터 개체 만들기  
이 단계에서는 R을 사용하여 두 개의 테이블을 만들고 채웁니다. 두 테이블에 모두 시뮬레이트된 신용 카드 사기 데이터가 포함됩니다. 한 테이블은 모델 학습에 사용되고 다른 테이블은 점수 매기기에 사용됩니다. 

원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 테이블을 만들려면 **RevoScaleR** 패키지에 제공된 `RxSqlServerData` 함수를 사용합니다.  

> [!TIP]
> R Tools for Visual Studio를 사용하는 도구 모음에서 **R 도구**를 선택하고 **Windows**를 클릭하여 R 변수 디버깅 및 보기에 대한 옵션을 표시하세요.
  
#### 학습 데이터 테이블을 만들려면  
  
1.  R 변수에 데이터베이스 연결 문자열을 제공합니다. 여기서는 SQL Server에 대한 유효한 ODBC 연결 문자열의 두 가지 예(SQL 로그인을 사용하는 경우와 Windows 통합 인증(권장)을 사용하는 경우)를 제공했습니다.

    **SQL 로그인 사용**
    ```R  
    sqlConnString <- "Driver=SQL Server;Server=instance_name; Database=DeepDive;Uid=user_name;Pwd=password"   
    ```

    **Windows 통합 인증 사용**
    ```R  
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
    ```

    인스턴스 이름, 데이터베이스 이름, 사용자 이름 및 암호를 적절하게 수정해야 합니다.  
  
2.  만들려는 테이블의 이름을 지정하고 R 변수에 저장합니다.  
  
    ```R  
    sqlFraudTable <- "ccFraudSmall"       
    ```  
  
    인스턴스 및 데이터베이스 이름이 연결 문자열의 일부로 이미 지정되었으므로 두 변수를 결합할 경우 새 테이블의 *정규화된* 이름은 _instance.database.schema.ccFraudSmall_이 됩니다.  
  
3.  데이터 원본 개체를 인스턴스화하기 전에 추가 매개 변수 *rowsPerRead*를 지정하는 줄을 추가합니다.  *rowsPerRead* 매개 변수는 각 배치에서 읽는 데이터 행 수를 제어합니다.  
  
    ```R  
    sqlRowsPerRead = 5000   
    ```  
  
    이 매개 변수는 선택 사항이지만 메모리 사용량 및 효율적인 계산을 처리하는 데 중요합니다.  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에서 대부분의 향상된 분석 함수는 데이터를 청크로 처리하고 중간 결과를 누적하며, 모든 데이터를 읽은 후 최종 계산을 반환합니다.  
  
    이 매개 변수의 값이 너무 크면 큰 데이터 청크를 효율적으로 처리할 수 있는 메모리가 없기 때문에 데이터 액세스 속도가 느려질 수 있습니다.  일부 시스템에서는 *rowsPerRead* 값이 너무 작은 경우 성능이 느려질 수 있습니다.  
  
    이 연습에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 의해 정의된 배치 프로세스 크기를 사용하여 각 청크의 행 수를 제어하고 해당 값을 *sqlRowsPerRead* 변수에 저장합니다.  큰 데이터 집합으로 작업하는 경우 해당 시스템에서 이 설정을 실험하는 것이 좋습니다.  
  
4.  마지막으로, 새 데이터 원본 개체에 대한 변수를 정의하고 이전에 정의한 인수를 *RxSqlServerData* 생성자에 전달합니다. 이렇게 하면 데이터 원본 개체가 만들어지기만 하고 채워지지는 않습니다.  
  
    ```R  
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable, 
       rowsPerRead = sqlRowsPerRead)  
    ```  

  
#### 점수 매기기 데이터 테이블을 만들려면  

같은 프로세스를 사용하여 점수 매기기 데이터를 저장하는 테이블을 만듭니다.  
  
1.  새 R 변수 *sqlScoreTable*을 만들어 점수 매기기에 사용되는 테이블의 이름을 저장합니다.  
  
    ```R  
    sqlScoreTable <- "ccFraudScoreSmall"  
    ```  
  
2.  해당 변수를 *RxSqlServerData* 함수에 대한 인수로 제공하여 두 번째 데이터 원본 개체 *sqlScoreDS*를 정의합니다.  
  
    ```R   
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead) 
    ```  
  
  
R 작업 영역에서 연결 문자열 및 기타 매개 변수를 변수로 이미 정의했으므로 다른 테이블, 뷰 또는 쿼리에 사용할 새 데이터 원본을 쉽게 만들 수 있습니다. 다른 테이블 이름을 지정하기만 하면 됩니다.  
  
이 자습서의 뒷부분에서는 SQL 쿼리를 기반으로 하여 데이터 원본 개체를 만드는 방법을 알아봅니다.  
  
## R을 사용하여 SQL 테이블에 데이터 로드  
이제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 만들었으므로 적절한 **Rx** 함수를 사용하여 해당 테이블에 데이터를 로드할 수 있습니다.  
  
**RevoScaleR** 패키지에는 다양한 데이터 원본을 지원하는 함수가 포함되어 있습니다. 텍스트 데이터의 경우 *RxTextData*를 사용하여 데이터 원본 개체를 생성합니다. Hadoop 데이터, ODBC 데이터 등에서 데이터 원본 개체를 만들기 위한 추가 함수가 있습니다.  
  
> [!NOTE]  
> 이 섹션을 수행하려면 데이터베이스에 대한 DDL 실행 권한이 있어야 합니다.
  
#### 학습 테이블에 데이터를 로드하려면  
  
1.  R 변수 *ccFraudCsv*를 만들고 이 변수에 Microsoft R에 포함된 샘플 데이터를 포함하는 CSV 파일의 파일 경로를 할당합니다.  
  
    ```R  
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")   
    ```  
  
    유틸리티 함수 *rxGetOption*이 사용되었습니다. 이 함수는 기본 공유 디렉터리, 계산에 사용할 프로세서(코어) 수 등의 로컬 및 원격 계산 컨텍스트와 관련된 옵션을 설정하고 관리하는 데 도움이 되도록 **RevoScaleR** 패키지에 제공됩니다.  이 함수는 코드를 실행하는 위치와 관계없이 올바른 라이브러리에서 샘플을 가져오므로 유용합니다. 예를 들어 SQL Server 및 개발 컴퓨터에서 함수를 실행해 보고 경로가 어떻게 다른지 확인하세요.
  
2.  새 데이터를 저장할 변수를 정의하고 *RxTextData* 함수를 사용하여 텍스트 데이터 원본을 지정합니다.  
  
    ```R  
    inTextData <- RxTextData(file = ccFraudCsv,      colClasses = c(   
        "custID" = "integer", "gender" = "integer", "state" = "integer",   
        "cardholder" = "integer", "balance" = "integer",    
        "numTrans" = "integer",   
        "numIntlTrans" = "integer", "creditLine" = "integer",    
        "fraudRisk" = "integer"))    
    ```  
  
    *colClasses* 인수가 중요합니다. 이 인수를 사용하여 텍스트 파일에서 로드된 데이터의 각 열에 할당할 데이터 형식을 나타냅니다. 이 예제에서는 정수로 처리되는 명명된 열을 제외하고 모든 열이 텍스트로 처리됩니다.  
  
3.  이 시점에서 일시 중지하고 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 데이터베이스를 확인하는 것이 좋습니다.  데이터베이스의 테이블 목록을 새로 고칩니다.  
  
    로컬 작업 영역에서 R 데이터 개체를 만들었지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서는 아직 테이블이 생성되지 않았습니다. 텍스트 파일에서 R 변수로 실제로 로드된 데이터도 없습니다. 
  
4.  이제 *rxDataStep* 함수를 호출하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 데이터를 삽입합니다.  
  
    ```R  
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)   
    ```  
  
    연결 문자열에 문제가 없다고 가정하면 잠시 후 다음과 같은 결과가 표시됩니다.  
  
      *Total Rows written: 10000, Total time: 0.466*
      *Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.577 seconds*  
  
5.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 테이블 목록을 새로 고칩니다. 각 변수의 데이터 형식이 올바르고 각 변수를 가져왔는지 확인하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 테이블을 마우스 오른쪽 단추로 클릭하고 **상위 1000개의 행 선택**을 선택할 수도 있습니다.  
  
#### 점수 매기기 테이블에 데이터를 로드하려면  
  
1.  동일한 단계에 따라 점수 매기기에 사용되는 데이터 집합을 데이터베이스에 로드합니다.  
  
    먼저 원본 파일의 경로를 제공합니다.  
  
    ```R  
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")   
    ```  
  
2.  *RxTextData* 함수를 사용하여 데이터를 가져와 *inTextData* 변수에 저장합니다.  
  
    ```R  
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(   
        "custID" = "integer", "gender" = "integer", "state" = "integer",   
        "cardholder" = "integer", "balance" = "integer",    
        "numTrans" = "integer",   
        "numIntlTrans" = "integer", "creditLine" = "integer"))  
  
    ```  
  
3.  *rxDataStep* 함수를 호출하여 현재 테이블을 새 스키마와 데이터로 덮어씁니다.  
  
    ```R  
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)    
    ```  
  
    -   *inData* 인수는 사용할 데이터 원본을 정의합니다.  
  
    -   *outFile* 인수는 데이터를 저장할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 테이블을 지정합니다.  
  
    -   테이블이 이미 있고 *덮어쓰기* 옵션을 사용하지 않으면 결과가 잘림 없이 삽입됩니다.  
  
다시, 연결에 성공하면 완료를 나타내는 메시지와 테이블에 데이터를 기록하는 데 필요한 시간이 표시됩니다. 

*Total Rows written: 10000, Total time: 0.384*
*Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.456 seconds*  
  
## RxDataStep에 대한 자세한 정보  
*rxDataStep*은 대상에 필요한 표현으로 데이터를 변환하기 위해 R 데이터 프레임에서 여러 변환을 수행할 수 있는 **RevoScaleR** 패키지의 강력한 함수입니다. 이 경우 대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다.  
  
*rxDataStep*에 대한 인수에 R 함수를 사용하여 제외할 열, 새 열 추가 또는 데이터 형식 변경 등 데이터에 대한 변환을 지정할 수도 있습니다. [4단원](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)에서 이러한 작업의 예제를 볼 수 있습니다.  
  
## 다음 단계  
[SQL Server 데이터 쿼리 및 수정&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/query-and-modify-the-sql-server-data-data-science-deep-dive.md)  
  
## 이전 단계  
[1단원: R을 사용하여 SQL Server 데이터 작업&#40;데이터 과학 심층 분석&#41;](../../advanced-analytics/r-services/lesson-1-work-with-sql-server-data-using-r-data-science-deep-dive.md)  
  
