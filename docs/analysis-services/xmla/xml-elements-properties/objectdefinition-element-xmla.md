---
title: ObjectDefinition 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b7eefa09388bc6b847d2d9c4d07074102f6c0c79
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="objectdefinition-element-xmla"></a>ObjectDefinition 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  하나 이상의 Analysis Services Scripting Language (ASSL) 요소를 만들거나 개체의 인스턴스를 변경 하는 데 포함 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Create> <!-- or Alter -->  
   ...  
   <ObjectDefinition>  
      <!-- One or more ASSL elements -->  
   </ObjectDefinition>  
   ...  
</Create>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), [만들기](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)|  
|자식 요소|필수 ASSL 요소. 하나 이상의 ASSL 요소는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체를 정의하는 데 사용됩니다. ASSL에 대 한 자세한 내용은 참조 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)합니다.|  
  
## <a name="remarks"></a>주의  
  
## <a name="example"></a>예제  
 다음 예에서는 라는 빈 데이터베이스 **테스트 데이터베이스** 에 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
```  
  
      <Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
   <ObjectDefinition>  
      <Database xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
         <Name>Test Database</Name>  
         <Description>A test database.</Description>  
      </Database>  
   </ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>관련 항목:  
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
