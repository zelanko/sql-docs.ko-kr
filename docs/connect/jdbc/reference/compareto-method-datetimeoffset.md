---
title: compareTo 메서드(DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04f19f08deda9cd42affa0a5ced28255c1bb521b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742931"
---
# <a name="compareto-method-datetimeoffset"></a>compareTo 메서드(DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  비교 **DateTimeOffset** 개체를 다른 **DateTimeOffset** GMT 시간을 기준으로 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int compareTo(DateTimeOffset other)  
```  
  
#### <a name="parameters"></a>매개 변수  
 현재 인스턴스와 비교할 [DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) 값입니다.  
  
## <a name="return-value"></a>반환 값  
 다음 표에서는 이 메서드의 반환 값에 대해 설명합니다.  
  
|반환 값|설명|  
|------------------|-----------------|  
|0|둘 다 **DateTimeOffset** 개체가 동일한 시각을 나타내는지 합니다.|  
|음수|이렇게 **DateTimeOffset** 개체가 앞에 있는 시간에는 시각을 나타내는지 *다른*합니다.|  
|양수|이렇게 **DateTimeOffset** 개체가 시간 후에 시각을 나타내는지 *다른*합니다.|  
  
## <a name="remarks"></a>Remarks  
 두 **DateTimeOffset** 개체가 GMT에서 동일한 시간을 갖고 있으면 오프셋에 따라 개체의 순서가 추가로 지정되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
