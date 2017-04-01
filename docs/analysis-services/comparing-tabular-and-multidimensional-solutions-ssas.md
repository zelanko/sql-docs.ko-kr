---
title: "테이블 형식 및 다차원 솔루션(SSAS) 비교 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
caps.latest.revision: 49
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 47
---
# 테이블 형식 및 다차원 솔루션(SSAS) 비교
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]는 비즈니스 인텔리전스 의미 체계 모델을 만드는 다양한 접근 방식(다차원, 테이블 형식 및 파워 피벗)을 제공합니다.  
  
 둘 이상의 접근 방식을 사용하면 다양한 비즈니스 및 사용자 요구 사항에 맞게 모델링 환경을 조정할 수 있습니다. 다차원은 다양한 BI 소프트웨어 공급업체에서 수용하는 개방형 표준 기반의 완성도 높은 기술이지만 습득하기 어려울 수 있습니다. 테이블 형식은 많은 개발자에게 보다 직관적인 관계형 모델링 접근 방식을 제공합니다. 파워 피벗은 훨씬 간단한 접근 방식으로, SharePoint를 통해 제공되는 서버 지원과 더불어 Excel에서 시각적 데이터 모델링을 제공합니다.  
  
 모든 모델은 Analysis Services 인스턴스에서 실행되고, 단일 데이터 공급자 집합을 사용하여 클라이언트 도구에서 액세스하며, Excel, Reporting Services, Power BI 및 다른 공급업체의 BI 도구를 통해 대화형 및 정적 보고서에 시각화되는 데이터베이스로 배포됩니다.  
  
 메모리 아키텍처와 메타데이터 간의 차이로 인해 상호 교환 가능한 모델 형식은 없지만 테이블 형식 1050-1103 모델에서 테이블 형식 1200 모델로 매우 쉽게 업그레이드할 수 있으며, PowerPivot을 가져와 완전히 새로운 모델을 및 테이블 형식 프로젝트로 만들 수 있습니다.  
  
 테이블 형식 및 다차원 솔루션은 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 를 통해 구축되었으며, 독립 실행형 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에서 실행되는 기업 BI 프로젝트에 사용됩니다. 두 솔루션 모두 BI 클라이언트와 쉽게 통합되는 고성능 분석 데이터베이스를 제공합니다. 하지만 각 솔루션은 구축,  사용 및 배포되는 방법이 다릅니다. 이 항목에서는 대부분 사용자에게 적합한 접근 방식을 식별할 수 있도록 이 두 가지 유형을 비교합니다.  
  
 새로운 개발 프로젝트에는 일반적으로 테이블 형식이 권장됩니다. 테이블 형식은 설계, 테스트 및 배포 속도가 빠르고, Microsoft에서 제공되는 최신 셀프 서비스 BI 응용 프로그램 및 클라우드 서비스와의 효율성도 뛰어납니다.  
  
##  <a name="a-namebkmkoverviewa-overview-of-modeling-types"></a><a name="bkmk_overview"></a> 모델링 유형에 대한 개요  
 Analysis Services를 처음 접하는 사용자를 위해 다음 표에서는 다양한 모델을 열거하고, 접근 방식을 요약하며, 초기 릴리스 수단을 식별합니다.  
  
||||  
|-|-|-|  
|**형식**|**모델링 설명**|**릴리스됨**|  
|다차원|OLAP 모델링 구문(큐브, 차원, 측정값)입니다.|SQL Server 2000 이상|  
|테이블 형식|관계형 모델링 구문(모델, 테이블, 열)입니다.<br /><br /> 내부적으로 메타데이터는 OLAP 모델링 구문(큐브, 차원, 측정값)에서 상속됩니다. 코드 및 스크립트에는 OLAP 메타데이터가 사용됩니다.|SQL Server 2012 이상(호환성 수준 1050 - 1103) <sup>1</sup>|  
|SQL Server 2016의 테이블 형식|스크립트 및 코드의 테이블 형식 메타데이터 개체 정의에 표시되는 관계형 모델링 구문(모델, 테이블, 열)입니다.|SQL Server 2016(호환성 수준 1200)|  
|Power Pivot|원래는 추가 기능이었지만 지금은 Excel에 완전히 통합되어 있습니다. 내부 테이블 형식 인프라를 통해서만 지원되는 시각적 모델링입니다. PowerPivot 모델을 SSDT로 가져와 Analysis Services 인스턴스에서 실행되는 새 테이블 형식 모델을 만들 수 있습니다.|Excel 및 PowerPivot BI Desktop을 통해|  
  
 <sup>1</sup> 호환성 수준은 SQL Server 2012에서 도입되었으며 새로운 테이블 형식 메타데이터 엔진 및 더 높은 수준에서만 제공되는 시나리오 지원 기능으로 인해 현재 릴리스에서 중요한 요소입니다. 주목할 만한 향상된 기능에는 DirectQuery, 스크립트 및 프로그래밍 기능이 있습니다. 자세한 내용은 [What's New in Analysis Services](../analysis-services/what-s-new-in-analysis-services.md) 를 참조하세요.  
  
##  <a name="a-namebkmkmodelsa-model-features"></a><a name="bkmk_models"></a> 모델 기능  
  다음 표에는 모델 수준에서의 기능 가용성이 요약되어 있습니다. 사용하고 싶은 기능이 빌드하려는 모델 유형에서 제공되는지 알아보려면 다음 목록을 검토하세요.  
  
|||||  
|-|-|-|-|  
||다차원|테이블 형식|Power Pivot|  
|작업|예|아니요|아니오|  
|Aggregations|예|아니요|아니오|  
|계산된 열|아니오|사용자 계정 컨트롤|예|  
|계산 측정값|예|사용자 계정 컨트롤|예|  
|계산된 테이블|아니요|예 <sup>1</sup>|아니요|  
|사용자 지정 어셈블리|예|아니요|아니오|  
|사용자 지정 롤업|예|아니요|아니오|  
|기본 멤버|예|아니요|아니오|  
|표시 폴더|예|예 <sup>1</sup>|아니오|  
|Distinct Count|예|예(DAX를 통해)|예(DAX를 통해)|  
|드릴스루|예|예(세부 정보가 별도의 워크시트에서 열림)|예|  
|계층 구조|예|사용자 계정 컨트롤|예|  
|KPI|예|사용자 계정 컨트롤|예|  
|연결된 개체|예|예(연결된 테이블)|아니오|  
|다 대 다 관계|예|아니요(하지만 1200 호환성 수준에서 [양방향 교차 필터](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md)가 있음)|아니오|  
|명명된 집합|예|아니요|아니오|  
|부모-자식 계층 구조|예|예(DAX를 통해)|예(DAX를 통해)|  
|파티션|예|사용자 계정 컨트롤|예|  
|큐브 뷰|예|사용자 계정 컨트롤|예|  
|반가산적 측정값|예|사용자 계정 컨트롤|예|  
|Translations|[예](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|예|[예](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)|  
|사용자 정의 계층|예|사용자 계정 컨트롤|예|  
|쓰기 저장(writeback)|예|아니요|아니오|  
  
 <sup>1</sup> 테이블 형식 범위 내의 기능 차이점에 대한 자세한 내용은 [Analysis Services에서 테이블 형식 모델에 대한 호환성 수준](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)을 참조하세요.  
  
##  <a name="a-namebkmkdsa-data-considerations"></a><a name="bkmk_ds"></a> 데이터 고려 사항  
 테이블 형식 및 다차원 모델은 외부 원본에서 가져온 데이터를 사용합니다. 가져와야 하는 데이터의 양 및 형식은 데이터에 가장 적합한 모델 유형을 결정할 때 주요 고려 사항일 수 있습니다.  
  
 **압축**  
  
 테이블 형식 및 다차원 솔루션 모두에는 데이터를 가져오는 데이터 웨어하우스에 비해 Analysis Services 데이터베이스 크기를 줄여 주는 데이터 압축 기술이 사용됩니다. 실제 압축 비율은 기본 데이터의 특성에 따라 크게 달라지기 때문에 쿼리에서 데이터를 처리하고 사용한 후에 솔루션에 필요한 디스크 및 메모리의 양은 정확하게 예측할 수는 없습니다.  
  
 여러 Analysis Services 개발자들은 일반적으로 다차원 데이터베이스에 필요한 기본 저장소 크기를 원본 데이터 크기의 1/3 정도로 예상합니다. 테이블 형식 데이터베이스에서는 대부분의 데이터가 사실 값 데이터로부터 가져온 데이터인 경우 특히 압축 효율을 1/10까지 높일 수 있습니다.  
  
 **모델의 크기 및 리소스 편차(메모리 내 또는 디스크)**  
  
 Analysis Services 데이터베이스의 크기는 이를 실행하는 데 사용할 수 있는 리소스에 의해서만 제한됩니다. 또한 모델 유형 및 저장소 모드는 데이터베이스가 증가할 수 있는 크기에 양향을 줍니다.  
  
 테이블 형식 데이터베이스는 메모리 내에서 실행되거나, 외부 데이터베이스에 쿼리 실행을 오프로드하는 DirectQuery 모드에서 실행됩니다. 테이블 형식 메모리 내 분석의 경우 데이터베이스는 완전히 메모리 내에 저장됩니다. 따라서 모든 데이터를 로드할 뿐만 아니라 쿼리를 지원하기 위해 만든 추가 데이터 구조를 로드할 수 있는 충분한 메모리가 있어야 합니다.  
  
 이 릴리스에서 수정된 DirectQuery는 이전보다 제한 사항이 적고 성능이 향상되었습니다. 저장소 및 쿼리 실행에 백 엔드 관계형 데이터베이스를 활용하면 이전보다 더 적합하게 대규모 테이블 형식 모델을 구축할 수 있습니다.  
  
 지금까지 프로덕션 환경에서 가장 큰 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스는 처리 및 쿼리 워크로드가 각각 해당 용도에 최적화되어 전용 하드웨어에서 독립적으로 실행되는 다차원입니다.  테이블 형식 데이터베이스가 이를 빠르게 따라잡고 있으며, DirectQuery의 새로운 발전이 격차를 더욱 해소하도록 도와줍니다.  
  
 다차원의 경우 데이터 저장소 및 쿼리 실행 오프로드는 ROLAP를 통해 사용할 수 있습니다.   쿼리 서버에서 행 집합을 캐시하고 오래된 행 집합을 페이징할 수 있습니다. 메모리 및 디스크 리소스의 효율적이고 균형 있는 사용은 종종 고객을 다차원 솔루션으로 안내합니다.  
  
 부하가 클 때는 Analysis  Services의 데이터 캐싱,  저장,  스캔 및 쿼리에 따라 어느 솔루션 유형이든 디스크 및 메모리 요구 사항이 모두 증가할 수 있습니다. 메모리 페이징 옵션에 대한 자세한 내용은 [Memory Properties](../analysis-services/server-properties/memory-properties.md)을 참조하세요. 크기 조정에 대한 자세한 내용은 [High availability and Scalability in Analysis Services](../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)을 참조하세요.  
  
 PowerPivot for Excel의 인위적인 파일 크기 제한은 2GB입니다. 이러한 크기 제한은 PowerPivot for Excel에서 만든 통합 문서를 SharePoint에 업로드할 수 있도록 보장하기 위해 파일 업로드 크기에 대해 설정된 최대 제한 크기입니다. 독립 실행형 Analysis Services 인스턴스에서 PowerPivot 통합 문서를 테이블 형식 솔루션으로 마이그레이션하는 주요 이유 중 하나는 이러한 파일 크기 제한을 해결하기 위한 것입니다. 최대 파일 업로드 크기를 구성하는 방법에 대한 자세한 내용은 [최대 파일 업로드 크기 구성&#40;SharePoint용 파워 피벗&#41;](../analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md)을 참조하세요.  
  
 **지원되는 데이터 원본**  
  
 다차원 솔루션에서는 OLE DB 기본 및 관리 공급자를 사용하여 관계형 데이터 원본으로부터 데이터를 가져올 수 있습니다.  
  
 테이블 형식 모델은 관계형 데이터 원본, 데이터 피드 및 일부 문서 형식에서 데이터를 가져올 수 있습니다. 테이블 형식에서 ODBC 공급자에 대한 OLE DB를 사용할 수도 있습니다.  
  
 각 모델로 가져올 수 있는 외부 데이터 원본 목록을 보려면 다음 항목을 참조하십시오.  
  
-   [지원되는 데이터 원본&#40;SSAS - 다차원&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
-   [지원되는 데이터 원본&#40;SSAS 테이블 형식&#41;](../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
##  <a name="a-namebkmklanga-query-and-scripting-language-support"></a><a name="bkmk_lang"></a> 쿼리 및 스크립팅 언어 지원  
 Analysis Services에는 MDX, DMX, DAX, XML/A, ASSL 및 TMSL이 포함되어 있습니다. 이러한 언어에 대한 지원은 모델 유형별로 다를 수 있습니다. 쿼리 및 스크립팅 언어 요구 사항을 고려해야 하는 경우 다음 목록을 검토하세요.  
  
-   파워 피벗 통합 문서에서는 계산에 DAX를 사용하고, 쿼리에 DAX 또는 MDX를 사용합니다.  
  
-   테이블 형식 모델 데이터베이스는 DAX 계산, DAX 쿼리 및 MDX 쿼리를 지원합니다. 이는 모든 호환성 수준에서 적용됩니다. 스크립트 언어는 호환성 수준 1050~1103의 경우 ASSL(XMLA)이고, 호환성 수준 1200의 경우 TMSL(XMLA)입니다.  
  
-   다차원 model 데이터베이스는 ASSL뿐만 아니라 MDX  계산 및 MDX  쿼리를 지원합니다.  
  
-   데이터 마이닝 모델은 DMX와 ASSL을 지원합니다.  
  
-   Analysis Services PowerShell은 테이블 형식 및 다차원 모델과 데이터베이스에 지원됩니다.  
  
 모든 데이터베이스는 XML/A를 지원합니다. 자세한 내용은 [쿼리 및 식 언어 참조&#40;Analysis Services&#41;](../Topic/Query%20and%20Expression%20Language%20Reference%20\(Analysis%20Services\).md) 및 [Analysis Services 개발자 설명서](../analysis-services/analysis-services-developer-documentation.md)를 참조하세요.  
  
##  <a name="a-namebkmkseca-security-features"></a><a name="bkmk_sec"></a> 보안 기능  
 모든 Analysis Services 솔루션은 데이터베이스 수준에서 보안이 유지될 수 있습니다. 보다 세부적인 보안 옵션은 모드마다 다릅니다. 세부적인 보안 설정이 솔루션의 요구 사항인 경우 다음 목록을 검토하여 원하는 보안 수준이 작성하려는 솔루션 유형에서 지원되는지 확인하세요.  
  
-   [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 통합 문서는 SharePoint 사용 권한을 통해 파일 수준에서 보안이 유지됩니다.  
  
-   테이블 모델 데이터베이스에서는 Analysis Services의 역할 기반 사용 권한을 통해 행 수준 보안을 사용할 수 있습니다.  
  
-   다차원 데이터베이스에서는 Analysis Services의 역할 기반 사용 권한을 통해 차원 및 셀 수준 보안을 사용할 수 있습니다.  
  
 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 통합 문서는 테이블 형식 모드 서버에 복원될 수 있습니다. 파일이 복원되면 SharePoint에서 분리되므로 행 수준 보안을 비롯하여 모든 테이블 형식 모델링 기능을 사용할 수 있습니다.  
  
##  <a name="a-namebkmkdesignera-design-tools"></a><a name="bkmk_designer"></a> 디자인 도구  
 데이터 모델링 역량 및 기술 전문성은 분석 모델을 작성하는 사용자 간에 크게 다를 수 있습니다. 도구 친숙성 또는 사용자 전문성이 솔루션의 고려 사항인 경우 다음과 같은 모델 생성 환경을 비교하세요.  
  
|모델링 도구|사용 방법|  
|-------------------|--------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|테이블 형식, 다차원 및 데이터 마이닝 솔루션을 만드는 데 사용됩니다. 이 제작 환경에서는 Visual Studio 셸을 사용하여 작업 영역, 속성 창 및 개체 탐색을 제공합니다. Visual Studio를 이미 사용 중인 기술 사용자는 비즈니스 인텔리전스 응용 프로그램을 생성할 때 대부분 이 도구를 선호합니다.|  
|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for Excel|나중에 SharePoint용 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 이 설치된 SharePoint 팜에 배포할 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 통합 문서를 만드는 데 사용됩니다. Excel용 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]에는 Excel에서 열리는 별도의 응용 프로그램 작업 영역이 있습니다. 사용되는 시각적 요소(탭 페이지,  모눈 레이아웃 및 수식 표시줄)는 Excel과 동일합니다. Excel에 능숙한 사용자는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 이 도구를 사용하는 것을 선호할 것입니다.|  
  
##  <a name="a-namebkmkclienta-client-application-support"></a><a name="bkmk_client"></a> 클라이언트 응용 프로그램 지원  
 Reporting  Services를 사용하는 경우 보고서 기능의 가용성은 버전 및 서버 모드에 따라 다릅니다. 따라서 작성하려는 보고서 유형은 설치하려고 선택하는 서버 모드에 영향을 줄 수 있습니다.  
  
 SharePoint에서 실행되는 Reporting Services 제작 도구인 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]는 SharePoint 2010 팜에 배포된 보고서 서버에서 사용할 수 있습니다. 이 보고서에 사용할 수 있는 데이터 원본 유형은 Analysis Services 테이블 형식 데이터베이스 또는 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 통합 문서뿐입니다. 따라서 이 보고서 유형에 사용되는 데이터 원본을 호스팅할 테이블 형식 모드 서버 또는 SharePoint용 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 서버가 있어야 합니다. 다차원 모델은 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 보고서의 데이터 원본으로 사용할 수 없습니다. [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 보고서에 대한 데이터 원본으로 사용하려면 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] BI 의미 체계 모델 연결 또는 Reporting Services 공유 데이터 원본을 만들어야 합니다.  
  
 보고서 작성기 및 보고서 디자이너는 SharePoint용 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 에서 호스트되는 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 통합 문서를 포함하여 모든 Analysis Services 데이터베이스를 사용할 수 있습니다.  
  
 Excel  피벗 테이블 보고서는 모든 Analysis  Services  데이터베이스에서 지원됩니다. Excel 기능은 테이블 형식 데이터베이스를 사용하든 다차원 데이터베이스를 사용하든 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 통합 문서를 사용하든 동일합니다. 단, 쓰기 저장은 다차원 데이터베이스에만 지원됩니다.  
  
 PerformancePoint 대시보드에서는 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 통합 문서를 포함하여 모든 Analysis Services 데이터베이스에 연결할 수 있습니다. 자세한 내용은 [데이터 연결 만들기(PerformancePoint Services)](http://go.microsoft.com/fwlink/?linkdID=218155)를 참조하세요.  
  
##  <a name="a-namebkmkdeploymentmodea-server-deployment-modes-for-multidimensional-and-tabular-solutions"></a><a name="bkmk_deploymentmode"></a> 다차원 및 테이블 형식 솔루션의 서버 배포 모드  
 Analysis Services 인스턴스는 서버의 작업 컨텍스트를 설정하는 세 가지 모드 중 하나로 설치됩니다. 설치하는 서버 모드에 따라 해당 서버에 배포할 수 있는 솔루션 유형이 결정됩니다. 세 모드 간의 가장 큰 차이점은 저장소 및 메모리 아키텍처이지만 그 밖에 다른 차이점도 있습니다. 다음 표에서는 세 가지 서버 모드에 대해 간단히 설명합니다. 자세한 내용은 [Analysis Services 인스턴스의 서버 모드 확인](../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)을 참조하세요.  
  
|배포 모드|설명|  
|---------------------|-----------------|  
|0 - 다차원 및 데이터 마이닝|Analysis Services의 기본 인스턴스에 배포하는 다차원 및 데이터 마이닝 솔루션을 실행합니다. 배포 모드 0은 Analysis  Services  설치의 기본값입니다.|  
|1 - SharePoint용 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]|[!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 데이터 액세스에서 Analysis Services는 SharePoint용 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 설치의 내부 구성 요소입니다. Analysis Services는 배포 모드 1에 설치되며 SharePoint 환경에서 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 서비스에 의해 배타적으로 사용됩니다.|  
|2 - 테이블 형식|배포 모드 2로 구성된 Analysis Services의 독립 실행형 인스턴스에서 테이블 형식 솔루션을 실행합니다.|  
  
 자세한 내용은 [Analysis Services 설치](../analysis-services/instances/install-windows/install-analysis-services.md)를 참조하세요.  
  
##  <a name="a-namebkmksharepointa-sharepoint-requirements"></a><a name="bkmk_sharePoint"></a> SharePoint 요구 사항  
 SQL Server는 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 데이터 액세스 및 테이블 형식 데이터 액세스를 위한 지원을 추가하여 SharePoint와 통합됩니다. 각 제품에 사용된 기능 수를 극대화하면 SharePoint  및 SQL  Server  통합에 대한 투자가 늘어납니다. SharePoint가 있으면 SharePoint용 SQL Server [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 을 설치하여 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 데이터 액세스를 지원하고 네트워크 서버의 외부 Analysis Services 인스턴스에서 실행되는 테이블 형식 데이터베이스에 액세스하는 데 사용되는 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] .bism 연결 파일을 가져올 수 있습니다.  
  
 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 및 테이블 형식 데이터베이스를 데이터 원본으로 사용하는 파워 뷰 보고는 SQL Server에서 제공되는 SharePoint 기능과 Excel의 기본 제공 기능입니다. 테이블 형식 데이터베이스가 SharePoint  외부의 Analysis  Services  인스턴스에서 실행되지만 데이터는 SharePoint에서 실행되는 Power  View  보고서에서 소비됩니다.  
  
 SharePoint를 사용하지 않을 경우에도 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for Excel을 사용하여 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 통합 문서를 작성할 수 있지만 응집력이 있는 데이터 시각화 환경을 얻을 수 없습니다. 통합 문서를 사용하는 각각의 사용자가 슬라이서, 필터 및 피벗을 사용한 데이터 상호 작용 및 탐색 기능을 이용하기 위해서는 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] for Excel 추가 기능을 사용하여 Excel에서 각 통합 문서를 다운로드하고 확인해야 합니다. 그렇지 않으면 통합 문서를 열었을 때 표시된 대로 통합 문서 시각화가 정적 데이터로 제한됩니다.  
  
 테이블 형식, 다차원 및 데이터 마이닝 솔루션은 SharePoint에 대한 종속성 없이 네트워크의 Analysis Services 인스턴스에서 실행됩니다.  
  
##  <a name="a-namebkmkexta-programmability-and-extensibility-support"></a><a name="bkmk_ext"></a> 프로그래밍 기능 및 확장성 지원  
 Power BI에 대한 개발자 지원은 있지만 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 통합 문서에 대한 개발 지원은 없습니다. [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 통합 문서를 사용하는 경우 기본 제공 클라이언트 및 서버 응용 프로그램을 솔루션의 일부로 사용해야 합니다. Excel  프로그래밍 및 SharePoint  프로그래밍은 옵션일 뿐입니다.  
  
 Power BI에 대한 자세한 내용은 [Power BI 포함](https://azure.microsoft.com/services/power-bi-embedded/)을 참조하세요.  
  
 테이블 형식 솔루션은 솔루션당 model.bim  파일을 하나만 지원합니다.  즉,  모든 작업을 단일 파일에서 수행해야 합니다. 단일 솔루션에서 여러 프로젝트를 작업하는 데 익숙한 개발 팀의 경우 공유 테이블 형식 솔루션을 빌드할 때 작업 방식을 수정할 필요가 있을 수 있습니다.  
  
 호환성 수준 1200의 테이블 형식 솔루션은 테이블 형식 메타데이터를 사용하는 새 개체 모델에 매핑됩니다. 이전 테이블 형식 및 모든 다차원 모델에서는 다차원 메타데이터를 설명자로 사용합니다. 사용자 지정 코드 및 스크립트에 AMO의 테이블 형식 네임스페이스를 사용할 수 있도록 이전 테이블 형식 모델을 1200 호환성 수준으로 업그레이드 하는 것이 좋습니다.  
  
 자세한 내용은 [Analysis Services 개발자 설명서](https://msdn.microsoft.com/library/bb500153.aspx) 를 참조하세요.  
  
##  <a name="a-namebkmknexta-next-step-build-a-solution"></a><a name="bkmk_Next"></a> 다음 단계: 솔루션 빌드  
 각 솔루션의 비교 방법에 대한 기본적인 이해를 마쳤으므로, 다음 자습서를 통해 각 솔루션을 작성하는 단계를 배워 보시기 바랍니다. 다음 링크는 각 단계를 설명하는 자습서로 이어집니다.  
  
-   [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 모델을 빌드합니다. [Microsoft Excel에서 Power Pivot 시작](https://support.office.com/article/Get-started-with-Power-Pivot-in-Microsoft-Excel-fdfcf944-7876-424a-8437-1a6c1043a80b)을 참조하세요.  
  
-   테이블 형식 모델을 빌드합니다. [테이블 형식 모델링&#40;Adventure Works 자습서&#41;](../analysis-services/tabular-modeling-adventure-works-tutorial.md)을 참조하세요.  
  
-   다차원 모델을 빌드합니다. [다차원 모델링&#40;Adventure Works 자습서&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)을 참조하세요.  
  
-   데이터 마이닝 모델을 구축합니다. [기본 데이터 마이닝 자습서](../Topic/Basic%20Data%20Mining%20Tutorial.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 인스턴스 관리](../analysis-services/instances/analysis-services-instance-management.md)   
 [Analysis Services의 새로운 기능](../analysis-services/what-s-new-in-analysis-services.md)     
 [파워 피벗의 새로운 기능](http://go.microsoft.com/fwlink/?LinkId=238141)   
 [파워 피벗 BI 의미 체계 모델 연결&#40;.bism&#41;](../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [공유 데이터 원본 만들기 및 관리&#40;SharePoint 통합 모드의 Reporting Services&#41;](../Topic/Create%20and%20Manage%20Shared%20Data%20Sources%20\(Reporting%20Services%20in%20SharePoint%20Integrated%20Mode\).md)  
  
  