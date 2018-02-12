---
title: "미리 학습 된 기계 학습 모델을 SQL Server에 설치 | Microsoft Docs"
ms.date: 11/16/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 5d9f60684cc749c35674233fbdaaa222953396d9
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>SQL Server에 대 한 모델을 학습 하는 미리 학습 된 컴퓨터를 설치 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에는 어떻게 인스턴스에 SQL Server의 미리 학습 된 모델을 추가할 이미 R 서비스 또는 컴퓨터 학습 서비스 설치 설명 합니다.

Microsoft R Server 또는 서버를 학습 하는 컴퓨터에 대 한 별도 Windows installer를 사용 하 여 미리 학습 된 모델을 설치할 수 있는 옵션이 표시 됩니다. 이 설치 관리자를 사용 하 여 미리 학습 된 모델만 가져오려는 하거나에 사용할 수 있습니다 [기계 학습 구성 요소 업그레이드](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md) 인스턴스의 SQL Server 2016 또는 SQL Server 2017 합니다.

설치 프로그램을 실행 하 여 미리 학습 된 모델을 다운로드 한 후에 SQL Server와 함께 사용 하기 위해 모델을 구성 하려면 몇 가지 추가 단계. 이 문서는 프로세스를 설명합니다.

SQL Server 데이터를 미리 학습 된 모델을 사용 하는 방법의 예는 SQL Server 기계 학습 팀이 블로그를 참조: 

+ [SQL Server 컴퓨터 학습 서비스에서 python 감정 분석](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

## <a name="benefits-of-using-pretrained-models"></a>미리 학습 된 모델을 사용할 때의 이점

감성 분석 이나 이미지 기능 생성 등의 작업 수행을 해야 하는 하지만 큰 데이터 집합을 구하거 나 복잡 한 모델을 학습 하는 리소스 없는 고객에 게 유용한 이러한 미리 학습 된 모델을 만들었습니다. 미리 학습 된 모델을 사용 하 여 텍스트 및 이미지 프로세스를 효율적으로 시작할 수 있습니다.

현재 사용할 수 있는 모델은 감성 분석 및 이미지 분류에 대 한 심층 신경망 (DNN) 모델입니다. Microsoft의를 사용 하 여 모든 미리 학습 된 모델의 성향을 습득할 된 [계산 네트워크 도구 키트](https://cntk.ai/Features/Index.html), 또는 **CNTK**합니다.

각 네트워크의 구성 된 다음 참조 구현이 기반으로 합니다.

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

이러한 모델에 대 한 자세한 내용은 참조 [미리 학습 된 기계 학습 감성 분석 및 이미지 검색에 대 한 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)

심층 학습 네트워크 및 CNTK를 사용 하 여 구현 하는 방법에 대 한 자세한 내용은 다음이 문서를 참조 합니다.

+ [Microsoft 연구원 알고리즘 ImageNet 챌린지 마일스 톤 설정](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [네트워크 도구 키트를 계산 하는 Microsoft 제공 정도의 계산 성능을 학습 하는 가장 효율적인 분산된 딥](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-install-the-models-on-sql-server"></a>SQL Server에서 모델을 설치 하는 방법

1. 서버를 학습 하는 컴퓨터에 대 한 별도 Windows 기반 설치를 실행 합니다. 다운로드 위치에 대 한 참조.

    + [Windows에 대 한 서버를 학습 하는 컴퓨터를 설치 합니다.](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
    + [Windows 용 R Server 9.1 설치](https://docs.microsoft.com/r-server/install/r-server-install-windows)

2. 설치할 기능 선택 모델만을 가져오기 또는 설치 관리자를 사용 하 여 다른 업데이트 수행 여부에 따라 달라 집니다.
 
    + 이 서버를 학습 하는 컴퓨터를 새로 설치 하 고 Python 또는 R 구성 요소를 선택에 다른 변경을 수행 하지 않을 경우 **만** 미리 학습 된 모델 옵션입니다. 사용권 계약을 포함 하 여 다른 모든 메시지를 수락 합니다.

    + Python 또는 R 구성 요소를 동시에 업그레이드 하려면 업데이트 언어 (R, Python, 또는 둘 다)을 선택 하 고 미리 학습 된 모델 옵션을 선택 합니다. 이러한 변경 내용을 적용할 하나 이상의 인스턴스를 선택 합니다.

    + 서버를 학습 하는 컴퓨터를 설치 하 고 업데이트 된 Python 또는 R 구성 요소 바인딩 옵션을 사용 하 여 이전에, 이전에 선택한 모든가 종료 **그대로**, 미리 학습 된 모델 옵션을 선택 합니다. 이전에 선택한 옵션; 선택은 취소 하지 마십시오 이렇게 하면 설치 관리자 구성 요소를 제거 합니다.

3. Windows 명령 프롬프트를 열고 설치가 완료 되 면 **관리자 권한으로**, 또한 Microsoft R 설치 관리자를 포함 하는 SQL Server에 대 한 설치 부트스트랩 폴더로 이동 합니다. SQL Server 2017의 기본 인스턴스에 폴더가 합니다.
    
    `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\SQL2017\x64\`

4. RSetup.exe를 실행 하 고 구성 요소를 설치, 버전 및 이러한 예제에 표시 된 명령줄 인수를 사용 하 여 모델 원본 파일을 포함 하는 폴더를 나타냅니다.

    + 사용 하 여 모델을 사용 하려면 **R_SERVICES**:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    예를 들어 기본 인스턴스의 SQL Server 2017 년에 R에 대 한 미리 학습 된 모델의 최신 버전을 사용할 수 있도록 하려면이 문을 실행 합니다.

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    명명 된 인스턴스에서 명령은 다음과 같습니다. 다음과 같이

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + R Server (독립 실행형) 또는 컴퓨터 학습 서버 (독립 실행형)와 미리 학습 된 모델 사용:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    예를 들어 사용할 수 있도록 미리 학습 된 모델의 최신 버전, R에 대 한 SQL Server 2016을 사용 하 여 R server 기본 설치에서이 문을 실행 합니다.

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir ‘C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\MicrosoftML\mxLibs\"`
    
    + 사용 하 여 미리 학습 된 모델을 사용 하려면 **PYTHON_SERVICES**:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    예를 들어 기본 인스턴스의 SQL Server 2017 년 1에서 Python에 대 한 미리 학습 된 모델의 최신 버전을 사용할 수 있도록 하려면이 문을 실행 합니다.

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    명명 된 인스턴스에서 명령은 다음과 같습니다. 다음과 같이

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + Python을 사용 하도록 학습 Server 컴퓨터 (독립 실행형) 사용 하 여 모델을 미리 학습 된:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<sql_folder>\PYTHON_SERVER\site-packages\microsoftml\mxLibs"`

    예를 들어 SQL Server 2017 설치 프로그램을 사용 하 여 학습 Server (독립 실행형)를 컴퓨터의 기본 설치 라고 가정할 경우이 문을 실행 합니다.

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER\Lib\site-packages\microsoftml\mxLibs"`

5. Version 매개 변수는 다음 값 지원 됩니다.

    + 릴리스 후보 0: **9.1.0.0**
    + 릴리스 후보 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + 누적 업데이트 1: **9.2.0.24**

6. R에 다음과 같은 모델을 추가 해야 설치에 성공한 경우\_서비스 또는 PYTHON\_서비스 폴더:

    - AlexNet\_Updated.model
    - ImageNet1K\_mean.xml
    - pretrained.model
    - ResNet\_101\_Updated.model
    - ResNet\_18\_Updated.model
    - ResNet\_50\_Updated.model


> [!NOTE]
> 
> 모델 파일의 경로를 너무 긴 경우에 모델 파일에서 Python 코드를 호출할 때 오류가 발생할 수 있습니다. 현재 Python 구현에서 제한 사항 때문입니다. 이 문제는 향후 서비스 릴리스에서 수정 될 예정입니다.

## <a name="examples"></a>예

모델을 설치한 후에 사용자 코드에서 호출 하 여 모델을 사용할 수 있습니다.

### <a name="image-featurization-example"></a>이미지 기능 생성 예제

이미지에 대 한 모델은 전면의 기능 제공 하는 이미지의 생성을 지원 합니다. 사용 하 여이 특정 모델을 학습 [CNTK](https://docs.microsoft.com/cognitive-toolkit/)합니다. 

모델을 사용 하려면 호출는 **featurizeImage** 변환 합니다.

+ [featurizeImage: 컴퓨터 학습 이미지 기능 생성 변형](https://docs.microsoft.com/r-server/r-reference/microsoftml/featurizeimage)

이 예제에서는 두 번째 코드 블록을 참조 하십시오. 이미지가 로드 될 크기를 조정 하 고 convolutional DNN 미리 학습 된 모델에 들어가지 않고 기능화 합니다. DNN featurizer 출력 이미지 분류에 대 한 선형 모델 학습에 사용 됩니다.

학습된 된 모델의 요구 사항에 맞게 이미지 크기를 조정 해야: 학습에 사용 되는 이미지 되었습니다 224 x 224 px 합니다. AlexNet 모델을 사용한 경우 이미지 크기는 조정 227 x 227를 px 합니다.

```R
 model <- rxFastLinear(
     Label ~ Features,
     data = train,
     mlTransforms = list(
         loadImage(vars = list(Features = "Path")),
         resizeImage(vars = "Features", width = 224, height = 224), 
         extractPixels(vars = "Features"),
         featurizeImage(var = "Features")
         ),
     mlTransformVars = "Path")
```

> [!NOTE]
> 수 없으면를 읽거나 수정할 미리 학습 된 모델을 네이티브 형식을 사용 하 여 성능 향상을 위해 압축 때문에 있습니다.

### <a name="text-analysis-example"></a>텍스트 분석 예

텍스트 분류에 대 한 미리 학습 된 텍스트 기능 생성 모델을 사용 하는 방법 보여 주는 다음 예제를 참조 하십시오.

[텍스트 Featurizer를 사용 하 여 의미 분석](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)
