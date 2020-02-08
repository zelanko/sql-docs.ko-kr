---
title: microsoftml Python 패키지
description: SQL Server Machine Learning 워크로드와 관련하여 Python용 Microsoft Machine Learning 알고리즘 및 모델을 소개합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7ecbfd2edd20a312fc8a6d451938f1407585ded5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73706955"
---
# <a name="microsoftml-python-module-in-sql-server"></a>microsoftml(SQL Server의 Python 모듈)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**microsoftml**은 고성능 기계 학습 알고리즘을 제공하는 Microsoft의 Python35 호환 모듈입니다. 여기에는 학습 및 변환, 점수 매기기, 텍스트 및 이미지 분석, 기존 데이터에서 값을 파생하기 위한 기능 추출을 위한 함수가 포함됩니다.

기계 학습 API는 내부 기계 학습 애플리케이션을 위해 Microsoft에서 개발했으며, 다중 코어 처리 및 빠른 데이터 스트리밍을 사용하여 빅 데이터에 대한 고성능을 지원하기 위해 수년에 걸쳐 조정되었습니다. 이 패키지는 유사한 함수를 포함하는 R 버전 [MicrosoftML](../r/ref-r-microsoftml.md)과 동급인 Python으로 작성되었습니다. 

## <a name="full-reference-documentation"></a>전체 참조 설명서

**microsoftml** 라이브러리는 여러 Microsoft 제품에 배포되지만, SQL Server에서 라이브러리를 가져오든, 다른 제품에서 라이브러리를 가져오든, 사용 방식은 동일합니다. 함수는 동일하기 때문에 [개별 microsoftml 함수에 대한 설명서](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)는 Microsoft Machine Learning Server에 대한 [Python 참조](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) 아래의 한 위치에만 게시됩니다. 제품별로 고유한 동작이 있는 경우 함수 도움말 페이지에 차이점이 표시됩니다.

## <a name="versions-and-platforms"></a>버전 및 플랫폼

**microsoftml** 모듈은 Python 3.5을 기준으로 하며, 다음 Microsoft 제품 또는 다운로드 중 하나를 설치한 경우에만 사용할 수 있습니다.

+ [SQL Server Machine Learning 서비스](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 이상](https://docs.microsoft.com/machine-learning-server/)
+ [데이터 과학 클라이언트용 Python 클라이언트 라이브러리](setup-python-client-tools-sql.md)

> [!NOTE]
> 전체 제품 릴리스 버전은 SQL Server 2017에서 Windows 전용입니다. Windows 및 Linux는 [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md)의 **microsoftml**에서 둘 다 지원됩니다.

## <a name="package-dependencies"></a>패키지 종속성

**microsoftml**의 알고리즘은 다음에 대해 [revoscalepy](ref-py-revoscalepy.md)에 따라 좌우됩니다.

+ 데이터 원본 개체 **microsoftml** 함수에서 사용하는 데이터는 **revoscalepy** 함수를 사용하여 생성됩니다.
+ 원격 컴퓨팅(원격 SQL Server 인스턴스로 함수 실행 이동) **revoscalepy** 라이브러리는 SQL Server에 대한 원격 컴퓨팅 컨텍스트를 만들고 활성화하는 함수를 제공합니다.

대부분의 경우 **microsoftml**을 사용할 때마다 패키지를 함께 로드하게 됩니다.

## <a name="functions-by-category"></a>범주별 함수

이 섹션에서는 사용 방법에 대한 이해를 돕기 위해 각 함수를 범주별로 구분해서 제공합니다. [목차](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)를 사용하여 사전순으로 함수를 찾을 수도 있습니다.

## <a name="1-training-functions"></a>1 - 학습 함수

| 함수 | Description |
|----------|-------------|
|[microsoftml rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | 모델 앙상블을 학습합니다. |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | 임의 포리스트입니다. |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | 선형 모델입니다. SDCA(Stochastic Dual Coordinate Ascent)를 사용합니다. |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | 부스팅 트리입니다. |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | 로지스틱 회귀 분석입니다. |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | 신경망입니다. |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | 변칙 검색입니다. |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2 - 변환 함수

### <a name="categorical-variable-handling"></a>범주 변수 처리

| 함수 | Description |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | 텍스트 열을 범주로 변환합니다. |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | 텍스트 열을 해시하고 범주로 변환합니다. |

### <a name="schema-manipulation"></a>스키마 조작

| 함수 | Description |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | 여러 열을 단일 벡터로 연결합니다. |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | 데이터 세트에서 열을 삭제합니다. |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | 데이터 세트의 열을 유지합니다. |


### <a name="variable-selection"></a>변수 선택

| 함수 | Description |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |개수에 따른 기능 선택입니다. |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | 상호 정보에 따른 기능 선택입니다. |


### <a name="text-analytics"></a>텍스트 분석

| 함수 | Description |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | 텍스트 열을 숫자 기능으로 변환합니다. |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | 감정 분석입니다. |


### <a name="image-analytics"></a>이미지 분석 

| 함수 | Description |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | 이미지를 로드합니다. |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | 이미지 크기를 조정합니다. |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | 이미지에서 픽셀을 추출합니다. |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 이미지를 기능으로 변환합니다. |

### <a name="featurization-functions"></a>기능화 함수

| 함수 | Description |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | 데이터 원본에 대한 데이터 변환 |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3 - 점수 매기기 함수

| 함수 | Description |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | Microsoft Machine Learning 모델을 사용하여 점수 매기기 |

## <a name="how-to-call-microsoftml"></a>microsoftml을 호출하는 방법

**microsoftml**의 함수는 저장 프로시저에서 캡슐화된 Python 코드에서 호출할 수 있습니다. 대부분의 개발자는 **microsoftml** 솔루션을 로컬로 빌드한 다음, 완성된 Python 코드를 배포 연습으로 사용하기 위해 저장 프로시저로 마이그레이션합니다.

Python용 **microsoftml** 패키지는 기본적으로 설치되지만 **revoscalepy**와 달리, SQL Server와 함께 설치된 Python 실행 파일을 사용하여 Python 세션을 시작할 때는 기본적으로 로드되지 않습니다.

첫 번째 단계로 **microsoftml** 패키지를 가져오고, 원격 컴퓨팅 컨텍스트 또는 관련된 연결 또는 데이터 원본 개체를 사용해야 하는 경우 **revoscalepy**를 가져옵니다. 그런 다음, 필요한 개별 함수를 참조합니다.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>참고 항목

+ [Python 자습서](../tutorials/sql-server-python-tutorials.md)
+ [자습서: T-SQL에 Python 코드 포함](../tutorials/run-python-using-t-sql.md)
+ [Python 참조(Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

