---
title: SQL Server 2016의 버전 및 지원하는 기능 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql
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
ms.openlocfilehash: 39694d0bbcf365712c34811bbedab76ad3cff950
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51702331"
---
# <a name="editions-and-supported-features-of-sql-server-2016"></a>SQL Server 2016의 버전 및 지원하는 기능
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

이 항목에서는 SQL Server 버전에서 지원하는 기능에 대해 자세히 설명합니다.  지금은 SQL Server 2017의 버전에서 지원하는 기능에 대해 변경된 내용이 없습니다.  
  
설치 요구 사항은 사용자의 응용 프로그램 요구에 따라 달라질 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전별로 각기 다르게 조직 및 개인의 고유한 성능, 런타임 및 가격 요구 사항을 충족시켜 줍니다. 설치하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소도 특정 요구 사항에 따라 달라집니다. 다음 섹션은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 사용할 수 있는 여러 버전과 구성 요소 중에서 가장 적합한 항목을 선택하는 방법을 이해하는 데 도움이 될 것입니다.  

SQL Server Evaluation 버전은 180일 동안 시험용으로 사용할 수 있습니다.  
  
최신 릴리스 정보 및 새로운 기능 정보는 다음을 참조하세요.
- [SQL Server 2017 릴리스 정보](../sql-server/sql-server-2017-release-notes.md)
- [SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md)
- [SQL Server 2017의 새로운 기능](../sql-server/what-s-new-in-sql-server-2017.md)
- [SQL Server 2016의 새로운 기능](../sql-server/what-s-new-in-sql-server-2016.md)

### <a name="try-sql-server"></a>SQL Server를 사용해 보세요.    
    
> [![평가 센터에서 다운로드](../analysis-services/media/download.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) **[평가 센터에서 SQL Server 2016 다운로드](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure 가상 머신 소형](../analysis-services/media/azure-virtual-machine-small.png)**[이미 설치된 SQL Server 2016으로 가상 머신을 스핀업](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SQL2016SP1-WS2016?tab=Overview?wt.mc_id=sqL16_vm)**   
  
## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] 버전  
 다음 표에서는 이러한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]버전에 대해 설명합니다. 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전|정의|  
|---------------------------------------|----------------|  
|Enterprise|프리미엄 제품인 [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise 버전에서는 초고속 성능, 무제한 가상화 및 종단 간 비즈니스 인텔리전스 기능이 포함된 포괄적인 고성능 데이터 센터를 제공함으로써 중요한 작업의 서비스 수준을 높이고 데이터 인사이트에 대한 최종 사용자의 액세스가 가능하도록 합니다.|  
|표준|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard 버전에서는 부서와 소규모 조직이 응용 프로그램을 실행하기 위한 기본 데이터 관리 및 비즈니스 인텔리전스 데이터베이스를 제공하고 온-프레미스 및 클라우드용 공용 개발 도구를 지원함으로써, 최소한의 IT 리소스만으로도 데이터베이스 관리를 효율적으로 수행할 수 있도록 합니다.|  
|Web|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web 버전을 사용하면 소규모부터 대규모에 이르는 웹 속성에 대한 확장성, 경제성 및 관리 효율성 기능을 제공하여 웹 호스터와 웹 VAP의 총 소유 비용을 낮출 수 있습니다.|  
|Developer|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer 버전을 사용하면 개발자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]기반에서 어떤 유형의 응용 프로그램도 빌드할 수 있습니다. 이 버전은 Enterprise 버전의 모든 기능을 포함하지만 프로덕션 서버가 아닌 개발 및 테스트 시스템으로 사용하도록 라이선스가 허여되어 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 개발자는 [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)]를 빌드하고 응용 프로그램을 테스트하는 사용자에게 적합한 버전입니다.|  
|Express 버전:|Express 버전은 초급 단계의 무료 데이터베이스로 데스크톱 및 소규모 서버 데이터 기반 응용 프로그램을 분석 및 빌드하는 데 적합합니다. 이 버전은 개별 소프트웨어 공급업체, 개발자 및 취미로 클라이언트 응용 프로그램을 빌드하는 사용자에게 이상적입니다. 고급 데이터베이스 기능이 필요할 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express를 다른 고급 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 원활하게 업그레이드할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB는 모든 프로그래밍 기능을 포함하지만 사용자 모드에서 실행되며 구성이 필요 없는 빠른 설치가 가능하고 필수 구성 요소가 적은 새로운 경량 버전의 Express입니다|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-an-internet-server"></a>인터넷 서버에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용  
 인터넷 정보 서비스(IIS)를 실행하는 서버와 같은 인터넷 서버에는 일반적으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 클라이언트 도구를 설치합니다. 클라이언트 도구에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 연결하는 응용 프로그램이 사용하는 클라이언트 연결 구성 요소가 포함됩니다.  
  
> **참고:**  IIS를 실행하는 컴퓨터에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 설치할 수 있지만 이러한 설치는 일반적으로 단일 서버 컴퓨터를 사용하는 소규모 웹 사이트에서만 수행됩니다. 대부분의 웹 사이트에서는 한 대의 서버나 서버 클러스터에 중간 계층 IIS 시스템이 있고 별도의 서버나 서버 페더레이션에 데이터베이스가 있습니다.  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>클라이언트/서버 응용 프로그램으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 직접 연결되는 클라이언트/서버 응용 프로그램 실행 컴퓨터에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]클라이언트 구성 요소만 설치하면 됩니다. 데이터베이스 서버의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 관리하거나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 응용 프로그램을 개발하려는 경우에는 클라이언트 구성 요소를 설치하는 것도 좋은 방법입니다.  
  
 클라이언트 도구 옵션은 이전 버전과의 호환성 구성 요소, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , 연결 구성 요소, 관리 도구, 소프트웨어 개발 키트 및 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]온라인 설명서 구성 요소와 같은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 기능을 설치합니다. 자세한 내용은 [Install SQL Server](../database-engine/install-windows/install-sql-server.md)(SQL Server 설치)를 참조하세요.  
  
## <a name="deciding-among-includessnoversionincludesssnoversion-mdmd-components"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 요소 결정  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 마법사의 기능 선택 페이지를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]설치에 포함할 구성 요소를 선택할 수 있습니다. 트리에 있는 기능은 모두 기본적으로 선택되지 않습니다.  
  
 다음 표의 정보를 사용하여 사용자 요구에 가장 적합한 기능 집합을 결정하십시오.  
  
|서버 구성 요소|설명|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에는 [!INCLUDE[ssDE](../includes/ssde-md.md)], 데이터 저장, 처리 및 보안을 위한 핵심 서비스, 복제, 전체 텍스트 검색, Hadoop 및 기타 다른 유형의 데이터 원본에 액세스하기 위한 PolyBase 통합 및 데이터베이스 분석 통합에서 관계형 및 XML 데이터를 관리하는 도구, DQS([!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]) 서버 등이 포함되어 있습니다.|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에는 OLAP(온라인 분석 처리) 및 데이터 마이닝 응용 프로그램을 생성하고 관리하기 위한 도구가 포함되어 있습니다.|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 에는 테이블 형식, 행렬, 그래픽 및 자유 형식 보고서를 생성, 관리 및 배포하기 위한 서버/클라이언트 구성 요소가 포함되어 있습니다. 또한[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 는 보고서 응용 프로그램을 개발하는 데 사용할 수 있는 확장 가능 플랫폼입니다.|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 는 데이터 이동, 복사 및 변환을 위한 그래픽 도구 및 프로그래밍 가능 개체 집합입니다. 또한 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 에 대한 DQS( [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]) 구성 요소도 포함됩니다.|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|MDS([!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] )는 마스터 데이터 관리용 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 솔루션입니다. MDS는 모든 도메인(제품, 고객, 계정)을 관리하도록 구성할 수 있으며 계층, 세부적인 보안, 트랜잭션, 데이터 버전 관리 및 비즈니스 규칙은 물론 데이터 관리에 사용할 수 있는 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 을 포함합니다.|  
|[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]|[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] 은 다수의 플랫폼에서 확장 가능하고 분산된 R 솔루션을 지원하며 Linux, Hadoop, Teradata를 비롯한 다수의 엔터프라이즈 데이터 원본 사용을 지원합니다.|  
  
|관리 도구|설명|  
|----------------------|-----------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 모든 구성 요소를 액세스, 구성, 관리, 운영 및 개발하기 위한 통합 환경입니다. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 에서는 모든 수준의 개발자와 관리자가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]를 사용할 수 있습니다.<br /><br /> 를 다운로드하여 설치합니다 <br />                [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] SQL Server Management Studio 다운로드  [에서](https://msdn.microsoft.com/library/mt238290.aspx)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구성 관리자에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서비스, 서버 프로토콜, 클라이언트 프로토콜 및 클라이언트 별칭에 대한 기본 구성 관리 작업을 수행할 수 있습니다.|  
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 또는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스를 모니터링하기 위한 그래픽 사용자 인터페이스를 제공합니다.|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)] 튜닝 관리자|[!INCLUDE[ssDE](../includes/ssde-md.md)] 튜닝 관리자는 최적의 인덱스, 인덱싱된 뷰 및 파티션 집합을 만드는 데 도움을 줍니다.|  
|Data Quality 클라이언트|DQS 서버에 연결하고 데이터 정리 작업을 수행하기 위한 매우 간단하고 직관적인 그래픽 사용자 인터페이스를 제공합니다. 또한 데이터 정리 작업 중에 수행되는 다양한 활동들을 중앙에서 모니터링할 수 있습니다.|  
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 에서는 비즈니스 인텔리전스 구성 요소( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)])를 위한 솔루션을 작성할 수 있는 IDE를 제공합니다.<br /><br /> (이전의 Business Intelligence Development Studio).<br /><br /> 또한[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 에 포함된 “데이터베이스 프로젝트”에서는 Visual Studio 내의 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 플랫폼(온-프레미스 및 온-프레미스 모두)에서 모든 해당 데이터베이스 디자인 작업을 수행하도록 데이터베이스 개발자에게 통합 환경을 제공합니다. 데이터베이스 개발자는 Visual Studio에서 향상된 서버 탐색기를 사용하여 데이터베이스 개체 및 데이터를 쉽게 만들거나 편집하고 쿼리를 실행할 수 있습니다.|  
|연결 구성 요소|클라이언트와 서버 간 통신 구성 요소와 DB-Library, ODBC 및 OLE DB용 네트워크 라이브러리를 설치합니다.|  
  
|설명서|설명|  
|-------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 온라인 설명서|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 핵심 설명서입니다.| 

**Developer 및 Evaluation Edition**  
Developer 및 Evaluation Edition에서 지원하는 기능의 경우 아래 표에서 SQL Server Enterprise Edition에 대해 나열된 기능을 참조하세요.
[!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1용 Developer Edition에 추가된 기능 목록은 [SQL Server 2016 SP1 버전](https://aka.ms/uw6cw4)을 참조하세요.  

Developer Edition은 [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md)에 대해 클라이언트 1개만 계속 지원합니다. 
  
##  <a name="Cross-BoxScaleLimits"></a> Scale Limits  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|단일 인스턴스에서 사용되는 최대 계산 용량 - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|운영 체제가 지원하는 최대 크기|소켓 4개 또는 코어 24개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨| 
|단일 인스턴스에서 사용되는 최대 계산 용량 - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 또는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|운영 체제가 지원하는 최대 크기|소켓 4개 또는 코어 24개 미만으로 제한됨|소켓 4개 또는 코어 16개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|소켓 1개 또는 코어 4개 미만으로 제한됨|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스당 최대 버퍼 풀 메모리|운영 체제가 지원하는 최대 크기|128GB|64GB|1410MB|1410MB|
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 인스턴스당 최대 Columnstore 세그먼트 캐시 메모리|무제한 메모리| 32GB<sup>2</sup>| 16GB<sup>2</sup>| 352MB<sup>2</sup>| 352MB<sup>2</sup>|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]의 데이터베이스당 메모리 최적화 데이터의 최대 크기|무제한 메모리| 32GB<sup>2</sup>| 16GB<sup>2</sup>| 352MB<sup>2</sup>| 352MB<sup>2</sup>|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스당 최대 메모리 사용량|운영 체제가 지원하는 최대 크기|테이블 형식: 16GB<br /><br /> MOLAP: 64GB|해당 사항 없음|해당 사항 없음|해당 사항 없음|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 인스턴스당 최대 메모리 사용량|운영 체제가 지원하는 최대 크기|64GB|64GB|4GB|해당 사항 없음|
|최대 관계형 데이터베이스 크기|524PB|524PB|524PB|10GB|10GB|  
  
<sup>1</sup> Server + CAL(클라이언트 액세스 라이선스) 기반 라이선스가 포함된 엔터프라이즈 버전(새 계약에 사용할 수 없음)은 SQL Server 인스턴스마다 최대 20개의 코어로 제한됩니다. 코어 기반 서버 라이선스 모델에서는 제한이 없습니다. 자세한 내용은 [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)을 참조하세요.  
  
<sup>2</sup> [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1에 적용됩니다. 

##  <a name="RDBMSHA"></a> RDBMS High Availability  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Server Core 지원 <sup>1</sup>|예|예|예|예|예|  
|로그 전달|예|예|예|아니오|아니오|  
|데이터베이스 미러링|예|예<br /><br /> Full 보안만|미러링 모니터만|미러링 모니터만|미러링 모니터만| 
|백업 압축|예|예|아니오|아니오|아니오| 
|데이터베이스 스냅숏|예|예 <sup>3</sup>|예 <sup>3</sup>|예 <sup>3</sup>|예 <sup>3</sup>|
|Always On 장애 조치(failover) 클러스터 인스턴스|예<br /><br /> 운영 체제가 지원하는 최대 크기의 노드 수|예<br /><br /> 노드 2개 지원|아니오|아니오|아니오|  
|Always On 가용성 그룹|예<br /><br /> 2개의 동기 보조 복제본을 포함하여 최대 8개까지 보조 복제본 지원|아니오|아니오|아니오|아니오|
|기본 가용성 그룹 <sup>2</sup>|아니오|예<br /><br /> 노드 2개 지원|아니오|아니오|아니오|
|온라인 페이지 및 파일 복원|예|아니오|아니오|아니오|아니오|
|온라인 인덱싱|예|아니오|아니오|아니오|아니오|
|온라인 스키마 변경|예|아니오|아니오|아니오|아니오|
|빠른 복구|예|아니오|아니오|아니오|아니오|
|미러된 백업|예|아니오|아니오|아니오|아니오|
|Hot Add 메모리 및 CPU|예|아니오|아니오|아니오|아니오|
|데이터베이스 복구 관리자|예|예|예|예|예|
|암호화된 백업|예|예|아니오|아니오|아니오|
|Microsoft Azure에 하이브리드 백업(URL에 백업)|예|예|아니오|아니오|아니오|  
  
 <sup>1</sup> Server Core에 SQL Server를 설치하는 방법에 대한 자세한 내용은 [Install SQL Server on Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md)(Server Core에 SQL Server 설치)를 참조하세요. 

<sup>2</sup> 기본 가용성 그룹에 대한 자세한 내용은 [기본 가용성 그룹](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)을 참조하세요.  

<sup>3</sup> [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1에 적용됩니다.
  
##  <a name="RDBMSSP"></a> RDBMS Scalability and Performance  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Columnstore <sup>1</sup>|예|예 <sup>2</sup>|예 <sup>2</sup>|예<sup>2</sup>|예<sup>2</sup>|  
|메모리 내 OLTP <sup>1</sup>|예|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>, <sup>3</sup>|예 <sup>2</sup>|
|Stretch Database|예|예|예|예|예|
|영구 주 메모리|예|예|예|예|예|
|다중 인스턴스 지원|50|50|50|50|50|
|테이블 및 인덱스 분할|예|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>|  
|데이터 압축|예|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>|
|관리|예|아니오|아니오|아니오|아니오|  
|분할된 테이블 병렬 처리|예|아니오|아니오|아니오|아니오|
|여러 Filestream 컨테이너|예|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>|예 <sup>2</sup>|
|NUMA 인식 및 큰 페이지 메모리 및 버퍼 배열 할당|예|아니오|아니오|아니오|아니오|
|Buffer Pool Extension|예|예|아니오|아니오|아니오|
|IO 리소스 관리|예|아니오|아니오|아니오|아니오|  
|지연된 내구성|예|예|예|예|예|

<sup>1</sup> 메모리 내 OLTP 데이터 크기 및 Columnstore 세그먼트 캐시는 크기 조정 제한 섹션에서 버전별로 지정된 메모리 양으로 제한됩니다. 최대 병렬 처리 수준도 제한됩니다. 인덱스 작성에 대한 DOP(병렬 처리 수준)는 Standard Edition의 경우 2DOP, Web 및 Express Edition의 경우 1DOP로 제한됩니다. 디스크 기반 테이블과 메모리 최적화 테이블에서 생성된 columnstore 인덱스가 해당합니다.

<sup>2</sup> [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1에 적용됩니다. 

<sup>3</sup> 이 기능은 LocalDB 설치 옵션에 포함되지 않습니다.
##  <a name="RDBMSS"></a> RDBMS Security  
  
|기능|Enterprise|Standard|Web|Express|Express with Advanced Services|  
|-------------|----------------|--------------|---------|-------------|------------------------------------| 
|행 수준 보안|예|예|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>|  
|항상 암호화|예|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>| 
|동적 데이터 마스킹|예|예|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>|   
|기본 감사|예|예|예|예|예| 
|미세 감사|예|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>|예 <sup>1</sup>| 
|투명한 데이터베이스 암호화|예|아니오|아니오|아니오|아니오|   
|확장 가능 키 관리|예|아니오|아니오|아니오|아니오| 
|사용자 정의 역할|예|예|예|예|예| 
|포함된 데이터베이스|예|예|예|예|예| 
|백업을 위한 암호화|예|예|아니오|아니오|아니오|  

<sup>1</sup> [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1에 적용됩니다.  
##  <a name="Replication"></a> Replication  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|다른 유형의 구독자|예|예|아니오|아니오|아니오|  
|병합 복제|예|예|예(구독자만)|예(구독자만)|예(구독자만)|   
|Oracle 게시|예|아니오|아니오|아니오|아니오| 
|피어 투 피어 트랜잭션 복제|예|아니오|아니오|아니오|아니오|   
|스냅숏 복제|예|예|예(구독자만)|예(구독자만)|예(구독자만)|   
|SQL Server 변경 내용 추적|예|예|예|예|예| 
|트랜잭션 복제|예|예|예(구독자만)|예(구독자만)|예(구독자만)|   
|Azure에 대한 트랜잭션 복제|예|예|아니오|아니오|아니오|   
|트랜잭션 복제 업데이트 가능한 구독|예|아니오|아니오|아니오|아니오|  
  
##  <a name="SSMS"></a> Management Tools  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SMO(SQL Management Objects)|예|예|예|예|예|  
|SQL 구성 관리자|예|예|예|예|예|   
|SQL CMD(명령 프롬프트 도구)|예|예|예|예|예|      
|Distributed Replay - 관리 도구|예|예|예|예|아니오|  
|Distribute Replay - Client|예|예|예|아니오|아니오|  
|Distributed Replay - 컨트롤러|예(최대 16개 클라이언트)|예(1개 클라이언트)|예(1개 클라이언트)|아니오|아니오|   
|SQL 프로파일러|예|예|아니요 <sup>1</sup>|아니요 <sup>1</sup>|아니요 <sup>1</sup>|  
|SQL Server 에이전트|예|예|예|아니오|아니오| 
|Microsoft System Center Operations Manager 관리 팩|예|예|예|아니오|아니오|  
|DTA(데이터베이스 튜닝 관리자)|예|예 <sup>2</sup>|예 <sup>2</sup>|아니오|아니오|      
  
 <sup>1</sup> SQL Server Web, SQL Server Express, SQL Server Express with Tools 및 SQL Server Express with Advanced Services는 SQL Server Standard 및 SQL Server Enterprise Edition을 사용하여 프로파일링할 수 있습니다.  
  
 <sup>2</sup> 튜닝은 Standard Edition 기능에서만 사용됩니다.  
  
##  <a name="RDBMSM"></a> RDBMS Manageability  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|사용자 인스턴스|아니오|아니오|아니오|예|예| 
|LocalDB|아니오|아니오|아니오|예|아니오| 
|관리자 전용 연결|예|예|예|예, 추적 플래그 있음|예, 추적 플래그 있음|   
|PowerShell 스크립팅 지원|예|예|예|예|예| 
|SysPrep 지원 <sup>1</sup>|예|예|예|예|예| 
|데이터 계층 응용 프로그램 구성 요소 작업 지원 - 추출, 배포, 업그레이드, 삭제|예|예|예|예|예| 
|정책 자동화(일정 및 변경 내용 검사)|예|예|예|아니오|아니오|   
|성능 데이터 수집기|예|예|예|아니오|아니오| 
|다중 인스턴스 관리에서 관리되는 인스턴스로 등록 가능|예|예|예|아니오|아니오|   
|표준 성능 보고서|예|예|예|아니오|아니오| 
|계획 지침을 위한 계획 지침 및 계획 고정|예|예|예|아니오|아니오|   
|인덱스 뷰의 직접 쿼리(NOEXPAND 힌트 사용)|예|예|예|예|예| 
|인덱싱된 뷰의 자동 유지 관리|예|예|예|아니오|아니오| 
|분산형 분할 뷰|예|아니오|아니오|아니오|아니오| 
|병렬 인덱스 작업|예|아니오|아니오|아니오|아니오|  
|쿼리 최적화 프로그램의 인덱싱된 뷰 자동 사용|예|아니오|아니오|아니오|아니오| 
|병렬 일관성 검사|예|아니오|아니오|아니오|아니오| 
|SQL Server 유틸리티 제어 지점|예|아니오|아니오|아니오|아니오|    
|버퍼 풀 확장|예|예|아니오|아니오|아니오| 
  
 <sup>1</sup> 자세한 내용은 [SysPrep을 사용하여 SQL Server 설치 시 고려 사항](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)을 참조하세요.  
 
<sup>2</sup> [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1에 적용됩니다. 
  
##  <a name="DevTools"></a> Development Tools  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Microsoft Visual Studio 통합|예|예|예|예|예| 
|Intellisense(Transact-SQL 및 MDX)|예|예|예|예|예| 
|SQL  Server  Data  Tools(SSDT)|예|예|예|예|아니오|    
|MDX 편집, 디버그 및 디자인 도구|예|예|아니오|아니오|아니오|   
  
##  <a name="Programmability"></a> Programmability  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|기본 R 통합|예|예|예|예|아니오|   
|고급 R 통합|예|아니오|아니오|아니오|아니오| 
|R Server (Standalone)|예|아니오|아니오|아니오|아니오|   
|PolyBase 계산 노드|예|예 <sup>1</sup>|예 <sup>1</sup>, <sup>2</sup>|예 <sup>1</sup>, <sup>2</sup>|예 <sup>1</sup>, <sup>2</sup>| 
|PolyBase 헤드 노드|예|아니오|아니오|아니오|아니오| 
|JSON|예|예|예|예|예|   
|쿼리 저장소|예|예|예|예|예|   
|임시 테이블|예|예|예|예|예|   
|CLR(공용 언어 런타임) 통합|예|예|예|예|예|   
|네이티브 XML 지원|예|예|예|예|예| 
|XML 인덱싱|예|예|예|예|예| 
|MERGE 및 UPSERT 기능|예|예|예|예|예|   
|FILESTREAM 지원|예|예|예|예|예| 
|FileTable|예|예|예|예|예| 
|날짜 및 시간 데이터 형식|예|예|예|예|예|  
|국제화 지원|예|예|예|예|예| 
|전체 텍스트 및 의미 체계 검색|예|예|예|예|아니오| 
|쿼리에서 언어 지정|예|예|예|예|아니오|   
|Service Broker(메시징)|예|예|아니요(클라이언트 전용)|아니요(클라이언트 전용)|아니요(클라이언트 전용)|   
|Transact-SQL 엔드포인트|예|예|예|아니오|아니오| 

<sup>1</sup> 여러 계산 노드를 사용하는 확장에는 헤드 노드가 필요합니다.

<sup>2</sup> [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1에 적용됩니다.
  
## <a name="IS"></a> Integration Services

[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 버전에서 지원되는 SSIS(Integration Services) 기능에 대한 자세한 내용은 [SQL Server 버전에서 지원하는 Integration Services 기능](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md)을 참조하세요.

##  <a name="MDS"></a> Master Data Services  
 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 버전에서 지원되는 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 및 Data Quality Services 기능에 대한 자세한 내용은 [SQL Server 버전에서 지원하는 Master Data Services 및 Data Quality Services 기능](../master-data-services/master-data-services-and-data-quality-services-features-support.md)을 참조하세요. 

  
##  <a name="DW"></a> Data Warehouse  
  
|기능|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|데이터베이스 없이 큐브 만들기|예|예|아니오|아니오|아니오 |   
|준비 및 데이터 웨어하우스 스키마 자동 생성|예|예|아니오|아니오|아니오| 
|변경 데이터 캡처|예|예 <sup>1</sup>|아니오|아니오|아니오| 
|스타 조인 쿼리 최적화|예|아니오|아니오|아니오|아니오| 
|확장 가능한 읽기 전용 Analysis Services 구성|예|아니오|아니오|아니오|아니오| 
|분할된 테이블 및 인덱스의 병렬 쿼리 처리|예|아니오|아니오|아니오|아니오|   
|글로벌 일괄 집계|예|아니오|아니오|아니오|아니오| 

<sup>1</sup> [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] SP1에 적용됩니다.  
##  <a name="SSAS"></a> Analysis Services  
  
[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 버전에서 지원하는 Analysis Services 기능에 대한 자세한 내용은 [SQL Server 버전에서 지원하는 Analysis Services 기능](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요. 
  
##  <a name="BIMD"></a> BI Semantic Model (Multi Dimensional)  
  
[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 버전에서 지원하는 Analysis Services 기능에 대한 자세한 내용은 [SQL Server 버전에서 지원하는 Analysis Services 기능](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요.
   
##  <a name="BIT"></a> BI Semantic Model (Tabular)  
  
[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 버전에서 지원하는 Analysis Services 기능에 대한 자세한 내용은 [SQL Server 버전에서 지원하는 Analysis Services 기능](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요.
  
##  <a name="PPSP"></a> Power Pivot for SharePoint  
  
[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 버전에서 지원하는 SharePoint용 Power Pivot 기능에 대한 자세한 내용은 [SQL Server 버전에서 지원하는 Analysis Services 기능](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요.
  
##  <a name="DM"></a> Data Mining  
  
[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 버전에서 지원하는 데이터 마이닝 기능에 대한 자세한 내용은 [SQL Server 버전에서 지원하는 Analysis Services 기능](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요.
  
##  <a name="SSRS"></a> Reporting  Services  
  
[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 버전에서 지원되는 Reporting Services 기능에 대한 자세한 내용은 [SQL Server 버전에서 지원하는 Reporting Services 기능](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요.

##  <a name="BIC"></a> Business Intelligence 클라이언트  

[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 버전에서 지원하는 비즈니스 인텔리전스 클라이언트 기능에 대한 자세한 내용은 [SQL Server 버전에서 지원하는 Analysis Services 기능](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) 또는 [SQL Server 버전에서 지원하는 Reporting Services 기능](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)을 참조하세요.
  
##  <a name="SLS"></a> Spatial and Location Services  
  
|기능 이름|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|공간 인덱스|예|예|예|예|예|   
|평면 및 측지 데이터 형식|예|예|예|예|예| 
|고급 공간 라이브러리|예|예|예|예|예|   
|산업 표준 공간 데이터 형식 가져오기/내보내기|예|예|예|예|예|   
  
##  <a name="ADS"></a> Additional Database Services  
  
|기능 이름|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|예|예|예|예|예|   
|데이터베이스 메일|예|예|예|아니오|아니오| 
  
##  <a name="Other"></a> Other Components  
  
|기능 이름|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|아니오|아니오| 
|StreamInsight HA|StreamInsight Premium Edition|아니오|아니오|아니오|아니오|   
  
> [![SSMS 다운로드](../analysis-services/media/download.png)](../ssms/download-sql-server-management-studio-ssms.md) 최신 버전의 **[SQL Server Management Studio 다운로드](../ssms/download-sql-server-management-studio-ssms.md)**      
  
## <a name="see-also"></a>참고 항목  
 [SQL Server에 대한 제품 사양](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [SQL Server 설치](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 
  
  
