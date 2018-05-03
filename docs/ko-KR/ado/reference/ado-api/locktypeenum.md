---
title: LockTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- LockTypeEnum
helpviewer_keywords:
- LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba3e63dffbac818f9be074deef15f598b8905aa9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="locktypeenum"></a>LockTypeEnum
편집 중 레코드에 적용 되는 잠금 유형을 지정 합니다.  
  
|상수|Value|Description|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|낙관적 일괄 업데이트를 나타냅니다. 일괄 업데이트 모드에 필요합니다.|  
|**adLockOptimistic**|3|낙관적 잠금 레코드를 나타냅니다. 공급자 사용 낙관적 잠금 호출 하는 경우에 레코드 잠금는 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드.|  
|**adLockPessimistic**|2|레코드 별로 비관적 잠금을 나타냅니다. 공급자가 제대로 편집 하는 레코드의 일반적으로 데이터 소스에서 레코드를 편집한 후 즉시 잠금을 설정 하면 필요한 합니다.|  
|**adLockReadOnly**|1.|읽기 전용 레코드를 나타냅니다. 데이터를 변경할 수 없습니다.|  
|**adLockUnspecified**|-1|잠금 유형을 지정 하지 않습니다. 복제를 복제본에서 원본과 동일한 잠금 유형으로 만들어집니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
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
