---
description: Clone 메서드(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c91960975b04e5c09cf2745e1bb77e7b343dbd2e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776252"
---
# <a name="clone-method-ado"></a>Clone 메서드(ADO)
기존 **recordset** 개체에서 중복 [레코드 집합](./recordset-object-ado.md) 개체를 만듭니다. 필요에 따라 복제본을 읽기 전용으로 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>Return Value  
 **레코드 집합** 개체 참조를 반환 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *rstDuplicate*  
 만들 중복 **레코드 집합** 개체를 식별 하는 개체 변수입니다.  
  
 *rstOriginal*  
 복제할 **레코드 집합** 개체를 식별 하는 개체 변수입니다.  
  
 *LockType*  
 선택 사항입니다. 원본 **레코드 집합**의 잠금 유형 또는 읽기 전용 **레코드 집합**을 지정 하는 [LockTypeEnum](./locktypeenum.md) 값입니다. 유효한 값은 **Adlockunspecified 되지** 않았거나 **adlockunspecified**입니다.  
  
## <a name="remarks"></a>설명  
 **복제** 메서드를 사용 하 여 여러 중복 **레코드 집합** 개체를 만들 수 있습니다. 특히 지정 된 레코드 집합에서 둘 이상의 현재 레코드를 유지 관리 하려는 경우에 사용 합니다. **Clone** 메서드를 사용 하는 것은 원래와 동일한 정의를 사용 하는 새 **레코드 집합** 개체를 만들고 여는 것 보다 더 효율적입니다.  
  
 원래 **레코드 집합**의 [필터](./filter-property.md) 속성 (있는 경우)은 복제본에 적용 되지 않습니다. 새 **레코드 집합** 의 **필터** 속성을 설정 하 여 결과를 필터링 합니다. 모든 기존 **필터** 값을 복사 하는 가장 간단한 방법은 다음과 같이 직접 할당 하는 것입니다.  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 새로 만든 클론의 현재 레코드는 첫 번째 레코드로 설정 됩니다.  
  
 하나의 **레코드 집합** 개체에 대 한 변경 내용은 커서 유형에 관계 없이 모든 클론에 표시 됩니다. 그러나 원래 **레코드 집합**에서 [Requery](./requery-method.md) 를 실행 한 후에는 복제본이 더 이상 원래와 동기화 되지 않습니다.  
  
 원래 **레코드 집합** 을 닫으면 복사본은 닫히지 않으며 복사본을 닫지 않고 원본 또는 기타 복사본을 닫습니다.  
  
 책갈피를 지 원하는 **레코드 집합** 개체만 복제할 수 있습니다. 책갈피 값은 서로 바꿔 사용할 수 있습니다. 즉, 한 **레코드 집합** 개체의 책갈피 참조는 해당 복제본의 동일한 레코드를 참조 합니다.  
  
 트리거된 일부 **레코드 집합** 이벤트도 모든 **레코드 집합** 복제에서 발생 합니다. 그러나 현재 레코드는 복제 된 **레코드 집합**간에 다를 수 있으므로 해당 이벤트는 복제본에 대해 유효 하지 않을 수 있습니다. 예를 들어 필드의 값을 변경 하면 변경 된 **레코드 집합** 및 모든 복제본에서 [WillChangeField](./willchangefield-and-fieldchangecomplete-events-ado.md) 이벤트가 발생 합니다. 복제 된 **레코드 집합** 에 대 한 **WillChangeField** 이벤트의 *fields* 매개 변수 (변경 되지 않은 경우)는 복제본의 현재 레코드에 대 한 필드를 참조 하며,이는 변경 내용이 발생 한 원래 **레코드 집합** 의 현재 레코드와 다른 레코드가 될 수 있습니다.  
  
 다음 표에서는 모든 **레코드 집합** 이벤트의 전체 목록을 제공 합니다. **Clone** 메서드를 사용 하 여 생성 된 모든 레코드 집합에 대해 유효 하 고 트리거되는 지 여부를 나타냅니다.  
  
|이벤트|복제에서 트리거 되었습니까?|  
|-----------|--------------------------|  
|[EndOfRecordset](./endofrecordset-event-ado.md)|아니요|  
|[FetchComplete](./fetchcomplete-event-ado.md)|아니요|  
|[FetchProgress](./fetchprogress-event-ado.md)|아니요|  
|[FieldChangeComplete](./willchangefield-and-fieldchangecomplete-events-ado.md)|예|  
|[MoveComplete](./willmove-and-movecomplete-events-ado.md)|아니요|  
|[RecordChangeComplete](./willchangerecord-and-recordchangecomplete-events-ado.md)|예|  
|[RecordsetChangeComplete](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|아니요|  
|[WillChangeField](./willchangefield-and-fieldchangecomplete-events-ado.md)|예|  
|[WillChangeRecord](./willchangerecord-and-recordchangecomplete-events-ado.md)|예|  
|[WillChangeRecordset](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|아니요|  
|[WillMove](./willmove-and-movecomplete-events-ado.md)|아니요|  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Clone 메서드 예제 (VB)](./clone-method-example-vb.md)   
 [Clone 메서드 예제 (VBScript)](./clone-method-example-vbscript.md)   
 [Clone 메서드 예제(VC++)](./clone-method-example-vc.md)