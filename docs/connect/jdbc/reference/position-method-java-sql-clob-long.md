---
title: "position 메서드 (java.sql.Clob, long) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerClob.position (java.sql.Clob, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2fb34d5-1d34-4764-a795-712d9c6aa313
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9dc0e364f962206b701fd00219f0f6eb7b46a849
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="position-method-javasqlclob-long"></a>position 메서드(java.sql.Clob, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 시작 위치에 따라 CLOB에서 지정된 CLOB 개체가 있는 문자 위치를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public long position(java.sql.Clob searchstr,  
                     long start)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *searchstr*  
  
 검색할 부분 문자열입니다.  
  
 *시작*  
  
 검색을 시작할 위치입니다. 첫 번째 위치는 1입니다.  
  
## <a name="return-value"></a>반환 값  
 부분 문자열이 나타나는 위치이며, 부분 문자열이 없으면 -1입니다. 첫 번째 위치는 1입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 위치 메서드는 java.sql.Clob 인터페이스의 위치 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [방법 &#40; 배치 SQLServerClob &#41;](../../../connect/jdbc/reference/position-method-sqlserverclob.md)   
 [SQLServerClob 메서드](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 멤버](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 클래스](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  

