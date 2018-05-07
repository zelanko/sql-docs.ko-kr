---
title: valueOf 메서드 (java.sql.Timestamp, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7320c383-0b06-446d-963b-7005e50324a2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2b742e3ccdf297aaa6ede4feb5bb93b04224823
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="valueof-method-javasqltimestamp-javautilcalendar"></a>valueOf 메서드(java.sql.Timestamp, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  만듭니다는 **DateTimeOffset** 지정 된 java.sql.Timestamp 값과 오프셋을 나타내는 java.util.Calendar 값 GMT에서 특정 오프셋의 시점을 나타내는 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, java.util.Calendar calendar)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *timestamp*  
  
 java.sql.Timestamp값입니다.  
  
 *달력*  
  
 오프셋 값입니다.  날짜 및 시간 구성 요소 *달력* 에 따라 설정할 수는 *타임 스탬프* 값입니다.  
  
## <a name="return-value"></a>반환 값  
 주어진된 java.util.Calendar 개체의 표준 시간대에 java.sql.Timestamp 개체에 의해 제공에서 된 시점을 나타내는 DateTimeOffset 개체를 반환 합니다.  
  
## <a name="remarks"></a>주의  
 이 메서드는 또한 java.sql.Timestamp 개체로 제공 지점 java.util.Calendar 개체를 설정 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  
