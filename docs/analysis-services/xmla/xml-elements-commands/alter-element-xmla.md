---
title: Alter 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Alter Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Alter
- microsoft.xml.analysis.alter
- urn:schemas-microsoft-com:xml-analysis#Alter
helpviewer_keywords:
- Alter command
ms.assetid: 84e58385-c9ba-48fa-a867-94d35b777a56
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d6d234801cb298f15982bfc4ac1d75a493dd6aa8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="alter-element-xmla"></a>Alter 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]사용 하는 Analysis Services Scripting Language (ASSL) 요소를 포함 된 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 개체의 인스턴스를 변경 하려면 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
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
|부모 요소|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|자식 요소|[개체](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [ObjectDefinition](../../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|AllowCreate|(선택 사항 **부울** 특성)에 정의 된 개체가 있는지 여부를 나타내는 **Alter** 존재 하지 않을 경우 명령을 만들어야 합니다.<br /><br /> 경우에 정의 된 개체를 true로 설정 된 **ObjectDefinition** 요소에 생성 됩니다는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 이미 존재 하지 않는 경우 인스턴스. 즉,는 **Alter** 명령으로 처리 됩니다는 **만들기** 경우는 개체가 존재 하지 않는 이미 인스턴스에서 명령입니다.<br /><br /> 이 특성이 생략 되거나로 설정 된 경우 **false**, 개체가 아직 존재 하지 않는 경우 오류가 발생 합니다.|  
|ObjectExpansion|(선택 사항 **열거형** 특성)에서 수행할 변경의 범위를 정의 고 **Execute** 메서드.<br /><br /> 경우로 설정 *ObjectProperties*, **ObjectDefinition** 요소 포함 되어야 변경, 주요 개체의 전체 정의 하위 보조 개체를 포함 합니다. 변경할 개체의 하위 주요 개체는 변경되지 않은 상태로 유지됩니다.<br /><br /> 참고: 사용 하는 경우는 *ObjectProperties* 사용 하 여 설정 된 [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) 데이터 형식으로는 [데이터](../../../analysis-services/scripting/objects/data-element-assl.md) 관련 된 요소 [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) 데이터 형식을 지정할 필요가 없습니다. 지정 하지 않으면는 **ClrAssembly** 기존 파일을 사용 합니다.<br /><br /> 경우 설정 *ExpandFull*, **ObjectDefinition** 요소 뿐 아니라 변경, 개체의 정의 뿐만 아니라 개체의 하위 항목인 모든 주요 개체의 정의 포함 되어야 변경 합니다.<br /><br /> 참고:는 *ExpandFull* 설정은 함께 사용할 수 없습니다는 [서버](../../../analysis-services/scripting/objects/server-element-assl.md) 요소입니다.|  
|범위|(선택 사항 **Enum** 특성)에 정의 된 개체의 기간을 정의 **ObjectDefinition** 요소입니다.<br /><br /> 경우로 설정 *세션*에 정의 된 개체는 **ObjectDefinition** 요소 XMLA 세션 기간 동안만 존재 합니다.<br /><br /> 참고: 사용 하는 경우는 *세션* 설정을 **ObjectDefinition** 요소만 포함할 수 있습니다 [차원](../../../analysis-services/scripting/objects/dimension-element-assl.md), [큐브](../../../analysis-services/scripting/objects/cube-element-assl.md), 또는 [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) ASSL 요소.<br /><br /> 이 특성이 생략 된 경우 개체에 정의 된 **ObjectDefinition** 요소는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스.|  
  
## <a name="remarks"></a>주의  
 각 **Alter** 명령으로 지정 된 부모 개체 아래로 주요 개체 하나의 정의 변경 합니다.는 [ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md) 요소입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [명령 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
