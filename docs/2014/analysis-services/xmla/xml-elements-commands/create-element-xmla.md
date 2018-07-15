---
title: Create 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Create Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Create
- urn:schemas-microsoft-com:xml-analysis#Create
- microsoft.xml.analysis.create
helpviewer_keywords:
- Create command (XMLA)
ms.assetid: a623d362-a1ac-40e4-8816-65fac89cb391
caps.latest.revision: 17
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a3679fd48885b3538996b38286709e14b665bef0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247735"
---
# <a name="create-element-xmla"></a>Create 요소(XMLA)
  사용 되는 Analysis Services Scripting Language (ASSL) 요소를 포함 합니다 `Execute` 에서 개체를 만드는 방법을 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.  
  
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[Command](../xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[ObjectDefinition](../xml-elements-properties/objectdefinition-element-xmla.md), [ParentObject](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|AllowOverwrite|선택적 `Boolean` 특성입니다. 이 값을 True로 설정하면 `ObjectDefinition` 요소에 정의된 개체가 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스의 기존 개체를 덮어쓸 수 있습니다. 이 특성이 생략되거나 False로 설정된 경우 기존 개체가 있으면 오류가 발생합니다.|  
|범위|선택적 `Enum` 특성입니다. `ObjectDefinition` 요소에 정의된 개체의 지속 기간을 정의합니다. 이 특성이 생략된 경우 `ObjectDefinition` 요소에 정의된 개체는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 저장됩니다. 사용할 수 있는 값은 다음과 같습니다.<br /><br /> -   *세션*<br />     `ObjectDefinition` 요소에 정의된 개체가 XMLA(XML for Analysis) 세션이 지속되는 동안에만 존재합니다. **참고:** 사용 하는 경우는 *세션* 설정에 `ObjectDefinition` 요소만 포함할 수 있습니다 [차원](../../scripting/objects/dimension-element-assl.md)를 [큐브](../../scripting/objects/cube-element-assl.md), 또는 [MiningModel ](../../scripting/objects/miningmodel-element-assl.md) ASSL 요소.|  
  
## <a name="remarks"></a>Remarks  
 각 `Create` 작업은 `ParentObject` 요소에서 지정하는 부모 아래에 주요 개체 하나를 만듭니다. 부모 개체가 생략된 경우 대상 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스인 것으로 간주됩니다. 주요 개체의 부모가 대상 인스턴스가 아니면 오류가 발생합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에서 `Test Database`라는 빈 데이터베이스를 만듭니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
