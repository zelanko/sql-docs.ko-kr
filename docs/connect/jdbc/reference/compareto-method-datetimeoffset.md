---
title: compareTo 메서드 (DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e2953d21306cf69582e2744c4fb96e13e0098d6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32829428"
---
# <a name="compareto-method-datetimeoffset"></a>compareTo 메서드(DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  비교 하 여 **DateTimeOffset** 개체를 다른 **DateTimeOffset** GMT 시간을 기반으로 하는 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>매개 변수  
 A [DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) 가 현재 인스턴스와 비교할 값입니다.  
  
## <a name="return-value"></a>반환 값  
 다음 표에서는 이 메서드의 반환 값에 대해 설명합니다.  
  
|반환 값|Description|  
|------------------|-----------------|  
|0|둘 다 **DateTimeOffset** 개체 시간에 동일한 시점을 나타냅니다.|  
|음수|이 **DateTimeOffset** 개체 앞에 있는 시간 점을 나타내는 *다른*합니다.|  
|양수|이 **DateTimeOffset** 개체가 나타냅니다는 지점 뒤에 있는 *다른*합니다.|  
  
## <a name="remarks"></a>주의  
 두 개의 **DateTimeOffset** GMT에서 시간이 동일한 개체, 오프셋에 따라 개체의 순서가 추가로 있지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
