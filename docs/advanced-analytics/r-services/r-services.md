---
title: "R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/20/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 341e80f5-3b59-4122-bbaa-969d7904297d
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 20
---
# R Services
  Microsoft R Services는 인기 있는 오픈 소스 R 언어를 비즈니스 응용 프로그램 **SQL Server R Services(In-Database)**에 통합하기 위해, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 **Microsoft R Server** 통합을 위해 두 개의 서버 플랫폼을 제공합니다.  
  
-   **R Services(In-Database)**  
  
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 목표는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 플랫폼 및 관련 서비스를 기반으로 R 솔루션을 신속하게 개발, 배포 및 운용할 수 있도록 하는 것입니다.  
  
     [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]는 데이터베이스와 동일한 컴퓨터에서 R을 실행하여 데이터를 계산할 수 있도록 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스 외부에서 실행되고 R 런타임과 안전하게 통신하는 데이터베이스 서비스를 포함합니다. R 모델을 학습하고, R 플롯을 생성하고, 점수를 매기고, R과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간에 데이터를 쉽게 이동할 수 있습니다. 솔루션을 개발하고 테스트하는 데이터 과학자는 원격 개발 컴퓨터에서 서버와 통신하고 R 코드를 서버에서 실행하고 저장 프로시저에 R에 대한 호출을 포함하여 완성된 솔루션을 SQL Server에 배포할 수 있습니다.  
  
     이 다운로드에는 오픈 소스 R 언어 배포 외에 고성능의 확장 가능 R 패키지인 ScaleR이 포함되어 있습니다. 또한 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술을 통한 간편하고 신속한 연결을 위해 공급자를 포함합니다.  
  
     자세한 내용은 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)를 참조하세요. 샘플 시나리오는 [SQL Server R Services 자습서](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)를 참조하세요.  
  
-   **Microsoft R Server**  
  
     이 독립 실행형 서버 시스템은 다수의 플랫폼에서 확장 가능하고 분산된 R 솔루션을 지원하며 Linux, Hadoop, Teradata를 비롯한 다수의 엔터프라이즈 데이터 원본 사용을 지원합니다.  
  
     자세한 내용은 [Microsoft R Server(MSDN)](https://msdn.microsoft.com/microsoft-r/index)를 참조하세요.  
  
## <a name="related-technologies"></a>관련 기술  
 Microsoft는 오픈 소스 R 언어 에코시스템에 대해 도구, 공급자, 고급 R 패키지, 통합된 개발 환경을 비롯한 폭넓은 지원을 제공합니다.  
  
-   **R Tools for Visual Studio**  
  
     Visual Studio에서는 R 언어에 대한 완전한 개발 환경을 제공합니다. 편집기, 대화형 창, 그리기, 디버거를 비롯한 많은 플러그인을 포함합니다. R.NET 및 rClr 등의 오픈 소스 라이브러리를 통해 .NET에서 R을 호출하거나 R에서 .NET 언어를 사용할 수 있습니다.  
  
     자세한 내용은 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)를 참조하세요.  
  
-   **Azure Machine Learning의 R**  
  
     Azure 기계 학습 스튜디오에 사용자의 작업 영역을 만들면 미리 로드해 놓은 400개 이상의 R 패키지에 액세스할 수 있습니다. 웹 서비스로 배포하기 위해 모델을 구축하고 학습하거나 데이터를 변환하도록 사용자 지정 스크립트를 작성합니다. 자신만의 R 패키지를 만들고 Azure에 업로드하여 사용자 지정 모듈로 실행하고 [Machine Learning Marketplace](http://datamarket.azure.com/browse/data?category=machine-learning)(기계 학습 마켓플레이스)에 솔루션을 게시합니다.  
  
     자세한 내용은 [R을 사용하여 실험 확장](https://docs.microsoft.com/azure/machine-learning/machine-learning-extend-your-experiment-with-r) 및 [Azure Machine Learning에서 사용자 지정 R 모듈 작성](https://docs.microsoft.com/azure/machine-learning/machine-learning-custom-r-modules)을 참조하세요.  
  
-   **데이터 과학 가상 컴퓨터**  
  
     Microsoft Azure에 사전 설치 및 구성된 [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] 버전을 배포하면, 온-프레미스에 완벽하게 구성된 시스템을 설정하지 않고도 클라우드에서 데이터 탐색과 모델링을 손쉽게 바로 시작할 수 있습니다.  
  
     Azure Marketplace에는 데이터 과학을 지원하는 여러 가상 컴퓨터가 포함되어 있습니다.
     + **Microsoft 데이터 과학 가상 컴퓨터**는 Python(Anaconda 배포), Jupyter 노트북 서버, Visual Studio Community Edition, Power BI Desktop, Azure SDK, SQL Server Express Edition 및 Microsoft R Server로 구성되어 있습니다. 
     + **Linux용 Microsoft R Server 2016**에는 최신 버전의 R 서버(버전 9.0.1)가 포함되어 있습니다. CentOS 버전 7.2 및 Ubuntu 버전 16.04에 대해 별도 VM을 사용할 수 있습니다. 
     + **R 서버 전용 SQL Server 2016 Enterprise** 가상 컴퓨터에는 새 최신 소프트웨어 수명 주기 라이선스 모델을 지원하는 R Server 9.0.1의 독립 실행형 설치 관리자가 포함되어 있습니다.
 

## <a name="see-also"></a>관련 항목:  
[SQL Server R Services 시작](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md) 

[Microsoft R Server 시작](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  

 [SQL Server 데이터베이스 엔진 설치](../../database-engine/install-windows/install-sql-server-database-engine.md)  
  
  