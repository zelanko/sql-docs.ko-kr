---
title: 미리 학습 된 기계 학습 모델을 SQL Server에 설치 | Microsoft Docs
ms.date: 03/14/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: ''
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: a1228597a1781ca13952a249f554bdea0a990a4d
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="install-pre-trained-machine-learning-models-on-sql-server"></a>SQL Server에 대 한 모델을 학습 하는 미리 학습 된 컴퓨터를 설치 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에는 어떻게 인스턴스에 SQL Server의 미리 학습 된 모델을 추가할 이미 R 서비스 또는 설치 된 SQL Server 컴퓨터 학습 서비스 설명 합니다. 

미리 학습 된 모델을 감성 분석 이나 이미지 기능 생성 등의 작업을 수행 해야 하는 하지만 큰 데이터 집합을 구하거 나 복잡 한 모델을 학습 하는 리소스 없는 고객에 게 유용한 존재 합니다. 컴퓨터 학습 서버 팀 생성 하 고 텍스트와 이미지 프로세스를 효율적으로 시작할 수 있도록 이러한 모델을 학습 합니다. 자세한 내용은 참조는 [리소스](#bkmk_resources) 이 문서의 섹션.

SQL Server 데이터를 미리 학습 된 모델을 사용 하는 방법의 예는 SQL Server 기계 학습 팀이 블로그를 참조: [SQL Server 컴퓨터 학습 서비스에서 python 감정 분석](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/11/01/sentiment-analysis-with-python-in-sql-server-machine-learning-services/)

## <a name="pre-trained-model-availability"></a>미리 학습 된 모델 가용성

미리 학습 된 모델은 Microsoft 컴퓨터 학습 서버 (또는 Microsoft R Server를 SQL Server 2016 설치에 모델을 추가 하는 경우)의 설치 미디어를 사용 하 여 설치 됩니다. 모델을 설치 하려면 무료 개발자 버전을 사용할 수 있습니다. 추가 모델을 설치와 관련 된 비용입니다. 

미리 학습 된 모델에서 다음 제품 및 언어와 작동 합니다. 설치 프로그램 언어 통합, MicrosoftML 또는 microsoftml 라이브러리를 검색 한 다음 해당 라이브러리에 미리 학습 된 모델을 삽입 합니다. 모델 설치가 완료 되 면 라이브러리 함수를 통해 모델 액세스.

+ SQL Server 2016 R Services (In-database)-R만,와 [MicrosoftML 라이브러리](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ SQL Server 2016 R 서버 (독립 실행형)-R만,와 [MicrosoftML 라이브러리](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)
+ SQL Server 2017 컴퓨터 학습 Services (In-database)-R [MicrosoftML 라이브러리]와 (https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), Python는 [microsoftml 라이브러리](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)
+ SQL Server 2017 컴퓨터 학습 Server (독립 실행형)-R [MicrosoftML 라이브러리]와 (https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), Python는 [microsoftml 라이브러리](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)

설치 프로세스는 SQL Server의 버전에 따라 약간 다릅니다. 각 버전에 대 한 지침은 다음 섹션을 참조 합니다.

> [!NOTE]
> 읽기 또는 미리 학습 된 모델을 수정 하는 것이 불가능 합니다. 네이티브 형식을 사용 하 여 성능 향상을 위해 압축 합니다.

## <a name="obtain-files-for-an-offline-installation"></a>오프 라인 설치에 대 한 파일 가져오기

미리 학습 된 모델을 인터넷에 연결 되지 않은 서버에 설치 하려면 사전에 적절 한 설치 관리자를 다운로드 하 고 서버에서 로컬 폴더에 설치 관리자를 복사 해야 합니다. 

모든 R 서버와 컴퓨터 학습 서버 설치 관리자에 대 한 다운로드 링크에 대 한이 페이지를 참조 하십시오: [오프 라인 설치](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)

## <a name="install-pre-trained-models-on-sql-server-2016-r-services"></a>SQL Server 2016 R Services에 미리 학습 된 모델을 설치 합니다.

SQL Server 2016 설치 및 기계 학습 이라는 프로세스에서 구성 요소를 먼저 업그레이드 하는 경우에 미리 학습 된 R 모델을 사용 하 여 수 **바인딩**합니다. 

이렇게 하려면가 SQL Server 2016 R Services 설치와 인스턴스 또는 인스턴스를 선택 하는 컴퓨터에서 Microsoft R Server 또는 서버를 학습 하는 컴퓨터에 대 한 별도 Windows installer를 실행 **바인딩할**합니다. 오른쪽에 좀 더 자주 업데이트를 허용 하도록 변경 될 지원 정책 인스턴스와 연결 된 하는 인스턴스 방법을 바인딩 

1. 실행에 대 한 별도 Windows 기반 설치 시작 [R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server) 또는 [컴퓨터 학습 서버](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)합니다.

2. 를 업그레이드 하려면 인스턴스를 선택 하 고 미리 학습 된 모델을 가져올 옵션을 선택 합니다.

    자세한 내용은 참조 [컴퓨터 학습 구성 요소를 SQL Server에서 사용 되는 업그레이드](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

    바인딩하는 R 구성 요소를 업데이트 하 고 미리 학습 된 모델을 추가 하려면 이전에 수행한 경우 이전에 선택한 항목을 그대로 둡니다 **그대로**, 미리 학습 된 모델 옵션을 선택 합니다. 
    
    이전에 선택한 옵션; 선택은 취소 하지 마십시오 이렇게 하면 설치 관리자 구성 요소를 제거 합니다.

3. 모델 위치에 대 한 기본 설정을 적용 하는 것이 좋습니다.

4. 사용권 계약을 포함 하 여 다른 모든 메시지를 수락 합니다.

바인딩이 완료 되 면 R 버전 및 인스턴스와 연결 된 라이브러리 R 서버 또는 서버를 학습 하는 컴퓨터에 제공 된 새 버전으로 대체 됩니다. 

SQL Server 2016에서는 SQL Server 2016 인스턴스 라이브러리와 모델을 등록 하려면 몇 가지 추가 단계를 수행 해야 합니다. 미리 학습 된 모델을 설치 된 각 인스턴스에 대해 이러한 단계를 반복 합니다.

1. Windows 명령 프롬프트를 열고 **관리자 권한으로**합니다.

2. 또한 Microsoft R 설치 관리자를 포함 하는 SQL Server에 대 한 설치 부트스트랩 폴더로 이동 합니다. SQL Server 2016의 기본 인스턴스에 폴더가 합니다.
    
    `C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\SQL2017\x64\`

3. 실행 `RSetup.exe` 구성 요소를 설치, 버전 및이 구문을 사용 하 여 모델 원본 파일을 포함 하는 폴더를 나타냅니다.

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<SQL_DB_instance_folder>\R_SERVICES\library\MicrosoftML\mxLibs\x64"`을 참조하세요. 

    Version 매개 변수는 다음 값 지원 됩니다.

    + 릴리스 후보 0: **9.1.0.0**
    + 릴리스 후보 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + 누적 업데이트 1: **9.2.0.24**
    + 누적 업데이트 4: **9.3.0**

    > [!NOTE]
    > 해당 SQL Server 릴리스에 알 수 있는 업데이트가 게시 된 시간의 나열 됩니다. SQL Server와 함께 설치 된 버전을 잘 모를 경우, 인스턴스에 대 한 R_SERVICES 폴더 열고 열고 관리자 권한 (`~\R_SERVICES\bin\x64`). 시작 화면에는 Microsoft R Open 버전 및 서버를 학습 하는 컴퓨터에 대 한 버전이 표시 됩니다. 

    예를 들어 미리 학습 된 r의 기본 인스턴스와 모델링 **R_SERVICES**,이 명령을 실행 합니다.

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

    명명 된 인스턴스에서 명령은 다음과 같습니다. 다음과 같이

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL13.MyInstanceName\R_SERVICES\library\MicrosoftML\mxLibs\x64"`

4. 다음과 같은 모델에 추가 해야 설치가 성공적으로 하는 경우 프로그램 `R_SERVICES` 폴더:

    + AlexNet\_Updated.model
    + ImageNet1K\_mean.xml
    + pretrained.model
    + ResNet\_101\_Updated.model
    + ResNet\_18\_Updated.model
    + ResNet\_50\_Updated.model

## <a name="install-pre-trained-models-on-sql-server-machine-learning-services-in-database"></a>SQL Server 컴퓨터 학습 Services (In-database)에 미리 학습 된 모델을 설치 합니다.

SQL Server 2017 이미 설치한 경우에 두 가지 방법으로 미리 학습 된 모델을 얻을 수 있습니다.

+ 바인딩을 사용 하 여 Python 및 R 구성 요소를 업그레이드 하 고 동시에 미리 학습 된 모델을 설치
+ 미리 학습 된 모델에만 설치 합니다.

다음 지침에서는 컴퓨터 학습 구성 요소를 업그레이드 하 고 동시에 미리 학습 된 모델을 가져오기는 프로세스에 설명 합니다.

1. 서버를 학습 하는 컴퓨터에 대 한 Windows 기반 설치 프로그램을 실행 합니다. 이 페이지의 링크에서 설치 관리자를 다운로드할 수 있습니다: [Windows 용 컴퓨터 학습 서버 설치](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)합니다.

2. 인터넷에 연결 하지 않은 서버에 모델을 설치 하는 경우에이 페이지에서 미리 학습 된 모델에 대 한 설치 관리자 다운로드 있는지 확인: [학습 서버 컴퓨터에 대 한 오프 라인 설치](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)합니다.

3. 설치 프로그램을 실행 합니다.

4. Python 또는 R 구성 요소를 동시에 업그레이드 하려면 업데이트 하려는 언어 (R, Python, 또는 둘 다)을 선택 합니다.

    서버를 학습 하는 컴퓨터를 설치 하 고 업데이트 된 Python 또는 R 구성 요소 바인딩 옵션을 사용 하 여 이전에, 이전에 선택한 모든가 종료 **그대로**, 미리 학습 된 모델 옵션을 선택 합니다. 이전에 선택한 옵션; 선택은 취소 하지 마십시오 이렇게 하면 설치 관리자 구성 요소를 제거 합니다.

5. 사용권 계약을 포함 하 여 다른 모든 메시지를 수락 합니다.

SQL Server 2017와 추가 구성은 필요 하지 않습니다.

> [!NOTE]
> 
> Python 모델에 대 한 모델 파일에서 Python 코드를 호출할 때 오류가 발생할 수 있습니다. 이 현재 Python 구현에서 제한으로 인해 모델 파일에 대 한 경로의 길이 제한 하는입니다. 이 문제 해결 및 향후 서비스 릴리스에서 사용할 수 있습니다.

## <a name="install-pre-trained-models-with-sql-server-standalone-r-server"></a>SQL Server 독립 실행형 R 서버와 미리 학습 된 모델을 설치 합니다.

SQL Server 2016 설치를 사용 하는 이전 버전의 R Server (독립 실행형)를 설치한 경우에 최신 Windows 기반 설치 관리자를 사용 하 여 R 서버를 업그레이드 하 여 미리 학습 된 모델을 사용 하는 기능을 추가할 수 있습니다. 

미리 학습 된 모델 처음 사용 하는 옵션으로 제공 된 [Microsoft R Server 9.1](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/introducing-microsoft-r-server-9-1-release/), 있지만 업그레이드 각 릴리스에 추가 되었습니다. 가능한 최신 버전을 가져오는 것이 좋습니다 하지만 이전 릴리스에서 다음과 같은 [R Server 해제](https://docs.microsoft.com/machine-learning-server/install/r-server-install)

다음 지침에는 R 구성 요소를 업그레이드 하 고 동시에 미리 학습 된 모델을 추가 하는 방법을 설명 합니다.

1. 실행에 대 한 별도 Windows 기반 설치 시작 [R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server) 또는 [컴퓨터 학습 서버](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)합니다.

2. 업데이트 하 고, 선택 하려는 언어 선택에서 **Pre-trained 모델** 옵션입니다.

    > [!TIP]
    > 이전에 R Server (독립 실행형)를 업데이트 하 고 미리 학습 된 모델을 추가 하 려 하는 설치 관리자를 실행 하는 경우 이전에 선택한 항목에 둡니다 **그대로**는 이전 버전을 선택 하 고**-모델을 학습** 옵션 . **없는** 이전에 선택한 옵션 선택을 취소 한; 이렇게 하면 설치 관리자 구성 요소를 제거 합니다.

    모델 위치에 대 한 기본 설정을 적용 하는 것이 좋습니다.

3. **계속**을 클릭합니다. 

4. 사용권 계약을 포함 하 여 다른 모든 메시지를 수락 합니다.

설치가 완료 되 면 미리 학습 된 모델을 등록 하는 몇 가지 추가 단계를 수행 해야 합니다.

1. Windows 명령 프롬프트를 열고 **관리자 권한으로**합니다.

2. 또한 Microsoft R 설치 관리자를 포함 하는 R Server (독립 실행형)에 대 한 설치 부트스트랩 폴더로 이동 합니다. 

3. 실행 `RSetup.exe` 구성 요소를 설치, 버전 및이 구문을 사용 하 여 모델 원본 파일을 포함 하는 폴더를 나타냅니다.

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    Version 매개 변수는 다음 값 지원 됩니다.

    + 릴리스 후보 0: **9.1.0.0**
    + 릴리스 후보 1: **9.2.0.22**
    + RTM: **9.2.0.100**
    + 누적 업데이트 1: **9.2.0.24**
    + 누적 업데이트 4: **9.3.0**

    예를 들어 R Server (독립 실행형)의 기본 설치에 R에 대 한 미리 학습 된 모델의 최신 버전을 사용할 수 있도록 하려면이 문을 실행 합니다.

    `RSetup.exe /install /component MLM /version 9.3.0 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\MicrosoftML\mxLibs\"`

## <a name="install-pre-trained-models-with-sql-server-2017-standalone-server"></a>미리 학습 된 모델 SQL Server 2017 독립 실행형 서버 설치

SQL Server 2017 설치 프로그램을 사용 하 여 컴퓨터 학습 서버를 설치한 경우 Windows 기반 설치 프로그램을 실행 하 여 미리 학습 된 모델을 추가 합니다. Python 또는 R 구성 요소를 업그레이드 하는 옵션을 선택할 수 있으며 동시에 미리 학습 된 모델을 추가 합니다. 

설치가 완료 된 후 추가 구성이 필요 합니다.

## <a name="bkmk_resources"></a> 연구 및 리소스

현재 사용할 수 있는 모델은 감성 분석 및 이미지 분류에 대 한 심층 신경망 (DNN) 모델입니다. Microsoft의를 사용 하 여 모든 미리 학습 된 모델의 성향을 습득할 된 [계산 네트워크 도구 키트](https://cntk.ai/Features/Index.html), 또는 **CNTK**합니다.

각 네트워크의 구성 된 다음 참조 구현이 기반으로 합니다.

+ ResNet-18
+ ResNet-50
+ ResNet-101
+ AlexNet

구현 하는 방법 및 이러한 심층 학습 모델에 사용 된 알고리즘에 대 한 자세한 내용은 다음이 문서를 참조 CNTK를 사용 하 여 학습, 및:

+ [Microsoft 연구원 알고리즘 ImageNet 챌린지 마일스 톤 설정](https://www.microsoft.com/research/blog/microsoft-researchers-algorithm-sets-imagenet-challenge-milestone/)

+ [네트워크 도구 키트를 계산 하는 Microsoft 제공 정도의 계산 성능을 학습 하는 가장 효율적인 분산된 딥](https://www.microsoft.com/research/blog/microsoft-computational-network-toolkit-offers-most-efficient-distributed-deep-learning-computational-performance/)

## <a name="how-to-use-pre-trained-models-for-text-analysis"></a>텍스트 분석을 위해 미리 학습 된 모델을 사용 하는 방법

텍스트 분류에 대 한 미리 학습 된 텍스트 기능 생성 모델을 사용 하는 방법 보여 주는 다음 예제를 참조 하십시오.

[텍스트 Featurizer를 사용 하 여 의미 분석](https://github.com/Microsoft/microsoft-r/tree/master/microsoft-ml/Samples/101/BinaryClassification/SimpleSentimentAnalysis)

## <a name="how-to-use-pre-trained-models-for-image-detection"></a>이미지 검색에 대 한 미리 학습 된 모델을 사용 하는 방법

이미지에 대 한 미리 학습 된 모델 기능 제공 하는 이미지의 생성을 지원 합니다. 모델을 사용 하려면 호출는 **featurizeImage** 변환 합니다. 이미지가 로드 될 크기를 조정 하 고 학습 된 모델에 들어가지 않고 기능화 합니다. DNN featurizer 출력 이미지 분류에 대 한 선형 모델 학습에 사용 됩니다.

이 모델을 사용 하려면 모든 이미지 학습된 된 모델의 요구 사항에 맞게 크기가 조정 해야 합니다. 예를 들어 AlexNet 모델을 사용 하는 경우 이미지 크기가 조정 되도록 227 x 227를 px 합니다.

자세한 내용은 참조 [감성 분석 및 이미지 검색에 대 한 미리 학습 된 모델](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)
