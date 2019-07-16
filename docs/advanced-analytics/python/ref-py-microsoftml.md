---
title: microsoftml Python 패키지-SQL Server Machine Learning 서비스
description: Python에 대 한 SQL Server machine learning 작업에 관련 모델을 Microsoft 기계 학습 알고리즘을 소개 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 8f4c0eb20b0e0cd64065c7db0687b1dc36b2dbe7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962752"
---
# <a name="microsoftml-python-module-in-sql-server"></a>microsoftml (SQL Server에서 Python 모듈)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**microsoftml** 고속 기계 학습 알고리즘을 제공 하는 Microsoft에서 Python35-호환 되는 모듈입니다. 교육 및 변환, 점수 매기기, 텍스트 및 이미지 분석 및 기존 데이터에서 값을 파생 시키기 위한 기능 추출에 대 한 함수를 포함 합니다.

기계 학습 Api 내부 기계 학습 응용 프로그램에 대 한 Microsoft에서 개발한 및 된 구체화 된 고성능 빅 데이터에서 수 년에 걸쳐 멀티 코어 처리 및 빠른 데이터 스트리밍을 사용 하 여 합니다. 이 패키지는 R 버전의 Python과 같은 시작 [MicrosoftML](../r/ref-r-microsoftml.md), 있는 비슷한 함수입니다. 

## <a name="full-reference-documentation"></a>전체 참조 설명서

합니다 **microsoftml** 라이브러리는 여러 Microsoft 제품을 배포 하지만 SQL Server 또는 다른 제품에서 라이브러리를 표시 하는지 여부를 사용량은 동일 합니다. 함수는 동일 하므로 [개별 microsoftml 함수에 대 한 설명서](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 아래에 있는 하나의 위치에 게시 되는 [Python 참조](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) Microsoft Machine Learning Server에 대 한 합니다. 모든 제품별 해야 동작 존재, 불일치 함수 도움말 페이지에 표시 됩니다.

## <a name="versions-and-platforms"></a>버전 및 플랫폼

합니다 **microsoftml** 모듈은 Python 3.5에 기반 하 고 사용할 수 있는 다음과 같은 Microsoft 제품 또는 다운로드 중 하나를 설치 하는 경우에:

+ [SQL Server 2017 Machine Learning 서비스](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 이상](https://docs.microsoft.com/machine-learning-server/)
+ [데이터 과학 클라이언트에 대 한 Python 클라이언트 라이브러리](setup-python-client-tools-sql.md)

> [!NOTE]
> 전체 제품 릴리스 버전은 Windows 전용 SQL Server 2017을 사용 하 여 시작 합니다. 에 대 한 Linux 지원을 **microsoftml** 의 새로운 [SQL Server 2019 Preview](../../linux/sql-server-linux-setup-machine-learning.md)합니다.

## <a name="package-dependencies"></a>패키지 종속성

알고리즘 **microsoftml** 종속 [revoscalepy](ref-py-revoscalepy.md) 에 대 한 합니다.

+ 데이터 원본 개체입니다. 데이터를 사용할 **microsoftml** 함수를 사용 하 여 만들어지며 **revoscalepy** 함수입니다.
+ 원격 (원격 SQL Server 인스턴스로 변화 함수 실행)를 계산 합니다. 합니다 **revoscalepy** 라이브러리 만들기 및 원격 활성화에 대 한 계산 컨텍스트 SQL server에 대 한 함수를 제공 합니다.

대부분의 경우, 로드 하려는 패키지를 함께 사용할 때마다 **microsoftml**합니다.

## <a name="functions-by-category"></a>범주별으로 함수

이 섹션에서는 범주를 각각 사용 하는 방법의 아이디어를 제공 하 여 함수를 나열 합니다. 사용할 수도 있습니다는 [목차](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) 알파벳 순서로 함수를 찾으려고 합니다.

## <a name="1-training-functions"></a>1-교육 함수

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | 모델의 앙상블을 교육 합니다. |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | 임의 포리스트입니다. |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | 선형 모델입니다. 확률적 이중 좌표 경사를 사용 하 여 |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | 승격 된 트리입니다. |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | 로지스틱 회귀 분석입니다. |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | 신경망입니다. |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | 변칙 검색 합니다. |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2-변환 함수

### <a name="categorical-variable-handling"></a>범주 변수 처리

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | 범주로 텍스트 열을 변환합니다. |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | 해시 및 범주 텍스트 열을 변환 합니다. |

### <a name="schema-manipulation"></a>스키마 조작

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | 단일 벡터에 여러 열을 연결합니다. |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | 데이터 집합에서 열을 삭제합니다. |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | 데이터 집합의 열을 유지합니다. |


### <a name="variable-selection"></a>변수 선택

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |개수 기반 기능 선택 합니다. |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | 상호 정보를 기반으로 하는 기능 선택 합니다. |


### <a name="text-analytics"></a>텍스트 분석

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | 숫자 기능으로 텍스트 열을 변환합니다. |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | 감정 분석 합니다. |


### <a name="image-analytics"></a>이미지 분석 

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | 이미지를 로드합니다. |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | 이미지 크기를 조정 합니다. |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | 이미지에서 픽셀을 추출합니다. |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 이미지를 기능으로 변환합니다. |

### <a name="featurization-functions"></a>기능화 (featurization) 함수

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | 데이터 원본에 대 한 데이터 변환 |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3-점수 매기기 함수

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | Microsoft machine learning 모델을 사용 하 여 점수 |

## <a name="how-to-call-microsoftml"></a>Microsoftml를 호출 하는 방법

함수가 **microsoftml** 저장된 프로시저에서 캡슐화 하는 Python 코드에서 호출할 수 있습니다. 대부분의 개발자는 빌드할 **microsoftml** 솔루션을 로컬로 다음 배포 연습으로 저장된 프로시저에 완성 된 Python 코드를 마이그레이션합니다.

합니다 **microsoftml** 와 달리 하지만 기본적으로 Python이 설치에 대 한 패키지 **revoscalepy**, SQL Server와 함께 설치 된 Python 실행 파일을 사용 하 여 Python 세션을 시작할 때는 기본적으로 로드 되지 않습니다.

첫 번째 단계에서는 가져오기 합니다 **microsoftml** 패키지를 가져와 **revoscalepy** 원격 계산 컨텍스트 또는 관련 된 연결 또는 데이터 원본 개체를 사용 해야 하는 경우. 그런 다음 필요한 개별 함수를 참조 합니다.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>참조

+ [Python 자습서](../tutorials/sql-server-python-tutorials.md)
+ [자습서: T-sql로 Python 코드를 포함 합니다.](../tutorials/run-python-using-t-sql.md)
+ [Python 참조 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

