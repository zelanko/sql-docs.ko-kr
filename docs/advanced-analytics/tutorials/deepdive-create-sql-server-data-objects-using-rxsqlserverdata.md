---
title: RevoScaleR RxSqlServerData-SQL Server Machine Learning을 사용 하 여 SQL Server 데이터 개체 만들기
description: SQL Server에서 R 언어를 사용 하 여 데이터 개체를 만드는 방법에 대 한 연습 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cbd6f8bb9fd44be44132fd71e7e8eca3c9625b43
ms.sourcegitcommit: 33712a0587c1cdc90de6dada88d727f8623efd11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53596394"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>RxSqlServerData (RevoScaleR 및 SQL Server 자습서)를 사용 하 여 SQL Server 데이터 개체 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는의 일부인를 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 사용 하는 방법에 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server를 사용 하 여 합니다.

단원 2는 데이터베이스 만들기의 연속: 테이블을 추가 하 고 데이터를 로드 합니다. Dba가 데이터베이스 및 로그인을 만든 경우 [하나 단원](deepdive-work-with-sql-server-data-using-r.md)와 같은 기본 제공 도구, RStudio 등 R IDE를 사용 하 여 테이블을 추가할 수 있습니다 **Rgui**합니다.

R에서 SQL Server에 연결 하 고 사용 하 여 **RevoScaleR** 다음 작업을 수행 하는 함수:

> [!div class="checklist"]
> * 학습 데이터 및 예측에 대 한 테이블 만들기
> * 로컬.csv 파일에서 데이터를 사용 하 여 테이블을 로드 합니다.

샘플 데이터는 학습 및 데이터 집합 점수 매기기로 분할 된 시뮬레이트된 신용 카드 사기 데이터 (ccFraud 데이터 집합). 데이터 파일에 포함 되어 **RevoScaleR**합니다.

R IDE를 사용 하거나 **Rgui** 이러한 taks 완료 합니다. 이 위치에 있는 R 실행 파일을 사용 해야 합니다. C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 (C:\Program Files\Microsoft\R Client\R_SERVER 가리키는 R IDE 든 해당 도구를 사용 하는 경우 두 Rgui.exe). 필요는 [R 클라이언트 워크스테이션](../r/set-up-a-data-science-client.md) 이러한 실행 파일에는이 자습서의 필수 구성 요소 간주 됩니다.

## <a name="create-the-training-data-table"></a>학습 데이터 테이블 만들기

1. R 변수에 데이터베이스 연결 문자열을 저장 합니다. SQL Server에 대 한 다음은 유효한 ODBC 연결 문자열의 두 가지 예제: Windows 통합 인증 및 SQL 로그인을 사용 하 여 합니다. 

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
  
    서버 인스턴스 및 데이터베이스 이름이 이미 지정 되었으므로 연결 문자열의 일부로 두 변수를 결합 하는 경우는 *정규화* 새 테이블의 이름은  *instance.database.schema.ccFraudSmall*합니다.
  
3.  선택적으로 지정할 *rowsPerRead* 각 일괄 처리에서 읽는 데이터 행의 수를 제어 합니다.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    이 매개 변수 선택 사항 이지만 설정 보다 효율적으로 계산 될 수 있습니다. 대부분의 향상 된 분석 함수 **RevoScaleR** 하 고 **MicrosoftML** 데이터 청크를 처리 합니다. 합니다 *rowsPerRead* 매개 변수는 각 청크의 행 수를 결정 합니다.
  
    적절 한 균형을 찾으려면이 설정을 사용 하 여 실험을 해야 합니다. 값을 너무 큰 경우에 데이터 액세스에서 해당 크기의 청크로 데이터를 처리할 충분 한 메모리가 없을 경우 느려질 수 있습니다. 반대로, 일부 시스템의 경우 값 *rowsPerRead* 너무 작은 경우 성능이 저하 될 수 있습니다도 합니다.
  
    초기 값으로 (5,000 개 행) 각 청크의 행 수를 제어 하려면 데이터베이스 엔진 인스턴스에 의해 정의 된 기본 배치 프로세스 크기를 사용 합니다. 변수에 값을 저장할 *sqlRowsPerRead*합니다.
  
4.  새 데이터 원본 개체에 대 한 변수를 정의 하 고 이전에 정의 된 인수를 전달 합니다 **RxSqlServerData** 생성자입니다. 이렇게 하면 데이터 원본 개체가 만들어지기만 하고 채워지지는 않습니다. 데이터를 로드 하는 것은 별도 단계입니다.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>점수 매기기 데이터 테이블을 만들려면

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

연결 문자열 및 기타 매개 변수 R 작업 영역에서 변수로 이미 정의 했으므로, 다른 테이블, 뷰 또는 쿼리를 나타내는 새 데이터 원본에 대 한 다시 사용할 수 있습니다.

> [!NOTE]
> 함수는 쿼리를 기반으로 한 데이터 원본이 아니라 전체 테이블을 기반으로 데이터 원본을 정의하기 위해 여러 인수를 사용합니다. SQL Server 데이터베이스 엔진에서 쿼리를 다르게 준비해야 하기 때문입니다. 이 자습서의 뒷부분에서 SQL 쿼리를 기반으로 데이터 원본을 만드는 방법에 대해 배웁니다.

## <a name="load-data-into-sql-tables-using-r"></a>R을 사용하여 SQL 테이블에 데이터 불러오기

이제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 만들었으므로 적절한 **Rx** 함수를 사용하여 해당 테이블에 데이터를 로드할 수 있습니다.

합니다 **RevoScaleR** 패키지 데이터 원본 형식에 특정 함수를 포함 합니다. 텍스트 데이터를 사용 하 여 [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) 데이터 원본 개체를 생성 합니다. 이밖에도 Hadoop 데이터, ODBC 데이터 등에서 데이터 원본 개체를 만들기 위한 추가 함수들이 있습니다.

> [!NOTE]
> 이 섹션을 진행하려면 데이터베이스에 대한 **DDL 실행** 권한이 필요합니다.

### <a name="load-data-into-the-training-table"></a>학습 테이블에 데이터 로드하기

1. R 변수 *ccFraudCsv*를 만들고 샘플 데이터가 들어있는 CSV 파일의 경로를 변수에 할당합니다. 이 데이터 집합에서 제공 됩니다 **RevoScaleR**합니다. "sampleDataDir" 키워드를 **rxGetOption** 함수입니다.
  
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
  
4. 함수를 호출 하 여 데이터를 삽입할 [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 함수입니다.
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    연결 문자열에 문제가 없다고 가정하면 잠시 후 다음과 같은 결과가 표시됩니다.
  
    *총 쓴 행 수: 10000, 총 시간: 0.466* *읽은 행: 총 행 수, 10000 처리: 10000, total Chunk Time: 0.577 시간 (초)*
  
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
  
    - 테이블이 이미 있고 사용 하지 않는 경우는 *덮어쓰기* 옵션 결과가 잘림 없이 삽입 됩니다.
  
다시, 연결에 성공하면 완료를 나타내는 메시지와 테이블에 데이터를 기록하는 데 필요한 시간이 표시됩니다.

*총 쓴 행 수: 10000, 총 시간: 0.384*
*읽은 행: 총 행 수, 10000 처리: 10000, total Chunk Time: 0.456 시간 (초)*

## <a name="more-about-rxdatastep"></a>RxDataStep에 대한 추가 정보

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)은 R 데이터 프레임에서 여러 변환을 수행할 수 있는 강력한 함수입니다. 데이터를 저장할 곳에 맞게 변환하는 데에도 rxDataStep을 사용할 수 있습니다. 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 맞게 변환했습니다.

또한 **rxDataStep**의 인수로 R 함수를 사용함으로써 데이터의 변환을 지정할 수 있습니다. 이 자습서의 뒷부분에 나오는 이러한 작업의 예로 제공됩니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [SQL Server 데이터 쿼리 및 수정](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)