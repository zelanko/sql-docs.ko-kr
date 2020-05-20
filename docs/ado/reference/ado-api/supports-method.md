---
title: 지원 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Supports
- Recordset15::Supports
helpviewer_keywords:
- Supports method [ADO]
ms.assetid: 298fc41c-0b55-42fc-b373-c5133b4da6a5
author: rothja
ms.author: jroth
ms.openlocfilehash: 3fbfbf28c430fb698f5e024fe3359027c84512c0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765364"
---
# <a name="supports-method"></a>Supports 메서드
지정 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체가 특정 유형의 기능을 지원 하는지 여부를 확인 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>Return Value  
 *CursorOptions* 인수로 식별 되는 모든 기능이 공급자에 의해 지원 되는지 여부를 나타내는 **부울** 값을 반환 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *CursorOptions*  
 하나 이상의 [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) 값으로 구성 된 **Long** 식입니다.  
  
## <a name="remarks"></a>설명  
 **Supports** 메서드를 사용 하 여 **레코드 집합** 개체가 지 원하는 기능 유형을 확인할 수 있습니다. **Recordset** 개체가 *CursorOptions*에 있는 해당 상수를 포함 하는 기능을 지 원하는 경우 **지원** 메서드는 **True**를 반환 합니다. 그렇지 않으면 **False**를 반환 합니다.  
  
> [!NOTE]
>  **지원** 메서드는 지정 된 기능에 대해 **True** 를 반환할 수 있지만, 공급자가 모든 상황에서 기능을 사용할 수 있도록 보장 하지는 않습니다. **Supports** 메서드는 특정 조건이 충족 될 경우 공급자가 지정 된 기능을 지원할 수 있는지 여부를 반환 합니다. 예를 들어 **지원** 메서드는 커서가 여러 테이블 조인을 기반으로 하 고, 일부 열이 업데이트 되지 않는 경우에도 **레코드 집합** 개체가 업데이트를 지원함을 나타낼 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Supports 메서드 예제 (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [지원 메서드 예제 (VC + +)](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [CursorType 속성(ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
