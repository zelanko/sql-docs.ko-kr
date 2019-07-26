---
title: RevoScaleR RxSqlServerData를 사용 하 여 SQL Server 데이터 개체 만들기
description: SQL Server에서 R 언어를 사용 하 여 데이터 개체를 만드는 방법에 대 한 자습서 연습입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 423a90fe66749a3192c6f03c0efee314b4ceef37
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469756"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>RxSqlServerData를 사용 하 여 SQL Server 데이터 개체 만들기 (SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 단원에서는 SQL Server [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 를 사용 하는 방법에 대 한 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 의 일부입니다.

2 단원에서는 데이터베이스를 만들고, 테이블을 추가 하 고, 데이터를 로드 하는 연속 작업을 수행 합니다. DBA가 데이터베이스를 만들고 [단원 1](deepdive-work-with-sql-server-data-using-r.md)에서 로그인 한 경우 rstudio와 같은 R IDE 또는 **rstudio**와 같은 기본 제공 도구를 사용 하 여 테이블을 추가할 수 있습니다.

R에서 SQL Server에 연결 하 고 **RevoScaleR** 함수를 사용 하 여 다음 작업을 수행 합니다.

> [!div class="checklist"]
> * 학습 데이터 및 예측에 대 한 테이블 만들기
> * 로컬 .csv 파일의 데이터를 사용 하 여 테이블 로드

샘플 데이터는 학습 및 점수 매기기 데이터 집합으로 분할 된, 시뮬레이션 된 신용 카드 사기 데이터 (ccFraud 데이터 집합)입니다. 데이터 파일은 **RevoScaleR**에 포함 되어 있습니다.

R IDE 또는 **Rgui** 를 사용 하 여 이러한 taks를 완료 합니다. 이 위치에 있는 R 실행 파일을 사용 해야 합니다. C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 (해당 도구를 사용 하는 경우 Rgui .exe 또는 C:\Program Files\Microsoft\R Client\R_SERVER를 가리키는 R IDE). 이러한 실행 파일을 포함 하는 [R 클라이언트 워크스테이션](../r/set-up-a-data-science-client.md) 은이 자습서의 필수 구성 요소로 간주 됩니다.

## <a name="create-the-training-data-table"></a>학습 데이터 테이블 만들기

1. 데이터베이스 연결 문자열을 R 변수에 저장 합니다. 다음은 SQL Server에 대 한 유효한 ODBC 연결 문자열의 두 가지 예입니다. 하나는 SQL 로그인을 사용 하 고 다른 하나는 Windows 통합 인증입니다. 

   서버 이름, 사용자 이름 및 암호를 적절 하 게 수정 해야 합니다.

    **SQL 로그인**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>; Database=RevoDeepDive;Uid=<user_name>;Pwd=<password>"
    ```

    **Windows 인증**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>;Database=RevoDeepDive;Trusted_Connection=True"
    ```

2. 만들려는 테이블의 이름을 지정하고 R 변수에 저장합니다.
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    서버 인스턴스와 데이터베이스 이름이 이미 연결 문자열의 일부로 지정 되어 있기 때문에 두 변수를 결합할 때 새 테이블의 정규화 *된 이름은* *ccFraudSmall*가 됩니다.
  
3.  필요에 따라 *Rowsperread* 를 지정 하 여 각 일괄 처리에서 읽을 데이터 행 수를 제어 합니다.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    이 매개 변수는 선택 사항 이지만이 매개 변수를 설정 하면 보다 효율적인 계산을 수행할 수 있습니다. **RevoScaleR** 및 **MicrosoftML** 에서 향상 된 대부분의 분석 함수는 데이터를 청크로 처리 합니다. *Rowsperread* 매개 변수는 각 청크의 행 수를 결정 합니다.
  
    올바른 잔액을 찾으려면이 설정을 시험해 보아야 할 수 있습니다. 값이 너무 크면 해당 크기의 청크로 데이터를 처리 하는 데 충분 한 메모리가 없는 경우 데이터 액세스가 느릴 수 있습니다. 반대로, 일부 시스템에서는 *Rowsperread* 값이 너무 작으면 성능이 저하 될 수도 있습니다.
  
    초기 값으로 데이터베이스 엔진 인스턴스에서 정의한 기본 일괄 처리 크기를 사용 하 여 각 청크의 행 수 (5000 행)를 제어 합니다. *Sqlrowsperread*변수에 해당 값을 저장 합니다.
  
4.  새 데이터 원본 개체에 대 한 변수를 정의 하 고 이전에 정의 된 인수를 **RxSqlServerData** 생성자에 전달 합니다. 이렇게 하면 데이터 원본 개체가 만들어지기만 하고 채워지지는 않습니다. 데이터 로드는 별도의 단계입니다.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>점수 매기기 데이터 테이블 만들기

동일한 단계에 따라 동일한 프로세스를 사용하여 채점 데이터를 보관하는 테이블을 만듭니다.

1. 새 R 변수 *sqlScoreTable*을 만들어 채점에 사용되는 테이블의 이름을 저장합니다.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. 해당 변수를 **RxSqlServerData** 함수에 대한 인수로 제공하여 두 번째 데이터 원본 개체 *sqlScoreDS*를 정의합니다.
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

R 작업 영역에서 연결 문자열 및 기타 매개 변수를 변수로 이미 정의 했으므로 다른 테이블, 뷰 또는 쿼리를 나타내는 새 데이터 원본에 다시 사용할 수 있습니다.

> [!NOTE]
> 함수는 쿼리를 기반으로 한 데이터 원본이 아니라 전체 테이블을 기반으로 데이터 원본을 정의하기 위해 여러 인수를 사용합니다. SQL Server 데이터베이스 엔진에서 쿼리를 다르게 준비해야 하기 때문입니다. 이 자습서의 뒷부분에서 SQL 쿼리를 기반으로 데이터 원본을 만드는 방법에 대해 배웁니다.

## <a name="load-data-into-sql-tables-using-r"></a>R을 사용하여 SQL 테이블에 데이터 불러오기

이제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 만들었으므로 적절한 **Rx** 함수를 사용하여 해당 테이블에 데이터를 로드할 수 있습니다.

**RevoScaleR** 패키지에는 데이터 원본 유형과 관련 된 함수가 포함 되어 있습니다. 텍스트 데이터의 경우 [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) 를 사용 하 여 데이터 원본 개체를 생성 합니다. 이밖에도 Hadoop 데이터, ODBC 데이터 등에서 데이터 원본 개체를 만들기 위한 추가 함수들이 있습니다.

> [!NOTE]
> 이 섹션을 진행하려면 데이터베이스에 대한 **DDL 실행** 권한이 필요합니다.

### <a name="load-data-into-the-training-table"></a>학습 테이블에 데이터 로드하기

1. R 변수 *ccFraudCsv*를 만들고 샘플 데이터가 들어있는 CSV 파일의 경로를 변수에 할당합니다. 이 데이터 집합은 **RevoScaleR**에 제공 됩니다. "SampleDataDir"는 **Rxgetoption** 함수의 키워드입니다.
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    **rxGetOption**함수가 호출된 것을 확인하십시오. 이 함수는 **RevoScaleR**에 있는 [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions)에 관련된 GET 메서드입니다. 이 유틸리티를 사용하여 기본 공유 디렉토리나 계산에 사용할 코어의 숫자와 같은 로컬 및 원격 계산 환경에 대한 설정을 변경하거나 확인하십시오.
    
    특히, 이 호출은 코드를 실행하는 위치에 관계없이 올바른 라이브러리에서 샘플을 가져옵니다. 예를 들어 SQL Server 및 개발 컴퓨터에서 함수를 실행해 보고 경로가 어떻게 다른지 확인해보세요.
  
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
  
3. 이 시점에서 잠시 멈추고 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 데이터베이스를 볼 수 있습니다. 데이터베이스의 테이블 목록을 새로 고칩니다.
  
    R 데이터 개체를 로컬 환경에서 생성했으므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에는 테이블이 생성되지 않았음을 확인할 수 있습니다. 또한, 데이터가 텍스트 파일로부터 R 변수에 로드되지 않았습니다.
  
4. [Rxdatastep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 함수 함수를 호출 하 여 데이터를 삽입 합니다.
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    연결 문자열에 문제가 없다고 가정하면 잠시 후 다음과 같은 결과가 표시됩니다.
  
    *작성 된 총 행: 1만, 총 시간:*  0.466*행 읽기: 1만, 총 처리 된 행: 1만, 총 청크 시간: 0.577 초*
  
5. 테이블 목록을 새로 고칩니다. 각 변수가 올바른 데이터 형식을 갖고 성공적으로 가져왔는지 확인하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 테이블을 마우스 오른쪽 단추로 클릭하고 **상위 1000개 행 선택**을 선택합니다.

### <a name="load-data-into-the-scoring-table"></a>채점 테이블에 데이터 로드하기

1. 모델 평가에 쓰일 데이터 집합을 데이터베이스에 로드하기 위해 아래 단계를 반복합니다.
  
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
  
    - 테이블이 이미 있고 *덮어쓰기* 옵션을 사용 하지 않는 경우에는 결과가 잘림 없이 삽입 됩니다.
  
다시, 연결에 성공하면 완료를 나타내는 메시지와 테이블에 데이터를 기록하는 데 필요한 시간이 표시됩니다.

*작성 된 총 행: 1만, 총 시간: 0.384*
행읽기 *: 1만, 총 처리 된 행: 1만, 총 청크 시간: 0.456 초*

## <a name="more-about-rxdatastep"></a>RxDataStep에 대한 추가 정보

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)은 R 데이터 프레임에서 여러 변환을 수행할 수 있는 강력한 함수입니다. 데이터를 저장할 곳에 맞게 변환하는 데에도 rxDataStep을 사용할 수 있습니다. 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 맞게 변환했습니다.

또한 **rxDataStep**의 인수로 R 함수를 사용함으로써 데이터의 변환을 지정할 수 있습니다. 이 자습서의 뒷부분에 나오는 이러한 작업의 예로 제공됩니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [SQL Server 데이터 쿼리 및 수정](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)