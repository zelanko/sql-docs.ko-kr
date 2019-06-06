---
title: Status 속성 (ADO 레코드 집합) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetStatus
- Recordset15::Status
helpviewer_keywords:
- Status property [ADO Recordset]
ms.assetid: 41d70d89-880f-4850-9d17-19d9790cc8eb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d57767cb50382f676aec2e11eaef77a8cdab9a87
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711002"
---
# <a name="status-property-ado-recordset"></a>Status 속성(ADO 레코드 집합)
일괄 처리 업데이트와 관련 하 여 현재 레코드 또는 다른 대량 작업의 상태를 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 하나 이상의 합계를 반환 합니다 [RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md) 값입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **상태** 보류 중인 변경 내용을 확인 하려면 속성 일괄 처리 업데이트 하는 동안 수정 된 레코드입니다. 사용할 수도 있습니다는 **상태** 속성을 호출 하는 경우와 같은 대량 작업 중 오류가 발생 한 레코드의 상태를 확인 합니다 [다시 동기화](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 메서드를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체를 가져오거나 설정 합니다 [필터](../../../ado/reference/ado-api/filter-property.md) 속성을를 **레코드 집합** 책갈피의 배열 개체입니다. 이 속성을 사용 하 여 지정된 된 레코드 못했으며 적절 하 게 해결 하는 방법을 확인할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Status 속성 예제 (레코드 집합) (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Status 속성 예제(VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
