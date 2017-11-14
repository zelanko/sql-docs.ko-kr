---
title: "Clone 메서드 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset20::Clone
- Recordset20::raw_Clone
helpviewer_keywords:
- Clone method [ADO]
ms.assetid: ad49265f-1c05-4271-9bbf-7c00010ac18c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9b7586bef017cd4e5f3a89586b8600abfd183f5a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="clone-method-ado"></a>Clone 메서드 (ADO)
복제를 만들어 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 기존 개체 **레코드 집합** 개체입니다. 필요에 따라 읽기 전용 복제 되도록 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 **레코드 집합** 개체 참조입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *rstDuplicate*  
 중복을 식별 하는 개체 변수 **레코드 집합** 만들 개체입니다.  
  
 *rstOriginal*  
 개체 변수를 식별 하는 **레코드 집합** 를 중복 하는 개체입니다.  
  
 *LockType*  
 (선택 사항) A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) 원래 잠금 유형을 지정 하는 값 **레코드 집합**, 읽기 전용 또는 **레코드 집합**합니다. 유효한 값은 **adLockUnspecified** 또는 **adLockReadOnly**합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **복제** 메서드를 여러 개 만듭니다 중복 **레코드 집합** 개체, 특히 여러 레코드의 지정한 집합의 현재 레코드를 유지 관리 하려는 경우. 사용 하 여는 **복제** 메서드 만들고 새 열 보다 더 효율적입니다. **레코드 집합** 원본과 동일한 정의 사용 하는 개체입니다.  
  
 [필터](../../../ado/reference/ado-api/filter-property.md) 원래 속성 **레코드 집합**를 복제본에 적용 되지 것입니다 있는 경우. 설정의 **필터** 새 속성 **레코드 집합** 결과를 필터링 합니다. 모든 기존 복사 하는 가장 간단한 방법은 **필터** 값은 다음과 같이, 직접 할당할 수 있습니다.  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 새로 만든된 복제본의 현재 레코드 첫 번째 레코드로 설정 됩니다.  
  
 하나를 적용 한 변경 내용 **레코드 집합** 개체 모든 커서 유형에 관계 없이 해당 복제 중에 표시 됩니다. 그러나 실행 후 [Requery](../../../ado/reference/ado-api/requery-method.md) 원래에 **레코드 집합**, 클론 원본에 더 이상 동기화 되지 것입니다.  
  
 원래 닫는 **레코드 집합** 복사본 닫히지 않으며 원본이 나 다른 복사본은 닫기 복사본을 닫으면지 않습니다.  
  
 복제할 수 있습니다는 **레코드 집합** 책갈피를 지 원하는 개체입니다. 책갈피 값은 교환할 수 있습니다. 즉, 하나에서 책갈피 참조 **레코드 집합** 개체 모든 복제본에서 동일한 레코드를 참조 합니다.  
  
 일부 **레코드 집합** 트리거되는 이벤트를 모든 페이지에서 발생 합니다 **레코드 집합** 를 복제 합니다. 그러나 현재 레코드 간에 다를 수 있으므로 복제 **레코드 집합**, 이벤트를 복제에 유효할 수 있습니다. 예를 들어, 필드의 값을 변경 하면는 [WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md) 에서 변경 된 이벤트는 발생 **레코드 집합** 및 모든 복제본에서 합니다. *필드* 의 매개 변수는 **WillChangeField** 이벤트의 복제 된 **레코드 집합** 는 복제본의 현재 레코드의 필드를 참조 합니다 (여기서 되지 변경) 원래의 현재 레코드 보다 다른 레코드로 발생할 수 있는 **레코드 집합** 변경이 발생 한 합니다.  
  
 다음 표에서 모든 전체 목록이 **레코드 집합** 이벤트입니다. 유효 하 고 사용 하 여 생성 된 모든 레코드 집합 복제본에 대 한 트리거된 지 여부를 나타냅니다는 **복제** 메서드.  
  
|이벤트|복제본에서 트리거되며?|  
|-----------|--------------------------|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|아니요|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|아니요|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|아니요|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|예|  
|[두](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|아니요|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|예|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|아니요|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|예|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|예|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|아니요|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|아니요|  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Clone 메서드 예제 (VB)](../../../ado/reference/ado-api/clone-method-example-vb.md)   
 [Clone 메서드 예제 (VBScript)](../../../ado/reference/ado-api/clone-method-example-vbscript.md)   
 [Clone 메서드 예제(VC++)](../../../ado/reference/ado-api/clone-method-example-vc.md)   

