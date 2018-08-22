---
title: 실시간 점수 매기기 또는 SQL Server Machine Learning에서 네이티브 점수 매기기를 수행 하는 방법 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: dfea308f268d666ce070c21a7dd9afa513f95406
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2018
ms.locfileid: "40394572"
---
# <a name="how-to-perform-real-time-scoring-or-native-scoring-in-sql-server"></a>실시간 점수 매기기 또는 SQL Server의 네이티브 점수 매기기를 수행 하는 방법
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server의 두 가지 방법에서 결과 예측에 대 한 R에서 작성 하는 미리 학습 된 모델을 사용 하 여 실시간을 보여 줍니다. 실시간 점수 매기기와 네이티브 점수 매기기 기계 학습 모델을 R을 설치 하지 않고도 사용할 수 있도록 설계 되었습니다. -SQL Server 데이터베이스에 저장-호환 형식으로 미리 학습 된 모델을 지정 신속 하 게 새 입력에 대 한 예측 점수를 생성 하려면 표준 데이터 액세스 기법을 사용할 수 있습니다.

## <a name="choose-a-scoring-method"></a>점수 매기기 방법 선택

다음 옵션은 빠른 일괄 처리 예측을 위해 지원 됩니다.

+ **네이티브 점수 매기기**: SQL Server 2017 Windows, SQL Server 2017 Linux 및 Azure SQL Database의 T-SQL PREDICT 함수입니다.
+ **실시간 점수 매기기**: sp를 사용 하 여\_rxPredict 저장 프로시저에서 SQL Server 2016 또는 SQL Server 2017 (Windows만 해당).

> [!NOTE]
> SQL Server 2017의 PREDICT 함수를 사용 하는 것이 좋습니다.
> Sp 데\_rxPredict SQLCLR 통합을 사용 해야 합니다. 이 옵션을 사용 하기 전에 보안 문제를 고려 합니다.

모델을 준비 하 고 점수를 생성 한 다음 전체 프로세스는 유사 합니다.

1. 지원 되는 알고리즘을 사용 하 여 모델을 만듭니다.
2. 특수 이진 형식을 사용 하 여 모델을 serialize 합니다.
3. SQL Server에 사용할 수 있는 모델을 확인 합니다. 일반적으로 즉, SQL Server 테이블에 직렬화 된 모델을 저장 합니다.
4. 함수 또는 저장된 프로시저를 호출 하 고 모델 및 입력된 데이터를 전달 합니다.

### <a name="requirements"></a>요구 사항

+ PREDICT 함수는 SQL Server 2017의 모든 버전에서 제공 하 고 기본적으로 활성화 됩니다. R을 설치 하거나 추가 기능을 활성화할 필요가 없습니다.

+ Sp를 사용 하는 경우\_rxPredict, 몇 가지 추가 단계가 필요 합니다. 참조 [실시간 점수 매기기를 사용 하도록 설정](#bkmk_enableRtScoring)합니다.

+ 이때 RevoScaleR 및 MicrosoftML 호환 되는 모델을 만들 수 있습니다. 나중에 추가 모델 유형에 사용할 수 있습니다. 현재 지원 되는 알고리즘 목록은 참조 하세요 [실시간 점수 매기기](../real-time-scoring.md)합니다.

### <a name="serialization-and-storage"></a>Serialization 및 저장소

빠른 점수 매기기 옵션 중 하나를 사용 하 여 모델을 사용 하려면 크기에 대 한 최적화 된 특수 한 serialize 된 형식을 사용 하 여 및 효율성을 점수 매기기 모델을 저장 합니다.

+ 호출 `rxSerializeModel` 지원 되는 모델을 작성 하는 **원시** 형식입니다.
+ 호출 `rxUnserializeModel` 다른 R 코드에서 사용 하 여 모델을 다시 구성 하기 위해 또는 모델을 표시 합니다.

자세한 내용은 [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)합니다.

**SQL을 사용 하 여**

사용 하 여 모델 학습 수 SQL 코드에서 `sp_execute_external_script`에서 직접 학습된 된 모델에 테이블 형식의 열을 삽입할 **varbinary (max)** 합니다.

간단한 예제를 보려면 [이 자습서](../tutorials/rtsql-create-a-predictive-model-r.md)

**R을 사용 하 여**

R 코드에서 모델을 테이블에 저장 하는 방법은 두 가지 있습니다.

+ 호출 된 `rxWriteObject` 모델 데이터베이스에 직접 작성 하는 RevoScaleR 패키지에서 작동 합니다.

  `rxWriteObject()` 함수 SQL Server와 같은 ODBC 데이터 소스에서 R 개체를 검색 또는 SQL Server 개체를 쓸 수 있습니다. API는 간단한 키-값 저장소를 따라 모델링 됩니다.
  
  이 함수를 사용 하는 경우에 먼저 새 serialization 함수를 사용 하 여 모델을 직렬화 해야 합니다. 그런 다음 설정 합니다 *serialize* 인수에서 `rxWriteObject` serialization 단계를 반복 하지 않으려면 FALSE로 합니다.

+ 파일에 원시 형식으로 모델을 저장할 수도 수 있으며 그런 다음 SQL Server에 파일에서 읽을 수 있습니다. 이동 하거나 환경 간에 모델을 복사 하는 경우에이 옵션이 유용할 수 있습니다.

## <a name="native-scoring-with-predict"></a>네이티브 예측 된 점수 매기기

이 예제에서는 모델을 만들고 T-SQL에서 실시간 예측 함수를 호출 합니다.

### <a name="step-1-prepare-and-save-the-model"></a>1단계. 준비 및 모델 저장

샘플 데이터베이스 및 필요한 테이블을 만들려면 다음 코드를 실행 합니다.

```SQL
CREATE DATABASE NativeScoringTest;
GO
USE NativeScoringTest;
GO
DROP TABLE IF EXISTS iris_rx_data;
GO
CREATE TABLE iris_rx_data (
  "Sepal.Length" float not null, "Sepal.Width" float not null
  , "Petal.Length" float not null, "Petal.Width" float not null
  , "Species" varchar(100) null
);
GO
```

데이터를 사용 하 여 데이터 테이블을 구성 하려면 다음 문을 사용 합니다 **아이리스** 데이터 집합입니다.

```SQL
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

이제 모델을 저장 하는 것에 대 한 테이블을 만듭니다.

```SQL
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

다음 코드를 기반으로 모델을 만듭니다는 **iris** 데이터 집합 이라는 테이블에 저장 **모델**합니다.

```SQL
DECLARE @model varbinary(max);
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'
    iris.sub <- c(sample(1:50, 25), sample(51:100, 25), sample(101:150, 25))
    iris.dtree <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris[iris.sub, ])
    model <- rxSerializeModel(iris.dtree, realtimeScoringOnly = TRUE)
    '
  , @params = N'@model varbinary(max) OUTPUT'
  , @model = @model OUTPUT
  INSERT [dbo].[ml_models]([model_name], [model_version], [native_model_object])
  VALUES('iris.dtree','v1', @model) ;
```

> [!NOTE] 
> 사용 해야 합니다 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) 모델을 저장 하는 RevoScaleR 함수입니다. 표준 R `serialize` 함수에 필요한 형식을 생성할 수 없습니다.

이진 형식으로 저장 된 모델을 보려면 다음을과 같은 문은 실행할 수 있습니다.

```SQL
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>2단계. 모델에 예측을 실행 합니다.

다음 간단한 예측 문을 사용 하 여 의사 결정 트리 모델에서 분류를 가져옵니다 합니다 **네이티브 점수 매기기** 함수입니다. 사용자가 제공한 특성, 꽃잎 길이 너비에 따라 붓 꽃 종류를 예측 합니다.

```SQL
DECLARE @model varbinary(max) = (
  SELECT native_model_object
  FROM ml_models
  WHERE model_name = 'iris.dtree'
  AND model_version = 'v1');
SELECT d.*, p.*
  FROM PREDICT(MODEL = @model, DATA = dbo.iris_rx_data as d)
  WITH(setosa_Pred float, versicolor_Pred float, virginica_Pred float) as p;
go
```

오류를 받게 되 면 "동안 오류가 발생 했습니다 PREDICT 함수를 실행 합니다. 모델이 손상 되었거나 잘못 된", 일반적으로 쿼리 모델을 반환 하지 않았습니다.을 의미 합니다. 모델 이름을 올바르게 입력 여부 또는 모델 테이블이 비어 있는지 확인 합니다.

> [!NOTE]
> 열 및 값을 반환 하므로 **PREDICT** 모델 유형별로 다를 수 있습니다 사용 하 여 반환된 된 데이터의 스키마를 정의 해야 합니다는 **WITH** 절.

## <a name="real-time-scoring-with-sprxpredict"></a>Sp_rxPredict으로 실시간 점수 매기기

이 섹션에서는 설정 하는 데 필요한 단계를 설명 **실시간** 예측을 T-SQL에서 함수를 호출 하는 방법의 예제를 제공 합니다.

### <a name ="bkmk_enableRtScoring"></a> 1 단계입니다. 실시간 점수 매기기 절차를 사용 하도록 설정

점수 매기기에 사용 하려는 각 데이터베이스에 대해이 기능을 활성화 해야 합니다. 서버 관리자에 RevoScaleR 패키지에 포함 되어 있는 명령줄 유틸리티를 RegisterRExt.exe를 실행 해야 합니다.

> [!NOTE]
> 작업 실시간 채 점을 위해 순서로 SQL CLR 기능을 사용 해야 인스턴스에; 또한 데이터베이스는 신뢰할 수 있는 표시 해야 합니다. 스크립트를 실행 하는 경우 이러한 함수를 수행 됩니다. 그러나이 작업을 수행 하기 전에 추가 보안에 미치는 영향을 고려해 야!

1. 관리자 권한 명령 프롬프트를 열고 RegisterRExt.exe가 있는 폴더로 이동 합니다. 기본 설치에서 경로 사용할 수 있습니다.
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. 인스턴스 및 확장된 저장된 프로시저를 사용 하도록 설정 하려는 대상 데이터베이스의 이름을 대체 하 여 다음 명령을 실행 합니다.

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    예를 들어 CLRPredict 데이터베이스 기본 인스턴스에서 확장된 저장된 프로시저에 추가 하려면 다음을 입력 합니다.

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    인스턴스 이름을 데이터베이스가 기본 인스턴스에 있는 경우 선택 사항입니다. 명명된 된 인스턴스를 사용 하는 경우 인스턴스 이름을 지정 해야 합니다.

3. RegisterRExt.exe 다음 개체를 만듭니다.

    + 신뢰할 수 있는 어셈블리
    + 저장된 프로시저 `sp_rxPredict`
    + 새 데이터베이스 역할을 `rxpredict_users`입니다. 데이터베이스 관리자가 실시간 점수 매기기 기능을 사용 하는 사용자에 권한을 부여 하려면이 역할을 사용 합니다.

4. 모든 사용자가 실행 해야 하는 추가 `sp_rxPredict` 새 역할을 합니다.

> [!NOTE]
> 
> SQL Server 2017에 추가 보안 조치의에서 경우 CLR 통합을 사용 하 여 문제를 방지 하기 위해 이러한 측정값도이 저장된 프로시저의 사용에 대해 추가적인 제한을 적용합니다. 

### <a name="step-2-prepare-and-save-the-model"></a>2단계. 준비 및 모델 저장

Sp에 의해 필요한 이진 형식\_rxPredict PREDICT 함수를 사용 하는 데 필요한 형식으로 동일 합니다. 따라서 R 코드에서 호출을 포함할 [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)를 지정 해야 하 고 `realtimeScoringOnly = TRUE`이 예제와 같이:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>3단계. Sp_rxPredict 호출

Sp 호출\_rxPredict 것은 다른 저장 프로시저입니다. 현재 릴리스에서 저장된 프로시저는 두 개의 매개 변수를 사용 합니다.  _\@모델_ 이진 형식으로 모델에 대 한 및  _\@inputData_ 점수 매기기에 사용 하 여 데이터에 대 한 정의 유효한 SQL 쿼리입니다.

PREDICT 함수에서 사용 되는 동일한 이진 형식 이므로 앞의 예제에서 모델 및 데이터 테이블을 사용할 수 있습니다.

```SQL
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 
> Sp에 대 한 호출\_rxPredict 점수 매기기에 대 한 입력된 데이터에 모델의 요구 사항과 일치 하는 열이 포함 되어 있지 않으면 실패 합니다. 현재 다음.NET 데이터 형식만 지원 됩니다: double, float, short, ushort, long, ulong 및 문자열입니다.
> 
> 따라서 실시간 점수 매기기에 사용 하기 전에 입력된 데이터에서 지원 되지 않는 형식 필터링 해야 합니다.
> 
> 해당 SQL 형식에 대 한 자세한 내용은 [SQL-CLR 형식 매핑](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) 하거나 [CLR 매개 변수 데이터 매핑](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data)합니다.

## <a name="disable-real-time-scoring"></a>실시간 점수 매기기를 사용 하지 않도록 설정

실시간 점수 매기기 기능을 사용 하지 않으려면 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 합니다. `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="real-time-scoring-in-other-microsoft-product"></a>다른 Microsoft 제품의 실시간 점수 매기기

독립 실행형 서버 또는 Microsoft Machine Learning Server 대신 SQL Server 데이터베이스 내 분석을 사용할 경우 저장된 프로시저 및 예측을 생성 하기 위한 T-SQL 함수 외에 다른 옵션입니다.

독립 실행형 서버 및 Machine Learning Server 지원의 개념을 *웹 서비스* 코드 배포에 대 한 합니다. 번들로 R 또는 Python 미리 학습 된 모델을 웹 서비스로 새 데이터 입력을 평가 하려면 런타임에 호출 합니다. 자세한 내용은 다음 문서를 참조하세요.

+ [Machine Learning Server에 웹 서비스는 무엇입니까?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [운영 화 란?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-operationalize-deploy-consume)
+ [Python 모델 azureml 모델-관리 sdk를 사용 하 여 웹 서비스로 배포](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [R 코드 블록 또는 실시간 모델을 새 웹 서비스로 게시](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [R에 대 한 mrsdeploy 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)
