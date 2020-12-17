---
title: '빠른 시작: R에서 모델 학습'
titleSuffix: SQL machine learning
description: 이 빠른 시작에서는 T를 사용하여 예측 모델을 만들어 학습시키고, 모델을 테이블에 저장한 다음, 모델에서 SQL 기계 학습을 사용하여 새 데이터로 값을 예측합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: 9e2f5f7d35eb029dce0b88825f3c60989e35db06
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470234"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-r-with-sql-machine-learning"></a>빠른 시작: R에서 SQL 기계 학습을 사용하여 예측 모델 만들기 및 채점
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
이 빠른 시작에서는 T를 사용하여 예측 모델을 만들어 학습시키고, 모델을 SQL Server 인스턴스의 테이블에 저장한 다음, 모델에서 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) 또는 [빅 데이터 클러스터](../../big-data-cluster/machine-learning-services.md)를 사용하여 새 데이터로 값을 예측합니다.
::: moniker-end
::: moniker range="=sql-server-2017"
이 빠른 시작에서는 T를 사용하여 예측 모델을 만들어 학습시키고, 모델을 SQL Server 인스턴스의 테이블에 저장한 다음, [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)를 사용하여 모델로 새 데이터의 값을 예측합니다.
::: moniker-end
::: moniker range="=sql-server-2016"
이 빠른 시작에서는 T를 사용하여 예측 모델을 만들어 학습시키고, 모델을 SQL Server 인스턴스의 테이블에 저장한 다음, 모델에서 [SQL Server R Services](../r/sql-server-r-services.md)를 사용하여 새 데이터로 값을 예측합니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
이 빠른 시작에서는 T를 사용하여 예측 모델을 만들어 학습시키고, 모델을 SQL Server 인스턴스의 테이블에 저장한 다음, [Azure SQL Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)를 사용하여 모델로 새 데이터의 값을 예측합니다.
::: moniker-end

SQL에서 실행되는 두 개의 저장 프로시저를 만들고 실행합니다. 첫 번째 저장 프로시저는 R에 포함된 **mtcars** 데이터 세트를 사용하여 차량에 수동 변속기가 장착되었을 확률을 예측하는 단순한 일반화된 선형 모델(GLM)을 생성합니다. 두 번째 저장 프로시저는 첫 번째 프로시저에서 생성된 모델을 호출하여 새 데이터를 기반으로 예측 세트를 출력합니다. SQL 저장 프로시저에 R 코드를 배치하면 작업이 SQL에 포함되고 다시 사용할 수 있으며 다른 저장 프로시저와 클라이언트 애플리케이션에서 호출할 수 있습니다.

> [!TIP]
> 선형 모델에 리프레셔가 필요한 경우 rxLinMod를 사용하여 모델을 맞추는 프로세스를 설명하는 다음 자습서를 참조하세요. [선형 모델 맞춤](/machine-learning-server/r/how-to-revoscaler-linear-model) 자습서를 권장합니다.

이 빠른 시작을 완료하면 다음을 배울 수 있습니다.

> [!div class="checklist"]
> - 저장 프로시저에 R 코드를 포함하는 방법
> - 저장 프로시저의 입력을 통해 코드에 입력을 전달하는 방법
> - 저장 프로시저를 사용하여 모델을 운영하는 방법

## <a name="prerequisites"></a>사전 요구 사항

이 빠른 시작을 실행하려면 다음과 같은 필수 구성 요소가 필요합니다.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
- SQL Server Machine Learning Services. Machine Learning Services를 설치하려면 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md) 또는 [Linux 설치 가이드](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)를 참조하세요. [SQL Server 빅 데이터 클러스터에서 Machine Learning Services를 사용하도록 설정](../../big-data-cluster/machine-learning-services.md)할 수도 있습니다.
::: moniker-end
::: moniker range="=sql-server-2017"
- SQL Server Machine Learning Services. Machine Learning Services를 설치하려면 [Windows 설치 가이드](../install/sql-machine-learning-services-windows-install.md)를 참조하세요. 
::: moniker-end
::: moniker range="=sql-server-2016"
- SQL Server 2016 R Services. R Services를 설치하려면 [Windows 설치 가이드](../install/sql-r-services-windows-install.md)를 참조하세요.
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
- Azure SQL Managed Instance Machine Learning Services. 자세한 내용은 [Azure SQL Managed Instance Machine Learning Services 개요](/azure/azure-sql/managed-instance/machine-learning-services-overview)를 참조하세요.
::: moniker-end

- R 스크립트가 포함된 SQL 쿼리를 실행하기 위한 도구. 이 빠른 시작에서는 [Azure Data Studio](../../azure-data-studio/what-is.md)를 사용합니다.

## <a name="create-the-model"></a>모델 만들기

모델을 만들려면 학습시킬 원본 데이터를 만들고, 모델을 만들고, 데이터를 사용하여 학습시킨 다음, 새 데이터로 예측을 생성하는 데 사용할 수 있는 데이터베이스에 모델을 저장합니다.

### <a name="create-the-source-data"></a>원본 데이터 만들기

1. Azure Data Studio를 열고 인스턴스에 연결한 다음, 새 쿼리 창을 엽니다.

1. 먼저 학습 데이터를 저장할 테이블을 만듭니다.

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

1. 기본 제공 데이터 세트 `mtcars`의 데이터를 삽입합니다.

   ```SQL
   INSERT INTO dbo.MTCars
   EXEC sp_execute_external_script @language = N'R'
       , @script = N'MTCars <- mtcars;'
       , @input_data_1 = N''
       , @output_data_1_name = N'MTCars';
   ```

   > [!TIP]
   > R 런타임에는 작고 큰 많은 데이터 세트가 포함되어 있습니다. R과 함께 설치된 데이터 세트 목록을 가져오려면 R 명령 프롬프트에서 `library(help="datasets")`를 입력합니다.

### <a name="create-and-train-the-model"></a>모델 만들기 및 학습

자동차 속도 데이터에는 둘 다 숫자인 마력(`hp`) 및 중량(`wt`)의 두 열이 포함되어 있습니다. 이 데이터를 사용하여 차량에 수동 변속기가 장착되었을 확률을 예측하는 일반화된 선형 모델(GLM)을 만듭니다.

모델을 빌드하려면 R 코드 내에서 수식을 정의하고 데이터를 입력 매개 변수로 전달합니다.

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

- `glm`에 대한 첫 번째 인수는 `am`를 `hp + wt`에 종속된 것으로 정의하는 *formula* 매개 변수입니다.
- 입력 데이터는 SQL 쿼리에 의해 채워지는 `MTCarsData` 변수에 저장됩니다. 입력 데이터에 구체적인 이름을 할당하지 않으면 기본 변수 이름 _InputDataSet_ 가 사용됩니다.

### <a name="store-the-model-in-the-database"></a>모델을 데이터베이스에 저장

다음으로, 모델을 예측에 사용하거나 다시 학습시킬 수 있도록 데이터베이스에 저장합니다. 

1. 모델을 저장할 테이블을 만듭니다.

   모델을 만드는 R 패키지의 출력은 일반적으로 이진 개체입니다. 따라서 모델을 저장하는 테이블은 **varbinary(max)** 형식의 열을 제공해야 합니다.

   ```sql
   CREATE TABLE GLM_models (
       model_name varchar(30) not null default('default model') primary key,
       model varbinary(max) not null
   );
   ```

1. 다음 Transact-SQL 문을 실행하여 저장 프로시저를 호출하고 모델을 생성한 다음, 생성된 테이블에 저장합니다.

   ```sql
   INSERT INTO GLM_models(model)
   EXEC generate_GLM;
   ```

   > [!TIP]
   > 이 코드를 두 번째로 실행하면 다음 오류가 표시됩니다. "PRIMARY KEY 제약 조건 위반...dbo.stopping_distance_models 개체에 중복 키를 삽입할 수 없습니다." 이 오류를 방지하는 한 가지 옵션은 각 새 모델의 이름을 업데이트하는 것입니다. 예를 들어 좀 더 구체적인 이름으로 변경하고 모델 유형, 만든 날짜 등을 포함할 수 있습니다.

     ```sql
     UPDATE GLM_models
     SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
     WHERE model_name = 'default model'
     ```

## <a name="score-new-data-using-the-trained-model"></a>학습된 모델을 사용하여 새 데이터 채점

*채점* 이란 데이터 과학에서 사용되는 용어로, 학습된 모델에 공급되는 새로운 데이터를 기반으로 예측, 확률 또는 기타 값을 생성하는 것을 의미합니다. 이전 섹션에서 만든 모델을 사용하여 새 데이터에 대 한 예측 점수를 계산합니다.

### <a name="create-a-table-of-new-data"></a>새 데이터의 테이블 만들기

먼저 새 데이터로 테이블을 만듭니다.

```sql
CREATE TABLE dbo.NewMTCars(
    hp INT NOT NULL
    , wt DECIMAL(10,3) NOT NULL
    , am INT NULL
)
GO

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (110, 2.634)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (72, 3.435)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (220, 5.220)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (120, 2.800)
GO
```

### <a name="predict-manual-transmission"></a>수동 변속기 예측

모델을 기반으로 예측을 얻으려면 다음을 수행하는 SQL 스크립트를 작성해야 합니다.

1. 원하는 모델을 가져옵니다.
1. 새 입력 데이터를 가져옵니다.
1. 해당 모델과 호환되는 R 예측 함수를 호출합니다.

시간이 지나면서 테이블에 여러 R 모델이 포함되고 모든 모델은 서로 다른 매개 변수 또는 알고리즘을 사용하여 빌드되거나 다양한 데이터 하위 집합을 기반으로 학습됩니다. 이 예에서는 `default model`이라는 모델을 사용합니다.

```sql
DECLARE @glmmodel varbinary(max) = 
    (SELECT model FROM dbo.GLM_models WHERE model_name = 'default model');

EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(glmmodel));
            new <- data.frame(NewMTCars);
            predicted.am <- predict(current_model, new, type = "response");
            str(predicted.am);
            OutputDataSet <- cbind(new, predicted.am);
            '
    , @input_data_1 = N'SELECT hp, wt FROM dbo.NewMTCars'
    , @input_data_1_name = N'NewMTCars'
    , @params = N'@glmmodel varbinary(max)'
    , @glmmodel = @glmmodel
WITH RESULT SETS ((new_hp INT, new_wt DECIMAL(10,3), predicted_am DECIMAL(10,3)));
```

위의 스크립트는 다음 단계를 수행합니다.

- SELECT 문을 사용하여 테이블에서 단일 모델을 가져온 후 입력 매개 변수로 전달합니다.

- 테이블에서 모델을 검색한 후 모델에서 `unserialize` 함수를 호출합니다.

- 적절한 인수를 사용하여 `predict` 함수를 모델에 적용하고, 새 입력 데이터를 제공합니다.

> [!NOTE]
> 이 예에서는 R에서 반환되는 데이터의 스키마를 확인하기 위해 테스트 단계에서 `str` 함수가 추가되었습니다. 나중에 해당 문을 제거할 수 있습니다.
>
> R 스크립트에 사용된 열 이름이 저장 프로시저 출력에 반드시 전달되는 것은 아닙니다. 여기서 WITH RESULTS 절은 몇 가지 새로운 열 이름을 정의하는 데 사용됩니다.

**결과**

![수동 변속기의 확률 예측을 위한 결과 집합](./media/r-predict-am-resultset.png)

또한 [PREDICT(Transact-SQL)](../../t-sql/queries/predict-transact-sql.md) 문을 사용하여 저장된 모델을 기반으로 예측된 값이나 점수를 생성할 수 있습니다.

## <a name="next-steps"></a>다음 단계

SQL 기계 학습을 사용하는 R 자습서에 대한 자세한 내용은 다음을 참조하세요.

- [R 자습서](r-tutorials.md)
