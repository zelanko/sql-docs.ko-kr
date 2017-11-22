---
title: "OriginalValue 속성 (ADO) | Microsoft Docs"
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
f1_keywords: Field20::OriginalValue
helpviewer_keywords: OriginalValue property [ADO]
ms.assetid: 6e33c6ec-14d9-4b1d-ba9b-cb99862e7bac
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: baa1b522660f2ed7d521a55ad995ed8347c0a2fb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="originalvalue-property-ado"></a>OriginalValue 속성 (ADO)
값을 나타냅니다는 [필드](../../../ado/reference/ado-api/field-object.md) 는 전의 레코드에서 변경 작업을 수행 합니다.  
  
## <a name="return-value"></a>반환 값  
 반환 된 **Variant** 변경 작업 이전의 필드의 값을 나타내는 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **OriginalValue** 속성을 현재 레코드에서 필드에 대 한 원래 필드 값을 반환 합니다.  
  
 *즉시 업데이트 모드* (있는 공급자 변경 기록의 데이터 원본에 호출한 후의 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드), **OriginalValue** 속성 반환 변경 전에 존재 하는 필드 값 (즉, 마지막 이후 **업데이트** 메서드 호출). 이 동일 값는 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 메서드 사용 하 여 대체는 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성입니다.  
  
 *일괄 업데이트 모드* (공급자는 여러 변경 내용을 캐시와 호출 된 경우에 기본 데이터 원본에 기록 된 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 메서드), **OriginalValue** 속성 변경 전에 존재 하는 필드 값을 반환 (즉, 마지막 이후 **UpdateBatch** 메서드 호출). 이 동일 값는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드 사용 하 여 대체는 **값** 속성입니다. 이 속성을 사용 하는 경우는 [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) 속성을 일괄 처리 업데이트에서 발생 하는 충돌을 해결할 수 있습니다.  
  
## <a name="record"></a>레코드  
 에 대 한 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체는 **OriginalValue** 속성 앞에 추가 하는 필드에 대 한 빈 됩니다 [업데이트](../../../ado/reference/ado-api/update-method.md) 호출 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [OriginalValue 및 UnderlyingValue 속성 예제 (VB)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 및 UnderlyingValue 속성 예제 (VC + +)](../../../ado/reference/ado-api/originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [UnderlyingValue 속성](../../../ado/reference/ado-api/underlyingvalue-property.md)
