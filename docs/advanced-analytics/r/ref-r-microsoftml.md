---
title: MicrosoftML R 함수 라이브러리
description: SQL Server 2016 R Services에서 MicrosoftML 함수 라이브러리를 소개 하 고 R을 사용 하 여 Machine Learning Services SQL Server 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: af9e85586a2aad69a87072caa820fff4026d1feb
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715661"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML (SQL Server의 R 라이브러리)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**MicrosoftML** 은 고성능 기계 학습 알고리즘을 제공 하는 Microsoft의 R 함수 라이브러리입니다. 여기에는 학습 및 변환, 점수 매기기, 텍스트 및 이미지 분석, 기존 데이터에서 값을 파생 하기 위한 기능 추출을 위한 함수가 포함 됩니다.

기계 학습 Api는 내부 기계 학습 응용 프로그램을 위해 Microsoft에서 개발 했으며 다중 코어 처리 및 빠른 데이터 스트리밍을 사용 하 여 빅 데이터에 대 한 높은 성능을 지원 하기 위해 몇 년 동안 구체화 되었습니다. 또한 MicrosoftML에는 텍스트 및 이미지 처리를 위한 다양 한 변환이 포함 되어 있습니다.

## <a name="full-reference-documentation"></a>전체 참조 설명서

**MicrosoftML** 라이브러리는 여러 Microsoft 제품에 배포 되지만, SQL Server 또는 다른 제품에 라이브러리를 가져올 때 사용 됩니다. 함수는 동일 하기 때문에 [개별 RevoScaleR 함수에 대 한 설명서](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 는 Microsoft Machine Learning Server에 대 한 [R 참조](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 의 한 위치에만 게시 됩니다. 제품별 동작이 있는 경우 함수 도움말 페이지에 차이점이 표시 됩니다.

## <a name="versions-and-platforms"></a>버전 및 플랫폼

**MicrosoftML** 라이브러리는 R 3.4.3를 기반으로 하며 다음 Microsoft 제품 또는 다운로드 중 하나를 설치 하는 경우에만 사용할 수 있습니다.

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 컴퓨터 학습 서비스](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 이상](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R 클라이언트](set-up-a-data-science-client.md)

> [!NOTE]
> 전체 제품 릴리스 버전은 SQL Server 2017부터 Windows 전용입니다. **MicrosoftML** 에 대 한 Linux 지원은 [SQL Server 2019 미리 보기](../../linux/sql-server-linux-setup-machine-learning.md)의 새로운 기능입니다.

## <a name="package-dependencies"></a>패키지 종속성

**MicrosoftML** 의 알고리즘은 다음에 대 한 [RevoScaleR](ref-r-revoscaler.md) 에 종속 됩니다.

+ 데이터 원본 개체입니다. **MicrosoftML** 함수에서 사용 되는 데이터는 **RevoScaleR** 함수를 사용 하 여 생성 됩니다.
+ 원격 컴퓨팅 (원격 SQL Server 인스턴스로 함수 실행 이동) **RevoScaleR** 라이브러리는 SQL server에 대 한 원격 계산 컨텍스트를 만들고 활성화 하는 함수를 제공 합니다.

대부분의 경우 **MicrosoftML**를 사용할 때마다 패키지를 함께 로드 합니다.

## <a name="functions-by-category"></a>범주별 함수

이 섹션에서는 각 함수를 사용 하는 방법에 대 한 아이디어를 제공 하기 위해 범주별로 함수를 나열 합니다. [목차](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 를 사용 하 여 알파벳 순서로 함수를 찾을 수도 있습니다.

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1-기계 학습 알고리즘

| 함수 이름 | 설명 |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | FastRank의 구현으로, 마트 그라데이션 향상 알고리즘을 효율적으로 구현 합니다.  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | [Rxfasttrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)를 사용 하는 임의 포리스트 및 변 위치 회귀 포리스트 구현.  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | BFGS를 사용 하 여 회귀를 로지스틱 합니다.  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | 한 클래스가 벡터 컴퓨터를 지원 합니다.  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | 이진, 다중 클래스 및 회귀 신경망입니다.  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | 선형 이진 분류 및 회귀에 대 한 듀얼 좌표 어센더 최적화를 추계 합니다. |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | 단일 모델에서 얻을 수 있는 것 보다 더 나은 예측 성능을 얻기 위해 다양 한 종류의 모델을 학습 합니다.|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2 변환 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | 여러 열에서 단일 벡터 값 열을 만드는 변환입니다.  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | 사전을 사용 하 여 범주 변형을 사용 하 여 표시기 벡터를 만듭니다.  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | 해시를 통해 범주 값을 표시기 배열로 변환 합니다. |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | 지정 된 텍스트 모음에서 n 그램 이라고 하는 연속 단어 시퀀스 수의 모음을 생성 합니다. 언어 검색, 토큰화, 중지 단어 제거, 텍스트 정규화 및 기능 생성을 제공 합니다.  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | 자연어 텍스트의 점수를 입력 하 고 텍스트의 정서가 양수인 확률을 포함 하는 열을 만듭니다.|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | 개수 기반 및 해시 기반 기능 추출에 대 한 인수를 정의할 수 있습니다.|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | 다시 학습 열 집합을 선택 하 여 다른 모든 항목을 삭제 합니다. |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | 지정 된 모드를 사용 하 여 지정 된 변수에서 기능을 선택 합니다.|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | 이미지 데이터를 로드 합니다.|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | 지정 된 크기 조정 메서드를 사용 하 여 지정 된 차원으로 이미지의 크기를 조정 합니다.|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | 이미지에서 픽셀 값을 추출 합니다.|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | 미리 학습 된 심층 신경망 모델을 사용 하 여 이미지를 특성화 합니다.|


## <a name="3-scoring-and-training-functions"></a>3-점수 매기기 및 학습 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | SQL Server에서 저장 프로시저를 사용 하거나, R 코드에서 실시간 점수 매기기를 사용 하 여 예측 성능을 훨씬 빠르게 제공할 수 있도록 점수 매기기 라이브러리를 실행 합니다.|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | 입력 데이터 집합의 데이터를 출력 데이터 집합으로 변환 합니다.|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | Microsoft R Machine Learning 모델에 대 한 요약을 제공 합니다.|


## <a name="4-loss-functions-for-classification-and-regression"></a>4-분류 및 회귀에 대 한 손실 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 지 수 분류 손실 함수에 대 한 사양입니다. | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 로그 분류 손실 함수에 대 한 사양입니다.  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 힌지 분류 손실 함수에 대 한 사양입니다. | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 부드러운 힌지 분류 손실 함수에 대 한 사양입니다.  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 포아송 회귀 손실 함수에 대 한 사양입니다. | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 제곱 회귀 손실 함수에 대 한 사양입니다.   |   

## <a name="5-feature-selection-functions"></a>5-기능 선택 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | 개수 모드의 기능 선택에 대 한 사양입니다. |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | 상호 정보 모드에서 기능 선택에 대 한 사양입니다. |

## <a name="6-ensemble-modeling-functions"></a>6-앙상블 모델링 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | [RxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)를 사용 하 여 빠른 트리 모델을 학습 하는 함수 이름과 인수를 포함 하는 목록을 만듭니다.|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | [RxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)를 사용 하 여 빠른 포리스트 모델을 학습 하는 함수 이름과 인수를 포함 하는 목록을 만듭니다.|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | [RxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)를 사용 하 여 빠른 선형 모델을 학습 하는 함수 이름과 인수를 포함 하는 목록을 만듭니다.|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | [RxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)를 사용 하 여 로지스틱 회귀 모델을 학습 하는 함수 이름과 인수를 포함 하는 목록을 만듭니다.|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | [RxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)를 사용 하 여 OneClassSvm 모델을 학습 하는 함수 이름과 인수를 포함 하는 목록을 만듭니다.|

## <a name="7-neural-networking-functions"></a>7-신경망 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | [Rxneuralnet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) 기계 학습 알고리즘에 대 한 최적화 알고리즘을 지정 합니다.|


## <a name="8-package-state-functions"></a>8-패키지 상태 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | 패키지 전체 상태를 저장 하는 데 사용 되는 환경 개체입니다. |


## <a name="how-to-use-microsoftml"></a>MicrosoftML 사용 방법

**MicrosoftML** 의 함수는 저장 프로시저에서 캡슐화 된 R 코드에서 호출할 수 있습니다. 대부분의 개발자는 **MicrosoftML** 솔루션을 로컬로 빌드한 다음 배포 연습으로 완료 된 R 코드를 저장 프로시저로 마이그레이션합니다.

R에 대 한 **MicrosoftML** 패키지는 SQL Server 2017의 "기본"으로 설치 됩니다. 인스턴스에 대 한 R 구성 요소를 업그레이드 하는 경우에도 SQL Server 2016와 함께 사용할 수 있습니다. [바인딩을 사용 하 여 SQL Server 인스턴스 업그레이드](../install/upgrade-r-and-python.md)

패키지는 기본적으로 로드 되지 않습니다. 첫 번째 단계로, **MicrosoftML** 패키지를 로드 한 다음 원격 계산 컨텍스트 또는 관련 된 연결 또는 데이터 원본 개체를 사용 해야 하는 경우 **RevoScaleR** 를 로드 합니다. 그런 다음 필요한 개별 함수를 참조 합니다.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>참조

+ [R 자습서](../tutorials/sql-server-r-tutorials.md)
+ [계산 컨텍스트 사용 방법 알아보기](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [SQL 개발자를 위한 R: 모델 학습 및 운영](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub의 Microsoft 제품 샘플](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 참조 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 