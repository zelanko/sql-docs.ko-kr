---
title: Statement 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d9197a13f1d21492d7a7f6af9c3e33b6d71e0ad0
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="statement-element-xmla"></a>Statement 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  쿼리 또는 문을 보낼 포함를 사용 하는 **Execute** 메서드의 인스턴스를 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Statement>...</Statement>  
</Command>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **문을** 명령에 쿼리 또는 문을 실행의 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]가 지원하는 언어는 다음과 같습니다.  
  
-   MDX(Multidimensional Expressions)  
  
-   MDX(Data Mining Extensions)  
  
-   SQL(구조적 쿼리 언어) 하위 집합  
  
## <a name="see-also"></a>관련 항목:  
 [명령 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
