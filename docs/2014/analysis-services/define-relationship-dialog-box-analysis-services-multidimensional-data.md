---
title: 관계 정의 대화 상자 (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.cubeeditor.dimensionusage.definerelationship.f1
helpviewer_keywords:
- Define Relationship dialog box
ms.assetid: 0fcee7f1-f138-4c2e-ae8c-245395ee0fe8
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5cb46c19a45b85e90a0484a5f0ac33eff0077298
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092295"
---
# <a name="define-relationship-dialog-box-analysis-services---multidimensional-data"></a>관계 정의 대화 상자(Analysis Services - 다차원 데이터)
  **관계 정의** 대화 상자를 사용하여 큐브 디자이너에서 큐브 차원과 측정값 그룹 간의 관계를 정의할 수 있습니다. 큐브 디자이너 **차원 용도** 탭의 **표** 창에서 셀의 **...** 를 클릭하면 **관계 정의** 대화 상자를 표시할 수 있습니다.  
  
## <a name="options"></a>변수  
 **관계 유형 선택**  
 큐브 차원과 측정값 그룹 간에 만들 차원 관계 유형을 선택합니다. 차원 관계 유형을 선택하면 **세부 정보** 창의 내용이 변경됩니다.  
  
 **관계 없음** 을 선택하면 차원 관계가 생성되지 않습니다.  
  
 **Detail**  
 **관계 유형 선택**에서 선택한 차원 관계 유형에 사용할 수 있는 옵션을 표시합니다.  
  
## <a name="detail-pane-options"></a>세부 정보 창 옵션  
 **관계 유형 선택** 에서 선택한 관계 유형에 따라 **세부 정보**창에는 다음 옵션이 표시됩니다.  
  
|관계 유형|Description|옵션|  
|-----------------------|-----------------|------------|  
|**관계 없음**|관계를 정의하지 않으면 **세부 정보** 창에 옵션이 표시되지 않습니다.||  
|**Regular**|일반 차원 관계를 지정합니다. **세부 정보** 창에는 다음 옵션이 표시됩니다.|**세분성 특성**: <br />                      차원과 관련하여 측정값 그룹의 세분성을 정의하는 특성을 선택합니다. 이 특성은 일반적으로 차원의 키 특성입니다.|  
|||**차원 테이블**: 차원의 주 테이블을 표시합니다.|  
|||**측정값 그룹 테이블**: 측정값 그룹의 팩트 테이블을 표시합니다.|  
|||**관계**: 관계의 기반이 되는 차원 열과 측정값 그룹 열의 표를 표시합니다. 표에는 다음 열이 있습니다.<br /><br /> **차원 열**: 선택한 세분성 특성과 연결된 열을 표시합니다. 참고: 차원이 아직 생성되지 않은 경우 이 옵션은 **생성**으로 설정됩니다.<br />**측정값 그룹 열** :<br />                              측정값 그룹에서 차원 열과 관련된 열을 선택합니다.|  
|||**고급**:<br />                      **측정값 그룹 바인딩** 대화 상자를 표시하고 특성과 측정값 그룹 열 간의 관계에 대한 Null 처리 등의 고급 속성을 편집하려면 클릭합니다. **측정값 그룹 바인딩** 대화 상자에 대한 자세한 내용은 [측정값 그룹 바인딩 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](measure-group-bindings-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.|  
|**팩트**|팩트 차원 관계를 지정합니다. **세부 정보** 창에는 다음 옵션이 표시됩니다.|**세분성 특성**: 차원과 관련하여 측정값 그룹의 세분성을 정의하는 특성을 선택합니다. 이 특성은 일반적으로 차원의 키 특성입니다.|  
|||**차원 테이블**: 주 차원 테이블을 표시합니다.|  
|||**측정값 그룹 테이블**: <br />                      측정값 그룹의 기반이 되는 테이블을 표시합니다.|  
|**참조**|참조 차원 관계를 지정합니다. **세부 정보** 창에는 다음 옵션이 표시됩니다.|**참조 차원**: <br />                      선택한 차원을 표시합니다.|  
|||**중간 차원**: <br />                      중간 차원을 선택합니다.|  
|||**참조 차원 특성**: <br />                      **중간 차원 특성**에 지정한 중간 차원 특성과 관련된 참조 차원 특성을 선택합니다.|  
|||**중간 차원 특성**: <br />                      **참조 차원**에 지정한 참조 차원 특성과 관련된 중간 차원 특성을 선택합니다.|  
|||**구체화**: <br />                      참조 차원의 특성을 MOLAP 구조의 팩트 테이블에 연결하는 중간 차원의 특성 멤버를 저장하려면 선택합니다. 기본적으로 쿼리 성능을 극대화하기 위해 관계를 구체화하는 동작이 수행되지만 이 경우 처리 시간과 저장 공간이 늘어나게 됩니다.|  
|**다 대 다**|다 대 다 차원 관계를 지정합니다. **세부 정보** 창에는 다음 옵션이 표시됩니다.|**차원** : 선택한 차원을 표시합니다.|  
|||**중간 측정값 그룹** : <br />                      관련된 중간 측정값 그룹을 선택합니다.<br /><br /> 참고: 중간 측정값 그룹에는 선택한 측정값 그룹과 공통된 차원이 하나 이상 있어야 합니다. 또한 중간 측정값 그룹과 공통 차원 간의 관계 세분성이 공통 차원과 선택한 측정값 그룹 간의 세분성보다 크거나 같아야 합니다.|  
|**데이터 마이닝**|데이터 마이닝 차원 관계를 지정합니다. **세부 정보** 창에는 다음 옵션이 표시됩니다.|**대상 차원**: 선택한 데이터 마이닝 차원을 표시합니다.<br /><br /> 참고: 데이터 마이닝 차원 관계를 만들려면 데이터 마이닝 차원을 선택해야 합니다.|  
|||**원본 차원**: 데이터 마이닝 차원에서 예측 분석을 제공하는 차원을 선택합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [차원 관계](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [차원 용도 &#40;큐브 디자이너&#41; &#40;Analysis Services-다차원 데이터&#41;](dimension-usage-cube-designer-analysis-services-multidimensional-data.md)   
 [Analysis Services 디자이너 및 대화 상자 &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  