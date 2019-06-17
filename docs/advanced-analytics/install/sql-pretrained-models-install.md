---
title: 미리 학습 된 기계 학습 모델-SQL Server Machine Learning 설치
description: SQL Server 2017 Machine Learning Services (R 또는 Python) 또는 SQL Server 2016 R Services에 감정 분석 및 이미지 기능화 (featurization)에 대 한 미리 학습 된 모델을 추가 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 002713c8c3eb92a33cbb1461eaacb8a0d63a5c3f
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140747"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>SQL Server에 대 한 모델을 학습 하는 미리 학습 된 기계를 설치 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 Powershell을 사용 하 여 무료 미리 학습 된 기계 학습에 대 한 모델을 추가 하는 방법에 설명 *감정 분석* 하 고 *이미지 기능화 (featurization)* SQL Server 인스턴스에 있는 R 또는 Python 통합 합니다. 미리 학습 된 모델은 Microsoft 및 사용 준비를 하 여 빌드됩니다. 설치 후 태스크로 인스턴스를 추가 합니다. 이러한 모델에 대 한 자세한 내용은 참조는 [리소스](#bkmk_resources) 이 문서의 섹션입니다.

설치 되 면 미리 학습된 된 모델 MicrosoftML (R) 및 microsoftml (Python) 라이브러리의 특정 함수는 구현 세부 사항으로 간주 됩니다. 처리할 수 있습니다 하 고 사용자 지정 코드에는 독립 된 리소스로 안 (이며) 보기, 사용자 지정 또는 모델을 재 학습 또는 다른 함수 쌍을 이룹니다. 

미리 학습 된 모델을 사용 하려면 다음 표에 나열 된 함수를 호출 합니다.

| R 함수 (MicrosoftML) | Python 함수 (microsoftml) | 사용법 |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | 텍스트 입력에 대해 양수 음수가 감정 점수를 생성합니다. |
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 이미지 파일 입력에서 텍스트 정보를 추출합니다. |

## <a name="prerequisites"></a>사전 요구 사항

기계 학습 알고리즘입니다. 계산이있지 않습니다. 16GB RAM의 모든 샘플 데이터를 사용 하 여 자습서 연습 완료 등 낮음-보통 워크 로드에 대 한 사용 하는 것이 좋습니다.

미리 학습 된 모델에 추가할 컴퓨터와 SQL Server에 대 한 관리자 권한이 있어야 합니다.

외부 스크립트를 사용 하도록 설정 하 고 SQL Server 실행 패드 서비스가 실행 되어야 합니다. 설치 지침을 활성화 하 고 이러한 기능을 확인 하는 단계를 제공 합니다. 

[MicrosoftML R 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 나 [microsoftml Python 패키지](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 미리 학습된 된 모델을 포함 합니다.

+ [SQL Server 2017 Machine Learning Services](sql-machine-learning-services-windows-install.md) 사용자의 추가 작업이 없으므로 사용 하 여이 필수 조건을 충족 하므로 두 언어 버전의 machine learning 라이브러리를 포함 합니다. 라이브러리가 있는 이기 때문에 이러한 라이브러리에 미리 학습된 된 모델을 추가 하려면이 문서에 설명 된 PowerShell 스크립트를 사용할 수 있습니다.

+ [SQL Server 2016 R Services](sql-r-services-windows-install.md)에 R 전용 이며, 포함 되지 않습니다 [MicrosoftML 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 기본적입니다. MicrosoftML를 추가 하려면 수행 해야 합니다는 [구성 요소 업그레이드](../install/upgrade-r-and-python.md)합니다. 구성 요소 업그레이드의 장점 중 하나는 추가할 수 있는 동시에 미리 학습 된 모델에 불필요 한 PowerShell 스크립트를 실행할 수 있습니다. 그러나 이미 업그레이드 하지만 경우 처음에는 미리 학습된 된 모델을 추가 하는 누락 된이 문서에 설명 된 대로 PowerShell 스크립트를 실행할 수 있습니다. 두 버전의 SQL Server에서 작동합니다. 를 수행 하기 전에 MicrosoftML 라이브러리 C:\Program Files\Microsoft SQL Server\MSSQL13에 존재 하는지 확인 합니다. MSSQLSERVER\R_SERVICES\library 합니다.


<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>미리 학습 된 모델의 설치 여부를 확인 합니다.

R 및 Python 모델에 대 한 설치 경로 다음과 같습니다.

+ R:에 대 한 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ Python: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

모델 파일 이름 아래에 나열 됩니다.

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.model
+ ResNet\_101\_Updated.model
+ ResNet\_18\_Updated.model
+ ResNet\_50\_Updated.model

모델은 이미 설치 된 경우는 [유효성 검사 단계](#verify) 사용할 수 있는지 확인 합니다.

## <a name="download-the-installation-script"></a>설치 스크립트를 다운로드 합니다.

클릭 [ https://aka.ms/mlm4sql ](https://aka.ms/mlm4sql) 파일을 다운로드 하려면 **설치 MLModels.ps1**합니다.

## <a name="execute-with-elevated-privileges"></a>상승 된 권한으로 실행

1. PowerShell을 시작 합니다. 작업 표시줄에서 PowerShell 프로그램 아이콘을 마우스 오른쪽 단추로 클릭 하 고 선택 **관리자 권한으로 실행**합니다.
2. 설치 스크립트 파일에 정규화 된 경로 입력 하 고 인스턴스 이름을 포함 합니다. Downloads 폴더 및 기본 인스턴스를 사용 한다고 가정 합니다 명령을 다음과 같이 표시 될 수 있습니다.

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**출력**

인터넷에 연결 된 SQL Server 2017의 Machine Learning 기본 인스턴스에 R 및 Python을 사용 하 여 다음과 비슷한 메시지가 표시 됩니다.

   ```powershell
   MSSQL14.MSSQLSERVER
        Verifying R models [9.2.0.24]
        Downloading R models [C:\Users\<user-name>\AppData\Local\Temp]
        Installing R models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\]
        Verifying Python models [9.2.0.24]
        Installing Python models [C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\]
   PS C:\WINDOWS\system32>
   ```

<a name="verify"> </a>

## <a name="verify-installation"></a>설치 확인

먼저 새 파일을 확인 합니다 [mxlibs 폴더](#file-location)합니다. 데모 코드 모델이 설치 되어 작동을 확인 하려면 다음을 실행 합니다. 

### <a name="r-verification-steps"></a>R 확인 단계

1. Start **RGUI.EXE** at C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64.

2. 명령 프롬프트에서 다음 R 스크립트에 붙여 넣습니다.

    ```R
    # Create the data
    CustomerReviews <- data.frame(Review = c(
    "I really did not like the taste of it",
    "It was surprisingly quite good!",
    "I will never ever ever go to that place again!!"),
    stringsAsFactors = FALSE)

    # Get the sentiment scores
    sentimentScores <- rxFeaturize(data = CustomerReviews, 
                                    mlTransforms = getSentiment(vars = list(SentimentScore = "Review")))

    # Let's translate the score to something more meaningful
    sentimentScores$PredictedRating <- ifelse(sentimentScores$SentimentScore > 0.6, 
                                            "AWESOMENESS", "BLAH")

    # Let's look at the results
    sentimentScores
    ```

3. Enter 키를 눌러 감정 점수를 볼 수 있습니다. 출력은 다음과 같이 됩니다.

    ```R
    > sentimentScores
                                            Review SentimentScore
    1           I really did not like the taste of it      0.4617899
    2                 It was surprisingly quite good!      0.9601924
    3 I will never ever ever go to that place again!!      0.3103435
    PredictedRating
    1            BLAH
    2     AWESOMENESS
    3            BLAH
    ```

### <a name="python-verification-steps"></a>Python 확인 단계

1. 시작 **Python.exe** C:\Program Files\Microsoft SQL Server\MSSQL14에서. MSSQLSERVER\PYTHON_SERVICES 합니다.

2. 명령 프롬프트에서 다음 Python 스크립트에 붙여 넣습니다.

    ```python
    import numpy
    import pandas
    from microsoftml import rx_logistic_regression, rx_featurize, rx_predict, get_sentiment

    # Create the data
    customer_reviews = pandas.DataFrame(data=dict(review=[
                "I really did not like the taste of it",
                "It was surprisingly quite good!",
                "I will never ever ever go to that place again!!"]))
                
    # Get the sentiment scores
    sentiment_scores = rx_featurize(
        data=customer_reviews,
        ml_transforms=[get_sentiment(cols=dict(scores="review"))])
        
    # Let's translate the score to something more meaningful
    sentiment_scores["eval"] = sentiment_scores.scores.apply(
                lambda score: "AWESOMENESS" if score > 0.6 else "BLAH")
    print(sentiment_scores)
    ```

3. Enter 키를 눌러 점수를 인쇄 합니다. 출력은 다음과 같이 됩니다.

    ```python
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> 데모 스크립트 실패 하는 경우 먼저 파일 위치를 확인 합니다. SQL Server의 여러 인스턴스가 포함 된 시스템에서 실행 되는 인스턴스 또는-side-by-side 독립 실행형 버전을 사용 하 여, 있기 잘못가 환경의 읽 및 잘못 된 위치에 파일을 배치 하기 위한 설치 스크립트가 있습니다. 일반적으로 올바른 mxlib 폴더로 파일을 수동으로 복사 문제를 해결 합니다.

## <a name="examples-using-pre-trained-models"></a>미리 학습 된 모델을 사용 하는 예제

다음 링크를 미리 학습 된 모델을 호출 하는 예제 코드를 포함 합니다.

+ [코드 샘플: 텍스트 Featurizer를 사용 하 여 감정 분석](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>연구 및 리소스

현재 사용할 수 있는 모델은 감정 분석 및 이미지 분류에 대 한 심층 신경망 (DNN) 모델. Microsoft의를 사용 하 여 모든 미리 학습 된 모델이 학습 되었습니다 [계산 Network Toolkit](https://cntk.ai/Features/Index.html), 또는 **CNTK**합니다.

각 네트워크의 구성 된 다음 참조 구현을 기반으로 합니다.

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

이러한 심층 학습 모델 및 그 구현 방법에 사용 되는 알고리즘에 대 한 자세한 내용은 및 CNTK를 사용 하 여 학습, 이러한 문서를 참조 하세요.

+ [Microsoft 연구원 들은 알고리즘 마일스 톤을 ImageNet 챌린지를 설정합니다.](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft Computational Network Toolkit는 가장 효율적인 분산된 심층 학습 계산 성능을 제공합니다](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>참고자료

+ [SQL Server 2016 R Services](sql-r-services-windows-install.md)
+ [SQL Server 2017 Machine Learning Services](sql-machine-learning-services-windows-install.md)
+ [SQL Server 인스턴스에 R 및 Python 구성 요소를 업그레이드 합니다.](../install/upgrade-r-and-python.md)
+ [R에 대 한 MicrosoftML 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [Python 용 microsoftml 패키지](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
