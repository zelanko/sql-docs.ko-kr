---
description: Axes 컬렉션(ADO MD)
title: 축 컬렉션 (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axes
- Cellset::Axes
helpviewer_keywords:
- Axes collection [ADO MD]
ms.assetid: 072fb21a-ec0f-4b02-9022-1cef3ad4bfff
author: rothja
ms.author: jroth
ms.openlocfilehash: 33839c31745976cc6df89e02b728a25ae8624fa5
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776711"
---
# <a name="axes-collection-ado-md"></a>Axes 컬렉션(ADO MD)
셀 집합을 정의 하는 [축](./axis-object-ado-md.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 [셀 집합](./cellset-object-ado-md.md) 개체는 **축** 컬렉션을 포함 합니다. **셀 집합** 을 열면이 컬렉션에 하나 이상의 **축**이 포함 됩니다. **축 개체를 사용 하** 는 방법에 대 한 자세한 설명은 [axis](./axis-object-ado-md.md) 개체를 참조 하세요.  
  
> [!NOTE]
>  **셀 집합** 의 필터 축은 **축** 컬렉션에 포함 되지 않습니다. 자세한 내용은 [Filteraxis](./filteraxis-property-ado-md.md) 속성을 참조 하세요.  
  
 **축은** 표준 ADO 컬렉션입니다. 컬렉션의 속성과 메서드를 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Count](../ado-api/count-property-ado.md) 속성을 사용 하 여 컬렉션의 개체 수를 가져옵니다.  
  
-   기본 [항목](../ado-api/item-property-ado.md) 속성을 사용 하 여 컬렉션에서 개체를 반환 합니다.  
  
-   [Refresh](../ado-api/refresh-method-ado.md) 메서드를 사용 하 여 공급자에서 컬렉션의 개체를 업데이트 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [속성, 메서드 및 이벤트](./axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [셀 집합 예제 (VB)](./cellset-example-vb.md)   
 [Axis 개체(ADO MD)](./axis-object-ado-md.md)