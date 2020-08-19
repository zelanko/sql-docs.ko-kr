---
description: CursorType 속성(ADO)
title: CursorType 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CursorType
helpviewer_keywords:
- CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
author: rothja
ms.author: jroth
ms.openlocfilehash: 7eae60dc133734edb666737356a214af5bd9ea8c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444255"
---
# <a name="cursortype-property-ado"></a>CursorType 속성(ADO)
[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체에 사용 되는 커서 유형을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) 값을 설정 하거나 반환 합니다. 기본값은 **Adopenforwardonly**입니다.  
  
## <a name="remarks"></a>설명  
 **CursorType** 속성을 사용 하 여 **레코드 집합** 개체를 열 때 사용 해야 하는 커서 유형을 지정할 수 있습니다.  
  
 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 속성이 **adUseClient**로 설정 된 경우 **adopenstatic** 의 설정만 지원 됩니다. 지원 되지 않는 값이 설정 되 면 오류가 발생 하지 않습니다. 가장 가까운 지원 **CursorType** 대신 사용 됩니다.  
  
 요청 된 커서 유형을 지원 하지 않는 공급자는 다른 커서 유형을 반환할 수 있습니다. **CursorType** 속성은 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체가 열려 있을 때 사용 중인 실제 커서 유형과 일치 하도록 변경 됩니다. 반환 된 커서의 특정 기능을 확인 하려면 [지원](../../../ado/reference/ado-api/supports-method.md) 메서드를 사용 합니다. **레코드 집합**을 닫은 후 **CursorType** 속성은 원래 설정으로 되돌아갑니다.  
  
 다음 차트에서는 각 커서 유형에 필요한 공급자 기능 ( **메서드 상수로** 식별)을 보여 줍니다.  
  
|이 CursorType 레코드 집합의 경우|Supports 메서드는 이러한 모든 상수에 대해 True를 반환 해야 합니다.|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|없음|  
|**adOpenKeyset**|**Adbookmark**, **adHoldRecords**, **adMovePrevious**, **adbookmark**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**Adbookmark**, **adHoldRecords**, **adMovePrevious**, **adbookmark**|  
  
> [!NOTE]
>  는 동적 및 전진 전용 커서에 **대해 (****adupdatebatch**)가 true 일 수 있지만 일괄 처리 업데이트의 경우 키 집합 또는 정적 커서를 사용 해야 합니다. [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) 속성을 **Adlockbatchoptimistic** 으로 설정 하 고 **CursorLocation** 속성을 **adUseClient** 로 설정 하 여 batch 업데이트에 필요한 OLE DB에 커서 서비스를 사용 하도록 설정 합니다.  
  
 **CursorType** 속성은 **레코드 집합이** 닫혀 있을 때 읽기/쓰기이 고, 열려 있으면 읽기 전용입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽 **레코드 집합** 개체에서 사용 하는 경우 **CursorType** 속성은 **adopenstatic**으로만 설정할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [CursorType, LockType 및 EditMode 속성 예제 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType 및 EditMode 속성 예제 (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Supports 메서드](../../../ado/reference/ado-api/supports-method.md)
