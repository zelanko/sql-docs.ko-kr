---
title: 미리 학습된 모델 설치
description: 감정 분석 및 이미지 기능화용으로 미리 학습된 모델을 SQL Server Machine Learning Services(R 또는 Python) 또는 SQL Server R Services에 추가합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/30/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 86aad616cc8c9fc54adc2fffd14bfc663acf3887
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179729"
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>SQL Server에 미리 학습된 기계 학습 모델 설치
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이 문서에서는 Powershell을 사용하여 *감정 분석* 및 *이미지 기능화*용으로 미리 학습된 무료 기계 학습 모델을 R 또는 Python이 통합된 SQL Server 인스턴스에 추가하는 방법을 설명합니다. 미리 학습된 모델은 Microsoft에서 빌드하고 사용 가능한 상태가 되며 설치 후 작업으로 인스턴스에 추가됩니다. 이러한 모델에 대한 자세한 내용은 이 문서의 [리소스](#bkmk_resources) 섹션을 참조하세요.

미리 학습된 모델은 설치 후 MicrosoftML(R) 및 microsoftml(Python) 라이브러리의 특정 기능을 지원하는 구현 세부 정보로 간주됩니다. 모델을 보거나, 사용자 지정하거나, 다시 학습시켜서는 안 되고(그럴 수도 없고) 사용자 지정 코드의 독립적인 리소스로 취급하거나 다른 함수를 페어링할 수도 없습니다. 

미리 학습된 모델을 사용하려면 다음 표에 나열된 함수를 호출합니다.

| R 함수(MicrosoftML) | Python 함수(microsoftml) | 사용 |
|--------------------------|-------------------------------|-------|
| [getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | [get_sentiment](https://docs.microsoft.com//machine-learning-server/python-reference/microsoftml/get-sentiment) | 텍스트 입력에 대한 긍정-부정 감정 점수를 생성합니다. |
| [featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | [featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | 이미지 파일 입력에서 텍스트 정보를 추출합니다. |

## <a name="prerequisites"></a>사전 요구 사항

기계 학습 알고리즘은 컴퓨팅 집약적입니다. 모든 샘플 데이터를 사용하는 자습서 연습 완료를 포함한 중소 규모의 워크로드에 16GB RAM을 권장합니다.

미리 학습된 모델을 추가하려면 컴퓨터 및 SQL Server에 대한 관리자 권한이 있어야 합니다.

외부 스크립트가 사용하도록 설정되어 있고 SQL Server LaunchPad 서비스가 실행되고 있어야 합니다. 설치 지침은 이러한 기능을 사용하도록 설정하고 확인하는 단계를 제공합니다. 

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
[MicrosoftML R 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 또는 [microsoftml Python](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 패키지에는 미리 학습된 모델이 들어 있습니다.

[SQL Server](sql-machine-learning-services-windows-install.md) Machine Learning Services에는 기계 학습 라이브러리의 언어 버전이 모두 포함되어 있으므로 이 사전 요구 사항은 사용자의 추가 작업 없이도 충족됩니다. 라이브러리가 제공되므로 이 문서에 설명된 PowerShell 스크립트를 사용하여 미리 학습된 모델을 이러한 라이브러리에 추가할 수 있습니다.
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[MicrosoftML R 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)에는 미리 학습된 모델이 들어 있습니다.

R 전용 [SQL Server R Services](sql-r-services-windows-install.md)에는 기본적으로 [MicrosoftML 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)가 포함되지 않습니다. MicrosoftML을 추가하려면 [구성 요소 업그레이드](../install/upgrade-r-and-python.md)를 수행해야 합니다. 구성 요소 업그레이드의 이점 중 하나는 PowerShell 스크립트를 실행할 필요 없이 미리 학습 된 모델을 동시에 추가할 수 있다는 것입니다. 그러나 이미 업그레이드했지만 처음에 미리 학습된 모델을 추가하지 못한 경우 이 문서에 설명된 대로 PowerShell 스크립트를 실행할 수 있습니다. 이 방법은 SQL Server의 두 버전 모두에서 작동합니다. 이 작업을 수행하기 전에 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`에 MicrosoftML 라이브러리가 있는지 확인합니다.
::: moniker-end

<a name="file-location"></a>

## <a name="check-whether-pre-trained-models-are-installed"></a>미리 학습된 모델 설치 여부 확인

R 및 Python 모델의 설치 경로는 다음과 같습니다.

+ R의 경우: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64`

+ Python의 경우: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

모델 파일 이름은 다음과 같습니다.

+ AlexNet\_Updated.model
+ ImageNet1K\_mean.xml
+ pretrained.model
+ ResNet\_101\_Updated.model
+ ResNet\_18\_Updated.model
+ ResNet\_50\_Updated.model

모델이 이미 설치되어 있는 경우에는 [유효성 검사 단계](#verify)로 이동하여 사용 가능 여부를 확인합니다.

## <a name="download-the-installation-script"></a>설치 스크립트 다운로드

[https://aka.ms/mlm4sql](https://aka.ms/mlm4sql)을 클릭하여 **Install-MLModels.ps1** 파일을 다운로드합니다.

## <a name="execute-with-elevated-privileges"></a>상승된 권한으로 실행

1. PowerShell을 시작합니다. 작업 표시줄에서 PowerShell 프로그램 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.
2. 설치 스크립트 파일의 정규화된 경로를 입력하고 인스턴스 이름을 포함합니다. 다운로드 폴더와 기본 인스턴스를 가정하면 명령은 다음과 같이 표시될 수 있습니다.

   ```powershell
   PS C:\WINDOWS\system32> C:\Users\<user-name>\Downloads\Install-MLModels.ps1 MSSQLSERVER
   ```

**출력**

R 및 Python을 사용하여 인터넷에 연결된 SQL Server Machine Learning Services 기본 인스턴스에서 다음과 비슷한 메시지가 표시됩니다.

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

먼저 [mxlibs 폴더](#file-location)에서 새 파일을 확인합니다. 다음으로 데모 코드를 실행하여 모델이 설치되어 있고 작동하는지 확인합니다. 

### <a name="r-verification-steps"></a>R 확인 단계

1. C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64에서 **RGUI.EXE**를 시작합니다.

2. 명령 프롬프트에 다음 R 스크립트를 붙여넣습니다.

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

3. Enter 키를 눌러 감정 점수를 확인합니다. 출력은 다음과 같이 표시됩니다.

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

1. C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES에서 **Python.exe**를 시작합니다.

2. 명령 프롬프트에 다음 Python 스크립트 붙여넣기

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

3. Enter 키를 눌러 점수를 출력합니다. 출력은 다음과 같이 표시됩니다.

    ```python
    >>> print(sentiment_scores)
                                                review    scores         eval
    0            I really did not like the taste of it  0.461790         BLAH
    1                  It was surprisingly quite good!  0.960192  AWESOMENESS
    2  I will never ever ever go to that place again!!  0.310344         BLAH
    >>>
    ```

> [!NOTE]
> 데모 스크립트가 실패할 경우 먼저 파일 위치를 확인합니다. SQL Server 인스턴스가 여러 개 있는 시스템 또는 독립 실행형 버전과 함께 나란히 실행되는 인스턴스의 경우에는 설치 스크립트에서 환경을 잘못 읽을 수 있으며 파일을 잘못된 위치에 저장할 수 있습니다. 일반적으로 파일을 올바른 mxlib 폴더에 수동으로 복사하면 문제가 해결됩니다.

## <a name="examples-using-pre-trained-models"></a>미리 학습된 모델을 사용하는 예제

다음 링크에는 미리 학습된 모델을 호출하는 예제 코드가 포함되어 있습니다.

+ [코드 샘플: 텍스트 기능화기를 사용하여 감정 분석](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

<a name="bkmk_resources"></a> 

## <a name="research-and-resources"></a>연구 및 리소스

현재 사용할 수 있는 모델은 감정 분석 및 이미지 분류를 위한 심층 신경망(DNN) 모델입니다. 미리 학습된 모든 모델은 Microsoft의 [Computation Network Toolkit](https://cntk.ai/Features/Index.html), 즉 **CNTK**를 사용하여 학습되었습니다.

각 네트워크의 구성은 다음 참조 구현을 기반으로 합니다.

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

이러한 딥 러닝 모델에 사용되는 알고리즘과 이러한 알고리즘이 CNTK를 사용하여 구현 및 학습되는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

+ [ImageNet 챌린지 마일스톤을 설정하는 Microsoft 연구원의 알고리즘](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [가장 효율적인 분산 딥 러닝 컴퓨팅 성능을 제공하는 Microsoft Computational Network Toolkit](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="see-also"></a>참고 항목

+ [SQL Server Machine Learning 서비스](sql-machine-learning-services-windows-install.md)
+ [SQL Server 인스턴스에서 R 및 Python 구성 요소 업그레이드](../install/upgrade-r-and-python.md)
+ [R용 MicrosoftML 패키지](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ [Python용 microsoftml 패키지](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
