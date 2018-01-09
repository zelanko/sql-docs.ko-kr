---
title: "만들기 predictive 모델 (SQL 빠른 시작에서 R) | Microsoft Docs"
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
ms.assetid: 6eb78a80-5791-438f-9ca6-d142ab5d9bb1
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 19b041df85b3ee1de97e8b5e62295608786a0f0a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="create-a-predictive-model-r-in-sql-quickstart"></a>예측 모델 (SQL 빠른 시작에서 R) 만들기

이 단계에서는 R을 사용하여 모델을 학습한 다음 SQL Server의 테이블에 모델을 저장하는 방법을 알아봅니다. 모델은 속도에 따라 자동차의 정지 거리를 예측하는 간단한 회귀 모델입니다. 사용 하 여는 `cars` 작고 쉽게 이해할 수 있기 때문에 R을에 포함 된 데이터 집합입니다.

## <a name="create-the-source-data"></a>원본 데이터 만들기

먼저 학습 데이터를 저장할 테이블을 만듭니다.

```sql
CREATE TABLE CarSpeed ([speed] int not null, [distance] int not null)
INSERT INTO CarSpeed
EXEC sp_execute_external_script
        @language = N'R'
        , @script = N'car_speed <- cars;'
        , @input_data_1 = N''
        , @output_data_1_name = N'car_speed'
```

+ 어떤 사람들 일부 R 클라이언트가 일괄 처리 간의 세션 연결을 끊을 있는지 수 있지만 임시 테이블을 사용 하려고 합니다.

+ R 런타임에는 작고 큰 많은 데이터 집합이 포함되어 있습니다. R과 함께 설치된 데이터 집합 목록을 가져오려면 R 명령 프롬프트에서 `library(help="datasets")`를 입력합니다.

## <a name="create-a-regression-model"></a>회귀 모델 만들기

자동차 속도 데이터에는 둘 다 숫자인 `dist` 및 `speed`의 두 열이 포함되어 있습니다. 일부 속도의 경우 여러 관찰이 있습니다. 이 데이터에서 자동차 속도와 자동차를 정지하는 데 필요한 거리 간의 몇 가지 관계를 설명하는 선형 회귀 모델을 만들게 됩니다.

선형 모델의 요구 사항은 간단합니다.

+ 종속 변수 `speed`와 독립 변수 `distance` 간의 관계를 설명하는 수식 정의

+ 모델 학습에 사용할 입력 데이터 제공

> [!TIP]
> RxLinMod를 사용 하 여 모델을 맞추는 하는 과정을 설명 하는이 자습서에서는 권장 복습 선형 모델에 필요한 경우: [선형 모델 맞춤](https://docs.microsoft.com/r-server/r/how-to-revoscaler-linear-model)

실제로 모델을 빌드하려면 R 코드 내에서 수식을 정의하고 데이터를 입력 매개 변수로 전달합니다.

```sql
DROP PROCEDURE IF EXISTS generate_linear_model;
GO
CREATE PROCEDURE generate_linear_model
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'lrmodel <- rxLinMod(formula = distance ~ speed, data = CarsData);
        trained_model <- data.frame(payload = as.raw(serialize(lrmodel, connection=NULL)));'
    , @input_data_1 = N'SELECT [speed], [distance] FROM CarSpeed'
    , @input_data_1_name = N'CarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model varbinary(max)));
END;
GO
```

+ rxLinMod에 대한 첫 번째 인수는 거리를 속도에 종속된 것으로 정의하는 *formula* 매개 변수입니다.
+ 입력 데이터는 SQL 쿼리에 의해 채워지는 `CarsData` 변수에 저장됩니다. 입력 데이터에 특정 이름을 할당하지 않는 경우 기본 변수 이름은 _InputDataSet_입니다.

## <a name="create-a-table-for-storing-the-model"></a>모델을 저장하기 위한 테이블 만들기

다음으로 다시 학습 하거나 예측에 사용할 수 있도록 모델을 저장 합니다. 모델을 만드는 R 패키지의 출력은 일반적으로 **이진 개체**입니다. 따라서 모델을 저장하는 테이블은 **varbinary** 형식의 열을 제공해야 합니다.

```sql
CREATE TABLE stopping_distance_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null);
```

## <a name="save-the-model"></a>모델 저장

모델을 저장하려면 다음 Transact-SQL 문을 실행하여 저장 프로시저를 호출하고 모델을 생성한 다음 테이블에 저장합니다.

```sql
INSERT INTO stopping_distance_models (model)
EXEC generate_linear_model;
```

이 코드를 두 번 실행 하는 경우이 오류가 참고:

```
Violation of PRIMARY KEY constraint...Cannot insert duplicate key in object dbo.stopping_distance_models
```

이 오류를 방지하는 한 가지 옵션은 각 새 모델의 이름을 업데이트하는 것입니다. 예를 들어 이름을 추가 설명이 포함된 이름으로 변경하고 모델 유형, 모델 유형을 만든 날짜 등을 포함할 수 있습니다.

```sql
UPDATE stopping_distance_models
SET model_name = 'rxLinMod ' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
WHERE model_name = 'default model'
```

## <a name="output-additional-variables"></a>추가 변수 출력

일반적으로 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 R 출력은 단일 데이터 프레임으로 제한됩니다. 이 제한은 나중에 제거될 수도 있습니다.

그러나 데이터 프레임 외에 스칼라 등 다른 유형의 출력을 반환할 수 있습니다.

예를 들어 모델을 학습하지만 모델의 계수 테이블을 즉시 보려고 한다고 가정합니다. 계수 테이블을 기본 결과 집합으로 만들고 학습된 모델을 SQL 변수에 출력할 수 있습니다. 변수를 호출 하 여 모델을 다시 사용 즉시 수 또는 다음과 같이 테이블에 모델을 저장할 수 없습니다.

```sql
DECLARE @model varbinary(max), @modelname varchar(30)
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
        speedmodel <- rxLinMod(distance ~ speed, CarsData)
        modelbin <- serialize(speedmodel, NULL)
        OutputDataSet <- data.frame(coefficients(speedmodel));'
    , @input_data_1 = N'SELECT [speed], [distance] FROM CarSpeed'
    , @input_data_1_name = N'CarsData'
    , @params = N'@modelbin varbinary(max) OUTPUT'
    , @modelbin = @model OUTPUT
    WITH RESULT SETS (([Coefficient] float not null));

-- Save the generated model
INSERT INTO [dbo].[stopping_distance_models] (model_name, model)
VALUES (' latest model', @model)
```

**결과**

![rslq_basictut_coefficients](media/rslq-basictut-coefficients.PNG)

### <a name="summary"></a>요약

SQL 매개 변수 및 변수 R 작업에 대 한 규칙이 `sp_execute_external_script`:

+ R 스크립트에 매핑된 모든 SQL 매개 변수에서 이름으로 나열 되어야 합니다는  _@params_  인수입니다.
+ 이러한 매개 변수 중 하나를 출력하려면 _@params_ 목록에 OUTPUT 키워드를 추가합니다.
+ 매핑된 매개 변수를 나열한 후 _@params_ 목록 바로 뒤의 R 변수에 SQL 매개 변수의 매핑을 줄 단위로 제공합니다.

## <a name="next-lesson"></a>다음 단원

이제 모델이 있으며, 최종 단계로 모델에서 예측을 생성하고 결과를 그림으로 나타내는 방법을 알아보겠습니다.

[모델에서 예측 및 그리기](../tutorials/rtsql-predict-and-plot-from-model.md)


