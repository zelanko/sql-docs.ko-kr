---
description: Name 속성(ADO MD)
title: Name 속성 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Name
- CubeDef::Name
- Member::Name
- Catalog::Name
- Dimension::Name
- Name
- Axis::Name
- Hierarchy::Name
helpviewer_keywords:
- Name property [ADO MD]
ms.assetid: 4a04380b-51dc-4aaf-8d25-123cdd589641
author: rothja
ms.author: jroth
ms.openlocfilehash: 4dfec86bb631dda661b957e02667cd320c20fec6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986244"
---
# <a name="name-property-ado-md"></a>Name 속성(ADO MD)
개체의 이름을 나타냅니다.  
  
## <a name="return-values"></a>반환 값  
 는 **문자열** 을 반환 하며 읽기 전용입니다.  
  
## <a name="remarks"></a>설명  
 서 수 참조로 개체의 **이름** 속성을 검색할 수 있으며, 그 후에는 개체를 이름으로 직접 참조할 수 있습니다. 예를 들어가 `cdf.CubeDefs(0).Name` "Bobs 비디오 저장소"를 생성 하는 경우이 [CubeDef](./cubedef-object-ado-md.md) 를으로 참조할 수 있습니다 `cdf.CubeDefs("Bobs Video Store")` .  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [Axis 개체(ADO MD)](./axis-object-ado-md.md)  
        [Catalog 개체(ADO MD)](./catalog-object-ado-md.md)  
        [CubeDef 개체(ADO MD)](./cubedef-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Dimension 개체(ADO MD)](./dimension-object-ado-md.md)  
        [Hierarchy 개체(ADO MD)](./hierarchy-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Level 개체(ADO MD)](./level-object-ado-md.md)  
        [Member 개체(ADO MD)](./member-object-ado-md.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [Catalog 예제 (VB)](./catalog-example-vb.md)   
 [Caption 속성 (ADO MD)](./caption-property-ado-md.md)   
 [Description 속성 (ADO MD)](./description-property-ado-md.md)   
 [UniqueName 속성(ADO MD)](./uniquename-property-ado-md.md)