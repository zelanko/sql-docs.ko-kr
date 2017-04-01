---
title: "Analysis Services | Microsoft Docs"
ms.date: "03/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "Analysis Services, Analysis Services - 다차원 데이터 정보"
  - "SSAS"
  - "Analysis Services"
  - "SQL Server Analysis Services, Analysis Services - 다차원 데이터 정보"
  - "SQL Server Analysis Services"
  - "다차원 데이터 [Analysis Services]"
  - "SSAS, Analysis Services - 다차원 데이터 정보"
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: 60
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 60
---
# Analysis Services
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]는 의사 결정 지원 및 비즈니스 분석에서 사용되는 온라인 분석 데이터 엔진으로, Power BI, Excel, Reporting Services 보고서 및 기타 데이터 시각화 도구와 같은 클라이언트 응용 프로그램 및 비즈니스 보고서용으로 분석 데이터를 제공합니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 의 일반적인 워크플로에는 다차원 또는 테이블 형식 데이터 모델 제작, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 모델을 데이터베이스로 배포, 데이터베이스를 처리하여 데이터 또는 메타데이터와 함께 로드, 데이터 새로 고침 설정, 최종 사용자의 데이터 액세스를 허용하도록 사용 권한 할당 등이 포함됩니다. 이 다목적 데이터 모델을 사용할 준비가 되면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 를 데이터 원본으로 지원하는 클라이언트 응용 프로그램에서 해당 모델에 액세스할 수 있습니다.  
  
 모델은 주로 SQL Server 또는 Oracle 관계형 데이터베이스 엔진에서 호스팅되는 데이터 웨어하우스와 같은 외부 데이터 시스템의 데이터로 채워집니다(테이블 형식 모델은 추가 데이터 원본 유형을 지원함). 모델은 큐브와 같은 쿼리 개체를 지정할 뿐만 아니라 여러 큐브 및 계산과 비즈니스 논리와 탐색 및 드릴스루 동작과 같은 상호 작용을 캡슐화하는 KPI에서 사용할 수 있는 차원도 지정합니다.  
 
## <a name="analysis-services-on-premises-and-in-the-cloud"></a>온-프레미스와 클라우드에서 사용 가능한 Analysis Services
이제 Analysis Services를 클라우드에서 Azure 서비스 형태로 사용할 수 있습니다. 현재 미리 보기 단계에 있는 Azure Analysis Services는 1200 호환성 수준에서 테이블 형식 모델을 지원합니다. DirectQuery, 파티션, 행 수준 보안, 양방향 관계, 변환이 모두 지원됩니다. 자세한 내용을 알아보고 무료 시험 버전을 사용하려면 [Azure Analysis Services](https://azure.microsoft.com/en-us/services/analysis-services/)를 참조하세요. 
  
## <a name="server-mode"></a>서버 모드  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 설치 프로그램을 사용하여 Analysis Services를 설치하는 경우 구성하는 동안 해당 인스턴스에 대해 서버 모드를 지정합니다.  각 모드에는 특정 Analysis Services 솔루션에 고유한 여러 기능이 포함됩니다.  
  
-   **다차원 및 데이터 마이닝 모드** - OLAP 모델링 구문(큐브, 차원, 측정값)을 구현합니다.  
  
-   **테이블 형식 모드** - 메모리 내 관계형 데이터 모델링 구문(모델, 테이블, 열)을 구현합니다.  
  
     테이블 형식 모델은 최신 기능을 사용하여 기본 호환성 수준 1200에서 만들거나 이전의 1103 호환성 수준에서 만들 수 있습니다. 호환성 수준 간에는 중요한 차이가 있습니다. 수준이 어떻게 비교되는지에 대한 자세한 내용은 [Analysis Services의 테이블 형식 모델에 대한 호환성 수준](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)을 참조하세요.  
  
-   **파워 피벗 모드** - SharePoint에서 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 및 Excel 데이터 모델을 구현합니다(SharePoint용[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 은 SharePoint에서 호스트되는 데이터 모델을 로드 및 쿼리하고 새로 고치는 중간 계층 데이터 엔진임).  
  
 단일 인스턴스는 하나의 모드로만 구성할 수 있으며 나중에 변경할 수 없습니다.  동일한 서버에 각기 다른 모드의 여러 인스턴스를 설치할 수 있지만 설치 프로그램을 실행하고 각 인스턴스에 대한 구성 설정을 지정해야 합니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 기능은 버전별로 다릅니다. 자세한 내용은 [SQL Server 2016의 버전과 지원하는 기능](../sql-server/sql-server-2016의-버전과-지원하는-기능.md)을 참조하세요. 
  
## <a name="authoring-solutions"></a>솔루션 제작  
 모델을 만들려면 SQL Server Data Tools를 사용하고( [Analysis Services에서 사용되는 도구 및 응용 프로그램](../analysis-services/tools-and-applications-used-in-analysis-services.md)참조) 테이블 형식 또는 다차원 및 데이터 마이닝 프로젝트 템플릿을 선택합니다. 프로젝트 템플릿에는 모델에 필요한 모든 개체에 대한 폴더가 포함되어 있습니다. 마법사는 데이터 원본, 데이터 원본 뷰, 차원, 큐브, 역할 등 많은 기본 요소를 만드는 데 도움이 됩니다.  
  
## <a name="documentation-by-area"></a>영역별 설명서  
Analysis Services에 대한 설명서는 작성할 프로젝트 유형에 해당하는 여러 섹션으로 구성되어 있습니다. 다음 링크를 선택하면 각 모드 또는 기능 영역에 대한 자세한 내용을 볼 수 있습니다.  
   
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘")[ 새로운 기능](../analysis-services/what-s-new-in-analysis-services.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [테이블 형식 및 다차원 솔루션 비교](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [테이블 형식 모델](../analysis-services/tabular-models/tabular-models-ssas.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [다차원 모델](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [데이터 마이닝](../analysis-services/data-mining/data-mining-ssas.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘")[PowerPivot for SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [Analysis Services 인스턴스 관리](../analysis-services/instances/analysis-services-instance-management.md)  
   
 ![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [Analysis Services 자습서](../analysis-services/analysis-services-tutorials-ssas.md)  
  
![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [Analysis Services 개발자 설명서](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx)  
 
![작은 파일 폴더 아이콘](../analysis-services/media/filefolder-small.png "작은 파일 폴더 아이콘") [기술 참조(SSAS)](../analysis-services/powershell/technical-reference-ssas.md)