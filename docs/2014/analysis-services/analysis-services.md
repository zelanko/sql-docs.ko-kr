---
title: Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c2bcf7cb620a97578b921ca09d565ff2ef2fe77a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48080975"
---
# <a name="analysis-services"></a>Analysis Services
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]는 의사 결정 지원 및 BI(비즈니스 인텔리전스) 솔루션에서 사용되는 온라인 분석 데이터 엔진으로, Excel, Reporting Services 보고서, 타사 BI 도구와 같은 클라이언트 응용 프로그램 및 비즈니스 보고서에 대해 분석 데이터를 제공합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 일반적인 워크플로에는 OLAP 또는 표 형식 데이터 모델 작성, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 데이터베이스로 모델 배포, 데이터베이스를 처리하여 데이터와 함께 로드, 데이터 액세스 허용 권한 할당이 포함됩니다. 이 다목적 데이터 모델은 준비가 되면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]를 데이터 원본으로 지원하는 클라이언트 응용 프로그램에서 액세스할 수 있습니다.  
  
 모델을 만들려면 SQL Server Data Tools를 사용 하 여 (참조 [Analysis Services에 사용 되는 응용 프로그램과 도구](tools-and-applications-used-in-analysis-services.md)), 테이블 형식 또는 다차원 및 데이터 마이닝 프로젝트 템플릿을 선택 합니다. 프로젝트 템플릿에는 모델에 필요한 모든 개체에 대한 폴더가 포함되어 있습니다. 마법사를 사용하여 데이터 원본, 데이터 원본 뷰, 차원, 큐브 및 역할과 같은 모든 기본 요소를 만들 수 있습니다.  
  
 모델은 주로 SQL Server 또는 Oracle 관계형 데이터베이스 엔진에서 호스팅되는 데이터 웨어하우스와 같은 외부 데이터 시스템의 데이터로 채워집니다(테이블 형식 모델은 추가 데이터 원본 유형을 지원함). 모델은 큐브와 같은 쿼리 개체를 지정할 뿐만 아니라 여러 큐브 및 계산과 비즈니스 논리와 탐색 및 드릴스루 동작과 같은 상호 작용을 캡슐화하는 KPI에서 사용할 수 있는 차원도 지정합니다.  
  
 모델을 사용하려면 Excel 또는 다른 응용 프로그램을 통해 연결하는 권한 있는 사용자가 데이터를 사용할 수 있도록 특정 서버 모드에서 데이터베이스를 실행하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 배포됩니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스를 다음 세 서버 모드 중 하나에서 설치할 수 있습니다.  
  
-   테이블 형식 모델을 실행하는 테이블 형식 인스턴스로.  
  
-   OLAP 큐브 및 데이터 마이닝 모델(기본값임)을 실행하는 다차원 및 데이터 마이닝 인스턴스로.  
  
-   SharePoint에서 PowerPivot 및 Excel 데이터 모델을 실행하는 SharePoint용 PowerPivot으로(SharePoint용 PowerPivot은 SharePoint에서 호스팅되는 데이터 모델을 로드하고 쿼리하고 새로 고치는 중간 계층 데이터 엔진임).  
  
 같은 데이터 엔진. 사용할 수 있는 3개의 다른 방법이 있습니다. 서버 모드는 설치 과정에서 설정되고 나중에 변경할 수 없습니다. 다른 모드로 변경하려면 새 인스턴스를 설치해야 합니다.  
  
 Analysis Services에 대한 기본 설명서는 작성할 프로젝트 유형에 해당하는 여러 섹션으로 구성되어 있습니다. 다음 링크를 선택하면 각 모드 또는 기능 영역에 대한 자세한 내용을 볼 수 있습니다.  
  
 **영역별 내용 찾아보기**  
 ![작은 파일 폴더 아이콘](../../2014/integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") [테이블 형식 및 다차원 솔루션 비교 &#40;SSAS&#41;](comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![작은 파일 폴더 아이콘](../../2014/integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") [Analysis Services 인스턴스 관리](instances/analysis-services-instance-management.md)  
  
 ![작은 파일 폴더 아이콘](../../2014/integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") [테이블 형식 모델링 &#40;&AMP;#40;SSAS 테이블 형식&#41;](tabular-models/tabular-models-ssas.md)  
  
 ![작은 파일 폴더 아이콘](../../2014/integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") [다차원 모델링 &#40;SSAS&#41;](multidimensional-models/multidimensional-models-ssas.md)  
  
 ![작은 파일 폴더 아이콘](../../2014/integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") [비교 &#40;SSAS&#41;](data-mining/data-mining-ssas.md)  
  
 ![작은 파일 폴더 아이콘](../../2014/integration-services/media/filefolder-small.gif "작은 파일 폴더 아이콘") [PowerPivot for SharePoint &#40;SSAS&#41;](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 기능은 버전별로 다릅니다. 다차원 및 데이터 마이닝 모델은 스탠더드 버전에서 사용할 수 있지만 상위 버전에 비해 기능이 제한됩니다. 테이블 형식 모델 및 SharePoint용 PowerPivot은 프리미엄 기능으로 스탠더드 버전 라이선스에서 사용할 수 없습니다. 자세한 내용은 [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 자습서 &#40;SSAS&#41;](analysis-services-tutorials-ssas.md)   
 [SQL Server 2014 설치](../database-engine/install-windows/installation-for-sql-server.md)   
 [개발자 가이드 &#40;Analysis Services&#41;](analysis-services-developer-documentation.md)   
 [SQL Server 리소스 센터](http://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](http://go.microsoft.com/fwlink/?linkID=220963)  
  
  
