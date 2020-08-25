---
description: GetChunk 메서드(ADO)
title: GetChunk 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::raw_GetChunk
- Field20::GetChunk
helpviewer_keywords:
- GetChunk method [ADO]
ms.assetid: fc268e22-205b-44a3-9038-ffed51e23e10
author: rothja
ms.author: jroth
ms.openlocfilehash: dcf021282d4fce049cd89a154c2d00186b3cbee1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775082"
---
# <a name="getchunk-method-ado"></a>GetChunk 메서드(ADO)
크게 텍스트 또는 이진 데이터 [필드](./field-object.md) 개체의 내용 전체 또는 일부를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>Return Value  
 **Variant**를 반환 합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *크기*  
 검색 하려는 바이트 또는 문자 수와 동일한 **Long** 식입니다.  
  
## <a name="remarks"></a>설명  
 **Field** 개체에 대해 **GetChunk** 메서드를 사용 하 여 긴 이진 또는 문자 데이터의 일부 또는 전체를 검색 합니다. 시스템 메모리가 제한 된 경우에는 **GetChunk** 메서드를 사용 하 여 전체 값이 아닌 부분에서 긴 값을 조작할 수 있습니다.  
  
 **GetChunk** 호출에서 반환 하는 데이터는 *변수에*할당 됩니다. *Size* 가 나머지 데이터 보다 큰 경우 **GetChunk** 메서드는 공백이 있는 *변수* 를 사용 하지 않고 나머지 데이터만 반환 합니다. 필드가 비어 있으면 **GetChunk** 메서드는 null 값을 반환 합니다.  
  
 각 후속 **GetChunk** 호출은 이전 **GetChunk** 호출이 중단 된 위치부터 데이터를 검색 합니다. 그러나 한 필드에서 데이터를 검색 한 다음 현재 레코드의 다른 필드 값을 설정 하거나 읽으면 ADO는 첫 번째 필드에서 데이터를 검색 하는 것으로 가정 합니다. 첫 번째 필드에서 **GetChunk** 메서드를 다시 호출 하는 경우 ADO는 호출을 새 **GetChunk** 작업으로 해석 하 고 데이터의 시작 부분에서 읽기를 시작 합니다. 첫 번째 **레코드 집합** 개체의 클론이 아닌 다른 [레코드 집합](./recordset-object-ado.md) 개체의 필드에 액세스 하면 **GetChunk** 작업이 중단 되지 않습니다.  
  
 **Field** 개체의 [Attributes](./attributes-property-ado.md) 속성에서 **Adfldlong** 비트가 **True**로 설정 된 경우 해당 필드에 대해 **GetChunk** 메서드를 사용할 수 있습니다.  
  
 **필드** 개체에서 **GetChunk** 메서드를 사용할 때 현재 레코드가 없으면 오류 3021 (현재 레코드 없음)이 발생 합니다.  
  
> [!NOTE]
>  **GetChunk** 메서드는 [Record](./record-object-ado.md) 개체의 **필드** 개체에 대해 작동 하지 않습니다. 작업을 수행 하지 않으며 런타임 오류를 생성 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](./field-object.md)  
  
## <a name="see-also"></a>참고 항목  
 [AppendChunk 및 GetChunk 메서드 예제 (VB)](./appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 및 GetChunk 메서드 예제 (VC + +)](./appendchunk-and-getchunk-methods-example-vc.md)   
 [AppendChunk 메서드 (ADO)](./appendchunk-method-ado.md)   
 [Attributes 속성(ADO)](./attributes-property-ado.md)