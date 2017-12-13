---
title: "View (Analysis Services)를 원본 데이터를 정의 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- names [Analysis Services], data source views
- name matching criteria [Analysis Services]
- Data Source View Wizard
- data source views [Analysis Services], creating
ms.assetid: 0bae4ee4-1742-40e9-bebe-17c788854484
caps.latest.revision: "42"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4331bf4de9efa68338e509976b534549bd3506d5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="defining-a-data-source-view-analysis-services"></a>데이터 원본 뷰 정의(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]사용 하는 스키마의 논리 모델을 포함 하는 데이터 원본 뷰 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 다차원 데이터베이스 개체-큐브, 차원 및 마이닝 구조입니다. 데이터 원본 뷰는 UDM(Unified Dimensional Model)과 마이닝 구조에서 사용하는 이러한 스키마 요소의 메타데이터 정의이며 XML 형식으로 저장됩니다. 데이터 원본 뷰의 특성은 다음과 같습니다.  
  
-   스키마 생성에 대한 하향식 접근 방식을 사용할 경우 여러 기본 데이터 원본에서 선택한 개체를 나타내는 메타데이터 또는 기본 관계형 데이터 저장소를 생성하는 데 사용될 메타데이터를 포함합니다.  
  
-   여러 데이터 원본에서 작성할 수 있으므로 여러 원본의 데이터를 통합하는 다차원 및 데이터 마이닝 개체를 정의할 수 있습니다.  
  
-   기본 데이터 원본에는 표시되지 않으며 기본 데이터 원본과 별도로 존재하는 관계, 기본 키, 개체 이름, 계산 열 및 쿼리를 포함할 수 있습니다.  
  
-   클라이언트 응용 프로그램에서 표시 또는 쿼리할 수 없습니다.  
  
 DSV는 다차원 모델의 필수 구성 요소입니다. 대부분의 Analysis Services 개발자는 초기 모델 디자인 단계 중에 DSV를 만들며, 기본 데이터를 제공하는 외부 관계형 데이터베이스에 따라 최소한 한 개 이상의 DSV를 생성합니다. 하지만 이후 단계에서도 차원 및 큐브가 생성된 후 스키마 및 기본 데이터베이스 구조를 생성하여 DSV를 만들 수 있습니다. 이러한 두 번째 방법은 하향식 디자인이라고도 하며 프로토타입 및 분석 모델링에 자주 사용됩니다. 이 방법을 사용할 경우 스키마 생성 마법사를 사용하여 Analysis Services 프로젝트나 데이터베이스에서 정의한 OLAP 개체를 기반으로 기본 데이터 원본과 데이터 원본 개체를 만듭니다. DSV를 만드는 방법 및 시간에 관계없이, 모델을 처리할 수 있으려면 모든 모델에 DSV가 하나 포함되어야 합니다.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
 [데이터 원본 뷰 작성](#bkmk_dsvdef)  
  
 [데이터 원본 뷰 마법사를 사용하여 DSV 만들기](#bkmk_startWiz)  
  
 [관계에 대한 이름 일치 조건 지정](#bkmk_NameMatch)  
  
 [보조 데이터 원본 추가](#bkmk_secondaryDS)  
  
##  <a name="bkmk_dsvdef"></a> 데이터 원본 뷰 작성  
 데이터 원본 뷰는 다음 항목으로 이루어집니다.  
  
-   이름 및 설명  
  
-   하나 이상의 데이터 원본에서 전체 스키마에 이르기까지 검색되는 스키마의 다음을 포함하는 모든 하위 집합 정의  
  
    -   테이블 이름  
  
    -   열 이름  
  
    -   데이터 형식  
  
    -   Null 허용 여부  
  
    -   열 길이  
  
    -   기본 키  
  
    -   기본 키 - 외래 키 관계  
  
-   기본 데이터 원본의 스키마에 대한 다음을 포함하는 주석  
  
    -   테이블, 뷰 및 열의 이름  
  
    -   스키마에 테이블로 표시되는 하나 이상의 데이터 원본의 열을 반환하는 명명된 쿼리  
  
    -   테이블이나 뷰에 열로 표시되는 데이터 원본의 열을 반환하는 명명된 계산  
  
    -   논리적 기본 키(기본 테이블에 기본 키가 정의되지 않았거나 뷰 또는 명명된 쿼리에 기본 키가 포함되지 않은 경우에 필요함)  
  
    -   논리적 기본 키 - 테이블, 뷰 및 명명된 쿼리 간의 외래 키 관계  
  
##  <a name="bkmk_startWiz"></a> 데이터 원본 뷰 마법사를 사용하여 DSV 만들기  
 DSV를 만들려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 서버 탐색기에서 데이터 원본 뷰 마법사를 실행합니다.  
  
> [!NOTE]  
>  또는 차원과 큐브를 먼저 생성한 후 스키마 생성 마법사를 사용해서 모델에 대해 DSV를 생성할 수 있습니다. 자세한 내용은 [스키마 생성 마법사&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/schema-generation-wizard-analysis-services.md)를 참조하세요.  
  
1.  솔루션 탐색기에서 데이터 원본 뷰 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터 원본 뷰**를 클릭합니다.  
  
2.  외부 관계형 데이터베이스에 대해 연결 정보를 제공하는 새로운 또는 기존의 데이터 원본 개체를 지정합니다(마법사에서 데이터 원본을 하나만 선택할 수 있음).  
  
3.  같은 페이지에서 **고급** 을 클릭하여 특정 스키마를 선택하거나, 필터를 적용하거나, 테이블 관계 정보를 제외시킵니다.  
  
     **스키마 선택**  
  
     여러 스키마가 포함된 매우 큰 데이터 원본에서는 공백 없이 쉼표로 구분된 목록으로 사용할 스키마를 선택할 수 있습니다.  
  
     **관계 검색**  
  
     고급 데이터 원본 뷰 옵션 대화 상자에서 **관계 검색** 확인란을 선택 취소해서 테이블 관계 정보를 의도적으로 생략하여 데이터 원본 뷰 디자이너의 각 테이블 간의 관계를 수동으로 만들 수 있습니다.  
  
4.  **사용 가능한 개체 필터**  
  
     사용 가능한 개체 목록에 많은 개체가 포함된 경우 문자열을 선택 조건으로 지정하는 간단한 필터를 적용하여 목록을 줄일 수 있습니다. 예를 들어 **dbo** 를 입력하고 **필터** 단추를 클릭하면 "dbo"로 시작하는 항목만 **사용 가능한 개체** 목록에 표시됩니다. 필터는 부분 문자열(예: “sal”은 매출과 급여를 반환함)이 될 수 있지만 여러 문자열 또는 연산자를 포함할 수 없습니다.  
  
5.  테이블 관계가 정의되지 않은 관계형 데이터 원본에 대해서는 적절한 이름 일치 방법을 선택할 수 있도록 **이름 일치** 페이지가 표시됩니다. 자세한 내용은 이 항목의 [관계에 대한 이름 일치 조건 지정](#bkmk_NameMatch) 섹션을 참조하세요.  
  
##  <a name="bkmk_secondaryDS"></a> 보조 데이터 원본 추가  
 여러 데이터 원본의 테이블, 뷰 또는 열이 포함된 데이터 원본 뷰를 정의하는 경우 데이터 원본 뷰에 개체를 추가하는 첫 번째 데이터 원본이 주 데이터 원본으로 지정됩니다. 정의한 후에는 주 데이터 원본을 변경할 수 없습니다. 단일 데이터 원본의 개체를 기반으로 데이터 원본 뷰를 정의한 후 다른 데이터 원본의 개체를 추가할 수 있습니다.  
  
 OLAP 처리나 데이터 마이닝 쿼리에 여러 데이터 원본의 데이터가 단일 쿼리로 필요한 경우 주 데이터 원본에서 **OpenRowset**을 사용하여 원격 쿼리를 지원해야 합니다. 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 원본이 여기에 해당합니다. 예를 들어 여러 데이터 원본의 열에 바인딩된 특성이 포함된 OLAP 차원을 지정하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 **OpenRowset** 쿼리를 생성하여 처리 중에 이 차원을 채웁니다. 그러나 단일 데이터 원본에서 OLAP 개체를 채우거나 데이터 마이닝 쿼리를 해결할 수 있는 경우에는 **OpenRowset** 쿼리가 생성되지 않습니다. **OpenRowset** 쿼리가 필요하지 않도록 특성 간에 특성 관계를 정의할 수 있는 경우도 있습니다. 특성 관계에 대한 자세한 내용은 [특성 관계](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md), [데이터 원본 뷰에서 테이블이나 뷰 추가 또는 제거&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md) 및 [특성 관계 정의](../../analysis-services/multidimensional-models/attribute-relationships-define.md)의 서버 탐색기에서 데이터 원본 뷰 마법사를 실행합니다.  
  
 보조 데이터 원본에서 테이블과 열을 추가하려면 솔루션 탐색기에서 DSV를 두 번 클릭하여 데이터 원본 뷰 디자이너에서 DSV를 연 다음 테이블 추가/제거 대화 상자를 사용하여 프로젝트에 정의된 다른 데이터 원본에서 개체를 포함합니다. 자세한 내용은 [데이터 원본 뷰에서 테이블이나 뷰 추가 또는 제거&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)의 서버 탐색기에서 데이터 원본 뷰 마법사를 실행합니다.  
  
##  <a name="bkmk_NameMatch"></a> 관계에 대한 이름 일치 조건 지정  
 DSV를 만들 때 데이터 원본의 외래 키 제약 조건을 기반으로 테이블 간의 관계가 생성됩니다. 이러한 관계는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 엔진에서 적절한 OLAP 처리 및 데이터 마이닝 쿼리를 구성하는 데 필요합니다. 그러나 여러 개의 테이블이 포함된 데이터 원본에 FOREIGN KEY 제약 조건이 없을 수도 있습니다. 데이터 원본에 FOREIGN KEY 제약 조건이 없으면 데이터 원본 뷰 마법사에서 여러 테이블의 열 이름을 일치시키는 방법을 정의하라는 메시지가 표시됩니다.  
  
> [!NOTE]  
>  기본 데이터 원본에서 외래 키 관계가 검색되지 않는 경우에만 이름 일치 조건을 제공하라는 메시지가 표시됩니다. 외래 키 관계가 검색되면 검색된 관계가 사용되며 논리적 기본 키를 포함하여 DSV에 포함시킬 추가 관계를 수동으로 정의해야 합니다. 자세한 내용은 [데이터 원본 뷰에서 논리적 관계 정의&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md) 및 [데이터 원본 뷰에서 논리적 기본 키 정의&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-logical-primary-keys-in-a-data-source-view-analysis-services.md)를 참조하세요.  
  
 데이터 원본 뷰 마법사는 사용자 응답을 사용하여 열 이름을 일치시키고 DSV의 여러 테이블 간에 관계를 만듭니다. 다음 표에 나열된 조건 중 하나를 지정할 수 있습니다.  
  
|이름 일치 조건|Description|  
|----------------------------|-----------------|  
|**기본 키와 같은 이름**|원본 테이블의 외래 키 열 이름이 대상 테이블의 기본 키 열 이름과 같습니다. 예를 들어 외래 키 열인 `Order.CustomerID` 는 기본 키 열인 `Customer.CustomerID`와 같습니다.|  
|**대상 테이블 이름과 같은 이름**|원본 테이블의 외래 키 열 이름이 대상 테이블의 이름과 같습니다. 예를 들어 외래 키 열인 `Order.Customer` 는 기본 키 열인 `Customer.CustomerID`와 같습니다.|  
|**대상 테이블 이름 + 기본 키 이름**|대상 테이블 이름과 기본 키 열 이름이 연결되어 원본 테이블의 외래 키 열 이름이 됩니다. 공백이나 밑줄 구분 기호를 사용할 수 있습니다. 예를 들어 다음과 같은 외래-기본 키 쌍은 모두 일치합니다.<br /><br /> `Order.CustomerID` 및 `Customer.ID`<br /><br /> `Order.Customer ID` 및 `Customer.ID`<br /><br /> `Order.Customer_ID` 및 `Customer.ID`|  
  
 선택한 조건은 DSV의 **NameMatchingCriteria** 속성 설정을 변경합니다. 이 설정은 마법사에서 관련 테이블을 추가하는 방법을 결정합니다. 데이터 원본 뷰 디자이너를 사용하여 데이터 원본 뷰를 변경할 때 이 지정은 디자이너에서 열을 일치시켜 DSV의 테이블 간에 관계를 만드는 방법을 결정합니다. 데이터 원본 뷰 디자이너에서 **NameMatchingCriteria** 속성 설정을 변경할 수 있습니다. 자세한 내용은 [데이터 원본 뷰에서 속성 변경&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)을 참조하세요.  
  
> [!NOTE]  
>  데이터 원본 뷰 마법사를 완료한 후 데이터 원본 뷰 디자이너의 스키마 창에서 관계를 추가 또는 제거할 수 있습니다. 자세한 내용은 [데이터 원본 뷰에서 논리적 관계 정의&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 원본 뷰에서 테이블이나 뷰 추가 또는 제거&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)   
 [데이터 원본 뷰 &#40;에서 논리적 기본 키 정의 Analysis Services &#41;](../../analysis-services/multidimensional-models/define-logical-primary-keys-in-a-data-source-view-analysis-services.md)   
 [데이터 원본 뷰 &#40; 명명 된 계산을 정의 합니다. Analysis Services &#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)   
 [데이터 원본 뷰 &#40; 명명 된 쿼리 정의 Analysis Services &#41;](../../analysis-services/multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)   
 [테이블 또는 데이터 원본 뷰 &#40; 명명 된 쿼리 바꾸기 Analysis Services &#41;](../../analysis-services/multidimensional-models/replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services.md)   
 [데이터 원본 뷰 디자이너 &#40;에서 다이어그램 작업 Analysis Services &#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)   
 [데이터 원본 뷰 &#40;의 데이터를 탐색 Analysis Services &#41;](../../analysis-services/multidimensional-models/explore-data-in-a-data-source-view-analysis-services.md)   
 [데이터 원본 뷰 &#40; 삭제 Analysis Services &#41;](../../analysis-services/multidimensional-models/delete-a-data-source-view-analysis-services.md)   
 [데이터 원본 뷰에서 스키마 새로 고침&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/refresh-the-schema-in-a-data-source-view-analysis-services.md)  
  
  
