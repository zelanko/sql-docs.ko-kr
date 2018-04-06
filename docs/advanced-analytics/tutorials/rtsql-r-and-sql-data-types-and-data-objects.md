---
title: R 및 SQL 데이터 형식과 데이터 개체 (R in SQL 빠른 시작) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
dev_langs:
- R
- SQL
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: b763fd5b7c5707d5cc4f49c1ec93b10a0b53c321
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="r-and-sql-data-types-and-data-objects-r-in-sql-quickstart"></a>R 및 SQL 데이터 형식과 데이터 개체 (R in SQL 빠른 시작)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단계에서는 R과 SQL Server 간에 데이터를 이동할 때 발생하는 몇 가지 일반적인 문제에 관해 배웁니다. 

+ 데이터 형식이 일치하지 않는 경우가 있음
+ 암시적 변환이 일어날 수 있음
+ CAST 및 Convert 연산이 필요함 
+ R 및 SQL이 서로 다른 데이터 개체를 사용함

## <a name="always-return-r-data-as-a-data-frame"></a>R 데이터는 항상 데이터 프레임으로 반환

스크립트가 R에서 SQL Server로 결과를 반환할 경우 데이터를 **data.frame**으로 반환해야 합니다. 스크립트에서 생성하는 다른 형식의 개체는 리스트(list), 팩터(factor), 벡터(vector) 또는 이진 데이터이든 관계없이 저장 프로시저 결과의 일부로 출력하려면 데이터 프레임으로 변환되어야 합니다. 다행히도 기타 개체를 데이터 프레임으로 변경하는 기능을 지원하는 여러 R 함수가 있습니다. 이진 모델 또한 직렬화해서 데이터 프레임으로 반환할 수 있으며, 이 자습서의 뒷부분에서 수행할 것입니다.

우선, 벡터, 행렬 및 리스트와 같은 몇 가지 기본 R 개체를 실험한 뒤 데이터 프레임으로 변환하면 SQL Server로 전달되는 출력이 어떻게 변경되는지 확인합니다. 

R에서 다음 두 "Hello World" 스크립트를 비교하세요. 스크립트는 거의 동일 하지만 첫 번째는 세 개의 값을 단일 열로 반환하는 반면, 두 번째는 각각 단일 값을 가진 3개의 열을 반환합니다. 

**예제 1**

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
     , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
     , @input_data_1 = N' ';
```

**예제 2**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'
      , @input_data_1 = N'  ';
```

## <a name="identifying-the-schema-and-data-types-of-r-data"></a>R 데이터의 스키마 및 데이터 형식 식별

왜 결과가 다를까요?

일반적으로 R `str()` 명령을 사용하여 그 대답을 찾을 수 있습니다. R 스크립트 임의 위치에 `str(object_name)` 함수를 추가하여 지정된 R 개체의 데이터 스키마를 정보성 메시지로 반환합니다. 메시지를 보려면 Visual Studio Code의 **Message** 창 또는 SSMS의 **메시지** 탭에서 확인합니다.

예제 1 및 예제 2의 결과가 다른 이유를 확인하려면 다음과 같이 각 문에서 _@script_ 변수 정의의 끝 부분에 `str(OutputDataSet)` 줄을 삽입합니다.

**예제 1 str 함수 추가**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      OutputDataSet <- as.data.frame(mytextvariable);
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**예제 2 str 함수 추가**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet);' , 
  @input_data_1 = N'  ';
```

이제 **Message**에 텍스트를 검토하여 출력이 다른 이유를 확인합니다. 

**결과 - 예제 1**

```
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**결과 - 예제 2**

```
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

확인한 것처럼 R 구문을 약간 변경한 것이 결과의 스키마에 큰 영향을 미쳤습니다. R 데이터 형식의 차이점은 Hadley Wickham의 글 [R 데이터 구조](http://adv-r.had.co.nz/Data-structures.html)에서 보다 자세하게 설명하므로 여기서는 생략합니다.

현재로서는 R 개체를 데이터 프레임으로 강제 변환할 때 예상되는 결과를 확인해야 합니다.

> [!TIP]
> 
> `is.matrix`, `is.vector`등과 같은 R 함수를 사용할 수도 있습니다. 

## <a name="implicit-conversion-of-data-objects"></a>데이터 개체의 암시적 변환

각 R 데이터 개체에는 두 개의 데이터 개체가 같은 수의 차원을 가지거나 데이터 개체에 다른 데이터 형식이 포함될 경우 다른 데이터 개체와 결합될 때 값을 처리하는 방법에 대한 자체 규칙이 있습니다.

예를 들어 다음 문을 실행하여 R을 사용한 행렬 곱셈을 수행한다고 가정합니다. 3개 값이 포함된 단일 열 행렬에 4개 값이 포함된 배열을 곱하고 결과로 4x3 행렬을 예상합니다.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:15);
    OutputDataSet <- as.data.frame(x %*% y);'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));
```

내부적으로 3개의 값으로 구성된 단일 열이 단일-열 행렬로 변환됩니다. 행렬은 R에서 단지 배열의 특수한 형태이므로, 배열 `y`는 두 인수가 일치하도록 단일 열 행렬로 강제 변환됩니다.

**결과**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|

하지만 `y` 배열 크기를 변경하면 어떻게 되는지 주목하세요.

```sql
execute sp_execute_external_script
   @language = N'R'
   , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:14);
   OutputDataSet <- as.data.frame(y %*% x);'
   , @input_data_1 = N' SELECT [Col1]  from RTestData;'
   WITH RESULT SETS (([Col1] int ));
```

이제 R는 결과로 단일 값을 반환합니다.

**결과**
    
|Col1|
|---|
|1542|

이유가 무엇일까요? 이 경우 두 인수는 동일한 길이의 벡터로 처리될 수 있으므로 R이 내적(inner product)을 행렬로 반환합니다.  이것은 선형 대수 규칙에 따라 예상된 동작입니다. 하지만 다운스트림 응용 프로그램에서 출력 스키마가 절대 변경되지 않을 것으로 예상할 경우에는 이 동작으로 인해 문제가 발생할 수 있습니다.

> [!TIP]
> 
> 오류가 발생 했습니까? 이 예제는 **RTestData** 테이블을 필요로 합니다. 테스트 데이터 테이블을 만들지 않은 경우 [입 / 출력 작업](../tutorials/rtsql-working-with-inputs-and-outputs.md) 주제로 다시 이동하세요.
> 
> 테이블이 만들어져도 여전히 오류가 발생한다면, 해당 테이블을 포함한 데이터베이스 내에서 저장 프로시저를 실행하고 있는지 **master** 혹은 다른 데이터베이스가 아닌지 확인해 보세요.
> 
> 또한 예제에서 임시 테이블을 사용하지 않는 것이 좋습니다. 일부 R 클라이언트는 일괄 처리 사이의 연결을 종료하고 임시 테이블을 삭제합니다.

## <a name="merge-or-multiply-columns-of-different-length"></a>다른 길이의 열 병합 또는 곱하기

R은 다양한 크기의 벡터로 작업하고 이러한 열과 같은 구조를 데이터 프레임에 결합하는데 뛰어난 유연성을 제공합니다. 벡터 리스트는 테이블처럼 보일 수 있지만 데이터베이스 테이블을 관리하는 모든 규칙을 따르지 않습니다.

예를 들어 다음 스크립트는 길이가 6인 숫자 배열을 정의하고 R 변수 `df1`에 저장합니다. 그런 다음 숫자 배열에는 3개의 값이 포함된 RTestData 테이블의 정수와 결합하여 세 데이터 프레임 `df2`를 만듭니다. 

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
               df1 <- as.data.frame( array(1:6) );
               df2 <- as.data.frame( c( InputDataSet , df1 ));
               OutputDataSet <- df2'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));
```

R은 데이터 프레임을 채우기 위해 RTestData에서 검색된 요소를 `df1` 배열의 요소 수와 일치하도록 필요한 횟수만큼 반복합니다.

**결과**
    
|*Col2*|*Col3*|
|----|----|
|1.|1.|
|10|2|
|100|3|
|1.|4|
|10|5|
|100|6|

데이터 프레임이 테이블처럼 보이지만 실제로는 벡터의 리스트라는 것을 기억하세요.

## <a name="cast-or-convert-sql-server-data"></a>SQL Server 데이터 Cast 또는 convert

R 과 SQL Server는 같은 데이터 형식을 사용하지 않으므로, SQL Server에서 쿼리를 실행하여 데이터를 가져오고 이를 R 런타임에 전달할 경우 일부 유형에서 종종 암시적 변환이 이루어집니다. R에서 SQL Server로 데이터를 반환할 경우에는 또 다른 일련의 변환이 이루어집니다.

- SQL Server는 쿼리의 데이터를 Launchpad 서비스가 관리하는 R 프로세스에 넣고 효율성을 높이기 위한 내부 표현으로 변환합니다.
- R 런타임이 데이터를 data.frame 변수에 로드하고 데이터에서 고유한 작업을 수행합니다.
- 데이터베이스 엔진은 보안 설정된 내부 연결을 통해 데이터를 SQL Server로 반환하고 SQL Server 데이터 형식을 기준으로 데이터를 제공합니다.
- SQL 쿼리를 실행하고 테이블 형식 데이터 집합을 처리할 수 있는 클라이언트 또는 네트워크 라이브러리를 사용하여 SQL Server에 연결하는 방식으로 데이터를 가져옵니다. 이 클라이언트 응용 프로그램은 다른 방식으로 데이터에 영향을 미칠 수 있습니다.

이 응용 프로그램이 작동하는 방식을 확인하려면 AdventureWorksDW 데이터 웨어하우스에서 이와 같은 쿼리를 실행합니다. 이 뷰는 예측 생성에 사용된 매출 데이터를 반환합니다.

```sql
SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW2014].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
> 
> 모든 버전의 AdventureWorks를 사용할 수 있으며, 자신의 데이터베이스를 사용해 다른 쿼리를 만들 수 있습니다. 요점은 텍스트, 날짜/시간 및 숫자 값이 포함된 일부 데이터를 처리하는 것입니다.

이제, 저장된 프로시저에 입력으로 이 쿼리를 붙여넣으세요.

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
      , @script = N' str(InputDataSet);
      OutputDataSet <- InputDataSet;'
      , @input_data_1 = N'
           SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW2014].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = ''M200 Europe''
           ORDER BY ReportingDate ASC ;'
WITH RESULT SETS undefined;
```

오류가 발생하면 쿼리 텍스트를 약간 편집해야 할 수 있습니다. 예를 들어 WHERE 절의 문자열 조건자는 두 개의 작은따옴표 집합으로 묶어야 합니다.

쿼리를 실행한 후 `str` 함수의 결과를 검토하여 R에서 입력 데이터가 어떻게 처리되는지 확인합니다.

**결과**

```
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

+ datetime 열은 R 데이터 형식 **POSIXct**를 사용하여 처리되었습니다.
+ 텍스트 "ProductSeries"는 **팩터**로 인식되었으며 이는 범주 변수임을 의미합니다. 문자열 값은 기본적으로 팩터로 처리됩니다. 문자열 값은 기본적으로 요소로 처리됩니다. R에 문자열을 전달하면 문자열은 내부 사용을 위해 정수로 변환되고 다시 문자열에 매핑되어서 출력됩니다.

### <a name="summary"></a>요약

간단한 예제를 통해 입력으로 SQL 쿼리를 전달할 때 데이터 변환의 결과를 확인할 필요가 있음을 볼 수 있습니다. 일부 SQL Server 데이터 형식은 R에서 지원되지 않으므로, 오류를 방지하려면 다음과 같은 방법을 고려합니다.

+ 데이터를 미리 테스트해서 R 코드에 전달할 때 문제가 될 수 있는 스키마의 열 혹은 값을 검사합니다.
+ `SELECT *`를 사용하지 않고 입력 데이터 원본에서 열을 개별적으로 지정하고 각 열이 어떻게 처리되는지 알아봅니다.
+ 문제를 방지하려면 입력 데이터를 준비할 때 필요에 따라 명시적 Cast를 수행합니다.
+ 오류를 유발하거나 모델링에 유용하지 않은 데이터 열(예: GUID 또는 rowguids)은 전달하지 않습니다. 

지원되는 혹은 지원되지 않는 데이터 형식에 대한 추가 정보는 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md)을 참조하십시오. 

런타임에 문자열에서 숫자 팩터로의 변환이 성능에 미치는 영향에 대한 정보는 [SQL Server R Services 성능 튜닝](../r/sql-server-r-services-performance-tuning.md)을 참조하십시오.

## <a name="next-lesson"></a>다음 단원

다음 단계에서는 SQL Server 데이터에 R 함수를 적용하는 방법을 알아봅니다.

[R 함수를 SQL Server 데이터와 함께 사용](../../advanced-analytics/tutorials/rtsql-using-r-functions-with-sql-server-data.md)
