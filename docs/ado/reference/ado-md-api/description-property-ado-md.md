---
description: Description 속성(ADO MD)
title: Description 속성 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Description
- Level::Description
- CubeDef::Description
- Hierarchy::Description
- Description
- Dimension::Description
helpviewer_keywords:
- Description property [ADO MD]
ms.assetid: 6d626d35-0bf3-4f24-9934-ad9c9c91273a
author: rothja
ms.author: jroth
ms.openlocfilehash: acc3d3554e4046321b1fe76beebc9dddc942b5ac
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778222"
---
# <a name="description-property-ado-md"></a>Description 속성(ADO MD)
현재 개체의 텍스트 설명을 반환 합니다.  
  
## <a name="return-values"></a>반환 값  
 는 **문자열** 을 반환 하며 읽기 전용입니다.  
  
## <a name="remarks"></a>설명  
 [멤버](./member-object-ado-md.md) 개체에 대 한 **설명은** 측정값 및 수식 멤버에만 적용 됩니다. **Description** 은 다른 모든 멤버 형식에 대해 빈 문자열 ("")을 반환 합니다. 다양 한 멤버 형식에 대 한 자세한 내용은 [Type](./type-property-ado-md.md) 속성을 참조 하세요.  
  
 이 속성은 [수준](./level-object-ado-md.md) 개체에 속하는 **멤버** 개체에 대해서만 지원 됩니다. [Position](./position-object-ado-md.md) 개체에 속하는 **멤버** 개체에서이 속성을 참조 하는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [CubeDef 개체(ADO MD)](./cubedef-object-ado-md.md)  
        [Dimension 개체(ADO MD)](./dimension-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Hierarchy 개체(ADO MD)](./hierarchy-object-ado-md.md)  
        [Level 개체(ADO MD)](./level-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Member 개체(ADO MD)](./member-object-ado-md.md)  
    :::column-end:::
:::row-end:::