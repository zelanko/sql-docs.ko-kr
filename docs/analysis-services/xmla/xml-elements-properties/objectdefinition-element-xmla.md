---
title: ObjectDefinition 요소 (XMLA) | Microsoft Docs
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
- ObjectDefinition Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#ObjectDefinition
- http://schemas.microsoft.com/analysisservices/2003/engine#ObjectDefinition
- microsoft.xml.analysis.objectdefinition
helpviewer_keywords:
- ObjectDefinition element
ms.assetid: 1911868c-a018-4308-8cf9-972a57f610a1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 31127a642891b317118a8ce3995d198fb6426e6e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="objectdefinition-element-xmla"></a>ObjectDefinition 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]하나 이상의 Analysis Services Scripting Language (ASSL) 요소를 만들거나 개체의 인스턴스를 변경 하는 데 포함 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
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
|자식 요소|필수 ASSL 요소. 하나 이상의 ASSL 요소는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 개체를 정의하는 데 사용됩니다. ASSL에 대 한 자세한 내용은 참조 하십시오. [속성 &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md).|  
  
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
 [속성 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
