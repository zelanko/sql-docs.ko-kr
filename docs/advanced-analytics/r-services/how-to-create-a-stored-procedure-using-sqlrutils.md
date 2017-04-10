---
title: "sqlrutils를 사용하여 저장 프로시저를 만드는 방법 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 5ba99b49-481e-4b30-967a-a429b855b1bd
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# sqlrutils를 사용하여 저장 프로시저를 만드는 방법
이 항목에서는 R 코드를 변환하여 T-SQL 저장 프로시저로 실행하는 단계에 대해 설명합니다. 최상의 결과를 얻으려면 모든 입력을 매개 변수화할 수 있도록 코드를 약간 수정해야 할 수 있습니다.

## <a name="step-1-format-your-r-script"></a>1단계. R 스크립트 서식 지정

1. 모든 코드를 단일 함수로 래핑합니다.

   즉, 함수에서 사용되는 모든 변수를 함수 내에 정의하거나 입력 매개 변수로 정의해야 한다는 의미입니다. 이 항목의 [샘플 코드](#samples)를 참조하세요.

## <a name="step-2-standardize-the-inputs-and-outputs"></a>2단계. 입력 및 출력 표준화

함수의 입력 매개 변수는 SQL 저장 프로시저의 입력 매개 변수가 되므로 다음과 같은 형식 요구 사항을 따라야 합니다.
- 입력 매개 변수 중 하나의 데이터 프레임만 있을 수 있습니다.
- 함수의 다른 모든 입력 매개 변수뿐만 아니라 데이터 프레임 내의 개체는 다음과 같은 R 데이터 형식이어야 합니다.
    - POSIXct
    - numeric
    - character
    - integer
    - 논리
    - raw

- 입력 형식이 위 형식 중 하나가 아닌 경우 직렬화하고 *raw*로 함수에 전달해야 합니다. 이 경우 입력을 역직렬화하는 코드도 함수에 있어야 합니다.

함수는 다음 중 하나를 출력할 수 있습니다.

- 지원되는 데이터 형식을 포함하는 데이터 프레임. 데이터 프레임의 모든 개체는 지원되는 데이터 형식 중 하나를 사용해야 합니다.
- 하나의 데이터 프레임만 포함하는 명명된 목록. 목록의 모든 멤버는 지원되는 데이터 형식 중 하나를 사용해야 합니다. 
- 함수에서 결과를 반환하지 않는 경우 NULL

## <a name="step-3-make-calls-to-the-sqlrutils-package-to-generate-the-stored-procedure"></a>3단계. sqlrutils 패키지를 호출하여 저장 프로시저 생성

R 코드가 정리되고 단일 함수로 호출할 수 있는 경우 **sqlrutils**에서 함수를 사용하여 코드를 저장 프로시저로 변환하는 프로세스를 시작할 수 있습니다.

매개 변수의 데이터 형식에 따라 서로 다른 함수를 사용하여 데이터를 캡처하고 매개 변수 개체를 만듭니다.

1. 함수가 입력 매개 변수를 사용하는 경우 각 매개 변수에 대해 다음 개체 중 하나를 만듭니다. 
    - 입력 매개 변수가 데이터 프레임인 경우 `setInputData`를 사용합니다.
    - 다른 모든 입력 매개 변수의 경우 `setInputParameter`를 사용합니다.

2. 함수가 목록을 출력하는 경우 다음과 같이 개체를 만들어 목록에서 원하는 데이터를 처리합니다. 
    - 목록의 변수가 데이터 프레임인 경우 `setOutputData`를 사용합니다.
    - 목록의 다른 모든 멤버에는 `setOutputParameter`를 사용합니다.
    - 함수가 데이터 프레임을 목록에 먼저 래핑하지 않고 직접 출력하는 경우 이 단계를 건너뛸 수 있습니다. 
    - 함수가 NULL을 반환하는 경우 이 단계를 건너뜁니다.

3. 모든 입력 및 출력 매개 변수가 준비되면 `StoredProcedure` 생성자를 호출하여 R 함수를 포함하는 저장 프로시저를 생성합니다.
4. 데이터베이스에 저장 프로시저를 즉시 등록하려면 `registerStoredProcedure`를 사용합니다.

## <a name="step-4-execute-the-stored-procedure"></a>4단계. 저장 프로시저 실행

1. SQL Server가 아닌 R 코드에서 저장 프로시저를 실행하려고 하고 저장 프로시저에 입력이 필요한 경우 함수를 실행하기 전에 해당 입력 매개 변수를 설정해야 합니다. 
    - `getInputParameters`를 호출하여 입력 매개 변수 개체 목록을 가져옵니다.
    - 각 입력 매개 변수에 대해 `$query`를 정의하거나 `$value`를 설정합니다. 

2. `executeStoredProcedure`를 사용하여 R 개발 환경에서 저장 프로시저를 실행하고 설정한 입력 매개 변수 개체 목록을 전달합니다.

## <a name="a-name-samplesaexamples-prepare-your-code"></a><a name = "samples"></a>예제: 코드 준비 

이 예제에서 R 코드는 데이터베이스에서 읽고 데이터에서 몇 가지 변환을 수행한 후 다른 데이터베이스에 저장합니다. 이 간단한 예제는 저장 프로시저 변환에 더 간단한 인터페이스를 제공하기 위해 R 코드를 다시 정렬하는 방법을 보여 주기 위해서만 사용됩니다.

**서식 지정 전**


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
*RxSqlServerData* 함수를 호출하는 대신 ODBC 연결을 사용하는 경우 데이터베이스에서 작업을 수행하기 전에 *rxOpen*을 사용하여 연결을 열어야 합니다.



**서식 지정 후**

서식이 다시 지정된 버전에서 첫 번째 줄은 함수 이름을 정의합니다.

원래 R 솔루션의 다른 모든 코드는 해당 함수의 일부가 됩니다. 

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
ODBC 연결을 코드의 일부로 명시적으로 열 필요는 없지만 **sqlrutils**를 사용하려면 ODBC 연결이 필요합니다. 


## <a name="see-also"></a>관련 항목:

[sqlrutils를 사용하여 저장 프로시저 생성](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

