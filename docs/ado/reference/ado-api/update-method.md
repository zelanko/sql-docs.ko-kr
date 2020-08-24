---
description: Update 메서드
title: Update 메서드 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 819e6ebaa3932f19a693cb3d50651f7c451200e6
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777002"
---
# <a name="update-method"></a>Update 메서드
레코드 [집합](./recordset-object-ado.md) 개체의 현재 행 또는 [Record](./record-object-ado.md) 개체의 [Fields](./fields-collection-ado.md) 컬렉션에 대 한 변경 내용을 저장 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>매개 변수  
 *필드*  
 선택 사항입니다. 수정 하려는 필드 또는 필드의 이름 또는 서 수 **위치를 나타내는 variant 배열 또는** 단일 이름을 나타내는 **variant** 입니다.  
  
 *값*  
 선택 사항입니다. 단일 값 또는 새 레코드의 필드에 대 한 값을 나타내는 **variant** 배열을 나타내는 **variant** 입니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="recordset"></a>레코드 집합  
 [AddNew](./addnew-method-ado.md) 메서드를 호출 하거나 기존 레코드의 필드 값을 변경한 후에는 **Update** 메서드를 사용 하 여 **레코드 집합** 개체의 현재 레코드에 대 한 변경 내용을 저장할 수 있습니다. **레코드 집합** 개체는 업데이트를 지원 해야 합니다.  
  
 필드 값을 설정 하려면 다음 중 하나를 수행 합니다.  
  
-   [필드](./field-object.md) 개체의 [값](./value-property-ado.md) 속성에 값을 할당 하 고 **Update** 메서드를 호출 합니다.  
  
-   **업데이트** 호출을 사용 하 여 필드 이름 및 값을 인수로 전달 합니다.  
  
-   **업데이트** 호출을 사용 하 여 필드 이름 배열과 값 배열을 전달 합니다.  
  
 필드와 값의 배열을 사용 하는 경우 두 배열에 동일한 수의 요소가 있어야 합니다. 또한 필드 이름의 순서는 필드 값의 순서와 일치 해야 합니다. 필드 및 값의 개수와 순서가 일치 하지 않으면 오류가 발생 합니다.  
  
 **레코드 집합** 개체가 일괄 처리 업데이트를 지 원하는 경우 [UpdateBatch](./updatebatch-method.md) 메서드를 호출할 때까지 하나 이상의 레코드에 대 한 여러 변경 내용을 로컬로 캐시할 수 있습니다. 현재 레코드를 편집 하거나 **UpdateBatch** 메서드를 호출할 때 새 레코드를 추가 하는 경우, ADO는 일괄 처리 된 변경 내용을 공급자에 전송 하기 전에 **업데이트** 메서드를 자동으로 호출 하 여 현재 레코드에 대 한 보류 중인 변경 내용을 저장 합니다.  
  
 **Update** 메서드를 호출 하기 전에 추가 하거나 편집 하는 레코드에서 이동 하는 경우 ADO는 자동으로 **업데이트** 를 호출 하 여 변경 내용을 저장 합니다. 현재 레코드에 대 한 변경 내용을 취소 하거나 새로 추가 된 레코드를 삭제 하려는 경우에는 [CancelUpdate](./cancelupdate-method-ado.md) 메서드를 호출 해야 합니다.  
  
 **Update** 메서드를 호출한 후에는 현재 레코드가 최신 상태로 유지 됩니다.  
  
## <a name="record"></a>레코드  
 **Update** 메서드는 **Record** 개체의 [fields](./fields-collection-ado.md) 컬렉션에 있는 필드에 대 한 추가, 삭제 및 업데이트를 종결 합니다.  
  
 예를 들어 **Delete** 메서드를 사용 하 여 삭제 된 필드는 즉시 삭제 되도록 표시 되지만 컬렉션에 남아 있습니다. 공급자의 컬렉션에서 이러한 필드를 실제로 삭제 하려면 **Update** 메서드를 호출 해야 합니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [Fields 컬렉션(ADO)](./fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [Update 및 CancelUpdate 메서드 예제 (VB)](./update-and-cancelupdate-methods-example-vb.md)   
 [Update 및 CancelUpdate 메서드 예제 (VC + +)](./update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 메서드 (ADO)](./addnew-method-ado.md)   
 [CancelUpdate 메서드 (ADO)](./cancelupdate-method-ado.md)   
 [EditMode 속성](./editmode-property.md)   
 [UpdateBatch 메서드](./updatebatch-method.md)