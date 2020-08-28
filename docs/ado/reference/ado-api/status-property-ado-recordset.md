---
description: Status 속성(ADO 레코드 집합)
title: Status 속성 (ADO 레코드 집합) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 546fc85e2f6fc2753b85a055f597b3d39129dd61
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988714"
---
# <a name="status-property-ado-recordset"></a>Status 속성(ADO 레코드 집합)
일괄 업데이트 또는 기타 대량 작업과 관련 하 여 현재 레코드의 상태를 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 하나 이상의 [Recordstatusenum](./recordstatusenum.md) 값의 합을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **상태** 속성을 사용 하 여 일괄 처리를 업데이트 하는 동안 수정 된 레코드에 대해 보류 중인 변경 내용을 확인 합니다. 또한 **Status** 속성을 사용 하 여 [레코드 집합](./recordset-object-ado.md) 개체에 대해 [Resync](./resync-method.md), [UpdateBatch](./updatebatch-method.md)또는 [CancelBatch](./cancelbatch-method-ado.md) 메서드를 호출 하거나 **레코드 집합** 개체에 대 한 [필터](./filter-property.md) 속성을 책갈피 배열로 설정 하는 경우와 같이 대량 작업 중에 실패 하는 레코드의 상태를 볼 수 있습니다. 이 속성을 사용 하 여 지정 된 레코드가 실패 한 방법을 확인 하 고 그에 따라 해결할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Status 속성 예제 (레코드 집합) (VB)](./status-property-example-recordset-vb.md)   
 [Status 속성 예제(VC++)](./status-property-example-vc.md)