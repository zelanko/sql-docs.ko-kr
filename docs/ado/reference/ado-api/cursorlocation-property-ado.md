---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 344956b349e51a448a768988ff5062bfbc532562
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698430"
---
# <a name="cursorlocation-property-ado"></a>CursorLocation 속성(ADO)
커서 서비스의 위치를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환을 **긴** 중 하나로 설정할 수 있는 값을 [CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md) 값.  
  
## <a name="remarks"></a>Remarks  
 이 속성을 사용 하면 공급자에 액세스할 수 있는 다양 한 커서 라이브러리를 선택할 수 있습니다. 일반적으로 클라이언트 쪽 커서 라이브러리 또는 있는 하나를 사용 하 여 서버에서 선택할 수 있습니다.  
  
 이 속성 설정 속성을 설정한 후에 설정 하는 연결을 영향을 줍니다. 변경 된 **CursorLocation** 속성이 기존 연결에 영향을 주지 않습니다.  
  
 반환 된 커서를 [Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md) 메서드는이 설정을 상속 합니다. **레코드 집합** 개체 관련된 연결에서이 설정을 자동으로 상속 됩니다.  
  
 이 속성은 읽기/쓰기를 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 또는 닫힌 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 및를 열 때 읽기 전용 **레코드 집합**합니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용할 때 **레코드 집합** 하거나 **연결** 개체를 **CursorLocation** 속성 만설정할수있습니다**adUseClient**합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목  
 [부록 A: 공급자](../../../ado/guide/appendixes/appendix-a-providers.md)
