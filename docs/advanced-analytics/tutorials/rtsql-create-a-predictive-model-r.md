---
title: "모델에서 예측 및 그리기(SQL에서 R 빠른 시작) | Microsoft Docs"
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
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 1b40295452da5b7da34a31e6825630da9c6c4861
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="create-a-predictive-model-r-in-sql-quickstart"></a>모델에서 예측 및 그리기(SQL에서 R 빠른 시작)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단계에서는 R을 사용하여 모델을 학습한 다음 SQL Server의 테이블에 모델을 저장하는 방법을 알아봅니다. 모델은 자동차의 속도에 따른 정지 거리를 예측하는 간단한 회귀 모델입니다. R에 내장된 `cars` 데이터 집합은 작고 이해하기 쉬우므로 이를 사용할 것입니다.

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

+ 임시 테이블 사용을 좋아하는 사람도 있겠지만, 일부 R 클라이언트는 배치 간의 세션 연결을 끊는다는 점을 유의하세요.

+ R 런타임에는 작고 큰 많은 데이터 집합이 포함되어 있습니다. R과 함께 설치된 데이터 집합 목록을 가져오려면 R 명령 프롬프트에서 `library(help="datasets")` 를 입력합니다.

## <a name="create-a-regression-model"></a>회귀 모델 만들기

자동차 속도 데이터에는 둘 다 숫자인 `dist` 및 `speed` 의 두 열이 포함되어 있습니다. 어떤 속도는 여러 개의 관찰 값이 있습니다. 이 데이터에서 자동차 속도와 자동차를 정지하는 데 필요한 거리 간의 몇 가지 관계를 설명하는 선형 회귀 모델을 만들게 됩니다.

선형 모델의 요구 사항은 간단합니다.

+ 독립 변수 `speed` 와 종속 변수 `distance` 간의 관계를 설명하는 수식 정의 `(역주. 원문에는 두 가지 변수의 순서가 거꾸로 되어 있어서 수정함)`

+ 모델 훈련용 입력 데이터 제공

> [!TIP]
> 선형 모델에 재교육(refresher)이 필요하다면 RxLinMod를 사용하여 모델 적합화 과정을 설명하는 이 자습서를 권장합니다. [선형 모델 맞춤](https://docs.microsoft.com/r-server/r/how-to-revoscaler-linear-model)

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
+ 입력 데이터는 SQL 쿼리로 데이터를 채운 `CarsData` 변수에 저장됩니다. 입력 데이터에 특정 이름을 할당하지 않는 경우 기본 변수 이름은 _InputDataSet_ 입니다.

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

이 코드를 두 번 실행하면 다음 오류가 발생합니다.

```
Violation of PRIMARY KEY constraint...Cannot insert duplicate key in object dbo.stopping_distance_models
```

이 오류를 방지하는 한 가지 옵션은 각 새 모델의 이름을 업데이트하는 것입니다. 예를 들어 모델의 유형, 생성한 날짜 등을 포함해서 좀 더 서술적인 이름으로 변경할 수 있습니다.

```sql
UPDATE stopping_distance_models
SET model_name = 'rxLinMod ' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
WHERE model_name = 'default model'
```

## <a name="output-additional-variables"></a>추가 변수 출력

일반적으로 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 R 출력은 단일 데이터 프레임으로 제한됩니다. 이 제한은 나중에 제거될 수도 있습니다.

그러나 데이터 프레임 외에 스칼라 등 다른 유형의 출력을 반환할 수 있습니다.

예를 들어 모델을 학습하지만 모델의 계수(coefficients) 표를 즉시 보려고 한다고 가정합니다. 계수 표는 기본 결과 집합으로 만들고 학습된 모델은 SQL 변수에 출력할 수 있습니다. 변수를 호출하여 모델을 재사용하거나 다음과 같이 테이블에 저장할 수 있습니다.

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

`sp_execute_external_script` 에서 SQL 매개변수와 R 변수를 함께 작업할 때 기억할 규칙:

+ R 스크립트에 매핑된 모든 SQL 매개 변수는 _@params_ 인수에 이름이 나열되어야 합니다.
+ 이러한 매개 변수 중 하나를 출력하려면 _@params_ 목록에 OUTPUT 키워드를 추가합니다.
+ 매핑된 매개 변수를 나열한 후 _@params_ 목록 바로 뒤의 R 변수에 SQL 매개 변수의 매핑을 줄 단위로 제공합니다.

## <a name="next-lesson"></a>다음 단원

이제 모델을 만들었으므로 최종 단계에서 모델로부터의 예측을 생성하고 결과를 그림으로 나타내는 방법을 배웁니다.

[모델에서 예측 및 출력](../tutorials/rtsql-predict-and-plot-from-model.md)


