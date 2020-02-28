---
title: MDX용 Analysis Services 연결 형식 | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: bd2e7148-3124-4e07-9734-22333127c3be
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: eff17f770599ae953afeaae81779f0326ad89e4c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081832"
---
# <a name="analysis-services-connection-type-for-mdx-ssrs"></a>MDX용 Analysis Services 연결 형식(SSRS)
  보고서에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브의 데이터를 포함하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]형식의 보고서 데이터 원본을 기반으로 하는 데이터 세트가 있어야 합니다. 이 기본 제공 데이터 원본 형식은 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 확장 프로그램을 기반으로 합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브에서 보고서 데이터로 사용할 차원, 계층, 수준, KPI(핵심 성과 지표), 측정값 및 특성에 대한 메타데이터를 검색할 수 있습니다.  
  
 이 데이터 처리 확장 프로그램은 연결 문자열과 별개로 관리되는 다중값 매개 변수, 서버 집계 및 자격 증명을 지원합니다.  
  
 이 항목의 정보를 사용하여 데이터 원본을 작성할 수 있습니다. 단계별 지침은 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="Connection"></a> 연결 문자열  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브에 연결할 때는 서버에 있는 Analysis Services 인스턴스의 데이터베이스 개체에 연결하게 됩니다. 데이터베이스에는 큐브가 여러 개 있을 수 있으므로 쿼리를 작성할 때 쿼리 디자이너에서 큐브를 지정합니다. 다음 예에서는 연결 문자열을 보여 줍니다.  
  
```  
data source=<server name>;initial catalog=<database name>  
```  
  
 연결 문자열 예제는 [데이터 연결 문자열 만들기 - 보고서 작성기 및 SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)를 참조하세요.  
  
  
##  <a name="Credentials"></a> 자격 증명  
 쿼리를 실행하거나 보고서를 로컬로 미리 보거나 보고서 서버의 보고서를 미리 보려면 자격 증명이 필요합니다.  
  
 보고서를 게시한 후 보고서를 보고서 서버에서 실행할 때 데이터를 검색할 수 있는 권한이 유효하도록 데이터 원본에 대한 자격 증명을 변경해야 할 수도 있습니다.  
  
 보고서 작성 클라이언트에서는 다음 옵션을 사용하여 자격 증명을 지정할 수 있습니다.  
  
-   현재 Windows 사용자(통합 보안)  
  
-   저장된 사용자 이름 및 암호 사용.  
  
-   사용자에게 자격 증명을 입력하도록 메시지 표시 이 옵션은 Windows 통합 보안만 지원합니다.  
  
-   자격 증명 필요 없음. 이 옵션을 사용하려면 보고서 서버에서 무인 실행 계정을 구성해야 합니다. 자세한 내용은 [무인 실행 계정 구성&#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)를 참조하세요.
  
 자세한 내용은 [데이터 연결 문자열 만들기 - 보고서 작성기 및 SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 또는 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](specify-credential-and-connection-information-for-report-data-sources.md)을 참조하세요.  
  
  
##  <a name="Query"></a> 쿼리  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본에 데이터를 연결한 후에는 데이터 세트를 만들고 큐브에서 검색할 데이터를 지정하는 MDX(Multidimensional Expression) 쿼리를 정의합니다. MDX 그래픽 쿼리 디자이너를 사용하여 데이터 원본의 기본 데이터 구조를 찾아보고 선택할 수 있습니다.  
  
 다음과 같은 방법으로 쿼리를 지정할 수 있습니다.  
  
-   대화식으로 쿼리를 작성합니다. Analysis Services MDX 쿼리 디자이너에서는 다음과 같은 뷰를 지원합니다.  
  
    -   **디자인 뷰** 차원, 멤버, 멤버 속성, 측정값 및 KPI를 메타데이터 브라우저에서 **데이터** 창으로 끌어서 MDX 쿼리를 작성합니다. 추가 데이터 세트 필드를 정의하려면 계산 멤버 창의 계산 멤버를 데이터 창으로 끕니다.  
  
    -   **쿼리 뷰** 차원, 멤버, 멤버 속성, 측정값 및 KPI를 메타데이터 브라우저에서 쿼리 창으로 끌어서 MDX 쿼리를 작성합니다. 그런 다음 쿼리 창에서 직접 MDX 텍스트를 편집할 수 있습니다. 추가 데이터 세트 필드를 정의하려면 계산 멤버 창의 계산 멤버를 쿼리 창으로 끕니다.  
  
     자세한 내용은 [Analysis Services MDX 쿼리 디자이너 사용자 인터페이스&#40;보고서 작성기&#41;](../../reporting-services/report-data/analysis-services-mdx-query-designer-user-interface.md)를 참조하세요.  
  
-   보고서에서 기존 MDX 쿼리를 가져옵니다. **쿼리 가져오기** 단추를 사용하여 .rdl 파일을 찾아서 쿼리를 가져옵니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본을 기반으로 하는 포함된 데이터 세트가 들어 있는 보고서에서 쿼리를 가져올 수 있습니다. .mdx 파일에서 MDX 쿼리를 직접 가져올 수는 없습니다.  
  
 디자인 타임에 쿼리를 실행하여 결과 집합을 확인합니다. 쿼리 결과는 자동으로 일반 행 집합으로 검색됩니다. 쿼리 결과 집합의 열은 데이터 세트의 필드 컬렉션을 채웁니다. 쿼리를 작성한 후 메타데이터에서 생성되는 데이터 세트 필드 컬렉션을 보고서 데이터 창에서 확인합니다. 보고서를 실행하면 외부 데이터 원본에서 실제 데이터가 반환됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 처리 확장 프로그램은 확장 데이터 세트 필드 속성을 지원합니다. 이러한 속성은 외부 데이터 원본에서 사용할 수 있지만 보고서 데이터 창에 표시되지 않는 값입니다. 기본 제공 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Fields **컬렉션을 통해** 데이터 처리 확장 프로그램이 지원하는 확장 필드 속성을 보고서에 사용할 수 있습니다. 데이터 원본에 값이 있는 속성의 경우 **FormattedValue**, **Color**또는 **UniqueName**과 같은 미리 정의된 속성 값에 액세스할 수 있습니다. 자세한 내용은 msdn.microsoft.com의 [Analysis Services 데이터베이스에 대한 확장 필드 속성&#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)을 참조하세요.  
  
  
##  <a name="Parameters"></a> 매개 변수  
 쿼리 매개 변수를 포함하려면 쿼리 디자이너에서 필터 영역에 필터를 만들고 필터를 매개 변수로 표시합니다. 각 필터에 대해 데이터 세트가 자동으로 생성되어 사용 가능한 값을 제공합니다. 기본적으로 이러한 데이터 세트는 보고서 데이터 창에 나타나지 않습니다. 자세한 내용은 [Analysis Services용 MDX 쿼리 디자이너에서 매개 변수 정의&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md) 및 [다차원 데이터의 매개 변수 값에 대해 숨겨진 데이터 세트 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/show-hidden-datasets-for-parameter-values-multidimensional-data.md)을 참조하세요.  
  
 기본적으로 각 보고서 매개 변수의 데이터 형식은 **Text**입니다. 보고서 매개 변수가 만들어진 후에는 기본값을 변경해야 할 수 있습니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)에 대해 자세히 알아봅니다.  
  
  
##  <a name="Remarks"></a> 주의  
 Analysis Services 데이터 확장 프로그램은 XMLA(XML for Analysis) 프로토콜을 기반으로 합니다. 큐브의 결과 집합은 XMLA 프로토콜을 통해 플랫 행 집합으로 검색됩니다. 비정형 계층은 지원되지 않습니다. 자세한 내용은 [비정형 계층 구조](https://docs.microsoft.com/analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies)를 참조하세요.  
  
 OLE DB 데이터 원본 유형에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 큐브의 데이터를 검색할 수도 있습니다. 자세한 내용은 [OLE DB 연결 형식&#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)을 참조하세요.  
  
 버전 지원에 대한 자세한 내용은 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)을 참조하세요.  
  
  
##  <a name="Related"></a> 관련 단원  
 설명서의 다음 섹션에서는 보고서 데이터에 대한 깊이 있는 개념 정보를 제공하며, 데이터와 관련된 보고서 부분을 정의, 사용자 지정 및 사용하는 방법을 절차적인 측면에서 소개합니다.  
  
 [보고서 데이터 세트&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 보고서의 데이터 액세스에 대한 개요를 제공합니다.  
  
 [데이터 연결 문자열 만들기 - 보고서 작성기 및 SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
 데이터 연결 및 데이터 원본에 대한 정보를 제공합니다.  
  
 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 포함된 데이터 세트 및 공유 데이터 세트에 대한 정보를 제공합니다.  
  
 [데이터 세트 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 쿼리에 의해 생성되는 데이터 세트 필드 컬렉션에 대한 정보를 제공합니다.  
  
 [Analysis Services 데이터베이스에 대한 확장 필드 속성&#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)  
 XMLA 데이터 공급자를 통해 사용할 수 있는 추가 필드에 대한 정보를 제공합니다.  
  
 [Reporting Services&#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
 각 데이터 확장 프로그램의 플랫폼 및 버전 지원에 대한 자세한 정보를 제공합니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
