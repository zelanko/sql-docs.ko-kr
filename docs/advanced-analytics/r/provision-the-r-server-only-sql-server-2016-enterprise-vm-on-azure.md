---
title: "Azure에서 R Server 전용 SQL Server 2016 Enterprise VM에 프로비전 | Microsoft 문서"
ms.custom: 
ms.date: 06/05/2017
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3bfca0753984f09220d8ca4e4f6933c949daf2b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="advanced-analytics-virtual-machines-on-azure"></a>Azure에서 고급 분석 가상 컴퓨터

Azure에서 가상 컴퓨터는 기계 학습 솔루션에 대 한 전체 서버 환경을 신속 하 게 구성 하는 데 편리한 옵션입니다. 이 항목에서는 R 서버, 기계 학습을 사용한 SQL Server 또는 Microsoft의 다른 데이터 과학 도구를 포함 하는 일부 가상 컴퓨터 이미지를 나열 합니다.

> [!TIP]
> Azure 포털 및 Azure Marketplace의 새 버전을 사용 하는 것이 좋습니다. 클래식 포털에서 Azure 갤러리를 검색할 때 일부 이미지를 사용할 수 없는 경우

Azure 마켓플레이스 데이터 과학을 지 원하는 여러 가상 컴퓨터를 포함 합니다. 이 목록은 나와 있으며, Microsoft R Server 또는 SQL Server 컴퓨터 학습 검색을 용이 하 게 하려면 서비스를 포함 하는 이미지의 이름을 제공 하는 적합 하지 않습니다.

## <a name="how-to-provision-a-vm"></a>VM을 프로 비전 하는 방법

Azure Vm을 사용 하 여 처음 하려는 경우에 포털을 사용 하 고 가상 컴퓨터를 구성 하는 방법에 대 한 자세한 내용은 다음이 문서를 참조 하는 것이 좋습니다.

+ [가상 컴퓨터-시작](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [Windows 가상 컴퓨터 시작](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-hero-tutorial/)

### <a name="find-an-image"></a>이미지 찾기

1. Azure 대시보드에서 클릭 **마켓플레이스**합니다.

    - 클릭 **인텔리전스 및 분석** 또는 **데이터베이스**, 다음에 "R"을 입력 하 고는 **필터** R Server 가상 컴퓨터의 목록을 보려면 제어 합니다.
    - 다른 가능한에 대 한 문자열의 **필터** 제어 *데이터 과학* 및 *기계 학습*
    - 검색에서 % 와일드 카드를 사용 하 여와 같은 대상 문자열을 포함 하는 VM 이름을 찾으려면 *R* 또는 *Julia*합니다.

2. Windows 용 R 서버를 가져오려면 선택 **R 서버만 SQL Server 2016 Enterprise**합니다.
  
    [R 서버](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) 는 SQL Server Enterprise Edition 기능을 사용 하지만 버전 9.1으로 사용이 허가 됩니다. 독립 실행형 서버로 설치 되 고 최신 수명 주기 지원 정책에 따라 서비스를 제공 합니다.

3. VM을 만들고 실행한 후에는 **연결** 단추를 클릭하여 연결 상자를 열어 새 컴퓨터에 로그인합니다.

4. 연결 된 후 추가 R 도구 또는 개발 도구를 설치 해야 합니다.

### <a name="install-additional-r-tools"></a>추가 R 도구를 설치 합니다.

기본적으로 Microsoft R Server에는 RTerm 및 RGui 등 기본 R 설치를 통해 설치된 모든 R 도구가 포함됩니다. R를 사용하여 지금 바로 시작하려는 경우 RGui 바로 가기가 바탕 화면에 추가되어 있습니다.

RStudio, Visual Studio (RTVS) 또는 Microsoft R Client에 대 한 R 도구와 같은 추가 R 도구를 설치 하려면 백업본 수도 있습니다. 다운로드 위치 및 지침은 다음 링크를 참조하세요.
+ [R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)
+ [Microsoft R Client](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [Windows용 RStudio](https://www.rstudio.com/products/rstudio/download/)

설치가 완료된 후 모든 R 개발 도구에 Microsoft R Server 라이브러리가 사용되도록 기본 R 런타임 위치를 변경해야 합니다.

### <a name="configure-server-for-web-services"></a>웹 서비스에 대 한 서버 구성

가상 컴퓨터에 R Server가 포함된 경우 웹 서비스 배포, 원격 실행을 사용하거나 조직에서 R Server를 배포 서버로 사용하려면 추가 구성이 필요합니다. 자세한 내용은 [Configure R Server for Operationalization](https://msdn.microsoft.com/microsoft-r/operationalize/configuration-initial)(운영화를 위한 R Server 구성)을 참조하세요.

> [!NOTE]
> RevoScaleR 또는 MicrosoftML 같은 패키지를 사용 하려는 경우에 추가 구성이 필요 하지 않습니다.

## <a name="r-server-images"></a>R 서버 이미지

### <a name="microsoft-data-science-virtual-machine"></a>Microsoft 데이터 과학 가상 컴퓨터

Microsoft R 서버 뿐만 아니라 Python (Anaconda 배포), Jupyter 노트북 서버, Visual Studio Community Edition, Power BI Desktop, Azure SDK 및 SQL Server Express edition으로 구성 되어 제공 됩니다.

Windows 버전 Windows Server 2012에서 실행 되며 모델링 및 분석을 CNTK 및 mxnet, xgboost, 및 Vowpal Wabbit 같은 인기 있는 R 패키지가 포함 하는 많은 특별 한 도구가 있습니다.

### <a name="linux-data-science-virtual-machine"></a>Linux 데이터 과학 가상 컴퓨터

또한 Python, R 및 Julia에 대 한 Microsoft R Open, Microsoft R Server Developer Edition, Anaconda Python 및 Jupyter 노트북을 포함 하 여 데이터 과학 및 개발 작업을 위한 인기 있는 도구를 포함 합니다.

이 VM 이미지를 최근에 JupyterHub, 오픈 소스 소프트웨어를 로컬 운영 체제 계정 인증 및 Github 계정 인증을 포함 하는 서로 다른 인증 방법을 통해 여러 사용자가 사용할 수 있도록 포함 하도록 업데이트 됩니다. JupyterHub는 교육 과정을 실행 하 고 동일한 서버를 공유 하지만 개별 전자 필기장 및 디렉터리를 사용 하 여 모든 학생 원하는 하려는 경우 특히 유용한 옵션입니다.

Ubuntu, Centos 및 Centos CSP에 대 한 이미지 제공 됩니다.

### <a name="r-server-only-sql-server-2016-enterprise"></a>R 서버 SQL Server 2016 Enterprise

이 가상 컴퓨터에 대 한 독립 실행형 설치 관리자 포함 [R 서버 9.1 합니다.](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) 지 원하는 새로운 최신 소프트웨어 수명 주기 라이선스 모델입니다.

 R 서버 Linux CentOS 버전 7.2, Linux RedHat 버전 7.2, 및 16.04 Ubuntu 버전에 대 한 이미지에서 제공 됩니다.

 > [!NOTE]
 > 이러한 가상 컴퓨터는 이전에 Azure Marketplace에서 사용할 수 있었던 **Windows 가상 컴퓨터용 RRE**를 대체합니다.

## <a name="sql-server-images"></a>SQL Server 이미지

R Services (In-database) 또는 컴퓨터 학습 서비스를 사용 하려면 SQL Server Enterprise 또는 Developer edition 가상 컴퓨터 중 하나를 설치 및 여기에 설명 된 대로 기계 학습 서비스를 추가 해야 합니다: [Installing SQL Server R Services에는 Azure 가상 컴퓨터](../../advanced-analytics/r-services/installing-sql-server-r-services-on-an-azure-virtual-machine.md)합니다.

> [!NOTE]
> 현재 Azure SQL 데이터베이스 또는 SQL Server 2017 년에 대 한 컴퓨터 학습 서비스 Linux 가상 컴퓨터에서 지원 되지 않습니다. Windows 용 SQL Server 2016 SP1 또는 SQL Server 2017 중 하나를 사용 해야 합니다.

R 서비스 기능이 이미 활성화 된 SQL Server 2016 데이터 과학 가상 컴퓨터 포함 됩니다.


## <a name="other-vms"></a>다른 Vm

### <a name="deep-learning-toolkit-for-the-data-science-virtual-machine"></a>세부적 데이터 과학 가상 컴퓨터에 대 한 도구 키트 학습

이 가상 컴퓨터에 동일한 기계 학습 도구 데이터 과학 가상 컴퓨터에서 사용할 수 있지만 mxnet, CNTK, TensorFlow, 및 Keras GPU 버전입니다. 이 이미지는 Azure GPU N 시리즈 인스턴스에만 사용할 수 있습니다. 

또한 심층 학습 도구 키트 학습 CIFAR 10 데이터베이스에서 이미지 인식 및 MNIST 데이터베이스에서 문자 인식 샘플을 포함 하 여 GPU를 사용 하는 솔루션 전체 샘플의 집합을 제공 합니다. GPU 인스턴스가 현재 미국 중남부, 미국 동부, 서 부 유럽 및 동남 아시아에서 제공 됩니다.

> [!IMPORTANT]
> GPU 인스턴스는 현재 미국 중남부에서만 사용할 수 있습니다.


## <a name="frequently-asked-questions"></a>질문과 대답

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>SQL Server 2017와 가상 컴퓨터를 설치할 수 있습니까?

이미지는 사용할 수 있는 포함 하는 SQL Server 2017 CTP 2.0 Linux 환경에 대 한 되지만 이러한 환경 컴퓨터 학습 서비스를 현재 지원 하지 않습니다. 

컴퓨터 학습 서비스를 포함 하는 SQL Server 2017 Enterprise Edition에 대 한 Windows 기반 가상 컴퓨터 공용 릴리스 이후 제공 됩니다. 

대신 SQL Server 2016 이미지를 사용 하 고 여기에 설명 된 대로 R의 인스턴스를 업그레이드할 수 있습니다: [SqlBindR를 사용 하 여 인스턴스를 업그레이드](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다. 

또는 가상 컴퓨터를 만들고의 CTP 2.0 preview 다운로드 [SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-2017)합니다.

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>Azure Storage 계정의 데이터에 어떻게 액세스하나요?

Azure Storage 계정에서 데이터를 사용해야 할 때 데이터에 액세스하거나 데이터를 이동하는 데 필요한 몇 가지 옵션이 있습니다.

+ [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)와 같은 유틸리티를 사용하여 저장소 계정에서 로컬 파일 시스템으로 데이터를 복사합니다. 

+ 저장소 계정에서 파일 공유에 파일을 추가하고 VM에 파일 공유를 네트워크 드라이브로 탑재합니다.  자세한 내용은 [Mounting Azure files](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/)(Azure 파일 탑재)를 참조하세요. 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>ADLS(Azure Data Lake Storage)의 데이터를 어떻게 사용하나요?

WebHDFS를 사용 하 여 동일한는 HDFS 하듯이 파일 시스템, 저장소 계정을 참조 하는 경우, RevoScaleR을 사용 하 여 ADLS 저장소에서 데이터를 읽을 수 있습니다.  자세한 내용은이 문서를 참조 하십시오.: [Azure 데이터 레이크 저장소의 파일 시스템 작업을 수행할 수를 사용 하 여 R](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/)합니다.

## <a name="see-also"></a>관련 항목:

[SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)


