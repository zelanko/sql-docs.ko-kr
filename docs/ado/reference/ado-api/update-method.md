---
title: 메서드를 업데이트 합니다. | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Update
helpviewer_keywords:
- Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ce247905afd6ed34366424f5f905d57b42d988f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938847"
---
# <a name="update-method"></a>Update 메서드
현재 행에 수행한 변경 내용 저장을 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 또는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Fields*  
 (선택 사항) A **Variant** 나타내는 단일 이름, 또는 **Variant** 이름 또는 하나 이상의 수정 하려는 필드의 서 수 위치를 나타내는 배열입니다.  
  
 *값*  
 (선택 사항) A **Variant** 단일 값을 나타내는 또는 **Variant** 새 레코드의 필드에 대 한 값을 나타내는 배열입니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="recordset"></a>레코드 집합  
 사용 하 여는 **업데이트** 의 현재 레코드에 변경 내용을 저장 하는 방법을 **레코드 집합** 호출한 후 개체를 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 메서드에서 모든 필드 값을 변경 이후 또는 기존 레코드입니다. 합니다 **레코드 집합** 개체 업데이트를 지원 해야 합니다.  
  
 필드 값을 설정 하려면 다음 중 하나를 수행 합니다.  
  
-   값을 할당 한 [필드](../../../ado/reference/ado-api/field-object.md) 개체의 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성과 호출 합니다 **업데이트** 메서드.  
  
-   필드 이름 및 값을 인수로 전달 된 **업데이트** 호출 합니다.  
  
-   필드 이름 및 값의 배열을 전달 합니다 **업데이트** 호출 합니다.  
  
 필드 및 값의 배열을 사용할 때 두 배열에서 요소는 같은 숫자 여야 합니다. 또한 필드 이름의 순서 필드 값의 순서가 일치 해야 합니다. 개수 및 필드와 값의 순서가 일치 하지 않는 경우 오류가 발생 했습니다.  
  
 경우는 **레코드 집합** 개체가 일괄 처리 업데이트를 지원, 호출할 때까지 로컬로 여러 변경 내용을 하나 이상의 레코드를 캐시할 수 있습니다 합니다 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드. 현재 레코드를 편집 하거나 호출 하는 경우 새 레코드를 추가 하는 경우는 **UpdateBatch** 메서드를 ADO를 자동으로 호출 합니다 **업데이트** 하기 전에 현재 레코드에 보류 중인 변경 내용을 저장 하는 방법 공급자에 게 일괄 처리 된 변경 내용을 전송 합니다.  
  
 레코드에서 이동 하는 경우 추가 또는 편집 하는 호출 하기 전에 합니다 **업데이트** 메서드를 ADO를 자동으로 호출 **업데이트** 변경 내용을 저장 합니다. 호출 해야 합니다 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 메서드 현재 레코드에 변경한 내용을 취소 하거나 새로 추가 된 레코드를 삭제 하려는 경우.  
  
 현재 레코드를 호출한 후 계속 합니다 **업데이트** 메서드.  
  
## <a name="record"></a>녹음  
 **업데이트** 메서드를 추가, 삭제 및 업데이트의 필드를 종료 합니다 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 **레코드** 개체입니다.  
  
 예를 들어, 필드를 사용 하 여 삭제 합니다 **삭제** 메서드는 즉시 삭제로 표시 하지만 컬렉션에 유지 됩니다. 합니다 **업데이트** 실제로 공급자의 컬렉션에서 이러한 필드를 삭제 하려면 메서드를 호출 해야 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Fields 컬렉션(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목  
 [Update 및 CancelUpdate 메서드 예제 (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Update 및 CancelUpdate 메서드 예제 (VC + +)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 메서드 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [CancelUpdate 메서드 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode 속성](../../../ado/reference/ado-api/editmode-property.md)   
 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md)
