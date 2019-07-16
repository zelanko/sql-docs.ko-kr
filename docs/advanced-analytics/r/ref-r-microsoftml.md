---
title: MicrosoftML R 함수 라이브러리-SQL Server Machine Learning 서비스
description: SQL Server 2016 R Services 및 R. 사용 하 여 SQL Server 2017 Machine Learning Services에서 MicrosoftML 함수 라이브러리 소개
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: e3dc94026f90ef769abb3889a716b5dadb317c4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962508"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML (SQL Server의 R 라이브러리)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**MicrosoftML** 는 고속 기계 학습 알고리즘을 제공 하는 Microsoft에서 R 함수 라이브러리입니다. 교육 및 변환, 점수 매기기, 텍스트 및 이미지 분석 및 기존 데이터에서 값을 파생 시키기 위한 기능 추출에 대 한 함수를 포함 합니다.

기계 학습 Api 내부 기계 학습 응용 프로그램, Microsoft에서 개발한 및 된 구체화 된 고성능 빅 데이터에서 수 년에 걸쳐 멀티 코어 처리 및 빠른 데이터 스트리밍을 사용 하 여 합니다. MicrosoftML에 텍스트 및 이미지 처리를 위한 다양 한 변환도 포함 됩니다.

## <a name="full-reference-documentation"></a>전체 참조 설명서

합니다 **MicrosoftML** 라이브러리는 여러 Microsoft 제품을 배포 하지만 SQL Server 또는 다른 제품에서 라이브러리를 표시 하는지 여부를 사용량은 동일 합니다. 함수는 동일 하므로 [개별 RevoScaleR 함수에 대 한 설명서](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 아래에 있는 하나의 위치에 게시 되는 [R 참조](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) Microsoft Machine Learning Server에 대 한 합니다. 모든 제품별 해야 동작 존재, 불일치 함수 도움말 페이지에 표시 됩니다.

## <a name="versions-and-platforms"></a>버전 및 플랫폼

합니다 **MicrosoftML** 라이브러리 이며 R 3.4.3에 따라 사용 가능한 다음 Microsoft 제품 또는 다운로드 중 하나를 설치 하는 경우에:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning 서비스](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 이상](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> 전체 제품 릴리스 버전은 Windows 전용 SQL Server 2017을 사용 하 여 시작 합니다. 에 대 한 Linux 지원을 **MicrosoftML** 의 새로운 [SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md)합니다.

## <a name="package-dependencies"></a>패키지 종속성

알고리즘 **MicrosoftML** 종속 [RevoScaleR](ref-r-revoscaler.md) 에 대 한 합니다.

+ 데이터 원본 개체입니다. 데이터를 사용할 **MicrosoftML** 함수를 사용 하 여 만들어지며 **RevoScaleR** 함수입니다.
+ 원격 (원격 SQL Server 인스턴스로 변화 함수 실행)를 계산 합니다. 합니다 **RevoScaleR** 라이브러리 만들기 및 원격 활성화에 대 한 계산 컨텍스트 SQL server에 대 한 함수를 제공 합니다.

대부분의 경우, 로드 하려는 패키지를 함께 사용할 때마다 **MicrosoftML**합니다.

## <a name="functions-by-category"></a>범주별으로 함수

이 섹션에서는 범주를 각각 사용 하는 방법의 아이디어를 제공 하 여 함수를 나열 합니다. 사용할 수도 있습니다는 [목차](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 알파벳 순서로 함수를 찾으려고 합니다.

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1-기계 학습 알고리즘

| 함수 이름 | 설명 |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | FastRank, MART 그라데이션 승격 알고리즘의 유효 구현의 구현입니다.  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | 임의 포리스트 및 변 위치 회귀 포리스트 사용 하 여 구현 [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees)합니다.  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | L-BFGS를 사용 하 여 로지스틱 회귀 분석입니다.  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | 1 클래스 지원 벡터 컴퓨터입니다.  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | 이진 파일, 다중 클래스 및 회귀 신경망입니다.  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | 선형 이진 분류 및 회귀에 대 한 확률적 이중 좌표 경사 최적화 합니다. |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | 다양 한 예측 성능 향상을 위해 단일 모델에서 가져올 수 있습니다 보다 가져오려고 다양 한 종류의 모델을 학습 합니다.|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2-변환 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | 여러 열에서 단일 벡터 반환 열을 만드는 변환입니다.  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | 표시기 벡터로를 변환 범주를 사용 하 여 사전을 사용 하 여 만듭니다.  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | 해시 하 여 범주 값을 표시기 배열로 변환합니다. |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | N-그램, 지정 된 텍스트 모음에에서 호출 하는 연속 단어의 시퀀스의 개수는 모음을 생성 합니다. 언어 감지, 토큰화, 중지 단어 제거, 텍스트 정규화 및 기능 생성을 제공 합니다.  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | 자연어 텍스트 점수 및 텍스트에서 정서 양수는 확률을 포함 하는 열을 만듭니다.|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | 개수 기반 및 해시 기반 기능 추출에 대 한 인수를 정의할 수 있습니다.|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | 삭제 하는 다른 모든 열을 다시 학습 하려면 집합을 선택 합니다. |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | 지정 된 모드를 사용 하 여 지정된 된 변수에서 기능을 선택 합니다.|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | 이미지 데이터를 로드 합니다.|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | 지정된 된 크기 조정 메서드를 사용 하 여 지정 된 차원에는 이미지 크기를 조정 합니다.|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | 이미지에서 픽셀 값을 추출합니다.|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | 미리 학습 된 심층 신경망 모델을 사용 하 여 이미지를 특성화 합니다.|


## <a name="3-scoring-and-training-functions"></a>3-점수 매기기 및 교육 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | 저장된 프로시저를 사용 하 여 SQL Server, 또는 훨씬 더 빠른 예측 성능을 제공 하기 위해 실시간 점수 매기기를 사용 하도록 설정 하는 R 코드에서 점수 매기기 라이브러리를 실행 합니다.|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | 출력 데이터 집합에는 입력된 데이터 집합에서 데이터를 변환합니다.|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | Microsoft R Machine Learning 모델의 요약을 제공합니다.|


## <a name="4-loss-functions-for-classification-and-regression"></a>분류 및 회귀에 대 한 4 손실 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 지 수 백오프 분류 손실 함수에 대 한 사양입니다. | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 로그 분류 손실 함수에 대 한 사양입니다.  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 힌지 분류 손실 함수에 대 한 사양입니다. | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 부드러운 힌지 분류 손실 함수에 대 한 사양입니다.  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 포아송 회귀 손실 함수에 대 한 사양입니다. | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | 제곱된 회귀 손실 함수에 대 한 사양입니다.   |   

## <a name="5-feature-selection-functions"></a>5-기능 선택 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | 세기 모드의 기능 선택에 대 한 사양입니다. |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | 상호 정보 모드의 기능 선택에 대 한 사양입니다. |

## <a name="6-ensemble-modeling-functions"></a>6-앙상블 모델링 기능

| 함수 이름 | 설명 |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | 함수 이름 및 사용 하 여 빠른 트리 모델을 학습 하는 인수를 포함 하는 목록을 만듭니다 [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)합니다.|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | 함수 이름 및 사용 하 여 빠른 포리스트 모델을 학습 하는 인수를 포함 하는 목록을 만듭니다 [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)합니다.|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | 함수 이름 및 사용 하 여 빠른 선형 모델을 학습 하는 인수를 포함 하는 목록을 만듭니다 [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)합니다.|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | 함수 이름과 인수를 사용 하 여 로지스틱 회귀 모델 학습을 포함 하는 목록을 만듭니다 [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)합니다.|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | 함수 이름과 인수를 사용 하 여 OneClassSvm 모델 학습을 포함 하는 목록을 만듭니다 [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble)합니다.|

## <a name="7-neural-networking-functions"></a>7-신경망 네트워킹 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | 에 대 한 최적화 알고리즘을 지정 합니다 [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) 기계 학습 알고리즘입니다.|


## <a name="8-package-state-functions"></a>8-패키지 상태 함수

| 함수 이름 | 설명 |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | 패키지 전체 상태를 저장 하는 데 사용 되는 환경 개체입니다. |


## <a name="how-to-use-microsoftml"></a>MicrosoftML를 사용 하는 방법

함수가 **MicrosoftML** 저장된 프로시저에서 캡슐화 하는 R 코드에서 호출할 수 있습니다. 대부분의 개발자는 빌드할 **MicrosoftML** 솔루션을 로컬로 다음 배포 연습으로 저장된 프로시저에 완성 된 R 코드를 마이그레이션합니다.

합니다 **MicrosoftML** R 설치 "-의-기본" SQL Server 2017에서에 대 한 패키지 있습니다. 인스턴스에 대 한 R 구성 요소를 업그레이드 하는 경우에 SQL Server 2016와 함께 사용할 수도: [바인딩을 사용 하 여 SQL Server 인스턴스 업그레이드](../install/upgrade-r-and-python.md)

기본적으로 패키지 로드 되지 않습니다. 첫 번째 단계로, 로드 된 **MicrosoftML** 패키지를 찾은 다음 로드 **RevoScaleR** 원격 계산 컨텍스트 또는 관련 된 연결 또는 데이터 원본 개체를 사용 해야 하는 경우. 그런 다음 필요한 개별 함수를 참조 합니다.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>참조

+ [R 자습서](../tutorials/sql-server-r-tutorials.md)
+ [계산 컨텍스트를 사용 하는 방법을 알아봅니다](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [SQL 개발자를 위한 R: 학습 및 모델 운영](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub의 Microsoft 제품 샘플](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R 참조 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 