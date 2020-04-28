---
title: 모델&gt;에서 &lt;선택 합니다. DIMENSION_CONTENT (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7fac89454cd31c1334e41d4c2367143f31476e20
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67928365"
---
# <a name="select-from-ltmodelgtdimension_content-dmx"></a>모델&gt;에서 &lt;선택 합니다. DIMENSION_CONTENT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  OLAP 큐브에서 모델의 각 노드가 차원 멤버를 나타내도록 하여 마이닝 모델을 차원으로 사용할 수 있습니다. **SELECT FROM \<model>입니다. Dimension_CONTENT** 문은 차원으로 사용 하는 것과 관련 된 모델의 콘텐츠를 반환 합니다.  
  
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
  
 *model*  
 모델 식별자입니다.  
  
 *조건 식*  
 (선택 사항) 열 목록에서 반환되는 값을 제한하는 조건입니다.  
  
 *expression*  
 (선택 사항) 스칼라 값을 반환하는 식입니다.  
  
## <a name="remarks"></a>설명  
 알고리즘 공급자는 반환되는 내용과 이 내용의 구성 방법을 정의합니다. 예를 들어 공급자는 차원 내용에 설명된 노드 수를 제한할 수 있습니다.  
  
 다음 표에서는 차원 내용에 대해 쿼리할 수 있는 열 및 각 열이 데이터 마이닝 차원으로서 수행하는 함수를 나열합니다.  
  
|CONTENT 행 집합 열|데이터 마이닝 차원의 함수|  
|---------------------------|---------------------------------------|  
|ATTRIBUTE_NAME|멤버 속성|  
|NODE_NAME|멤버 속성|  
|NODE_UNIQUE_NAME|키 특성|  
|NODE_TYPE|멤버 속성|  
|NODE_CAPTION|**키** 특성에 대 한 CaptionColumn입니다.|  
|CHILDREN_CARDINALITY|멤버 속성|  
|PARENT_UNIQUE_NAME|**키** 특성 (부모-자식 계층의 parentattribute)에 대 한 RelatedAttribute입니다.|  
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
  
## <a name="see-also"></a>참고 항목  
 [DMX &#40;선택&#41;](../dmx/select-dmx.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 정의 문](../dmx/dmx-statements-data-definition.md)   
 [데이터 마이닝 확장 &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#40;Data Mining Extensions&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
