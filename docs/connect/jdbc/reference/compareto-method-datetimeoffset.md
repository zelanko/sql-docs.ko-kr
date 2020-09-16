---
description: compareTo 메서드(DateTimeOffset)
title: compareTo 메서드(DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e4cf2ea4-0fe9-40ce-ba79-f2a2b616997e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d4673597255819521bc5becf48a92908ea1330a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438005"
---
# <a name="compareto-method-datetimeoffset"></a>compareTo 메서드(DateTimeOffset)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 **DateTimeOffset** 개체를 GMT의 시간을 기준으로 다른 **DateTimeOffset** 개체와 비교합니다.  
  
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
|0|**DateTimeOffset** 개체가 둘 다 동일한 시점을 나타냅니다.|  
|음수|이 **DateTimeOffset** 개체는 ‘다른’ 시점 이전 시점을 나타냅니다.**|  
|양수|이 **DateTimeOffset** 개체는 ‘다른’ 시점 이후 시점을 나타냅니다.**|  
  
## <a name="remarks"></a>설명  
 두 **DateTimeOffset** 개체가 GMT에서 동일한 시간을 갖고 있으면 오프셋에 따라 개체의 순서가 추가로 지정되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
