---
title: SQL Server에서 MicrosoftML 패키지 사용 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 51ffa33bef7ab880704c9c1391a69feb3e194202
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984565"
---
# <a name="using-the-microsoftml-package-with-sql-server"></a>SQL Server에서 MicrosoftML 패키지 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

합니다 [ **MicrosoftML** ](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) Microsoft R Server 및 SQL Server 2017을 사용 하 여 제공 되는 패키지에 여러 기계 학습 알고리즘을 포함 합니다. 이러한 Api는 내부 기계 학습 응용 프로그램, Microsoft에서 개발한 및 된 구체화 된 고성능 빅 데이터에서 수 년에 걸쳐 멀티 코어 처리 및 빠른 데이터 스트리밍을 사용 하 여 합니다. MicrosoftML에 텍스트 및 이미지 처리를 위한 다양 한 변환도 포함 됩니다.

SQL Server 2017 CTP 2.0에서 Python 언어에 대 한 지원이 추가 되었습니다. 합니다 **microsoftml** r에서 MicrosoftML 패키지에서 해당 함수를 포함 하는 Python에 대 한 패키지 

+ **R에 대 한 MicrosoftML**

    소개 및 패키지 참조: [MicrosoftML: machine learning R 알고리즘](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)

    R은 대/소문자 구분, 때문에 참조 이름을 올바르게 패키지를 로드할 때 있는지 확인 합니다.

+ **Python 용 microsoftml**

    소개 및 패키지 참조: [microsoftml (Python에 대 한 함수 라이브러리)](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)합니다. 

## <a name="whats-in-microsoftml"></a>MicrosoftML의 새로운 기능

MicrosoftML 다양 한 기계 학습 알고리즘 및 성능을 위해 최적화 된 변환을 포함 합니다.

### <a name="machine-learning-algorithms"></a>기계 학습 알고리즘

-  선형 모델: `rxFastLinear` 는 선형 학습자에 이진 분류 또는 회귀에 사용할 수 있는 확률적 이중 좌표 경사를 기반 합니다. 이 모델은 L1 및 L2 정규화를 지원합니다.

- 의사 결정 트리 및 의사 결정 포리스트 모델: `rxFastTree` 은 원래 Bing에서 사용 하기 위해 개발 된 FastRank로 알려진 향상 된 의사 결정 트리 알고리즘입니다. 가장 빠르고 가장 인기 있는 학습자 중 하나입니다. 이진 분류 및 회귀를 지원합니다.

  `rxFastForest` 로지스틱 회귀 모델을 기반으로 임의 포리스트 방법을 합니다. 이 모델은 RevoScaleR의 `rxLogit` 함수와 유사하지만 L1 및 L2 정규화를 지원합니다. 이진 분류 및 회귀를 지원합니다.

- 로지스틱 회귀: `rxLogisticRegression` 비슷합니다 로지스틱 회귀 모델을 `rxLogit` L1 및 L2 정규화에 대 한 추가 지원으로에서 RevoScaleR 함수입니다. 이진 또는 다중 클래스 분류를 지원합니다.

- 신경망:는 `rxNeuralNet` 이진 분류, 다중 클래스 분류 및 회귀 신경망을 사용 하 여 함수를 지원 합니다. 단일 GPU를 사용 하 여 GPU 가속을 사용 하 여 복잡 한 네트워크를 사용자 지정 가능한 및 지원 합니다.

- 변칙 검색 합니다.  `rxOneClassSvm` 함수 SVM 방법을 기반으로 하지만 불균형된 데이터 집합에서 이진 분류 용으로 최적화 됩니다.

### <a name="transformation-functions"></a>변환 함수

MicrosoftML은 데이터 변환 및 기능 추출에 유용한 다양 한 특수 함수를 포함 합니다.

- 텍스트 처리 기능을 포함 합니다 `featurizeText` 및 `getSentiment` 함수입니다. N-gram을 계산 하를 사용 하는 언어를 검색 하거나 텍스트 정규화를 수행할 수 있습니다. 또한 텍스트에서 해시 또는 개수 기반 기능 생성 또는 중지 단어 제거 등의 작업을 정리 하는 일반 텍스트를 수행할 수 있습니다.

- 기능 선택 및 변환 함수를 같은 기능 `selectFeatures` 또는 `getSentiment`, 데이터 분석 및 모델링에 대 한 가장 유용한 기능을 만듭니다.

- 와 같은 사용 하 여 범주 변수를 사용 하 여 작동 `categorical` 또는 `categoricalHash`, 성능 향상을 위해 인덱싱된 배열로 범주 값을 변환 하는 합니다.

- 와 같은 이미지 처리 및 분석, 관련 함수 `extractPixels` 또는 `featurizeImage`, 이미지에 대 한 가장 정보를 가져올 하 고 이미지를 더 빠르게 처리 합니다.

자세한 내용은 [MicrosoftML 함수](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)를 참조하세요.

## <a name="how-to-use-microsoftml"></a>MicrosoftML를 사용 하는 방법

이 섹션에 찾고 R 및 Python 코드에서 패키지를 로드 하는 방법을 설명 합니다.

+ R에 대 한 MicrosoftML 패키지는 SQL Server 2017 및 Microsoft R server 9.1.0 기본적으로 설치 됩니다.

    Microsoft R Server 설치 관리자를 설명 된 대로 여기 사용 하는 인스턴스에 대 한 R 구성 요소를 업그레이드 하는 경우 SQL Server 2016을 사용 하 여 사용할 수도 수: [바인딩을 사용 하 여 SQL Server 인스턴스 업그레이드](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

+ 합니다 **microsoftml** Python이 기본적으로 SQL Server 2017 설치에 대 한 패키지 

   이 패키지를 사용 하려면 릴리스 후보 2 이상 업그레이드 하는 것이 좋습니다. RC1을 사용 하 여 초기 버전 릴리스된 하지만 라이브러리에 함수 이름 변경을 비롯 한 많은 수정 되었습니다. 

그러나 R 및 Python 모두에 대 한 패키지 로드 되지 않는 기본; 따라서 해당 함수를 사용 하 여 코드의 일부로 패키지를 명시적으로 로드 해야 합니다.

### <a name="calling-microsoftml-functions-from-r-in-sql-server"></a>SQL Server에서 R에서 MicrosoftML 함수 호출

R 코드에서 MicrosoftML 패키지를 로드 하 고 다른 패키지와 같은 해당 함수를 호출 합니다.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

**참고**

+ MicrosoftML 패키지는 RevoScaleR 패키지에서 제공 하는 데이터 처리 파이프라인과 완전히 통합 됩니다. 따라서 MicrosoftML 패키지 사용 하도록 설정 하는 기계 학습 확장 되어 있는 SQL Server의 인스턴스를 포함 하 여 모든 Windows 기반 계산 컨텍스트에서 사용할 수 있습니다.

    그러나 MicrosoftML 계산 컨텍스트를 RevoScaleR 및 원격을 사용 하려면 해당 함수에 대 한 참조가 필요 합니다.

### <a name="calling-microsoftml-functions-from-python-in-sql-server"></a>SQL Server의 Python에서 microsoftml 함수 호출

가져올 패키지를 Python 코드에서 함수를 호출 하는 **microsoftml** 패키지를 가져와 **revoscalepy** 원격 계산 컨텍스트 또는 관련 된 연결 또는 데이터 원본을 사용 하는 경우 개체입니다. 그런 다음 필요한 개별 함수를 참조 합니다.

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**참고**

+ SQL Server 2017에서 **microsoftml** Python35-호환 되는 모듈입니다. 

+ 함수가 **microsoftml** 에서 지원 되는 계산 컨텍스트 및 데이터 소스와 통합 되어 **revoscalepy**합니다. 따라서 사용할 수 있습니다 합니다 **microsoftml** Python 패키지를 만들고 기계 학습 확장 되어 있는 SQL Server의 인스턴스를 포함 하 여 모든 Windows 기반 계산 컨텍스트에서 모델에서 점수 매기기입니다. 사용할 수 있습니다.

    그러나 **microsoftml** Python에 대 한 참조가 필요 **revoscalepy** 원격을 사용 하려면 해당 함수 계산 컨텍스트 및 합니다.

Revoscalepy에 대 한 자세한 내용은 다음을 참조 하세요.

+ [Revoscalepy 란](python/what-is-revoscalepy.md)

+ [revoscalepy 함수 라이브러리](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
