---
title: "메서드를 지원 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::raw_Supports
- Recordset15::Supports
helpviewer_keywords: Supports method [ADO]
ms.assetid: 298fc41c-0b55-42fc-b373-c5133b4da6a5
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 13186c130b85de50bc6cff9487d8fec11359d008
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="supports-method"></a>메서드를 지원
지정 된 있는지 여부를 결정 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체는 특정 종류의 기능을 지원 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>반환 값  
 반환은 **부울** 의 모든 기능으로 식별 하는지 여부를 나타내는 값의 *CursorOptions* 인수 공급자가 지원 됩니다.  
  
#### <a name="parameters"></a>매개 변수  
 *CursorOptions*  
 A **긴** 하나 이상의 구성 된 식 [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **지원** 어떤 유형의 기능을 확인 하는 **레코드 집합** 개체를 지원 합니다. 경우는 **레코드 집합** 개체에 있는 해당 상수는 기능을 지원 *CursorOptions*, **지원** 메서드 반환 **True**. 그렇지 않으면 반환 **False**합니다.  
  
> [!NOTE]
>  하지만 **지원** 반환 될 수 있으며 **True** 지정된 된 기능에 대 한 보장 하지는 않습니다 공급자 사용할 수 있는 기능 모든 상황에서. **지원** 메서드는 특정 조건이 충족 된다는 가정 하는 공급자 지정 된 기능을 지원할 수 있는지 여부를 반환 합니다. 예를 들어는 **지원** 메서드를 나타낼 수 있습니다는 **레코드 집합** 커서의 일부 열을 업데이트할 수 없는 여러 테이블 조인에 기반 하는 경우에 개체 업데이트를 지원 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [메서드 예제 (VB)를 지원합니다.](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [지원 메서드 예제 (VC + +)](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [CursorType 속성(ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
