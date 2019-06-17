---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c5dc09043d780c2a743059773eed56e16a799bf5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66694945"
---
# <a name="getchunk-method-ado"></a>GetChunk 메서드(ADO)
큰 텍스트 또는 이진 데이터의 내용 중 일부 또는 모두 반환 [필드](../../../ado/reference/ado-api/field-object.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 **Variant**합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *크기*  
 A **긴** 검색 하려는 문자 또는 바이트의 수와 같은 식입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 하 여 합니다 **GetChunk** 메서드를 **필드** 긴 이진 또는 문자 데이터의 일부 또는 전체를 검색할 개체입니다. 시스템 메모리가 제한 된 상황에서 사용할 수 있습니다 합니다 **GetChunk** 부분을 대신 전체적으로 긴 값을 조작 하는 방법입니다.  
  
 데이터는 한 **GetChunk** 호출 반환에 할당 된 *변수*합니다. 하는 경우 *크기* 나머지 데이터를 보다는 **GetChunk** 메서드 패딩 나머지 데이터만 반환 *변수* 빈 공간을 사용 하 여 합니다. 필드가 비어 있으면 합니다 **GetChunk** 메서드는 null 값을 반환 합니다.  
  
 각 후속 **GetChunk** 위치에서 시작 하는 데이터를 검색 하는 호출 이전 **GetChunk** 호출을 중단 합니다. 그러나 하나의 필드를 설정 하거나 현재 레코드의 다른 필드의 값을 읽을에서 데이터를 검색 하는 경우 ADO 첫 번째 필드에서 데이터를 검색 하는 것이 마친 가정 합니다. 호출 하는 경우는 **GetChunk** 새 호출을 해석 하는 첫 번째 필드에 다시 ADO 메서드 **GetChunk** 작업 및 데이터의 시작 부분에서 읽기 시작 합니다. 다른 필드에 액세스할 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) 첫 번째 복제 되지 않은 개체 **레코드 집합** 개체에 영향을 주지 **GetChunk** 작업 합니다.  
  
 경우는 **adFldLong** 비트를 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성을 **필드** 개체로 설정 됩니다 **True**, 사용할 수는 **GetChunk**  해당 필드에 대 한 메서드.  
  
 사용 하는 경우 현재 레코드가 없는 경우는 **GetChunk** 메서드를 **필드** 개체 3021 (현재 레코드 없음) 오류가 발생 합니다.  
  
> [!NOTE]
>  합니다 **GetChunk** 메서드에서 작동 하지 않습니다 **필드** 개체를 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체입니다. 아무 작업도 수행 하지 않습니다 하 고 런타임 오류를 생성 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>관련 항목  
 [AppendChunk 및 GetChunk 메서드 예제 (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 및 GetChunk 메서드 예제 (VC + +)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [AppendChunk 메서드 (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Attributes 속성(ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
