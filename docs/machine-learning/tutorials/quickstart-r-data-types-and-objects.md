---
title: '빠른 시작: R 데이터 구조, 데이터 형식, 개체'
description: 이 빠른 시작에서 SQL Server Machine Learning Services에서 R을 사용하는 경우 데이터 구조, 데이터 형식, 개체를 사용하는 방법을 알아봅니다. R과 SQL Server 서버 사이의 데이터 이동과 일반적으로 발생할 수 있는 문제에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 07d167ddc39f281a3330ffd80460d9cc34ccfa65
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487328"
---
# <a name="quickstart-data-structures-data-types-and-objects-using-r-in-sql-server-machine-learning-services"></a>빠른 시작: SQL Server Machine Learning Services에서 R을 사용하는 데이터 구조, 데이터 형식 및 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 SQL Server Machine Learning Services에서 R을 사용하는 경우 데이터 구조와 데이터 형식을 사용하는 방법을 알아봅니다. R과 SQL Server 서버 사이의 데이터 이동과 일반적으로 발생할 수 있는 문제에 대해 알아봅니다.

처음에 알아야 할 일반적인 문제는 다음과 같습니다.

- 경우에 따라 데이터 형식이 일치하지 않음
- 암시적 변환이 발생할 수 있음
- 경우에 따라 캐스트 및 변환 작업이 필요함
- R 및 SQL이 서로 다른 데이터 개체를 사용함

## <a name="prerequisites"></a>사전 요구 사항

- 이 빠른 시작에서는 R 언어가 설치된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)를 사용하여 SQL Server 인스턴스에 액세스해야 합니다.

  SQL Server 인스턴스는 Azure 가상 머신 또는 온-프레미스에 있을 수 있습니다. 외부 스크립팅 기능은 기본적으로 사용하지 않도록 설정되어 있으므로 시작하기 전에 [외부 스크립팅을 활성화](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)하고 **SQL Server 실행 패드 서비스**가 실행 중인지 확인해야 합니다.

- R 스크립트가 포함된 SQL 쿼리를 실행하기 위한 도구도 필요합니다. SQL Server 인스턴스에 연결할 수 있는 데이터베이스 관리 또는 쿼리 도구를 사용하여 이러한 스크립트를 실행하고 T-SQL 쿼리 또는 저장 프로시저를 실행할 수 있습니다. 이 빠른 시작에서는 [SSMS(SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용합니다.

## <a name="always-return-a-data-frame"></a>항상 데이터 프레임 반환

스크립트가 R에서 SQL Server로 결과를 반환할 경우 데이터를 **data.frame**으로 반환해야 합니다. 스크립트에서 생성하는 다른 형식의 개체는 목록, 요소, 벡터 또는 이진 데이터이든 관계없이 저장 프로시저 결과의 일부로 출력하려면 데이터 프레임으로 변환되어야 합니다. 다행히도 기타 개체를 데이터 프레임으로 변경하는 기능을 지원하는 여러 R 함수가 있습니다. 이진 모델을 serialize하고 데이터 프레임에서 반환할 수 있고 이 작업은 이 빠른 시작의 뒷부분에서 수행하게 됩니다.

먼저 R 기본 R 개체인 벡터, 메트릭 및 목록을 실험해 보고 데이터 프레임으로 변환하면 SQL Server에 전달되는 출력이 어떻게 변경되는지 살펴봅니다.

R에서 두 가지 "Hello World" 스크립트를 비교합니다. 두 스크립트가 거의 동일하게 보이지만 첫 번째 스크립트는 3개 값의 단일 열을 반환하고, 두 번째 스크립트는 각각 하나의 단일 값이 포함된 세 개의 열을 반환합니다.

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

## <a name="identify-schema-and-data-types"></a>스키마 및 데이터 형식 식별

결과가 다른 이유는 무엇일까요?

일반적으로 R `str()` 명령을 사용하여 그 대답을 찾을 수 있습니다. R 스크립트에 `str(object_name)` 함수를 추가하여 지정된 R 개체의 데이터 스키마가 정보 메시지로 반환되도록 합니다. 메시지를 보려면 Visual Studio Code의 **메시지** 창 또는 SSMS의 **메시지** 탭에서 확인합니다.

예제 1 및 예제 2의 결과가 다른 이유를 확인하려면 다음과 같이 각 문에서 `@script` 변수 정의의 끝부분에 `str(OutputDataSet)` 줄을 삽입합니다.

**str 함수가 추가된 예제 1**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      OutputDataSet <- as.data.frame(mytextvariable);
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**str 함수가 추가된 예제 2**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet);' , 
  @input_data_1 = N'  ';
```

이제 **메시지**의 텍스트를 검토하여 출력이 다른 이유를 확인합니다.

**결과 - 예제 1**

```sql
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**결과 - 예제 2**

```sql
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

확인한 것처럼 R 구문을 약간 변경한 것이 결과의 스키마에 큰 영향을 미쳤습니다. 여기에서 그 이유를 살펴보지는 않지만, R 데이터 형식의 차이는 [Hadley Wickham의 "Advanced R"(고급 R)](http://adv-r.had.co.nz)에 있는 *Data Structures*(데이터 구조)에 자세히 설명되어 있습니다.

우선은 R 개체를 데이터 프레임으로 강제 변환할 때 예상 결과를 확인해야 합니다.

> [!TIP]
> 또한 `is.matrix`, `is.vector`와 같은 R ID 함수를 사용하여 내부 데이터 구조에 대한 정보를 반환할 수 있습니다.

## <a name="implicit-conversion-of-data-objects"></a>데이터 개체의 암시적 변환

각 R 데이터 개체에는 두 개의 개체에 같은 수의 차원이 포함되거나 데이터 개체에 다른 데이터 형식이 포함될 경우 다른 데이터 개체와 결합될 때 값을 처리하는 방법에 대한 자체 규칙이 있습니다.

먼저 작은 테스트 데이터 테이블을 만듭니다.

```sql
CREATE TABLE RTestData (col1 INT NOT NULL)

INSERT INTO RTestData
VALUES (1);

INSERT INTO RTestData
VALUES (10);

INSERT INTO RTestData
VALUES (100);
GO
```

예를 들어 다음 명령문을 실행하여 R을 사용한 행렬 곱셈을 수행한다고 가정합니다. 3개 값이 포함된 단일 열 행렬에 4개 값이 포함된 배열을 곱하고 결과로 4x3 행렬을 예상합니다.

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

하지만 `y` 배열의 크기를 변경할 경우 발생하는 상황을 확인하세요.

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

그 이유는 이 경우 두 인수가 동일한 길이의 벡터로 처리될 수 있기 때문에 R는 내부 곱을 행렬로 반환합니다.  이것은 선형 대수 규칙에 따라 예상된 동작입니다. 하지만 다운스트림 애플리케이션에서 출력 스키마가 절대 변경되지 않을 것으로 예상할 경우에는 이 동작으로 인해 문제가 발생할 수 있습니다.

> [!TIP]
> 
> 오류가 발생했나요? **마스터** 또는 다른 데이터베이스가 아닌 해당 테이블이 포함된 데이터베이스의 컨텍스트에서 저장 프로시저를 실행 중인지 확인하세요.
>
> 또한 이 예제에 대해서는 임시 테이블을 사용하지 않는 것이 좋습니다. 일부 R 클라이언트가 일괄 처리 사이의 연결을 종료하여 임시 테이블이 삭제될 수 있습니다.

## <a name="merge-or-multiply-columns-of-different-length"></a>다른 길이의 열 병합 또는 곱하기

R은 다양한 크기의 벡터를 사용하고 이러한 열 유사 구조를 데이터 프레임으로 결합하는 뛰어난 유연성을 제공합니다. 벡터 목록은 테이블처럼 보일 수 있지만 데이터 테이블에 적용되는 모든 규칙을 따르는 것은 아닙니다.

예를 들어 다음 스크립트는 길이가 6인 숫자 배열을 정의하고 R 변수 `df1`에 저장합니다. 그런 다음, 숫자형 배열을 3개의 값이 포함된 RTestData 테이블의 정수와 함께 결합하여 새 데이터 프레임 `df2`를 만듭니다.

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

- SQL Server는 실행 패드 서비스에서 관리하는 R 프로세스로 쿼리의 데이터를 푸시하고 내부 표현으로 변환하여 효율성을 높여줍니다.
- R 런타임이 데이터를 data.frame 변수에 로드하고 데이터에서 고유한 작업을 수행합니다.
- 데이터베이스 엔진은 보안 설정된 내부 연결을 통해 데이터를 SQL Server로 반환하고 SQL Server 데이터 형식을 기준으로 데이터를 제공합니다.
- SQL 쿼리를 실행하고 테이블 형식 데이터 집합을 처리할 수 있는 클라이언트 또는 네트워크 라이브러리를 사용하여 SQL Server에 연결하는 방식으로 데이터를 가져옵니다. 이 클라이언트 애플리케이션은 다른 방식으로 데이터에 영향을 미칠 수 있습니다.

이 애플리케이션이 작동하는 방식을 확인하려면 [AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) 데이터 웨어하우스에서 이와 같은 쿼리를 실행합니다. 이 뷰는 예측 생성에 사용된 매출 데이터를 반환합니다.

```sql
USE AdventureWorksDW
GO

SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
>
> 모든 AdventureWorks 버전을 사용하거나 고유 데이터베이스를 사용해서 다른 쿼리를 만들 수 있습니다. 중요한 것은 텍스트, 날짜/시간 및 숫자 값이 포함된 일부 데이터를 처리하는 것입니다.

이제 이 쿼리를 저장 프로시저에 대한 입력으로 붙여넣습니다.

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
      , @script = N' str(InputDataSet);
      OutputDataSet <- InputDataSet;'
      , @input_data_1 = N'
           SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = ''M200 Europe''
           ORDER BY ReportingDate ASC ;'
WITH RESULT SETS undefined;
```

오류가 발생하면 쿼리 텍스트를 약간 편집해야 할 수 있습니다. 예를 들어 WHERE 절의 문자열 조건자는 두 개의 작은따옴표 집합으로 묶어야 합니다.

쿼리를 실행한 후 `str` 함수의 결과를 검토하여 R에서 입력 데이터가 어떻게 처리되는지 확인합니다.

**결과**

```sql
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

- datetime 열은 R 데이터 형식 **POSIXct**를 사용하여 처리되었습니다.
- 텍스트 열 "ProductSeries"는 범주 변수를 의미하는 **요소**로 식별되었습니다. 문자열 값은 기본적으로 요소로 처리됩니다. R에 문자열을 전달하면 문자열은 내부에서 사용하도록 정수로 변환되고 다시 출력의 문자열에 매핑됩니다.

### <a name="summary"></a>요약

이러한 간단한 예제로부터 SQL 쿼리를 입력으로 전달할 때 데이터 변환으로 인한 효과를 확인할 필요성이 있다는 것을 알 수 있습니다. 일부 SQL Server 데이터 형식은 R에서 지원되지 않기 때문에 오류 방지를 위해 다음과 같은 방법들을 고려하세요.

- 데이터를 미리 테스트하고 R 코드에 전달될 때 문제가 될 수 있는 스키마의 열 또는 값을 확인합니다.
- `SELECT *`를 사용하지 않고 입력 데이터 원본에서 열을 개별적으로 지정하고 각 열이 어떻게 처리되는지 알아봅니다.
- 문제를 방지하려면 입력 데이터를 준비할 때 필요에 따라 명시적 캐스트를 수행합니다.
- 오류를 일으키고 모델링에 유용하지 않은 데이터 열 전달(예: GUIDS 또는 rowguids)을 방지합니다.

데이터 형식 지원 및 미지원에 대한 자세한 내용은 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md)을 참조하세요.

런타임에 문자열을 숫자 요소로 변환할 경우 성능에 미치는 영향에 대한 자세한 내용은 [SQL Server R Services 성능 튜닝](../r/sql-server-r-services-performance-tuning.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

SQL Server에서 고급 R 함수 작성에 대해 알아보려면 다음 빠른 시작을 참조하세요.

> [!div class="nextstepaction"]
> [SQL Server Machine Learning Services를 사용하여 고급 R 함수 작성](quickstart-r-functions.md)

SQL Server Machine Learning Services에서 R 사용에 대한 자세한 내용은 다음 문서를 참조하세요.

- [SQL Server Machine Learning Services를 사용하여 R에서 예측 모델 만들기 및 채점](quickstart-r-train-score-model.md)
- [SQL Server Machine Learning Services(Python 및 R)란?](../sql-server-machine-learning-services.md)
