---
description: CursorLocation 속성(ADO)
title: CursorLocation 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::CursorLocation
- Recordset15::CursorLocation
helpviewer_keywords:
- CursorLocation property [ADO]
ms.assetid: 39c8d86e-7ee9-4182-be5e-aad5ce952f84
author: rothja
ms.author: jroth
ms.openlocfilehash: 6bb1c7932047e72d586275a4b56d1424539477f4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775592"
---
# <a name="cursorlocation-property-ado"></a>CursorLocation 속성(ADO)
커서 서비스의 위치를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 [CursorLocationEnum](./cursorlocationenum.md) 값 중 하나로 설정할 수 있는 **Long** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 이 속성을 사용 하면 공급자가 액세스할 수 있는 다양 한 커서 라이브러리 중에서 선택할 수 있습니다. 일반적으로 클라이언트 쪽 커서 라이브러리를 사용 하거나 서버에 있는 항목을 사용 하도록 선택할 수 있습니다.  
  
 이 속성 설정은 속성이 설정 된 후에만 설정 된 연결에 영향을 줍니다. **CursorLocation** 속성을 변경 해도 기존 연결에는 영향을 주지 않습니다.  
  
 [Execute](./execute-method-ado-connection.md) 메서드에서 반환한 커서는이 설정을 상속 합니다. **레코드 집합** 개체는 연결 된 연결에서이 설정을 자동으로 상속 합니다.  
  
 이 속성은 [연결](./connection-object-ado.md) 또는 닫힌 [레코드 집합](./recordset-object-ado.md)에 대 한 읽기/쓰기 이며 열려 있는 **레코드 집합**에 대 한 읽기 전용입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽 **레코드 집합** 또는 **연결** 개체에서 사용 하는 경우 **CursorLocation** 속성은 **adUseClient**로만 설정할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [연결 개체(ADO)](./connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [부록 A: 공급자](../../guide/appendixes/appendix-a-providers.md)