---
description: LockTypeEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ba912f082cbd621d2d2205c6505e8c2be309bec
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774552"
---
# <a name="locktypeenum"></a>LockTypeEnum
편집 하는 동안 레코드에 적용 되는 잠금 유형을 지정 합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|낙관적 일괄 처리 업데이트를 나타냅니다. 일괄 업데이트 모드에 필요 합니다.|  
|**adLockOptimistic**|3|낙관적 잠금, 레코드 별로 기록을 나타냅니다. 공급자는 낙관적 잠금을 사용 하 고 [Update](./update-method.md) 메서드를 호출 하는 경우에만 레코드를 잠급니다.|  
|**adLockPessimistic**|2|비관적 잠금, 레코드 별로 기록 함을 나타냅니다. 공급자는 일반적으로 편집 후 즉시 데이터 원본에서 레코드를 잠가 레코드를 성공적으로 편집 하는 데 필요한 작업을 수행 합니다.|  
|**adLockReadOnly**|1|읽기 전용 레코드를 나타냅니다. 데이터를 변경할 수 없습니다.|  
|**adLockUnspecified 되지 않음**|-1|가 잠금 유형을 지정 하지 않습니다. 클론의 경우 원래와 동일한 잠금 유형으로 클론을 만듭니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [Clone 메서드(ADO)](./clone-method-ado.md)  
        [LockType 속성(ADO)](./locktype-property-ado.md)  
    :::column-end:::
    :::column:::
        [Open 메서드(ADO 레코드 집합)](./open-method-ado-recordset.md)  
        [WillExecute 이벤트(ADO)](./willexecute-event-ado.md)  
    :::column-end:::
:::row-end:::