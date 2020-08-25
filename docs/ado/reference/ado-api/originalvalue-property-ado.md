---
description: OriginalValue 속성(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5aedfa688b2d29a80eb0bc2e06d113e908e122c2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773572"
---
# <a name="originalvalue-property-ado"></a>OriginalValue 속성(ADO)
변경을 수행 하기 전에 레코드에 있던 [필드](./field-object.md) 의 값을 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 변경 전 필드의 값을 나타내는 **Variant** 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **Originalvalue** 속성을 사용 하 여 현재 레코드의 필드에 대 한 원래 필드 값을 반환 합니다.  
  
 [업데이트](./update-method.md) 메서드를 호출한 후 공급자가 기본 데이터 원본에 변경 내용을 쓰는 *즉시 업데이트 모드* 에서 **originalvalue** 속성은 마지막 **업데이트** 메서드 호출 이후 존재 했던 필드 값을 반환 합니다. 이 값은 [CancelUpdate](./cancelupdate-method-ado.md) 메서드에서 [value](./value-property-ado.md) 속성을 바꾸는 데 사용 하는 것과 동일한 값입니다.  
  
 *일괄 업데이트 모드* 에서 ( [updatebatch](./updatebatch-method.md) 메서드를 호출 하는 경우에만 공급자가 여러 변경 내용을 캐시 하 고 기본 데이터 소스에이를 기록) **Originalvalue** 속성은 마지막 **UpdateBatch** 메서드 호출 이후 변경 된 이전에 있던 필드 값을 반환 합니다. [CancelBatch](./cancelbatch-method-ado.md) 메서드가 **value** 속성을 대체 하는 데 사용 하는 것과 동일한 값입니다. [UnderlyingValue](./underlyingvalue-property.md) 속성을 사용 하 여이 속성을 사용 하는 경우 일괄 업데이트에서 발생 하는 충돌을 해결할 수 있습니다.  
  
## <a name="record"></a>레코드  
 [Record](./record-object-ado.md) 개체의 경우 [Update](./update-method.md) 를 호출 하기 전에 추가 된 필드에 대해 **originalvalue** 속성이 비어 있게 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](./field-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [OriginalValue 및 UnderlyingValue 속성 예제 (VB)](./originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 및 UnderlyingValue 속성 예제 (VC + +)](./originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [UnderlyingValue 속성](./underlyingvalue-property.md)