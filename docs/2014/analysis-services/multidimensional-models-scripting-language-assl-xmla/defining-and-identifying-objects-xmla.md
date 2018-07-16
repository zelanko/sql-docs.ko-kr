---
title: 정의 개체 및 식별 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- identifying objects [XML for Analysis]
- XML for Analysis, objects
- object references [XML for Analysis]
- object identifiers [XML for Analysis]
- object definitions [XML for Analysis]
- XMLA, objects
ms.assetid: 43b65f6d-0123-4556-81f0-c7a0b84361e5
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c788129026d4dffe5c81efc82492fa8a5566de2a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37303043"
---
# <a name="defining-and-identifying-objects-xmla"></a>개체 정의 및 식별(XMLA)
  XMLA(XML for Analysis) 명령에서 개체를 식별하는 데는 개체 식별자와 개체 참조를 사용하며 개체를 정의하는 데는 ASSL(Analysis Services Scripting Language) 요소 XMLA 명령을 사용합니다.  
  
## <a name="object-identifiers"></a>개체 식별자  
 개체의 인스턴스에 정의 된 개체의 고유 식별자를 사용 하 여 식별 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다. 개체 식별자는 명시적으로 지정할 수도 있고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 개체를 만들 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 의해 결정될 수도 있습니다. 사용할 수는 [Discover](../xmla/xml-elements-methods-discover.md) 에 대 한 개체 식별자를 검색 하는 방법 후속 `Discover` 또는 [Execute](../xmla/xml-elements-methods-execute.md) 메서드 호출 합니다.  
  
## <a name="object-references"></a>개체 참조  
 일부 XMLA 명령은 같은 [삭제](../xmla/xml-elements-commands/delete-element-xmla.md) 또는 [프로세스](../xmla/xml-elements-commands/process-element-xmla.md), 개체를 참조 하는 명확한 방식으로 개체 참조를 사용 합니다. 개체 참조에는 명령이 실행되는 대상 개체에 대한 개체 식별자와 해당 개체의 상위 항목에 대한 개체 식별자가 포함됩니다. 예를 들어 파티션의 개체 참조에는 해당 파티션에 대한 개체 식별자와 해당 파티션의 부모 측정값 그룹, 큐브 및 데이터베이스에 대한 개체 식별자가 포함됩니다.  
  
## <a name="object-definitions"></a>개체 정의  
 [만들기](../xmla/xml-elements-commands/create-element-xmla.md) 하 고 [Alter](../xmla/xml-elements-commands/alter-element-xmla.md) XMLA의 명령 만들기 또는 대 한 alter 권한, 각각 개체는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스. 이러한 개체에 대 한 정의가 표시 됩니다는 [ObjectDefinition](../xmla/xml-elements-properties/objectdefinition-element-xmla.md) ASSL의에서 요소를 포함 하는 요소입니다. 사용 하 여 모든 주요 개체와 많은 보조 개체에 대 한 개체 식별자를 명시적으로 지정할 수 있습니다 합니다 [ID](../xmla/xml-elements-properties/id-element-xmla.md) 요소입니다. `ID` 요소를 사용하지 않으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서는 식별할 개체에 따라 명명 규칙을 사용하여 고유 식별자를 제공합니다. 사용 하는 방법에 대 한 자세한 합니다 `Create` 및 `Alter` 개체를 정의 하는 명령을 참조 [만들기 및 변경 개체 &#40;XMLA&#41;](../xmla/xml-elements-objects.md).  
  
## <a name="see-also"></a>관련 항목  
 [개체 요소 &#40;XMLA&#41;](../xmla/xml-elements-properties/object-element-xmla.md)   
 [ParentObject 요소 &#40;XMLA&#41;](../xmla/xml-elements-properties/parentobject-element-xmla.md)   
 [Source 요소 &#40;XMLA&#41;](../xmla/xml-elements-properties/source-element-xmla.md)   
 [Target 요소 &#40;XMLA&#41;](../xmla/xml-elements-properties/target-element-xmla.md)   
 [Analysis Services에서 XMLA를 사용하여 개발](developing-with-xmla-in-analysis-services.md)  
  
  
