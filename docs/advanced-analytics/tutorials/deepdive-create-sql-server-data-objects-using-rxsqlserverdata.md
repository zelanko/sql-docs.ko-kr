---
title: RxSqlServerData 개체 만들기
description: 'RevoScaleR 자습서 2: SQL Server에서 R 언어를 사용하여 데이터 개체를 만드는 방법.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7869fc3fc67cb24542223c2300cd7b6ebcf1eb41
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76922566"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>RxSqlServerData를 사용하여 SQL Server 데이터 개체 만들기(SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이것은 SQL Server에서 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)를 사용하는 방법에 대한 [RevoScaleR 자습서 시리즈](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 중 자습서 2에 해당됩니다.

이 자습서는 테이블을 추가하고 데이터를 로드하는 데이터 생성 작업에 이어지는 것입니다. [자습서 2](deepdive-work-with-sql-server-data-using-r.md)에서 DBA가 데이터베이스 및 로그인을 만들었다면 RStudio와 같은 R IDE 또는 **Rgui** 같은 기본 제공 도구를 사용하여 테이블을 추가할 수 있습니다.

R에서 SQL Server에 연결하고 **RevoScaleR** 함수를 사용하여 다음 작업을 수행합니다.

> [!div class="checklist"]
> * 학습 데이터 및 예측용 테이블 만들기
> * 로컬 .csv 파일의 데이터를 사용하여 테이블 로드

샘플 데이터는 학습 및 채점 데이터 세트로 분할된, 시뮬레이션된 신용 카드 사기 데이터(ccFraud 데이터 세트)입니다. 데이터 파일은 **RevoScaleR**에 포함되어 있습니다.

이러한 작업을 완료하려면 R IDE 또는 **Rgui**를 사용합니다. 이 위치에 있는 R 실행 파일을 사용해야 합니다. C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64(해당 도구를 사용하는 경우 Rgui.exe 또는 C:\Program Files\Microsoft\R Client\R_SERVER를 가리키는 경우 R IDE). 이러한 실행 파일이 포함된 [R 클라이언트 워크스테이션](../r/set-up-a-data-science-client.md)을 갖는 것은 이 자습서의 사전 요구 사항으로 간주됩니다.

## <a name="create-the-training-data-table"></a>학습 데이터 테이블 만들기

1. R 변수에 데이터베이스 연결 문자열을 저장합니다. SQL Server에 대한 유효한 ODBC 연결 문자열의 두 가지 예(SQL 로그인을 사용하는 경우와 Windows 통합 인증을 사용하는 경우)는 아래와 같습니다. 

   서버 이름, 사용자 이름 및 암호를 적절하게 수정해야 합니다.

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
  
    서버 인스턴스 및 데이터베이스 이름이 연결 문자열의 일부로 이미 지정되었으므로 두 변수를 결합할 경우 새 테이블의 *정규화된* 이름은 *instance.database.schema.ccFraudSmall*이 됩니다.
  
3.  필요한 경우 *rowsPerRead*를 지정하여 각 배치에서 읽는 데이터 행 수를 제어합니다.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    이 매개 변수는 선택 사항이지만 이 매개 변수를 설정하면 보다 효율적인 계산을 수행할 수 있습니다. **RevoScaleR** 및 **MicrosoftML**의 고급 분석 함수는 대부분은 데이터를 청크로 처리합니다. *rowsPerRead* 매개 변수는 각 청크의 행 수를 결정합니다.
  
    올바른 균형을 찾기 위해 이 설정으로 실험해 보아야 할 수 있습니다. 값이 너무 크면 해당 크기의 청크로 데이터를 처리하는 데 충분한 메모리가 없는 경우 데이터 액세스가 느릴 수 있습니다. 반대로, 일부 시스템에서는 *rowsPerRead* 값이 너무 작은 경우 성능이 느려질 수 있습니다.
  
    초기 값으로 데이터베이스 엔진 인스턴스에서 정의한 기본 일괄 처리 크기를 사용하여 각 청크의 행 수(5,000개 행)를 제어합니다. *sqlRowsPerRead* 변수에 해당 값을 저장합니다.
  
4.  새 데이터 원본 개체에 대한 변수를 정의하고 이전에 정의한 인수를 **RxSqlServerData** 생성자에 전달합니다. 이렇게 하면 데이터 원본 개체가 만들어지기만 하고 채워지지는 않습니다. 데이터 로드는 별도의 단계입니다.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>채점 데이터 테이블 만들기

동일한 단계를 따라 채점 데이터를 저장하는 테이블을 만듭니다.

1. 새 R 변수 *sqlScoreTable*을 만들어 점수 매기기에 사용되는 테이블의 이름을 저장합니다.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. 해당 변수를 **RxSqlServerData** 함수에 대한 인수로 제공하여 두 번째 데이터 원본 개체 *sqlScoreDS*를 정의합니다.
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

R 작업 영역에서 연결 문자열 및 기타 매개 변수를 변수로 이미 정의했으므로 다른 테이블, 뷰 또는 쿼리를 나타내는 새 데이터 원본에 재사용할 수 있습니다.

> [!NOTE]
> 함수는 전체 테이블에 기반을 둔 데이터 원본을 정의할 때 쿼리에 기반을 둔 데이터 원본을 정의할 때와 다른 인수를 사용합니다. SQL Server 데이터베이스 엔진은 쿼리를 다르게 준비해야 하기 때문입니다. 이 자습서의 뒷부분에서는 SQL 쿼리를 기반으로 하여 데이터 원본 개체를 만드는 방법을 알아봅니다.

## <a name="load-data-into-sql-tables-using-r"></a>R을 사용하여 SQL 테이블에 데이터 로드

이제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 만들었으므로 적절한 **Rx** 함수를 사용하여 해당 테이블에 데이터를 로드할 수 있습니다.

**RevoScaleR** 패키지에는 데이터 원본 유형과 관련된 함수가 포함되어 있습니다. 텍스트 데이터의 경우 [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata)를 사용하여 데이터 원본 개체를 생성합니다. Hadoop 데이터, ODBC 데이터 등에서 데이터 원본 개체를 만들기 위한 추가 함수가 있습니다.

> [!NOTE]
> 이 섹션을 수행하려면 데이터베이스에 대한 **DDL 실행** 권한이 있어야 합니다.

### <a name="load-data-into-the-training-table"></a>학습 테이블에 데이터 로드

1. R 변수 *ccFraudCsv*를 만들고 이 변수에 샘플 데이터를 포함하는 CSV 파일의 파일 경로를 할당합니다. 이 데이터 세트는 **RevoScaleR**에 제공됩니다. "sampleDataDir"은 **rxGetOption** 함수의 키워드입니다.
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    **RevoScaleR**의 [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions)와 연결된 GET 메서드인 **rxGetOption**에 대한 호출을 확인하세요. 기본 공유 디렉터리 또는 계산에 사용할 프로세서(코어) 수와 같은 로컬 및 원격 컴퓨팅 컨텍스트와 관련된 옵션을 설정하고 나열하려면 이 유틸리티를 사용합니다.
    
    이 함수는 코드를 실행하는 위치와 관계없이 올바른 라이브러리에서 샘플을 가져옵니다. 예를 들어 SQL Server 및 개발 컴퓨터에서 함수를 실행해 보고 경로가 어떻게 다른지 확인하세요.
  
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
  
3. 이 시점에서 일시 중지하고 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 데이터베이스를 확인하는 것이 좋습니다. 데이터베이스의 테이블 목록을 새로 고칩니다.
  
    로컬 작업 영역에서 R 데이터 개체를 만들었지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서는 테이블이 생성되지 않은 것을 볼 수 있습니다. 텍스트 파일에서 R 변수로 로드된 데이터도 없습니다.
  
4. [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 함수를 호출하여 데이터를 삽입합니다.
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    연결 문자열에 문제가 없다고 가정하면 잠시 후 다음과 같은 결과가 표시됩니다.
  
    *Total Rows written: 10000, Total time: 0.466* *읽은 행: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.577 seconds*
  
5. 테이블 목록을 새로 고칩니다. 각 변수의 데이터 형식이 올바르고 각 변수를 가져왔는지 확인하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 테이블을 마우스 오른쪽 단추로 클릭하고 **상위 1,000개의 행 선택**을 선택할 수도 있습니다.

### <a name="load-data-into-the-scoring-table"></a>채점 테이블에 데이터 로드

1. 채점에 사용되는 데이터 세트를 데이터베이스에 로드하는 단계를 반복합니다.
  
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
  
    - 테이블이 이미 있고 *덮어쓰기* 옵션을 사용하지 않으면 결과가 잘림 없이 삽입됩니다.
  
다시, 연결에 성공하면 완료를 나타내는 메시지와 테이블에 데이터를 기록하는 데 필요한 시간이 표시됩니다.

*Total Rows written: 10000, Total time: 0.384*
*Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.456 seconds*

## <a name="more-about-rxdatastep"></a>RxDataStep에 대한 자세한 정보

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)은 R 데이터 프레임에서 여러 변환을 수행할 수 있는 강력한 함수입니다. rxDataStep을 사용하여 대상에 필요한 표현으로 데이터를 변환할 수도 있습니다(이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).

필요에 따라 **rxDataStep**에 대한 인수에 R 함수를 사용하여 데이터에 대한 변환을 지정할 수 있습니다. 이러한 작업의 예는 이 자습서의 뒷부분에서 제공됩니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [SQL Server 데이터 쿼리 및 수정](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)