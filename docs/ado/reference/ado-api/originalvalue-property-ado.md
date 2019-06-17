---
title: OriginalValue 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::OriginalValue
helpviewer_keywords:
- OriginalValue property [ADO]
ms.assetid: 6e33c6ec-14d9-4b1d-ba9b-cb99862e7bac
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e9a576220d7771ed539765da2947f6a7cc750f64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66706930"
---
# <a name="originalvalue-property-ado"></a>OriginalValue 속성(ADO)
값을 나타내는 [필드](../../../ado/reference/ado-api/field-object.md) 는 이전부터 있던 레코드에서 변경 작업을 수행 합니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **Variant** 변경 하기 전에 필드의 값을 나타내는 값입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **OriginalValue** 현재 레코드에서 필드의 원래 필드 값을 반환 하는 속성입니다.  
  
 *즉시 업데이트 모드* (있는 공급자 변경 기록의 데이터 원본에 호출한 후 합니다 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드), **OriginalValue** 속성 반환 변경 전에 존재 했던 필드 값 (즉, 마지막 **업데이트** 메서드 호출). 동일 하는 값을 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 메서드 사용 하 여 합니다 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성.  
  
 *일괄 처리 업데이트 모드* (공급자는 여러 변경 내용을 캐시 및 호출 된 경우에 기본 데이터 원본에 기록 합니다 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드), **OriginalValue** 속성에는 변경 전에 존재 했던 필드 값을 반환 합니다 (즉, 마지막 **UpdateBatch** 메서드 호출). 동일 하는 값을 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드 사용 하 여 합니다 **값** 속성. 이 속성을 사용 하는 경우는 [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) 속성인 일괄 업데이트에서 발생 하는 충돌을 해결할 수 있습니다.  
  
## <a name="record"></a>레코드  
 에 대 한 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체를 **OriginalValue** 속성 앞에 추가 하는 필드에 대 한 빈 됩니다 [업데이트](../../../ado/reference/ado-api/update-method.md) 라고 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [OriginalValue 및 UnderlyingValue 속성 예제 (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 및 UnderlyingValue 속성 예제 (VC + +)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [UnderlyingValue 속성](../../../ado/reference/ado-api/underlyingvalue-property.md)
