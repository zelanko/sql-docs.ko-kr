---
title: Analysis Services | Microsoft Docs
ms.date: 05/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: 60
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8c3a514f91e9af8de54fdbd4d9ef851c72f1911e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="what-is-analysis-services"></a>Analysis Services 란?
  Analysis Services는 의사 결정 지원 및 Reporting Services 보고서를 Power BI에서 Excel과 같은 클라이언트 응용 프로그램 및 비즈니스 보고서에 대 한 분석 데이터를 제공 하는 비즈니스 분석 및 기타 데이터 시각화 도구에 사용 되는 분석 데이터 엔진.  
  
 온-프레미스 Azure Analysis Services 또는 SQL Server Analysis Services 서버 인스턴스에 데이터베이스로 모델을 배포, 되풀이 데이터 처리를 설정 및 할당 하는 다차원 또는 테이블 형식 데이터 모델을 제작 하는 일반적인 워크플로 포함 최종 사용자가 데이터 액세스할 수 있도록 권한입니다. 준비 완료 되었을 때 의미 체계 데이터 모델을 데이터 소스로 Analysis Services를 지 원하는 모든 클라이언트 응용 프로그램에서 액세스할 수 있습니다.  
 
## <a name="analysis-services-on-premises-and-in-the-cloud"></a>온-프레미스와 클라우드에서 사용 가능한 Analysis Services
이제 Analysis Services를 클라우드에서 Azure 서비스 형태로 사용할 수 있습니다. Azure Analysis Services 1200 이상 호환성 수준의 테이블 형식 모델을 지원합니다. DirectQuery, 파티션, 행 수준 보안, 양방향 관계, 변환이 모두 지원됩니다. 자세한 내용을 알아보고 무료 시험 버전을 사용하려면 [Azure Analysis Services](https://azure.microsoft.com/en-us/services/analysis-services/)를 참조하세요. 
  
## <a name="server-mode"></a>서버 모드  
 SQL Server 설치 프로그램을 사용 하 여 Analysis Services를 설치할 때 구성 하는 동안 지정할수록 해당 인스턴스에 대 한 서버 모드입니다.  각 모드에는 특정 Analysis Services 솔루션에 고유한 여러 기능이 포함됩니다.   
  
-   **테이블 형식 모드** -구현 메모리 내 관계형 데이터 모델링 구문 (모델, 테이블, 열, 측정값, 계층).  

-   **다차원 및 데이터 마이닝 모드** - OLAP 모델링 구문(큐브, 차원, 측정값)을 구현합니다. 

-   **Power Pivot Mode** -SharePoint에서 파워 피벗 구현 및 Excel 데이터 모델 (SharePoint 용 파워 피벗은 로드, 쿼리 및 SharePoint에서 호스트 되는 데이터 모델을 새로 고치는 다층 계층 데이터 엔진).  
  
 단일 인스턴스는 하나의 모드로만 구성할 수 있으며 나중에 변경할 수 없습니다.  동일한 서버에 각기 다른 모드의 여러 인스턴스를 설치할 수 있지만 설치 프로그램을 실행하고 각 인스턴스에 대한 구성 설정을 지정해야 합니다. 자세한 정보 및 각 모드에서 제공 하는 다른 기능 비교에 대 한 참조 [비교 테이블 형식 및 다차원 솔루션](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)합니다.
  
## <a name="authoring-and-managing-solutions"></a>제작 및 솔루션 관리  
 모델을 만들고 서버에 배포 하려면 SQL Server Data Tools, 중 하나는 테이블 형식 또는 다차원 및 데이터 마이닝 프로젝트 템플릿을 선택 사용할 수 있습니다. 프로젝트 템플릿에는 모델에 필요한 모든 개체에 대한 폴더가 포함되어 있습니다. 사이트, 도메인 마법사와 디자이너 다양 한 데이터 원본, 관계, 측정값 및 역할에 연결 하는 등의 기본 요소를 만들 수 있습니다. Model 데이터베이스 서버에 배포 되 면 데이터 처리를 구성, 모니터링 및 관리 서버 및 데이터베이스를 SQL Server Management Studio (SSMS)를 사용 합니다. 자세한 내용은 참고 [도구 및 Analysis Services에서 사용 되는 응용 프로그램](../analysis-services/tools-and-applications-used-in-analysis-services.md)합니다. 
  
## <a name="documentation-by-area"></a>영역별 설명서  
일반에서 Azure Analysis Services에 대 한 설명서 Azure 문서 포함 되어 있습니다. 및 SQL Server Analysis Services에 대 한 설명서는 SQL 설명서에 포함 되어 있습니다. 그러나 이상 테이블 형식 모델에 대 한 만들고 프로젝트를 배포할은 사용 중인 어떤 플랫폼에 관계 없이 거의 동일 합니다.  
   
*  [Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/)
*  [SQL Server Analysis Services의 새로운 기능](../analysis-services/what-s-new-in-analysis-services.md)   
*  [테이블 형식 및 다차원 솔루션 비교](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
*  [테이블 형식 모델](../analysis-services/tabular-models/tabular-models-ssas.md)  
*  [다차원 모델](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
*  [데이터 마이닝](../analysis-services/data-mining/data-mining-ssas.md)  
*  [SharePoint 용 power Pivot](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
*  [인스턴스 관리](../analysis-services/instances/analysis-services-instance-management.md)    
*  [자습서](../analysis-services/analysis-services-tutorials-ssas.md)   
*  [개발자 설명서](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx)  
*  [기술 참조 (SSAS)](../analysis-services/powershell/technical-reference-ssas.md)

