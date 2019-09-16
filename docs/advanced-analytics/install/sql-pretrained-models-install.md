---
title: 미리 학습 된 기계 학습 모델 설치
description: 감정 분석 및 이미지 기능화에 대해 미리 학습 된 모델을 SQL Server Machine Learning Services (R 또는 Python) 또는 SQL Server R Services에 추가 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 87f75b8ef8f9f151eb548787da4c9791eb1437b9
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715165"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>SQL Server에 미리 학습 된 기계 학습 모델 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 Powershell을 사용 하 여 *감정 분석* 및 *이미지 기능화* 을 위한 무료 미리 학습 된 기계 학습 모델을 R 또는 Python 통합이 있는 SQL Server 인스턴스에 추가 하는 방법을 설명 합니다. 미리 학습 된 모델은 설치 후 작업으로 인스턴스에 추가 되 고 Microsoft에서 바로 사용할 수 있습니다. 이러한 모델에 대 한 자세한 내용은이 문서의 [리소스](#bkmk_resources) 섹션을 참조 하세요.

일단 설치 되 면 미리 학습 된 모델은 MicrosoftML (R) 및 MicrosoftML (Python) 라이브러리의 특정 기능에 대 한 구현 세부 정보로 간주 됩니다. 모델을 보거나, 사용자 지정 하거나, 다시 학습, 사용자 지정 코드 또는 쌍을 이루는 다른 함수에서 독립적인 리소스로 취급할 수 없습니다. 

사전 학습 된 모델을 사용 하려면 다음 표에 나열 된 함수를 호출 합니다.

| R 함수 (MicrosoftML) | Python 함수 (microsoftml) | 사용 |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | 텍스트 입력에 대해 긍정 네거티브 감정 점수를 생성 합니다. |
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 이미지 파일 입력에서 텍스트 정보를 추출 합니다. |

## <a name="prerequisites"></a>사전 요구 사항

기계 학습 알고리즘은 계산 집약적입니다. 모든 샘플 데이터를 사용 하는 자습서 연습을 완료 하는 것을 포함 하 여 낮은 규모의 워크 로드에 16gb RAM을 권장 합니다.

미리 학습 된 모델을 추가 하려면 컴퓨터에 대 한 관리자 권한이 있어야 하 고 SQL Server 합니다.

외부 스크립트를 사용 하도록 설정 하 고 SQL Server 실행 패드 서비스가 실행 되 고 있어야 합니다. 설치 지침은 이러한 기능을 사용 하도록 설정 하 고 확인 하는 단계를 제공 합니다. 

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[MicrosoftML R 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 또는 [MicrosoftML Python 패키지](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 는 미리 학습 된 모델을 포함 합니다.

[SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md) 에는 Machine Learning 라이브러리의 언어 버전이 모두 포함 되어 있으므로이 필수 구성 요소는 추가 작업 없이 충족 됩니다. 라이브러리가 존재 하므로이 문서에 설명 된 PowerShell 스크립트를 사용 하 여 미리 학습 된 모델을 이러한 라이브러리에 추가할 수 있습니다.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[MicrosoftML R 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 는 미리 학습 된 모델을 포함 합니다.

R 전용 [SQL Server R Services](sql-r-services-windows-install.md)은 기본적으로 [MicrosoftML 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 를 포함 하지 않습니다. MicrosoftML를 추가 하려면 [구성 요소 업그레이드](../install/upgrade-r-and-python.md)를 수행 해야 합니다. 구성 요소 업그레이드의 이점 중 하나는 미리 학습 된 모델을 동시에 추가 하 여 PowerShell 스크립트를 불필요 하 게 실행 하는 것입니다. 그러나 이미 업그레이드 했지만 처음으로 미리 학습 된 모델을 추가 하지 못한 경우이 문서에 설명 된 대로 PowerShell 스크립트를 실행할 수 있습니다. SQL Server의 두 버전 모두에 대해 작동 합니다. 이렇게 하려면 먼저 MicrosoftML 라이브러리가 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`있는지 확인 합니다.
::: moniker-end

<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>미리 학습 된 모델 설치 여부 확인

R 및 Python 모델의 설치 경로는 다음과 같습니다.

+ R의 경우:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ Python의 경우:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

모델 파일 이름은 다음과 같습니다.

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.model
+ ResNet\_101\_Updated.model
+ ResNet\_18\_Updated.model
+ ResNet\_50\_Updated.model

모델이 이미 설치 되어 있는 경우 [유효성 검사 단계로](#verify) 이동 하 여 가용성을 확인 합니다.

## <a name="download-the-installation-script"></a>설치 스크립트 다운로드

Install-MLModels [https://aka.ms/mlm4sql](https://aka.ms/mlm4sql) 파일을 다운로드 하려면클릭 합니다.

## <a name="execute-with-elevated-privileges"></a>상승 된 권한으로 실행

1. PowerShell을 시작 합니다. 작업 표시줄에서 PowerShell 프로그램 아이콘을 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행**을 선택 합니다.
2. 설치 스크립트 파일의 정규화 된 경로를 입력 하 고 인스턴스 이름을 포함 합니다. 다운로드 폴더와 기본 인스턴스를 가정 하면 명령은 다음과 같이 표시 될 수 있습니다.

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**출력**

R 및 Python을 사용 하 여 인터넷에 연결 된 SQL Server Machine Learning Services 기본 인스턴스에서 다음과 비슷한 메시지가 표시 됩니다.

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

먼저 [mxlibs 폴더](#file-location)에서 새 파일을 확인 합니다. 다음으로 데모 코드를 실행 하 여 모델이 설치 되 고 작동 하는지 확인 합니다. 

### <a name="r-verification-steps"></a>R 확인 단계

1. **Rgui를 시작 합니다.** C:\Program FILES\MICROSOFT SQL Server\MSSQL14.의 EXE MSSQLSERVER\R_SERVICES\bin\x64.

2. 명령 프롬프트에서 다음 R 스크립트를 붙여 넣습니다.

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

3. Enter 키를 눌러 감정 점수를 확인 합니다. 출력은 다음과 같아야 합니다.

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

1. C:\Program Files\Microsoft SQL Server\MSSQL14.에서 **Python을** 시작 합니다. MSSQLSERVER\PYTHON_SERVICES.

2. 다음 Python 스크립트를 명령 프롬프트에 붙여 넣습니다.

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

3. Enter 키를 눌러 점수를 인쇄 합니다. 출력은 다음과 같아야 합니다.

    ```python
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> 데모 스크립트가 실패할 경우 먼저 파일 위치를 확인 합니다. SQL Server 인스턴스를 여러 개 포함 하거나 독립 실행형 버전과 함께 실행 되는 인스턴스의 경우에는 설치 스크립트에서 환경을 잘못 읽을 수 있으며 파일을 잘못 된 위치에 저장할 수 있습니다. 일반적으로 파일을 올바른 mxlib 폴더에 수동으로 복사 하면 문제가 해결 됩니다.

## <a name="examples-using-pre-trained-models"></a>미리 학습 된 모델을 사용 하는 예제

다음 링크에는 미리 학습 된 모델을 호출 하는 예제 코드가 포함 되어 있습니다.

+ [코드 샘플: 텍스트 Featurizer를 사용 하 여 감정 분석](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>연구 및 리소스

현재 사용할 수 있는 모델은 감정 분석 및 이미지 분류를 위한 심층 신경망 (DNN) 모델입니다. 미리 학습 된 모든 모델은 Microsoft의 [계산 네트워크 도구 키트](https://cntk.ai/Features/Index.html)또는 **CNTK**를 사용 하 여 학습 되었습니다.

각 네트워크의 구성은 다음 참조 구현을 기반으로 합니다.

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

이러한 심층 학습 모델에 사용 되는 알고리즘과 CNTK를 사용 하 여 구현 및 학습 되는 방법에 대 한 자세한 내용은 다음 문서를 참조 하세요.

+ [Microsoft 연구원의 알고리즘이 ImageNet 챌린지 마일스 톤을 설정 합니다.](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [Microsoft 컴퓨팅 네트워크 도구 키트는 가장 효율적인 분산 심층 학습 계산 성능을 제공 합니다.](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>참조

+ [SQL Server 컴퓨터 학습 서비스](sql-machine-learning-services-windows-install.md)
+ [SQL Server 인스턴스에서 R 및 Python 구성 요소 업그레이드](../install/upgrade-r-and-python.md)
+ [R에 대 한 MicrosoftML 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [Python 용 microsoftml 패키지](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
