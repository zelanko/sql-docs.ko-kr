---
title: Sqlrutils를 사용 하 여 저장 프로시저를 만드는 방법
description: SQL Server의 sqlrutils R 패키지를 사용 하 여 R 언어 코드를 저장 프로시저에 인수로 전달할 수 있는 단일 함수로 묶을 수 있습니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0713a126a237f20b2de4e3b16225bb9e5ae26307
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345573"
---
# <a name="create-a-stored-pprocedure-using-sqlrutils"></a>Sqlrutils를 사용 하 여 저장 된 pProcedure 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 T-sql 저장 프로시저로 실행 되도록 R 코드를 변환 하는 단계를 설명 합니다. 최상의 결과를 얻으려면 모든 입력을 매개 변수화할 수 있도록 코드를 약간 수정해야 할 수 있습니다.

## <a name="bkmk_rewrite"></a>1단계. R 스크립트 재작성

최상의 결과를 위해서는 단일 함수로 캡슐화 하기 위해 R 코드를 다시 작성 해야 합니다.

함수에서 사용 하는 모든 변수는 함수 내에서 정의 되거나 입력 매개 변수로 정의 되어야 합니다. 이 문서의 [샘플 코드](#samples) 를 참조 하세요.

또한 R 함수의 입력 매개 변수는 SQL 저장 프로시저의 입력 매개 변수가 되기 때문에 입력 및 출력이 다음 형식 요구 사항을 준수 하는지 확인 해야 합니다.

### <a name="inputs"></a>입력

입력 매개 변수 중 하나의 데이터 프레임만 있을 수 있습니다.

함수의 다른 모든 입력 매개 변수뿐만 아니라 데이터 프레임 내의 개체는 다음과 같은 R 데이터 형식이어야 합니다.
- POSIXct
- NUMERIC
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

## <a name="step-2-generate-required-objects"></a>2단계. 필수 개체 생성

R 코드가 정리 되 고 단일 함수로 호출 될 수 있는 경우 **sqlrutils** 패키지의 함수를 사용 하 여 실제로 저장 프로시저를 작성 하는 생성자에 전달 될 수 있는 형식으로 입력 및 출력을 준비 합니다.

**sqlrutils** 는 입력 데이터 스키마와 유형을 정의 하 고 출력 데이터 스키마와 유형을 정의 하는 함수를 제공 합니다. 또한 R 개체를 필요한 출력 형식으로 변환할 수 있는 함수를 포함 합니다. 코드에서 사용 하는 데이터 형식에 따라 여러 함수 호출을 수행 하 여 필요한 개체를 만들 수 있습니다.

### <a name="inputs"></a>입력

함수에서 입력을 사용 하는 경우 각 입력에 대해 다음 함수를 호출 합니다.

- `setInputData`입력이 데이터 프레임인 경우
- `setInputParameter`기타 모든 입력 형식

각 함수를 호출 하는 경우 나중에에 `StoredProcedure`인수로 전달 하 여 전체 저장 프로시저를 만드는 R 개체가 만들어집니다.

### <a name="outputs"></a>출력

**sqlrutils** 는 목록 같은 R 개체를 데이터로 변환 하기 위한 여러 함수를 제공 합니다. SQL Server에 필요한 프레임입니다.
함수가 데이터 프레임을 목록에 먼저 래핑하지 않고 직접 출력하는 경우 이 단계를 건너뛸 수 있습니다.
함수에서 NULL을 반환 하는 경우이 단계 변환을 건너뛸 수도 있습니다.

목록을 변환 하거나 목록에서 특정 항목을 가져오는 경우 다음 함수 중에서 선택 합니다.

- `setOutputData`목록에서 가져올 변수가 데이터 프레임인 경우
- `setOutputParameter`목록의 다른 모든 멤버

각 함수를 호출 하는 경우 나중에에 `StoredProcedure`인수로 전달 하 여 전체 저장 프로시저를 만드는 R 개체가 만들어집니다.

## <a name="step-3-generate-the-stored-procedure"></a>3단계. 저장 프로시저 생성

모든 입력 및 출력 매개 변수가 준비 되 면 `StoredProcedure` 생성자를 호출 합니다.

**Usage**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

이를 설명 하기 위해 다음 매개 변수를 사용 하 여 **sp_rsample** 라는 저장 프로시저를 만들려고 한다고 가정 합니다.

- 기존 함수 **foosql**을 사용 합니다. 함수는 R 함수 **foo**의 기존 코드를 기반으로 하지만 [이 섹션](#bkmk_rewrite)에 설명 된 대로 함수를 효율적인 하 고 업데이트 된 함수의 이름을 **foosql**로 지정 했습니다.
- 데이터 프레임 **queryinput** 을 입력으로 사용 합니다.
- R 변수 이름, **sqloutput** 을 사용 하 여 데이터 프레임을 출력으로 생성 합니다.
- 나중에 SQL Server Management Studio를 사용 하 여 실행할 수 있도록 t-sql 코드를 `C:\Temp` 폴더에 파일로 만들려고 합니다.

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> 파일 시스템에 파일을 작성 하기 때문에 데이터베이스 연결을 정의 하는 인수를 생략할 수 있습니다.

함수의 출력은 SQL Server 2016의 인스턴스에서 실행할 수 있는 T-sql 저장 프로시저 (R Services 필요) 또는 SQL Server 2017 (R로 Machine Learning Services 필요)입니다. 

추가 예제는 R 환경에서를 호출 `help(StoredProcedure)` 하 여 패키지 도움말을 참조 하세요.

## <a name="step-4-register-and-run-the-stored-procedure"></a>4단계. 저장 프로시저 등록 및 실행

저장 프로시저를 실행 하는 방법에는 두 가지가 있습니다.

- SQL Server 2016 또는 SQL Server 2017 인스턴스에 대 한 연결을 지 원하는 모든 클라이언트에서 T-sql 사용
- R 환경에서

두 방법 모두 저장 프로시저를 사용 하려는 데이터베이스에 저장 프로시저를 등록 해야 합니다.

### <a name="register-the-stored-procedure"></a>저장 프로시저 등록

R을 사용 하 여 저장 프로시저를 등록 하거나 T-sql에서 CREATE PROCEDURE 문을 실행할 수 있습니다.

- T-sql 사용.  T-sql을 사용 하는 것이 더 어려우면 sql Server Management Studio (또는 sql DDL 명령을 실행할 수 있는 다른 클라이언트)를 열고 `StoredProcedure` 함수에서 준비한 코드를 사용 하 여 CREATE PROCEDURE 문을 실행 합니다.
- R 사용. R 환경에서 `registerStoredProcedure` **sqlrutils** 의 함수를 사용 하 여 저장 프로시저를 데이터베이스에 등록할 수 있습니다.

  예를 들어 다음 R 호출을 수행 하  여 *sqlsp_rsample str*에 정의 된 인스턴스 및 데이터베이스에 저장 프로시저를 등록할 수 있습니다.

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> R 또는 SQL을 사용 하는지 여부에 관계 없이 새 데이터베이스 개체를 만들 수 있는 권한이 있는 계정을 사용 하 여 문을 실행 해야 합니다.

### <a name="run-using-sql"></a>SQL을 사용 하 여 실행

저장 프로시저를 만든 후 T-sql을 지 원하는 모든 클라이언트를 사용 하 여 SQL database에 대 한 연결을 열고 저장 프로시저에 필요한 매개 변수에 대 한 값을 전달 합니다.

### <a name="run-using-r"></a>R을 사용 하 여 실행

SQL Server 대신 R 코드에서 저장 프로시저를 실행 하려는 경우에는 몇 가지 추가 준비를 수행 해야 합니다. 예를 들어 저장 프로시저에 입력 값이 필요한 경우 함수를 실행 하기 전에 해당 입력 매개 변수를 설정 하 고 해당 개체를 R 코드의 저장 프로시저에 전달 해야 합니다.

준비 된 SQL 저장 프로시저를 호출 하는 전체 프로세스는 다음과 같습니다.

1. `getInputParameters` 를 호출하여 입력 매개 변수 개체 목록을 가져옵니다.
2. 각 입력 매개 변수에 대해 `$query` 를 정의하거나 `$value` 를 설정합니다.
3. `executeStoredProcedure` 를 사용하여 R 개발 환경에서 저장 프로시저를 실행하고 설정한 입력 매개 변수 개체 목록을 전달합니다.

## <a name = "samples"></a>예 들어

이 예에서는 SQL Server 데이터베이스에서 데이터를 가져오고, 데이터에 대 한 일부 변환을 수행 하 고, 다른 데이터베이스에 저장 하는 R 스크립트의 이전 및 이후 버전을 보여 줍니다.

이 간단한 예제는 저장 프로시저로 쉽게 변환할 수 있도록 R 코드를 다시 정렬 하는 방법을 보여 주기 위해 사용 됩니다.

### <a name="before-code-preparation"></a>코드 준비 전


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
> *RxSqlServerData* 함수를 호출 하는 대신 ODBC 연결을 사용 하는 경우 데이터베이스에 대 한 작업을 수행 하려면 먼저 *rxopen* 을 사용 하 여 연결을 열어야 합니다.


### <a name="after-code-preparation"></a>코드 준비 후

업데이트 된 버전에서 첫 번째 줄은 함수 이름을 정의 합니다. 원래 R 솔루션의 다른 모든 코드는 해당 함수의 일부가 됩니다.

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

## <a name="see-also"></a>관련 항목

[sqlrutils (SQL)](ref-r-sqlrutils.md)


