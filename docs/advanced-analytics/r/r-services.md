---
title: "Microsoft 컴퓨터 학습 서비스 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 341e80f5-3b59-4122-bbaa-969d7904297d
caps.latest.revision: 23
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 246ea9f306c7d99b835c933c9feec695850a861b
ms.openlocfilehash: ddc9b3f17afe1f9d4c811e4a5871f48a3a08de7f
ms.contentlocale: ko-kr
ms.lasthandoff: 10/13/2017

---
# <a name="microsoft-machine-learning-services"></a>Microsoft 기계 학습 서비스

Microsoft 컴퓨터 학습 서비스 목표 기계 학습 작업 및 도구 컴퓨터 학습 서비스를 사용 하는 응용 프로그램과 통합 하기 위한 확장 가능 하 고 확장 가능한 플랫폼을 제공 하는 것입니다. 플랫폼 제공 해야 모든 사용자의 요구 사항을 데이터 개발 및 분석 프로세스에 관련 된 데이터 과학자에서 설계자와 데이터베이스 관리자에 게 합니다.

주요 이점은 다음과 같습니다.

+ 확장 가능한 분석
+ 여러 플랫폼 및 "한 번 작성, 배포 원하는 위치 에" 솔루션에 대 한 계산 컨텍스트
+ 데이터를 분석 하 여 데이터 이동 및 데이터 위험을 방지
+ 데이터 과학자가 자신의 도구 및 언어를 선택할 수 있습니다.
+ Microsoft의 엔터프라이즈 기능와 오픈 소스의 가장 유용한 기능 통합
+ 간편한 관리
+ 쉽게 배포 하 고 예측 모델을 사용할 수

## <a name="in-database-analytics-with-sql-server"></a>SQL Server로 데이터베이스에서 분석

SQL Server 2016 Microsoft 인기 있는 오픈 소스 R 언어를 비즈니스 응용 프로그램과 통합 하기 위한 두 개의 서버 플랫폼을 시작 합니다.

+ **SQL Server R Services(In-Database)**에 통합하기 위해, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
+ **Microsoft R Server**, Windows 및 Linux 서버에 배포 하는 엔터프라이즈 수준의 R에 대 한

SQL Server 2017 이름 인기 있는 Python 언어에 대 한 지원이 반영 되도록 변경 되었습니다.

+ **SQL Server 컴퓨터 학습 Services (In-database)** 데이터베이스에서 분석에 대 한 R 및 Python 모두를 지원 합니다.
+ **서버를 Microsoft 컴퓨터 학습** 런타임에 2017에 대 한 계획 된 다른 지원 되는 플랫폼에 대 한 확장 된 Windows 서버에서 R 및 Python 배포를 지원 합니다.

### <a name="benefits"></a>이점

Microsoft 컴퓨터 학습 서비스는 데이터베이스와 동일한 컴퓨터에서 실행을 허용 하 여 데이터를 compute를 제공 합니다. 외부에서 실행 하는 신뢰할 수 있는 실행 패드 서비스에 포함 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 처리 하 고 Python 또는 R 런타임과 안전 하 게 통신 합니다.

SQL Server 컴퓨터 학습 서비스를 사용 하 여 모델을 학습, 플롯을 생성, 상태 평가 수행 하 고 쉽게 이동할 수 사이 데이터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R, Python 및 합니다.

테스트 및 솔루션을 개발 하는 데이터 과학자는 서버에 안전 하 게 코드를 실행 하는 원격 개발 컴퓨터에서 스크립트를 보낼 수 또는 컴퓨터 학습 코드 SQL 저장 프로시저에 포함 하 여 SQL Server에 완성 된 솔루션을 배포할 수 있습니다.

SQL Server에 대 한 기계 학습을 설치 하면 오픈 소스 R 또는 Python 언어 뿐만 아니라 Microsoft에서 제공 하는 확장 가능한 R 및 Python 라이브러리의 분포를 가져옵니다. 또한 SQL Server 데이터베이스 엔진 연결을 강화 하 고 더 빨라지고, Python 또는 R 등의 외부 언어와의 보다 안전한 통신을 확인 하도록 설계 된 새 구성 요소를 포함 합니다.

### <a name="where-to-get-it"></a>가져올 위치

시작 하려면 다음이 리소스를 참조 합니다.

+ [SQL Server R Services](sql-server-r-services.md)
+ [SQL Server Python 서비스](../python/sql-server-python-services.md)
+ [기계 학습 자습서](../tutorials/machine-learning-services-tutorials.md)

> [!NOTE]
> Python에 대 한 지원이 SQL Server 2017 으로만 제공 됩니다. 

## <a name="machine-learning-server-standalone-and-microsoft-r-server-standalone"></a>기계 학습 Server (독립 실행형) 및 Microsoft R Server (독립 실행형)

이 독립 실행형 서버 시스템 여러 플랫폼 및 Linux 등 HD Insight의 여러 엔터프라이즈 데이터 원본 사용에 분산 하 고 확장 가능한 R 솔루션을 지원 합니다. SQL Server와 통합에 필요 하지 않으면를 신속 하 게 개발, 배포 및 기계 학습 솔루션의 해결해줍니다 사용할 수 있도록 R Server를 설치할 수 있습니다. SQL Server 인스턴스와 연결 된 R 구성 요소를 업그레이드 하는 최신 버전은 R입니다. R 서버 설치 관리자를 사용할 수도 있습니다.

SQL Server 2017 설치 프로그램을 사용 하 여 Microsoft 컴퓨터를 학습 하는 서버를 설치 하는 경우 배포 수 및 Python 응용 프로그램을 사용 해야 합니다.

자세한 내용은 참조 [Microsoft 컴퓨터 학습 서버](https://docs.microsoft.com/r-server/index)합니다.

## <a name="related-technologies"></a>관련된 기술

Microsoft는 도구, 공급자, 고급 R 및 Python 패키지, 클라우드 개발 및 서비스 플랫폼, 통합된 개발 환경 등 컴퓨터 학습 에코 시스템에 대 한 광범위 한 지원을 제공 합니다.

### <a name="r-tools-for-visual-studio"></a>R Tools for Visual Studio

Visual Studio에서는 R 언어에 대한 완전한 개발 환경을 제공합니다. 편집기, 대화형 창, 그리기, 디버거를 비롯한 많은 플러그인을 포함합니다. R.NET 및 rClr 등의 오픈 소스 라이브러리를 통해 .NET에서 R을 호출하거나 R에서 .NET 언어를 사용할 수 있습니다.

Visual Studio에는 뛰어난 Python 개발 환경입니다. SQL 데이터베이스 개발 도구에 대 한 액세스를 활용 하면서 컴퓨터 학습 언어를 사용 하는 보다 쉽게 방식은 없습니다.

참조 항목:

+ [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)
+ [Python-Visual Studio](https://www.visualstudio.com/vs/python/)

### <a name="azure-machine-learning"></a>Azure 기계 학습

Azure 기계 학습 스튜디오에 사용자의 작업 영역을 만들 때 미리 400 개 이상의 R 패키지에 대 한 액세스를 해야 합니다. 표준 CRAN R 배포 또는 Microsoft R Open을 사용 하 여 R을 배포 하기 위해 R을 사용 하는 실험을 만들 때 선택할 수 있습니다. 도 자신만 R 패키지 만들고 사용자 지정 모듈로 실행 하는 Azure에 업로드할 수 있습니다.

자세한 내용은 다음 리소스를 참조하십시오.

+ [R을 사용하여 실험 확장](https://docs.microsoft.com/azure/machine-learning/machine-learning-extend-your-experiment-with-r)
+ [Azure 기계 학습에서 사용자 지정 R 모듈 작성자](https://docs.microsoft.com/azure/machine-learning/machine-learning-custom-r-modules)

대부분의 Azure ML에서 제공 하는 알고리즘은 이제 MicrosoftML 패키지의 일부로 Microsoft 컴퓨터 학습 서비스에 포함 됩니다. 자세한 내용은 참조 [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)합니다.

Azure 기계 학습은 데이터 과학자 및 작성, 학습 및 웹 서비스를 사용 하 여 모델을 배포 하는 개발자에 대 한 다른 편리한 플랫폼입니다. 에 대 한 솔루션을 게시할 수 있습니다는 [Machine Learning Marketplace](http://datamarket.azure.com/browse/data?category=machine-learning)합니다.

### <a name="data-science-virtual-machines"></a>데이터 과학 가상 컴퓨터

Microsoft Azure에 사전 설치 및 구성된 [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] 버전을 배포하면, 온-프레미스에 완벽하게 구성된 시스템을 설정하지 않고도 클라우드에서 데이터 탐색과 모델링을 손쉽게 바로 시작할 수 있습니다.

Azure Marketplace에는 데이터 과학을 지원하는 여러 가상 컴퓨터가 포함되어 있습니다.

+ **Microsoft 데이터 과학 가상 컴퓨터** 는 Python(Anaconda 배포), Jupyter 노트북 서버, Visual Studio Community Edition, Power BI Desktop, Azure SDK, SQL Server Express Edition 및 Microsoft R Server로 구성되어 있습니다.

+ **Linux용 Microsoft R Server 2016** 에는 최신 버전의 R 서버(버전 9.0.1)가 포함되어 있습니다. 별도 Vm CentOS 버전 7.2 및 Ubuntu 버전 16.04 수 있습니다.

+ **R 서버만 SQL Server 2016 Enterprise** 가상 컴퓨터에 새로운 최신 소프트웨어 수명 주기 라이선스 모델을 지 원하는 R 서버 9.0.1에 대 한 독립 실행형 설치 관리자에 포함 됩니다.

> [!TIP]
> 새 [데이터 과학 VM에 대 한 Windows Server 2016](http://aka.ms/dsvm/win2016) CNTK와 같은 인기 있는 심층 학습 프레임 워크의 GPU 버전을 제공 합니다. 사전 설치 된 도구는 GPU NVIDIA 드라이버, CUDA 도구 키트 8.0 및 NVIDIA cuDNN 라이브러리 GPU 작업을 위해 포함 됩니다. 몇 분만에 CPU 또는 CPU와 GPU에서 실행할 수 있는 심층 학습 모델을 작성 하기 위한 완벽 한 환경을 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

[컴퓨터 학습 서비스 시작](getting-started-with-sql-server-r-services.md)

[서버를 학습 하는 컴퓨터 시작](getting-started-with-microsoft-r-server-standalone.md)

[SQL Server 데이터베이스 엔진 설치](../../database-engine/install-windows/install-sql-server-database-engine.md)

