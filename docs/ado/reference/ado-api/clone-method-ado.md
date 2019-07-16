---
title: Clone 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Clone
- Recordset20::raw_Clone
helpviewer_keywords:
- Clone method [ADO]
ms.assetid: ad49265f-1c05-4271-9bbf-7c00010ac18c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7439f9a4a04582f4cf4c4878892ed0f4f33e228c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920012"
---
# <a name="clone-method-ado"></a>Clone 메서드(ADO)
복제본을 만듭니다 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) 기존 개체 **Recordset** 개체입니다. 필요에 따라 읽기 전용 복제본 수를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 **레코드 집합** 개체 참조입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *rstDuplicate*  
 중복을 식별 하는 개체 변수에 **레코드 집합** 개체를 만들 수 있습니다.  
  
 *rstOriginal*  
 식별 하는 개체 변수를 **레코드 집합** 중복 되는 개체입니다.  
  
 *LockType*  
 (선택 사항) A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) 원래 잠금 형식을 지정 하는 값 **레코드 집합**, 또는 읽기 전용 **레코드 집합**합니다. 유효한 값은 **adLockUnspecified** 하거나 **adLockReadOnly**합니다.  
  
## <a name="remarks"></a>설명  
 사용 합니다 **복제** 메서드를 여러 중복 **레코드 집합** 개체에 지정된 된 레코드 집합에서 현재 둘 이상의 레코드를 유지 하려는 경우에 특히 합니다. 사용 하는 **복제** 메서드를 만들고 새 열 보다 더 효율적입니다 **레코드 집합** 원본과 동일한 정의 사용 하는 개체입니다.  
  
 합니다 [필터](../../../ado/reference/ado-api/filter-property.md) 속성의 원래 **레코드 집합**복제본에 적용 되지 것입니다 있는 경우. 설정 된 **필터** 새 속성 **레코드 집합** 결과를 필터링 합니다. 기존 복사 하는 가장 간단한 방법은 **필터** 값을 다음과 같이 직접 할당 하는 것입니다.  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 새로 만든된 복제본의 현재 레코드는 첫 번째 레코드에 설정 됩니다.  
  
 하나를 변경한 **레코드 집합** 개체 모든 커서 유형에 관계 없이 해당 복제 중에 표시 됩니다. 그러나 실행 후 [Requery](../../../ado/reference/ado-api/requery-method.md) 원본에서 **레코드 집합**, 복제본 원래 더 이상 동기화 되지 것입니다.  
  
 원래 닫는 **레코드 집합** 해당 복사본을 닫히지 않으며 원본 또는 다른 복사본은 닫기 복사본을 닫지 않습니다.  
  
 복제할 수 있습니다는 **레코드 집합** 책갈피를 지 원하는 개체입니다. 책갈피 값은 교환할 수 있습니다. 즉, 책갈피에서 참조를 하나 **레코드 집합** 개체의 모든 해당 복제본에 동일한 레코드를 가리킵니다.  
  
 일부 **Recordset** 트리거되는 이벤트에도 모든 발생 **Recordset** 복제 합니다. 현재 레코드 간에 다를 수 있으므로 복제 하는 반면 **레코드 집합**, 이벤트를 복제에 대 한 잘못 되었을 수 있습니다. 예를 들어, 필드의 값을 변경 하는 경우는 [WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md) 변경에서 이벤트가 발생 하는 **레코드 집합** 및 모든 복제본입니다. 합니다 *필드* 의 매개 변수를 **WillChangeField** 복제 된 이벤트 **레코드 집합** 복제의 현재 레코드의 필드를 참조 합니다 (여기서 없습니다 변경 된) 원래의 현재 레코드 보다 다른 레코드를 사용할 수 있습니다 **레코드 집합** 변경 발생 합니다.  
  
 다음 표에서 모든 전체 목록이 **레코드 집합** 이벤트입니다. 유효 하 고 사용 하 여 생성 된 모든 레코드 집합 복제본에 대 한 트리거된 지 여부를 나타냅니다. 합니다 **복제** 메서드.  
  
|이벤트|복제본에서 트리거 되나요?|  
|-----------|--------------------------|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|아니요|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|아니요|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|아니요|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|예|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|아니요|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|예|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|아니요|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|예|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|예|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|아니요|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|아니요|  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Clone 메서드 예제 (VB)](../../../ado/reference/ado-api/clone-method-example-vb.md)   
 [Clone 메서드 예제 (VBScript)](../../../ado/reference/ado-api/clone-method-example-vbscript.md)   
 [Clone 메서드 예제(VC++)](../../../ado/reference/ado-api/clone-method-example-vc.md)   
