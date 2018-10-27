---
title: 삽입, 업데이트 및 삭제 (XMLA) 멤버 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- inserting dimension members
- XML for Analysis, members
- removing dimension members
- dropping dimension members
- write-enabled dimensions [Analysis Services]
- XMLA, members
- deleting dimension members
- dimensions [Analysis Services], XML for Analysis
ms.assetid: bba922b5-8b88-4051-9506-ff055248182a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c1c30b916d910b93b53ae10a9eefaa19d45c957a
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148028"
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>멤버 삽입, 업데이트 및 삭제(XMLA)
  사용할 수는 [삽입](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)를 [업데이트](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla), 및 [Drop](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla) 명령은 xml에서 for Analysis (XMLA) 삽입, 업데이트 또는 쓰기 가능 차원에서 멤버를 삭제 합니다. 쓰기 가능 차원에 대 한 자세한 내용은 참조 하세요. [쓰기 가능한 차원](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)합니다.  
  
## <a name="inserting-new-members"></a>새 멤버 삽입  
 `Insert` 명령은 쓰기 가능 차원에서 지정된 특성에 새 멤버를 삽입합니다.  
  
 `Insert` 명령을 생성하기 전에 새 멤버 삽입을 위한 다음 정보가 필요합니다.  
  
-   새 멤버를 삽입할 차원.  
  
-   새 멤버를 삽입할 차원 특성.  
  
-   이름의 적용할 수 있는 번역을 포함한 새 멤버의 이름.  
  
-   새 멤버의 키. 특성이 복합 키를 사용하는 경우 이 키에는 값이 여러 개 필요할 수 있습니다.  
  
-   차원 내에서 다른 특성으로 구현되지 않은 적용 가능한 모든 특성 속성의 값. 이러한 특성 속성에는 단항 연산, 번역, 사용자 지정 롤업, 사용자 지정 롤업 속성 및 건너뛴 수준이 있습니다.  
  
 `Insert` 명령에서는 다음과 같은 두 개의 속성만 사용합니다.  
  
-   합니다 [개체](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) 멤버를 삽입할에 차원에 대 한 개체 참조를 포함 하는 속성입니다. 개체 참조는 차원에 대한 데이터베이스 식별자, 큐브 식별자 및 차원 식별자를 포함합니다.  
  
-   합니다 [특성](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attributes-element-xmla) 속성을 하나 이상 포함 [특성](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attribute-element-xmla) 멤버를 삽입할에 특성을 식별 하는 요소입니다. 각 `Attribute` 요소는 특성을 식별하며 식별된 특성에 추가할 단일 멤버의 이름, 값, 번역, 단항 연산자, 사용자 지정 롤업, 사용자 지정 롤업 속성 및 건너뛴 수준을 제공합니다.  
  
    > [!NOTE]  
    >  `Attribute` 요소의 모든 속성이 포함되어야 합니다. 그렇지 않으면 오류가 발생할 수 있습니다.  
  
## <a name="updating-existing-members"></a>기존 멤버 업데이트  
 `Update` 명령에서는 쓰기 가능 차원에서 다른 특성의 다른 멤버와의 관계를 기반으로 지정된 특성의 기존 멤버를 업데이트합니다. `Update` 명령은 차원에 포함된 계층의 다른 수준으로 멤버를 이동할 수 있으며 부모 특성에 따라 정의된 부모-자식 계층을 다시 구성하는 데 사용할 수 있습니다.  
  
 `Update` 명령을 생성하기 전에 멤버 업데이트를 위한 다음 정보가 필요합니다.  
  
-   기존 멤버를 업데이트할 차원.  
  
-   기존 멤버를 업데이트할 차원 특성.  
  
-   기존 멤버의 키. 특성이 복합 키를 사용하는 경우 이 키에는 값이 여러 개 필요할 수 있습니다.  
  
-   차원 내에서 다른 특성으로 구현되지 않은 적용 가능한 모든 특성 속성의 값. 이러한 특성 속성에는 단항 연산, 번역, 사용자 지정 롤업, 사용자 지정 롤업 속성 및 건너뛴 수준이 있습니다.  
  
 `Update` 명령에서는 다음과 같은 세 개의 필수 속성만을 사용합니다.  
  
-   업데이트할 멤버의 차원에 대한 개체 참조가 포함된 `Object` 속성. 개체 참조는 차원에 대한 데이터베이스 식별자, 큐브 식별자 및 차원 식별자를 포함합니다.  
  
-   업데이트할 멤버의 특성을 식별하는 하나 이상의 `Attributes` 요소가 포함된 `Attribute` 속성. `Attribute` 요소는 특성을 식별하며 식별된 특성에 대해 업데이트된 단일 멤버의 이름, 값, 번역, 단항 연산자, 사용자 지정 롤업, 사용자 지정 롤업 속성 및 건너뛴 수준을 제공합니다.  
  
    > [!NOTE]  
    >  `Attribute` 요소의 모든 속성이 포함되어야 합니다. 그렇지 않으면 오류가 발생할 수 있습니다.  
  
-   [여기서](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/where-element-xmla) 속성을 하나 이상 포함 `Attribute` 멤버를 업데이트할에 특성을 제한 하는 요소입니다. `Where` 속성은 `Update` 명령을 멤버의 특정 인스턴스로 제한하는 데 유용하게 사용됩니다. 경우는 `Where` 속성이 지정 되지 않은, 지정된 된 멤버의 모든 인스턴스가 업데이트 됩니다. 예를 들어, 세 명의 고객에 대한 도시 이름을 Redmond에서 Bellevue로 변경하려고 합니다. 도시 이름을 변경하려면 변경해야 하는 City 특성의 멤버에 대해 Customer 특성의 세 멤버를 식별하는 `Where` 속성을 제공해야 합니다. 이 `Where` 속성을 제공하지 않으면 `Update` 명령 실행 후에 도시 이름이 현재 Redmond로 되어 있는 모든 고객의 도시 이름이 Bellevue로 변경됩니다.  
  
    > [!NOTE]  
    >  `Update` 명령에서는 새 멤버를 제외하고 `Where` 절에 포함되지 않은 특성의 특성 키 값만을 업데이트할 수 있습니다. 예를 들어, 고객을 업데이트하는 경우 도시 이름을 업데이트할 수 없습니다. 이렇게 하지 않으면 모든 고객의 도시 이름이 변경됩니다.  
  
### <a name="updating-members-in-parent-attributes"></a>부모 특성의 멤버 업데이트  
 부모 특성을 지원 하 여 `Update` 명령에 선택적 [MoveWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/movewithdescendants-element-xmla)위해 속성입니다. `MoveWithDescendants` 속성을 true로 설정하면 부모 멤버의 식별자가 변경될 때 부모 멤버의 하위 항목도 부모 멤버와 함께 이동합니다. 이 값을 false로 설정한 경우 부모 멤버를 이동하면 해당 부모 멤버의 직계 하위 항목이 부모 멤버의 이전 수준으로 승격됩니다.  
  
 부모 특성의 멤버를 업데이트할 때 `Update` 명령은 다른 특성의 멤버를 업데이트할 수 없습니다.  
  
## <a name="dropping-existing-members"></a>기존 멤버 삭제  
 `Drop` 명령을 생성하기 전에 멤버 삭제를 위한 다음 정보가 필요합니다.  
  
-   기존 멤버를 삭제할 차원.  
  
-   기존 멤버를 삭제할 차원 특성.  
  
-   삭제할 기존 멤버의 키. 특성이 복합 키를 사용하는 경우 이 키에는 값이 여러 개 필요할 수 있습니다.  
  
 `Drop` 명령에서는 다음과 같은 두 개의 필수 속성만을 사용합니다.  
  
-   삭제할 멤버의 차원에 대한 개체 참조가 포함된 `Object` 속성. 개체 참조는 차원에 대한 데이터베이스 식별자, 큐브 식별자 및 차원 식별자를 포함합니다.  
  
-   삭제할 멤버의 특성을 제한하는 하나 이상의 `Where` 요소가 포함된 `Attribute` 속성. `Where` 속성은 `Drop` 명령을 멤버의 특정 인스턴스로 제한하는 데 유용하게 사용됩니다. `Where` 명령을 지정하지 않으면 지정된 멤버의 모든 인스턴스가 삭제됩니다. 예를 들어, Redmond의 고객 세 명을 삭제하려고 합니다. 이러한 고객을 삭제하려면 제거할 Customer 특성의 세 멤버와 세 고객을 제거할 City 특성의 Redmond 멤버를 식별하는 `Where` 속성을 제공해야 합니다. `Where` 속성에 City 특성의 Redmond 멤버만 지정된 경우 `Drop` 명령에 의해 Redmond에 연결된 모든 고객이 삭제됩니다. `Where` 속성에 Customer 특성의 세 멤버만 지정된 경우 `Drop` 명령에 의해 세 명의 고객이 완전히 삭제됩니다.  
  
    > [!NOTE]  
    >  `Attribute` 명령에 포함된 `Drop` 요소는 `AttributeName` 및 `Keys` 속성만을 포함해야 합니다. 그렇지 않으면 오류가 발생할 수 있습니다.  
  
### <a name="dropping-members-in-parent-attributes"></a>부모 특성의 멤버 삭제  
 설정 된 [DeleteWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/deletewithdescendants-element-xmla) 속성은 부모 멤버를 사용 하 여도 부모 멤버의 하위 항목을 삭제 해야 함을 나타냅니다. 이 값을 false로 설정한 경우에는 부모 멤버의 직계 하위 항목이 부모 멤버의 이전 수준으로 승격됩니다.  
  
> [!IMPORTANT]  
>  부모 멤버와 해당 하위 항목을 모두 삭제하려면 부모 멤버에 대한 삭제 권한만 있으면 됩니다. 하위 항목에 대한 삭제 권한은 필요하지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Drop 요소 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)   
 [요소를 삽입 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)   
 [Update 요소 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [개체 정의 및 식별 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)   
 [Analysis Services에서 XMLA를 사용하여 개발](developing-with-xmla-in-analysis-services.md)  
  
  
