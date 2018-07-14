---
title: Alter 요소 (XMLA) | Microsoft Docs
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
- Alter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Alter
- microsoft.xml.analysis.alter
- urn:schemas-microsoft-com:xml-analysis#Alter
helpviewer_keywords:
- Alter command
ms.assetid: 84e58385-c9ba-48fa-a867-94d35b777a56
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e13819d301af842eb2094d7b6ad3367cde424c72
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192416"
---
# <a name="alter-element-xmla"></a>Alter 요소(XMLA)
  사용 되는 Analysis Services Scripting Language (ASSL) 요소를 포함 합니다 [Execute](../xml-elements-methods-execute.md) 인스턴스의 개체를 변경 하는 방법 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Command>  
   <Alter Scope="enum" AllowCreate="boolean" ObjectExpansion="enum">  
      <Object>...</Object>  
      <ObjectDefinition>...</ObjectDefinition>  
   </Alter>  
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
|자식 요소|[개체](../xml-elements-properties/object-element-xmla.md), [ObjectDefinition](../xml-elements-properties/objectdefinition-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|AllowCreate|선택적 `Boolean` 특성입니다. `Alter` 명령에 정의된 개체가 아직 존재하지 않는 경우 해당 개체를 만들어야 하는지 여부를 나타냅니다.<br /><br /> True로 설정하면 `ObjectDefinition` 요소에 정의된 개체가 아직 존재하지 않는 경우 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에서 생성됩니다. 즉, 개체가 아직 해당 인스턴스에 없는 경우 `Alter` 명령은 `Create` 명령으로 처리됩니다.<br /><br /> 이 특성을 생략하거나 `false`로 설정하면 개체가 아직 존재하지 않는 경우 오류가 발생합니다.|  
|ObjectExpansion|선택적 `Enum` 특성입니다. `Execute` 메서드로 수행할 변경의 범위를 정의합니다.<br /><br /> 경우로 *ObjectProperties*는 `ObjectDefinition` 요소 있어야 변경할 주요 개체의 전체 정의 하위 보조 개체를 포함 합니다. 변경할 개체의 하위 주요 개체는 변경되지 않은 상태로 유지됩니다. **참고:** 사용 하는 경우는 *ObjectProperties* 사용 하 여 설정 합니다 [ClrAssembly](../../scripting/data-type/assembly-data-type-assl.md) 데이터 형식으로는 [데이터](../../scripting/objects/data-element-assl.md) 연결된 된 요소의 [ ClrAssemblyFile](../../scripting/data-type/clrassemblyfile-data-type-assl.md) 데이터 형식을 지정할 필요가 없습니다. 지정하지 않은 경우 `ClrAssembly`는 기존 파일을 사용합니다. <br /><br /> 경우로 *ExpandFull*는 `ObjectDefinition` 요소 뿐만 아니라 변경할 개체의 정의 뿐만 아니라 변경할 개체의 하위 항목인 모든 주요 개체의 정의 포함 해야 합니다. **참고:** 는 *ExpandFull* 설정을 사용 하 여 사용할 수 없습니다는 [Server](../../scripting/objects/server-element-assl.md) 요소입니다.|  
|범위|선택적 `Enum` 특성입니다. `ObjectDefinition` 요소에 정의된 개체의 기간을 정의합니다.<br /><br /> 경우로 *세션*, 정의 된 개체는 `ObjectDefinition` 요소 XMLA 세션 기간 동안만 존재 합니다. **참고:** 사용 하는 경우는 *세션* 설정에 `ObjectDefinition` 요소만 포함할 수 있습니다 [차원](../../scripting/objects/dimension-element-assl.md)를 [큐브](../../scripting/objects/cube-element-assl.md), 또는 [MiningModel ](../../scripting/objects/miningmodel-element-assl.md) ASSL 요소. <br /><br /> 이 특성이 생략된 경우 `ObjectDefinition` 요소에 정의된 개체는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 저장됩니다.|  
  
## <a name="remarks"></a>Remarks  
 각 `Alter` 명령으로 지정 된 부모 개체 아래에 있는 주요 개체 하나의 정의 변경 합니다 [ParentObject](../xml-elements-properties/parentobject-element-xmla.md) 요소입니다.  
  
## <a name="see-also"></a>관련 항목  
 [명령 &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
