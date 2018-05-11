---
title: Create 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb4183c650c82123693e3d217e52e585130f4d36
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="create-element-xmla"></a>Create 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  사용 하는 Analysis Services Scripting Language (ASSL) 요소를 포함 된 **Execute** 메서드 개체를 만들는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Create Scope="enum" AllowOverwrite="boolean">  
      <ParentObject>...</ParentObject>  
      <ObjectDefinition>...</ObjectDefinition>  
   </Create>  
</Command>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[ObjectDefinition](../../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md), [ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|Attribute|설명|  
|---------------|-----------------|  
|AllowOverwrite|선택적 **Boolean** 특성입니다. 경우 True로 설정 된 개체에 정의 된는 **ObjectDefinition** 요소에서 기존 개체를 덮어쓸 수는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. 이 특성이 생략되거나 False로 설정된 경우 기존 개체가 있으면 오류가 발생합니다.|  
|범위|선택적 **Enum** 특성입니다. **ObjectDefinition** 요소에 정의된 개체의 지속 기간을 정의합니다. 이 특성이 생략 된 경우 개체에 정의 된 **ObjectDefinition** 요소는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스. 다음 값을 사용할 수 있습니다.<br /><br /> *세션*:에 정의 된 개체는 **ObjectDefinition** 요소 Analysis (XMLA) 세션에 대 한 XML의 기간 동안만 존재 합니다.<br />                  사용할 때의 *세션* 설정을 **ObjectDefinition** 요소만 포함할 수 있습니다 [차원](../../../analysis-services/scripting/objects/dimension-element-assl.md), [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md), 또는 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) ASSL 요소.|  
  
## <a name="remarks"></a>주의  
 각 **Create** 작업은 **ParentObject** 요소에서 지정하는 부모 아래에 주요 개체 하나를 만듭니다. 부모 개체가 생략된 경우 대상 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스인 것으로 간주됩니다. 주요 개체의 부모가 대상 인스턴스가 아니면 오류가 발생합니다.  
  
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
 [명령 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
