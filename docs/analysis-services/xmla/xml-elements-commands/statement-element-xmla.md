---
title: Statement 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 49238b50457a586bbf23cc75ee454003c57ac04e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979165"
---
# <a name="statement-element-xmla"></a>Statement 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  쿼리 또는 문을 전송할 포함를 사용 하 여 합니다 **Execute** Analysis Services 인스턴스에 메서드.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Statement>...</Statement>  
</Command>  
```  
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 합니다 **문** 명령에서 쿼리 또는 문을 실행 합니다 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]가 지원하는 언어는 다음과 같습니다.  
  
-   MDX(Multidimensional Expressions)  
  
-   MDX(Data Mining Extensions)  
  
-   SQL(구조적 쿼리 언어) 하위 집합  
  
## <a name="see-also"></a>참고자료
 [명령 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
