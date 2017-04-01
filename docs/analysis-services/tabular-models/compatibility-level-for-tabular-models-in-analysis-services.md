---
title: "Analysis services에서 테이블 형식 모델에 대한 호환성 수준 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.bidtoolset.versioncompat.f1"
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: 27
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 27
---
# Analysis services에서 테이블 형식 모델에 대한 호환성 수준
  모델 또는 데이터베이스의 *호환성 수준*은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 엔진의 릴리스 관련 동작의 집합을 참조합니다. 특정 릴리스의 동작을 가져오도록 모든 지원되는 호환성 수준에서 모델을 만들 수 있습니다. 예를 들어 DirectQuery 및 테이블 형식 개체 메타데이터에는 호환성 수준 할당에 따라 서로 다른 구현이 있습니다.  
  
 **SQL Server 2016 RTM(1200)** 또는 줄여서 1200 호환성 수준은 SQL Server 2016에서 새로 도입되었으며 테이블 형식 모델에만 적용됩니다.  1200 호환성 수준에서 테이블 형식 모델은 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 테이블 형식 인스턴스에서만 실행됩니다.  
  
 테이블 형식 모델을 만들거나 업그레이드하려면 프로젝트가 만들어진 후 **model.bim** 파일에서 또는 프로젝트를 만들 때 SSDT(SQL Server Data Tools)를 사용하고 **호환성 수준** 속성을 설정합니다.  
  
> [!NOTE]  
>  다차원 모델은 호환성 수준 기준으로 독립적인 버전 경로를 따릅니다. 1103의 경우와 숫자가 동일한 경우 이는 우연의 일치입니다. 자세한 내용은 [다차원 데이터베이스의 호환성 수준&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)을 참조하세요.  
  
## 테이블 형식 모델 데이터베이스에 대한 지원되는 호환성 수준  
 Analysis Services는 모델 및 데이터베이스 모두에 적용할 수 있는 다음 호환성 수준을 지원합니다.  모델을 만드는 데 사용되는 도구의 버전은 더 높은 호환성 수준을 사용할 수 있는지 확인합니다.  
  
||||  
|-|-|-|  
|호환성 수준|서버 버전|모델링 도구 버전|  
|1200|SQL Server 2016 인스턴스에서만 실행|[Visual Studio 2015용 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>1</sup><br /><br /> [What's New in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md) 은(는) 이 수준에서 사용할 수 있는 기능을 설명합니다.|  
|1103|SQL Server 2016<br /><br /> SQL Server 2014<br /><br /> SQL Server 2012 SP1|[Visual Studio 2015용 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>2</sup><br /><br /> [Business Intelligence용 SQL Server Data Tools(Visual Studio 2013)](https://www.microsoft.com/en-us/download/details.aspx?id=42313)<br /><br /> [Business Intelligence용 SQL Server Data Tools(Visual Studio 2012)](http://www.microsoft.com/en-us/download/details.aspx?id=36843)|  
|1100|SQL Server 2016<br /><br /> SQL Server 2014<br /><br /> SQL Server 2012 SP1<br /><br /> SQL Server 2012|[Visual Studio 2015용 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>1</sup><br /><br /> [Business Intelligence용 SQL Server Data Tools(Visual Studio 2013)](https://www.microsoft.com/en-us/download/details.aspx?id=42313)<br /><br /> [Business Intelligence용 SQL Server Data Tools(Visual Studio 2012)](http://www.microsoft.com/en-us/download/details.aspx?id=36843)<br /><br /> Business Intelligence Development Studio(Visual Studio 2010 Shell에서 실행 및 SQL Server 설치 프로그램을 통해 설치)|  
  
 <sup>1</sup> Visual Studio 2015용 SQL Server Data Tools를 사용하여 이전 버전의 Analysis Services에 1100 또는 1103 테이블 형식 모델을 배포할 수 있습니다.  
  
 <sup>2</sup> 호환성 수준 1100, 1103 및 1200은 Visual Studio 2015용 SQL Server Data Tools의 테이블 형식 모델 프로젝트에 대해 모두 유효하지만 Analysis Services의 SQL Server 2016 인스턴스에서 1200 모델을 배포 및 실행할 수 있습니다.  
  
## SSDT에서 테이블 형식을 만들거나 업그레이드할 때 호환성 수준 설정  
 SSDT(SQL Server Data Tools)에서 새 테이블 형식 모델 프로젝트를 만들 때 **새 테이블 형식 프로젝트 옵션** 대화 상자에서 호환성 수준을 지정할 수 있습니다.  
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.jpg "ssas_tabularproject_compat1200")  
  
 또한 **이 메시지를 다시 표시 안 함** 옵션을 선택하여 기본 호환성 수준을 지정할 수도 있습니다. 모든 후속 프로젝트는 지정된 호환성 수준을 사용합니다. SSDT의 **도구** > **옵션**에서 기본 호환성 수준을 변경할 수 있습니다.  
  
 테이블 형식 모델 프로젝트를 업그레이드하려면 모델 **속성** 창의 **호환성 수준** 속성을 **SQL Server 2016 RTM(1200)**으로 설정합니다.  자세한 내용은 [Upgrade Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) 을 참조하세요.  
  
> [!NOTE]  
>  테이블 형식 모델을 만드는 한 가지 방법은 가져오는 Power Pivot 통합 문서를 기준으로 하는 것입니다. 기본적으로 Power BI Desktop은 1200 호환성 수준에서 테이블 형식 모델을 자동으로 만듭니다. 그러나 이전 버전의 Power Pivot 통합 문서는 1100 수준에 있을 수 있습니다. 이전 통합 문서를 사용할 경우 **호환성 수준** 속성을 변경하여 업그레이드해야 합니다.  
  
## SSMS에서 데이터베이스에 대한 호환성 수준 확인  
 SSMS에서 데이터베이스 이름 > **속성**  > **호환성 수준** 속성을 마우스 오른쪽 단추로 클릭합니다.  
  
## SSMS의 서버에 대해 지원되는 호환성 수준 확인  
 SSMS에서 서버 이름 > **속성** > **지원되는 호환성 수준**을 마우스 오른쪽 단추로 클릭합니다.  
  
 이 속성은 서버에서 실행되는 데이터베이스의 가장 높은 호환성 수준을 지정합니다.  지원되는 호환성 수준은 읽기 전용이며 변경할 수 없습니다.  
  
## 관련 항목:  
 [다차원 데이터베이스의 호환성 수준&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Analysis Services의 새로운 기능](../../analysis-services/what-s-new-in-analysis-services.md)   
 [파워 피벗에서 가져오기&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)   
 [새 테이블 형식 모델 프로젝트 만들기&#40;Reporting Services&#41;](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  