---
title: LockTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- LockTypeEnum
helpviewer_keywords:
- LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bcd2e4d2a3b84ef913954c1a1a2d7fa76393040c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864076"
---
# <a name="locktypeenum"></a>LockTypeEnum
편집 하는 동안 기록에 배치 하는 잠금 유형을 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|낙관적 일괄 처리 업데이트를 나타냅니다. 일괄 업데이트 모드에 필요합니다.|  
|**adLockOptimistic**|3|낙관적 잠금, 레코드를 나타냅니다. 공급자를 사용 하 여 낙관적 잠금 호출 하는 경우에 레코드 잠금 합니다 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드.|  
|**adLockPessimistic**|2|비관적 잠금, 레코드를 나타냅니다. 공급자가 제대로 편집 하는 레코드의 일반적으로 편집한 후에 바로 데이터 원본에서 레코드를 잠그는 방식으로 필요한 것입니다.|  
|**adLockReadOnly**|1|읽기 전용으로 레코드를 나타냅니다. 데이터를 변경할 수 없습니다.|  
|**adLockUnspecified**|-1|잠금의 종류를 지정 하지 않습니다. 복제본, 복제본에서 원본과 동일한 잠금 유형으로 만들어집니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums.LockType.OPTIMISTIC|  
|AdoEnums.LockType.PESSIMISTIC|  
|AdoEnums.LockType.READONLY|  
|AdoEnums.LockType.UNSPECIFIED|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Clone 메서드(ADO)](../../../ado/reference/ado-api/clone-method-ado.md)|[LockType 속성(ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)|  
|[Open 메서드(ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[WillExecute 이벤트(ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|
