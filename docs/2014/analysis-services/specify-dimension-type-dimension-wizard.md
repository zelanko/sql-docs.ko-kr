---
title: 차원 유형 (차원 마법사)를 지정 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.bidimensionproperties.f1
ms.assetid: 3215282a-532d-4ff2-b721-286f088967fc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 166fae1cb6fb76587b6741b6f47449d2600bf8e8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155863"
---
# <a name="specify-dimension-type-dimension-wizard"></a>차원 유형 지정(차원 마법사)
  **차원 유형 지정** 페이지를 사용하여 차원 유형을 정의하고 선택한 차원 유형과 관련된 특수 특성 유형을 차원에 추가할 수 있습니다.  
  
> [!NOTE]  
>  이 페이지는 **차원 유형 선택** 페이지에서 **표준 차원** 을 선택한 경우에만 표시됩니다.  
  
## <a name="options"></a>변수  
 **차원 유형**  
 차원의 차원 유형을 선택합니다. 다음 표에서는 사용 가능한 차원 유형을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**계정**|계정 차원은 계정 목록을 나타내는 데이터와 메타데이터를 포함합니다.<br /><br /> 계정 차원에 대한 자세한 내용은 [부모-자식 유형 차원의 재무 계정 만들기](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)를 참조하세요.|  
|**BillOfMaterials**|제품 구성 정보(BOM) 차원은 데이터와 메타데이터가 제품 부품 목록과 같은 제조 정보나 재고를 나타내는 일반 차원입니다.<br /><br /> 일반 차원에 대한 자세한 내용은 [차원 유형](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)을 참조하세요.|  
|**채널**|채널 차원은 데이터와 메타데이터가 채널 정보를 나타내는 일반 차원입니다.<br /><br /> 일반 차원에 대한 자세한 내용은 [차원 유형](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)을 참조하세요.|  
|**Currency**|통화 차원은 통화 정보를 나타내는 데이터와 메타데이터를 포함합니다.<br /><br /> 통화 차원에 대한 자세한 내용은 [통화 유형 차원 만들기](multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)를 참조하세요.|  
|**고객**|고객 차원은 데이터와 메타데이터가 고객 또는 연락처 정보를 나타내는 일반 차원입니다.<br /><br /> 일반 차원에 대한 자세한 내용은 [차원 유형](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)을 참조하세요.|  
|**Geography**|지리 차원은 데이터와 메타데이터가 구/군/시 또는 우편 번호와 같은 지리 정보를 나타내는 일반 차원입니다.<br /><br /> 일반 차원에 대한 자세한 내용은 [차원 유형](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)을 참조하세요.|  
|**조직**|조직 차원은 데이터와 메타데이터가 직원 또는 계열사와 같은 조직 정보를 나타내는 일반 차원입니다.<br /><br /> 일반 차원에 대한 자세한 내용은 [차원 유형](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)을 참조하세요.|  
|**제품**|제품 차원은 데이터와 메타데이터가 제품 정보를 나타내는 일반 차원입니다.<br /><br /> 일반 차원에 대한 자세한 내용은 [차원 유형](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)을 참조하세요.|  
|**홍보 행사**|홍보 행사 차원은 데이터와 메타데이터가 마케팅 홍보 행사 정보를 나타내는 일반 차원입니다.<br /><br /> 일반 차원에 대한 자세한 내용은 [차원 유형](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)을 참조하세요.|  
|**정량**|정량 차원은 데이터와 메타데이터가 정량 정보를 나타내는 일반 차원입니다.<br /><br /> 일반 차원에 대한 자세한 내용은 [차원 유형](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)을 참조하세요.|  
|**요금**|요율 차원은 환율과 통화 변환 정보를 나타내는 데이터와 메타데이터를 포함합니다.|  
|**Regular**|일반 차원은 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에 가장 많이 사용되는 차원 유형입니다.<br /><br /> 일반 차원에 대한 자세한 내용은 [차원 유형](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)을 참조하세요.|  
|**시나리오**|시나리오 차원은 데이터와 메타데이터가 계획 또는 전략 분석 정보를 나타내는 일반 차원입니다.<br /><br /> 일반 차원에 대한 자세한 내용은 [차원 유형](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)을 참조하세요.|  
|**Time**|시간 차원은 시간 지향적인 데이터와 메타데이터를 포함합니다.<br /><br /> 시간 차원에 대한 자세한 내용은 [날짜 유형 차원 만들기](multidimensional-models/database-dimensions-create-a-date-type-dimension.md)를 참조하세요.|  
|**유틸리티**|유틸리티 차원은 데이터와 메타데이터가 다른 차원 유형과 일치하지 않는 정보를 나타내는 일반 차원입니다.<br /><br /> 일반 차원에 대한 자세한 내용은 [차원 유형](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)을 참조하세요.|  
  
## <a name="dimension-attributes-options"></a>차원 특성 옵션  
  
> [!NOTE]  
>  이 섹션의 옵션은 선택한 **차원 유형** 에 특수 특성 유형이 관련된 경우에만 사용할 수 있습니다. 모든 차원 유형이 특수 특성 유형과 관련된 것은 아닙니다.  
  
 **포함**  
 차원에 특성 유형을 포함하려면 선택합니다.  
  
 **특성 유형**  
 **차원 유형**에서 선택한 차원 유형과 관련된 특성 유형을 표시합니다. 특성 유형에 대한 자세한 내용은 [Type 요소&#40;DimensionAttribute&#41;&#40;ASSL&#41;](scripting/properties/type-element-dimensionattribute-assl.md)를 참조하세요.  
  
 **차원 특성**  
 차원 마법사에서 **특성 유형**에 표시된 특수 특성 유형을 할당할 차원 특성을 선택합니다.  
  
## <a name="see-also"></a>관련 항목  
 [차원 마법사 F1 도움말](dimension-wizard-f1-help.md)   
 [차원 &#40;Analysis Services-다차원 데이터&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [다차원 모델의 차원](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
