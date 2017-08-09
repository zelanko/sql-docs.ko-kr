---
title: "외부 데이터 소스에서 데이터 추가(SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 924a2ec3-150c-4bb2-83c9-4c7b440e8c03
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 76e09d1f90d7eb2f3d91aef60e4ce2a9c671ab13
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="add-data-from-external-data-sources-ssrs"></a>외부 데이터 원본의 데이터 추가(SSRS)
  외부 데이터 원본에서 데이터를 검색하려면 데이터 연결을 사용합니다. 일반적으로 데이터 연결 정보는 사용 권한을 부여하고 사용할 자격 증명 유형을 지정하는 외부 데이터 원본의 소유자가 제공합니다. 데이터 연결 정보는 보고서 데이터 원본으로 저장됩니다. 데이터 원본 유형에 따라 데이터를 검색하는 데 사용할 데이터 확장 프로그램이 결정됩니다.  
  
 데이터 원본 유형에 대한 자세한 내용은 [섹션 내용](#InThisSection)을 참조하십시오.  
  
##  <a name="DataAccess"></a> 데이터 액세스 기술 이해  
 보고서 데이터 집합의 데이터를 검색하려면 여러 계층의 데이터 액세스 소프트웨어가 필요합니다. 다음 목록에서는 보고서에서 데이터 액세스 기술을 사용하는 방법을 간략하게 설명합니다.  
  
-   **응용 프로그램 및 사용자 인터페이스** 데이터 원본을 만들거나, 공유 데이터 원본에 대한 참조를 추가하거나, 공유 데이터 집합을 추가하거나, 자신이 종속된 데이터 원본과 데이터 집합을 포함하는 보고서 파트를 추가하는 데 사용되는 보고서 작성기 응용 프로그램입니다.  
  
-   **보고서 정의 요소** 데이터 원본과 데이터 집합은 보고서 정의의 일부입니다. 보고서 서버에 보고서를 게시하고 나면 공유 데이터 원본과 공유 데이터 집합이 보고서 정의와 독립적으로 관리됩니다.  
  
    -   **데이터 원본 및 공유 데이터 원본** 데이터 처리 확장 프로그램, 연결 정보 및 인증의 유형에 대한 정보를 포함하는 보고서 정의의 일부입니다.  
  
    -   **데이터 집합 및 필드 컬렉션** 쿼리, 필드 컬렉션 및 필드 데이터 유형을 포함하는 보고서 정의의 일부입니다.  
  
-   **Reporting Services 데이터 확장 프로그램** 보고서 작성기와 함께 설치되는 기본 제공 데이터 확장 프로그램입니다. 데이터 확장 프로그램은 인증, 서버 집계 및 다중 값 매개 변수를 처리하는 기능을 제공합니다.  
  
-   **데이터 공급자** 외부 데이터 원본의 데이터에 대한 연결 및 검색을 관리하는 소프트웨어입니다. 데이터 공급자는 연결 문자열 구문을 정의합니다. 대부분의 데이터 확장 프로그램은 데이터 공급자 계층 위에 빌드됩니다.  
  
-   **외부 데이터 원본** 보고서 데이터를 검색할 대상 위치(예: 데이터베이스, 파일, 큐브 또는 웹 서비스)입니다.  
  
> [!NOTE]  
>  보고서 서버에 연결되어 있지 않을 때는 보고서 작성기와 함께 설치되는 데이터 확장 프로그램에서 선택할 수 있습니다. 이 경우 컴퓨터의 자격 증명을 사용하여 단일 사용자로 데이터에 액세스합니다. 보고서 서버에 연결되어 있을 때는 보고서 서버에 설치되는 데이터 확장 프로그램에서 선택할 수 있습니다. 이 경우 보고서를 실행하는 여러 사용자 중 한 명으로 데이터에 액세스하고 보고서 서버의 자격 증명을 사용합니다. 자세한 내용은 [보고서 작성기에 자격 증명 지정](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)을 참조하세요.  
  
##  <a name="ReportData"></a> 보고서 데이터 이해  
 가장 단순한 형태의 보고서는 보고서 페이지의 데이터 영역(예: 단일 테이블, 차트, 행렬 등)에 보고서 데이터 집합의 데이터를 표시합니다. 보고서 데이터 집합의 데이터는 외부 데이터 원본에 대한 읽기 전용 액세스를 통해 실행되는 단일 쿼리 명령이 반환하는 첫 번째 결과 집합에서 제공됩니다. 각 데이터 영역은 데이터 집합의 모든 데이터가 표시되도록 확장됩니다.  
  
 기본적으로 데이터 집합의 데이터는 테이블 형식으로 되어 있습니다. 열은 데이터 집합 쿼리에서 가져온 필드이고 행은 결과 집합의 행에서 가져옵니다. 다음과 같은 일반화된 형식의 데이터를 보고서에서 사용할 수 있습니다.  
  
-   사각형 데이터. 모든 행에 동일한 수의 열이 있는 결과 집합에서 가져온 데이터입니다.  
  
-   일반 행 집합으로 지원되는 계층적 데이터  
  
    -   각 데이터 행에 서로 다른 수의 열이 있는 비정형 계층은 지원되지 않습니다. 일부 데이터 확장 프로그램의 경우 이로 인해 약간의 영향을 받습니다.  
  
    -   다차원 데이터 원본을 처리하는 데이터 확장 프로그램은 XML for Analysis 프로토콜을 사용하여 셀 집합이 아닌 일반 행 집합으로 데이터를 검색합니다.  
  
    -   XML 데이터 확장 프로그램은 보고서에서 사용할 수 있도록 XML 데이터를 자동으로 일반화합니다. XML 요소의 첫 번째 인스턴스에 특성 또는 하위 요소가 모두 포함되어 있지 않은 경우에는 데이터를 보고서 데이터로 사용하지 못할 수 있습니다.  
  
-   재귀적 데이터. 재귀적 데이터 계층을 포함하는 결과 집합에는 사각형 결과 집합의 계층 구조에 대한 모든 정보가 포함됩니다. 예를 들어 직원과 관리자라는 두 개의 열이 있는 테이블로 회사의 보고 구조를 나타낼 수 있습니다. 각 관리자도 마찬가지로 관리자가 있는 직원입니다. 일반적으로 최고 관리자 열에는 null이나 관리자가 없는 직원임을 나타내는 다른 특별한 식별자가 포함됩니다.  
  
  
##  <a name="DataTypes"></a> 데이터 형식 사용  
 데이터 집합을 만들 때 필드의 데이터 형식이 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에서 CLR(공용 언어 런타임) 데이터 형식의 하위 집합으로 매핑됩니다. 명확하게 매핑될 수 없는 데이터 형식은 문자열로 반환됩니다. 필드 데이터 형식 작업에 대한 자세한 내용은 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)을 참조하십시오. 매개 변수를 만들 때 데이터 형식은 지원되는 보고서 정의 데이터 형식이어야 합니다. 데이터 공급자에서 보고서 매개 변수로 데이터 형식을 매핑하는 방법은 [식의 데이터 형식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
  
##  <a name="HowTo"></a> 방법 도움말 항목  
 이 섹션에서는 데이터 연결, 데이터 원본 및 데이터 집합을 사용하는 방법을 단계별로 설명합니다.  
  
 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [공유 데이터 집합 또는 포함된 데이터 집합 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [데이터 집합에 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="InThisSection"></a> 섹션 내용  
 다음 항목에서는 각 기본 제공 데이터 확장 프로그램에 대한 정보를 제공합니다.  
  
|항목|데이터 원본 유형|  
|-----------|----------------------|  
|[SQL Server 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|[MDX용 Analysis Services 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[파워 피벗 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/power-pivot-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[SharePoint 목록 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/sharepoint-list-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 목록|  
|[SQL Azure 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/sql-azure-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|[SQL Server 병렬 데이터 웨어하우스 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|  
|[SAP NetWeaver BI 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/sap-netweaver-bi-connection-type-ssrs.md)|SAP NetWeaver BI|  
|[Hyperion Essbase 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/hyperion-essbase-connection-type-ssrs.md)|Hyperion Essbase|  
|[OLE DB 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)|OLE DB|  
|[ODBC 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/odbc-connection-type-ssrs.md)|ODBC|  
|[XML 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)|XML|  
|[보고서 모델 연결&#40;SSRS&#41;](../../reporting-services/report-data/report-model-connection-ssrs.md)|.smdl 모델|  
  
  
##  <a name="Related"></a> 관련 단원  
 설명서의 다음 섹션에서는 보고서 데이터에 대한 깊이 있는 개념 정보를 제공하며, 데이터와 관련된 보고서 부분을 정의, 사용자 지정 및 사용하는 방법을 절차적인 측면에서 소개합니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[보고서 데이터 집합&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)|보고서의 데이터 액세스에 대한 개요를 제공합니다.|  
|[보고서 작성기의 데이터 연결, 데이터 원본 및 연결 문자열](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)|데이터 연결 및 데이터 원본에 대한 정보를 제공합니다.|  
|[보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|포함된 데이터 집합 및 공유 데이터 집합에 대한 정보를 제공합니다.|  
|[데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)|쿼리에 의해 생성되는 데이터 집합 필드 컬렉션에 대한 정보를 제공합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)에 있는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서의 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).|각 데이터 확장 프로그램의 플랫폼 및 버전 지원에 대한 자세한 정보를 제공합니다.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [온라인 설명서](http://go.microsoft.com/fwlink/?linkid=121312)의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 설명서에서 [데이터 처리 확장 프로그램 개요](../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)를 참조하세요.|고급 사용자를 위해 데이터 확장 프로그램에 대한 자세한 정보를 제공합니다.|  
  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 데이터 집합&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [쿼리 디자이너&#40;보고서 작성기&#41;](http://msdn.microsoft.com/library/553f0d4e-8b1d-4148-9321-8b41a1e8e1b9)  
  
  
