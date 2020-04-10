---
title: MicrosoftML R 함수 라이브러리
description: SQL Server 2016 R Services 및 SQL Server Machine Learning Services(R 포함)의 MicrosoftML 함수 라이브러리를 소개합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 450091bba39cf10e551b8da5e62993ca676c64af
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117446"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML(SQL Server의 R 라이브러리)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**MicrosoftML**은 고성능 기계 학습 알고리즘을 제공하는 Microsoft의 R 함수 라이브러리입니다. 여기에는 학습 및 변환, 점수 매기기, 텍스트 및 이미지 분석, 기존 데이터에서 값을 파생하기 위한 기능 추출을 위한 함수가 포함됩니다.

기계 학습 API는 내부 기계 학습 애플리케이션을 위해 Microsoft에서 개발했으며, 다중 코어 처리 및 빠른 데이터 스트리밍을 사용하여 빅 데이터에 대한 고성능을 지원하기 위해 수년에 걸쳐 조정되었습니다. 또한 MicrosoftML에는 텍스트 및 이미지 처리를 위한 다양한 변환이 포함되어 있습니다.

## <a name="full-reference-documentation"></a>전체 참조 설명서

**MicrosoftML** 라이브러리는 여러 Microsoft 제품에 배포되지만, SQL Server에서 라이브러리를 가져오든, 다른 제품에서 라이브러리를 가져오든, 사용 방식은 동일합니다. 함수는 동일하기 때문에 [개별 RevoScaleR 함수에 대한 설명서](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)는 Microsoft Machine Learning Server에 대한 [R 참조](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 아래의 한 위치에만 게시됩니다. 제품별로 고유한 동작이 있는 경우 함수 도움말 페이지에 차이점이 표시됩니다.

## <a name="versions-and-platforms"></a>버전 및 플랫폼

**MicrosoftML** 라이브러리는 R 3.4.3을 기준으로 하며, 다음 Microsoft 제품 또는 다운로드 중 하나를 설치한 경우에만 사용할 수 있습니다.

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server Machine Learning 서비스](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 이상](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R Client](set-up-a-data-science-client.md)

> [!NOTE]
> 전체 제품 릴리스 버전은 SQL Server 2017에서 Windows 전용입니다. Windows 및 Linux는 [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md)의 **MicrosoftML**에서 둘 다 지원됩니다.

## <a name="package-dependencies"></a>패키지 종속성

**MicrosoftML**의 알고리즘은 다음에 대해 [RevoScaleR](ref-r-revoscaler.md)에 따라 좌우됩니다.

+ 데이터 원본 개체 **MicrosoftML** 함수에서 사용하는 데이터는 **RevoScaleR** 함수를 사용하여 생성됩니다.
+ 원격 컴퓨팅(원격 SQL Server 인스턴스로 함수 실행 이동) **RevoScaleR** 라이브러리는 SQL Server에 대한 원격 컴퓨팅 컨텍스트를 만들고 활성화하는 함수를 제공합니다.

대부분의 경우 **MicrosoftML**을 사용할 때마다 패키지를 함께 로드하게 됩니다.

## <a name="functions-by-category"></a>범주별 함수

이 섹션에서는 사용 방법에 대한 이해를 돕기 위해 각 함수를 범주별로 구분해서 제공합니다. [목차](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)를 사용하여 사전순으로 함수를 찾을 수도 있습니다.

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1 - 기계 학습 알고리즘

| 함수 이름 | Description |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | FastRank의 구현으로, MART 경사 부스팅 알고리즘의 유효 구현을 나타냅니다.  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)를 사용하는 임의 포리스트 및 분위 회귀 포리스트 구현입니다.  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | L-BFGS를 사용하는 로지스틱 회귀입니다.  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | 1 클래스 지원 벡터 컴퓨터입니다.  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | 이진, 다중 클래스 및 회귀 신경망입니다.  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | 선형 이진 분류 및 회귀에 대한 확률 이중 좌표 경사 최적화입니다. |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | 단일 모델에서 얻을 수 있는 것보다 더 나은 예측 성능을 얻기 위해 다양한 종류의 모델을 학습합니다.|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2 - 변환 함수

| 함수 이름 | Description |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | 여러 열에서 단일 벡터 값 열을 만드는 변환입니다.  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | 사전에서 범주별 변형을 사용하여 표시기 벡터를 만듭니다.  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | 해시를 통해 범주 값을 표시기 배열로 변환합니다. |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | 지정된 텍스트 모음에서 n 그램이라고 하는 연속된 수의 단어 시퀀스 모음을 생성합니다. 언어 검색, 토큰화, 중지 단어 제거, 텍스트 정규화 및 특성 생성을 제공합니다.  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | 자연어 텍스트의 점수를 매기고, 텍스트의 감정 점수가 양수인 확률을 포함하는 열을 만듭니다.|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | 개수 기반 및 해시 기반 기능 추출을 위한 인수를 정의할 수 있습니다.|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | 다시 학습할 열 세트를 선택하고 다른 모든 열은 삭제합니다. |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | 지정된 모드를 사용하여 지정된 변수에서 특성을 선택합니다.|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | 이미지 데이터를 로드합니다.|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | 지정된 크기 조정 메서드를 사용하여 지정된 차원으로 이미지의 크기를 조정합니다.|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | 이미지에서 픽셀 값을 추출합니다.|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | 미리 학습된 심층 신경망 모델을 사용하여 이미지를 특성화합니다.|


## <a name="3-scoring-and-training-functions"></a>3 - 점수 매기기 및 학습 함수

| 함수 이름 | Description |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | SQL Server에서 저장 프로시저를 사용하거나, R 코드에서 점수 매기기 라이브러리를 실행하여 실시간 점수 매기기를 통해 훨씬 더 빠른 예측 성능을 제공합니다.|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | 입력 데이터 세트의 데이터를 출력 데이터 세트로 변환합니다.|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | Microsoft R Machine Learning 모델에 대한 요약을 제공합니다.|


## <a name="4-loss-functions-for-classification-and-regression"></a>4 - 분류 및 회귀에 대한 손실 함수

| 함수 이름 | Description |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 지수 분류 손실 함수에 대한 사양입니다. | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 로그 분류 손실 함수에 대한 사양입니다.  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 힌지 분류 손실 함수에 대한 사양입니다. | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 매끄러운 힌지 분류 손실 함수에 대한 사양입니다.  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 포아송 회귀 손실 함수에 대한 사양입니다. | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 제곱 회귀 손실 함수에 대한 사양입니다.   |   

## <a name="5-feature-selection-functions"></a>5 - 특성 선택 함수

| 함수 이름 | Description |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | 개수 모드에서 특성 선택에 대한 사양입니다. |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | 상호 정보 모드에서 특성 선택에 대한 사양입니다. |

## <a name="6-ensemble-modeling-functions"></a>6 - 앙상블 모델링 함수

| 함수 이름 | Description |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)을 사용하여 빠른 트리 모델을 학습하기 위한 함수 이름과 인수를 포함하는 목록을 만듭니다.|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)을 사용하여 빠른 포리스트 모델을 학습하기 위한 함수 이름과 인수를 포함하는 목록을 만듭니다.|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)을 사용하여 빠른 선형 모델을 학습하기 위한 함수 이름과 인수를 포함하는 목록을 만듭니다.|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)을 사용하여 로지스틱 회귀 모델을 학습하기 위한 함수 이름과 인수를 포함하는 목록을 만듭니다.|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)을 사용하여 OneClassSvm 모델을 학습하기 위한 함수 이름과 인수를 포함하는 목록을 만듭니다.|

## <a name="7-neural-networking-functions"></a>7 - 신경망 함수

| 함수 이름 | Description |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) 기계 학습 알고리즘에 대한 최적화 알고리즘을 지정합니다.|


## <a name="8-package-state-functions"></a>8 - 패키지 상태 함수

| 함수 이름 | Description |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | 패키지 전체 상태를 저장하는 데 사용되는 환경 개체입니다. |


## <a name="how-to-use-microsoftml"></a>MicrosoftML 사용 방법

**MicrosoftML**의 함수는 저장 프로시저에서 캡슐화된 R 코드에서 호출할 수 있습니다. 대부분의 개발자는 **MicrosoftML** 솔루션을 로컬로 빌드한 다음, 완성된 R 코드를 배포 연습으로 사용하기 위해 저장 프로시저로 마이그레이션합니다.

R용 **MicrosoftML** 패키지는 SQL Server 2017에 "기본적으로" 설치됩니다. 예를 들어 R 구성 요소를 업그레이드하는 경우에도 SQL Server 2016에서 함께 사용할 수 있습니다. [바인딩을 사용하여 SQL Server 인스턴스 업그레이드](../install/upgrade-r-and-python.md)

패키지는 기본적으로 로드되지 않습니다. 첫 번째 단계로 **MicrosoftML** 패키지를 로드한 다음, 원격 컴퓨팅 컨텍스트 또는 관련된 연결 또는 데이터 원본 개체를 사용해야 하는 경우 **RevoScaleR**을 로드합니다. 그런 다음, 필요한 개별 함수를 참조합니다.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>참고 항목

+ [R 자습서](../tutorials/sql-server-r-tutorials.md)
+ [컴퓨팅 컨텍스트 사용 방법 알아보기](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [SQL 개발자를 위한 R: 모델 학습 및 운영](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub의 Microsoft 제품 샘플](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 참조(Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 