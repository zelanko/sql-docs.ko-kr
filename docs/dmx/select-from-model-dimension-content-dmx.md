---
title: SELECT FROM &lt;모델&gt;합니다. DIMENSION_CONTENT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 29f730f0bdff985ffceb849c429e5d1b02f70d5f
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842526"
---
# <a name="select-from-ltmodelgtdimensioncontent-dmx"></a>SELECT FROM &lt;모델&gt;합니다. DIMENSION_CONTENT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  OLAP 큐브에서 모델의 각 노드가 차원 멤버를 나타내도록 하여 마이닝 모델을 차원으로 사용할 수 있습니다. **SELECT FROM \<모델 >. Dimension_CONTENT** 문은 차원으로 사용 하기 적합 한 모델 내용을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.Dimension_CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>인수  
 *n*  
 (선택 사항) 반환할 행의 수를 지정하는 정수입니다.  
  
 *식 목록*  
 관련 열 식별자의 쉼표로 구분된 목록이며 내용 스키마 행 집합에서 파생됩니다.  
  
 *모델*  
 모델 식별자입니다.  
  
 *조건 식*  
 (선택 사항) 열 목록에서 반환되는 값을 제한하는 조건입니다.  
  
 *expression*  
 (선택 사항) 스칼라 값을 반환하는 식입니다.  
  
## <a name="remarks"></a>Remarks  
 알고리즘 공급자는 반환되는 내용과 이 내용의 구성 방법을 정의합니다. 예를 들어 공급자는 차원 내용에 설명된 노드 수를 제한할 수 있습니다.  
  
 다음 표에서는 차원 내용에 대해 쿼리할 수 있는 열 및 각 열이 데이터 마이닝 차원으로서 수행하는 함수를 나열합니다.  
  
|CONTENT 행 집합 열|데이터 마이닝 차원의 함수|  
|---------------------------|---------------------------------------|  
|ATTRIBUTE_NAME|멤버 속성|  
|NODE_NAME|멤버 속성|  
|NODE_UNIQUE_NAME|키 특성|  
|NODE_TYPE|멤버 속성|  
|NODE_CAPTION|에 대 한 CaptionColumn **키** 특성입니다.|  
|CHILDREN_CARDINALITY|멤버 속성|  
|PARENT_UNIQUE_NAME|**키** 특성 (부모-자식 계층 구조의 ParentAttribute).|  
|NODE_DESCRIPTION|멤버 속성|  
|NODE_RULE|멤버 속성|  
|MARGINAL_RULE|멤버 속성|  
|NODE_PROBABILITY|멤버 속성|  
|MARGINAL_PROBABILITY|멤버 속성|  
|NODE_SUPPORT|멤버 속성|  
  
## <a name="examples"></a>예  
  
### <a name="description"></a>Description  
 이 예에서는 `[TM Decision Tree]` 모델 내용에서 모델을 차원으로 사용하는 데 적합한 모든 열을 선택합니다.  
  
### <a name="code"></a>코드  
  
```  
SELECT *   
FROM [TM Decision Tree].Dimension_Content  
```  
  
## <a name="see-also"></a>관련 항목  
 [선택 &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [Data Mining Extensions &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
