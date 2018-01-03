---
title: LockTypeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: LockTypeEnum
helpviewer_keywords: LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 48c9909bf228a6bad0ad7e6d44415a1499fd5ea5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="locktypeenum"></a>LockTypeEnum
편집 중 레코드에 적용 되는 잠금 유형을 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|낙관적 일괄 업데이트를 나타냅니다. 일괄 업데이트 모드에 필요합니다.|  
|**adLockOptimistic**|3|낙관적 잠금 레코드를 나타냅니다. 공급자 사용 낙관적 잠금 호출 하는 경우에 레코드 잠금는 [업데이트](../../../ado/reference/ado-api/update-method.md) 메서드.|  
|**adLockPessimistic**|2|레코드 별로 비관적 잠금을 나타냅니다. 공급자가 제대로 편집 하는 레코드의 일반적으로 데이터 소스에서 레코드를 편집한 후 즉시 잠금을 설정 하면 필요한 합니다.|  
|**adLockReadOnly**|1|읽기 전용 레코드를 나타냅니다. 데이터를 변경할 수 없습니다.|  
|**adLockUnspecified**|-1|잠금 유형을 지정 하지 않습니다. 복제를 복제본에서 원본과 동일한 잠금 유형으로 만들어집니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
 패키지에 대 한 **com.ms.wfc.data**  
  
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
