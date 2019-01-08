---
title: 테이블 형식 모델 데이터 액세스 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 6ae74a8b-0025-450d-94a5-4e601831d420
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5dc6ccd51a1ce8c64ef301e7435ee9ce21879cb5
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53364105"
---
# <a name="tabular-model-data-access"></a>테이블 형식 모델 데이터 액세스
  Analysis Services의 테이블 형식 model 데이터베이스에는 다차원 모델에서 데이터 또는 메타데이터를 검색하는 데 사용하는 것과 동일한 대부분의 클라이언트, 인터페이스 및 언어로 액세스할 수 있습니다. 자세한 내용은 [다차원 모델 데이터 액세스&#40;Analysis Services - 다차원 데이터&#41;](../multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)를 참조하세요.  
  
 이 항목에서는 테이블 형식 모델에서 사용할 수 있는 클라이언트, 쿼리 언어 및 프로그래밍 인터페이스에 대해 설명합니다.  
  
## <a name="clients"></a>클라이언트  
 다음 Microsoft 클라이언트 애플리케이션은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 테이블 형식 모델 데이터베이스에 대한 네이티브 연결을 지원합니다.  
  
### <a name="excel"></a>내보내기  
 Excel의 데이터 시각화 및 분석 기능을 사용하여 Excel에서 테이블 형식 model 데이터베이스에 연결하여 데이터를 사용할 수 있습니다. 데이터에 액세스하려면 Analysis Services 데이터 연결을 정의하고, 테이블 형식 서버 모드로 실행되는 서버를 지정한 다음, 사용할 데이터베이스를 선택합니다. 자세한 내용은 [SQL Server Analysis Services에 연결 또는 데이터 가져오기](https://go.microsoft.com/fwlink/?linkID=215150)를 참조하십시오.  
  
 Excel은 또한 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 테이블 형식 모델을 찾아보는 데 권장되는 애플리케이션입니다. 이 도구에는 Excel의 새 인스턴스를 시작하고, Excel 통합 문서를 만들고, 통합 문서에서 모델 작업 영역 데이터베이스로의 데이터 연결을 여는 **Excel에서 분석** 옵션이 포함되어 있습니다. Excel에서 테이블 형식 모델 데이터를 찾아보는 경우 Excel은 Excel 피벗 테이블 클라이언트를 사용하여 모델에 대한 쿼리를 실행한다는 사실을 기억하십시오. 따라서 Excel 통합 문서 내에서 작업할 경우 DAX 쿼리가 아니라 MDX 쿼리가 작업 영역 데이터베이스로 전송됩니다. SQL 프로파일러 또는 기타 모니터링 도구를 사용하여 쿼리를 모니터링하는 경우 프로파일러 추적에 DAX가 아니라 MDX가 표시됩니다. Excel에서 분석 기능에 대한 자세한 내용은 [Excel에서 분석&#40;SSAS 테이블 형식&#41;](analyze-in-excel-ssas-tabular.md)을 참조하세요.  
  
### <a name="power-view"></a>파워 뷰  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 는 SharePoint 2010 환경에서 실행되는 Reporting Services 보고 클라이언트 응용 프로그램입니다. 이 프로그램은 데이터 탐색, 쿼리 디자인 및 프레젠테이션 레이아웃을 통합된 임시 보고 환경으로 통합합니다. [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 는 모델이 테이블 형식 모드로 실행되는 Analysis Services의 인스턴스에서 호스팅되는지 또는 DirectQuery 모드를 사용하여 관계형 데이터 저장소에서 검색되는지 여부에 관계없이 테이블 형식 모델을 데이터 원본으로 사용할 수 있습니다. [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]에서 테이블 형식 모델에 연결하려면 서버 위치 및 데이터베이스 이름이 포함된 연결 파일을 만들어야 합니다. SharePoint에서 Reporting Services 공유 데이터 원본 또는 BI 의미 체계 모델 연결 파일을 만들 수 있습니다. BI 의미 체계 모델 연결에 대 한 자세한 내용은 참조 하세요. [PowerPivot BI 의미 체계 모델 연결 &#40;.bism&#41;](../power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)합니다.  
  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 클라이언트는 지정된 데이터 원본에 요청을 보내 지정된 모델의 구조를 확인합니다. 이 요청에서는 클라이언트가 데이터 원본인 모델에 대한 쿼리를 만들고 데이터를 기반으로 작업을 수행하는 데 사용할 수 있는 스키마가 반환됩니다. [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 사용자 인터페이스에서 데이터를 필터링하고, 계산 또는 집계를 수행하고, 관련 데이터를 표시하는 후속 작업은 클라이언트에 의해 제어되며 프로그래밍 방식으로 조작할 수 없습니다.  
  
 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 클라이언트에서 모델로 보내는 쿼리는 모델에 대해 추적을 설정하여 모니터링할 수 있는 DAX 문으로 실행됩니다.  또한 클라이언트는 CSDL(개념 스키마 정의 언어)에 따라 제공되는 초기 스키마 정의에 대한 요청을 서버에 보냅니다. 자세한 내용은 [CSDL Annotations for Business Intelligence &#40;CSDLBI&#41;](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)  
  
### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 테이블 형식 모델을 호스팅하는 인스턴스를 관리하고 해당 메타데이터 및 데이터를 쿼리할 수 있습니다. 모델 또는 모델의 개체를 처리하고, 파티션을 생성 및 관리하고, 데이터 액세스를 관리하는 데 사용될 수 있는 보안을 설정할 수 있습니다. 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [Analysis Services 인스턴스의 서버 모드 확인](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
-   [Analysis Services에 연결](../instances/connect-to-analysis-services.md)  
  
-   [Analysis Services 인스턴스 모니터링](../instances/monitor-an-analysis-services-instance.md)  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 MDX 및 XMLA 쿼리 창을 사용하여 테이블 형식 데이터베이스에서 데이터 및 메타데이터를 검색할 수 있습니다. 그러나 다음과 같은 제한 사항이 있습니다.  
  
-   MDX 및 DMX를 사용하는 문은 DirectQuery 모드로 배포된 모델에 지원되지 않으므로 DirectQuery 모드에서 테이블 형식 모델에 대한 쿼리를 만들려면 대신 **XMLA 쿼리** 창을 사용해야 합니다.  
  
-   **쿼리** 창을 연 후에는 XMLA 쿼리 창의 데이터베이스 컨텍스트를 변경할 수 없습니다. 따라서 다른 데이터베이스 또는 다른 인스턴스에 쿼리를 보내려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 해당 데이터베이스 또는 인스턴스를 열고 해당 컨텍스트 내에서 새 **XMLA 쿼리** 창을 열어야 합니다.  
  
 다차원 솔루션에서와 마찬가지로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 테이블 형식 모델에 대한 추적을 만들 수 있습니다. 이 릴리스의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 메모리 사용, 쿼리 및 처리 작업, 파일 사용 등을 추적하는 데 사용할 수 있는 많은 새 이벤트를 제공합니다. 자세한 내용은 [Analysis Services 추적 이벤트](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)를 참조하세요.  
  
> [!WARNING]  
>  테이블 형식 model 데이터베이스에 추적을 두면 DMX 쿼리로 분류되는 몇 가지 이벤트를 볼 수 있습니다. 그러나 데이터 마이닝은 테이블 형식 모델 데이터에서 지원되지 않으며 데이터베이스에서 실행되는 DMX 쿼리는 모델 메타데이터에 대한 SELECT 문으로 제한됩니다. 동일한 파서 프레임워크가 MDX에 사용되므로 이벤트는 DMX로만 분류됩니다.  
  
## <a name="query-languages"></a>쿼리 언어  
 Analysis Services 테이블 형식 모델은 다차원 모델에 대한 액세스를 위해 제공되는 것과 동일한 쿼리 언어의 대부분을 지원합니다. DirectQuery 모드로 배포된 테이블 형식 모델은 예외인데, 이러한 모델은 Analysis Services 데이터 저장소에서 데이터를 검색하는 것이 아니라 SQL Server 데이터 원본에서 직접 데이터를 검색하기 때문입니다. 이러한 모델은 MDX를 사용하여 쿼리할 수 없으며, DAX 식을 Transact-SQL 문으로 변환하도록 지원하는 클라이언트(예: [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 클라이언트)를 사용해야 합니다.  
  
### <a name="dax"></a>DAX  
 모델이 PowerPivot 사용 Excel 통합문서로 SharePoint에 저장되는지 아니면 Analysis Services의 인스턴스에 저장되는지에 관계없이 모든 종류의 테이블 형식 모델에서 식과 수식을 만드는 데 DAX를 사용할 수 있습니다.  
  
 또한 XMLA EXECUTE 명령 문의 컨텍스트 내에서 DAX 식을 사용하여 DirectQuery 모드로 배포된 테이블 형식 모델로 쿼리를 보낼 수 있습니다.  
  
 DAX를 사용한 테이블 형식 모델의 쿼리에 대한 예는 [DAX 쿼리 구문 참조](https://msdn.microsoft.com/library/ee634217.aspx)를 참조하세요.  
  
### <a name="mdx"></a>MDX  
 MDX를 사용하여 메모리 내 캐시를 기본 쿼리 방법으로 사용하는 테이블 모델(즉, DirectQuery 모드로 배포되지 않은 모델)에 대한 쿼리를 만들 수 있습니다. [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 와 같은 클라이언트는 집계를 만드는 작업과 모델을 데이터 원본으로 쿼리하는 작업 모두에 DAX를 사용하지만 MDX에 친숙한 경우 MDX에서 예제 쿼리를 만드는 것이 더욱 효율적일 수 있습니다. 자세한 내용은 [MDX로 측정값 만들기](../multidimensional-models/mdx/mdx-building-measures.md)를 참조하세요.  
  
### <a name="csdl"></a>CSDL  
 개념 스키마 정의 언어는 쿼리 언어가 아니지만 본질적으로 모델 및 모델 메타데이터 정보를 검색하는 데 사용될 수 있습니다. 이러한 정보는 나중에 해당 모델에 대한 보고서나 쿼리를 만드는 데 사용될 수 있습니다.  
  
 테이블 형식 모델에서 CSDL을 사용하는 방법에 대한 자세한 내용은 [비즈니스 인텔리전스에 대한 CSDL 주석&#40;CSDLBI&#41;](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)을 참조하세요.  
  
## <a name="programmatic-interfaces"></a>프로그래밍 방식 인터페이스  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 테이블 형식 모델과 상호 작용하는 데 사용되는 주요 인터페이스는 스키마 행 집합, XMLA 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 와 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 제공하는 쿼리 클라이언트 및 쿼리 도구입니다.  
  
### <a name="data-and-metadata"></a>데이터 및 메타데이터  
 ADOMD.NET을 사용하여 관리 애플리케이션의 테이블 형식 모델에서 데이터 및 메타데이터를 검색할 수 있습니다. 테이블 형식 모델에서 개체를 만들고 수정하는 애플리케이션의 예는 다음 리소스를 참조하십시오.  
  
-   Codeplex에서 테이블 형식 모델 AMO 예제  
  
-   [DMV&#40;동적 관리 뷰&#41;를 사용하여 Analysis Services 모니터링](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
 관리되지 않는 클라이언트 애플리케이션에서 Analysis Services 9.0 OLE DB 공급자를 사용하여 테이블 형식 모델에 대한 OLE DB 액세스를 지원할 수 있습니다. 테이블 형식 모델 액세스를 사용하도록 설정하려면 업데이트된 버전의 Analysis Services OLE DB 공급자가 필요합니다. 테이블 형식 모델과 함께 사용되는 공급자에 대한 자세한 내용은 [SharePoint 서버에서 Analysis Services OLE DB 공급자 설치](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) 를 참조하세요.  
  
 XML 기반 형식으로 Analysis Services 인스턴스에서 직접 데이터를 검색할 수도 있습니다. DISCOVER_CSDL_METADATA 행 집합을 사용하여 테이블 형식 모델의 스키마를 검색하거나 기본 ASSL 요소, 개체 또는 속성에 EXECUTE 또는 DISCOVER 명령을 사용할 수 있습니다. 자세한 내용은 다음 리소스를 참조하십시오.  
  
-   [비즈니스 인텔리전스에 대한 CSDL 주석&#40;CSDLBI&#41;](https://docs.microsoft.com/bi-reference/csdl/csdl-annotations-for-business-intelligence-csdlbi)  
  
### <a name="manipulate-analysis-services-objects"></a>Analysis Services 개체 조작  
 XMLA 명령 또는 AMO를 사용하여 테이블 형식 모델과 해당 모델의 개체(예: 테이블, 열, 큐브 뷰, 측정값 및 파티션)를 생성, 수정, 삭제 및 처리할 수 있습니다. AMO와 XMLA 둘 다 향상된 보고 및 모델링을 위해 테이블 형식 모델에 사용되는 추가 속성을 지원하도록 업데이트되었습니다.  
  
 AMO 및 XMLA를 사용하여 테이블 형식 모델을 스크립팅할 수 있는 방법에 대한 예는 다음 리소스를 참조하십시오.  
  
-   Codeplex에서 테이블 형식 모델 AMO 예제  
  
-   CodePlex의 AdventureWorks 예제  
  
 PowerShell을 사용하여 Analysis Services 인스턴스를 관리 및 모니터링하고 테이블 모델 액세스에 사용되는 보안을 만들고 모니터링할 수 있습니다. 자세한 내용은 [Analysis Services PowerShell](../analysis-services-powershell.md)합니다.  
  
### <a name="schema-rowsets"></a>스키마 행 집합  
 클라이언트 애플리케이션에서는 스키마 행 집합을 사용하여 테이블 형식 모델의 메타데이터를 검사하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에서 지원 및 모니터링 정보를 검색할 수 있습니다. 이 릴리스의 SQL Server에는 새로운 스키마 행 집합이 추가되었으며 테이블 형식 모델과 관련된 기능을 지원하고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서의 모니터링 및 성능 분석을 향상시키도록 기존 스키마 행 집합이 확장되었습니다.  
  
-   [DISCOVER_CALC_DEPENDENCY 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-calc-dependency-rowset)  
  
     테이블 형식 모델에서 열 및 참조 간의 종속성을 추적하는 새로운 스키마 행 집합  
  
-   [DISCOVER_CSDL_METADATA 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-csdl-metadata-rowset)  
  
     테이블 형식 모델의 CSDL 표현을 가져오는 새로운 스키마 행 집합  
  
-   [DISCOVER_XEVENT_TRACE_DEFINITION 행 집합](../dev-guide/discover-xevent-trace-definition-rowset.md)  
  
     SQL Server 확장 이벤트를 모니터링하는 새로운 스키마 행 집합. 자세한 내용은 [사용 하 여 SQL Server 확장 이벤트 &#40;Xevent&#41; to Monitor Analysis Services](../instances/monitor-analysis-services-with-sql-server-extended-events.md)합니다.  
  
-   [DISCOVER_TRACES 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-traces-rowset)  
  
     범주별로 추적을 필터링할 수 있는 새로운 `Type` 열. 자세한 내용은 [재생에 대한 프로파일러 추적 만들기&#40;Analysis Services&#41;](../instances/create-profiler-traces-for-replay-analysis-services.md)를 참조하세요.  
  
-   [MDSCHEMA_HIERARCHIES 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset)  
  
     테이블 형식 모델에 생성된 사용자 정의 계층을 식별하는 새로운 `STRUCTURE_TYPE` 열거형. 자세한 내용은 [계층 구조&#40;SSAS 테이블 형식&#41;](hierarchies-ssas-tabular.md)를 참조하세요.  
  
 데이터 마이닝 스키마 행 집합용 OLE DB는 이 릴리스에서 업데이트되지 않았습니다.  
  
> [!WARNING]  
>  DirectQuery 모드로 배포된 데이터베이스에는 MDX 또는 DMX 쿼리를 사용할 수 없습니다. 따라서 스키마 행 집합을 사용하여 DirectQuery 모델에 대해 쿼리를 실행해야 하는 경우 연결된 DMV가 아니라 XMLA를 사용해야 합니다. $system.DBSCHEMA_CATALOGS 또는 DISCOVER_TRACES의 SELECT *와 같이 전체 서버에 대한 결과를 반환하는 DMV의 경우 캐시된 모드로 배포된 데이터베이스 내용에서 쿼리를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 형식 model 데이터베이스에 연결&#40;SSAS&#41;](connect-to-a-tabular-model-database-ssas.md)   
 [PowerPivot 데이터 액세스](../power-pivot-sharepoint/power-pivot-data-access.md)   
 [Analysis Services에 연결](../instances/connect-to-analysis-services.md)  
  
  
