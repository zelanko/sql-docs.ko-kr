---
title: "Azure 기계 학습에 대 한 가상 컴퓨터를 프로 비전 | Microsoft Docs"
ms.custom: 
ms.date: 10/16/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: 7cb9e069fc3b537f8aab9d048a152435ad0cc6ac
ms.contentlocale: ko-kr
ms.lasthandoff: 10/17/2017

---
# <a name="provision-a-virtual-machine-for-machine-learning-on-azure"></a>Azure 기계 학습에 대 한 가상 컴퓨터를 프로 비전

Azure에서 가상 컴퓨터는 기계 학습 솔루션에 대 한 전체 서버 환경을 신속 하 게 구성 하는 데 편리한 옵션입니다. 이 문서에서는 기계 학습 된 R 서버, 컴퓨터 학습 서버 또는 SQL Server를 포함 하는 일부 가상 컴퓨터 이미지를 나열 합니다.

이 목록은 나와 있으며, 컴퓨터 학습 서버 또는 SQL Server 컴퓨터 학습 서비스 검색을 용이 하 게 관련 된 이미지의 이름을 제공 하는 적합 하지 않습니다.

> [!TIP]
> Azure 포털 및 Azure Marketplace의 새 버전을 사용 하는 것이 좋습니다. 클래식 포털에서 Azure 갤러리를 검색할 때 일부 이미지를 사용할 수 없는 경우

## <a name="how-to-provision-a-virtual-machine"></a>가상 컴퓨터를 프로 비전 하는 방법

Azure Vm을 사용 하 여 처음 하려는 경우에 포털을 사용 하 고 가상 컴퓨터를 구성 하는 방법에 대 한 자세한 내용은 다음이 문서를 참조 하는 것이 좋습니다.

+ [가상 컴퓨터-시작](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [Windows 가상 컴퓨터 시작](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/)

## <a name="find-a-machine-learning-image"></a>컴퓨터 학습 이미지 찾기

1. Azure 포털 (portal.azure.com)에서 클릭 **가상 컴퓨터**, 하거나 클릭 **새로 만들기**합니다.

2. 이름별으로 리소스를 필터링 할 수 있는 페이지의 위쪽에 있는 검색 상자를 찾습니다. 

3. 에 "R" 서버나 "ML 서버 (")을 입력에서 **필터** 관련된 리소스의 목록을 보려면 제어 합니다. 클릭 **시장에서 검색** 가상 컴퓨터를 볼 수 있습니다.

    > [!TIP]
    > 
    > 필터 컨트롤에 대 한 가능한 다른 문자열은 "데이터 과학" 및 "기계 학습"입니다.
    > 
    > 사용 된 `%` 가상 컴퓨터의 이름을 확인 하려면 검색에 와일드 카드입니다. 예를 들어 입력할 수 있습니다 `"`% Julia %` or `%R %'입니다.

4. Windows 용 R 서버를 가져오려면 선택 **R 서버만 SQL Server 2016 Enterprise**합니다.
  
    [R 서버](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) 는 SQL Server Enterprise Edition 기능으로, 사용이 허가 하지만 버전 9.1 독립 실행형 서버로 설치 되 고 최신 수명 주기 지원 정책에 서비스를 제공 합니다.

    > [!NOTE] 
    > 
    > 이 조회는 9.2.1 및 SQL Server 2017을 포함 하는 새 가상 컴퓨터의 릴리스에 대 한 학습 서버 컴퓨터의 릴리스 합니다.
    > 그때 까지는 SQL Server 설치 센터를 사용 하 고 업그레이드 옵션을 선택 하 여이 가상 컴퓨터에 설치 된 SQL server 버전을 업데이트할 수 있습니다. 자세한 내용은 참조 [설치 마법사를 사용 하 여 SQL Server 업그레이드](https://docs.microsoft.com/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup)합니다.

5. 만든 가상 컴퓨터를 실행 중인 후 클릭는 **연결** 단추에 대 한 연결을 열고 새 컴퓨터에 로그인 합니다.

5. 연결 된 후에 추가 R 패키지 또는 선호 하는 개발 도구를 설치할 수 있습니다.

### <a name="install-additional-r-tools"></a>추가 R 도구를 설치 합니다.

기본적으로 Microsoft R Server에는 RTerm 및 RGui 등 기본 R 설치를 통해 설치된 모든 R 도구가 포함됩니다. 또한 관리자 권한 바로 가기는 바탕 화면에 추가 되었습니다.

RStudio, R Tools for Visual Studio (RTVS) 또는 Microsoft R Client 등의 추가 R 도구를 설치 하려면 백업본 수도 있습니다. 다운로드 위치 및 지침은 다음 링크를 참조하세요.

+ [R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)
+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [Windows용 RStudio](https://www.rstudio.com/products/rstudio/download/)

설치가 완료된 후 모든 R 개발 도구에 Microsoft R Server 라이브러리가 사용되도록 기본 R 런타임 위치를 변경해야 합니다.

### <a name="configure-r-server-to-support-web-services"></a>R 서버 웹 서비스를 지원 하도록 구성

추가 구성은 웹 서비스 배포 시 원격 실행을 사용 하거나 R Server를 활용 하 여 조직에 배포 서버로 하려면 필요 합니다. 자세한 내용은 [분석을 운용 하려면 R 서버 구성](https://docs.microsoft.com/machine-learning-server/install/operationalize-r-server-one-box-config)합니다.

> [!NOTE]
> RevoScaleR 또는 MicrosoftML 같은 패키지를 사용 하려는 경우에 추가 구성이 필요 하지 않습니다.

## <a name="other-virtual-machines"></a>다른 가상 컴퓨터

다음 그림은 Azure 마켓플레이스에서 사용할 수 있는 등과 완전히 구성 된 기계 학습 도구 하지만 반드시 SQL Server를 포함 하지 마십시오.

### <a name="data-science-virtual-machine"></a>데이터 과학 가상 컴퓨터

이 이미지는 Microsoft R Server 뿐만 아니라 Python (Anaconda 배포), Jupyter 노트북 서버, Visual Studio Community Edition, Power BI Desktop, Azure SDK 및 SQL Server Express edition와 미리 구성 합니다.

Windows 버전 Windows Server 2012에서 실행 되 고 모델링 및 분석을 포함 하 여 많은 특별 한 도구가 포함 되어 [CNTK](https://www.microsoft.com/cognitive-toolkit/), [mxNet](https://mxnet.incubator.apache.org/), 인기 있는 R 패키지와 같은 고 **xgboost**.

Linux 버전 Ubuntu, Centos 및 Centos CSP에 대 한 제공 및 데이터 과학 및 개발 작업에 대 한 인기 있는 여러 도구를 포함 합니다.

자세한 내용은 참조 [소개 Azure 데이터 과학 가상 컴퓨터에 Linux 및 Windows 용](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/provision-vm)합니다.

최근에이 이미지를 포함 하도록 업데이트 되었습니다. 

+ Julia 앞으로의 확장 가능 하 고 강력한 데이터 과학 언어에 대 한 지원 
+ JupyterHub 교육 과정을 실행 하 고 동일한 서버를 공유 하지만 개별 전자 필기장 및 디렉터리를 사용 하 여 모든 학생 원하는 하려는 경우 유용한 옵션입니다.

지원 되는 도구 및 컴퓨터 학습 프레임 워크에 대 한 자세한 내용은 참조 [데이터 과학 가상 컴퓨터 알아보기](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/dsvm-tools-overview)

### <a name="r-server-virtual-machines"></a>R 서버 가상 컴퓨터

이외에 **R 서버만 SQL Server 2016 Enterprise** 이미지 R Server가 포함 된 독립 실행형 가상 컴퓨터를 가져올 수 있습니다. 이미지는 Linux CentOS 버전 7.2, Linux RedHat 버전 7.2, 및 16.04 Ubuntu 버전에 사용할 수 있습니다.

자세한 내용은 참조 [클라우드에서 학습 서버 컴퓨터](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-in-the-cloud)

 > [!NOTE]
 > 이러한 가상 컴퓨터는 이전에 Azure Marketplace에서 사용할 수 있었던 **Windows 가상 컴퓨터용 RRE**를 대체합니다.

### <a name="sql-server-virtual-machines"></a>SQL Server 가상 컴퓨터

Azure에서 학습 하는 SQL Server 컴퓨터를 사용 하기 위한 두 가지가 있습니다.

+ 사전 설치 된 SQL Server R Services를 포함 하는 가상 컴퓨터 이미지 중 하나를 가져옵니다.
+ Azure 가상 컴퓨터를 만들고 사용자 고유의 라이선스 키를 사용 하 여 SQL Server Enterprise 또는 Developer 버전을 설치 합니다. 
  
    그런 다음 다시 추가 하 고 여기에 설명 된 대로 기계 학습 서비스를 활성화 하려면 설치 프로그램을 실행: [Azure 가상 컴퓨터에서 SQL Server R Services 설치](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)합니다.
+ 기계 학습을 지원 하 고 미리 보기에서 새 R 서비스 기능을 현재 사용할 수 있는 서비스 계층을 사용 하 여 Azure SQL 데이터베이스를 만듭니다. 자세한 내용은 참조 [Azure SQL DB](../r/using-r-in-azure-sql-database.md)합니다.

> [!NOTE]
> 현재, SQL Server 컴퓨터 학습 서비스는 SQL Server 2017에 대 한 Linux 가상 컴퓨터에서 지원 되지 않습니다. 그러나 T-SQL 예측 함수를 사용 하 여 학습된 된 모델에서 점수 매기기를 수행할 수 있습니다. 자세한 내용은 참조 [SQl Server의 기본 점수 매기기](../sql-native-scoring.md)합니다. 

### <a name="virtual-machines-for-deep-learning"></a>심층 학습을 위한 가상 컴퓨터 

이전에 Microsoft에서 제공 하는 전체 학습 도구 키트에 대 한 데이터 과학 가상 컴퓨터를 기존 데이터 과학 가상 컴퓨터에 추가 될 수 있습니다. 이 도구 키트는 지금 인기 있는 심층 학습 도구를 포함 하는 전체 학습 가상 컴퓨터로 대체 됩니다.

+ Microsoft Cognitive Toolkit, TensorFlow, Keras, 및 Caffe 심층 학습 프레임 워크의 GPU 버전 등의
+ 기본 제공 GPU 드라이버
+ 이미지 및 텍스트 처리를 위한 도구 모음
+ Enterprise와 같은 개발 도구 Microsoft R Server Developer Edition, Anaconda Python, Python 및 R에 대 한 Jupyter 노트북
+ Python, R, SQL Server, 등에 대 한 개발 도구
+ 이미지 및 텍스트 이해에 대 한 종단 간 예제

심층 학습 가상 컴퓨터가 Windows 2016 또는 Ubuntu Linux 플랫폼에 사용할 수 있습니다. 자세한 내용은 참조 [심층 학습 및 AI 프레임 워크](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/dsvm-deep-learning-ai-frameworks)합니다.

> [!IMPORTANT]
> 
> 이 가상 컴퓨터를 배포 하려면 제한 된 Azure 지역에서 사용할 수 있는 Azure GPU NC 시리즈 가상 컴퓨터 이미지 합니다. 가용성에 대 한 정보를 참조 하십시오. [지역에 따라 사용할 수 있는 제품](https://azure.microsoft.com/en-us/regions/services/)합니다. 가상 컴퓨터를 프로 비전 할 때 사용 해야 **HDD** 디스크 유형으로 되지 **SSD**합니다.

## <a name="frequently-asked-questions"></a>질문과 대답

이 섹션에서는 기계 학습에서 Microsoft 가상 컴퓨터에 대 한 몇 가지 일반적인 질문 합니다.

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>SQL Server 2017와 가상 컴퓨터를 설치할 수 있습니까?

컴퓨터 학습 서비스를 포함 하는 SQL Server 2017 Enterprise Edition에 대 한 Windows 기반 가상 컴퓨터를 곧 사용할 수 있습니다. 이러한 블로그 사이트에서의 알림을 찾습니다.

+ [Cortana 인텔리전스 및 기계 학습](https://blogs.technet.microsoft.com/machinelearning/)
+ [Data Platform Insider](https://blogs.technet.microsoft.com/dataplatforminsider/)

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>Azure Storage 계정의 데이터에 어떻게 액세스하나요?

Azure Storage 계정에서 데이터를 사용해야 할 때 데이터에 액세스하거나 데이터를 이동하는 데 필요한 몇 가지 옵션이 있습니다.

+ [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)와 같은 유틸리티를 사용하여 저장소 계정에서 로컬 파일 시스템으로 데이터를 복사합니다. 

+ 저장소 계정에서 파일 공유에 파일을 추가하고 VM에 파일 공유를 네트워크 드라이브로 탑재합니다.  자세한 내용은 [Mounting Azure files](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/)(Azure 파일 탑재)를 참조하세요. 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>ADLS(Azure Data Lake Storage)의 데이터를 어떻게 사용하나요?

WebHDFS를 사용 하 여 동일한는 HDFS 하듯이 파일 시스템, 저장소 계정을 참조 하는 경우, RevoScaleR을 사용 하 여 ADLS 저장소에서 데이터를 읽을 수 있습니다.  자세한 내용은이 문서를 참조 하십시오.: [Azure 데이터 레이크 저장소의 파일 시스템 작업을 수행할 수를 사용 하 여 R](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/)합니다.



