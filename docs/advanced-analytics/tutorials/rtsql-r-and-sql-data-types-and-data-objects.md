---
title: "R 및 SQL 데이터 형식과 데이터 개체 (SQL 빠른 시작에서 R) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
dev_langs:
- R
- SQL
ms.assetid: 1a17fc5b-b8c5-498f-b8b1-3b7b43a567e1
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d3773c56310b3d91b20acd05b40fc00ae5003b43
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="r-and-sql-data-types-and-data-objects-r-in-sql-quickstart"></a>R 및 SQL 데이터 형식과 데이터 개체 (SQL 빠른 시작에서 R)

이 단계에서는 R 및 SQL Server 간에 데이터를 이동할 때 발생 하는 몇 가지 일반적인 문제에 대 한 방법을 배웁니다.

+ 경우에 따라 데이터 형식이 일치하지 않음
+ 암시적 변환이 수행 될 수 있습니다.
+ 경우에 따라 캐스트 및 변환 작업이 필요함
+ R 및 SQL이 서로 다른 데이터 개체를 사용함

## <a name="always-return-r-data-as-a-data-frame"></a>항상 R 데이터를 데이터 프레임으로 반환함

스크립트가 R에서 SQL Server로 결과를 반환할 경우 데이터를 **data.frame**으로 반환해야 합니다. 스크립트에서 생성하는 다른 형식의 개체는 목록, 요소, 벡터 또는 이진 데이터이든 관계없이 저장 프로시저 결과의 일부로 출력하려면 데이터 프레임으로 변환되어야 합니다. 다행히도 기타 개체를 데이터 프레임으로 변경하는 기능을 지원하는 여러 R 함수가 있습니다. 이진 모델을 serialize하고 데이터 프레임에서 반환할 수 있고 이 작업은 이 자습서의 뒷부분에서 수행하게 됩니다.

첫째, 보겠습니다 일부 R 기본 R 개체를 시험해-벡터, 행렬 및 목록을-변환 데이터 프레임으로 SQL Server에 전달 된 출력을 변경 하는 방법을 확인 합니다.

R에서 "Hello World" 스크립트를 비교 합니다. 스크립트는 거의 동일 하지만 첫 번째, 두 번째 각각 단일 세 개의 열 값을 반환 하는 반면 3 개의 값의 단일 열을 반환 합니다.

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

결과가 다른 이유는 무엇일까요?

일반적으로 R `str()` 명령을 사용하여 그 대답을 찾을 수 있습니다. R 스크립트에 `str(object_name)` 함수를 추가하여 지정된 R 개체의 데이터 스키마가 정보 메시지로 반환되도록 합니다. 메시지를 보려면 Visual Studio Code의 **메시지** 창 또는 SSMS의 **메시지** 탭에서 확인합니다.

예제 1 및 예제 2의 결과가 다른 이유를 확인하려면 다음과 같이 각 문에서 _@script_ 변수 정의의 끝 부분에 `str(OutputDataSet)` 줄을 삽입합니다.

**예제 1 str 함수 추가**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**예제 2 str 함수 추가**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet)' , 
  @input_data_1 = N'  ';
```

이제 **메시지**의 텍스트를 검토하여 출력이 다른 이유를 확인합니다.

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

확인한 것처럼 R 구문을 약간 변경한 것이 결과의 스키마에 큰 영향을 미쳤습니다. 않겠습니다 이유, 차이점 R 데이터 형식에는 완벽 하 게이 문서에서 설명 Hadley Wickham 여 때문에: [R 데이터 구조](http://adv-r.had.co.nz/Data-structures.html)합니다.

우선은 R 개체를 데이터 프레임으로 강제 변환할 때 예상 결과를 확인해야 합니다.

> [!TIP]
> 
> 사용할 수도 있습니다 R id 함수 같은 `is.matrix`, `is.vector`등입니다.

## <a name="implicit-conversion-of-data-objects"></a>데이터 개체의 암시적 변환

각 R 데이터 개체에는 두 개의 개체에 같은 수의 차원이 포함되거나 데이터 개체에 다른 데이터 형식이 포함될 경우 다른 데이터 개체와 결합될 때 값을 처리하는 방법에 대한 자체 규칙이 있습니다.

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

내부적으로 3개 열이 포함된 열이 단일 열 행렬로 변환됩니다. 행렬은 R에서 특별한 경우인 배열이므로 두 인수가 일치하도록 `y`는 암시적으로 단일 열 행렬로 강제 변환됩니다.

**결과**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|

그러나 배열 크기를 변경 하면 어떤 일이 생기 메모 `y`합니다.

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

이유가 무엇일까요? 이 경우 두 인수는 동일한 길이의 벡터로 처리 될 수 있습니다, 때문에 R 행렬으로 내부의 제품을 반환 합니다.  이것은 선형 대수 규칙에 따라 예상된 동작입니다. 하지만 다운스트림 응용 프로그램에서 출력 스키마가 절대 변경되지 않을 것으로 예상할 경우에는 이 동작으로 인해 문제가 발생할 수 있습니다.

> [!TIP]
> 
> 오류가 발생 했습니다? 이 예제 테이블 필요 **RTestData**합니다. 테스트 데이터 테이블을 만들지 않은 경우이 항목으로 다시 이동: [입 / 출력 작업](../tutorials/rtsql-working-with-inputs-and-outputs.md)합니다.
> 
> 테이블이 만들어져 해도 여전히 오류가 발생 하는 경우 저장된 프로시저를에 없는 한 테이블을 포함 하는 데이터베이스의 컨텍스트에서 실행 되 고 있는지 확인 **마스터** 또는 다른 데이터베이스입니다.
> 
> 또한이 예제에 대 한 임시 테이블을 사용 하지 않는 것이 좋습니다. 일부 R 클라이언트는 임시 테이블을 삭제 하는 일괄 처리 간의 연결을 종료 합니다.

## <a name="merge-or-multiply-columns-of-different-length"></a>다른 길이의 열 병합 또는 곱하기

R은 데이터 프레임으로 이러한 열 구조를 조합 및는 다양 한 크기의 벡터 작업에 대 한 뛰어난 유연성을 제공 합니다. 벡터 목록은 테이블처럼 보일 수 있지만 데이터 테이블에 적용되는 모든 규칙을 따르는 것은 아닙니다.

예를 들어 다음 스크립트는 길이가 6인 숫자 배열을 정의하고 R 변수 `df1`에 저장합니다. 숫자 배열에는 다음을 새 데이터 프레임을 확인 하려면 3 개의 값이 포함 되어 있는 RTestData 테이블의 정수 함께 `df2`합니다.

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

데이터 프레임을 채우기 위해 R는 RTestData에서 검색된 요소를 `df1` 배열의 요소 수와 일치하도록 필요한 횟수만큼 반복합니다.

**결과**
    
|*Col2*|*Col3*|
|----|----|
|1|1|
|10|2|
|100|3|
|1|4|
|10|5|
|100|6|

데이터 프레임이 테이블처럼 보이지만 실제로는 벡터 목록이라는 것을 기억하세요.

## <a name="cast-or-convert-sql-server-data"></a>SQL Server 데이터 캐스트 또는 변환

R 및 SQL Server는 같은 데이터 형식을 사용하지 않으므로, SQL Server에서 쿼리를 실행하여 데이터를 가져오고 이를 R 런타임에 전달할 경우 대개 일부 유형의 암시적 변환이 이루어집니다. R에서 SQL Server로 데이터를 반환할 경우 또 다른 일련의 변환이 이루어집니다.

- SQL Server 실행 패드 서비스에서 관리 하는 R 프로세스에 쿼리에서 데이터를 푸시 및 효율성을 높이기 위한 내부 표현으로 변환 합니다.
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
> 모든 버전의 AdventureWorks 사용 하거나 자신만의 데이터베이스를 사용 하 여 다른 쿼리를 만들 수 있습니다. 점이 텍스트, 날짜/시간 및 숫자 값이 있는 일부 데이터를 처리 하려고 합니다.

이제, 저장된 프로시저에 대 한 입력으로이 쿼리를 붙여 넣는 시도 하십시오.

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
+ 텍스트 열으로 확인 되었습니다 "ProductSeries"는 **비율**, 범주 변수를 의미 합니다. 문자열 값은 기본적으로 요소로 처리됩니다. R에 문자열을 전달하면 문자열은 내부에서 사용하도록 정수로 변환되고 다시 출력의 문자열에 매핑됩니다.

### <a name="summary"></a>요약

이 간단한 예제에서 입력으로 쿼리하여 SQL 전달 하는 경우 데이터 변환의 결과 확인할 필요가 볼 수 있습니다. 일부 SQL Server 데이터 형식은 R에서 지원 되지 않으므로, 오류를 방지 하려면 다음과 같은 방법이으로 것이 좋습니다.

+ 데이터를 미리 테스트 하 고 열 또는 R 코드에 전달 하는 경우 문제가 될 수 있는 스키마에서 값을 확인 합니다.
+ `SELECT *`를 사용하지 않고 입력 데이터 원본에서 열을 개별적으로 지정하고 각 열이 어떻게 처리되는지 알아봅니다.
+ 문제를 방지하려면 입력 데이터를 준비할 때 필요에 따라 명시적 캐스트를 수행합니다.
+ 전달 되는 데이터 열을 (예: GUID 또는 rowguids) 오류가 발생 하 고 모델링 하는 데 유용 하지 않은 하지 마십시오.

지원 되는 / 지원 되지 않는 데이터 형식에 대 한 자세한 내용은 참조 하십시오. [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md)합니다.

숫자 요소 문자열의 런타임 변환의 성능에 미치는 영향에 대 한 정보를 참조 하십시오. [SQL Server R Services 성능 튜닝](../r/sql-server-r-services-performance-tuning.md)합니다.

## <a name="next-lesson"></a>다음 단원

다음 단계에서는 SQL Server 데이터에 R 함수를 적용하는 방법을 알아봅니다.

[R 함수를 SQL Server 데이터와 함께 사용](../../advanced-analytics/tutorials/rtsql-using-r-functions-with-sql-server-data.md)
