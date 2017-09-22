---
title: "미리 학습 된 기계 학습 모델을 SQL Server에 설치 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/15/2017
ms.prod: sql-server-2016
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
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: b52fcc1e4ac77df2968a4ea6cbd6e546ff1b74ac
ms.contentlocale: ko-kr
ms.lasthandoff: 09/19/2017

---
# <a name="install-pretrained-machine-learning-models-on-sql-server"></a>SQL Server에 대 한 모델을 학습 하는 미리 학습 된 컴퓨터를 설치 합니다.

이 항목에는 어떻게 인스턴스에 SQL Server의 미리 학습 된 모델을 추가할 이미 R 서비스 또는 컴퓨터 학습 서비스 설치 설명 합니다.

미리 학습 된 모델은 Microsoft R Server (또는 Microsoft 학습 서버 컴퓨터에 대 한 업데이트)는 업데이트로 제공 됩니다. 인스턴스 및 Microsoft R의 최신 버전 가져오기 하는 방법에 대 한 정보를 참조 하십시오. [R Services의 인스턴스에 R 구성 요소를 업그레이드](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

R 서버에 대 한 별도 Windows 기반 설치를 실행 해야만 이러한 모델을 설치할 수 있습니다.
그러나 모델은 SQL Server를 설치할 때 사용 하 여 몇 가지 추가 단계가 있습니다. 이 항목에서는 프로세스를 설명 합니다.

## <a name="benefits-of-using-pretrained-models"></a>미리 학습 된 모델을 사용할 때의 이점

미리 학습 된 모델 기능 생성, 이미지 또는 감성 분석 등의 작업을 수행할 필요는 없지만 리소스가 큰 데이터 집합을 구하거 나 복잡 한 모델을 학습 하는 고객을 지원 하기 위해 제공 되었습니다. 미리 학습 된 모델을 사용 하 여 텍스트 및 이미지 처리를 가장 효율적으로 시작할 수 있습니다.

현재 사용할 수 있는 모델은 감성 분석 및 이미지 분류에 대 한 심층 신경망 (DNN) 모델입니다. 모든 4 개의 미리 학습 된 모델 CNTK에 대해 학습 되었습니다. 각 네트워크의 구성 된 다음 참조 구현이 기반으로 합니다.

+ ResNet 18
+ ResNet 50
+ ResNet 101
+ AlexNet

심층 잔여 네트워크와 CNTK를 사용 하 여 구현 하는 방법에 대 한 자세한 내용은 다음이 문서를 참조 합니다.

+ [Microsoft 연구원 알고리즘 ImageNet 챌린지 마일스 톤 설정](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [네트워크 도구 키트를 계산 하는 Microsoft 제공 정도의 계산 성능을 학습 하는 가장 효율적인 분산된 딥](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-install-the-models-on-sql-server"></a>SQL Server에서 모델을 설치 하는 방법

   > [!NOTE]
   > 
   > Microsoft R Server를 설치 하거나 SQL Server의 인스턴스는 별도 Windows 기반 설치 관리자를 사용 하면 미리 학습 된 모델은 설치 프로그램에서 사용할 수 있는 합니다. 참조 [Windows 용 R 설치 서버](https://docs.microsoft.com/en-us/r-server/install/r-server-install-windows)합니다.
   > 
   > Microsoft R server는 모델을 사용 하 몇 가지 추가 단계가 필요할 수 있습니다. 자세한 내용은 참조 [설치 및 배포 하는 방법을 미리 MicrosoftML와 기계 학습 모델을 학습](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models)

1. 미리 학습 된 모델은 SQL Server; 설치할 때 기본적으로 설치 되지 SQL Server 설치 프로그램을 마친 후 설치 프로그램 명령줄 유틸리티를 실행 하 여에 추가 해야 합니다.

2. 관리자 권한 명령 프롬프트를 열고도 Microsoft R 설치 관리자를 포함 하는 SQL Server에 대 한 부트스트랩 설치 폴더로 이동 합니다.

    SQL Server 2017 RC 1의 기본 인스턴스에이 합니다.
    
    `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\SQL2017RC1\x64\`

3. 를 설치 하려면 구성 요소와 여기서 미리 학습 된 모델을 추가 하도록 다음 인수를 사용 하 여 폴더를 지정 합니다.

  + 사용 하 여 모델을 사용 하려면 **R_SERVICES**

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\R_SERVICES`

    예를 들어 기본 인스턴스의 SQL Server 2017에서 R을 사용 하 여 미리 학습 된 모델의 사용을 사용 하려면이 문을 실행 합니다.

    `RSetup.exe /install /component MLM /version 9.2.0.22 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES"`

  + 사용 하 여 모델을 사용 하려면 **PYTHON_SERVICES**

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir <SQL_DB_instance_folder>\PYTHON_SERVICES`

    예를 들어 Python을 사용 하 여 SQL Server 2017 년 1의 기본 인스턴스에 대 한 미리 학습 된 모델을 사용 하도록 설정 하려면이 문을 실행 합니다.

    `RSetup.exe /install /component MLM /version 9.2.0.22 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES"`

4. 버전 매개 변수는 다음 값이 지원 됩니다.

    + 릴리스 후보 0: **9.1.0.0**
    + 릴리스 후보 1: **9.2.0.22**
    + 최종 버전 번호 (릴리스되지): **9.2.0.100**

5. R에 다음과 같은 모델을 추가 해야 설치에 성공한 경우\_서비스 또는 PYTHON\_서비스 폴더:

    - AlexNet_Updated.model
    - ImageNet1K_mean.xml
    - pretrained.model
    - ResNet_101_Updated.model
    - ResNet_18_Updated.model
    - ResNet_50_Updated.model

## <a name="examples"></a>예

모델을 설치한 후에 R 코드에서 호출 하 여 모델을 사용할 수 있습니다.

### <a name="image-featurization-example"></a>이미지 기능 생성 예제

이미지에 대 한 모델은 전면의 기능 제공 하는 이미지의 생성을 지원 합니다. 모델을 사용 하려면 호출는 **featurizeImage** 변환 합니다.

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
> 
> 읽기 또는 미리 학습 된 모델 자체를 수정 하는 것이 불가능 합니다. 이 특정 모델 기반 [CNTK](https://docs.microsoft.com/cognitive-toolkit/) 모델 하지만 성능상의 이유로 네이티브 형식을 사용 하 여 압축 됩니다.

### <a name="text-analysis-example"></a>텍스트 분석 예

이 샘플 분류에 대 한 미리 학습 된 모델의 사용을 보여 줍니다.

[텍스트 Featurizer를 사용 하 여 의미 분석](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

