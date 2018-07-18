---
title: WritebackTableCreation 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e04f44d9caa3ae51ea141997e83de54524000fee
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38046733"
---
# <a name="writebacktablecreation-element-xmla"></a>WritebackTableCreation 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  하는 동안 쓰기 저장 테이블을 만들지 여부를 결정 합니다 [프로세스](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) 작업 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Process>  
...  
   <WritebackTableCreation>...</WritebackTableCreation>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[처리](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 Analysis Services 인스턴스에서 개체를 사용할 수 있는 처리 옵션에 대 한 자세한 내용은 참조 [다차원 모델 처리 &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)합니다.  
  
 **WritebackTableCreation** 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*만들기*|쓰기 저장 테이블이 없는 경우 새 쓰기 저장 테이블을 만듭니다. 쓰기 저장 테이블이 이미 있으면 오류가 발생합니다.|  
|*CreateAlways*|새 쓰기 저장 테이블을 만들고 기존 쓰기 저장 테이블이 있으면 덮어씁니다.|  
|*Useexisting이*|기존 쓰기 저장 테이블이 있으면 사용합니다. 기존 쓰기 저장 테이블이 없으면 오류가 발생합니다.|  
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
