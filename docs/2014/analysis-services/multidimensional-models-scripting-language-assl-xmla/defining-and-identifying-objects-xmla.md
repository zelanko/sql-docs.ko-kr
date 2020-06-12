---
title: 개체 정의 및 식별 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
author: minewiskan
ms.author: owend
ms.openlocfilehash: d2fd3263a2f8050c36747a81ab3473f5b405ef21
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545033"
---
# <a name="defining-and-identifying-objects-xmla"></a>개체 정의 및 식별(XMLA)
  XMLA(XML for Analysis) 명령에서 개체를 식별하는 데는 개체 식별자와 개체 참조를 사용하며 개체를 정의하는 데는 ASSL(Analysis Services Scripting Language) 요소 XMLA 명령을 사용합니다.  
  
## <a name="object-identifiers"></a>개체 식별자  
 개체는 인스턴스에 정의 된 개체의 고유 식별자를 사용 하 여 식별 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . 개체 식별자는 명시적으로 지정할 수도 있고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 개체를 만들 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 의해 결정될 수도 있습니다. [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) 메서드를 사용 하 여 후속 `Discover` 또는 [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) 메서드 호출에 대 한 개체 식별자를 검색할 수 있습니다.  
  
## <a name="object-references"></a>개체 참조  
 [Delete](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla) 또는 [Process](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)와 같은 일부 XMLA 명령은 개체 참조를 사용 하 여 명확한 방식으로 개체를 참조 합니다. 개체 참조에는 명령이 실행되는 대상 개체에 대한 개체 식별자와 해당 개체의 상위 항목에 대한 개체 식별자가 포함됩니다. 예를 들어 파티션의 개체 참조에는 해당 파티션에 대한 개체 식별자와 해당 파티션의 부모 측정값 그룹, 큐브 및 데이터베이스에 대한 개체 식별자가 포함됩니다.  
  
## <a name="object-definitions"></a>개체 정의  
 XMLA의 [create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) 및 [alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) 명령은 인스턴스의 개체를 각각 생성 하거나 변경 합니다 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . 이러한 개체에 대 한 정의는 개체의 요소가 포함 된 [Objectdefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) 요소로 표시 됩니다. [ID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) 요소를 사용 하 여 모든 주요 개체와 많은 보조 개체에 대해 개체 식별자를 명시적으로 지정할 수 있습니다. `ID` 요소를 사용하지 않으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서는 식별할 개체에 따라 명명 규칙을 사용하여 고유 식별자를 제공합니다. 및 명령을 사용 하 여 개체를 정의 하는 방법에 대 한 자세한 내용은 `Create` `Alter` [개체 만들기 및 변경 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XMLA&#41;&#40;개체 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [ParentObject 요소 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [원본 요소 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)   
 [XMLA&#41;대상 요소 &#40;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)   
 [Analysis Services에서 XMLA를 사용하여 개발](developing-with-xmla-in-analysis-services.md)  
  
  
