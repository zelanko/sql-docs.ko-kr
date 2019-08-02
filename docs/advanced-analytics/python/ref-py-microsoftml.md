---
title: microsoftml Python 패키지
description: SQL Server machine learning 워크 로드와 관련 하 여 Python 용 Microsoft machine learning 알고리즘 및 모델을 소개 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c7e7a25749484ff0db4d133f10862438ae5f8ea1
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715146"
---
# <a name="microsoftml-python-module-in-sql-server"></a>microsoftml (SQL Server)의 Python 모듈
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**microsoftml** 은 고성능 기계 학습 알고리즘을 제공 하는 Microsoft의 Python35 호환 모듈입니다. 여기에는 학습 및 변환, 점수 매기기, 텍스트 및 이미지 분석, 기존 데이터에서 값을 파생 하기 위한 기능 추출을 위한 함수가 포함 됩니다.

기계 학습 Api는 내부 기계 학습 응용 프로그램을 위해 Microsoft에서 개발 했으며 다중 코어 처리 및 빠른 데이터 스트리밍을 사용 하 여 빅 데이터에 대 한 고성능을 지원 하기 위해 몇 년 동안 구체화 되었습니다. 이 패키지는 유사한 함수를 포함 하는 R 버전 [MicrosoftML](../r/ref-r-microsoftml.md)와 동일한 Python으로 시작 되었습니다. 

## <a name="full-reference-documentation"></a>전체 참조 설명서

**Microsoftml** 라이브러리는 여러 Microsoft 제품에 배포 되지만, SQL Server 또는 다른 제품에 라이브러리를 가져올 때 사용 됩니다. 함수는 동일 하기 때문에 [개별 microsoftml 함수에 대 한 설명서](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 는 Microsoft Machine Learning Server에 대 한 [Python 참조](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) 아래의 한 위치에만 게시 됩니다. 제품별 동작이 있는 경우 함수 도움말 페이지에 차이점이 표시 됩니다.

## <a name="versions-and-platforms"></a>버전 및 플랫폼

**Microsoftml** 모듈은 Python 3.5을 기반으로 하며 다음 Microsoft 제품 또는 다운로드 중 하나를 설치한 경우에만 사용할 수 있습니다.

+ [SQL Server 컴퓨터 학습 서비스](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 이상](https://docs.microsoft.com/machine-learning-server/)
+ [데이터 과학 클라이언트용 Python 클라이언트 라이브러리](setup-python-client-tools-sql.md)

> [!NOTE]
> 전체 제품 릴리스 버전은 SQL Server 2017부터 Windows 전용입니다. **Microsoftml** 에 대 한 Linux 지원은 [SQL Server 2019 미리 보기](../../linux/sql-server-linux-setup-machine-learning.md)의 새로운 기능입니다.

## <a name="package-dependencies"></a>패키지 종속성

**Microsoftml** 의 알고리즘은 다음에 대 한 [revoscalepy](ref-py-revoscalepy.md) 에 종속 됩니다.

+ 데이터 원본 개체입니다. **Microsoftml** 함수에서 사용 되는 데이터는 **revoscalepy** 함수를 사용 하 여 생성 됩니다.
+ 원격 컴퓨팅 (원격 SQL Server 인스턴스로 함수 실행 이동) **Revoscalepy** 라이브러리는 SQL server에 대 한 원격 계산 컨텍스트를 만들고 활성화 하는 함수를 제공 합니다.

대부분의 경우 **microsoftml**를 사용할 때마다 패키지를 함께 로드 합니다.

## <a name="functions-by-category"></a>범주별 함수

이 섹션에서는 각 함수를 사용 하는 방법에 대 한 아이디어를 제공 하기 위해 범주별로 함수를 나열 합니다. [목차](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) 를 사용 하 여 알파벳 순서로 함수를 찾을 수도 있습니다.

## <a name="1-training-functions"></a>1-학습 함수

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | 앙상블 모델을 학습 합니다. |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | 임의 포리스트. |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | 선형 모델. 추계 이중 좌표 어센더를 사용 합니다. |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | 승격 된 트리. |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | 로지스틱 회귀 |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | 신경망. |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | 변칙 검색. |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2-변환 함수

### <a name="categorical-variable-handling"></a>범주 변수 처리

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | 텍스트 열을 범주로 변환 합니다. |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | 텍스트 열을 해시 하 고 범주로 변환 합니다. |

### <a name="schema-manipulation"></a>스키마 조작

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | 여러 열을 단일 벡터로 연결 합니다. |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | 데이터 집합에서 열을 삭제 합니다. |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | 데이터 집합의 열을 유지 합니다. |


### <a name="variable-selection"></a>변수 선택

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |개수에 따라 기능을 선택 합니다. |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | 상호 정보에 따라 기능을 선택 합니다. |


### <a name="text-analytics"></a>텍스트 분석

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | 텍스트 열을 숫자 기능으로 변환 합니다. |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | 감정 분석 |


### <a name="image-analytics"></a>이미지 분석 

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | 이미지를 로드 합니다. |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | 이미지 크기를 조정 합니다. |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | 이미지에서 픽셀을 추출 합니다. |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 이미지를 기능으로 변환 합니다. |

### <a name="featurization-functions"></a>기능화 함수

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | 데이터 원본에 대 한 데이터 변환 |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3-점수 매기기 함수

| 함수 | 설명 |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | Microsoft machine learning 모델을 사용 하는 점수 |

## <a name="how-to-call-microsoftml"></a>Microsoftml를 호출 하는 방법

**Microsoftml** 의 함수는 저장 프로시저에 캡슐화 된 Python 코드에서 호출할 수 있습니다. 대부분의 개발자는 **microsoftml** 솔루션을 로컬로 빌드한 다음 배포 연습으로 완성 된 Python 코드를 저장 프로시저로 마이그레이션합니다.

Python 용 **microsoftml** 패키지는 기본적으로 설치 되지만 **revoscalepy**와는 달리, SQL Server와 함께 설치 된 python 실행 파일을 사용 하 여 python 세션을 시작할 때 기본적으로 로드 되지 않습니다.

첫 번째 단계로, **microsoftml** 패키지를 가져오고, 원격 계산 컨텍스트 또는 관련 된 연결 또는 데이터 원본 개체를 사용 해야 하는 경우 **revoscalepy** 를 가져옵니다. 그런 다음 필요한 개별 함수를 참조 합니다.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>참조

+ [Python 자습서](../tutorials/sql-server-python-tutorials.md)
+ [자습서: T-sql에 Python 코드 포함](../tutorials/run-python-using-t-sql.md)
+ [Python 참조 (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

