---
title: 메서드를 지 원하는 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 97c0e4660c14845ddfb59ce4f5f509a0954d98f0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47616981"
---
# <a name="supports-method"></a>Supports 메서드
지정 된 결정 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체는 특정 종류의 기능을 지원 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>반환 값  
 반환을 **부울** 의 모든 기능으로 식별 하는지 여부를 나타내는 값을 *CursorOptions* 인수 공급자가 지원 됩니다.  
  
#### <a name="parameters"></a>매개 변수  
 *CursorOptions*  
 A **긴** 하나 이상의 구성 된 식 [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) 값입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여는 **지원** 기능의 유형을 확인 하는 방법을 **레코드 집합** 지원 개체입니다. 경우는 **레코드 집합** 개체에 있는 해당 상수는 기능을 지원 합니다 *CursorOptions*의 **지 원하는** 메서드가 반환 되는 **True**. 그렇지 **False**합니다.  
  
> [!NOTE]
>  하지만 합니다 **지원** 메서드를 반환할 수 있습니다 **True** 지정된 된 기능에 대 한 보장 하지는 않습니다 공급자를 사용할 수 있는 기능을 모든 상황입니다. 합니다 **지원** 메서드는 단순히 특정 조건이 충족 될 된다는 가정 하는 공급자 지정 된 기능을 지원할 수 있는지 여부를 반환 합니다. 예를 들어 합니다 **지원** 메서드 되었음을 나타낼 수는 **레코드 집합** 커서의 일부 열을 업데이트할 수 없는 여러 개의 테이블 조인을 기반으로 하는 경우에 개체 업데이트를 지원 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Supports 메서드 예제 (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [Supports 메서드 예제 (VC + +)](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [CursorType 속성(ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
