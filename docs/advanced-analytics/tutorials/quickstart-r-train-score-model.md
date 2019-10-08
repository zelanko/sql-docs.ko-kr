---
title: R에서 예측 모델 만들기 및 점수 매기기
titleSuffix: SQL Server Machine Learning Services
description: SQL Server Machine Learning Services를 사용 하 여 R에서 간단한 예측 모델을 만든 다음 새 데이터를 사용 하 여 결과를 예측 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fc968c9364f23826b366721590f72ac1b0af0391
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005983"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-r-with-sql-server-machine-learning-services"></a>빠른 시작: SQL Server를 사용 하 여 R에서 예측 모델 생성 및 점수 매기기 Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 빠른 시작에서는 R을 사용 하 여 예측 모델을 만들고 학습 하 고, 모델을 SQL Server 인스턴스의 테이블에 저장 한 다음, 모델을 사용 하 여 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)를 사용 하 여 새 데이터의 값을 예측할 수 있습니다.

이 빠른 시작에서 사용할 모델은 차량에서 수동 전송에 적합 한 확률을 예측 하는 단순한 일반화 된 선형 모델 (글 화 m)입니다. R에 포함 된 **mtcars** 데이터 집합을 사용 합니다.

> [!TIP]
> 선형 모델에 리프레셔가 필요한 경우 rxLinMod를 사용 하 여 모델을 맞추는 프로세스를 설명 하는이 자습서를 사용해 보세요.  [Fitting Linear Models](/machine-learning-server/r/how-to-revoscaler-linear-model)(선형 모델 맞춤)

## <a name="prerequisites"></a>사전 요구 사항

- 이 빠른 시작을 사용 하려면 R 언어가 설치 된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 를 사용 하 여 SQL Server 인스턴스에 액세스 해야 합니다.

  SQL Server 인스턴스는 Azure 가상 머신 또는 온-프레미스에 있을 수 있습니다. 외부 스크립팅 기능은 기본적으로 사용 하지 않도록 설정 되어 있으므로 [외부 스크립팅을 사용 하도록 설정](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) 하 고 시작 하기 전에 **SQL Server 실행 패드 서비스가** 실행 중인지 확인 해야 할 수 있습니다.

- R 스크립트를 포함 하는 SQL 쿼리를 실행 하기 위한 도구도 필요 합니다. 모든 데이터베이스 관리 또는 쿼리 도구를 사용 하 여 이러한 스크립트를 실행 하 고 SQL Server 인스턴스에 연결 하 고 T-sql 쿼리 또는 저장 프로시저를 실행할 수 있습니다. 이 빠른 시작에서는 [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용 합니다.

## <a name="create-the-model"></a>모델 만들기

모델을 만들려면 학습을 위한 원본 데이터를 만들고, 모델을 만들고, 데이터를 사용 하 여 학습 한 다음, 새 데이터를 사용 하 여 예측을 생성 하는 데 사용할 수 있는 SQL 데이터베이스에 모델을 저장 합니다.

### <a name="create-the-source-data"></a>원본 데이터 만들기

1. **SQL Server Management Studio** 를 열고 SQL Server 인스턴스에 연결 합니다.

1. 학습 데이터를 저장할 테이블을 만듭니다.

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

1. 기본 제공 데이터 집합의 데이터를 `mtcars`으로 삽입 합니다.

   ```SQL
   INSERT INTO dbo.MTCars
   EXEC sp_execute_external_script @language = N'R'
       , @script = N'MTCars <- mtcars;'
       , @input_data_1 = N''
       , @output_data_1_name = N'MTCars';
   ```

   > [!TIP]
   > R 런타임에는 작고 큰 많은 데이터 세트가 포함되어 있습니다. R을 사용 하 여 설치 된 데이터 집합 목록을 가져오려면 R 명령 프롬프트에서 `library(help="datasets")`을 입력 합니다.

### <a name="create-and-train-the-model"></a>모델 만들기 및 학습

차 속도 데이터에는 두 개의 열, @no__t @no__t 즉 두 개의 열이 포함 됩니다. 이 데이터를 사용 하 여 차량에서 수동 전송에 적합 한 확률을 예측 하는 일반화 된 선형 모델 (글 화)을 만듭니다.

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

- @No__t에 대 한 첫 번째 인수는 `am`를 `hp + wt`에 따라 정의 하는 *수식* 매개 변수입니다.
- 입력 데이터는 SQL 쿼리로 데이터를 채운 `MTCarsData` 변수에 저장됩니다. 입력 데이터에 특정 이름을 할당하지 않는 경우 기본 변수 이름은 _InputDataSet_ 입니다.

### <a name="store-the-model-in-the-sql-database"></a>SQL 데이터베이스에 모델 저장

다음으로, 예측 또는 다시 학습 모델을 사용할 수 있도록 SQL 데이터베이스에 모델을 저장 합니다. 

1. 모델을 저장할 테이블을 만듭니다.

   모델을 만드는 R 패키지의 출력은 일반적으로 이진 개체입니다. 따라서 모델을 저장 하는 테이블은 **varbinary (max)** 유형의 열을 제공 해야 합니다.

   ```sql
   CREATE TABLE GLM_models (
       model_name varchar(30) not null default('default model') primary key,
       model varbinary(max) not null
   );
   ```

1. 다음 Transact-sql 문을 실행 하 여 저장 프로시저를 호출 하 고 모델을 생성 한 다음 만든 테이블에 저장 합니다.

   ```sql
   INSERT INTO GLM_models(model)
   EXEC generate_GLM;
   ```

   > [!TIP]
   > 이 코드를 두 번째로 실행 하면 다음 오류가 발생 합니다. "PRIMARY KEY 제약 조건 위반 ... 개체 stopping_distance_models "에 중복 키를 삽입할 수 없습니다. 이 오류를 방지하는 한 가지 옵션은 각 새 모델의 이름을 업데이트하는 것입니다. 예를 들어 모델의 유형, 생성한 날짜 등을 포함해서 좀 더 서술적인 이름으로 변경할 수 있습니다.

     ```sql
     UPDATE GLM_models
     SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
     WHERE model_name = 'default model'
     ```

## <a name="score-new-data-using-the-trained-model"></a>학습 된 모델을 사용 하 여 새 데이터 점수 매기기

*점수 매기기* 는 학습 된 모델에 공급 되는 새 데이터를 기반으로 예측, 확률 또는 기타 값을 생성 하는 것을 의미 하는 데이터 과학에 사용 되는 용어입니다. 이전 섹션에서 만든 모델을 사용 하 여 새 데이터에 대 한 예측 점수를 계산 합니다.

### <a name="create-a-table-of-new-data"></a>새 데이터의 테이블 만들기

먼저 새 데이터가 있는 테이블을 만듭니다.

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

### <a name="predict-manual-transmission"></a>수동 전송 예측

모델을 기반으로 예측을 가져오려면 다음을 수행 하는 SQL 스크립트를 작성 합니다.

1. 원하는 모델을 가져옵니다.
1. 새 입력 데이터를 가져옵니다.
1. 해당 모델과 호환되는 R 예측 함수를 호출합니다.

시간이 지남에 따라 테이블은 여러 R 모델을 포함 하거나 다른 매개 변수 또는 알고리즘을 사용 하 여 작성 되거나 다른 데이터 하위 집합에 대해 학습 될 수 있습니다. 이 예제에서는 `default model` 이라는 모델을 사용 합니다.

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

위의 스크립트는 다음 단계를 수행 합니다.

- SELECT 문을 사용하여 테이블에서 단일 모델을 가져오고 입력 매개 변수로 전달합니다.

- 테이블에서 모델을 검색한 후 모델에서 `unserialize` 함수를 호출합니다.

- 모델에 필요한 인수들로 `predict` 함수를 적용하고 새 입력 데이터를 제공합니다.

> [!NOTE]
> 예제에서 추가된 `str` 함수는 테스트 단계에 R에서 반환되는 데이터의 스키마를 확인하기 위한 용도입니다. 나중에 제거할 수 있습니다.
>
> R 스크립트에 사용된 열 이름은 저장 프로시저 출력으로 반드시 전달되지는 않습니다. 여기서 WITH RESULTS 절은 몇 가지 새로운 열 이름을 정의 하는 데 사용 됩니다.

**결과**

![수동 전송의 properbility 예측에 대 한 결과 집합](./media/r-predict-am-resultset.png)

또한 [PREDICT (transact-sql)](../../t-sql/queries/predict-transact-sql.md) 문을 사용 하 여 저장 된 모델을 기반으로 예측 된 값 이나 점수를 생성할 수 있습니다.

## <a name="next-steps"></a>다음 단계

Machine Learning Services SQL Server에 대 한 자세한 내용은 다음을 참조 하세요.

- [SQL Server Machine Learning Services (Python 및 R)는 무엇 인가요?](../what-is-sql-server-machine-learning.md)
