---
title: sqlrutils를 사용하여 저장 프로시저를 만드는 방법 | Microsoft 문서
ms.custom: ''
ms.date: 12/16/2016
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 8d451a353e9bcd1468b1ebea4920182efaead182
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="create-a-stored-procedure-using-sqlrutils"></a>저장 프로시저를 사용 하 여 sqlrutils 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 R 코드를 T-SQL 저장 프로시저 실행을 변환 하기 위한 단계를 설명 합니다. 최상의 결과를 얻으려면 모든 입력을 매개 변수화할 수 있도록 코드를 약간 수정해야 할 수 있습니다.

## <a name="bkmk_rewrite"></a>1단계. R 스크립트를 다시 작성

최상의 결과 단일 함수로 캡슐화 하 여 R 코드를 다시 작성 해야 합니다.

함수에서 사용 되는 모든 변수는 함수 내에 정의 되어야 합니다 또는 입력된 매개 변수로 정의 되어야 합니다. 참조는 [샘플 코드](#samples) 이 문서의 내용입니다.

또한 R 함수에 대 한 입력된 매개 변수 될 때문에 SQL의 입력된 매개 변수 저장 프로시저를 입 / 출력 준수 다음 형식 요구 사항을 확인 해야 합니다.

### <a name="inputs"></a>입력

입력 매개 변수 중 하나의 데이터 프레임만 있을 수 있습니다.

함수의 다른 모든 입력 매개 변수뿐만 아니라 데이터 프레임 내의 개체는 다음과 같은 R 데이터 형식이어야 합니다.
- POSIXct
- numeric
- character
- integer
- 논리
- raw

입력 형식이 위 형식 중 하나가 아닌 경우 직렬화하고 *raw*로 함수에 전달해야 합니다. 이 경우 입력을 역직렬화하는 코드도 함수에 있어야 합니다.

### <a name="outputs"></a>출력

함수는 다음 중 하나를 출력할 수 있습니다.

- 지원되는 데이터 형식을 포함하는 데이터 프레임. 데이터 프레임의 모든 개체는 지원되는 데이터 형식 중 하나를 사용해야 합니다.
- 하나의 데이터 프레임만 포함하는 명명된 목록. 목록의 모든 멤버는 지원되는 데이터 형식 중 하나를 사용해야 합니다.
- 함수에서 결과를 반환하지 않는 경우 NULL

## <a name="step-2-generate-required-objects"></a>2단계. 필요한 개체를 생성 합니다.

R 코드 그룹이 정리 되 고 단일 함수로 호출할 수 있습니다, 후에 함수에 사용 합니다는 **sqlrutils** 입력 및 출력에서 실제로 작성 하는 생성자에 전달 될 수 있는 폼을 준비 하는 패키지는 저장된 프로시저입니다.

**sqlrutils** 입력된 데이터 스키마 및 유형을 정의 하 고 출력 데이터 스키마 및 유형을 정의 하는 함수를 제공 합니다. 또한 R 개체는 필요한 출력 형식으로 변환할 수 있는 기능을 포함 합니다. 코드를 사용 하는 데이터 형식에 따라 필요한 개체를 만드는 데 여러 함수 호출을 할 수 있습니다.

### <a name="inputs"></a>입력

사용자 함수는 입력을 사용 하는 경우 각 입력에 대해 다음 함수를 호출 합니다.

- `setInputData` 입력이 데이터 프레임
- `setInputParameter` 다른 모든 입력된 형식에 대 한

나중에 인수로 전달 합니다 R 개체를 만들 각 함수 호출을 수행 하면 `StoredProcedure`, 전체 저장된 프로시저를 만듭니다.

### <a name="outputs"></a>출력

**sqlrutils** SQL Server에 필요한 data.frame 목록을 같은 개체 R 변환에 대 한 여러 기능을 제공 합니다.
함수가 데이터 프레임을 목록에 먼저 래핑하지 않고 직접 출력하는 경우 이 단계를 건너뛸 수 있습니다.
또한 경우 건너뛸 수 있습니다 변환이이 단계 함수가 NULL을 반환 합니다.

때 목록을 변환 하거나 목록에서 특정 항목을 가져오기 이러한 함수를 선택 합니다.

- `setOutputData` 변수를 목록에서 가져올 데이터 프레임인 경우
- `setOutputParameter` 목록의 다른 모든 멤버에 대 한

나중에 인수로 전달 합니다 R 개체를 만들 각 함수 호출을 수행 하면 `StoredProcedure`, 전체 저장된 프로시저를 만듭니다.

## <a name="step-3-generate-the-stored-procedure"></a>3단계. 저장된 프로시저를 생성 합니다.

모든 입력 및 출력 매개 변수 준비 되 면 확인에 대 한 호출에서 `StoredProcedure` 생성자입니다.

**사용법**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

을 설명 하기 위해 명명 된 저장된 프로시저를 만드는 한다고 가정해 보십시오 **sp_rsample** 이러한 매개 변수를 사용 합니다.

- 기존 함수를 사용 하 여 **foosql**합니다. 함수 R 함수에서 기존 코드 기반 **foo**에 설명 된 대로 요구 사항을 충족 하는 함수를은 있지만 [이 여기서](#bkmk_rewrite)와 업데이트 된 기능을 명명 된  **foosql**합니다.
- 데이터 프레임을 사용 하 여 **queryinput** 입력으로
- R 변수 이름으로 데이터 프레임을 출력으로 생성 **sqloutput**
- 파일로 T-SQL 코드를 만들려는 `C:\Temp` 폴더, SQL Server Management Studio를 사용 하 여 나중에 실행할 수 있도록

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> 파일 시스템에 파일을 작성 하는 때문에 데이터베이스 연결을 정의 하는 인수를 생략할 수 있습니다.

함수의 출력은 SQL Server 2016 (R Services 필요) 또는 SQL Server 2017 (R 사용 하 여 컴퓨터 학습 서비스 필요)의 인스턴스에서 실행 될 수 있는 T-SQL 저장 프로시저. 

추가 예제를 호출 하 여 패키지 도움말 참조 `help(StoredProcedure)` R 환경에서 합니다.

## <a name="step-4-register-and-run-the-stored-procedure"></a>4단계. 등록 하 고 저장된 프로시저 실행

두 가지 방법으로 저장된 프로시저를 실행할 수 있습니다.

- T-SQL, SQL Server 2016 또는 SQL Server 2017 인스턴스로 연결을 지 원하는 모든 클라이언트에서 사용 하 여
- R 환경에서

두 방법 모두 저장된 프로시저를 사용 하려는 데이터베이스에 저장된 프로시저에 등록 해야 합니다.

### <a name="register-the-stored-procedure"></a>저장된 프로시저를 등록

R을 사용 하 여 저장된 프로시저를 등록할 수 있습니다 또는 T-SQL에서 CREATE PROCEDURE 문을 실행할 수 있습니다.

- T-SQL을 사용 합니다.  T-SQL에 익숙해지기 인 경우 SQl Server Management Studio (또는 SQL DDL 명령을 실행할 수 있는 다른 모든 클라이언트)를 열고 여 준비 하는 코드를 사용 하 여 CREATE PROCEDURE 문을 실행 하 고는 `StoredProcedure` 함수입니다.
- 오른쪽을 사용 하 여 여전히 R 환경에 있는 동안 사용할 수 있습니다는 `registerStoredProcedure` 함수 **sqlrutils** 데이터베이스와 저장된 프로시저를 등록 합니다.

  예를 들어 저장된 프로시저를 등록할 수 있습니다 **sp_rsample** 인스턴스 및 데이터베이스에 정의 된 *sqlConnStr*, R 호출 하 여:

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> 것 R 또는 SQL을 사용, 새 데이터베이스 개체를 만들 수 있는 권한이 있는 계정을 사용 하는 문을 실행 해야 합니다.

### <a name="run-using-sql"></a>SQL을 사용 하 여 실행

저장된 프로시저를 만든 후 T-SQL를 지 원하는 모든 클라이언트를 사용 하 여 SQL 데이터베이스에 연결을 열고 저장된 프로시저에 필요한 모든 매개 변수에 대 한 값을 전달 합니다.

### <a name="run-using-r"></a>R을 사용 하 여 실행

대신 SQL Server에서에서 R 코드에서 저장된 프로시저를 실행 하려는 경우 몇 가지 추가 준비가 필요 합니다. 예를 들어 저장된 프로시저는 입력된 값을 필요한 경우에 함수가 실행 될 수 하 고 다음 R 코드에서 저장된 프로시저에 해당 개체를 전달 하기 전에 이러한 입력된 매개 변수를 설정 해야 합니다.

준비 된 SQL 저장 프로시저 호출의 전체 프로세스는 다음과 같습니다.

1. `getInputParameters` 를 호출하여 입력 매개 변수 개체 목록을 가져옵니다.
2. 각 입력 매개 변수에 대해 `$query` 를 정의하거나 `$value` 를 설정합니다.
3. `executeStoredProcedure` 를 사용하여 R 개발 환경에서 저장 프로시저를 실행하고 설정한 입력 매개 변수 개체 목록을 전달합니다.

## <a name = "samples"></a>예제

이 예제는 이전 및 이후 버전의 SQL Server 데이터베이스에서 데이터를 가져오는 데이터에 몇 가지 변환을 수행 하 고 다른 데이터베이스에 저장 하는 R 스크립트.

이 간단한 예는 R 코드를 저장된 프로시저로 변환 하는 쉽게 수행할 수 있도록 다시 정렬할 수를 설명 하기 위해서만 사용 됩니다.

### <a name="before-code-preparation"></a>코드 준비 하기 전에


```R
sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineSrc;Trusted_Connection=Yes;"
  
sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineTest;Trusted_Connection=Yes;"
  
sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"
  
dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
xFunc <- function(data) {
    data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
    return(data)
    }
  
xVars <- c("CRSDepTime")
  
sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
rxOpen(dsSqlFrom)
rxOpen(dsSqlTo)
  
if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo))   {
    rxSqlServerDropTable("cleanData")}
  
rxDataStep(inData = dsSqlFrom, 
     outFile = dsSqlTo,
     transformFunc = xFunc,
     transformVars = xVars,
     overwrite = TRUE)
```

> [!NOTE]
> 
> ODBC 연결을 사용 하는 경우 호출 하는 대신는 *RxSqlServerData* 함수를 사용 하 여 연결을 열어야 *rxOpen* 전에 데이터베이스에 대 한 작업을 수행할 수 있습니다.


### <a name="after-code-preparation"></a>코드 준비 후

업데이트 된 버전에서 첫 번째 줄 함수 이름을 정의합니다. 원래 R 솔루션에서 다른 모든 코드는 해당 함수의 부분이 됩니다.

```R
myetl1function <- function() { 
   sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=Airline01;Trusted_Connection=Yes;"
   sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer02;Database=Airline02;Trusted_Connection=Yes;"
    
   sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"

   dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
   dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
   xFunc <- function(data) {
     data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
     return(data)}
  
   xVars <- c("CRSDepTime")
  
   sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
   if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo)) {rxSqlServerDropTable("cleanData")}
  
   rxDataStep(inData = dsSqlFrom, 
        outFile = dsSqlTo,
        transformFunc = xFunc,
        transformVars = xVars,
        overwrite = TRUE)
   return(NULL)
}
```

> [!NOTE]
> 
> ODBC 연결을 코드의 일부로 명시적으로 열 필요는 없지만 **sqlrutils**를 사용하려면 ODBC 연결이 필요합니다.

## <a name="see-also"></a>관련 항목:

[sqlrutils를 사용하여 저장 프로시저 생성](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)


