---
title: "다차원 모델 데이터 액세스 (Analysis Services-다차원 데이터) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSAS, data access interfaces
- objects [Analysis Services], data access interfaces
- Analysis Services data access interfaces
- data retrieval [Analysis Services]
- retrieving data
- metadata [Analysis Services]
- data access interfaces [Analysis Services]
- manipulating objects [Analysis Services]
- Analysis Services data access interfaces, about data access interfaces
ms.assetid: 46388efb-3c78-47a2-b5c9-5a69ff394d03
caps.latest.revision: 46
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b659b4fd581742270fe5d38e5791ef215002757b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="multidimensional-model-data-access-analysis-services---multidimensional-data"></a>다차원 모델 데이터 액세스(Analysis Services - 다차원 데이터)
  이 항목에서는 네트워크의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버에 대한 연결을 기본적으로 지원하는 클라이언트 응용 프로그램, 프로그래밍 방법 또는 스크립트를 사용하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 다차원 데이터에 액세스하는 방법에 대해 설명합니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
 [클라이언트 응용 프로그램](#bkmk_clientapps)  
  
 [쿼리 언어](#bkmk_querylang)  
  
 [프로그래밍 방식 인터페이스](#bkmk_api)  
  
##  <a name="bkmk_clientapps"></a> 클라이언트 응용 프로그램  
 Analysis Services에는 프로그래밍 방식으로 다차원 데이터베이스를 작성 또는 통합할 수 있는 인터페이스가 포함되어 있지만 Microsof 또는 Analysis Services 데이터에 대한 액세스를 기본적으로 제공하는 다른 소프트웨어 공급업체의 기존 클라이언트 응용 프로그램을 사용하는 것이 더 일반적입니다.  
  
 다음 Microsoft 응용 프로그램은 다차원 데이터에 대한 네이티브 연결을 지원합니다.  
  
### <a name="excel"></a>Excel  
 Analysis Services 다차원 데이터는 대개 Excel 통합 문서의 피벗 테이블 및 피벗 차트 컨트롤을 사용하여 표시됩니다. 피벗 테이블이 다차원 데이터에 적합한 이유는 모델의 계층, 집계 및 탐색 구성이 피벗 테이블의 데이터 요약 기능과 잘 맞기 때문입니다. Analysis Services OLE DB 데이터 공급자는 데이터 연결을 쉽게 설정할 수 있도록 Excel 설치에 포함되어 있습니다. 자세한 내용은 [SQL Server Analysis Services에 연결 또는 데이터 가져오기](http://go.microsoft.com/fwlink/?linkID=215150)를 참조하십시오.  
  
### <a name="reporting-services-reports"></a>Reporting Services 보고서  
 보고서 작성기 또는 보고서 디자이너를 사용하여 분석 데이터가 포함된 Analysis Services 데이터베이스를 사용하는 보고서를 만들 수 있습니다. 보고서 작성기와 보고서 디자이너에는 사용 가능한 데이터 원본에서 데이터를 검색하는 MDX 문을 입력하거나 설계하는 데 사용할 수 있는 MDX 쿼리 디자이너가 포함되어 있습니다. 자세한 내용은 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) 및 [MDX용 Analysis Services 연결 형식&#40;SSRS&#41;](../../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)을 참조하세요.  
  
### <a name="performancepoint-dashboards"></a>PerformancePoint 대시보드  
 PerformancePoint 대시보드는 Sharepoint에서 미리 정의된 측정값에 대해 사업 성과를 평가하는 성과 기록표를 만드는 데 사용됩니다. PerformancePoint에는 Analysis Services 다차원 데이터에 대한 데이터 연결을 지원하는 기능이 포함되어 있습니다. 자세한 내용은 [Analysis Services 데이터 연결 만들기(PerformancePoint Services)](http://go.microsoft.com/fwlink/?linkid=232471)를 참조하세요.  
  
### <a name="sql-server-data-tools"></a>SQL Server Data Tools  
 모델 및 보고서 디자이너는 SQL Server Data Tools를 사용하여 다차원 모델을 포함하는 솔루션을 구축합니다. 솔루션을 Analysis Services 인스턴스에 배포하면 나중에 Excel, Reporting Services 및 기타 비즈니스 인텔리전스 클라이언트 응용 프로그램에서 연결할 데이터베이스가 만들어집니다.  
  
 SQL Server Data Tools는 Visual Studio 셸을 기반으로 작성되었으며 프로젝트를 사용하여 모델을 구성하고 포함합니다. 자세한 내용은 [SSDT&#40;SQL Server Data Tools&#41;를 사용하여 다차원 모델 만들기](../../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)를 참조하세요.  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 SQL Server Management Studio는 데이터베이스 관리자가 Analysis Services 인스턴스 및 다차원 데이터베이스를 비롯하여 SQL Server 인스턴스를 관리하는 통합 환경입니다. 자세한 내용은 [SQL Server Management Studio](http://msdn.microsoft.com/library/66a6b7b1-de6a-4161-82bd-98ded486947b) 및 [Analysis Services에 연결](../../../analysis-services/instances/connect-to-analysis-services.md)을 참조하세요.  
  
##  <a name="bkmk_querylang"></a> 쿼리 언어  
 MDX는 OLAP 데이터베이스에서 데이터를 검색하는 데 사용되는 산업 표준 쿼리 및 계산 언어입니다. Analysis Services에서 MDX는 데이터를 검색하는 데 사용되는 쿼리 언어지만 데이터 정의 및 데이터 조작도 지원합니다. MDX 편집기는 SQL Server Management Studio, Reporting Services 및 SQL Server Data Tools에 기본 제공됩니다. MDX 편집기를 사용하여 임시 쿼리를 만들거나 반복 가능한 데이터 작업의 경우 다시 사용할 수 있는 스크립트를 만들 수 있습니다.  
  
 Excel과 같은 일부 도구 및 응용 프로그램은 MDX 구문을 사용하여 Analysis Services 데이터 원본을 내부적으로 쿼리합니다. 또한 MDX 문을 XMLA 실행 요청에 포함하여 프로그래밍 방식으로 MDX를 사용할 수 있습니다.  
  
 MDX에 대한 자세한 내용은 다음 링크를 참조하십시오.  
  
 [MDX를 사용하여 다차원 데이터 쿼리](../../../analysis-services/multidimensional-models/mdx/querying-multidimensional-data-with-mdx.md)  
  
 [MDX의 주요 개념&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
 [MDX 쿼리 기본 사항&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
 [MDX 스크립팅 기본 사항&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
##  <a name="bkmk_api"></a> 프로그래밍 방식 인터페이스  
 다차원 데이터를 사용하는 사용자 지정 응용 프로그램을 작성하는 경우 다음과 같은 방법 중 하나로 데이터에 액세스합니다.  
  
-   **XMLA**. 다양한 운영 체제 및 프로토콜과의 호환성이 필요한 경우 XMLA를 사용합니다. XMLA는 가장 유연한 방식이지만 성능 및 프로그래밍의 용이성은 좀 떨어질 수 있습니다.  
  
-   **클라이언트 라이브러리**. Microsoft Windows 운영 체제에서 실행되는 클라이언트 응용 프로그램에서 프로그래밍 방식으로 데이터에 액세스하려는 경우 ADOMD.NET, AMO 및 OLE DB와 같은 Analysis Services 클라이언트 라이브러리를 사용합니다. 클라이언트 라이브러리는 개체 모델 및 성능을 향상시키는 최적화로 XMLA를 래핑합니다.  
  
     ADOMD.NET 및 AMO 클라이언트 라이브러리는 관리 코드로 작성된 응용 프로그램을 위한 것입니다. 네이티브 코드로 작성된 응용 프로그램의 경우 Analysis Services용 OLE DB를 사용하십시오.  
  
 다음 표에서는 Analysis Services를 사용자 지정 응용 프로그램에 연결하는 데 사용되는 클라이언트 라이브러리에 대한 추가 정보 및 링크를 제공합니다.  
  
|인터페이스|Description|  
|---------------|-----------------|  
|AMO(Analysis Services Management Objects)|AMO는 코드에서 Analysis Services 인스턴스 및 다차원 데이터베이스를 관리하는 기본 개체 모델입니다. 예를 들어 SQL Server Management Studio는 AMO를 사용하여 서버 및 데이터베이스 관리를 지원합니다. 자세한 내용은 [AMO&#40;Analysis Management Objects&#41;를 사용하여 개발](../../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)을 참조하세요.|  
|ADOMD.NET|ADOMD.NET은 사용자 지정 응용 프로그램에서 다차원 데이터를 만들고 액세스하는 기본 개체 모델입니다. 관리되는 클라이언트 응용 프로그램에서 ADOMD.NET을 사용하여 공용 Microsoft .NET Framework 데이터 액세스 인터페이스를 통해 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 정보를 검색할 수 있습니다. 자세한 내용은 [ADOMD.NET을 사용하여 개발](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md) 및 [ADOMD.NET 클라이언트 프로그래밍](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)을 참조하세요.|  
|Analysis Services OLE DB 공급자(MSOLAP.dll)|네이티브 OLE DB 공급자를 사용하여 관리되지 않는 API에서 프로그래밍 방식으로 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 액세스할 수 있습니다. 자세한 내용은 [Analysis Services OLE DB 공급자&#40;Analysis Services - 다차원 데이터&#41;](http://msdn.microsoft.com/library/cdeecd50-1d91-4162-a4a2-01c7799b02a8)를 참조하세요.|  
|스키마 행 집합|스키마 행 집합 테이블은 서버에 배포된 다차원 모델에 대한 정보 및 서버의 현재 작업에 대한 설명 정보를 포함하는 데이터 구조입니다. 프로그래머는 클라이언트 응용 프로그램에서 스키마 행 집합 테이블을 쿼리하여 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 저장된 메타데이터를 검토하고 지원 및 모니터링 정보를 검색할 수 있습니다. OLE DB, Analysis Services용 OLE DB, 데이터 마이닝용 OLE DB 또는 XMLA 프로그래밍 인터페이스를 통해 스키마 행 집합을 사용할 수 있습니다. 자세한 내용은 [Analysis Services 스키마 행 집합](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)을 참조하세요.<br /><br /> 다음 목록에서는 스키마 행 집합을 사용하는 몇 가지 방법에 대해 설명합니다.<br /><br /> SQL Server Management Studio 또는 사용자 지정 보고서에서 DMV 쿼리를 실행하여 SQL 구문을 통해 스키마 행 집합에 액세스합니다. 자세한 내용은 [DMV&#40;동적 관리 뷰&#41;를 사용하여 Analysis Services 모니터링](../../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)을 참조하세요.<br /><br /> -스키마 행 집합을 호출하는 ADOMD.NET 코드를 작성합니다.<br /><br /> - [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 대해 직접 XMLA **Discover** 메서드를 실행하여 스키마 행 집합 정보를 검색합니다. 자세한 내용은 [Discover 메서드&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-methods-discover.md)를 참조하세요.|  
|XMLA|XMLA는 Analysis Services 프로그래머가 사용할 수 있는 가장 낮은 수준의 API이며 모든 Analysis Services 데이터 액세스 방법의 공통 분모입니다. XMLA는 HTTP 연결에서 사용할 수 있는 모든 표준 다차원 데이터 원본에 대한 범용 데이터 액세스를 지원하는 산업 표준, SOAP 기반 XML 프로토콜입니다. XMLA는 SOAP를 사용하여 다차원 데이터에 대한 요청 및 응답을 작성합니다. 응용 프로그램이 Windows 이외의 플랫폼에서 실행되는 경우 XMLA를 사용하여 네트워크의 Windows 서버에서 실행되고 있는 다차원 데이터베이스에 액세스할 수 있습니다. 자세한 내용은 [Analysis Services에서 XMLA를 사용하여 개발](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)을 참조하세요.|  
|ASSL(Analysis Services Scripting Language)|ASSL은 XMLA 프로토콜의 Analysis Services 확장에 적용되는 설명적인 용어입니다. XMLA 프로토콜에서 설명하는 Execute와 Discover 메서드 외에 ASSL은 다음과 같은 기능을 추가합니다.<br /><br /> -XMLA 스크립트<br /><br /> -XMLA 개체 정의<br /><br /> -XMLA 명령<br /><br /> ASSL 확장을 통해 Analysis Services는 프로토콜에서 기본적으로 제공하는 기능 외에 데이터 정의, 데이터 조작 및 데이터 제어 지원까지 추가하여 XMLA 구문을 사용할 수 있습니다. 자세한 내용은 [ASSL&#40;Analysis Services Scripting Language&#41;을 사용하여 개발](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)를 참조하십시오.|  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services에 연결](../../../analysis-services/instances/connect-to-analysis-services.md)   
 [스크립팅 언어 &#40; Analysis Services를 사용 하 여 개발 ASSL &#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Analysis Services에서 XMLA를 사용 하 여 개발](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [테이블 형식 모델 데이터 액세스](../../../analysis-services/tabular-models/tabular-model-data-access.md)  
  
  

