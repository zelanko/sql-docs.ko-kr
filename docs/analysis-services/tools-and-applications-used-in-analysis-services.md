---
title: "Analysis Services에서 사용되는 도구 및 응용 프로그램 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 0ddb3b7a-7464-4d04-8659-11cb2e4cf3c3
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 17
---
# Analysis Services에서 사용되는 도구 및 응용 프로그램
  Analysis Services 모델을 개발하고 Analysis Services 인스턴스에서 연결된 데이터베이스를 관리하기 위해 필요한 도구 및 응용 프로그램을 찾으세요.  
  
## Analysis Services 모델 디자이너  
 테이블 형식 및 다차원 모델은 Visual Studio 셸에서 작성된 솔루션의 프로젝트 템플릿에서 생성됩니다. 프로젝트 템플릿은 Analysis Services 솔루션을 구성하는 테이블, 관계, 큐브, 차원 및 역할을 만들기 위해 디자이너를 제공합니다. 셸은 시각적 작업 영역, 속성 페이지 및 프로젝트가 생성되는 명령 프레임워크를 제공합니다. 셸과 템플릿을 제공하는 모델 디자이너는 웹에서 무료로 다운로드할 수 있습니다.  
  
 모델은 기능 가용성을 결정하고 Analysis Services의 릴리스가 모델을 실행하는 호환성 수준 설정을 가지고 있습니다.  지정된 호환성 수준을 지정할 수 있는지 여부는 부분적으로 모델 디자이너에 의해 결정됩니다.  
  
 테이블 형식 JSON 형식의 BIM 파일 및 양방향 교차 필터링 등 SQL Server 2016의 최신 기능을 사용하는 테이블 형식 모델은 호환성 수준 1200에서, 즉 SQL Server 2016과 동시에 배송되는 SQL Server 2015용 SQL Server Data Tools의 버전에서 생성해야 합니다(다운로드 링크는 아래 참조).  
  
 아마도 Analysis Services의 이전 버전에서 모델을 배포하고자 하기 때문에 더 낮은 호환성 수준이 필요한 경우에도 여전히 Visual Studio 2015용 SSDT에서 모델 디자이너를 사용할 수 있습니다. 최신 버전의 도구는 필요한 임의의 호환성 수준에서 모델 형식(테이블 형식 또는 다차원)의 생성을 지원합니다. 단지 이전 모델을 빌드하거나 편집하려는 경우 이전 도구를 유지할 필요는 없습니다.  
  
### 모델 디자이너 다운로드  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]은(는) 이전에 SSDT-BI(SQL Server Data Tools for Business Intelligence)라고 했고 그 이전에는 BIDS(Business Intelligence Development Studio)라고 했으며, Analysis Services 모델을 생성하는 데 사용됩니다.  
  
||  
|-|  
|**[Visual Studio 2015용 SSDT 다운로드](https://msdn.microsoft.com/mt429383)**|  
  
 디자이너의 이전 버전에 비해 Visual Studio 2015용 SQL Server Data Tools를 사용하는 것이 좋습니다. 이 도구는 관계 데이터베이스, Analysis Services 모델, Reporting Service 보고서 및 Reporting Services 패키지를 비롯한 모든 SQL Server 콘텐츠 유형에 대한 프로젝트 템플릿을 포함하고 있습니다.  
  
 SSDT는 Visual Studio 2015 셸에서 실행됩니다. 이미 Visual Studio 2015를 가지고 있는 경우 SSDT 설치 프로그램에서 프로젝트 템플릿만 추가합니다. Visual Studio 2015가 없는 경우 셸과 템플릿이 모두 설치됩니다.  
  
 이전 버전의 SSDT-BI 또는 BIDS가 컴퓨터에 설치되어 있는 경우 최신 버전이 이전 버전과 함께 설치됩니다.  
  
 SSDT를 설치한 후 새 프로젝트 대화 상자에 비즈니스 인텔리전스 템플릿이 표시됩니다.  
  
 ![SSDT의 새 프로젝트 템플릿](../analysis-services/media/ssdt-biprojects.png "SSDT의 새 프로젝트 템플릿")  
  
## 관리 도구  
  
### SQL Server Management Studio 다운로드  
 Management Studio는 Analysis Services를 비롯하여 모든 SQL Server 기능의 기본 관리 도구입니다. 이 도구는 이제 따로 다운로드해야 합니다.  
  
||  
|-|  
|**[SQL Server Management Studio 다운로드](https://msdn.microsoft.com/library/mt238290.aspx)**|  
  
 SQL Server 2016에서 Management Studio는 작업을 모니터링하고 서버 문제를 진단하는 데 사용되는 SQL Server Profiler 추적의 경량급 대안을 제공하는 Analysis Services용 확장 이벤트(xEvents)를 포함하고 있습니다. 자세한 내용은 [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) 을(를) 참조하세요.  
  
### SQL Server 프로파일러  
 공식적으로는 xEvents에 유리하게 사용되지 않지만 SQL Server Profiler는 연결, MDX 쿼리 실행 및 기타 서버 작동을 모니터링하는 친숙한 방법을 제공합니다. SQL Server Profiler는 기본적으로 설치됩니다. Windows Server 2012의 앱에서 SQL Server 응용 프로그램과 함께 찾을 수 있습니다.  
  
### PowerShell  
 PowerShell 명령을 사용하여 많은 관리 작업을 수행할 수 있습니다. 자세한 내용은 [Analysis Services의 PowerShell 스크립팅](../analysis-services/instances/powershell-scripting-in-analysis-services.md)을 참조하세요.  
  
### 커뮤니티 및 타사 도구  
 커뮤니티 코드 샘플은 [Analysis Services codeplex 페이지](http://sqlsrvanalysissrvcs.codeplex.com/) (영문)를 참조하세요. Analysis Services를 지원하는 타사 도구에 대한 추천을 검색하는 경우에는 [포럼](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices)이 도움이 됩니다.  
  
## 관련 항목:  
 [다차원 데이터베이스의 호환성 수준&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Analysis services에서 테이블 형식 모델에 대한 호환성 수준](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  