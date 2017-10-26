---
title: "valueOf 메서드 (java.sql.Timestamp, int) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 114f55af-62ab-4c60-8724-0affbbbbbcdc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b5bd8228a590f165b9df5df8dcc76798dea81e43
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="valueof-method-javasqltimestamp-int"></a>valueOf 메서드(java.sql.Timestamp, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  만듭니다는 **DateTimeOffset** 지정 된 java.sql.Timestamp 값과 분 단위 오프셋을 나타내는 값을 GMT에서 특정 오프셋의 시점을 나타내는 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public static DateTimeOffset valueOf(java.sql.Timestamp timestamp, int minutesOffset)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *timestamp*  
  
 java.sql.Timestamp값입니다.  
  
 *minutesOffset*  
  
 분 단위 오프셋입니다.  
  
## <a name="return-value"></a>반환 값  
 에 지정 된 시간이 지정 된 오프셋 위치 java.sql.Timestamp 개체로 분 GMT에서는 시점을 나타내는 DateTimeOffset 개체를 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md)   
 [DateTimeOffset 멤버](../../../connect/jdbc/reference/datetimeoffset-members.md)  
  
  

