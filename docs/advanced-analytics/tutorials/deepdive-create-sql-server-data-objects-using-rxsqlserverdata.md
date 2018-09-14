---
title: RxSqlServerData(SQL과 R 심층 분석)를 사용하여 SQL Server 데이터 개체 만들기 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e15c3e7c13c1be4f524c25bb1cec6da3c8e20c7e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203465"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-and-r-deep-dive"></a>RxSqlServerData(SQL과 R 심층 분석)를 사용하여 SQL Server 데이터 개체 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)과 SQL Server를 함께 쓰는 방법에 대한 데이터 과학 심층 분석 자습서의 일부입니다.

지금까지 데이터를 다루기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 만들고 필요한 권한을 얻었습니다. 이 단계에서는 데이터를 다루는 데 쓸 수 있는 몇 개체를 R로 만들겠습니다.

## <a name="create-the-sql-server-data-objects"></a>SQL Server 데이터 개체 만들기

이 단계에서는 두 개의 테이블을 만들고 채우기 위해 **RevoScaleR** 패키지의 함수를 사용합니다. 하나는 모델을 훈련하는 데 사용하고, 다른 테이블은 모델을 평가하는 데 사용됩니다. 두 테이블은 가상의 신용 카드 사기 데이터를 포함합니다. 

원격 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 테이블을 만들기 위해 **RxSqlServerData** 함수를 호출하십시오.

> [!TIP]
> R Tools for Visual Studio를 사용하는 경우, 도구 모음에서 **R Tools**를 선택하고 **Windows**를 클릭하여 R 변수를 확인하거나 디버깅할 때 사용할 수 있는 옵션을 확인하세요.

### <a name="create-the-training-data-table"></a>학습 데이터 테이블 만들기

1. 데이터베이스 연결 문자열을 R 변수에 저장하십시오. 다음은 SQL Server를 위한 유효한 ODBC 연결 문자열의 두 가지 예시입니다. SQL 로그인과 Windows 통합 인증

    **SQL 로그인**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name; Database=DeepDive;Uid=user_name;Pwd=password"
    ```

    **Windows 인증**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
    ```

    인스턴스 이름, 데이터베이스 이름, 사용자 이름 및 암호를 적절하게 수정해야 합니다.
  
2. 만들려는 테이블의 이름을 지정하고 R 변수에 저장합니다.
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    인스턴스 및 데이터베이스 이름이 연결 문자열의 일부로 이미 지정되었으므로 두 변수를 결합할 경우 새 테이블의 *정규화된* 이름은 _instance.database.schema.ccFraudSmall_이 됩니다.
  
3.  데이터 원본 개체를 인스턴스화하기 전에 추가 매개 변수 *rowsPerRead*를 지정하는 줄을 추가합니다.  *rowsPerRead* 매개 변수는 각 배치에서 읽는 데이터 행 수를 제어합니다.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    이 매개 변수는 선택 사항이지만 메모리 사용 및 효율적인 계산을 처리하는 데 중요합니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에 포함된 대부분의 고급 분석 함수는 데이터를 한 번에 처리하고 중간 결과를 저장하면서 모든 데이터를 읽은 후 최종 계산 결과를 반환합니다.
  
    이 매개 변수의 값이 너무 크면 큰 데이터 묶음을 효율적으로 처리할 수 있는 메모리가 없기 때문에 데이터 액세스 속도가 느려질 수 있습니다. 일부 시스템에서는 *rowsPerRead* 값이 너무 작은 경우 성능이 느려질 수 있습니다. 따라서 큰 데이터로 작업하는 경우엔 시스템에서 이 설정값을 시험해보는 것이 좋습니다.
  
    이 과정을 하는 동안에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 정의된 기본 일괄 처리 프로세스 수로 각 묶음의 행의 갯수를 조정하세요. 해당 값을 `sqlRowsPerRead` 변수에 저장합니다.
  
4.  마지막으로, 새 데이터 원본 개체에 대한 변수를 정의하고 이전에 정의한 인수를 RxSqlServerData 생성자에 전달합니다. 이렇게 하면 데이터 원본 개체가 만들어지기만 하고 채워지지는 않습니다.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

#### <a name="to-create-the-scoring-data-table"></a>모델 평가 데이터 테이블 만들기

동일한 단계에 따라 동일한 프로세스를 사용하여 채점 데이터를 보관하는 테이블을 만듭니다.

1. 새 R 변수 *sqlScoreTable*을 만들어 모델을 평가하는 데에 사용되는 테이블의 이름을 저장합니다.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. 이 변수를 RxSqlServerData 함수의 인수로 넘겨 두 번째 데이터 원본 개체인 *sqlScoreDS*를 정의합니다.
  
    ```R
    sqlScoreDS \<- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

이미 R 작업 영역에서 연결 문자열 및 다른 매개 변수를 변수로 정의했으므로 여러 테이블, 뷰 또는 쿼리를 위한 새 데이터 원본을 만드는 것은 간단합니다.

> [!NOTE]
> 함수는 쿼리를 기반으로 데이터 원본에 대 한 보다는 전체 테이블을 기반으로 데이터 원본을 정의 하기 위해 서로 다른 인수를 사용 합니다. 즉, SQL Server 데이터베이스 엔진 쿼리를 다르게 준비 해야 합니다. 이 자습서의 뒷부분에 나오는 SQL 쿼리를 기반으로 하는 데이터 원본 개체를 만드는 방법을 배웁니다.

## <a name="load-data-into-sql-tables-using-r"></a>R을 사용 하 여 SQL 테이블에 데이터를 로드 합니다.

이제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 만들었으므로 적절한 **Rx** 함수를 사용하여 해당 테이블에 데이터를 로드할 수 있습니다.

**RevoScaleR** 패키지에는 다양한 데이터 원본을 지원하는 함수가 있습니다. 텍스트 데이터의 경우 [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) 를 사용해서 데이터 원본 개체를 생성합니다. Hadoop 데이터, ODBC 데이터 등에서 데이터 원본 개체를 만들기 위한 추가 함수들이 있습니다.

> [!NOTE]
> 이 섹션에 대 한 있어야 **DDL 실행** 데이터베이스에 대 한 권한이 있습니다.

### <a name="load-data-into-the-training-table"></a>학습 테이블에 데이터 로드하기

1. R 변수 *ccFraudCsv*를 만들고 샘플 데이터를 포함하는 CSV 파일의 경로를 변수에 할당합니다.
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    에 대 한 호출을 확인할 **rxGetOption**, GET 메서드가 관련 된 [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions) 에 **RevoScaleR**합니다. 이 유틸리티를 사용 하 여 설정 하 고 기본 공유 디렉터리 또는 계산에 사용할 (코어) 프로세서 수 등의 로컬 및 원격 계산 컨텍스트에 관련 된 옵션 목록.
    
    이 특정 한 호출 코드를 실행 중인에 관계 없이 올바른 라이브러리에서 샘플을 가져옵니다. 예를 들어 SQL Server 및 개발 컴퓨터에서 함수를 실행해 보고 경로가 어떻게 다른지 확인하세요.
  
2. 새 데이터를 저장할 변수를 정의하고 **RxTextData** 함수를 사용하여 텍스트 데이터 원본을 지정합니다.
  
    ```R
    inTextData <- RxTextData(file = ccFraudCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer",
        "fraudRisk" = "integer"))
    ```
  
    *colClasses* 인수가 중요합니다. 이 인수를 사용하여 텍스트 파일에서 로드된 데이터의 각 열에 할당할 데이터 형식을 나타냅니다. 이 예제에서는 정수로 처리되는 명명된 열을 제외하고 모든 열이 텍스트로 처리됩니다.
  
3. 이 시점에서 잠시 멈추고 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 데이터베이스를 볼 수 있습니다.  데이터베이스의 테이블 목록을 새로 고칩니다.
  
    즉, 로컬 작업 영역에서 R 데이터 개체를 만든 있지만 테이블 만들지 않은에서 볼 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다. 또한, 텍스트 파일에서 R 변수에 데이터가 로드되지 않았습니다.
  
4. 이제 [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 함수를 호출하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 데이터를 삽입합니다.
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
  
    연결 문자열에 문제가 없다고 가정하면 잠시 후 다음과 같은 결과가 표시됩니다.
  
      *Total Rows written: 10000, Total time: 0.466*

      *Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.577 seconds*
  
5. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 테이블 목록을 새로 고칩니다. 각 변수가 올바른 데이터 형식을 갖고 성공적으로 가져왔는지 확인하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 테이블을 마우스 오른쪽 단추로 클릭하고 **상위 1000개 행 선택**을 선택합니다.

### <a name="load-data-into-the-scoring-table"></a>채점 테이블에 데이터 로드하기

1. 데이터베이스에 대 한 평가에 사용 되는 데이터 집합을 로드 하는 단계를 반복 합니다.
  
    먼저 원본 파일의 경로를 제공합니다.
  
    ```R
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")
    ```
  
2. **RxTextData** 함수를 사용하여 데이터를 가져와 *inTextData*변수에 저장합니다.
  
    ```R
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer"))
    ```
  
3.  **rxDataStep** 함수를 호출하여 현재 테이블을 새 스키마와 데이터로 덮어씁니다.
  
    ```R
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)
    ```
  
    - *inData* 인수는 사용할 데이터 원본을 정의합니다.
  
    - *outFile* 인수는 데이터를 저장할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 테이블을 지정합니다.
  
    - 테이블이 이미 존재 하 고 사용 하지 않는 경우는 *덮어쓰기* 옵션을 결과가 잘림 없이 삽입 됩니다.
  
다시, 연결에 성공하면 완료를 나타내는 메시지와 테이블에 데이터를 기록하는 데 필요한 시간이 표시됩니다.

*Total Rows written: 10000, Total time: 0.384*

*Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.456 seconds*

## <a name="more-about-rxdatastep"></a>RxDataStep에 대한 추가 정보

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) R 데이터 프레임에서 여러 변환을 수행할 수 있는 강력한 함수입니다. 데이터를 대상에 필요한 표현으로 변환 rxDataStep을 사용할 수도 있습니다:이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.

에 대 한 인수에서 R 함수를 사용 하 여 데이터에 대해 변환을 지정할 수는 필요에 따라 **rxDataStep**합니다. 이 자습서의 뒷부분에 나오는 이러한 작업의 예로 제공 됩니다.

## <a name="next-step"></a>다음 단계

[SQL Server 데이터 쿼리 및 수정](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)

## <a name="previous-step"></a>이전 단계

[R을 사용하여 SQL Server 데이터 작업하기](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
