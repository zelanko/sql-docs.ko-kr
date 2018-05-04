---
title: 앞 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::CursorLocation
- Recordset15::CursorLocation
helpviewer_keywords:
- CursorLocation property [ADO]
ms.assetid: 39c8d86e-7ee9-4182-be5e-aad5ce952f84
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c169441ffc1cc455e0474f54fe923c3e4cd0f4d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="cursorlocation-property-ado"></a>앞 속성 (ADO)
커서 서비스의 위치를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **긴** 중 하나로 설정할 수 있는 값은 [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) 값입니다.  
  
## <a name="remarks"></a>주의  
 이 속성을 사용 하면 공급자에 액세스할 수 있는 다양 한 커서 라이브러리 중에서 선택할 수 있습니다. 일반적으로 서버에 클라이언트 쪽 커서 라이브러리 또는 있는 하나를 사용 하 여 선택할 수 있습니다.  
  
 이 속성 설정 속성이 설정 된 후에 설정 하는 연결을 영향을 줍니다. 변경 된 **앞** 속성이 기존 연결에 적용 되지 않습니다.  
  
 반환 된 커서는 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 메서드는이 설정을 상속 합니다. **레코드 집합** 개체에 자동으로 관련된 연결에서이 설정을 상속 합니다.  
  
 이 속성은 읽기/쓰기는 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 닫힌 또는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 열린에서 읽기 전용 및 **레코드 집합**합니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용할 때 **레코드 집합** 또는 **연결** 개체는 **앞** 시키면 속성**adUseClient**합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
