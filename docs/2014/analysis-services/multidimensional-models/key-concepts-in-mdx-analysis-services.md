---
title: MDX의 주요 개념 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], about MDX
- dimensional modeling [MDX]
- MDX [Analysis Services], about MDX
- Multidimensional Expressions [Analysis Services], dimensional modeling
- MDX [Analysis Services], dimensional modeling
ms.assetid: 4797ddc8-6423-497a-9a43-81a1af7eb36c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b51c763987fdfe8bbaf08851094a5e6e6d267c36
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66074855"
---
# <a name="key-concepts-in-mdx-analysis-services"></a>MDX의 주요 개념(Analysis Services)
  MDX(Multidimensional Expressions)를 사용하여 다차원 데이터를 쿼리하거나 큐브 내에 MDX 식을 만들기 전에 다차원의 개념과 용어를 이해하는 것이 도움이 됩니다.  
  
 이미 알고 있는 데이터 요약 예제를 사용하여 시작한 다음 MDX가 어떻게 관련되는지 확인하는 것이 좋습니다. Excel에서 만든 피벗 테이블은 Analysis Services 샘플 큐브의 데이터로 채워집니다.  
  
 ![측정값과 차원이 호출된 피벗 테이블](../media/ssas-keyconcepts-pivot1-measures-dimensions.png "측정값과 차원이 호출된 피벗 테이블")  
  
## <a name="measures-and-dimensions"></a>측정값 및 차원  
 Analysis Services 큐브는 측정값, 차원 및 차원 특성으로 구성되며, 모두 피벗 테이블 예제에서 분명하게 확인할 수 있습니다.  
  
 **측정값** 은 셀에 있는 숫자 데이터 값으로 합계, 개수, 백분율, 최소, 최대 또는 평균으로 집계 됩니다. 측정값은 사용자 탐색 및 피벗 테이블과의 상호 작용에 응답하여 실시간으로 계산되는 동적인 값입니다. 이 예에서 셀은 축을 확장하거나 축소함에 따라 늘어나거나 줄어드는 Reseller Sales Amounts를 보여 줍니다. Date(연도, 분기, 월 또는 날짜) 및 Sales Territory(Country group, Country, Region) 조합의 경우, 해당 특정 컨텍스트에 대해 합산된 Reseller Sales Amount를 얻을 수 있습니다. 측정값과 동의어인 다른 용어는 팩트(데이터 웨어하우스)와 계산된 필드(테이블 및 Excel 데이터 모델)입니다.  
  
 **차원은** 피벗 테이블의 열 및 행 축에 있으며 측정값의 의미를 제공 합니다. 차원은 관계형 데이터 모델에서 테이블과 유사합니다. 차원의 일반적인 예로는 Time, Geography, Products, Customers, Employees 등이 있습니다. 이 예에는 행에 Sales Territory라는 차원과 위에 Date라는 차원이 있지만, Promotions 또는 Products처럼 Reseller Sales와 연관된 다른 차원을 쉽게 끌어서 놓고 이러한 차원과 함께 판매 실적을 볼 수 있습니다. 데이터를 재미있게 탐색하는 기능은 생성하는 차원 및 이러한 차원이 데이터 원본의 팩트 테이블과 연관되는지에 달려 있습니다.  
  
 **차원 특성** 은 테이블의 열과 비슷한 차원 내의 명명 된 항목입니다. 이 예에서 Sales Territory 차원 특성은 Country Group(Europe, North America, Pacific), Country(Canada, United States) 및 Region(Central, Northeast, Northwest, Southeast, Southwest)으로 구성됩니다.  
  
 각 특성에는 연관된 데이터 값 또는 구성원의 컬렉션이 있습니다. 예에서 Country Group 특성의 구성원은 Europe, North America 및 Pacific입니다. **멤버** 는 특성에 속하는 실제 데이터 값을 나타냅니다.  
  
> [!NOTE]  
>  데이터 모델링의 한 가지 측면은 이미 데이터 자체 내에 존재하는 패턴과 관계를 형식화하는 것입니다. 국가-지역-도시의 경우처럼 자연 계층에 속하는 데이터로 작업할 때 **특성 관계**를 생성하여 해당 관계를 형식화할 수 있습니다. 특성 관계는 특성 간의 일 대 다 관계입니다. 예를 들어 상태와 도시 간의 관계는 많은 도시를 갖지만 도시는 한 가지 상태에만 속합니다. 모델에서 특성 관계를 만들면 쿼리 성능이 향상 되므로 데이터에서 지 원하는 경우이를 만드는 것이 가장 좋습니다. SQL Server Data Tools의 차원 디자이너에서 특성 관계를 만들 수 있습니다. 
  [Define Attribute Relationships](attribute-relationships-define.md)를 참조하십시오.  
  
 Excel에서 모델 메타데이터가 피벗 테이블 필드 목록에 표시됩니다.  위 피벗 테이블과 아래 필드 목록을 비교해 보세요. 필드 목록에는 Sales Territory, Group, Country, Region(메타데이터)이 포함되는 반면, 피벗 테이블에는 구성원(데이터 값)만 포함됩니다. 아이콘 모양을 알면 다차원 모델의 부분과 Excel의 피벗 테이블을 쉽게 연결할 수 있습니다.  
  
 ![피벗 테이블 필드 목록](../media/ssas-keyconcepts-ptfieldlist.png "피벗 테이블 필드 목록")  
  
## <a name="attribute-hierarchies"></a>특성 계층  
 각 축을 따라 수준을 확장하고 축소하면 피벗 테이블의 값이 위 또는 아래로 이동한다는 것은 모두 알고 계실 것입니다. 하지만 어떤 원리에 의해 이것이 가능한 것일까요? 그 답은 특성 계층에 있습니다.  
  
 모든 수준을 축소하고 각 Country Group 및 Calendar Year의 총합계를 보세요. 이 값은 계층 구조 내의 **(전체) 구성원** 이라는 항목에서 파생됩니다. (전체) 구성원은 특성 계층의 모든 구성원에 대해 계산된 값입니다.  
  
-   결합된 모든 Country Group 및 Date의 (전체) 구성원은 $80,450,596.98입니다.  
  
-   CY2008의 (전체) 구성원은 $16,038,062.60입니다.  
  
-   Pacific의 (전체) 구성원은 $1,594,335.38입니다.  
  
 이처럼 집계는 미리 사전 계산되고 저장됩니다. 이것이 바로 Analysis Services가 제공하는 빠른 쿼리 성능의 비결입니다.  
  
 ![모든 구성원이 호출된 피벗 테이블](../media/ssas-keyconcepts-pivot2-allmember.png "모든 구성원이 호출된 피벗 테이블")  
  
 계층을 확장하면 결국 최저 수준으로 이동합니다. 이를 **리프 구성원**이라고 합니다. 리프 구성원은 계층에서 하위 항목이 없는 구성원입니다. 이 예에서는 Australia가 리프 구성원입니다.  
  
 ![리프 구성원이 호출된 피벗 테이블](../media/ssas-keyconcepts-pivot3-leafparent.PNG "리프 구성원이 호출된 피벗 테이블")  
  
 그 위의 것은 **상위 구성원**이라고 합니다. Pacific은 Australia의 상위입니다.  
  
 **특성 계층의 구성 요소**  
  
 이러한 개념이 모두 함께 **특성 계층**의 개념을 형성합니다. 특성 계층은 다음 수준이 들어 있는 특성 구성원의 트리입니다.  
  
-   각각의 고유 특성 멤버가 들어 있는 리프 수준. 리프 수준의 각 멤버는 **리프 멤버**라고도 합니다.  
  
-   특성 계층이 상위-하위 계층인 경우, 중간 수준(나중에 자세히 설명).  
  
-   모든 하위 특성의 집계된 값이 들어 있는 (전체) 구성원. 필요에 따라 (All) 수준을 숨기 거 나 해제 하 여 데이터에 적합 하지 않을 수 있습니다. 예를 들어 제품 코드는 숫자 이지만 합계 또는 평균을 계산 하거나 모든 제품 코드를 집계 하는 것은 의미가 없습니다.  
  
> [!NOTE]  
>  BI 개발자는 종종 특성 계층에 속성을 설정하여 클라이언트 애플리케이션에서 특정 동작을 얻거나 특정 성능 혜택을 얻습니다. 예를 들어 (All) 멤버가 적절 하지 않은 특성에 AttributeHierarchyEnabled = False를 설정할 수 있습니다. 또는 단순히 (전체) 구성원을 숨기고자 하는 경우 AttributeHierarchyVisible=False를 설정할 수 있습니다. 속성에 대한 자세한 내용은 [Dimension Attribute Properties Reference](dimension-attribute-properties-reference.md) (영문)를 참조하세요.  
  
## <a name="navigation-hierarchies"></a>탐색 계층  
 이 예를 살펴보면 피벗 테이블 내에서 행 및 열 축을 확장하여 특성의 더 낮은 수준을 볼 수 있습니다. 모델에서 생성하는 탐색 계층을 통해 확장 가능한 트리를 얻습니다.  AdventureWorks 샘플 모델에서 Sales Territory 차원에는 Country Group으로 시작하여 Country, Region으로 이어지는 여러 수준의 계층이 있습니다.  
  
 이처럼 계층은 피벗 테이블 또는 다른 데이터 요약 개체에서 탐색 경로를 제공하는 데 사용됩니다. 기본 유형으로는 균형과 불균형이 있습니다.  
  
 **균형 계층**  
  
|||  
|-|-|  
|![균형 있는 계층 구조가 호출된 피벗 테이블](../media/ssas-keyconcepts-pivot4-balancedhierarchy.PNG "균형 있는 계층 구조가 호출된 피벗 테이블")|
  **균형 계층** 은 최상위 수준과 모든 리프 구성원 사이의 수준 수가 동일한 계층입니다.<br /><br /> 
  **자연 계층** 은 기본 데이터에서 자연적으로 발생하는 계층입니다. 일반적인 예로는 Country-Region-State, Year-Month-Date 또는 Category-Subcategory-Model이 있으며 각 하위 수준은 상위로부터 예측할 수 있습니다.<br /><br /> 다차원 모델에서 계층 대부분은 균형 계층이며, 이 중 대부분이 자연 계층입니다.<br /><br /> 관련된 다른 모델링 용어는 `user-defined hierarchy`이며 종종 특성 계층과 대조적으로 사용됩니다. BI 개발자가 생성한 계층이라는 의미로, 특성을 정의할 때 Analysis Services에서 자동으로 생성되는 특성 계층과 반대되는 개념입니다.|  
  
 **불균형 계층**  
  
|||  
|-|-|  
|![비정형 계층이 호출된 피벗 테이블](../media/ssas-keyconcepts-pivot15-raggedhierarchy.PNG "비정형 계층이 호출된 피벗 테이블")|
  **비정형 계층** 또는 **불균형 계층** 은 최상위 수준과 리프 구성원 사이의 수준 수가 다른 계층입니다. 또한 BI 개발자가 만든 계층 구조 이지만이 경우 데이터에 간격이 있습니다.<br /><br /> AdventureWorks 샘플 모델에서, 미국에는 이 예의 다른 국가에는 존재하지 않는 추가 수준(Regions)이 있기 때문에 Sales Territory는 비정형 계층을 보여 줍니다.<br /><br /> 클라이언트 애플리케이션이 비정형 계층을 원활하게 처리하지 못하는 경우 비정형 계층은 BI 개발자에게 문제가 됩니다. Analysis Services 모델에서 여러 수준 데이터 간의 관계를 명확하게 정의하는 **상위-하위 계층 구조** 를 만들어 한 수준이 다른 수준과 관련되는 방식의 모호성을 없앨 수 있습니다. 
  [Parent-Child Hierarchy](parent-child-dimension.md) 를 참조하세요.|  
  
## <a name="key-attributes"></a>키 특성  
 모델은 키와 인덱스를 사용하여 연결을 만드는 관련 개체의 컬렉션입니다. Analysis Services 모델도 다르지 않습니다. 각 차원(관계형 모델의 테이블과 동일)에 대해 키 특성이 있습니다. 
  **키 특성** 은 팩트 테이블(측정값 그룹)에 대한 외래 키 관계에서 사용됩니다. 차원에서 키가 아닌 모든 특성이 키 특성에 직접적으로 또는 간접적으로 연결됩니다.  
  
 항상은 아니지만, 종종 키 특성은 **세분성 특성**이기도 합니다. 세분성이란 데이터 내의 세부 정보 또는 정밀도 수준을 의미합니다. 다시, 가장 쉽게 이해할 수 있도록 일반적인 예를 들어 설명해 보겠습니다. 날짜 값을 생각해 봅시다. 일일 판매의 경우, 해당 일에 지정된 날짜 값이 필요합니다. 할당량의 경우 분기별로 설정해도 충분하겠지만, 데이터 분석이 스포츠 행사의 경기 결과로 구성되는 경우 세분성은 밀리초 단위로 설정되어야 할 것입니다. 데이터 값의 정확도 수준은 세분성입니다.  
  
 또 다른 예로 통화를 들 수 있습니다. 금융 응용 프로그램은 통화 값을 많은 소수 자릿수로 추적할 수 있습니다. 반면, 현지 학교 기금 모금 기금에는 가장 가까운 달러의 값만 필요할 수 있습니다. 불필요한 데이터를 저장하지 않으려면 세분성에 대한 이해가 중요합니다. 타임스탬프에서 밀리초를 잘라내거나 판매액에서 페니를 잘라내면, 해당 수준의 세부 정보가 분석과 관련 있지 않을 때 스토리지와 처리 시간을 절약할 수 있습니다.  
  
 세분성 특성을 설정하려면 SQL Server Data Tools의 큐브 디자이너에서 차원 용도 탭을 사용합니다. AdventureWorks 샘플 모델에서 Date 차원의 키 특성은 Date 키입니다. Sales Orders의 경우 세분성 특성은 키 특성과 같습니다. Sales Targets의 경우 세분성 수준이 분기별이므로 세분성 특성은 Calendar Quarter로 설정됩니다.  
  
 ![세분성 특성을 보여 주는 모델](../media/ssas-keyconcepts-granularityattrib.png "세분성 특성을 보여 주는 모델")  
  
> [!NOTE]  
>  세분성 특성과 키 특성이 다른 경우, 키가 아닌 모든 특성은 세분성 특성에 직접 또는 간접적으로 연결되어야 합니다. 큐브 내에서 세분성 특성은 차원 세분성을 정의합니다.  
  
## <a name="query-scope-cube-space"></a>쿼리 범위(큐브 공간)  
 쿼리 범위는 데이터가 선택되는 경계를 의미합니다. 범위는 전체 큐브(큐브는 가장 큰 쿼리 개체)에서 셀까지 가능합니다.  
  
 큐브 **공간** 은 큐브의 측정값을 사용 하는 큐브의 특성 계층 멤버에 대 한 곱입니다.  
  
 하위 큐브는 큐브의 필터링 된 뷰를 나타내는 큐브의 하위 **집합입니다.** 하위 큐브는 MDX 계산 스크립트의 SCOPE 문이나 MDX 쿼리의 하위 SELECT 절을 사용하여 정의하거나 세션 큐브로 정의할 수 있습니다.  
  
 **셀** 은 측정값 차원 멤버의 멤버와 큐브의 각 특성 계층에 있는 멤버의 교집합에 있는 공간을 나타냅니다.  
  
## <a name="other-modeling-terms"></a>기타 모델링 용어  
 이 섹션은 다른 섹션에는 쉽게 맞지 않는 개념 및 용어의 모음 이지만 여전히 알아야 합니다.  
  
 **계산 멤버** 는 쿼리 시 정의 및 계산 되는 차원 멤버입니다. 계산 멤버는 사용자 쿼리나 MDX 계산 스크립트에서 정의되고 서버에 저장될 수 있습니다. 계산 멤버는 해당 멤버가 정의된 차원의 차원 테이블에 있는 행에 대응됩니다.  
  
 **고유 카운트** 는 한 번만 계산 되어야 하는 데이터 항목에 사용 되는 특별 한 유형의 측정입니다. AdventureWorks 샘플 모델에 Internet Orders, Reseller Orders 및 Sales Orders에 대한 고유 카운트 측정값이 포함됩니다.  
  
 **측정값 그룹** 은 하나 이상의 측정값 컬렉션입니다. 측정값 그룹은 대부분 사용자 정의되며, 측정값 그룹을 사용하여 관련 측정값을 함께 유지할 수 있습니다. 고유 카운트 측정값은 예외입니다. 고유 카운트 측정값은 항상 고유 측정값만 들어 있는 전용 측정값 그룹에 있습니다. 피벗 테이블 예에서는 측정값 그룹을 볼 수 없지만 피벗 테이블 필드 목록에는 명명 된 측정값 컬렉션으로 표시 됩니다.  
  
 **측정값 차원** 은 큐브의 모든 측정값을 포함 하는 차원입니다. SQL Server Data Tools에서 작성 하는 다차원 모델에는 표시 되지 않지만 동일 하 게 존재 합니다. 측정값을 포함하기 때문에 측정값 차원의 모든 구성원은 일반적으로 합계 또는 횟수 등으로 집계됩니다.  
  
 **데이터베이스 차원 및 큐브 차원**. 모델 내에서 같은 모델에 있는 임의 개수의 큐브에 포함되는 독립 실행형 차원을 정의할 수 있습니다. 큐브에 차원을 추가 하면 큐브 차원 이라고 합니다. 프로젝트 내에서 개체 탐색기의 독립 실행형 항목으로 서 데이터베이스 차원 이라고 합니다. 이렇게 구분하는 이유는 무엇일까요? 독립적으로 속성을 설정할 수 있기 때문입니다. 제품 설명서에는 두 용어가 모두 표시 되므로 의미를 이해 하는 것이 좋습니다.  
  
## <a name="next-steps"></a>다음 단계  
 이제 중요한 개념과 용어에 대해 살펴봤으므로 Analysis Services의 기본 개념을 더 자세히 설명하는 다음과 같은 추가 항목을 진행할 수 있습니다.  
  
-   [MDX &#40;기본 MDX 쿼리&#41;](mdx/mdx-query-the-basic-query.md)  
  
-   [MDX &#40;기본 MDX 스크립트&#41;](mdx/the-basic-mdx-script-mdx.md)  
  
-   [&#40;의 다차원 모델링은 놀이 Works 자습서&#41;](../multidimensional-modeling-adventure-works-tutorial.md)  
  
## <a name="see-also"></a>참고 항목  
 [큐브 공간](mdx/cube-space.md)   
 [옥](mdx/tuples.md)   
 [Autoexist](mdx/autoexists.md)   
 [MDX &#40;멤버, 튜플 및 집합을 사용 하 여 작업&#41;](mdx/working-with-members-tuples-and-sets-mdx.md)   
 [보이는 합계 및 비시각적 합계](mdx/visual-totals-and-non-visual-totals.md)   
 [MDX 쿼리 기본 사항 &#40;Analysis Services&#41;](mdx/mdx-query-fundamentals-analysis-services.md)   
 [MDX 스크립팅 기본 사항 &#40;Analysis Services&#41;](mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [Mdx 언어 참조 &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)   
 [MDX&#41; 참조 &#40;다차원 식](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
