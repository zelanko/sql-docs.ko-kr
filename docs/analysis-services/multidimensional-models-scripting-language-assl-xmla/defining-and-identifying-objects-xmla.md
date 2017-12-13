---
title: "(XMLA) 개체 정의 및 식별 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- objects [XML for Analysis]
- identifying objects [XML for Analysis]
- XML for Analysis, objects
- object references [XML for Analysis]
- object identifiers [XML for Analysis]
- object definitions [XML for Analysis]
- XMLA, objects
ms.assetid: 43b65f6d-0123-4556-81f0-c7a0b84361e5
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bb3185b6c95807fa4adb383844a62dcb14342a7c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="defining-and-identifying-objects-xmla"></a>개체 정의 및 식별(XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]개체는 XML에서 개체 식별자 및 개체 참조를 사용 하 여 Analysis (XMLA) 명령에 대 한 식별 되 고 Analysis Services Scripting Language (ASSL) 요소 XMLA 명령을 사용 하 여 정의 됩니다.  
  
## <a name="object-identifiers"></a>개체 식별자  
 인스턴스에서 정의 된 개체의 고유 식별자를 사용 하 여 식별 되는 개체 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다. 개체 식별자는 명시적으로 지정할 수도 있고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 개체를 만들 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 의해 결정될 수도 있습니다. 사용할 수는 [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) 에 대 한 개체 식별자를 검색할 메서드 후속 **Discover** 또는 [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드를 호출 합니다.  
  
## <a name="object-references"></a>개체 참조  
 일부 XMLA 명령은 같은 [삭제](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md) 또는 [프로세스](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md), 개체 참조를 사용 하 여 모호 하지 않은 방식에서으로 개체를 참조 합니다. 개체 참조에는 명령이 실행되는 대상 개체에 대한 개체 식별자와 해당 개체의 상위 항목에 대한 개체 식별자가 포함됩니다. 예를 들어 파티션의 개체 참조에는 해당 파티션에 대한 개체 식별자와 해당 파티션의 부모 측정값 그룹, 큐브 및 데이터베이스에 대한 개체 식별자가 포함됩니다.  
  
## <a name="object-definitions"></a>개체 정의  
 [만들기](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md) 및 [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) XMLA의 명령 개체 만들거나 변경, 각각에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스. 이러한 개체에 대 한 정의로 표시 됩니다는 [ObjectDefinition](../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md) ASSL의에서 요소를 포함 하는 요소입니다. 사용 하 여 모든 주요 개체와 많은 보조 개체에 대 한 개체 식별자를 명시적으로 지정할 수 있습니다는 [ID](../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md) 요소입니다. 경우는 **ID** 요소가 사용 되지 않습니다는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 식별할 개체에 의존 하는 명명 규칙의 고유 식별자를 제공 합니다. 사용 하는 방법에 대 한 자세한 내용은 **만들기** 및 **Alter** 개체를 정의 하는 명령을 참조 [만들기 및 개체 변경 &#40; XMLA &#41; ](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md).  
  
## <a name="see-also"></a>관련 항목:  
 [Object 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [ParentObject 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)   
 [Source 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)   
 [Target 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)   
 [Analysis Services에서 XMLA를 사용하여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
