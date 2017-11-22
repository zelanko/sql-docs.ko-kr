---
title: "Status 속성 (ADO 레코드 집합) | Microsoft Docs"
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
f1_keywords:
- Recordset15::GetStatus
- Recordset15::Status
helpviewer_keywords: Status property [ADO Recordset]
ms.assetid: 41d70d89-880f-4850-9d17-19d9790cc8eb
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0005de0669a2dd68622c2e81c9f7b3be2f912da1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="status-property-ado-recordset"></a>Status 속성 (ADO 레코드 집합)
일괄 처리 업데이트에 대해 현재 레코드 또는 다른 대량 작업의 상태를 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 하나 이상의의 합을 반환 [RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md) 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **상태** 보류 중인 변경 내용을 확인 하려면 속성 일괄 처리 업데이트 중 수정 된 레코드입니다. 사용할 수도 있습니다는 **상태** 속성을 호출 하는 경우와 같은 대량 작업 중 실패 하는 레코드의 상태를 볼는 [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), 또는 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 에 대 한 메서드는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) , 개체 또는 설정는 [필터](../../../ado/reference/ado-api/filter-property.md) 속성에는 **레코드 집합** 개체 책갈피의 배열입니다. 이 속성 지정된 된 레코드가 실패 하 및 그에 따라 해결 하는 방법을 결정할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [상태 속성 예제 (레코드 집합) (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Status 속성 예제(VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
