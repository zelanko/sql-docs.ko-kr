---
title: "Update 메서드 | Microsoft Docs"
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
f1_keywords: Recordset15::Update
helpviewer_keywords: Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b8d9acf6072961b1d63a691033d4c2ecd578cb4b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="update-method"></a>Update 메서드
현재 행에 수행한 변경 내용을 저장 하는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 또는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션은 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>매개 변수  
 *필드*  
 (선택 사항) A **Variant** 단일 이름을 나타내는 또는 **Variant** 이름 또는 하나 이상의 수정할 필드의 서 수 위치를 나타내는 배열입니다.  
  
 *값*  
 (선택 사항) A **Variant** 단일 값을 나타내는 또는 **Variant** 하나 이상의 새 레코드의 필드에 대 한 값을 나타내는 배열입니다.  
  
## <a name="remarks"></a>주의  
  
## <a name="recordset"></a>레코드 집합  
 사용 하 여는 **업데이트** 의 현재 레코드에 변경 내용을 저장 하는 메서드는 **레코드 집합** 호출 이후 개체는 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 메서드의 모든 필드 값을 변경 이후 또는 기존 레코드입니다. **레코드 집합** 개체 업데이트를 지원 해야 합니다.  
  
 필드 값을 설정 하려면 다음 중 하나를 수행 합니다.  
  
-   값을 할당 한 [필드](../../../ado/reference/ado-api/field-object.md) 개체의 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성과 호출은 **업데이트** 메서드.  
  
-   필드 이름 및 값을 인수로 전달 된 **업데이트** 호출 합니다.  
  
-   필드 이름 및 값의 배열을 전달는 **업데이트** 호출 합니다.  
  
 필드와 값의 배열을 사용할 때 동일한 두 배열에 있는 요소의 수 있어야 합니다. 또한 필드 이름은 순서에는 필드 값의 순서와 일치 해야 합니다. 개수 및 필드와 값의 순서가 일치 하지 않으면 오류가 발생 합니다.  
  
 경우는 **레코드 집합** 를 호출 하기 전에 로컬로 하나 이상의 레코드의 여러 변경 내용을 캐시할 수 있습니다, 개체 지원 일괄 처리 업데이트는 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드. 현재 레코드를 편집 하거나 호출 하는 경우 새 레코드를 추가 하는 경우는 **UpdateBatch** 메서드, ADO를 자동으로 호출 된 **업데이트** 하기 전에 현재 레코드에 보류 중인 변경 내용을 저장 하는 메서드 공급자에 게 일괄 처리 된 변경 내용을 전송 합니다.  
  
 레코드에서 이동 하는 경우 추가 하거나 편집 하는 호출 하기 전에 **업데이트** 메서드, ADO를 자동으로 호출 **업데이트** 여 변경 내용을 저장 합니다. 호출 해야 합니다는 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 메서드 현재 레코드에 변경한 내용을 취소 하거나 새로 추가 된 레코드를 삭제 하려는 경우.  
  
 호출한 후에 현재 레코드가 남아는 **업데이트** 메서드.  
  
## <a name="record"></a>레코드  
 **업데이트** 메서드 추가, 삭제 및의 필드에 대 한 업데이트 작업을 마무리는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 **레코드** 개체입니다.  
  
 예, 필드와 함께 삭제는 **삭제** 메서드는 즉시 삭제로 표시 되지만 컬렉션에 그대로 남아 있습니다. **업데이트** 실제로 공급자의 컬렉션에서 이러한 필드를 삭제 하려면 메서드를 호출 해야 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Fields 컬렉션(ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [업데이트 및 CancelUpdate 메서드 예제 (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [업데이트 및 CancelUpdate 메서드 예제 (VC + +)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 메서드 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [CancelUpdate 메서드 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode 속성](../../../ado/reference/ado-api/editmode-property.md)   
 [UpdateBatch 메서드](../../../ado/reference/ado-api/updatebatch-method.md)
