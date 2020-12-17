---
title: Sqlrutils 패키지를 사용하여 번들 R 코드에서 함수 만들기
description: SQL Server의 sqlrutils R 패키지를 사용하여 R 언어 코드를 단일 함수로 번들화합니다. 이는 저장 프로시저에 인수로 전달할 수 있습니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/06/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: f90c1b004dae28f98b1b7f250cf16e0ed0d2ae5b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470864"
---
# <a name="create-a-stored-procedure-using-sqlrutils"></a>sqlrutils를 사용하여 저장 프로시저 만들기
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

이 문서에서는 R 코드를 변환하여 T-SQL 저장 프로시저로 실행하는 단계에 대해 설명합니다. 최상의 결과를 얻으려면 모든 입력을 매개 변수화할 수 있도록 코드를 약간 수정해야 할 수 있습니다.

## <a name="step-1-rewrite-r-script"></a><a name="bkmk_rewrite"></a>1단계. R 스크립트 다시 작성

최상의 결과를 위해서는 단일 함수로 캡슐화하도록 R 코드를 다시 작성해야 합니다.

함수에서 사용되는 모든 변수를 함수 내에 정의하거나 입력 매개 변수로 정의해야 합니다. 이 문서의 [샘플 코드](#samples)를 참조하세요.

또한 R 함수의 입력 매개 변수는 SQL 저장 프로시저의 입력 매개 변수가 되므로 입력 및 출력은 다음과 같은 형식 요구 사항을 따라야 합니다.

### <a name="inputs"></a>입력

입력 매개 변수 중 데이터 프레임은 최대 한 개만 있을 수 있습니다.

함수의 다른 모든 입력 매개 변수뿐만 아니라 데이터 프레임 내의 개체는 다음과 같은 R 데이터 형식이어야 합니다.
- POSIXct
- numeric
- character
- integer
- 논리
- raw

입력 형식이 위 형식 중 하나가 아닌 경우 직렬화하고 *raw* 로 함수에 전달해야 합니다. 이 경우 입력을 역직렬화하는 코드도 함수에 있어야 합니다.

### <a name="outputs"></a>outputs

함수는 다음 중 하나를 출력할 수 있습니다.

- 지원되는 데이터 형식을 포함하는 데이터 프레임. 데이터 프레임의 모든 개체는 지원되는 데이터 형식 중 하나를 사용해야 합니다.
- 하나의 데이터 프레임만 포함하는 명명된 목록. 목록의 모든 멤버는 지원되는 데이터 형식 중 하나를 사용해야 합니다.
- 함수에서 결과를 반환하지 않는 경우 NULL

## <a name="step-2-generate-required-objects"></a>2단계. 필요한 개체 생성

R 코드가 정리되고 단일 함수로 호출될 수 있으면 **sqlrutils** 패키지의 함수를 사용하여 실제로 저장 프로시저를 빌드하는 생성자에 전달될 수 있는 형식으로 입력 및 출력을 준비합니다.

**sqlrutils** 는 입력 데이터 스키마와 형식을 정의하고 출력 데이터 스키마와 형식을 정의하는 함수를 제공합니다. 또한 R 개체를 필요한 출력 형식으로 변환할 수 있는 함수가 포함됩니다. 코드에서 사용하는 데이터 형식에 따라 여러 함수 호출을 수행하여 필요한 개체를 만들 수 있습니다.

### <a name="inputs"></a>입력

함수에서 입력을 사용하는 경우 각 입력에 대해 다음 함수를 호출합니다.

- 입력이 데이터 프레임인 경우 `setInputData`
- 기타 모든 입력 형식에 대해 `setInputParameter`

각 함수를 호출하는 경우 나중에 `StoredProcedure`에 인수로 전달하여 전체 저장 프로시저를 만들 수 있도록 R 개체가 만들어집니다.

### <a name="outputs"></a>outputs

**sqlrutils** 는 목록과 같은 R 개체를 SQL Server에 필요한 데이터 프레임으로 변환하기 위한 여러 함수를 제공합니다.
함수가 데이터 프레임을 목록에 먼저 래핑하지 않고 직접 출력하는 경우 이 단계를 건너뛸 수 있습니다.
또한 함수가 NULL을 반환하는 경우 이 단계의 변환을 생략할 수 있습니다.

목록을 변환하거나 특정 항목을 목록에서 가져올 때 다음과 같은 함수에서 선택합니다.

- 목록에서 가져오려는 변수가 데이터 프레임인 경우 `setOutputData`
- 목록의 다른 모든 멤버에 대해서는 `setOutputParameter`

각 함수를 호출하는 경우 나중에 `StoredProcedure`에 인수로 전달하여 전체 저장 프로시저를 만들 수 있도록 R 개체가 만들어집니다.

## <a name="step-3-generate-the-stored-procedure"></a>3단계. 저장 프로시저 생성

모든 입력 및 출력 매개 변수가 준비되면 `StoredProcedure` 생성자를 호출합니다.

**사용 현황**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

설명을 위해 다음 매개 변수를 사용하여 **sp_rsample** 이라는 저장 프로시저를 생성한다고 가정해보겠습니다.

- 기존 함수 **foosql** 을 사용합니다. 함수는 R 함수 **foo** 의 기존 코드를 기반으로 하지만, [이 섹션](#bkmk_rewrite)에서 설명한 것처럼 요구 사항을 준수하기 위해 함수를 다시 작성하고 업데이트된 함수의 이름을 **foosql** 로 지정했습니다.
- 데이터 프레임 **queryinput** 을 입력으로 사용합니다.
- R 변수 이름이 **sqloutput** 인 데이터 프레임을 출력하여 생성합니다.
- 나중에 SQL Server Management Studio를 사용하여 실행할 수 있도록 T-SQL 코드를 `C:\Temp` 폴더에 파일로 생성하려고 합니다.

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> 파일을 파일 시스템에 쓰기 때문에 데이터베이스 연결을 정의하는 인수를 생략할 수 있습니다.

함수의 출력은 SQL Server 2016(R Services 필요) 또는 SQL Server 2017(Machine Learning Services with R 필요)의 인스턴스에서 실행될 수 있는 T-SQL 저장 프로시저입니다. 

추가 예제의 경우 R 환경에서 `help(StoredProcedure)`를 호출하면 패키지 도움말에서 확인할 수 있습니다.

## <a name="step-4-register-and-run-the-stored-procedure"></a>4단계. 저장 프로시저 등록 및 실행

다음과 같은 두 가지 방법으로 저장 프로시저를 실행할 수 있습니다.

- SQL Server 2016 또는 SQL Server 2017 인스턴스에 대한 연결을 지원하는 클라이언트에서 T-SQL 사용
- R 환경에서

두 방법 모두 저장 프로시저를 사용하려는 데이터베이스에 저장 프로시저를 등록해야 합니다.

### <a name="register-the-stored-procedure"></a>저장 프로시저 등록

R을 사용하여 저장 프로시저를 등록하거나, T-SQL에서 CREATE PROCEDURE 문을 실행할 수 있습니다.

- T-SQL 사용.  T-SQL이 더 편한 경우 SQL Server Management Studio(또는 SQL DDL 명령을 실행할 수 있는 다른 클라이언트)를 열고 `StoredProcedure` 함수에서 준비된 코드를 사용하여 CREATE PROCEDURE 문을 실행합니다.
- R 사용. R 환경에서는 `registerStoredProcedure`sqlrutils **의**  함수를 사용하여 저장 프로시저를 데이터베이스에 등록할 수 있습니다.

  예를 들어 다음 R 호출을 수행하여 **sqlConnStr** 에 정의된 데이터베이스와 인스턴스에 저장 프로시저 *sp_rsample* 을 등록할 수 있습니다.

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> R을 사용하든 SQL을 사용하든 상관없이 새 데이터베이스 개체를 만들 수 있는 사용 권한이 있는 계정을 사용하여 문을 실행해야 합니다.

### <a name="run-using-sql"></a>SQL을 사용하여 실행

저장 프로시저가 생성된 후에는 T-SQL을 지원하는 클라이언트를 사용하여 SQL 데이터베이스에 대한 연결을 열고 저장 프로시저에 필요한 매개 변수에 대한 값을 전달합니다.

### <a name="run-using-r"></a>R을 사용하여 실행

SQL Server가 아닌 R 코드에서 저장 프로시저를 실행하려면 몇 가지 추가 준비가 필요합니다. 예를 들어 저장 프로시저에 입력 값이 필요한 경우 함수를 실행하기 전에 해당 입력 매개 변수를 설정한 다음, 해당 개체를 R 코드의 저장 프로시저에 전달해야 합니다.

준비된 SQL 저장 프로시저를 호출하는 전체 프로세스는 다음과 같습니다.

1. `getInputParameters` 를 호출하여 입력 매개 변수 개체 목록을 가져옵니다.
2. 각 입력 매개 변수에 대해 `$query` 를 정의하거나 `$value` 를 설정합니다.
3. `executeStoredProcedure` 를 사용하여 R 개발 환경에서 저장 프로시저를 실행하고 설정한 입력 매개 변수 개체 목록을 전달합니다.

## <a name="example"></a><a name = "samples"></a>예제

이 예제에서는 SQL Server 데이터베이스에서 데이터를 가져와서 데이터에 대해 일부 변환을 수행하고 다른 데이터베이스에 저장하는 R 스크립트의 전후 버전을 보여줍니다.

이 간단한 예제는 더 간단하게 저장 프로시저로 변환하도록 R 코드를 다시 정렬하는 방법을 보여주기 위해서만 사용됩니다.

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
> *RxSqlServerData* 함수를 호출하는 대신 ODBC 연결을 사용하는 경우 데이터베이스에서 작업을 수행하기 전에 *rxOpen* 을 사용하여 연결을 열어야 합니다.


### <a name="after-code-preparation"></a>코드 준비 후

업데이트된 버전에서 첫 번째 줄은 함수 이름을 정의합니다. 원래 R 솔루션의 다른 모든 코드는 해당 함수의 일부가 됩니다.

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
> ODBC 연결을 코드의 일부로 명시적으로 열 필요는 없지만 **sqlrutils** 를 사용하려면 ODBC 연결이 필요합니다.

## <a name="see-also"></a>참고 항목

[sqlrutils(SQL)](ref-r-sqlrutils.md)


