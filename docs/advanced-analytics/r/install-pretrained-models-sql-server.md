---
title: "미리 학습 된 기계 학습 모델을 SQL Server에 설치 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 8f4a145700d12f31a868cc3fc20a9dbdbe6f45ea
ms.contentlocale: ko-kr
ms.lasthandoff: 10/24/2017

---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>SQL Server에 대 한 모델을 학습 하는 미리 학습 된 컴퓨터를 설치 합니다.

이 문서에는 어떻게 인스턴스에 SQL Server의 미리 학습 된 모델을 추가할 이미 R 서비스 또는 컴퓨터 학습 서비스 설치 설명 합니다.

미리 학습 된 모델은 Microsoft R Server를 설치할 때 또는 독립 실행형 설치 관리자를 사용 하 여 컴퓨터 학습 서버 옵션으로 제공 됩니다. 이 설치 관리자를 사용 하 여 미리 학습 된 모델만 가져오려는 또는 기계 학습의 SQL Server 2016 또는 SQl Server 2017 인스턴스의 구성 요소 업그레이드를 사용할 수 있습니다.

설치 프로그램을 실행 하 여 미리 학습 된 모델을 다운로드 한 후에 SQL Server와 함께 사용 하기 위해 모델을 구성 하려면 몇 가지 추가 단계. 이 문서는 프로세스를 설명합니다.

자세한 내용은 다음 문서를 참조하세요.

+ [미리 학습 된 기계 학습 감성 분석 및 이미지 검색에 대 한 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)

+ [R Services의 인스턴스에 R 구성 요소를 업그레이드](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

## <a name="benefits-of-using-pretrained-models"></a>미리 학습 된 모델을 사용할 때의 이점

기능 생성, 이미지 또는 감성 분석 등의 작업을 수행할 필요는 없지만 큰 데이터 집합을 구하거 나 복잡 한 모델을 학습 하는 리소스가 고객이 이러한 미리 학습 된 모델을 만들었습니다. 미리 학습 된 모델을 사용 하 여 텍스트 및 이미지 처리를 가장 효율적으로 시작할 수 있습니다.

현재 사용할 수 있는 모델은 감성 분석 및 이미지 분류에 대 한 심층 신경망 (DNN) 모델입니다. Microsoft의를 사용 하 여 모든 미리 학습 된 모델의 성향을 습득할 된 [계산 네트워크 도구 키트](https://cntk.ai/Features/Index.html), 또는 **CNTK**합니다. 

각 네트워크의 구성 된 다음 참조 구현이 기반으로 합니다.

+ ResNet 18
+ ResNet 50
+ ResNet 101
+ AlexNet

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

    + 서버를 학습 하는 컴퓨터를 설치 하 고 업데이트 된 Python 또는 R 구성 요소 바인딩 옵션을 사용 하 여 이전에, 이전에 선택한 모든가 종료 **그대로**, 미리 학습 된 모델 옵션을 선택 합니다. 이전에 선택한 옵션을 선택 취소 하지 마십시오 또는 제거 됩니다.

3. Windows 명령 프롬프트를 열고 설치가 완료 되 면 **관리자 권한으로**, 또한 Microsoft R 설치 관리자를 포함 하는 SQL Server에 대 한 설치 부트스트랩 폴더로 이동 합니다. SQL Server 2017의 기본 인스턴스에 폴더가 합니다.
    
    `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\SQL2017\x64\`

4. 구성 요소를 설치, 버전 및 다음 예에서 같이 RSetup.exe에 대 한 인수를 사용 하 여 모델 원본 파일을 포함 하는 폴더를 지정 합니다.

  + 사용 하 여 모델을 사용 하려면 **R_SERVICES**, 다음 구문 및 경로 사용 하 여:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\R_SERVICES\library\MicrosoftML\mxLibs\x64`

    예를 들어 기본 인스턴스의 SQL Server 2017 년에 R에 대 한 미리 학습 된 모델의 최신 버전을 사용할 수 있도록 하려면이 문을 실행 합니다.

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    명명 된 인스턴스에서 명령은 다음과 같습니다. 다음과 같이

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

  + 사용 하 여 모델을 사용 하려면 **PYTHON_SERVICES**, 다음 구문 및 경로 사용 하 여:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs`

    예를 들어 기본 인스턴스의 SQL Server 2017 년 1에서 Python에 대 한 미리 학습 된 모델의 최신 버전을 사용할 수 있도록 하려면이 문을 실행 합니다.

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs"`

    명명 된 인스턴스에서 명령은 다음과 같습니다. 다음과 같이

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\PYTHON_SERVICES\Lib\site-packages\microsoftml\mxLibs"`

5. 버전 매개 변수는 다음 값이 지원 됩니다.

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

