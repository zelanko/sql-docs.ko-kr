---
title: "GetChunk 메서드 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::raw_GetChunk
- Field20::GetChunk
helpviewer_keywords:
- GetChunk method [ADO]
ms.assetid: fc268e22-205b-44a3-9038-ffed51e23e10
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b479146e26196e42836ce381e3f5e555dd0a9a6b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="getchunk-method-ado"></a>GetChunk 메서드 (ADO)
큰 텍스트 또는 이진 데이터의 내용 중 일부 또는 모두 반환 [필드](../../../ado/reference/ado-api/field-object.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>반환 값  
 반환 된 **Variant**합니다.  
  
#### <a name="parameters"></a>매개 변수  
 *크기*  
 A **긴** 검색할 문자 또는 바이트의 수와 같은 식입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **GetChunk** 에서 메서드는 **필드** 긴 이진 또는 문자 데이터의 일부 또는 전체를 검색 하는 개체입니다. 시스템 메모리가 제한 된 상황에서 사용할 수 있습니다는 **GetChunk** 메서드,으로 아니라 전체에서 긴 값을 조작 합니다.  
  
 데이터를 한 **GetChunk** 호출이 반환에 할당 된 *변수*합니다. 경우 *크기* 나머지 데이터를 보다 크면는 **GetChunk** 메서드 패딩 없이 나머지 데이터만 반환 *변수* 빈 공백을 사용 하 여 합니다. 필드가 비어 있으면는 **GetChunk** 메서드는 null 값을 반환 합니다.  
  
 각 후속 **GetChunk** 어디에서 시작 하는 데이터를 검색 하는 호출 이전 **GetChunk** 호출을 중단 합니다. 그러나 한 필드 및에서 다음을 설정 하거나 현재 레코드의 다른 필드의 값을 읽는 데이터를 검색 하는 경우 ADO 첫 번째 필드에서 데이터를 검색 했으면 가정 합니다. 호출 하는 경우는 **GetChunk** 첫 번째 필드에 다시 ADO 1 보다 크거나 새 호출 **GetChunk** 작업과 데이터의 시작 부분에서 읽기 시작 합니다. 다른 필드에 액세스 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 첫 번째 복제본 없는 개체가 **레코드 집합** 개체에 영향을 주지 **GetChunk** 작업 합니다.  
  
 경우는 **adFldLong** 비트는 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성의는 **필드** 개체로 설정 되어 **True**, 사용할 수 있습니다는 **GetChunk**  해당 필드에 대 한 메서드.  
  
 사용 하는 경우 현재 레코드가 없는 경우는 **GetChunk** 에서 메서드는 **필드** 개체 3021 (현재 레코드 없음) 오류가 발생 합니다.  
  
> [!NOTE]
>  **GetChunk** 메서드에서 작동 하지 않습니다 **필드** 의 개체는 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체입니다. 아무 작업도 수행 하지 않는 하 고 실행 시 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>관련 항목:  
 [AppendChunk 및 GetChunk 메서드 예제 (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 및 GetChunk 방법 예 (VC + +)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [AppendChunk 메서드 (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Attributes 속성(ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
