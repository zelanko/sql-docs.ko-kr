---
title: "Transact-SQL에서 R 코드 사용(SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/10/2017"
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
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: 36
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 28
---
# Transact-SQL에서 R 코드 사용(SQL Server R Services)
이 자습서에서는 SQL Server R Services에서 R로 작업하기 위한 구문의 매우 간단한 예를 제공합니다.    
    
    
SQL Server R Services를 처음 사용하며 T-SQL 저장 프로시저에서 R 스크립트를 정의하는 방법, 데이터를 입력으로 사용하는 방법 및 출력을 정의하는 방법의 기본 사항을 알아보려는 경우 여기서 시작하는 것이 좋습니다.    
    
**필수 조건:** SQL Server R Services에서 R 코드를 실행하려면 R Services가 이미 설치되어 있는 SQL Server 인스턴스에 연결해야 합니다.     
    
## 1부 - 기본 작업  

다음 섹션에서는 매개 변수를 추가하여 저장 프로시저를 확장하는 방법 및 입/출력을 구성하는 방법을 알아봅니다.   
  
### 1.1. SQL Server에서 R이 작동하는지 확인  

이 쿼리에서는 SQL Server 컨텍스트에서 R을 호출하는 방법인 시스템 저장 프로시저 [sp_execute_external_script](https://msdn.microsoft.com/library/mt604368.aspx)를 사용합니다. 이 예제에서는 SQL 쿼리를 R에 입력으로 전달하고, R은 해당 데이터 프레임을 SQL Server에 반환합니다.     
    
1. Windows 시작 메뉴에서 Microsoft SQL Server Management Studio를 찾습니다.     
2. 찾을 수 없는 경우 설치해야 할 수도 있습니다. [SQL Server Management Studio 다운로드](https://msdn.microsoft.com/library/mt238290.aspx).    
3. **서버에 연결** 대화 상자에서 SQL Server R Services가 사용하도록 설정된 서버 또는 인스턴스의 이름을 입력합니다. 이러한 예제에서는 새 데이터베이스를 만들고, SELECT 문을 실행하고, 테이블을 볼 수 있는 계정을 사용하여 로그인해야 합니다.  새 **쿼리** 창을 열고 이 문을 붙여넣어 모든 것이 작동하는지 확인합니다.    
    
    ```sql   
    exec sp_execute_external_script  
      @language =N'R',    
      @script=N'OutputDataSet<-InputDataSet',      
      @input_data_1 =N'select 1 as hello'    
      with result sets (([hello] int not null));    
    go    
    ```   
       
       
  
### <a name="bkmk_SSMSBasics"></a>1.2. 몇 가지 간단한 테스트 데이터 만들기  
    
복잡한 데이터 과학 솔루션을 개발하기 전에 SQL Server와 R 간의 차이점을 이해하는 것이 중요합니다.    
  
1. 다음 T-SQL 문을 실행하여 임시 데이터 테이블을 만듭니다.     
   
    ```sql    
    CREATE TABLE #MyData ([Col1] int not null) ON [PRIMARY]    
    INSERT INTO #MyData   VALUES (1);    
    INSERT INTO #MyData   Values (10);    
    INSERT INTO #MyData   Values (100) ;    
    GO    
    ```    
5. 테이블을 만들었으면 다음 문을 사용하여 테이블을 쿼리합니다.  
    ```sql  
    SELECT * from #MyData  
    ```  

**결과**  
  
|Col1 |   
|----|   
|1|   
|10|   
|100|   
  
    
### 1.3. R 스크립트를 사용하여 테스트 데이터 가져오기    
  
테이블을 만든 후 다음 문을 실행합니다.  
  
  ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet <- InputDataSet;'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
    WITH RESULT SETS (([NewColName] int NOT NULL));
  ```    
    
동일한 값이 새 열 이름으로 반환됩니다.  
  
**참고**    
- *@language* 매개 변수는 호출할 언어 확장(이 경우 R)을 정의합니다.    
- *@script* 매개 변수에서 R 런타임에 유니코드 텍스트로 전달할 명령을 정의합니다. **nvarchar** 형식의 변수에 텍스트를 추가한 다음 변수를 호출할 수도 있습니다.    
- `N'OutputDataSet <- InputDataSet;'` 줄은 기본 변수 이름 **InputDataSet**에 포함된 입력 데이터를 R에 전달한 다음 추가 작업 없이 결과로 다시 전달합니다. R은 대/소문자를 구분하므로 입력 및 출력 변수 이름 둘 다에서 올바른 대/소문자를 사용해야 합니다. 그러지 않으면 오류가 발생합니다.    
   
    
다른 입력 또는 출력 변수를 지정하려면 *@input_data_1_name* 매개 변수를 사용하고 유효한 SQL 식별자를 입력합니다. 예를 들어 이 예제에서는 출력 및 입력 변수 이름이 각각 *SQLOut* 및 *SQLIn*으로 변경되었습니다.    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' SQLOut <- SQLIn;'    
    , @input_data_1 = N' SELECT 12 as Col;'    
    , @input_data_1_name  = N'SQLIn'    
    , @output_data_1_name =  N'SQLOut'    
    WITH RESULT SETS (([NewColName] int NOT NULL));    
```    
    
**참고**    
- 선택적 매개 변수 *@input_data_1_name* 및 *@output_data_1_name*을 사용하려면 필수 매개 변수 *@input_data_1* 및 *@output_data_1*을 먼저 지정해야 합니다.    
- SQL 및 R은 동일한 데이터 형식을 지원하지 않으므로 SQL Server에서 R로 데이터를 보낼 때 형식 변환이 자주 발생하며, 그 반대의 경우도 마찬가지입니다. 자세한 내용은 [R 데이터 형식 사용](../../advanced-analytics/r-services/working-with-r-data-types.md)을 참조하세요.    
- 하나의 입력 데이터 집합만 매개 변수로 전달할 수 있으며 하나의 데이터 집합만 반환할 수 있습니다. 그러나 R 코드 내에서 다른 데이터 집합을 호출할 수 있으며 데이터 집합 외에 다른 유형의 출력을 반환할 수 있습니다. 또한 모든 매개 변수에 OUTPUT 키워드를 추가하여 결과와 함께 매개 변수를 반환할 수도 있습니다.      
- 반환된 데이터 집합(R data.frame)에 대한 스키마는 `WITH RESULT SETS` 문을 통해 정의됩니다. 이 문을 생략하고 결과를 확인해 보세요.    
- 테이블 형식 결과가 **값** 창에 반환됩니다. R 런타임을 통해 반환된 메시지는 **메시지**에 제공됩니다.     
  
### 1.4. R을 사용하여 결과 생성    
    
R 스크립트를 사용하여 값을 생성하고 _@input_data_1_의 입력 쿼리 문자열은 비워 둘 수도 있습니다. 또는 유효한 SQL SELECT 문을 자리 표시자로 사용하되 R 스크립트에 SQL 결과를 사용하지 않을 수도 있습니다.    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' mytextvariable <- c("hello", " ", "world");    
                         OutputDataSet <- as.data.frame(mytextvariable);'    
    , @input_data_1 = N' SELECT 1 as Temp1'    
    WITH RESULT SETS (([col] char(20) NOT NULL));    
```    
    
**결과**    
    
    
 |*col* |    
 |-----|    
 |*hello*|    
 |     |    
 |*world*|    
    

이제 위에 제공된 Hello World 샘플의 다른 버전을 사용합니다.     
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'    
    , @input_data_1 = N'  '    
    WITH RESULT SETS (([col1] varchar(20) , [col2] char(1), [col3] varchar(20) ));    
```    
    
    
**결과**    
    
    
 |*col1* | *col2* | *col3*|    
 |-------|-------|-------    
 |*hello*|  |*world*|    
    
두 문 모두 세 개의 값이 포함된 벡터를 만들 수 있지만, 두 번째 예제에서는 세 개 열과 한 개 행을 반환하고, 첫 번째 예제에서는 한 개 열과 세 개 행을 반환합니다. 이유가 무엇일까요?
    
이유는 R은 값 열로 작업하는 다양한 방법(벡터, 행렬, 배열 및 목록)을 제공하기 때문입니다. 이러한 작업은 강력하고 유연하지만 항상 SQL 개발자의 예상을 따르지는 않습니다.  일부 R 함수는 목록 및 행렬에 대해 암시적 데이터 개체 변환을 수행합니다.

> [!TIP] 
> 
> 항상 결과를 검토하고 R 코드에서 반환하는 데이터 열 수와 데이터 형식을 확인합니다.    
>     
> R 코드에서 행렬, 벡터 또는 다른 데이터 구조 중 어느 것을 사용하는지와 관계없이 R 스크립트에서 저장 프로시저로 출력되는 결과는 **data.frame**이어야 합니다.      
  
  
## 2부 - 데이터 변환 및 기타 문제  
  
이 섹션에서는 SQL Server에서 R 코드를 실행할 때 알아야 할 몇 가지 문제에 대한 간략한 개요를 제공합니다.  
  
+ 데이터 형식: 암시적 변환뿐만 아니라 캐스트 및 변환 옵션 이해  
+ 테이블 형식 결과 집합: R에서 데이터 열과 행을 변경하는 방법 예측    
  
### 2.1 데이터 형식의 암시적 강제 변환  
    
R과 SQL Server는 같은 데이터 형식을 사용하지 않으므로 R과 데이터베이스 간에 데이터를 이동할 때 제한 사항에 유의해야 합니다. 다음 예제에서는 몇 가지 일반적인 문제를 보여 줍니다.   
    
    
1. 다음 문을 실행하여 R을 사용한 행렬 곱셈을 수행합니다. 이 스크립트에서는 세 개의 값을 가진 단일 열이 단일 열 행렬로 변환됩니다.  그런 다음 R은 암시적으로 두 번째 변수인 `y`를 단일 열 행렬로 강제 변환하여 두 인수를 일치시킵니다.  
    
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:15);    
      OutputDataSet <- as.data.frame(x %*% y);'    
     , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));    
    ```    
**결과**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|
 
  
      
2. 이제 유사한 다음 스크립트를 실행하고 배열의 길이를 변경할 때 어떻게 되는지 확인합니다. 
   
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:14);    
      OutputDataSet <- as.data.frame(y %*% x);'    
      , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int ));    
    ```    

**결과**    
    
|Col1|
|---|    
|1542|    
  
  이번에는 R에서 단일 값을 결과로 반환합니다. 이 결과는 두 인수가 동일한 길이의 벡터이기 때문에 유효하므로 R에서 내부 곱을 행렬로 반환합니다.    
    
   
  
### 2.2 길이가 다른 열 병합 또는 곱하기    
    
  
다음 스크립트는 데이터베이스 개발자의 예상을 따르지 않을 수도 있는 R의 몇 가지 동작을 보여 줍니다.   
  
스크립트에서 길이가 6인 새 숫자형 배열을 정의하고 R 변수 `df1`에 저장합니다. 그런 다음 숫자형 배열을 3개의 값이 포함된 #MyData 테이블의 정수와 함께 결합하여 새 데이터 프레임 `df2`를 만듭니다.   
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
               df1 <- as.data.frame( array(1:6) );    
               df2 <- as.data.frame( c( InputDataSet , df1 ));    
               OutputDataSet <- df2'    
    , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));    
```    
    
**결과**    
    
|*Col2*|*Col3*|    
|----|----|    
|1|1|    
|10|2|    
|100|3|    
|1|4|    
|10|5|    
|100|6|    
    
테이블 형식 출력을 만들지만 R 데이터 개체에 따라 값에서 전혀 다른 작업을 수행하는 많은 R 함수가 있습니다. 이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저의 경우 입력 및 출력을 모두 data.frame으로 전달해야 하므로 자주 함수를 사용하여 열과 행을 데이터 프레임으로 변환하거나 그 반대로 변환합니다.    
    
사용 중인 R 데이터 개체와 관련해서 의문 사항이 있을 경우 R `str()` 함수 또는 ID 함수 중 하나(`is.matrix`, `is.vector` 등)를 추가하여 결과를 검사하고 실제 스키마와 값 형식을 가져옵니다.    
  
  
자세한 내용은 Hadley Wickham이 작성한 [R 데이터 구조](http://adv-r.had.co.nz/Data-structures.html)와 관련된 이 문서를 참조하세요.    
    
### 2.3 데이터 형식 식별 및 스키마 확인   
R 코드에서 반환되는 열 수와 각 열의 데이터 형식을 정확하게 아는 것이 중요함을 확인할 수 있습니다.     
    
  
R 스크립트에 `str()` 함수를 사용하여 SQL Server에서 R 개체의 데이터 스키마가 정보 메시지로 반환되도록 할 수 있습니다. 

예를 들어 다음 문은 #MyData 테이블의 스키마를 반환합니다.    
        
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' str(InputDataSet);'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
      WITH RESULT SETS undefined;    
```    
    
    
**결과**    
    
*STDOUT message (s) from external script:*    
*'data.frame': 3 obs. of 1 variable:*    
*STDOUT message (s) from external script:*    
*$ Col1: int 1   10   100*    
    
  
  
### 2.4 열 캐스트 또는 변환   
  
SQL Server에서 R로 데이터를 보낼 때 적절하게 처리되도록 데이터 형식을 캐스트 또는 변환해야 하는 경우가 많습니다.    
  
R 코드에 대한 입력으로 SQL 쿼리를 사용하는 경우 여러 데이터 변환이 수행됩니다.    
- SQL Server는 실행 패드 서비스에서 관리하는 R 프로세스로 쿼리의 데이터를 푸시하고 내부 표현으로 변환합니다.    
- R 런타임이 데이터를 data.frame 변수에 로드하고 데이터에서 고유한 작업을 수행합니다.    
- 데이터베이스 엔진이 SQL Server 데이터 형식을 사용하여 데이터를 Management Studio 또는 다른 클라이언트에 반환합니다.  
    
1. AdventureWorksDW 데이터 웨어하우스에서 다음 쿼리를 실행합니다. 입력 데이터 쿼리는 예측을 만드는 데 사용할 판매 데이터 테이블을 정의합니다.   
  
    ```sql    
    execute sp_execute_external_script    
       @language = N'R'    
      , @script = N' str(InputDataSet);'    
      , @input_data_1 = N'
           SELECT ReportingDate    
         , CAST(ModelRegion as varchar(50)) as ProductSeries    
         , Amount    
           FROM [AdventureworksDW2016CTP3].[dbo].[vTimeSeries]     
           WHERE [ModelRegion] = ''M200 Europe''    
           ORDER BY ReportingDate ASC ;'    
        WITH RESULT SETS undefined;    
    ```    
  
2. 이제 `str` 함수의 결과를 검토하여 R에서 입력 데이터를 어떻게 처리했는지 확인합니다.
      
**결과**    
    
  *STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:*    
  *STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"*    
  *STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1 ...*    
  *STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950*    
    
    
**참고**    
    
- 일부 SQL Server 데이터 형식은 R에서 지원되지 않습니다. 따라서 오류를 방지하려면 열을 개별적으로 지정하고 일부 열을 캐스트해야 합니다.    
- WHERE 절의 문자열 조건자는 두 개의 작은따옴표 집합으로 묶어야 합니다.    
- datetime 열은 R 데이터 형식 **POSIXct**로 반환되었습니다.    
- [ProductSeries] 열은 **인수**로 (올바르게) 식별되었습니다.    
     
  
### 2.5 여러 입력 사용   
하나의 입력 데이터 집합만 매개 변수로 전달할 수 있습니다. 그러나 RODBC를 사용하여 R 코드 내에서 다른 데이터 집합을 호출할 수 있습니다.     
  
예를 들어 다음 샘플에서는 SELECT 문에서 데이터를 지정하여 RODBC 패키지를 호출합니다.    
    
```sql    
    @script = N' 
       <other R code here>;    
       library(RODBC);    
       connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");        dbhandle <- odbcDriverConnect(connStr)    
       OutputDataSet <- sqlQuery(dbhandle, "SELECT * from <table_name>");    
       <more R code combining the data>'    
```

SQL Server에서, 조회 또는 인수 목록과 같은 작은 데이터 집합을 가져오려면 RODBC를 사용하고, 모델 학습에 사용되는 데이터 집합과 같은 큰 데이터 집합을 가져오려면 @input_data 매개 변수를 사용하는 것이 좋습니다. 


### 2.6 여러 출력 생성

SQL Server 2016에서는 저장 프로시저 sp_execute_external_script의 R 출력이 단일 data.frame 또는 데이터 집합으로 제한됩니다. 이 제한은 나중에 제거될 수도 있습니다.   
그러나 데이터 집합 외에 다른 유형의 출력을 반환할 수 있습니다. 예를 들어 단일 데이터 집합을 입력으로 사용하여 모델을 학습하지만 통계 테이블을 출력으로 반환할 뿐 아니라 학습된 모델을 개체로 반환할 수 있습니다.    
    
또한 모든 입력 매개 변수에 `OUTPUT` 키워드를 추가하여 결과와 함께 매개 변수를 반환할 수도 있습니다.   
    
### 2.7 병렬 처리    
    
큰 데이터 집합을 사용 중이며 데이터를 가져오는 SQL 쿼리에서 병렬 쿼리 계획을 생성할 수 있는 경우 *@parallel* 매개 변수를 1로 설정하여 R 스크립트를 병렬로 실행할 수 있습니다. 이 기능은 일반적으로 큰 결과 집합의 점수를 매기는 경우에 유용합니다. 이 옵션을 사용하는 경우 WITH RESULT SETS를 통해 출력 결과 스키마를 미리 지정해야 합니다.    
    
그러나 모든 행을 사용하는 모델을 학습해야 하는 경우에는 이 매개 변수가 적용되지 않습니다. 이 경우 **ScaleR** 패키지를 사용하는 것이 좋습니다. 이러한 패키지는 sp_execute_external_script 호출에 *@parallel =1*을 지정하지 않아도 자동으로 처리를 분산할 수 있습니다.    
    
      
  
## 3부. 저장 프로시저에 R 함수 래핑  
  
R은 T-SQL을 사용하여 재현하려면 복잡한 코드가 필요할 수 있는 여러 고급 통계 함수를 수행할 수 있습니다.  그러나 R Services를 사용할 경우 저장 프로시저에서 R 유틸리티 스크립트를 실행하여 다음과 같은 작업을 지원할 수 있습니다.   
    
- SQL Server 데이터에 R의 수치 연산 및 통계 함수 적용    
    
- R 코드를 사용하는 테이블 반환 함수 또는 스칼라 함수 만들기    
     

 일반적으로 매개 변수를 더 쉽게 전달하기 위해 저장 프로시저에 이러한 R 함수 호출을 캡슐화합니다. 이 프로세스를 보여 주기 위해 같은 함수가 R 코드, sp_execute_external_script에 대한 임시 저장 프로시저 호출 및 R 함수를 매개 변수화하는 데 사용할 수 있는 저장 프로시저에 제공됩니다.
 
      
### 3.1. 난수 생성  
  
다음 문에서는 R Services를 설치할 때 기본적으로 로드되는 `stats` 패키지의 R 함수 중 하나를 사용합니다. 여기에 표시된 `rnorm` 함수는 평균이 100인 정규 분포를 사용하여 20개의 난수를 생성합니다.    

이 작업을 수행하는 R 코드는 다음과 같습니다.

```r
as.data.frame(rnorm(20, mean = 100));
```

이 문은 T-SQL에서 함수를 호출하고 SQL Server에 결과를 출력합니다.  
   
```sql    
EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N' 
         OutputDataSet <- as.data.frame(rnorm(20, mean = 100));'    
    , @input_data_1 = N'   ;'    
      WITH RESULT SETS (([Density] float NOT NULL));    
```    

다음으로, 매개 변수를 더 쉽게 전달하기 위해 또 다른 저장 프로시저에 저장 프로시저를 래핑합니다. _@params_ 인수에 각 입력 매개 변수를 정의하고 각 매개 변수를 이름으로 해당 R 매개 변수에 매핑해야 합니다.

```sql
CREATE PROCEDURE MyRNorm (@mynorm int, @mymean int)
AS
    EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynorm, mymean));'    
    , @input_data_1 = N'   ;' 
    , @params = N' @mynorm int, @mymean int'  
    , @mynorm = @mynorm
    , @mymean = @mymean
    WITH RESULT SETS (([Density] float NOT NULL));    
```

새 저장 프로시저를 호출하고 값을 전달합니다.

```sql
exec MyRNorm @mynorm = 20,@mymean = 100
```  
    
### 3.2 R 유틸리티 함수의 추가 용도  
  
이 예제에서는 R 유틸리티 패키지 중 하나를 호출하고 해당 `memory.limit()` 함수를 사용하여 현재 환경에 대한 메모리를 가져옵니다. `utils` 패키지는 설치되어 있지만 기본적으로 로드되지 않습니다.    
    
```sql    
execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
        library(utils);    
        mymemory <- memory.limit();    
        OutputDataSet <- as.data.frame(mymemory);'    
    , @input_data_1 = N' ;'    
     WITH RESULT SETS (([Col1] int not null));    
```    

다음 예제에서는 R .Machine 함수를 사용하여 현재 컴퓨터에서 지원되는 정수의 최대 길이를 가져오고 해당 길이를 콘솔에 출력합니다.

```R
localmax <- .Machine$integer.max;
localmax;
```

```sql
execute sp_execute_external_script
  @language = N'R'
  , @script = N'
      localmax <- .Machine$integer.max;
      OutputDataSet <- as.data.frame(localmax);'
  , @input_data_1 = N'select [Col1]  from #MyData;'
  WITH RESULT SETS (([MaxIntValue] int not null));
```     
    
그러나 항상 R을 사용한 작업이 더 나은 것은 아닙니다. 데이터 과학자가 기존에 R에서 수행하던 일부 작업의 경우 SQL Server의 집합 기반 작업이 훨씬 더 효율적일 수 있습니다. R 함수와 T-SQL 사용자 지정 함수의 성능 비교 예는 [데이터 과학 종단 간 솔루션](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)을 참조하세요. 

R, T-SQL 또는 기타 도구 중 어느 것을 사용하는 것이 지정된 작업을 수행하는 데 더 적합한 방법인지는 사례별로 평가하는 것이 좋습니다.    
    
    
    
### 추가 리소스    
    
[데이터 과학 심층 분석: RevoScaleR 패키지 사용](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md): 이 연습에서는 일반적인 데이터 과학 작업을 사용한 실습 경험을 제공합니다.    
[데이터 과학 종단 간 솔루션](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md): 이 연습에서는 SQL 및 R 방법의 균형을 유지하는 개발 및 배포 프로세스를 보여 줍니다.       
[SQL 개발자를 위한 고급 분석](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md): SQL 개발자를 위한 전체 모델 운영을 보여 줍니다.     
    
    
    
    
