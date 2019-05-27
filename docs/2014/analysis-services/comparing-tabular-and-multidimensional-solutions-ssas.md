---
title: 테이블 형식 및 다차원 솔루션 (SSAS) 비교 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 76ee5e96-6a04-49af-a88e-cb5fe29f2e9a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1da4224387e70ccc76e069aa3ce411dddb79b805
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66087767"
---
# <a name="comparing-tabular-and-multidimensional-solutions-ssas"></a>테이블 형식 및 다차원 솔루션(SSAS) 비교
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터 모델링에 대 한 두 가지 고유한 방법을 제공 합니다: 테이블 형식 및 다차원입니다. 두 방식 간에 중요한 공통점이 있지만 작업 진행 방식을 어떻게 결정할지에 영향을 미치는 중요한 차이점도 있습니다. 이 항목에서는 기능을 비교하고 각 접근 방식이 일반적인 프로젝트 요구 사항을 해결하는 방법을 설명합니다. 예를 들어 특정 데이터 원본을 지원하는 것이 가장 중요하게 고려되는 경우 데이터 원본에 대한 섹션이 사용할 모델링 방법을 결정하는 데 도움이 될 수 있습니다.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
-   [Analysis Services의 모델링 개요](#bkmk_overview)  
  
-   [솔루션 유형별 데이터 원본 지원](#bkmk_ds)  
  
-   [모델 기능](#bkmk_models)  
  
-   [모델 크기](#bkmk_modelsize)  
  
-   [프로그래밍 기능 및 개발자 환경](#bkmk_ext)  
  
-   [쿼리 및 스크립팅 언어 지원](#bkmk_lang)  
  
-   [보안 기능 지원](#bkmk_sec)  
  
-   [디자인 도구](#bkmk_designer)  
  
-   [클라이언트 및 보고 응용 프로그램](#bkmk_client)  
  
-   [호스팅 플랫폼](#bkmk_sharePoint)  
  
-   [다차원 및 테이블 형식 솔루션에 대 한 서버 배포 모드](#bkmk_deploymentmode)  
  
-   [다음 단계: 솔루션 빌드](#bkmk_Next)  
  
 추가 정보는 MSDN의 다음 기술 문서에서 확인할 수 있습니다. [SQL Server 2012 Analysis Services에서 테이블 형식 또는 다차원 모델링 환경 선택](https://go.microsoft.com/fwlink/?LinkId=251588)합니다.  
  
##  <a name="bkmk_overview"></a> Analysis Services의 모델링 개요  
 Analysis Services는 모델 개발 환경을 제공하며 Analysis Services 인스턴스의 데이터베이스 호스팅을 통한 모델 배포도 지원합니다. 모델 형식에는 테이블 형식 및 다차원 형식이 포함됩니다. 예상할 수 있는 것처럼 데이터베이스 호스팅은 사용자가 만드는 테이블 형식 및 다차원 솔루션을 지원하지만 SharePoint용 PowerPivot도 포함합니다.  
  
 SharePoint용 PowerPivot은 *SharePoint 모드의 Analysis Services*입니다. 이 모드에서 Analysis Services는 SharePoint의 부속 서비스로 작동하여 이전에 Excel에서 만든 다음 SharePoint에 저장한 Excel 데이터 모델을 호스트하고 관리하도록 지원합니다. 이 컨텍스트에서 Analysis Services의 역할은 데이터 모델을 메모리에 로드하고, 외부 데이터 원본에서 데이터를 새로 고치고, 모델에 대해 쿼리를 실행하는 것입니다. 이 구성에서는 Analysis Services가 백그라운드에서 작동합니다. Analysis Services에 대한 모든 연결과 요청은 SharePoint에서 수행하며, Excel 통합 문서에 데이터 모델이 포함되었을 때만 이러한 연결과 요청이 수행됩니다(Excel 통합 문서에서는 데이터 모델이 선택 사항임). Excel에서 데이터 모델을 작성 하 고 SharePoint에 호스팅하 맞춥니다. 프로젝트 요구 사항, 참조 [파워 피벗: 강력한 데이터 분석 및 Excel에서 데이터 모델링](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b) 하 고 [PowerPivot for SharePoint &#40;SSAS&#41; ](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md) 에 대 한 자세한 내용은 합니다.  
  
> [!NOTE]  
>  Excel 데이터 모델 및 테이블 형식 모델은 구조적 측면에서 비슷합니다. 더 많은 양의 데이터를 지원하거나 Excel에서 사용할 수 없는 다른 모델 기능을 사용해야 하는 경우 Excel 데이터 모델을 테이블 형식 모델로 가져올 수 있습니다.  
  
 테이블 형식 및 다차원 솔루션은 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 를 통해 구축되었으며, 독립 실행형 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에서 실행되는 기업 BI 프로젝트에 사용됩니다. 두 솔루션 모두 Excel, Reporting Services 보고서 및 기타 Microsoft 및 타사 애플리케이션의 BI 애플리케이션과 쉽게 통합되는 고성능 분석 데이터베이스를 제공합니다. 두 솔루션 모두 Analysis Services를 지원하는 모든 클라이언트 애플리케이션에서 사용할 수 있는 독립 실행형 데이터베이스를 구현합니다.  
  
 테이블 형식 및 다차원 모델 간의 차이점을 다음과 같이 좀 더 자세히 설명할 수 있습니다.  
  
-   다차원 및 데이터 마이닝 솔루션은 디스크를 미리 집계된 데이터에 대한 기본 데이터 스토리지로 사용하는 OLAP 모델링 구문(큐브 및 차원)과 MOLAP, ROLAP 또는 HOLAP 스토리지를 사용합니다.  
  
-   테이블 형식 솔루션의 경우 데이터 모델링을 위해 테이블 및 관계와 같은 관계형 모델링 구문을 사용하고, 데이터 저장 및 계산을 위해서는 메모리 내 분석 엔진을 사용합니다. 모든 그런 것은 아니지만 대부분의 모델은 RAM에 저장되며 다차원 방식의 모델보다 훨씬 더 빠릅니다.  
  
 새 프로젝트의 경우에는 먼저 테이블 형식 접근 방식을 고려해보세요. 테이블 형식은 설계, 테스트 및 배포 속도가 빠르고, Microsoft에서 제공되는 최신의 셀프 서비스 BI 애플리케이션과의 효율성도 뛰어납니다.  
  
##  <a name="bkmk_ds"></a> 솔루션 유형별 데이터 원본 지원  
 다차원 및 테이블 형식 모델은 외부 원본에서 가져온 데이터를 사용합니다. 대부분의 개발자는 보고 데이터 구조를 지원하도록 설계된 데이터 웨어하우스를 모델의 기본 데이터 원본으로 사용합니다. 데이터 웨어하우스는 별모양 또는 눈송이 스키마에 주로 기반 및 SSIS는 OLTP 솔루션에서 데이터 웨어하우스로 데이터를 로드하는 데 사용됩니다. 모델링은 데이터 웨어하우스를 백엔드 데이터 원본으로 사용하는 경우에 더 간단합니다.  
  
|**링크**|**지원 되는 옵션 요약**|  
|--------------|--------------------------------------|  
|[지원 되는 데이터 원본 &#40;SSAS 다차원&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)|다차원 모델은 관계형 데이터 원본의 데이터를 사용합니다.|  
|[지원되는 데이터 원본&#40;SSAS 테이블 형식&#41;](tabular-models/data-sources-supported-ssas-tabular.md)|테이블 형식 모델은 ODBC 데이터 공급자를 통해 액세스할 수 있는 데이터 원본, 플랫 파일 및 데이터 피드를 비롯한 다양한 데이터 원본을 지원합니다.|  
  
 두 모델링 방법 모두 동일한 모델의 여러 데이터 원본에서 가져온 데이터를 사용할 수 있습니다.  
  
 솔루션이 관계형 데이터베이스에 모델 외부의 모델 데이터를 저장할 것을 요구하는 경우(데이터 크기 요구 사항이 특히 클 때 사용되는 기술) 데이터 원본 유형이 SQL Server 관계형 데이터베이스여야 합니다. 다차원 모델에 대한 ROLAP 스토리지와 테이블 형식 모델에 대한 DirectQuery 둘 다에 이러한 요구 사항이 적용됩니다.  
  
 **데이터 크기**  
  
 테이블 형식 및 다차원 솔루션 모두에는 데이터를 가져오는 데이터 웨어하우스에 비해 Analysis Services 데이터베이스 크기를 줄여 주는 데이터 압축 기술이 사용됩니다. 실제 압축 비율은 기본 데이터의 특성에 따라 크게 달라지기 때문에 쿼리에서 데이터를 처리하고 사용한 후에 솔루션에 필요한 디스크 및 메모리의 양은 정확하게 예측할 수는 없습니다. 여러 Analysis Services 개발자들은 일반적으로 다차원 데이터베이스에 필요한 기본 스토리지 크기를 원본 데이터 크기의 1/3 정도로 예상합니다.  
  
 테이블 형식 데이터베이스에서는 대부분의 데이터가 사실 값 데이터로부터 가져온 데이터인 경우 특히 압축 효율을 1/10까지 높일 수 있습니다. 테이블 형식의 경우 테이블 형식 데이터베이스를 메모리에 로드할 때 발생하는 추가적인 데이터 구조로 인해 메모리 요구 사항이 디스크 상의 데이터 크기보다 큽니다. 부하가 클 때는 Analysis Services의 캐시, 저장, 스캔 및 쿼리에 따라 어느 솔루션 유형이든 디스크 및 메모리 요구 사항이 모두 증가할 수 있습니다.  
  
 일부 프로젝트의 경우 데이터 요구 사항이 너무 커서 두 모델 유형 간의 중요한 선택 기준이 될 수 있습니다. 로드해야 하는 데이터 크기가 수 테라바이트에 달하는 경우, 가용 메모리로 해당 데이터를 수용할 수 없기 때문에 테이블 형식 솔루션으로는 요구 사항을 충족하지 못할 수 있습니다. 메모리 내 데이터를 디스크로 스왑하는 페이징 옵션이 있지만 매우 큰 데이터 용량은 다차원 솔루션을 이용하는 것이 더 좋습니다. 현재 운용 환경에 사용되는 가장 큰 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스는 다차원 방식입니다. 테이블 형식 솔루션의 메모리 페이징 옵션에 대한 자세한 내용은 [Memory Properties](server-properties/memory-properties.md)을 참조하세요. 다차원 솔루션의 확장에 대한 자세한 내용은 [읽기 전용 데이터베이스로 Analysis Services의 쿼리 확장](https://go.microsoft.com/fwlink/?LinkId=251711)을 참조하세요.  
  
##  <a name="bkmk_models"></a> 모델 기능  
 다음 표에는 모델 수준에서의 기능 가용성이 요약되어 있습니다. Analysis Services를 이미 설치한 경우 이 정보를 사용하여 설치한 서버 모드의 기능을 이해할 수 있습니다. Analysis Services의 모델 기능에 이미 익숙하고 비즈니스 요구 사항에 이러한 기능 중 하나 이상이 포함되어 있는 경우 이 목록을 검토하여 사용할 기능을 작성하려는 유형의 모델에서 사용할 수 있는지 확인할 수 있습니다.  
  
 모델링 접근 방법에 따른 기능 비교에 대한 자세한 내용은 MSDN의 [SQL Server 2012 Analysis Services에서 테이블 형식 또는 다차원 모델링 환경 선택](https://go.microsoft.com/fwlink/?LinkId=251588) 기술 문서를 참조하세요.  
  
> [!NOTE]  
>  테이블 형식 모델링은 특정 버전의 SQL Server에서 지원됩니다. 자세한 내용은 [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조하세요.  
  
||||  
|-|-|-|  
||**다차원**|**테이블 형식**|  
|동작|[예](multidimensional-models/actions-in-multidimensional-models.md)|아니요|  
|집계 개체|[예](multidimensional-models/designing-aggregations-analysis-services-multidimensional.md)|아니요|  
|계산 측정값|[예](multidimensional-models/create-calculated-members.md)|사용자 계정 컨트롤|  
|사용자 지정 어셈블리|[예](multidimensional-models/multidimensional-model-assemblies-management.md)|아니요|  
|사용자 지정 롤업|사용자 계정 컨트롤|아니요|  
|Distinct Count|[예](multidimensional-models/use-aggregate-functions.md)|예 (DAX를 통해) *|  
|드릴스루|[예](multidimensional-models/actions-in-multidimensional-models.md)|사용자 계정 컨트롤|  
|계층 구조|[예](multidimensional-models/user-defined-hierarchies-create.md)|사용자 계정 컨트롤|  
|KPI|[예](multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)|사용자 계정 컨트롤|  
|연결된 측정값 그룹|[예](multidimensional-models/linked-measure-groups.md)|아니요|  
|다 대 다 관계|[예](multidimensional-models/define-a-many-to-many-relationship-and-many-to-many-relationship-properties.md)|아니요|  
|부모-자식 계층 구조|[예](multidimensional-models/parent-child-dimension.md)|예(DAX를 통해)|  
|파티션|[예](tabular-models/partitions-ssas-tabular.md)|  
|큐브 뷰|[예](multidimensional-models/perspectives-in-multidimensional-models.md)|[예](tabular-models/partitions-ssas-tabular.md)|  
|반가산적 측정값|[예](multidimensional-models/define-semiadditive-behavior.md)|예(DAX를 통해)|  
|Translations|[예](multidimensional-models/translations-in-multidimensional-models-analysis-services.md)|아니요|  
|사용자 정의 계층|[예](multidimensional-models/user-defined-hierarchies-create.md)|사용자 계정 컨트롤|  
|쓰기 저장(writeback)|[예](multidimensional-models/set-partition-writeback.md)|아니요|  
  
 * 솔루션을 많은 수의 고유 카운트 (예: 수백만 개의 고객 Id)를 지원 해야 하는 경우 테이블 형식을 먼저 고려 합니다. 이 시나리오에서는 이 형식의 성능이 더 우수합니다. 백서, 고유 카운트에 대 한 섹션을 참조 [Analysis Services 사례 연구: 대규모 상용 솔루션에서 테이블 형식 모델을 사용 하 여](https://msdn.microsoft.com/library/dn751533.aspx)입니다.  
  
##  <a name="bkmk_modelsize"></a> 모델 크기  
 총 개체 수 측면에서 모델 크기는 솔루션 유형에 따라 달라지지 않습니다. 하지만 각 솔루션을 구축하는 데 사용된 각 설계 도구에 따라 대량의 개체를 얼마나 잘 지원하는 지가 결정됩니다. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서는 모델이 클수록 구축하기가 더 편합니다.  이유는 개체 탐색기 및 솔루션 탐색기에서 개체 다이어그램 설정 및 나열을 위한 더 많은 기능을 제공하기 때문입니다.  
  
 수백 개의 테이블 또는 차원으로 구성되는 매우 큰 모델은 디자인 도구가 아닌 Visual Studio에서 프로그래밍 방식으로 빌드되는 경우가 많습니다. 모델의 개체의 최대 수에 대 한 자세한 내용은 참조 하세요. [최대 용량 사양 &#40;Analysis Services&#41;](multidimensional-models/olap-physical/maximum-capacity-specifications-analysis-services.md)합니다.  
  
##  <a name="bkmk_ext"></a> 프로그래밍 기능 및 개발자 환경  
 테이블 형식 및 다차원 모델의 경우 두 형식 모두에 공유되는 하나의 개체 모델이 있습니다. AMO 및 ADOMD.NET은 두 모드를 모두 지원합니다. 어느 쪽의 클라이언트 라이브러리도 테이블 형식 구문에 맞게 개정되지 않았으므로, 다차원 및 테이블 형식 구문 및 명명 규칙이 서로 연관되는 방식을 이해할 필요가 있습니다. 첫 번째 단계로는 AMO-테이블 형식 프로그래밍 샘플에서 테이블 형식 모델에 대한 AMO 프로그래밍을 확인해야 합니다. 자세한 내용을 보려면 [Codeplex 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=221036)에서 샘플을 다운로드하세요.  
  
 테이블 형식 솔루션은 솔루션당 model.bim 파일을 하나만 지원합니다. 즉, 모든 작업을 단일 파일에서 수행해야 합니다. 단일 솔루션에서 여러 프로젝트를 작업하는 데 익숙한 개발 팀의 경우 공유 테이블 형식 솔루션을 빌드할 때 작업 방식을 수정할 필요가 있을 수 있습니다.  
  
##  <a name="bkmk_lang"></a> 쿼리 및 스크립팅 언어 지원  
 Analysis Services에는 MDX, DMX, DAX, XML/A 및 ASSL이 포함되어 있습니다. 이러한 언어에 대한 지원은 모델 유형별로 약간 다릅니다. 쿼리 및 스크립팅 언어 요구 사항을 고려해야 하는 경우 다음 목록을 검토하세요.  
  
-   테이블 형식 모델 데이터베이스는 DAX 계산, DAX 쿼리 및 MDX 쿼리를 지원합니다.  
  
-   다차원 모델 데이터베이스는 ASSL뿐만 아니라 MDX 계산 및 MDX 쿼리를 지원합니다.  
  
-   데이터 마이닝 모델은 DMX와 ASSL을 지원합니다.  
  
-   Analysis Services PowerShell은 서버 및 데이터베이스 관리를 위해 지원됩니다. 모델 형식(또는 서버 모드)은 PowerShell cmdlet과는 관계가 없습니다.  
  
 모든 데이터베이스는 XML/A를 지원합니다.  
  
##  <a name="bkmk_sec"></a> 보안 기능 지원  
 모든 Analysis Services 솔루션은 데이터베이스 수준에서 보안이 유지될 수 있습니다. 보다 세부적인 보안 옵션은 모드마다 다릅니다. 세부적인 보안 설정이 솔루션의 요구 사항인 경우 다음 목록을 검토하여 원하는 보안 수준이 작성하려는 솔루션 유형에서 지원되는지 확인하세요.  
  
-   테이블 모델 데이터베이스에서는 Analysis Services의 역할 기반 사용 권한을 통해 행 수준 보안을 사용할 수 있습니다.  
  
-   다차원 데이터베이스에서는 Analysis Services의 역할 기반 사용 권한을 통해 차원 및 셀 수준 보안을 사용할 수 있습니다.  
  
 Excel 데이터 모델을 테이블 형식 모드 서버로 복원할 수 있습니다. 파일이 복원되면 SharePoint에서 분리되므로(SharePoint 위치에서 복원한다고 가정) 행 수준 보안을 비롯하여 거의 모든 테이블 형식 모델링 기능을 사용할 수 있습니다. 복원된 통합 문서에서 사용할 수 없는 한 가지 테이블 형식 모델링 기능은 연결된 테이블입니다.  
  
##  <a name="bkmk_designer"></a> 디자인 도구  
 데이터 모델링 역량 및 기술 전문성은 분석 모델을 작성하는 사용자 간에 크게 다를 수 있습니다. 도구 친숙성 또는 사용자 전문성이 솔루션의 고려 사항인 경우 다음과 같은 모델 생성 환경을 비교하세요.  
  
|**모델링 도구**|**사용 방법**|  
|-----------------------|------------------|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|테이블 형식, 다차원 및 데이터 마이닝 솔루션을 만드는 데 사용됩니다. 이 제작 환경에서는 Visual Studio 셸을 사용하여 작업 영역, 속성 창 및 개체 탐색을 제공합니다. Visual Studio를 이미 사용 중인 기술 사용자는 비즈니스 인텔리전스 애플리케이션을 생성할 때 대부분 이 도구를 선호합니다. 자세한 내용은 [Tools and applications used in Analysis Services](tools-and-applications-used-in-analysis-services.md) 를 참조하세요.|  
|Excel 2013 이상, Excel용 파워 피벗 추가 기능 포함|Excel용 파워 피벗은 Excel 데이터 모델을 편집하고 개선하는 데 사용하는 도구입니다. Excel에서 별도의 애플리케이션 작업 영역이 열리지만 Excel과 동일한 시각적 요소(탭된 페이지, 모눈 레이아웃 및 수식 입력줄)를 사용합니다. Excel에 능숙한 사용자는 일반적으로 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 이 도구를 사용하는 것을 선호할 것입니다. 참조 [파워 피벗: 강력한 데이터 분석 및 Excel에서 데이터 모델링](https://support.office.com/en-ie/article/Power-Pivot-Powerful-data-analysis-and-data-modeling-in-Excel-d7b119ed-1b3b-4f23-b634-445ab141b59b)합니다.|  
  
##  <a name="bkmk_client"></a> 클라이언트 및 보고 응용 프로그램  
 이전 릴리스에서는 사용자가 선택한 모델 유형이 사용할 수 있는 클라이언트 애플리케이션에 영향을 미치지만 시간이 지나면서 이러한 구분이 모호해졌습니다. 테이블 형식 및 다차원 형식은 Analysis Services 데이터에 연결하는 클라이언트 애플리케이션 관련하여 거의 동일한 지원을 제공합니다. 다음 표는 Analysis Services 데이터 모델과 함께 사용할 수 있는 Microsoft 클라이언트 애플리케이션의 목록입니다.  
  
|**응용 프로그램**|**설명**|  
|---------------------|---------------------|  
|Excel 피벗 테이블 보고서|쓰기 저장(Excel 구현하는 Analysis Services 기능)은 다차원 모델에 대해서만 지원되지만 Excel 기능은 테이블 형식 및 다차원 모델 둘 다에서 동일합니다.|  
|Reporting Services RDL 보고서|보고서 작성기 또는 보고서 디자이너에서 만든 RDL 보고서에는 SharePoint용 PowerPivot에 호스트되는 Excel 데이터 모델은 물론 모든 Analysis Services 모델을 사용할 수 있습니다.|  
|PerformancePoint 대시보드|SharePoint에서 PerformancePoint 대시보드는 Excel 데이터 모델을 포함하여 모든 Analysis Services 데이터베이스에 연결할 수 있습니다. 자세한 내용은 [데이터 연결 만들기(PerformancePoint Services)](https://go.microsoft.com/fwlink/?linkdID=218155)를 참조하세요.|  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] Office 365 또는 Power BI 사이트|테이블 형식 모델에만 해당합니다.|  
|SharePoint 온-프레미스의 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]|SharePoint의 ClickOnce 응용 프로그램으로 실행되는 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]는 Analysis Services 큐브 또는 테이블 형식 모델을 사용할 수 있습니다.|  
  
##  <a name="bkmk_deploymentmode"></a> 다차원 및 테이블 형식 솔루션의 서버 배포 모드  
 Analysis Services 인스턴스는 서버의 작업 컨텍스트를 설정하는 세 가지 모드 중 하나로 설치됩니다. 설치하는 서버 모드에 따라 해당 서버에 배포할 수 있는 솔루션 유형이 결정됩니다. 세 모드 간의 가장 큰 차이점은 스토리지 및 메모리 아키텍처이지만 그 밖에 다른 차이점도 있습니다. 다음 표에서는 세 가지 서버 모드에 대해 간단히 설명합니다. 자세한 내용은 [Analysis Services 인스턴스의 서버 모드 확인](instances/determine-the-server-mode-of-an-analysis-services-instance.md)을 참조하세요.  
  
|배포 모드|Description|  
|---------------------|-----------------|  
|0 - 다차원 및 데이터 마이닝|Analysis Services의 기본 인스턴스에 배포하는 다차원 및 데이터 마이닝 솔루션을 실행합니다. 배포 모드 0은 Analysis Services 설치의 기본값입니다. 자세한 내용은 [Install Analysis Services in Multidimensional and Data Mining Mode](../../2014/sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)을 참조하세요.|  
|1 - SharePoint용 PowerPivot|Excel 데이터 모델 액세스의 경우 Analysis Services는 SharePoint의 내부 구성 요소입니다. Analysis Services는 배포 모드 1에 설치되며 SharePoint 환경에서 Excel Services의 요청만 수락합니다. 자세한 내용은 [PowerPivot for SharePoint 2010 Installation](../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)을 참조하세요.|  
|2 - 테이블 형식|배포 모드 2로 구성된 Analysis Services의 독립 실행형 인스턴스에서 테이블 형식 솔루션을 실행합니다. 자세한 내용은 [Install Analysis Services in Tabular Mode](instances/install-windows/install-analysis-services.md)을 참조하세요.|  
  
 서버 모델은 서로 교환할 수 없습니다. 설치 시 서버 작업에 대한 모드를 선택합니다. 모든 작업을 지원하기 위해 각 서버 모드에 대해 하나씩 여러 인스턴스를 설치해야 합니다.  
  
##  <a name="bkmk_sharePoint"></a> 호스팅 플랫폼  
 Microsoft는 데이터, 애플리케이션, 보고서 및 협업을 호스팅하기 위한 여러 방법을 제공합니다. 이 섹션에서는 각 호스팅 플랫폼과 관련된 Analysis Services 상호 운용성을 다룹니다.  
  
|**플랫폼**|**설명**|  
|------------------|---------------------|  
|Microsoft Azure|Azure 가상 머신에서 지원되는 모든 Analysis Services 버전 및 에디션을 실행할 수 있습니다. 온-프레미스 관계형 데이터베이스 엔진과 동일한 기능을 많이 제공하는 Azure의 서비스인 Azure SQL 데이터베이스와 달리, Azure에는 동급의 Analysis Services가 없습니다. Azure VM에서의 Analysis Services 설치, 구성 및 실행이 유일한 Azure 옵션입니다.|  
|Office 365|Office 365의 Excel Online은 온-프레미스에서 실행되는 테이블 형식 및 다차원 모델에 대한 원격 연결을 지원합니다.|  
|Office 365의 Power BI 사이트|Power BI 사이트에서 파워 뷰 보고서는 온-프레미스에서 실행되는 표 형식 데이터 모델에 연결할 수 있습니다.|  
|온-프레미스 서버(SharePoint 및 SQL Server 인스턴스)|온-프레미스 데이터베이스 서버(즉, Analysis Services가 설치된 SQL Server 인스턴스)는 여전히 보고서 및 클라이언트 애플리케이션에 Analysis Services 데이터를 사용할 수 있도록 하는 기본 수단입니다. 테이블 형식, 다차원 및 데이터 마이닝 솔루션은 SharePoint에 대한 종속성 없이 네트워크의 Analysis Services 인스턴스에서 실행됩니다.<br /><br /> SQL Server는 PowerPivot 데이터 액세스 및 테이블 형식 데이터 액세스를 위한 지원을 추가하여 SharePoint와 통합됩니다. 각 제품에 사용된 기능 수를 극대화하면 SharePoint 및 SQL Server 통합에 대한 투자가 늘어납니다. SharePoint가 있으면 SharePoint용 SQL Server PowerPivot을 설치하여 PowerPivot 데이터 액세스를 지원하고 네트워크 서버의 외부 Analysis Services 인스턴스에서 실행되는 테이블 형식 데이터베이스에 액세스하는 데 사용되는 PowerPivot .bism 연결 파일을 가져올 수 있습니다.<br /><br /> SharePoint 및 SQL Server가 둘 다 있으면 다음과 같은 서비스 및 애플리케이션 조합을 지원할 수 있습니다.<br /><br /> Analysis Services 모델(테이블 형식 또는 다차원 형식)<br /><br /> 중간 계층 SharePoint Services(Excel Services, SharePoint의 Reporting Services 또는 PerformancePoint Services)<br /><br /> 심층 데이터 분석 및 탐색을 위한 브라우저 클라이언트 또는 리치 클라이언트(Excel)|  
  
##  <a name="bkmk_Next"></a> 다음 단계: 솔루션 빌드  
 각 솔루션의 비교 방법에 대한 기본적인 이해를 마쳤으므로, 다음 자습서를 통해 각 솔루션을 작성하는 단계를 배워 보시기 바랍니다. 다음 링크는 각 단계를 설명하는 자습서로 이어집니다.  
  
-   [테이블 형식 모델링&#40;Adventure Works 자습서&#41;](tabular-modeling-adventure-works-tutorial.md)를 사용하여 테이블 형식 모델을 작성합니다.  
  
-   [다차원 모델링&#40;Adventure Works 자습서&#41;](multidimensional-modeling-adventure-works-tutorial.md)를 사용하여 다차원 모델을 작성합니다.  
  
-   [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md)를 사용하여 데이터 마이닝 모델을 빌드합니다.  
  
-   [PowerPivot for Excel 자습서](https://go.microsoft.com/fwlink/?LinkId=251135)를 사용하여 PowerPivot 모델을 빌드합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 인스턴스 관리](instances/analysis-services-instance-management.md)   
 [Analysis Services 및 Business Intelligence의 새로운 기능](what-s-new-in-analysis-services.md)   
 [새로운 &#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md)   
 [PowerPivot의 새로운 기능](https://go.microsoft.com/fwlink/?LinkId=238141)   
 [SQL Server 2012 용 PowerPivot 도움말](https://go.microsoft.com/fwlink/?LinkID=220946)   
 [PowerPivot BI 의미 체계 모델 연결 &#40;.bism&#41;](power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [공유 데이터 원본 만들기 및 관리&#40;SharePoint 통합 모드의 Reporting Services&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)  
  
  
