---
description: UnderlyingValue 속성
title: UnderlyingValue 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::GetUnderlyingValue
- Field20::get_UnderlyingValue
- Field20::UnderlyingValue
helpviewer_keywords:
- UnderlyingValue property
ms.assetid: 00a0c8b8-8b63-433f-95b8-020ab05874a0
author: rothja
ms.author: jroth
ms.openlocfilehash: a96924a682a0c916da8c6834ea7b290b88b6f690
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988174"
---
# <a name="underlyingvalue-property"></a>UnderlyingValue 속성
데이터베이스에 있는 [Field](./field-object.md) 개체의 현재 값을 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 **필드**의 값을 나타내는 **Variant** 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **UnderlyingValue** 속성을 사용 하 여 데이터베이스에서 현재 필드 값을 반환 합니다. **UnderlyingValue** 속성의 필드 값은 트랜잭션에 표시 되는 값 이며 다른 트랜잭션에의 한 최근 업데이트의 결과일 수 있습니다. 원래 [레코드 집합](./recordset-object-ado.md)에 반환 된 값을 반영 하는 [originalvalue](./originalvalue-property-ado.md) 속성과 다를 수 있습니다.  
  
 이는 [Resync](./resync-method.md) 메서드를 사용 하는 것과 비슷하지만 **UnderlyingValue** 속성은 현재 레코드의 특정 필드에 대 한 값만 반환 합니다. 이 값은 [Resync](./resync-method.md) 메서드에서 [value](./value-property-ado.md) 속성을 대체 하는 데 사용 하는 것과 동일한 값입니다.  
  
 **Originalvalue** 속성을 사용 하 여이 속성을 사용 하는 경우 일괄 업데이트에서 발생 하는 충돌을 해결할 수 있습니다.  
  
## <a name="record"></a>레코드  
 [Record](./record-object-ado.md) 개체의 경우이 속성은 [Update](./update-method.md) 를 호출 하기 전에 추가 된 필드에 대해 비어 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](./field-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [OriginalValue 및 UnderlyingValue 속성 예제 (VB)](./originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue 및 UnderlyingValue 속성 예제 (VC + +)](./originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [OriginalValue 속성 (ADO)](./originalvalue-property-ado.md)   
 [Resync 메서드](./resync-method.md)