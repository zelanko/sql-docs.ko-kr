---
title: RequestType 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cc420aa56d535c826bcff4b78739740e8e5f6bbe
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="requesttype-element-xmla"></a>RequestType 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  반환 된 메타 데이터의 유형을 결정는 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Discover>  
   ...  
   <RequestType>...</RequestType>  
   ...  
</Discover>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[검색](../../../analysis-services/xmla/xml-elements-methods-discover.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **RequestType** 있는 스키마 행 집합을 결정 하는 요소는 **Discover** 메서드 데이터를 반환 합니다. 지 원하는 스키마 행 집합의 이름에 제한 된이 열거형은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다. 스키마 행 집합에 대 한 자세한 내용은 참조 [Analysis Services 스키마 행 집합](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)합니다.  
  
> [!NOTE]  
>  **RequestType** 요소는 스키마 행 집합 이름만 열거 합니다. 스키마 행 집합 GUID를 사용하면 오류가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
