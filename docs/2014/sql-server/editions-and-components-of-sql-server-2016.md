---
title: SQL Server 2014의 버전 및 구성 요소 Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- 32-bit vs. 64-bit editions [SQL Server]
- default components
- Workgroup Edition [SQL Server]
- Internet servers [SQL Server]
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- client/server applications [SQL Server]
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- 64-bit edition [SQL Server]
- IIS [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
ms.assetid: e5186f02-dd91-47d0-8fa4-de3f41c76903
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9610dc1cc729dc555d42c0dfe5eeb117f9cfba18
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62806353"
---
# <a name="editions-and-components-of-sql-server-2014"></a>SQL Server 2014 버전 및 구성 요소
  설치 요구 사항은 사용자의 애플리케이션 요구에 따라 달라질 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전별로 각기 다르게 조직 및 개인의 고유한 성능, 런타임 및 가격 요구 사항을 충족시켜 줍니다. 설치하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소도 특정 요구 사항에 따라 달라집니다. 다음 섹션은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 사용할 수 있는 여러 버전과 구성 요소 중에서 가장 적합한 항목을 선택하는 방법을 이해하는 데 도움이 될 것입니다.  
  
## <a name="principal-editions-of-includesscurrentincludessscurrent-mdmd"></a>
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]의 주 버전  
 다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 주 버전에 대해 설명합니다. 자세한 내용은 [SQL Server 2014 버전에서 지 원하는 기능](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md) 을 참조 하세요.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|정의|  
|---------------------------------------|----------------|  
|Enterprise(64비트 및 32비트)|프리미엄 제품인 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise 버전에서는 초고속 성능, 무제한 가상화 및 엔드투엔드 비즈니스 인텔리전스 기능이 포함된 포괄적인 고성능 데이터 센터를 제공하여 중요한 워크로드의 서비스 수준을 높이고 데이터 인사이트에 대해 최종 사용자 액세스를 가능하게 합니다.|  
|Business Intelligence(64비트 및 32비트)|
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Business Intelligence 버전에서는 안전하고 확장 가능하며 관리하기 쉬운 BI 솔루션을 구축하고 배포할 수 있도록 조직의 능력을 강화하는 포괄적인 플랫폼을 제공합니다. 이 버전에서는 데이터 탐색 및 시각화를 기반으로 한 브라우저, 강력한 데이터 분해 기능 및 향상된 통합 관리와 같은 뛰어난 기능이 제공됩니다.|  
|Standard(64비트 및 32비트)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]Standard edition은 부서와 소규모 조직을 위한 기본 데이터 관리 및 비즈니스 인텔리전스 데이터베이스를 제공 하 여 응용 프로그램을 실행 하 고, 온-프레미스 및 클라우드를 사용 하는 효율적인 데이터베이스 관리를 위한 일반적인 개발 도구를 지원 합니다. 최소 IT 리소스.|  
  
## <a name="specialized-editions-of-includesscurrentincludessscurrent-mdmd"></a>
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]의 특수 버전  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 특수 버전은 비즈니스 작업을 대상으로 합니다. 다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 특수 버전에 대해 설명합니다.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|Description|  
|---------------------------------------|-----------------|  
|Web(64비트 및 32비트)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Web 버전을 사용하면 소규모부터 대규모에 이르는 웹 속성에 대한 확장성, 경제성 및 관리 효율성 기능을 제공하여 웹 호스터와 웹 VAP의 총 소유 비용을 낮출 수 있습니다.|  
  
## <a name="breadth-editions-of-includesscurrentincludessscurrent-mdmd"></a>
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]의 확장형 버전  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 확장형 버전은 특정 고객 시나리오에 맞게 엔지니어링되었으며 무료로 또는 최소한의 비용으로 제공됩니다. 다음 표에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 확장형 버전에 대해 설명합니다.  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|Description|  
|---------------------------------------|-----------------|  
|Developer(64비트 및 32비트)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Developer 버전을 사용하면 개발자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]기반에서 어떤 유형의 애플리케이션도 빌드할 수 있습니다. 이 버전은 Enterprise 버전의 모든 기능을 포함하지만 프로덕션 서버가 아닌 개발 및 테스트 시스템으로 사용하도록 라이선스가 허여되어 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer는 애플리케이션을 빌드하고 테스트하는 사용자에게 적합한 버전입니다.|  
|Express(64비트 및 32비트) 버전|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]Express edition은 초급 수준의 무료 데이터베이스 이며 데스크톱 및 소규모 서버 데이터 기반 응용 프로그램을 학습 하 고 구축 하는 데 적합 합니다. 이 버전은 개별 소프트웨어 공급업체, 개발자 및 취미로 클라이언트 애플리케이션을 빌드하는 사용자에게 이상적입니다. 고급 데이터베이스 기능이 필요할 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express를 다른 고급 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 원활하게 업그레이드할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Express LocalDB는 모든 프로그래밍 기능을 포함 하지만 사용자 모드에서 실행 되며 구성이 필요 없는 빠른 설치가 가능 하 고 필수 구성 요소가 적은 간단한 Express 버전의 Express입니다.|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-an-internet-server"></a>인터넷 서버에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용  
 인터넷 정보 서비스(IIS)를 실행하는 서버와 같은 인터넷 서버에는 일반적으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 클라이언트 도구를 설치합니다. 클라이언트 도구에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 연결하는 애플리케이션이 사용하는 클라이언트 연결 구성 요소가 포함됩니다.  
  
> [!NOTE]  
>  IIS를 실행하는 컴퓨터에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 설치할 수 있지만 이러한 설치는 일반적으로 단일 서버 컴퓨터를 사용하는 소규모 웹 사이트에서만 수행됩니다. 대부분의 웹 사이트에서는 한 대의 서버나 서버 클러스터에 중간 계층 IIS 시스템이 있고 별도의 서버나 서버 페더레이션에 데이터베이스가 있습니다.  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>클라이언트/서버 애플리케이션으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 직접 연결되는 클라이언트/서버 애플리케이션 실행 컴퓨터에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]클라이언트 구성 요소만 설치하면 됩니다. 데이터베이스 서버의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 관리하거나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 애플리케이션을 개발하려는 경우에는 클라이언트 구성 요소를 설치하는 것도 좋은 방법입니다.  
  
 클라이언트 도구 옵션은 이전 버전과의 호환성 구성 요소, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , 연결 구성 요소, 관리 도구, 소프트웨어 개발 키트 및 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]온라인 설명서 구성 요소와 같은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기능을 설치합니다. 자세한 내용은 설치 [마법사 &#40;설치&#41;에서 SQL Server 2014 설치 ](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)를 참조 하세요.  
  
## <a name="deciding-among-includessnoversionincludesssnoversion-mdmd-components"></a>
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소 결정  
 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 마법사의 기능 선택 페이지를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]설치에 포함할 구성 요소를 선택할 수 있습니다. 트리에 있는 기능은 모두 기본적으로 선택되지 않습니다.  
  
 다음 표의 정보를 사용하여 사용자 요구에 가장 적합한 기능 집합을 결정하십시오.  
  
|서버 구성 요소|Description|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에는 [!INCLUDE[ssDE](../includes/ssde-md.md)]데이터 저장, 처리 및 보안 유지를 위한 핵심 서비스인, 복제 기능, 전체 텍스트 검색 기능 및 관계형 데이터와 XML 데이터 관리 도구 및 DQS [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] () 서버가 포함 되어 있습니다.|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에는 OLAP(온라인 분석 처리) 및 데이터 마이닝 애플리케이션을 생성하고 관리하기 위한 도구가 포함되어 있습니다.|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에는 테이블 형식, 행렬, 그래픽 및 자유 형식 보고서를 생성, 관리 및 배포하기 위한 서버/클라이언트 구성 요소가 포함되어 있습니다. 또한[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 는 보고서 애플리케이션을 개발하는 데 사용할 수 있는 확장 가능 플랫폼입니다.|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 데이터 이동, 복사 및 변환을 위한 그래픽 도구 및 프로그래밍 가능 개체 집합입니다. 또한 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 에 대한 DQS( [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]) 구성 요소도 포함됩니다.|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|MDS([!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] )는 마스터 데이터 관리용 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 솔루션입니다. MDS는 모든 도메인(제품, 고객, 계정)을 관리하도록 구성할 수 있으며 계층, 세부적인 보안, 트랜잭션, 데이터 버전 관리 및 비즈니스 규칙은 물론 데이터 관리에 사용할 수 있는 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 을 포함합니다.|  
  
|관리 도구|Description|  
|----------------------|-----------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]]의 모든 구성 요소를 액세스, 구성, 관리, 운영 및 개발하기 위한 통합 환경입니다. 
  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 에서는 모든 수준의 개발자와 관리자가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 사용할 수 있습니다.|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Configuration Manager|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스, 서버 프로토콜, 클라이언트 프로토콜 및 클라이언트 별칭에 대한 기본 구성 관리 작업을 수행할 수 있습니다.|  
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|
  [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 또는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 모니터링하기 위한 그래픽 사용자 인터페이스를 제공합니다.|  
|
  [!INCLUDE[ssDE](../includes/ssde-md.md)] 튜닝 관리자|
  [!INCLUDE[ssDE](../includes/ssde-md.md)] 튜닝 관리자는 최적의 인덱스, 인덱싱된 뷰 및 파티션 집합을 만드는 데 도움을 줍니다.|  
|Data Quality 클라이언트|DQS 서버에 연결하고 데이터 정리 작업을 수행하기 위한 매우 간단하고 직관적인 그래픽 사용자 인터페이스를 제공합니다. 또한 데이터 정리 작업 중에 수행되는 다양한 활동들을 중앙에서 모니터링할 수 있습니다.|  
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|
  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 에서는 비즈니스 인텔리전스 구성 요소( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)])를 위한 솔루션을 작성할 수 있는 IDE를 제공합니다.<br /><br /> (이전의 Business Intelligence Development Studio).<br /><br /> 또한[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 에 포함된 “데이터베이스 프로젝트”에서는 Visual Studio 내의 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 플랫폼(온-프레미스 및 온-프레미스 모두)에서 모든 해당 데이터베이스 디자인 작업을 수행하도록 데이터베이스 개발자에게 통합 환경을 제공합니다. 데이터베이스 개발자는 Visual Studio에서 향상된 서버 탐색기를 사용하여 데이터베이스 개체 및 데이터를 쉽게 만들거나 편집하고 쿼리를 실행할 수 있습니다.|  
|연결 구성 요소|클라이언트와 서버 간 통신 구성 요소와 DB-Library, ODBC 및 OLE DB용 네트워크 라이브러리를 설치합니다.|  
  
|문서화|Description|  
|-------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 온라인 설명서|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 핵심 설명서입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 설치 계획](install/planning-a-sql-server-installation.md)   
 [설치 마법사 &#40;설치 프로그램에서 SQL Server 2014을 설치&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
  
