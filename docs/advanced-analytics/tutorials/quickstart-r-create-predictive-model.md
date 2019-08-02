---
title: R을 사용 하 여 예측 모델을 만들기 위한 빠른 시작
description: 이 빠른 시작에서는 SQL Server 데이터를 사용 하 여 R에서 모델을 작성 하 여 예측을 그리는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f902bd7325e84f07d50196c19338d9c05b3503d8
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715438"
---
# <a name="quickstart-create-a-predictive-model-using-r-in-sql-server"></a>빠른 시작: SQL Server에서 R을 사용 하 여 예측 모델 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 R을 사용 하 여 모델을 학습 한 다음 SQL Server의 테이블에 모델을 저장 하는 방법을 배웁니다. 모델은 차량에서 수동 전송에 적합 한 확률을 예측 하는 단순한 일반화 된 선형 모델 (글 화 m)입니다. R에 포함 된 `mtcars` 데이터 집합을 사용 합니다.

## <a name="prerequisites"></a>사전 요구 사항

이전 퀵 스타트 인 [r이 SQL Server에 있는지 확인](quickstart-r-verify.md)하 고,이 빠른 시작에 필요한 r 환경을 설정 하기 위한 정보 및 링크를 제공 합니다.

## <a name="create-the-source-data"></a>원본 데이터 만들기

먼저 학습 데이터를 저장할 테이블을 만듭니다.

```sql
CREATE TABLE dbo.MTCars(
    mpg decimal(10, 1) NOT NULL,
    cyl int NOT NULL,
    disp decimal(10, 1) NOT NULL,
    hp int NOT NULL,
    drat decimal(10, 2) NOT NULL,
    wt decimal(10, 3) NOT NULL,
    qsec decimal(10, 2) NOT NULL,
    vs int NOT NULL,
    am int NOT NULL,
    gear int NOT NULL,
    carb int NOT NULL
);
```

그런 다음 데이터 집합 `mtcars`의 빌드에서 데이터를 삽입 합니다.

```SQL
INSERT INTO dbo.MTCars
EXEC sp_execute_external_script
        @language = N'R'
        , @script = N'MTCars <- mtcars;'
        , @input_data_1 = N''
        , @output_data_1_name = N'MTCars';
```

+ 임시 테이블 사용을 좋아하는 사람도 있겠지만, 일부 R 클라이언트는 배치 간의 세션 연결을 끊는다는 점을 유의하세요.

+ R 런타임에는 작고 큰 많은 데이터 세트가 포함되어 있습니다. R과 함께 설치된 데이터 집합 목록을 가져오려면 R 명령 프롬프트에서 `library(help="datasets")` 를 입력합니다.

## <a name="create-a-model"></a>모델 만들기

차 속도 데이터에는 두 개의 열, 즉 숫자, 마`hp`력 () 및`wt`가중치 ()가 포함 됩니다. 이 데이터를 사용 하 여 차량에서 수동 전송에 적합 한 확률을 예측 하는 일반화 된 선형 모델 (글 화)을 만듭니다.

모델을 작성 하려면 R 코드 내에서 수식을 정의 하 고 데이터를 입력 매개 변수로 전달 합니다.

```sql
DROP PROCEDURE IF EXISTS generate_GLM;
GO
CREATE PROCEDURE generate_GLM
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'carsModel <- glm(formula = am ~ hp + wt, data = MTCarsData, family = binomial);
        trained_model <- data.frame(payload = as.raw(serialize(carsModel, connection=NULL)));'
    , @input_data_1 = N'SELECT hp, wt, am FROM MTCars'
    , @input_data_1_name = N'MTCarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model VARBINARY(max)));
END;
GO
```

+ 에 대 `glm` 한 첫 번째 인수는 *수식* 매개 변수 이며 `am` 에 `hp + wt`종속 된 것으로 정의 됩니다.
+ 입력 데이터는 SQL 쿼리로 데이터를 채운 `MTCarsData` 변수에 저장됩니다. 입력 데이터에 특정 이름을 할당하지 않는 경우 기본 변수 이름은 _InputDataSet_ 입니다.

## <a name="create-a-table-for-the-model"></a>모델에 대 한 테이블 만들기

다음으로 다시 학습 하거나 예측에 사용할 수 있도록 모델을 저장 합니다. 모델을 만드는 R 패키지의 출력은 일반적으로 **이진 개체**입니다. 따라서 모델을 저장 하는 테이블은 **varbinary (max)** 유형의 열을 제공 해야 합니다.

```sql
CREATE TABLE GLM_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
```

## <a name="save-the-model"></a>모델 저장

모델을 저장하려면 다음 Transact-SQL 문을 실행하여 저장 프로시저를 호출하고 모델을 생성한 다음 테이블에 저장합니다.

```sql
INSERT INTO GLM_models(model)
EXEC generate_GLM;
```

이 코드를 두 번 실행하면 다음 오류가 발생합니다.

```sql
Violation of PRIMARY KEY constraint...Cannot insert duplicate key in object dbo.stopping_distance_models
```

이 오류를 방지하는 한 가지 옵션은 각 새 모델의 이름을 업데이트하는 것입니다. 예를 들어 모델의 유형, 생성한 날짜 등을 포함해서 좀 더 서술적인 이름으로 변경할 수 있습니다.

```sql
UPDATE GLM_models
SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
WHERE model_name = 'default model'
```

## <a name="next-steps"></a>다음 단계

이제 모델을 만들었으므로 최종 퀵 스타트에서 예측을 생성 하 고 결과를 그리는 방법을 배웁니다.

> [!div class="nextstepaction"]
> [빠른 시작: 모델에서 예측 및 그리기](quickstart-r-predict-from-model.md)