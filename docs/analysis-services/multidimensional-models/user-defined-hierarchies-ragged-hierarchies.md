---
title: "비정형 계층 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ragged hierarchies [Analysis Services]
ms.assetid: e40a5788-7ede-4b0f-93ab-46ca33d0cace
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: df06dbfc368310427d1359f78de557c910b94af9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="user-defined-hierarchies---ragged-hierarchies"></a>사용자 정의 계층-비정형된 계층 구조
  비정형 계층은 균일하지 않은 수준 수가 있는 사용자 정의 계층입니다. 일반적인 예로 계정 차트, 고위 관리자가 부서 관리자와 비관리자를 부하 직원으로 둔 조직 차트, Washington D.C., Vatican City 또는 New Delhi와 같이 부모 State 또는 Province가 없이 Country-Region-City로 구성된 지역 계층 등이 있습니다.  
  
 차원의 대부분의 계층에서는 각 수준 위에 동일한 수준의 다른 멤버와 같은 수의 멤버가 있습니다. 비정형 계층에서는 최소한 한 멤버의 논리적 부모 멤버가 해당 멤버 바로 위 수준에 있지 않다는 점이 다릅니다. 이러한 경우 계층이 여러 드릴다운 경로에 대한 서로 다른 수준으로 이어집니다. 클라이언트 응용 프로그램에서 이로 인해 드릴다운 경로가 불필요하게 복잡해질 수 있습니다.  
  
 클라이언트 응용 프로그램에 따라 비정형 계층을 얼마나 효과적으로 처리하는지가 달라집니다. 비정형 계층이 모델에 있는 경우 예상하는 렌더링 동작을 얻으려면 약간의 추가 작업을 수행해야 합니다.  
  
 첫 번째 단계로 클라이언트 응용 프로그램을 확인하여 드릴다운 경로를 처리하는 방법을 확인합니다. 예를 들어 Excel의 경우 누락된 값에 대한 자리 표시자로 부모 이름이 반복됩니다. 이 동작을 직접 보려면 Adventure Works 다차원 모델에서 Sales Territory 차원을 사용하여 피벗 테이블을 만듭니다. Group, Country 및 Region이라는 Sales Territory 특성이 있는 피벗 테이블에서 지역 값이 없는 국가가 자리 표시자를 얻게 되며, 이 경우에는 자리 표시자 위에 부모(국가 이름)가 반복됩니다. 이 동작은 Excel에서 수정된 MDX Compatibility=1 연결 문자열 속성에서 파생된 것입니다. 클라이언트가 찾고 있는 드릴다운 동작을 자연히 제공하지 않는 경우 이러한 동작 중 최소한 일부를 변경하도록 모델의 속성을 설정할 수 있습니다.  
  
 이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [비정형 계층에서 드릴다운 탐색을 수정하기 위한 방법](#bkmk_approach)  
  
-   [일반 계층에서 멤버를 숨기도록 HideMemberIf 설정](#bkmk_Hide)  
  
-   [MDX Compatibility를 설정하여 자리 표시자가 클라이언트 응용 프로그램에서 표현되는 방법 결정](#bkmk_Mdx)  
  
##  <a name="bkmk_approach"></a> 비정형 계층에서 드릴다운 탐색을 수정하기 위한 방법  
 비정형 계층의 존재는 드릴다운 탐색이 예상되는 값을 반환하지 않거나 사용하기에 비효율적인 것으로 인식될 때 문제가 됩니다. 비정형 계층으로 인해 발생하는 탐색 문제를 해결하려면 다음 옵션을 사용해 보십시오.  
  
-   일반 계층을 사용하지만 각 수준에 대해 **HideMemberIf** 속성을 설정하여 누락된 수준을 사용자에게 시각화할지 여부를 지정합니다. **HideMemberIf**를 설정하는 경우 연결 문자열에 대한 **MDXCompatibility** 도 설정하여 기본 탐색 동작을 재정의해야 합니다. 이러한 속성을 설정하는 지침이 이 항목에 설명되어 있습니다.  
  
-   수준 멤버를 명시적으로 관리하는 부모-자식 계층을 만듭니다. 이 기술의 일러스트레이션을 보려면 [SSAS의 비정형 계층(블로그 포스트)](http://dwbi1.wordpress.com/2011/03/30/ragged-hierarchy-in-ssas/)을 참조하세요. 자세한 내용은 온라인 설명서의 [부모-자식 차원](../../analysis-services/multidimensional-models/parent-child-dimension.md)을 참조하세요. 부모-자식 계층을 만드는 경우의 단점은 차원당 부모-자식 계층이 하나만 있을 수 있으며 중간 멤버에 대한 집계를 계산할 때 일반적으로 성능 저하가 발생하는 것입니다.  
  
 차원에 둘 이상의 비정형 계층이 포함된 경우 첫 번째 방법인 **HideMemberIf**를 설정해야 합니다. 비정형 계층 작업 실무 경험이 있는 BI 개발자는 물리적 데이터 테이블에서 추가 변경 내용을 지원하고 각 수준에 대한 별도의 테이블을 만듭니다. 이 기술에 대한 자세한 내용은 [Martin Mason의 SSAS 재무 큐브–1a 파트–비정형 계층(블로그)](http://martinmason.wordpress.com/2012/03/03/the-ssas-financial-cubepart-1aragged-hierarchies-cont/) 을 참조하세요.  
  
##  <a name="bkmk_Hide"></a> 일반 계층에서 멤버를 숨기도록 HideMemberIf 설정  
 비정형 차원 테이블의 경우 논리적으로 누락된 멤버를 여러 방법으로 표시할 수 있습니다. 테이블 셀에는 Null 또는 빈 문자열을 포함할 수 있습니다. 또는 자리 표시자 역할을 하기 위해 부모와 같은 값을 포함할 수도 있습니다. 자리 표시자의 표현은 클라이언트 응용 프로그램에 대한 **HideMemberIf** 연결 문자열 속성 및 **MDX Compatibility** 속성에 의해 결정되는 자식 멤버의 자리 표시자 상태에 의해 결정됩니다.  
  
 비정형 계층의 표시를 지원하는 클라이언트 응용 프로그램의 경우 논리적으로 누락된 멤버를 숨기도록 이러한 속성을 사용할 수 있습니다.  
  
1.  SSDT에서 차원을 두 번 클릭하여 차원 디자이너에서 차원을 엽니다. 계층 창에서 첫 번째 탭, 차원, 구조가 특성 계층을 나타냅니다.  
  
2.  계층 내의 멤버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **HideMemberIf** 를 아래 설명된 값 중 하나로 설정합니다.  
  
    |HideMemberIf 설정|Description|  
    |--------------------------|-----------------|  
    |**안 함**|수준 멤버를 숨기지 않습니다. 이 값은 기본값입니다.|  
    |**OnlyChildWithNoName**|부모의 유일한 자식이고 이름이 Null 또는 빈 문자열인 수준 멤버를 숨깁니다.|  
    |**OnlyChildWithParentName**|부모의 유일한 자식이고 이름이 부모와 동일한 수준 멤버를 숨깁니다.|  
    |**NoName**|이름이 비어 있는 수준 멤버를 숨깁니다.|  
    |**ParentName**|이름이 부모와 동일한 수준 멤버를 숨깁니다.|  
  
##  <a name="bkmk_Mdx"></a> MDX Compatibility를 설정하여 자리 표시자가 클라이언트 응용 프로그램에서 표현되는 방법 결정  
 계층 수준에서 **HideMemberIf** 를 설정한 후 클라이언트 응용 프로그램에서 전송된 연결 문자열에 **MDX Compatibility** 속성도 설정해야 합니다. **MDX Compatibility** 설정은 **HideMemberIf** 가 사용되는지 여부를 결정합니다.  
  
|MDX 호환성 설정|Description|사용법|  
|-------------------------------|-----------------|-----------|  
|**1.**|자리 표시자 값을 표시합니다.|이 값은 Excel, SSDT 및 SSMS에서 사용되는 기본값입니다. 비정형 계층에서 빈 수준을 드릴다운할 때 서버에서 자리 표시자 값을 반환하도록 지시합니다. 자리 표시자 값을 클릭하면 자식(리프) 노드로 계속 드릴다운할 수 있습니다.<br /><br /> Excel은 Analysis Services에 연결하는 데 사용되는 연결 문자열을 소유하고 각 새 연결에 대해 **MDX Compatibility** 을 항상 1로 설정합니다. 이 동작은 이전 버전과의 호환성을 유지됩니다.|  
|**2**|자리 표시자 값(부모 수준의 null 값 또는 중복)을 숨기지만 관련 값을 가진 다른 수준 및 노드는 표시합니다.|**MDX Compatibility**=2는 일반적으로 비정형 계층의 개념으로 기본 설정으로 표시됩니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 및 일부 타사 클라이언트 응용 프로그램에서는 이 설정을 유지할 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 정의 계층 만들기](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)   
 [사용자 계층](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [부모-자식 차원](../../analysis-services/multidimensional-models/parent-child-dimension.md)   
 [연결 문자열 속성&#40;Analysis Services&#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)  
  
  
