---
title: "Azure 기계 학습에 대 한 가상 컴퓨터를 프로 비전 | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 781622d51b7112d3a501652b7c320ab27e74ae35
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2018
---
# <a name="provision-a-virtual-machine-for-machine-learning-on-azure"></a>Azure 기계 학습에 대 한 가상 컴퓨터를 프로 비전

Azure에서 가상 컴퓨터는 기계 학습 솔루션에 대 한 전체 서버 환경을 신속 하 게 구성 하는 데 편리한 옵션입니다.

이 문서에서는 기계 학습, 뿐 아니라 몇 가지 관련된 Vm에 SQL Server가 포함 된 가상 컴퓨터 이미지를 나열 합니다.

또한이 문서에는 수정 하거나 가상 컴퓨터에서 기존 SQL Server 인스턴스를 업그레이드 하는 방법에 대 한 일반적인 질문과 대답을 제공 합니다.

+ [현재 가상 컴퓨터의 목록](#bkmk_list)

## <a name="provision-a-virtual-machine-with-sql-server-and-machine-learning"></a>SQL Server와 함께 가상 컴퓨터를 프로 비전 하 고 기계 학습

Azure Vm을 사용 하 여 처음 하려는 경우에 포털을 사용 하 고 가상 컴퓨터를 구성 하는 방법에 대 한 자세한 내용은 다음이 문서를 참조 하는 것이 좋습니다.

+ [가상 컴퓨터-시작](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [Windows 가상 컴퓨터를 시작 하기](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/)

새 버전의 Azure 포털 또는 Azure Marketplace를 사용 해야 합니다. 클래식 포털에서 Azure 갤러리를 검색할 때 일부 이미지를 사용할 수 없는 경우

**가상 컴퓨터 만들기**

1. Azure 포털을 열고: [portal.azure.com](https:portal.azure.com)합니다.

2. 클릭 **가상 컴퓨터**, 하거나 클릭 **새로**합니다.

3. **추가**를 클릭합니다.

4. 페이지 맨 위에 있는 검색 상자에 관련 된 가상 컴퓨터의 목록을 보려면 "Server 학습 컴퓨터" 또는 "SQL Server"를 입력 합니다.

5. 요구 사항을 검토 하 고 클릭 **만들기** 를 시작 합니다.

6. 만든 가상 컴퓨터를 실행 중인 후 클릭는 **연결** 단추에 대 한 연결을 열고 새 컴퓨터에 로그인 합니다.

5. 연결 된 후 추가 Python 또는 R 패키지를 설치할 수도 있고 선호 하는 개발 도구를 구성할 수 있습니다.

### <a name="connect-to-the-virtual-machine"></a>가상 컴퓨터에 연결

클라이언트가 가상 컴퓨터에서 실행 중인 SQL Server에 연결 하는 방법은 클라이언트 및 네트워킹 구성의 위치에 따라 달라 집니다.

자세한 내용은 참조 [Azure에서 SQL Server 가상 컴퓨터에 연결](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-connect)합니다.

## <a name="frequently-asked-questions"></a>질문과 대답

이 섹션에서는 기계 학습에서 Microsoft 가상 컴퓨터에 대 한 몇 가지 일반적인 질문 합니다.

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>SQL Server 2017와 가상 컴퓨터를 설치할 수 있습니까?

컴퓨터 학습 서비스를 포함 하는 SQL Server 2017 Enterprise Edition에 대 한 Windows 기반 가상 컴퓨터는 2017 년 11 월 버전부터 사용 가능 합니다. 

새 데이터 과학 가상 컴퓨터에 대 한 공지 사항에 대 한이 블로그 사이트 보기:

+ [Cortana 인텔리전스 및 기계 학습](https://blogs.technet.microsoft.com/machinelearning/)
+ [Data Platform Insider](https://blogs.technet.microsoft.com/dataplatforminsider/)

### <a name="adding-sql-server-to-an-existing-virtual-machine"></a>기존 가상 컴퓨터에 SQL Server 추가

가상 컴퓨터를 만들 뿐만 아니라 SQL Server 기계 학습, 기존 가상 컴퓨터에 SQL Server를 설치 하 고 사용 하는 기능을 학습 하는 컴퓨터 수를 이미 포함 된 이미지를 사용 하 여 합니다. 리소스 제약을 방지 하기 위해 Enterprise 또는 Developer 버전을 사용 하는 것이 좋습니다. 설치에서는 라이센스 키를 사용 해야 합니다.

설치 프로그램을 실행 하는 경우에 기계 학습 기능 및 (R 또는 Python)는 하나 이상의 언어를 선택 해야 합니다. 몇 가지 추가 단계는 SQL Server와 통신 하 고 가상 컴퓨터에서 네트워킹을 사용 하려면 컴퓨터 학습 서비스를 사용 하도록 설정 해야 합니다.

자세한 내용은 참조 [Azure 가상 컴퓨터에서 SQL Server R Services 설치](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)합니다.

### <a name="using-machine-learning-in-azure-sql-database"></a>기계 학습을 사용 하 여 Azure SQL 데이터베이스에서

현재 Azure SQL에서는 R 지원의 미리 보기는 개발 작업에 대 한 일시 중단 됩니다. 자세한 내용은 참조 [Azure SQL DB](../r/using-r-in-azure-sql-database.md)합니다.

### <a name="can-i-upgrade-the-sql-server-version-on-a-virtual-machine"></a>가상 컴퓨터에서 SQL Server 버전을 업그레이드할 수 있습니까?

SQL Server 2016 이미지를 지원 하지만 R, Python을 사용 하려는 경우에 다른 기계 학습 구성 요소를 업그레이드 하는 SQL Server 2017 년으로 업그레이드할 수 있습니다.

설치 된 SQL Server의 버전을 업데이트 하려면 가상 컴퓨터에서 SQL Server 설치 센터를 열고을 선택 된 **업그레이드** 옵션입니다. 가상 컴퓨터에 따라 사용자가 만든, 라이선스가 필요할 수 있습니다.

자세한 내용은 참조 [설치 마법사를 사용 하 여 SQL Server 업그레이드](https://docs.microsoft.com/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup)합니다.

### <a name="can-i-upgrade-just-the-machine-learning-components"></a>방금 기계 학습 구성 요소를 업그레이드할 수 있습니까?

새 업그레이드 RevoScaleR, MicrosoftML, 또는 revoscalepy 게시 되 면 기계 학습 이라는 프로세스를 사용 하 여 SQL Server에서 사용 하는 구성 요소를 업그레이드할 수 있습니다 _바인딩_합니다. 이 SQL Server 버전 바뀌지 않지만 인스턴스에 대 한 지원 정책 변경지 않습니다.

자세한 내용은 참조 [컴퓨터 학습 구성 요소를 SQL Server에서 업그레이드를 사용 하 여 SqlBindR](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>Azure Storage 계정의 데이터에 어떻게 액세스하나요?

Azure Storage 계정에서 데이터를 사용해야 할 때 데이터에 액세스하거나 데이터를 이동하는 데 필요한 몇 가지 옵션이 있습니다.

+ [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only)와 같은 유틸리티를 사용하여 저장소 계정에서 로컬 파일 시스템으로 데이터를 복사합니다. 

+ 저장소 계정에서 파일 공유에 파일을 추가하고 VM에 파일 공유를 네트워크 드라이브로 탑재합니다. 자세한 내용은 [Mounting Azure files](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/)(Azure 파일 탑재)를 참조하세요. 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>ADLS(Azure Data Lake Storage)의 데이터를 어떻게 사용하나요?

RevoScaleR을 사용 하 여 webHDFS를 사용 하 여 동일한는 HDFS 하듯이 파일 시스템 저장소 계정을 참조 하 여 ADLS 저장소에서 데이터를 읽을 수 있습니다. 자세한 내용은이 문서를 참조 하십시오.: [Azure 데이터 레이크 저장소의 파일 시스템 작업을 수행할 수를 사용 하 여 R](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/)합니다.

### <a name="i-cant-find-the-rre-virtual-machine"></a>RRE 가상 컴퓨터를 찾을 수 없습니다.

이전에 제공 했던 "RRE에 대 한 Windows 가상 컴퓨터의" Azure 마켓플레이스 이미지 "컴퓨터 학습 서버에 대 한 Windows"로 대체 되었습니다.

컴퓨터 학습 서버 이미지 Linux CentOS 버전 7.2, Linux RedHat 버전 7.2, 및 16.04 Ubuntu 버전에 대해 사용할 수 있습니다.

자세한 내용은 참조 [클라우드에서 학습 서버 컴퓨터](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-in-the-cloud)

### <a name="configuring-machine-learning-server-or-r-server-to-support-web-services"></a>웹 서비스를 지원 하도록 서버를 학습 하는 컴퓨터 또는 R 서버 구성

서버를 학습 하는 컴퓨터를 포함 하는 가상 컴퓨터를 사용 하는 경우에 추가 구성이 웹 서비스 배포 시 원격 실행을 사용 하거나 조직에 배포 서버로 가상 컴퓨터를 사용 하려면 필요할 수 있습니다.

자세한 내용은 [분석을 운용 하려면 컴퓨터 학습 서버 구성](https://docs.microsoft.com/machine-learning-server/operationalize/configure-machine-learning-server-one-box)합니다.

RevoScaleR 또는 MicrosoftML 같은 패키지를 사용 하려는 경우에 추가 구성이 필요 하지 않습니다.

## <a name="bkmk_list"></a>가상 컴퓨터의 목록

현재 가상 컴퓨터는 SQL Server와 함께 기계 학습에 사용할 수 있습니다.

|이름| 설명|
|----|----|----|
| **SQL Server 2016**| ***  |
|Windows에서 SQL Server 2016 SP1 Enterprise|통합된 고급 분석을 위해 R 서비스입니다.|
|Windows Server에서 BYOL SQL Server 2016 SP1 Enterprise |통합된 고급 분석을 위해 R 서비스입니다. |
|Windows Server 2016에서 SQL Server 2016 SP1 Developer 무료 라이선스: |통합된 고급 분석을 위해 R 서비스입니다. |
| 데이터 과학 가상 컴퓨터-Windows 2012|Microsoft R Server Developer Edition, SQL Server 2016 Developer edition, Anaconda Python 배포, Julia Pro developer edition 및 Jupyter 노트북을 포함 하 여 r 되는 데이터 과학을 위한 인기 있는 도구를 포함 합니다.| 
| 데이터 과학 가상 컴퓨터-Windows 2016|데이터베이스에서 R 분석에 대 한 지원과 함께 SQL Server 2016 Developer Edition을 포함합니다.|
|**SQL Server 2017**| ***   |
|SQL Server 2017 Enterprise Windows Server 2016| 컴퓨터 학습 Python과 R 언어를 지 원하는 서비스입니다.|
|BYOL SQL Server 2017 Enterprise Windows Server 2016|컴퓨터 학습 Python과 R 언어를 지 원하는 서비스입니다.|
| Windows Server에서 사용 가능한 SQL Server 라이선스: SQL Server 2017 Developer|컴퓨터 학습 Python과 R 언어를 지 원하는 서비스입니다.|
| **기타**| *** |
| 기계 학습 서버 SQL Server 2017 Enterprise|SQL Server 2016 Enterprise 이미지와 마찬가지로 하지만 학습 서버 컴퓨터의 독립 실행형 버전을 포함 ScaleR 코어 하 고 Windows 용으로 최적화 해결해줍니다 기능 환경입니다.|
| Windows 용 기계 학습 서버|Windows 환경에 최적화 된 해결해줍니다 기능으로 컴퓨터 학습 서버의 독립 실행형 버전을 포함 합니다.|
|데이터 과학 가상 컴퓨터 |Linux 버전 R Server에 포함 되어 있습니다. SQL Server 2017을 포함 하는 Linux 가상 컴퓨터는 SQL Server의 R, Python 코드를 실행할 수 없습니다. 그러나 T-SQL 예측 함수를 사용 하 여 학습된 된 모델에서 점수 매기기를 수행할 수 있습니다. 자세한 내용은 참조 [SQl Server의 기본 점수 매기기](../sql-native-scoring.md)합니다.|
