---
title: "SQL Server와 함께 MicrosoftML 패키지를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 1c377717-e281-431e-8171-3924dcce1cdd
caps.latest.revision: 132
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 38af2297d176205b06bd104228d44e50b4c94861
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="using-the-microsoftml-package-with-sql-server"></a>SQL Server MicrosoftML 패키지 사용

[ **MicrosoftML** ](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) Microsoft R Server 및 SQL Server 2017와 함께 제공 되는 패키지에 여러 기계 학습 알고리즘을 포함 합니다. 이러한 Api 응용 프로그램을 학습 하는 내부 컴퓨터에 대 한 Microsoft에서 개발 된 및 했을 구체화 고성능 빅 데이터를 지원 하기 위해 수 년에 걸쳐 멀티 코어 처리 및 빠른 데이터 스트리밍를 사용 하 여 합니다. MicrosoftML에는 텍스트 및 이미지 처리를 위한 다양 한 변환이 포함 됩니다.

SQL Server 2017 CTP 2.0에서 Python 언어에 대 한 지원이 추가 되었습니다. **microsoftml** r MicrosoftML 패키지에 동일한 함수를 포함 하는 Python에 대 한 패키지 

+ **R에 대 한 MicrosoftML**

    소개 및 패키지 참조: [MicrosoftML: 기계 학습 R 알고리즘](https://docs.microsoft.com/en-us/r-server/r-reference/microsoftml/microsoftml-package)

    대/소문자 구분 R 이므로 참조할 수 있는 이름을 올바르게 패키지를 로드할 때 있는지 확인 합니다.

+ **Python 용 microsoftml**

    소개 및 패키지 참조: [microsoftml (Python에 대 한 함수 라이브러리)](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)합니다. 

## <a name="whats-in-microsoftml"></a>MicrosoftML에 포함 된 내용

MicrosoftML 다양 한 기계 학습 알고리즘 및 성능을 위해 최적화 된 변형이 포함 되어 있습니다.

### <a name="machine-learning-algorithms"></a>기계 학습 알고리즘

-  선형 모델: `rxFastLinear` 선형 학습자 이진 분류 또는 회귀에 대 한 사용할 수 있는 추계 이중 좌표 경사에 기반 합니다. 이 모델은 L1 및 L2 정규화를 지원합니다.

- 의사 결정 트리 및 의사 결정 포리스트 모델: `rxFastTree` 은 승격 된 의사 결정 트리 알고리즘 FastRank Bing에서 사용 하기 위해 개발 된 원래 라고 합니다. 가장 빠르고 가장 인기 있는 학습자 중 하나입니다. 이진 분류 및 회귀를 지원합니다.

  `rxFastForest`로지스틱 회귀 모델은 임의 포리스트 방법에 따라. 이 모델은 RevoScaleR의 `rxLogit` 함수와 유사하지만 L1 및 L2 정규화를 지원합니다. 이진 분류 및 회귀를 지원합니다.

- 로지스틱 회귀: `rxLogisticRegression` 로지스틱 회귀 모델은 비슷합니다는 `rxLogit` L1 및 L2 정규화에 대 한 추가 지원으로, RevoScaleR 함수입니다. 이진 또는 다중 클래스 분류를 지원합니다.

- 신경망:는 `rxNeuralNet` 이진 분류, 다중 클래스 분류 및 회귀 신경망을 사용 하 여 함수를 지원 합니다. 사용자 지정 가능한 네트워크와 지원 convoluted 네트워크 GPU를 사용 하 여 GPU 가속을 사용 합니다.

- 이상 탐지 합니다.  `rxOneClassSvm` 함수 SVM 메서드를 기반으로 하지만 불균형된 데이터 집합에 있는 이진 분류에 대 한 최적화 됩니다.

### <a name="transformation-functions"></a>변환 함수

MicrosoftML 하는 데이터를 변환 하 고 기능을 추출 하는 데 유용한 다양 한 특수 함수를 포함 합니다.

- 텍스트 처리 기능에 포함 된 `featurizeText` 및 `getSentiment` 함수입니다. N 그램 계산을 사용 하는 언어를 검색 또는 텍스트 정규화를 수행할 수 있습니다. 또한 텍스트에서 해시 된 또는 개수 기반 기능 생성 또는 중지 단어 제거 등의 작업을 정리 하는 일반 텍스트를 수행할 수 있습니다.

- 기능 선택 및와 같은 변환 함수를 기능 `selectFeatures` 또는 `getSentiment`, 데이터를 분석 하 고 모델링에 대 한 가장 유용한 기능을 만듭니다.

- 와 같은 사용 하 여 범주 변수 작업 `categorical` 또는 `categoricalHash`, 범주 값 성능 향상을 위해 인덱싱된 배열로 변환입니다.

- 와 같은 이미지 처리 및 분석의 경우에 함수가 `extractPixels` 또는 `featurizeImage`let, 이미지를 더 빠르게 처리 및 이미지에 대 한 가장 정보를 가져옵니다.

자세한 내용은 [MicrosoftML 함수](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)를 참조하세요.

## <a name="how-to-use-microsoftml"></a>MicrosoftML를 사용 하는 방법

이 섹션에서는 찾아 R 및 Python 코드의 패키지를 로드 하는 방법을 설명 합니다.

+ R에 대 한 MicrosoftML 패키지는 Microsoft R server 9.1.0 및 SQL Server 2017에 기본적으로 설치 됩니다.

    사용 하 여 Microsoft R Server installer 설명 된 대로 여기는 인스턴스에 대 한 R 구성 요소를 업그레이드 하는 경우이 둘은 SQL Server 2016과 함께 사용할 수 또한: [바인딩을 사용 하 여 SQL Server의 인스턴스를 업그레이드 합니다.](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

+ **microsoftml** 패키지 Python는 SQL Server 2017 함께 기본적으로 설치 됩니다. 

   이 패키지를 사용 하려면 이상 Release Candidate 2로 업그레이드 하는 것이 좋습니다. 초기 버전 RC1와 함께 릴리스된 하지만 라이브러리에 상당한 수정 버전을 함수 이름에 대 한 변경을 포함 되었습니다. 

그러나 R와 Python에 대 한 패키지 되지 기본적으로 로드 됩니다. 따라서 해당 기능을 사용 하 여 코드의 일부로 패키지를 명시적으로 로드 해야 합니다.

### <a name="calling-microsoftml-functions-from-r-in-sql-server"></a>SQL Server의 R에서 MicrosoftML 함수 호출

R 코드에서 MicrosoftML 패키지를 로드 하 고 있는 다른 패키지와 같은 함수를 호출 합니다.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

**참고**

+ RevoScaleR 패키지에서 제공 하는 데이터 처리 파이프라인 MicrosoftML 패키지 완벽 하 게 통합 되어 있습니다. 따라서 컴퓨터 학습 확장을 사용할 수 있는 SQL Server의 인스턴스를 포함 하 여 모든 Windows 기반 계산 컨텍스트에서 MicrosoftML 패키지를 사용할 수 있습니다.

    그러나 MicrosoftML 계산 컨텍스트 RevoScaleR 및 원격을 사용 하려면 해당 함수에 대 한 참조가 필요 합니다.

### <a name="calling-microsoftml-functions-from-python-in-sql-server"></a>SQL Server에서 Python에서 microsoftml 함수 호출

함수를 호출 하 여 Python 코드의 패키지에서 가져올는 **microsoftml** 패키지 가져오기 및 **revoscalepy** 원격 계산 컨텍스트 또는 관련된 연결이 나 데이터 원본을 사용 하려는 경우 개체입니다. 그런 다음 필요한 개별 함수를 참조할 수 있습니다.

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**참고**

+ SQL Server 2017에 **microsoftml** Python35 호환 모듈입니다. 

+ 함수에 **microsoftml** 에서 지원 되는 계산 컨텍스트 및 데이터 소스와 통합 되어 **revoscalepy**합니다. 따라서 사용할 수 있습니다는 **microsoftml** Python 패키지를 만들고 모든 Windows 기반 계산 컨텍스트에서 컴퓨터 학습 확장에 있는 SQL Server의 인스턴스를 포함 하 여 모델에서 점수를 매깁니다. 사용할 수 있습니다.

    그러나 **microsoftml** Python에 대 한 참조를 필요한 **revoscalepy** 원격을 사용 하려면 해당 함수 계산 컨텍스트 및 합니다.

Revoscalepy에 대 한 자세한 내용은 다음을 참조 하세요.

+ [Revoscalepy 란](python/what-is-revoscalepy.md)

+ [revoscalepy 함수 라이브러리](https://docs.microsoft.com/en-us/r-server/python-reference/revoscalepy/revoscalepy-package) 
