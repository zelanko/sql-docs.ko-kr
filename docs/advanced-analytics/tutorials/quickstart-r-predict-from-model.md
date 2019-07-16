---
title: R-SQL Server Machine Learning을 사용 하 여 모델에서 예측 하는 빠른 시작
description: 이 빠른 시작에서는 미리 작성 된 모델을 사용 하 여 R 및 SQL Server 데이터에 점수 매기기에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 00fdcb0c8c9c535645268a0212e52eef6f7c88f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961992"
---
# <a name="quickstart-predict-from-model-using-r-in-sql-server"></a>빠른 시작: SQL Server에서 R을 사용 하 여 모델에서 예측
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 빠른 시작에서는 새로운 데이터에 대 한 예측 점수를 매길 이전 빠른 시작에서 만든 모델을 사용 합니다. 새로운 데이터를 사용한 _채점(scoring)_ 을 위해서 테이블로부터 훈련된 모델 중 하나를 가져온 다음 예측을 기반으로 새로운 데이터 집합을 호출합니다. 채점이란 훈련된 모델에 주어진 새로운 데이터에 기반한 예측, 확률, 혹은 기타 값을 생성함을 의미하는 데이터 과학에서 종종 사용되는 용어입니다.

## <a name="prerequisites"></a>사전 요구 사항

이 빠른 시작은의 확장인 [예측 모델 만들기](quickstart-r-create-predictive-model.md)합니다.

## <a name="create-the-table-of-new-data"></a>새 데이터의 테이블 만들기

먼저, 새 데이터로 테이블을 만듭니다. 

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

## <a name="predict-manual-transmission"></a>수동 전송 예측

이제 프로그램 `dbo.GLM_models` 테이블 여러 R 모델을 다른 매개 변수 또는 알고리즘을 사용 하 여 빌드된 모든 포함 될 수 있습니다 또는 데이터의 여러 하위 집합에서 학습 합니다.

하나의 특정 모델을 기반으로 예측을 가져오려면 다음을 수행 하는 SQL 스크립트를 작성 해야 합니다.

1. 원하는 모델을 가져옵니다.
2. 새 입력 데이터를 가져옵니다.
3. 해당 모델과 호환되는 R 예측 함수를 호출합니다.

이 예제에서는 명명 된 모델 사용 `default model`합니다.

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

+ SELECT 문을 사용하여 테이블에서 단일 모델을 가져오고 입력 매개 변수로 전달합니다.

+ 테이블에서 모델을 검색한 후 모델에서 `unserialize` 함수를 호출합니다.

+ 모델에 필요한 인수들로 `predict` 함수를 적용하고 새 입력 데이터를 제공합니다.

+ 예제에서 추가된 `str` 함수는 테스트 단계에 R에서 반환되는 데이터의 스키마를 확인하기 위한 용도입니다. 나중에 제거할 수 있습니다.

+ R 스크립트에 사용된 열 이름은 저장 프로시저 출력으로 반드시 전달되지는 않습니다. 새 열 이름을 정의하는 WITH RESULTS 절을 사용했습니다.

**결과**

![수동 전송 properbility 예측의 결과 집합](./media/r-predict-am-resultset.png)

것도 사용할 수는 [TRANSACT-SQL의 PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) 예측된 값 또는 저장 된 모델을 기반으로 점수를 생성할 수 있습니다.

## <a name="next-steps"></a>다음 단계

R 및 SQL Server를 통합하면 고성능 데이터 처리 및 빠른 R 분석을 위해 R 및 관계형 데이터베이스의 최고 기능을 이용하여 R 솔루션을 대규모로 더 쉽게 배포할 수 있습니다. 

SQL Server를 사용 하 여 R을 사용 하 여 Microsoft 데이터 과학 및 R Services 개발 팀에서 생성 하는 종단 간 시나리오를 통해 솔루션에 대 한 학습을 계속 합니다.

> [!div class="nextstepaction"]
> [SQL Server R 자습서](sql-server-r-tutorials.md)
