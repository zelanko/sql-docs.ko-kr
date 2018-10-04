---
title: AppendChunk 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords:
- AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ac0174a223571e29973ad854f9350a6e60f1de9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812001"
---
# <a name="appendchunk-method-ado"></a>AppendChunk 메서드(ADO)
큰 텍스트 또는 이진 데이터에 데이터 추가 [필드](../../../ado/reference/ado-api/field-object.md), 또는 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>매개 변수  
 *object*  
 A **필드** 하거나 **매개 변수** 개체입니다.  
  
 *데이터*  
 A **Variant** 개체에 추가할 데이터를 포함 하는 합니다.  
  
## <a name="remarks"></a>Remarks  
 사용 합니다 **AppendChunk** 메서드를 **필드** 또는 **매개 변수** 긴 이진 또는 문자 데이터로 채울 개체입니다. 시스템 메모리가 제한 된 상황에서 사용할 수 있습니다 합니다 **AppendChunk** 부분에서 아니라 온전히에서 long 값을 조작 하는 방법입니다.  
  
## <a name="field"></a>필드  
 경우는 **adFldLong** 비트를 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성을 **필드** 개체로 설정 됩니다 **true**, 사용할 수는  **AppendChunk** 해당 필드에 대 한 메서드.  
  
 첫 번째 **AppendChunk** 호출을 **필드** 모든 기존 데이터를 덮어쓰지 개체 필드 데이터를 씁니다. 후속 **AppendChunk** 호출 기존 데이터를 추가 합니다. 하나의 필드에 데이터를 추가 하 고 설정 하거나 현재 레코드의 다른 필드의 값을 읽은 다음, ADO는 완성 된 데이터의 첫 번째 필드를 추가 한다고 가정 합니다. 호출 하는 경우는 **AppendChunk** 새 호출을 해석 하는 첫 번째 필드에 다시 ADO 메서드 **AppendChunk** 작업 하 고 기존 데이터를 덮어씁니다. 다른 필드에 액세스할 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) 첫 번째 복제 되지 않은 개체 **레코드 집합** 개체에 영향을 주지 **AppendChunk** 작업 합니다.  
  
 호출할 때 현재 레코드가 없는 경우 **AppendChunk** 에 **필드** 개체에 오류가 발생 합니다.  
  
> [!NOTE]
>  합니다 **AppendChunk** 메서드에서 작동 하지 않습니다 **필드** 개체를 [레코드 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md) 개체입니다. 아무 작업도 수행 하지 않습니다 하 고 런타임 오류를 생성 합니다.  
  
## <a name="parameter"></a>매개 변수  
 경우는 **adParamLong** 비트를 **특성** 속성을 **매개 변수** 개체로 설정 됩니다 **true**, 사용할 수는  **AppendChunk** 메서드의 해당 매개 변수에 대해 합니다.  
  
 첫 번째 **AppendChunk** 호출을 **매개 변수** 모든 기존 데이터를 덮어쓰지 개체 매개 변수에 데이터를 씁니다. 후속 **AppendChunk** 에서 호출을 **매개 변수** 개체 매개 변수는 기존 데이터를 추가 합니다. **AppendChunk** null 값을 전달 하는 호출 매개 변수 데이터를 모두 삭제 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Field 개체](../../../ado/reference/ado-api/field-object.md)|[Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>관련 항목  
 [AppendChunk 및 GetChunk 메서드 예제 (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 및 GetChunk 메서드 예제 (VC + +)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Attributes 속성 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [GetChunk 메서드(ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
