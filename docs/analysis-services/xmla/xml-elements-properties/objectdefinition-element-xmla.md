---
title: ObjectDefinition 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 71a8b5fe9e5fe1778ca941a597f86fb13249d623
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575895"
---
# <a name="objectdefinition-element-xmla"></a>ObjectDefinition 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  만들거나 변경할의 Analysis Services 인스턴스에서 개체에 사용 되는 하나 이상의 Analysis Services Scripting Language (ASSL) 요소를 포함 합니다.  
  
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), [만들기](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)|  
|자식 요소|필수 ASSL 요소. 하나 이상의 ASSL 요소는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체를 정의하는 데 사용됩니다. ASSL에 대 한 자세한 내용은 참조 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)합니다.|  
  
## <a name="remarks"></a>Remarks  
  
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
  
## <a name="see-also"></a>참고자료
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
