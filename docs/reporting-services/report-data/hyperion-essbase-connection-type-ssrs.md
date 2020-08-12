---
title: Hyperion Essbase 연결 형식 | Microsoft Docs
description: 보고서에 포함할 Hyperion Essbase 외부 데이터 원본에서 다차원 데이터를 검색하는 방법을 알아봅니다.
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 108a00b6-799f-4066-b796-da59e95c09fd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d6ee62393c6b9a74dee16acf532d474a7a344b54
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85808435"
---
# <a name="hyperion-essbase-connection-type-ssrs"></a>Hyperion Essbase 연결 형식(SSRS)
  보고서에 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 외부 데이터 원본의 데이터를 포함하려면 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 유형의 보고서 데이터 원본에 기초하는 데이터 세트가 있어야 합니다. 이 기본 제공 데이터 원본 유형은 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]외부 데이터 원본에서 다차원 데이터를 검색할 수 있게 하는 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 에 대한 데이터 확장 프로그램을 기반으로 합니다.  
  
 이 항목의 정보를 사용하여 데이터 원본을 작성할 수 있습니다. 단계별 지침은 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)을 참조하세요.  
  
##  <a name="connection-string"></a><a name="Connection"></a> 연결 문자열  
 다음 연결 문자열 예에서는 SOAP를 사용하는 인터넷을 통해 포트 13080과 XMLA(XML for [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] )를 사용하는 서버의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본을 지정하고 예제 카탈로그에 연결합니다.  
  
```  
Data Source=https://localhost:13080/aps/XMLA; Initial Catalog=Sample  
```  
  
 연결 문자열 예제에 대한 자세한 내용은 [데이터 연결 문자열 만들기 - 보고서 작성기 및 SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)를 참조하십시오.  
  
  
##  <a name="credentials"></a><a name="Credentials"></a> 자격 증명  
 쿼리를 실행하거나 보고서를 로컬로 미리 보거나 보고서 서버의 보고서를 미리 보려면 자격 증명이 필요합니다.  
  
 보고서를 게시한 후 보고서를 보고서 서버에서 실행할 때 데이터를 검색할 수 있는 권한이 유효하도록 데이터 원본에 대한 자격 증명을 변경해야 할 수도 있습니다.  
  
 자세한 내용은 [보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정](specify-credential-and-connection-information-for-report-data-sources.md)을 참조하세요.  
  
  
##  <a name="queries"></a><a name="Query"></a> 쿼리  
 다음과 같은 방법으로 쿼리를 지정할 수 있습니다.  
  
-   대화식으로 쿼리를 작성합니다. 디자인 모드나 쿼리 모드의 그래픽 쿼리 디자이너에서 외부 데이터 원본의 메타데이터를 찾고 MDX(Multidimensional Expression) 구문으로 쿼리를 생성합니다.  
  
    -   **디자인 뷰** 차원, 멤버, 멤버 속성, 측정값 및 KPI를 메타데이터 브라우저에서 **데이터** 창으로 끌어서 MDX 쿼리를 작성합니다. 추가 데이터 세트 필드를 정의하려면 계산 멤버 창의 계산 멤버를 데이터 창으로 끕니다.  
  
    -   **쿼리 뷰** 차원, 멤버, 멤버 속성, 측정값 및 KPI를 메타데이터 브라우저에서 쿼리 창으로 끌어서 MDX 쿼리를 작성합니다. 그런 다음 쿼리 창에서 직접 MDX 텍스트를 편집할 수 있습니다. 추가 데이터 세트 필드를 정의하려면 계산 멤버 창의 계산 멤버를 쿼리 창으로 끕니다.  
  
     자세한 내용은 [Hyperion Essbase 쿼리 디자이너 사용자 인터페이스&#40;보고서 작성기&#41;](../../reporting-services/report-data/hyperion-essbase-query-designer-user-interface.md)를 참조하세요.  
  
-   보고서에서 기존 MDX 쿼리를 가져옵니다. **쿼리 가져오기** 단추를 사용하여 .rdl 파일을 찾아서 쿼리를 가져옵니다. [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 데이터 원본을 기반으로 하는 포함된 데이터 세트가 들어 있는 보고서에서 쿼리를 가져올 수 있습니다. .mdx 파일에서 MDX 쿼리를 직접 가져올 수는 없습니다.  
  
 디자인 타임에 쿼리를 실행하여 결과 집합을 확인합니다. 쿼리를 작성한 후 메타데이터에서 생성되는 데이터 세트 필드 컬렉션을 보고서 데이터 창에서 확인합니다. 보고서를 실행하면 외부 데이터 원본에서 실제 데이터가 반환됩니다.  
  
 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 데이터 처리 확장 프로그램은 확장 데이터 세트 필드 속성을 지원합니다. 이러한 속성은 외부 데이터 원본에서 사용할 수 있지만 보고서 데이터 창에 표시되지 않는 값입니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [확장 필드 속성](#Extended) 을 참조하십시오.  
  
  
##  <a name="query-parameters"></a><a name="Parameters"></a>쿼리 매개 변수  

 쿼리 매개 변수를 포함하려면 쿼리 디자이너에서 필터 영역에 필터를 만들고 필터를 매개 변수로 표시합니다. 각 필터에 대해 데이터 세트가 자동으로 생성되어 사용 가능한 값을 제공합니다. 기본적으로 이러한 데이터 세트는 보고서 데이터 창에 나타나지 않습니다. 자세한 내용은 [다차원 데이터의 매개 변수 값에 대해 숨겨진 데이터 세트 표시&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/show-hidden-datasets-for-parameter-values-multidimensional-data.md)을 참조하세요.

 기본적으로 각 보고서 매개 변수의 데이터 형식은 **Text**입니다. 보고서 매개 변수가 만들어진 후에는 기본값을 변경해야 할 수 있습니다. 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)에 대해 자세히 알아봅니다.  
  
  
##  <a name="extended-field-properties"></a><a name="Extended"></a> 확장 필드 속성  
 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 데이터 처리 확장 프로그램은 확장 필드 속성을 지원합니다. 확장 필드 속성은 **Value** 및 **IsMissing** 외에 데이터 처리 확장 프로그램에서 데이터 세트 필드에 대해 정의한 속성입니다. 확장 속성에는 미리 정의된 속성과 사용자 지정 속성이 포함됩니다. 미리 정의된 속성은 여러 데이터 원본에 공통된 속성이고 사용자 지정 속성은 각 데이터 원본에 고유한 속성입니다.  
  
 확장 필드 속성은 보고서 데이터 창에 보고서 레이아웃으로 끌 수 있는 항목으로 나타나지 않습니다. 대신 속성의 부모 필드를 보고서로 끈 다음 기본 속성 **Value** 를 사용하려는 속성으로 변경합니다.  
  
 확장 필드 속성의 이름은 쿼리 디자이너의 메타데이터 창에서 필드 위에 마우스를 놓으면 도구 설명에 나타납니다. 기본 데이터를 탐색할 때 사용할 수 있는 쿼리 디자이너에 대한 자세한 내용은 [Hyperion Essbase Query Designer User Interface](../../reporting-services/report-data/hyperion-essbase-query-designer-user-interface.md)를 참조하십시오.  
  
> [!NOTE]  
>  MDX 식에 포함되어 있고 보고서가 실행되어 해당 데이터 세트에 대한 데이터를 검색할 때 데이터 원본에서 확장 필드 속성 값을 제공하는 경우에만 이러한 속성에 대한 값이 있습니다. 그러면 다음 섹션에 설명된 구문을 사용하여 모든 식에서 해당 **Field** 속성 값을 참조할 수 있습니다. 그러나 이러한 필드는 해당 데이터 공급자와만 관련이 있고 보고서 정의 언어에는 포함되지 않으므로 이러한 값을 변경해도 보고서 정의에는 변경된 값이 저장되지 않습니다.  
  
  
### <a name="predefined-field-properties"></a>미리 정의된 필드 속성  
 일반적으로 여러 데이터 공급자에 의해 지원되며 보고서 데이터 세트에 대한 기본 MDX 쿼리에 나타나는 미리 정의된 필드 속성. 예를 들어 MDX 차원 속성 MEMBER_UNIQUE_NAME은 미리 정의된 보고서 데이터 세트 필드 속성 **UniqueName**에 매핑됩니다. 입력란에 고유한 이름 값을 포함하려면 `=Fields!` *\<FieldName>* `.UniqueName` 식을 사용합니다.  
  
 다음 표에서는 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 데이터 원본에 사용할 수 있는 미리 정의된 필드 속성 목록을 제공합니다.  
  
|**Property**|**Type**|**설명 또는 필요한 값**|  
|------------------|--------------|---------------------------------------|  
|**값**|**Object**|필드의 데이터 값을 지정합니다.<br /><br /> 차원 속성의 경우 MEMBER_CAPTION에 매핑됩니다. 측정값의 경우 데이터 값에 매핑됩니다.|  
|**IsMissing**|**Boolean**|필드가 결과 데이터 집합에 있는지 여부를 나타냅니다.|  
|**FormattedValue**|**String**|주요 숫자 값의 형식화된 값을 반환합니다.<br /><br /> MDX 식의 FORMATTED_VALUE에서 매핑됩니다.|  
|**BackgroundColor**|**String**|필드에 대해 데이터베이스에 정의된 배경색을 반환합니다.<br /><br /> MDX 식의 BACK_COLOR에서 매핑됩니다.|  
|**Color**|**String**|항목에 대해 데이터베이스에 정의된 전경색을 반환합니다.<br /><br /> MDX 식의 FORE_COLOR에서 매핑됩니다.|  
|**UniqueName**|**String**|수준의 정규화된 이름을 반환합니다.<br /><br /> MDX 식의 MEMBER_UNIQUE_NAME에서 매핑됩니다.|  
  
 식에 필드 및 필드 속성을 사용하는 방법에 대한 자세한 내용은 [식의 기본 제공 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)을 참조하세요.  
  
  
### <a name="custom-properties"></a>사용자 지정 속성  
 데이터 공급자가 지원하고 보고서 데이터 세트에 대한 기본 MDX 쿼리에 나타나지만 보고서 데이터 세트 창에 해당 데이터 세트 아래의 필드로 표시되지 않는 사용자 지정 필드 속성. 예를 들어 **Long Names** 는 차원 수준에 대해 정의된 멤버 속성입니다. 입력란에 값을 포함하려면 `=Fields!` *\<FieldName>* `("Long Names")` 식을 사용합니다. 식의 필드 이름은 대/소문자를 구분합니다.  
  
 식에서 사용자 지정 확장 속성을 참조하려면 다음 구문을 사용합니다.  
  
-   *Fields!FieldName("PropertyName")*  
  
 다음 표에서는 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 데이터 원본에 사용할 수 있는 사용자 지정 필드 속성을 보여 줍니다.  
  
|**Property**|**Type**|**설명 또는 필요한 값**|  
|------------------|--------------|---------------------------------------|  
|**FORMAT_STRING**|**String**|측정값에 대해 정의되며, String 유형으로 사용할 수 있는 **FormattedValue** 입니다.|  
  
  
##  <a name="remarks"></a><a name="Remarks"></a> 주의  
 이 데이터 공급자는 일부 보고서 배달 모드만 지원합니다. 이 데이터 처리 확장 프로그램에서는 데이터 기반 구독을 통한 보고서 배달이 지원되지 않습니다. 자세한 내용은 [구독자 데이터에 외부 데이터 원본 사용&#40;데이터 기반 구독&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)을 참조하세요. 
  
 자세한 내용은 [Hyperion Essbase와 함께 SQL Server 2005 Reporting Services 사용(Using SQL Server 2005 Reporting Services with Hyperion Essbase)](https://go.microsoft.com/fwlink/?LinkId=81970)을 참조하십시오.  
  
  
##  <a name="how-to-topics"></a><a name="HowTo"></a> 방법 도움말 항목  
 이 섹션에서는 데이터 연결, 데이터 원본 및 데이터 세트를 사용하는 방법을 단계별로 설명합니다.  
  
 [데이터 연결 추가 및 확인&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [공유 데이터 세트 또는 포함된 데이터 세트 만들기&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [데이터 세트에 필터 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="related-sections"></a><a name="Related"></a> 관련 단원  
 설명서의 다음 섹션에서는 보고서 데이터에 대한 깊이 있는 개념 정보를 제공하며, 데이터와 관련된 보고서 부분을 정의, 사용자 지정 및 사용하는 방법을 절차적인 측면에서 소개합니다.  
  
 [보고서 데이터 세트&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 보고서의 데이터 액세스에 대한 개요를 제공합니다.  
  
 [데이터 연결 문자열 만들기 - 보고서 작성기 및 SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
 데이터 연결 및 데이터 원본에 대한 정보를 제공합니다.  
  
 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 포함된 데이터 세트 및 공유 데이터 세트에 대한 정보를 제공합니다.  
  
 [데이터 세트 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 데이터 세트 쿼리에 의해 생성되는 필드 컬렉션에 대한 정보를 제공합니다.  
  
 [Reporting Services &#40;SSRS&#41;에서 지원하는 데이터 원본](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) 각 데이터 확장 프로그램에 대한 플랫폼 및 버전 지원에 관한 자세한 정보를 제공합니다.  
  
 [Hyperion Essbase와 함께 SQL Server 2005 Reporting Services 사용(Using SQL Server 2005 Reporting Services with Hyperion Essbase)](https://go.microsoft.com/fwlink/?LinkId=81970)  
 이 데이터 확장 프로그램을 사용하는 방법에 대한 자세한 정보를 제공합니다.  
  
  
## <a name="see-also"></a>참고 항목  
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [데이터 필터링, 그룹화 및 정렬&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
