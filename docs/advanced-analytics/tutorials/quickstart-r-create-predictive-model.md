---
title: R-SQL Server Machine Learning을 사용 하 여 예측 모델을 만드는 빠른 시작
description: 이 빠른 시작에서는 SQL Server 데이터를 사용 하 여 예측을 그릴 R에서 모델을 빌드하는 방법에 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: f1eaa39e5f22efbe7bea7a44ac2ce93a5e28205e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962034"
---
# <a name="quickstart-create-a-predictive-model-using-r-in-sql-server"></a>빠른 시작: SQL Server에서 R을 사용 하 여 예측 모델 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 빠른 시작에서는 R을 사용 하는 모델을 학습 하는 방법을 한 알아봅니다 다음 SQL Server의 테이블에 모델을 저장 합니다. 모델은 단순 일반화 된 선형 모델 (GLM) 수단 수동 전송을 사용 하 여 장식적인는 확률을 예측 합니다. 사용 하 여는 `mtcars` R.를 사용 하 여 포함 된 데이터 집합

## <a name="prerequisites"></a>사전 요구 사항

이전 빠른 시작에서는 [SQL Server에 있는지 확인 하는 R](quickstart-r-verify.md), 정보를 제공 하 고이 빠른 시작에 필요한 R 환경 설정에 대 한 링크입니다.

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

다음으로, 데이터 집합의 빌드에서 데이터를 삽입 `mtcars`합니다.

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

두 개의 열, 모두 숫자, 마 력 자동차 속도 데이터에 포함 되어 있습니다 (`hp`) 및 가중치 (`wt`). 이 데이터는 차량 수동 전송을 사용 하 여 장식적인는 확률을 예측 하는 일반화 된 선형 모델 (GLM) 만들게 됩니다.

모델을 작성 하려면 R 코드 내에서 수식을 정의 하 고 데이터 입력된 매개 변수로 전달 합니다.

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

+ 첫 번째 인수 `glm` 되는 *수식을* 매개 변수를 정의 하는 `am` 따라 `hp + wt`합니다.
+ 입력 데이터는 SQL 쿼리로 데이터를 채운 `MTCarsData` 변수에 저장됩니다. 입력 데이터에 특정 이름을 할당하지 않는 경우 기본 변수 이름은 _InputDataSet_ 입니다.

## <a name="create-a-table-for-the-model"></a>모델에 대 한 테이블 만들기

다음으로 다시 학습 하거나 예측에 사용할 수 있도록 모델을 저장 합니다. 모델을 만드는 R 패키지의 출력은 일반적으로 **이진 개체**입니다. 따라서 모델을 저장할 테이블의 열을 제공 해야 합니다 **varbinary (max)** 형식입니다.

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

모델을 마지막 빠른 시작에서 설정한 했으므로에서 예측을 생성 하 고 결과 출력 하는 방법을 배웁니다.

> [!div class="nextstepaction"]
> [빠른 시작: 모델에서 예측 및 그리기](quickstart-r-predict-from-model.md)