---
title: "AppendChunk 메서드 (ADO) | Microsoft Docs"
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
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords:
- AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 32430fd62de54adfba22af5d3ea5447a70fd75a7
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="appendchunk-method-ado"></a>AppendChunk 메서드 (ADO)
데이터는 큰 텍스트 또는 이진 데이터를 추가 [필드](../../../ado/reference/ado-api/field-object.md), 또는 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>매개 변수  
 *개체*  
 A **필드** 또는 **매개 변수** 개체입니다.  
  
 *데이터*  
 A **Variant** 개체에 추가할 데이터를 포함 하 합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **AppendChunk** 에서 메서드는 **필드** 또는 **매개 변수** 긴 이진 또는 문자 데이터로 채울 개체입니다. 시스템 메모리가 제한 된 상황에서 사용할 수 있습니다는 **AppendChunk** 메서드 긴 값으로 아니라 전체에서를 합니다.  
  
## <a name="field"></a>필드  
 경우는 **adFldLong** 비트는 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 속성의는 **필드** 개체로 설정 되어 **true**, 사용할 수 있습니다는  **AppendChunk** 해당 필드에 대 한 메서드.  
  
 첫 번째 **AppendChunk** 에서 호출 된 **필드** 기존 데이터 덮어쓰기 개체 필드를 데이터를 씁니다. 후속 **AppendChunk** 호출 기존 데이터에 추가 합니다. 한 필드를 데이터를 추가 하 고 다음을 설정 하거나 현재 레코드의 다른 필드의 값을 읽을 경우 ADO 완료 데이터 첫 번째 필드를 추가 한다고 가정 합니다. 호출 하는 경우는 **AppendChunk** 첫 번째 필드에 다시 ADO 1 보다 크거나 새 호출 **AppendChunk** 작업 하 고 기존 데이터를 덮어씁니다. 다른 필드에 액세스 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 첫 번째 복제본 없는 개체가 **레코드 집합** 개체에 영향을 주지 **AppendChunk** 작업 합니다.  
  
 호출 하는 경우 현재 레코드가 없는 경우 **AppendChunk** 에 **필드** 개체, 오류가 발생 합니다.  
  
> [!NOTE]
>  **AppendChunk** 메서드에서 작동 하지 않습니다 **필드** 의 개체는 [레코드 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md) 개체입니다. 아무 작업도 수행 하지 않는 하 고 실행 시 오류가 발생 합니다.  
  
## <a name="parameter"></a>매개 변수  
 경우는 **adParamLong** 비트는 **특성** 속성의는 **매개 변수** 개체로 설정 되어 **true**, 사용할 수 있습니다는  **AppendChunk** 메서드의 해당 매개 변수에 대해 합니다.  
  
 첫 번째 **AppendChunk** 에서 호출 된 **매개 변수** 기존 데이터 덮어쓰기 개체는 매개 변수를 데이터를 씁니다. 후속 **AppendChunk** 에서 호출 된 **매개 변수** 개체 매개 변수는 기존 데이터를 추가 합니다. **AppendChunk** null 값을 전달 하는 호출의 모든 매개 변수 데이터를 삭제 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Field 개체](../../../ado/reference/ado-api/field-object.md)|[Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [AppendChunk 및 GetChunk 메서드 예제 (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 및 GetChunk 방법 예 (VC + +)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [특성 속성 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [GetChunk 메서드(ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
